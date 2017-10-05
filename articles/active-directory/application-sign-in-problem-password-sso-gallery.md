---
title: "登入針對同盟單一登入設定之 Azure AD 資源庫應用程式的問題 | Microsoft Docs"
description: "如何為針對密碼單一登入設定的 Azure AD 資源庫應用程式問題疑難排解"
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: f8521d1386bba8004e84fe8862a5f59a65ea19ad
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="5e322-103">登入針對同盟單一登入設定之 Azure AD 資源庫應用程式的問題</span><span class="sxs-lookup"><span data-stu-id="5e322-103">Problems signing in to an Azure AD Gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="5e322-104">存取面板是網頁型入口網站，可讓在 Azure Active Directory (Azure AD) 中具有公司或學校帳戶的使用者，檢視和啟動 Azure AD 系統管理員已授權他們存取的雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e322-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="5e322-105">具有 Azure AD 版本的使用者也可以透過存取面板使用自助群組和應用程式管理功能。</span><span class="sxs-lookup"><span data-stu-id="5e322-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="5e322-106">存取面板與 Azure 入口網站分開，使用者不需要具備 Azure 訂用帳戶也能使用。</span><span class="sxs-lookup"><span data-stu-id="5e322-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="5e322-107">若要在存取面板中使用密碼單一登入 (SSO)，必須在使用者的瀏覽器中安裝存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5e322-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="5e322-108">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5e322-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="5e322-109">符合存取面板的瀏覽器需求</span><span class="sxs-lookup"><span data-stu-id="5e322-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="5e322-110">存取面板需要支援 JavaScript 且已啟用 CSS 的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5e322-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="5e322-111">若要在存取面板中使用密碼單一登入 (SSO)，必須在使用者的瀏覽器中安裝存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5e322-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="5e322-112">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5e322-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="5e322-113">若是密碼 SSO，則使用者的瀏覽器可以是：</span><span class="sxs-lookup"><span data-stu-id="5e322-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="5e322-114">Internet Explorer 8、9、10、11 - 在 Windows 7 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="5e322-114">Internet Explorer 8, 9, 10, 11 - on Windows 7 or later</span></span>

