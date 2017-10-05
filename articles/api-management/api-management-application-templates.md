---
title: "Azure API 管理中的應用程式範本 | Microsoft Docs"
description: "了解如何在「Azure API 管理」中自訂開發人員入口網站中的「應用程式」頁面內容。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: f3122c4d-e10e-4cdf-977b-36e8f4133fc8
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 6d2d44465800219f16866a621d4822614ac9e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="abf6d-103">Azure API 管理中的應用程式範本</span><span class="sxs-lookup"><span data-stu-id="abf6d-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="abf6d-104">「Azure API 管理」可讓您使用一組可設定開發人員入口網站頁面內容的範本，來自訂那些頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="abf6d-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="abf6d-105">使用這些範本時，您可以運用 [DotLiquid](http://dotliquidmarkup.org/) 語法和您選擇的編輯器 (例如 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers))，以及一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)、[字符資源](api-management-template-resources.md#glyphs)和[頁面控制項](api-management-page-controls.md)，依照您的想法自由靈活地設定頁面內容。</span><span class="sxs-lookup"><span data-stu-id="abf6d-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="abf6d-106">本節的範本可讓您自訂開發人員入口網站中「應用程式」頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="abf6d-106">The templates in this section allow you to customize the content of the Application pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="abf6d-107">應用程式清單</span><span class="sxs-lookup"><span data-stu-id="abf6d-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="abf6d-108">應用程式</span><span class="sxs-lookup"><span data-stu-id="abf6d-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="abf6d-109">下列文件中包含範例預設範本，但範本可能會因持續進行的改善而有變更。</span><span class="sxs-lookup"><span data-stu-id="abf6d-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="abf6d-110">您可以瀏覽至想要的個別範本，來檢視開發人員入口網站中的即時預設範本。</span><span class="sxs-lookup"><span data-stu-id="abf6d-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="abf6d-111">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。</span><span class="sxs-lookup"><span data-stu-id="abf6d-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="abf6d-112"><a name="ProductList"></a> 應用程式清單</span><span class="sxs-lookup"><span data-stu-id="abf6d-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="abf6d-113">「應用程式清單」範本可讓您自訂開發人員入口網站中應用程式清單頁面的主體。</span><span class="sxs-lookup"><span data-stu-id="abf6d-113">The **Application list** template allows you to customize the body of the application list page in the developer portal.</span></span>  
  
 <span data-ttu-id="abf6d-114">![應用程式清單頁面開發人員入口網站範本](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM 應用程式清單頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="abf6d-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="abf6d-115">預設範本</span><span class="sxs-lookup"><span data-stu-id="abf6d-115">Default template</span></span>  
  
```xml  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "AppStrings|WebApplicationsHeader" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if applications.size > 0 %}  
        <ul class="list-unstyled">  
        {% for app in applications %}  
            <li>  
            {% if app.application.icon.url != "" %}  
                <aside>  
                    <a href="/applications/details/{{app.application.id}}"><img src="{{app.application.icon.url}}" alt="App Icon" /></a>  
                </aside>  
            {% endif %}  
                <h3><a href="/applications/details/{{app.application.id}}">{{app.application.title}}</a></h3>  
                {{app.application.description}}  
            </li>     
        {% endfor %}  
        </ul>  
        <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="abf6d-116">控制</span><span class="sxs-lookup"><span data-stu-id="abf6d-116">Controls</span></span>  
 <span data-ttu-id="abf6d-117">`Product list` 範本可能會使用下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="abf6d-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="abf6d-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="abf6d-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="abf6d-119">資料模型</span><span class="sxs-lookup"><span data-stu-id="abf6d-119">Data model</span></span>  
  
|<span data-ttu-id="abf6d-120">屬性</span><span class="sxs-lookup"><span data-stu-id="abf6d-120">Property</span></span>|<span data-ttu-id="abf6d-121">類型</span><span class="sxs-lookup"><span data-stu-id="abf6d-121">Type</span></span>|<span data-ttu-id="abf6d-122">說明</span><span class="sxs-lookup"><span data-stu-id="abf6d-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="abf6d-123">分頁</span><span class="sxs-lookup"><span data-stu-id="abf6d-123">Paging</span></span>|<span data-ttu-id="abf6d-124">[分頁](api-management-template-data-model-reference.md#Paging)實體。</span><span class="sxs-lookup"><span data-stu-id="abf6d-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="abf6d-125">應用程式集合的分頁資訊。</span><span class="sxs-lookup"><span data-stu-id="abf6d-125">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="abf6d-126">應用程式</span><span class="sxs-lookup"><span data-stu-id="abf6d-126">Applications</span></span>|<span data-ttu-id="abf6d-127">[應用程式](api-management-template-data-model-reference.md#Application)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="abf6d-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="abf6d-128">目前使用者可看見的應用程式。</span><span class="sxs-lookup"><span data-stu-id="abf6d-128">The applications visible to the current user.</span></span>|  
|<span data-ttu-id="abf6d-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="abf6d-129">CategoryName</span></span>|<span data-ttu-id="abf6d-130">字串</span><span class="sxs-lookup"><span data-stu-id="abf6d-130">string</span></span>|<span data-ttu-id="abf6d-131">應用程式的類別。</span><span class="sxs-lookup"><span data-stu-id="abf6d-131">The category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="abf6d-132">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="abf6d-132">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Applications": [  
        {  
            "Application": {  
                "Id": "5702b96fb16653124c8f9ba8",  
                "Title": "Contoso Calculator",  
                "Description": "A simple online calculator.",  
                "Url": null,  
                "Version": null,  
                "Requirements": "Free application with no requirements.",  
                "State": 2,  
                "RegistrationDate": "2016-04-04T18:59:00",  
                "CategoryId": 5,  
                "DeveloperId": "5702b5b0b16653124c8f9ba4",  
                "Attachments": [  
                    {  
                        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                        "Type": "Icon",  
                        "ContentType": "image/png"  
                    },  
                    {  
                        "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
                        "Type": "Screenshot",  
                        "ContentType": "image/png"  
                    }  
                ],  
                "Icon": {  
                    "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                    "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                    "Type": "Icon",  
                    "ContentType": "image/png"  
                }  
            },  
            "CategoryName": "Finance"  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="abf6d-133"><a name="Application"></a> 應用程式</span><span class="sxs-lookup"><span data-stu-id="abf6d-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="abf6d-134">「應用程式」範本可讓您自訂開發人員入口網站中應用程式頁面的主體。</span><span class="sxs-lookup"><span data-stu-id="abf6d-134">The **Application** template allows you to customize the body of the application page in the developer portal.</span></span>  
  
 <span data-ttu-id="abf6d-135">![應用程式頁面開發人員入口網站範本](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM 應用程式頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="abf6d-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="abf6d-136">預設範本</span><span class="sxs-lookup"><span data-stu-id="abf6d-136">Default template</span></span>  
  
```xml  
<h2>{{title}}</h2>  
{% if icon.url != "" %}  
<aside class="applications_aside">  
  <div class="image-placeholder">  
    <img src="{{icon.url}}" alt="Application Icon" />  
  </div>  
</aside>  
{% endif %}  
  
<article>  
  {% if url != "" %}  
    <a target="_blank" href="{{url}}">{{url}}</a>  
  {% endif %}  
  
  <p>{{description}}</p>  
  
  {% if requirements != null %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsRequirementsHeader" %}</h3>  
  <p>{{requirements}}</p>  
  {% endif %}  
  
  {% if attachments.size > 0 %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsScreenshotsHeader" %}</h3>  
    {% for screenshot in attachments %}  
      {% if screenshot.type != "Icon" %}  
      <a href="{{screenshot.url}}" data-lightbox="example-set">  
          <img src="/Developer/Applications/Thumbnail?url={{screenshot.url}}" alt='{% localized "AppDetailsStrings|WebApplicationsScreenshotAlt" %}' />  
      </a>  
      {% endif %}  
    {% endfor %}  
  {% endif %}  
</article>  
  
```  
  
### <a name="controls"></a><span data-ttu-id="abf6d-137">控制</span><span class="sxs-lookup"><span data-stu-id="abf6d-137">Controls</span></span>  
 <span data-ttu-id="abf6d-138">`Application` 範本不允許使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="abf6d-138">The `Application` template does not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="abf6d-139">資料模型</span><span class="sxs-lookup"><span data-stu-id="abf6d-139">Data model</span></span>  
 <span data-ttu-id="abf6d-140">[應用程式](api-management-template-data-model-reference.md#Application)實體。</span><span class="sxs-lookup"><span data-stu-id="abf6d-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="abf6d-141">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="abf6d-141">Sample template data</span></span>  
  
```json  
{  
    "Id": "5702b96fb16653124c8f9ba8",  
    "Title": "Contoso Calculator",  
    "Description": "A simple online calculator.",  
    "Url": null,  
    "Version": null,  
    "Requirements": "Free application with no requirements.",  
    "State": 2,  
    "RegistrationDate": "2016-04-04T18:59:00",  
    "CategoryId": 5,  
    "DeveloperId": "5702b5b0b16653124c8f9ba4",  
    "Attachments": [  
        {  
            "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
            "Type": "Icon",  
            "ContentType": "image/png"  
        },  
        {  
            "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
            "Type": "Screenshot",  
            "ContentType": "image/png"  
        }  
    ],  
    "Icon": {  
        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
        "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
        "Type": "Icon",  
        "ContentType": "image/png"  
    }  
}  
```

## <a name="next-steps"></a><span data-ttu-id="abf6d-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abf6d-142">Next steps</span></span>
<span data-ttu-id="abf6d-143">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="abf6d-143">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>