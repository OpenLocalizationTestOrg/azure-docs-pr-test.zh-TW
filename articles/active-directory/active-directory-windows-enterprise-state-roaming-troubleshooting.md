---
title: "針對 Azure Active Directory 中的企業狀態漫遊設定進行疑難排解 | Microsoft Docs"
description: "提供有關設定和應用程式資料同步可能答案 toosome 問題 IT 系統管理員。"
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
ms.openlocfilehash: 4636d016983426e30d696459f54167b8ad2babcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a><span data-ttu-id="bdc9d-104">針對 Azure Active Directory 中的企業狀態漫遊設定進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="bdc9d-104">Troubleshooting Enterprise State Roaming settings in Azure Active Directory</span></span>

<span data-ttu-id="bdc9d-105">本主題提供如何的相關資訊 tootroubleshoot 和診斷企業狀態漫遊的問題，並提供的已知問題清單。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-105">This topic provides information on how tootroubleshoot and diagnose issues with Enterprise State Roaming, and provides a list of known issues.</span></span>

## <a name="preliminary-steps-for-troubleshooting"></a><span data-ttu-id="bdc9d-106">疑難排解的預備步驟</span><span class="sxs-lookup"><span data-stu-id="bdc9d-106">Preliminary steps for troubleshooting</span></span> 
<span data-ttu-id="bdc9d-107">開始之前疑難排解確認，hello 使用者和裝置已設定正確，且裝置 hello 和 hello 使用者符合所有 hello 需求的企業狀態漫遊。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-107">Before beginning troubleshooting verify that hello user and device have been configured properly, and that all hello requirements of Enterprise State Roaming are met by hello device and hello user.</span></span> 

1. <span data-ttu-id="bdc9d-108">Hello 裝置上安裝 Windows 10 與 hello 最新的更新和最小版本 1511 （作業系統組建 10586 或更新版本）。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-108">Windows 10, with hello latest updates, and a minimum Version 1511 (OS Build 10586 or later) is installed on hello device.</span></span> 
2. <span data-ttu-id="bdc9d-109">hello 裝置已加入，或已加入網域並向 Azure AD 註冊的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-109">hello device is Azure AD joined, or domain-joined and registered with Azure AD.</span></span>
3. <span data-ttu-id="bdc9d-110">在 hello Azure Active Directory 入口網站**企業狀態漫遊**hello 目錄下啟用**設定** > **裝置** > **使用者可以同步設定及企業應用程式資料**。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-110">In hello Azure Active Directory portal, **Enterprise State Roaming** is enabled for hello directory under **Configure** > **Devices** > **Users May Sync Settings and Enterprise App Data**.</span></span> <span data-ttu-id="bdc9d-111">選取所有的使用者，或是 hello 使用者是用於透過 hello 選取選項的同步處理已啟用，而且包含在 hello 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-111">Either all users are selected, or hello user is enabled for syncing through hello selected option, and included in hello security group.</span></span>
4. <span data-ttu-id="bdc9d-112">hello 使用者具有 Azure Active Directory Premium 訂閱指派 toothem。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-112">hello user has an Azure Active Directory Premium subscription assigned toothem.</span></span>  
5. <span data-ttu-id="bdc9d-113">hello 裝置已重新啟動，並啟用企業狀態漫遊之後 hello 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-113">hello device has been restarted, and hello user has logged in after Enterprise State Roaming has been enabled.</span></span>

## <a name="information-tooinclude-when-you-need-help"></a><span data-ttu-id="bdc9d-114">當您需要協助的資訊 tooinclude</span><span class="sxs-lookup"><span data-stu-id="bdc9d-114">Information tooinclude when you need help</span></span>
<span data-ttu-id="bdc9d-115">如果您無法解決您的問題與下列 hello 指引，您可以連絡我們的支援工程師。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-115">If you cannot solve your issue with hello guidance below, you can contact our support engineers.</span></span> <span data-ttu-id="bdc9d-116">當您與他們連絡時，我們建議 tooinclude hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="bdc9d-116">When you contact them, it is recommended tooinclude hello following information:</span></span>

