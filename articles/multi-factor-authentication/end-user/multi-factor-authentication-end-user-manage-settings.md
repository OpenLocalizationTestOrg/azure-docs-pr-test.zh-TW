---
title: "管理雙步驟驗證設定 | Microsoft Docs"
description: "管理您使用 Azure Multi-Factor Authentication 的方式，包括變更您的連絡資訊或是設定您的裝置。"
services: multi-factor-authentication
keywords: "多重要素驗證用戶端, 驗證的問題, 相互關聯識別碼"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: f752fb19e4ff2f831d50104e9c7d5f42cc3486d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="c6c54-104">管理您的雙步驟驗證設定</span><span class="sxs-lookup"><span data-stu-id="c6c54-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="c6c54-105">本文章回答有關如何更新雙步驟驗證或 Multi-Factor Authentication 的設定。</span><span class="sxs-lookup"><span data-stu-id="c6c54-105">This article answers questions about how to update settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="c6c54-106">如果您登入帳戶時遇到問題，請參閱[雙步驟驗證遇到困難](multi-factor-authentication-end-user-troubleshoot.md)以取得疑難排解說明。</span><span class="sxs-lookup"><span data-stu-id="c6c54-106">If you are having issues signing in to your account, refer to [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-to-find-the-settings-page"></a><span data-ttu-id="c6c54-107">哪裡可以找到設定頁面</span><span class="sxs-lookup"><span data-stu-id="c6c54-107">Where to find the settings page</span></span>
<span data-ttu-id="c6c54-108">視您的公司使用 Azure Multi-Factor Authentication 的方式而定，有一些地方可讓您變更如電話號碼等設定。</span><span class="sxs-lookup"><span data-stu-id="c6c54-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="c6c54-109">如果您的 IT 管理員送出特定的 URL 或步驟來管理雙步驟驗證，請遵循這些指示。</span><span class="sxs-lookup"><span data-stu-id="c6c54-109">If your IT admin sent out a specific URL or steps to manage two-step verification, follow those instructions.</span></span> <span data-ttu-id="c6c54-110">否則，下面的指示應可適用於其他所有人。</span><span class="sxs-lookup"><span data-stu-id="c6c54-110">Otherwise, the following instructions should work for everybody else.</span></span> <span data-ttu-id="c6c54-111">如果您遵循下列步驟，但沒有看到相同的選項，表示您的工作或學校自訂了自己的網站。</span><span class="sxs-lookup"><span data-stu-id="c6c54-111">If you follow these steps but don't see the same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="c6c54-112">請要求系統管理員提供您的 Azure Multi-factor Authentication 入口網站連結。</span><span class="sxs-lookup"><span data-stu-id="c6c54-112">Ask your admin for the link to your Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="c6c54-113">登入 [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="c6c54-113">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="c6c54-114">在右上方選取您的帳戶名稱，然後選取 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="c6c54-114">Select your account name in the top right, then select **profile**.</span></span>  
3. <span data-ttu-id="c6c54-115">選取 [其他安全性驗證]。</span><span class="sxs-lookup"><span data-stu-id="c6c54-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="c6c54-117">[其他安全性驗證] 頁面會載入您的設定。</span><span class="sxs-lookup"><span data-stu-id="c6c54-117">The Additional security verification page loads with your settings.</span></span>

    ![Proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="c6c54-119">我想要變更我的電話號碼，或新增次要號碼</span><span class="sxs-lookup"><span data-stu-id="c6c54-119">I want to change my phone number, or add a secondary number</span></span>
<span data-ttu-id="c6c54-120">請務必設定次要驗證電話號碼。</span><span class="sxs-lookup"><span data-stu-id="c6c54-120">It is important to configure a secondary authentication phone number.</span></span>  <span data-ttu-id="c6c54-121">由於您的主要電話號碼與行動應用程式可能在同一個手機上，因此如果您的手機遺失或遭竊，您只能依靠次要電話號碼恢復使用您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c6c54-121">Because your primary phone number and your mobile app are probably on the same phone, the secondary phone number is the only way you will be able to get back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="c6c54-122">如果您不能存取您的主要電話號碼，並需要協助進入您的帳戶，請參閱我們 [雙步驟驗證遇到困難](multi-factor-authentication-end-user-troubleshoot.md)中的說明主題。</span><span class="sxs-lookup"><span data-stu-id="c6c54-122">If you don't have access to your primary phone number, and need help getting in to your account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="c6c54-123">**若要變更您的主要電話號碼︰**</span><span class="sxs-lookup"><span data-stu-id="c6c54-123">**To change your primary phone number:**</span></span>  

1. <span data-ttu-id="c6c54-124">在 [其他安全性驗證] 頁面上，選取包含目前電話號碼的文字方塊，並使用新的電話號碼進行編輯。</span><span class="sxs-lookup"><span data-stu-id="c6c54-124">On the Additional security verification page, select the text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="c6c54-125">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="c6c54-125">Select **Save**.</span></span>  
3. <span data-ttu-id="c6c54-126">如果這是您針對慣用驗證選項使用的數字，您必須先確定新的數字後，才能進行儲存。</span><span class="sxs-lookup"><span data-stu-id="c6c54-126">If this is the number that you use for your preferred verification option, you have to verify the new number before you can save it.</span></span>  

<span data-ttu-id="c6c54-127">**若要新增次要電話號碼︰**</span><span class="sxs-lookup"><span data-stu-id="c6c54-127">**To add a secondary phone number:**</span></span>  

1. <span data-ttu-id="c6c54-128">在 [其他安全性驗證] 頁面上，勾選 [替代驗證電話] 旁的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="c6c54-128">On the Additional security verification page, check the box next to **Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="c6c54-129">在文字方塊中輸入您的次要電話號碼。</span><span class="sxs-lookup"><span data-stu-id="c6c54-129">Enter your secondary phone number in the text box.</span></span>  
3. <span data-ttu-id="c6c54-130">選取 [儲存] 您的變更即完成。</span><span class="sxs-lookup"><span data-stu-id="c6c54-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="c6c54-131">需要在已標示為受信任的裝置上再次進行雙步驟驗證</span><span class="sxs-lookup"><span data-stu-id="c6c54-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="c6c54-132">根據您組織的設定，當您在您的瀏覽器上執行雙步驟驗證時，您可能會看到核取方塊指出「**X** 天內不要再問我」。</span><span class="sxs-lookup"><span data-stu-id="c6c54-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="c6c54-133">如果核取此方塊然後遺失您的裝置，或認為您的帳戶遭到入侵，您應該將雙步驟驗證還原到所有的裝置。</span><span class="sxs-lookup"><span data-stu-id="c6c54-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification to all your devices.</span></span> 

1. <span data-ttu-id="c6c54-134">在 [其他安全性驗證] 頁面上，選取 [還原先前受信任裝置上的 Multi-Factor Authentication]。</span><span class="sxs-lookup"><span data-stu-id="c6c54-134">On the Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="c6c54-135">下次您在任何裝置上登入時，程式將會提示您執行雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="c6c54-135">The next time you sign in on any device, you'll be prompted to perform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a><span data-ttu-id="c6c54-136">如何清除舊裝置的 Microsoft驗證器並移到新裝置？</span><span class="sxs-lookup"><span data-stu-id="c6c54-136">How do I clean up Microsoft Authenticator from my old device and move to a new one?</span></span>
<span data-ttu-id="c6c54-137">無論您是從裝置解除安裝應用程式或是重設裝置，都不會移除後端的啟動功能。</span><span class="sxs-lookup"><span data-stu-id="c6c54-137">When you uninstall the app from your device or reset the device, it does not remove the activation on the back end.</span></span> <span data-ttu-id="c6c54-138">如需詳細資訊，請參閱 [Microsoft Authenticator](microsoft-authenticator-app-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="c6c54-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6c54-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6c54-139">Next steps</span></span>
* <span data-ttu-id="c6c54-140">取得疑難排解提示以及[使用雙步驟驗證遇到困難](multi-factor-authentication-end-user-troubleshoot.md)的說明。</span><span class="sxs-lookup"><span data-stu-id="c6c54-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="c6c54-141">針對不支援雙步驟驗證的任何應用程式，設定[應用程式密碼](multi-factor-authentication-end-user-app-passwords.md)。</span><span class="sxs-lookup"><span data-stu-id="c6c54-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
