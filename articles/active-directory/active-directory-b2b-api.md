---
title: "Azure Active Directory B2B 共同作業 API 和自訂 | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業讓企業合作夥伴選擇性地存取您的公司應用程式，以支援公司間的關係"
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: c85e05b38b4a9525e13ec510a17b7ef4841198d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="e0bd7-103">Azure Active Directory B2B 共同作業 API 和自訂</span><span class="sxs-lookup"><span data-stu-id="e0bd7-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="e0bd7-104">有許多客戶告訴我們他們想要以最適合其組織的方式自訂邀請程序。</span><span class="sxs-lookup"><span data-stu-id="e0bd7-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="e0bd7-105">使用我們的 API，您可以進行自訂。</span><span class="sxs-lookup"><span data-stu-id="e0bd7-105">With our API, you can do just that.</span></span> [<span data-ttu-id="e0bd7-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="e0bd7-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a><span data-ttu-id="e0bd7-107">邀請 API 的功能</span><span class="sxs-lookup"><span data-stu-id="e0bd7-107">Capabilities of the invitation API</span></span>
<span data-ttu-id="e0bd7-108">API 提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="e0bd7-108">The API offers the following capabilities:</span></span>

1. <span data-ttu-id="e0bd7-109">使用*任何*電子郵件地址來邀請外部使用者。</span><span class="sxs-lookup"><span data-stu-id="e0bd7-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="e0bd7-110">自訂使用者接受其邀請之後將會看到的內容。</span><span class="sxs-lookup"><span data-stu-id="e0bd7-110">Customize where you want your users to land after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="e0bd7-111">選擇透過我們的服務 傳送標準邀請郵件</span><span class="sxs-lookup"><span data-stu-id="e0bd7-111">Choose to send the standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="e0bd7-112">使用您可以自訂的訊息傳送給收件者</span><span class="sxs-lookup"><span data-stu-id="e0bd7-112">with a message to the recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="e0bd7-113">此外，您也可以選擇在邀請共同作業者時將相關人員新增到副本收件者。</span><span class="sxs-lookup"><span data-stu-id="e0bd7-113">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="e0bd7-114">或者，透過選擇不以 Azure AD 傳送通知，以完全自訂您的邀請與上線工作流程。</span><span class="sxs-lookup"><span data-stu-id="e0bd7-114">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="e0bd7-115">在此案例中，您會從 API 取得兌換 URL，您可以將它內嵌在電子郵件範本、IM 或其他發佈方法。</span><span class="sxs-lookup"><span data-stu-id="e0bd7-115">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="e0bd7-116">最後，若您是系統管理員，您可以選擇邀請使用者做為成員。</span><span class="sxs-lookup"><span data-stu-id="e0bd7-116">Finally, if you are an admin, you can choose to invite the user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="e0bd7-117">授權模型</span><span class="sxs-lookup"><span data-stu-id="e0bd7-117">Authorization model</span></span>
<span data-ttu-id="e0bd7-118">API 可以在下列授權模型中執行：</span><span class="sxs-lookup"><span data-stu-id="e0bd7-118">The API can be run in the following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="e0bd7-119">應用程式 + 使用者模式</span><span class="sxs-lookup"><span data-stu-id="e0bd7-119">App + User mode</span></span>
<span data-ttu-id="e0bd7-120">在此模式中，使用 API 的任何使用者必須有建立 B2B 邀請的權限。</span><span class="sxs-lookup"><span data-stu-id="e0bd7-120">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="e0bd7-121">僅應用程式模式</span><span class="sxs-lookup"><span data-stu-id="e0bd7-121">App only mode</span></span>
<span data-ttu-id="e0bd7-122">在僅應用程式模式中，應用程式需要 User.ReadWrite.All 或 Directory.ReadWrite.All 範圍，邀請才能成功。</span><span class="sxs-lookup"><span data-stu-id="e0bd7-122">In app only context, the app needs the User.ReadWrite.All or Directory.ReadWrite.All scopes for the invitation to succeed.</span></span>

<span data-ttu-id="e0bd7-123">如需詳細資訊，請參閱︰ https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="e0bd7-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="e0bd7-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0bd7-124">PowerShell</span></span>
<span data-ttu-id="e0bd7-125">您現在可以輕鬆地使用 PowerShell 來新增並邀請外部使用者加入組織。</span><span class="sxs-lookup"><span data-stu-id="e0bd7-125">It is now possible to use PowerShell to add and invite external users to an organization easily.</span></span> <span data-ttu-id="e0bd7-126">使用 Cmdlet 建立邀請：</span><span class="sxs-lookup"><span data-stu-id="e0bd7-126">Create an invitation using the cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="e0bd7-127">您可以使用下列選項：</span><span class="sxs-lookup"><span data-stu-id="e0bd7-127">You can use the following options:</span></span>

* <span data-ttu-id="e0bd7-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="e0bd7-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="e0bd7-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="e0bd7-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="e0bd7-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="e0bd7-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="e0bd7-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="e0bd7-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="e0bd7-132">您也可以參考 [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation) 中的邀請 API 參考資料</span><span class="sxs-lookup"><span data-stu-id="e0bd7-132">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0bd7-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0bd7-133">Next steps</span></span>

<span data-ttu-id="e0bd7-134">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="e0bd7-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="e0bd7-135">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="e0bd7-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="e0bd7-136">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="e0bd7-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="e0bd7-137">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="e0bd7-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="e0bd7-138">B2B 共同作業邀請電子郵件的元素</span><span class="sxs-lookup"><span data-stu-id="e0bd7-138">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="e0bd7-139">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="e0bd7-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="e0bd7-140">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="e0bd7-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="e0bd7-141">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="e0bd7-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="e0bd7-142">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="e0bd7-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="e0bd7-143">適用於 B2B 共同作業使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="e0bd7-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="e0bd7-144">在沒有邀請的情況下新增 B2B 共同作業使用者</span><span class="sxs-lookup"><span data-stu-id="e0bd7-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="e0bd7-145">Azure Active Directory 中應用程式管理的文章索引</span><span class="sxs-lookup"><span data-stu-id="e0bd7-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
