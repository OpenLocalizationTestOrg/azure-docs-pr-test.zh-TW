---
title: "aaaCustomize Swashbuckle 產生應用程式開發介面定義"
description: "深入了解如何在 Azure App Service API 應用程式產生的 Swashbuckle toocustomize Swagger 應用程式開發介面定義。"
services: app-service\api
documentationcenter: .net
author: bradygaster
manager: erikre
editor: jimbe
ms.assetid: 6b8cbc38-d282-4a0f-b0c5-762631bae6f3
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: e31c665f8993533c5ec9a935e42cce34f86a5ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a><span data-ttu-id="1f1fe-103">自訂 Swashbuckle 產生的 API 定義</span><span class="sxs-lookup"><span data-stu-id="1f1fe-103">Customize Swashbuckle-generated API definitions</span></span>
## <a name="overview"></a><span data-ttu-id="1f1fe-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1f1fe-104">Overview</span></span>
<span data-ttu-id="1f1fe-105">這篇文章說明如何 toocustomize Swashbuckle toohandle 常見案例中，您可能 tooalter hello 預設行為：</span><span class="sxs-lookup"><span data-stu-id="1f1fe-105">This article explains how toocustomize Swashbuckle toohandle common scenarios where you may want tooalter hello default behavior:</span></span>

* <span data-ttu-id="1f1fe-106">Swashbuckle 針對控制器方法的多載產生重複作業辨識碼</span><span class="sxs-lookup"><span data-stu-id="1f1fe-106">Swashbuckle generates duplicate operation identifiers for overloads of controller methods</span></span>
* <span data-ttu-id="1f1fe-107">Swashbuckle 只從方法的有效回應 HTTP 200 （確定），假設該 hello</span><span class="sxs-lookup"><span data-stu-id="1f1fe-107">Swashbuckle assumes that hello only valid response from a method is HTTP 200 (OK)</span></span> 

## <a name="customize-operation-identifier-generation"></a><span data-ttu-id="1f1fe-108">自訂作業識別碼產生</span><span class="sxs-lookup"><span data-stu-id="1f1fe-108">Customize operation identifier generation</span></span>
<span data-ttu-id="1f1fe-109">Swashbuckle 會藉由串連控制器名稱與方法名稱來產生 Swagger 作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-109">Swashbuckle generates Swagger operation identifiers by concatenating controller name and method name.</span></span> <span data-ttu-id="1f1fe-110">當一個方法的多個多載時，此模式會產生問題：Swashbuckle 會產生重複的作業識別碼，這是無效的 Swagger JSON。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-110">This pattern creates a problem when you have multiple overloads of a method: Swashbuckle generates duplicate operation ids, which is invalid Swagger JSON.</span></span>

<span data-ttu-id="1f1fe-111">例如，hello 遵循控制器的程式碼會造成 Swashbuckle toogenerate 三個 Contact_Get 作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-111">For example, hello following controller code causes Swashbuckle toogenerate three Contact_Get operation ids.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

<span data-ttu-id="1f1fe-112">您可以提供唯一的名稱，例如此範例中的 hello 下列 hello 方法，以手動方式解決 hello 問題：</span><span class="sxs-lookup"><span data-stu-id="1f1fe-112">You can solve hello problem manually by giving hello methods unique names, such as hello following for this example:</span></span>

* <span data-ttu-id="1f1fe-113">取得</span><span class="sxs-lookup"><span data-stu-id="1f1fe-113">Get</span></span>
* <span data-ttu-id="1f1fe-114">GetById</span><span class="sxs-lookup"><span data-stu-id="1f1fe-114">GetById</span></span>
* <span data-ttu-id="1f1fe-115">GetPage</span><span class="sxs-lookup"><span data-stu-id="1f1fe-115">GetPage</span></span>

<span data-ttu-id="1f1fe-116">hello 的替代方式是 tooextend Swashbuckle toomake，它會自動產生的唯一作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-116">hello alternative is tooextend Swashbuckle toomake it automatically generate unique operation ids.</span></span>

