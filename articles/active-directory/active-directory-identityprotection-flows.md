---
title: "使用 Azure AD Identity Protection 時的登入體驗 | Microsoft Docs"
description: "當 Identity Protection 已降低或補救使用者時，或是原則需要 Multi-Factor Authentication 時，請提供使用者經驗的概觀。"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, 管理應用程式, 安全性, 風險, 風險層級, 弱點, 安全性原則"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e45936280b51fb2e54012a688fceddcc8dabe984
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="00f3b-104">使用 Azure AD Identity Protection 時的登入體驗</span><span class="sxs-lookup"><span data-stu-id="00f3b-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="00f3b-105">透過 Azure Active Directory Identity Protection，您可以：</span><span class="sxs-lookup"><span data-stu-id="00f3b-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="00f3b-106">要求使用者進行註冊，以進行 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="00f3b-106">require users to register for multi-factor authentication</span></span>
* <span data-ttu-id="00f3b-107">處理高風險的登入和遭到入侵的使用者</span><span class="sxs-lookup"><span data-stu-id="00f3b-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="00f3b-108">系統對這些問題的回應會影響使用者的登入體驗，因為只藉由提供使用者名稱和密碼直接登入已不再可行。</span><span class="sxs-lookup"><span data-stu-id="00f3b-108">The response of the system to these issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="00f3b-109">需要有其他步驟，才能讓使用者安全返回工作。</span><span class="sxs-lookup"><span data-stu-id="00f3b-109">Additional steps are required to get a user safely back into business.</span></span>

<span data-ttu-id="00f3b-110">本主題會針對可能發生的所有案例，為您提供使用者的登入體驗概觀。</span><span class="sxs-lookup"><span data-stu-id="00f3b-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="00f3b-111">**Multi-Factor Authentication**</span><span class="sxs-lookup"><span data-stu-id="00f3b-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="00f3b-112">Multi-Factor Authentication 註冊</span><span class="sxs-lookup"><span data-stu-id="00f3b-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="00f3b-113">**有風險的登入**</span><span class="sxs-lookup"><span data-stu-id="00f3b-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="00f3b-114">有風險的登入復原</span><span class="sxs-lookup"><span data-stu-id="00f3b-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="00f3b-115">已封鎖有風險的登入</span><span class="sxs-lookup"><span data-stu-id="00f3b-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="00f3b-116">在有風險的登入期間註冊 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="00f3b-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="00f3b-117">**有風險的使用者**</span><span class="sxs-lookup"><span data-stu-id="00f3b-117">**User at risk**</span></span>

* <span data-ttu-id="00f3b-118">遭到入侵的帳戶復原</span><span class="sxs-lookup"><span data-stu-id="00f3b-118">Compromised account recovery</span></span>
* <span data-ttu-id="00f3b-119">已封鎖遭到入侵的帳戶</span><span class="sxs-lookup"><span data-stu-id="00f3b-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="00f3b-120">Multi-Factor Authentication 註冊</span><span class="sxs-lookup"><span data-stu-id="00f3b-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="00f3b-121">在遭到入侵的帳戶復原流程和有風險的登入流程中，最佳的使用者體驗皆是使用者可以自行復原。</span><span class="sxs-lookup"><span data-stu-id="00f3b-121">The best user experience for both, the compromised account recovery flow and the risky sign-in flow, is when the user can self-recover.</span></span> <span data-ttu-id="00f3b-122">如果使用者已註冊 Multi-Factor Authentication，他們便有與其帳戶相關聯的電話號碼可用來通過安全性挑戰。</span><span class="sxs-lookup"><span data-stu-id="00f3b-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used to pass security challenges.</span></span> <span data-ttu-id="00f3b-123">從帳戶入侵復原時，不需要技術服務人員或系統管理員介入。</span><span class="sxs-lookup"><span data-stu-id="00f3b-123">No help desk or administrator involvement is needed to recover from account compromise.</span></span> <span data-ttu-id="00f3b-124">因此，強烈建議您讓使用者註冊 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="00f3b-124">Thus, it’s highly recommended to get your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="00f3b-125">系統管理員可以：</span><span class="sxs-lookup"><span data-stu-id="00f3b-125">Administrators can:</span></span>

* <span data-ttu-id="00f3b-126">設定一個原則，要求使用者設定其帳戶進行其他安全性驗證。</span><span class="sxs-lookup"><span data-stu-id="00f3b-126">set a policy that requires users to set up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="00f3b-127">允許最多略過 Multi-Factor Authentication 註冊 30 天 (如果他們想給予使用者註冊前的寬限期)。</span><span class="sxs-lookup"><span data-stu-id="00f3b-127">allow skipping multi-factor authentication registration for up to 30 days, in case they want to give users a grace period before registering.</span></span>

