---
title: "aaaAzure AD v2 JS SPA 引導式安裝-測試 |Microsoft 文件"
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
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="61dd5-103">測試您的程式碼</span><span class="sxs-lookup"><span data-stu-id="61dd5-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="61dd5-104">使用 Visual Studio 進行測試</span><span class="sxs-lookup"><span data-stu-id="61dd5-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="61dd5-105">如果您使用 Visual Studio，請按`F5`toorun 您的專案： hello 瀏覽器會開啟並引導您太*http://localhost: {port}*看 hello*呼叫 Microsoft Graph API* ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="61dd5-105">If you are using Visual Studio, press `F5` toorun your project: hello browser opens and directs you too*http://localhost:{port}* where you see hello *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="61dd5-106">使用 Python 或另一部 web 伺服器進行測試</span><span class="sxs-lookup"><span data-stu-id="61dd5-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="61dd5-107">如果您不使用 Visual Studio，請確定您的網頁伺服器已啟動，且設定 toolisten tooa TCP 連接埠會根據 hello 資料夾包含您*index.html*檔案。</span><span class="sxs-lookup"><span data-stu-id="61dd5-107">If you are not using Visual Studio, make sure your web server is started and it is configured toolisten tooa TCP port based on hello folder containing your *index.html* file.</span></span> <span data-ttu-id="61dd5-108">對於 Python，您可以開始接聽 toohello 連接埠執行 hello hello 命令提示 / 終端機，從 hello 應用程式資料夾中：</span><span class="sxs-lookup"><span data-stu-id="61dd5-108">For Python, you can start listening toohello port by running hello in hello command prompt/ terminal, from hello app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="61dd5-109">然後，開啟 [hello 瀏覽器並輸入*http://localhost:8080/<*或*http://localhost: {port}* -hello*連接埠*對應 toohello 網頁伺服器的連接埠接聽。</span><span class="sxs-lookup"><span data-stu-id="61dd5-109">Then, open hello browser and type *http://localhost:8080* or *http://localhost:{port}* - where hello *port* corresponds toohello port that your web server is listening to.</span></span> <span data-ttu-id="61dd5-110">您應該會看到 hello 的您 index.html 分頁內容以 hello*呼叫 Microsoft Graph API* ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="61dd5-110">You should see hello contents of your index.html page with hello *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="61dd5-111">測試您的應用程式</span><span class="sxs-lookup"><span data-stu-id="61dd5-111">Test your application</span></span>

<span data-ttu-id="61dd5-112">Hello 瀏覽器之後載入您*index.html*，按一下 hello*呼叫 Microsoft Graph API* ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="61dd5-112">After hello browser loads your *index.html*, click hello *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="61dd5-113">如果這是 hello 第一次，hello 瀏覽器重新導向您 Microsoft Azure Active Directory v2 toohello 端點，您所處提示 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="61dd5-113">If this is hello first time, hello browser redirects you toohello Microsoft Azure Active Directory v2 endpoint, where you are  prompted toosign in.</span></span>
 
![範例螢幕擷取畫面](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="61dd5-115">同意</span><span class="sxs-lookup"><span data-stu-id="61dd5-115">Consent</span></span>
<span data-ttu-id="61dd5-116">hello tooyour 應用程式，在您登入第一次您會看到同意畫面類似 toohello 下列程式碼，您需要 tooaccept:</span><span class="sxs-lookup"><span data-stu-id="61dd5-116">hello very first time you sign in tooyour application, you are presented with a consent screen similar toohello following, where you need tooaccept:</span></span>

 ![同意畫面](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="61dd5-118">預期的結果</span><span class="sxs-lookup"><span data-stu-id="61dd5-118">Expected results</span></span>
<span data-ttu-id="61dd5-119">您應該會看到 hello Microsoft Graph API 呼叫的回應所傳回的使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="61dd5-119">You should see user profile information returned by hello Microsoft Graph API call response.</span></span>
 
 ![結果](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="61dd5-121">另請參閱在 hello hello 權杖的基本資訊*存取權杖*和*識別碼權杖宣告*方塊。</span><span class="sxs-lookup"><span data-stu-id="61dd5-121">You also see basic information about hello token acquired in hello *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="61dd5-122">與範圍和委派的權限有關的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="61dd5-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="61dd5-123">hello Microsoft Graph API 需要 hello`user.read`範圍 tooread hello 使用者的設定檔。</span><span class="sxs-lookup"><span data-stu-id="61dd5-123">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="61dd5-124">根據預設值，在我們註冊入口網站上註冊的每個應用程式中都會自動新增此範圍。</span><span class="sxs-lookup"><span data-stu-id="61dd5-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="61dd5-125">Microsoft Graph 的某些其他 API 與您後端伺服器的自訂 API 一樣，需要其他範圍。</span><span class="sxs-lookup"><span data-stu-id="61dd5-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="61dd5-126">例如，針對 Microsoft Graph hello 範圍`Calendars.Read`是必要的 toolist hello 使用者的行事曆。</span><span class="sxs-lookup"><span data-stu-id="61dd5-126">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="61dd5-127">順序 tooaccess hello hello 應用程式內容中的使用者的行事曆，您需要 tooadd hello`Calendars.Read`委派權限 toohello 應用程式註冊的資訊，然後再加入 hello`Calendars.Read`範圍 toohello`acquireTokenSilent`呼叫。</span><span class="sxs-lookup"><span data-stu-id="61dd5-127">In order tooaccess hello user’s calendar in hello context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="61dd5-128">隨著您增加 hello 範圍數目，可能會提示 hello 使用者輸入其他的同意授權。</span><span class="sxs-lookup"><span data-stu-id="61dd5-128">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<span data-ttu-id="61dd5-129">如果後端 API 不需要的範圍 （不建議），您可以使用 hello`clientId`成 hello 範圍： hello`acquireTokenSilent`及/或`acquireTokenRedirect`呼叫。</span><span class="sxs-lookup"><span data-stu-id="61dd5-129">If a backend API does not require a scope (not recommended), you can use hello `clientId` as hello scope in hello `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
