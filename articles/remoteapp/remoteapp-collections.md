---
title: "Azure RemoteApp 需要何種集合？ | Microsoft Docs"
description: "深入了解可搭配 Azure RemoteApp 使用的集合類型。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 10f6c0533027767b6635ebff1e6a9872bde06a68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a><span data-ttu-id="142b1-104">Azure RemoteApp 需要何種集合？</span><span class="sxs-lookup"><span data-stu-id="142b1-104">What kind of collection do you need for Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="142b1-105">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="142b1-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="142b1-106">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="142b1-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="142b1-107">Azure RemoteApp 可讓您在任何裝置上與使用者共用應用程式和資源。</span><span class="sxs-lookup"><span data-stu-id="142b1-107">Azure RemoteApp lets you share apps and resources with users on any device.</span></span> <span data-ttu-id="142b1-108">做法是建立來保存應用程式和資源的集合，然後與使用者共用那些集合。</span><span class="sxs-lookup"><span data-stu-id="142b1-108">We do this by creating collections to hold the apps and resources, and then you share those collections with users.</span></span> <span data-ttu-id="142b1-109">有兩個不同的集合選項，各有不同的網路和驗證選項 - 哪一種最適合您？</span><span class="sxs-lookup"><span data-stu-id="142b1-109">There are 2 different collection options, with different network and authentication options - which is right for you?</span></span>

<span data-ttu-id="142b1-110">讓我們逐步說明不同的考量和您必須做的選擇，以充分利用 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="142b1-110">Let's walk through the different considerations and choices you need to make to get the most out of your Azure RemoteApp collection.</span></span> 

## <a name="quick-differences-between-the-collection-types"></a><span data-ttu-id="142b1-111">快速了解不同集合類型間的差異</span><span class="sxs-lookup"><span data-stu-id="142b1-111">Quick differences between the collection types</span></span>
|  | <span data-ttu-id="142b1-112">雲端</span><span class="sxs-lookup"><span data-stu-id="142b1-112">Cloud</span></span> | <span data-ttu-id="142b1-113">混合式</span><span class="sxs-lookup"><span data-stu-id="142b1-113">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="142b1-114">使用現有的 VNET</span><span class="sxs-lookup"><span data-stu-id="142b1-114">Use an existing VNET</span></span> |<span data-ttu-id="142b1-115">是</span><span class="sxs-lookup"><span data-stu-id="142b1-115">Yes</span></span> |<span data-ttu-id="142b1-116">是</span><span class="sxs-lookup"><span data-stu-id="142b1-116">Yes</span></span> |
| <span data-ttu-id="142b1-117">需要連線到 AD 的帳戶 (DirSync)</span><span class="sxs-lookup"><span data-stu-id="142b1-117">Requires AD-connected accounts (DirSync)</span></span> |<span data-ttu-id="142b1-118">否</span><span class="sxs-lookup"><span data-stu-id="142b1-118">No</span></span> |<span data-ttu-id="142b1-119">是</span><span class="sxs-lookup"><span data-stu-id="142b1-119">Yes</span></span> |
| <span data-ttu-id="142b1-120">需要加入網域</span><span class="sxs-lookup"><span data-stu-id="142b1-120">Requires domain join</span></span> |<span data-ttu-id="142b1-121">否</span><span class="sxs-lookup"><span data-stu-id="142b1-121">No</span></span> |<span data-ttu-id="142b1-122">是</span><span class="sxs-lookup"><span data-stu-id="142b1-122">Yes</span></span> |
| <span data-ttu-id="142b1-123">需讓網域控制站可以存取 VNET</span><span class="sxs-lookup"><span data-stu-id="142b1-123">Requires domain controller accessible to VNET</span></span> |<span data-ttu-id="142b1-124">否</span><span class="sxs-lookup"><span data-stu-id="142b1-124">No</span></span> |<span data-ttu-id="142b1-125">是</span><span class="sxs-lookup"><span data-stu-id="142b1-125">Yes</span></span> |

