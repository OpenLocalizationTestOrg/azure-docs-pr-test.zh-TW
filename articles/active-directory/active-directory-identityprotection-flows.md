---
title: "aaaSign 中的體驗與 Azure AD Identity Protection |Microsoft 文件"
description: "識別身分保護已降低或補救使用者或原則時需要多重要素驗證時，請提供 hello 使用者經驗的概觀。"
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
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="187b1-104">使用 Azure AD Identity Protection 時的登入體驗</span><span class="sxs-lookup"><span data-stu-id="187b1-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="187b1-105">透過 Azure Active Directory Identity Protection，您可以：</span><span class="sxs-lookup"><span data-stu-id="187b1-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="187b1-106">需要 multi-factor authentication 使用者 tooregister</span><span class="sxs-lookup"><span data-stu-id="187b1-106">require users tooregister for multi-factor authentication</span></span>
* <span data-ttu-id="187b1-107">處理高風險的登入和遭到入侵的使用者</span><span class="sxs-lookup"><span data-stu-id="187b1-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="187b1-108">因為只要直接登入藉由提供使用者名稱和密碼不是可能再 hello 回應 hello 系統 toothese 問題上使用者的登入體驗有影響。</span><span class="sxs-lookup"><span data-stu-id="187b1-108">hello response of hello system toothese issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="187b1-109">使用者安全地送回商務的必要的 tooget 不額外的步驟。</span><span class="sxs-lookup"><span data-stu-id="187b1-109">Additional steps are required tooget a user safely back into business.</span></span>

<span data-ttu-id="187b1-110">本主題會針對可能發生的所有案例，為您提供使用者的登入體驗概觀。</span><span class="sxs-lookup"><span data-stu-id="187b1-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="187b1-111">**Multi-Factor Authentication**</span><span class="sxs-lookup"><span data-stu-id="187b1-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="187b1-112">Multi-Factor Authentication 註冊</span><span class="sxs-lookup"><span data-stu-id="187b1-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="187b1-113">**有風險的登入**</span><span class="sxs-lookup"><span data-stu-id="187b1-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="187b1-114">有風險的登入復原</span><span class="sxs-lookup"><span data-stu-id="187b1-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="187b1-115">已封鎖有風險的登入</span><span class="sxs-lookup"><span data-stu-id="187b1-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="187b1-116">在有風險的登入期間註冊 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="187b1-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="187b1-117">**有風險的使用者**</span><span class="sxs-lookup"><span data-stu-id="187b1-117">**User at risk**</span></span>

* <span data-ttu-id="187b1-118">遭到入侵的帳戶復原</span><span class="sxs-lookup"><span data-stu-id="187b1-118">Compromised account recovery</span></span>
* <span data-ttu-id="187b1-119">已封鎖遭到入侵的帳戶</span><span class="sxs-lookup"><span data-stu-id="187b1-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="187b1-120">Multi-Factor Authentication 註冊</span><span class="sxs-lookup"><span data-stu-id="187b1-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="187b1-121">hello 最佳的使用者體驗，同時 hello 遭盜用的帳戶復原流程和 hello 危險的登入流程、 hello 使用者可以自行復原時。</span><span class="sxs-lookup"><span data-stu-id="187b1-121">hello best user experience for both, hello compromised account recovery flow and hello risky sign-in flow, is when hello user can self-recover.</span></span> <span data-ttu-id="187b1-122">使用者所註冊的多重要素驗證，如果他們已經有可以使用的 toopass 安全性挑戰其帳戶相關聯的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="187b1-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used toopass security challenges.</span></span> <span data-ttu-id="187b1-123">沒有說明服務台或系統管理員介入是需要的 toorecover 從帳戶遭到入侵。</span><span class="sxs-lookup"><span data-stu-id="187b1-123">No help desk or administrator involvement is needed toorecover from account compromise.</span></span> <span data-ttu-id="187b1-124">因此，強烈建議您 tooget 您的使用者註冊 multi-factor authentication。</span><span class="sxs-lookup"><span data-stu-id="187b1-124">Thus, it’s highly recommended tooget your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="187b1-125">系統管理員可以：</span><span class="sxs-lookup"><span data-stu-id="187b1-125">Administrators can:</span></span>

* <span data-ttu-id="187b1-126">設定原則，需要進行額外安全性驗證的使用者 tooset 註冊他們的帳戶。</span><span class="sxs-lookup"><span data-stu-id="187b1-126">set a policy that requires users tooset up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="187b1-127">允許略過多重要素驗證登錄向上 too30 天，如果他們想 toogive 使用者註冊之前請先在寬限期。</span><span class="sxs-lookup"><span data-stu-id="187b1-127">allow skipping multi-factor authentication registration for up too30 days, in case they want toogive users a grace period before registering.</span></span>

