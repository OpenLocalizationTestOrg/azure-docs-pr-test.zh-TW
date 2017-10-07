---
title: "單一登入的登入 tooan 密碼設定的 Azure AD 庫應用程式的 aaaProblems |Microsoft 文件"
description: "討論提供指引 tootroubleshoot 發出相關的 toosigning tooAzure 中設定密碼單一登入的 AD 庫應用程式的問題區域"
services: active-directory
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
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="fdb22-103">登入 tooan 設定密碼單一登入 Azure AD 庫應用程式的問題</span><span class="sxs-lookup"><span data-stu-id="fdb22-103">Problems signing in tooan Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="fdb22-104">hello 存取面板是網頁型入口網站讓使用者具有工作或學校帳戶在 Azure Active Directory (Azure AD) tooview 並啟動雲端型應用程式中的 hello Azure AD 系統管理員已被授與存取權。</span><span class="sxs-lookup"><span data-stu-id="fdb22-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="fdb22-105">自助式群組並透過 hello 存取面板應用程式管理功能，也可以使用具有 Azure AD 版本的使用者。</span><span class="sxs-lookup"><span data-stu-id="fdb22-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="fdb22-106">hello 存取面板是分開 hello Azure 入口網站，而且不需要使用者 toohave Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fdb22-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="fdb22-107">toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="fdb22-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="fdb22-108">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="fdb22-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="fdb22-109">會議 hello 存取面板 的瀏覽器需求</span><span class="sxs-lookup"><span data-stu-id="fdb22-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="fdb22-110">存取面板 hello 需要支援 JavaScript 的瀏覽器，並啟用 CSS。</span><span class="sxs-lookup"><span data-stu-id="fdb22-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="fdb22-111">toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="fdb22-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="fdb22-112">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="fdb22-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="fdb22-113">針對密碼型 SSO，hello 終端使用者的瀏覽器可以是：</span><span class="sxs-lookup"><span data-stu-id="fdb22-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="fdb22-114">Internet Explorer 8、9、10、11 -- 在 Windows 7 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="fdb22-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="fdb22-115">Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="fdb22-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="fdb22-116">Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="fdb22-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="fdb22-117">hello 密碼型 SSO 延伸模組時，可以使用 Windows 10 中的 edge 瀏覽器延伸模組會變成支援 edge。</span><span class="sxs-lookup"><span data-stu-id="fdb22-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="fdb22-118">如何 tooinstall hello 存取面板瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="fdb22-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="fdb22-119">tooinstall hello 存取面板瀏覽器延伸模組，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="fdb22-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="fdb22-120">開啟 hello[存取面板](https://myapps.microsoft.com)其中一種支援的 hello 瀏覽器和登入為**使用者**Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="fdb22-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="fdb22-121">按一下**password SSO 應用程式**hello 存取面板中。</span><span class="sxs-lookup"><span data-stu-id="fdb22-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="fdb22-122">在 hello 提示詢問 tooinstall hello 軟體，選取 **立即安裝**。</span><span class="sxs-lookup"><span data-stu-id="fdb22-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="fdb22-123">根據您的瀏覽器就導向的 toohello 下載連結。</span><span class="sxs-lookup"><span data-stu-id="fdb22-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="fdb22-124">**新增**hello 延伸 tooyour 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="fdb22-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="fdb22-125">如果您的瀏覽器要求，請選取 tooeither**啟用**或**允許**hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="fdb22-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="fdb22-126">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="fdb22-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="fdb22-127">到 hello 存取面板登入，請參閱 < 是否您可以**啟動**password SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="fdb22-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="fdb22-128">您可能也 hello 從下載擴充功能的 Chrome 和 Firefox hello 以下的直接連結：</span><span class="sxs-lookup"><span data-stu-id="fdb22-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="fdb22-129">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="fdb22-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="fdb22-130">Firefox 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="fdb22-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="fdb22-131">設定適用於 Internet Explorer 的群組原則</span><span class="sxs-lookup"><span data-stu-id="fdb22-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="fdb22-132">您可以設定群組原則可讓您 tooremotely 安裝 hello 存取面板延伸模組的 Internet Explorer 上使用者的機器。</span><span class="sxs-lookup"><span data-stu-id="fdb22-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="fdb22-133">hello 的先決條件包括：</span><span class="sxs-lookup"><span data-stu-id="fdb22-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="fdb22-134">您已設定[Active Directory 網域服務](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)，及您已加入您的使用者機器 tooyour 網域。</span><span class="sxs-lookup"><span data-stu-id="fdb22-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="fdb22-135">您必須擁有 hello [編輯設定] 的權限 tooedit hello 群組原則物件 (GPO)。</span><span class="sxs-lookup"><span data-stu-id="fdb22-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="fdb22-136">根據預設，hello 下列安全性群組的成員擁有此權限： 網域系統管理員、 企業系統管理員和 Group Policy Creator Owners。</span><span class="sxs-lookup"><span data-stu-id="fdb22-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="fdb22-137">[深入了解](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fdb22-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="fdb22-138">請遵循 hello 教學課程[如何 tooDeploy hello 存取面板延伸模組使用群組原則設定 Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy)如需有關如何 tooconfigure hello 群組原則，並將其部署 toousers 的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="fdb22-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="fdb22-139">疑難排解 hello Internet Explorer 中的 存取面板</span><span class="sxs-lookup"><span data-stu-id="fdb22-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="fdb22-140">請遵循 hello[疑難排解 hello Internet explorer 的 存取面板延伸模組](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot)引導存取診斷工具和逐步指示在 ie 設定 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="fdb22-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="fdb22-141">如何 tooconfigure 密碼單一登入非組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="fdb22-141">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="fdb22-142">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="fdb22-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="fdb22-143">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="fdb22-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="fdb22-144">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="fdb22-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="fdb22-145">將使用者指派 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="fdb22-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="fdb22-146">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="fdb22-146">Add a non-gallery application</span></span>

<span data-ttu-id="fdb22-147">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="fdb22-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="fdb22-148">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**</span><span class="sxs-lookup"><span data-stu-id="fdb22-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="fdb22-149">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="fdb22-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fdb22-150">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="fdb22-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fdb22-151">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="fdb22-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fdb22-152">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="fdb22-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="fdb22-153">按一下 [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fdb22-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="fdb22-154">輸入 hello 應用程式的名稱在 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="fdb22-154">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="fdb22-155">選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="fdb22-155">Select **Add.**</span></span>

<span data-ttu-id="fdb22-156">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fdb22-156">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="fdb22-157">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="fdb22-157">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="fdb22-158">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="fdb22-158">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="fdb22-159">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="fdb22-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fdb22-160">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="fdb22-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fdb22-161">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="fdb22-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fdb22-162">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="fdb22-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fdb22-163">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fdb22-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="fdb22-164">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="fdb22-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="fdb22-165">選取您想 tooconfigure 單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="fdb22-165">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="fdb22-166">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="fdb22-166">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fdb22-167">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="fdb22-167">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="fdb22-168">輸入 hello**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="fdb22-168">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="fdb22-169">這是讓使用者輸入其使用者名稱和密碼 toosign 中的以 hello URL。</span><span class="sxs-lookup"><span data-stu-id="fdb22-169">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="fdb22-170">請確定 hello 登入欄位會顯示在 hello URL。</span><span class="sxs-lookup"><span data-stu-id="fdb22-170">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="fdb22-171">將使用者指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdb22-171">Assign users toohello application.</span></span>

11. <span data-ttu-id="fdb22-172">此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="fdb22-172">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="fdb22-173">否則，使用者在提示的 tooenter hello 認證本身在啟動。</span><span class="sxs-lookup"><span data-stu-id="fdb22-173">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="fdb22-174">將使用者指派 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="fdb22-174">Assign users toohello application</span></span>

<span data-ttu-id="fdb22-175">tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="fdb22-175">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="fdb22-176">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="fdb22-176">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fdb22-177">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="fdb22-177">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fdb22-178">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="fdb22-178">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fdb22-179">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="fdb22-179">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fdb22-180">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fdb22-180">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="fdb22-181">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="fdb22-181">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="fdb22-182">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdb22-182">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="fdb22-183">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="fdb22-183">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fdb22-184">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fdb22-184">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="fdb22-185">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fdb22-185">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="fdb22-186">Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="fdb22-186">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="fdb22-187">將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="fdb22-187">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="fdb22-188">按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="fdb22-188">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="fdb22-189">**選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="fdb22-189">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="fdb22-190">當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdb22-190">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="fdb22-191">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。</span><span class="sxs-lookup"><span data-stu-id="fdb22-191">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="fdb22-192">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="fdb22-192">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="fdb22-193">在短時間，您已選取的 hello 使用者會無法 toolaunch 中的這些應用程式之後 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="fdb22-193">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="fdb22-194">如果不執行 hello 這些疑難排解步驟解決 hello 問題</span><span class="sxs-lookup"><span data-stu-id="fdb22-194">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="fdb22-195">開啟支援票證以 hello 如果有的話，下列資訊：</span><span class="sxs-lookup"><span data-stu-id="fdb22-195">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="fdb22-196">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="fdb22-196">Correlation error ID</span></span>

-   <span data-ttu-id="fdb22-197">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="fdb22-197">UPN (user email address)</span></span>

-   <span data-ttu-id="fdb22-198">TenantID</span><span class="sxs-lookup"><span data-stu-id="fdb22-198">TenantID</span></span>

-   <span data-ttu-id="fdb22-199">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="fdb22-199">Browser type</span></span>

-   <span data-ttu-id="fdb22-200">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="fdb22-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="fdb22-201">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="fdb22-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdb22-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fdb22-202">Next steps</span></span>
[<span data-ttu-id="fdb22-203">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="fdb22-203">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

