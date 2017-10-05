---
title: "針對 Azure Active Directory 中的企業狀態漫遊設定進行疑難排解 | Microsoft Docs"
description: "回答 IT 系統管理員可能會遇到的設定和應用程式資料同步處理的一些問題。"
services: active-directory
keywords: "企業狀態漫遊設定, windows 雲端, 企業狀態漫遊常見問題集"
documentationcenter: 
author: tanning
manager: swadhwa
editor: 
ms.assetid: f45d0515-99f7-42ad-94d8-307bc0d07be5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 5d6b0869d2cf0e90b7b81b2304d95e01d1937925
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a><span data-ttu-id="4eca4-104">針對 Azure Active Directory 中的企業狀態漫遊設定進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="4eca4-104">Troubleshooting Enterprise State Roaming settings in Azure Active Directory</span></span>

<span data-ttu-id="4eca4-105">本主題提供有關如何針對企業狀態漫遊問題進行疑難排解及診斷的資訊，並提供已知問題的清單。</span><span class="sxs-lookup"><span data-stu-id="4eca4-105">This topic provides information on how to troubleshoot and diagnose issues with Enterprise State Roaming, and provides a list of known issues.</span></span>

## <a name="preliminary-steps-for-troubleshooting"></a><span data-ttu-id="4eca4-106">疑難排解的預備步驟</span><span class="sxs-lookup"><span data-stu-id="4eca4-106">Preliminary steps for troubleshooting</span></span> 
<span data-ttu-id="4eca4-107">在開始進行疑難排解之前，請先確認使用者和裝置已正確設定，且裝置和使用者符合企業狀態漫遊的所有需求。</span><span class="sxs-lookup"><span data-stu-id="4eca4-107">Before beginning troubleshooting verify that the user and device have been configured properly, and that all the requirements of Enterprise State Roaming are met by the device and the user.</span></span> 