<span data-ttu-id="00f3b-128">**Multi-Factor Authentication 註冊具有三個步驟：**</span><span class="sxs-lookup"><span data-stu-id="00f3b-128">**The multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="00f3b-129">在第一個步驟中，使用者會得到設定此帳戶進行 Multi-Factor Authentication 之需求的相關通知。</span><span class="sxs-lookup"><span data-stu-id="00f3b-129">In the first step, the user gets a notification about the requirement to set the account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="00f3b-130">![補救](./media/active-directory-identityprotection-flows/140.png "補救")</span><span class="sxs-lookup"><span data-stu-id="00f3b-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="00f3b-131">若要設定 Multi-Factor Authentication，您需要讓系統知道您要連線的方式。</span><span class="sxs-lookup"><span data-stu-id="00f3b-131">To set multi-factor authentication up, you need to let the system know how you want to be contacted.</span></span>
   
    <span data-ttu-id="00f3b-132">![補救](./media/active-directory-identityprotection-flows/141.png "補救")</span><span class="sxs-lookup"><span data-stu-id="00f3b-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="00f3b-133">系統會送出一項挑戰給您，而您需要回應。</span><span class="sxs-lookup"><span data-stu-id="00f3b-133">The system submits a challenge to you and you need to respond.</span></span>
   
    <span data-ttu-id="00f3b-134">![補救](./media/active-directory-identityprotection-flows/142.png "補救")</span><span class="sxs-lookup"><span data-stu-id="00f3b-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="00f3b-135">有風險的登入復原</span><span class="sxs-lookup"><span data-stu-id="00f3b-135">Risky sign-in recovery</span></span>
<span data-ttu-id="00f3b-136">當系統管理員設定登入風險的原則後，受影響的使用者會在嘗試登入時收到通知。</span><span class="sxs-lookup"><span data-stu-id="00f3b-136">When an administrator has configured a policy for sign-in risks, the affected users are notified when they try to sign-in.</span></span> 

<span data-ttu-id="00f3b-137">**有風險的登入流程有兩個步驟：**</span><span class="sxs-lookup"><span data-stu-id="00f3b-137">**The risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="00f3b-138">使用者獲知偵測到不尋常的登入，例如從新的位置、裝置或 app 登入。</span><span class="sxs-lookup"><span data-stu-id="00f3b-138">The user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="00f3b-139">![補救](./media/active-directory-identityprotection-flows/120.png "補救")</span><span class="sxs-lookup"><span data-stu-id="00f3b-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="00f3b-140">使用者必須解決安全性挑戰以證明其身分識別。</span><span class="sxs-lookup"><span data-stu-id="00f3b-140">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="00f3b-141">如果使用者已註冊 Multi-Factor Authentication，他們必須回傳送至其電話號碼的安全碼。</span><span class="sxs-lookup"><span data-stu-id="00f3b-141">If the user is registered for multi-factor authentication they need to round-trip a security code to their phone number.</span></span> <span data-ttu-id="00f3b-142">由於這只是有風險的登入，並不是遭到入侵的帳戶，所以使用者不必在此流程中變更密碼。</span><span class="sxs-lookup"><span data-stu-id="00f3b-142">Since this is a just a risky sign in and not a compromised account, the user won’t have to change the password in this flow.</span></span> 
   
    <span data-ttu-id="00f3b-143">![補救](./media/active-directory-identityprotection-flows/121.png "補救")</span><span class="sxs-lookup"><span data-stu-id="00f3b-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="00f3b-144">已封鎖有風險的登入</span><span class="sxs-lookup"><span data-stu-id="00f3b-144">Risky sign-in blocked</span></span>
