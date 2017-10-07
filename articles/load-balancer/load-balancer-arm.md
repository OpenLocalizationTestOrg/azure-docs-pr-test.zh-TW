---
title: "負載平衡器的資源管理員支援 aaaAzure |Microsoft 文件"
description: "搭配使用適用於 Load Balancer 的 PowerShell 與 Azure Resource Manager。 在負載平衡器中使用範本"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>搭配 Azure Load Balancer 使用 Azure Resource Manager 支援

Azure 資源管理員是在 Azure 中服務的 hello 慣用的管理架構。 Azure Load Balancer 可使用以 Azure Resource Manager 為基礎的 API 和工具進行管理。

## <a name="concepts"></a>概念

使用資源管理員，Azure 負載平衡器包含下列子資源的 hello:

* 前端 IP 組態 - Load balancer 可以包括一或多個前端 IP 位址 (亦稱為虛擬 IP (VIP))。 這些 IP 位址做為輸入 hello 流量。
* 後端位址集區-這些是 hello 虛擬機器網路介面卡 (NIC) toowhich 負載會分散到相關聯的 IP 位址。
* 負載平衡規則-規則屬性對應指定的前端 IP 和連接埠組合 tooa 組的後端 IP 位址和連接埠組合。 單一負載平衡器可以有多個負載平衡規則。 每個規則都是與 VM 相關聯的前端 IP 和連接埠以及後端 IP 和連接埠的組合。
* 探查 – 探查可讓您 tookeep 追蹤 hello 的 VM 執行個體的健全狀況。 如果健全狀況探查失敗，hello VM 執行個體將會進入離輪替循環自動。
* 輸入的 NAT 規則-NAT 規則定義 hello 輸入的流量流經 hello 前端 IP 和分散式的 toohello 回結尾 IP。

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>快速入門範本

Azure 資源管理員可讓您 tooprovision 使用宣告式範本的應用程式。 在單一的範本中，您可以部署多個服務及其相依性。 使用 hello 相同範本 toorepeatedly 部署應用程式在每個階段中的 hello 應用程式生命週期。

範本可以包含虛擬機器、虛擬網路、可用性設定組、網路介面 (NIC)、儲存體帳戶、負載平衡器、網路安全性群組和公開 IP 的定義。 您可以使用範本來建立複雜應用程式所需的一切。 hello 範本檔案可以簽入版本控制和共同作業的內容管理系統中。

[深入了解範本](../azure-resource-manager/resource-manager-template-walkthrough.md)

[深入了解網路資源](../virtual-network/resource-groups-networking.md)

您可以在 [GitHub 儲存機制](https://github.com/Azure/azure-quickstart-templates) (裝載了一組社群產生的範本) 中找到使用 Azure Load Balancer 的快速入門範本。

範本的範例：

* [負載平衡器中的 2 部 VM 和負載平衡規則](http://go.microsoft.com/fwlink/?LinkId=544799)
* [搭配內部負載平衡器的 VNET 中的 2 部 VM 和負載平衡器規則](http://go.microsoft.com/fwlink/?LinkId=544800)
* [負載平衡器中的 2 個 Vm 上 hello LB 設定 NAT 規則](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>使用 PowerShell 或 CLI 設定 Azure 負載平衡器

開始使用 Azure Resource Manager Cmdlet、命令列工具和 REST API

* [Azure 網路 Cmdlet](https://msdn.microsoft.com/library/azure/mt163510.aspx)可以是使用的 toocreate 負載平衡器。
* [如何使用 Azure Resource Manager 負載平衡器 toocreate](load-balancer-get-started-ilb-arm-ps.md)
* [使用 Azure CLI hello 與 Azure 資源管理](../xplat-cli-azure-resource-manager.md)
* [負載平衡器 REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>後續步驟

您也可以[開始建立網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)，以及為特定負載平衡器的網路流量行為設定[分配模式](load-balancer-distribution-mode.md)類型。

深入了解如何 toomanage[閒置 TCP 逾時設定的負載平衡器](load-balancer-tcp-idle-timeout.md)。 當您的應用程式需要 tookeep 連線運作的負載平衡器後方的伺服器，這很重要。
