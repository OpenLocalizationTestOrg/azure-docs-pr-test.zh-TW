---
title: "Azure API 管理中的 API 範本 | Microsoft Docs"
description: "了解如何在「Azure API 管理」中自訂開發人員入口網站中的 API 頁面內容。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3642fd09-ba98-4358-93a6-c48ab0500431
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 3802868470f0f74cd1f895a00195259861ea16f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="api-templates-in-azure-api-management"></a><span data-ttu-id="ee2c5-103">Azure API 管理中的 API 範本</span><span class="sxs-lookup"><span data-stu-id="ee2c5-103">API templates in Azure API Management</span></span>
<span data-ttu-id="ee2c5-104">「Azure API 管理」可讓您使用一組可設定開發人員入口網站頁面內容的範本，來自訂那些頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="ee2c5-105">使用這些範本時，您可以運用 [DotLiquid](http://dotliquidmarkup.org/) 語法和您選擇的編輯器 (例如 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers))，以及一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)、[字符資源](api-management-template-resources.md#glyphs)和[頁面控制項](api-management-page-controls.md)，依照您的想法自由靈活地設定頁面內容。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="ee2c5-106">本節的範本可讓您自訂開發人員入口網站中 API 頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-106">The templates in this section allow you to customize the content of the API pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="ee2c5-107">API 清單</span><span class="sxs-lookup"><span data-stu-id="ee2c5-107">API list</span></span>](#APIList)  
-   [<span data-ttu-id="ee2c5-108">作業</span><span class="sxs-lookup"><span data-stu-id="ee2c5-108">Operation</span></span>](#Product)  
-   [<span data-ttu-id="ee2c5-109">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="ee2c5-109">Code samples</span></span>](#CodeSamples)  
    -   [<span data-ttu-id="ee2c5-110">Curl</span><span class="sxs-lookup"><span data-stu-id="ee2c5-110">Curl</span></span>](#Curl)  
    -   [<span data-ttu-id="ee2c5-111">C#</span><span class="sxs-lookup"><span data-stu-id="ee2c5-111">C#</span></span>](#CSharp)  
    -   [<span data-ttu-id="ee2c5-112">Java</span><span class="sxs-lookup"><span data-stu-id="ee2c5-112">Java</span></span>](#Stub)  
    -   [<span data-ttu-id="ee2c5-113">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ee2c5-113">JavaScript</span></span>](#JavaScript)  
    -   [<span data-ttu-id="ee2c5-114">Objective C</span><span class="sxs-lookup"><span data-stu-id="ee2c5-114">Objective C</span></span>](#ObjectiveC)  
    -   [<span data-ttu-id="ee2c5-115">PHP</span><span class="sxs-lookup"><span data-stu-id="ee2c5-115">PHP</span></span>](#PHP)  
    -   [<span data-ttu-id="ee2c5-116">Python</span><span class="sxs-lookup"><span data-stu-id="ee2c5-116">Python</span></span>](#Python)  
    -   [<span data-ttu-id="ee2c5-117">Ruby</span><span class="sxs-lookup"><span data-stu-id="ee2c5-117">Ruby</span></span>](#Ruby)  

> [!NOTE]
>  <span data-ttu-id="ee2c5-118">下列文件中包含範例預設範本，但範本可能會因持續進行的改善而有變更。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-118">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="ee2c5-119">您可以瀏覽至想要的個別範本，來檢視開發人員入口網站中的即時預設範本。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-119">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="ee2c5-120">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-120">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="ee2c5-121"><a name="APIList"></a>API 清單</span><span class="sxs-lookup"><span data-stu-id="ee2c5-121"><a name="APIList"></a> API list</span></span>  
 <span data-ttu-id="ee2c5-122">**API 清單**範本可讓您自訂開發人員入口網站中 API 清單頁面的主體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-122">The **API list** template allows you to customize the body of the API list page in the developer portal.</span></span>  
  
 <span data-ttu-id="ee2c5-123">![開發人員入口網站 API 清單](./media/api-management-api-templates/APIM-Developer-Portal-Templates-API-List.png "APIM 開發人員入口網站範本 API 清單")</span><span class="sxs-lookup"><span data-stu-id="ee2c5-123">![Developer Portal API List](./media/api-management-api-templates/APIM-Developer-Portal-Templates-API-List.png "APIM Developer Portal Templates API List")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="ee2c5-124">預設範本</span><span class="sxs-lookup"><span data-stu-id="ee2c5-124">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ApisStrings|PageTitleApis" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if apis.size > 0 %}  
    <ol class="list-unstyled">  
    {% for api in apis %}  
        <li>  
        <h3>  
          <a href="/docs/services/{{api.id}}">{{api.name}}</a>  
        </h3>  
       {{api.description}}  
      </li>  
    {% endfor %}  
    </ol>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="ee2c5-125">控制</span><span class="sxs-lookup"><span data-stu-id="ee2c5-125">Controls</span></span>  
 <span data-ttu-id="ee2c5-126">`API list` 範本可能會使用下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-126">The `API list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="ee2c5-127">paging-control</span><span class="sxs-lookup"><span data-stu-id="ee2c5-127">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="ee2c5-128">search-control</span><span class="sxs-lookup"><span data-stu-id="ee2c5-128">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="ee2c5-129">資料模型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-129">Data model</span></span>  
  
|<span data-ttu-id="ee2c5-130">屬性</span><span class="sxs-lookup"><span data-stu-id="ee2c5-130">Property</span></span>|<span data-ttu-id="ee2c5-131">類型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-131">Type</span></span>|<span data-ttu-id="ee2c5-132">說明</span><span class="sxs-lookup"><span data-stu-id="ee2c5-132">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="ee2c5-133">apis</span><span class="sxs-lookup"><span data-stu-id="ee2c5-133">apis</span></span>|<span data-ttu-id="ee2c5-134">[API 摘要](api-management-template-data-model-reference.md#APISummary)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-134">Collection of [API summary](api-management-template-data-model-reference.md#APISummary) entities.</span></span>|<span data-ttu-id="ee2c5-135">目前使用者可看見的 API。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-135">The APIs visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="ee2c5-136">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="ee2c5-136">Sample template data</span></span>  
  
```json  
{  
    "apis": [  
        {  
            "id": "570275f1b16653124c8f9ba3",  
            "name": "Basic Calculator",  
            "description": "Arithmetics is just a call away!"  
        },  
        {  
            "id": "57026e30de15d80041040001",  
            "name": "Echo API",  
            "description": null  
        }  
    ],  
    "pageTitle": "APIs"  
}  
```  
  
##  <span data-ttu-id="ee2c5-137"><a name="Product"></a>作業</span><span class="sxs-lookup"><span data-stu-id="ee2c5-137"><a name="Product"></a> Operation</span></span>  
 <span data-ttu-id="ee2c5-138">**作業**範本可讓您自訂開發人員入口網站中作業頁面的主體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-138">The **Operation** template allows you to customize the body of the operation page in the developer portal.</span></span>  
  
 <span data-ttu-id="ee2c5-139">![開發人員入口網站作業頁面](./media/api-management-api-templates/APIM-Developer-Portal-templates-Operation-page.png "APIM 開發人員入口網站範本作業頁面")</span><span class="sxs-lookup"><span data-stu-id="ee2c5-139">![Developer Portal Operation page](./media/api-management-api-templates/APIM-Developer-Portal-templates-Operation-page.png "APIM Developer Portal templates Operation page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="ee2c5-140">預設範本</span><span class="sxs-lookup"><span data-stu-id="ee2c5-140">Default template</span></span>  
  
```xml  
<h2>{{api.name}}</h2>  
<p>{{api.description }}</p>  
  
<div class="panel">  
    <h3>{{operation.name}}</h3>  
    <p>{{operation.description }}</p>  
    <a class="btn btn-primary" href="{{consoleUrl}}" id="btnOpenConsole" role="button">  
        Try it  
    </a>  
</div>  
  
<h4>{% localized "Documentation|SectionHeadingRequestUrl" %}</h4>  
<div class="panel">  
    <div class="panel-body">  
        <label>{{ sampleUrl | escape }}</label>  
    </div>  
</div>  
  
{% if operation.request %}  
    {% if operation.request.parameters.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestParameters" %}</h4>  
  
        <div class="panel">  
            {% for parameter in operation.request.parameters %}  
                 <div class="row panel-body">  
                    <div class="col-md-3">  
                        <label>{{parameter.name}}</label>  
                        {% unless parameter.required %}  
                            <span class="text-muted">({% localized "Documentation|FormLabelSubtextOptional" %})</span>  
                        {% endunless %}  
                    </div>  
                    <div class="col-md-1">  
                        {{parameter.typeName}}  
                    </div>  
                    <div class="col-md-8">  
                        {{parameter.description}}  
                    </div>  
                 </div>  
            {% endfor %}  
        </div>  
    {% endif %}  
  
    {% if operation.request.headers.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestHeaders" %}</h4>  
        <div class="panel">  
            {% for header in operation.request.headers %}  
                 <div class="row panel-body">  
                    <div class="col-md-3">  
                        <label>{{header.name}}</label>  
                        {%unless header.required %}  
                            <span class="text-muted">({% localized "Documentation|FormLabelSubtextOptional" %})</span>  
                        {% endunless %}  
                    </div>  
                    <div class="col-md-1">  
                        {{header.typeName}}  
                    </div>  
                    <div class="col-md-8">  
                        {{header.description}}  
                    </div>  
                 </div>  
            {% endfor %}  
        </div>  
    {% endif %}  
  
    {% if operation.request.description or operation.request.representations.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestBody" %}</h4>  
        <div class="panel">  
            {% if operation.request.description %}  
                <p>{{operation.request.description }}</p>     
            {% endif %}  
  
            {% if operation.request.representations.size > 0 %}  
                <div role="tabpanel">  
                    <ul class="nav nav-tabs" role="tablist">  
                        {% for representation in operation.request.representations %}  
                            <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                                <a href="#requesttab{{forloop.index}}" role="tab" data-toggle="tab">  
                                    {{representation.contentType}}  
                                </a>  
                            </li>  
                        {% endfor %}  
                    </ul>  
                    <div class="tab-content tab-content-boxed">  
                        {% for representation in operation.request.representations %}  
                            <div id="requesttab{{forloop.index}}" role="tabpanel" class="tab-pane snippet{% if forloop.first %} active{% endif %}">  
  
                                {% if representation.sample or representation.schema %}   
                                <div role="tabpanel">  
                                    {% if representation.sample and representation.schema %}   
                                    <ul class="nav nav-tabs-borderless" role="tablist">  
                                        <li role="presentation" class="active">  
                                            <a href="#requesttab{{forloop.index}}sample" role="tab" data-toggle="tab">Sample</a>  
                                        </li>  
                                        <li role="presentation">  
                                            <a href="#requesttab{{forloop.index}}schema" role="tab" data-toggle="tab">Schema</a>  
                                        </li>  
                                    </ul>  
                                    {% endif %}  
  
                                    <div class="tab-content">  
                                        {% if representation.sample %}  
                                        <div id="requesttab{{forloop.index}}sample" role="tabpanel" class="tab-pane snippet active">  
                                            <pre><code class="{{representation.Brush}}">{{ representation.sample | escape }}</code></pre>  
                                        </div>  
                                        {% endif %}  
  
                                        {% if representation.schema %}  
                                        <div id="requesttab{{forloop.index}}schema" role="tabpanel" class="tab-pane snippet">  
                                            <pre><code class="{{representation.Brush}}">{{ representation.schema | escape }}</code></pre>  
                                        </div>  
                                        {% endif %}  
                                    </div>  
                                </div>  
                                {% endif %}  
                            </div>  
                        {% endfor %}  
                    </div>  
                </div>  
            {% endif %}  
  
            <div class="clearfix"></div>  
        </div>  
    {% endif %}  
{% endif %}  
  
{% if operation.responses.size > 0 %}  
    {% for response in operation.responses %}  
        {% if response.description or response.representations.size > 0 %}  
            <h4>{% localized "Documentation|SectionHeadingResponse" %} {{response.statusCode}}</h4>  
  
            <div class="panel">  
                {% if response.description %}  
                    <p>{{ response.description }}</p>  
                {% endif %}  
  
                {% if response.representations.size > 0 %}  
                    <div role="tabpanel">  
                        <ul class="nav nav-tabs" role="tablist">  
                            {% for representation in response.representations %}  
                                <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                                    <a href="#response{{response.statusCode}}tab{{forloop.index}}" role="tab" data-toggle="tab">  
                                        {{representation.contentType}}  
                                    </a>  
                                </li>  
                            {% endfor %}  
                        </ul>  
                        <div class="tab-content tab-content-boxed">  
                            {% for representation in response.representations %}  
                                <div id="response{{response.statusCode}}tab{{forloop.index}}" role="tabpanel" class="tab-pane snippet{% if forloop.first %} active{% endif %}">  
  
                                    {% if representation.sample or representation.schema %}  
                                    <div role="tabpanel">  
  
                                        {% if representation.sample and representation.schema %}  
                                        <ul class="nav nav-tabs-borderless" role="tablist">  
                                            <li role="presentation" class="active">  
                                                <a href="#response{{response.statusCode}}tab{{forloop.index}}sample" role="tab" data-toggle="tab">  
                                                    Sample  
                                                </a>  
                                            </li>  
                                            <li role="presentation">  
                                                <a href="#response{{response.statusCode}}tab{{forloop.index}}schema" role="tab" data-toggle="tab">  
                                                    Schema  
                                                </a>  
                                            </li>  
                                        </ul>  
                                        {% endif %}  
  
                                        <div class="tab-content">  
                                            {% if representation.sample %}  
                                            <div id="response{{response.statusCode}}tab{{forloop.index}}sample" role="tabpanel" class="tab-pane snippet active">  
                                                <pre><code class="{{representation.Brush}}">{{ representation.sample | escape }}</code></pre>  
                                            </div>  
                                            {% endif %}  
  
                                            {% if representation.schema %}  
                                            <div id="response{{response.statusCode}}tab{{forloop.index}}schema" role="tabpanel" class="tab-pane snippet">  
                                                <pre><code class="{{representation.Brush}}">{{ representation.schema | escape }}</code></pre>  
                                            </div>  
                                            {% endif %}  
                                        </div>  
                                    </div>  
                                    {% endif %}  
                                </div>  
                            {% endfor %}  
                        </div>  
                    </div>  
                {% endif %}  
  
                <div class="clearfix"></div>  
            </div>  
  
        {% endif %}  
    {% endfor %}  
{% endif %}  
  
<h4>{% localized "Documentation|SectionHeadingCodeSamples" %}</h4>  
<div role="tabpanel">  
    <ul class="nav nav-tabs" role="tablist">  
        {% for sample in samples %}  
            <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                <a href="#{{sample.brush}}" aria-controls="{{sample.brush}}" role="tab" data-toggle="tab">  
                    {{sample.title}}  
                </a>  
            </li>  
        {% endfor %}  
    </ul>  
    <div class="tab-content tab-content-boxed" title="{% localized "Documentation|TooltipTextDoubleClickToSelectAll=""" %}">  
        {% for sample in samples %}  
            <div role="tabpanel" class="tab-pane tab-content-boxed {% if forloop.first %} active{% endif %} snippet snippet-resizable" id="{{sample.brush}}" >  
                <pre><code class="{{sample.brush}}">{% partial sample.template for sample in samples %}</code></pre>  
            </div>  
        {% endfor %}  
    </div>  
    <div class="clearfix"></div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="ee2c5-141">控制</span><span class="sxs-lookup"><span data-stu-id="ee2c5-141">Controls</span></span>  
 <span data-ttu-id="ee2c5-142">`Operation` 範本不允許使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-142">The `Operation` template does not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="ee2c5-143">資料模型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-143">Data model</span></span>  
  
|<span data-ttu-id="ee2c5-144">屬性</span><span class="sxs-lookup"><span data-stu-id="ee2c5-144">Property</span></span>|<span data-ttu-id="ee2c5-145">類型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-145">Type</span></span>|<span data-ttu-id="ee2c5-146">說明</span><span class="sxs-lookup"><span data-stu-id="ee2c5-146">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="ee2c5-147">apiId</span><span class="sxs-lookup"><span data-stu-id="ee2c5-147">apiId</span></span>|<span data-ttu-id="ee2c5-148">字串</span><span class="sxs-lookup"><span data-stu-id="ee2c5-148">string</span></span>|<span data-ttu-id="ee2c5-149">目前 API 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-149">The id of the current API.</span></span>|  
|<span data-ttu-id="ee2c5-150">apiName</span><span class="sxs-lookup"><span data-stu-id="ee2c5-150">apiName</span></span>|<span data-ttu-id="ee2c5-151">字串</span><span class="sxs-lookup"><span data-stu-id="ee2c5-151">string</span></span>|<span data-ttu-id="ee2c5-152">API 的名稱。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-152">The name of the API.</span></span>|  
|<span data-ttu-id="ee2c5-153">apiDescription</span><span class="sxs-lookup"><span data-stu-id="ee2c5-153">apiDescription</span></span>|<span data-ttu-id="ee2c5-154">字串</span><span class="sxs-lookup"><span data-stu-id="ee2c5-154">string</span></span>|<span data-ttu-id="ee2c5-155">API 的描述。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-155">A description of the API.</span></span>|  
|<span data-ttu-id="ee2c5-156">api</span><span class="sxs-lookup"><span data-stu-id="ee2c5-156">api</span></span>|<span data-ttu-id="ee2c5-157">[API 摘要](api-management-template-data-model-reference.md#APISummary)實體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-157">[API summary](api-management-template-data-model-reference.md#APISummary) entity.</span></span>|<span data-ttu-id="ee2c5-158">目前的 API。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-158">The current API.</span></span>|  
|<span data-ttu-id="ee2c5-159">operation</span><span class="sxs-lookup"><span data-stu-id="ee2c5-159">operation</span></span>|[<span data-ttu-id="ee2c5-160">作業</span><span class="sxs-lookup"><span data-stu-id="ee2c5-160">Operation</span></span>](api-management-template-data-model-reference.md#Operation)|<span data-ttu-id="ee2c5-161">目前顯示的作業。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-161">The currently displayed operation.</span></span>|  
|<span data-ttu-id="ee2c5-162">sampleUrl</span><span class="sxs-lookup"><span data-stu-id="ee2c5-162">sampleUrl</span></span>|<span data-ttu-id="ee2c5-163">字串</span><span class="sxs-lookup"><span data-stu-id="ee2c5-163">string</span></span>|<span data-ttu-id="ee2c5-164">目前作業的 URL。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-164">The URL for the current operation.</span></span>|  
|<span data-ttu-id="ee2c5-165">operationMenu</span><span class="sxs-lookup"><span data-stu-id="ee2c5-165">operationMenu</span></span>|[<span data-ttu-id="ee2c5-166">作業功能表</span><span class="sxs-lookup"><span data-stu-id="ee2c5-166">Operation menu</span></span>](api-management-template-data-model-reference.md#Menu)|<span data-ttu-id="ee2c5-167">此 API 的作業功能表。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-167">A menu of operations for this API.</span></span>|  
|<span data-ttu-id="ee2c5-168">consoleUrl</span><span class="sxs-lookup"><span data-stu-id="ee2c5-168">consoleUrl</span></span>|<span data-ttu-id="ee2c5-169">URI</span><span class="sxs-lookup"><span data-stu-id="ee2c5-169">URI</span></span>|<span data-ttu-id="ee2c5-170">[試用] 按鈕的 URI。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-170">The URI for the **Try it** button.</span></span>|  
|<span data-ttu-id="ee2c5-171">範例</span><span class="sxs-lookup"><span data-stu-id="ee2c5-171">samples</span></span>|<span data-ttu-id="ee2c5-172">[程式碼範例](api-management-template-data-model-reference.md#Sample)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-172">Collection of [Code sample](api-management-template-data-model-reference.md#Sample) entities.</span></span>|<span data-ttu-id="ee2c5-173">目前作業的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-173">The code samples for the current operation..</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="ee2c5-174">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="ee2c5-174">Sample template data</span></span>  
  
```json  
{  
    "apiId": "570275f1b16653124c8f9ba3",  
    "apiName": "Basic Calculator",  
    "apiDescription": "Arithmetics is just a call away!",  
    "api": {  
        "id": "570275f1b16653124c8f9ba3",  
        "name": "Basic Calculator",  
        "description": "Arithmetics is just a call away!"  
    },  
    "operation": {  
        "id": "570275f2b1665305c811cf49",  
        "name": "Add two integers",  
        "description": "Produces a sum of two numbers.",  
        "scheme": "https",  
        "uriTemplate": "calc/add?a={a}&b={b}",  
        "host": "sdcontoso5.azure-api.net",  
        "httpMethod": "GET",  
        "request": {  
            "description": null,  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": [  
                {  
                    "name": "a",  
                    "description": "First operand. Default value is <code>51</code>.",  
                    "value": "51",  
                    "options": [  
                        "51"  
                    ],  
                    "required": true,  
                    "kind": 1,  
                    "typeName": null  
                },  
                {  
                    "name": "b",  
                    "description": "Second operand. Default value is <code>49</code>.",  
                    "value": "49",  
                    "options": [  
                        "49"  
                    ],  
                    "required": true,  
                    "kind": 1,  
                    "typeName": null  
                }  
            ],  
            "representations": []  
        },  
        "responses": []  
    },  
    "sampleUrl": "https://sdcontoso5.azure-api.net/calc/add?a={a}&b={b}",  
    "operationMenu": {  
        "ApiId": "570275f1b16653124c8f9ba3",  
        "CurrentOperationId": "570275f2b1665305c811cf49",  
        "Action": "Operation",  
        "MenuItems": [  
            {  
                "Id": "570275f2b1665305c811cf49",  
                "Title": "Add two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4c",  
                "Title": "Divide two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4b",  
                "Title": "Multiply two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4a",  
                "Title": "Subtract two integers",  
                "HttpMethod": "GET"  
            }  
        ]  
    },  
    "consoleUrl": "/docs/services/570275f1b16653124c8f9ba3/operations/570275f2b1665305c811cf49/console",  
    "samples": [  
        {  
            "title": "Curl",  
            "snippet": null,  
            "brush": "plain",  
            "template": "DocumentationSamplesCurl",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "C#",  
            "snippet": null,  
            "brush": "csharp",  
            "template": "DocumentationSamplesCsharp",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Java",  
            "snippet": null,  
            "brush": "java",  
            "template": "DocumentationSamplesJava",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "JavaScript",  
            "snippet": null,  
            "brush": "xml",  
            "template": "DocumentationSamplesJs",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "ObjC",  
            "snippet": null,  
            "brush": "objc",  
            "template": "DocumentationSamplesObjc",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "PHP",  
            "snippet": null,  
            "brush": "php",  
            "template": "DocumentationSamplesPhp",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Python",  
            "snippet": null,  
            "brush": "python",  
            "template": "DocumentationSamplesPython",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Ruby",  
            "snippet": null,  
            "brush": "ruby",  
            "template": "DocumentationSamplesRuby",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="ee2c5-175"><a name="CodeSamples"></a> 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="ee2c5-175"><a name="CodeSamples"></a> Code samples</span></span>  
 <span data-ttu-id="ee2c5-176">下列範本可讓您自訂作業頁面上個別程式碼範例的主體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-176">The following templates allow you to customize the body of the individual code samples on the operation page.</span></span>  
  
 <span data-ttu-id="ee2c5-177">![開發人員入口網站範本程式碼範例](./media/api-management-api-templates/APIM-Developer-Portal-Templates-Code-samples.png "APIM 開發人員入口網站範本程式碼範例")</span><span class="sxs-lookup"><span data-stu-id="ee2c5-177">![Developer Portal Templates Code samples](./media/api-management-api-templates/APIM-Developer-Portal-Templates-Code-samples.png "APIM Developer Portal Templates Code samples")</span></span>  
  
-   [<span data-ttu-id="ee2c5-178">Curl</span><span class="sxs-lookup"><span data-stu-id="ee2c5-178">Curl</span></span>](#Curl)  
  
-   [<span data-ttu-id="ee2c5-179">C#</span><span class="sxs-lookup"><span data-stu-id="ee2c5-179">C#</span></span>](#CSharp)  
  
-   [<span data-ttu-id="ee2c5-180">Java</span><span class="sxs-lookup"><span data-stu-id="ee2c5-180">Java</span></span>](#Stub)  
  
-   [<span data-ttu-id="ee2c5-181">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ee2c5-181">JavaScript</span></span>](#JavaScript)  
  
-   [<span data-ttu-id="ee2c5-182">Objective C</span><span class="sxs-lookup"><span data-stu-id="ee2c5-182">Objective C</span></span>](#ObjectiveC)  
  
-   [<span data-ttu-id="ee2c5-183">PHP</span><span class="sxs-lookup"><span data-stu-id="ee2c5-183">PHP</span></span>](#PHP)  
  
-   [<span data-ttu-id="ee2c5-184">Python</span><span class="sxs-lookup"><span data-stu-id="ee2c5-184">Python</span></span>](#Python)  
  
-   [<span data-ttu-id="ee2c5-185">Ruby</span><span class="sxs-lookup"><span data-stu-id="ee2c5-185">Ruby</span></span>](#Ruby)  
  
###  <span data-ttu-id="ee2c5-186"><a name="Curl"></a>Curl</span><span class="sxs-lookup"><span data-stu-id="ee2c5-186"><a name="Curl"></a> Curl</span></span>  
 <span data-ttu-id="ee2c5-187">**DocumentationSamplesCurl** 範本可讓您在作業頁面的程式碼範例區段中自訂該程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-187">The **DocumentationSamplesCurl** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="ee2c5-188">預設範本</span><span class="sxs-lookup"><span data-stu-id="ee2c5-188">Default template</span></span>  
  
```xml  
@ECHO OFF  
  
curl -v -X {{method}} "{{scheme}}://{{host}}{{path}}{{query | escape }}"  
{% for header in headers -%}  
-H "{{ header.name }}: {{ header.value }}"  
{% endfor -%}  
{% if body -%}   
--data-ascii "{{ body | replace:'"','^"' }}"   
{% endif -%}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="ee2c5-189">控制</span><span class="sxs-lookup"><span data-stu-id="ee2c5-189">Controls</span></span>  
 <span data-ttu-id="ee2c5-190">程式碼範例範本不允許使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-190">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="ee2c5-191">資料模型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-191">Data model</span></span>  
 <span data-ttu-id="ee2c5-192">[程式碼範例](api-management-template-data-model-reference.md#Sample)實體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-192">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="ee2c5-193">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="ee2c5-193">Sample template data</span></span>  
  
```json  
{  
    "title": "Curl",  
    "snippet": null,  
    "brush": "plain",  
    "template": "DocumentationSamplesCurl",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="ee2c5-194"><a name="CSharp"></a> C#</span><span class="sxs-lookup"><span data-stu-id="ee2c5-194"><a name="CSharp"></a> C#</span></span>  
 <span data-ttu-id="ee2c5-195">**DocumentationSamplesCsharp** 範本可讓您在作業頁面的程式碼範例區段中自訂該程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-195">The **DocumentationSamplesCsharp** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="ee2c5-196">預設範本</span><span class="sxs-lookup"><span data-stu-id="ee2c5-196">Default template</span></span>  
  
```xml  
using System;  
using System.Net.Http.Headers;  
using System.Text;  
using System.Net.Http;  
using System.Web;  
  
namespace CSHttpClientSample  
{  
    static class Program  
    {  
        static void Main()  
        {  
            MakeRequest();  
            Console.WriteLine("Hit ENTER to exit...");  
            Console.ReadLine();  
        }  
  
        static async void MakeRequest()  
        {  
            var client = new HttpClient();  
            var queryString = HttpUtility.ParseQueryString(string.Empty);  
  
{% if headers.size > 0 -%}  
            // Request headers  
{% for header in headers -%}  
{% case header.Name -%}  
{% when "Accept"%}  
            client.DefaultRequestHeaders.Accept.Add(MediaTypeWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Charset" -%}  
            client.DefaultRequestHeaders.AcceptCharset.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Encoding" -%}  
            client.DefaultRequestHeaders.AcceptEncoding.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Language" -%}  
            client.DefaultRequestHeaders.AcceptLanguage.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Cache-Control" -%}  
            client.DefaultRequestHeaders.CacheControl = CacheControlHeaderValue.Parse("{{header.value}}");  
{% when "Connection" -%}  
            client.DefaultRequestHeaders.Connection.Add("{{header.value}}");  
{% when "Date" -%}  
            client.DefaultRequestHeaders.Date = DateTimeOffset.Parse("{{header.value}}");  
{% when "Expect" -%}  
            client.DefaultRequestHeaders.Expect.Add(NameValueWithParametersHeaderValue.Parse("{{header.value}}"));  
{% when "If-Match" -%}  
            client.DefaultRequestHeaders.IfMatch.Add(EntityTagHeaderValue.Parse("{{header.value}}"));  
{% when "If-Modified-Since" -%}  
            client.DefaultRequestHeaders.IfModifiedSince = DateTimeOffset.Parse("{{header.value}}");  
{% when "If-None-Match" -%}  
            client.DefaultRequestHeaders.IfNoneMatch.Add(EntityTagHeaderValue.Parse("{{header.value}}"));  
{% when "If-Range" -%}  
            client.DefaultRequestHeaders.IfRange = RangeConditionHeaderValue.Parse("{{header.value}}");  
{% when "If-Unmodified-Since" -%}  
            client.DefaultRequestHeaders.IfUnmodifiedSince = DateTimeOffset.Parse("{{header.value}}");  
{% when "Max-Forwards" -%}  
            client.DefaultRequestHeaders.MaxForwards = int.Parse("{{header.value}}");  
{% when "Pragma" -%}  
            client.DefaultRequestHeaders.Pragma.Add(NameValueHeaderValue.Parse("{{header.value}}"));  
{% when "Range" -%}  
            client.DefaultRequestHeaders.Range = RangeHeaderValue.Parse("{{header.value}}");  
{% when "Referer" -%}  
            client.DefaultRequestHeaders.Referrer = new Uri("{{header.value}}");  
{% when "TE" -%}  
            client.DefaultRequestHeaders.TE.Add(TransferCodingWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Transfer-Encoding" -%}  
            client.DefaultRequestHeaders.TransferEncoding.Add(TransferCodingHeaderValue.Parse("{{header.value}}"));  
{% when "Upgrade" -%}  
            client.DefaultRequestHeaders.Upgrade.Add(ProductHeaderValue.Parse("{{header.value}}"));  
{% when "User-Agent" -%}  
            client.DefaultRequestHeaders.UserAgent.Add(ProductInfoHeaderValue.Parse("{{header.value}}"));  
{% when "Via" -%}                
            client.DefaultRequestHeaders.Via.Add(ViaHeaderValue.Parse("{{header.value}}"));  
{% when "Warning" -%}  
            client.DefaultRequestHeaders.Warning.Add(WarningHeaderValue.Parse("{{header.value}}"));  
{% when "Content-Type" -%}  
{% else -%}  
            client.DefaultRequestHeaders.Add("{{header.Name}}", "{{header.value}}");  
{% endcase -%}  
{% endfor -%}  
{% endif -%}  
  
{% if parameters.size > 0 -%}  
            // Request parameters  
{% for parameter in parameters -%}  
            queryString["{{parameter.Name}}"] = "{{parameter.Value}}";  
{% endfor -%}  
{% endif -%}  
            var uri = "{{scheme}}://{{host}}{{path}}{% if path contains '?' %}&{% else %}?{% endif %}" + queryString;  
  
{% case method -%}  
  
{% when "POST" -%}  
            HttpResponseMessage response;  
  
            // Request body  
            byte[] byteData = Encoding.UTF8.GetBytes("{{ body | replace:'"','\"'}}");  
  
            using (var content = new ByteArrayContent(byteData))  
            {  
{% if body -%}  
               content.Headers.ContentType = new MediaTypeHeaderValue("< your content type, i.e. application/json >");  
{% endif -%}  
               response = await client.PostAsync(uri, content);  
            }  
  
{% when "GET" -%}  
            var response = await client.GetAsync(uri);  
{% when "DELETE" -%}  
            var response = await client.DeleteAsync(uri);  
{% when "PUT" -%}  
            HttpResponseMessage response;  
  
            // Request body  
            byte[] byteData = Encoding.UTF8.GetBytes("{{ body | replace:'"','\"'}}");  
  
            using (var content = new ByteArrayContent(byteData))  
            {  
{% if body -%}  
                content.Headers.ContentType = new MediaTypeHeaderValue("< your content type, i.e. application/json >");  
{% endif -%}  
                response = await client.PutAsync(uri, content);  
            }  
{% when "HEAD" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Head, uri));  
{% when "OPTIONS" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Options, uri));  
{% when "TRACE" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Trace, uri));  
  
            if (response.Content != null)  
            {  
                var responseString = await response.Content.ReadAsStringAsync();  
                Console.WriteLine(responseString);      
            }  
{% endcase -%}  
        }  
    }  
}     
```  
  
#### <a name="controls"></a><span data-ttu-id="ee2c5-197">控制</span><span class="sxs-lookup"><span data-stu-id="ee2c5-197">Controls</span></span>  
 <span data-ttu-id="ee2c5-198">程式碼範例範本不允許使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-198">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="ee2c5-199">資料模型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-199">Data model</span></span>  
 <span data-ttu-id="ee2c5-200">[程式碼範例](api-management-template-data-model-reference.md#Sample)實體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-200">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="ee2c5-201">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="ee2c5-201">Sample template data</span></span>  
  
```json  
{  
    "title": "C#",  
    "snippet": null,  
    "brush": "csharp",  
    "template": "DocumentationSamplesCsharp",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="ee2c5-202"><a name="Stub"></a>Java</span><span class="sxs-lookup"><span data-stu-id="ee2c5-202"><a name="Stub"></a> Java</span></span>  
 <span data-ttu-id="ee2c5-203">**DocumentationSamplesJava** 範本可讓您在作業頁面的程式碼範例區段中自訂該程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-203">The **DocumentationSamplesJava** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="ee2c5-204">預設範本</span><span class="sxs-lookup"><span data-stu-id="ee2c5-204">Default template</span></span>  
  
```xml  
// // This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)  
import java.net.URI;  
import org.apache.http.HttpEntity;  
import org.apache.http.HttpResponse;  
import org.apache.http.client.HttpClient;  
import org.apache.http.client.methods.HttpGet;  
import org.apache.http.client.utils.URIBuilder;  
import org.apache.http.impl.client.HttpClients;  
import org.apache.http.util.EntityUtils;  
  
public class JavaSample   
{  
    public static void main(String[] args)   
    {  
        HttpClient httpclient = HttpClients.createDefault();  
  
        try  
        {  
            URIBuilder builder = new URIBuilder("{{scheme}}://{{host}}{{path}}");  
  
{% if parameters.size > 0 -%}  
{% for parameter in parameters -%}  
            builder.setParameter("{{parameter.name}}", "{{parameter.value}}");  
{% endfor -%}  
{% endif -%}  
  
            URI uri = builder.build();  
            Http{{ method | downcase | capitalize }} request = new Http{{ method | downcase | capitalize }}(uri);  
{% for header in headers -%}  
            request.setHeader("{{header.Name}}", "{{header.value}}");  
{% endfor %}  
  
{% if body -%}  
            // Request body  
            StringEntity reqEntity = new StringEntity("{{ body | replace:'"','\"' }}");  
            request.setEntity(reqEntity);  
{% endif -%}  
  
            HttpResponse response = httpclient.execute(request);  
            HttpEntity entity = response.getEntity();  
  
            if (entity != null)   
            {  
                System.out.println(EntityUtils.toString(entity));  
            }  
        }  
        catch (Exception e)  
        {  
            System.out.println(e.getMessage());  
        }  
    }  
}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="ee2c5-205">控制</span><span class="sxs-lookup"><span data-stu-id="ee2c5-205">Controls</span></span>  
 <span data-ttu-id="ee2c5-206">程式碼範例範本不允許使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-206">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="ee2c5-207">資料模型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-207">Data model</span></span>  
 <span data-ttu-id="ee2c5-208">[程式碼範例](api-management-template-data-model-reference.md#Sample)實體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-208">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="ee2c5-209">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="ee2c5-209">Sample template data</span></span>  
  
```json  
{  
    "title": "Java",  
    "snippet": null,  
    "brush": "java",  
    "template": "DocumentationSamplesJava",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="ee2c5-210"><a name="JavaScript"></a>JavaScript</span><span class="sxs-lookup"><span data-stu-id="ee2c5-210"><a name="JavaScript"></a> JavaScript</span></span>  
 <span data-ttu-id="ee2c5-211">**DocumentationSamplesJs** 範本可讓您在作業頁面的程式碼範例區段中自訂該程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-211">The **DocumentationSamplesJs** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="ee2c5-212">預設範本</span><span class="sxs-lookup"><span data-stu-id="ee2c5-212">Default template</span></span>  
  
```xml  
<!DOCTYPE html>  
<html>  
<head>  
    <title>JSSample</title>  
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>  
</head>  
<body>  
  
<script type="text/javascript">  
    $(function() {  
        var params = {  
{% if parameters.size > 0 -%}  
            // Request parameters  
{% for parameter in parameters -%}  
            "{{parameter.name}}": "{{parameter.value}}",  
{% endfor -%}  
{% endif -%}  
        };  
  
        $.ajax({  
            url: "{{scheme}}://{{host}}{{path}}{% if path contains '?' %}&{% else %}?{% endif %}" + $.param(params),  
{% if headers.size > 0 -%}  
            beforeSend: function(xhrObj){  
                // Request headers  
{% for header in headers -%}  
                xhrObj.setRequestHeader("{{header.name}}","{{header.value}}");  
{% endfor -%}  
            },  
{% endif -%}  
            type: "{{method}}",  
{% if body -%}  
            // Request body  
            data: "{{ body | replace:'"','\"' }}",  
{% endif -%}  
        })  
        .done(function(data) {  
            alert("success");  
        })  
        .fail(function() {  
            alert("error");  
        });  
    });  
</script>  
</body>  
</html>  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="ee2c5-213">控制</span><span class="sxs-lookup"><span data-stu-id="ee2c5-213">Controls</span></span>  
 <span data-ttu-id="ee2c5-214">程式碼範例範本不允許使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-214">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="ee2c5-215">資料模型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-215">Data model</span></span>  
 <span data-ttu-id="ee2c5-216">[程式碼範例](api-management-template-data-model-reference.md#Sample)實體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-216">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="ee2c5-217">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="ee2c5-217">Sample template data</span></span>  
  
```json  
{  
    "title": "JavaScript",  
    "snippet": null,  
    "brush": "xml",  
    "template": "DocumentationSamplesJs",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="ee2c5-218"><a name="ObjectiveC"></a>Objective C</span><span class="sxs-lookup"><span data-stu-id="ee2c5-218"><a name="ObjectiveC"></a> Objective C</span></span>  
 <span data-ttu-id="ee2c5-219">**DocumentationSamplesObjc** 範本可讓您在作業頁面的程式碼範例區段中自訂該程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-219">The **DocumentationSamplesObjc** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="ee2c5-220">預設範本</span><span class="sxs-lookup"><span data-stu-id="ee2c5-220">Default template</span></span>  
  
```xml  
#import <Foundation/Foundation.h>  
  
int main(int argc, const char * argv[])  
{  
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];  
  
    NSString* path = @"{{scheme}}://{{host}}{{path}}";  
    NSArray* array = @[  
                         // Request parameters  
                         @"entities=true",  
{% if parameters.size > 0 -%}  
{% for parameter in parameters -%}  
                         @"{{parameter.name}}={{parameter.value}}",  
{% endfor -%}  
{% endif -%}  
                      ];  
  
    NSString* string = [array componentsJoinedByString:@"&"];  
    path = [path stringByAppendingFormat:@"?%@", string];  
  
    NSLog(@"%@", path);  
  
    NSMutableURLRequest* _request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:path]];  
    [_request setHTTPMethod:@"{{method}}"];  
{% if headers.size > 0 -%}  
    // Request headers  
{% for header in headers -%}  
    [_request setValue:@"{{header.value}}" forHTTPHeaderField:@"{{header.name}}"];  
{% endfor -%}  
{% endif -%}  
{% if body -%}  
    // Request body  
    [_request setHTTPBody:[@"{{ body | replace:'"','\"' }}" dataUsingEncoding:NSUTF8StringEncoding]];  
{% endif -%}  
  
    NSURLResponse *response = nil;  
    NSError *error = nil;  
    NSData* _connectionData = [NSURLConnection sendSynchronousRequest:_request returningResponse:&response error:&error];  
  
    if (nil != error)  
    {  
        NSLog(@"Error: %@", error);  
    }  
    else  
    {  
        NSError* error = nil;  
        NSMutableDictionary* json = nil;  
        NSString* dataString = [[NSString alloc] initWithData:_connectionData encoding:NSUTF8StringEncoding];  
        NSLog(@"%@", dataString);  
  
        if (nil != _connectionData)  
        {  
            json = [NSJSONSerialization JSONObjectWithData:_connectionData options:NSJSONReadingMutableContainers error:&error];  
        }  
  
        if (error || !json)  
        {  
            NSLog(@"Could not parse loaded json with error:%@", error);  
        }  
  
        NSLog(@"%@", json);  
        _connectionData = nil;  
    }  
  
    [pool drain];  
  
    return 0;  
}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="ee2c5-221">控制</span><span class="sxs-lookup"><span data-stu-id="ee2c5-221">Controls</span></span>  
 <span data-ttu-id="ee2c5-222">程式碼範例範本不允許使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-222">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="ee2c5-223">資料模型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-223">Data model</span></span>  
 <span data-ttu-id="ee2c5-224">[程式碼範例](api-management-template-data-model-reference.md#Sample)實體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-224">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="ee2c5-225">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="ee2c5-225">Sample template data</span></span>  
  
```json  
{  
    "title": "ObjC",  
    "snippet": null,  
    "brush": "objc",  
    "template": "DocumentationSamplesObjc",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="ee2c5-226"><a name="PHP"></a>PHP</span><span class="sxs-lookup"><span data-stu-id="ee2c5-226"><a name="PHP"></a> PHP</span></span>  
 <span data-ttu-id="ee2c5-227">**DocumentationSamplesPhp** 範本可讓您在作業頁面的程式碼範例區段中自訂該程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-227">The **DocumentationSamplesPhp** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="ee2c5-228">預設範本</span><span class="sxs-lookup"><span data-stu-id="ee2c5-228">Default template</span></span>  
  
```xml  
<?php  
// This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)  
require_once 'HTTP/Request2.php';  
  
$request = new Http_Request2('{{scheme}}://{{host}}{{path}}');  
$url = $request->getUrl();  
  
{% if headers.size > 0 -%}  
$headers = array(  
    // Request headers  
{% for header in headers -%}  
    '{{header.name}}' => '{{header.value}}',  
{% endfor -%}  
);  
  
$request->setHeader($headers);  
{% endif -%}  
  
{% if parameters.size > 0 -%}  
$parameters = array(  
    // Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}' => '{{parameter.value}}',  
{% endfor -%}  
);  
  
$url->setQueryVariables($parameters);  
{% endif -%}  
  
$request->setMethod(HTTP_Request2::METHOD_{{method}});  
  
{% if body -%}  
// Request body  
$request->setBody("{{ body | replace:'"','\"' }}");  
{% endif -%}  
  
try  
{  
    $response = $request->send();  
    echo $response->getBody();  
}  
catch (HttpException $ex)  
{  
    echo $ex;  
}  
  
?>  
```  
  
#### <a name="controls"></a><span data-ttu-id="ee2c5-229">控制</span><span class="sxs-lookup"><span data-stu-id="ee2c5-229">Controls</span></span>  
 <span data-ttu-id="ee2c5-230">程式碼範例範本不允許使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-230">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="ee2c5-231">資料模型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-231">Data model</span></span>  
 <span data-ttu-id="ee2c5-232">[程式碼範例](api-management-template-data-model-reference.md#Sample)實體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-232">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="ee2c5-233">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="ee2c5-233">Sample template data</span></span>  
  
```json  
{  
    "title": "PHP",  
    "snippet": null,  
    "brush": "php",  
    "template": "DocumentationSamplesPhp",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="ee2c5-234"><a name="Python"></a>Python</span><span class="sxs-lookup"><span data-stu-id="ee2c5-234"><a name="Python"></a> Python</span></span>  
 <span data-ttu-id="ee2c5-235">**DocumentationSamplesPython** 範本可讓您在作業頁面的程式碼範例區段中自訂該程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-235">The **DocumentationSamplesPython** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="ee2c5-236">預設範本</span><span class="sxs-lookup"><span data-stu-id="ee2c5-236">Default template</span></span>  
  
```xml  
########### Python 2.7 #############  
import httplib, urllib, base64  
  
headers = {  
{% if headers.size > 0 -%}  
    # Request headers  
{% for header in headers -%}  
    '{{header.name}}': '{{header.value}}',  
{% endfor -%}  
{% endif -%}  
}  
  
params = urllib.urlencode({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}': '{{parameter.value}}',  
{% endfor -%}  
{% endif -%}  
})  
  
try:  
{% case scheme -%}  
{% when "http" -%}  
    conn = httplib.HTTPConnection('{{host}}')  
{% when "https" -%}  
    conn = httplib.HTTPSConnection('{{host}}')  
{% endcase -%}  
    conn.request("{{method}}", "{{path}}{% if path contains '?' %}&{% else %}?{% endif %}%s" % params{% if body %}, "{{ body | replace:'"','\"' }}"{% endif %}, headers)  
    response = conn.getresponse()  
    data = response.read()  
    print(data)  
    conn.close()  
except Exception as e:  
    print("[Errno {0}] {1}".format(e.errno, e.strerror))  
  
####################################  
  
########### Python 3.2 #############  
import http.client, urllib.request, urllib.parse, urllib.error, base64  
  
headers = {  
{% if headers.size > 0 -%}  
    # Request headers  
{% for header in headers -%}  
    '{{header.name}}': '{{header.value}}',  
{% endfor -%}  
{% endif -%}  
}  
  
params = urllib.parse.urlencode({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}': '{{parameter.value}}',  
{% endfor -%}  
{% endif -%}  
})  
  
try:  
{% case scheme -%}  
{% when "http" -%}  
    conn = http.client.HTTPConnection('{{host}}')  
{% when "https" -%}  
    conn = http.client.HTTPSConnection('{{host}}')  
{% endcase -%}  
    conn.request("{{method}}", "{{path}}{% if path contains '?' %}&{% else %}?{% endif %}%s" % params{% if body %}, "{{ body | replace:'"','\"' }}"{% endif %}, headers)  
    response = conn.getresponse()  
    data = response.read()  
    print(data)  
    conn.close()  
except Exception as e:  
    print("[Errno {0}] {1}".format(e.errno, e.strerror))  
  
####################################  
```  
  
#### <a name="controls"></a><span data-ttu-id="ee2c5-237">控制</span><span class="sxs-lookup"><span data-stu-id="ee2c5-237">Controls</span></span>  
 <span data-ttu-id="ee2c5-238">程式碼範例範本不允許使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-238">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="ee2c5-239">資料模型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-239">Data model</span></span>  
 <span data-ttu-id="ee2c5-240">[程式碼範例](api-management-template-data-model-reference.md#Sample)實體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-240">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="ee2c5-241">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="ee2c5-241">Sample template data</span></span>  
  
```json  
{  
    "title": "Python",  
    "snippet": null,  
    "brush": "python",  
    "template": "DocumentationSamplesPython",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="ee2c5-242"><a name="Ruby"></a>Ruby</span><span class="sxs-lookup"><span data-stu-id="ee2c5-242"><a name="Ruby"></a> Ruby</span></span>  
 <span data-ttu-id="ee2c5-243">**DocumentationSamplesRuby** 範本可讓您在作業頁面的程式碼範例區段中自訂該程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-243">The **DocumentationSamplesRuby** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="ee2c5-244">預設範本</span><span class="sxs-lookup"><span data-stu-id="ee2c5-244">Default template</span></span>  
  
```xml  
require 'net/http'  
  
uri = URI('{{scheme}}://{{host}}{{path}}')  
uri.query = URI.encode_www_form({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}' => '{{parameter.value}}'{% unless forloop.last %},{% endunless %}  
{% endfor -%}  
{% endif -%}  
})  
  
request = Net::HTTP::{{ method | downcase | capitalize }}.new(uri.request_uri)  
{% for header in headers -%}  
# Request headers  
request['{{header.name}}'] = '{{header.value}}'  
{% endfor -%}  
{% if body -%}  
# Request body  
request.body = "{{ body | replace:'"','\"' }}"  
{% endif -%}  
  
response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|  
    http.request(request)  
end  
  
puts response.body  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="ee2c5-245">控制</span><span class="sxs-lookup"><span data-stu-id="ee2c5-245">Controls</span></span>  
 <span data-ttu-id="ee2c5-246">程式碼範例範本不允許使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-246">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="ee2c5-247">資料模型</span><span class="sxs-lookup"><span data-stu-id="ee2c5-247">Data model</span></span>  
 <span data-ttu-id="ee2c5-248">[程式碼範例](api-management-template-data-model-reference.md#Sample)實體。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-248">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="ee2c5-249">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="ee2c5-249">Sample template data</span></span>  
  
```json  
{  
    "title": "Ruby",  
    "snippet": null,  
    "brush": "ruby",  
    "template": "DocumentationSamplesRuby",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```

## <a name="next-steps"></a><span data-ttu-id="ee2c5-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee2c5-250">Next steps</span></span>
<span data-ttu-id="ee2c5-251">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="ee2c5-251">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>