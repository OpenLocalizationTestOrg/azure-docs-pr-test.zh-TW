---
title: "Azure AD v2 JS SPA 指引設定 - 設定 (ARP) | Microsoft Docs"
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
ms.openlocfilehash: 708f4ff606d79639de979918a9cacd4ed75db311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="1be30-103">將應用程式的註冊資訊新增到您的應用程式</span><span class="sxs-lookup"><span data-stu-id="1be30-103">Add the application’s registration information to your App</span></span>

<span data-ttu-id="1be30-104">在此步驟中，您需要設定應用程式註冊資訊的重新導向 URL，然後將應用程式識別碼新增至 JavaScript SPA 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1be30-104">In this step, you need to configure the Redirect URL of your application registration information and then add the Application Id to your JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="1be30-105">設定重新導向 URL</span><span class="sxs-lookup"><span data-stu-id="1be30-105">Configure redirect URL</span></span>

<span data-ttu-id="1be30-106">使用以您的 Web 伺服器為基礎的 index.html 網頁 URL 設定上述 `Redirect URL` 欄位，然後按一下 [更新]。</span><span class="sxs-lookup"><span data-stu-id="1be30-106">Configure the `Redirect URL` field above with the URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="1be30-107">取得重新導向 URL 的 Visual Studio 指示</span><span class="sxs-lookup"><span data-stu-id="1be30-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="1be30-108">若要取得重新導向 URL，請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="1be30-108">To obtain your redirect URL, follow the instructions below:</span></span>
> 1.    <span data-ttu-id="1be30-109">在「方案總管」中，選取專案並查看 `Properties` 視窗 (如果您沒有看到屬性視窗，請按 `F4`)</span><span class="sxs-lookup"><span data-stu-id="1be30-109">In *Solution Explorer*, select the project and look at the `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="1be30-110">將此值從 `URL` 複製到剪貼簿：</span><span class="sxs-lookup"><span data-stu-id="1be30-110">Copy the value from `URL` to the clipboard:</span></span><br/> <span data-ttu-id="1be30-111">![專案屬性](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="1be30-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="1be30-112">貼上此值作為此分頁頂端的 `Redirect URL`，然後按一下 `Update`</span><span class="sxs-lookup"><span data-stu-id="1be30-112">Paste the value as a `Redirect URL` on the top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="1be30-113">設定 Python 的重新導向 URL</span><span class="sxs-lookup"><span data-stu-id="1be30-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="1be30-114">對於 Python，您可以透過命令列設定 Web 伺服器連接埠。</span><span class="sxs-lookup"><span data-stu-id="1be30-114">For Python, you can set the web server port via command line.</span></span> <span data-ttu-id="1be30-115">此指引設定會使用連接埠 8080 作為參考，但是可以隨意使用任何其他可用的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="1be30-115">This guided setup uses the port 8080 for reference but feel free to use any other port available.</span></span> <span data-ttu-id="1be30-116">在任何情況下，請遵循下列指示以在應用程式註冊資訊中設定重新導向 URL：</span><span class="sxs-lookup"><span data-stu-id="1be30-116">In any case, follow the instructions below to set up a redirect URL in the application registration information:</span></span><br/>
> <span data-ttu-id="1be30-117">設定 `http://localhost:8080/` 作為此分頁頂端的 `Redirect URL`，或者如果您使用自訂 TCP 連接埠，則使用 `http://localhost:[port]/` (其中 [port] 是自訂 TCP 通訊埠號碼)，然後按一下 [更新]</span><span class="sxs-lookup"><span data-stu-id="1be30-117">Set `http://localhost:8080/` as a `Redirect URL` on the top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is the custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="1be30-118">設定您的 JavaScript SPA 應用程式</span><span class="sxs-lookup"><span data-stu-id="1be30-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="1be30-119">建立名為 `msalconfig.js` 的檔案，其中包含應用程式註冊資訊。</span><span class="sxs-lookup"><span data-stu-id="1be30-119">Create a file named `msalconfig.js` containing the application registration information.</span></span> <span data-ttu-id="1be30-120">如果您使用 Visual Studio，請選取專案 (專案根資料夾)，以滑鼠右鍵按一下並選取：`Add` > `New Item` > `JavaScript File`。</span><span class="sxs-lookup"><span data-stu-id="1be30-120">If you are using Visual Studio, select the project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="1be30-121">將它命名為 `msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="1be30-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="1be30-122">將下列程式碼新增至 `msalconfig.js` 檔案：</span><span class="sxs-lookup"><span data-stu-id="1be30-122">Add the following code to your `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter the application Id here]",
    redirectUri: location.origin
};
``` 
