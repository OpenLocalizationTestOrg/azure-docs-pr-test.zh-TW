---
title: "使用 PowerShell 設定 ExpressRoute 的 VNet 閘道：傳統：Azure | Microsoft Docs"
description: "針對 ExpressRoute 組態，使用 PowerShell 設定傳統部署模型 VNet 的 VNet 閘道。"
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 6f37d4d9cba546b5416ab99040f5ef6dae273380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="aedb5-103">使用 PowerShell 設定 ExpressRoute 的虛擬網路閘道閘道 (傳統)</span><span class="sxs-lookup"><span data-stu-id="aedb5-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aedb5-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="aedb5-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="aedb5-105">傳統 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="aedb5-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="aedb5-106">視訊 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="aedb5-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="aedb5-107">本文將逐步引導您透過 hello 步驟 tooadd，調整大小，並移除虛擬網路 (VNet) 閘道預先存在的 vnet。</span><span class="sxs-lookup"><span data-stu-id="aedb5-107">This article will walk you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="aedb5-108">hello 此設定步驟是特別針對使用 hello 所建立的 Vnet**傳統部署模型**而它即是可用於 ExpressRoute 組態。</span><span class="sxs-lookup"><span data-stu-id="aedb5-108">hello steps for this configuration are specifically for VNets that were created using hello **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="aedb5-109">**關於 Azure 部署模型**</span><span class="sxs-lookup"><span data-stu-id="aedb5-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="aedb5-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="aedb5-110">Before beginning</span></span>
<span data-ttu-id="aedb5-111">請確認您已安裝此設定所需的 hello Azure PowerShell cmdlet (1.0.2 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="aedb5-111">Verify that you have installed hello Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="aedb5-112">如果您尚未安裝 hello cmdlet，您將需要 toodo 如此之前開始 hello 組態步驟。</span><span class="sxs-lookup"><span data-stu-id="aedb5-112">If you haven't installed hello cmdlets, you'll need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="aedb5-113">如需有關如何安裝 Azure PowerShell 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="aedb5-113">For more information about installing Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="aedb5-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aedb5-114">Next steps</span></span>
<span data-ttu-id="aedb5-115">建立 hello VNet 閘道之後，您可以連結您的 VNet tooan ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="aedb5-115">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="aedb5-116">請參閱[連結 ExpressRoute 電路的虛擬網路 tooan](expressroute-howto-linkvnet-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="aedb5-116">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