- <span data-ttu-id="bdc9d-117">**Hello 錯誤的一般描述**– 有 hello 使用者看見的錯誤訊息？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-117">**General description of hello error** – Are there error messages seen by hello user?</span></span> <span data-ttu-id="bdc9d-118">如果不發生任何錯誤訊息，說明 hello 未預期的行為，您會注意到，在詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-118">If there was no error message, describe hello unexpected behavior you noticed, in detail.</span></span> <span data-ttu-id="bdc9d-119">哪些功能可供同步和是預期 toosync hello 使用者？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-119">What features are enabled for sync and what is hello user expecting toosync?</span></span> <span data-ttu-id="bdc9d-120">多項功能不會同步，或者是隔離的 it tooone？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-120">Are multiple features not syncing or is it isolated tooone?</span></span>
- <span data-ttu-id="bdc9d-121">**受影響的使用者** – 是有一位還是多位使用者的同步處理成功/失敗？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-121">**Users affected** – Is sync working/failing for one user or multiple users?</span></span> <span data-ttu-id="bdc9d-122">每個使用者涉及多少裝置？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-122">How many devices are involved per user?</span></span> <span data-ttu-id="bdc9d-123">它們是否都沒有同步處理，或它們之間部分已同步處理，部分沒有同步處理？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-123">Are all of them not syncing or are some of them syncing and some not syncing?</span></span>
- <span data-ttu-id="bdc9d-124">**Hello 使用者資訊**– 何種身分識別是使用 toolog toohello 裝置中的 hello 使用者嗎？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-124">**Information about hello user** – What identity is hello user using toolog in toohello device?</span></span> <span data-ttu-id="bdc9d-125">Hello 使用者如何記錄 toohello 裝置？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-125">How is hello user logging in toohello device?</span></span> <span data-ttu-id="bdc9d-126">它們屬於選取的安全性群組，允許 toosync 嗎？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-126">Are they part of a selected security group allowed toosync?</span></span> 
- <span data-ttu-id="bdc9d-127">**Hello 裝置的相關資訊**– 此裝置加入 Azure AD 之或已加入網域？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-127">**Information about hello device** – Is this device Azure AD Joined or domain-joined?</span></span> <span data-ttu-id="bdc9d-128">哪些組建是 hello 的裝置上？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-128">What build is hello device on?</span></span> <span data-ttu-id="bdc9d-129">Hello 最新的更新有哪些？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-129">What are hello most recent updates?</span></span>
- <span data-ttu-id="bdc9d-130">**日期 / 時間 / 時區**– hello 確切的日期和的時間看到 hello 錯誤 （包含 hello 時區）？</span><span class="sxs-lookup"><span data-stu-id="bdc9d-130">**Date / Time / Timezone** – What was hello precise date and time you saw hello error (include hello timezone)?</span></span>
- <span data-ttu-id="bdc9d-131">包含這項資訊有助於我們盡快為您解決問題。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-131">Including this information helps us solve your problem as quickly as possible.</span></span>

## <a name="troubleshooting-and-diagnosing-issues"></a><span data-ttu-id="bdc9d-132">疑難排解和診斷問題</span><span class="sxs-lookup"><span data-stu-id="bdc9d-132">Troubleshooting and diagnosing issues</span></span>
<span data-ttu-id="bdc9d-133">本節提供如何建議 tootroubleshoot 及診斷問題的相關的 tooEnterprise 漫遊狀態。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-133">This section gives suggestions on how tootroubleshoot and diagnose problems related tooEnterprise State Roaming.</span></span>

## <a name="verify-sync-and-hello-sync-your-settings-settings-page"></a><span data-ttu-id="bdc9d-134">確認同步處理，並 hello"同步您的設定 」 設定 頁面</span><span class="sxs-lookup"><span data-stu-id="bdc9d-134">Verify sync, and hello “Sync your settings” settings page</span></span> 

1. <span data-ttu-id="bdc9d-135">加入 Windows 10 電腦 tooa 之後網域設定 tooallow 企業狀態漫遊，請使用您的工作帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-135">After joining your Windows 10 PC tooa domain that is configured tooallow Enterprise State Roaming, logon with your work account.</span></span> <span data-ttu-id="bdc9d-136">跳過**設定** > **帳戶** > **同步處理您的設定**，並確認同步處理和 hello 個別的設定，和該 hello 頂端hello 設定頁面會指出您正在使用工作帳戶同步處理。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-136">Go too**Settings** > **Accounts** > **Sync Your Settings** and confirm that sync and hello individual settings are on, and that hello top of hello settings page indicates that you are syncing with your work account.</span></span> <span data-ttu-id="bdc9d-137">確認在您登入帳戶也會使用相同帳戶的 hello**設定** > **帳戶** > **您資訊**。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-137">Confirm hello same account is also used as your login account in **Settings** > **Accounts** > **Your Info**.</span></span> 
2. <span data-ttu-id="bdc9d-138">確認同步處理運作跨多部機器 hello 原始電腦，例如移動 hello 工作列 toohello 靠右或最上層的一端囉 」 畫面上，進行一些變更。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-138">Verify that sync works across multiple machines by making some changes on hello original machine, such as moving hello taskbar toohello right or top side of hello screen.</span></span> <span data-ttu-id="bdc9d-139">觀賞 hello 變更五分鐘內傳播 toohello 第二部電腦。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-139">Watch hello change propagate toohello second machine within five minutes.</span></span> 
 - <span data-ttu-id="bdc9d-140">鎖定和解除鎖定囉 」 畫面 （Win + L） 可協助您在同步處理觸發程序。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-140">Locking and unlocking hello screen (Win + L) can help trigger a sync.</span></span>
 - <span data-ttu-id="bdc9d-141">您必須使用 hello 的同步處理 toowork – 這兩種電腦上的相同登入帳戶，因為企業狀態漫遊是繫結的 toohello 使用者帳戶和 hello 電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-141">You must be using hello same logon account on both PCs for sync toowork – as Enterprise State Roaming is tied toohello user account and not hello machine account.</span></span>

