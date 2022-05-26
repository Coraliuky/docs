# Example of Training on the Ascend NPU Version of PaddlePaddle

## Example of Training YOLOv3 

**Step 1**：Download and install PaddleDetection Suites

```bash
# Download the suite code
cd path_to_clone_PaddleDetection
git clone -b develop https://github.com/PaddlePaddle/PaddleDetection.git

# Compile and install the suites
cd PaddleDetection
python setup.py install

# Install other dependencies
pip install -r requirements.txt
```

You can also refer to PaddleDetection's [Github Repo](https://github.com/PaddlePaddle/PaddleDetection) to the source code of the develop branch.

**Step 2**：Prepare the VOC training datasets

```bash
cd PaddleDetection/static/dataset/roadsign_voc
python download_roadsign_voc.py

# After the download, the directory structure is: 
PaddleDetection/static/dataset/roadsign_voc/
├── annotations
├── download_roadsign_voc.py
├── images
├── label_list.txt
├── train.txt
└── valid.txt
```

**Step 3**：Perform single-card training

```bash
export FLAGS_selected_npus=0

# Single-card training
python -u tools/train.py -c configs/yolov3_darknet_roadsign.yml -o use_npu=True

# Single-card assessment
python -u tools/eval.py -c configs/yolov3_darknet_roadsign.yml -o use_npu=True

# Final precision
INFO:ppdet.utils.voc_eval:mAP(0.50, integral) = 76.78%
```

**Step 4**：Perform multi-card training

> Attention：You can refer to the next section here-- the preparation of "configuration of the NPU multi-card training".

```bash
# Configuration of the NPU multi-card training
export FLAGS_selected_npus=0,1,2,3
export RANK_TABLE_FILE=/root/hccl_4p_0123_127.0.0.1.json

# Setting of relevant environment variables of HCCL 
export HCCL_CONNECT_TIMEOUT=7200
export HCCL_WHITELIST_DISABLE=1
export HCCL_SECURITY_MODE=1

# Multi-card training
python -m paddle.distributed.fleet.launch --run_mode=collective \
       tools/train.py -c configs/yolov3_darknet_roadsign.yml -o use_npu=True

# Training result assessment
python -u tools/eval.py -c configs/yolov3_darknet_roadsign.yml -o use_npu=True

# Final precision
INFO:ppdet.utils.voc_eval:mAP(0.50, integral) = 83.00%
```

## Configuration of the NPU Multi-Card Training

**Prerequisite**：Deploy and Configure the NPU runtime environment according to Huawei Ascend 910 NPU's [Configuring the IP of device network cards](https://support.huaweicloud.com/instg-cli-cann502-alpha005/atlasdeploy_03_0105.html). Then, check whether there is a `/etc/hccn.conf` doc in the device.

If it is a physical machine environment, follow the [hccl_tools description document](https://github.com/mindspore-ai/mindspore/tree/v1.4.0/model_zoo/utils/hccl_tools) on the official website of Huawei. If it is a container environemnt run by the Paddle official docker image，follow this guide:

**Step 1**：Create the `/etc/hccn.conf` file in the container according to the ID of the device it maps when it starts. 

For example, the content of `/etc/hccn.conf` of the card numbered 8 on the physical machine is: 

```
address_0=192.168.10.21
netmask_0=255.255.255.0
address_1=192.168.20.21
netmask_1=255.255.255.0
address_2=192.168.30.21
netmask_2=255.255.255.0
address_3=192.168.40.21
netmask_3=255.255.255.0
address_4=192.168.10.22
netmask_4=255.255.255.0
address_5=192.168.20.22
netmask_5=255.255.255.0
address_6=192.168.30.22
netmask_6=255.255.255.0
address_7=192.168.40.22
netmask_7=255.255.255.0
```

If the devices that the container maps at startup are four NPU cards numbered between 4 and 7, the content of `/etc/hccn.conf` is：

> Attention：Here, address_4 and netmask_4 should be modified to address_0 and netmask_0 respectively, and so on.

```
address_0=192.168.10.22
netmask_0=255.255.255.0
address_1=192.168.20.22
netmask_1=255.255.255.0
address_2=192.168.30.22
netmask_2=255.255.255.0
address_3=192.168.40.22
netmask_3=255.255.255.0
```

**Step 2**：Create the configuration file of the training with a single machine and four cards following the [hccl_tools description document](https://github.com/mindspore-ai/mindspore/tree/v1.4.0/model_zoo/utils/hccl_tools) on the official website of Huawei. 

```
# Download the file hccl_tools.py
wget https://raw.githubusercontent.com/mindspore-ai/mindspore/v1.4.0/model_zoo/utils/hccl_tools/hccl_tools.py

# Create the configuration file of the training with a single machine and two cards. The IP of the machine can be 127.0.0.1
python hccl_tools.py --device_num "[0,4)" --server_ip 127.0.0.1
```

After the successful operation, there will be a new file named  `hccl_4p_0123_127.0.0.1.json` stored in the current directory. Its content should be:

```json
{
    "version": "1.0",
    "server_count": "1",
    "server_list": [
        {
            "server_id": "127.0.0.1",
            "device": [
                {
                    "device_id": "0",
                    "device_ip": "192.168.10.22",
                    "rank_id": "0"
                },
                {
                    "device_id": "1",
                    "device_ip": "192.168.20.22",
                    "rank_id": "1"
                },
                {
                    "device_id": "2",
                    "device_ip": "192.168.30.22",
                    "rank_id": "2"
                },
                {
                    "device_id": "3",
                    "device_ip": "192.168.40.22",
                    "rank_id": "3"
                }
            ],
            "host_nic_ip": "reserve"
        }
    ],
    "status": "completed"
}
```

**Step 3**：Before performing the multi-card training of PaddlePaddle, configure the environment variable `RANK_TABLE_FILE` to point to the absolute path of the json file created in the previous step.

```bash
# 1) Configure the environment variable of the ranktable file
export RANK_TABLE_FILE=$(readlink -f hccl_4p_0123_127.0.0.1.json)
# Or modify to the absolute path of the json file
export RANK_TABLE_FILE=/root/hccl_4p_0123_127.0.0.1.json

# 2) Set environment variables of HCCL
export HCCL_CONNECT_TIMEOUT=7200
export HCCL_WHITELIST_DISABLE=1
export HCCL_SECURITY_MODE=1

# 3) Start the distributed tasks. You should know here the available run_mode only includes the collective mode. 
python -m paddle.distributed.fleet.launch --run_mode=collective train.py ...
```
