---
title: "Azure AD v2 JS SPA 指引設定 - 測試 | Microsoft Docs"
description: "JavaScript SPA 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: c888760ab311e8ac08b1e625bb837f91047db645
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
## <a name="test-your-code"></a><span data-ttu-id="5aac4-103">測試您的程式碼</span><span class="sxs-lookup"><span data-stu-id="5aac4-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="5aac4-104">使用 Visual Studio 進行測試</span><span class="sxs-lookup"><span data-stu-id="5aac4-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="5aac4-105">如果您使用 Visual Studio，請按 `F5` 來執行您的專案：瀏覽器會開啟並將您導引至 http://localhost:{port}，您會在其中看見 [呼叫 Microsoft Graph API] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5aac4-105">If you are using Visual Studio, press `F5` to run your project: the browser opens and directs you to *http://localhost:{port}* where you see the *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="5aac4-106">使用 Python 或另一部 web 伺服器進行測試</span><span class="sxs-lookup"><span data-stu-id="5aac4-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="5aac4-107">如果您不是使用 Visual Studio，請確定您的 Web 伺服器已啟動，而且已設定為接聽 TCP 連接埠 (以含有 index.html 檔案的資料夾為基礎)。</span><span class="sxs-lookup"><span data-stu-id="5aac4-107">If you are not using Visual Studio, make sure your web server is started and it is configured to listen to a TCP port based on the folder containing your *index.html* file.</span></span> <span data-ttu-id="5aac4-108">對於 Python，您可以在命令提示字元 / 終端機從應用程式的資料夾執行，開始接聽此連接埠：</span><span class="sxs-lookup"><span data-stu-id="5aac4-108">For Python, you can start listening to the port by running the in the command prompt/ terminal, from the app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="5aac4-109">然後，開啟瀏覽器並輸入 http://localhost:8080 或 http://localhost:{port} - 其中的 port 對應至您的 Web 伺服器正在接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="5aac4-109">Then, open the browser and type *http://localhost:8080* or *http://localhost:{port}* - where the *port* corresponds to the port that your web server is listening to.</span></span> <span data-ttu-id="5aac4-110">使用 [呼叫 Microsoft Graph API] 按鈕，您應會看到 index.html 頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="5aac4-110">You should see the contents of your index.html page with the *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="5aac4-111">測試您的應用程式</span><span class="sxs-lookup"><span data-stu-id="5aac4-111">Test your application</span></span>

<span data-ttu-id="5aac4-112">在瀏覽器載入您的 index.html 之後，按一下 [呼叫 Microsoft Graph API] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5aac4-112">After the browser loads your *index.html*, click the *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="5aac4-113">如果這是第一次，瀏覽器會將您重新導向到 Microsoft Azure Active Directory v2 端點，系統會在此提示您登入。</span><span class="sxs-lookup"><span data-stu-id="5aac4-113">If this is the first time, the browser redirects you to the Microsoft Azure Active Directory v2 endpoint, where you are  prompted to sign in.</span></span>
 
![範例螢幕擷取畫面](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="5aac4-115">同意</span><span class="sxs-lookup"><span data-stu-id="5aac4-115">Consent</span></span>
<span data-ttu-id="5aac4-116">第一次登入應用程式時，系統會顯示如下所示的類似同意畫面，其中包含您必須接受的事項：</span><span class="sxs-lookup"><span data-stu-id="5aac4-116">The very first time you sign in to your application, you are presented with a consent screen similar to the following, where you need to accept:</span></span>

 ![同意畫面](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="5aac4-118">預期的結果</span><span class="sxs-lookup"><span data-stu-id="5aac4-118">Expected results</span></span>
<span data-ttu-id="5aac4-119">您應該會看到 Microsoft Graph API 回應所傳回的使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="5aac4-119">You should see user profile information returned by the Microsoft Graph API call response.</span></span>
 
 ![結果](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="5aac4-121">您也會在 [存取權杖] 和 [ID 權杖宣告] 方塊中看到取得之權杖的相關基本資訊。</span><span class="sxs-lookup"><span data-stu-id="5aac4-121">You also see basic information about the token acquired in the *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="5aac4-122">與範圍和委派的權限有關的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="5aac4-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="5aac4-123">Microsoft Graph API 需要 `user.read` 範圍以讀取使用者的設定檔。</span><span class="sxs-lookup"><span data-stu-id="5aac4-123">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="5aac4-124">根據預設值，在我們註冊入口網站上註冊的每個應用程式中都會自動新增此範圍。</span><span class="sxs-lookup"><span data-stu-id="5aac4-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="5aac4-125">Microsoft Graph 的某些其他 API 與您後端伺服器的自訂 API 一樣，需要其他範圍。</span><span class="sxs-lookup"><span data-stu-id="5aac4-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="5aac4-126">例如，針對 Microsoft Graph，需要範圍 `Calendars.Read` 才能列出使用者的行事曆。</span><span class="sxs-lookup"><span data-stu-id="5aac4-126">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="5aac4-127">為了在應用程式內容中存取使用者的行事曆，您需要將 `Calendars.Read` 委派權限新增至應用程式註冊的資訊，然後將 `Calendars.Read` 範圍新增至 `acquireTokenSilent` 呼叫。</span><span class="sxs-lookup"><span data-stu-id="5aac4-127">In order to access the user’s calendar in the context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="5aac4-128">系統可能會在您增加範圍數目時，提示使用者同意其他事項。</span><span class="sxs-lookup"><span data-stu-id="5aac4-128">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<span data-ttu-id="5aac4-129">如果後端 API 不需要範圍 (不建議)，您可以在 `acquireTokenSilent` 和/或 `acquireTokenRedirect` 呼叫中使用 `clientId` 作為範圍。</span><span class="sxs-lookup"><span data-stu-id="5aac4-129">If a backend API does not require a scope (not recommended), you can use the `clientId` as the scope in the `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
