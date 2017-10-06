---
title: "安裝 hello 應用程式存取面板瀏覽器延伸模組的 aaaProblem |Microsoft 文件"
description: "安裝 hello 存取面板瀏覽器延伸模組時，toofix 常見錯誤如何發生"
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
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a><span data-ttu-id="08b05-103">安裝 hello 應用程式存取面板瀏覽器延伸模組的問題</span><span class="sxs-lookup"><span data-stu-id="08b05-103">Problem installing hello application access panel browser extension</span></span>

<span data-ttu-id="08b05-104">hello 存取面板是網頁型入口網站讓使用者具有工作或學校帳戶在 Azure Active Directory (Azure AD) tooview 並啟動雲端型應用程式中的 hello Azure AD 系統管理員已被授與存取權。</span><span class="sxs-lookup"><span data-stu-id="08b05-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="08b05-105">自助式群組並透過 hello 存取面板應用程式管理功能，也可以使用具有 Azure AD 版本的使用者。</span><span class="sxs-lookup"><span data-stu-id="08b05-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="08b05-106">hello 存取面板是分開 hello Azure 入口網站，而且不需要使用者 toohave Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="08b05-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="08b05-107">toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="08b05-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="08b05-108">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="08b05-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="08b05-109">會議 hello 存取面板 的瀏覽器需求</span><span class="sxs-lookup"><span data-stu-id="08b05-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="08b05-110">存取面板 hello 需要支援 JavaScript 的瀏覽器，並啟用 CSS。</span><span class="sxs-lookup"><span data-stu-id="08b05-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="08b05-111">toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="08b05-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="08b05-112">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="08b05-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="08b05-113">針對密碼型 SSO，hello 終端使用者的瀏覽器可以是：</span><span class="sxs-lookup"><span data-stu-id="08b05-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="08b05-114">Internet Explorer 8、9、10、11 -- 在 Windows 7 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="08b05-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="08b05-115">Windows 10 Anniversary Edition 或更新版本上的 Edge</span><span class="sxs-lookup"><span data-stu-id="08b05-115">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="08b05-116">Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="08b05-116">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="08b05-117">Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="08b05-117">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="08b05-118">如何 tooinstall hello 存取面板瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="08b05-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="08b05-119">tooinstall hello 存取面板瀏覽器延伸模組，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="08b05-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="08b05-120">開啟 hello[存取面板](https://myapps.microsoft.com)其中一種支援的 hello 瀏覽器和登入為**使用者**Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="08b05-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="08b05-121">按一下**password SSO 應用程式**hello 存取面板中。</span><span class="sxs-lookup"><span data-stu-id="08b05-121">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="08b05-122">在 hello 提示詢問 tooinstall hello 軟體，選取 **立即安裝**。</span><span class="sxs-lookup"><span data-stu-id="08b05-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="08b05-123">根據您的瀏覽器就導向的 toohello 下載連結。</span><span class="sxs-lookup"><span data-stu-id="08b05-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="08b05-124">**新增**hello 延伸 tooyour 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="08b05-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="08b05-125">如果您的瀏覽器要求，請選取 tooeither**啟用**或**允許**hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="08b05-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="08b05-126">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="08b05-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="08b05-127">到 hello 存取面板登入，請參閱 < 是否您可以**啟動**password SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="08b05-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="08b05-128">您可能也 hello 從下載擴充功能的 Chrome 和邊緣 hello 以下的直接連結：</span><span class="sxs-lookup"><span data-stu-id="08b05-128">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="08b05-129">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="08b05-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="08b05-130">Edge 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="08b05-130">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="08b05-131">設定適用於 Internet Explorer 的群組原則</span><span class="sxs-lookup"><span data-stu-id="08b05-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="08b05-132">您可以設定群組原則可讓您 tooremotely 安裝 hello 存取面板延伸模組的 Internet Explorer 上使用者的機器。</span><span class="sxs-lookup"><span data-stu-id="08b05-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="08b05-133">hello 的先決條件包括：</span><span class="sxs-lookup"><span data-stu-id="08b05-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="08b05-134">您已設定[Active Directory 網域服務](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)，及您已加入您的使用者機器 tooyour 網域。</span><span class="sxs-lookup"><span data-stu-id="08b05-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="08b05-135">您必須擁有 hello [編輯設定] 的權限 tooedit hello 群組原則物件 (GPO)。</span><span class="sxs-lookup"><span data-stu-id="08b05-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="08b05-136">根據預設，hello 下列安全性群組的成員擁有此權限： 網域系統管理員、 企業系統管理員和 Group Policy Creator Owners。</span><span class="sxs-lookup"><span data-stu-id="08b05-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="08b05-137">[深入了解](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="08b05-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="08b05-138">請遵循 hello 教學課程[如何 tooDeploy hello 存取面板延伸模組使用群組原則設定 Internet Explorer](active-directory-saas-ie-group-policy.md)如需有關如何 tooconfigure hello 群組原則，並將其部署 toousers 的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="08b05-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="08b05-139">疑難排解 hello Internet Explorer 中的 存取面板</span><span class="sxs-lookup"><span data-stu-id="08b05-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="08b05-140">請遵循 hello[疑難排解 hello Internet explorer 的 存取面板延伸模組](active-directory-saas-ie-troubleshooting.md)引導存取診斷工具和逐步指示在 ie 設定 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="08b05-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="08b05-141">如果這些疑難排解步驟無法解決 hello 問題</span><span class="sxs-lookup"><span data-stu-id="08b05-141">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="08b05-142">開啟支援票證以 hello 如果有的話，下列資訊：</span><span class="sxs-lookup"><span data-stu-id="08b05-142">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="08b05-143">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="08b05-143">Correlation error ID</span></span>

-   <span data-ttu-id="08b05-144">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="08b05-144">UPN (user email address)</span></span>

-   <span data-ttu-id="08b05-145">TenantID</span><span class="sxs-lookup"><span data-stu-id="08b05-145">TenantID</span></span>

-   <span data-ttu-id="08b05-146">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="08b05-146">Browser type</span></span>

-   <span data-ttu-id="08b05-147">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="08b05-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="08b05-148">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="08b05-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="08b05-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08b05-149">Next steps</span></span>
[<span data-ttu-id="08b05-150">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="08b05-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
