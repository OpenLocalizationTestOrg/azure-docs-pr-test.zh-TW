---
title: "行動電話的 aaaMicrosoft Authenticator 應用程式 |Microsoft 文件"
description: "深入了解如何 tooupgrade toohello 最新版本的 Azure Authenticator。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="2917f-103">開始使用 hello Microsoft 驗證器應用程式</span><span class="sxs-lookup"><span data-stu-id="2917f-103">Get started with hello Microsoft Authenticator app</span></span>
<span data-ttu-id="2917f-104">hello Microsoft Authenticator 應用程式提供額外一層的安全性工作或學校帳戶 (例如， bsimon@contoso.com) 或您的 Microsoft 帳戶 (例如， bsimon@outlook.com)。</span><span class="sxs-lookup"><span data-stu-id="2917f-104">hello Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="2917f-105">hello 應用程式的運作方式在兩種方式之一：</span><span class="sxs-lookup"><span data-stu-id="2917f-105">hello app works in one of two ways:</span></span>

* <span data-ttu-id="2917f-106">**通知**。</span><span class="sxs-lookup"><span data-stu-id="2917f-106">**Notification**.</span></span> <span data-ttu-id="2917f-107">hello 應用程式可協助防止未經授權的存取 tooaccounts 並停止詐騙交易將推送通知 tooyour 智慧型手機或平板電腦。</span><span class="sxs-lookup"><span data-stu-id="2917f-107">hello app can help prevent unauthorized access tooaccounts and stop fraudulent transactions by pushing a notification tooyour smartphone or tablet.</span></span> <span data-ttu-id="2917f-108">只檢視 hello 通知，如果合法，請選取**確認**。</span><span class="sxs-lookup"><span data-stu-id="2917f-108">Simply view hello notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="2917f-109">否則，您可以選取 [拒絕] 。</span><span class="sxs-lookup"><span data-stu-id="2917f-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="2917f-110">**驗證碼**。</span><span class="sxs-lookup"><span data-stu-id="2917f-110">**Verification code**.</span></span> <span data-ttu-id="2917f-111">hello 應用程式可以做為軟體權杖 toogenerate OAuth 驗證碼。</span><span class="sxs-lookup"><span data-stu-id="2917f-111">hello app can be used as a software token toogenerate an OAuth verification code.</span></span> <span data-ttu-id="2917f-112">您輸入使用者名稱和密碼之後，您會輸入 hello hello 登入畫面 hello 應用程式所提供的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2917f-112">After you enter your username and password, you enter hello code provided by hello app into hello sign-in screen.</span></span> <span data-ttu-id="2917f-113">hello 驗證程式碼會提供第二種形式的驗證。</span><span class="sxs-lookup"><span data-stu-id="2917f-113">hello verification code provides a second form of authentication.</span></span>

<span data-ttu-id="2917f-114">hello Microsoft 驗證器應用程式取代 hello Azure Authenticator 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2917f-114">hello Microsoft Authenticator app replaces hello Azure Authenticator app.</span></span> <span data-ttu-id="2917f-115">hello Azure Authenticator 應用程式仍能運作，但如果您決定 toomove toohello 新 Microsoft Authenticator 應用程式，這篇文章可協助您。</span><span class="sxs-lookup"><span data-stu-id="2917f-115">hello Azure Authenticator app still works, but if you decide toomove toohello new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="2917f-116">選擇雙步驟驗證</span><span class="sxs-lookup"><span data-stu-id="2917f-116">Opt in for two-step verification</span></span>

<span data-ttu-id="2917f-117">hello Microsoft 驗證器應用程式並不可行的。</span><span class="sxs-lookup"><span data-stu-id="2917f-117">hello Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="2917f-118">設定每個您輸入之後的第二個驗證方法使用您的使用者名稱和密碼登入您的帳戶 tooprompt。</span><span class="sxs-lookup"><span data-stu-id="2917f-118">Configure each of your accounts tooprompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="2917f-119">工作或學校帳戶，就無法通常取得 toochoose 這項功能自行。</span><span class="sxs-lookup"><span data-stu-id="2917f-119">For a work or school account, you don't usually get toochoose this feature for yourself.</span></span> <span data-ttu-id="2917f-120">相反地，安全性系統管理員選擇代表您，，然後通知您 tooregister 驗證方法，為您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2917f-120">Instead, a security administrator opts in on your behalf and then notifies you tooregister verification methods for your account.</span></span> <span data-ttu-id="2917f-121">如果此案例適用於 tooyou，進一步了解[Azure Multi-factor Authentication 什麼我](multi-factor-authentication-end-user.md)。</span><span class="sxs-lookup"><span data-stu-id="2917f-121">If this scenario applies tooyou, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="2917f-122">個人的帳戶，您必須註冊您自己的雙步驟驗證 tooset。</span><span class="sxs-lookup"><span data-stu-id="2917f-122">For a personal account, you need tooset up two-step verification for yourself.</span></span> <span data-ttu-id="2917f-123">如果您有 Microsoft 帳戶，[關於雙步驟驗證](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)中說明這些步驟。</span><span class="sxs-lookup"><span data-stu-id="2917f-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="2917f-124">您也可以使用 Microsoft Authenticator hello 與非 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2917f-124">You can also use hello Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="2917f-125">它們可能會呼叫 hello 功能以外的雙步驟驗證，但是您應該能夠 toofind 在安全性 」 或 「 登入設定。</span><span class="sxs-lookup"><span data-stu-id="2917f-125">They may call hello feature something other than two-step verification, but you should be able toofind it under security or sign-in settings.</span></span> 

