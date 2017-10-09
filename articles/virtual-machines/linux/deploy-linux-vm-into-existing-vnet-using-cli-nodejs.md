---
title: "aaaDeploy Linux Vm 到現有的網路與 Azure CLI 1.0 |Microsoft 文件"
description: "如何在現有的虛擬網路使用 Linux VM toodeploy hello Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a>如何在 Linux 虛擬機器，在現有的 Azure 虛擬網路以 hello Azure CLI 1.0 toodeploy

本文章將示範如何 toouse Azure CLI 1.0 toodeploy 到現有的虛擬網路 (VNet) 的虛擬機器 (VM)。 hello 需求如下：

- [一個 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)
- [SSH 公開金鑰和私密金鑰檔案](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -hello 資源管理部署模型我們下一個層代 CLI


## <a name="quick-commands"></a>快速命令

如果您需要 tooquickly 完成 hello 工作，下列區段的 hello 詳細資料所需的 hello 命令。 詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough)。

必要條件︰資源群組、VNet、具有 SSH 輸入的 NSG、子網路。 將任何範例換成您自己的設定。

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>部署 hello VM hello 虛擬網路基礎結構

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a>詳細的逐步解說

Azure 資產像是 hello Vnet 和網路安全性群組應為靜態和長時間存在很少部署的資源。 部署的 VNet 之後, 可以重複使用由沒有任何負面影響 toohello 基礎結構的新部署。 將 VNet 想成是傳統硬體網路交換器。 您不需要的 tooconfigure 全新的硬體交換器每一次部署。 具有正確設定 VNet，您可以繼續 toodeploy 新伺服器到該 VNet 反覆數，如果有的話，hello VNet hello 生命週期所需的變更。

## <a name="create-hello-resource-group"></a>建立 hello 資源群組

首先，建立資源群組 tooorganize 您在本逐步解說中建立的所有項目。 如需有關資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a>建立 hello VNet

hello 第一個步驟是的 toobuild VNet toolaunch hello 到 Vm。 hello VNet 包含此逐步解說中的一個子網路。 如需有關 Azure Vnet 的詳細資訊，請參閱[建立虛擬網路使用 Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a>建立 hello 網路安全性群組

hello 子網路建立現有的網路安全性群組背後因此建立 hello 之前 hello 子網路的網路安全性群組。 Azure 網路安全性群組是相等的 tooa hello 網路層級的防火牆。 如需有關 Azure 網路安全性群組的詳細資訊，請參閱[toocreate 網路安全性 hello Azure CLI 中群組的方式](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>新增輸入 SSH 允許規則

hello VM 需要的 hello 需要讓規則，允許輸入連接埠 22 流量 toobe 傳遞 hello 網路 tooport 22 hello VM 上的網際網路存取權。

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>新增子網路 toohello VNet

Hello VNet 必須位於子網路內的 Vm。 每一個 VNet 可以有多個子網路。 建立 hello 子網路，並與 hello 網路安全性群組相關聯。

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

hello 子網路是現在新增 hello VNet 內，並與網路安全性群組 hello 和規則相關聯。


## <a name="add-a-vnic-toohello-subnet"></a>加入 VNic toohello 子網路

虛擬網路卡 (VNics) 是重要，因為您可以重複使用這些連接這些 toodifferent Vm。 這個方法會保持 hello VNic 當做靜態資源時可能是暫時的 hello Vm。 建立 VNic，並將它與 hello hello 先前步驟中建立的子網路產生關聯。

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>部署至 hello VNet hello VM 和 NSG

您現在有 VNet 的 VNet 及藉由封鎖所有傳入的流量，除了連接埠 22 ssh 的 tooprotect hello 子網路的網路安全性群組內的子網路。 hello VM 現在可以部署在現有的網路基礎結構內。

使用 hello Azure CLI 和 hello`azure vm create`命令 hello Linux VM 是已部署的 toohello 現有的 Azure 資源群組、 VNet、 子網路和 VNic。 如需有關使用 hello CLI toodeploy 完成 VM 的詳細資訊，請參閱[使用 hello Azure CLI 建立完整的 Linux 環境](create-cli-complete.md)

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

使用 hello CLI 旗標 toocall 出現有的資源，指示 Azure toodeploy hello VM hello 現有網路內。 VNet 和子網路部署之後，就可以在 Azure 區域內保持為靜態或永久性資源。  

## <a name="next-steps"></a>後續步驟

* [使用 Azure Resource Manager 範本 toocreate 特定部署](../windows/cli-deploy-templates.md)
* [直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境](create-cli-complete.md)
* [使用範本在 Azure 上建立 Linux VM](create-ssh-secured-vm-from-template.md)
