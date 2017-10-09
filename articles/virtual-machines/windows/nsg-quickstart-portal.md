---
title: "aaaOpen 連接埠 tooa VM 使用 hello Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 tooopen 連接埠建立端點 tooyour Windows VM / hello Azure 入口網站中使用 hello 資源管理員部署模型"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a>如何 tooopen 連接埠 tooa hello Azure 入口網站的虛擬機器
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>快速命令
您也可以 [使用 Azure PowerShell 來執行這些步驟](nsg-quickstart-powershell.md)。

首先，建立您的「網路安全性群組」。 在 hello 入口網站中選取資源群組中，選擇 **新增**，然後搜尋並選取**網路安全性群組**:

![新增網路安全性群組](./media/nsg-quickstart-portal/add-nsg.png)

輸入您「網路安全性群組」的名稱，選取或建立資源群組，然後選取位置。 完成後，請選取 [建立]：

![建立網路安全性群組](./media/nsg-quickstart-portal/create-nsg.png)

選取您的新「網路安全性群組」。 選取 '輸入安全性規則'，然後選取 hello**新增**按鈕 toocreate 規則：

![新增輸入規則](./media/nsg-quickstart-portal/add-inbound-rule.png)

選擇一般**服務**從 hello 下拉式選單，例如*HTTP*。 您也可以選取*自訂*tooprovide 特定通訊埠 toouse。 如有需要，變更 hello 優先順序或名稱。 hello 優先權會影響 hello 規則會套用的順序-hello 低 hello 數值，hello 早 hello 套用規則。 您也可以選取**進階**頂端 hello 這個畫面 tooenter 特定來源 IP 區塊或連接埠範圍，例如。 當您準備好時，選取**確定**toocreate hello 規則：

![建立輸入規則](./media/nsg-quickstart-portal/create-inbound-rule.png)

最後一個步驟是的 tooassociate 群組與子網路或特定的網路介面的網路安全性。 讓我們 hello 網路安全性群組關聯的子網路。 選取 [子網路]，然後選擇 [關聯]：

![將網路安全性群組與子網路建立關聯](./media/nsg-quickstart-portal/associate-subnet.png)

選取您的虛擬網路，然後選取 hello 適當的子網路：

![將網路安全性群組與虛擬網路功能建立關聯](./media/nsg-quickstart-portal/select-vnet-subnet.png)

您現在已建立「網路安全性群組」、已建立允許連接埠 80 上流量的輸入規則，並且已將它與子網路建立關聯。 任何連接 toothat 子網路的 Vm 會連線到通訊埠 80 上。

## <a name="more-information-on-network-security-groups"></a>網路安全性群組的詳細資訊
這裡 hello 快速命令可讓您設定 tooget 和流量流動 tooyour VM 執行。 網路安全性群組可提供許多很棒的功能和控制存取 tooyour 資源的資料粒度。 您可以深入了解 [建立網路安全性群組和 ACL 規則](../../virtual-network/virtual-networks-create-nsg-arm-ps.md)。

針對高可用性 Web 應用程式，您應該將 VM 放在 Azure Load Balancer 後方。 hello 負載平衡器會將流量 tooVMs，以提供的流量篩選的網路安全性群組。 如需詳細資訊，請參閱[如何 tooload 平衡 Linux 虛擬機器中 Azure toocreate 高可用性的應用程式](tutorial-load-balancer.md)。

## <a name="next-steps"></a>後續步驟
在此範例中，您可以建立簡單的規則 tooallow HTTP 流量。 您可以找到有關 hello 下列文件中建立更詳細的環境：

* [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)
* [什麼是網路安全性群組 (NSG)？](../../virtual-network/virtual-networks-nsg.md)