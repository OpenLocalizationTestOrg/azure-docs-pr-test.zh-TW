---
title: "aaaTroubleshoot Azure 註冊問題 |Microsoft 文件"
description: "描述如何 tootroubleshoot 某些常見的 Azure 註冊問題。"
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee649bfc3be7ba1fe2dd863fac09e1c2311d835b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a><span data-ttu-id="dd74f-103">針對 Azure 的註冊問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="dd74f-103">Troubleshoot sign-up issues for Azure</span></span>
<span data-ttu-id="dd74f-104">如果您無法註冊 Azure，請在此發行項 tootroubleshoot 常見的問題使用 hello 秘訣。</span><span class="sxs-lookup"><span data-stu-id="dd74f-104">If you can't sign up for Azure, use hello tips in this article tootroubleshoot common issues.</span></span> <span data-ttu-id="dd74f-105">如果在註冊期間遇到信用卡的問題，請參閱[在 Azure 註冊時信用卡或金融卡遭到拒絕](billing-credit-card-fails-during-azure-sign-up.md)。</span><span class="sxs-lookup"><span data-stu-id="dd74f-105">If you have an issue with your credit card during sign-up, see [your debit card or credit card is declined at Azure sign-up](billing-credit-card-fails-during-azure-sign-up.md).</span></span> <span data-ttu-id="dd74f-106">如果您有 Azure 帳戶，但無法登入，請參閱[無法登入 toomanage 我 Azure 訂用帳戶](billing-cannot-login-subscription.md)。</span><span class="sxs-lookup"><span data-stu-id="dd74f-106">If you have an Azure account but can't sign in, see [I can't sign in toomanage my Azure subscription](billing-cannot-login-subscription.md).</span></span>

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a><span data-ttu-id="dd74f-107">[依據卡片進行身分識別驗證] 區段中的進度列停止回應</span><span class="sxs-lookup"><span data-stu-id="dd74f-107">Progress bar hangs in "Identity verification by card" section</span></span>

<span data-ttu-id="dd74f-108">卡 toocomplete hello 身分識別驗證，您的瀏覽器必須允許第三方 cookie。</span><span class="sxs-lookup"><span data-stu-id="dd74f-108">toocomplete hello identity verification by card, third-party cookies must be allowed for your browser.</span></span>

![Hello 卡區段在註冊期間溢出的身分識別驗證的螢幕擷取畫面](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

<span data-ttu-id="dd74f-110">使用下列步驟 tooupdate hello 瀏覽器的 cookie 設定。</span><span class="sxs-lookup"><span data-stu-id="dd74f-110">Use hello following steps tooupdate your browser's cookie settings.</span></span>

1. <span data-ttu-id="dd74f-111">如果您使用 Chrome，請移至太**設定** > **顯示進階設定** > **隱私權** > **內容設定**。</span><span class="sxs-lookup"><span data-stu-id="dd74f-111">If you're using Chrome, go too**Settings** > **Show advanced settings** > **Privacy** > **Content settings**.</span></span> <span data-ttu-id="dd74f-112">取消選取 [封鎖第三方 Cookie 和網站資料]。</span><span class="sxs-lookup"><span data-stu-id="dd74f-112">Uncheck **Block third-party cookies and site data**.</span></span>
2. <span data-ttu-id="dd74f-113">如果您使用邊緣，請移至太**設定** > **檢視進階設定** > **Cookie**。</span><span class="sxs-lookup"><span data-stu-id="dd74f-113">If you're using Edge, go too**Settings** > **View advanced settings** > **Cookies**.</span></span> <span data-ttu-id="dd74f-114">選取 [不要封鎖 Cookie]。</span><span class="sxs-lookup"><span data-stu-id="dd74f-114">Select **Don't block cookies**.</span></span>
3. <span data-ttu-id="dd74f-115">重新整理 hello Azure 註冊頁面上，並檢查是否已解決 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="dd74f-115">Refresh hello Azure sign-up page, and check if hello problem is resolved.</span></span>
4. <span data-ttu-id="dd74f-116">如果 hello 重新整理後仍無法解決 hello 問題，請結束並重新啟動瀏覽器然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="dd74f-116">If hello refresh didn't solve hello issue, quit and restart your browser then try again.</span></span>

## <a name="credit-card-form-doesnt-support-my-billing-address"></a><span data-ttu-id="dd74f-117">信用卡表單不支援我的帳單地址</span><span class="sxs-lookup"><span data-stu-id="dd74f-117">Credit card form doesn't support my billing address</span></span>
<span data-ttu-id="dd74f-118">帳單地址必須在您選取在 hello hello 國家/地區的 toobe**關於您**> 一節。</span><span class="sxs-lookup"><span data-stu-id="dd74f-118">Your billing address needs toobe in hello country that you selected in hello **About you** section.</span></span> <span data-ttu-id="dd74f-119">請確定您選取 hello 正確的國家/地區。</span><span class="sxs-lookup"><span data-stu-id="dd74f-119">Make sure you select hello correct country.</span></span>

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a><span data-ttu-id="dd74f-120">註冊帳戶驗證期間沒有文字訊息或呼叫</span><span class="sxs-lookup"><span data-stu-id="dd74f-120">No text messages or calls during sign-up account verification</span></span>
<span data-ttu-id="dd74f-121">雖然通常會更快，就會在傳送驗證碼 toobe toofour 分鐘。</span><span class="sxs-lookup"><span data-stu-id="dd74f-121">While it is usually much faster, it may take up toofour minutes for verification code toobe delivered.</span></span> <span data-ttu-id="dd74f-122">您輸入驗證 hello 電話號碼不儲存為 hello 帳號的連絡電話號碼。</span><span class="sxs-lookup"><span data-stu-id="dd74f-122">hello phone number you enter for verification isn't stored as a contact number for hello account.</span></span>

<span data-ttu-id="dd74f-123">以下是一些其他的祕訣：</span><span class="sxs-lookup"><span data-stu-id="dd74f-123">Here are some additional tips:</span></span>
* <span data-ttu-id="dd74f-124">VOIP 電話號碼不能用於 hello 電話驗證程序。</span><span class="sxs-lookup"><span data-stu-id="dd74f-124">A VOIP phone number can't be used for hello phone verification process.</span></span>
* <span data-ttu-id="dd74f-125">檢查輸入，包括您在 [hello] 下拉式功能表中選取的 hello 國碼 hello 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="dd74f-125">Double check hello phone number you enter, including hello country code you selected in hello dropdown menu.</span></span>
* <span data-ttu-id="dd74f-126">如果您的電話未收到簡訊 (SMS)，再試一次 hello**撥號給我**選項。</span><span class="sxs-lookup"><span data-stu-id="dd74f-126">If your phone doesn't receive text messages (SMS), try hello **Call me** option.</span></span>
* <span data-ttu-id="dd74f-127">請確定您的電話可以接收來自美國電話號碼的來電或簡訊。</span><span class="sxs-lookup"><span data-stu-id="dd74f-127">Ensure that your phone can receive calls or SMS messages from a United States based number.</span></span>

<span data-ttu-id="dd74f-128">當您取得 hello 簡訊或電話時，輸入程式碼，您會收到 hello 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="dd74f-128">When you get hello text message or phone call, enter code that you receive into hello text box.</span></span>

## <a name="credit-card-declined-or-not-accepted"></a><span data-ttu-id="dd74f-129">信用卡被拒絕或不被接受</span><span class="sxs-lookup"><span data-stu-id="dd74f-129">Credit card declined or not accepted</span></span>
<span data-ttu-id="dd74f-130">虛擬卡、預付信用卡或金融卡不被視為 Azure 訂用帳戶的付款方式。</span><span class="sxs-lookup"><span data-stu-id="dd74f-130">Virtual or prepaid credit or debit cards aren't accepted as payment for Azure subscriptions.</span></span> <span data-ttu-id="dd74f-131">toosee 還發生了什麼可能會造成您的卡片 toobe 拒絕，請參閱[您的信用卡或扣款卡被拒絕，以註冊 Azure](billing-credit-card-fails-during-azure-sign-up.md)。</span><span class="sxs-lookup"><span data-stu-id="dd74f-131">toosee what else may cause your card toobe declined, see [your debit card or credit card is declined at Azure sign-up](billing-credit-card-fails-during-azure-sign-up.md).</span></span>

## <a name="free-trial-is-not-available"></a><span data-ttu-id="dd74f-132">「無法使用免費試用版」</span><span class="sxs-lookup"><span data-stu-id="dd74f-132">"Free Trial is not available"</span></span>
<span data-ttu-id="dd74f-133">您使用 Azure 訂用帳戶中的 hello 過去嗎？hello Azure 使用規定限制僅針對該使用者是新 tooAzure 免費試用啟用。</span><span class="sxs-lookup"><span data-stu-id="dd74f-133">Have you used an Azure subscription in hello past? hello Azure Terms of Use agreement limits free trial activation only for a user that's new tooAzure.</span></span> <span data-ttu-id="dd74f-134">如果您有任何其他類型的 Azure 訂用帳戶，會無法啟用免費試用。</span><span class="sxs-lookup"><span data-stu-id="dd74f-134">If you have had any other type of Azure subscription, you can't activate a free trial.</span></span> <span data-ttu-id="dd74f-135">請考慮註冊[隨用隨付訂用帳戶](https://azure.microsoft.com/offers/ms-azr-0003p/)。</span><span class="sxs-lookup"><span data-stu-id="dd74f-135">Consider signing up for a [Pay-As-You-Go subscription](https://azure.microsoft.com/offers/ms-azr-0003p/).</span></span>

## <a name="i-saw-a-charge-on-my-free-trial-account"></a><span data-ttu-id="dd74f-136">我的免費試用帳戶收到一筆費用</span><span class="sxs-lookup"><span data-stu-id="dd74f-136">I saw a charge on my Free Trial account</span></span>
<span data-ttu-id="dd74f-137">您可能會看到一個小型您登入設定，這會移除 3 too5 天內後保留在您的信用卡帳戶驗證。</span><span class="sxs-lookup"><span data-stu-id="dd74f-137">You may see a small verification hold on your credit card account after you sign up, which is removed within 3 too5 days.</span></span> <span data-ttu-id="dd74f-138">如果您擔心管理成本，請深入了解[如何避免非預期的成本](https://docs.microsoft.com/azure/billing/billing-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="dd74f-138">If you are worried about managing costs, read more about [preventing unexpected costs](https://docs.microsoft.com/azure/billing/billing-getting-started).</span></span>

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a><span data-ttu-id="dd74f-139">無法啟用 MSDN、BizSpark、BizSparkPlus 或 MPN 之類的 Azure 權益方案</span><span class="sxs-lookup"><span data-stu-id="dd74f-139">Can’t activate Azure benefit plan like MSDN, BizSpark, BizSparkPlus, or MPN</span></span>
<span data-ttu-id="dd74f-140">請確定您使用 hello 右登入認證。</span><span class="sxs-lookup"><span data-stu-id="dd74f-140">Make sure that you're using hello right sign-in credentials.</span></span> <span data-ttu-id="dd74f-141">然後檢查 hello 權益程式 toomake 確定您符合資格。</span><span class="sxs-lookup"><span data-stu-id="dd74f-141">Then check hello benefit program toomake sure that you're eligible.</span></span> 

* <span data-ttu-id="dd74f-142">MSDN</span><span class="sxs-lookup"><span data-stu-id="dd74f-142">MSDN</span></span>
  * <span data-ttu-id="dd74f-143">請在您的 [MSDN 帳戶頁面](https://msdn.microsoft.com/subscriptions/manage/default.aspx)驗證自己的資格狀態。</span><span class="sxs-lookup"><span data-stu-id="dd74f-143">Verify your eligibility status in your [MSDN account page](https://msdn.microsoft.com/subscriptions/manage/default.aspx).</span></span>
  * <span data-ttu-id="dd74f-144">如果您無法驗證您的狀態，請連絡 hello [MSDN 訂用帳戶客戶服務中心](https://msdn.microsoft.com/subscriptions/contactus.aspx)</span><span class="sxs-lookup"><span data-stu-id="dd74f-144">If you can't verify your status, contact hello [MSDN Subscriptions Customer Service Centers](https://msdn.microsoft.com/subscriptions/contactus.aspx)</span></span>
* <span data-ttu-id="dd74f-145">BizSpark</span><span class="sxs-lookup"><span data-stu-id="dd74f-145">BizSpark</span></span>
  * <span data-ttu-id="dd74f-146">登入 toohello [BizSpark 入口網站](https://www.microsoft.com/bizspark/default.aspx#start-two)和 BizSpark 和 BizSpark 加號確認資格狀態。</span><span class="sxs-lookup"><span data-stu-id="dd74f-146">Sign in toohello [BizSpark portal](https://www.microsoft.com/bizspark/default.aspx#start-two) and verify your eligibility status for BizSpark and BizSpark Plus.</span></span>
  * <span data-ttu-id="dd74f-147">如果您無法驗證您的狀態，您可以[在 hello BizSpark 論壇取得說明](http://aka.ms/bzforums)。</span><span class="sxs-lookup"><span data-stu-id="dd74f-147">If you can't verify your status, you can [get help at hello BizSpark forums](http://aka.ms/bzforums).</span></span>
* <span data-ttu-id="dd74f-148">MPN</span><span class="sxs-lookup"><span data-stu-id="dd74f-148">MPN</span></span>
  * <span data-ttu-id="dd74f-149">登入 toohello [MPN 入口網站](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx)並驗證資格狀態。</span><span class="sxs-lookup"><span data-stu-id="dd74f-149">Sign in toohello [MPN portal](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) and verify your eligibility status.</span></span> <span data-ttu-id="dd74f-150">如果您有適當的 hello[雲端平台能力](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx)，您可進行額外的好處。</span><span class="sxs-lookup"><span data-stu-id="dd74f-150">If you have hello appropriate [Cloud Platform Competencies](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), you may be eligible for additional benefits.</span></span>
  * <span data-ttu-id="dd74f-151">如果您無法驗證自己的狀態，請連絡 [MPN 支援](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dd74f-151">If you can't verify your status, contact [MPN support](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).</span></span>

## <a name="cant-activate-new-azure-in-open-subscription"></a><span data-ttu-id="dd74f-152">無法啟用新的 Azure in Open 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dd74f-152">Can’t activate new Azure In Open subscription</span></span>
<span data-ttu-id="dd74f-153">toocreate 開啟中 Azure 訂用帳戶，您必須至少一個 「 開啟 Azure 中的語彙基元相關聯 tooit 與有效的線上服務啟用 (OSA) 金鑰。</span><span class="sxs-lookup"><span data-stu-id="dd74f-153">toocreate an Azure In Open subscription, you must have a valid Online Service Activation (OSA) key with at least one Azure In Open token associated tooit.</span></span> <span data-ttu-id="dd74f-154">如果您沒有 OSA 金鑰，請連絡 [Microsoft Pinpoint](http://pinpoint.microsoft.com/) 中列出的其中一個 Microsoft 合作夥伴。</span><span class="sxs-lookup"><span data-stu-id="dd74f-154">If you don't have an OSA key, contact one of Microsoft Partners listed in [Microsoft Pinpoint](http://pinpoint.microsoft.com/).</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="dd74f-155">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="dd74f-155">Need help?</span></span> <span data-ttu-id="dd74f-156">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="dd74f-156">Contact support.</span></span>
<span data-ttu-id="dd74f-157">如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="dd74f-157">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
