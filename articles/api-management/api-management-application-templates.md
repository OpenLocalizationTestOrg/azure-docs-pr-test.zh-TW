---
title: "在 Azure API 管理 aaaApplication 範本 |Microsoft 文件"
description: "了解如何 toocustomize hello hello hello 開發人員入口網站在 Azure API 管理中的應用程式頁面的內容。"
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
ms.openlocfilehash: f4dc078be7163b047ca2e640a9065ba9e5ba709e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="185fe-103">Azure API 管理中的應用程式範本</span><span class="sxs-lookup"><span data-stu-id="185fe-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="185fe-104">Azure API 管理提供 hello 能力 toocustomize hello 網頁內容的開發人員入口網站使用的一組設定其內容的範本。</span><span class="sxs-lookup"><span data-stu-id="185fe-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="185fe-105">使用[DotLiquid](http://dotliquidmarkup.org/)語法和 hello 您選擇的編輯器例如[針對設計人員 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers)，和一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)， [字符資源](api-management-template-resources.md#glyphs)，和[頁面控制項](api-management-page-controls.md)，視使用這些範本，您會有很大的彈性 tooconfigure hello 網頁內容的 hello。</span><span class="sxs-lookup"><span data-stu-id="185fe-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="185fe-106">本節中的 hello 範本允許您 toocustomize hello 網頁內容的 hello 應用程式在 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="185fe-106">hello templates in this section allow you toocustomize hello content of hello Application pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="185fe-107">應用程式清單</span><span class="sxs-lookup"><span data-stu-id="185fe-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="185fe-108">應用程式</span><span class="sxs-lookup"><span data-stu-id="185fe-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="185fe-109">預設範本範例隨附的 hello 下列文件，但主旨 toochange 到期 toocontinuous 增強功能。</span><span class="sxs-lookup"><span data-stu-id="185fe-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="185fe-110">您可以檢視 hello 開發人員入口網站中的 hello 即時預設範本，藉由瀏覽 toohello 需要個別的範本。</span><span class="sxs-lookup"><span data-stu-id="185fe-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="185fe-111">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。</span><span class="sxs-lookup"><span data-stu-id="185fe-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="185fe-112"><a name="ProductList"></a> 應用程式清單</span><span class="sxs-lookup"><span data-stu-id="185fe-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="185fe-113">hello**應用程式清單**範本可讓您 toocustomize hello 主體 hello 應用程式清單頁面 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="185fe-113">hello **Application list** template allows you toocustomize hello body of hello application list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="185fe-114">![應用程式清單頁面開發人員入口網站範本](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM 應用程式清單頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="185fe-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="185fe-115">預設範本</span><span class="sxs-lookup"><span data-stu-id="185fe-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="185fe-116">控制</span><span class="sxs-lookup"><span data-stu-id="185fe-116">Controls</span></span>  
 <span data-ttu-id="185fe-117">hello`Product list`範本可能使用 hello 下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="185fe-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="185fe-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="185fe-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="185fe-119">資料模型</span><span class="sxs-lookup"><span data-stu-id="185fe-119">Data model</span></span>  
  
|<span data-ttu-id="185fe-120">屬性</span><span class="sxs-lookup"><span data-stu-id="185fe-120">Property</span></span>|<span data-ttu-id="185fe-121">類型</span><span class="sxs-lookup"><span data-stu-id="185fe-121">Type</span></span>|<span data-ttu-id="185fe-122">說明</span><span class="sxs-lookup"><span data-stu-id="185fe-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="185fe-123">分頁</span><span class="sxs-lookup"><span data-stu-id="185fe-123">Paging</span></span>|<span data-ttu-id="185fe-124">[分頁](api-management-template-data-model-reference.md#Paging)實體。</span><span class="sxs-lookup"><span data-stu-id="185fe-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="185fe-125">hello hello 應用程式集合的分頁資訊。</span><span class="sxs-lookup"><span data-stu-id="185fe-125">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="185fe-126">應用程式</span><span class="sxs-lookup"><span data-stu-id="185fe-126">Applications</span></span>|<span data-ttu-id="185fe-127">[應用程式](api-management-template-data-model-reference.md#Application)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="185fe-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="185fe-128">hello 應用程式顯示 toohello 目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="185fe-128">hello applications visible toohello current user.</span></span>|  
|<span data-ttu-id="185fe-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="185fe-129">CategoryName</span></span>|<span data-ttu-id="185fe-130">字串</span><span class="sxs-lookup"><span data-stu-id="185fe-130">string</span></span>|<span data-ttu-id="185fe-131">hello 類別的應用程式。</span><span class="sxs-lookup"><span data-stu-id="185fe-131">hello category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="185fe-132">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="185fe-132">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="185fe-133"><a name="Application"></a>應用程式</span><span class="sxs-lookup"><span data-stu-id="185fe-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="185fe-134">hello**應用程式**範本可讓您 toocustomize hello 主體 hello 應用程式頁面上的 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="185fe-134">hello **Application** template allows you toocustomize hello body of hello application page in hello developer portal.</span></span>  
  
 <span data-ttu-id="185fe-135">![應用程式頁面開發人員入口網站範本](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM 應用程式頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="185fe-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="185fe-136">預設範本</span><span class="sxs-lookup"><span data-stu-id="185fe-136">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="185fe-137">控制</span><span class="sxs-lookup"><span data-stu-id="185fe-137">Controls</span></span>  
 <span data-ttu-id="185fe-138">hello`Application`範本不允許任何 hello 使用[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="185fe-138">hello `Application` template does not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="185fe-139">資料模型</span><span class="sxs-lookup"><span data-stu-id="185fe-139">Data model</span></span>  
 <span data-ttu-id="185fe-140">[應用程式](api-management-template-data-model-reference.md#Application)實體。</span><span class="sxs-lookup"><span data-stu-id="185fe-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="185fe-141">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="185fe-141">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="185fe-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="185fe-142">Next steps</span></span>
<span data-ttu-id="185fe-143">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="185fe-143">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
