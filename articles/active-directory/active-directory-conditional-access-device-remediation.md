---
title: "aaaYou 無法取得那里以下 hello Azure 入口網站，從 Windows 裝置 |Microsoft 文件"
description: "了解，您不能那里從這裡來自的 get 和什麼您可以檢查 tooavoid 執行此對話方塊。"
services: active-directory
keywords: "裝置型條件式存取、裝置註冊、啟用裝置註冊、裝置註冊和 MDM"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="c2e2f-104">您無法在 Windows 裝置上從這裡前往該處</span><span class="sxs-lookup"><span data-stu-id="c2e2f-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="c2e2f-105">例如，在嘗試存取貴組織的 SharePoint Online 內部網路期間，您可能會碰到一個頁面指出「您無法從這裡前往該處」。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="c2e2f-106">您會看到此頁面上，因為您的系統管理員已設定讓存取 tooyour 組織的資源，在某些情況下的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access tooyour organization's resources under certain conditions.</span></span> <span data-ttu-id="c2e2f-107">雖然這可能需要 toocontact 技術服務人員或您的系統管理員 tooget 解決這個問題，有幾件事，您可以試用您自己，第一次。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-107">While it might be necessary toocontact helpdesk or your administrator tooget this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="c2e2f-108">如果您使用**Windows**裝置，您應該檢查下列 hello:</span><span class="sxs-lookup"><span data-stu-id="c2e2f-108">If you are using a **Windows** device, you should check hello following:</span></span>

- <span data-ttu-id="c2e2f-109">您使用支援的瀏覽器？</span><span class="sxs-lookup"><span data-stu-id="c2e2f-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="c2e2f-110">您在裝置上執行支援的 Windows 版本？</span><span class="sxs-lookup"><span data-stu-id="c2e2f-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="c2e2f-111">您的裝置是否符合規範？</span><span class="sxs-lookup"><span data-stu-id="c2e2f-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="c2e2f-112">支援的瀏覽器</span><span class="sxs-lookup"><span data-stu-id="c2e2f-112">Supported browser</span></span>

<span data-ttu-id="c2e2f-113">如果您的系統管理員已設定條件式存取原則，您只可以使用支援的瀏覽器來存取貴組織的資源。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="c2e2f-114">在 Windows 裝置上，只支援 **Internet Explorer** 和 **Edge**。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="c2e2f-115">您可以輕鬆地識別是否您無法存取的資源，因為 tooan 不支援的瀏覽器查看 hello hello 錯誤頁面的詳細資料 區段：</span><span class="sxs-lookup"><span data-stu-id="c2e2f-115">You can easily identify whether you can't access a resource due tooan unsupported browser by looking at hello details section of hello error page:</span></span>

<span data-ttu-id="c2e2f-116">![不受支援的瀏覽器會收到「您無法從這裡前往該處」訊息](./media/active-directory-conditional-access-device-remediation/02.png "例")</span><span class="sxs-lookup"><span data-stu-id="c2e2f-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="c2e2f-117">hello 只有補救是 toouse hello 應用程式對您的裝置平台所支援的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-117">hello only remediation is toouse a browser that hello application supports for your device platform.</span></span> <span data-ttu-id="c2e2f-118">如需支援的瀏覽器完整清單，請參閱[支援的瀏覽器](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies)。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="c2e2f-119">支援的 Windows 版本</span><span class="sxs-lookup"><span data-stu-id="c2e2f-119">Supported versions of Windows</span></span>

<span data-ttu-id="c2e2f-120">hello 下列條件必須為 true hello Windows 作業系統，您的裝置上的相關：</span><span class="sxs-lookup"><span data-stu-id="c2e2f-120">hello following must be true about hello Windows operating system on your device:</span></span> 

- <span data-ttu-id="c2e2f-121">如果您 Windows 桌面作業系統上執行您的裝置，它會需要 toobe Windows 7 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-121">If you are running a Windows desktop operating system on your device, it needs toobe Windows 7 or later.</span></span>
- <span data-ttu-id="c2e2f-122">如果您在裝置上執行 Windows server 作業系統，它需要 toobe Windows Server 2008 R2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-122">If you are running a Windows server operating system on your device, it needs toobe Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="c2e2f-123">符合規範的裝置</span><span class="sxs-lookup"><span data-stu-id="c2e2f-123">Compliant device</span></span>

