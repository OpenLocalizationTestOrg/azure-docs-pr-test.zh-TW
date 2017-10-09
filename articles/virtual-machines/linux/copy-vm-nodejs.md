---
title: "一份您的 Linux VM 以 hello Azure CLI 1.0 aaaCreate |Microsoft 文件"
description: "了解與您 Azure Linux 虛擬機器的複本 toocreate 如何 hello Azure CLI 1.0 hello Resource Manager 部署模型中"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a>建立 hello Azure CLI 1.0 使用在 Azure 上執行的 Linux 虛擬機器的複本
本文章將示範如何 toocreate 程式 Azure 虛擬機器 (VM) 執行 Linux，請使用一份 hello Resource Manager 部署模型。 第一次您已複製 hello 作業系統和資料磁碟 tooa 新的容器，然後設定 hello 網路資源並建立新虛擬機器 hello。

您也可以[上傳自訂磁碟映像並從這個映像建立 VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- Azure CLI 1.0 – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI

## <a name="before-you-begin"></a>開始之前
請確定您符合下列必要條件再啟動 hello 步驟 hello:

* 您已擁有 hello [Azure CLI](../../cli-install-nodejs.md)下載並安裝在您的電腦。 
* 您也需要現有 Azure Linux VM 的一些相關資訊：

| 來源 VM 資訊 | 其中 tooget 它 |
| --- | --- |
| VM 名稱 |`azure vm list` |
| 資源群組名稱 |`azure vm list` |
| 位置 |`azure vm list` |
| 儲存體帳戶名稱 |`azure storage account list -g <resourceGroup>` |
| 容器名稱 |`azure storage container list -a <sourcestorageaccountname>` |
| 來源 VM VHD 檔案名稱 |`azure storage blob list --container <containerName>` |

* 您將有關新的 VM 需要 toomake 一些選項：   <br> -容器名稱    <br> -VM 名稱    <br> -VM 大小    <br> -vNet 名稱    <br> -SubNet 名稱    <br> -IP 名稱    <br> -NIC 名稱

## <a name="login-and-set-your-subscription"></a>登入及設定您的訂用帳戶
1. 登入 toohello CLI。

    ```azurecli
    azure login
    ```
2. 確定您處於 Resource Manager 模式。

    ```azurecli
    azure config mode arm
    ```
3. 設定 hello 正確的訂用帳戶。 您可以使用 '的 azure 帳戶 list' toosee 您所有的訂閱。

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a>停止 hello VM
停止並取消配置 hello 來源 VM。 您可以使用 'azure vm list' tooget 所有 hello Vm 的清單中訂用帳戶及資源群組名稱。

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a>複製 hello VHD
您可以從 hello 來源儲存體 toohello 目的地使用 hello 複製 hello VHD `azure storage blob copy start`。 在此範例中，我們會 toocopy hello VHD toohello 相同的儲存體帳戶，但不同的容器。

在 hello toocopy hello VHD tooanother 容器相同的儲存體帳戶中，輸入：

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a>新的 vm 設定 hello 虛擬網路
為新 VM 設定虛擬網路和 NIC。 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a>建立 hello 新的 VM
您現在可以從已上傳虛擬硬碟建立 VM[使用資源管理員範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd)或藉由指定 hello URI tooyour CLI hello 透過輸入複製磁碟：

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a>後續步驟
toolearn 如何 toouse Azure CLI toomanage 新的虛擬機器，請參閱[hello Azure 資源管理員的 Azure CLI 命令](../azure-cli-arm-commands.md)。