1. <span data-ttu-id="4eca4-108">裝置上已安裝 Windows 10，包含最新更新且最低版本為 1511 (作業系統組建 10586 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="4eca4-108">Windows 10, with the latest updates, and a minimum Version 1511 (OS Build 10586 or later) is installed on the device.</span></span> 
2. <span data-ttu-id="4eca4-109">裝置已經加入 Azure AD，或已經加入網域並在 Azure AD 註冊。</span><span class="sxs-lookup"><span data-stu-id="4eca4-109">The device is Azure AD joined, or domain-joined and registered with Azure AD.</span></span>
3. <span data-ttu-id="4eca4-110">在 Azure Active Directory 入口網站中，已在 [設定] > [裝置] > [使用者可以同步設定及企業應用程式資料] 底下啟用 [企業狀態漫遊]。</span><span class="sxs-lookup"><span data-stu-id="4eca4-110">In the Azure Active Directory portal, **Enterprise State Roaming** is enabled for the directory under **Configure** > **Devices** > **Users May Sync Settings and Enterprise App Data**.</span></span> <span data-ttu-id="4eca4-111">已選取所有使用者，或已允許使用者透過所選選項進行同步處理且已將該使用者包括在安全性群組中。</span><span class="sxs-lookup"><span data-stu-id="4eca4-111">Either all users are selected, or the user is enabled for syncing through the selected option, and included in the security group.</span></span>
4. <span data-ttu-id="4eca4-112">已指派 Azure Active Directory Premium 訂用帳戶給使用者。</span><span class="sxs-lookup"><span data-stu-id="4eca4-112">The user has an Azure Active Directory Premium subscription assigned to them.</span></span>  
5. <span data-ttu-id="4eca4-113">裝置已經重新啟動，且使用者已經在企業狀態漫遊啟用之後登入。</span><span class="sxs-lookup"><span data-stu-id="4eca4-113">The device has been restarted, and the user has logged in after Enterprise State Roaming has been enabled.</span></span>

## <a name="information-to-include-when-you-need-help"></a><span data-ttu-id="4eca4-114">您需要協助時應包含的資訊</span><span class="sxs-lookup"><span data-stu-id="4eca4-114">Information to include when you need help</span></span>
<span data-ttu-id="4eca4-115">如果在進行過下列指導方針後仍無法解決問題，請連絡我們的支援工程師。</span><span class="sxs-lookup"><span data-stu-id="4eca4-115">If you cannot solve your issue with the guidance below, you can contact our support engineers.</span></span> <span data-ttu-id="4eca4-116">當您與他們連絡時，建議您包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="4eca4-116">When you contact them, it is recommended to include the following information:</span></span>

- <span data-ttu-id="4eca4-117">**錯誤的一般描述** – 使用者已看到錯誤訊息嗎？</span><span class="sxs-lookup"><span data-stu-id="4eca4-117">**General description of the error** – Are there error messages seen by the user?</span></span> <span data-ttu-id="4eca4-118">如果沒有任何錯誤訊息，請詳細說明您所注意到的未預期行為。</span><span class="sxs-lookup"><span data-stu-id="4eca4-118">If there was no error message, describe the unexpected behavior you noticed, in detail.</span></span> <span data-ttu-id="4eca4-119">已允許哪些功能進行同步處理，以及使用者預期同步處理哪些項目？</span><span class="sxs-lookup"><span data-stu-id="4eca4-119">What features are enabled for sync and what is the user expecting to sync?</span></span> <span data-ttu-id="4eca4-120">是否有多項功能未同步處理，或已將功能隔離以個別同步處理？</span><span class="sxs-lookup"><span data-stu-id="4eca4-120">Are multiple features not syncing or is it isolated to one?</span></span>
- <span data-ttu-id="4eca4-121">**受影響的使用者** – 是有一位還是多位使用者的同步處理成功/失敗？</span><span class="sxs-lookup"><span data-stu-id="4eca4-121">**Users affected** – Is sync working/failing for one user or multiple users?</span></span> <span data-ttu-id="4eca4-122">每個使用者涉及多少裝置？</span><span class="sxs-lookup"><span data-stu-id="4eca4-122">How many devices are involved per user?</span></span> <span data-ttu-id="4eca4-123">它們是否都沒有同步處理，或它們之間部分已同步處理，部分沒有同步處理？</span><span class="sxs-lookup"><span data-stu-id="4eca4-123">Are all of them not syncing or are some of them syncing and some not syncing?</span></span>
- <span data-ttu-id="4eca4-124">**使用者相關資訊** – 使用者是使用什麼身分識別登入裝置？</span><span class="sxs-lookup"><span data-stu-id="4eca4-124">**Information about the user** – What identity is the user using to log in to the device?</span></span> <span data-ttu-id="4eca4-125">使用者如何登入裝置？</span><span class="sxs-lookup"><span data-stu-id="4eca4-125">How is the user logging in to the device?</span></span> <span data-ttu-id="4eca4-126">它們是否屬於允許同步處理的所選安全性群組中的裝置？</span><span class="sxs-lookup"><span data-stu-id="4eca4-126">Are they part of a selected security group allowed to sync?</span></span> 
- <span data-ttu-id="4eca4-127">**裝置相關資訊** – 此裝置是否已經加入 Azure AD 或已經加入網域？</span><span class="sxs-lookup"><span data-stu-id="4eca4-127">**Information about the device** – Is this device Azure AD Joined or domain-joined?</span></span> <span data-ttu-id="4eca4-128">此裝置使用哪一個組建？</span><span class="sxs-lookup"><span data-stu-id="4eca4-128">What build is the device on?</span></span> <span data-ttu-id="4eca4-129">最新的更新是？</span><span class="sxs-lookup"><span data-stu-id="4eca4-129">What are the most recent updates?</span></span>
- <span data-ttu-id="4eca4-130">**日期/時間/時區** – 您看到錯誤時的精確日期和時間 (包含時區)。</span><span class="sxs-lookup"><span data-stu-id="4eca4-130">**Date / Time / Timezone** – What was the precise date and time you saw the error (include the timezone)?</span></span>
- <span data-ttu-id="4eca4-131">包含這項資訊有助於我們盡快為您解決問題。</span><span class="sxs-lookup"><span data-stu-id="4eca4-131">Including this information helps us solve your problem as quickly as possible.</span></span>

## <a name="troubleshooting-and-diagnosing-issues"></a><span data-ttu-id="4eca4-132">疑難排解和診斷問題</span><span class="sxs-lookup"><span data-stu-id="4eca4-132">Troubleshooting and diagnosing issues</span></span>
<span data-ttu-id="4eca4-133">本節提供有關如何針對企業狀態漫遊相關問題進行疑難排解及診斷的建議。</span><span class="sxs-lookup"><span data-stu-id="4eca4-133">This section gives suggestions on how to troubleshoot and diagnose problems related to Enterprise State Roaming.</span></span>

## <a name="verify-sync-and-the-sync-your-settings-settings-page"></a><span data-ttu-id="4eca4-134">確認同步處理，以及 [同步您的設定] 設定頁面</span><span class="sxs-lookup"><span data-stu-id="4eca4-134">Verify sync, and the “Sync your settings” settings page</span></span> 

1. <span data-ttu-id="4eca4-135">將您的 Windows 10 電腦加入已設定為允許企業狀態漫遊的網域之後，使用您的公司帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="4eca4-135">After joining your Windows 10 PC to a domain that is configured to allow Enterprise State Roaming, logon with your work account.</span></span> <span data-ttu-id="4eca4-136">移至 [設定] > [帳戶] > [同步您的設定]，並確認同步處理和個別設定都已啟用，且設定頁面頂端指示您正使用公司帳戶進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="4eca4-136">Go to **Settings** > **Accounts** > **Sync Your Settings** and confirm that sync and the individual settings are on, and that the top of the settings page indicates that you are syncing with your work account.</span></span> <span data-ttu-id="4eca4-137">確認您在 [設定] > [帳戶] > [您的資訊] 中也是使用相同帳戶作為登入帳戶。</span><span class="sxs-lookup"><span data-stu-id="4eca4-137">Confirm the same account is also used as your login account in **Settings** > **Accounts** > **Your Info**.</span></span> 
2. <span data-ttu-id="4eca4-138">透過在原始電腦上進行一些變更 (例如將工作列移至畫面右側或頂端)，來確認同步處理可跨多部電腦運作。</span><span class="sxs-lookup"><span data-stu-id="4eca4-138">Verify that sync works across multiple machines by making some changes on the original machine, such as moving the taskbar to the right or top side of the screen.</span></span> <span data-ttu-id="4eca4-139">監看變更是否在 5 分鐘內傳送至第二部電腦。</span><span class="sxs-lookup"><span data-stu-id="4eca4-139">Watch the change propagate to the second machine within five minutes.</span></span> 
 - <span data-ttu-id="4eca4-140">將畫面鎖定和解除鎖定 (Win + L) 有助於觸發同步處理。</span><span class="sxs-lookup"><span data-stu-id="4eca4-140">Locking and unlocking the screen (Win + L) can help trigger a sync.</span></span>
 - <span data-ttu-id="4eca4-141">您必須在兩部電腦上使用相同的登入帳戶，同步處理才能運作 – 因為「企業狀態漫遊」是繫結至使用者帳戶而不是電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="4eca4-141">You must be using the same logon account on both PCs for sync to work – as Enterprise State Roaming is tied to the user account and not the machine account.</span></span>

<span data-ttu-id="4eca4-142">**可能的問題**：設定頁面的切換功能顯示為灰色，且您看不到帳戶，而是看到「只有當您使用 Microsoft 帳戶或公司帳戶時，某些 Windows 功能才能使用。」文字。</span><span class="sxs-lookup"><span data-stu-id="4eca4-142">**Potential Issue**: The settings page has the toggles grayed out, and instead of seeing an account, you see the text “Some Windows features are only available if you are using a Microsoft account or work account”.</span></span> <span data-ttu-id="4eca4-143">當裝置設定成已加入網域，或者已在 Azure AD 註冊卻尚未成功向 Azure AD 驗證時，可能就會發生這個問題。</span><span class="sxs-lookup"><span data-stu-id="4eca4-143">This issue may arise for devices that have been set up to be domain-joined and registered to Azure AD, but the device has not successfully authenticated to Azure AD.</span></span> <span data-ttu-id="4eca4-144">可能的原因是必須套用裝置原則，但這個套用作業是非同步的，而且可能會延遲幾個小時。</span><span class="sxs-lookup"><span data-stu-id="4eca4-144">A possible cause is that the device policy must be applied, but this application happens asynchronously, and could be delayed by a few hours.</span></span> <span data-ttu-id="4eca4-145">若要確認此問題，請依照確認裝置註冊狀態中的步驟，來檢查是否是因為這個原因。</span><span class="sxs-lookup"><span data-stu-id="4eca4-145">To verify this issue, follow the steps in verify the device registration status to check if this is the case.</span></span>

### <a name="verify-the-device-registration-status"></a><span data-ttu-id="4eca4-146">確認裝置註冊狀態</span><span class="sxs-lookup"><span data-stu-id="4eca4-146">Verify the device registration status</span></span>
<span data-ttu-id="4eca4-147">企業狀態漫遊需要在 Azure AD 註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="4eca4-147">Enterprise State Roaming requires the device to be registered with Azure AD.</span></span> <span data-ttu-id="4eca4-148">雖然並非針對企業狀態漫遊，但遵循下列指示有助於確認 Windows 10 用戶端是否已經註冊，並確認憑證指紋、Azure AD 設定 URL、NGC 狀態及其他資訊。</span><span class="sxs-lookup"><span data-stu-id="4eca4-148">Although not specific to Enterprise State Roaming, following the instructions below can help confirm that the Windows 10 Client is registered, and confirm thumbprint, Azure AD settings URL, NGC status, and other information.</span></span>

1.  <span data-ttu-id="4eca4-149">在未提高權限的情況下開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="4eca4-149">Open the command prompt unelevated.</span></span> <span data-ttu-id="4eca4-150">若要在 Windows 中執行此操作，請開啟「執行」啟動程式 (Win + R) 並輸入 "cmd" 來開啟。</span><span class="sxs-lookup"><span data-stu-id="4eca4-150">To do this in Windows, open the Run launcher (Win + R) and type “cmd” to open.</span></span>
2.  <span data-ttu-id="4eca4-151">命令提示字元開啟後，輸入 *dsregcmd.exe /status*。</span><span class="sxs-lookup"><span data-stu-id="4eca4-151">Once the command prompt is open, type “*dsregcmd.exe /status*”.</span></span>
3.  <span data-ttu-id="4eca4-152">若要獲得預期的輸出，[AzureAdJoined] 欄位值應該是 [YES]、[WamDefaultSet] 欄位值應該是 [YES]，而 [WamDefaultGUID] 欄位值則應該是一個結尾為 “(AzureAd)” 的 GUID。</span><span class="sxs-lookup"><span data-stu-id="4eca4-152">For expected output, the **AzureAdJoined** field value should be “YES”, **WamDefaultSet** field value should be “YES”, and the **WamDefaultGUID** field value should be a GUID with “(AzureAd)” at the end.</span></span>

<span data-ttu-id="4eca4-153">**可能的原因**：**WamDefaultSet** 和 **AzureAdJoined** 的欄位值都是 [NO]、裝置已經加入網域且已經在 Azure AD 註冊，以及裝置沒有同步處理。</span><span class="sxs-lookup"><span data-stu-id="4eca4-153">**Potential issue**: **WamDefaultSet** and **AzureAdJoined** both have “NO” in the field value, the device was domain-joined and registered with Azure AD, and the device does not sync.</span></span> <span data-ttu-id="4eca4-154">如果顯示此問題，表示裝置可能需要等待原則套用，或裝置在連線至 Azure AD 時驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="4eca4-154">If it is showing this, the device may need to wait for policy to be applied or the authentication for the device failed when connecting to Azure AD.</span></span> <span data-ttu-id="4eca4-155">使用者可能需等待幾個小時來等待原則套用。</span><span class="sxs-lookup"><span data-stu-id="4eca4-155">The user may have to wait a few hours for the policy to be applied.</span></span> <span data-ttu-id="4eca4-156">其他疑難排解步驟可能包括透過登出並重新登入來重試自動註冊，或在工作排程器中啟動工作。</span><span class="sxs-lookup"><span data-stu-id="4eca4-156">Other troubleshooting steps may include retrying auto-registration by signing out and back in, or launching the task in Task Scheduler.</span></span> <span data-ttu-id="4eca4-157">在某些情況下，於已提升權限的命令提示字元視窗中執行 *dsregcmd.exe /leave*、重新開機，然後再試一次註冊，可能有助於解決此問題。</span><span class="sxs-lookup"><span data-stu-id="4eca4-157">In some cases, running “*dsregcmd.exe /leave*” in an elevated command prompt window, rebooting, and trying registration again may help with this issue.</span></span>


<span data-ttu-id="4eca4-158">**可能的原因**：**AzureAdSettingsUrl** 的欄位空白且裝置沒有同步處理。</span><span class="sxs-lookup"><span data-stu-id="4eca4-158">**Potential issue**: The field for **AzureAdSettingsUrl** is empty and the device does not sync.</span></span> <span data-ttu-id="4eca4-159">使用者上次登入裝置的時間可能是在於 Azure Active Directory 入口網站中啟用企業狀態漫遊之前。</span><span class="sxs-lookup"><span data-stu-id="4eca4-159">The user may have last logged in to the device before Enterprise State Roaming was enabled in the Azure Active Directory Portal.</span></span> <span data-ttu-id="4eca4-160">重新啟動裝置並讓使用者登入。</span><span class="sxs-lookup"><span data-stu-id="4eca4-160">Restart the device and have the user login.</span></span> <span data-ttu-id="4eca4-161">(選擇性) 在入口網站中，嘗試停用 IT 系統管理員，然後重新啟用「使用者可以同步設定及企業應用程式資料」。</span><span class="sxs-lookup"><span data-stu-id="4eca4-161">Optionally, in the portal, try having the IT Admin disable and re-enable Users May Sync Settings and Enterprise App Data.</span></span> <span data-ttu-id="4eca4-162">重新啟用之後，請重新啟動裝置並讓使用者登入。</span><span class="sxs-lookup"><span data-stu-id="4eca4-162">Once re-enabled, restart the device and have the user login.</span></span> <span data-ttu-id="4eca4-163">如果這樣做無法解決問題，錯誤裝置憑證中的 **AzureAdSettingsUrl** 可能是空的。</span><span class="sxs-lookup"><span data-stu-id="4eca4-163">If this does not resolve the issue, **AzureAdSettingsUrl** may be empty in the case of a bad device certificate.</span></span> <span data-ttu-id="4eca4-164">在此情況下，於已提升權限的命令提示字元視窗中執行 *dsregcmd.exe /leave*、重新開機，然後再試一次註冊，可能有助於解決此問題。</span><span class="sxs-lookup"><span data-stu-id="4eca4-164">In this case, running “*dsregcmd.exe /leave*” in an elevated command prompt window, rebooting, and trying registration again may help with this issue.</span></span>

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a><span data-ttu-id="4eca4-165">企業狀態漫遊與 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="4eca4-165">Enterprise State Roaming and Multi-Factor Authentication</span></span> 
<span data-ttu-id="4eca4-166">在某些情況下，如果設定了 Azure Multi-Factor Authentication，「企業狀態漫遊」可能會無法同步處理資料。</span><span class="sxs-lookup"><span data-stu-id="4eca4-166">Under certain conditions, Enterprise State Roaming can fail to sync data if Azure Multi-Factor Authentication is configured.</span></span> <span data-ttu-id="4eca4-167">如需有關這些徵兆的其他詳細資料，請參閱支援文件 [KB3193683](https://support.microsoft.com/kb/3193683)。</span><span class="sxs-lookup"><span data-stu-id="4eca4-167">For additional details on these symptoms, see the support document [KB3193683](https://support.microsoft.com/kb/3193683).</span></span> 

<span data-ttu-id="4eca4-168">**可能的原因**：如果您的裝置已設定為在 Azure Active Directory 入口網站上需要 Multi-Factor Authentication，則使用密碼登入 Windows 10 裝置時，可能無法同步處理設定。</span><span class="sxs-lookup"><span data-stu-id="4eca4-168">**Potential issue**: If your device is configured to require Multi-Factor Authentication on the Azure Active Directory portal, you may fail to sync settings while signing in to a Windows 10 device using a password.</span></span> <span data-ttu-id="4eca4-169">這類型的 Multi-Factor Authentication 組態是用來保護 Azure 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="4eca4-169">This type of Multi-Factor Authentication configuration is intended to protect an Azure administrator account.</span></span> <span data-ttu-id="4eca4-170">系統管理員使用者仍然能夠藉由使用 Microsoft Passport for Work PIN 登入他們的 Windows 10 裝置，或藉由在存取其他 Azure 服務 (例如 Office 365) 時完成 Multi-Factor Authentication，來進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="4eca4-170">Admin users may still be able to sync by signing in to their Windows 10 devices with their Microsoft Passport for Work PIN or by completing Multi-Factor Authentication while accessing other Azure services like Office 365.</span></span>

<span data-ttu-id="4eca4-171">**可能的原因**：如果系統管理員設定 Active Directory Federation Services Multi-Factor Authentication 條件式存取原則，而裝置上的存取權杖到期，則同步處理可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="4eca4-171">**Potential issue**: Sync can fail if the admin configures the Active Directory Federation Services Multi-Factor Authentication conditional access policy and the access token on the device expires.</span></span> <span data-ttu-id="4eca4-172">務必使用 Microsoft Passport for Work PIN 來登入和登出，或在存取其他 Azure 服務 (例如 Office 365) 時完成 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="4eca4-172">Ensure that you sign in and sign out using the Microsoft Passport for Work PIN or complete Multi-Factor Authentication while accessing other Azure services like Office 365.</span></span>

###<a name="event-viewer"></a><span data-ttu-id="4eca4-173">事件檢視器</span><span class="sxs-lookup"><span data-stu-id="4eca4-173">Event Viewer</span></span>
<span data-ttu-id="4eca4-174">進行進階疑難排解時，可以使用「事件檢視器」來找出特定錯誤。</span><span class="sxs-lookup"><span data-stu-id="4eca4-174">For advanced troubleshooting, Event Viewer can be used to find specific errors.</span></span> <span data-ttu-id="4eca4-175">這些錯誤記載在下面的表格中。</span><span class="sxs-lookup"><span data-stu-id="4eca4-175">These are documented in the table below.</span></span> <span data-ttu-id="4eca4-176">您可以在 [事件檢視器] > [應用程式及服務紀錄檔] > [Microsoft] > [Windows] > [SettingSync] 底下找到事件，和身分識別有關的問題則可以透過同步處理 [Microsoft] > [Windows] > [Azure AD] 來找到。</span><span class="sxs-lookup"><span data-stu-id="4eca4-176">The events can be found under Event Viewer > Applications and Services Logs > **Microsoft** > **Windows** > **SettingSync** and for identity-related issues with sync **Microsoft** > **Windows** > **Azure AD**.</span></span>


## <a name="known-issues"></a><span data-ttu-id="4eca4-177">已知問題</span><span class="sxs-lookup"><span data-stu-id="4eca4-177">Known issues</span></span>

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a><span data-ttu-id="4eca4-178">同步處理在使用 MDM 軟體側載應用程式的裝置上無法運作</span><span class="sxs-lookup"><span data-stu-id="4eca4-178">Sync does not work on devices that have apps side-loaded using MDM software</span></span>

<span data-ttu-id="4eca4-179">會影響執行 Windows 10 年度更新版 (版本 1607) 的裝置。</span><span class="sxs-lookup"><span data-stu-id="4eca4-179">Affects devices running the Windows 10 Anniversary Update (Version 1607).</span></span> <span data-ttu-id="4eca4-180">在 [事件檢視器] 中的 [SettingSync-Azure 記錄] 底下，常會看到事件識別碼 6013 與錯誤 80070259。</span><span class="sxs-lookup"><span data-stu-id="4eca4-180">In Event Viewer under the SettingSync-Azure logs, the Event ID 6013 with error 80070259 is frequently seen.</span></span>

<span data-ttu-id="4eca4-181">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="4eca4-181">**Recommended action**</span></span>  
<span data-ttu-id="4eca4-182">確定 Windows 10 v1607 用戶端具有 2016 年 ８ 月 23 日累積更新 ([KB3176934](https://support.microsoft.com/kb/3176934) 作業系統組建 14393.82)。</span><span class="sxs-lookup"><span data-stu-id="4eca4-182">Make sure the Windows 10 v1607 client has the August 23, 2016 Cumulative Update ([KB3176934](https://support.microsoft.com/kb/3176934) OS Build 14393.82).</span></span> 

---

### <a name="internet-explorer-favorites-do-not-sync"></a><span data-ttu-id="4eca4-183">Internet Explorer 我的最愛不會同步</span><span class="sxs-lookup"><span data-stu-id="4eca4-183">Internet Explorer Favorites do not sync</span></span>

<span data-ttu-id="4eca4-184">會影響執行 Windows 10 11 月更新版 (版本 1511) 的裝置。</span><span class="sxs-lookup"><span data-stu-id="4eca4-184">Affects devices running the Windows 10 November Update (Version 1511).</span></span>

<span data-ttu-id="4eca4-185">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="4eca4-185">**Recommended action**</span></span>  
<span data-ttu-id="4eca4-186">確定 Windows 10 v1511 用戶端具有 2016 年 7 月累積更新 ([KB3172985](https://support.microsoft.com/kb/3172985) 作業系統組建 10586.494)。</span><span class="sxs-lookup"><span data-stu-id="4eca4-186">Make sure the Windows 10 v1511 client has the July 2016 Cumulative Update ([KB3172985](https://support.microsoft.com/kb/3172985) OS Build 10586.494).</span></span>

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a><span data-ttu-id="4eca4-187">佈景主題和使用「Windows 資訊保護」保護的資料不會同步處理</span><span class="sxs-lookup"><span data-stu-id="4eca4-187">Theme is not syncing, as well as data protected with Windows Information Protection</span></span> 

<span data-ttu-id="4eca4-188">爲防止資料外洩，使用 [Windows 資訊保護 (英文)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) 保護的資料不會透過使用 Windows 10 年度更新版之裝置的企業狀態漫遊來進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="4eca4-188">To prevent data leakage, data that is protected with [Windows Information Protection](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) will not sync through Enterprise State Roaming for devices using the Windows 10 Anniversary Update.</span></span>



<span data-ttu-id="4eca4-189">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="4eca4-189">**Recommended action**</span></span>  
<span data-ttu-id="4eca4-190">無。</span><span class="sxs-lookup"><span data-stu-id="4eca4-190">None.</span></span> <span data-ttu-id="4eca4-191">未來的 Windows 更新可能會解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="4eca4-191">Future updates to Windows may resolve this issue.</span></span>

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a><span data-ttu-id="4eca4-192">已加入網域的裝置上不會同步處理日期、時間及地區設定</span><span class="sxs-lookup"><span data-stu-id="4eca4-192">Date, Time, and Region settings do not sync on domain-joined device</span></span> 
  
<span data-ttu-id="4eca4-193">已加入網域的裝置將不會同步處理日期、時間及地區：自動時間設定。</span><span class="sxs-lookup"><span data-stu-id="4eca4-193">Devices that are domain-joined will not experience sync for the setting Date, Time, and Region: automatic time.</span></span> <span data-ttu-id="4eca4-194">使用自動時間可能會複寫其他日期、時間及地區設定，並導致那些設定不會同步處理。</span><span class="sxs-lookup"><span data-stu-id="4eca4-194">Using automatic time may override the other Date, Time, and Region settings and cause those settings not to sync.</span></span> 

<span data-ttu-id="4eca4-195">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="4eca4-195">**Recommended action**</span></span>  
<span data-ttu-id="4eca4-196">無。</span><span class="sxs-lookup"><span data-stu-id="4eca4-196">None.</span></span> 

---

### <a name="uac-prompts-when-syncing-passwords"></a><span data-ttu-id="4eca4-197">同步密碼時出現 UAC 提示</span><span class="sxs-lookup"><span data-stu-id="4eca4-197">UAC Prompts when syncing passwords</span></span>

<span data-ttu-id="4eca4-198">會影響執行 Windows 10 11 月更新版 (版本 1511) 並具備無線 NIC 且已設定為同步處理密碼的裝置。</span><span class="sxs-lookup"><span data-stu-id="4eca4-198">Affects devices running the Windows 10 November Update (Version 1511) with a wireless NIC that is configured to sync passwords.</span></span>

<span data-ttu-id="4eca4-199">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="4eca4-199">**Recommended action**</span></span>  
<span data-ttu-id="4eca4-200">確定 Windows 10 v1511 用戶端具有累積更新 ([KB3140743](https://support.microsoft.com/kb/3140743) 作業系統組建 10586.494)。</span><span class="sxs-lookup"><span data-stu-id="4eca4-200">Make sure the Windows 10 v1511 client has the Cumulative Update ([KB3140743](https://support.microsoft.com/kb/3140743) OS Build 10586.494).</span></span>

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a><span data-ttu-id="4eca4-201">同步處理不會在使用智慧卡登入的裝置上運作</span><span class="sxs-lookup"><span data-stu-id="4eca4-201">Sync does not work on devices that use smart card for login</span></span>
<span data-ttu-id="4eca4-202">如果您嘗試使用智慧卡或虛擬智慧卡來登入您的 Windows 裝置，設定同步處理將會停止運作。</span><span class="sxs-lookup"><span data-stu-id="4eca4-202">If you attempt to sign in to your Windows device using a smart card or virtual smart card, settings sync will stop working.</span></span>     

<span data-ttu-id="4eca4-203">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="4eca4-203">**Recommended action**</span></span>  
<span data-ttu-id="4eca4-204">無。</span><span class="sxs-lookup"><span data-stu-id="4eca4-204">None.</span></span> <span data-ttu-id="4eca4-205">未來的 Windows 更新可能會解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="4eca4-205">Future updates to Windows may resolve this issue.</span></span>

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a><span data-ttu-id="4eca4-206">已加入網域的裝置不會在離開公司網路後同步處理</span><span class="sxs-lookup"><span data-stu-id="4eca4-206">Domain-joined device is not syncing after leaving corporate network</span></span>     
<span data-ttu-id="4eca4-207">如果已加入網域並已向 Azure AD 註冊的裝置離站很長的時間，同步處理可能會失敗且無法完成網域驗證。</span><span class="sxs-lookup"><span data-stu-id="4eca4-207">Domain-joined devices registered to Azure AD may experience sync failure if the device is off-site for extended periods of time, and domain authentication can't complete.</span></span>

<span data-ttu-id="4eca4-208">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="4eca4-208">**Recommended action**</span></span>  
<span data-ttu-id="4eca4-209">請將裝置連線到公司網路，以便讓同步處理能夠繼續執行。</span><span class="sxs-lookup"><span data-stu-id="4eca4-209">Connect the device to a corporate network so that sync can resume.</span></span>

---

 ### <a name="azure-ad-joined-device-is-not-syncing-and-the-user-has-a-mixed-case-user-principal-name"></a><span data-ttu-id="4eca4-210">Azure AD 聯結裝置未同步處理，而且使用者的使用者主體名稱混用大小寫。</span><span class="sxs-lookup"><span data-stu-id="4eca4-210">Azure AD Joined device is not syncing and the user has a mixed case User Principal Name.</span></span>
 <span data-ttu-id="4eca4-211">如果使用者有混用大小寫的 UPN (例如 UserName 而不是 username)，而且使用者在已從 Windows 10 組建 10586 升級至 14393 的 Azure AD 聯結裝置上，使用者的裝置可能無法同步處理。</span><span class="sxs-lookup"><span data-stu-id="4eca4-211">If the user has a mixed case UPN (e.g. UserName instead of username) and the user is on an Azure AD Joined device which has upgraded from Windows 10 Build 10586 to 14393, the user's device may fail to sync.</span></span> 

<span data-ttu-id="4eca4-212">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="4eca4-212">**Recommended action**</span></span>  
<span data-ttu-id="4eca4-213">使用者必須退出裝置並重新加入到雲端。</span><span class="sxs-lookup"><span data-stu-id="4eca4-213">The user will need to unjoin and rejoin the device to the cloud.</span></span> <span data-ttu-id="4eca4-214">若要這樣做，請以本機系統管理員使用者的身分登入，並移至 [設定]  >  [系統]  >  [關於]，然後選取 [管理或中斷連線公司或學校帳戶] 以退出裝置。</span><span class="sxs-lookup"><span data-stu-id="4eca4-214">To do this, login as the Local Administrator user and unjoin the device by going to **Settings** > **System** > **About** and select "Manage or disconnect from work or school".</span></span> <span data-ttu-id="4eca4-215">清除下列檔案，在 [設定]  >  [系統]  >  [關於] 中選取 [連線到公司或學校]，Azure AD 就會再次加入裝置。</span><span class="sxs-lookup"><span data-stu-id="4eca4-215">Clean up the files below, and then Azure AD Join the device again in **Settings** > **System** > **About** and selecting "Connect to Work or School".</span></span> <span data-ttu-id="4eca4-216">繼續將裝置加入 Azure Active Directory，並完成流程。</span><span class="sxs-lookup"><span data-stu-id="4eca4-216">Continue to join the device to Azure Active Directory and complete the flow.</span></span>

<span data-ttu-id="4eca4-217">在清除步驟中，清除下列檔案︰</span><span class="sxs-lookup"><span data-stu-id="4eca4-217">In the cleanup step, cleanup the following files:</span></span>
- <span data-ttu-id="4eca4-218">`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\` 中的 Settings.dat</span><span class="sxs-lookup"><span data-stu-id="4eca4-218">Settings.dat in `C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\`</span></span>
- <span data-ttu-id="4eca4-219">資料夾 `C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account` 下的所有檔案</span><span class="sxs-lookup"><span data-stu-id="4eca4-219">All the files under the folder `C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`</span></span>

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a><span data-ttu-id="4eca4-220">事件識別碼 6065：80070533 此使用者無法登入，因為此帳戶目前已停用</span><span class="sxs-lookup"><span data-stu-id="4eca4-220">Event ID 6065: 80070533 This user can’t sign in because this account is currently disabled</span></span>  
<span data-ttu-id="4eca4-221">在「事件檢視器」的 SettingSync/Debug 記錄檔底下，當使用者的認證過期時，可能會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4eca4-221">In Event Viewer under the SettingSync/Debug logs, this error can be seen when the user's credentials have expired.</span></span> <span data-ttu-id="4eca4-222">此外，當租用戶未自動佈建 AzureRMS 時，可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4eca4-222">In addition, it can occur when the tenant did not automatically have AzureRMS provisioned.</span></span> 

<span data-ttu-id="4eca4-223">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="4eca4-223">**Recommended action**</span></span>  
<span data-ttu-id="4eca4-224">在第一個案例中，讓使用者更新其認證，並使用新的認證登入到裝置。</span><span class="sxs-lookup"><span data-stu-id="4eca4-224">In the first case, have the user update their credentials and login to the device with the new credentials.</span></span> <span data-ttu-id="4eca4-225">若要解決 AzureRMS 問題，請繼續執行 [KB3193791](https://support.microsoft.com/kb/3193791) 中列出的步驟。</span><span class="sxs-lookup"><span data-stu-id="4eca4-225">To solve the AzureRMS issue, proceed with the steps listed in [KB3193791](https://support.microsoft.com/kb/3193791).</span></span> 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a><span data-ttu-id="4eca4-226">事件識別碼 1098：錯誤：0xCAA5001C 權杖代理人操作失敗</span><span class="sxs-lookup"><span data-stu-id="4eca4-226">Event ID 1098: Error: 0xCAA5001C Token broker operation failed</span></span>  
<span data-ttu-id="4eca4-227">在「事件檢視器」中的 AAD/作業記錄底下，可能會在事件 1104：AAD 雲端 AP 外掛程式呼叫 Get token 但傳回錯誤：0xC000005F 時看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4eca4-227">In Event Viewer under the AAD/Operational logs, this error may be seen with Event 1104: AAD Cloud AP plugin call Get token returned error: 0xC000005F.</span></span> <span data-ttu-id="4eca4-228">如果缺少權限或擁有權屬性，就會發生這個問題。</span><span class="sxs-lookup"><span data-stu-id="4eca4-228">This issue occurs if there are missing permissions or ownership attributes.</span></span>  

<span data-ttu-id="4eca4-229">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="4eca4-229">**Recommended action**</span></span>  
<span data-ttu-id="4eca4-230">請繼續執行 [KB3196528](https://support.microsoft.com/kb/3196528) 中列出的步驟。</span><span class="sxs-lookup"><span data-stu-id="4eca4-230">Proceed with the steps listed [KB3196528](https://support.microsoft.com/kb/3196528).</span></span>  



## <a name="next-steps"></a><span data-ttu-id="4eca4-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4eca4-231">Next steps</span></span>

- <span data-ttu-id="4eca4-232">利用[使用者心聲論壇](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming)來提供意見並提出如何改善企業狀態漫遊的建議。</span><span class="sxs-lookup"><span data-stu-id="4eca4-232">Use the [User Voice forum](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming) to provide feedback and make suggestions on how to improve Enterprise State Roaming.</span></span>

- <span data-ttu-id="4eca4-233">如需詳細資訊，請參閱[企業狀態漫遊概觀](active-directory-windows-enterprise-state-roaming-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4eca4-233">For more information, see the [Enterprise State Roaming overview](active-directory-windows-enterprise-state-roaming-overview.md).</span></span> 

## <a name="related-topics"></a><span data-ttu-id="4eca4-234">相關主題</span><span class="sxs-lookup"><span data-stu-id="4eca4-234">Related topics</span></span>
* [<span data-ttu-id="4eca4-235">企業狀態漫遊概觀</span><span class="sxs-lookup"><span data-stu-id="4eca4-235">Enterprise state roaming overview</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)
* [<span data-ttu-id="4eca4-236">在 Azure Active Directory 中啟用企業狀態漫遊</span><span class="sxs-lookup"><span data-stu-id="4eca4-236">Enable enterprise state roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md)
* [<span data-ttu-id="4eca4-237">設定和資料漫遊常見問題集</span><span class="sxs-lookup"><span data-stu-id="4eca4-237">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md)
* [<span data-ttu-id="4eca4-238">設定同步處理的群組原則和 MDM 設定</span><span class="sxs-lookup"><span data-stu-id="4eca4-238">Group policy and MDM settings for settings sync</span></span>](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [<span data-ttu-id="4eca4-239">Windows 10 漫遊設定參考</span><span class="sxs-lookup"><span data-stu-id="4eca4-239">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
