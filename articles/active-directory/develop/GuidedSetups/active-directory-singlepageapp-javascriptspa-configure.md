---
title: "aaaAzure AD v2 JS SPA 引導式安裝-設定 |Microsoft 文件"
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
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a><span data-ttu-id="127e5-103">註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="127e5-103">Register your application</span></span>

<span data-ttu-id="127e5-104">有多個方式 toocreate 應用程式，請選取其中一個：</span><span class="sxs-lookup"><span data-stu-id="127e5-104">There are multiple ways toocreate an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="127e5-105">選項 1：註冊您的應用程式 (快速模式)</span><span class="sxs-lookup"><span data-stu-id="127e5-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="127e5-106">現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:</span><span class="sxs-lookup"><span data-stu-id="127e5-106">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="127e5-107">註冊您的應用程式，透過 hello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="127e5-107">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="127e5-108">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="127e5-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="127e5-109">請確定 hello 選項*引導式安裝*會檢查</span><span class="sxs-lookup"><span data-stu-id="127e5-109">Make sure hello option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="127e5-110">遵循 hello 指示 tooobtain hello 應用程式識別碼，並將它貼到您的程式碼</span><span class="sxs-lookup"><span data-stu-id="127e5-110">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="127e5-111">選項 2：註冊您的應用程式 (進階模式)</span><span class="sxs-lookup"><span data-stu-id="127e5-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="127e5-112">移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app)tooregister 應用程式</span><span class="sxs-lookup"><span data-stu-id="127e5-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="127e5-113">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="127e5-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="127e5-114">請確定 hello 選項*引導式安裝*未選取</span><span class="sxs-lookup"><span data-stu-id="127e5-114">Make sure hello option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="127e5-115">按一下 `Add Platform`，然後選取 `Web`</span><span class="sxs-lookup"><span data-stu-id="127e5-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="127e5-116">新增 hello`Redirect URL`對應 toohello 應用程式的 URL，根據您的 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="127e5-116">Add hello `Redirect URL` that correspond toohello application's URL based on your web server.</span></span> <span data-ttu-id="127e5-117">請參閱 hello 下列各節以指示 tooset / 取得 Visual Studio 和 Python 中的 hello 重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="127e5-117">See hello sections below for instructions on how tooset/ obtain hello redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="127e5-118">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="127e5-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="127e5-119">取得重新導向 URL 的 Visual Studio 指示</span><span class="sxs-lookup"><span data-stu-id="127e5-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="127e5-120">請依照下列 hello 指示 tooobtain 重新導向 URL:</span><span class="sxs-lookup"><span data-stu-id="127e5-120">Follow hello instructions tooobtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="127e5-121">在*方案總管 中*選取 hello 專案，看看 hello`Properties`視窗 (如果您沒有看到 屬性 視窗，請按`F4`)</span><span class="sxs-lookup"><span data-stu-id="127e5-121">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="127e5-122">複製 hello 值從`URL`toohello 剪貼簿：</span><span class="sxs-lookup"><span data-stu-id="127e5-122">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="127e5-123">![專案屬性](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="127e5-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="127e5-124">切換後 toohello*應用程式註冊入口網站*貼上為 hello 值`Redirect URL`，按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="127e5-124">Switch back toohello *Application Registration Portal* and paste hello value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="127e5-125">設定 Python 的重新導向 URL</span><span class="sxs-lookup"><span data-stu-id="127e5-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="127e5-126">對於 Python，您可以設定 hello web 伺服器連接埠，透過命令列。</span><span class="sxs-lookup"><span data-stu-id="127e5-126">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="127e5-127">此 「 引導式的安裝程式會使用 hello 連接埠 8080 的參考，但覺得可用 toouse 任何其他可用的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="127e5-127">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="127e5-128">在任何情況下，請遵循以下 tooset hello 應用程式註冊資訊的重新導向 URL 設定的 hello 指示：</span><span class="sxs-lookup"><span data-stu-id="127e5-128">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> - <span data-ttu-id="127e5-129">切換後 toohello*應用程式註冊入口網站*並設定`http://localhost:8080/`為`Redirect URL`，或使用`http://localhost:[port]/`如果您使用自訂的 TCP 連接埠 (其中*[port]*為 hello 自訂 TCP 通訊埠數字），按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="127e5-129">Switch back toohello *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="127e5-130">設定您的 JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="127e5-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="127e5-131">建立名為`msalconfig.js`包含 hello 應用程式註冊資訊。</span><span class="sxs-lookup"><span data-stu-id="127e5-131">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="127e5-132">如果您使用 Visual Studio 中，選取 hello 專案 （專案根資料夾） 上按一下滑鼠右鍵，然後選取： `Add`  >  `New Item`  >  `JavaScript File`。</span><span class="sxs-lookup"><span data-stu-id="127e5-132">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="127e5-133">將它命名為 `msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="127e5-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="127e5-134">新增下列程式碼 tooyour hello`msalconfig.js`檔案：</span><span class="sxs-lookup"><span data-stu-id="127e5-134">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="127e5-135">取代<code>Enter_the_Application_Id_here</code>以 hello 您剛登錄的應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="127e5-135">Replace <code>Enter_the_Application_Id_here</code> with hello Application Id you just registered</span></span>
</li>
</ol>