<span data-ttu-id="1f1fe-117">hello 下列步驟示範如何使用 toocustomize Swashbuckle hello *SwaggerConfig.cs* hello Visual Studio 應用程式開發介面應用程式預覽專案範本包含 hello 專案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-117">hello following steps show how toocustomize Swashbuckle by using hello *SwaggerConfig.cs* file that is included in hello project by hello Visual Studio API Apps Preview project template.</span></span>  <span data-ttu-id="1f1fe-118">您也可以在您設定以供部署為 API 應用程式的 Web API 專案中自訂 Swashbuckle。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-118">You can also customize Swashbuckle in a Web API project that you configure for deployment as an API app.</span></span>

1. <span data-ttu-id="1f1fe-119">建立自訂 `IOperationFilter` 實作</span><span class="sxs-lookup"><span data-stu-id="1f1fe-119">Create a custom `IOperationFilter` implementation</span></span> 
   
    <span data-ttu-id="1f1fe-120">hello`IOperationFilter`介面提供的擴充性點想 toocustomize Swashbuckle 使用者 hello Swagger 中繼資料的程序的各個層面。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-120">hello `IOperationFilter` interface provides an extensibility point for Swashbuckle users who want toocustomize various aspects of hello Swagger metadata process.</span></span> <span data-ttu-id="1f1fe-121">hello 下列程式碼示範一種方法的變更 hello 作業 id 產生行為。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-121">hello following code demonstrates one method of changing hello operation-id-generation behavior.</span></span> <span data-ttu-id="1f1fe-122">hello 程式碼會附加參數名稱 toohello 作業識別碼名稱。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-122">hello code appends parameter names toohello operation id name.</span></span>  
   
        using Swashbuckle.Swagger;
        using System.Web.Http.Description;
   
        namespace ContactsList
        {
            public class MultipleOperationsWithSameVerbFilter : IOperationFilter
            {
                public void Apply(
                    Operation operation,
                    SchemaRegistry schemaRegistry,
                    ApiDescription apiDescription)
                {
                    if (operation.parameters != null)
                    {
                        operation.operationId += "By";
                        foreach (var parm in operation.parameters)
                        {
                            operation.operationId += string.Format("{0}",parm.name);
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="1f1fe-123">在*App_Start\SwaggerConfig.cs*檔案，呼叫 hello`OperationFilter`方法 toocause Swashbuckle toouse hello 新`IOperationFilter`實作。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-123">In *App_Start\SwaggerConfig.cs* file, call hello `OperationFilter` method toocause Swashbuckle toouse hello new `IOperationFilter` implementation.</span></span>
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    <span data-ttu-id="1f1fe-124">hello *SwaggerConfig.cs* hello Swashbuckle NuGet 封裝來卸除的檔案包含許多標記為註解範例的擴充點。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-124">hello *SwaggerConfig.cs* file that is dropped in by hello Swashbuckle NuGet package contains many commented-out examples of extensibility points.</span></span> <span data-ttu-id="1f1fe-125">此處未顯示 hello 其他註解。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-125">hello additional comments are not shown here.</span></span> 
   
    <span data-ttu-id="1f1fe-126">進行這項變更之後您`IOperationFilter`實作會使用，而且會導致產生的唯一作業識別碼 toobe。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-126">After you make this change, your `IOperationFilter` implementation is used and causes unique operation ids toobe generated.</span></span>
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a><span data-ttu-id="1f1fe-127">允許 200 以外的回應碼</span><span class="sxs-lookup"><span data-stu-id="1f1fe-127">Allow response codes other than 200</span></span>
<span data-ttu-id="1f1fe-128">根據預設，Swashbuckle 假設 HTTP 200 （確定） 回應 hello*只*合法從 Web 應用程式開發介面方法的回應。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-128">By default, Swashbuckle assumes that an HTTP 200 (OK) response is hello *only* legitimate response from a Web API method.</span></span> <span data-ttu-id="1f1fe-129">在某些情況下，您可能想 tooreturn 其他回應碼而不會造成 hello 用戶端 tooraise 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-129">In some cases, you may want tooreturn other response codes without causing hello client tooraise an exception.</span></span>  <span data-ttu-id="1f1fe-130">比方說，hello 下列 Web 應用程式開發介面程式碼示範的案例中，您會想 hello 用戶端 tooaccept 200 或 404 有效回應。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-130">For example, hello following Web API code demonstrates a scenario in which you would want hello client tooaccept either a 200 or a 404 as valid responses.</span></span>

    [ResponseType(typeof(Contact))]
    public HttpResponseMessage Get(int id)
    {
        var contacts = GetContacts();

        var requestedContact = contacts.FirstOrDefault(x => x.Id == id);

        if (requestedContact == null)
        {
            return Request.CreateResponse(HttpStatusCode.NotFound);
        }
        else
        {
            return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
        }
    }

<span data-ttu-id="1f1fe-131">在此案例中，hello Swashbuckle 會預設產生的 Swagger 指定只有一個合法 HTTP 狀態碼，HTTP 200。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-131">In this scenario, hello Swagger that Swashbuckle generates by default specifies only one legitimate HTTP status code, HTTP 200.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

<span data-ttu-id="1f1fe-132">因為 Visual Studio 會針對 hello 用戶端使用 hello Swagger API 定義 toogenerate 程式碼，它會建立會引發例外狀況的任何回應 HTTP 200 以外的用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-132">Since Visual Studio uses hello Swagger API definition toogenerate code for hello client, it creates client code that raises an exception for any response other than an HTTP 200.</span></span> <span data-ttu-id="1f1fe-133">hello 的下列程式碼是從產生此範例 Web 應用程式開發介面方法的 C# 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-133">hello code below is from a C# client generated for this sample Web API method.</span></span>

    if (statusCode != HttpStatusCode.OK)
    {
        HttpOperationException<object> ex = new HttpOperationException<object>();
        ex.Request = httpRequest;
        ex.Response = httpResponse;
        ex.Body = null;
        if (shouldTrace)
        {
            ServiceClientTracing.Error(invocationId, ex);
        }
        throw ex;
    } 

<span data-ttu-id="1f1fe-134">Swashbuckle 提供兩種自訂的預期它產生的 HTTP 回應碼 hello 清單使用 XML 註解或 hello`SwaggerResponse`屬性。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-134">Swashbuckle provides two ways of customizing hello list of expected HTTP response codes that it generates, using XML comments or hello `SwaggerResponse` attribute.</span></span> <span data-ttu-id="1f1fe-135">hello 屬性比較簡單，但是它只是用於 Swashbuckle 5.1.5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-135">hello attribute is easier, but it is only available in Swashbuckle 5.1.5 or later.</span></span> <span data-ttu-id="1f1fe-136">hello API 應用程式預覽新專案範本在 Visual Studio 2013 包括 Swashbuckle 版本 5.0.0，因此，如果您使用 hello 範本，而不想 tooupdate Swashbuckle，唯一的選擇就 toouse XML 註解。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-136">hello API Apps preview new-project template in Visual Studio 2013 includes Swashbuckle version 5.0.0, so if you used hello template and don't want tooupdate Swashbuckle, your only option is toouse XML comments.</span></span> 

### <a name="customize-expected-response-codes-using-xml-comments"></a><span data-ttu-id="1f1fe-137">使用 XML 註解自訂預期的回應碼</span><span class="sxs-lookup"><span data-stu-id="1f1fe-137">Customize expected response codes using XML comments</span></span>
<span data-ttu-id="1f1fe-138">如果您 Swashbuckle 版本早於 5.1.5，請使用此方法 toospecify 回應碼。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-138">Use this method toospecify response codes if your Swashbuckle version is earlier than 5.1.5.</span></span>

1. <span data-ttu-id="1f1fe-139">首先，透過 HTTP 回應碼，如想 toospecify hello 方法中加入 XML 文件註解。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-139">First, add XML documentation comments over hello methods you wish toospecify HTTP response codes for.</span></span> <span data-ttu-id="1f1fe-140">採取任何行動 hello 範例 Web 應用程式開發介面顯示於上方並套用 hello XML 文件 tooit 會導致 hello 下列範例類似的程式碼。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-140">Taking hello sample Web API action shown above and applying hello XML documentation tooit would result in code like hello following example.</span></span> 
   
        /// <summary>
        /// Returns hello specified contact.
        /// </summary>
        /// <param name="id">hello ID of hello contact.</param>
        /// <returns>A contact record with an HTTP 200, or null with an HTTP 404.</returns>
        /// <response code="200">OK</response>
        /// <response code="404">Not Found</response>
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
   
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
2. <span data-ttu-id="1f1fe-141">新增指示在 hello *SwaggerConfig.cs*檔案 toodirect Swashbuckle toomake 使用 hello XML 文件檔。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-141">Add instructions in hello *SwaggerConfig.cs* file toodirect Swashbuckle toomake use of hello XML documentation file.</span></span>
   
   * <span data-ttu-id="1f1fe-142">開啟*SwaggerConfig.cs* hello 上建立一個方法*SwaggerConfig*類別 toospecify hello 路徑 toohello 文件 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-142">Open *SwaggerConfig.cs* and create a method on hello *SwaggerConfig* class toospecify hello path toohello documentation XML file.</span></span> 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * <span data-ttu-id="1f1fe-143">Hello 中向下捲動*SwaggerConfig.cs*直至您看見 hello 標記為註解線條，類似一個框住 hello 下列螢幕擷取畫面的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-143">Scroll down in hello *SwaggerConfig.cs* file until you see hello commented-out line of code resembling hello screen shot below.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * <span data-ttu-id="1f1fe-144">取消註解 hello 行 tooenable hello XML 註解 Swagger 產生期間所處理。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-144">Uncomment hello line tooenable hello XML comments processing during Swagger generation.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. <span data-ttu-id="1f1fe-145">順序 toogenerate hello XML 文件檔移入 hello 專案屬性並啟用 hello 的 XML 文件檔中 hello 以下螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-145">In order toogenerate hello XML documentation file, go into hello project's properties and enable hello XML documentation file as shown in hello screenshot below.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

<span data-ttu-id="1f1fe-146">一旦您執行這些步驟，hello Swashbuckle 所產生的 Swagger JSON 會反映在 hello XML 註解中所指定的 hello HTTP 回應碼。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-146">Once you perform these steps, hello Swagger JSON generated by Swashbuckle will reflect hello HTTP response codes that you specified in hello XML comments.</span></span> <span data-ttu-id="1f1fe-147">hello 以下螢幕擷取畫面會示範這個新的 JSON 裝載。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-147">hello screenshot below demonstrates this new JSON payload.</span></span> 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

<span data-ttu-id="1f1fe-148">當您使用 Visual Studio tooregenerate hello 用戶端程式碼的 REST API 時，hello C# 程式碼會接受兩個 hello HTTP OK，而且找不到狀態碼而不會引發例外狀況，允許使用的程式碼 toomake 決策上 toohandle hello 傳回的 null 值的方式請連絡記錄。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-148">When you use Visual Studio tooregenerate hello client code for your REST API, hello C# code accepts both hello HTTP OK and Not Found status codes without raising an exception, allowing your consuming code toomake decisions on how toohandle hello return of a null Contact record.</span></span> 

        if (statusCode != HttpStatusCode.OK && statusCode != HttpStatusCode.NotFound)
        {
            HttpOperationException<object> ex = new HttpOperationException<object>();
            ex.Request = httpRequest;
            ex.Response = httpResponse;
            ex.Body = null;
            if (shouldTrace)
            {
                ServiceClientTracing.Error(invocationId, ex);
            }
                throw ex;
        }

<span data-ttu-id="1f1fe-149">此示範中的 hello 程式碼位於[這個 GitHub 儲存機制](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse)。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-149">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span></span> <span data-ttu-id="1f1fe-150">Hello Web API 以 XML 文件註解標記的專案會包含產生的用戶端，此 api 的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-150">Along with hello Web API project marked up with XML documentation comments is a Console Application project that contains a generated client for this API.</span></span> 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a><span data-ttu-id="1f1fe-151">自訂使用 hello SwaggerResponse 屬性預期的回應碼</span><span class="sxs-lookup"><span data-stu-id="1f1fe-151">Customize expected response codes using hello SwaggerResponse attribute</span></span>
<span data-ttu-id="1f1fe-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs)屬性是用於 Swashbuckle 5.1.5 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribute is available in Swashbuckle 5.1.5 and later.</span></span> <span data-ttu-id="1f1fe-153">如果您在專案中有較早版本，本節一開始會說明如何 tooupdate hello Swashbuckle NuGet 封裝，這樣您就可以使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-153">In case you have an earlier version in your project, this section starts by explaining how tooupdate hello Swashbuckle NuGet package so that you can use this attribute.</span></span>

1. <span data-ttu-id="1f1fe-154">在 [方案總管] 中，以滑鼠右鍵按一下您的專案並選擇 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-154">In **Solution Explorer**, right-click your Web API project and click **Manage NuGet Packages**.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. <span data-ttu-id="1f1fe-155">按一下 hello*更新*按鈕的下一個 toohello *Swashbuckle* NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-155">Click hello *Update* button next toohello *Swashbuckle* NuGet package.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. <span data-ttu-id="1f1fe-156">新增 hello *SwaggerResponse*屬性 toohello Web API 的動作方法，您會想 toospecify 有效的 HTTP 回應碼。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-156">Add hello *SwaggerResponse* attributes toohello Web API action methods for which you want toospecify valid HTTP response codes.</span></span> 
   
        [SwaggerResponse(HttpStatusCode.OK)]
        [SwaggerResponse(HttpStatusCode.NotFound)]
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
4. <span data-ttu-id="1f1fe-157">新增`using`hello 屬性的命名空間陳述式：</span><span class="sxs-lookup"><span data-stu-id="1f1fe-157">Add a `using` statement for hello attribute's namespace:</span></span>
   
        using Swashbuckle.Swagger.Annotations;
5. <span data-ttu-id="1f1fe-158">瀏覽 toohello */swagger/docs/v1* URL，您的專案與 hello 各種 HTTP 回應碼會顯示在 hello Swagger JSON。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-158">Browse toohello */swagger/docs/v1* URL of your project and hello various HTTP response codes will be visible in hello Swagger JSON.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

<span data-ttu-id="1f1fe-159">此示範中的 hello 程式碼位於[這個 GitHub 儲存機制](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes)。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-159">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span></span> <span data-ttu-id="1f1fe-160">Web API 專案裝飾以 hello 以及 hello *SwaggerResponse*屬性會包含產生的用戶端，此 api 的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-160">Along with hello Web API project decorated with hello *SwaggerResponse* attribute is a Console Application project that contains a generated client for this API.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1f1fe-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f1fe-161">Next steps</span></span>
<span data-ttu-id="1f1fe-162">這篇文章已示範 toocustomize hello 方式 Swashbuckle 會產生作業的識別碼和有效的回應碼。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-162">This article has shown how toocustomize hello way Swashbuckle generates operation ids and valid response codes.</span></span> <span data-ttu-id="1f1fe-163">如需詳細資訊，請參閱 [GitHub 上的 Swashbuckle](https://github.com/domaindrivendev/Swashbuckle)。</span><span class="sxs-lookup"><span data-stu-id="1f1fe-163">For more information, see [Swashbuckle on GitHub](https://github.com/domaindrivendev/Swashbuckle).</span></span>

