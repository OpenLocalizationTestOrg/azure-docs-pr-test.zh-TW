---
title: "安裝應用程式存取面板的瀏覽器延伸模組時出現的錯誤 | Microsoft Docs"
description: "如何修正在安裝存取面板的瀏覽器延伸模組時所遇到的常見錯誤"
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
ms.openlocfilehash: 8b7327508633e33917d1fa9c1f35ed1bde5a26e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-access-panel-browser-extension"></a><span data-ttu-id="622ce-103">安裝應用程式存取面板的瀏覽器延伸模組時出現的錯誤</span><span class="sxs-lookup"><span data-stu-id="622ce-103">Problem installing the application access panel browser extension</span></span>

<span data-ttu-id="622ce-104">存取面板是網頁型入口網站，可讓在 Azure Active Directory (Azure AD) 中具有公司或學校帳戶的使用者，檢視和啟動 Azure AD 系統管理員已授權他們存取的雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="622ce-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="622ce-105">具有 Azure AD 版本的使用者也可以透過存取面板使用自助群組和應用程式管理功能。</span><span class="sxs-lookup"><span data-stu-id="622ce-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="622ce-106">存取面板與 Azure 入口網站分開，使用者不需要具備 Azure 訂用帳戶也能使用。</span><span class="sxs-lookup"><span data-stu-id="622ce-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="622ce-107">若要在存取面板中使用密碼單一登入 (SSO)，必須在使用者的瀏覽器中安裝存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="622ce-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="622ce-108">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="622ce-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="622ce-109">符合存取面板的瀏覽器需求</span><span class="sxs-lookup"><span data-stu-id="622ce-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="622ce-110">存取面板需要支援 JavaScript 且已啟用 CSS 的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="622ce-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="622ce-111">若要在存取面板中使用密碼單一登入 (SSO)，必須在使用者的瀏覽器中安裝存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="622ce-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="622ce-112">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="622ce-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="622ce-113">若是密碼 SSO，則使用者的瀏覽器可以是：</span><span class="sxs-lookup"><span data-stu-id="622ce-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="622ce-114">Internet Explorer 8、9、10、11 -- 在 Windows 7 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="622ce-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="622ce-115">Windows 10 Anniversary Edition 或更新版本上的 Edge</span><span class="sxs-lookup"><span data-stu-id="622ce-115">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="622ce-116">Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="622ce-116">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="622ce-117">Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="622ce-117">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="622ce-118">如何安裝存取面板的瀏覽器延伸模組</span><span class="sxs-lookup"><span data-stu-id="622ce-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="622ce-119">若要安裝存取面板的瀏覽器延伸模組，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="622ce-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="622ce-120">在其中一種支援的瀏覽器中開啟[存取面板](https://myapps.microsoft.com)，然後在您的 Azure AD 中以**使用者**身分登入。</span><span class="sxs-lookup"><span data-stu-id="622ce-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="622ce-121">按一下存取面板中的 [密碼-SSO 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="622ce-121">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="622ce-122">在要求安裝軟體的提示中，選取 [立即安裝]。</span><span class="sxs-lookup"><span data-stu-id="622ce-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="622ce-123">系統會根據您的瀏覽器將您導向至下載連結。</span><span class="sxs-lookup"><span data-stu-id="622ce-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="622ce-124">將延伸模組**新增**到瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="622ce-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="622ce-125">如果您的瀏覽器要求，請選取 [啟用] 或 [允許] 該延伸模組。</span><span class="sxs-lookup"><span data-stu-id="622ce-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="622ce-126">安裝之後，**重新啟動**瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="622ce-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="622ce-127">登入存取面板，並查看您是否可以**啟動**密碼-SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="622ce-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="622ce-128">您可能也會從下列直接連結中下載適用於 Chrome 和 Edge 的擴充功能：</span><span class="sxs-lookup"><span data-stu-id="622ce-128">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="622ce-129">Chrome 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="622ce-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="622ce-130">Edge 存取面板延伸模組</span><span class="sxs-lookup"><span data-stu-id="622ce-130">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="622ce-131">設定適用於 Internet Explorer 的群組原則</span><span class="sxs-lookup"><span data-stu-id="622ce-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="622ce-132">您可以設定一個群組原則，以允許您在使用者電腦上遠端安裝適用於 Internet Explorer 的存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="622ce-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="622ce-133">必要條件包括：</span><span class="sxs-lookup"><span data-stu-id="622ce-133">The prerequisites include:</span></span>

-   <span data-ttu-id="622ce-134">您已設定了 [Active Directory 網域服務](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)，並且已將使用者的電腦加入網域。</span><span class="sxs-lookup"><span data-stu-id="622ce-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="622ce-135">您必須擁有「編輯設定」權限，才能編輯群組原則物件 (GPO)。</span><span class="sxs-lookup"><span data-stu-id="622ce-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="622ce-136">根據預設，下列安全性群組的成員擁有此權限：網域系統管理員、企業系統管理員及群組原則建立者擁有者。</span><span class="sxs-lookup"><span data-stu-id="622ce-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="622ce-137">[深入了解](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="622ce-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="622ce-138">如需如何設定群組原則並將它部署到使用者的逐步指示，請遵循[如何使用群組原則部署 Internet Explorer 的存取面板延伸模組](active-directory-saas-ie-group-policy.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="622ce-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="622ce-139">進行 Internet Explorer 中存取面板的疑難排解</span><span class="sxs-lookup"><span data-stu-id="622ce-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="622ce-140">如需存取診斷工具和設定 IE 延伸模組的逐步指示，請遵循[疑難排解 Internet Explorer 的存取面板延伸模組](active-directory-saas-ie-troubleshooting.md)指南。</span><span class="sxs-lookup"><span data-stu-id="622ce-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="622ce-141">如果這些疑難排解步驟無法解決問題</span><span class="sxs-lookup"><span data-stu-id="622ce-141">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="622ce-142">使用下列資訊 (若有的話) 開啟支援票證︰</span><span class="sxs-lookup"><span data-stu-id="622ce-142">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="622ce-143">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="622ce-143">Correlation error ID</span></span>

-   <span data-ttu-id="622ce-144">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="622ce-144">UPN (user email address)</span></span>

-   <span data-ttu-id="622ce-145">TenantID</span><span class="sxs-lookup"><span data-stu-id="622ce-145">TenantID</span></span>

-   <span data-ttu-id="622ce-146">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="622ce-146">Browser type</span></span>

-   <span data-ttu-id="622ce-147">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="622ce-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="622ce-148">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="622ce-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="622ce-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="622ce-149">Next steps</span></span>
[<span data-ttu-id="622ce-150">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="622ce-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