## <a name="cloud-collections"></a><span data-ttu-id="142b1-126">雲端集合</span><span class="sxs-lookup"><span data-stu-id="142b1-126">Cloud collections</span></span>
* <span data-ttu-id="142b1-127">可快速建立 - 集合的佈建速度很快，這表示使用者能更快取得您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="142b1-127">Quick to create - the collection is quickly provisioned, meaning your apps get to users quicker.</span></span>
* <span data-ttu-id="142b1-128">提供您自己的應用程式或共用我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="142b1-128">Bring your own apps or share ours.</span></span> <span data-ttu-id="142b1-129">您可以使用自訂映像 (從 Azure VM 建立) 或您訂用帳戶隨附的其中一個映像。</span><span class="sxs-lookup"><span data-stu-id="142b1-129">You can use a custom image (built from an Azure VM) or one of the images included with your subscription.</span></span>
* <span data-ttu-id="142b1-130">您不需要設定集合與內部部署的網域之間的連線。</span><span class="sxs-lookup"><span data-stu-id="142b1-130">You don't need to configure a connection between your collection and your on-premises domain.</span></span>
* <span data-ttu-id="142b1-131">但您可以選擇使用自己的 Azure VNET 為您的內部部署環境提供存取方式以共用資料，或對資源 (如 SQL Server) 使用非 Windows 驗證 (使用資料庫驗證)。</span><span class="sxs-lookup"><span data-stu-id="142b1-131">But you can optionally use your own Azure VNET to provide access into your on-premises environment for data sharing or to use non-Windows authentication into resources like SQL Server (using database authentication).</span></span>

<span data-ttu-id="142b1-132">那麼，要怎麼建立？</span><span class="sxs-lookup"><span data-stu-id="142b1-132">Ok, how do I create one?</span></span>

* <span data-ttu-id="142b1-133">僅限雲端使用嗎？</span><span class="sxs-lookup"><span data-stu-id="142b1-133">Cloud only?</span></span> <span data-ttu-id="142b1-134">使用入口網站中的 [快速建立]  選項建立。</span><span class="sxs-lookup"><span data-stu-id="142b1-134">Create with the **Quick Create** option in the portal.</span></span>
* <span data-ttu-id="142b1-135">雲端 + VNET？</span><span class="sxs-lookup"><span data-stu-id="142b1-135">Cloud + VNET?</span></span> <span data-ttu-id="142b1-136">使用 [使用 VNET 建立]  選項建立，但「不要」選擇加入網域。</span><span class="sxs-lookup"><span data-stu-id="142b1-136">Create using the **Create with VNET** option but do NOT choose to join a domain.</span></span>

