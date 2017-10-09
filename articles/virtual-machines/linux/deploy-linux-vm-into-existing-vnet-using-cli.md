---
title: "aaaDeploy Linux Vm 到現有的網路與 Azure CLI 2.0 |Microsoft 文件"
description: "了解如何 toodeploy Linux 虛擬機器到現有的虛擬網路使用 hello Azure CLI 2.0"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a>如何在 Linux 虛擬機器，在現有的 Azure 虛擬網路以 hello Azure CLI toodeploy

本文章將示範如何 toouse 會 hello Azure CLI 2.0 toodeploy 虛擬機器 (VM)，在現有的虛擬網路。 hello 需求如下：

- [一個 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)
- [SSH 公開金鑰和私密金鑰檔案](mac-create-ssh-keys.md)

您也可以執行下列步驟以 hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md)。


## <a name="quick-commands"></a>快速命令
如果您需要 tooquickly 完成 hello 工作，下列區段的 hello 詳細資料所需的 hello 命令。 詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](#detailed-walkthrough)。

toocreate 這個自訂的環境中，您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。

**必要條件︰**Azure 資源群組、虛擬網路與子網路、允許 SSH 連入流量的網路安全性群組，以及虛擬網路介面卡。

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>部署 hello VM hello 虛擬網路基礎結構

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a>詳細的逐步解說

像虛擬網路和網路安全性群組之類的 Azure 資產應為鮮少部署的靜態且長久資源。 部署虛擬網路之後可以重複使用由沒有任何負面影響 toohello 基礎結構的新部署。 考慮為傳統的硬體的網路交換器的虛擬網路-不需要的 tooconfigure 全新的硬體交換器每一次部署。 有正確設定的虛擬網路，您可以繼續 toodeploy 在該反覆與少的虛擬網路的新 Vm，如果有的話，需要變更虛擬網路的 hello hello 生命週期。

toocreate 這個自訂的環境中，您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。

## <a name="create-hello-resource-group"></a>建立 hello 資源群組

首先，建立 Azure 資源群組 tooorganize 您在本逐步解說中建立的所有項目。 如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。 建立 hello 資源群組與[az 群組建立](/cli/azure/group#create)。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a>建立 hello 虛擬網路

可讓建置 Azure 虛擬網路 toolaunch hello 到 Vm。 如需有關虛擬網路的詳細資訊，請參閱[建立虛擬網路使用 Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)。 建立 hello 虛擬網路與[az 網路 vnet 建立](/cli/azure/network/vnet#create)。 hello 下列範例會建立虛擬網路，名為*myVnet*和名為的子網路*mySubnet*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a>建立 hello 網路安全性群組

Azure 網路安全性群組是相等的 tooa hello 網路層級的防火牆。 如需網路安全性群組的詳細資訊，請參閱[如何 toocreate 網路安全性群組中 hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)。 建立 hello 與網路安全性群組[az 網路 nsg 建立](/cli/azure/network/nsg#create)。 hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a>新增輸入 SSH 允許規則

hello VM 需要從 hello 網際網路，所以規則，允許輸入連接埠 22 流量 toobe 傳遞 hello 網路 tooport 22 hello VM 上所需的存取。 新增輸入的規則 hello 與網路安全性群組[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)。 hello 下列範例會建立名為的規則*myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a>附加 hello 子網路 toohello 網路安全性群組

hello 網路安全性群組規則可以套用的 tooa 子網路或特定虛擬網路介面。 可讓附加 hello 網路安全性群組 tooour 子網路。 附加您子網路 toohello 網路安全性群組與[az 網路 vnet 子網路更新](/cli/azure/network/vnet/subnet#update):

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a>新增虛擬網路介面卡 toohello 子網路

虛擬網路介面卡 (VNics) 而言很重要，因為您可以重複使用這些連接這些 toodifferent Vm。 這種重新使用可讓您 tookeep hello VNic 為靜態資源時可能是暫時的 hello Vm。 建立 VNic，並將它與 hello 的子網路關聯[az 網路 nic 建立](/cli/azure/network/nic#create)。 hello 下列範例會建立名為 VNic *myNic*:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>部署 hello VM hello 虛擬網路基礎結構

您現在會有虛擬網路和子網路和安全性群組 tooprotect hello 子網路透過 ssh 封鎖所有傳入的流量，除了連接埠 22。 hello VM 現在可以部署在現有的網路基礎結構內。

使用 [az vm create](/cli/azure/vm#create) 建立 VM。 如需 hello 旗標與 hello Azure CLI 2.0 toodeploy toouse 完成 VM，請參閱 <<c0> [ 完整 Linux 環境建立使用 Azure CLI hello](create-cli-complete.md)。

hello 下列範例會建立使用 Azure 受管理磁碟的 VM。 這些磁碟都由 hello Azure 平台，而且不需要任何準備或位置 toostore 它們。 如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../../storage/storage-managed-disks-overview.md)。 如果您想 toouse unmanaged 磁碟，請參閱 hello 下列的其他注意事項。

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

如果您使用受控磁碟，請略過此步驟。 如果您想 toouse unmanaged 磁碟時，您需要下列額外的參數 toohello 繼續命令 toocreate unmanaged 磁碟 hello 儲存體帳戶中的 tooadd hello `mystorageaccount`: 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

使用 hello CLI 旗標 toocall 出現有的資源，指示 Azure toodeploy hello VM hello 現有網路內。 虛擬網路和子網路部署之後，就可以在 Azure 區域內保持為靜態或永久性資源。 在此範例中，您建立，且指派公用 IP 位址 toohello VNic，讓此 VM 不是可公開存取 hello 網際網路。 如需詳細資訊，請參閱[建立 VM 的靜態公用 ip 位址使用 hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md)。

## <a name="next-steps"></a>後續步驟
如需在 Azure 中的方式 toocreate 虛擬機器的詳細資訊，請參閱下列資源的 hello:

* [使用 Azure Resource Manager 範本 toocreate 特定部署](../windows/cli-deploy-templates.md)
* [直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境](create-cli-complete.md)
* [使用範本在 Azure 上建立 Linux VM](create-ssh-secured-vm-from-template.md)
