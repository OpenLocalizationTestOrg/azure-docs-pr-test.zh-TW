---
title: "單一登入的登入 tooan 已設定為同盟的 Azure AD 庫應用程式的 aaaProblems |Microsoft 文件"
description: "Tootroubleshoot，如何與 Azure AD 的組件庫設定為 密碼單一登入的應用程式問題"
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
ms.openlocfilehash: 7ba28765e1d1f13025d740790a2f87654ae0daed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="047d4-103">登入 tooan 設定同盟單一登入 Azure AD 庫應用程式的問題</span><span class="sxs-lookup"><span data-stu-id="047d4-103">Problems signing in tooan Azure AD Gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="047d4-104">hello 存取面板是網頁型入口網站讓使用者具有工作或學校帳戶在 Azure Active Directory (Azure AD) tooview 並啟動雲端型應用程式中的 hello Azure AD 系統管理員已被授與存取權。</span><span class="sxs-lookup"><span data-stu-id="047d4-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="047d4-105">自助式群組並透過 hello 存取面板應用程式管理功能，也可以使用具有 Azure AD 版本的使用者。</span><span class="sxs-lookup"><span data-stu-id="047d4-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="047d4-106">hello 存取面板是分開 hello Azure 入口網站，而且不需要使用者 toohave Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="047d4-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="047d4-107">toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="047d4-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="047d4-108">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="047d4-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="047d4-109">會議 hello 存取面板 的瀏覽器需求</span><span class="sxs-lookup"><span data-stu-id="047d4-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="047d4-110">存取面板 hello 需要支援 JavaScript 的瀏覽器，並啟用 CSS。</span><span class="sxs-lookup"><span data-stu-id="047d4-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="047d4-111">toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="047d4-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="047d4-112">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="047d4-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="047d4-113">針對密碼型 SSO，hello 終端使用者的瀏覽器可以是：</span><span class="sxs-lookup"><span data-stu-id="047d4-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="047d4-114">Internet Explorer 8、9、10、11 - 在 Windows 7 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="047d4-114">Internet Explorer 8, 9, 10, 11 - on Windows 7 or later</span></span>

