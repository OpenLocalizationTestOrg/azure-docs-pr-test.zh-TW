---
title: "適用於行動電話的 Microsoft Authenticator 應用程式 | Microsoft Docs"
description: "了解如何升級至最新版的 Azure Authenticator。"
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
ms.openlocfilehash: 6bcb6d9f7a1e9b241fa70690016b03d6eb5887ab
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-microsoft-authenticator-app"></a><span data-ttu-id="9812d-103">開始使用 Microsoft 驗證器應用程式</span><span class="sxs-lookup"><span data-stu-id="9812d-103">Get started with the Microsoft Authenticator app</span></span>
<span data-ttu-id="9812d-104">Microsoft Authenticator 應用程式可以為您的工作或學校帳戶 (例如 bsimon@contoso.com) 或 Microsoft 帳戶 (例如 bsimon@outlook.com) 提供額外一層安全性。</span><span class="sxs-lookup"><span data-stu-id="9812d-104">The Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="9812d-105">此應用程式可以下列兩種方式之一運作︰</span><span class="sxs-lookup"><span data-stu-id="9812d-105">The app works in one of two ways:</span></span>

* <span data-ttu-id="9812d-106">**通知**。</span><span class="sxs-lookup"><span data-stu-id="9812d-106">**Notification**.</span></span> <span data-ttu-id="9812d-107">此應用程式可協助防止未經授權即存取帳戶，並藉由推播通知到您的手機或平板電腦來停止詐騙交易。</span><span class="sxs-lookup"><span data-stu-id="9812d-107">The app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span></span> <span data-ttu-id="9812d-108">只需檢視通知，如果合法，則選取 [驗證] 。</span><span class="sxs-lookup"><span data-stu-id="9812d-108">Simply view the notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="9812d-109">否則，您可以選取 [拒絕] 。</span><span class="sxs-lookup"><span data-stu-id="9812d-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="9812d-110">**驗證碼**。</span><span class="sxs-lookup"><span data-stu-id="9812d-110">**Verification code**.</span></span> <span data-ttu-id="9812d-111">此應用程式可以作為軟體權杖來產生 OATH 驗證碼。</span><span class="sxs-lookup"><span data-stu-id="9812d-111">The app can be used as a software token to generate an OAuth verification code.</span></span> <span data-ttu-id="9812d-112">在您輸入使用者名稱和密碼後，必須在登入畫面出現提示時輸入應用程式提供的驗證碼。</span><span class="sxs-lookup"><span data-stu-id="9812d-112">After you enter your username and password, you enter the code provided by the app into the sign-in screen.</span></span> <span data-ttu-id="9812d-113">驗證碼提供第二種形式的驗證。</span><span class="sxs-lookup"><span data-stu-id="9812d-113">The verification code provides a second form of authentication.</span></span>

<span data-ttu-id="9812d-114">Microsoft Authenticator 應用程式會取代 Azure Authenticator 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9812d-114">The Microsoft Authenticator app replaces the Azure Authenticator app.</span></span> <span data-ttu-id="9812d-115">Azure 驗證器應用程式仍可運作，但如果您決定改用新的 Microsoft Authenticator 應用程式，本文可協助您。</span><span class="sxs-lookup"><span data-stu-id="9812d-115">The Azure Authenticator app still works, but if you decide to move to the new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="9812d-116">選擇雙步驟驗證</span><span class="sxs-lookup"><span data-stu-id="9812d-116">Opt in for two-step verification</span></span>

<span data-ttu-id="9812d-117">Microsoft Authenticator 無法自行運作。</span><span class="sxs-lookup"><span data-stu-id="9812d-117">The Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="9812d-118">將您的每個帳戶設定為在以您的使用者名稱和密碼登入之後，提示您選擇第二個驗證方法。</span><span class="sxs-lookup"><span data-stu-id="9812d-118">Configure each of your accounts to prompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="9812d-119">如果是公司或學校帳戶，您通常不需要自行選擇此功能。</span><span class="sxs-lookup"><span data-stu-id="9812d-119">For a work or school account, you don't usually get to choose this feature for yourself.</span></span> <span data-ttu-id="9812d-120">相反地，安全性系統管理員會代替您選擇，然後通知您為您的帳戶註冊驗證方法。</span><span class="sxs-lookup"><span data-stu-id="9812d-120">Instead, a security administrator opts in on your behalf and then notifies you to register verification methods for your account.</span></span> <span data-ttu-id="9812d-121">如果此案例適用於您，請參閱 [Azure Multi-Factor Authentication 對我有何意義](multi-factor-authentication-end-user.md)以深入了解。</span><span class="sxs-lookup"><span data-stu-id="9812d-121">If this scenario applies to you, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="9812d-122">如果是個人帳戶，您必須自行設定雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="9812d-122">For a personal account, you need to set up two-step verification for yourself.</span></span> <span data-ttu-id="9812d-123">如果您有 Microsoft 帳戶，[關於雙步驟驗證](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)中說明這些步驟。</span><span class="sxs-lookup"><span data-stu-id="9812d-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="9812d-124">您也可以搭配非 Microsoft 帳戶使用 Microsoft Authenticator。</span><span class="sxs-lookup"><span data-stu-id="9812d-124">You can also use the Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="9812d-125">它們可能不是將此功能叫做雙步驟驗證，但您應該能夠在安全性或登入設定下找到它。</span><span class="sxs-lookup"><span data-stu-id="9812d-125">They may call the feature something other than two-step verification, but you should be able to find it under security or sign-in settings.</span></span> 

