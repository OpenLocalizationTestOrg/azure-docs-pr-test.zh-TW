---
title: "aaaManage 雙步驟驗證設定 |Microsoft 文件"
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
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="d7dc4-104">管理您的雙步驟驗證設定</span><span class="sxs-lookup"><span data-stu-id="d7dc4-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="d7dc4-105">本文回答有關的問題 tooupdate 設定進行兩步驟驗證或多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-105">This article answers questions about how tooupdate settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="d7dc4-106">如果您有登入 tooyour 帳戶的問題，請參閱太[遇到雙步驟驗證](multi-factor-authentication-end-user-troubleshoot.md)的疑難排解說明。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-106">If you are having issues signing in tooyour account, refer too[Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-toofind-hello-settings-page"></a><span data-ttu-id="d7dc4-107">其中 toofind hello 設定 頁面</span><span class="sxs-lookup"><span data-stu-id="d7dc4-107">Where toofind hello settings page</span></span>
<span data-ttu-id="d7dc4-108">視您的公司使用 Azure Multi-Factor Authentication 的方式而定，有一些地方可讓您變更如電話號碼等設定。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="d7dc4-109">如果您的 IT 管理員送出特定的 URL 或步驟 toomanage 雙步驟驗證，請遵循這些指示。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-109">If your IT admin sent out a specific URL or steps toomanage two-step verification, follow those instructions.</span></span> <span data-ttu-id="d7dc4-110">否則，請遵循指示 hello 應該適用其他人。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-110">Otherwise, hello following instructions should work for everybody else.</span></span> <span data-ttu-id="d7dc4-111">如果您遵循這些步驟，但看不到 hello 相同的選項，這表示您的工作或學校自訂自己的入口網站。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-111">If you follow these steps but don't see hello same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="d7dc4-112">您的系統管理員尋求 hello 連結 tooyour Azure Multi-factor Authentication 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-112">Ask your admin for hello link tooyour Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="d7dc4-113">登入太[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="d7dc4-113">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="d7dc4-114">Hello 右上方，選取您的帳戶名稱，然後選取**設定檔**。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-114">Select your account name in hello top right, then select **profile**.</span></span>  
3. <span data-ttu-id="d7dc4-115">選取 [其他安全性驗證]。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="d7dc4-117">hello 其他安全性驗證頁面載入的設定。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-117">hello Additional security verification page loads with your settings.</span></span>

    ![Proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="d7dc4-119">我想 toochange 我的電話號碼，或新增次要號碼</span><span class="sxs-lookup"><span data-stu-id="d7dc4-119">I want toochange my phone number, or add a secondary number</span></span>
<span data-ttu-id="d7dc4-120">它是重要 tooconfigure 次要驗證電話號碼。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-120">It is important tooconfigure a secondary authentication phone number.</span></span>  <span data-ttu-id="d7dc4-121">因為您的主要電話號碼和您的行動裝置應用程式都可能在 hello 相同電話，hello 次要的電話號碼是 hello 唯一的方式，您將會無法 tooget 回您的帳戶，如果您的手機遺失或遭竊。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-121">Because your primary phone number and your mobile app are probably on hello same phone, hello secondary phone number is hello only way you will be able tooget back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="d7dc4-122">如果您不具有存取 tooyour 主要電話號碼，而需要取得 tooyour 帳戶中的說明，請參閱我們的說明主題中[遇到雙步驟驗證](multi-factor-authentication-end-user-troubleshoot.md)。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-122">If you don't have access tooyour primary phone number, and need help getting in tooyour account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="d7dc4-123">**toochange 您的主要電話號碼：**</span><span class="sxs-lookup"><span data-stu-id="d7dc4-123">**toochange your primary phone number:**</span></span>  

1. <span data-ttu-id="d7dc4-124">在 hello 其他安全性驗證 頁面上，選取與您目前的電話號碼的 hello 文字方塊中，編輯與新的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-124">On hello Additional security verification page, select hello text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="d7dc4-125">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-125">Select **Save**.</span></span>  
3. <span data-ttu-id="d7dc4-126">如果這是您使用您的慣用的驗證選項的 hello 數目時，才可儲存有 tooverify hello 新數字。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-126">If this is hello number that you use for your preferred verification option, you have tooverify hello new number before you can save it.</span></span>  

<span data-ttu-id="d7dc4-127">**tooadd 次要的電話號碼：**</span><span class="sxs-lookup"><span data-stu-id="d7dc4-127">**tooadd a secondary phone number:**</span></span>  

1. <span data-ttu-id="d7dc4-128">在 hello 其他安全性驗證 頁面上，核取 hello 方塊旁太**替代驗證電話。**</span><span class="sxs-lookup"><span data-stu-id="d7dc4-128">On hello Additional security verification page, check hello box next too**Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="d7dc4-129">在 hello 文字方塊中輸入您的第二個電話號碼。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-129">Enter your secondary phone number in hello text box.</span></span>  
3. <span data-ttu-id="d7dc4-130">選取 [儲存] 您的變更即完成。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="d7dc4-131">需要在已標示為受信任的裝置上再次進行雙步驟驗證</span><span class="sxs-lookup"><span data-stu-id="d7dc4-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="d7dc4-132">根據您組織的設定，當您在您的瀏覽器上執行雙步驟驗證時，您可能會看到核取方塊指出「**X** 天內不要再問我」。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="d7dc4-133">如果您核取此方塊，然後遺失裝置或認為您的帳戶遭到洩露時，您應該還原兩步驟驗證 tooall 您的裝置。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification tooall your devices.</span></span> 

1. <span data-ttu-id="d7dc4-134">在 hello 其他安全性驗證 頁面上，選取 **先前所信任的裝置上還原多重要素驗證**。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-134">On hello Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="d7dc4-135">hello 下次您任何裝置登入，您將會提示的 tooperform 雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-135">hello next time you sign in on any device, you'll be prompted tooperform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a><span data-ttu-id="d7dc4-136">如何從我的舊裝置清除 Microsoft Authenticator 和移動 tooa 新？</span><span class="sxs-lookup"><span data-stu-id="d7dc4-136">How do I clean up Microsoft Authenticator from my old device and move tooa new one?</span></span>
<span data-ttu-id="d7dc4-137">當您解除 hello 應用程式安裝從您的裝置或重設的 hello 裝置時，它不會移除 hello 啟用 hello 後端。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-137">When you uninstall hello app from your device or reset hello device, it does not remove hello activation on hello back end.</span></span> <span data-ttu-id="d7dc4-138">如需詳細資訊，請參閱 [Microsoft Authenticator](microsoft-authenticator-app-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7dc4-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d7dc4-139">Next steps</span></span>
* <span data-ttu-id="d7dc4-140">取得疑難排解提示以及[使用雙步驟驗證遇到困難](multi-factor-authentication-end-user-troubleshoot.md)的說明。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="d7dc4-141">針對不支援雙步驟驗證的任何應用程式，設定[應用程式密碼](multi-factor-authentication-end-user-app-passwords.md)。</span><span class="sxs-lookup"><span data-stu-id="d7dc4-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
