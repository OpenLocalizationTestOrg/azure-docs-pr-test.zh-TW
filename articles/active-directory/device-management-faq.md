---
title: "aaaAzure Active Directory 裝置管理常見問題集 |Microsoft 文件"
description: "Azure Active Directory 裝置管理常見問題集。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 000eb6a930187e13cb24cf628793afd06813be23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-device-management-faq"></a><span data-ttu-id="a091e-103">Azure Active Directory 裝置管理常見問題集</span><span class="sxs-lookup"><span data-stu-id="a091e-103">Azure Active Directory device management FAQ</span></span>

<span data-ttu-id="a091e-104">**問： 我最近註冊 hello 裝置。為什麼在 我的使用者資訊 hello Azure 入口網站中看不到 hello 裝置？**</span><span class="sxs-lookup"><span data-stu-id="a091e-104">**Q: I registered hello device recently. Why can’t I see hello device under my user info in hello Azure portal?**</span></span>

<span data-ttu-id="a091e-105">**答：**與自動裝置註冊加入網域的 Windows 10 裝置不會出現在 hello 使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="a091e-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under hello USER info.</span></span>
<span data-ttu-id="a091e-106">您需要 toouse PowerShell toosee 所有裝置。</span><span class="sxs-lookup"><span data-stu-id="a091e-106">You need toouse PowerShell toosee all devices.</span></span> 

<span data-ttu-id="a091e-107">只有 hello 下列裝置列在 hello 使用者資訊：</span><span class="sxs-lookup"><span data-stu-id="a091e-107">Only hello following devices are listed under hello USER info:</span></span>

- <span data-ttu-id="a091e-108">所有未加入企業的個人裝置</span><span class="sxs-lookup"><span data-stu-id="a091e-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="a091e-109">所有非 Windows 10/Windows Server 2016 裝置</span><span class="sxs-lookup"><span data-stu-id="a091e-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="a091e-110">所有非 Windows 裝置</span><span class="sxs-lookup"><span data-stu-id="a091e-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="a091e-111">**問： 為什麼不看到 hello Azure 入口網站中註冊 Azure Active Directory 中的所有 hello 裝置？**</span><span class="sxs-lookup"><span data-stu-id="a091e-111">**Q: Why can I not see all hello devices registered in Azure Active Directory in hello Azure portal?**</span></span> 

