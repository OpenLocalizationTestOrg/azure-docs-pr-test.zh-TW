---
title: "aaaProtect Web API 後端 API 管理 Azure Active Directory 與 |Microsoft 文件"
description: "深入了解如何 tooprotect Web API 後端 API 管理與 Azure Active Directory。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="a078d-103">如何 tooprotect Web API 後端，使用 Azure Active Directory 與 API 管理</span><span class="sxs-lookup"><span data-stu-id="a078d-103">How tooprotect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="a078d-104">hello 下列影片示範如何 toobuild Web API 後端，然後使用 Azure Active Directory 與 API 管理使用 OAuth 2.0 通訊協定加以保護。</span><span class="sxs-lookup"><span data-stu-id="a078d-104">hello following video shows how toobuild a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="a078d-105">本文章提供概觀和步驟 hello 視訊中的 hello 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="a078d-105">This article provides an overview and additional information for hello steps in hello video.</span></span> <span data-ttu-id="a078d-106">這段 24 分鐘的視訊示範如何：</span><span class="sxs-lookup"><span data-stu-id="a078d-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="a078d-107">使用 AAD 建置 Web API 後端以及保護安全 - 從 1:30 開始</span><span class="sxs-lookup"><span data-stu-id="a078d-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="a078d-108">Hello API 匯入 API 管理-開始 7:10</span><span class="sxs-lookup"><span data-stu-id="a078d-108">Import hello API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="a078d-109">設定 hello 開發人員入口網站 toocall hello API-開始 9:09</span><span class="sxs-lookup"><span data-stu-id="a078d-109">Configure hello Developer portal toocall hello API - starting at 9:09</span></span>
* <span data-ttu-id="a078d-110">設定桌面應用程式 toocall hello API-開始 18:08</span><span class="sxs-lookup"><span data-stu-id="a078d-110">Configure a desktop application toocall hello API - starting at 18:08</span></span>
* <span data-ttu-id="a078d-111">設定 JWT 驗證原則 toopre-授權要求數-開始 20:47</span><span class="sxs-lookup"><span data-stu-id="a078d-111">Configure a JWT validation policy toopre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="a078d-112">建立 Azure AD 目錄</span><span class="sxs-lookup"><span data-stu-id="a078d-112">Create an Azure AD directory</span></span>
<span data-ttu-id="a078d-113">使用 Azure Active Directory 必須先備份您的 Web API 的 toosecure AAD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="a078d-113">toosecure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="a078d-114">在這段視訊中，使用名為 **APIMDemo** 的租用戶。</span><span class="sxs-lookup"><span data-stu-id="a078d-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="a078d-115">toocreate AAD 租用戶登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)按一下**新增**->**應用程式服務**->**Active目錄**->**目錄**->**自訂建立**。</span><span class="sxs-lookup"><span data-stu-id="a078d-115">toocreate an AAD tenant, sign-in toohello [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="a078d-117">此範例會一同建立名為 **APIMDemo** 的目錄與名為 **DemoAPIM.onmicrosoft.com** 的預設網域。這個目錄會使用整個 hello 視訊。</span><span class="sxs-lookup"><span data-stu-id="a078d-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**. This directory is used throughout hello video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="a078d-119">建立由 Azure Active Directory 保護的 Web API 服務</span><span class="sxs-lookup"><span data-stu-id="a078d-119">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="a078d-120">在此步驟中，Web API 後端會使用 Visual Studio 2013 建立。</span><span class="sxs-lookup"><span data-stu-id="a078d-120">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="a078d-121">Hello 視訊的這個步驟會在 1:30。</span><span class="sxs-lookup"><span data-stu-id="a078d-121">This step of hello video starts at 1:30.</span></span> <span data-ttu-id="a078d-122">toocreate Web API 後端專案在 Visual Studio 中，按一下**檔案**->**新增**->**專案**，然後選擇  **ASP.NET 網頁應用程式**從 hello **Web**範本清單。</span><span class="sxs-lookup"><span data-stu-id="a078d-122">toocreate Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from hello **Web** templates list.</span></span> <span data-ttu-id="a078d-123">在這個視訊 hello 專案命名為**APIMAADDemo**。</span><span class="sxs-lookup"><span data-stu-id="a078d-123">In this video hello project is named **APIMAADDemo**.</span></span> <span data-ttu-id="a078d-124">按一下**確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="a078d-124">Click **OK** toocreate hello project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="a078d-126">按一下**Web API**從 hello**從範本清單中選取**toocreate Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="a078d-126">Click **Web API** from hello **Select a template list** toocreate a Web API project.</span></span> <span data-ttu-id="a078d-127">按一下 Azure Directory Authentication tooconfigure**變更驗證**。</span><span class="sxs-lookup"><span data-stu-id="a078d-127">tooconfigure Azure Directory Authentication click **Change Authentication**.</span></span>

![新增專案][api-management-new-project]

