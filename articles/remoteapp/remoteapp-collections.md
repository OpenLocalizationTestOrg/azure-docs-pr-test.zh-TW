---
title: "您需要的 Azure RemoteApp aaaWhat 種集合嗎？ | Microsoft Docs"
description: "深入了解 hello 種集合類型與 Azure RemoteApp 一起使用。"
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
ms.openlocfilehash: f00b5fe41af597cf75e26300bf7842c3a8ff94fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a><span data-ttu-id="f32b2-104">Azure RemoteApp 需要何種集合？</span><span class="sxs-lookup"><span data-stu-id="f32b2-104">What kind of collection do you need for Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f32b2-105">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="f32b2-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f32b2-106">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f32b2-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f32b2-107">Azure RemoteApp 可讓您在任何裝置上與使用者共用應用程式和資源。</span><span class="sxs-lookup"><span data-stu-id="f32b2-107">Azure RemoteApp lets you share apps and resources with users on any device.</span></span> <span data-ttu-id="f32b2-108">要執行此作業建立集合 toohold hello 應用程式及資源，並接著與使用者共用這些集合。</span><span class="sxs-lookup"><span data-stu-id="f32b2-108">We do this by creating collections toohold hello apps and resources, and then you share those collections with users.</span></span> <span data-ttu-id="f32b2-109">有兩個不同的集合選項，各有不同的網路和驗證選項 - 哪一種最適合您？</span><span class="sxs-lookup"><span data-stu-id="f32b2-109">There are 2 different collection options, with different network and authentication options - which is right for you?</span></span>

<span data-ttu-id="f32b2-110">讓我們逐步 hello 不同考量和選項，您需要 toomake tooget hello 最超出您的 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="f32b2-110">Let's walk through hello different considerations and choices you need toomake tooget hello most out of your Azure RemoteApp collection.</span></span> 

## <a name="quick-differences-between-hello-collection-types"></a><span data-ttu-id="f32b2-111">快速 hello 集合型別之間的差異</span><span class="sxs-lookup"><span data-stu-id="f32b2-111">Quick differences between hello collection types</span></span>
|  | <span data-ttu-id="f32b2-112">雲端</span><span class="sxs-lookup"><span data-stu-id="f32b2-112">Cloud</span></span> | <span data-ttu-id="f32b2-113">混合式</span><span class="sxs-lookup"><span data-stu-id="f32b2-113">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f32b2-114">使用現有的 VNET</span><span class="sxs-lookup"><span data-stu-id="f32b2-114">Use an existing VNET</span></span> |<span data-ttu-id="f32b2-115">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-115">Yes</span></span> |<span data-ttu-id="f32b2-116">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-116">Yes</span></span> |
| <span data-ttu-id="f32b2-117">需要連線到 AD 的帳戶 (DirSync)</span><span class="sxs-lookup"><span data-stu-id="f32b2-117">Requires AD-connected accounts (DirSync)</span></span> |<span data-ttu-id="f32b2-118">否</span><span class="sxs-lookup"><span data-stu-id="f32b2-118">No</span></span> |<span data-ttu-id="f32b2-119">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-119">Yes</span></span> |
| <span data-ttu-id="f32b2-120">需要加入網域</span><span class="sxs-lookup"><span data-stu-id="f32b2-120">Requires domain join</span></span> |<span data-ttu-id="f32b2-121">否</span><span class="sxs-lookup"><span data-stu-id="f32b2-121">No</span></span> |<span data-ttu-id="f32b2-122">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-122">Yes</span></span> |
| <span data-ttu-id="f32b2-123">需要網域控制站可存取 tooVNET</span><span class="sxs-lookup"><span data-stu-id="f32b2-123">Requires domain controller accessible tooVNET</span></span> |<span data-ttu-id="f32b2-124">否</span><span class="sxs-lookup"><span data-stu-id="f32b2-124">No</span></span> |<span data-ttu-id="f32b2-125">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-125">Yes</span></span> |