<span data-ttu-id="bdc9d-142">**可能的問題**: hello 設定 頁面上有呈灰色，hello 切換，而不是查看帳戶，您看到 hello 文字"一些 Windows 功能才會出現您使用 Microsoft 帳戶或工作帳戶 」。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-142">**Potential Issue**: hello settings page has hello toggles grayed out, and instead of seeing an account, you see hello text “Some Windows features are only available if you are using a Microsoft account or work account”.</span></span> <span data-ttu-id="bdc9d-143">針對已設定 toobe 的裝置已加入網域並註冊 tooAzure AD，但是 hello 裝置已成功驗證 tooAzure AD，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-143">This issue may arise for devices that have been set up toobe domain-joined and registered tooAzure AD, but hello device has not successfully authenticated tooAzure AD.</span></span> <span data-ttu-id="bdc9d-144">可能的原因是必須套用 hello 裝置原則，但此應用程式會以非同步的方式，而且可能會因為幾小時的時間延遲。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-144">A possible cause is that hello device policy must be applied, but this application happens asynchronously, and could be delayed by a few hours.</span></span> <span data-ttu-id="bdc9d-145">這個問題，請依照中的 hello 步驟確認的 tooverify hello 裝置登錄狀態 toocheck 如果 hello 這樣的狀況。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-145">tooverify this issue, follow hello steps in verify hello device registration status toocheck if this is hello case.</span></span>

### <a name="verify-hello-device-registration-status"></a><span data-ttu-id="bdc9d-146">確認 hello 裝置登錄狀態</span><span class="sxs-lookup"><span data-stu-id="bdc9d-146">Verify hello device registration status</span></span>
<span data-ttu-id="bdc9d-147">企業狀態漫遊需要 hello 裝置 toobe 向 Azure AD 註冊。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-147">Enterprise State Roaming requires hello device toobe registered with Azure AD.</span></span> <span data-ttu-id="bdc9d-148">雖然不是特定 tooEnterprise 狀態漫遊，遵循下列指示 hello 可以幫助確認該 hello 註冊 Windows 10 用戶端，並確認憑證指紋，Azure AD 設定 URL，NGC 狀態，以及其他資訊。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-148">Although not specific tooEnterprise State Roaming, following hello instructions below can help confirm that hello Windows 10 Client is registered, and confirm thumbprint, Azure AD settings URL, NGC status, and other information.</span></span>

1.  <span data-ttu-id="bdc9d-149">開啟 hello 命令提示字元停權。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-149">Open hello command prompt unelevated.</span></span> <span data-ttu-id="bdc9d-150">這在 Windows 中，開啟 toodo hello 執行啟動器 （Win + R），並輸入"cmd"tooopen。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-150">toodo this in Windows, open hello Run launcher (Win + R) and type “cmd” tooopen.</span></span>
2.  <span data-ttu-id="bdc9d-151">一旦開啟 hello 命令提示字元，輸入 「*dsregcmd.exe /status*"。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-151">Once hello command prompt is open, type “*dsregcmd.exe /status*”.</span></span>
3.  <span data-ttu-id="bdc9d-152">預期的輸出，如 hello **AzureAdJoined**欄位值應該是"YES"， **WamDefaultSet**欄位值應該是"YES"，並且 hello **WamDefaultGUID**欄位值應該是GUID"(azure Ad)"hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-152">For expected output, hello **AzureAdJoined** field value should be “YES”, **WamDefaultSet** field value should be “YES”, and hello **WamDefaultGUID** field value should be a GUID with “(AzureAd)” at hello end.</span></span>