<span data-ttu-id="a078d-129">按一下**組織帳戶**，並指定 hello**網域**的 AAD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="a078d-129">Click **Organizational Accounts**, and specify hello **Domain** of your AAD tenant.</span></span> <span data-ttu-id="a078d-130">在此範例 hello 網域是**DemoAPIM.onmicrosoft.com**。 您可以從 hello 取得您目錄中的 hello 網域**網域**您目錄的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a078d-130">In this example hello domain is **DemoAPIM.onmicrosoft.com**. hello domain of your directory can be obtained from hello **Domains** tab of your directory.</span></span>

![網域][api-management-aad-domains]

<span data-ttu-id="a078d-132">在 hello 中設定所需的 hello**變更驗證**對話方塊，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a078d-132">Configure hello desired settings in hello **Change Authentication** dialog box and click **OK**.</span></span>

![變更驗證][api-management-change-authentication]

<span data-ttu-id="a078d-134">當您按一下**確定**Visual Studio 將會嘗試 tooregister 應用程式與 Azure AD 目錄，而且可能會提示的 toosign 中由 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a078d-134">When you click **OK** Visual Studio will attempt tooregister your application with your Azure AD directory and you may be prompted toosign in by Visual Studio.</span></span> <span data-ttu-id="a078d-135">使用您目錄的系統管理帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="a078d-135">Sign in using an administrative account for your directory.</span></span>

