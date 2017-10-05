---
title: "針對 Azure Active Directory B2B 共同作業問題進行疑難排解 | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業常見問題的補救方式"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 2009cfc956a2703e268c9364996aa2d0fbd8f279
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="8ea5f-103">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="8ea5f-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="8ea5f-104">以下是 Azure Active Directory (Azure AD) B2B 共同作業常見問題的補救方式。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a><span data-ttu-id="8ea5f-105">我已新增外部使用者，但在我的全域通訊錄或人員選擇器中未看到他們</span><span class="sxs-lookup"><span data-stu-id="8ea5f-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span></span>

<span data-ttu-id="8ea5f-106">若清單中未顯示外部使用者，該物件可能需要一些時間才能複寫。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="8ea5f-107">B2B 來賓使用者不會顯示在 SharePoint Online/OneDrive 人員選擇器中</span><span class="sxs-lookup"><span data-stu-id="8ea5f-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="8ea5f-108">在 SharePoint Online (SPO) 人員選擇器中搜尋現有來賓使用者的功能預設為關閉，以符合舊版的行為。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-108">The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.</span></span>

<span data-ttu-id="8ea5f-109">您可以使用租用戶和網站集合層級中的 'ShowPeoplePickerSuggestionsForGuestUsers' 設定來啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-109">You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span></span> <span data-ttu-id="8ea5f-110">您可以使用 Set-SPOTenant 和 Set-SPOSite Cmdlet 來設定此功能，讓成員搜尋目錄中所有的現有來賓使用者。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-110">You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span></span> <span data-ttu-id="8ea5f-111">租用戶範圍中的變更不會影響已佈建的 SPO 網站。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="8ea5f-112">已針對目錄停用邀請</span><span class="sxs-lookup"><span data-stu-id="8ea5f-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="8ea5f-113">若收到通知指出您沒有邀請使用者的權限，請在 [使用者設定] 下，確認您的使用者帳戶已獲邀請外部使用者的授權：</span><span class="sxs-lookup"><span data-stu-id="8ea5f-113">If you are notified that you do not have permissions to invite users, verify that your user account is authorized to invite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="8ea5f-114">若您最近曾修改這些設定或已獲指派使用者的「來賓邀請者」角色，變更可能需要 15-60 分鐘才會生效。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-114">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span></span>

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="8ea5f-115">我邀請的使用者在兌換期間遇到錯誤</span><span class="sxs-lookup"><span data-stu-id="8ea5f-115">The user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="8ea5f-116">常見錯誤包括：</span><span class="sxs-lookup"><span data-stu-id="8ea5f-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="8ea5f-117">受邀者的管理員不允許在其租用戶中建立 EmailVerified 使用者</span><span class="sxs-lookup"><span data-stu-id="8ea5f-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="8ea5f-118">當邀請使用者的組織使用 Azure Active Directory，但指定使用者的帳戶不存在 (例如，使用者不存在於 Azure AD contoso.com 中)。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-118">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="8ea5f-119">contoso.com 的系統管理員可能已建立防止建立使用者的原則。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-119">The administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="8ea5f-120">使用者必須向管理員確認，以判斷是否允許外部使用者。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-120">The user must check with their admin to determine if external users are allowed.</span></span> <span data-ttu-id="8ea5f-121">外部使用者的管理員需要允許其網域中存在已驗證的電子郵件使用者 (請參閱[本文](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)，了解允許已驗證的電子郵件使用者)。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-121">The external user’s admin may need to allow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="8ea5f-122">外部使用者不存在於同盟網域中</span><span class="sxs-lookup"><span data-stu-id="8ea5f-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="8ea5f-123">如果您使用同盟驗證，而使用者目前不在 Azure Active Directory 中，則無法邀請使用者。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-123">If you are using federation authentication and the user does not already exist in Azure Active Directory, the user cannot be invited.</span></span>

