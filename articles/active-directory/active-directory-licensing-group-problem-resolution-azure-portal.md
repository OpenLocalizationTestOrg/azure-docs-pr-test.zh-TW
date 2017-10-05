---
title: "解決 Azure Active Directory 中群組的授權問題 | Microsoft Docs"
description: "當您使用 Azure Active Directory 以群組為基礎的授權時，如何識別及解決授權指派問題"
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
ms.openlocfilehash: bfa951a897c9b383072c0d29c9a4266c163fe753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a><span data-ttu-id="1aba2-104">識別及解決 Azure Active Directory 中群組的授權指派問題</span><span class="sxs-lookup"><span data-stu-id="1aba2-104">Identify and resolve license assignment problems for a group in Azure Active Directory</span></span>

<span data-ttu-id="1aba2-105">Azure Active Directory (Azure AD) 中以群組為基礎的授權會介紹使用者授權錯誤狀態的概念。</span><span class="sxs-lookup"><span data-stu-id="1aba2-105">Group-based licensing in Azure Active Directory (Azure AD) introduces the concept of users in a licensing error state.</span></span> <span data-ttu-id="1aba2-106">在本文章中，我們會說明使用者最後都處於此狀態的原因。</span><span class="sxs-lookup"><span data-stu-id="1aba2-106">In this article, we explain the reasons why users might end up in this state.</span></span>

<span data-ttu-id="1aba2-107">當您將授權直接指派給個別使用者，而不使用以群組為基礎的授權時，指派作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="1aba2-107">When you assign licenses directly to individual users, without using group-based licensing, the assignment operation might fail.</span></span> <span data-ttu-id="1aba2-108">例如，當您對使用者執行 PowerShell Cmdlet `Set-MsolUserLicense` 時，此 Cmdlet 可能會因為一些商務邏輯相關原因而失敗。</span><span class="sxs-lookup"><span data-stu-id="1aba2-108">For example, when you execute the PowerShell cmdlet `Set-MsolUserLicense` on a user, the cmdlet can fail for a number of reasons that are related to business logic.</span></span> <span data-ttu-id="1aba2-109">例如，可能是授權數量不足，或無法同時指派兩個服務方案的衝突。</span><span class="sxs-lookup"><span data-stu-id="1aba2-109">For example, there might be an insufficient number of licenses or a conflict between two service plans that can't be assigned at the same time.</span></span> <span data-ttu-id="1aba2-110">系統會立即向您回報此問題。</span><span class="sxs-lookup"><span data-stu-id="1aba2-110">The problem is immediately reported back to you.</span></span>

<span data-ttu-id="1aba2-111">當您使用以群組為基礎的授權時，可能會發生相同錯誤，但是當 Azure AD 服務指派授權時會在背景中發生。</span><span class="sxs-lookup"><span data-stu-id="1aba2-111">When you're using group-based licensing, the same errors can occur, but they happen in the background when the Azure AD service is assigning licenses.</span></span> <span data-ttu-id="1aba2-112">基於這個原因，無法立即向您通知這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="1aba2-112">For this reason, the errors can't be communicated to you immediately.</span></span> <span data-ttu-id="1aba2-113">而是會記錄在使用者物件上，然後透過系統管理入口網站報告。</span><span class="sxs-lookup"><span data-stu-id="1aba2-113">Instead, they're recorded on the user object and then reported via the administrative portal.</span></span> <span data-ttu-id="1aba2-114">請注意，授權使用者的原始目的永遠不會遺失，但是會針對未來的調查和解決記錄於錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="1aba2-114">Note that the original intent to license the user is never lost, but it's recorded in an error state for future investigation and resolution.</span></span>

## <a name="how-to-find-license-assignment-errors"></a><span data-ttu-id="1aba2-115">如何找出授權指派錯誤</span><span class="sxs-lookup"><span data-stu-id="1aba2-115">How to find license assignment errors</span></span>