<span data-ttu-id="187b1-128">**hello 多重要素驗證註冊具有三個步驟：**</span><span class="sxs-lookup"><span data-stu-id="187b1-128">**hello multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="187b1-129">在 hello 第一個步驟中，hello 使用者會收到 multi-factor authentication hello 需求 tooset hello 帳戶的相關通知。</span><span class="sxs-lookup"><span data-stu-id="187b1-129">In hello first step, hello user gets a notification about hello requirement tooset hello account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="187b1-130">![補救](./media/active-directory-identityprotection-flows/140.png "補救")</span><span class="sxs-lookup"><span data-stu-id="187b1-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="187b1-131">tooset 註冊多重要素驗證，您需要 toolet hello 系統知道您想 toobe 連絡。</span><span class="sxs-lookup"><span data-stu-id="187b1-131">tooset multi-factor authentication up, you need toolet hello system know how you want toobe contacted.</span></span>
   
    <span data-ttu-id="187b1-132">![補救](./media/active-directory-identityprotection-flows/141.png "補救")</span><span class="sxs-lookup"><span data-stu-id="187b1-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="187b1-133">hello 系統提交挑戰 tooyou，而且您需要 toorespond。</span><span class="sxs-lookup"><span data-stu-id="187b1-133">hello system submits a challenge tooyou and you need toorespond.</span></span>
   
    <span data-ttu-id="187b1-134">![補救](./media/active-directory-identityprotection-flows/142.png "補救")</span><span class="sxs-lookup"><span data-stu-id="187b1-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="187b1-135">有風險的登入復原</span><span class="sxs-lookup"><span data-stu-id="187b1-135">Risky sign-in recovery</span></span>
<span data-ttu-id="187b1-136">系統管理員已設定的原則，登入的風險時嘗試 toosign 中, 會通知 hello 受影響的使用者。</span><span class="sxs-lookup"><span data-stu-id="187b1-136">When an administrator has configured a policy for sign-in risks, hello affected users are notified when they try toosign-in.</span></span> 

<span data-ttu-id="187b1-137">**hello 風險登入流程有兩個步驟：**</span><span class="sxs-lookup"><span data-stu-id="187b1-137">**hello risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="187b1-138">hello 使用者異常偵測其登入，例如從新的位置、 裝置或應用程式登入的相關通知。</span><span class="sxs-lookup"><span data-stu-id="187b1-138">hello user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="187b1-139">![補救](./media/active-directory-identityprotection-flows/120.png "補救")</span><span class="sxs-lookup"><span data-stu-id="187b1-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="187b1-140">hello 使用者所解決的安全性挑戰是必要的 tooprove 其身分識別。</span><span class="sxs-lookup"><span data-stu-id="187b1-140">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="187b1-141">如果 hello 使用者已註冊的多重要素驗證它們需要 tooround 路線安全性程式碼 tootheir 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="187b1-141">If hello user is registered for multi-factor authentication they need tooround-trip a security code tootheir phone number.</span></span> <span data-ttu-id="187b1-142">由於這是僅有風險的登入並遭盜用的帳戶，hello 使用者不需要 toochange hello 密碼，此流程中。</span><span class="sxs-lookup"><span data-stu-id="187b1-142">Since this is a just a risky sign in and not a compromised account, hello user won’t have toochange hello password in this flow.</span></span> 
   
    <span data-ttu-id="187b1-143">![補救](./media/active-directory-identityprotection-flows/121.png "補救")</span><span class="sxs-lookup"><span data-stu-id="187b1-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="187b1-144">已封鎖有風險的登入</span><span class="sxs-lookup"><span data-stu-id="187b1-144">Risky sign-in blocked</span></span>