## <a name="hybrid-collections"></a><span data-ttu-id="142b1-137">混合式集合</span><span class="sxs-lookup"><span data-stu-id="142b1-137">Hybrid collections</span></span>
* <span data-ttu-id="142b1-138">提供內部部署網路 + Azure VNET 的完整存取權限。</span><span class="sxs-lookup"><span data-stu-id="142b1-138">Provide full access to on-premises network + Azure VNET.</span></span>
* <span data-ttu-id="142b1-139">包含應用程式和資料的網域加入存取權限。</span><span class="sxs-lookup"><span data-stu-id="142b1-139">Includes domain join access for apps and data.</span></span> <span data-ttu-id="142b1-140">遠端應用程式可以向您內部部署的 Active Directory 驗證 - 接著便能存取您網域中的資源。</span><span class="sxs-lookup"><span data-stu-id="142b1-140">Remote applications can authentication against your on-premises Active Directory - they can then access resources in your domain.</span></span>
* <span data-ttu-id="142b1-141">以現有的 System Center 解決方案和 Windows 群組原則啟用進階監視和管理功能 (透過在 Windows Server 2012 R2 上建置的自訂映像)</span><span class="sxs-lookup"><span data-stu-id="142b1-141">Enable advanced monitoring and management with existing System Center solutions and Windows Group Policies (through a custom image built on Windows Server 2012 R2)</span></span>
* <span data-ttu-id="142b1-142">支援 [ExpressRoute](https://azure.microsoft.com/services/expressroute/) ，可將您的 Azure VNET 連線到本機 VNET。</span><span class="sxs-lookup"><span data-stu-id="142b1-142">Support [ExpressRoute](https://azure.microsoft.com/services/expressroute/) to connect your Azure VNET to your local VNET.</span></span>

<span data-ttu-id="142b1-143">使用 [使用 VNET 建立]  選項建立，並「選擇」加入網域。</span><span class="sxs-lookup"><span data-stu-id="142b1-143">Create using the **Create with VNET** option and DO choose to join a domain.</span></span>

## <a name="authentication-options"></a><span data-ttu-id="142b1-144">驗證選項</span><span class="sxs-lookup"><span data-stu-id="142b1-144">Authentication options</span></span>
<span data-ttu-id="142b1-145">Azure RemoteApp 支援 Microsoft 帳戶和 Azure Active Directory 帳戶，但並非所有集合都支援所有方法。</span><span class="sxs-lookup"><span data-stu-id="142b1-145">Azure RemoteApp supports both Microsoft accounts and Azure Active Directory accounts, but not all collections support all methods.</span></span> 

| <span data-ttu-id="142b1-146">帳戶類型</span><span class="sxs-lookup"><span data-stu-id="142b1-146">Account type</span></span> |  | <span data-ttu-id="142b1-147">雲端</span><span class="sxs-lookup"><span data-stu-id="142b1-147">Cloud</span></span> | <span data-ttu-id="142b1-148">雲端 + VNET</span><span class="sxs-lookup"><span data-stu-id="142b1-148">Cloud + VNET</span></span> | <span data-ttu-id="142b1-149">混合式</span><span class="sxs-lookup"><span data-stu-id="142b1-149">Hybrid</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="142b1-150">Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="142b1-150">Microsoft Account</span></span> | |<span data-ttu-id="142b1-151">是</span><span class="sxs-lookup"><span data-stu-id="142b1-151">Yes</span></span> |<span data-ttu-id="142b1-152">是</span><span class="sxs-lookup"><span data-stu-id="142b1-152">Yes</span></span> |<span data-ttu-id="142b1-153">否</span><span class="sxs-lookup"><span data-stu-id="142b1-153">No</span></span> |
| <span data-ttu-id="142b1-154">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="142b1-154">Azure Active Directory (Azure AD)</span></span> | | | | |
| <span data-ttu-id="142b1-155">僅限 Azure AD 使用</span><span class="sxs-lookup"><span data-stu-id="142b1-155">Azure AD only</span></span> |<span data-ttu-id="142b1-156">是</span><span class="sxs-lookup"><span data-stu-id="142b1-156">Yes</span></span> |<span data-ttu-id="142b1-157">是</span><span class="sxs-lookup"><span data-stu-id="142b1-157">Yes</span></span> |<span data-ttu-id="142b1-158">否</span><span class="sxs-lookup"><span data-stu-id="142b1-158">No</span></span> | |
| <span data-ttu-id="142b1-159">具有密碼同步的 AD Connect</span><span class="sxs-lookup"><span data-stu-id="142b1-159">AD Connect with password sync</span></span> |<span data-ttu-id="142b1-160">是</span><span class="sxs-lookup"><span data-stu-id="142b1-160">Yes</span></span> |<span data-ttu-id="142b1-161">是</span><span class="sxs-lookup"><span data-stu-id="142b1-161">Yes</span></span> |<span data-ttu-id="142b1-162">是</span><span class="sxs-lookup"><span data-stu-id="142b1-162">Yes</span></span> | |
| <span data-ttu-id="142b1-163">不具密碼同步的 AD Connect</span><span class="sxs-lookup"><span data-stu-id="142b1-163">AD Connect without password sync</span></span> |<span data-ttu-id="142b1-164">是</span><span class="sxs-lookup"><span data-stu-id="142b1-164">Yes</span></span> |<span data-ttu-id="142b1-165">是</span><span class="sxs-lookup"><span data-stu-id="142b1-165">Yes</span></span> |<span data-ttu-id="142b1-166">否</span><span class="sxs-lookup"><span data-stu-id="142b1-166">No</span></span> | |
| <span data-ttu-id="142b1-167">具 AD FS 的 AD Connect</span><span class="sxs-lookup"><span data-stu-id="142b1-167">AD Connect with AD FS</span></span> |<span data-ttu-id="142b1-168">是</span><span class="sxs-lookup"><span data-stu-id="142b1-168">Yes</span></span> |<span data-ttu-id="142b1-169">是</span><span class="sxs-lookup"><span data-stu-id="142b1-169">Yes</span></span> |<span data-ttu-id="142b1-170">是</span><span class="sxs-lookup"><span data-stu-id="142b1-170">Yes</span></span> | |
| <span data-ttu-id="142b1-171">Azure 支援的第三方識別提供者 (例如 Ping)</span><span class="sxs-lookup"><span data-stu-id="142b1-171">3rd-party Azure-supported identity providers (such as Ping)</span></span> |<span data-ttu-id="142b1-172">是</span><span class="sxs-lookup"><span data-stu-id="142b1-172">Yes</span></span> |<span data-ttu-id="142b1-173">是</span><span class="sxs-lookup"><span data-stu-id="142b1-173">Yes</span></span> |<span data-ttu-id="142b1-174">是</span><span class="sxs-lookup"><span data-stu-id="142b1-174">Yes</span></span> | |
| <span data-ttu-id="142b1-175">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="142b1-175">Multi-Factor Authentication</span></span> | |<span data-ttu-id="142b1-176">是</span><span class="sxs-lookup"><span data-stu-id="142b1-176">Yes</span></span> |<span data-ttu-id="142b1-177">是</span><span class="sxs-lookup"><span data-stu-id="142b1-177">Yes</span></span> |<span data-ttu-id="142b1-178">是</span><span class="sxs-lookup"><span data-stu-id="142b1-178">Yes</span></span> |

### <a name="cloud-and-cloud--vnet"></a><span data-ttu-id="142b1-179">雲端和雲端 + VNET</span><span class="sxs-lookup"><span data-stu-id="142b1-179">Cloud and Cloud + VNET</span></span>
<span data-ttu-id="142b1-180">使用雲端集合時，您可以使用 Microsoft 帳戶、Azure AD 帳戶或混合使用兩者。</span><span class="sxs-lookup"><span data-stu-id="142b1-180">With cloud collections, you can use Microsoft accounts, Azure AD accounts, or a mix of the two.</span></span> <span data-ttu-id="142b1-181">使用您的使用者最適合的帳戶。</span><span class="sxs-lookup"><span data-stu-id="142b1-181">Use the accounts that work best for your users.</span></span>

<span data-ttu-id="142b1-182">使用 Microsoft 帳戶沒有任何明確要求。</span><span class="sxs-lookup"><span data-stu-id="142b1-182">There are no specific requirements for using Microsoft accounts.</span></span> 

<span data-ttu-id="142b1-183">如果您想要使用 Azure AD 帳戶，您必須確定您的 Azure AD 租用戶符合與您的訂用帳戶關聯的租用戶。</span><span class="sxs-lookup"><span data-stu-id="142b1-183">If you want to use Azure AD accounts, you need to make sure that your Azure AD tenant matches the one associated with your subscription.</span></span> <span data-ttu-id="142b1-184">當您建立 Azure RemoteApp 訂用帳戶時，您使用的 Azure AD 租用戶已自動與該訂用帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="142b1-184">When you created your Azure RemoteApp subscription, the Azure AD tenant you were using was automatically associated with your subscription.</span></span> <span data-ttu-id="142b1-185">您授與權限的任一 Azure AD 使用者都必須是該租用戶。</span><span class="sxs-lookup"><span data-stu-id="142b1-185">Any Azure AD user you give permission to needs to be that same tenant.</span></span> <span data-ttu-id="142b1-186">如有需要，您可以 [變更 Azure AD 租用戶](remoteapp-changetenant.md) (與您的訂用帳戶關聯的 Azure AD 租用戶)。</span><span class="sxs-lookup"><span data-stu-id="142b1-186">If needed, you can [change the Azure AD tenant](remoteapp-changetenant.md) associated with your subscription.</span></span>

### <a name="hybrid-or-cloud--azure-ad--ad"></a><span data-ttu-id="142b1-187">混合式 (或雲端 + Azure AD + AD)</span><span class="sxs-lookup"><span data-stu-id="142b1-187">Hybrid (or cloud + Azure AD + AD)</span></span>
<span data-ttu-id="142b1-188">使用 Azure AD + 內部部署 Active Directory 是混合式集合的必要條件。</span><span class="sxs-lookup"><span data-stu-id="142b1-188">Using Azure AD + on-premises Active Directory is a prerequisite for a hybrid collection.</span></span> <span data-ttu-id="142b1-189">您需要使用 AD Connect 來整合兩個目錄。</span><span class="sxs-lookup"><span data-stu-id="142b1-189">You need to use AD Connect to integrate the two directories.</span></span> <span data-ttu-id="142b1-190">但是您可以自行選擇如何設定 AD Connect。</span><span class="sxs-lookup"><span data-stu-id="142b1-190">But you do have some choice when it comes to how you configure AD Connect.</span></span> 

<span data-ttu-id="142b1-191">AD Connect 有兩種案例 - 使用密碼同步化或使用 AD 同盟。</span><span class="sxs-lookup"><span data-stu-id="142b1-191">There are 2 AD Connect scenarios - using password synchronization or using AD federation.</span></span> <span data-ttu-id="142b1-192">請參閱 [AD Connect 資訊](../active-directory/active-directory-aadconnect.md) ，了解哪一種案例最適合您。</span><span class="sxs-lookup"><span data-stu-id="142b1-192">Check out the [AD Connect information](../active-directory/active-directory-aadconnect.md) to figure out which of these works best for you.</span></span>

<span data-ttu-id="142b1-193">您也可以使用 Azure AD + AD 搭配雲端集合。</span><span class="sxs-lookup"><span data-stu-id="142b1-193">You can also use Azure AD + AD with a cloud collection.</span></span> <span data-ttu-id="142b1-194">請確定您有遵循相同的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="142b1-194">Make sure you follow the same set up steps.</span></span>

<span data-ttu-id="142b1-195">如需設定 Azure AD 和 Active Directory 所需的步驟，請參閱 [Azure RemoteApp 的 Azure AD + Active Directory 需求](remoteapp-ad.md) 。</span><span class="sxs-lookup"><span data-stu-id="142b1-195">Check out [Azure AD + Active Directory requirements for Azure RemoteApp](remoteapp-ad.md) for the steps required to configure Azure AD and Active Directory.</span></span>

## <a name="go-create-your-collection"></a><span data-ttu-id="142b1-196">立即建立您的集合！</span><span class="sxs-lookup"><span data-stu-id="142b1-196">Go create your collection!</span></span>
<span data-ttu-id="142b1-197">嗯，我想我們現在已經說明白了，那麼只剩下一件事要做 - 建立您的第一個 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="142b1-197">Ok, I think we've figured it out now, so there's just one thing left to do - create your first Azure RemoteApp collection.</span></span>

<span data-ttu-id="142b1-198">[建立雲端集合](remoteapp-create-cloud-deployment.md)或[建立混合式集合](remoteapp-create-hybrid-deployment.md) -立即建立。</span><span class="sxs-lookup"><span data-stu-id="142b1-198">[Create a cloud collection](remoteapp-create-cloud-deployment.md) or [create a hybrid collection](remoteapp-create-hybrid-deployment.md) - just get creating.</span></span>

