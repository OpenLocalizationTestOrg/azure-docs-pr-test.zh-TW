---
title: "將虛擬網路閘道新增到 ExpressRoute 的 VNet：PowerShell：Azure | Microsoft Docs"
description: "本文會逐步引導您完成將 VNet 閘道新增到已經建立的 ExpressRoute 的 Resource Manager VNet。"
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
ms.openlocfilehash: 3aeddd03e0be548933775164ae790ba208fc13ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="55b1a-103">使用 PowerShell 為 ExpressRoute 設定虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="55b1a-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="55b1a-104">Resource Manager - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="55b1a-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="55b1a-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="55b1a-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="55b1a-106">傳統 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="55b1a-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="55b1a-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="55b1a-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="55b1a-108">本文將逐步引導您完成為既存的 VNet 新增虛擬網路 (VNet) 閘道、調整該閘道大小及移除該閘道的步驟。</span><span class="sxs-lookup"><span data-stu-id="55b1a-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="55b1a-109">此組態的步驟是使用 Resource Manager 部署模型來建立的 VNet 所專用，而在 ExpressRoute 組態中也將使用該部署模型。</span><span class="sxs-lookup"><span data-stu-id="55b1a-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="55b1a-110">如需有關 ExpressRoute 之虛擬網路閘道和閘道組態設定的詳細資訊，請參閱[關於 ExpressRoute 的虛擬網路閘道](expressroute-about-virtual-network-gateways.md)。</span><span class="sxs-lookup"><span data-stu-id="55b1a-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="55b1a-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="55b1a-111">Before beginning</span></span>
<span data-ttu-id="55b1a-112">確認您已安裝最新的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="55b1a-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="55b1a-113">如果您尚未安裝最新的 Cmdlet，您必須先安裝，然後才能開始進行組態步驟。</span><span class="sxs-lookup"><span data-stu-id="55b1a-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="55b1a-114">如需詳細資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="55b1a-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="55b1a-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55b1a-115">Next steps</span></span>
<span data-ttu-id="55b1a-116">建立 VNet 閘道之後，您可以將 VNet 連結至 ExpressRoute 循環。</span><span class="sxs-lookup"><span data-stu-id="55b1a-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="55b1a-117">請參閱 [將虛擬網路連結到 ExpressRoute 循環](expressroute-howto-linkvnet-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="55b1a-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