<span data-ttu-id="8ea5f-124">若要解決此問題，外部使用者的系統管理員必須將該使用者的帳戶同步到 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-124">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="8ea5f-125">‘\#’ (通常是無效的字元) 如何與 Azure AD 同步？</span><span class="sxs-lookup"><span data-stu-id="8ea5f-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="8ea5f-126">因為受邀帳戶 user@contoso.com 會成為 user_contoso.com#EXT@fabrikam.onmicrosoft.com，所以 “\#” 是 Azure AD B2B 共同作業或外部使用者之 UPN 中的保留字元。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because the invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span></span> <span data-ttu-id="8ea5f-127">因此，來自內部部署之 UPN 中的 \# 不可登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-127">Therefore, \# in UPNs coming from on-premises aren't allowed to sign in to the Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a><span data-ttu-id="8ea5f-128">我在將外部使用者新增到已同步的群組時遇到錯誤</span><span class="sxs-lookup"><span data-stu-id="8ea5f-128">I receive an error when adding external users to a synchronized group</span></span>

<span data-ttu-id="8ea5f-129">您只能將外部使用者新增到「已指派」或「安全性」群組，而無法指派到主控內部部署群組。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a><span data-ttu-id="8ea5f-130">我的外部使用者未收到兌換電子郵件</span><span class="sxs-lookup"><span data-stu-id="8ea5f-130">My external user did not receive an email to redeem</span></span>

<span data-ttu-id="8ea5f-131">受邀者應該連絡其 ISP 或檢查其垃圾郵件篩選設定，以確定下列地址在允許清單中：Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="8ea5f-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="8ea5f-132">我注意到自訂訊息有時候不會包含在邀請訊息中</span><span class="sxs-lookup"><span data-stu-id="8ea5f-132">I notice that the custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="8ea5f-133">為了符合隱私權法律，在下列情況下，我們的 API 不會在電子郵件邀請中包含自訂訊息：</span><span class="sxs-lookup"><span data-stu-id="8ea5f-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when:</span></span>

- <span data-ttu-id="8ea5f-134">邀請者在提出邀請的租用戶中沒有電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="8ea5f-134">The inviter doesn’t have an email address in the inviting tenant</span></span>
- <span data-ttu-id="8ea5f-135">應用程式服務主體傳送邀請時</span><span class="sxs-lookup"><span data-stu-id="8ea5f-135">When an appservice principal sends the invitation</span></span>

<span data-ttu-id="8ea5f-136">如果此案例對您很重要，您可以隱藏我們的 API 邀請電子郵件，然後透過您選擇的電子郵件機制傳送邀請電子郵件。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-136">If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice.</span></span> <span data-ttu-id="8ea5f-137">請諮詢貴組織的法律顧問，以確定透過此方式傳送的任何電子郵件也符合隱私權法律。</span><span class="sxs-lookup"><span data-stu-id="8ea5f-137">Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ea5f-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ea5f-138">Next steps</span></span>

<span data-ttu-id="8ea5f-139">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="8ea5f-139">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="8ea5f-140">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="8ea5f-140">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="8ea5f-141">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="8ea5f-141">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="8ea5f-142">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="8ea5f-142">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="8ea5f-143">B2B 共同作業邀請電子郵件的元素</span><span class="sxs-lookup"><span data-stu-id="8ea5f-143">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="8ea5f-144">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="8ea5f-144">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="8ea5f-145">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="8ea5f-145">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="8ea5f-146">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="8ea5f-146">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="8ea5f-147">Azure Active Directory B2B 共同作業 API 和自訂</span><span class="sxs-lookup"><span data-stu-id="8ea5f-147">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="8ea5f-148">適用於 B2B 共同作業使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="8ea5f-148">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="8ea5f-149">在沒有邀請的情況下新增 B2B 共同作業使用者</span><span class="sxs-lookup"><span data-stu-id="8ea5f-149">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="8ea5f-150">Azure Active Directory 中應用程式管理的文章索引</span><span class="sxs-lookup"><span data-stu-id="8ea5f-150">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