-   <span data-ttu-id="047d4-115">Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="047d4-115">Chrome - on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="047d4-116">Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="047d4-116">Firefox 26.0 or later - on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="047d4-117">hello 密碼型 SSO 延伸模組時，可以使用 Windows 10 中的 edge 瀏覽器延伸模組會變成支援 edge。</span><span class="sxs-lookup"><span data-stu-id="047d4-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="047d4-118">如何 tooinstall hello 存取面板瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="047d4-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="047d4-119">tooinstall hello 存取面板瀏覽器延伸模組，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="047d4-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="047d4-120">開啟 hello[存取面板](https://myapps.microsoft.com)其中一種支援的 hello 瀏覽器和登入為**使用者**Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="047d4-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="047d4-121">按一下**password SSO 應用程式**hello 存取面板中。</span><span class="sxs-lookup"><span data-stu-id="047d4-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="047d4-122">在 hello 提示詢問 tooinstall hello 軟體，選取 **立即安裝**。</span><span class="sxs-lookup"><span data-stu-id="047d4-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="047d4-123">根據您的瀏覽器就導向的 toohello 下載連結。</span><span class="sxs-lookup"><span data-stu-id="047d4-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="047d4-124">**新增**hello 延伸 tooyour 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="047d4-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="047d4-125">如果您的瀏覽器要求，請選取 tooeither**啟用**或**允許**hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="047d4-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="047d4-126">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="047d4-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="047d4-127">到 hello 存取面板登入，請參閱 < 是否您可以**啟動**password SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="047d4-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="047d4-128">您可能也 hello 從下載擴充功能的 Chrome 和 Firefox hello 以下的直接連結：</span><span class="sxs-lookup"><span data-stu-id="047d4-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="047d4-129">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="047d4-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="047d4-130">Firefox 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="047d4-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="047d4-131">設定適用於 Internet Explorer 的群組原則</span><span class="sxs-lookup"><span data-stu-id="047d4-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="047d4-132">您可以設定群組原則可讓您 tooremotely 安裝 hello 存取面板延伸模組的 Internet Explorer 上使用者的機器。</span><span class="sxs-lookup"><span data-stu-id="047d4-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="047d4-133">hello 的先決條件包括：</span><span class="sxs-lookup"><span data-stu-id="047d4-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="047d4-134">您已設定[Active Directory 網域服務](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)，及您已加入您的使用者機器 tooyour 網域。</span><span class="sxs-lookup"><span data-stu-id="047d4-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="047d4-135">您必須擁有 hello [編輯設定] 的權限 tooedit hello 群組原則物件 (GPO)。</span><span class="sxs-lookup"><span data-stu-id="047d4-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="047d4-136">根據預設，hello 下列安全性群組的成員擁有此權限： 網域系統管理員、 企業系統管理員和 Group Policy Creator Owners。</span><span class="sxs-lookup"><span data-stu-id="047d4-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="047d4-137">[深入了解](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="047d4-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="047d4-138">請遵循 hello 教學課程[如何 tooDeploy hello 存取面板延伸模組使用群組原則設定 Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy)如需有關如何 tooconfigure hello 群組原則，並將其部署 toousers 的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="047d4-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="047d4-139">疑難排解 hello Internet Explorer 中的 存取面板</span><span class="sxs-lookup"><span data-stu-id="047d4-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="047d4-140">請遵循 hello[疑難排解 hello Internet explorer 的 存取面板延伸模組](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot)引導存取診斷工具和逐步指示在 ie 設定 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="047d4-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="047d4-141">如何 tooconfigure 密碼單一登入 Azure AD 圖庫應用程式</span><span class="sxs-lookup"><span data-stu-id="047d4-141">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="047d4-142">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="047d4-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="047d4-143">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="047d4-143">Add an application from hello Azure AD gallery</span></span>](#_Add_an_application)

-   [<span data-ttu-id="047d4-144">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="047d4-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="047d4-145">將使用者指派 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="047d4-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="047d4-146">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="047d4-146">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="047d4-147">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="047d4-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="047d4-148">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**</span><span class="sxs-lookup"><span data-stu-id="047d4-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="047d4-149">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="047d4-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="047d4-150">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="047d4-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="047d4-151">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="047d4-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="047d4-152">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="047d4-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="047d4-153">在 hello**輸入的名稱**文字方塊中，從 hello**從 hello 圖庫新增**> 一節中，輸入 hello 名稱 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="047d4-153">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="047d4-154">選取要用於單一登入 tooconfigure hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="047d4-154">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="047d4-155">然後再加入 hello 應用程式，您可以變更其名稱從 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="047d4-155">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="047d4-156">按一下**新增**按鈕，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="047d4-156">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="047d4-157">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="047d4-157">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="047d4-158">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="047d4-158">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="047d4-159">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="047d4-159">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="047d4-160">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="047d4-160">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="047d4-161">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="047d4-161">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="047d4-162">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="047d4-162">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="047d4-163">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="047d4-163">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="047d4-164">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="047d4-164">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="047d4-165">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="047d4-165">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="047d4-166">選取您想 tooconfigure 單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="047d4-166">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="047d4-167">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="047d4-167">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="047d4-168">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="047d4-168">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="047d4-169">[將使用者指派 toohello 應用程式](#_How_to_assign)。</span><span class="sxs-lookup"><span data-stu-id="047d4-169">[Assign users toohello application](#_How_to_assign).</span></span>

10. <span data-ttu-id="047d4-170">此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="047d4-170">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="047d4-171">否則，使用者在提示的 tooenter hello 認證本身在啟動。</span><span class="sxs-lookup"><span data-stu-id="047d4-171">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="047d4-172">將使用者指派 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="047d4-172">Assign users toohello application</span></span>

<span data-ttu-id="047d4-173">tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="047d4-173">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="047d4-174">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="047d4-174">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="047d4-175">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="047d4-175">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="047d4-176">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="047d4-176">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="047d4-177">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="047d4-177">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="047d4-178">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="047d4-178">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="047d4-179">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="047d4-179">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="047d4-180">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="047d4-180">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="047d4-181">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="047d4-181">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="047d4-182">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="047d4-182">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="047d4-183">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="047d4-183">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="047d4-184">Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="047d4-184">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="047d4-185">將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="047d4-185">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="047d4-186">按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="047d4-186">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="047d4-187">**選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="047d4-187">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="047d4-188">當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="047d4-188">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="047d4-189">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。</span><span class="sxs-lookup"><span data-stu-id="047d4-189">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="047d4-190">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="047d4-190">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="047d4-191">在短時間，您已選取的 hello 使用者會無法 toolaunch 中的這些應用程式之後 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="047d4-191">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshoot-steps-dont-resolve-hello-issue"></a><span data-ttu-id="047d4-192">如果這些疑難排解步驟沒有解決 hello 問題</span><span class="sxs-lookup"><span data-stu-id="047d4-192">If these troubleshoot steps don't resolve hello issue</span></span> 
<span data-ttu-id="047d4-193">開啟支援票證以 hello 如果有的話，下列資訊：</span><span class="sxs-lookup"><span data-stu-id="047d4-193">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="047d4-194">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="047d4-194">Correlation error ID</span></span>

-   <span data-ttu-id="047d4-195">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="047d4-195">UPN (user email address)</span></span>

-   <span data-ttu-id="047d4-196">TenantID</span><span class="sxs-lookup"><span data-stu-id="047d4-196">TenantID</span></span>

-   <span data-ttu-id="047d4-197">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="047d4-197">Browser type</span></span>

-   <span data-ttu-id="047d4-198">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="047d4-198">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="047d4-199">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="047d4-199">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="047d4-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="047d4-200">Next steps</span></span>
[<span data-ttu-id="047d4-201">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="047d4-201">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
