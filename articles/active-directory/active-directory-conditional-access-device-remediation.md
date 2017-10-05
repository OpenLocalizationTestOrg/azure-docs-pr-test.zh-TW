---
title: "在 Windows 裝置的 Azure 入口網站上您無法從這裡前往該處 | Microsoft Docs"
description: "了解您無法從這裡前往該處的原因，以及可以查看哪些內容來避免產生此對話方塊。"
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
ms.openlocfilehash: 16543c7bb7b6b236dcc24093c9963bc218ca1fa6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="db670-104">您無法在 Windows 裝置上從這裡前往該處</span><span class="sxs-lookup"><span data-stu-id="db670-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="db670-105">例如，在嘗試存取貴組織的 SharePoint Online 內部網路期間，您可能會碰到一個頁面指出「您無法從這裡前往該處」。</span><span class="sxs-lookup"><span data-stu-id="db670-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="db670-106">您會看到此頁面，因為您的系統管理員已設定條件式存取原則，以防止在某些情況下存取貴組織的資源。</span><span class="sxs-lookup"><span data-stu-id="db670-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access to your organization's resources under certain conditions.</span></span> <span data-ttu-id="db670-107">雖然可能需要連絡技術支援或系統管理員才能解決此問題，但您可以先自行嘗試幾件事。</span><span class="sxs-lookup"><span data-stu-id="db670-107">While it might be necessary to contact helpdesk or your administrator to get this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="db670-108">如果您使用 **Windows** 裝置，您應該檢查下列事項︰</span><span class="sxs-lookup"><span data-stu-id="db670-108">If you are using a **Windows** device, you should check the following:</span></span>

- <span data-ttu-id="db670-109">您使用支援的瀏覽器？</span><span class="sxs-lookup"><span data-stu-id="db670-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="db670-110">您在裝置上執行支援的 Windows 版本？</span><span class="sxs-lookup"><span data-stu-id="db670-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="db670-111">您的裝置是否符合規範？</span><span class="sxs-lookup"><span data-stu-id="db670-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="db670-112">支援的瀏覽器</span><span class="sxs-lookup"><span data-stu-id="db670-112">Supported browser</span></span>

<span data-ttu-id="db670-113">如果您的系統管理員已設定條件式存取原則，您只可以使用支援的瀏覽器來存取貴組織的資源。</span><span class="sxs-lookup"><span data-stu-id="db670-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="db670-114">在 Windows 裝置上，只支援 **Internet Explorer** 和 **Edge**。</span><span class="sxs-lookup"><span data-stu-id="db670-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="db670-115">查看錯誤頁面的詳細資料區段，即可輕鬆地識別您是否因為不支援的瀏覽器而無法存取資源︰</span><span class="sxs-lookup"><span data-stu-id="db670-115">You can easily identify whether you can't access a resource due to an unsupported browser by looking at the details section of the error page:</span></span>

<span data-ttu-id="db670-116">![不受支援的瀏覽器會收到「您無法從這裡前往該處」訊息](./media/active-directory-conditional-access-device-remediation/02.png "例")</span><span class="sxs-lookup"><span data-stu-id="db670-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="db670-117">唯一的補救方式是根據您的裝置平台來使用應用程式所支援的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="db670-117">The only remediation is to use a browser that the application supports for your device platform.</span></span> <span data-ttu-id="db670-118">如需支援的瀏覽器完整清單，請參閱[支援的瀏覽器](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies)。</span><span class="sxs-lookup"><span data-stu-id="db670-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="db670-119">支援的 Windows 版本</span><span class="sxs-lookup"><span data-stu-id="db670-119">Supported versions of Windows</span></span>

<span data-ttu-id="db670-120">您裝置上的 Windows 作業系統必須符合下列敘述：</span><span class="sxs-lookup"><span data-stu-id="db670-120">The following must be true about the Windows operating system on your device:</span></span> 

- <span data-ttu-id="db670-121">如果您在裝置上執行 Windows 桌面作業系統，它必須是 Windows 7 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="db670-121">If you are running a Windows desktop operating system on your device, it needs to be Windows 7 or later.</span></span>
- <span data-ttu-id="db670-122">如果您在裝置上執行 Windows Server 作業系統，它必須是 Windows Server 2008 R2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="db670-122">If you are running a Windows server operating system on your device, it needs to be Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="db670-123">符合規範的裝置</span><span class="sxs-lookup"><span data-stu-id="db670-123">Compliant device</span></span>

<span data-ttu-id="db670-124">您的系統管理員可能已設定條件式存取原則，其只允許您從符合規範的裝置存取貴組織的資源。</span><span class="sxs-lookup"><span data-stu-id="db670-124">Your administrator might have configured a conditional access policy that allows access to your organization's resources only from compliant devices.</span></span> <span data-ttu-id="db670-125">為了符合規範，您的裝置必須加入內部部署 Active Directory 或加入您的 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="db670-125">To be compliant, your device must be either joined to your on-premises Active Directory or joined to your Azure Active Directory.</span></span>