<span data-ttu-id="00f3b-145">系統管理員也可以選擇設定登入風險原則，以根據風險層級防止使用者登入。</span><span class="sxs-lookup"><span data-stu-id="00f3b-145">Administrators can also choose to set a Sign-In Risk policy to block users upon sign-in depending on the risk level.</span></span> <span data-ttu-id="00f3b-146">若要解除封鎖，使用者必須連絡系統管理員或技術服務人員，或者嘗試從熟悉的位置或裝置登入。</span><span class="sxs-lookup"><span data-stu-id="00f3b-146">To get unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="00f3b-147">藉由解決 Multi-Factor Authentication 自行復原，不是此種情況的適用選項。</span><span class="sxs-lookup"><span data-stu-id="00f3b-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="00f3b-148">![補救](./media/active-directory-identityprotection-flows/200.png "補救")</span><span class="sxs-lookup"><span data-stu-id="00f3b-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="00f3b-149">遭到入侵的帳戶復原</span><span class="sxs-lookup"><span data-stu-id="00f3b-149">Compromised account recovery</span></span>
<span data-ttu-id="00f3b-150">設定使用者風險安全性原則之後，符合原則中指定的使用者風險層級 (因而假定遭到入侵) 的使用者，必須先經歷使用者入侵復原流程，才可以登入。</span><span class="sxs-lookup"><span data-stu-id="00f3b-150">When a user risk security policy has been configured, users who meet the user risk level specified in the policy (and are therefore assumed compromised) must go through the user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="00f3b-151">**使用者入侵復原流程有三個步驟：**</span><span class="sxs-lookup"><span data-stu-id="00f3b-151">**The user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="00f3b-152">使用者獲知其帳戶安全性因為可疑活動或認證外洩而有風險。</span><span class="sxs-lookup"><span data-stu-id="00f3b-152">The user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="00f3b-153">![補救](./media/active-directory-identityprotection-flows/101.png "補救")</span><span class="sxs-lookup"><span data-stu-id="00f3b-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="00f3b-154">使用者必須解決安全性挑戰以證明其身分識別。</span><span class="sxs-lookup"><span data-stu-id="00f3b-154">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="00f3b-155">如果使用者已註冊 Multi-Factor Authentication，他們可以從損害中自行復原。</span><span class="sxs-lookup"><span data-stu-id="00f3b-155">If the user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="00f3b-156">他們必須回傳送至其電話號碼的安全碼。</span><span class="sxs-lookup"><span data-stu-id="00f3b-156">They will need to round-trip a security code to their phone number.</span></span> 
   
   <span data-ttu-id="00f3b-157">![補救](./media/active-directory-identityprotection-flows/110.png "補救")</span><span class="sxs-lookup"><span data-stu-id="00f3b-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="00f3b-158">最後，使用者會被迫變更其密碼，因為其他人可能有其帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="00f3b-158">Finally, the user is forced to change their password since someone else may have had access to their account.</span></span> 
   <span data-ttu-id="00f3b-159">這項體驗的螢幕擷取畫面如下。</span><span class="sxs-lookup"><span data-stu-id="00f3b-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="00f3b-160">![補救](./media/active-directory-identityprotection-flows/111.png "補救")</span><span class="sxs-lookup"><span data-stu-id="00f3b-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="00f3b-161">已封鎖遭到入侵的帳戶</span><span class="sxs-lookup"><span data-stu-id="00f3b-161">Compromised account blocked</span></span>
<span data-ttu-id="00f3b-162">若要讓遭到使用者風險安全性原則封鎖的使用者解除封鎖，該使用者必須連絡系統管理員或技術服務人員。</span><span class="sxs-lookup"><span data-stu-id="00f3b-162">To get a user that was blocked by a user risk security policy unblocked, the user must contact an administrator or help desk.</span></span> <span data-ttu-id="00f3b-163">藉由解決 Multi-Factor Authentication 自行復原，不是此種情況的適用選項。</span><span class="sxs-lookup"><span data-stu-id="00f3b-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="00f3b-164">![補救](./media/active-directory-identityprotection-flows/104.png "補救")</span><span class="sxs-lookup"><span data-stu-id="00f3b-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="00f3b-165">重設密碼</span><span class="sxs-lookup"><span data-stu-id="00f3b-165">Reset password</span></span>
<span data-ttu-id="00f3b-166">如果遭到入侵的使用者已遭封鎖而無法登入，系統管理員可以為其產生暫時密碼。</span><span class="sxs-lookup"><span data-stu-id="00f3b-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="00f3b-167">使用者必須在下次登入期間變更密碼。</span><span class="sxs-lookup"><span data-stu-id="00f3b-167">The users will have to change their password during a next sign-in.</span></span>

<span data-ttu-id="00f3b-168">![補救](./media/active-directory-identityprotection-flows/160.png "補救")</span><span class="sxs-lookup"><span data-stu-id="00f3b-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="00f3b-169">另請參閱</span><span class="sxs-lookup"><span data-stu-id="00f3b-169">See also</span></span>
* [<span data-ttu-id="00f3b-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="00f3b-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