<span data-ttu-id="bdc9d-153">**可能的問題**: **WamDefaultSet**和**AzureAdJoined** hello 欄位值中有 「 否 」，hello 裝置已加入網域且已註冊使用 Azure AD，和 hello 裝置不會同步。如果顯示這個，hello 裝置可能需要套用的原則 toobe toowait 或 hello hello 裝置連線 tooAzure AD 時發生失敗的驗證。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-153">**Potential issue**: **WamDefaultSet** and **AzureAdJoined** both have “NO” in hello field value, hello device was domain-joined and registered with Azure AD, and hello device does not sync. If it is showing this, hello device may need toowait for policy toobe applied or hello authentication for hello device failed when connecting tooAzure AD.</span></span> <span data-ttu-id="bdc9d-154">hello 使用者有 toowait hello 原則 toobe 套用的幾個小時。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-154">hello user may have toowait a few hours for hello policy toobe applied.</span></span> <span data-ttu-id="bdc9d-155">其他疑難排解步驟可能包含由簽署 out 與中，或啟動工作排程器中的 hello 工作重試自動註冊。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-155">Other troubleshooting steps may include retrying auto-registration by signing out and back in, or launching hello task in Task Scheduler.</span></span> <span data-ttu-id="bdc9d-156">在某些情況下，於已提升權限的命令提示字元視窗中執行 *dsregcmd.exe /leave*、重新開機，然後再試一次註冊，可能有助於解決此問題。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-156">In some cases, running “*dsregcmd.exe /leave*” in an elevated command prompt window, rebooting, and trying registration again may help with this issue.</span></span>


