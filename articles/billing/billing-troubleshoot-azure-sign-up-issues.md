---
title: "針對 Azure 註冊問題進行疑難排解 | Microsoft Docs"
description: "說明如何疑難排解一些常見 Azure 登入問題。"
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
ms.openlocfilehash: 647509ea36e487aca5db661adb3268e845988f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a><span data-ttu-id="cca1a-103">針對 Azure 的註冊問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="cca1a-103">Troubleshoot sign-up issues for Azure</span></span>
<span data-ttu-id="cca1a-104">如果您無法註冊 Azure，請使用此文章中的祕訣來針對常見問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="cca1a-104">If you can't sign up for Azure, use the tips in this article to troubleshoot common issues.</span></span> <span data-ttu-id="cca1a-105">如果在註冊期間遇到信用卡的問題，請參閱[在 Azure 註冊時信用卡或金融卡遭到拒絕](billing-credit-card-fails-during-azure-sign-up.md)。</span><span class="sxs-lookup"><span data-stu-id="cca1a-105">If you have an issue with your credit card during sign-up, see [your debit card or credit card is declined at Azure sign-up](billing-credit-card-fails-during-azure-sign-up.md).</span></span> <span data-ttu-id="cca1a-106">如果您有 Azure 帳戶但無法登入，請參閱[我無法登入來管理我的 Azure 訂用帳戶](billing-cannot-login-subscription.md)。</span><span class="sxs-lookup"><span data-stu-id="cca1a-106">If you have an Azure account but can't sign in, see [I can't sign in to manage my Azure subscription](billing-cannot-login-subscription.md).</span></span>

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a><span data-ttu-id="cca1a-107">[依據卡片進行身分識別驗證] 區段中的進度列停止回應</span><span class="sxs-lookup"><span data-stu-id="cca1a-107">Progress bar hangs in "Identity verification by card" section</span></span>

<span data-ttu-id="cca1a-108">若要使用卡片完成身分識別驗證，您必須允許瀏覽器接受第三方 Cookie。</span><span class="sxs-lookup"><span data-stu-id="cca1a-108">To complete the identity verification by card, third-party cookies must be allowed for your browser.</span></span>

![註冊時 [依據卡片進行身分識別驗證] 區段停止回應的螢幕擷取畫面](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

<span data-ttu-id="cca1a-110">使用下列步驟來更新瀏覽器的 Cookie 設定。</span><span class="sxs-lookup"><span data-stu-id="cca1a-110">Use the following steps to update your browser's cookie settings.</span></span>

1. <span data-ttu-id="cca1a-111">如果您是使用 Chrome，請移至 [設定]  > [顯示進階設定] > [隱私權] > [內容設定]。</span><span class="sxs-lookup"><span data-stu-id="cca1a-111">If you're using Chrome, go to **Settings** > **Show advanced settings** > **Privacy** > **Content settings**.</span></span> <span data-ttu-id="cca1a-112">取消選取 [封鎖第三方 Cookie 和網站資料]。</span><span class="sxs-lookup"><span data-stu-id="cca1a-112">Uncheck **Block third-party cookies and site data**.</span></span>
2. <span data-ttu-id="cca1a-113">如果您是使用 Edge，請移至 [設定]  > [檢視進階設定][Cookie] > 。</span><span class="sxs-lookup"><span data-stu-id="cca1a-113">If you're using Edge, go to **Settings** > **View advanced settings** > **Cookies**.</span></span> <span data-ttu-id="cca1a-114">選取 [不要封鎖 Cookie]。</span><span class="sxs-lookup"><span data-stu-id="cca1a-114">Select **Don't block cookies**.</span></span>
3. <span data-ttu-id="cca1a-115">重新整理 Azure 登入頁面，然後檢查問題是否已獲得解決。</span><span class="sxs-lookup"><span data-stu-id="cca1a-115">Refresh the Azure sign-up page, and check if the problem is resolved.</span></span>
4. <span data-ttu-id="cca1a-116">如果重新整理並未解決問題，請結束瀏覽器並重新啟動，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="cca1a-116">If the refresh didn't solve the issue, quit and restart your browser then try again.</span></span>

## <a name="credit-card-form-doesnt-support-my-billing-address"></a><span data-ttu-id="cca1a-117">信用卡表單不支援我的帳單地址</span><span class="sxs-lookup"><span data-stu-id="cca1a-117">Credit card form doesn't support my billing address</span></span>
<span data-ttu-id="cca1a-118">您的帳單地址必須位於您在 [關於您] 一節所選的國家/地區。</span><span class="sxs-lookup"><span data-stu-id="cca1a-118">Your billing address needs to be in the country that you selected in the **About you** section.</span></span> <span data-ttu-id="cca1a-119">請確定您選取正確的國家/地區。</span><span class="sxs-lookup"><span data-stu-id="cca1a-119">Make sure you select the correct country.</span></span>

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a><span data-ttu-id="cca1a-120">註冊帳戶驗證期間沒有文字訊息或呼叫</span><span class="sxs-lookup"><span data-stu-id="cca1a-120">No text messages or calls during sign-up account verification</span></span>
<span data-ttu-id="cca1a-121">雖然通常會更快，但傳送驗證碼最多可能需花費四分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="cca1a-121">While it is usually much faster, it may take up to four minutes for verification code to be delivered.</span></span> <span data-ttu-id="cca1a-122">您針對驗證所輸入的電話號碼，並不會儲存為帳戶的連絡電話。</span><span class="sxs-lookup"><span data-stu-id="cca1a-122">The phone number you enter for verification isn't stored as a contact number for the account.</span></span>

<span data-ttu-id="cca1a-123">以下是一些其他的祕訣：</span><span class="sxs-lookup"><span data-stu-id="cca1a-123">Here are some additional tips:</span></span>
* <span data-ttu-id="cca1a-124">VOIP 電話號碼無法用於電話驗證程序。</span><span class="sxs-lookup"><span data-stu-id="cca1a-124">A VOIP phone number can't be used for the phone verification process.</span></span>
* <span data-ttu-id="cca1a-125">再次確認您輸入的電話號碼，包括您在下拉式功能表中選取的國碼 (地區碼)。</span><span class="sxs-lookup"><span data-stu-id="cca1a-125">Double check the phone number you enter, including the country code you selected in the dropdown menu.</span></span>
* <span data-ttu-id="cca1a-126">如果您的手機沒有收到簡訊 (SMS)，請嘗試 [撥號給我] 選項。</span><span class="sxs-lookup"><span data-stu-id="cca1a-126">If your phone doesn't receive text messages (SMS), try the **Call me** option.</span></span>
* <span data-ttu-id="cca1a-127">請確定您的電話可以接收來自美國電話號碼的來電或簡訊。</span><span class="sxs-lookup"><span data-stu-id="cca1a-127">Ensure that your phone can receive calls or SMS messages from a United States based number.</span></span>

<span data-ttu-id="cca1a-128">當您收到簡訊或來電時，請在文字方塊中輸入您收到的代碼。</span><span class="sxs-lookup"><span data-stu-id="cca1a-128">When you get the text message or phone call, enter code that you receive into the text box.</span></span>

## <a name="credit-card-declined-or-not-accepted"></a><span data-ttu-id="cca1a-129">信用卡被拒絕或不被接受</span><span class="sxs-lookup"><span data-stu-id="cca1a-129">Credit card declined or not accepted</span></span>
<span data-ttu-id="cca1a-130">虛擬卡、預付信用卡或金融卡不被視為 Azure 訂用帳戶的付款方式。</span><span class="sxs-lookup"><span data-stu-id="cca1a-130">Virtual or prepaid credit or debit cards aren't accepted as payment for Azure subscriptions.</span></span> <span data-ttu-id="cca1a-131">若要查看其他造成卡片被拒絕的可能原因，請參閱[在 Azure 註冊時信用卡或金融卡遭到拒絕](billing-credit-card-fails-during-azure-sign-up.md)。</span><span class="sxs-lookup"><span data-stu-id="cca1a-131">To see what else may cause your card to be declined, see [your debit card or credit card is declined at Azure sign-up](billing-credit-card-fails-during-azure-sign-up.md).</span></span>

## <a name="free-trial-is-not-available"></a><span data-ttu-id="cca1a-132">「無法使用免費試用版」</span><span class="sxs-lookup"><span data-stu-id="cca1a-132">"Free Trial is not available"</span></span>
<span data-ttu-id="cca1a-133">過去曾使用 Azure 訂用帳戶嗎？</span><span class="sxs-lookup"><span data-stu-id="cca1a-133">Have you used an Azure subscription in the past?</span></span> <span data-ttu-id="cca1a-134">Azure 使用規定協議限制免費試用啟動僅適用 Azure 的新使用者。</span><span class="sxs-lookup"><span data-stu-id="cca1a-134">The Azure Terms of Use agreement limits free trial activation only for a user that's new to Azure.</span></span> <span data-ttu-id="cca1a-135">如果您有任何其他類型的 Azure 訂用帳戶，會無法啟用免費試用。</span><span class="sxs-lookup"><span data-stu-id="cca1a-135">If you have had any other type of Azure subscription, you can't activate a free trial.</span></span> <span data-ttu-id="cca1a-136">請考慮註冊[隨用隨付訂用帳戶](https://azure.microsoft.com/offers/ms-azr-0003p/)。</span><span class="sxs-lookup"><span data-stu-id="cca1a-136">Consider signing up for a [Pay-As-You-Go subscription](https://azure.microsoft.com/offers/ms-azr-0003p/).</span></span>

## <a name="i-saw-a-charge-on-my-free-trial-account"></a><span data-ttu-id="cca1a-137">我的免費試用帳戶收到一筆費用</span><span class="sxs-lookup"><span data-stu-id="cca1a-137">I saw a charge on my Free Trial account</span></span>
<span data-ttu-id="cca1a-138">您在註冊後可能會在信用卡帳戶上看到一筆小額度的驗證保留費用，這會在 3 到 5 天內移除。</span><span class="sxs-lookup"><span data-stu-id="cca1a-138">You may see a small verification hold on your credit card account after you sign up, which is removed within 3 to 5 days.</span></span> <span data-ttu-id="cca1a-139">如果您擔心管理成本，請深入了解[如何避免非預期的成本](https://docs.microsoft.com/azure/billing/billing-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="cca1a-139">If you are worried about managing costs, read more about [preventing unexpected costs](https://docs.microsoft.com/azure/billing/billing-getting-started).</span></span>

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a><span data-ttu-id="cca1a-140">無法啟用 MSDN、BizSpark、BizSparkPlus 或 MPN 之類的 Azure 權益方案</span><span class="sxs-lookup"><span data-stu-id="cca1a-140">Can’t activate Azure benefit plan like MSDN, BizSpark, BizSparkPlus, or MPN</span></span>
<span data-ttu-id="cca1a-141">請確定您是使用正確的登入認證。</span><span class="sxs-lookup"><span data-stu-id="cca1a-141">Make sure that you're using the right sign-in credentials.</span></span> <span data-ttu-id="cca1a-142">然後檢查權益方案，以確認您符合資格。</span><span class="sxs-lookup"><span data-stu-id="cca1a-142">Then check the benefit program to make sure that you're eligible.</span></span> 

* <span data-ttu-id="cca1a-143">MSDN</span><span class="sxs-lookup"><span data-stu-id="cca1a-143">MSDN</span></span>
  * <span data-ttu-id="cca1a-144">請在您的 [MSDN 帳戶頁面](https://msdn.microsoft.com/subscriptions/manage/default.aspx)驗證自己的資格狀態。</span><span class="sxs-lookup"><span data-stu-id="cca1a-144">Verify your eligibility status in your [MSDN account page](https://msdn.microsoft.com/subscriptions/manage/default.aspx).</span></span>
  * <span data-ttu-id="cca1a-145">如果您無法驗證自己的狀態，請連絡 [MSDN 訂閱客服中心](https://msdn.microsoft.com/subscriptions/contactus.aspx)</span><span class="sxs-lookup"><span data-stu-id="cca1a-145">If you can't verify your status, contact the [MSDN Subscriptions Customer Service Centers](https://msdn.microsoft.com/subscriptions/contactus.aspx)</span></span>
* <span data-ttu-id="cca1a-146">BizSpark</span><span class="sxs-lookup"><span data-stu-id="cca1a-146">BizSpark</span></span>
  * <span data-ttu-id="cca1a-147">登入 [BizSpark 入口網站](https://www.microsoft.com/bizspark/default.aspx#start-two) ，確認您 BizSpark 和 BizSpark Plus 的資格狀態。</span><span class="sxs-lookup"><span data-stu-id="cca1a-147">Sign in to the [BizSpark portal](https://www.microsoft.com/bizspark/default.aspx#start-two) and verify your eligibility status for BizSpark and BizSpark Plus.</span></span>
  * <span data-ttu-id="cca1a-148">如果您無法驗證您的狀態，您可以[在 BizSpark 論壇取得協助](http://aka.ms/bzforums)。</span><span class="sxs-lookup"><span data-stu-id="cca1a-148">If you can't verify your status, you can [get help at the BizSpark forums](http://aka.ms/bzforums).</span></span>
* <span data-ttu-id="cca1a-149">MPN</span><span class="sxs-lookup"><span data-stu-id="cca1a-149">MPN</span></span>
  * <span data-ttu-id="cca1a-150">登入 [MPN 入口網站](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) ，並驗證您的資格狀態。</span><span class="sxs-lookup"><span data-stu-id="cca1a-150">Sign in to the [MPN portal](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) and verify your eligibility status.</span></span> <span data-ttu-id="cca1a-151">如有適當的[雲端平台能力](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx)，您或許能夠得到額外的好處。</span><span class="sxs-lookup"><span data-stu-id="cca1a-151">If you have the appropriate [Cloud Platform Competencies](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), you may be eligible for additional benefits.</span></span>
  * <span data-ttu-id="cca1a-152">如果您無法驗證自己的狀態，請連絡 [MPN 支援](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cca1a-152">If you can't verify your status, contact [MPN support](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).</span></span>

## <a name="cant-activate-new-azure-in-open-subscription"></a><span data-ttu-id="cca1a-153">無法啟用新的 Azure in Open 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cca1a-153">Can’t activate new Azure In Open subscription</span></span>
<span data-ttu-id="cca1a-154">若要建立 Azure in Open 訂用帳戶，您必須具有有效的線上服務啟用 (OSA) 金鑰與至少一個相關聯的 Azure in Open 權杖。</span><span class="sxs-lookup"><span data-stu-id="cca1a-154">To create an Azure In Open subscription, you must have a valid Online Service Activation (OSA) key with at least one Azure In Open token associated to it.</span></span> <span data-ttu-id="cca1a-155">如果您沒有 OSA 金鑰，請連絡 [Microsoft Pinpoint](http://pinpoint.microsoft.com/) 中列出的其中一個 Microsoft 合作夥伴。</span><span class="sxs-lookup"><span data-stu-id="cca1a-155">If you don't have an OSA key, contact one of Microsoft Partners listed in [Microsoft Pinpoint](http://pinpoint.microsoft.com/).</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="cca1a-156">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="cca1a-156">Need help?</span></span> <span data-ttu-id="cca1a-157">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="cca1a-157">Contact support.</span></span>
<span data-ttu-id="cca1a-158">如果仍需要協助，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="cca1a-158">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
