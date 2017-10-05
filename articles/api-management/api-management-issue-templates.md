---
title: "Azure API 管理中的問題範本 | Microsoft Docs"
description: "了解如何在「Azure API 管理」中自訂開發人員入口網站中的「問題」頁面內容。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: e13344df198bca4f73c75fa58221436b94e2f258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="a21b1-103">Azure API 管理中的問題範本</span><span class="sxs-lookup"><span data-stu-id="a21b1-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="a21b1-104">「Azure API 管理」可讓您使用一組可設定開發人員入口網站頁面內容的範本，來自訂那些頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="a21b1-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="a21b1-105">使用這些範本時，您可以運用 [DotLiquid](http://dotliquidmarkup.org/) 語法和您選擇的編輯器 (例如 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers))，以及一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)、[字符資源](api-management-template-resources.md#glyphs)和[頁面控制項](api-management-page-controls.md)，依照您的想法自由靈活地設定頁面內容。</span><span class="sxs-lookup"><span data-stu-id="a21b1-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="a21b1-106">本節的範本可讓您自訂開發人員入口網站中「問題」頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="a21b1-106">The templates in this section allow you to customize the content of the Issue pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="a21b1-107">問題清單</span><span class="sxs-lookup"><span data-stu-id="a21b1-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="a21b1-108">下列文件中包含範例預設範本，但範本可能會因持續進行的改善而有變更。</span><span class="sxs-lookup"><span data-stu-id="a21b1-108">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="a21b1-109">您可以瀏覽至想要的個別範本，來檢視開發人員入口網站中的即時預設範本。</span><span class="sxs-lookup"><span data-stu-id="a21b1-109">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="a21b1-110">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="a21b1-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="a21b1-111"><a name="IssueList"></a> 問題清單</span><span class="sxs-lookup"><span data-stu-id="a21b1-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="a21b1-112">「問題清單」範本可讓您自訂開發人員入口網站中問題清單頁面的主體。</span><span class="sxs-lookup"><span data-stu-id="a21b1-112">The **Issue list** template allows you to customize the body of the issue list page in the developer portal.</span></span>  
  
 <span data-ttu-id="a21b1-113">![問題清單開發人員入口網站](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM 問題清單開發人員入口網站")</span><span class="sxs-lookup"><span data-stu-id="a21b1-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="a21b1-114">預設範本</span><span class="sxs-lookup"><span data-stu-id="a21b1-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="a21b1-115">控制</span><span class="sxs-lookup"><span data-stu-id="a21b1-115">Controls</span></span>  
 <span data-ttu-id="a21b1-116">`Issue list` 範本可能會使用下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="a21b1-116">The `Issue list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="a21b1-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="a21b1-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="a21b1-118">資料模型</span><span class="sxs-lookup"><span data-stu-id="a21b1-118">Data model</span></span>  
  
|<span data-ttu-id="a21b1-119">屬性</span><span class="sxs-lookup"><span data-stu-id="a21b1-119">Property</span></span>|<span data-ttu-id="a21b1-120">類型</span><span class="sxs-lookup"><span data-stu-id="a21b1-120">Type</span></span>|<span data-ttu-id="a21b1-121">說明</span><span class="sxs-lookup"><span data-stu-id="a21b1-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="a21b1-122">問題</span><span class="sxs-lookup"><span data-stu-id="a21b1-122">Issues</span></span>|<span data-ttu-id="a21b1-123">[問題](api-management-template-data-model-reference.md#Issue)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="a21b1-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="a21b1-124">目前使用者可看見的問題。</span><span class="sxs-lookup"><span data-stu-id="a21b1-124">The issues visible to the current user.</span></span>|  
|<span data-ttu-id="a21b1-125">分頁</span><span class="sxs-lookup"><span data-stu-id="a21b1-125">Paging</span></span>|<span data-ttu-id="a21b1-126">[分頁](api-management-template-data-model-reference.md#Paging)實體。</span><span class="sxs-lookup"><span data-stu-id="a21b1-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="a21b1-127">應用程式集合的分頁資訊。</span><span class="sxs-lookup"><span data-stu-id="a21b1-127">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="a21b1-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="a21b1-128">IsAuthenticated</span></span>|<span data-ttu-id="a21b1-129">布林值</span><span class="sxs-lookup"><span data-stu-id="a21b1-129">boolean</span></span>|<span data-ttu-id="a21b1-130">目前使用者是否已登入開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="a21b1-130">Whether the current user is signed-in to the developer portal.</span></span>|  
|<span data-ttu-id="a21b1-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="a21b1-131">CanReportIssues</span></span>|<span data-ttu-id="a21b1-132">布林值</span><span class="sxs-lookup"><span data-stu-id="a21b1-132">boolean</span></span>|<span data-ttu-id="a21b1-133">目前使用者是否具備提出問題的權限。</span><span class="sxs-lookup"><span data-stu-id="a21b1-133">Whether the current user has permissions to file an issue.</span></span>|  
|<span data-ttu-id="a21b1-134">搜尋</span><span class="sxs-lookup"><span data-stu-id="a21b1-134">Search</span></span>|<span data-ttu-id="a21b1-135">字串</span><span class="sxs-lookup"><span data-stu-id="a21b1-135">string</span></span>|<span data-ttu-id="a21b1-136">此屬性已過時而不應使用。</span><span class="sxs-lookup"><span data-stu-id="a21b1-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="a21b1-137">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="a21b1-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how to connect my application to the API",  
            "Description": "I'm having trouble connecting my application to the backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="a21b1-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a21b1-138">Next steps</span></span>
<span data-ttu-id="a21b1-139">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="a21b1-139">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>