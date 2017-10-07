---
title: "aaaConvert Azure VM tooa 規模調整集合 |Microsoft 文件"
description: "建立並部署以 hello Azure CLI 設定 Linux 的 Azure 虛擬機器規模。"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a>轉換現有的 Azure 虛擬機器 tooa 規模集

本教學課程會示範如何 toouse Azure CLI 2.0 tooconvert 虛擬機器 tooa 虛擬機器規模集。 您也可以學習如何 tooautomate hello hello hello 小數位數中的虛擬機器的設定。 如需有關如何 tooinstall Azure CLI 2.0，請參閱[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md)。 如需調整集的詳細資訊，請參閱 [虛擬機器調整集](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)。

## <a name="step-1---deprovision-hello-vm"></a>步驟 1-取消佈建 VM hello

使用 SSH tooconnect toohello VM。

取消佈建 hello VM 使用 hello Azure VM 代理程式 toodelete 檔案和資料。 如需取消佈建的詳細概觀，請參閱[擷取 Linux 虛擬機器](capture-image.md)。

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a>步驟 2-擷取 hello VM 映像

如需擷取的詳細概觀，請參閱[擷取 Linux 虛擬機器](capture-image.md)。

解除配置 hello 與 VM [az vm 解除配置](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

一般化 hello 與 VM [az vm 一般化](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

建立映像從 hello VM 資源[az 映像建立](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a>步驟 3-建立 hello 規模集

取得 hello**識別碼**hello 映像。

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

使用 [az vmss create](/cli/azure/vmss#create) 從映像資源建立 VM：

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

此命令也會連結 10 GB 的資料磁碟。 請注意，根據 hello VM 所選大小 (我們使用**Standard_DS1_v2**)，允許的資料磁碟的 hello 數目會不同。 如需詳細資訊，請檢閱 hello[虛擬機器大小](sizes.md)。

一旦 hello 小數位數設定完成，則連接 tooit。 取得與 SSH hello 執行個體的 IP 位址清單[az vmss 清單執行個體的連接-資訊](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

現在您可以連線 toohello 虛擬機器執行個體 tooinitialize hello 資料磁碟

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a>步驟 4-初始化 hello 資料磁碟

同時連接的 toohello 虛擬機器，分割 hello 磁碟`fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

寫入檔案系統 toohello 磁碟分割以 hello`mkfs`命令：

```bash
sudo mkfs -t ext4 /dev/sdc1
```

掛接 hello 新磁碟，使其在 hello 作業系統中存取：

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

hello 磁碟現在可以存取透過 hello datadrive 掛接，您可以使用驗證`ls /datadrive/`。

結束 hello SSH 工作階段。


## <a name="step-5---configure-firewall"></a>步驟 5 - 設定防火牆

打孔 hello 防火牆 toohello hello 規模調整集合所裝載的 web 伺服器上一個洞。 Hello 規模集建立時，會一併建立負載平衡器，您可以使用它**SSH** toohello 個別的虛擬機器。 tooopen 連接埠，您需要兩項資訊，就可以使用 Azure CLI。

* **前端 IP 位址集區**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **後端 IP 位址集區**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

使用這兩個名稱，您可以開啟連接埠 **80**。

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>步驟 6 - 自動化組態

hello 資料磁碟需要 toobe 每個虛擬機器執行個體上設定。 我們可以自動化 hello hello hello 虛擬機器設定**CustomScript**延伸模組。

首先，建立*.sh*包含 hello 磁碟格式的命令的指令碼。

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

接下來上, 傳該指令碼檔案 toowhere hello **CustomScript**延伸模組可以存取它。 複本可以在[這裡](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4)取得。

建立名為本機檔案**settings.json**和 put hello 下列 JSON 區塊中。 hello`flieUris`屬性應該設定指令碼檔案上傳到 toowhere。

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

部署設定以 hello 這個命令 tooyour 標尺**CustomScript**延伸模組，參考 hello **settings.json**剛才所建立的檔案。

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

此擴充功能會在所有目前執行個體和稍後藉由調整所建立的任何執行個體上自動執行。

## <a name="step-7---configure-autoscale-rules"></a>步驟 7 - 設定自動調整規則

目前，Azure CLI 中無法設定自動調整規則。 使用 hello [Azure 入口網站](https://portal.azure.com)tooconfigure 自動調整規模。

## <a name="step-8---management-tasks"></a>步驟 8 - 管理工作

整個 hello 規模集的 hello 生命週期，您可能需要 toorun 一或多個管理工作。 此外，您可能會想 toocreate 指令碼自動化各種生命週期的工作，與 hello Azure CLI 提供快速的方式 toodo 這些工作。 以下是一些常見工作。

### <a name="get-connection-info"></a>取得連線資訊

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a>設定執行個體計數 (手動調整)

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a>刪除資源群組

刪除資源群組同時會刪除其內含的所有資源。

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>後續步驟
toolearn 一些 hello 虛擬機器擴展集功能引入在此教學課程中，請參閱下列資訊的 hello:

- [Azure 虛擬機器擴展集概觀](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Azure 負載平衡器概觀](../../load-balancer/load-balancer-overview.md)
- [使用網路安全性群組來控制網路流量](../../virtual-network/virtual-networks-nsg.md)