## <a name="install-the-app"></a><span data-ttu-id="9812d-126">安裝應用程式</span><span class="sxs-lookup"><span data-stu-id="9812d-126">Install the app</span></span>
<span data-ttu-id="9812d-127">Microsoft Authenticator 應用程式適用於 [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071)、[Android](http://go.microsoft.com/fwlink/?Linkid=825072) 和 [iOS](http://go.microsoft.com/fwlink/?Linkid=825073)。</span><span class="sxs-lookup"><span data-stu-id="9812d-127">The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-to-the-app"></a><span data-ttu-id="9812d-128">將帳戶新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="9812d-128">Add accounts to the app</span></span>
<span data-ttu-id="9812d-129">針對每個想要新增至 Microsoft Authenticator 應用程式的帳戶，請使用下列其中一個程序：</span><span class="sxs-lookup"><span data-stu-id="9812d-129">For each account that you want to add to the Microsoft Authenticator app, use one of the following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-to-the-app"></a><span data-ttu-id="9812d-130">將個人的 Microsoft 帳戶新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="9812d-130">Add a personal Microsoft account to the app</span></span>

<span data-ttu-id="9812d-131">針對個人的 Microsoft 帳戶 (您用來登入 Outlook.com、Xbox、Skype 等的帳戶)，您只需要登入在 Microsoft Authenticator應用程式中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="9812d-131">For a personal Microsoft account (one that you use to sign in to Outlook.com, Xbox, Skype, etc.), all you have to do is sign in to your account in the Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-to-the-app-using-the-qr-code-scanner"></a><span data-ttu-id="9812d-132">使用 QR 代碼掃描器將工作或學校帳戶新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="9812d-132">Add a work or school account to the app using the QR code scanner</span></span>
1. <span data-ttu-id="9812d-133">移至安全性驗證設定畫面。</span><span class="sxs-lookup"><span data-stu-id="9812d-133">Go to the security verification settings screen.</span></span>  <span data-ttu-id="9812d-134">如需如何進入此畫面的詳細資訊，請參閱 [變更安全性設定](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page)。</span><span class="sxs-lookup"><span data-stu-id="9812d-134">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="9812d-135">核取 **Authenticator 應用程式**旁的方塊，然後選取 [設定]。</span><span class="sxs-lookup"><span data-stu-id="9812d-135">Check the box next to **Authenticator app** then select **Configure**.</span></span>

    ![安全性驗證設定畫面上的設定按鈕](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="9812d-137">這會顯示有 QR 代碼的畫面。</span><span class="sxs-lookup"><span data-stu-id="9812d-137">This brings up a screen with a QR code on it.</span></span>

    ![提供 QR 代碼的畫面](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="9812d-139">開啟 Microsoft 驗證器應用程式。</span><span class="sxs-lookup"><span data-stu-id="9812d-139">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="9812d-140">在 [帳戶] 畫面上，選取 [+]，然後指定您要新增工作帳戶或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="9812d-140">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>
4. <span data-ttu-id="9812d-141">使用相機來掃描 QR 代碼，然後選取 [完成]  關閉 QR 代碼畫面。</span><span class="sxs-lookup"><span data-stu-id="9812d-141">Use the camera to scan the QR code, and then select **Done** to close the QR code screen.</span></span>

    <span data-ttu-id="9812d-142">如果相機運作不正常，您可以[手動輸入 QR 代碼和 URL](#add-an-account-to-the-app-manually)。</span><span class="sxs-lookup"><span data-stu-id="9812d-142">If your camera is not working properly, you can [enter the QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="9812d-143">當應用程式顯示您的帳戶名稱與下面的六位數代碼時，則您已完成。</span><span class="sxs-lookup"><span data-stu-id="9812d-143">When the app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![帳戶畫面](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-manually"></a><span data-ttu-id="9812d-145">手動新增帳戶至應用程式</span><span class="sxs-lookup"><span data-stu-id="9812d-145">Add an account to the app manually</span></span>
1. <span data-ttu-id="9812d-146">移至安全性驗證設定畫面。</span><span class="sxs-lookup"><span data-stu-id="9812d-146">Go to the security verification settings screen.</span></span>  <span data-ttu-id="9812d-147">如需如何進入此畫面的詳細資訊，請參閱 [變更安全性設定](multi-factor-authentication-end-user-manage-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="9812d-147">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="9812d-148">選取 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="9812d-148">Select **Configure**.</span></span>

    ![安全性驗證設定畫面上的設定按鈕](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="9812d-150">這會顯示有 QR 代碼的畫面。</span><span class="sxs-lookup"><span data-stu-id="9812d-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="9812d-151">記下代碼和 URL。</span><span class="sxs-lookup"><span data-stu-id="9812d-151">Note the code and URL.</span></span>

    ![提供 QR 代碼與 URL 的畫面](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="9812d-153">開啟 Microsoft 驗證器應用程式。</span><span class="sxs-lookup"><span data-stu-id="9812d-153">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="9812d-154">在 [帳戶] 畫面上，選取 [+]，然後指定您要新增工作帳戶或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="9812d-154">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>

4. <span data-ttu-id="9812d-155">在掃描器上，選取 [手動輸入代碼] 。</span><span class="sxs-lookup"><span data-stu-id="9812d-155">In the scanner, select **enter code manually**.</span></span>

    ![掃描 QR 代碼的畫面](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="9812d-157">在應用程式的適當方塊中輸入代碼和 URL，然後選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="9812d-157">Enter the code and the URL in the appropriate boxes in the app, then select **Finish**.</span></span>

    ![輸入代碼和 URL 的畫面](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="9812d-159">當應用程式顯示您的帳戶名稱與下面的六位數代碼時，則您已完成。</span><span class="sxs-lookup"><span data-stu-id="9812d-159">When the app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![帳戶畫面](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-using-touch-id"></a><span data-ttu-id="9812d-161">使用 Touch ID 將帳戶新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="9812d-161">Add an account to the app using Touch ID</span></span>
<span data-ttu-id="9812d-162">在 iOS 上的 Microsoft 驗證器應用程式支援 Touch ID。</span><span class="sxs-lookup"><span data-stu-id="9812d-162">The Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="9812d-163">Azure Multi-Factor Authentication 可讓組織要求裝置的 PIN 碼。</span><span class="sxs-lookup"><span data-stu-id="9812d-163">Azure Multi-Factor Authentication allows organizations to require a PIN for devices.</span></span> <span data-ttu-id="9812d-164">使用 Touch ID 時，iOS 使用者不需要輸入 PIN 碼。</span><span class="sxs-lookup"><span data-stu-id="9812d-164">With Touch ID, iOS users don’t need to enter a PIN.</span></span> <span data-ttu-id="9812d-165">相反地，他們可以掃描其指紋，並選取 [核准] 。</span><span class="sxs-lookup"><span data-stu-id="9812d-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="9812d-166">設定 Touch ID 搭配 Azure 驗證器很簡單。</span><span class="sxs-lookup"><span data-stu-id="9812d-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="9812d-167">您可以使用 PIN 碼完成一般驗證挑戰。</span><span class="sxs-lookup"><span data-stu-id="9812d-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="9812d-168">如果您的裝置支援 Touch ID，Microsoft Authenticator 會自動為該帳戶進行設定。</span><span class="sxs-lookup"><span data-stu-id="9812d-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Touch ID 安裝程式的驗證](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="9812d-170">往後當您被要求驗證登入時，您只要選取收到的推播通知並且掃描您的指紋即可，不需要輸入您的 PIN。</span><span class="sxs-lookup"><span data-stu-id="9812d-170">From that point forward, when you're required to verify your sign-in, you select the received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![推播通知](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-the-app-when-you-sign-in"></a><span data-ttu-id="9812d-172">當您登入時使用應用程式</span><span class="sxs-lookup"><span data-stu-id="9812d-172">Use the app when you sign in</span></span>

<span data-ttu-id="9812d-173">當您的帳戶新增至應用程式後，可能會提示您執行測試驗證，以確保一切都已正確設定。</span><span class="sxs-lookup"><span data-stu-id="9812d-173">Once your account is added to the app, you may be prompted to do a test verification to make sure everything was configured correctly.</span></span> <span data-ttu-id="9812d-174">之後，就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="9812d-174">After that, you're done!</span></span> <span data-ttu-id="9812d-175">直到下次再登入之前，您不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="9812d-175">You don't need to do anything else until the next time you sign in.</span></span>

<span data-ttu-id="9812d-176">如果您選擇在應用程式中使用驗證碼，您會開始在首頁上看到它們。</span><span class="sxs-lookup"><span data-stu-id="9812d-176">If you chose to use verification codes in the app, you start to see them on the home page.</span></span> <span data-ttu-id="9812d-177">它們每 30 秒變更一次，所以當您需要時，一定可以獲得新的驗證碼。</span><span class="sxs-lookup"><span data-stu-id="9812d-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="9812d-178">但在您登入並接獲提示輸入驗證碼之前，不必理會它們。</span><span class="sxs-lookup"><span data-stu-id="9812d-178">But you don't need to do anything with them until you sign in and are prompted to enter a verification code.</span></span>  