---
title: "使用 Azure Active Directory 與 API 管理保護 Web API 後端 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory 與 API 管理保護 Web API 後端。"
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
ms.openlocfilehash: 0dfb4102904c2e972e6617fd3851fb1c50147357
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-protect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="d8f06-103">如何使用 Azure Active Directory 與 API 管理保護 Web API 後端</span><span class="sxs-lookup"><span data-stu-id="d8f06-103">How to protect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="d8f06-104">下列視訊示範如何使用 OAuth 2.0 通訊協定搭配 Azure Active Directory 與 API 管理建置 Web API 後端並加以保護。</span><span class="sxs-lookup"><span data-stu-id="d8f06-104">The following video shows how to build a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="d8f06-105">本文提供概觀以及視訊中步驟的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="d8f06-105">This article provides an overview and additional information for the steps in the video.</span></span> <span data-ttu-id="d8f06-106">這段 24 分鐘的視訊示範如何：</span><span class="sxs-lookup"><span data-stu-id="d8f06-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="d8f06-107">使用 AAD 建置 Web API 後端以及保護安全 - 從 1:30 開始</span><span class="sxs-lookup"><span data-stu-id="d8f06-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="d8f06-108">將 API 匯入 API 管理 - 從 7:10 開始</span><span class="sxs-lookup"><span data-stu-id="d8f06-108">Import the API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="d8f06-109">設定開發人員入口網站呼叫 API - 從 9:09 開始</span><span class="sxs-lookup"><span data-stu-id="d8f06-109">Configure the Developer portal to call the API - starting at 9:09</span></span>
* <span data-ttu-id="d8f06-110">設定桌面應用程式呼叫 API - 從 18:08 開始</span><span class="sxs-lookup"><span data-stu-id="d8f06-110">Configure a desktop application to call the API - starting at 18:08</span></span>
* <span data-ttu-id="d8f06-111">設定 JWT 驗證原則來預先授權要求 - 從 20:47 開始</span><span class="sxs-lookup"><span data-stu-id="d8f06-111">Configure a JWT validation policy to pre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="d8f06-112">建立 Azure AD 目錄</span><span class="sxs-lookup"><span data-stu-id="d8f06-112">Create an Azure AD directory</span></span>
<span data-ttu-id="d8f06-113">若要使用 Azure Active Directory 保護您的 Web API 後端，您必須先具備 AAD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="d8f06-113">To secure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="d8f06-114">在這段視訊中，使用名為 **APIMDemo** 的租用戶。</span><span class="sxs-lookup"><span data-stu-id="d8f06-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="d8f06-115">若要建立 AAD 租用戶，請登入 [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下 [新增] -> [應用程式服務] -> [Active Directory] -> [目錄] -> [自訂建立]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-115">To create an AAD tenant, sign-in to the [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="d8f06-117">此範例會一同建立名為 **APIMDemo** 的目錄與名為 **DemoAPIM.onmicrosoft.com** 的預設網域。</span><span class="sxs-lookup"><span data-stu-id="d8f06-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="d8f06-118">在整段視訊中都會使用這個目錄。</span><span class="sxs-lookup"><span data-stu-id="d8f06-118">This directory is used throughout the video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="d8f06-120">建立由 Azure Active Directory 保護的 Web API 服務</span><span class="sxs-lookup"><span data-stu-id="d8f06-120">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="d8f06-121">在此步驟中，Web API 後端會使用 Visual Studio 2013 建立。</span><span class="sxs-lookup"><span data-stu-id="d8f06-121">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="d8f06-122">這個步驟的視訊從 1:30 開始。</span><span class="sxs-lookup"><span data-stu-id="d8f06-122">This step of the video starts at 1:30.</span></span> <span data-ttu-id="d8f06-123">若要在 Visual Studio 中建立 Web API 後端專案，請按一下 [檔案] -> [新增] -> [專案]，然後從 [Web] 範本清單中選擇 [ASP.NET Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-123">To create Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from the **Web** templates list.</span></span> <span data-ttu-id="d8f06-124">在此影片中，專案的名稱為 **APIMAADDemo**。</span><span class="sxs-lookup"><span data-stu-id="d8f06-124">In this video the project is named **APIMAADDemo**.</span></span> <span data-ttu-id="d8f06-125">按一下 [確定]  以建立專案。</span><span class="sxs-lookup"><span data-stu-id="d8f06-125">Click **OK** to create the project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="d8f06-127">從 [選取範本清單] 按一下 [Web API] 來建立 Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="d8f06-127">Click **Web API** from the **Select a template list** to create a Web API project.</span></span> <span data-ttu-id="d8f06-128">若要設定 Azure Directory 驗證，請按一下 [變更驗證] 。</span><span class="sxs-lookup"><span data-stu-id="d8f06-128">To configure Azure Directory Authentication click **Change Authentication**.</span></span>

![新增專案][api-management-new-project]

<span data-ttu-id="d8f06-130">按一下 [組織帳戶]，並指定您 AAD 租用戶的 [網域]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-130">Click **Organizational Accounts**, and specify the **Domain** of your AAD tenant.</span></span> <span data-ttu-id="d8f06-131">此範例中的網域是 **DemoAPIM.onmicrosoft.com**。</span><span class="sxs-lookup"><span data-stu-id="d8f06-131">In this example the domain is **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="d8f06-132">您可以從目錄的 [網域] 索引標籤取得您目錄的網域。</span><span class="sxs-lookup"><span data-stu-id="d8f06-132">The domain of your directory can be obtained from the **Domains** tab of your directory.</span></span>

![網域][api-management-aad-domains]

<span data-ttu-id="d8f06-134">在 [變更驗證] 對話方塊中設定所需的設定，並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-134">Configure the desired settings in the **Change Authentication** dialog box and click **OK**.</span></span>

![變更驗證][api-management-change-authentication]

<span data-ttu-id="d8f06-136">按下 [確定]  之後，Visual Studio 將會嘗試使用您的 Azure AD 目錄註冊您的應用程式，Visual Studio 會提示您登入。</span><span class="sxs-lookup"><span data-stu-id="d8f06-136">When you click **OK** Visual Studio will attempt to register your application with your Azure AD directory and you may be prompted to sign in by Visual Studio.</span></span> <span data-ttu-id="d8f06-137">使用您目錄的系統管理帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="d8f06-137">Sign in using an administrative account for your directory.</span></span>

![登入 Visual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="d8f06-139">若要設定此專案為 Azure Web API，請核取 [在雲端中主控] 的方塊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-139">To configure this project as an Azure Web API check the box for **Host in the cloud** and then click **OK**.</span></span>

![新增專案][api-management-new-project-cloud]

<span data-ttu-id="d8f06-141">系統可能會提示您登入 Azure，接著您就可以設定 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8f06-141">You may be prompted to sign in to Azure, and then you can configure the Web App.</span></span>

![設定][api-management-configure-web-app]

<span data-ttu-id="d8f06-143">此範例指定了一個名為 **APIMAADDemo** 的新 **App Service 方案**。</span><span class="sxs-lookup"><span data-stu-id="d8f06-143">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="d8f06-144">按一下 [確定]  設定 Web 應用程式和建立專案。</span><span class="sxs-lookup"><span data-stu-id="d8f06-144">Click **OK** to configure the Web App and create the project.</span></span>

## <a name="add-the-code-to-the-web-api-project"></a><span data-ttu-id="d8f06-145">將程式碼加入 Web API 專案</span><span class="sxs-lookup"><span data-stu-id="d8f06-145">Add the code to the Web API project</span></span>
<span data-ttu-id="d8f06-146">視訊中的下一個步驟會將程式碼加入 Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="d8f06-146">The next step in the video adds the code to the Web API project.</span></span> <span data-ttu-id="d8f06-147">這個步驟從 4:35 開始。</span><span class="sxs-lookup"><span data-stu-id="d8f06-147">This step starts at 4:35.</span></span>

<span data-ttu-id="d8f06-148">此範例中的 Web API 使用模型和控制器實作基本的計算機服務。</span><span class="sxs-lookup"><span data-stu-id="d8f06-148">The Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="d8f06-149">若要新增服務的模型，請以滑鼠右鍵按一下 [方案總管] 中的 [模型]，然後選擇 [新增][類別]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-149">To add the model for the service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="d8f06-150">將類別命名為 `CalcInput`，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-150">Name the class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="d8f06-151">在 `CalcInput.cs` 檔案的開頭處新增下列 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="d8f06-151">Add the following `using` statement to the top of the `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="d8f06-152">將產生的類別取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="d8f06-152">Replace the generated class with the following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="d8f06-153">以滑鼠右鍵按一下 [方案總管] 中的 [控制器]，然後選擇 [新增] -> [控制器]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-153">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="d8f06-154">按一下 [Web API 2 控制器 - 空白]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-154">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="d8f06-155">輸入 **CalcController** 做為控制器名稱，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-155">Type **CalcController** for the Controller name and click **Add**.</span></span>

![新增控制器][api-management-add-controller]

<span data-ttu-id="d8f06-157">在 `CalcController.cs` 檔案的開頭處新增下列 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="d8f06-157">Add the following `using` statement to the top of the `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="d8f06-158">將產生的控制器類別取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="d8f06-158">Replace the generated controller class with the following code.</span></span> <span data-ttu-id="d8f06-159">此程式碼實作基本計算機 API 的 `Add`、`Subtract`、`Multiply` 以及 `Divide` 運算。</span><span class="sxs-lookup"><span data-stu-id="d8f06-159">This code implements the `Add`, `Subtract`, `Multiply`, and `Divide` operations of the Basic Calculator API.</span></span>

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

<span data-ttu-id="d8f06-160">按下 **F6** 來建置和驗證方案。</span><span class="sxs-lookup"><span data-stu-id="d8f06-160">Press **F6** to build and verify the solution.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="d8f06-161">將專案發佈到 Azure</span><span class="sxs-lookup"><span data-stu-id="d8f06-161">Publish the project to Azure</span></span>
<span data-ttu-id="d8f06-162">在此步驟中，Visual Studio 專案會發佈到 Azure。</span><span class="sxs-lookup"><span data-stu-id="d8f06-162">In this step the Visual Studio project is published to Azure.</span></span> <span data-ttu-id="d8f06-163">這個步驟的視訊從 5:45 開始。</span><span class="sxs-lookup"><span data-stu-id="d8f06-163">This step of the video starts at 5:45.</span></span>

<span data-ttu-id="d8f06-164">若要將專案發佈到 Azure，請以滑鼠右鍵按一下 Visual Studio 中的 [APIMAADDemo] 專案，然後選擇 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-164">To publish the project to Azure, right-click the **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="d8f06-165">保留 [發佈 Web] 對話方塊中的預設值，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-165">Keep the default settings in the **Publish Web** dialog box and click **Publish**.</span></span>

![Web 發佈][api-management-web-publish]

## <a name="grant-permissions-to-the-azure-ad-backend-service-application"></a><span data-ttu-id="d8f06-167">授與權限給 Azure AD 後端服務應用程式</span><span class="sxs-lookup"><span data-stu-id="d8f06-167">Grant permissions to the Azure AD backend service application</span></span>
<span data-ttu-id="d8f06-168">設定和發佈您的 Web API 專案時，您的 Azure AD 目錄中會建立一個新的應用程式用於後端服務。</span><span class="sxs-lookup"><span data-stu-id="d8f06-168">A new application for the backend service is created in your Azure AD directory as part of the configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="d8f06-169">這個步驟會授與權限給 Web API 後端，從視訊的 6:13 開始。</span><span class="sxs-lookup"><span data-stu-id="d8f06-169">In this step of the video, starting at 6:13, permissions are granted to the Web API backend.</span></span>

![應用程式][api-management-aad-backend-app]

<span data-ttu-id="d8f06-171">按一下要設定必要權限的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="d8f06-171">Click the name of the application to configure the required permissions.</span></span> <span data-ttu-id="d8f06-172">瀏覽到 [設定] 索引標籤，向下捲動到 [其他應用程式的權限] 區段。</span><span class="sxs-lookup"><span data-stu-id="d8f06-172">Navigate to the **Configure** tab and scroll down to the **permissions to other applications** section.</span></span> <span data-ttu-id="d8f06-173">按一下 [Windows Azure Active Directory] 旁邊的 [應用程式權限] 下拉式清單，核取 [讀取目錄資料] 的方塊，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-173">Click the **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check the box for **Read directory data**, and click **Save**.</span></span>

![新增權限][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="d8f06-175">如果 [Windows Azure Active Directory] 並未列在 [其他應用程式的權限] 之下，請按一下 [新增應用程式] 從清單將其新增。</span><span class="sxs-lookup"><span data-stu-id="d8f06-175">If **Windows** **Azure Active Directory** is not listed under permissions to other applications, click **Add application** and add it from the list.</span></span>
> 
> 

<span data-ttu-id="d8f06-176">請記下 [應用程式識別碼 URI]  供後續為 API 管理開發人員入口網站設定 Azure AD 應用程式的步驟時使用。</span><span class="sxs-lookup"><span data-stu-id="d8f06-176">Make a note of the **App Id URI** for use in a subsequent step when an Azure AD application is configured for the API Management developer portal.</span></span>

![App 識別碼 URI][api-management-aad-sso-uri]

## <a name="import-the-web-api-into-api-management"></a><span data-ttu-id="d8f06-178">將 Web API 匯入 API 管理</span><span class="sxs-lookup"><span data-stu-id="d8f06-178">Import the Web API into API Management</span></span>
<span data-ttu-id="d8f06-179">API 經由 API 發佈者入口網站進行設定，您可以透過 Azure 入口網站存取此入口網站。</span><span class="sxs-lookup"><span data-stu-id="d8f06-179">APIs are configured from the API publisher portal, which is accessed through the Azure Portal.</span></span> <span data-ttu-id="d8f06-180">若要觸達它，請從 API 管理服務的工具列按一下 [發佈者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-180">To reach it, click **Publisher portal** from the toolbar of your API Management service.</span></span> <span data-ttu-id="d8f06-181">如果您尚未建立 API 管理服務執行個體，請參閱[管理您的第一個 API][Manage your first API] 教學課程中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-181">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API][Manage your first API] tutorial.</span></span>

![發行者入口網站][api-management-management-console]

<span data-ttu-id="d8f06-183">您可以將運算 [手動加入 API](api-management-howto-add-operations.md)，也可以匯入運算。</span><span class="sxs-lookup"><span data-stu-id="d8f06-183">Operations can be [added to APIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="d8f06-184">在這段視訊中從 6:40 開始，運算會以 Swagger 格式匯入。</span><span class="sxs-lookup"><span data-stu-id="d8f06-184">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="d8f06-185">以下列內容建立名為 `calcapi.json` 的檔案，然後將檔案儲存到您的電腦。</span><span class="sxs-lookup"><span data-stu-id="d8f06-185">Create a file named `calcapi.json` with following contents and save it to your computer.</span></span> <span data-ttu-id="d8f06-186">確定 `host` 屬性指向您的 Web API 後端。</span><span class="sxs-lookup"><span data-stu-id="d8f06-186">Ensure that the `host` attribute points to your Web API backend.</span></span> <span data-ttu-id="d8f06-187">在此範例中使用 `"host": "apimaaddemo.azurewebsites.net"` 。</span><span class="sxs-lookup"><span data-stu-id="d8f06-187">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

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

<span data-ttu-id="d8f06-188">若要匯入計算機 API，請從左邊的 [API 管理] 功能表中按一下 [API]，然後按一下 [匯入 API]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-188">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![匯入 API 按鈕][api-management-import-api]

<span data-ttu-id="d8f06-190">執行下列步驟以設定計算機 API。</span><span class="sxs-lookup"><span data-stu-id="d8f06-190">Perform the following steps to configure the calculator API.</span></span>

1. <span data-ttu-id="d8f06-191">按一下 [從檔案]，瀏覽到您儲存的 `calculator.json` 檔案，然後按一下 [Swagger] 選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="d8f06-191">Click **From file**, browse to the `calculator.json` file you saved, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="d8f06-192">在 [Web API URL 尾碼] 文字方塊中輸入 **calc**。</span><span class="sxs-lookup"><span data-stu-id="d8f06-192">Type **calc** into the **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="d8f06-193">按一下 [產品 (選擇性)] 方塊，然後選擇 [入門]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-193">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="d8f06-194">按一下 [ **儲存** ] 匯入 API。</span><span class="sxs-lookup"><span data-stu-id="d8f06-194">Click **Save** to import the API.</span></span>

![Add new API][api-management-import-new-api]

<span data-ttu-id="d8f06-196">匯入 API 之後，API 的摘要頁面隨即會顯示在發行者入口網站中。</span><span class="sxs-lookup"><span data-stu-id="d8f06-196">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

## <a name="call-the-api-unsuccessfully-from-the-developer-portal"></a><span data-ttu-id="d8f06-197">從開發人員入口網站無法成功呼叫 API</span><span class="sxs-lookup"><span data-stu-id="d8f06-197">Call the API unsuccessfully from the developer portal</span></span>
<span data-ttu-id="d8f06-198">現在，API 已經匯入 API 管理，但是還無法從開發人員入口網站成功呼叫，因為使用 Azure AD 驗證保護後端服務。</span><span class="sxs-lookup"><span data-stu-id="d8f06-198">At this point, the API has been imported into API Management, but cannot yet be called successfully from the developer portal because the backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="d8f06-199">這會從視訊的 7:40 開始使用下列步驟示範。</span><span class="sxs-lookup"><span data-stu-id="d8f06-199">This is demonstrated in the video starting at 7:40 using the following steps.</span></span>

<span data-ttu-id="d8f06-200">從發佈者入口網站的右上角，按一下 [開發人員入口網站]  。</span><span class="sxs-lookup"><span data-stu-id="d8f06-200">Click **Developer portal** from the top-right side of the publisher portal.</span></span>

![開發人員入口網站][api-management-developer-portal-menu]

<span data-ttu-id="d8f06-202">按一下 [API]，然後按一下 [計算機] API。</span><span class="sxs-lookup"><span data-stu-id="d8f06-202">Click **APIs** and click the **Calculator** API.</span></span>

![開發人員入口網站][api-management-dev-portal-apis]

<span data-ttu-id="d8f06-204">按一下 [試試看] 。</span><span class="sxs-lookup"><span data-stu-id="d8f06-204">Click **Try it**.</span></span>

![試試看][api-management-dev-portal-try-it]

<span data-ttu-id="d8f06-206">按一下 [傳送]，注意回應狀態為 [401 未授權]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-206">Click **Send** and note the response status of **401 Unauthorized**.</span></span>

![傳送][api-management-dev-portal-send-401]

<span data-ttu-id="d8f06-208">因為後端 API 受到 Azure Active Directory 的保護，所以要求未獲授權。</span><span class="sxs-lookup"><span data-stu-id="d8f06-208">The request is unauthorized because the backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="d8f06-209">在成功呼叫 API 之前，必須先使用 OAuth 2.0 設定開發人員入口網站以授權開發人員。</span><span class="sxs-lookup"><span data-stu-id="d8f06-209">Before successfully calling the API the developer portal must be configured to authorize developers using OAuth 2.0.</span></span> <span data-ttu-id="d8f06-210">下列各節將說明這個程序。</span><span class="sxs-lookup"><span data-stu-id="d8f06-210">This process is described in the following sections.</span></span>

## <a name="register-the-developer-portal-as-an-aad-application"></a><span data-ttu-id="d8f06-211">將開發人員入口網站註冊為 AAD 應用程式</span><span class="sxs-lookup"><span data-stu-id="d8f06-211">Register the developer portal as an AAD application</span></span>
<span data-ttu-id="d8f06-212">使用 OAuth 2.0 設定開發人員入口網站來授權開發人員的第一個步驟是將開發人員入口網站註冊為 AAD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8f06-212">The first step in configuring the developer portal to authorize developers using OAuth 2.0 is to register the developer portal as an AAD application.</span></span> <span data-ttu-id="d8f06-213">這會從視訊的 8:27 開始示範。</span><span class="sxs-lookup"><span data-stu-id="d8f06-213">This is demonstrated starting at 8:27 in the video.</span></span>

<span data-ttu-id="d8f06-214">這段視訊第一個步驟是瀏覽到 Azure AD 租用戶，在此範例中是 **APIMDemo**，然後瀏覽到 [應用程式] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d8f06-214">Navigate to the Azure AD tenant from the first step of this video, in this example **APIMDemo** and navigate to the **Applications** tab.</span></span>

![新增應用程式][api-management-aad-new-application-devportal]

<span data-ttu-id="d8f06-216">按一下 [新增] 按鈕來建立新 Azure Active Directory 應用程式，並選擇 [新增我的組織正在開發的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-216">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![新增應用程式][api-management-new-aad-application-menu]

<span data-ttu-id="d8f06-218">選擇 [Web 應用程式和/或 Web API]、輸入名稱，然後按下一步箭頭。</span><span class="sxs-lookup"><span data-stu-id="d8f06-218">Choose **Web application and/or Web API**, enter a name, and click the next arrow.</span></span> <span data-ttu-id="d8f06-219">在此範例中使用 **APIMDeveloperPortal**。</span><span class="sxs-lookup"><span data-stu-id="d8f06-219">In this example **APIMDeveloperPortal** is used.</span></span>

![新增應用程式][api-management-aad-new-application-devportal-1]

<span data-ttu-id="d8f06-221">對 [登入 URL] 輸入您 API 管理服務的 URL，並且附加 `/signin`。</span><span class="sxs-lookup"><span data-stu-id="d8f06-221">For **Sign-on URL** enter the URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="d8f06-222">在此範例中使用 `https://contoso5.portal.azure-api.net/signin` 。</span><span class="sxs-lookup"><span data-stu-id="d8f06-222">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="d8f06-223">對 [應用程式識別碼 URL] 輸入您 API 管理服務的 URL，並且附加一些唯一字元。</span><span class="sxs-lookup"><span data-stu-id="d8f06-223">For **App Id URL** enter the URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="d8f06-224">這些字元可以是任何想要的字元，在此範例中使用 `https://contoso5.portal.azure-api.net/dp`。</span><span class="sxs-lookup"><span data-stu-id="d8f06-224">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="d8f06-225">設定想要的 [應用程式屬性] 之後，按一下核取記號以建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8f06-225">When the  desired **App properties** are configured, click the check mark to create the application.</span></span>

![新增應用程式][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="d8f06-227">設定 API 管理 OAuth 2.0 授權伺服器</span><span class="sxs-lookup"><span data-stu-id="d8f06-227">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="d8f06-228">下一步是在 API 管理中設定 OAuth 2.0 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="d8f06-228">The next step is to configure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="d8f06-229">這個步驟會從視訊的 9:43 開始示範。</span><span class="sxs-lookup"><span data-stu-id="d8f06-229">This step is demonstrated in the video starting at 9:43.</span></span>

<span data-ttu-id="d8f06-230">從左側的 [API 管理] 功能表按一下 [安全性]，然後依序按一下 [OAuth 2.0] 和 [新增授權伺服器]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-230">Click **Security** from the API Management menu on the left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![新增授權伺服器][api-management-add-authorization-server]

<span data-ttu-id="d8f06-232">在 [名稱] 和 [說明] 欄位中輸入名稱和選擇性的說明。</span><span class="sxs-lookup"><span data-stu-id="d8f06-232">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> <span data-ttu-id="d8f06-233">這些欄位是用來在 API 管理服務執行個體中識別 OAuth 2.0 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="d8f06-233">These fields are used to identify the OAuth 2.0 authorization server within the API Management service instance.</span></span> <span data-ttu-id="d8f06-234">在此範例中使用**授權伺服器示範**。</span><span class="sxs-lookup"><span data-stu-id="d8f06-234">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="d8f06-235">稍後當您指定要用於 API 驗證的 OAuth 2.0 伺服器時，您要選取這個名稱。</span><span class="sxs-lookup"><span data-stu-id="d8f06-235">Later when you specify an OAuth 2.0 server to be used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="d8f06-236">針對 [用戶端註冊頁面 URL]**`http://localhost` 輸入如** 的預留位置值。</span><span class="sxs-lookup"><span data-stu-id="d8f06-236">For the **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="d8f06-237">[用戶端註冊頁面 URL] 指向使用者可用來建立和設定其對 OAuth 2.0 提供者之專屬帳戶的頁面，而提供者支援使用者帳戶管理。</span><span class="sxs-lookup"><span data-stu-id="d8f06-237">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="d8f06-238">在此範例中，使用者沒有建立和設定自己的帳戶，因此使用預留位置。</span><span class="sxs-lookup"><span data-stu-id="d8f06-238">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![新增授權伺服器][api-management-add-authorization-server-1]

<span data-ttu-id="d8f06-240">接著，指定 [授權端點 URL] 和 [權杖端點 URL]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-240">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![授權伺服器][api-management-add-authorization-server-1a]

<span data-ttu-id="d8f06-242">這些值可以從您為開發人員入口網站建立的 AAD 應用程式的 [App 端點]  頁面擷取。</span><span class="sxs-lookup"><span data-stu-id="d8f06-242">These values can be retrieved from the **App Endpoints** page of the AAD application you created for the developer portal.</span></span> <span data-ttu-id="d8f06-243">若要存取端點，請瀏覽到 AAD 應用程式的 [設定] 索引標籤，然後按一下 [檢視端點]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-243">To access the endpoints navigate to the **Configure** tab for the AAD application and click **View endpoints**.</span></span>

![應用程式][api-management-aad-devportal-application]

![檢視端點][api-management-aad-view-endpoints]

<span data-ttu-id="d8f06-246">複製 [OAuth 2.0 授權端點] 並貼到 [授權端點 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="d8f06-246">Copy the **OAuth 2.0 authorization endpoint** and paste it into the **Authorization endpoint URL** textbox.</span></span>

![新增授權伺服器][api-management-add-authorization-server-2]

<span data-ttu-id="d8f06-248">複製 [OAuth 2.0 權杖端點] 並貼到 [權杖端點 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="d8f06-248">Copy the **OAuth 2.0 token endpoint** and paste it into the **Token endpoint URL** textbox.</span></span>

![新增授權伺服器][api-management-add-authorization-server-2a]

<span data-ttu-id="d8f06-250">除了貼上權杖端點，請新增名為 **resource** 的其他主體參數，值則使用發佈 Visual Studio 專案時建立的後端服務的 AAD 應用程式的 [應用程式識別碼 URI]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-250">In addition to pasting in the token endpoint, add an additional body parameter named **resource** and for the value use the **App Id URI** from the AAD application for the backend service that was created when the Visual Studio project was published.</span></span>

![App 識別碼 URI][api-management-aad-sso-uri]

<span data-ttu-id="d8f06-252">接著，指定用戶端認證。</span><span class="sxs-lookup"><span data-stu-id="d8f06-252">Next, specify the client credentials.</span></span> <span data-ttu-id="d8f06-253">這些是您想要存取之資源 (在此案例中是開發人員入口網站) 的認證。</span><span class="sxs-lookup"><span data-stu-id="d8f06-253">These are the credentials for the resource you want to access, in this case the developer portal.</span></span>

![用戶端認證][api-management-client-credentials]

<span data-ttu-id="d8f06-255">若要取得 [用戶端識別碼]，請瀏覽到開發人員入口網站之 AAD 應用程式的 [設定] 索引標籤，然後複製 [用戶端識別碼]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-255">To get the **Client Id**, navigate to the **Configure** tab of the AAD application for the developer portal and copy the **Client Id**.</span></span>

<span data-ttu-id="d8f06-256">若要取得 [用戶端密碼]，請按一下 [金鑰] 區段中的 [選取持續時間] 下拉式清單，然後指定間隔。</span><span class="sxs-lookup"><span data-stu-id="d8f06-256">To get the **Client Secret** click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="d8f06-257">在此範例中使用 1 年。</span><span class="sxs-lookup"><span data-stu-id="d8f06-257">In this example 1 year is used.</span></span>

![用戶端識別碼][api-management-aad-client-id]

<span data-ttu-id="d8f06-259">按一下 [ **儲存** ] 以儲存組態並顯示金鑰。</span><span class="sxs-lookup"><span data-stu-id="d8f06-259">Click **Save** to save the configuration and display the key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d8f06-260">記下此金鑰。</span><span class="sxs-lookup"><span data-stu-id="d8f06-260">Make a note of this key.</span></span> <span data-ttu-id="d8f06-261">關閉 Azure Active Directory 組態視窗之後，即無法再次顯示金鑰。</span><span class="sxs-lookup"><span data-stu-id="d8f06-261">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="d8f06-262">將金鑰複製到剪貼簿、切換回發佈者入口網站、將金鑰貼入 [用戶端密碼] 文字方塊中，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-262">Copy the key to the clipboard, switch back to the publisher portal, paste the key into the **Client Secret** textbox, and click **Save**.</span></span>

![新增授權伺服器][api-management-add-authorization-server-3]

<span data-ttu-id="d8f06-264">緊接在用戶端認證後面的是授權碼授與。</span><span class="sxs-lookup"><span data-stu-id="d8f06-264">Immediately following the client credentials is an authorization code grant.</span></span> <span data-ttu-id="d8f06-265">複製此授權碼並切換回 Azure AD 開發人員入口網站應用程式設定頁面，將授權授與貼入 [回覆 URL] 欄位，然後再按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-265">Copy this authorization code and switch back to your Azure AD developer portal application configure page, and paste the authorization grant into the **Reply URL** field, and click **Save** again.</span></span>

![回覆 URL][api-management-aad-reply-url]

<span data-ttu-id="d8f06-267">下一步是設定開發人員入口網站 AAD 應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="d8f06-267">The next step is to configure the permissions for the developer portal AAD application.</span></span> <span data-ttu-id="d8f06-268">按一下 [應用程式權限]，然後核取 [讀取目錄資料] 的方塊。</span><span class="sxs-lookup"><span data-stu-id="d8f06-268">Click **Application Permissions** and check the box for **Read directory data**.</span></span> <span data-ttu-id="d8f06-269">按一下 [儲存] 以儲存這項變更，然後按一下 [新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-269">Click **Save** to save this change, and then click **Add application**.</span></span>

![新增權限][api-management-add-devportal-permissions]

<span data-ttu-id="d8f06-271">按一下搜尋圖示，在 [開頭為] 方塊中輸入 **APIM**，選取 [APIMAADDemo]，然後按一下核取記號儲存。</span><span class="sxs-lookup"><span data-stu-id="d8f06-271">Click the search icon, type **APIM** into the Starting with box, select **APIMAADDemo**, and click the check mark to save.</span></span>

![新增權限][api-management-aad-add-app-permissions]

<span data-ttu-id="d8f06-273">按一下 [APIMAADDemo] 的 [委派權限]，核取 [存取 APIMAADDemo] 的方塊，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-273">Click **Delegated Permissions** for **APIMAADDemo** and check the box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="d8f06-274">這樣就允許開發人員入口網站應用程式存取後端服務。</span><span class="sxs-lookup"><span data-stu-id="d8f06-274">This allows the developer portal application to access the backend service.</span></span>

![新增權限][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-the-calculator-api"></a><span data-ttu-id="d8f06-276">啟用計算機 API 的 OAuth 2.0 使用者授權</span><span class="sxs-lookup"><span data-stu-id="d8f06-276">Enable OAuth 2.0 user authorization for the Calculator API</span></span>
<span data-ttu-id="d8f06-277">現在已經設定好 OAuth 2.0 伺服器，您可以在安全性設定中為您的 API 指定此伺服器。</span><span class="sxs-lookup"><span data-stu-id="d8f06-277">Now that the OAuth 2.0 server is configured, you can specify it in the security settings for your API.</span></span> <span data-ttu-id="d8f06-278">這個步驟會從視訊的 14:30 開始示範。</span><span class="sxs-lookup"><span data-stu-id="d8f06-278">This step is demonstrated in the video starting at 14:30.</span></span>

<span data-ttu-id="d8f06-279">按一下左側功能表中的 [API]，然後按一下 [計算機] 來檢視和設定其設定。</span><span class="sxs-lookup"><span data-stu-id="d8f06-279">Click **APIs** in the left menu, and click  **Calculator** to view and configure its settings.</span></span>

![計算機 API][api-management-calc-api]

<span data-ttu-id="d8f06-281">瀏覽到 [安全性] 索引標籤，核取 [OAuth 2.0] 核取方塊，從 [授權伺服器] 下拉式清單選取想要的授權伺服器，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-281">Navigate to the **Security** tab, check the **OAuth 2.0** checkbox, select the desired authorization server from the **Authorization server** drop-down, and click **Save**.</span></span>

![計算機 API][api-management-enable-aad-calculator]

## <a name="successfully-call-the-calculator-api-from-the-developer-portal"></a><span data-ttu-id="d8f06-283">從開發人員入口網站成功呼叫計算機 API</span><span class="sxs-lookup"><span data-stu-id="d8f06-283">Successfully call the Calculator API from the developer portal</span></span>
<span data-ttu-id="d8f06-284">現在已經在 API 上設定好 OAuth 2.0 授權，就可以從開發人員中心成功呼叫其運算。</span><span class="sxs-lookup"><span data-stu-id="d8f06-284">Now that the OAuth 2.0 authorization is configured on the API, its operations can be successfully called from the developer center.</span></span> <span data-ttu-id="d8f06-285">這個步驟會從視訊的 15:00 開始示範。</span><span class="sxs-lookup"><span data-stu-id="d8f06-285">THis step is demonstrated in the video starting at 15:00.</span></span>

<span data-ttu-id="d8f06-286">瀏覽回到開發人員入口網站中計算機服務的 [相加兩個整數] 運算，然後按一下 [試試看]。</span><span class="sxs-lookup"><span data-stu-id="d8f06-286">Navigate back to the **Add two integers** operation of the calculator service in the developer portal and click **Try it**.</span></span> <span data-ttu-id="d8f06-287">請注意，在 [授權]  區段中的新項目對應到您剛才加入的授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="d8f06-287">Note the new item in the **Authorization** section corresponding to the authorization server you just added.</span></span>

![計算機 API][api-management-calc-authorization-server]

<span data-ttu-id="d8f06-289">從授權下拉式清單選取 [授權碼]  ，然後輸入要使用的帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="d8f06-289">Select **Authorization code** from the authorization drop-down list and enter the credentials of the account to use.</span></span> <span data-ttu-id="d8f06-290">如果您已經使用帳戶登入，就不會提示您。</span><span class="sxs-lookup"><span data-stu-id="d8f06-290">If you are already signed in with the account you may not be prompted.</span></span>

![計算機 API][api-management-devportal-authorization-code]

<span data-ttu-id="d8f06-292">按一下 [傳送]，注意 [回應狀態] 為 [200 確定]，以及回應內容中的運算結果。</span><span class="sxs-lookup"><span data-stu-id="d8f06-292">Click **Send** and note the **Response status** of **200 OK** and the results of the operation in the response content.</span></span>

![計算機 API][api-management-devportal-response]

## <a name="configure-a-desktop-application-to-call-the-api"></a><span data-ttu-id="d8f06-294">設定桌面應用程式呼叫 API</span><span class="sxs-lookup"><span data-stu-id="d8f06-294">Configure a desktop application to call the API</span></span>
<span data-ttu-id="d8f06-295">視訊中的下一個程序從 16:30 開始，設定簡單的桌面應用程式呼叫 API。</span><span class="sxs-lookup"><span data-stu-id="d8f06-295">The next procedure in the video starts at 16:30 and configures a simple desktop application to call the API.</span></span> <span data-ttu-id="d8f06-296">第一個步驟是在 Azure AD 中註冊桌面應用程式，並且讓它能夠存取目錄和後端服務。</span><span class="sxs-lookup"><span data-stu-id="d8f06-296">The first step is to register the desktop application in Azure AD and give it access to the directory and to the backend service.</span></span> <span data-ttu-id="d8f06-297">在 18:25 處示範桌面應用程式呼叫計算機 API 的運算。</span><span class="sxs-lookup"><span data-stu-id="d8f06-297">At 18:25 there is a demonstration of the desktop application calling an operation on the calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-to-pre-authorize-requests"></a><span data-ttu-id="d8f06-298">設定 JWT 驗證原則來預先授權要求</span><span class="sxs-lookup"><span data-stu-id="d8f06-298">Configure a JWT validation policy to pre-authorize requests</span></span>
<span data-ttu-id="d8f06-299">最後的程序從視訊的 20:48 開始，示範如何使用 [驗證 JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) 原則，藉由驗證每個傳入要求的存取權杖來預先授權要求。</span><span class="sxs-lookup"><span data-stu-id="d8f06-299">The final procedure in the video starts at 20:48 and shows you how to use the [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy to pre-authorize requests by validating the access tokens of each incoming request.</span></span> <span data-ttu-id="d8f06-300">如果要求沒有經過「驗證 JWT」原則驗證，要求就會被 API 管理封鎖而不會傳入後端。</span><span class="sxs-lookup"><span data-stu-id="d8f06-300">If the request is not validated by the Validate JWT policy, the request is blocked by API Management and is not passed along to the backend.</span></span>

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

<span data-ttu-id="d8f06-301">如需設定和使用此原則的另一個示範，請觀賞 [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ，向前快轉到 13:50。</span><span class="sxs-lookup"><span data-stu-id="d8f06-301">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="d8f06-302">向前快轉到 15:00 可看到在原則編輯器中設定的原則，再到 18:50 可以看到一個示範，從開發人員入口網站 (使用和不使用必要的授權權杖) 呼叫運算。</span><span class="sxs-lookup"><span data-stu-id="d8f06-302">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8f06-303">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8f06-303">Next steps</span></span>
* <span data-ttu-id="d8f06-304">查看更多有關 API 管理的 [視訊](https://azure.microsoft.com/documentation/videos/index/?services=api-management) 。</span><span class="sxs-lookup"><span data-stu-id="d8f06-304">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="d8f06-305">如需其他保護後端服務的方式，請參閱[相互憑證驗證](api-management-howto-mutual-certificates.md)。</span><span class="sxs-lookup"><span data-stu-id="d8f06-305">For other ways to secure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

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
