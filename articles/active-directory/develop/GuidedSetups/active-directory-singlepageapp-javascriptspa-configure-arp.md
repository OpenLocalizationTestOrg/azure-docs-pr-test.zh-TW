---
title: "aaaAzure AD v2 JS SPA 引導式安裝-設定 (ARP) |Microsoft 文件"
description: "JavaScript SPA 應用程式如何呼叫需要來自 Azure Active Directory v2 端點 (ARP) 之存取權杖的 API"
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
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="1e56f-103">新增 hello 應用程式的註冊資訊 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="1e56f-103">Add hello application’s registration information tooyour App</span></span>

<span data-ttu-id="1e56f-104">在此步驟中，您會需要您的應用程式註冊資訊的 tooconfigure hello 重新導向 URL，然後再加入 hello 應用程式識別碼 tooyour JavaScript SPA 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e56f-104">In this step, you need tooconfigure hello Redirect URL of your application registration information and then add hello Application Id tooyour JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="1e56f-105">設定重新導向 URL</span><span class="sxs-lookup"><span data-stu-id="1e56f-105">Configure redirect URL</span></span>

<span data-ttu-id="1e56f-106">設定 hello`Redirect URL`欄位上方 hello index.html 網頁根據您的 web 伺服器的 url，然後按一下 *更新*。</span><span class="sxs-lookup"><span data-stu-id="1e56f-106">Configure hello `Redirect URL` field above with hello URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="1e56f-107">取得重新導向 URL 的 Visual Studio 指示</span><span class="sxs-lookup"><span data-stu-id="1e56f-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="1e56f-108">tooobtain 遵循下方的 hello 指示您重新導向 URL:</span><span class="sxs-lookup"><span data-stu-id="1e56f-108">tooobtain your redirect URL, follow hello instructions below:</span></span>
> 1.    <span data-ttu-id="1e56f-109">在*方案總管 中*選取 hello 專案，看看 hello`Properties`視窗 (如果您沒有看到 屬性 視窗，請按`F4`)</span><span class="sxs-lookup"><span data-stu-id="1e56f-109">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="1e56f-110">複製 hello 值從`URL`toohello 剪貼簿：</span><span class="sxs-lookup"><span data-stu-id="1e56f-110">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="1e56f-111">![專案屬性](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="1e56f-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="1e56f-112">貼上為 hello 值`Redirect URL`hello 這個頁面頂端，然後按一下`Update`</span><span class="sxs-lookup"><span data-stu-id="1e56f-112">Paste hello value as a `Redirect URL` on hello top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="1e56f-113">設定 Python 的重新導向 URL</span><span class="sxs-lookup"><span data-stu-id="1e56f-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="1e56f-114">對於 Python，您可以設定 hello web 伺服器連接埠，透過命令列。</span><span class="sxs-lookup"><span data-stu-id="1e56f-114">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="1e56f-115">此 「 引導式的安裝程式會使用 hello 連接埠 8080 的參考，但覺得可用 toouse 任何其他可用的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="1e56f-115">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="1e56f-116">在任何情況下，請遵循以下 tooset hello 應用程式註冊資訊的重新導向 URL 設定的 hello 指示：</span><span class="sxs-lookup"><span data-stu-id="1e56f-116">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> <span data-ttu-id="1e56f-117">設定`http://localhost:8080/`為`Redirect URL`在 hello 頂端的這個頁面上，或使用`http://localhost:[port]/`如果您使用自訂的 TCP 連接埠 (其中*[port]* hello 自訂 TCP 連接埠號碼)，然後按一下'Update'</span><span class="sxs-lookup"><span data-stu-id="1e56f-117">Set `http://localhost:8080/` as a `Redirect URL` on hello top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="1e56f-118">設定您的 JavaScript SPA 應用程式</span><span class="sxs-lookup"><span data-stu-id="1e56f-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="1e56f-119">建立名為`msalconfig.js`包含 hello 應用程式註冊資訊。</span><span class="sxs-lookup"><span data-stu-id="1e56f-119">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="1e56f-120">如果您使用 Visual Studio 中，選取 hello 專案 （專案根資料夾） 上按一下滑鼠右鍵，然後選取： `Add`  >  `New Item`  >  `JavaScript File`。</span><span class="sxs-lookup"><span data-stu-id="1e56f-120">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="1e56f-121">將它命名為 `msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="1e56f-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="1e56f-122">新增下列程式碼 tooyour hello`msalconfig.js`檔案：</span><span class="sxs-lookup"><span data-stu-id="1e56f-122">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
