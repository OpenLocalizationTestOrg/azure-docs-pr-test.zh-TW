---
title: "Azure Active Directory B2B 共同作業邀請電子郵件的元素 | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業邀請電子郵件範本"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 458a2cab13b7e83f120e0926a95d454070181dfb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a><span data-ttu-id="5e968-103">B2B 共同作業邀請電子郵件的元素</span><span class="sxs-lookup"><span data-stu-id="5e968-103">The elements of the B2B collaboration invitation email</span></span>

<span data-ttu-id="5e968-104">邀請電子郵件是一個可讓合作夥伴在 Azure AD 中以 B2B 共同作業使用者身分上線的重要元件。</span><span class="sxs-lookup"><span data-stu-id="5e968-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="5e968-105">您可以用它們提高收件者的信任度。</span><span class="sxs-lookup"><span data-stu-id="5e968-105">You can use them to increase the recipient's trust.</span></span> <span data-ttu-id="5e968-106">您可以為電子郵件增添合法性和社交證明，以確保收件者在選取 [開始使用] 按鈕來接受邀請時沒有疑慮。</span><span class="sxs-lookup"><span data-stu-id="5e968-106">you can add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span></span> <span data-ttu-id="5e968-107">此信任是減少共用摩擦的重要手段。</span><span class="sxs-lookup"><span data-stu-id="5e968-107">This trust is a key means to reduce sharing friction.</span></span> <span data-ttu-id="5e968-108">而且您也希望電子郵件看起來很讚！</span><span class="sxs-lookup"><span data-stu-id="5e968-108">And you also want to make the email look great!</span></span>

