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
# <a name="customize-swashbuckle-generated-api-definitions"></a>自訂 Swashbuckle 產生的 API 定義
## <a name="overview"></a>概觀
這篇文章說明如何 toocustomize Swashbuckle toohandle 常見案例中，您可能 tooalter hello 預設行為：

* Swashbuckle 針對控制器方法的多載產生重複作業辨識碼
* Swashbuckle 只從方法的有效回應 HTTP 200 （確定），假設該 hello 

## <a name="customize-operation-identifier-generation"></a>自訂作業識別碼產生
Swashbuckle 會藉由串連控制器名稱與方法名稱來產生 Swagger 作業識別碼。 當一個方法的多個多載時，此模式會產生問題：Swashbuckle 會產生重複的作業識別碼，這是無效的 Swagger JSON。

例如，hello 遵循控制器的程式碼會造成 Swashbuckle toogenerate 三個 Contact_Get 作業識別碼。

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

您可以提供唯一的名稱，例如此範例中的 hello 下列 hello 方法，以手動方式解決 hello 問題：

* 取得
* GetById
* GetPage

hello 的替代方式是 tooextend Swashbuckle toomake，它會自動產生的唯一作業識別碼。

hello 下列步驟示範如何使用 toocustomize Swashbuckle hello *SwaggerConfig.cs* hello Visual Studio 應用程式開發介面應用程式預覽專案範本包含 hello 專案中的檔案。  您也可以在您設定以供部署為 API 應用程式的 Web API 專案中自訂 Swashbuckle。

1. 建立自訂 `IOperationFilter` 實作 
   
    hello`IOperationFilter`介面提供的擴充性點想 toocustomize Swashbuckle 使用者 hello Swagger 中繼資料的程序的各個層面。 hello 下列程式碼示範一種方法的變更 hello 作業 id 產生行為。 hello 程式碼會附加參數名稱 toohello 作業識別碼名稱。  
   
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
2. 在*App_Start\SwaggerConfig.cs*檔案，呼叫 hello`OperationFilter`方法 toocause Swashbuckle toouse hello 新`IOperationFilter`實作。
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    hello *SwaggerConfig.cs* hello Swashbuckle NuGet 封裝來卸除的檔案包含許多標記為註解範例的擴充點。 此處未顯示 hello 其他註解。 
   
    進行這項變更之後您`IOperationFilter`實作會使用，而且會導致產生的唯一作業識別碼 toobe。
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>允許 200 以外的回應碼
根據預設，Swashbuckle 假設 HTTP 200 （確定） 回應 hello*只*合法從 Web 應用程式開發介面方法的回應。 在某些情況下，您可能想 tooreturn 其他回應碼而不會造成 hello 用戶端 tooraise 例外狀況。  比方說，hello 下列 Web 應用程式開發介面程式碼示範的案例中，您會想 hello 用戶端 tooaccept 200 或 404 有效回應。

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

在此案例中，hello Swashbuckle 會預設產生的 Swagger 指定只有一個合法 HTTP 狀態碼，HTTP 200。

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

因為 Visual Studio 會針對 hello 用戶端使用 hello Swagger API 定義 toogenerate 程式碼，它會建立會引發例外狀況的任何回應 HTTP 200 以外的用戶端程式碼。 hello 的下列程式碼是從產生此範例 Web 應用程式開發介面方法的 C# 用戶端。

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

Swashbuckle 提供兩種自訂的預期它產生的 HTTP 回應碼 hello 清單使用 XML 註解或 hello`SwaggerResponse`屬性。 hello 屬性比較簡單，但是它只是用於 Swashbuckle 5.1.5 或更新版本。 hello API 應用程式預覽新專案範本在 Visual Studio 2013 包括 Swashbuckle 版本 5.0.0，因此，如果您使用 hello 範本，而不想 tooupdate Swashbuckle，唯一的選擇就 toouse XML 註解。 

### <a name="customize-expected-response-codes-using-xml-comments"></a>使用 XML 註解自訂預期的回應碼
如果您 Swashbuckle 版本早於 5.1.5，請使用此方法 toospecify 回應碼。

1. 首先，透過 HTTP 回應碼，如想 toospecify hello 方法中加入 XML 文件註解。 採取任何行動 hello 範例 Web 應用程式開發介面顯示於上方並套用 hello XML 文件 tooit 會導致 hello 下列範例類似的程式碼。 
   
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
2. 新增指示在 hello *SwaggerConfig.cs*檔案 toodirect Swashbuckle toomake 使用 hello XML 文件檔。
   
   * 開啟*SwaggerConfig.cs* hello 上建立一個方法*SwaggerConfig*類別 toospecify hello 路徑 toohello 文件 XML 檔案。 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Hello 中向下捲動*SwaggerConfig.cs*直至您看見 hello 標記為註解線條，類似一個框住 hello 下列螢幕擷取畫面的程式碼檔案。 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * 取消註解 hello 行 tooenable hello XML 註解 Swagger 產生期間所處理。 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. 順序 toogenerate hello XML 文件檔移入 hello 專案屬性並啟用 hello 的 XML 文件檔中 hello 以下螢幕擷取畫面所示。 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

一旦您執行這些步驟，hello Swashbuckle 所產生的 Swagger JSON 會反映在 hello XML 註解中所指定的 hello HTTP 回應碼。 hello 以下螢幕擷取畫面會示範這個新的 JSON 裝載。 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

當您使用 Visual Studio tooregenerate hello 用戶端程式碼的 REST API 時，hello C# 程式碼會接受兩個 hello HTTP OK，而且找不到狀態碼而不會引發例外狀況，允許使用的程式碼 toomake 決策上 toohandle hello 傳回的 null 值的方式請連絡記錄。 

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

此示範中的 hello 程式碼位於[這個 GitHub 儲存機制](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse)。 Hello Web API 以 XML 文件註解標記的專案會包含產生的用戶端，此 api 的主控台應用程式專案。 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a>自訂使用 hello SwaggerResponse 屬性預期的回應碼
hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs)屬性是用於 Swashbuckle 5.1.5 和更新版本。 如果您在專案中有較早版本，本節一開始會說明如何 tooupdate hello Swashbuckle NuGet 封裝，這樣您就可以使用這個屬性。

1. 在 [方案總管] 中，以滑鼠右鍵按一下您的專案並選擇 [管理 NuGet 套件]。 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. 按一下 hello*更新*按鈕的下一個 toohello *Swashbuckle* NuGet 封裝。 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. 新增 hello *SwaggerResponse*屬性 toohello Web API 的動作方法，您會想 toospecify 有效的 HTTP 回應碼。 
   
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
4. 新增`using`hello 屬性的命名空間陳述式：
   
        using Swashbuckle.Swagger.Annotations;
5. 瀏覽 toohello */swagger/docs/v1* URL，您的專案與 hello 各種 HTTP 回應碼會顯示在 hello Swagger JSON。 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

此示範中的 hello 程式碼位於[這個 GitHub 儲存機制](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes)。 Web API 專案裝飾以 hello 以及 hello *SwaggerResponse*屬性會包含產生的用戶端，此 api 的主控台應用程式專案。 

## <a name="next-steps"></a>後續步驟
這篇文章已示範 toocustomize hello 方式 Swashbuckle 會產生作業的識別碼和有效的回應碼。 如需詳細資訊，請參閱 [GitHub 上的 Swashbuckle](https://github.com/domaindrivendev/Swashbuckle)。

