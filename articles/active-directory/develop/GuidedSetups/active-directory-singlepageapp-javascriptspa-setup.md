---
title: "aaaAzure AD v2 JS SPA 引導式安裝程式-安裝 |Microsoft 文件"
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
ms.openlocfilehash: 19e15c6c8db8bea2975f30e7505af79ccad17e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-web-server-or-project"></a><span data-ttu-id="d01f1-103">設定您的 Web 伺服器或專案</span><span class="sxs-lookup"><span data-stu-id="d01f1-103">Setting up your web server or project</span></span>

> <span data-ttu-id="d01f1-104">改為偏好 toodownload 這個範例專案嗎？</span><span class="sxs-lookup"><span data-stu-id="d01f1-104">Prefer toodownload this sample's project instead?</span></span> 
> - [<span data-ttu-id="d01f1-105">下載 hello Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="d01f1-105">Download hello Visual Studio project</span></span>](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> <span data-ttu-id="d01f1-106">或</span><span class="sxs-lookup"><span data-stu-id="d01f1-106">or</span></span>
> - <span data-ttu-id="d01f1-107">[下載 hello 專案檔](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip)的本機 web 伺服器，例如 Python</span><span class="sxs-lookup"><span data-stu-id="d01f1-107">[Download hello project files](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) for a local web server, such as Python</span></span>
>
> <span data-ttu-id="d01f1-108">然後略過 toohello[組態步驟](#create-an-application-express)tooconfigure hello 程式碼範例，然後再執行它。</span><span class="sxs-lookup"><span data-stu-id="d01f1-108">And then  skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d01f1-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="d01f1-109">Prerequisites</span></span>
<span data-ttu-id="d01f1-110">本機 web 伺服器這類[Python http.server](https://www.python.org/downloads/)， [http 伺服器](https://www.npmjs.com/package/http-server/)， [.NET Core](https://www.microsoft.com/net/core)，或與 IIS Express 整合[Visual Studio 2017](https://www.visualstudio.com/downloads/)是必要的 toorun 此引導式的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="d01f1-110">A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required toorun this guided setup.</span></span> 

<span data-ttu-id="d01f1-111">本指南中的指示為基礎的 Python 和 Visual Studio 2017，但覺得可用 toouse，任何其他開發環境或 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d01f1-111">Instructions in this guide are based on both Python and Visual Studio 2017, but feel free toouse any other development environment or Web Server.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="d01f1-112">建立專案</span><span class="sxs-lookup"><span data-stu-id="d01f1-112">Create your project</span></span> 

> ### <a name="option-1-visual-studio"></a><span data-ttu-id="d01f1-113">選項 1：Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d01f1-113">Option 1: Visual Studio</span></span> 
> <span data-ttu-id="d01f1-114">如果您使用 Visual Studio 並建立新的專案，請遵循下列 toocreate 新的 Visual Studio 方案的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="d01f1-114">If you are using Visual Studio and are creating a new project, follow hello steps below toocreate a new Visual Studio solution:</span></span>
> 1.    <span data-ttu-id="d01f1-115">在 Visual Studio 中：`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="d01f1-115">In Visual Studio:  `File` > `New` > `Project`</span></span>
> 2.    <span data-ttu-id="d01f1-116">在 `Visual C#\Web` 之下選取 `ASP.NET Web Application (.NET Framework)`</span><span class="sxs-lookup"><span data-stu-id="d01f1-116">Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`</span></span>
> 3.    <span data-ttu-id="d01f1-117">為您的應用程式命名並按一下 [確定]</span><span class="sxs-lookup"><span data-stu-id="d01f1-117">Name your application and click *OK*</span></span>
> 4.    <span data-ttu-id="d01f1-118">在 `New ASP.NET Web Application` 之下選取 `Empty`</span><span class="sxs-lookup"><span data-stu-id="d01f1-118">Under `New ASP.NET Web Application`, select `Empty`</span></span>

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a><span data-ttu-id="d01f1-119">選項 2：Python/其他網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="d01f1-119">Option 2: Python/ other web servers</span></span>
> <span data-ttu-id="d01f1-120">請確定您已安裝[Python](https://www.python.org/downloads/)，然後依照以下的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="d01f1-120">Make sure you have installed [Python](https://www.python.org/downloads/), then follow hello step below:</span></span>
> - <span data-ttu-id="d01f1-121">建立資料夾 toohost 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d01f1-121">Create a folder toohost your application.</span></span>


## <a name="create-your-single-page-applications-ui"></a><span data-ttu-id="d01f1-122">建立單一頁面應用程式的 UI</span><span class="sxs-lookup"><span data-stu-id="d01f1-122">Create your single page application’s UI</span></span>
1.  <span data-ttu-id="d01f1-123">為您的 JavaScript SPA 建立 *index.html* 檔案。</span><span class="sxs-lookup"><span data-stu-id="d01f1-123">Create an *index.html* file for your JavaScript SPA.</span></span> <span data-ttu-id="d01f1-124">如果您使用 Visual Studio 中，選取 hello 專案 （專案根資料夾中），以滑鼠右鍵按一下，然後選取： `Add`  >  `New Item`  >  `HTML page`並將它命名為 index.html</span><span class="sxs-lookup"><span data-stu-id="d01f1-124">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `HTML page` and name it index.html</span></span>
2.  <span data-ttu-id="d01f1-125">加入下列程式碼 tooyour 頁面 hello:</span><span class="sxs-lookup"><span data-stu-id="d01f1-125">Add hello following code tooyour page:</span></span>
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling hello page -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <title>JavaScript SPA Guided Setup</title>
</head>
<body style="margin: 40px">
    <button id="callGraphButton" type="button" class="btn btn-primary" onclick="callGraphApi()">Call Microsoft Graph API</button>
    <div id="errorMessage" class="text-danger"></div>
    <div class="hidden">
        <h3>Graph API Call Response</h3>
        <pre class="well" id="graphResponse"></pre>
    </div>
    <div class="hidden">
        <h3>Access Token</h3>
        <pre class="well" id="accessToken"></pre>
    </div>
    <div class="hidden">
        <h3>ID Token Claims</h3>
        <pre class="well" id="userInfo"></pre>
    </div>
    <button id="signOutButton" type="button" class="btn btn-primary hidden" onclick="signOut()">Sign out</button>

    <!-- This app uses cdn tooreference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- hello 'bluebird' and 'fetch' references below are required if you need toorun this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