## <a name="cloud-collections"></a><span data-ttu-id="f32b2-126">雲端集合</span><span class="sxs-lookup"><span data-stu-id="f32b2-126">Cloud collections</span></span>
* <span data-ttu-id="f32b2-127">快速 toocreate-hello 集合的快速佈建，這表示您的應用程式取得 toousers 速度較快。</span><span class="sxs-lookup"><span data-stu-id="f32b2-127">Quick toocreate - hello collection is quickly provisioned, meaning your apps get toousers quicker.</span></span>
* <span data-ttu-id="f32b2-128">提供您自己的應用程式或共用我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f32b2-128">Bring your own apps or share ours.</span></span> <span data-ttu-id="f32b2-129">您可以使用自訂映像 （內建的 Azure VM） 或其中一個 hello 映像包含您訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f32b2-129">You can use a custom image (built from an Azure VM) or one of hello images included with your subscription.</span></span>
* <span data-ttu-id="f32b2-130">您不需要 tooconfigure 連接您的集合與您在內部部署的網域之間。</span><span class="sxs-lookup"><span data-stu-id="f32b2-130">You don't need tooconfigure a connection between your collection and your on-premises domain.</span></span>
* <span data-ttu-id="f32b2-131">但是，您可以選擇性地使用您自己的 Azure VNET tooprovide 存取至內部部署環境到資源，例如 SQL Server （使用資料庫驗證） 的資料共用或 toouse 非 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="f32b2-131">But you can optionally use your own Azure VNET tooprovide access into your on-premises environment for data sharing or toouse non-Windows authentication into resources like SQL Server (using database authentication).</span></span>

<span data-ttu-id="f32b2-132">那麼，要怎麼建立？</span><span class="sxs-lookup"><span data-stu-id="f32b2-132">Ok, how do I create one?</span></span>

* <span data-ttu-id="f32b2-133">僅限雲端使用嗎？</span><span class="sxs-lookup"><span data-stu-id="f32b2-133">Cloud only?</span></span> <span data-ttu-id="f32b2-134">建立以 hello**快速建立**hello 入口網站中的選項。</span><span class="sxs-lookup"><span data-stu-id="f32b2-134">Create with hello **Quick Create** option in hello portal.</span></span>
* <span data-ttu-id="f32b2-135">雲端 + VNET？</span><span class="sxs-lookup"><span data-stu-id="f32b2-135">Cloud + VNET?</span></span> <span data-ttu-id="f32b2-136">建立使用 hello**使用 VNET 建立**選項，但不是選擇 toojoin 網域。</span><span class="sxs-lookup"><span data-stu-id="f32b2-136">Create using hello **Create with VNET** option but do NOT choose toojoin a domain.</span></span>

