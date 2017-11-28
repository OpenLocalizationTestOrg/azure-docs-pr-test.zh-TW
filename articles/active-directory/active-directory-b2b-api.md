---
title: "aaaAzure Active Directory B2B 共同作業應用程式開發介面和自訂 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業支援跨公司關聯性，方式是讓商務夥伴 tooselectively 存取公司的應用程式"
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
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="f2265-103">Azure Active Directory B2B 共同作業 API 和自訂</span><span class="sxs-lookup"><span data-stu-id="f2265-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="f2265-104">我們發現許多客戶，告訴他們想 toocustomize hello 邀請程序，最適合組織的方式。</span><span class="sxs-lookup"><span data-stu-id="f2265-104">We've had many customers tell us that they want toocustomize hello invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="f2265-105">使用我們的 API，您可以進行自訂。</span><span class="sxs-lookup"><span data-stu-id="f2265-105">With our API, you can do just that.</span></span> [<span data-ttu-id="f2265-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="f2265-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a><span data-ttu-id="f2265-107">Hello 邀請應用程式開發介面的功能</span><span class="sxs-lookup"><span data-stu-id="f2265-107">Capabilities of hello invitation API</span></span>
<span data-ttu-id="f2265-108">hello API 提供下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2265-108">hello API offers hello following capabilities:</span></span>

1. <span data-ttu-id="f2265-109">使用*任何*電子郵件地址來邀請外部使用者。</span><span class="sxs-lookup"><span data-stu-id="f2265-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="f2265-110">自訂您想之後他們接受的邀請使用者 tooland。</span><span class="sxs-lookup"><span data-stu-id="f2265-110">Customize where you want your users tooland after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="f2265-111">選擇透過我們的 toosend hello 標準邀請 mail</span><span class="sxs-lookup"><span data-stu-id="f2265-111">Choose toosend hello standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="f2265-112">您可以自訂訊息 toohello 收件者</span><span class="sxs-lookup"><span data-stu-id="f2265-112">with a message toohello recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="f2265-113">選擇 toocc： 您想要在 hello tookeep 人員迴圈關於邀請這個共同作業者。</span><span class="sxs-lookup"><span data-stu-id="f2265-113">And choose toocc: people you want tookeep in hello loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="f2265-114">或完全選擇不 toosend 透過 Azure AD 的通知，以自訂您的邀請和入門訓練工作流程。</span><span class="sxs-lookup"><span data-stu-id="f2265-114">Or completely customize your invitation and onboarding workflow by choosing not toosend notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="f2265-115">在此情況下，您會回到兌換 URL 從 hello API，您可以內嵌在電子郵件範本、 IM 或您選擇的其他發佈方法。</span><span class="sxs-lookup"><span data-stu-id="f2265-115">In this case, you get back a redemption URL from hello API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="f2265-116">最後，如果您是系統管理員，您可以選擇 tooinvite hello 使用者為成員。</span><span class="sxs-lookup"><span data-stu-id="f2265-116">Finally, if you are an admin, you can choose tooinvite hello user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="f2265-117">授權模型</span><span class="sxs-lookup"><span data-stu-id="f2265-117">Authorization model</span></span>
<span data-ttu-id="f2265-118">hello API 可以執行下列授權模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2265-118">hello API can be run in hello following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="f2265-119">應用程式 + 使用者模式</span><span class="sxs-lookup"><span data-stu-id="f2265-119">App + User mode</span></span>
<span data-ttu-id="f2265-120">在此模式中，所有人員都使用 hello API 需求 toohave hello 權限 toobe 建立 B2B 邀請。</span><span class="sxs-lookup"><span data-stu-id="f2265-120">In this mode, whoever is using hello API needs toohave hello permissions toobe create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="f2265-121">僅應用程式模式</span><span class="sxs-lookup"><span data-stu-id="f2265-121">App only mode</span></span>
<span data-ttu-id="f2265-122">應用程式只有在內容中，必須 hello User.ReadWrite.All 或 Directory.ReadWrite.All 範圍 hello 邀請 toosucceed hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2265-122">In app only context, hello app needs hello User.ReadWrite.All or Directory.ReadWrite.All scopes for hello invitation toosucceed.</span></span>

<span data-ttu-id="f2265-123">如需詳細資訊，請參閱︰ https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="f2265-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="f2265-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2265-124">PowerShell</span></span>
<span data-ttu-id="f2265-125">它是現在可能 toouse PowerShell tooadd 和邀請外部使用者 tooan 組織輕鬆。</span><span class="sxs-lookup"><span data-stu-id="f2265-125">It is now possible toouse PowerShell tooadd and invite external users tooan organization easily.</span></span> <span data-ttu-id="f2265-126">建立邀請使用 hello cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f2265-126">Create an invitation using hello cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="f2265-127">您可以使用下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2265-127">You can use hello following options:</span></span>

* <span data-ttu-id="f2265-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="f2265-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="f2265-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="f2265-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="f2265-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="f2265-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="f2265-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="f2265-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="f2265-132">您也可以查看中的 hello 邀請應用程式開發介面參考[https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="f2265-132">You can also check out hello invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2265-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2265-133">Next steps</span></span>

<span data-ttu-id="f2265-134">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="f2265-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="f2265-135">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="f2265-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="f2265-136">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="f2265-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="f2265-137">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="f2265-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="f2265-138">hello hello B2B 共同作業邀請電子郵件項目</span><span class="sxs-lookup"><span data-stu-id="f2265-138">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="f2265-139">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="f2265-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="f2265-140">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="f2265-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="f2265-141">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f2265-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="f2265-142">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="f2265-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="f2265-143">適用於 B2B 共同作業使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="f2265-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="f2265-144">在沒有邀請的情況下新增 B2B 共同作業使用者</span><span class="sxs-lookup"><span data-stu-id="f2265-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="f2265-145">Azure Active Directory 中應用程式管理的文章索引</span><span class="sxs-lookup"><span data-stu-id="f2265-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