![Azure AD B2b 邀請電子郵件](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a><span data-ttu-id="5e968-110">說明電子郵件</span><span class="sxs-lookup"><span data-stu-id="5e968-110">Explaining the email</span></span>
<span data-ttu-id="5e968-111">讓我們看看一些電子郵件項目，以便了解如何充分利用這些功能。</span><span class="sxs-lookup"><span data-stu-id="5e968-111">Let's look at a few elements of the email so you know how best to use their capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="5e968-112">主旨</span><span class="sxs-lookup"><span data-stu-id="5e968-112">Subject</span></span>
<span data-ttu-id="5e968-113">電子郵件的主旨依循以下模式：您收到加入 &lt;tenantname&gt; 組織的邀請</span><span class="sxs-lookup"><span data-stu-id="5e968-113">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="5e968-114">寄件者地址</span><span class="sxs-lookup"><span data-stu-id="5e968-114">From address</span></span>
<span data-ttu-id="5e968-115">針對「寄件者地址」，我們使用類似 LinkedIn 的模式。</span><span class="sxs-lookup"><span data-stu-id="5e968-115">We use a LinkedIn-like pattern for the From address.</span></span>  <span data-ttu-id="5e968-116">您應該清楚邀請者是誰及來自哪個公司，並且表明電子郵件是來自 Microsoft 電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e968-116">You should be clear who the inviter is and from which company, and also clarify that the email is coming from a Microsoft email address.</span></span> <span data-ttu-id="5e968-117">其格式為：來自 &lt;tenantname&gt; 的 &lt;邀請者的顯示名稱&gt; (透過 Microsoft) <invites@microsoft.com&gt;</span><span class="sxs-lookup"><span data-stu-id="5e968-117">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="5e968-118">回覆地址</span><span class="sxs-lookup"><span data-stu-id="5e968-118">Reply To</span></span>
<span data-ttu-id="5e968-119">回覆電子郵件會設定為邀請者的電子郵件 (如果可用)，以便在回覆電子郵件時會將電子郵件傳回給邀請者。</span><span class="sxs-lookup"><span data-stu-id="5e968-119">The reply-to email is set to the inviter's email when available, so that replying to the email sends an email back to the inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="5e968-120">商標</span><span class="sxs-lookup"><span data-stu-id="5e968-120">Branding</span></span>
<span data-ttu-id="5e968-121">來自您租用戶的邀請電子郵件會使用您可能已為租用戶設定的公司商標。</span><span class="sxs-lookup"><span data-stu-id="5e968-121">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="5e968-122">如果您想要利用此功能，[這裡](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal)提供有關如何設定的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5e968-122">If you want to take advantage of this capability, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span></span> <span data-ttu-id="5e968-123">電子郵件中會顯示橫幅標誌。</span><span class="sxs-lookup"><span data-stu-id="5e968-123">The banner logo appears in the email.</span></span> <span data-ttu-id="5e968-124">依照[這裡](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal)的影像大小和品質指示，以獲得最佳效果。</span><span class="sxs-lookup"><span data-stu-id="5e968-124">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="5e968-125">此外，公司名稱也會顯示在對動作的呼叫中。</span><span class="sxs-lookup"><span data-stu-id="5e968-125">In addition, the company name also shows up in the call to action.</span></span>

### <a name="call-to-action"></a><span data-ttu-id="5e968-126">對動作的呼叫</span><span class="sxs-lookup"><span data-stu-id="5e968-126">Call to action</span></span>
<span data-ttu-id="5e968-127">對動作的呼叫是由兩個部分組成：說明收件者收到郵件的原因，以及要求收件者採取的動作。</span><span class="sxs-lookup"><span data-stu-id="5e968-127">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span></span>
- <span data-ttu-id="5e968-128">「原因」區段可以使用以下模式來處理：您收到存取 &lt;tenantname&gt; 組織中應用程式的邀請</span><span class="sxs-lookup"><span data-stu-id="5e968-128">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="5e968-129">而「要求您採取的動作」區段是以 [開始使用] 按鈕的存在來表示。</span><span class="sxs-lookup"><span data-stu-id="5e968-129">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span></span> <span data-ttu-id="5e968-130">在已新增使用者而不需要邀請的情況下，就不會顯示此按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e968-130">When the recipient has been added without the need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="5e968-131">邀請者的資訊</span><span class="sxs-lookup"><span data-stu-id="5e968-131">Inviter's information</span></span>
<span data-ttu-id="5e968-132">邀請者的顯示名稱會包含在電子郵件中。</span><span class="sxs-lookup"><span data-stu-id="5e968-132">The inviter's display name is included in the email.</span></span> <span data-ttu-id="5e968-133">此外，如果您已為 Azure AD 帳戶設定個人檔案圖片，則邀請電子郵件也會包含該圖片。</span><span class="sxs-lookup"><span data-stu-id="5e968-133">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span></span> <span data-ttu-id="5e968-134">這兩項措施都是為了提升收件者對電子郵件的信賴感。</span><span class="sxs-lookup"><span data-stu-id="5e968-134">Both are intended to increase your recipient's confidence in the email.</span></span>

<span data-ttu-id="5e968-135">如果您尚未設定自己的個人檔案圖片，圖片位置就會顯示邀請者的姓名縮寫圖示：</span><span class="sxs-lookup"><span data-stu-id="5e968-135">If you haven't yet set up your profile picture, an icon with the inviter's initials in place of the picture is shown:</span></span>

  ![顯示邀請者的姓名縮寫](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="5e968-137">body</span><span class="sxs-lookup"><span data-stu-id="5e968-137">Body</span></span>
<span data-ttu-id="5e968-138">本文內容包含邀請者撰寫或透過邀請 API 傳遞的訊息。</span><span class="sxs-lookup"><span data-stu-id="5e968-138">The body contains the message that the inviter composes or is passed through the invitation API.</span></span> <span data-ttu-id="5e968-139">因為它是文字區域，所以不會基於安全考量處理 HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="5e968-139">It is a text area, so it does not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="5e968-140">頁尾區段</span><span class="sxs-lookup"><span data-stu-id="5e968-140">Footer section</span></span>
<span data-ttu-id="5e968-141">頁尾包含 Microsoft 公司品牌，並讓收件者知道電子郵件是否是由未受監視的別名所傳送。</span><span class="sxs-lookup"><span data-stu-id="5e968-141">The footer contains the Microsoft company brand and lets the recipient know if the email was sent from an unmonitored alias.</span></span> <span data-ttu-id="5e968-142">特殊案例：</span><span class="sxs-lookup"><span data-stu-id="5e968-142">Special cases:</span></span>

- <span data-ttu-id="5e968-143">邀請者在邀請方租用中沒有電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="5e968-143">The inviter doesn't have an email address in the inviting tenancy</span></span>

  ![在邀請方租用中沒有電子郵件地址的邀請者圖片](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="5e968-145">收件者不需要兌換邀請函</span><span class="sxs-lookup"><span data-stu-id="5e968-145">The recipient doesn't need to redeem the invitation</span></span>

  ![當收件者不需要兌換邀請函時](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="5e968-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e968-147">Next steps</span></span>

<span data-ttu-id="5e968-148">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="5e968-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="5e968-149">什麼是 Azure AD B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="5e968-149">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="5e968-150">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="5e968-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="5e968-151">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="5e968-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="5e968-152">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="5e968-152">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="5e968-153">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="5e968-153">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="5e968-154">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="5e968-154">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="5e968-155">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="5e968-155">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="5e968-156">Azure Active Directory B2B 共同作業 API 和自訂</span><span class="sxs-lookup"><span data-stu-id="5e968-156">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="5e968-157">適用於 B2B 共同作業使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="5e968-157">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="5e968-158">在沒有邀請的情況下新增 B2B 共同作業使用者</span><span class="sxs-lookup"><span data-stu-id="5e968-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="5e968-159">Azure Active Directory 中應用程式管理的文章索引</span><span class="sxs-lookup"><span data-stu-id="5e968-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
