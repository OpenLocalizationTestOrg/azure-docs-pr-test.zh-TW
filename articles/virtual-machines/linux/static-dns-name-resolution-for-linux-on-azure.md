---
title: "aaaUse vm 的內部 DNS 名稱解析與 hello Azure CLI 2.0 |Microsoft 文件"
description: "Toocreate 虛擬網路介面卡的方式，以及用於在 Azure 上以 hello Azure CLI 2.0 的 VM 名稱解析的內部 DNS"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a>在 Azure 上建立虛擬網路介面卡並使用內部 DNS 進行 VM 名稱解析
本文章將示範如何 tooset 靜態內部 DNS 名稱適用於 Linux Vm 使用虛擬網路介面卡 (vNics) 和標籤名稱，DNS hello Azure CLI 2.0。 您也可以執行下列步驟以 hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 靜態 DNS 名稱是用於永久基礎結構服務，例如 Jenkins 組建伺服器，它用於這份文件或 Git 伺服器。

hello 需求如下：

* [一個 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)
* [SSH 公開金鑰和私密金鑰檔案](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>快速命令
如果您需要 tooquickly 完成 hello 工作，下列區段的 hello 詳細資料所需的 hello 命令。 詳細資訊和內容的每個步驟可以在 hello hello 文件的其餘部分[這裡啟動](#detailed-walkthrough)。 tooperform 這些步驟，您需要 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。

先決條件︰資源群組、虛擬網路與子網路、具有 SSH 輸入的網路安全性群組。

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a>使用靜態內部 DNS 名稱來建立虛擬網路介面卡
建立與 hello vNic [az 網路 nic 建立](/cli/azure/network/nic#create)。 hello `--internal-dns-name` CLI 旗標適用於設定 hello DNS 標籤，可提供 hello hello 虛擬網路介面卡 (vNic) 的靜態 DNS 名稱。 hello 下列範例會建立名為 vNic `myNic`，將它連接 toohello`myVnet`虛擬網路，並建立呼叫的內部 DNS 名稱記錄`jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a>部署 VM，並連接 hello vNic
使用 [az vm create](/cli/azure/vm#create) 來建立 VM。 hello`--nics`旗標在 hello 部署 tooAzure 期間連線 hello vNic toohello VM。 hello 下列範例會建立名為的 VM`myVM`與 Azure 受管理磁碟和名為附加 hello vNic`myNic`從前面步驟中的 hello:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a>詳細的逐步解說

完整的持續整合與連續部署 (CiCd) 在 Azure 上的基礎結構需要特定伺服器 toobe 靜態或長時間執行的伺服器。 建議您使用 Azure 資產像 hello 虛擬網路與網路安全性群組是靜態的而且長時間存在很少部署的資源。 部署虛擬網路之後可以重複使用由沒有任何負面影響 toohello 基礎結構的新部署。 您可以稍後加入 Git 儲存機制伺服器或 Jenkins automation 伺服器提供您開發或測試環境的 CiCd toothis 虛擬網路。  

僅可在 Azure 虛擬網路內解析內部 DNS 名稱。 Hello DNS 名稱是內部的因為它們不是解析 toohello 外部網際網路上，提供額外的安全性 toohello 基礎結構。

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 `myResourceGroup`、`myNic` 和 `myVM`。

## <a name="create-hello-resource-group"></a>建立 hello 資源群組
首先，建立具有 hello 資源群組[az 群組建立](/cli/azure/group#create)。 hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westus`位置：

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a>建立 hello 虛擬網路

hello 下一個步驟是的 toobuild 虛擬網路 toolaunch hello 到 Vm。 hello 虛擬網路包含一個子網路對於此逐步解說。 如需有關 Azure 虛擬網路的詳細資訊，請參閱[建立虛擬網路使用 Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 

建立 hello 虛擬網路與[az 網路 vnet 建立](/cli/azure/network/vnet#create)。 hello 下列範例會建立虛擬網路，名為`myVnet`和名為的子網路`mySubnet`:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a>建立 hello 網路安全性群組
Azure 網路安全性群組是相等的 tooa hello 網路層級的防火牆。 如需網路安全性群組的詳細資訊，請參閱[toocreate Nsg 中的如何 hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 

建立 hello 與網路安全性群組[az 網路 nsg 建立](/cli/azure/network/nsg#create)。 hello 下列範例會建立名為的網路安全性群組`myNetworkSecurityGroup`:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a>新增輸入的規則 tooallow SSH
新增輸入的規則 hello 與網路安全性群組[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)。 hello 下列範例會建立名為的規則`myRuleAllowSSH`:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a>Hello 子網路建立關聯以 hello 網路安全性群組
以網路安全性群組，hello tooassociate hello 子網路使用[az 網路 vnet 子網路更新](/cli/azure/network/vnet/subnet#update)。 hello 下列範例將 hello 子網路名稱`mySubnet`hello 名為的網路安全性群組與`myNetworkSecurityGroup`:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a>建立 hello 虛擬網路介面卡和靜態 DNS 名稱
Azure 是非常有彈性，但 toouse VM 名稱解析的 DNS 名稱，您需要 toocreate 虛擬網路介面卡 (vNics)，包括 DNS 標籤。 vNics 而言很重要，因為您可以重複使用這些連接這些 toodifferent Vm hello 基礎結構的整個週期。 這個方法會保持 hello vNic 當做靜態資源時可能是暫時的 hello Vm。 使用標記 hello vNic 上的 DNS，我們將無法 tooenable hello VNet 中的其他 Vm 所傳來的簡單名稱解析。 使用可解析名稱可讓其他 Vm tooaccess hello automation 伺服器 hello DNS 名稱`Jenkins`或 hello Git 伺服器`gitrepo`。  

建立與 hello vNic [az 網路 nic 建立](/cli/azure/network/nic#create)。 hello 下列範例會建立名為 vNic `myNic`，將它連接 toohello`myVnet`虛擬網路，名為`myVnet`，並建立呼叫的內部 DNS 名稱記錄`jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>部署 hello VM hello 虛擬網路基礎結構
我們現在有了虛擬網路和子網路，網路安全性群組做為防火牆 tooprotect 我們的子網路透過 SSH 和 vNic 封鎖所有傳入的流量，除了連接埠 22。 您現在可以在這個現有的網路基礎結構內部署 VM。

使用 [az vm create](/cli/azure/vm#create) 來建立 VM。 hello 下列範例會建立名為的 VM`myVM`與 Azure 受管理磁碟和名為附加 hello vNic`myNic`從前面步驟中的 hello:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

使用 hello CLI 旗標 toocall 出現有的資源，我們指示 Azure toodeploy hello VM hello 現有網路內。 tooreiterate，一旦部署 VNet 和子網路，他們可以保留為您的 Azure 區域內的靜態或永久資源。  

## <a name="next-steps"></a>後續步驟
* [直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [使用範本在 Azure 上建立 Linux VM](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