<span data-ttu-id="c2e2f-124">您的系統管理員可能已經設定的條件式存取原則允許存取 tooyour 組織的資源，只會從相容的裝置。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-124">Your administrator might have configured a conditional access policy that allows access tooyour organization's resources only from compliant devices.</span></span> <span data-ttu-id="c2e2f-125">符合標準，您的裝置必須是其中一個聯結的 tooyour toobe 在內部部署 Active Directory 或是已加入 tooyour Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-125">toobe compliant, your device must be either joined tooyour on-premises Active Directory or joined tooyour Azure Active Directory.</span></span>

<span data-ttu-id="c2e2f-126">您可以輕鬆地識別您無法存取到期，藉由查看 hello 詳細資料區段的 hello 錯誤網頁不相容的 tooa 裝置資源是否：</span><span class="sxs-lookup"><span data-stu-id="c2e2f-126">You can easily identify whether you can't access a resource due tooa device that is not compliant by looking at hello details section of hello error page:</span></span>
 
<span data-ttu-id="c2e2f-127">![未註冊的裝置會收到「您無法從這裡前往該處」訊息](./media/active-directory-conditional-access-device-remediation/01.png "案例")</span><span class="sxs-lookup"><span data-stu-id="c2e2f-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="c2e2f-128">是聯結的裝置 tooan 內部部署 Active Directory？</span><span class="sxs-lookup"><span data-stu-id="c2e2f-128">Is your device joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="c2e2f-129">**如果您的裝置加入 tooan 內部部署 Active Directory 組織中：**</span><span class="sxs-lookup"><span data-stu-id="c2e2f-129">**If your device is joined tooan on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="c2e2f-130">請確定您使用工作帳戶 （您的 Active Directory 帳戶） 登入 tooWindows。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-130">Make sure that you sign in tooWindows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="c2e2f-131">透過虛擬私人網路 (VPN) 或 DirectAccess tooyour 公司網路連線。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-131">Connect tooyour corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="c2e2f-132">您連接之後，請按 hello Windows 標誌鍵 + hello L 金鑰 toolock Windows 工作階段。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-132">After you are connected, press hello Windows logo key + hello L key toolock your Windows session.</span></span>
4. <span data-ttu-id="c2e2f-133">輸入您的工作帳戶認證，以將 Windows 工作階段解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="c2e2f-134">等候數分鐘，然後再試 tooaccess hello 應用程式或服務。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-134">Wait for a minute, and then try again tooaccess hello application or service.</span></span>
6. <span data-ttu-id="c2e2f-135">如果您看到 hello 相同頁面上，按一下 hello**詳細**連結，然後再連絡管理員，並 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-135">If you see hello same page, click hello **More details** link, and then contact your administrator with hello details.</span></span>


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="c2e2f-136">是您的裝置未加入 tooan 內部部署 Active Directory？</span><span class="sxs-lookup"><span data-stu-id="c2e2f-136">Is your device not joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="c2e2f-137">如果您的裝置未加入 tooan 在內部部署 Active Directory 及執行 Windows 10 時，有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="c2e2f-137">If your device is not joined tooan on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="c2e2f-138">執行 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="c2e2f-138">Run Azure AD Join</span></span>
* <span data-ttu-id="c2e2f-139">加入您的工作或學校帳戶 tooWindows</span><span class="sxs-lookup"><span data-stu-id="c2e2f-139">Add your work or school account tooWindows</span></span>

