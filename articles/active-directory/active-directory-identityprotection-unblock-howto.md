---
title: "Active Directory 識別身分保護-aaaAzure 如何 toounblock 使用者 |Microsoft 文件"
description: "了解如何解鎖由 Azure Active Directory Identity Protection 原則所封鎖的使用者。"
services: active-directory
keywords: "Azure Active Directory Identity Protection，解鎖使用者"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a><span data-ttu-id="4f220-104">Azure Active Directory 識別身分保護-如何 toounblock 使用者</span><span class="sxs-lookup"><span data-stu-id="4f220-104">Azure Active Directory Identity Protection - How toounblock users</span></span>
<span data-ttu-id="4f220-105">與 Azure Active Directory 識別身分保護，您可以設定符合 tooblock 使用者如果 hello 設定條件的原則。</span><span class="sxs-lookup"><span data-stu-id="4f220-105">With Azure Active Directory Identity Protection, you can configure policies tooblock users if hello configured conditions are satisfied.</span></span> <span data-ttu-id="4f220-106">一般而言，封鎖的使用者的連絡人說明服務人員 toobecome 解除封鎖。</span><span class="sxs-lookup"><span data-stu-id="4f220-106">Typically, a blocked user contacts help desk toobecome unblocked.</span></span> <span data-ttu-id="4f220-107">本主題說明您可以執行 toounblock 封鎖的使用者的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="4f220-107">This topics explains hello steps you can perform toounblock a blocked user.</span></span>

## <a name="determine-hello-reason-for-blocking"></a><span data-ttu-id="4f220-108">判斷有封鎖的 hello 原因</span><span class="sxs-lookup"><span data-stu-id="4f220-108">Determine hello reason for blocking</span></span>
<span data-ttu-id="4f220-109">第一個步驟 toounblock 使用者，您必須已封鎖 hello 使用者，因為您的下一個步驟根據原則 toodetermine hello 型別。</span><span class="sxs-lookup"><span data-stu-id="4f220-109">As a first step toounblock a user, you need toodetermine hello type of policy that has blocked hello user because your next steps are depending on it.</span></span>
<span data-ttu-id="4f220-110">使用 Azure Active Directory Identity Protection 時，使用者可能是因登入風險原則或使用者風險原則而遭封鎖。</span><span class="sxs-lookup"><span data-stu-id="4f220-110">With Azure Active Directory Identity Protection, a user can be either blocked by a sign-in risk policy or a user risk policy.</span></span>

<span data-ttu-id="4f220-111">您可以取得 hello 已封鎖的使用者的登入嘗試期間輸入 toohello 使用者 hello 對話方塊中的 hello 標題的原則類型：</span><span class="sxs-lookup"><span data-stu-id="4f220-111">You can get hello type of policy that has blocked a user from hello heading in hello dialog that was presented toohello user during a sign-in attempt:</span></span>

| <span data-ttu-id="4f220-112">原則</span><span class="sxs-lookup"><span data-stu-id="4f220-112">Policy</span></span> | <span data-ttu-id="4f220-113">使用者對話方塊</span><span class="sxs-lookup"><span data-stu-id="4f220-113">User dialog</span></span> |
| --- | --- |
| <span data-ttu-id="4f220-114">登入風險</span><span class="sxs-lookup"><span data-stu-id="4f220-114">Sign-in risk</span></span> |![封鎖的登入](./media/active-directory-identityprotection-unblock-howto/02.png) |
| <span data-ttu-id="4f220-116">使用者風險</span><span class="sxs-lookup"><span data-stu-id="4f220-116">User risk</span></span> |![封鎖的帳戶](./media/active-directory-identityprotection-unblock-howto/104.png) |

<span data-ttu-id="4f220-118">封鎖使用者的類型為︰</span><span class="sxs-lookup"><span data-stu-id="4f220-118">A user that is blocked by:</span></span>

* <span data-ttu-id="4f220-119">登入風險原則，也就是可疑的登入</span><span class="sxs-lookup"><span data-stu-id="4f220-119">A sign-in risk policy is also known as suspicious sign-in</span></span>
* <span data-ttu-id="4f220-120">使用者風險原則，也就是有風險的帳戶</span><span class="sxs-lookup"><span data-stu-id="4f220-120">A user risk policy is also known as an account at risk</span></span>

## <a name="unblocking-suspicious-sign-ins"></a><span data-ttu-id="4f220-121">解鎖可疑的登入</span><span class="sxs-lookup"><span data-stu-id="4f220-121">Unblocking suspicious sign-ins</span></span>
<span data-ttu-id="4f220-122">toounblock 可疑的登入，您有下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f220-122">toounblock a suspicious sign-in, you have hello following options:</span></span>