1. <span data-ttu-id="1aba2-116">若要在特定群組中尋找處於錯誤狀態的使用者，請開啟該群組的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1aba2-116">To find users in an error state in a specific group, open the blade for the group.</span></span> <span data-ttu-id="1aba2-117">[授權] 底下會有一份通知，顯示是否有任何使用者處於錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="1aba2-117">Under **Licenses**, there will be a notification displayed if there are any users in an error state.</span></span>

![群組，錯誤通知](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. <span data-ttu-id="1aba2-119">按一下這份通知，以開啟所有受影響的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="1aba2-119">Click the notification to open a list of all affected users.</span></span> <span data-ttu-id="1aba2-120">您可以分別按一下每個使用者以查看詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1aba2-120">You can click on each user individually to see more details.</span></span>

![群組，處於錯誤狀態的使用者清單](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. <span data-ttu-id="1aba2-122">若要尋找包含至少一個錯誤的所有群組，在 [Azure Active Directory] 刀鋒視窗上選取 [授權]，然後選取 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="1aba2-122">To find all groups that contain at least one error, on the **Azure Active Directory** blade select **Licenses** and then **Overview**.</span></span> <span data-ttu-id="1aba2-123">某些群組需要您注意時，會顯示資訊方塊。</span><span class="sxs-lookup"><span data-stu-id="1aba2-123">An info box is displayed when some groups require your attention.</span></span>

![概觀，處於錯誤狀態的群組相關資訊](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. <span data-ttu-id="1aba2-125">按一下方塊以查看具有錯誤的所有群組清單。</span><span class="sxs-lookup"><span data-stu-id="1aba2-125">Click on the box to see a list of all groups with errors.</span></span> <span data-ttu-id="1aba2-126">您可以按一下每個群組以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1aba2-126">You can click each group for more details.</span></span>

![概觀，具有錯誤的群組清單](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


<span data-ttu-id="1aba2-128">以下是每個潛在問題及其解決方法的說明。</span><span class="sxs-lookup"><span data-stu-id="1aba2-128">Below is a description of each potential problem and the way to resolve it.</span></span>

## <a name="not-enough-licenses"></a><span data-ttu-id="1aba2-129">沒有足夠的授權</span><span class="sxs-lookup"><span data-stu-id="1aba2-129">Not enough licenses</span></span>

<span data-ttu-id="1aba2-130">**問題：**群組中指定的其中一項產品沒有足夠的可用授權。</span><span class="sxs-lookup"><span data-stu-id="1aba2-130">**Problem:** There aren't enough available licenses for one of the products that's specified in the group.</span></span> <span data-ttu-id="1aba2-131">您需要為產品購買更多授權，或從其他使用者或群組釋放未使用的授權。</span><span class="sxs-lookup"><span data-stu-id="1aba2-131">You need to either purchase more licenses for the product, or free up unused licenses from other users or groups.</span></span>

<span data-ttu-id="1aba2-132">若要查看有多少授權可用，請移至 [Azure Active Directory] > [授權] > [所有產品]。</span><span class="sxs-lookup"><span data-stu-id="1aba2-132">To see how many licenses are available, go to **Azure Active Directory** > **Licenses** > **All products**.</span></span>

<span data-ttu-id="1aba2-133">若要查看哪些使用者及群組在取用授權，請按一下某項產品。</span><span class="sxs-lookup"><span data-stu-id="1aba2-133">To see which users and groups are consuming licenses, click a product.</span></span> <span data-ttu-id="1aba2-134">在 [已授權的使用者] 底下，您會看到其授權已直接指派或透過一或多個群組指派的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="1aba2-134">Under **Licensed users**, you'll see all users who've had licenses assigned directly or via one or more groups.</span></span> <span data-ttu-id="1aba2-135">在 [已授權的群組] 底下，您會看到已被指派該產品的所有群組。</span><span class="sxs-lookup"><span data-stu-id="1aba2-135">Under **Licensed groups**, you'll see all groups that have that product assigned.</span></span>

<span data-ttu-id="1aba2-136">**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _CountViolation_。</span><span class="sxs-lookup"><span data-stu-id="1aba2-136">**PowerShell:** PowerShell cmdlets report this error as _CountViolation_.</span></span>

## <a name="conflicting-service-plans"></a><span data-ttu-id="1aba2-137">衝突的服務方案</span><span class="sxs-lookup"><span data-stu-id="1aba2-137">Conflicting service plans</span></span>

<span data-ttu-id="1aba2-138">**問題：**群組中指定的其中一個產品包含服務方案，與已透過不同產品指派給使用者的另一個服務方案相衝突。</span><span class="sxs-lookup"><span data-stu-id="1aba2-138">**Problem:** One of the products that's specified in the group contains a service plan that conflicts with another service plan that's already assigned to the user via a different product.</span></span> <span data-ttu-id="1aba2-139">某些服務方案設定的方式不同，所以無法將它們指派給另一個相關服務方案的相同使用者。</span><span class="sxs-lookup"><span data-stu-id="1aba2-139">Some service plans are configured in a way that they can't be assigned to the same user as another related service plan.</span></span>

<span data-ttu-id="1aba2-140">請思考一下下列範例。</span><span class="sxs-lookup"><span data-stu-id="1aba2-140">Consider the following example.</span></span> <span data-ttu-id="1aba2-141">使用者擁有直接指派的 Office 365 企業版 **E1** 授權，所有方案皆啟用。</span><span class="sxs-lookup"><span data-stu-id="1aba2-141">A user has a license for Office 365 Enterprise **E1** assigned directly, with all the plans enabled.</span></span> <span data-ttu-id="1aba2-142">使用者已新增至獲得 Office 365 企業版 **E3** 產品指派的群組。</span><span class="sxs-lookup"><span data-stu-id="1aba2-142">The user has been added to a group that has the Office 365 Enterprise **E3** product assigned to it.</span></span> <span data-ttu-id="1aba2-143">本產品包含的服務方案不能與 E1 包含的方案重疊，因此群組授權指派將會失敗，且具有「衝突的服務方案」錯誤。</span><span class="sxs-lookup"><span data-stu-id="1aba2-143">This product contains service plans that can't overlap with the plans included in E1, so the group license assignment will fail with the “Conflicting service plans” error.</span></span> <span data-ttu-id="1aba2-144">在此範例中，衝突的服務方案是︰</span><span class="sxs-lookup"><span data-stu-id="1aba2-144">In this example, the conflicting service plans are:</span></span>

-   <span data-ttu-id="1aba2-145">SharePoint Online (方案 2) 與 SharePoint Online (方案 1) 衝突。</span><span class="sxs-lookup"><span data-stu-id="1aba2-145">SharePoint Online (Plan 2) conflicts with SharePoint Online (Plan 1).</span></span>
-   <span data-ttu-id="1aba2-146">Exchange Online (方案 2) 與 Exchange Online (方案 1) 衝突。</span><span class="sxs-lookup"><span data-stu-id="1aba2-146">Exchange Online (Plan 2) conflicts with Exchange Online (Plan 1).</span></span>

<span data-ttu-id="1aba2-147">若要解決此衝突，您必須停用這兩個方案，不是在直接指派給使用者的 E1 授權上停用。</span><span class="sxs-lookup"><span data-stu-id="1aba2-147">To solve this conflict, you need to disable those two plans either on the E1 license that's directly assigned to the user.</span></span> <span data-ttu-id="1aba2-148">就是，必須在 E3 授權中修改整個群組授權指派並停用方案。</span><span class="sxs-lookup"><span data-stu-id="1aba2-148">Or, you need to modify the entire group license assignment and disable the plans in the E3 license.</span></span> <span data-ttu-id="1aba2-149">或者，如果在 E3 授權內容中是多餘的，您可能會決定從使用者移除 E1 授權。</span><span class="sxs-lookup"><span data-stu-id="1aba2-149">Alternatively, you might decide to remove the E1 license from the user if it's redundant in the context of the E3 license.</span></span>

<span data-ttu-id="1aba2-150">如何解決產品授權的衝突一律屬於系統管理員的決策。</span><span class="sxs-lookup"><span data-stu-id="1aba2-150">The decision about how to resolve conflicting product licenses always belongs to the administrator.</span></span> <span data-ttu-id="1aba2-151">Azure AD 不會自動解決授權衝突。</span><span class="sxs-lookup"><span data-stu-id="1aba2-151">Azure AD doesn't automatically resolve license conflicts.</span></span>

<span data-ttu-id="1aba2-152">**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _MutuallyExclusiveViolation_。</span><span class="sxs-lookup"><span data-stu-id="1aba2-152">**PowerShell:** PowerShell cmdlets report this error as _MutuallyExclusiveViolation_.</span></span>

## <a name="other-products-depend-on-this-license"></a><span data-ttu-id="1aba2-153">其他產品相依於此授權</span><span class="sxs-lookup"><span data-stu-id="1aba2-153">Other products depend on this license</span></span>

<span data-ttu-id="1aba2-154">**問題：**群組中指定的其中一個產品包含服務方案，必須在另一個產品中針對另一個服務方案啟用，才能夠運作。</span><span class="sxs-lookup"><span data-stu-id="1aba2-154">**Problem:** One of the products that's specified in the group contains a service plan that must be enabled for another service plan, in another product, to function.</span></span> <span data-ttu-id="1aba2-155">當 Azure AD 嘗試移除基礎服務方案時會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="1aba2-155">This error occurs when Azure AD attempts to remove the underlying service plan.</span></span> <span data-ttu-id="1aba2-156">例如，因為使用者從群組中移除而造成此問題。</span><span class="sxs-lookup"><span data-stu-id="1aba2-156">For example, this can happen as a result of the user being removed from the group.</span></span>

<span data-ttu-id="1aba2-157">若要解決這個問題，您必須確定所需的方案仍透過其他方法指派給使用者，或已停用這些使用者的相依服務。</span><span class="sxs-lookup"><span data-stu-id="1aba2-157">To solve this problem, you'll need to make sure that the required plan is still assigned to users through some other method, or that the dependent services are disabled for those users.</span></span> <span data-ttu-id="1aba2-158">之後，您可以適當地移除這些使用者的群組授權。</span><span class="sxs-lookup"><span data-stu-id="1aba2-158">After doing that, you can properly remove the group license from those users.</span></span>

<span data-ttu-id="1aba2-159">**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _DependencyViolation_。</span><span class="sxs-lookup"><span data-stu-id="1aba2-159">**PowerShell:** PowerShell cmdlets report this error as _DependencyViolation_.</span></span>

## <a name="usage-location-isnt-allowed"></a><span data-ttu-id="1aba2-160">不允許使用位置</span><span class="sxs-lookup"><span data-stu-id="1aba2-160">Usage location isn't allowed</span></span>

<span data-ttu-id="1aba2-161">**問題：**由於當地法律和法規，無法在所有位置使用某些 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="1aba2-161">**Problem:** Some Microsoft services aren't available in all locations because of local laws and regulations.</span></span> <span data-ttu-id="1aba2-162">您必須為使用者指定「使用位置」屬性，才可以將授權指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="1aba2-162">Before you can assign a license to a user, you have to specify the “Usage location” property for the user.</span></span> <span data-ttu-id="1aba2-163">您可以在 Azure 入口網站中 [使用者] > [設定檔] > [設定] 區段之下執行此作業。</span><span class="sxs-lookup"><span data-stu-id="1aba2-163">You can do this under the **User** > **Profile** > **Settings** section in the Azure portal.</span></span>

<span data-ttu-id="1aba2-164">當 Azure AD 嘗試將群組授權指派給不支援其使用位置的使用者時，將會發生失敗並將此錯誤記錄於該使用者。</span><span class="sxs-lookup"><span data-stu-id="1aba2-164">When Azure AD attempts to assign a group license to a user whose usage location isn't supported, it will fail and record this error on the user.</span></span>

<span data-ttu-id="1aba2-165">若要解決這個問題，請從授權群組不支援的位置中移除使用者。</span><span class="sxs-lookup"><span data-stu-id="1aba2-165">To solve this problem, remove users from nonsupported locations from the licensed group.</span></span> <span data-ttu-id="1aba2-166">或者，如果目前的使用位置值不代表實際使用者的位置，您可以進行修改，以便下一次正確指派授權 (如果支援新的位置)。</span><span class="sxs-lookup"><span data-stu-id="1aba2-166">Alternatively, if the current usage location values don't represent the actual user location, you can modify them so that the licenses are correctly assigned next time (if the new location is supported).</span></span>

<span data-ttu-id="1aba2-167">**PowerShell：**PowerShell Cmdlet 會將此錯誤報告為 _ProhibitedInUsageLocationViolation_。</span><span class="sxs-lookup"><span data-stu-id="1aba2-167">**PowerShell:** PowerShell cmdlets report this error as _ProhibitedInUsageLocationViolation_.</span></span>

> [!NOTE]
> <span data-ttu-id="1aba2-168">當 Azure AD 指派群組授權時，未指定使用位置的任何使用者會繼承目錄的位置。</span><span class="sxs-lookup"><span data-stu-id="1aba2-168">When Azure AD assigns group licenses, any users without a usage location specified inherit the location of the directory.</span></span> <span data-ttu-id="1aba2-169">我們建議系統管理員先為使用者設定正確的使用位置值，再使用以群組為基礎的授權，以符合當地法規。</span><span class="sxs-lookup"><span data-stu-id="1aba2-169">We recommend that administrators set the correct usage location values on users before using group-based licensing to comply with local laws and regulations.</span></span>

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a><span data-ttu-id="1aba2-170">當群組中有一個以上的產品授權時，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="1aba2-170">What happens when there's more than one product license on a group?</span></span>

<span data-ttu-id="1aba2-171">您可以將一個以上的產品授權指派給群組。</span><span class="sxs-lookup"><span data-stu-id="1aba2-171">You can assign more than one product license to a group.</span></span> <span data-ttu-id="1aba2-172">例如，您可以將 Office 365 企業版 E3 和 Enterprise Mobility + Security 指派給群組，以便輕鬆地為使用者啟用所有已納入的服務。</span><span class="sxs-lookup"><span data-stu-id="1aba2-172">For example, you can assign Office 365 Enterprise E3 and Enterprise Mobility + Security to a group to easily enable all included services for users.</span></span>

<span data-ttu-id="1aba2-173">Azure AD 會嘗試將群組中指定的所有授權指派給每位使用者。</span><span class="sxs-lookup"><span data-stu-id="1aba2-173">Azure AD attempts to assign all licenses that are specified in the group to each user.</span></span> <span data-ttu-id="1aba2-174">如果 Azure AD 因為商務邏輯問題而無法指派其中一個產品 (例如，沒有足夠授權供所有人使用，或與使用者已啟用的其他服務衝突)，我們也無法在群組中指派其他授權。</span><span class="sxs-lookup"><span data-stu-id="1aba2-174">If Azure AD can't assign one of the products because of business logic problems (for example, if there aren't enough licenses for all, or if there are conflicts with other services that are enabled on the user), it won't assign the other licenses in the group either.</span></span>

<span data-ttu-id="1aba2-175">您可以查看哪些使用者的指派失敗，以及檢查哪些產品受到影響。</span><span class="sxs-lookup"><span data-stu-id="1aba2-175">You'll be able to see the users who failed to get assigned failed and check which products have been affected by this.</span></span>

## <a name="license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online"></a><span data-ttu-id="1aba2-176">使用者的授權指派會因為 Exchange Online 中 Proxy 位址重複而無訊息的失敗</span><span class="sxs-lookup"><span data-stu-id="1aba2-176">License assignment fails silently for a user due to duplicate proxy addresses in Exchange Online</span></span>

<span data-ttu-id="1aba2-177">如果您是使用 Exchange Online，租用戶中有些使用者可能會使用相同的 Proxy 位址值導致設定錯誤。</span><span class="sxs-lookup"><span data-stu-id="1aba2-177">If you are using Exchange Online, some users in your tenant may be incorrectly configured with the same proxy address value.</span></span> <span data-ttu-id="1aba2-178">當群組型授權嘗試將授權指派給此類使用者時，它將會失敗且不會記錄錯誤 (不同於上述的其他錯誤情況) - 這是此功能預覽版本的限制，我們會在*上市*之前解決。</span><span class="sxs-lookup"><span data-stu-id="1aba2-178">When group-based licensing tries to assign a license to such a user, it will fail and will not record an error (unlike in the other error cases described above) - this is a limitation in the preview version of this feature and we are going to address it before *General Availability*.</span></span>

> [!TIP]
> <span data-ttu-id="1aba2-179">如果您發現某些使用者未收到授權，且未對這些使用者記錄錯誤，請先檢查他們是否有重複的 Proxy 位址。</span><span class="sxs-lookup"><span data-stu-id="1aba2-179">If you notice that some users did not receive a license and there is no error recorded on those users, first check if they have duplicate proxy address.</span></span>
> <span data-ttu-id="1aba2-180">可以藉由針對 Exchange Online 執行下列 PowerShell Cmdlet 來完成這項操作：</span><span class="sxs-lookup"><span data-stu-id="1aba2-180">This can be done by executing the following PowerShell cmdlet against Exchange Online:</span></span>
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> <span data-ttu-id="1aba2-181">[這篇文章](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online)包含更多關於此問題的詳細資料，包括[如何使用遠端 PowerShell 連線至 Exchange Online](https://technet.microsoft.com/library/jj984289.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1aba2-181">[This article](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) contains more details about this problem, including information on [how to connect to Exchange Online using remote PowerShell](https://technet.microsoft.com/library/jj984289.aspx).</span></span>

<span data-ttu-id="1aba2-182">為受影響的使用者解決 Proxy 位址問題之後，請確定在群組上強制執行授權處理，以確保現在可以再次套用授權。</span><span class="sxs-lookup"><span data-stu-id="1aba2-182">After proxy address problems have been resolved for the affected users, make sure to force license processing on the group to make sure licenses can now be applied again.</span></span>

## <a name="how-do-you-force-license-processing-in-a-group-to-resolve-errors"></a><span data-ttu-id="1aba2-183">如何強制處理群組中的授權來解決錯誤？</span><span class="sxs-lookup"><span data-stu-id="1aba2-183">How do you force license processing in a group to resolve errors?</span></span>

<span data-ttu-id="1aba2-184">根據您為了解決錯誤所採取的步驟，可能需要手動觸發群組的處理以更新使用者狀態。</span><span class="sxs-lookup"><span data-stu-id="1aba2-184">Depending on what steps you've taken to resolve errors, it might be necessary to manually trigger processing of a group to update the user state.</span></span>

<span data-ttu-id="1aba2-185">例如，如果您藉由移除使用者的直接授權指派來釋出一些授權，您必須觸發先前失敗之群組的處理，才能完整授權所有使用者成員。</span><span class="sxs-lookup"><span data-stu-id="1aba2-185">For example, if you freed up some licenses by removing direct license assignments from users, you'll need to trigger processing of groups that previously failed to fully license all user members.</span></span> <span data-ttu-id="1aba2-186">若要這樣做，請尋找 [群組] 刀鋒視窗，開啟 [授權]，然後選取工具列中的 [重新處理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1aba2-186">To do that, find the group blade, open **Licenses**, and select the **Reprocess** button in the toolbar.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1aba2-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1aba2-187">Next steps</span></span>

<span data-ttu-id="1aba2-188">若要深入了解透過群組管理授權的其他案例，請閱讀下列各項：</span><span class="sxs-lookup"><span data-stu-id="1aba2-188">To learn more about other scenarios for license management through groups, see the following:</span></span>

* [<span data-ttu-id="1aba2-189">將授權指派給 Azure Active Directory 中的群組</span><span class="sxs-lookup"><span data-stu-id="1aba2-189">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="1aba2-190">什麼是 Azure Active Directory 中以群組為基礎的授權？</span><span class="sxs-lookup"><span data-stu-id="1aba2-190">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="1aba2-191">如何將個別授權使用者移轉至 Azure Active Directory 中以群組為基礎的授權</span><span class="sxs-lookup"><span data-stu-id="1aba2-191">How to migrate individual licensed users to group-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="1aba2-192">Azure Active Directory 群組型授權其他案例 (英文)</span><span class="sxs-lookup"><span data-stu-id="1aba2-192">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