<span data-ttu-id="db670-126">查看錯誤頁面的詳細資料區段，即可輕鬆地識別您是否因為裝置不符合規範而無法存取資源︰</span><span class="sxs-lookup"><span data-stu-id="db670-126">You can easily identify whether you can't access a resource due to a device that is not compliant by looking at the details section of the error page:</span></span>
 
<span data-ttu-id="db670-127">![未註冊的裝置會收到「您無法從這裡前往該處」訊息](./media/active-directory-conditional-access-device-remediation/01.png "案例")</span><span class="sxs-lookup"><span data-stu-id="db670-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="db670-128">您的裝置已加入內部部署 Active Directory？</span><span class="sxs-lookup"><span data-stu-id="db670-128">Is your device joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="db670-129">**如果您的裝置已加入組織中的內部部署 Active Directory︰**</span><span class="sxs-lookup"><span data-stu-id="db670-129">**If your device is joined to an on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="db670-130">確定您使用工作帳戶 (Active Directory 帳戶) 登入 Windows。</span><span class="sxs-lookup"><span data-stu-id="db670-130">Make sure that you sign in to Windows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="db670-131">透過虛擬私人網路 (VPN) 或 DirectAccess 連接到公司網路。</span><span class="sxs-lookup"><span data-stu-id="db670-131">Connect to your corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="db670-132">連接之後，按 Windows 標誌鍵 + L 鍵來鎖定您的 Windows 工作階段。</span><span class="sxs-lookup"><span data-stu-id="db670-132">After you are connected, press the Windows logo key + the L key to lock your Windows session.</span></span>
4. <span data-ttu-id="db670-133">輸入您的工作帳戶認證，以將 Windows 工作階段解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="db670-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="db670-134">等候一分鐘，然後再次嘗試存取應用程式或服務。</span><span class="sxs-lookup"><span data-stu-id="db670-134">Wait for a minute, and then try again to access the application or service.</span></span>
6. <span data-ttu-id="db670-135">如果您看到相同的頁面，請按一下 [更多詳細資料] 連結，然後備妥詳細資料來連絡您的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="db670-135">If you see the same page, click the **More details** link, and then contact your administrator with the details.</span></span>


### <a name="is-your-device-not-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="db670-136">您的裝置未加入內部部署 Active Directory？</span><span class="sxs-lookup"><span data-stu-id="db670-136">Is your device not joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="db670-137">如果您的裝置未加入內部部署 Active Directory 且執行的是 Windows 10，您有兩個選項︰</span><span class="sxs-lookup"><span data-stu-id="db670-137">If your device is not joined to an on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="db670-138">執行 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="db670-138">Run Azure AD Join</span></span>
* <span data-ttu-id="db670-139">將您的工作帳戶或學校帳戶新增至 Windows</span><span class="sxs-lookup"><span data-stu-id="db670-139">Add your work or school account to Windows</span></span>