<span data-ttu-id="bdc9d-157">**可能的問題**: hello 欄位**AzureAdSettingsUrl**是空白的然後 hello 裝置不同步。 hello 使用者可能已上次登入 toohello 裝置 hello Azure Active 中啟用企業狀態漫遊之前目錄入口網站。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-157">**Potential issue**: hello field for **AzureAdSettingsUrl** is empty and hello device does not sync. hello user may have last logged in toohello device before Enterprise State Roaming was enabled in hello Azure Active Directory Portal.</span></span> <span data-ttu-id="bdc9d-158">重新啟動 hello 裝置並擁有 hello 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-158">Restart hello device and have hello user login.</span></span> <span data-ttu-id="bdc9d-159">（選擇性） 在 hello 入口網站，再試一次需要的 hello IT 系統管理員停用並重新啟用的使用者可能會同步處理設定及企業應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-159">Optionally, in hello portal, try having hello IT Admin disable and re-enable Users May Sync Settings and Enterprise App Data.</span></span> <span data-ttu-id="bdc9d-160">一旦重新啟用，重新啟動 hello 裝置，而且擁有 hello 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-160">Once re-enabled, restart hello device and have hello user login.</span></span> <span data-ttu-id="bdc9d-161">如果這樣做無法解決 hello 問題**AzureAdSettingsUrl**可能是空的不正確的裝置憑證 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-161">If this does not resolve hello issue, **AzureAdSettingsUrl** may be empty in hello case of a bad device certificate.</span></span> <span data-ttu-id="bdc9d-162">在此情況下，於已提升權限的命令提示字元視窗中執行 *dsregcmd.exe /leave*、重新開機，然後再試一次註冊，可能有助於解決此問題。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-162">In this case, running “*dsregcmd.exe /leave*” in an elevated command prompt window, rebooting, and trying registration again may help with this issue.</span></span>

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a><span data-ttu-id="bdc9d-163">企業狀態漫遊與 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="bdc9d-163">Enterprise State Roaming and Multi-Factor Authentication</span></span> 
<span data-ttu-id="bdc9d-164">某些狀況下，企業狀態漫遊可能會失敗 toosync 資料如果 Azure Multi-factor Authentication Server 設定。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-164">Under certain conditions, Enterprise State Roaming can fail toosync data if Azure Multi-Factor Authentication is configured.</span></span> <span data-ttu-id="bdc9d-165">如需這些徵狀的其他詳細資訊，請參閱 hello 支援文件[KB3193683](https://support.microsoft.com/kb/3193683)。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-165">For additional details on these symptoms, see hello support document [KB3193683](https://support.microsoft.com/kb/3193683).</span></span> 

<span data-ttu-id="bdc9d-166">**可能的問題**： 如果您的裝置 hello Azure Active Directory 入口網站上的設定的 toorequire Multi-factor Authentication，您可能會失敗 toosync 設定時登入 tooa Windows 10 裝置使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-166">**Potential issue**: If your device is configured toorequire Multi-Factor Authentication on hello Azure Active Directory portal, you may fail toosync settings while signing in tooa Windows 10 device using a password.</span></span> <span data-ttu-id="bdc9d-167">這種類型的 Multi-factor Authentication 設定是預定的 tooprotect Azure 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-167">This type of Multi-Factor Authentication configuration is intended tooprotect an Azure administrator account.</span></span> <span data-ttu-id="bdc9d-168">系統管理員使用者仍然可能無法 toosync 簽署 tootheir Windows 10 裝置與他們的 Microsoft Passport for Work 的 PIN，或藉由存取其他 Azure 服務，例如 Office 365 時完成多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-168">Admin users may still be able toosync by signing in tootheir Windows 10 devices with their Microsoft Passport for Work PIN or by completing Multi-Factor Authentication while accessing other Azure services like Office 365.</span></span>

<span data-ttu-id="bdc9d-169">**可能的問題**： 如果 hello 系統管理員設定 hello Active Directory 同盟服務多重要素驗證條件式存取原則和 hello hello 裝置上的存取權杖到期，同步處理可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-169">**Potential issue**: Sync can fail if hello admin configures hello Active Directory Federation Services Multi-Factor Authentication conditional access policy and hello access token on hello device expires.</span></span> <span data-ttu-id="bdc9d-170">請確認您登入和登出使用 hello Microsoft Passport for Work 的 PIN 或存取其他 Azure 服務，例如 Office 365 時完成多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-170">Ensure that you sign in and sign out using hello Microsoft Passport for Work PIN or complete Multi-Factor Authentication while accessing other Azure services like Office 365.</span></span>

###<a name="event-viewer"></a><span data-ttu-id="bdc9d-171">事件檢視器</span><span class="sxs-lookup"><span data-stu-id="bdc9d-171">Event Viewer</span></span>
<span data-ttu-id="bdc9d-172">對進階疑難排解，事件檢視器可以使用的 toofind 特定錯誤。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-172">For advanced troubleshooting, Event Viewer can be used toofind specific errors.</span></span> <span data-ttu-id="bdc9d-173">這些案例記載在 hello 表中。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-173">These are documented in hello table below.</span></span> <span data-ttu-id="bdc9d-174">您可以在事件檢視器找到 hello 事件 > 應用程式及服務記錄檔 > **Microsoft** > **Windows** > **SettingSync**和針對與同步處理身分識別相關的問題**Microsoft** > **Windows** > **Azure AD**。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-174">hello events can be found under Event Viewer > Applications and Services Logs > **Microsoft** > **Windows** > **SettingSync** and for identity-related issues with sync **Microsoft** > **Windows** > **Azure AD**.</span></span>


## <a name="known-issues"></a><span data-ttu-id="bdc9d-175">已知問題</span><span class="sxs-lookup"><span data-stu-id="bdc9d-175">Known issues</span></span>

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a><span data-ttu-id="bdc9d-176">同步處理在使用 MDM 軟體側載應用程式的裝置上無法運作</span><span class="sxs-lookup"><span data-stu-id="bdc9d-176">Sync does not work on devices that have apps side-loaded using MDM software</span></span>

<span data-ttu-id="bdc9d-177">執行會影響裝置 hello Windows 10 年度更新 (版本 1607)。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-177">Affects devices running hello Windows 10 Anniversary Update (Version 1607).</span></span> <span data-ttu-id="bdc9d-178">在 hello SettingSync Azure 記錄檔事件檢視器，經常會看到錯誤 80070259 hello 事件識別碼 6013。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-178">In Event Viewer under hello SettingSync-Azure logs, hello Event ID 6013 with error 80070259 is frequently seen.</span></span>

<span data-ttu-id="bdc9d-179">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="bdc9d-179">**Recommended action**</span></span>  
<span data-ttu-id="bdc9d-180">請確定 Windows 10 hello v1607 用戶端具有 hello 2016 年 8 月 23 日累計更新 ([KB3176934](https://support.microsoft.com/kb/3176934) OS 建置 14393.82)。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-180">Make sure hello Windows 10 v1607 client has hello August 23, 2016 Cumulative Update ([KB3176934](https://support.microsoft.com/kb/3176934) OS Build 14393.82).</span></span> 

---

### <a name="internet-explorer-favorites-do-not-sync"></a><span data-ttu-id="bdc9d-181">Internet Explorer 我的最愛不會同步</span><span class="sxs-lookup"><span data-stu-id="bdc9d-181">Internet Explorer Favorites do not sync</span></span>

<span data-ttu-id="bdc9d-182">執行會影響裝置 hello Windows 10 11 月更新 (版本 1511)。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-182">Affects devices running hello Windows 10 November Update (Version 1511).</span></span>

<span data-ttu-id="bdc9d-183">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="bdc9d-183">**Recommended action**</span></span>  
<span data-ttu-id="bdc9d-184">請確定 Windows 10 hello v1511 用戶端具有 hello 2016 年 7 月累計更新 ([KB3172985](https://support.microsoft.com/kb/3172985) OS 建置 10586.494)。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-184">Make sure hello Windows 10 v1511 client has hello July 2016 Cumulative Update ([KB3172985](https://support.microsoft.com/kb/3172985) OS Build 10586.494).</span></span>

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a><span data-ttu-id="bdc9d-185">佈景主題和使用「Windows 資訊保護」保護的資料不會同步處理</span><span class="sxs-lookup"><span data-stu-id="bdc9d-185">Theme is not syncing, as well as data protected with Windows Information Protection</span></span> 

<span data-ttu-id="bdc9d-186">tooprevent 資料外洩，與受保護的資料[Windows 資訊保護](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)將不會同步透過企業狀態漫遊的裝置使用 hello Windows 10 年度更新。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-186">tooprevent data leakage, data that is protected with [Windows Information Protection](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) will not sync through Enterprise State Roaming for devices using hello Windows 10 Anniversary Update.</span></span>



<span data-ttu-id="bdc9d-187">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="bdc9d-187">**Recommended action**</span></span>  
<span data-ttu-id="bdc9d-188">無。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-188">None.</span></span> <span data-ttu-id="bdc9d-189">未來的更新 tooWindows 可解決此問題。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-189">Future updates tooWindows may resolve this issue.</span></span>

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a><span data-ttu-id="bdc9d-190">已加入網域的裝置上不會同步處理日期、時間及地區設定</span><span class="sxs-lookup"><span data-stu-id="bdc9d-190">Date, Time, and Region settings do not sync on domain-joined device</span></span> 
  
<span data-ttu-id="bdc9d-191">加入網域的裝置不會經歷 hello 日期、 時間和地區設定的同步處理： 自動的時間。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-191">Devices that are domain-joined will not experience sync for hello setting Date, Time, and Region: automatic time.</span></span> <span data-ttu-id="bdc9d-192">使用自動時間可能會覆寫 hello 其他日期、 時間和地區設定和導致不 toosync 這些設定。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-192">Using automatic time may override hello other Date, Time, and Region settings and cause those settings not toosync.</span></span> 

<span data-ttu-id="bdc9d-193">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="bdc9d-193">**Recommended action**</span></span>  
<span data-ttu-id="bdc9d-194">無。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-194">None.</span></span> 

---

### <a name="uac-prompts-when-syncing-passwords"></a><span data-ttu-id="bdc9d-195">同步密碼時出現 UAC 提示</span><span class="sxs-lookup"><span data-stu-id="bdc9d-195">UAC Prompts when syncing passwords</span></span>

<span data-ttu-id="bdc9d-196">會影響裝置執行 hello Windows 10 11 月更新 (版本 1511) 與無線 NIC 設定 toosync 密碼。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-196">Affects devices running hello Windows 10 November Update (Version 1511) with a wireless NIC that is configured toosync passwords.</span></span>

<span data-ttu-id="bdc9d-197">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="bdc9d-197">**Recommended action**</span></span>  
<span data-ttu-id="bdc9d-198">請確定 Windows 10 hello v1511 用戶端具有 hello 累計更新 ([KB3140743](https://support.microsoft.com/kb/3140743) OS 建置 10586.494)。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-198">Make sure hello Windows 10 v1511 client has hello Cumulative Update ([KB3140743](https://support.microsoft.com/kb/3140743) OS Build 10586.494).</span></span>

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a><span data-ttu-id="bdc9d-199">同步處理不會在使用智慧卡登入的裝置上運作</span><span class="sxs-lookup"><span data-stu-id="bdc9d-199">Sync does not work on devices that use smart card for login</span></span>
<span data-ttu-id="bdc9d-200">如果您嘗試 toosign tooyour Windows 裝置使用智慧卡或虛擬智慧卡中的，設定同步處理將會停止運作。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-200">If you attempt toosign in tooyour Windows device using a smart card or virtual smart card, settings sync will stop working.</span></span>     

<span data-ttu-id="bdc9d-201">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="bdc9d-201">**Recommended action**</span></span>  
<span data-ttu-id="bdc9d-202">無。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-202">None.</span></span> <span data-ttu-id="bdc9d-203">未來的更新 tooWindows 可解決此問題。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-203">Future updates tooWindows may resolve this issue.</span></span>

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a><span data-ttu-id="bdc9d-204">已加入網域的裝置不會在離開公司網路後同步處理</span><span class="sxs-lookup"><span data-stu-id="bdc9d-204">Domain-joined device is not syncing after leaving corporate network</span></span>     
<span data-ttu-id="bdc9d-205">已加入網域的裝置註冊的 tooAzure AD 如果 hello 裝置是很長的時間，且位於異地，因此無法完成網域驗證，可能會發生同步處理失敗。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-205">Domain-joined devices registered tooAzure AD may experience sync failure if hello device is off-site for extended periods of time, and domain authentication can't complete.</span></span>

<span data-ttu-id="bdc9d-206">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="bdc9d-206">**Recommended action**</span></span>  
<span data-ttu-id="bdc9d-207">Hello 裝置 tooa 公司網路連線，以便可以繼續同步處理。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-207">Connect hello device tooa corporate network so that sync can resume.</span></span>

---

 ### <a name="azure-ad-joined-device-is-not-syncing-and-hello-user-has-a-mixed-case-user-principal-name"></a><span data-ttu-id="bdc9d-208">Azure AD 聯結裝置無法同步處理而且 hello 使用者混合大小寫的使用者主體名稱。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-208">Azure AD Joined device is not syncing and hello user has a mixed case User Principal Name.</span></span>
 <span data-ttu-id="bdc9d-209">Hello 使用者具有混合大小寫字母的 UPN （例如使用者名稱而不是使用者名稱） 而 hello 使用者是已經升級，從 Windows 10 組建 10586 too14393 加入 Azure AD 之裝置上，如果 hello 使用者的裝置可能會失敗 toosync。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-209">If hello user has a mixed case UPN (e.g. UserName instead of username) and hello user is on an Azure AD Joined device which has upgraded from Windows 10 Build 10586 too14393, hello user's device may fail toosync.</span></span> 

<span data-ttu-id="bdc9d-210">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="bdc9d-210">**Recommended action**</span></span>  
<span data-ttu-id="bdc9d-211">將需要 toounjoin hello 使用者，並將它重新加入 hello 裝置 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-211">hello user will need toounjoin and rejoin hello device toohello cloud.</span></span> <span data-ttu-id="bdc9d-212">toodo hello 本機系統管理員使用者身分，登入和移過退出 hello 裝置**設定** > **系統** > **有關**並選取"管理者或中斷與工作或學校 」。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-212">toodo this, login as hello Local Administrator user and unjoin hello device by going too**Settings** > **System** > **About** and select "Manage or disconnect from work or school".</span></span> <span data-ttu-id="bdc9d-213">清除 hello 以下檔案，然後按一下 Azure AD Join hello 裝置一次在**設定** > **系統** > **有關**，然後選取 連線tooWork 或學校 」。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-213">Clean up hello files below, and then Azure AD Join hello device again in **Settings** > **System** > **About** and selecting "Connect tooWork or School".</span></span> <span data-ttu-id="bdc9d-214">繼續 toojoin hello 裝置 tooAzure Active Directory 和完整 hello 流程。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-214">Continue toojoin hello device tooAzure Active Directory and complete hello flow.</span></span>

<span data-ttu-id="bdc9d-215">在 hello 清除步驟中，清除 hello 下列檔案：</span><span class="sxs-lookup"><span data-stu-id="bdc9d-215">In hello cleanup step, cleanup hello following files:</span></span>
- <span data-ttu-id="bdc9d-216">`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\` 中的 Settings.dat</span><span class="sxs-lookup"><span data-stu-id="bdc9d-216">Settings.dat in `C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\`</span></span>
- <span data-ttu-id="bdc9d-217">所有 hello hello 資料夾下的檔案`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`</span><span class="sxs-lookup"><span data-stu-id="bdc9d-217">All hello files under hello folder `C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`</span></span>

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a><span data-ttu-id="bdc9d-218">事件識別碼 6065：80070533 此使用者無法登入，因為此帳戶目前已停用</span><span class="sxs-lookup"><span data-stu-id="bdc9d-218">Event ID 6065: 80070533 This user can’t sign in because this account is currently disabled</span></span>  
<span data-ttu-id="bdc9d-219">在 hello SettingSync/偵錯記錄檔事件檢視器，可以 hello 使用者的認證已過期時會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-219">In Event Viewer under hello SettingSync/Debug logs, this error can be seen when hello user's credentials have expired.</span></span> <span data-ttu-id="bdc9d-220">此外，它可能發生在 hello 租用戶自動沒有 AzureRMS 佈建。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-220">In addition, it can occur when hello tenant did not automatically have AzureRMS provisioned.</span></span> 

<span data-ttu-id="bdc9d-221">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="bdc9d-221">**Recommended action**</span></span>  
<span data-ttu-id="bdc9d-222">在 hello 第一個案例中，有 hello 使用者更新其認證和登入 toohello 裝置 hello 新的認證。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-222">In hello first case, have hello user update their credentials and login toohello device with hello new credentials.</span></span> <span data-ttu-id="bdc9d-223">中所列的 hello 步驟繼續 toosolve hello AzureRMS 問題[KB3193791](https://support.microsoft.com/kb/3193791)。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-223">toosolve hello AzureRMS issue, proceed with hello steps listed in [KB3193791](https://support.microsoft.com/kb/3193791).</span></span> 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a><span data-ttu-id="bdc9d-224">事件識別碼 1098：錯誤：0xCAA5001C 權杖代理人操作失敗</span><span class="sxs-lookup"><span data-stu-id="bdc9d-224">Event ID 1098: Error: 0xCAA5001C Token broker operation failed</span></span>  
<span data-ttu-id="bdc9d-225">在 hello AAD/操作記錄檔事件檢視器，可能會出現此錯誤與事件 1104年: AAD 雲端 AP 外掛程式呼叫 Get 語彙基元傳回錯誤： 0xC000005F。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-225">In Event Viewer under hello AAD/Operational logs, this error may be seen with Event 1104: AAD Cloud AP plugin call Get token returned error: 0xC000005F.</span></span> <span data-ttu-id="bdc9d-226">如果缺少權限或擁有權屬性，就會發生這個問題。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-226">This issue occurs if there are missing permissions or ownership attributes.</span></span>    

<span data-ttu-id="bdc9d-227">**建議的動作**</span><span class="sxs-lookup"><span data-stu-id="bdc9d-227">**Recommended action**</span></span>  
<span data-ttu-id="bdc9d-228">繼續進行列出的 hello 步驟[KB3196528](https://support.microsoft.com/kb/3196528)。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-228">Proceed with hello steps listed [KB3196528](https://support.microsoft.com/kb/3196528).</span></span>  



## <a name="next-steps"></a><span data-ttu-id="bdc9d-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bdc9d-229">Next steps</span></span>

- <span data-ttu-id="bdc9d-230">使用 hello[使用者之聲論壇](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming)tooprovide 意見反應，讓的建議方式 tooimprove 企業狀態漫遊。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-230">Use hello [User Voice forum](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming) tooprovide feedback and make suggestions on how tooimprove Enterprise State Roaming.</span></span>

- <span data-ttu-id="bdc9d-231">如需詳細資訊，請參閱 hello[企業狀態漫遊概觀](active-directory-windows-enterprise-state-roaming-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bdc9d-231">For more information, see hello [Enterprise State Roaming overview](active-directory-windows-enterprise-state-roaming-overview.md).</span></span> 

## <a name="related-topics"></a><span data-ttu-id="bdc9d-232">相關主題</span><span class="sxs-lookup"><span data-stu-id="bdc9d-232">Related topics</span></span>
* [<span data-ttu-id="bdc9d-233">企業狀態漫遊概觀</span><span class="sxs-lookup"><span data-stu-id="bdc9d-233">Enterprise state roaming overview</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)
* [<span data-ttu-id="bdc9d-234">在 Azure Active Directory 中啟用企業狀態漫遊</span><span class="sxs-lookup"><span data-stu-id="bdc9d-234">Enable enterprise state roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md)
* [<span data-ttu-id="bdc9d-235">設定和資料漫遊常見問題集</span><span class="sxs-lookup"><span data-stu-id="bdc9d-235">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md)
* [<span data-ttu-id="bdc9d-236">設定同步處理的群組原則和 MDM 設定</span><span class="sxs-lookup"><span data-stu-id="bdc9d-236">Group policy and MDM settings for settings sync</span></span>](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [<span data-ttu-id="bdc9d-237">Windows 10 漫遊設定參考</span><span class="sxs-lookup"><span data-stu-id="bdc9d-237">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