<span data-ttu-id="c2e2f-140">如需這些選項有何差異的相關資訊，請參閱[在您的工作場所中使用 Windows 10 裝置](active-directory-azureadjoin-windows10-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="c2e2f-141">如果您的裝置：</span><span class="sxs-lookup"><span data-stu-id="c2e2f-141">If your device:</span></span>

- <span data-ttu-id="c2e2f-142">所屬 tooyour 組織，您應該執行 Azure AD Join。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-142">Belongs tooyour organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="c2e2f-143">個人裝置或 Windows phone，您應該加入您的工作或學校帳戶 tooWindows</span><span class="sxs-lookup"><span data-stu-id="c2e2f-143">Is a personal device or a Windows phone, you should add your work or school account tooWindows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="c2e2f-144">Windows 10 上的 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="c2e2f-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="c2e2f-145">hello 步驟 toojoin 您裝置 tooAzure AD 是繫結 hello 您正在執行的 Windows 10 版本。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-145">hello steps toojoin your device tooAzure AD are tied hello version of Windows 10 you are running on it.</span></span> <span data-ttu-id="c2e2f-146">toodetermine hello 版本的 Windows 10 作業系統，執行 hello **winver**命令：</span><span class="sxs-lookup"><span data-stu-id="c2e2f-146">toodetermine hello version of your Windows 10 operating system, run hello **winver** command:</span></span> 

![Windows 版本](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="c2e2f-148">**Windows 10 年度更新 (版本 1607)：**</span><span class="sxs-lookup"><span data-stu-id="c2e2f-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="c2e2f-149">開啟 hello**設定**應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-149">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c2e2f-150">按一下 [帳戶] > [存取工作或學校]。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="c2e2f-151">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-151">Click **Connect**.</span></span>
4. <span data-ttu-id="c2e2f-152">按一下**加入此裝置 tooAzure AD**。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-152">Click **Join this device tooAzure AD**.</span></span>
5. <span data-ttu-id="c2e2f-153">完成驗證 tooyour 組織時，如果出現提示，然後依照顯示 hello 步驟提供多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-153">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
6. <span data-ttu-id="c2e2f-154">登出，然後使用您的工作帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="c2e2f-155">再試一次 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-155">Try again tooaccess hello application.</span></span>

<span data-ttu-id="c2e2f-156">**Windows 10 2015 年 11 月更新 (版本 1511)：**</span><span class="sxs-lookup"><span data-stu-id="c2e2f-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="c2e2f-157">開啟 hello**設定**應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-157">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c2e2f-158">按一下 [系統] > [關於]。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="c2e2f-159">按一下 [加入 Azure AD] 。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="c2e2f-160">完成驗證 tooyour 組織時，如果出現提示，然後依照顯示 hello 步驟提供多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-160">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c2e2f-161">登出，然後使用您的工作帳戶 (Azure AD 帳戶) 登入。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="c2e2f-162">再試一次 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-162">Try again tooaccess hello application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="c2e2f-163">在 Windows 8.1 上的 Workplace Join</span><span class="sxs-lookup"><span data-stu-id="c2e2f-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="c2e2f-164">如果您的裝置未加入網域和執行 Windows 8.1，toodo 工作地點加入，且在 Microsoft Intune 中註冊，下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="c2e2f-164">If your device is not domain-joined and runs Windows 8.1, toodo a Workplace Join and enroll in Microsoft Intune, do hello following steps:</span></span>

1. <span data-ttu-id="c2e2f-165">開啟 [電腦設定] 。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="c2e2f-166">按一下 [網路] > [工作場所]。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="c2e2f-167">按一下 [ **加入**]。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-167">Click **Join**.</span></span>
4. <span data-ttu-id="c2e2f-168">完成驗證 tooyour 組織時，如果出現提示，然後依照顯示 hello 步驟提供多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-168">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c2e2f-169">按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="c2e2f-170">再試一次 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-170">Try again tooaccess hello application.</span></span>



#### <a name="add-your-work-or-school-account-toowindows"></a><span data-ttu-id="c2e2f-171">加入您的工作或學校帳戶 tooWindows</span><span class="sxs-lookup"><span data-stu-id="c2e2f-171">Add your work or school account tooWindows</span></span> 


<span data-ttu-id="c2e2f-172">**Windows 10 年度更新 (版本 1607)：**</span><span class="sxs-lookup"><span data-stu-id="c2e2f-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="c2e2f-173">開啟 hello**設定**應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-173">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c2e2f-174">按一下 [帳戶] > [存取工作或學校]。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="c2e2f-175">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-175">Click **Connect**.</span></span>
4. <span data-ttu-id="c2e2f-176">完成驗證 tooyour 組織時，如果出現提示，然後依照顯示 hello 步驟提供多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-176">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c2e2f-177">再試一次 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-177">Try again tooaccess hello application.</span></span>


<span data-ttu-id="c2e2f-178">**Windows 10 2015 年 11 月更新 (版本 1511)：**</span><span class="sxs-lookup"><span data-stu-id="c2e2f-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="c2e2f-179">開啟 hello**設定**應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-179">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c2e2f-180">按一下 [帳戶] > [您的帳戶]。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="c2e2f-181">按一下 [新增工作或學校帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="c2e2f-182">完成驗證 tooyour 組織時，如果出現提示，然後依照顯示 hello 步驟提供多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-182">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c2e2f-183">再試一次 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2e2f-183">Try again tooaccess hello application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="c2e2f-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2e2f-184">Next steps</span></span>
[<span data-ttu-id="c2e2f-185">Azure Active Directory 條件式存取</span><span class="sxs-lookup"><span data-stu-id="c2e2f-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