<span data-ttu-id="a091e-112">**答：**目前沒有任何方式 toosee 所有已註冊的裝置 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="a091e-112">**A:** Currently, there is no way toosee all registered devices in hello Azure portal.</span></span> <span data-ttu-id="a091e-113">您可以使用 Azure PowerShell toofind 所有裝置。</span><span class="sxs-lookup"><span data-stu-id="a091e-113">You can use Azure PowerShell toofind all devices.</span></span> <span data-ttu-id="a091e-114">如需詳細資訊，請參閱 hello [Get MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a091e-114">For more details, see hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="a091e-115">**問： 如何知道哪些 hello 裝置登錄狀態的 hello 用戶端是否？**</span><span class="sxs-lookup"><span data-stu-id="a091e-115">**Q: How do I know what hello device registration state of hello client is?**</span></span>

<span data-ttu-id="a091e-116">**答：** hello 裝置登錄狀態而定：</span><span class="sxs-lookup"><span data-stu-id="a091e-116">**A:** hello device registration state depends on:</span></span>

- <span data-ttu-id="a091e-117">哪些 hello 裝置</span><span class="sxs-lookup"><span data-stu-id="a091e-117">What hello device is</span></span>
- <span data-ttu-id="a091e-118">裝置的註冊方式</span><span class="sxs-lookup"><span data-stu-id="a091e-118">How it was registered</span></span> 
- <span data-ttu-id="a091e-119">Tooit 相關任何詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a091e-119">Any details related tooit.</span></span> 
 

---

<span data-ttu-id="a091e-120">**問： 為何我已刪除的裝置在 hello Azure 入口網站或使用 Windows PowerShell 仍然列為註冊嗎？**</span><span class="sxs-lookup"><span data-stu-id="a091e-120">**Q: Why is a device I have deleted in hello Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="a091e-121">**答：**原先的設計就是如此。</span><span class="sxs-lookup"><span data-stu-id="a091e-121">**A:** This is by design.</span></span> <span data-ttu-id="a091e-122">hello 裝置不會存取 tooresources hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="a091e-122">hello device will not have access tooresources in hello cloud.</span></span> <span data-ttu-id="a091e-123">如果您想 tooremove hello 裝置並重新登錄，手動動作必須 toobe 採取 hello 裝置上。</span><span class="sxs-lookup"><span data-stu-id="a091e-123">If you want tooremove hello device and register again, a manual action must be toobe taken on hello device.</span></span> 

<span data-ttu-id="a091e-124">針對已加入內部部署 AD 網域的 Windows 10 與 Windows Server 2016：</span><span class="sxs-lookup"><span data-stu-id="a091e-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="a091e-125">系統管理員身分開啟命令提示字元中 hello。</span><span class="sxs-lookup"><span data-stu-id="a091e-125">Open hello command prompt as an administrator.</span></span>

2.  <span data-ttu-id="a091e-126">輸入 `dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="a091e-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="a091e-127">登出再登入 tootrigger hello 排定的工作，重新登錄裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="a091e-127">Sign out and sign in tootrigger hello scheduled task that registers hello device again.</span></span> 

<span data-ttu-id="a091e-128">針對其他已加入內部部署 AD 網域的 Windows 平台：</span><span class="sxs-lookup"><span data-stu-id="a091e-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="a091e-129">系統管理員身分開啟命令提示字元中 hello。</span><span class="sxs-lookup"><span data-stu-id="a091e-129">Open hello command prompt as an administrator.</span></span>
2.  <span data-ttu-id="a091e-130">輸入 `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`。</span><span class="sxs-lookup"><span data-stu-id="a091e-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="a091e-131">輸入 `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`。</span><span class="sxs-lookup"><span data-stu-id="a091e-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="a091e-132">**問：為什麼我在 Azure 入口網站中看到重複的裝置項目？**</span><span class="sxs-lookup"><span data-stu-id="a091e-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="a091e-133">**答：**</span><span class="sxs-lookup"><span data-stu-id="a091e-133">**A:**</span></span>

-   <span data-ttu-id="a091e-134">針對 Windows 10 和 Windows Server 2016 中，會重複的嘗試 toounjoin 並重新聯結 hello 相同的裝置，可能會有重複的項目。</span><span class="sxs-lookup"><span data-stu-id="a091e-134">For Windows 10 and Windows Server 2016, if they are repeated attempts toounjoin and re-join hello same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="a091e-135">如果您已經使用新增工作或學校帳戶，每個 windows 使用者使用新增工作或學校帳戶的人員會建立新的裝置記錄 hello 與同一個裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="a091e-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with hello same device name.</span></span>

-   <span data-ttu-id="a091e-136">其他 Windows 的平台在內部部署 AD 加入網域使用自動註冊將會建立新的裝置記錄 hello 與相同的網域使用者之登入 hello 裝置的裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="a091e-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with hello same device name for each domain user who logs into hello device.</span></span> 

-   <span data-ttu-id="a091e-137">一經抹除，AADJ 機器重新安裝並重新加入 hello 與相同名稱，會顯示以 hello 的另一筆記錄為相同的裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="a091e-137">An AADJ machine that has been wiped, re-installed and re-joined with hello same name, will show up as another record with hello same device name.</span></span>

---

<span data-ttu-id="a091e-138">**問： 為什麼使用者仍然可以存取資源從我有 hello Azure 入口網站中停用的裝置？**</span><span class="sxs-lookup"><span data-stu-id="a091e-138">**Q: Why can a user still access resources from a device I have disabled in hello Azure portal?**</span></span>

<span data-ttu-id="a091e-139">**答：**就可以在套用 revoke toobe tooan 小時。</span><span class="sxs-lookup"><span data-stu-id="a091e-139">**A:** It can take up tooan hour for a revoke toobe applied.</span></span>

>[!Note] 
><span data-ttu-id="a091e-140">對於遺失裝置，我們建議抹除 hello 裝置 tooensure 使用者無法存取 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="a091e-140">For lost devices, we recommend wiping hello device tooensure that users cannot access hello device.</span></span> <span data-ttu-id="a091e-141">如需更多詳細資料，請參閱[註冊裝置以在 Intune 中管理](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)。</span><span class="sxs-lookup"><span data-stu-id="a091e-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="a091e-142">**問：為什麼我的使用者會看到「您無法從這裡前往該處」？**</span><span class="sxs-lookup"><span data-stu-id="a091e-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="a091e-143">**答：**如果您已設定特定的條件式存取規則 toorequire 特定裝置狀態，且 hello 裝置不符合 hello 準則，使用者會封鎖，並看到此訊息。</span><span class="sxs-lookup"><span data-stu-id="a091e-143">**A:** If you have configured certain conditional access rules toorequire a specific device state and hello device does not meet hello criteria, users are blocked and see this message.</span></span> <span data-ttu-id="a091e-144">請評估 hello 規則，並確認該 hello 裝置是無法 toomeet hello 準則 tooavoid 這則訊息。</span><span class="sxs-lookup"><span data-stu-id="a091e-144">Please evaluate hello rules and ensure that hello device is able toomeet hello criteria tooavoid this message.</span></span>

---


<span data-ttu-id="a091e-145">**問： 我看到 hello 下 hello hello Azure 入口網站中的使用者資訊的裝置記錄，並且可以看到 hello 狀態，hello 用戶端上註冊。我是否已針對使用條件式存取進行正確設定？**</span><span class="sxs-lookup"><span data-stu-id="a091e-145">**Q: I see hello device record under hello USER info in hello Azure portal and can see hello state as registered on hello client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="a091e-146">**答：** hello 裝置記錄 (deviceID) 和 hello Azure 入口網站上的狀態必須符合 hello 用戶端，並符合條件式存取的任何評估準則。</span><span class="sxs-lookup"><span data-stu-id="a091e-146">**A:** hello device record (deviceID) and state on hello Azure portal must match hello client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="a091e-147">如需更多詳細資料，請參閱[開始使用 Azure Active Directory 裝置註冊](active-directory-device-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="a091e-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="a091e-148">**問： 為什麼取得 「 使用者名稱或密碼不正確 」 訊息裝置我剛加入 tooAzure AD？**</span><span class="sxs-lookup"><span data-stu-id="a091e-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined tooAzure AD?**</span></span>

<span data-ttu-id="a091e-149">**答：**此情況的常見原因如下：</span><span class="sxs-lookup"><span data-stu-id="a091e-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="a091e-150">您的使用者認證已經無效。</span><span class="sxs-lookup"><span data-stu-id="a091e-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="a091e-151">您的電腦位於與 Azure Active Directory 無法 toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="a091e-151">Your computer is unable toocommunicate with Azure Active Directory.</span></span> <span data-ttu-id="a091e-152">請檢查是否有任何網路連線問題。</span><span class="sxs-lookup"><span data-stu-id="a091e-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="a091e-153">不符合 hello Azure AD Join 的必要元件。</span><span class="sxs-lookup"><span data-stu-id="a091e-153">hello Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="a091e-154">請確定您已遵循的步驟 hello[擴充雲端功能 tooWindows 10 裝置透過 Azure Active Directory Join](active-directory-azureadjoin-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a091e-154">Please ensure that you have followed hello steps for [Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="a091e-155">同盟登入需要您的同盟伺服器 toosupport Ws-trust 作用中的端點。</span><span class="sxs-lookup"><span data-stu-id="a091e-155">Federated logins requires your federation server toosupport a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="a091e-156">**問： 為什麼看 hello"...糟糕，發生錯誤 ！ 」 對話方塊時請勿加入我的電腦？**</span><span class="sxs-lookup"><span data-stu-id="a091e-156">**Q: Why do I see hello “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="a091e-157">**答：**這是使用 Intune 來設定 Azure Active Directory 註冊的結果。</span><span class="sxs-lookup"><span data-stu-id="a091e-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="a091e-158">如需更多詳細資料，請參閱[設定 Windows 裝置管理](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment)。</span><span class="sxs-lookup"><span data-stu-id="a091e-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="a091e-159">**問： 為什麼我的電腦失敗雖然未出現任何錯誤資訊的嘗試 toojoin 嗎？**</span><span class="sxs-lookup"><span data-stu-id="a091e-159">**Q: Why did my attempt toojoin a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="a091e-160">**答：**可能的原因是該的 hello 使用者已登入 toohello 裝置使用 hello 內建的 administrator 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a091e-160">**A:** A likely cause is that hello user is logged in toohello device using hello built-in administrator account.</span></span> <span data-ttu-id="a091e-161">請使用 Azure Active Directory Join toocomplete hello 安裝程式之前，建立不同的本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="a091e-161">Please create a different local account before using Azure Active Directory Join toocomplete hello setup.</span></span> 

---

<span data-ttu-id="a091e-162">**問： 哪裡可以找到指示 hello 安裝程式的自動裝置註冊？**</span><span class="sxs-lookup"><span data-stu-id="a091e-162">**Q: Where can I find instructions for hello setup of automatic device registration?**</span></span>

<span data-ttu-id="a091e-163">**答：**詳細指示，請參閱[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="a091e-163">**A:** For detailed instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="a091e-164">**問： 哪裡可以找到疑難排解 hello 自動裝置註冊相關資訊？**</span><span class="sxs-lookup"><span data-stu-id="a091e-164">**Q: Where can I find troubleshooting information about hello automatic device registration?**</span></span>

<span data-ttu-id="a091e-165">**答：**如需疑難排解資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="a091e-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="a091e-166">疑難排解自動登錄的網域加入電腦 tooAzure AD – Windows 10 和 Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a091e-166">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="a091e-167">疑難排解自動登錄的網域加入 Windows 下層用戶端電腦 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="a091e-167">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