1. <span data-ttu-id="4f220-123">**從熟悉的位置或裝置登入** - 可疑的登入會遭封鎖通常是因為使用者嘗試從不熟悉的位置或裝置登入。</span><span class="sxs-lookup"><span data-stu-id="4f220-123">**Sign-in from a familiar location or device** - A common reason for blocked suspicious sign-ins are sign-in attempts from unfamiliar locations or devices.</span></span> <span data-ttu-id="4f220-124">您的使用者可以快速判斷是否 hello toosign 在嘗試從熟悉的位置或裝置來封鎖原因。</span><span class="sxs-lookup"><span data-stu-id="4f220-124">Your users can quickly determine whether this is hello blocking reason by trying toosign-in from a familiar location or device.</span></span>
2. <span data-ttu-id="4f220-125">**從原則中排除**-如果您認為，hello 目前您登入的原則設定會造成特定使用者的問題，您可以 hello 使用者排除它。</span><span class="sxs-lookup"><span data-stu-id="4f220-125">**Exclude from policy** - If you think that hello current configuration of your sign-in policy is causing issues for specific users, you can exclude hello users from it.</span></span> <span data-ttu-id="4f220-126">如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="4f220-126">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>
3. <span data-ttu-id="4f220-127">**停用原則**-如果您認為，原則設定會造成問題的所有使用者，您可以停用 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="4f220-127">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable hello policy.</span></span> <span data-ttu-id="4f220-128">如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="4f220-128">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>

## <a name="unblocking-accounts-at-risk"></a><span data-ttu-id="4f220-129">解鎖有風險的帳戶</span><span class="sxs-lookup"><span data-stu-id="4f220-129">Unblocking accounts at risk</span></span>
<span data-ttu-id="4f220-130">toounblock 的帳戶有風險，您有下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f220-130">toounblock an account at risk, you have hello following options:</span></span>

1. <span data-ttu-id="4f220-131">**重設密碼**-您可以重設 hello 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="4f220-131">**Reset password** - You can reset hello user's password.</span></span> <span data-ttu-id="4f220-132">如需詳細資訊，請參閱 [手動安全密碼重設](active-directory-identityprotection.md#manual-secure-password-reset) 。</span><span class="sxs-lookup"><span data-stu-id="4f220-132">See [manual secure password reset](active-directory-identityprotection.md#manual-secure-password-reset) for more details.</span></span>
2. <span data-ttu-id="4f220-133">**關閉所有的風險事件**-hello 使用者風險原則封鎖的使用者，如果已達到設定的 hello 使用者風險層級是否有封鎖存取。</span><span class="sxs-lookup"><span data-stu-id="4f220-133">**Dismiss all risk events** - hello user risk policy blocks a user if hello configured user risk level for blocking access has been reached.</span></span> <span data-ttu-id="4f220-134">您可以手動關閉已報告的風險事件來降低使用者的風險層級。</span><span class="sxs-lookup"><span data-stu-id="4f220-134">You can reduce a user's risk level by manually closing reported risk events.</span></span> <span data-ttu-id="4f220-135">如需詳細資訊，請參閱 [手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)。</span><span class="sxs-lookup"><span data-stu-id="4f220-135">For more details, see [closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>
3. <span data-ttu-id="4f220-136">**從原則中排除**-如果您認為，hello 目前您登入的原則設定會造成特定使用者的問題，您可以 hello 使用者排除它。</span><span class="sxs-lookup"><span data-stu-id="4f220-136">**Exclude from policy** - If you think that hello current configuration of your sign-in policy is causing issues for specific users, you can exclude hello users from it.</span></span> <span data-ttu-id="4f220-137">如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="4f220-137">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>
4. <span data-ttu-id="4f220-138">**停用原則**-如果您認為，原則設定會造成問題的所有使用者，您可以停用 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="4f220-138">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable hello policy.</span></span> <span data-ttu-id="4f220-139">如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="4f220-139">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f220-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f220-140">Next steps</span></span>
 <span data-ttu-id="4f220-141">您想深入了解 Azure AD Identity Protection tooknow 嗎？</span><span class="sxs-lookup"><span data-stu-id="4f220-141">Do you want tooknow more about Azure AD Identity Protection?</span></span> <span data-ttu-id="4f220-142">查看 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="4f220-142">Check out [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>