<span data-ttu-id="187b1-145">系統管理員也可以選擇 tooset 時登入根據 hello 風險層級的登入風險原則 tooblock 使用者。</span><span class="sxs-lookup"><span data-stu-id="187b1-145">Administrators can also choose tooset a Sign-In Risk policy tooblock users upon sign-in depending on hello risk level.</span></span> <span data-ttu-id="187b1-146">解除封鎖 tooget，使用者必須連絡系統管理員或技術服務人員，或嘗試從熟悉的位置或裝置登入。</span><span class="sxs-lookup"><span data-stu-id="187b1-146">tooget unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="187b1-147">藉由解決 Multi-Factor Authentication 自行復原，不是此種情況的適用選項。</span><span class="sxs-lookup"><span data-stu-id="187b1-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="187b1-148">![補救](./media/active-directory-identityprotection-flows/200.png "補救")</span><span class="sxs-lookup"><span data-stu-id="187b1-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="187b1-149">遭到入侵的帳戶復原</span><span class="sxs-lookup"><span data-stu-id="187b1-149">Compromised account recovery</span></span>
<span data-ttu-id="187b1-150">符合 hello 使用者的使用者設定使用者風險安全性原則之後，請風險 hello 原則中指定的層級 (而因此假設危害) 之前他們可以登入，必須經過 hello 使用者洩露復原流程。</span><span class="sxs-lookup"><span data-stu-id="187b1-150">When a user risk security policy has been configured, users who meet hello user risk level specified in hello policy (and are therefore assumed compromised) must go through hello user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="187b1-151">**hello 使用者洩露復原流程有三個步驟：**</span><span class="sxs-lookup"><span data-stu-id="187b1-151">**hello user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="187b1-152">hello 使用者會收到通知，他們的帳戶安全性有風險，因為可疑活動或外洩的認證。</span><span class="sxs-lookup"><span data-stu-id="187b1-152">hello user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="187b1-153">![補救](./media/active-directory-identityprotection-flows/101.png "補救")</span><span class="sxs-lookup"><span data-stu-id="187b1-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="187b1-154">hello 使用者所解決的安全性挑戰是必要的 tooprove 其身分識別。</span><span class="sxs-lookup"><span data-stu-id="187b1-154">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="187b1-155">如果 hello 使用者已註冊的多重要素驗證它們可以自行復原而遭到危害。</span><span class="sxs-lookup"><span data-stu-id="187b1-155">If hello user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="187b1-156">他們必須 tooround 路線安全性程式碼 tootheir 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="187b1-156">They will need tooround-trip a security code tootheir phone number.</span></span> 
   
   <span data-ttu-id="187b1-157">![補救](./media/active-directory-identityprotection-flows/110.png "補救")</span><span class="sxs-lookup"><span data-stu-id="187b1-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="187b1-158">最後，hello 使用者是強制的 toochange 他們的密碼，因為有其他人可能沒有存取 tootheir 帳戶。</span><span class="sxs-lookup"><span data-stu-id="187b1-158">Finally, hello user is forced toochange their password since someone else may have had access tootheir account.</span></span> 
   <span data-ttu-id="187b1-159">這項體驗的螢幕擷取畫面如下。</span><span class="sxs-lookup"><span data-stu-id="187b1-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="187b1-160">![補救](./media/active-directory-identityprotection-flows/111.png "補救")</span><span class="sxs-lookup"><span data-stu-id="187b1-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="187b1-161">已封鎖遭到入侵的帳戶</span><span class="sxs-lookup"><span data-stu-id="187b1-161">Compromised account blocked</span></span>
<span data-ttu-id="187b1-162">tooget 解除封鎖使用者的風險安全性原則所封鎖的使用者，hello 使用者必須連絡管理員或服務台。</span><span class="sxs-lookup"><span data-stu-id="187b1-162">tooget a user that was blocked by a user risk security policy unblocked, hello user must contact an administrator or help desk.</span></span> <span data-ttu-id="187b1-163">藉由解決 Multi-Factor Authentication 自行復原，不是此種情況的適用選項。</span><span class="sxs-lookup"><span data-stu-id="187b1-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="187b1-164">![補救](./media/active-directory-identityprotection-flows/104.png "補救")</span><span class="sxs-lookup"><span data-stu-id="187b1-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="187b1-165">重設密碼</span><span class="sxs-lookup"><span data-stu-id="187b1-165">Reset password</span></span>
<span data-ttu-id="187b1-166">如果遭到入侵的使用者已遭封鎖而無法登入，系統管理員可以為其產生暫時密碼。</span><span class="sxs-lookup"><span data-stu-id="187b1-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="187b1-167">hello 使用者就能 toochange 密碼在下次登入。</span><span class="sxs-lookup"><span data-stu-id="187b1-167">hello users will have toochange their password during a next sign-in.</span></span>

<span data-ttu-id="187b1-168">![補救](./media/active-directory-identityprotection-flows/160.png "補救")</span><span class="sxs-lookup"><span data-stu-id="187b1-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="187b1-169">另請參閱</span><span class="sxs-lookup"><span data-stu-id="187b1-169">See also</span></span>
* [<span data-ttu-id="187b1-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="187b1-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