## <a name="install-hello-app"></a><span data-ttu-id="2917f-126">安裝 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="2917f-126">Install hello app</span></span>
<span data-ttu-id="2917f-127">hello Microsoft 驗證器應用程式是供[Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071)， [Android](http://go.microsoft.com/fwlink/?Linkid=825072)，和[iOS](http://go.microsoft.com/fwlink/?Linkid=825073)。</span><span class="sxs-lookup"><span data-stu-id="2917f-127">hello Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-toohello-app"></a><span data-ttu-id="2917f-128">新增帳戶 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="2917f-128">Add accounts toohello app</span></span>
<span data-ttu-id="2917f-129">針對每個您想 tooadd toohello Microsoft Authenticator 應用程式的帳戶，使用其中一種 hello 下列程序：</span><span class="sxs-lookup"><span data-stu-id="2917f-129">For each account that you want tooadd toohello Microsoft Authenticator app, use one of hello following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-toohello-app"></a><span data-ttu-id="2917f-130">新增個人 Microsoft 帳戶 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="2917f-130">Add a personal Microsoft account toohello app</span></span>

<span data-ttu-id="2917f-131">個人 Microsoft 帳戶 (其中一個您使用 toosign 中 tooOutlook.com Xbox、 Skype、 等)，您只需要 toodo 是登入 tooyour hello Microsoft 驗證器應用程式中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2917f-131">For a personal Microsoft account (one that you use toosign in tooOutlook.com, Xbox, Skype, etc.), all you have toodo is sign in tooyour account in hello Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a><span data-ttu-id="2917f-132">新增工作或學校帳戶 toohello 應用程式使用 hello QR 代碼掃描器</span><span class="sxs-lookup"><span data-stu-id="2917f-132">Add a work or school account toohello app using hello QR code scanner</span></span>
1. <span data-ttu-id="2917f-133">移 toohello 安全性驗證設定 畫面。</span><span class="sxs-lookup"><span data-stu-id="2917f-133">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="2917f-134">如需詳細資訊 tooget toothis 畫面上，請參閱[變更安全性設定](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page)。</span><span class="sxs-lookup"><span data-stu-id="2917f-134">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="2917f-135">核取 hello 方塊旁太**Authenticator 應用程式**然後選取**設定**。</span><span class="sxs-lookup"><span data-stu-id="2917f-135">Check hello box next too**Authenticator app** then select **Configure**.</span></span>

    ![hello hello 安全性驗證設定 畫面上的設定按鈕](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="2917f-137">這會顯示有 QR 代碼的畫面。</span><span class="sxs-lookup"><span data-stu-id="2917f-137">This brings up a screen with a QR code on it.</span></span>

    ![畫面，讓您 hello QR 代碼](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="2917f-139">開啟 hello Microsoft 驗證器應用程式。</span><span class="sxs-lookup"><span data-stu-id="2917f-139">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="2917f-140">在 hello**帳戶**畫面上，選取 **+** ，然後指定您想要 tooadd 工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="2917f-140">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>
4. <span data-ttu-id="2917f-141">使用 hello 相機 tooscan hello QR 代碼，然後選取**完成**tooclose hello QR 代碼螢幕。</span><span class="sxs-lookup"><span data-stu-id="2917f-141">Use hello camera tooscan hello QR code, and then select **Done** tooclose hello QR code screen.</span></span>

    <span data-ttu-id="2917f-142">如果您的相機未正常運作，您可以[手動輸入 hello QR 代碼和 URL](#add-an-account-to-the-app-manually)。</span><span class="sxs-lookup"><span data-stu-id="2917f-142">If your camera is not working properly, you can [enter hello QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="2917f-143">Hello 應用程式會顯示您的帳戶名稱，以六位數代碼其下，您已完成。</span><span class="sxs-lookup"><span data-stu-id="2917f-143">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![帳戶畫面](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a><span data-ttu-id="2917f-145">手動新增帳戶 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="2917f-145">Add an account toohello app manually</span></span>
1. <span data-ttu-id="2917f-146">移 toohello 安全性驗證設定 畫面。</span><span class="sxs-lookup"><span data-stu-id="2917f-146">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="2917f-147">如需詳細資訊 tooget toothis 畫面上，請參閱[變更安全性設定](multi-factor-authentication-end-user-manage-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="2917f-147">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="2917f-148">選取 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="2917f-148">Select **Configure**.</span></span>

    ![hello hello 安全性驗證設定 畫面上的設定按鈕](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="2917f-150">這會顯示有 QR 代碼的畫面。</span><span class="sxs-lookup"><span data-stu-id="2917f-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="2917f-151">請注意 hello 代碼和 URL。</span><span class="sxs-lookup"><span data-stu-id="2917f-151">Note hello code and URL.</span></span>

    ![提供 hello QR 代碼和 URL 的螢幕](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="2917f-153">開啟 hello Microsoft 驗證器應用程式。</span><span class="sxs-lookup"><span data-stu-id="2917f-153">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="2917f-154">在 hello**帳戶**畫面上，選取 **+** ，然後指定您想要 tooadd 工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="2917f-154">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>

4. <span data-ttu-id="2917f-155">在 hello 掃描器，請選取**手動輸入程式碼**。</span><span class="sxs-lookup"><span data-stu-id="2917f-155">In hello scanner, select **enter code manually**.</span></span>

    ![掃描 QR 代碼的畫面](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="2917f-157">Hello，hello 應用程式中的適當方塊中輸入 hello 代碼和 hello URL，然後選取 **完成**。</span><span class="sxs-lookup"><span data-stu-id="2917f-157">Enter hello code and hello URL in hello appropriate boxes in hello app, then select **Finish**.</span></span>

    ![輸入代碼和 URL 的畫面](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="2917f-159">Hello 應用程式會顯示您的帳戶名稱，以六位數代碼其下，您已完成。</span><span class="sxs-lookup"><span data-stu-id="2917f-159">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![帳戶畫面](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a><span data-ttu-id="2917f-161">新增帳戶 toohello 應用程式使用 Touch ID</span><span class="sxs-lookup"><span data-stu-id="2917f-161">Add an account toohello app using Touch ID</span></span>
<span data-ttu-id="2917f-162">hello Microsoft 驗證器應用程式在 iOS 上的支援 Touch ID</span><span class="sxs-lookup"><span data-stu-id="2917f-162">hello Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="2917f-163">Azure Multi-factor Authentication 可讓組織 toorequire 裝置的 PIN。</span><span class="sxs-lookup"><span data-stu-id="2917f-163">Azure Multi-Factor Authentication allows organizations toorequire a PIN for devices.</span></span> <span data-ttu-id="2917f-164">使用 Touch ID、 iOS 使用者不需要 tooenter PIN。</span><span class="sxs-lookup"><span data-stu-id="2917f-164">With Touch ID, iOS users don’t need tooenter a PIN.</span></span> <span data-ttu-id="2917f-165">相反地，他們可以掃描其指紋，並選取 [核准] 。</span><span class="sxs-lookup"><span data-stu-id="2917f-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="2917f-166">設定 Touch ID 搭配 Azure 驗證器很簡單。</span><span class="sxs-lookup"><span data-stu-id="2917f-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="2917f-167">您可以使用 PIN 碼完成一般驗證挑戰。</span><span class="sxs-lookup"><span data-stu-id="2917f-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="2917f-168">如果您的裝置支援 Touch ID，Microsoft Authenticator 會自動為該帳戶進行設定。</span><span class="sxs-lookup"><span data-stu-id="2917f-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Touch ID 安裝程式的驗證](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="2917f-170">從該點，當您準備 tooverify 需要您登入時，您選取 hello 接收推播通知，並掃描指紋而不是輸入 PIN。</span><span class="sxs-lookup"><span data-stu-id="2917f-170">From that point forward, when you're required tooverify your sign-in, you select hello received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![推播通知](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a><span data-ttu-id="2917f-172">當您登入使用 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="2917f-172">Use hello app when you sign in</span></span>

<span data-ttu-id="2917f-173">一旦您的帳戶新增 toohello 應用程式，您可能會提示的 toodo 測試驗證 toomake 確定所有項目已正確設定。</span><span class="sxs-lookup"><span data-stu-id="2917f-173">Once your account is added toohello app, you may be prompted toodo a test verification toomake sure everything was configured correctly.</span></span> <span data-ttu-id="2917f-174">之後，就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="2917f-174">After that, you're done!</span></span> <span data-ttu-id="2917f-175">您不需要 toodo 任何其他項目直到 hello 下次您登入。</span><span class="sxs-lookup"><span data-stu-id="2917f-175">You don't need toodo anything else until hello next time you sign in.</span></span>

<span data-ttu-id="2917f-176">如果您選擇 toouse 驗證碼 hello 應用程式中，您會啟動 toosee 它們 hello 首頁上。</span><span class="sxs-lookup"><span data-stu-id="2917f-176">If you chose toouse verification codes in hello app, you start toosee them on hello home page.</span></span> <span data-ttu-id="2917f-177">它們每 30 秒變更一次，所以當您需要時，一定可以獲得新的驗證碼。</span><span class="sxs-lookup"><span data-stu-id="2917f-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="2917f-178">但是您不需要 toodo 任何項目與它們直到您登入，並提示的 tooenter 驗證碼。</span><span class="sxs-lookup"><span data-stu-id="2917f-178">But you don't need toodo anything with them until you sign in and are prompted tooenter a verification code.</span></span>  
