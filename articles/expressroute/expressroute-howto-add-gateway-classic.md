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
ms.openlocfilehash: 195a38fa45f1c514a93980e777fb0d8238aa3f3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="febf3-103">使用 PowerShell 設定 ExpressRoute 的虛擬網路閘道閘道 (傳統)</span><span class="sxs-lookup"><span data-stu-id="febf3-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="febf3-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="febf3-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="febf3-105">傳統 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="febf3-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="febf3-106">視訊 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="febf3-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="febf3-107">本文將逐步引導您完成既存 VNet 的虛擬網路 (VNet) 閘道加入、重新調整和移除步驟。</span><span class="sxs-lookup"><span data-stu-id="febf3-107">This article will walk you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="febf3-108">此組態的步驟是使用 **傳統部署模型** 建立的 VNet 專用，且將用於 ExpressRoute 組態中。</span><span class="sxs-lookup"><span data-stu-id="febf3-108">The steps for this configuration are specifically for VNets that were created using the **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="febf3-109">**關於 Azure 部署模型**</span><span class="sxs-lookup"><span data-stu-id="febf3-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="febf3-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="febf3-110">Before beginning</span></span>
<span data-ttu-id="febf3-111">確認您已安裝此組態所需的 Azure PowerShell Cmdlet (1.0.2 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="febf3-111">Verify that you have installed the Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="febf3-112">如果您尚未安裝 Cmdlet，您必須先安裝，然後才能開始進行組態步驟。</span><span class="sxs-lookup"><span data-stu-id="febf3-112">If you haven't installed the cmdlets, you'll need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="febf3-113">如需安裝 Azure PowerShell 的詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="febf3-113">For more information about installing Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="febf3-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="febf3-114">Next steps</span></span>
<span data-ttu-id="febf3-115">建立 VNet 閘道之後，您可以將 VNet 連結至 ExpressRoute 循環。</span><span class="sxs-lookup"><span data-stu-id="febf3-115">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="febf3-116">請參閱 [將虛擬網路連結到 ExpressRoute 循環](expressroute-howto-linkvnet-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="febf3-116">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

