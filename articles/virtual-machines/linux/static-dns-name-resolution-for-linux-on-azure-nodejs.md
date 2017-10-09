---
title: "aaaUsing vm 的內部 DNS 名稱在 Azure 上的解析 |Microsoft 文件"
description: "在 Azure 上針對 VM 名稱解析使用內部 DNS。"
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
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a>在 Azure 上針對 VM 名稱解析使用內部 DNS

本文將說明如何 tooset 靜態內部 DNS 命名適用於 Linux Vm 使用虛擬 NIC 卡 (VNic) 和標籤的 DNS 名稱。 靜態 DNS 名稱是用於永久基礎結構服務，例如 Jenkins 組建伺服器，它用於這份文件或 Git 伺服器。

hello 需求如下：

* [一個 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)
* [SSH 公開金鑰和私密金鑰檔案](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI


## <a name="quick-commands"></a>快速命令

如果您需要 tooquickly 完成 hello 工作，下列區段的 hello 詳細資料所需的 hello 命令。 詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](#detailed-walkthrough)。  

必要條件︰資源群組、VNet、具有 SSH 輸入的 NSG、子網路。

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a>使用靜態內部 DNS 名稱建立 VNic

hello `-r` cli 旗標適用於設定 hello DNS 標籤，可提供 hello VNic hello 靜態 DNS 名稱。

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a>部署到 hello VNet，NSG hello VM，以及連線 hello VNic

hello`-N`連接 hello VNic toohello hello 部署 tooAzure 期間的新 VM。

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a>詳細的逐步解說

完整的持續整合與連續部署 (CiCd) 在 Azure 上的基礎結構需要特定伺服器 toobe 靜態或長時間執行的伺服器。  建議您使用 Azure 資產，例如 hello 虛擬網路 (Vnet) 和網路安全性群組 (Nsg)，應為靜態和長時間存在很少部署的資源。  部署的 VNet 之後, 可以重複使用由沒有任何負面影響 toohello 基礎結構的新部署。  加入 toothis 靜態網路 Git 儲存機制中伺服器與 Jenkins 自動化傳遞 CiCd tooyour 開發或測試環境。  

僅可在 Azure 虛擬網路內解析內部 DNS 名稱。  Hello DNS 名稱是內部的因為它們不是解析 toohello 外部網際網路上，提供額外的安全性 toohello 基礎結構。

_將任何範例換成您自己的名稱。_

## <a name="create-hello-resource-group"></a>建立 hello 資源群組

資源群組是需要的 tooorganize 我們在本逐步解說中建立的所有項目。  如需 Azure 資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a>建立 hello VNet

hello 第一個步驟是的 toobuild VNet toolaunch hello 到 Vm。  hello VNet 包含此逐步解說中的一個子網路。  如需有關 Azure Vnet 的詳細資訊，請參閱[建立虛擬網路使用 Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a>建立 hello NSG

hello 子網路是內建背後現有的網路安全性群組，所以我們建置 hello NSG 之前 hello 子網路。  Azure 的 Nsg 是相等的 tooa hello 網路層級的防火牆。  如需有關 Azure Nsg 的詳細資訊，請參閱[toocreate Nsg 中的如何 hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>新增輸入 SSH 允許規則

hello Linux VM 需要的 hello 需要讓規則，允許輸入連接埠 22 流量 toobe 傳遞 hello 網路 tooport 22 hello Linux VM 上的網際網路存取權。

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>新增子網路 toohello VNet

Hello VNet 必須位於子網路內的 Vm。  每一個 VNet 可以有多個子網路。  建立 hello 子網路，並將 hello 子網路與 hello NSG tooadd 防火牆 toohello 子網路產生關聯。

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

現在 hello 子網路是新增 hello VNet 內，並與 hello NSG 與 hello NSG 規則相關聯。

## <a name="creating-static-dns-names"></a>建立靜態 DNS 名稱

Azure 是非常有彈性，但 toouse Vm 名稱解析的 DNS 名稱，您需要的 toocreate 它們當做虛擬網路卡 (VNics) 使用 DNS 標籤。  VNics 而言很重要，因為您可以重複使用這些連接這些 toodifferent Vm 期間 hello Vm 可能是暫時性，維持 hello VNic 為靜態的資源。  使用標記 hello VNic 上的 DNS，我們將無法 tooenable hello VNet 中的其他 Vm 所傳來的簡單名稱解析。  使用可解析名稱可讓其他 Vm tooaccess hello automation 伺服器 hello DNS 名稱`Jenkins`或 hello Git 伺服器`gitrepo`。  建立 VNic，並將它與 hello hello 上一個步驟中建立子網路產生關聯。

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>部署至 hello VNet hello VM 和 NSG

我們現在有 VNet，而該 VNet 和我們的子網路防火牆 tooprotect 作為透過 ssh 封鎖所有傳入的流量，除了連接埠 22 NSG 內部的子網路。  hello VM 現在可以部署在現有的網路基礎結構內。

使用 hello Azure CLI 和 hello`azure vm create`命令 hello Linux VM 是已部署的 toohello 現有的 Azure 資源群組、 VNet、 子網路和 VNic。  如需有關使用 hello CLI toodeploy 完成 VM 的詳細資訊，請參閱[使用 hello Azure CLI 建立完整的 Linux 環境](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

使用 hello CLI 旗標 toocall 出現有的資源，我們指示 Azure toodeploy hello VM hello 現有網路內。  tooreiterate，一旦部署 VNet 和子網路，他們可以保留為您的 Azure 區域內的靜態或永久資源。  

## <a name="next-steps"></a>後續步驟
* [直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [使用範本在 Azure 上建立 Linux VM](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
