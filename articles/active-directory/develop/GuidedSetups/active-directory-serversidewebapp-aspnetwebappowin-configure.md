---
title: "aaaAzure AD v2 ASP.NET Web 伺服器快速入門-Config |Microsoft 文件"
description: "使用 OpenID Connect 標準，搭配傳統網頁瀏覽器型應用程式，在 ASP.NET 方案上實作 Microsoft 登入"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="9c4e5-103">建立應用程式 (快速)</span><span class="sxs-lookup"><span data-stu-id="9c4e5-103">Create an application (Express)</span></span>
<span data-ttu-id="9c4e5-104">現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:</span><span class="sxs-lookup"><span data-stu-id="9c4e5-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="9c4e5-105">註冊您的應用程式，透過 hello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="9c4e5-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="9c4e5-106">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="9c4e5-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="9c4e5-107">請確定已選取 hello 引導式安裝選項</span><span class="sxs-lookup"><span data-stu-id="9c4e5-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="9c4e5-108">請遵循 hello 指示 tooadd 重新導向 URL tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="9c4e5-108">Follow hello instructions tooadd a Redirect URL tooyour application</span></span>

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="9c4e5-109">新增應用程式註冊資訊 tooyour 方案 （進階）</span><span class="sxs-lookup"><span data-stu-id="9c4e5-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="9c4e5-110">現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:</span><span class="sxs-lookup"><span data-stu-id="9c4e5-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="9c4e5-111">移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app)tooregister 應用程式</span><span class="sxs-lookup"><span data-stu-id="9c4e5-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="9c4e5-112">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="9c4e5-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="9c4e5-113">請確定未引導式的安裝程式的 hello 選項</span><span class="sxs-lookup"><span data-stu-id="9c4e5-113">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="9c4e5-114">按一下 `Add Platform`，然後選取 `Web`</span><span class="sxs-lookup"><span data-stu-id="9c4e5-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="9c4e5-115">返回 tooVisual Studio，在 方案總管 中，選取 hello 專案並查看 hello 屬性 視窗 （如果您沒有看到 屬性 視窗中，按 F4）</span><span class="sxs-lookup"><span data-stu-id="9c4e5-115">Go back tooVisual Studio and, in Solution Explorer, select hello project and look at hello Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="9c4e5-116">也變更啟用 SSL`True`</span><span class="sxs-lookup"><span data-stu-id="9c4e5-116">Change SSL Enabled too`True`</span></span>
7.  <span data-ttu-id="9c4e5-117">複製 hello SSL URL，並將此 URL toohello 清單的重新導向 Url 的重新導向 Url 的 hello 註冊入口網站的清單中：</span><span class="sxs-lookup"><span data-stu-id="9c4e5-117">Copy hello SSL URL and add this URL toohello list of Redirect URLs in hello Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![專案屬性](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="9c4e5-119">新增中的 hello 下列`web.config`hello hello 區段下方的根資料夾中`configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="9c4e5-119">Add hello following in `web.config` located in hello root folder under hello section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="9c4e5-120">取代`ClientId`以 hello 您剛登錄的應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="9c4e5-120">Replace `ClientId` with hello Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="9c4e5-121">取代`redirectUri`以 hello 專案的 SSL URL</span><span class="sxs-lookup"><span data-stu-id="9c4e5-121">Replace `redirectUri` with hello SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
