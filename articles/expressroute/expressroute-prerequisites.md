---
title: "Azure ExpressRoute 採用 aaaPrerequisites |Microsoft 文件"
description: "此頁面會提供一份需求 toobe 符合之前，您可以訂購 Azure ExpressRoute 電路。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 524c86f6570dc6e6505fe55323b8508e8eeff791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-prerequisites--checklist"></a>ExpressRoute 必要條件和檢查清單
已符合 tooconnect tooMicrosoft 雲端服務使用 ExpressRoute，您需要 tooverify 該 hello 下列 hello 下列各節中所列的需求。

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a>Azure 帳戶
* 使用中的有效 Microsoft Azure 帳戶。 此帳戶是必要的 tooset 向上 hello ExpressRoute 電路。 ExpressRoute 循環是 Azure 訂用帳戶內的資源。 Azure 訂用帳戶是需求，即使連線能力是受限的 toonon Azure Microsoft 雲端服務，例如 Office 365 服務和 Dynamics 365。
* 使用中的 Office 365 訂用帳戶 (如果使用的是 Office 365 服務)。 如需詳細資訊，請參閱 hello [Office 365 特定需求](#office-365-specific-requirements)本文一節。

## <a name="connectivity-provider"></a>連線提供者

* 您可以使用[ExpressRoute 連線夥伴](expressroute-locations.md#partners)tooconnect toohello Microsoft 雲端。 您可以透過 [三種方法](expressroute-introduction.md)在內部部署網路與 Microsoft 之間設定連線。
* 如果您的提供者不是 ExpressRoute 連線協力電腦，您仍然可以連線到 toohello Microsoft 雲端[雲端交換服務提供者](expressroute-locations.md#connectivity-through-exchange-providers)。

## <a name="network-requirements"></a>網路需求
* **備援連線**︰您和您的提供者之間不需要實體連線備援。 Microsoft 需要備援的 BGP 工作階段 toobe，即使您只需要設定 Microsoft 的路由器和 hello 對等路由器之間[一個實體連接 tooa 雲端交換](expressroute-faqs.md#onep2plink)。
* **路由**： 根據您連接 toohello Microsoft 雲端方式，您或您的提供者需要 tooset 註冊和管理 hello BGP 工作階段[路由網域](expressroute-circuit-peerings.md)。 某些乙太網路連線服務提供者或雲端交換服務提供者可能會提供 BGP 管理功能做為附加價值服務。
* **NAT**：Microsoft 只接受透過 Microsoft 對等互連的公用 IP 位址。 如果您在內部部署網路中使用私人 IP 位址，您或您提供者需要 tootranslate hello 私人 IP 位址 toohello 公用 IP 位址[使用 hello NAT](expressroute-nat.md)。
* **QoS**：商務用 Skype 具有各種服務 (例如語音、視訊、文字)，其所要求的 QoS 處理方式各有差異。 您和您的提供者應該遵循 hello[服務需求品質](expressroute-qos.md)。
* **網路安全性**： 請考慮[網路安全性](../best-practices-network-security.md)連接 toohello 透過 ExpressRoute 的 Microsoft 雲端時。

## <a name="office-365"></a>Office 365
如果您計劃 ExpressRoute tooenable Office 365，請檢閱下列 Office 365 需求的詳細資訊的文件的 hello。

* [ExpressRoute for Office 365 概觀](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [使用 ExpressRoute for Office 365 進行路由](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [Office 365 URL 與 IP 位址範圍](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [Office 365 的網路規劃與效能調整](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [網路頻寬計算機和工具](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [整合 Office 365 與內部部署環境](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [Office 365 上的 ExpressRoute 進階訓練影片](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a>Dynamics 365
如果您計劃 ExpressRoute tooenable Dynamics 365，請檢閱下列文件，如需有關 Dynamics 365 hello

* [Dynamics 365 和 ExpressRoute 白皮書](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf)
* [Dynamics 365 URL](https://support.microsoft.com/kb/2655102) 和 [IP 位址範圍](https://support.microsoft.com/kb/2728473)

## <a name="next-steps"></a>後續步驟
* 如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。
* 尋找 ExpressRoute 連線提供者。 請參閱 [ExpressRoute 合作夥伴和對等位置](expressroute-locations.md)。
* 參考的 toorequirements[路由](expressroute-routing.md)， [NAT](expressroute-nat.md)，和[QoS](expressroute-qos.md)。
* 設定 ExpressRoute 連線。
  * [建立 ExpressRoute 線路](expressroute-howto-circuit-classic.md)
  * [設定路由](expressroute-howto-routing-classic.md)
  * [連結的 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-classic.md)