![登入 tooVisual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="a078d-137">tooconfigure 這個專案與 Azure Web 應用程式開發介面檢查 hello 方塊**hello 雲端中的主機**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a078d-137">tooconfigure this project as an Azure Web API check hello box for **Host in hello cloud** and then click **OK**.</span></span>

![新增專案][api-management-new-project-cloud]

<span data-ttu-id="a078d-139">您可能會提示的 toosign tooAzure 中,，然後您可以設定 hello Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a078d-139">You may be prompted toosign in tooAzure, and then you can configure hello Web App.</span></span>

![設定][api-management-configure-web-app]

<span data-ttu-id="a078d-141">此範例指定了一個名為 **APIMAADDemo** 的新 **App Service 方案**。</span><span class="sxs-lookup"><span data-stu-id="a078d-141">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="a078d-142">按一下**確定**tooconfigure hello Web 應用程式，並建立 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="a078d-142">Click **OK** tooconfigure hello Web App and create hello project.</span></span>

## <a name="add-hello-code-toohello-web-api-project"></a><span data-ttu-id="a078d-143">新增 hello 程式碼 toohello Web API 專案</span><span class="sxs-lookup"><span data-stu-id="a078d-143">Add hello code toohello Web API project</span></span>
<span data-ttu-id="a078d-144">hello hello 視訊中的下一個步驟將加入 hello 程式碼 toohello Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="a078d-144">hello next step in hello video adds hello code toohello Web API project.</span></span> <span data-ttu-id="a078d-145">這個步驟從 4:35 開始。</span><span class="sxs-lookup"><span data-stu-id="a078d-145">This step starts at 4:35.</span></span>

<span data-ttu-id="a078d-146">在此範例中的 hello Web API 實作使用模型和控制器的基本計算機服務。</span><span class="sxs-lookup"><span data-stu-id="a078d-146">hello Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="a078d-147">tooadd hello 模型 hello 服務，以滑鼠右鍵按一下**模型**中**方案總管 中**選擇**新增**，**類別**。</span><span class="sxs-lookup"><span data-stu-id="a078d-147">tooadd hello model for hello service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="a078d-148">Hello 類別命名`CalcInput`按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a078d-148">Name hello class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="a078d-149">新增下列 hello`using`陳述式 toohello 頂端 hello`CalcInput.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="a078d-149">Add hello following `using` statement toohello top of hello `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="a078d-150">取代下列程式碼的 hello hello 產生類別。</span><span class="sxs-lookup"><span data-stu-id="a078d-150">Replace hello generated class with hello following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="a078d-151">以滑鼠右鍵按一下 [方案總管] 中的 [控制器]，然後選擇 [新增] -> [控制器]。</span><span class="sxs-lookup"><span data-stu-id="a078d-151">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="a078d-152">按一下 [Web API 2 控制器 - 空白]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a078d-152">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="a078d-153">型別**CalcController** hello 控制器命名，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a078d-153">Type **CalcController** for hello Controller name and click **Add**.</span></span>

![新增控制器][api-management-add-controller]

<span data-ttu-id="a078d-155">新增下列 hello`using`陳述式 toohello 頂端 hello`CalcController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="a078d-155">Add hello following `using` statement toohello top of hello `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="a078d-156">取代下列程式碼的 hello hello 產生控制器類別。</span><span class="sxs-lookup"><span data-stu-id="a078d-156">Replace hello generated controller class with hello following code.</span></span> <span data-ttu-id="a078d-157">此程式碼會實作 hello `Add`， `Subtract`， `Multiply`，和`Divide`hello 基本計算機 API 的作業。</span><span class="sxs-lookup"><span data-stu-id="a078d-157">This code implements hello `Add`, `Subtract`, `Multiply`, and `Divide` operations of hello Basic Calculator API.</span></span>

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

<span data-ttu-id="a078d-158">按**F6** toobuild 及驗證 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="a078d-158">Press **F6** toobuild and verify hello solution.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="a078d-159">發行 hello 專案 tooAzure</span><span class="sxs-lookup"><span data-stu-id="a078d-159">Publish hello project tooAzure</span></span>
<span data-ttu-id="a078d-160">這個步驟 hello Visual Studio 專案是發行的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="a078d-160">In this step hello Visual Studio project is published tooAzure.</span></span> <span data-ttu-id="a078d-161">此步驟的視訊 hello 開頭 5:45。</span><span class="sxs-lookup"><span data-stu-id="a078d-161">This step of hello video starts at 5:45.</span></span>

<span data-ttu-id="a078d-162">toopublish hello 專案 tooAzure、 以滑鼠右鍵按一下 hello **APIMAADDemo**專案在 Visual Studio 中，選擇**發行**。</span><span class="sxs-lookup"><span data-stu-id="a078d-162">toopublish hello project tooAzure, right-click hello **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="a078d-163">保持 hello hello 預設設定**發行 Web**對話方塊，按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="a078d-163">Keep hello default settings in hello **Publish Web** dialog box and click **Publish**.</span></span>

![Web 發佈][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a><span data-ttu-id="a078d-165">授與權限 toohello Azure AD 後端服務應用程式</span><span class="sxs-lookup"><span data-stu-id="a078d-165">Grant permissions toohello Azure AD backend service application</span></span>
<span data-ttu-id="a078d-166">Hello 後端服務的新應用程式會建立在 Azure AD 目錄 hello 設定的一部分，以及發佈的 Web API 專案的程序。</span><span class="sxs-lookup"><span data-stu-id="a078d-166">A new application for hello backend service is created in your Azure AD directory as part of hello configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="a078d-167">在此步驟中的 hello 視訊，開始 6:13，權限會授與 toohello Web API 後端。</span><span class="sxs-lookup"><span data-stu-id="a078d-167">In this step of hello video, starting at 6:13, permissions are granted toohello Web API backend.</span></span>

![應用程式][api-management-aad-backend-app]

<span data-ttu-id="a078d-169">按一下 hello hello 應用程式 tooconfigure hello 所需的權限名稱。</span><span class="sxs-lookup"><span data-stu-id="a078d-169">Click hello name of hello application tooconfigure hello required permissions.</span></span> <span data-ttu-id="a078d-170">瀏覽 toohello**設定** 索引標籤並捲動 toohello**權限 tooother 應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="a078d-170">Navigate toohello **Configure** tab and scroll down toohello **permissions tooother applications** section.</span></span> <span data-ttu-id="a078d-171">按一下 hello**應用程式權限**旁邊的下拉式清單**Windows** **Azure Active Directory**，核取方塊 hello**讀取目錄資料**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="a078d-171">Click hello **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check hello box for **Read directory data**, and click **Save**.</span></span>

![新增權限][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="a078d-173">如果**Windows** **Azure Active Directory**是並未列在 權限 tooother 應用程式之下，按一下**新增應用程式**並將它加入從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="a078d-173">If **Windows** **Azure Active Directory** is not listed under permissions tooother applications, click **Add application** and add it from hello list.</span></span>
> 
> 

<span data-ttu-id="a078d-174">請記下 hello**應用程式識別碼 URI** hello API 管理開發人員入口網站設定 Azure AD 應用程式時，在後續步驟中使用。</span><span class="sxs-lookup"><span data-stu-id="a078d-174">Make a note of hello **App Id URI** for use in a subsequent step when an Azure AD application is configured for hello API Management developer portal.</span></span>

![App 識別碼 URI][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a><span data-ttu-id="a078d-176">Hello Web 應用程式開發介面匯入 API 管理</span><span class="sxs-lookup"><span data-stu-id="a078d-176">Import hello Web API into API Management</span></span>
<span data-ttu-id="a078d-177">應用程式開發介面會在 hello API 發行者入口網站，可從 hello Azure 入口網站存取設定。</span><span class="sxs-lookup"><span data-stu-id="a078d-177">APIs are configured from hello API publisher portal, which is accessed through hello Azure Portal.</span></span> <span data-ttu-id="a078d-178">tooreach，按一下 **發行者入口網站**從您的 API 管理服務的 hello 工具列。</span><span class="sxs-lookup"><span data-stu-id="a078d-178">tooreach it, click **Publisher portal** from hello toolbar of your API Management service.</span></span> <span data-ttu-id="a078d-179">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[管理您的第一個應用程式開發介面][Manage your first API]教學課程。</span><span class="sxs-lookup"><span data-stu-id="a078d-179">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API][Manage your first API] tutorial.</span></span>

![發行者入口網站][api-management-management-console]

<span data-ttu-id="a078d-181">作業可以是[手動加入 tooAPIs](api-management-howto-add-operations.md)，或可以匯入。</span><span class="sxs-lookup"><span data-stu-id="a078d-181">Operations can be [added tooAPIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="a078d-182">在這段視訊中從 6:40 開始，運算會以 Swagger 格式匯入。</span><span class="sxs-lookup"><span data-stu-id="a078d-182">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="a078d-183">建立名為`calcapi.json`與下列內容，並將它儲存 tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="a078d-183">Create a file named `calcapi.json` with following contents and save it tooyour computer.</span></span> <span data-ttu-id="a078d-184">請確定該 hello`host`屬性指向 tooyour Web API 後端。</span><span class="sxs-lookup"><span data-stu-id="a078d-184">Ensure that hello `host` attribute points tooyour Web API backend.</span></span> <span data-ttu-id="a078d-185">在此範例中使用 `"host": "apimaaddemo.azurewebsites.net"` 。</span><span class="sxs-lookup"><span data-stu-id="a078d-185">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

<span data-ttu-id="a078d-186">tooimport hello 計算機 API 中，按一下**Api**從 hello **API 管理**hello 左、，然後按一下功能表**匯入 API**。</span><span class="sxs-lookup"><span data-stu-id="a078d-186">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![匯入 API 按鈕][api-management-import-api]

<span data-ttu-id="a078d-188">執行下列步驟 tooconfigure hello [小算盤] 應用程式開發介面的 hello。</span><span class="sxs-lookup"><span data-stu-id="a078d-188">Perform hello following steps tooconfigure hello calculator API.</span></span>

1. <span data-ttu-id="a078d-189">按一下**檔案從**，瀏覽 toohello`calculator.json`檔案儲存，然後按一下 hello **Swagger**選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="a078d-189">Click **From file**, browse toohello `calculator.json` file you saved, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="a078d-190">型別**calc**到 hello **Web API URL 尾碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a078d-190">Type **calc** into hello **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="a078d-191">按一下 hello**產品 （選擇性）**方塊，然後選擇**入門**。</span><span class="sxs-lookup"><span data-stu-id="a078d-191">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="a078d-192">按一下**儲存**tooimport hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="a078d-192">Click **Save** tooimport hello API.</span></span>

![Add new API][api-management-import-new-api]

<span data-ttu-id="a078d-194">一旦匯入 hello API 時，hello hello api 摘要頁面會顯示 hello 發行者入口網站中。</span><span class="sxs-lookup"><span data-stu-id="a078d-194">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a><span data-ttu-id="a078d-195">從 hello 開發人員入口網站未順利呼叫 hello API</span><span class="sxs-lookup"><span data-stu-id="a078d-195">Call hello API unsuccessfully from hello developer portal</span></span>
<span data-ttu-id="a078d-196">此時，hello 應用程式開發介面已匯入 API 管理，但無法尚未成功從呼叫 hello 開發人員入口網站是 Azure AD 驗證受到 hello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="a078d-196">At this point, hello API has been imported into API Management, but cannot yet be called successfully from hello developer portal because hello backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="a078d-197">這示範於 hello 視訊開始使用 hello 步驟 7:40。</span><span class="sxs-lookup"><span data-stu-id="a078d-197">This is demonstrated in hello video starting at 7:40 using hello following steps.</span></span>

<span data-ttu-id="a078d-198">按一下**開發人員入口網站**從 hello 右上方 hello 發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="a078d-198">Click **Developer portal** from hello top-right side of hello publisher portal.</span></span>

![開發人員入口網站][api-management-developer-portal-menu]

<span data-ttu-id="a078d-200">按一下**Api**按一下 hello**計算機**應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="a078d-200">Click **APIs** and click hello **Calculator** API.</span></span>

![開發人員入口網站][api-management-dev-portal-apis]

<span data-ttu-id="a078d-202">按一下 [試試看] 。</span><span class="sxs-lookup"><span data-stu-id="a078d-202">Click **Try it**.</span></span>

![試試看][api-management-dev-portal-try-it]

<span data-ttu-id="a078d-204">按一下**傳送**並記下的 hello 回應狀態**401 未授權**。</span><span class="sxs-lookup"><span data-stu-id="a078d-204">Click **Send** and note hello response status of **401 Unauthorized**.</span></span>

![傳送][api-management-dev-portal-send-401]

<span data-ttu-id="a078d-206">hello 要求是未經授權的因為 hello 後端 API 受到 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="a078d-206">hello request is unauthorized because hello backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="a078d-207">在之前成功呼叫 hello API hello 開發人員入口網站必須先設定的 tooauthorize 開發人員使用 OAuth 2.0。</span><span class="sxs-lookup"><span data-stu-id="a078d-207">Before successfully calling hello API hello developer portal must be configured tooauthorize developers using OAuth 2.0.</span></span> <span data-ttu-id="a078d-208">Hello 下列各節說明此程序。</span><span class="sxs-lookup"><span data-stu-id="a078d-208">This process is described in hello following sections.</span></span>

## <a name="register-hello-developer-portal-as-an-aad-application"></a><span data-ttu-id="a078d-209">Hello 開發人員入口網站註冊為 AAD 應用程式</span><span class="sxs-lookup"><span data-stu-id="a078d-209">Register hello developer portal as an AAD application</span></span>
<span data-ttu-id="a078d-210">設定 hello 開發人員入口網站 tooauthorize 開發人員使用 OAuth 2.0 hello 第一個步驟是 tooregister hello 開發人員入口網站為 AAD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a078d-210">hello first step in configuring hello developer portal tooauthorize developers using OAuth 2.0 is tooregister hello developer portal as an AAD application.</span></span> <span data-ttu-id="a078d-211">這示範開始 8:27 hello 視訊中。</span><span class="sxs-lookup"><span data-stu-id="a078d-211">This is demonstrated starting at 8:27 in hello video.</span></span>

<span data-ttu-id="a078d-212">瀏覽 toohello Azure AD 租用戶的這段影片中，在此範例中的 hello 第一個步驟中**APIMDemo**並瀏覽 toohello**應用程式** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a078d-212">Navigate toohello Azure AD tenant from hello first step of this video, in this example **APIMDemo** and navigate toohello **Applications** tab.</span></span>

![新增應用程式][api-management-aad-new-application-devportal]

<span data-ttu-id="a078d-214">按一下 hello**新增**按鈕 toocreate 新的 Azure Active Directory 應用程式，然後選擇**加入我組織正在開發的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a078d-214">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![新增應用程式][api-management-new-aad-application-menu]

<span data-ttu-id="a078d-216">選擇**Web 應用程式和/或 Web API**，輸入名稱，然後按一下 hello 下一步箭頭。</span><span class="sxs-lookup"><span data-stu-id="a078d-216">Choose **Web application and/or Web API**, enter a name, and click hello next arrow.</span></span> <span data-ttu-id="a078d-217">在此範例中使用 **APIMDeveloperPortal**。</span><span class="sxs-lookup"><span data-stu-id="a078d-217">In this example **APIMDeveloperPortal** is used.</span></span>

![新增應用程式][api-management-aad-new-application-devportal-1]

<span data-ttu-id="a078d-219">如**登入 URL**輸入您的 API 管理服務的 hello URL，然後附加`/signin`。</span><span class="sxs-lookup"><span data-stu-id="a078d-219">For **Sign-on URL** enter hello URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="a078d-220">在此範例中使用 `https://contoso5.portal.azure-api.net/signin` 。</span><span class="sxs-lookup"><span data-stu-id="a078d-220">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="a078d-221">如**應用程式識別碼 URL**輸入您的 API 管理服務的 hello URL，然後附加一些獨特的字元。</span><span class="sxs-lookup"><span data-stu-id="a078d-221">For **App Id URL** enter hello URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="a078d-222">這些字元可以是任何想要的字元，在此範例中使用 `https://contoso5.portal.azure-api.net/dp`。</span><span class="sxs-lookup"><span data-stu-id="a078d-222">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="a078d-223">當 hello 預期**應用程式屬性**所設定，請按一下 hello 核取記號 toocreate hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a078d-223">When hello  desired **App properties** are configured, click hello check mark toocreate hello application.</span></span>

![新增應用程式][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="a078d-225">設定 API 管理 OAuth 2.0 授權伺服器</span><span class="sxs-lookup"><span data-stu-id="a078d-225">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="a078d-226">hello 下一個步驟是 tooconfigure API 管理中的 OAuth 2.0 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="a078d-226">hello next step is tooconfigure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="a078d-227">此步驟會示範 hello 視訊開始 9:43。</span><span class="sxs-lookup"><span data-stu-id="a078d-227">This step is demonstrated in hello video starting at 9:43.</span></span>

<span data-ttu-id="a078d-228">按一下**安全性**hello API 管理 hello 左側，按一下功能表**OAuth 2.0**，然後按一下**新增授權**伺服器。</span><span class="sxs-lookup"><span data-stu-id="a078d-228">Click **Security** from hello API Management menu on hello left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![新增授權伺服器][api-management-add-authorization-server]

<span data-ttu-id="a078d-230">中輸入名稱和選擇性描述 hello**名稱**和**描述**欄位。</span><span class="sxs-lookup"><span data-stu-id="a078d-230">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> <span data-ttu-id="a078d-231">這些欄位是 hello API 管理服務執行個體內使用的 tooidentify hello OAuth 2.0 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="a078d-231">These fields are used tooidentify hello OAuth 2.0 authorization server within hello API Management service instance.</span></span> <span data-ttu-id="a078d-232">在此範例中使用**授權伺服器示範**。</span><span class="sxs-lookup"><span data-stu-id="a078d-232">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="a078d-233">稍後當您指定用來驗證應用程式開發介面的 OAuth 2.0 伺服器 toobe，您會選取此名稱。</span><span class="sxs-lookup"><span data-stu-id="a078d-233">Later when you specify an OAuth 2.0 server toobe used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="a078d-234">Hello**用戶端註冊頁面 URL**輸入預留位置的值，例如`http://localhost`。</span><span class="sxs-lookup"><span data-stu-id="a078d-234">For hello **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="a078d-235">hello**用戶端註冊頁面 URL**點 toohello 頁面上的使用者可以使用 toocreate 並且支援帳戶的使用者管理的 OAuth 2.0 提供者設定自己的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a078d-235">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="a078d-236">在此範例中，使用者沒有建立和設定自己的帳戶，因此使用預留位置。</span><span class="sxs-lookup"><span data-stu-id="a078d-236">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![新增授權伺服器][api-management-add-authorization-server-1]

<span data-ttu-id="a078d-238">接著，指定 [授權端點 URL] 和 [權杖端點 URL]。</span><span class="sxs-lookup"><span data-stu-id="a078d-238">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![授權伺服器][api-management-add-authorization-server-1a]

<span data-ttu-id="a078d-240">這些值可以取自 hello**應用程式端點**hello hello 開發人員入口網站建立 AAD 應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="a078d-240">These values can be retrieved from hello **App Endpoints** page of hello AAD application you created for hello developer portal.</span></span> <span data-ttu-id="a078d-241">tooaccess hello 端點瀏覽 toohello**設定**hello AAD 應用程式索引標籤上，按一下 **檢視端點**。</span><span class="sxs-lookup"><span data-stu-id="a078d-241">tooaccess hello endpoints navigate toohello **Configure** tab for hello AAD application and click **View endpoints**.</span></span>

![應用程式][api-management-aad-devportal-application]

![檢視端點][api-management-aad-view-endpoints]

<span data-ttu-id="a078d-244">複製 hello **OAuth 2.0 授權端點**並將它貼到 hello**授權端點 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a078d-244">Copy hello **OAuth 2.0 authorization endpoint** and paste it into hello **Authorization endpoint URL** textbox.</span></span>

![新增授權伺服器][api-management-add-authorization-server-2]

<span data-ttu-id="a078d-246">複製 hello **OAuth 2.0 權杖端點**並將它貼到 hello**語彙基元端點 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a078d-246">Copy hello **OAuth 2.0 token endpoint** and paste it into hello **Token endpoint URL** textbox.</span></span>

![新增授權伺服器][api-management-add-authorization-server-2a]

<span data-ttu-id="a078d-248">此外 toopasting hello 權杖端點，新增名為的其他主體參數**資源**並用 hello 值 hello**應用程式識別碼 URI**從 hello hello 後端服務的 AAD 應用程式建立發行 hello Visual Studio 專案時。</span><span class="sxs-lookup"><span data-stu-id="a078d-248">In addition toopasting in hello token endpoint, add an additional body parameter named **resource** and for hello value use hello **App Id URI** from hello AAD application for hello backend service that was created when hello Visual Studio project was published.</span></span>

![App 識別碼 URI][api-management-aad-sso-uri]

<span data-ttu-id="a078d-250">接下來，指定 hello 用戶端認證。</span><span class="sxs-lookup"><span data-stu-id="a078d-250">Next, specify hello client credentials.</span></span> <span data-ttu-id="a078d-251">這些是您想要的 hello 資源的 hello 認證 tooaccess，在此情況下 hello 開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="a078d-251">These are hello credentials for hello resource you want tooaccess, in this case hello developer portal.</span></span>

![用戶端認證][api-management-client-credentials]

<span data-ttu-id="a078d-253">tooget hello**用戶端識別碼**，瀏覽 toohello**設定**hello hello 開發人員入口網站和複製 hello 的 AAD 應用程式 索引標籤**用戶端識別碼**。</span><span class="sxs-lookup"><span data-stu-id="a078d-253">tooget hello **Client Id**, navigate toohello **Configure** tab of hello AAD application for hello developer portal and copy hello **Client Id**.</span></span>

<span data-ttu-id="a078d-254">tooget hello**用戶端密碼**按一下 hello**選取持續時間**下拉式清單中 hello**金鑰**區段，並指定間隔。</span><span class="sxs-lookup"><span data-stu-id="a078d-254">tooget hello **Client Secret** click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="a078d-255">在此範例中使用 1 年。</span><span class="sxs-lookup"><span data-stu-id="a078d-255">In this example 1 year is used.</span></span>

![用戶端識別碼][api-management-aad-client-id]

<span data-ttu-id="a078d-257">按一下**儲存**toosave hello 組態和顯示 hello 金鑰。</span><span class="sxs-lookup"><span data-stu-id="a078d-257">Click **Save** toosave hello configuration and display hello key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a078d-258">記下此金鑰。</span><span class="sxs-lookup"><span data-stu-id="a078d-258">Make a note of this key.</span></span> <span data-ttu-id="a078d-259">一旦您關閉 hello Azure Active Directory 設定 視窗中，無法再次顯示 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a078d-259">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="a078d-260">複製 hello 金鑰 toohello 剪貼簿，交換器後 toohello 發行者入口網站將 hello 金鑰貼至 hello**用戶端密碼**文字方塊中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="a078d-260">Copy hello key toohello clipboard, switch back toohello publisher portal, paste hello key into hello **Client Secret** textbox, and click **Save**.</span></span>

![新增授權伺服器][api-management-add-authorization-server-3]

<span data-ttu-id="a078d-262">緊接 hello 用戶端認證是授權碼授與。</span><span class="sxs-lookup"><span data-stu-id="a078d-262">Immediately following hello client credentials is an authorization code grant.</span></span> <span data-ttu-id="a078d-263">複製此授權程式碼和參數後 tooyour Azure AD 開發人員入口網站應用程式設定 頁面上，並將 hello 授權授與貼入 hello**回覆 URL**欄位，然後按一下**儲存**一次。</span><span class="sxs-lookup"><span data-stu-id="a078d-263">Copy this authorization code and switch back tooyour Azure AD developer portal application configure page, and paste hello authorization grant into hello **Reply URL** field, and click **Save** again.</span></span>

![回覆 URL][api-management-aad-reply-url]

<span data-ttu-id="a078d-265">hello 下一個步驟是 tooconfigure hello hello 開發人員入口網站 AAD 應用程式權限。</span><span class="sxs-lookup"><span data-stu-id="a078d-265">hello next step is tooconfigure hello permissions for hello developer portal AAD application.</span></span> <span data-ttu-id="a078d-266">按一下**應用程式權限**和核取方塊 hello**讀取目錄資料**。</span><span class="sxs-lookup"><span data-stu-id="a078d-266">Click **Application Permissions** and check hello box for **Read directory data**.</span></span> <span data-ttu-id="a078d-267">按一下**儲存**toosave 這變更此項目，然後再按一下**新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a078d-267">Click **Save** toosave this change, and then click **Add application**.</span></span>

![新增權限][api-management-add-devportal-permissions]

<span data-ttu-id="a078d-269">按一下 hello 搜尋圖示，型別**APIM** hello 到開頭 方塊中，選取**APIMAADDemo**，按一下 hello 核取記號 toosave。</span><span class="sxs-lookup"><span data-stu-id="a078d-269">Click hello search icon, type **APIM** into hello Starting with box, select **APIMAADDemo**, and click hello check mark toosave.</span></span>

![新增權限][api-management-aad-add-app-permissions]

<span data-ttu-id="a078d-271">按一下**委派的權限**如**APIMAADDemo**和核取方塊 hello**存取 APIMAADDemo**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="a078d-271">Click **Delegated Permissions** for **APIMAADDemo** and check hello box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="a078d-272">這可讓 hello 開發人員入口網站應用程式 tooaccess hello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="a078d-272">This allows hello developer portal application tooaccess hello backend service.</span></span>

![新增權限][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a><span data-ttu-id="a078d-274">啟用 hello [小算盤] 應用程式開發介面的 OAuth 2.0 使用者授權</span><span class="sxs-lookup"><span data-stu-id="a078d-274">Enable OAuth 2.0 user authorization for hello Calculator API</span></span>
<span data-ttu-id="a078d-275">既然 hello OAuth 2.0 的伺服器設定，您可以指定它在您的應用程式開發介面的 hello 安全性設定。</span><span class="sxs-lookup"><span data-stu-id="a078d-275">Now that hello OAuth 2.0 server is configured, you can specify it in hello security settings for your API.</span></span> <span data-ttu-id="a078d-276">此步驟會示範 hello 視訊開始： 14:30。</span><span class="sxs-lookup"><span data-stu-id="a078d-276">This step is demonstrated in hello video starting at 14:30.</span></span>

<span data-ttu-id="a078d-277">按一下**Api**在 hello 左的窗格中，然後按一下**計算機**tooview 並設定其設定。</span><span class="sxs-lookup"><span data-stu-id="a078d-277">Click **APIs** in hello left menu, and click  **Calculator** tooview and configure its settings.</span></span>

![計算機 API][api-management-calc-api]

<span data-ttu-id="a078d-279">瀏覽 toohello**安全性**索引標籤上，檢查 hello **OAuth 2.0**核取方塊，選取 hello 所需的授權伺服器從 hello**授權伺服器**下拉式清單中，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="a078d-279">Navigate toohello **Security** tab, check hello **OAuth 2.0** checkbox, select hello desired authorization server from hello **Authorization server** drop-down, and click **Save**.</span></span>

![計算機 API][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a><span data-ttu-id="a078d-281">已成功從 hello 開發人員入口網站中呼叫 hello [小算盤] 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="a078d-281">Successfully call hello Calculator API from hello developer portal</span></span>
<span data-ttu-id="a078d-282">既然 hello 應用程式開發介面上設定了 hello OAuth 2.0 授權，其作業可以順利呼叫從 hello 開發人員中心。</span><span class="sxs-lookup"><span data-stu-id="a078d-282">Now that hello OAuth 2.0 authorization is configured on hello API, its operations can be successfully called from hello developer center.</span></span> <span data-ttu-id="a078d-283">此步驟會示範 hello 視訊開始 15:00。</span><span class="sxs-lookup"><span data-stu-id="a078d-283">THis step is demonstrated in hello video starting at 15:00.</span></span>

<span data-ttu-id="a078d-284">瀏覽後 toohello**加入兩個整數**hello 計算機服務中的 hello 開發人員入口網站按一下 操作的**試試**。</span><span class="sxs-lookup"><span data-stu-id="a078d-284">Navigate back toohello **Add two integers** operation of hello calculator service in hello developer portal and click **Try it**.</span></span> <span data-ttu-id="a078d-285">請注意 hello 中的新項目 hello**授權**區段您剛才加入的對應 toohello 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="a078d-285">Note hello new item in hello **Authorization** section corresponding toohello authorization server you just added.</span></span>

![計算機 API][api-management-calc-authorization-server]

<span data-ttu-id="a078d-287">選取**授權碼**從 hello 授權下拉式清單，然後輸入 hello 帳戶 toouse hello 認證。</span><span class="sxs-lookup"><span data-stu-id="a078d-287">Select **Authorization code** from hello authorization drop-down list and enter hello credentials of hello account toouse.</span></span> <span data-ttu-id="a078d-288">如果您已經登入 hello 可能不會提示您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a078d-288">If you are already signed in with hello account you may not be prompted.</span></span>

![計算機 API][api-management-devportal-authorization-code]

<span data-ttu-id="a078d-290">按一下**傳送**和附註 hello**回應狀態**的**200 確定**和 hello hello 回應的內容中的 hello 作業的結果。</span><span class="sxs-lookup"><span data-stu-id="a078d-290">Click **Send** and note hello **Response status** of **200 OK** and hello results of hello operation in hello response content.</span></span>

![計算機 API][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a><span data-ttu-id="a078d-292">設定桌面應用程式 toocall hello 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="a078d-292">Configure a desktop application toocall hello API</span></span>
<span data-ttu-id="a078d-293">hello hello 視訊中的下一個程序會從 16:30，然後設定簡單的桌面應用程式 toocall hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="a078d-293">hello next procedure in hello video starts at 16:30 and configures a simple desktop application toocall hello API.</span></span> <span data-ttu-id="a078d-294">hello 第一個步驟是 tooregister hello 桌面應用程式在 Azure AD 中的，並提供存取 toohello 目錄和 toohello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="a078d-294">hello first step is tooregister hello desktop application in Azure AD and give it access toohello directory and toohello backend service.</span></span> <span data-ttu-id="a078d-295">18:25 在沒有呼叫 hello [小算盤] 應用程式開發介面作業 hello 桌面應用程式的示範。</span><span class="sxs-lookup"><span data-stu-id="a078d-295">At 18:25 there is a demonstration of hello desktop application calling an operation on hello calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a><span data-ttu-id="a078d-296">設定 JWT 驗證原則 toopre-授權要求</span><span class="sxs-lookup"><span data-stu-id="a078d-296">Configure a JWT validation policy toopre-authorize requests</span></span>
<span data-ttu-id="a078d-297">hello hello 視訊中的最後一個程序會從 20:48，然後為您示範如何 toouse hello[驗證 JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT)原則 toopre-驗證每個傳入要求的 hello 存取權杖，以授權要求。</span><span class="sxs-lookup"><span data-stu-id="a078d-297">hello final procedure in hello video starts at 20:48 and shows you how toouse hello [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy toopre-authorize requests by validating hello access tokens of each incoming request.</span></span> <span data-ttu-id="a078d-298">如果 hello 要求未經過驗證的 JWT 原則 hello，hello 要求封鎖的 API 管理，並不會傳遞 toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="a078d-298">If hello request is not validated by hello Validate JWT policy, hello request is blocked by API Management and is not passed along toohello backend.</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

<span data-ttu-id="a078d-299">如需的設定和使用此原則的另一個示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too13:50 向前快轉。</span><span class="sxs-lookup"><span data-stu-id="a078d-299">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="a078d-300">向前快轉 too15:00 toosee hello 原則在 hello 原則編輯器中設定，然後示範從 hello 開發人員入口網站及 hello 未呼叫作業的 too18:50 所需授權權杖。</span><span class="sxs-lookup"><span data-stu-id="a078d-300">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a078d-301">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a078d-301">Next steps</span></span>
* <span data-ttu-id="a078d-302">查看更多有關 API 管理的 [視訊](https://azure.microsoft.com/documentation/videos/index/?services=api-management) 。</span><span class="sxs-lookup"><span data-stu-id="a078d-302">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="a078d-303">針對其他方式 toosecure 後端服務，請參閱[相互憑證驗證](api-management-howto-mutual-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="a078d-303">For other ways toosecure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
