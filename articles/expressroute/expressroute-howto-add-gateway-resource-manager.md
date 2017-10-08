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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="cff86-103">使用 PowerShell 為 ExpressRoute 設定虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="cff86-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cff86-104">Resource Manager - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cff86-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="cff86-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="cff86-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="cff86-106">傳統 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="cff86-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="cff86-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cff86-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="cff86-108">本文將引導您完成 hello 步驟 tooadd、 調整大小，並移除虛擬網路 (VNet) 閘道預先存在的 vnet。</span><span class="sxs-lookup"><span data-stu-id="cff86-108">This article walks you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="cff86-109">此組態的 hello 步驟是特別針對使用將用於 ExpressRoute 組態中的 hello Resource Manager 部署模型所建立的 Vnet。</span><span class="sxs-lookup"><span data-stu-id="cff86-109">hello steps for this configuration are specifically for VNets that were created using hello Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="cff86-110">如需有關 ExpressRoute 之虛擬網路閘道和閘道組態設定的詳細資訊，請參閱[關於 ExpressRoute 的虛擬網路閘道](expressroute-about-virtual-network-gateways.md)。</span><span class="sxs-lookup"><span data-stu-id="cff86-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="cff86-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="cff86-111">Before beginning</span></span>
<span data-ttu-id="cff86-112">請確認您已安裝最新 Azure PowerShell cmdlet hello。</span><span class="sxs-lookup"><span data-stu-id="cff86-112">Verify that you have installed hello latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="cff86-113">如果您尚未安裝 hello 最新的 cmdlet，您需要 toodo 如此之前開始 hello 組態步驟。</span><span class="sxs-lookup"><span data-stu-id="cff86-113">If you haven't installed hello latest cmdlets, you need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="cff86-114">如需詳細資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="cff86-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="cff86-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cff86-115">Next steps</span></span>
<span data-ttu-id="cff86-116">建立 hello VNet 閘道之後，您可以連結您的 VNet tooan ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="cff86-116">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="cff86-117">請參閱[連結 ExpressRoute 電路的虛擬網路 tooan](expressroute-howto-linkvnet-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="cff86-117">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

