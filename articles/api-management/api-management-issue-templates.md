---
title: "在 Azure API 管理 aaaIssue 範本 |Microsoft 文件"
description: "了解如何 toocustomize hello hello 開發人員入口網站在 Azure API 管理中的 hello 問題網頁的內容。"
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
ms.openlocfilehash: e12902e52c164f73902a97f15ea550790dfecf1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="def1f-103">Azure API 管理中的問題範本</span><span class="sxs-lookup"><span data-stu-id="def1f-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="def1f-104">Azure API 管理提供 hello 能力 toocustomize hello 網頁內容的開發人員入口網站使用的一組設定其內容的範本。</span><span class="sxs-lookup"><span data-stu-id="def1f-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="def1f-105">使用[DotLiquid](http://dotliquidmarkup.org/)語法和 hello 您選擇的編輯器例如[針對設計人員 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers)，和一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)， [字符資源](api-management-template-resources.md#glyphs)，和[頁面控制項](api-management-page-controls.md)，視使用這些範本，您會有很大的彈性 tooconfigure hello 網頁內容的 hello。</span><span class="sxs-lookup"><span data-stu-id="def1f-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="def1f-106">本節中的 hello 範本允許您 toocustomize hello 網頁內容的 hello 問題 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="def1f-106">hello templates in this section allow you toocustomize hello content of hello Issue pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="def1f-107">問題清單</span><span class="sxs-lookup"><span data-stu-id="def1f-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="def1f-108">預設範本範例隨附的 hello 下列文件，但主旨 toochange 到期 toocontinuous 增強功能。</span><span class="sxs-lookup"><span data-stu-id="def1f-108">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="def1f-109">您可以檢視 hello 開發人員入口網站中的 hello 即時預設範本，藉由瀏覽 toohello 需要個別的範本。</span><span class="sxs-lookup"><span data-stu-id="def1f-109">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="def1f-110">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="def1f-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="def1f-111"><a name="IssueList"></a> 問題清單</span><span class="sxs-lookup"><span data-stu-id="def1f-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="def1f-112">hello**問題清單**範本可讓您 toocustomize hello 主體 hello 問題清單頁面 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="def1f-112">hello **Issue list** template allows you toocustomize hello body of hello issue list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="def1f-113">![問題清單開發人員入口網站](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM 問題清單開發人員入口網站")</span><span class="sxs-lookup"><span data-stu-id="def1f-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="def1f-114">預設範本</span><span class="sxs-lookup"><span data-stu-id="def1f-114">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="def1f-115">控制</span><span class="sxs-lookup"><span data-stu-id="def1f-115">Controls</span></span>  
 <span data-ttu-id="def1f-116">hello`Issue list`範本可能使用 hello 下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="def1f-116">hello `Issue list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="def1f-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="def1f-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="def1f-118">資料模型</span><span class="sxs-lookup"><span data-stu-id="def1f-118">Data model</span></span>  
  
|<span data-ttu-id="def1f-119">屬性</span><span class="sxs-lookup"><span data-stu-id="def1f-119">Property</span></span>|<span data-ttu-id="def1f-120">類型</span><span class="sxs-lookup"><span data-stu-id="def1f-120">Type</span></span>|<span data-ttu-id="def1f-121">說明</span><span class="sxs-lookup"><span data-stu-id="def1f-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="def1f-122">問題</span><span class="sxs-lookup"><span data-stu-id="def1f-122">Issues</span></span>|<span data-ttu-id="def1f-123">[問題](api-management-template-data-model-reference.md#Issue)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="def1f-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="def1f-124">hello 問題可見 toohello 目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="def1f-124">hello issues visible toohello current user.</span></span>|  
|<span data-ttu-id="def1f-125">分頁</span><span class="sxs-lookup"><span data-stu-id="def1f-125">Paging</span></span>|<span data-ttu-id="def1f-126">[分頁](api-management-template-data-model-reference.md#Paging)實體。</span><span class="sxs-lookup"><span data-stu-id="def1f-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="def1f-127">hello hello 應用程式集合的分頁資訊。</span><span class="sxs-lookup"><span data-stu-id="def1f-127">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="def1f-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="def1f-128">IsAuthenticated</span></span>|<span data-ttu-id="def1f-129">布林值</span><span class="sxs-lookup"><span data-stu-id="def1f-129">boolean</span></span>|<span data-ttu-id="def1f-130">Hello 目前使用者是否登入的 toohello 開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="def1f-130">Whether hello current user is signed-in toohello developer portal.</span></span>|  
|<span data-ttu-id="def1f-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="def1f-131">CanReportIssues</span></span>|<span data-ttu-id="def1f-132">布林值</span><span class="sxs-lookup"><span data-stu-id="def1f-132">boolean</span></span>|<span data-ttu-id="def1f-133">Hello 目前使用者是否擁有權限 toofile 發生問題。</span><span class="sxs-lookup"><span data-stu-id="def1f-133">Whether hello current user has permissions toofile an issue.</span></span>|  
|<span data-ttu-id="def1f-134">搜尋</span><span class="sxs-lookup"><span data-stu-id="def1f-134">Search</span></span>|<span data-ttu-id="def1f-135">字串</span><span class="sxs-lookup"><span data-stu-id="def1f-135">string</span></span>|<span data-ttu-id="def1f-136">此屬性已過時而不應使用。</span><span class="sxs-lookup"><span data-stu-id="def1f-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="def1f-137">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="def1f-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how tooconnect my application toohello API",  
            "Description": "I'm having trouble connecting my application toohello backend API.",  
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

## <a name="next-steps"></a><span data-ttu-id="def1f-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="def1f-138">Next steps</span></span>
<span data-ttu-id="def1f-139">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="def1f-139">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
