---
title: "在 Azure Active Directory 群組 aaaResolve 授權問題 |Microsoft 文件"
description: "如何 tooidentify 並解決授權指派問題時您正在使用 Azure Active Directory 群組授權"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ec9c74214a9e246f21fcf767b0bbd586ae702445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a><span data-ttu-id="cf1e5-104">識別及解決 Azure Active Directory 中群組的授權指派問題</span><span class="sxs-lookup"><span data-stu-id="cf1e5-104">Identify and resolve license assignment problems for a group in Azure Active Directory</span></span>

<span data-ttu-id="cf1e5-105">群組為基礎授權 Azure Active Directory (Azure AD) 中引進使用者授權的錯誤狀態中的 hello 的概念。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-105">Group-based licensing in Azure Active Directory (Azure AD) introduces hello concept of users in a licensing error state.</span></span> <span data-ttu-id="cf1e5-106">在本文中，我們會說明為什麼使用者可能會結束此狀態中的 hello 原因。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-106">In this article, we explain hello reasons why users might end up in this state.</span></span>

<span data-ttu-id="cf1e5-107">當您將授權指派直接 tooindividual 使用者，而不需使用以群組為基礎的授權時，hello 分派作業可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-107">When you assign licenses directly tooindividual users, without using group-based licensing, hello assignment operation might fail.</span></span> <span data-ttu-id="cf1e5-108">例如，當您執行 hello PowerShell cmdlet`Set-MsolUserLicense`使用者，hello cmdlet 可以失敗的數目不相關的 toobusiness 邏輯的原因。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-108">For example, when you execute hello PowerShell cmdlet `Set-MsolUserLicense` on a user, hello cmdlet can fail for a number of reasons that are related toobusiness logic.</span></span> <span data-ttu-id="cf1e5-109">例如，可能會有授權或無法同時指派 hello 相同的兩個服務方案之間的衝突數目不足時間。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-109">For example, there might be an insufficient number of licenses or a conflict between two service plans that can't be assigned at hello same time.</span></span> <span data-ttu-id="cf1e5-110">hello 報告的問題時立即回 tooyou。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-110">hello problem is immediately reported back tooyou.</span></span>

<span data-ttu-id="cf1e5-111">當您使用以群組為基礎授權、 hello 可能會發生相同錯誤，但它們會在 hello 背景 hello Azure AD 服務會指派授權時。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-111">When you're using group-based licensing, hello same errors can occur, but they happen in hello background when hello Azure AD service is assigning licenses.</span></span> <span data-ttu-id="cf1e5-112">基於這個理由，hello 錯誤無法立即被溝通的 tooyou。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-112">For this reason, hello errors can't be communicated tooyou immediately.</span></span> <span data-ttu-id="cf1e5-113">相反地，它們是記錄在 hello 使用者物件上且然後經由 hello 系統管理網站回報。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-113">Instead, they're recorded on hello user object and then reported via hello administrative portal.</span></span> <span data-ttu-id="cf1e5-114">請注意，hello 原始意圖 toolicense hello 使用者不會遺失，它會記錄在未來進行調查並解決錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-114">Note that hello original intent toolicense hello user is never lost, but it's recorded in an error state for future investigation and resolution.</span></span>

## <a name="how-toofind-license-assignment-errors"></a><span data-ttu-id="cf1e5-115">如何 toofind 授權指派錯誤</span><span class="sxs-lookup"><span data-stu-id="cf1e5-115">How toofind license assignment errors</span></span>

1. <span data-ttu-id="cf1e5-116">在特定群組中的錯誤狀態中，開啟 hello 刀鋒視窗中的 hello 群組 toofind 使用者。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-116">toofind users in an error state in a specific group, open hello blade for hello group.</span></span> <span data-ttu-id="cf1e5-117">[授權] 底下會有一份通知，顯示是否有任何使用者處於錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-117">Under **Licenses**, there will be a notification displayed if there are any users in an error state.</span></span>

