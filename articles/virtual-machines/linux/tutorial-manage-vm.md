---
title: "aaaCreate 和管理 Linux Vm hello Azure CLI |Microsoft 文件"
description: "教學課程-建立和管理 Linux Vm 與 hello Azure CLI"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a>建立和管理 Linux Vm 與 hello Azure CLI

Azure 虛擬機器提供完全可設定且彈性的計算環境。 本教學課程涵蓋基本的「Azure 虛擬機器」部署項目，例如選取 VM 大小、選取 VM 映像、部署 VM。 您會了解如何：

> [!div class="checklist"]
> * 建立和連線 tooa VM
> * 選取及使用 VM 映像
> * 檢視及使用特定 VM 大小
> * 調整 VM 的大小
> * 檢視及了解 VM 狀態


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="create-resource-group"></a>建立資源群組

建立資源群組以 hello [az 群組建立](https://docs.microsoft.com/cli/azure/group#create)命令。 

Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 資源群組必須在虛擬機器之前建立。 在此範例中，資源群組命名為*myResourceGroupVM*會建立在 hello *eastus*區域。 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

建立或修改 VM，能看到本教學課程時，所指定 hello 資源群組。

## <a name="create-virtual-machine"></a>Create virtual machine

建立虛擬機器以 hello [az vm 建立](https://docs.microsoft.com/cli/azure/vm#create)命令。 

建立虛擬機器時，有數個可用的選項，例如作業系統映像、磁碟大小及系統管理認證。 在此範例中，是使用 myVM 名稱來建立執行 Ubuntu Server 的虛擬機器。 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

一次在建立 VM 的 hello，hello Azure CLI 輸出 hello VM 的相關資訊。 記下 hello `publicIpAddress`，此位址可以是使用的 tooaccess hello 虛擬機器... 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a>連接 tooVM

您現在可以連接 toohello VM 使用 SSH。 Hello 範例 IP 位址取代成 hello `publicIpAddress` hello 上一個步驟中所述。

```bash
ssh 52.174.34.95
```

一旦完成以 hello VM，請關閉 hello SSH 工作階段。 

```bash
exit
```

## <a name="understand-vm-images"></a>了解 VM 映像

hello Azure marketplace 包括許多可以使用的 toocreate Vm 的映像。 在 hello 先前步驟中，已使用 Ubuntu 映像建立虛擬機器。 在此步驟中，hello Azure CLI 會使用的 toosearch hello marketplace 中的一個 CentOS 映像，就會使用 toodeploy 第二個虛擬機器。  

一份 hello toosee 最常使用的映像，請使用 hello [az vm 映像清單](/cli/azure/vm/image#list)命令。

```azurecli-interactive 
az vm image list --output table
```

hello 命令輸出傳回 hello 最受歡迎的 VM 映像，在 Azure 上。

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

無法看到完整清單，請加入 hello`--all`引數。 hello 影像清單也可以篩選由`--publisher`或`–-offer`。 在此範例中，篩選與符合方案的所有映像 hello 清單*CentOS*。 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

部分輸出：

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

使用特定的映像的 VM toodeploy 記 hello 值中 hello *Urn*資料行。 當指定 hello 映像，hello 映像的版本號碼可以被取代 「 最新 」，以選取 hello hello 分配的最新的版本。 在此範例中，hello`--image`引數是使用的 toospecify hello 最新版本的 CentOS 6.5 映像。  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a>了解 VM 大小

虛擬機器大小會決定 hello 量，例如 CPU、 GPU，以及記憶體都會提供 toohello 虛擬機器的計算資源。 虛擬機器必須 toobe hello 預期工作負載的適當調整大小。 如果工作負載增加，可以調整現有虛擬機器的大小。

### <a name="vm-sizes"></a>VM 大小

下表中的 hello 將大小分類成使用案例。  

| 類型                     | 大小           |    說明       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [一般用途](sizes-general.md)         |Dsv3、Dv3、DSv2、Dv2、DS、D、Av2、A0-7| 平衡的 CPU 對記憶體。 適用於開發 / 測試及小型 toomedium 應用程式和資料解決方案。  |
| [計算最佳化](sizes-compute.md)   | Fs、F             | CPU 與記憶體的比例高。 適用於中流量應用程式、網路設備，以及批次處理。        |
| [記憶體最佳化](../virtual-machines-windows-sizes-memory.md)    | Esv3、Ev3、M、GS、G、DSv2、DS、Dv2、D   | 記憶體與核心的比例高。 太棒了關聯式資料庫、 中度 toolarge 快取，以及記憶體中分析。                 |
| [儲存體最佳化](../virtual-machines-windows-sizes-storage.md)      | Ls                | 高磁碟輸送量及 IO。 適用於巨量資料、SQL 及 NoSQL 資料庫。                                                         |
| [GPU](sizes-gpu.md)          | NV、NC            | 以大量圖形轉譯和視訊編輯為目標的特製化 VM。       |
| [高效能](sizes-hpc.md) | H、A8-11          | 我們的最強大 CPU VM，可搭配選用的高輸送量網路介面 (RDMA)。 


### <a name="find-available-vm-sizes"></a>尋找可用的 VM 大小

在特定區域大小可用 toosee VM 的清單，請使用 hello [az vm 清單大小](/cli/azure/vm#list-sizes)命令。 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

部分輸出：

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a>建立特定大小的 VM

在 hello 先前 VM 建立範例中，大小未提供，而這可能導致預設大小。 VM 大小可以選取在建立階段使用[az vm 建立](/cli/azure/vm#create)和 hello`--size`引數。 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a>調整 VM 的大小

已部署 VM 之後，它可以是調整過大小的 tooincrease 或減少資源配置。

調整 VM 大小時之前, 檢查是否 hello 所需的大小在 hello 目前 Azure 叢集上使用。 hello [az vm 清單-vm-調整大小的選項](/cli/azure/vm#list-vm-resize-options)命令傳回 hello 大小清單。 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
如果 hello 所需的大小是可用，hello VM 可以調整大小，從開機的狀態，不過 hello 作業期間重新開機。 使用 hello [az vm 調整]( /cli/azure/vm#resize)命令 tooperform hello 調整大小。

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

如果 hello 所需的大小不 hello 目前在叢集上，hello VM toobe hello 的調整大小作業之前取消配置可能會發生的需求。 使用 hello [az vm 解除配置]( /cli/azure/vm#deallocate)命令 toostop 及取消配置 hello VM。 請注意，當 hello VM 的電源已回復，可能會移除 hello 暫存磁碟上的任何資料。 hello 公用 IP 位址也會變更除非正在使用的靜態 IP 位址。 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

一旦取消配置，可能會發生 hello 調整大小。 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

Hello 調整大小之後，就可以啟動 hello VM。

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a>VM 電源狀態

Azure VM 的電源狀態可以是許多電源狀態的其中一種。 此狀態表示 hello 目前 hello VM 的狀態從 hello hypervisor hello 觀點來看。 

### <a name="power-states"></a>電源狀態

| 電源狀態 | 說明
|----|----|
| 啟動中 | 指出正在啟動 hello 虛擬機器。 |
| 執行中 | 指出該 hello 虛擬機器正在執行。 |
| 停止中 | 表示正在停止該 hello 虛擬機器。 | 
| 已停止 | 表示該 hello 虛擬機器已停止。 在 hello 停止狀態的虛擬機器仍會產生計算費用。  |
| 正在解除配置 | 表示已解除配置該 hello 虛擬機器。 |
| 已解除配置 | 表示該 hello 虛擬機器移除從 hello hypervisor 但 hello 控制平面中仍然可用。 Hello 取消配置狀態中的虛擬機器不會產生計算費用。 |
| - | 表示 hello hello 虛擬機器的電源狀態不明。 |

### <a name="find-power-state"></a>尋找電源狀態

特定的 VM，使用 hello tooretrieve hello 狀態[az vm 取得執行個體檢視](/cli/azure/vm#get-instance-view)命令。 為確定 toospecify 虛擬機器與資源群組的有效名稱。 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

輸出：

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a>管理工作

在 hello 生命週期的虛擬機器，您可能想 toorun 管理工作，例如啟動、 停止或刪除虛擬機器。 此外，您可能想 toocreate 指令碼 tooautomate 重複或複雜工作。 使用 Azure CLI hello，許多常見的管理工作可以執行從 hello 命令列或指令碼中。 

### <a name="get-ip-address"></a>取得 IP 位址

此命令會傳回虛擬機器的 hello 私人和公用 IP 位址。  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a>停止虛擬機器

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a>啟動虛擬機器

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a>刪除資源群組

刪除資源群組同時會刪除其內含的所有資源。

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解基本的 VM 建立和管理，像是如何：

> [!div class="checklist"]
> * 建立和連線 tooa VM
> * 選取及使用 VM 映像
> * 檢視及使用特定 VM 大小
> * 調整 VM 的大小
> * 檢視及了解 VM 狀態

前進 toohello 下一個教學課程的 toolearn 有關 VM 磁碟。  

> [!div class="nextstepaction"]
> [建立和管理 VM 磁碟](./tutorial-manage-disks.md)