## <a name="hybrid-collections"></a><span data-ttu-id="f32b2-137">混合式集合</span><span class="sxs-lookup"><span data-stu-id="f32b2-137">Hybrid collections</span></span>
* <span data-ttu-id="f32b2-138">提供的完整存取 tooon 內部部署網路 + Azure VNET。</span><span class="sxs-lookup"><span data-stu-id="f32b2-138">Provide full access tooon-premises network + Azure VNET.</span></span>
* <span data-ttu-id="f32b2-139">包含應用程式和資料的網域加入存取權限。</span><span class="sxs-lookup"><span data-stu-id="f32b2-139">Includes domain join access for apps and data.</span></span> <span data-ttu-id="f32b2-140">遠端應用程式可以向您內部部署的 Active Directory 驗證 - 接著便能存取您網域中的資源。</span><span class="sxs-lookup"><span data-stu-id="f32b2-140">Remote applications can authentication against your on-premises Active Directory - they can then access resources in your domain.</span></span>
* <span data-ttu-id="f32b2-141">以現有的 System Center 解決方案和 Windows 群組原則啟用進階監視和管理功能 (透過在 Windows Server 2012 R2 上建置的自訂映像)</span><span class="sxs-lookup"><span data-stu-id="f32b2-141">Enable advanced monitoring and management with existing System Center solutions and Windows Group Policies (through a custom image built on Windows Server 2012 R2)</span></span>
* <span data-ttu-id="f32b2-142">支援[ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect Azure VNET tooyour 區域 VNET。</span><span class="sxs-lookup"><span data-stu-id="f32b2-142">Support [ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect your Azure VNET tooyour local VNET.</span></span>

<span data-ttu-id="f32b2-143">建立使用 hello**使用 VNET 建立**選項，然後選擇 toojoin 網域。</span><span class="sxs-lookup"><span data-stu-id="f32b2-143">Create using hello **Create with VNET** option and DO choose toojoin a domain.</span></span>

## <a name="authentication-options"></a><span data-ttu-id="f32b2-144">驗證選項</span><span class="sxs-lookup"><span data-stu-id="f32b2-144">Authentication options</span></span>
<span data-ttu-id="f32b2-145">Azure RemoteApp 支援 Microsoft 帳戶和 Azure Active Directory 帳戶，但並非所有集合都支援所有方法。</span><span class="sxs-lookup"><span data-stu-id="f32b2-145">Azure RemoteApp supports both Microsoft accounts and Azure Active Directory accounts, but not all collections support all methods.</span></span> 

| <span data-ttu-id="f32b2-146">帳戶類型</span><span class="sxs-lookup"><span data-stu-id="f32b2-146">Account type</span></span> |  | <span data-ttu-id="f32b2-147">雲端</span><span class="sxs-lookup"><span data-stu-id="f32b2-147">Cloud</span></span> | <span data-ttu-id="f32b2-148">雲端 + VNET</span><span class="sxs-lookup"><span data-stu-id="f32b2-148">Cloud + VNET</span></span> | <span data-ttu-id="f32b2-149">混合式</span><span class="sxs-lookup"><span data-stu-id="f32b2-149">Hybrid</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="f32b2-150">Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="f32b2-150">Microsoft Account</span></span> | |<span data-ttu-id="f32b2-151">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-151">Yes</span></span> |<span data-ttu-id="f32b2-152">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-152">Yes</span></span> |<span data-ttu-id="f32b2-153">否</span><span class="sxs-lookup"><span data-stu-id="f32b2-153">No</span></span> |
| <span data-ttu-id="f32b2-154">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="f32b2-154">Azure Active Directory (Azure AD)</span></span> | | | | |
| <span data-ttu-id="f32b2-155">僅限 Azure AD 使用</span><span class="sxs-lookup"><span data-stu-id="f32b2-155">Azure AD only</span></span> |<span data-ttu-id="f32b2-156">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-156">Yes</span></span> |<span data-ttu-id="f32b2-157">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-157">Yes</span></span> |<span data-ttu-id="f32b2-158">否</span><span class="sxs-lookup"><span data-stu-id="f32b2-158">No</span></span> | |
| <span data-ttu-id="f32b2-159">具有密碼同步的 AD Connect</span><span class="sxs-lookup"><span data-stu-id="f32b2-159">AD Connect with password sync</span></span> |<span data-ttu-id="f32b2-160">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-160">Yes</span></span> |<span data-ttu-id="f32b2-161">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-161">Yes</span></span> |<span data-ttu-id="f32b2-162">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-162">Yes</span></span> | |
| <span data-ttu-id="f32b2-163">不具密碼同步的 AD Connect</span><span class="sxs-lookup"><span data-stu-id="f32b2-163">AD Connect without password sync</span></span> |<span data-ttu-id="f32b2-164">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-164">Yes</span></span> |<span data-ttu-id="f32b2-165">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-165">Yes</span></span> |<span data-ttu-id="f32b2-166">否</span><span class="sxs-lookup"><span data-stu-id="f32b2-166">No</span></span> | |
| <span data-ttu-id="f32b2-167">具 AD FS 的 AD Connect</span><span class="sxs-lookup"><span data-stu-id="f32b2-167">AD Connect with AD FS</span></span> |<span data-ttu-id="f32b2-168">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-168">Yes</span></span> |<span data-ttu-id="f32b2-169">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-169">Yes</span></span> |<span data-ttu-id="f32b2-170">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-170">Yes</span></span> | |
| <span data-ttu-id="f32b2-171">Azure 支援的第三方識別提供者 (例如 Ping)</span><span class="sxs-lookup"><span data-stu-id="f32b2-171">3rd-party Azure-supported identity providers (such as Ping)</span></span> |<span data-ttu-id="f32b2-172">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-172">Yes</span></span> |<span data-ttu-id="f32b2-173">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-173">Yes</span></span> |<span data-ttu-id="f32b2-174">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-174">Yes</span></span> | |
| <span data-ttu-id="f32b2-175">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f32b2-175">Multi-Factor Authentication</span></span> | |<span data-ttu-id="f32b2-176">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-176">Yes</span></span> |<span data-ttu-id="f32b2-177">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-177">Yes</span></span> |<span data-ttu-id="f32b2-178">是</span><span class="sxs-lookup"><span data-stu-id="f32b2-178">Yes</span></span> |

### <a name="cloud-and-cloud--vnet"></a><span data-ttu-id="f32b2-179">雲端和雲端 + VNET</span><span class="sxs-lookup"><span data-stu-id="f32b2-179">Cloud and Cloud + VNET</span></span>
<span data-ttu-id="f32b2-180">與雲端集合中，您可以使用 Microsoft 帳戶、 Azure AD 帳戶或 hello 兩者的混合。</span><span class="sxs-lookup"><span data-stu-id="f32b2-180">With cloud collections, you can use Microsoft accounts, Azure AD accounts, or a mix of hello two.</span></span> <span data-ttu-id="f32b2-181">使用最適合您的使用者的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f32b2-181">Use hello accounts that work best for your users.</span></span>

<span data-ttu-id="f32b2-182">使用 Microsoft 帳戶沒有任何明確要求。</span><span class="sxs-lookup"><span data-stu-id="f32b2-182">There are no specific requirements for using Microsoft accounts.</span></span> 

<span data-ttu-id="f32b2-183">如果您想 toouse Azure AD 帳戶，您需要確定您的 Azure AD 租用戶符合其中一個訂用帳戶相關聯的 hello toomake。</span><span class="sxs-lookup"><span data-stu-id="f32b2-183">If you want toouse Azure AD accounts, you need toomake sure that your Azure AD tenant matches hello one associated with your subscription.</span></span> <span data-ttu-id="f32b2-184">當您建立 Azure RemoteApp 訂閱後時，所使用的 hello Azure AD 租用戶已自動與您訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="f32b2-184">When you created your Azure RemoteApp subscription, hello Azure AD tenant you were using was automatically associated with your subscription.</span></span> <span data-ttu-id="f32b2-185">任何 Azure AD 使用者，您授與權限 tooneeds toobe 該相同的租用戶。</span><span class="sxs-lookup"><span data-stu-id="f32b2-185">Any Azure AD user you give permission tooneeds toobe that same tenant.</span></span> <span data-ttu-id="f32b2-186">如有需要您可以[變更 hello Azure AD 租用戶](remoteapp-changetenant.md)與您訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="f32b2-186">If needed, you can [change hello Azure AD tenant](remoteapp-changetenant.md) associated with your subscription.</span></span>

### <a name="hybrid-or-cloud--azure-ad--ad"></a><span data-ttu-id="f32b2-187">混合式 (或雲端 + Azure AD + AD)</span><span class="sxs-lookup"><span data-stu-id="f32b2-187">Hybrid (or cloud + Azure AD + AD)</span></span>
<span data-ttu-id="f32b2-188">使用 Azure AD + 內部部署 Active Directory 是混合式集合的必要條件。</span><span class="sxs-lookup"><span data-stu-id="f32b2-188">Using Azure AD + on-premises Active Directory is a prerequisite for a hybrid collection.</span></span> <span data-ttu-id="f32b2-189">您需要 toouse AD Connect toointegrate hello 兩個目錄。</span><span class="sxs-lookup"><span data-stu-id="f32b2-189">You need toouse AD Connect toointegrate hello two directories.</span></span> <span data-ttu-id="f32b2-190">但當您設定 AD Connect toohow 需要某些選擇。</span><span class="sxs-lookup"><span data-stu-id="f32b2-190">But you do have some choice when it comes toohow you configure AD Connect.</span></span> 

<span data-ttu-id="f32b2-191">AD Connect 有兩種案例 - 使用密碼同步化或使用 AD 同盟。</span><span class="sxs-lookup"><span data-stu-id="f32b2-191">There are 2 AD Connect scenarios - using password synchronization or using AD federation.</span></span> <span data-ttu-id="f32b2-192">簽出 hello [AD Connect 資訊](../active-directory/active-directory-aadconnect.md)toofigure 其中出最適合您。</span><span class="sxs-lookup"><span data-stu-id="f32b2-192">Check out hello [AD Connect information](../active-directory/active-directory-aadconnect.md) toofigure out which of these works best for you.</span></span>

<span data-ttu-id="f32b2-193">您也可以使用 Azure AD + AD 搭配雲端集合。</span><span class="sxs-lookup"><span data-stu-id="f32b2-193">You can also use Azure AD + AD with a cloud collection.</span></span> <span data-ttu-id="f32b2-194">請確定您遵循相同的設定步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="f32b2-194">Make sure you follow hello same set up steps.</span></span>

<span data-ttu-id="f32b2-195">簽出[Azure AD + 的 Azure RemoteApp 的 Active Directory 需求](remoteapp-ad.md)hello 步驟需要的 tooconfigure Azure AD 和 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="f32b2-195">Check out [Azure AD + Active Directory requirements for Azure RemoteApp](remoteapp-ad.md) for hello steps required tooconfigure Azure AD and Active Directory.</span></span>

## <a name="go-create-your-collection"></a><span data-ttu-id="f32b2-196">立即建立您的集合！</span><span class="sxs-lookup"><span data-stu-id="f32b2-196">Go create your collection!</span></span>
<span data-ttu-id="f32b2-197">好了，我認為我們已經知道它現在，因此只有一個項目左邊的 toodo-建立您的第一個 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="f32b2-197">Ok, I think we've figured it out now, so there's just one thing left toodo - create your first Azure RemoteApp collection.</span></span>

<span data-ttu-id="f32b2-198">[建立雲端集合](remoteapp-create-cloud-deployment.md)或[建立混合式集合](remoteapp-create-hybrid-deployment.md) -立即建立。</span><span class="sxs-lookup"><span data-stu-id="f32b2-198">[Create a cloud collection](remoteapp-create-cloud-deployment.md) or [create a hybrid collection](remoteapp-create-hybrid-deployment.md) - just get creating.</span></span>