![群組，錯誤通知](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. <span data-ttu-id="cf1e5-119">按一下 hello 通知 tooopen 的所有受影響的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-119">Click hello notification tooopen a list of all affected users.</span></span> <span data-ttu-id="cf1e5-120">您可以個別按一下每個使用者 toosee 更多詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-120">You can click on each user individually toosee more details.</span></span>

![群組，處於錯誤狀態的使用者清單](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. <span data-ttu-id="cf1e5-122">toofind 所有群組包含至少一個錯誤，在 hello **Azure Active Directory**刀鋒視窗選取**授權**然後**概觀**。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-122">toofind all groups that contain at least one error, on hello **Azure Active Directory** blade select **Licenses** and then **Overview**.</span></span> <span data-ttu-id="cf1e5-123">某些群組需要您注意時，會顯示資訊方塊。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-123">An info box is displayed when some groups require your attention.</span></span>

![概觀，處於錯誤狀態的群組相關資訊](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. <span data-ttu-id="cf1e5-125">按一下 hello 方塊 toosee 錯誤的所有群組的清單。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-125">Click on hello box toosee a list of all groups with errors.</span></span> <span data-ttu-id="cf1e5-126">您可以按一下每個群組以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-126">You can click each group for more details.</span></span>

![概觀，具有錯誤的群組清單](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


<span data-ttu-id="cf1e5-128">以下是每個潛在的問題和 hello 方式 tooresolve 描述它。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-128">Below is a description of each potential problem and hello way tooresolve it.</span></span>

## <a name="not-enough-licenses"></a><span data-ttu-id="cf1e5-129">沒有足夠的授權</span><span class="sxs-lookup"><span data-stu-id="cf1e5-129">Not enough licenses</span></span>

<span data-ttu-id="cf1e5-130">**問題：**沒有足夠的可用授權的其中一個指定 hello 群組中的 hello 產品。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-130">**Problem:** There aren't enough available licenses for one of hello products that's specified in hello group.</span></span> <span data-ttu-id="cf1e5-131">您需要 tooeither 購買更多授權 hello 的產品，或釋放未使用授權其他使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-131">You need tooeither purchase more licenses for hello product, or free up unused licenses from other users or groups.</span></span>

<span data-ttu-id="cf1e5-132">toosee 多少授權可用，請移過**Azure Active Directory** > **授權** > **所有產品**。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-132">toosee how many licenses are available, go too**Azure Active Directory** > **Licenses** > **All products**.</span></span>

<span data-ttu-id="cf1e5-133">toosee 哪些使用者和群組會使用授權，按一下 [產品]。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-133">toosee which users and groups are consuming licenses, click a product.</span></span> <span data-ttu-id="cf1e5-134">在 [已授權的使用者] 底下，您會看到其授權已直接指派或透過一或多個群組指派的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-134">Under **Licensed users**, you'll see all users who've had licenses assigned directly or via one or more groups.</span></span> <span data-ttu-id="cf1e5-135">在 [已授權的群組] 底下，您會看到已被指派該產品的所有群組。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-135">Under **Licensed groups**, you'll see all groups that have that product assigned.</span></span>

<span data-ttu-id="cf1e5-136">**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _CountViolation_。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-136">**PowerShell:** PowerShell cmdlets report this error as _CountViolation_.</span></span>

## <a name="conflicting-service-plans"></a><span data-ttu-id="cf1e5-137">衝突的服務方案</span><span class="sxs-lookup"><span data-stu-id="cf1e5-137">Conflicting service plans</span></span>

<span data-ttu-id="cf1e5-138">**問題：** hello 產品 hello 群組中所指定的其中一個包含已指派的 toohello 使用者透過不同的產品的另一個服務計劃與衝突的服務方案。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-138">**Problem:** One of hello products that's specified in hello group contains a service plan that conflicts with another service plan that's already assigned toohello user via a different product.</span></span> <span data-ttu-id="cf1e5-139">它們不能指派 toohello 的方式設定某些服務的方案相同的其他相關的服務方案的使用者。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-139">Some service plans are configured in a way that they can't be assigned toohello same user as another related service plan.</span></span>

<span data-ttu-id="cf1e5-140">請考慮下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-140">Consider hello following example.</span></span> <span data-ttu-id="cf1e5-141">使用者有 Office 365 企業版授權**E1**直接指派給所有啟用的 hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-141">A user has a license for Office 365 Enterprise **E1** assigned directly, with all hello plans enabled.</span></span> <span data-ttu-id="cf1e5-142">新增 hello 使用者具有 Office 365 企業版的 hello tooa 群組**E3**產品指派 tooit。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-142">hello user has been added tooa group that has hello Office 365 Enterprise **E3** product assigned tooit.</span></span> <span data-ttu-id="cf1e5-143">本產品包含具有 hello 計劃包含在 E1、 hello 群組授權指派將失敗 hello 」 衝突服務計劃 」 錯誤，因此不能重疊的服務方案。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-143">This product contains service plans that can't overlap with hello plans included in E1, so hello group license assignment will fail with hello “Conflicting service plans” error.</span></span> <span data-ttu-id="cf1e5-144">在此範例中，為 hello 衝突的服務方案：</span><span class="sxs-lookup"><span data-stu-id="cf1e5-144">In this example, hello conflicting service plans are:</span></span>

-   <span data-ttu-id="cf1e5-145">SharePoint Online (方案 2) 與 SharePoint Online (方案 1) 衝突。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-145">SharePoint Online (Plan 2) conflicts with SharePoint Online (Plan 1).</span></span>
-   <span data-ttu-id="cf1e5-146">Exchange Online (方案 2) 與 Exchange Online (方案 1) 衝突。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-146">Exchange Online (Plan 2) conflicts with Exchange Online (Plan 1).</span></span>

<span data-ttu-id="cf1e5-147">toosolve 這項衝突，您需要 toodisable hello E1 上授權的直接指派的 toohello 使用者的兩個方案。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-147">toosolve this conflict, you need toodisable those two plans either on hello E1 license that's directly assigned toohello user.</span></span> <span data-ttu-id="cf1e5-148">或者，您需要 toomodify hello 整個群組的授權指派，並停用 hello E3 授權中的 hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-148">Or, you need toomodify hello entire group license assignment and disable hello plans in hello E3 license.</span></span> <span data-ttu-id="cf1e5-149">或者，您可能決定 tooremove hello E1 授權 hello 使用者如果備援 hello hello E3 授權內容中。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-149">Alternatively, you might decide tooremove hello E1 license from hello user if it's redundant in hello context of hello E3 license.</span></span>

<span data-ttu-id="cf1e5-150">hello 決定如何 tooresolve 衝突產品授權一律屬於 toohello 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-150">hello decision about how tooresolve conflicting product licenses always belongs toohello administrator.</span></span> <span data-ttu-id="cf1e5-151">Azure AD 不會自動解決授權衝突。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-151">Azure AD doesn't automatically resolve license conflicts.</span></span>

<span data-ttu-id="cf1e5-152">**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _MutuallyExclusiveViolation_。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-152">**PowerShell:** PowerShell cmdlets report this error as _MutuallyExclusiveViolation_.</span></span>

## <a name="other-products-depend-on-this-license"></a><span data-ttu-id="cf1e5-153">其他產品相依於此授權</span><span class="sxs-lookup"><span data-stu-id="cf1e5-153">Other products depend on this license</span></span>

<span data-ttu-id="cf1e5-154">**問題：** hello 產品 hello 群組中所指定的其中一個包含您必須啟用另一個服務計劃，另一個產品，函式中的服務方案。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-154">**Problem:** One of hello products that's specified in hello group contains a service plan that must be enabled for another service plan, in another product, to function.</span></span> <span data-ttu-id="cf1e5-155">Azure AD 嘗試 tooremove hello 基礎服務計劃時，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-155">This error occurs when Azure AD attempts tooremove hello underlying service plan.</span></span> <span data-ttu-id="cf1e5-156">比方說，這種情形 hello 使用者正在從 hello 群組中移除。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-156">For example, this can happen as a result of hello user being removed from hello group.</span></span>

<span data-ttu-id="cf1e5-157">toosolve 這個問題，您將需要 toomake 確定 toousers 透過其他方法，或 hello 相依服務已停用這些使用者仍指派該 hello 需要計劃。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-157">toosolve this problem, you'll need toomake sure that hello required plan is still assigned toousers through some other method, or that hello dependent services are disabled for those users.</span></span> <span data-ttu-id="cf1e5-158">執行這個動作之後, 可以正確 hello 群組授權移除這些使用者。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-158">After doing that, you can properly remove hello group license from those users.</span></span>

<span data-ttu-id="cf1e5-159">**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _DependencyViolation_。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-159">**PowerShell:** PowerShell cmdlets report this error as _DependencyViolation_.</span></span>

## <a name="usage-location-isnt-allowed"></a><span data-ttu-id="cf1e5-160">不允許使用位置</span><span class="sxs-lookup"><span data-stu-id="cf1e5-160">Usage location isn't allowed</span></span>

<span data-ttu-id="cf1e5-161">**問題：**由於當地法律和法規，無法在所有位置使用某些 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-161">**Problem:** Some Microsoft services aren't available in all locations because of local laws and regulations.</span></span> <span data-ttu-id="cf1e5-162">您可以指派授權 tooa 使用者之前，您必須為 hello 使用者 toospecify hello 「 使用量位置 」 屬性。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-162">Before you can assign a license tooa user, you have toospecify hello “Usage location” property for hello user.</span></span> <span data-ttu-id="cf1e5-163">您可以在 hello**使用者** > **設定檔** > **設定**hello Azure 入口網站中的一節。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-163">You can do this under hello **User** > **Profile** > **Settings** section in hello Azure portal.</span></span>

<span data-ttu-id="cf1e5-164">當 Azure AD 會嘗試 tooassign 群組授權 tooa 使用者的使用位置不受支援時，它將會失敗，而且這個 hello 使用者的錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-164">When Azure AD attempts tooassign a group license tooa user whose usage location isn't supported, it will fail and record this error on hello user.</span></span>

<span data-ttu-id="cf1e5-165">toosolve 這個問題，請從支援的位置，從 hello 授權群組移除使用者。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-165">toosolve this problem, remove users from nonsupported locations from hello licensed group.</span></span> <span data-ttu-id="cf1e5-166">或者，如果 hello 目前使用量位置值不代表 hello 實際使用者的位置，您可以進行修改以便 hello 授權正確指派下一個階段 （如果支援 hello 新位置）。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-166">Alternatively, if hello current usage location values don't represent hello actual user location, you can modify them so that hello licenses are correctly assigned next time (if hello new location is supported).</span></span>

<span data-ttu-id="cf1e5-167">**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _ProhibitedInUsageLocationViolation_。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-167">**PowerShell:** PowerShell cmdlets report this error as _ProhibitedInUsageLocationViolation_.</span></span>

> [!NOTE]
> <span data-ttu-id="cf1e5-168">當 Azure AD 會指派給群組授權時，指定使用位置沒有任何使用者都會繼承 hello hello 目錄位置。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-168">When Azure AD assigns group licenses, any users without a usage location specified inherit hello location of hello directory.</span></span> <span data-ttu-id="cf1e5-169">我們建議系統管理員設定 hello 正確使用方式位置值上的使用者才能使用以群組為基礎的授權 toocomply 用戶所在地法律與規定。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-169">We recommend that administrators set hello correct usage location values on users before using group-based licensing toocomply with local laws and regulations.</span></span>

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a><span data-ttu-id="cf1e5-170">當群組中有一個以上的產品授權時，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="cf1e5-170">What happens when there's more than one product license on a group?</span></span>

<span data-ttu-id="cf1e5-171">您可以指派多個產品授權 tooa 群組。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-171">You can assign more than one product license tooa group.</span></span> <span data-ttu-id="cf1e5-172">例如，您可以指派 Office 365 企業版 E3 與企業行動力 + 安全性 tooa 群組 tooeasily 啟用使用者的所有內含的服務。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-172">For example, you can assign Office 365 Enterprise E3 and Enterprise Mobility + Security tooa group tooeasily enable all included services for users.</span></span>

<span data-ttu-id="cf1e5-173">Azure AD 會嘗試 tooassign hello 群組 tooeach 使用者中指定的所有授權。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-173">Azure AD attempts tooassign all licenses that are specified in hello group tooeach user.</span></span> <span data-ttu-id="cf1e5-174">如果 Azure AD 無法指定其中一個 hello 產品因為商務邏輯的問題 （例如，如果沒有足夠的授權，或與其他服務，在 hello 使用者上啟用衝突），它將不會指派 hello hello 群組中的其他授權其中一個。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-174">If Azure AD can't assign one of hello products because of business logic problems (for example, if there aren't enough licenses for all, or if there are conflicts with other services that are enabled on hello user), it won't assign hello other licenses in hello group either.</span></span>

<span data-ttu-id="cf1e5-175">您將會失敗，無法 tooget 指派的使用者可以 toosee hello 而且檢查哪些產品有已受此影響。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-175">You'll be able toosee hello users who failed tooget assigned failed and check which products have been affected by this.</span></span>

## <a name="license-assignment-fails-silently-for-a-user-due-tooduplicate-proxy-addresses-in-exchange-online"></a><span data-ttu-id="cf1e5-176">由於 tooduplicate proxy 位址，在 Exchange Online 中的使用者以無訊息模式失敗授權指派</span><span class="sxs-lookup"><span data-stu-id="cf1e5-176">License assignment fails silently for a user due tooduplicate proxy addresses in Exchange Online</span></span>

<span data-ttu-id="cf1e5-177">如果您使用 Exchange Online，您的租用戶中有些使用者可能設定不正確 hello 與相同的 proxy 位址值。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-177">If you are using Exchange Online, some users in your tenant may be incorrectly configured with hello same proxy address value.</span></span> <span data-ttu-id="cf1e5-178">當以群組為基礎的授權伺服器嘗試 tooassign 授權 toosuch 使用者時，它將會失敗並不會記錄錯誤 (不同於在 hello 上面所述的其他錯誤情況)-這是在 hello 預覽版本，這項功能的限制，我們 tooaddress前面*一般可用性*。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-178">When group-based licensing tries tooassign a license toosuch a user, it will fail and will not record an error (unlike in hello other error cases described above) - this is a limitation in hello preview version of this feature and we are going tooaddress it before *General Availability*.</span></span>

> [!TIP]
> <span data-ttu-id="cf1e5-179">如果您發現某些使用者未收到授權，且未對這些使用者記錄錯誤，請先檢查他們是否有重複的 Proxy 位址。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-179">If you notice that some users did not receive a license and there is no error recorded on those users, first check if they have duplicate proxy address.</span></span>
> <span data-ttu-id="cf1e5-180">執行下列 PowerShell 指令程式針對 Exchange Online 的 hello 可以達成此目的：</span><span class="sxs-lookup"><span data-stu-id="cf1e5-180">This can be done by executing hello following PowerShell cmdlet against Exchange Online:</span></span>
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> <span data-ttu-id="cf1e5-181">[這篇文章](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online)包含這個問題，請在包含資訊的更多詳細[如何使用遠端 PowerShell 線上 tooconnect tooExchange](https://technet.microsoft.com/library/jj984289.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-181">[This article](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) contains more details about this problem, including information on [how tooconnect tooExchange Online using remote PowerShell](https://technet.microsoft.com/library/jj984289.aspx).</span></span>

<span data-ttu-id="cf1e5-182">Proxy 位址的問題已解決的 hello 受影響的使用者之後，請確定 tooforce 授權處理 hello 群組 toomake 確定授權現在重新套用。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-182">After proxy address problems have been resolved for hello affected users, make sure tooforce license processing on hello group toomake sure licenses can now be applied again.</span></span>

## <a name="how-do-you-force-license-processing-in-a-group-tooresolve-errors"></a><span data-ttu-id="cf1e5-183">您要如何強制執行群組 tooresolve 錯誤處理授權？</span><span class="sxs-lookup"><span data-stu-id="cf1e5-183">How do you force license processing in a group tooresolve errors?</span></span>

<span data-ttu-id="cf1e5-184">取決於哪些步驟已取得 tooresolve 錯誤，可能需要 toomanually 觸發程序處理的群組 tooupdate hello 使用者狀態。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-184">Depending on what steps you've taken tooresolve errors, it might be necessary toomanually trigger processing of a group tooupdate hello user state.</span></span>

<span data-ttu-id="cf1e5-185">比方說，如果您釋放一些授權的移除使用者的直接授權指派，您必須 tootrigger 處理先前失敗 toofully 授權使用者的所有成員的群組。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-185">For example, if you freed up some licenses by removing direct license assignments from users, you'll need tootrigger processing of groups that previously failed toofully license all user members.</span></span> <span data-ttu-id="cf1e5-186">toodo，尋找 hello 群組刀鋒視窗中，開啟**授權**，並選取 hello**重新處理**hello 工具列中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="cf1e5-186">toodo that, find hello group blade, open **Licenses**, and select hello **Reprocess** button in hello toolbar.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf1e5-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf1e5-187">Next steps</span></span>

<span data-ttu-id="cf1e5-188">toolearn 有關的授權管理群組，透過其他案例的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="cf1e5-188">toolearn more about other scenarios for license management through groups, see hello following:</span></span>

* [<span data-ttu-id="cf1e5-189">Azure Active Directory 中指派的授權 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="cf1e5-189">Assigning licenses tooa group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="cf1e5-190">什麼是 Azure Active Directory 中以群組為基礎的授權？</span><span class="sxs-lookup"><span data-stu-id="cf1e5-190">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="cf1e5-191">如何 toomigrate 個別授權 toogroup 型授權 Azure Active Directory 中的使用者</span><span class="sxs-lookup"><span data-stu-id="cf1e5-191">How toomigrate individual licensed users toogroup-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="cf1e5-192">Azure Active Directory 群組型授權其他案例 (英文)</span><span class="sxs-lookup"><span data-stu-id="cf1e5-192">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
