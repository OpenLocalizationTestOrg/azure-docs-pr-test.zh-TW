---
title: "虛擬網路 tooan ExpressRoute 電路的連結： PowerShell： 傳統： Azure |Microsoft 文件"
description: "本文件概述 toolink 虛擬網路 (Vnet) tooExpressRoute 電路使用 hello 傳統部署模型和 PowerShell 的方式。"
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="7ce21-103">連接虛擬網路 tooan ExpressRoute 電路使用 PowerShell （傳統）</span><span class="sxs-lookup"><span data-stu-id="7ce21-103">Connect a virtual network tooan ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ce21-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7ce21-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="7ce21-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ce21-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="7ce21-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7ce21-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="7ce21-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7ce21-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="7ce21-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="7ce21-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="7ce21-109">本文將協助您使用 hello 傳統部署模型和 PowerShell 連結虛擬網路 (Vnet) tooAzure ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="7ce21-109">This article will help you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello classic deployment model and PowerShell.</span></span> <span data-ttu-id="7ce21-110">虛擬網路可以是在 hello 相同訂用帳戶，或可以是另一個訂用帳戶的一部分。</span><span class="sxs-lookup"><span data-stu-id="7ce21-110">Virtual networks can either be in hello same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="7ce21-111">**關於 Azure 部署模型**</span><span class="sxs-lookup"><span data-stu-id="7ce21-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="7ce21-112">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="7ce21-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="7ce21-113">您需要 hello hello Azure PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="7ce21-113">You need hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="7ce21-114">您可以從 hello hello PowerShell 區段下載最新 PowerShell 模組 hello [Azure 下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="7ce21-114">You can download hello latest PowerShell modules from hello PowerShell section of hello [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="7ce21-115">請依照下列中的 hello 指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)的逐步指示如何 tooconfigure 電腦 toouse hello Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="7ce21-115">Follow hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>
2. <span data-ttu-id="7ce21-116">您需要 tooreview hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="7ce21-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="7ce21-117">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="7ce21-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="7ce21-118">請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-classic.md)且有連線提供者啟用 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="7ce21-118">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable hello circuit.</span></span>
   * <span data-ttu-id="7ce21-119">確定您已針對循環設定了 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="7ce21-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="7ce21-120">請參閱 hello[設定路由](expressroute-howto-routing-classic.md)路由指示的發行項。</span><span class="sxs-lookup"><span data-stu-id="7ce21-120">See hello [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="7ce21-121">請確認 Azure 私用對等設定，且 hello BGP 對等互連網路與 Microsoft 之間，以便您可以啟用端對端連線已啟動。</span><span class="sxs-lookup"><span data-stu-id="7ce21-121">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="7ce21-122">您必須有已建立且完整佈建的虛擬網路和虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="7ce21-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="7ce21-123">請依照下列指示 hello 太[設定 expressroute 的虛擬網路](expressroute-howto-vnet-portal-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="7ce21-123">Follow hello instructions too[configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="7ce21-124">您可以連結 too10 虛擬網路 tooan ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="7ce21-124">You can link up too10 virtual networks tooan ExpressRoute circuit.</span></span> <span data-ttu-id="7ce21-125">所有虛擬網路必須位於 hello 相同地理政治區域。</span><span class="sxs-lookup"><span data-stu-id="7ce21-125">All virtual networks must be in hello same geopolitical region.</span></span> <span data-ttu-id="7ce21-126">您可以更大量的虛擬網路 tooyour ExpressRoute 電路的連結，或位於其他地緣政治區域，如果您啟用 hello ExpressRoute premium add-on 的虛擬網路連結。</span><span class="sxs-lookup"><span data-stu-id="7ce21-126">You can link a larger number of virtual networks tooyour ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="7ce21-127">檢查 hello[常見問題集](expressroute-faqs.md)如需有關 hello premium 附加元件。</span><span class="sxs-lookup"><span data-stu-id="7ce21-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="7ce21-128">連接 hello 中的虛擬網路相同的訂用帳戶 tooa 電路</span><span class="sxs-lookup"><span data-stu-id="7ce21-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="7ce21-129">您可以使用下列 cmdlet 的 hello 連結虛擬網路 tooan ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="7ce21-129">You can link a virtual network tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="7ce21-130">請確定該 hello 虛擬網路閘道建立並且準備好進行連結，然後再執行 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="7ce21-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="7ce21-131">在不同的訂用帳戶 tooa 電路的虛擬網路連線</span><span class="sxs-lookup"><span data-stu-id="7ce21-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="7ce21-132">您可以讓多個訂用帳戶共用 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="7ce21-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="7ce21-133">hello 遵循圖顯示的簡單圖解如何共用 ExpressRoute 電路的運作方式跨多個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ce21-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="7ce21-134">Hello hello 大型雲端內的小型雲端都屬於 toodifferent 部門組織內使用的 toorepresent 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ce21-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="7ce21-135">針對部署其服務： 但 hello 部門可以共用單一 ExpressRoute 電路 tooconnect 後 tooyour 在內部部署網路，hello 部門 hello 組織內的每個可以使用自己的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ce21-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but hello departments can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="7ce21-136">單一部門 (在此範例中： IT) 可以擁有 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="7ce21-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="7ce21-137">Hello 組織內其他訂用帳戶可以使用 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="7ce21-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="7ce21-138">Hello 專用循環的連線和頻寬費用將會套用的 toohello ExpressRoute 電路擁有者。</span><span class="sxs-lookup"><span data-stu-id="7ce21-138">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="7ce21-139">所有虛擬網路共用 hello 相同的頻寬。</span><span class="sxs-lookup"><span data-stu-id="7ce21-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="7ce21-141">系統管理</span><span class="sxs-lookup"><span data-stu-id="7ce21-141">Administration</span></span>
<span data-ttu-id="7ce21-142">hello*電路擁有者*是 hello 管理員/coadministrator hello 訂用帳戶中的 hello ExpressRoute 電路建立。</span><span class="sxs-lookup"><span data-stu-id="7ce21-142">hello *circuit owner* is hello administrator/coadministrator of hello subscription in which hello ExpressRoute circuit is created.</span></span> <span data-ttu-id="7ce21-143">hello 電路擁有者可以授權其他訂用帳戶，參照 tooas 的系統管理員/coadministrators*電路使用者*，toouse hello 專用他們所擁有的電路。</span><span class="sxs-lookup"><span data-stu-id="7ce21-143">hello circuit owner can authorize administrators/coadministrators of other subscriptions, referred tooas *circuit users*, toouse hello dedicated circuit that they own.</span></span> <span data-ttu-id="7ce21-144">循環的使用者授權的 toouse hello 組織的 ExpressRoute 電路可以連結 hello 中其訂用帳戶 toohello ExpressRoute 電路的虛擬網路之後他們獲授權。</span><span class="sxs-lookup"><span data-stu-id="7ce21-144">Circuit users who are authorized toouse hello organization's ExpressRoute circuit can link hello virtual network in their subscription toohello ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="7ce21-145">hello 電路擁有者隨時都有 hello 電源 toomodify 和撤銷授權。</span><span class="sxs-lookup"><span data-stu-id="7ce21-145">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="7ce21-146">撤銷授權會導致從已撤銷其存取權的 hello 訂用帳戶中刪除所有連結。</span><span class="sxs-lookup"><span data-stu-id="7ce21-146">Revoking an authorization will result in all links being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="7ce21-147">循環擁有者作業</span><span class="sxs-lookup"><span data-stu-id="7ce21-147">Circuit owner operations</span></span>

<span data-ttu-id="7ce21-148">**建立授權**</span><span class="sxs-lookup"><span data-stu-id="7ce21-148">**Creating an authorization**</span></span>

<span data-ttu-id="7ce21-149">hello 電路擁有者授與其他訂閱的 hello 管理員 toouse hello 指定循環。</span><span class="sxs-lookup"><span data-stu-id="7ce21-149">hello circuit owner authorizes hello administrators of other subscriptions toouse hello specified circuit.</span></span> <span data-ttu-id="7ce21-150">在下列範例的 hello，hello hello 電路 (Contoso IT) 系統管理員可讓向上 tootwo 虛擬網路 toohello 循環的另一個訂用帳戶 （開發測試） toolink hello 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="7ce21-150">In hello following example, hello administrator of hello circuit (Contoso IT) enables hello administrator of another subscription (Dev-Test) toolink up tootwo virtual networks toohello circuit.</span></span> <span data-ttu-id="7ce21-151">hello Contoso IT 系統管理員可讓這指定 hello 開發測試 Microsoft id。</span><span class="sxs-lookup"><span data-stu-id="7ce21-151">hello Contoso IT administrator enables this by specifying hello Dev-Test Microsoft ID.</span></span> <span data-ttu-id="7ce21-152">hello cmdlet 不會傳送電子郵件 toohello 指定的 Microsoft id。</span><span class="sxs-lookup"><span data-stu-id="7ce21-152">hello cmdlet doesn't send email toohello specified Microsoft ID.</span></span> <span data-ttu-id="7ce21-153">hello 電路擁有者必須 tooexplicitly 通知 hello hello 授權其他訂用帳戶擁有者已完成。</span><span class="sxs-lookup"><span data-stu-id="7ce21-153">hello circuit owner needs tooexplicitly notify hello other subscription owner that hello authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="7ce21-154">**檢閱授權**</span><span class="sxs-lookup"><span data-stu-id="7ce21-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="7ce21-155">hello 電路擁有者可以檢閱由執行下列 cmdlet 的 hello 特定電路發出的所有授權：</span><span class="sxs-lookup"><span data-stu-id="7ce21-155">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="7ce21-156">**更新授權**</span><span class="sxs-lookup"><span data-stu-id="7ce21-156">**Updating authorizations**</span></span>

<span data-ttu-id="7ce21-157">hello 電路擁有者可以使用下列 cmdlet 的 hello 修改授權：</span><span class="sxs-lookup"><span data-stu-id="7ce21-157">hello circuit owner can modify authorizations by using hello following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="7ce21-158">**刪除授權**</span><span class="sxs-lookup"><span data-stu-id="7ce21-158">**Deleting authorizations**</span></span>

<span data-ttu-id="7ce21-159">hello 電路擁有者可以撤銷/刪除授權 toohello 使用者藉由執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ce21-159">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="7ce21-160">循環使用者作業</span><span class="sxs-lookup"><span data-stu-id="7ce21-160">Circuit user operations</span></span>

<span data-ttu-id="7ce21-161">**檢閱授權**</span><span class="sxs-lookup"><span data-stu-id="7ce21-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="7ce21-162">hello 循環使用者可以使用下列 cmdlet 的 hello 來檢閱授權：</span><span class="sxs-lookup"><span data-stu-id="7ce21-162">hello circuit user can review authorizations by using hello following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="7ce21-163">**兌換連結授權**</span><span class="sxs-lookup"><span data-stu-id="7ce21-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="7ce21-164">hello 循環使用者可以執行下列 cmdlet tooredeem hello 連結授權：</span><span class="sxs-lookup"><span data-stu-id="7ce21-164">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="7ce21-165">Hello 虛擬網路的新連結的 hello 訂用帳戶中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="7ce21-165">Run this command in hello newly linked subscription for hello virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="7ce21-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ce21-166">Next steps</span></span>
<span data-ttu-id="7ce21-167">如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="7ce21-167">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

