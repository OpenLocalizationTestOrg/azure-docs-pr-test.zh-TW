---
title: "Azure Active Directory Identity Protection - 如何將使用者解除封鎖 | Microsoft Docs"
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
ms.openlocfilehash: ce6b2805e7281dff7752a73ada86be11d7e01fc3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection---how-to-unblock-users"></a><span data-ttu-id="33418-104">Azure Active Directory Identity Protection - 如何解鎖使用者</span><span class="sxs-lookup"><span data-stu-id="33418-104">Azure Active Directory Identity Protection - How to unblock users</span></span>
<span data-ttu-id="33418-105">使用 Azure Active Directory Identity Protection 時，如果符合設定的條件，您就可以設定原則來封鎖使用者。</span><span class="sxs-lookup"><span data-stu-id="33418-105">With Azure Active Directory Identity Protection, you can configure policies to block users if the configured conditions are satisfied.</span></span> <span data-ttu-id="33418-106">一般而言，遭封鎖的使用者會聯絡服務台以解除封鎖。</span><span class="sxs-lookup"><span data-stu-id="33418-106">Typically, a blocked user contacts help desk to become unblocked.</span></span> <span data-ttu-id="33418-107">本主題說明解鎖遭封鎖使用者的執行步驟。</span><span class="sxs-lookup"><span data-stu-id="33418-107">This topics explains the steps you can perform to unblock a blocked user.</span></span>

## <a name="determine-the-reason-for-blocking"></a><span data-ttu-id="33418-108">判斷封鎖的原因</span><span class="sxs-lookup"><span data-stu-id="33418-108">Determine the reason for blocking</span></span>
<span data-ttu-id="33418-109">解鎖使用者的第一個步驟，您需要判斷封鎖使用者的原則類型為何，以決定後續步驟。</span><span class="sxs-lookup"><span data-stu-id="33418-109">As a first step to unblock a user, you need to determine the type of policy that has blocked the user because your next steps are depending on it.</span></span>
<span data-ttu-id="33418-110">使用 Azure Active Directory Identity Protection 時，使用者可能是因登入風險原則或使用者風險原則而遭封鎖。</span><span class="sxs-lookup"><span data-stu-id="33418-110">With Azure Active Directory Identity Protection, a user can be either blocked by a sign-in risk policy or a user risk policy.</span></span>

<span data-ttu-id="33418-111">您可以從使用者嘗試登入期間所出現的對話方塊標題取得封鎖使用者的原則類型︰</span><span class="sxs-lookup"><span data-stu-id="33418-111">You can get the type of policy that has blocked a user from the heading in the dialog that was presented to the user during a sign-in attempt:</span></span>

| <span data-ttu-id="33418-112">原則</span><span class="sxs-lookup"><span data-stu-id="33418-112">Policy</span></span> | <span data-ttu-id="33418-113">使用者對話方塊</span><span class="sxs-lookup"><span data-stu-id="33418-113">User dialog</span></span> |
| --- | --- |
| <span data-ttu-id="33418-114">登入風險</span><span class="sxs-lookup"><span data-stu-id="33418-114">Sign-in risk</span></span> |![封鎖的登入](./media/active-directory-identityprotection-unblock-howto/02.png) |
| <span data-ttu-id="33418-116">使用者風險</span><span class="sxs-lookup"><span data-stu-id="33418-116">User risk</span></span> |![封鎖的帳戶](./media/active-directory-identityprotection-unblock-howto/104.png) |

<span data-ttu-id="33418-118">封鎖使用者的類型為︰</span><span class="sxs-lookup"><span data-stu-id="33418-118">A user that is blocked by:</span></span>

* <span data-ttu-id="33418-119">登入風險原則，也就是可疑的登入</span><span class="sxs-lookup"><span data-stu-id="33418-119">A sign-in risk policy is also known as suspicious sign-in</span></span>
* <span data-ttu-id="33418-120">使用者風險原則，也就是有風險的帳戶</span><span class="sxs-lookup"><span data-stu-id="33418-120">A user risk policy is also known as an account at risk</span></span>

## <a name="unblocking-suspicious-sign-ins"></a><span data-ttu-id="33418-121">解鎖可疑的登入</span><span class="sxs-lookup"><span data-stu-id="33418-121">Unblocking suspicious sign-ins</span></span>
<span data-ttu-id="33418-122">若要解鎖可疑的登入，您有下列選擇︰</span><span class="sxs-lookup"><span data-stu-id="33418-122">To unblock a suspicious sign-in, you have the following options:</span></span>