<span data-ttu-id="db670-140">如需這些選項有何差異的相關資訊，請參閱[在您的工作場所中使用 Windows 10 裝置](active-directory-azureadjoin-windows10-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="db670-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="db670-141">如果您的裝置：</span><span class="sxs-lookup"><span data-stu-id="db670-141">If your device:</span></span>

- <span data-ttu-id="db670-142">屬於您的組織，您應該執行 Azure AD Join。</span><span class="sxs-lookup"><span data-stu-id="db670-142">Belongs to your organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="db670-143">是個人裝置或 Windows 手機，您應該將您的工作或學校帳戶新增至 Windows。</span><span class="sxs-lookup"><span data-stu-id="db670-143">Is a personal device or a Windows phone, you should add your work or school account to Windows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="db670-144">Windows 10 上的 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="db670-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="db670-145">將裝置加入至 Azure AD 的步驟會繫結您執行的 Windows 10 版本。</span><span class="sxs-lookup"><span data-stu-id="db670-145">The steps to join your device to Azure AD are tied the version of Windows 10 you are running on it.</span></span> <span data-ttu-id="db670-146">若要判斷 Windows 10 作業系統的版本，請執行 **winver** 命令︰</span><span class="sxs-lookup"><span data-stu-id="db670-146">To determine the version of your Windows 10 operating system, run the **winver** command:</span></span> 

![Windows 版本](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="db670-148">**Windows 10 年度更新 (版本 1607)：**</span><span class="sxs-lookup"><span data-stu-id="db670-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="db670-149">開啟 [設定]  應用程式。</span><span class="sxs-lookup"><span data-stu-id="db670-149">Open the **Settings** app.</span></span>
2. <span data-ttu-id="db670-150">按一下 [帳戶] > [存取工作或學校]。</span><span class="sxs-lookup"><span data-stu-id="db670-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="db670-151">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="db670-151">Click **Connect**.</span></span>
4. <span data-ttu-id="db670-152">按一下 [將此裝置加入 Azure AD]。</span><span class="sxs-lookup"><span data-stu-id="db670-152">Click **Join this device to Azure AD**.</span></span>
5. <span data-ttu-id="db670-153">向您的組織驗證、提供多重要素驗證 (若提示的話)，然後依照顯示的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="db670-153">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
6. <span data-ttu-id="db670-154">登出，然後使用您的工作帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="db670-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="db670-155">再次嘗試存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="db670-155">Try again to access the application.</span></span>

<span data-ttu-id="db670-156">**Windows 10 2015 年 11 月更新 (版本 1511)：**</span><span class="sxs-lookup"><span data-stu-id="db670-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="db670-157">開啟 [設定]  應用程式。</span><span class="sxs-lookup"><span data-stu-id="db670-157">Open the **Settings** app.</span></span>
2. <span data-ttu-id="db670-158">按一下 [系統] > [關於]。</span><span class="sxs-lookup"><span data-stu-id="db670-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="db670-159">按一下 [加入 Azure AD] 。</span><span class="sxs-lookup"><span data-stu-id="db670-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="db670-160">向您的組織驗證、提供多重要素驗證 (若提示的話)，然後依照顯示的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="db670-160">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="db670-161">登出，然後使用您的工作帳戶 (Azure AD 帳戶) 登入。</span><span class="sxs-lookup"><span data-stu-id="db670-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="db670-162">再次嘗試存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="db670-162">Try again to access the application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="db670-163">在 Windows 8.1 上的 Workplace Join</span><span class="sxs-lookup"><span data-stu-id="db670-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="db670-164">如果您的裝置未加入網域且執行的是 Windows 8.1，若要執行 [加入工作場所] 並在 Microsoft Intune 中註冊，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="db670-164">If your device is not domain-joined and runs Windows 8.1, to do a Workplace Join and enroll in Microsoft Intune, do the following steps:</span></span>

1. <span data-ttu-id="db670-165">開啟 [電腦設定] 。</span><span class="sxs-lookup"><span data-stu-id="db670-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="db670-166">按一下 [網路] > [工作場所]。</span><span class="sxs-lookup"><span data-stu-id="db670-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="db670-167">按一下 [ **加入**]。</span><span class="sxs-lookup"><span data-stu-id="db670-167">Click **Join**.</span></span>
4. <span data-ttu-id="db670-168">向您的組織驗證、提供多重要素驗證 (若提示的話)，然後依照顯示的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="db670-168">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="db670-169">按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="db670-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="db670-170">再次嘗試存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="db670-170">Try again to access the application.</span></span>



#### <a name="add-your-work-or-school-account-to-windows"></a><span data-ttu-id="db670-171">將您的工作帳戶或學校帳戶新增至 Windows</span><span class="sxs-lookup"><span data-stu-id="db670-171">Add your work or school account to Windows</span></span> 


<span data-ttu-id="db670-172">**Windows 10 年度更新 (版本 1607)：**</span><span class="sxs-lookup"><span data-stu-id="db670-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="db670-173">開啟 [設定]  應用程式。</span><span class="sxs-lookup"><span data-stu-id="db670-173">Open the **Settings** app.</span></span>
2. <span data-ttu-id="db670-174">按一下 [帳戶] > [存取工作或學校]。</span><span class="sxs-lookup"><span data-stu-id="db670-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="db670-175">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="db670-175">Click **Connect**.</span></span>
4. <span data-ttu-id="db670-176">向您的組織驗證、提供多重要素驗證 (若提示的話)，然後依照顯示的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="db670-176">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="db670-177">再次嘗試存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="db670-177">Try again to access the application.</span></span>


<span data-ttu-id="db670-178">**Windows 10 2015 年 11 月更新 (版本 1511)：**</span><span class="sxs-lookup"><span data-stu-id="db670-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="db670-179">開啟 [設定]  應用程式。</span><span class="sxs-lookup"><span data-stu-id="db670-179">Open the **Settings** app.</span></span>
2. <span data-ttu-id="db670-180">按一下 [帳戶] > [您的帳戶]。</span><span class="sxs-lookup"><span data-stu-id="db670-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="db670-181">按一下 [新增工作或學校帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="db670-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="db670-182">向您的組織驗證、提供多重要素驗證 (若提示的話)，然後依照顯示的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="db670-182">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="db670-183">再次嘗試存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="db670-183">Try again to access the application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="db670-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db670-184">Next steps</span></span>
[<span data-ttu-id="db670-185">Azure Active Directory 條件式存取</span><span class="sxs-lookup"><span data-stu-id="db670-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