-   <span data-ttu-id="5e322-115">Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="5e322-115">Chrome - on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="5e322-116">Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="5e322-116">Firefox 26.0 or later - on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="5e322-117">當瀏覽器擴充開始支援 Edge 時，Windows 10 中的 Edge 就能使用密碼 SSO 擴充。</span><span class="sxs-lookup"><span data-stu-id="5e322-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="5e322-118">如何安裝存取面板瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="5e322-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="5e322-119">若要安裝存取面板的瀏覽器延伸模組，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5e322-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="5e322-120">在其中一種支援的瀏覽器中開啟[存取面板](https://myapps.microsoft.com)，然後在您的 Azure AD 中以**使用者**身分登入。</span><span class="sxs-lookup"><span data-stu-id="5e322-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="5e322-121">按一下存取面板中的 [密碼-SSO 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5e322-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="5e322-122">在要求安裝軟體的提示中，選取 [立即安裝]。</span><span class="sxs-lookup"><span data-stu-id="5e322-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="5e322-123">系統會根據您的瀏覽器將您導向至下載連結。</span><span class="sxs-lookup"><span data-stu-id="5e322-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="5e322-124">將延伸模組**新增**到瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="5e322-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="5e322-125">如果您的瀏覽器要求，請選取 [啟用] 或 [允許] 該延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5e322-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="5e322-126">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="5e322-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="5e322-127">登入存取面板，並查看您是否可以**啟動**密碼-SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e322-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="5e322-128">您可能也會從下列直接連結中下載適用於 Chrome 和 Firefox 的延伸模組：</span><span class="sxs-lookup"><span data-stu-id="5e322-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="5e322-129">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="5e322-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="5e322-130">Firefox 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="5e322-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="5e322-131">設定適用於 Internet Explorer 的群組原則</span><span class="sxs-lookup"><span data-stu-id="5e322-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="5e322-132">您可以設定一個群組原則，以允許您在使用者電腦上遠端安裝適用於 Internet Explorer 的存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5e322-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="5e322-133">必要條件包括：</span><span class="sxs-lookup"><span data-stu-id="5e322-133">The prerequisites include:</span></span>

-   <span data-ttu-id="5e322-134">您已設定了 [Active Directory 網域服務](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)，並且已將使用者的電腦加入網域。</span><span class="sxs-lookup"><span data-stu-id="5e322-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="5e322-135">您必須擁有「編輯設定」權限，才能編輯群組原則物件 (GPO)。</span><span class="sxs-lookup"><span data-stu-id="5e322-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="5e322-136">根據預設，下列安全性群組的成員擁有此權限：網域系統管理員、企業系統管理員及群組原則建立者擁有者。</span><span class="sxs-lookup"><span data-stu-id="5e322-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="5e322-137">[深入了解](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5e322-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="5e322-138">如需如何設定群組原則並將它部署到使用者的逐步指示，請遵循[如何使用群組原則部署 Internet Explorer 的存取面板延伸模組](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy)教學課程。</span><span class="sxs-lookup"><span data-stu-id="5e322-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="5e322-139">進行 Internet Explorer 中存取面板的疑難排解</span><span class="sxs-lookup"><span data-stu-id="5e322-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="5e322-140">如需存取診斷工具和設定 IE 延伸模組的逐步指示，請遵循[疑難排解 Internet Explorer 的存取面板延伸模組](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot)指南。</span><span class="sxs-lookup"><span data-stu-id="5e322-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="5e322-141">如何為 Azure AD 資源庫應用程式設定密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="5e322-141">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="5e322-142">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="5e322-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="5e322-143">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="5e322-143">Add an application from the Azure AD gallery</span></span>](#_Add_an_application)

-   [<span data-ttu-id="5e322-144">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="5e322-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="5e322-145">將使用者指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="5e322-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="5e322-146">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="5e322-146">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="5e322-147">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="5e322-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="5e322-148">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="5e322-148">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="5e322-149">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="5e322-149">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e322-150">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="5e322-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e322-151">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5e322-151">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e322-152">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e322-152">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="5e322-153">在 [從資源庫新增] 區段的 [輸入名稱] 文字方塊中，輸入應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="5e322-153">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="5e322-154">選取您要設為單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e322-154">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="5e322-155">新增應用程式之前，您可以從 [名稱] 文字方塊變更其名稱。</span><span class="sxs-lookup"><span data-stu-id="5e322-155">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="5e322-156">按一下 [新增] 按鈕新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e322-156">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="5e322-157">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5e322-157">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="5e322-158">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="5e322-158">Configure the application for password single sign-on</span></span>

<span data-ttu-id="5e322-159">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="5e322-159">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="5e322-160">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="5e322-160">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5e322-161">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="5e322-161">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e322-162">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="5e322-162">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e322-163">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5e322-163">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e322-164">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5e322-164">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="5e322-165">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5e322-165">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e322-166">選取您要設定單一登入的應用程式</span><span class="sxs-lookup"><span data-stu-id="5e322-166">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="5e322-167">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5e322-167">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e322-168">選取 [以密碼為基礎的登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="5e322-168">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="5e322-169">[將使用者指派至應用程式](#_How_to_assign)。</span><span class="sxs-lookup"><span data-stu-id="5e322-169">[Assign users to the application](#_How_to_assign).</span></span>

10. <span data-ttu-id="5e322-170">此外，您也可以選取使用者資料列，按一下 [更新認證]，然後代表使用者輸入使用者名稱和密碼，以代表使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="5e322-170">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="5e322-171">否則，系統會提示使用者在啟動時自行輸入認證。</span><span class="sxs-lookup"><span data-stu-id="5e322-171">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="5e322-172">將使用者指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="5e322-172">Assign users to the application</span></span>

<span data-ttu-id="5e322-173">若要直接將一或多個使用者指派至應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="5e322-173">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="5e322-174">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="5e322-174">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5e322-175">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="5e322-175">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5e322-176">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="5e322-176">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5e322-177">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5e322-177">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5e322-178">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="5e322-178">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="5e322-179">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5e322-179">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5e322-180">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e322-180">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="5e322-181">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5e322-181">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5e322-182">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5e322-182">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="5e322-183">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="5e322-183">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="5e322-184">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之使用者的**全名**或**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="5e322-184">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="5e322-185">將滑鼠停留在清單中的**使用者**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="5e322-185">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="5e322-186">按一下使用者設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="5e322-186">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="5e322-187">**選擇性︰**如果您想要**新增多位使用者**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**全名**或**電子郵件地址**，然後按一下核取方塊，將此使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="5e322-187">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="5e322-188">當您完成選取使用者時，按一下 [選取] 按鈕，將他們新增到要指派至應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="5e322-188">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="5e322-189">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="5e322-189">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="5e322-190">按一下 [指派] 按鈕，將應用程式指派給選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="5e322-190">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="5e322-191">稍待片刻，您已選取的使用者便能在存取面板中啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e322-191">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshoot-steps-dont-resolve-the-issue"></a><span data-ttu-id="5e322-192">如果這些疑難排解步驟無法解決問題</span><span class="sxs-lookup"><span data-stu-id="5e322-192">If these troubleshoot steps don't resolve the issue</span></span> 
<span data-ttu-id="5e322-193">使用下列資訊 (若有的話) 開啟支援票證︰</span><span class="sxs-lookup"><span data-stu-id="5e322-193">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="5e322-194">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="5e322-194">Correlation error ID</span></span>

-   <span data-ttu-id="5e322-195">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="5e322-195">UPN (user email address)</span></span>

-   <span data-ttu-id="5e322-196">TenantID</span><span class="sxs-lookup"><span data-stu-id="5e322-196">TenantID</span></span>

-   <span data-ttu-id="5e322-197">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="5e322-197">Browser type</span></span>

-   <span data-ttu-id="5e322-198">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="5e322-198">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="5e322-199">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="5e322-199">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e322-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e322-200">Next steps</span></span>
[<span data-ttu-id="5e322-201">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="5e322-201">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
