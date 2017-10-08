---
title: "新增虛擬網路閘道 tooa VNet expressroute: PowerShell: Azure |Microsoft 文件"
description: "這篇文章會引導您完成新增已建立 ExpressRoute 的資源管理員 VNet 的 VNet 閘道 tooan。"
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 8983430b426ad7c4af766294fa16427c5e9df5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a>使用 PowerShell 為 ExpressRoute 設定虛擬網路閘道
> [!div class="op_single_selector"]
> * [Resource Manager - Azure 入口網站](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [傳統 - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [影片 - Azure 入口網站](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

本文將引導您完成 hello 步驟 tooadd、 調整大小，並移除虛擬網路 (VNet) 閘道預先存在的 vnet。 此組態的 hello 步驟是特別針對使用將用於 ExpressRoute 組態中的 hello Resource Manager 部署模型所建立的 Vnet。 如需有關 ExpressRoute 之虛擬網路閘道和閘道組態設定的詳細資訊，請參閱[關於 ExpressRoute 的虛擬網路閘道](expressroute-about-virtual-network-gateways.md)。 


## <a name="before-beginning"></a>開始之前
請確認您已安裝最新 Azure PowerShell cmdlet hello。 如果您尚未安裝 hello 最新的 cmdlet，您需要 toodo 如此之前開始 hello 組態步驟。 如需詳細資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a>後續步驟
建立 hello VNet 閘道之後，您可以連結您的 VNet tooan ExpressRoute 電路。 請參閱[連結 ExpressRoute 電路的虛擬網路 tooan](expressroute-howto-linkvnet-arm.md)。

