---
title: "aaaDeploy Linux Vm 到現有的網路與 Azure 入口網站 |Microsoft 文件"
description: "將 Linux VM 部署到現有 Azure 虛擬網路使用 hello 入口網站。"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a>如何 toodeploy Linux 虛擬機器在現有的 Azure 虛擬網路以 hello Azure 入口網站

本文章將示範如何 toodeploy 到現有的虛擬網路 (VNet) 的虛擬機器 (VM)。 像 VNet 和網路安全性群組之類的 Azure 資產應為鮮少部署的靜態且長久資源。 一旦部署的 VNet，可以重複使用的常數的使用不含任何不良影響 toohello 基礎結構。 考慮為傳統 VNet 硬體網路交換器-不需要的 tooconfigure 全新的硬體交換器每一次部署。  

具有正確設定 VNet，您可以繼續 toodeploy 新伺服器到該 VNet 反覆數，如果有的話，hello VNet hello 生命週期所需的變更。

## <a name="create-hello-resource-group"></a>建立 hello 資源群組

首先，建立資源群組 tooorganize 您在本逐步解說中建立的所有項目。 如需 Azure 資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a>建立 hello VNet

接下來，建立 VNet toolaunch hello 到 Vm。 hello VNet 包含一個子網路，而且是 hello 稍後步驟中此子網路與網路安全性群組相關聯。

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a>加入 VNic toohello 子網路

虛擬網路卡 (VNics) 是重要，因為連接 toodifferent Vm。 這個方法會保持 hello VNic 當做靜態資源時可能是暫時的 hello Vm。 建立 VNic，並將它與 hello hello 先前步驟中建立的子網路產生關聯。

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a>建立 hello 網路安全性群組

Azure 網路安全性群組是相等的 tooa hello 網路層級的防火牆。 如需有關 Azure 網路安全性群組的詳細資訊，請參閱[什麼是網路安全性群組](../../virtual-network/virtual-networks-nsg.md)。

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>新增輸入 SSH 允許規則

hello VM 需要從 hello 存取網際網路，因此規則，允許輸入連接埠 22 流量 toobe 通過上建立 VM 的 hello hello 網路 tooport 22。

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a>將 hello NSG 與 hello 子網路產生關聯

Hello VNet 和建立 hello 子網路，請將 hello 網路安全性群組與 hello 子網路產生關聯。 網路安全性群組可以與整個子網路或個別的 VNic 產生關聯。 Hello 防火牆篩選 hello 子網路層級的流量時，所有 VNics 和 hello 子網路內的 hello Vm 已都受到 hello 網路安全性群組。 hello 另一種方法是 hello 網路安全性群組正在只單一 VNic 相關聯，並保護只在一個 VM。

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>部署至 hello VNet hello VM 和 NSG

使用 hello Azure 入口網站，hello Linux VM 是已部署的 toohello 現有的 Azure 資源群組、 VNet、 子網路和 VNic。

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

藉由使用 hello 入口 toochoose 現有資源，您可以指示 Azure toodeploy hello VM hello 現有網路內。 VNet 和子網路部署之後，就可以在 Azure 區域內保持為靜態或永久性資源。  

## <a name="next-steps"></a>後續步驟

* [使用 Azure Resource Manager 範本 toocreate 特定部署](../windows/cli-deploy-templates.md)
* [直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境](create-cli-complete.md)
* [使用範本在 Azure 上建立 Linux VM](create-ssh-secured-vm-from-template.md)