1. <span data-ttu-id="33418-123">**從熟悉的位置或裝置登入** - 可疑的登入會遭封鎖通常是因為使用者嘗試從不熟悉的位置或裝置登入。</span><span class="sxs-lookup"><span data-stu-id="33418-123">**Sign-in from a familiar location or device** - A common reason for blocked suspicious sign-ins are sign-in attempts from unfamiliar locations or devices.</span></span> <span data-ttu-id="33418-124">使用者可以嘗試從熟悉的位置或裝置登入，以迅速判斷這是否是遭封鎖的原因。</span><span class="sxs-lookup"><span data-stu-id="33418-124">Your users can quickly determine whether this is the blocking reason by trying to sign-in from a familiar location or device.</span></span>
2. <span data-ttu-id="33418-125">**從原則中排除** - 如果您認為目前的登入原則設定對特定使用者造成問題，您可以排除這些使用者。</span><span class="sxs-lookup"><span data-stu-id="33418-125">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span></span> <span data-ttu-id="33418-126">如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="33418-126">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>
3. <span data-ttu-id="33418-127">**停用原則** - 如果您認為您的原則設定對所有使用者造成問題，您可以停用原則。</span><span class="sxs-lookup"><span data-stu-id="33418-127">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span></span> <span data-ttu-id="33418-128">如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="33418-128">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>

## <a name="unblocking-accounts-at-risk"></a><span data-ttu-id="33418-129">解鎖有風險的帳戶</span><span class="sxs-lookup"><span data-stu-id="33418-129">Unblocking accounts at risk</span></span>
<span data-ttu-id="33418-130">若要解鎖有風險的帳戶，您有下列選擇︰</span><span class="sxs-lookup"><span data-stu-id="33418-130">To unblock an account at risk, you have the following options:</span></span>

1. <span data-ttu-id="33418-131">**重設密碼** - 您可以重設使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="33418-131">**Reset password** - You can reset the user's password.</span></span> <span data-ttu-id="33418-132">如需詳細資訊，請參閱 [手動安全密碼重設](active-directory-identityprotection.md#manual-secure-password-reset) 。</span><span class="sxs-lookup"><span data-stu-id="33418-132">See [manual secure password reset](active-directory-identityprotection.md#manual-secure-password-reset) for more details.</span></span>
2. <span data-ttu-id="33418-133">**關閉所有風險事件** - 如果已達到設定的封鎖存取權限之使用者風險層級，使用者風險原則就會封鎖使用者。</span><span class="sxs-lookup"><span data-stu-id="33418-133">**Dismiss all risk events** - The user risk policy blocks a user if the configured user risk level for blocking access has been reached.</span></span> <span data-ttu-id="33418-134">您可以手動關閉已報告的風險事件來降低使用者的風險層級。</span><span class="sxs-lookup"><span data-stu-id="33418-134">You can reduce a user's risk level by manually closing reported risk events.</span></span> <span data-ttu-id="33418-135">如需詳細資訊，請參閱 [手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)。</span><span class="sxs-lookup"><span data-stu-id="33418-135">For more details, see [closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>
3. <span data-ttu-id="33418-136">**從原則中排除** - 如果您認為目前的登入原則設定對特定使用者造成問題，您可以排除這些使用者。</span><span class="sxs-lookup"><span data-stu-id="33418-136">**Exclude from policy** - If you think that the current configuration of your sign-in policy is causing issues for specific users, you can exclude the users from it.</span></span> <span data-ttu-id="33418-137">如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="33418-137">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>
4. <span data-ttu-id="33418-138">**停用原則** - 如果您認為您的原則設定對所有使用者造成問題，您可以停用原則。</span><span class="sxs-lookup"><span data-stu-id="33418-138">**Disable policy** - If you think that your policy configuration is causing issues for all your users, you can disable the policy.</span></span> <span data-ttu-id="33418-139">如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="33418-139">See [Azure Active Directory Identity Protection](active-directory-identityprotection.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33418-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33418-140">Next steps</span></span>
 <span data-ttu-id="33418-141">您想要深入了解 Azure AD Identity Protection？</span><span class="sxs-lookup"><span data-stu-id="33418-141">Do you want to know more about Azure AD Identity Protection?</span></span> <span data-ttu-id="33418-142">查看 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="33418-142">Check out [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>
