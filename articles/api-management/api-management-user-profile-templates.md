---
title: "Azure API 管理中的使用者設定檔範本 | Microsoft Docs"
description: "了解如何在 Azure API 管理中自訂開發人員入口網站中的 [使用者設定檔] 頁面內容。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 9a11bd5800068a5725ab2f099043993bff0b28d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="0aec2-103">Azure API 管理中的使用者設定檔範本</span><span class="sxs-lookup"><span data-stu-id="0aec2-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="0aec2-104">「Azure API 管理」可讓您使用一組可設定開發人員入口網站頁面內容的範本，來自訂那些頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="0aec2-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="0aec2-105">使用這些範本時，您可以運用 [DotLiquid](http://dotliquidmarkup.org/) 語法和您選擇的編輯器 (例如 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers))，以及一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)、[字符資源](api-management-template-resources.md#glyphs)和[頁面控制項](api-management-page-controls.md)，依照您的想法自由靈活地設定頁面內容。</span><span class="sxs-lookup"><span data-stu-id="0aec2-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="0aec2-106">本節的範本可讓您自訂開發人員入口網站中 [使用者設定檔] 頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="0aec2-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="0aec2-107">設定檔</span><span class="sxs-lookup"><span data-stu-id="0aec2-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="0aec2-108">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0aec2-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="0aec2-109">應用程式</span><span class="sxs-lookup"><span data-stu-id="0aec2-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="0aec2-110">更新帳戶資訊</span><span class="sxs-lookup"><span data-stu-id="0aec2-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="0aec2-111">下列文件中包含範例預設範本，但範本可能會因持續進行的改善而有變更。</span><span class="sxs-lookup"><span data-stu-id="0aec2-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="0aec2-112">您可以瀏覽至想要的個別範本，來檢視開發人員入口網站中的即時預設範本。</span><span class="sxs-lookup"><span data-stu-id="0aec2-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="0aec2-113">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。</span><span class="sxs-lookup"><span data-stu-id="0aec2-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="0aec2-114"><a name="Profile"></a> 設定檔</span><span class="sxs-lookup"><span data-stu-id="0aec2-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="0aec2-115">**設定檔**範本可讓您自訂開發人員入口網站中 [使用者設定檔] 頁面的使用者設定檔區段。</span><span class="sxs-lookup"><span data-stu-id="0aec2-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="0aec2-116">![使用者設定檔頁面](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM 使用者設定檔頁面")</span><span class="sxs-lookup"><span data-stu-id="0aec2-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="0aec2-117">預設範本</span><span class="sxs-lookup"><span data-stu-id="0aec2-117">Default template</span></span>  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="0aec2-118">控制</span><span class="sxs-lookup"><span data-stu-id="0aec2-118">Controls</span></span>  
 <span data-ttu-id="0aec2-119">此範本可能不使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="0aec2-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="0aec2-120">資料模型</span><span class="sxs-lookup"><span data-stu-id="0aec2-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0aec2-121">[設定檔](#Profile)、[應用程式](#Applications)、[訂用帳戶](#Subscriptions)範本共用相同的資料模型，並接收相同的範本資料。</span><span class="sxs-lookup"><span data-stu-id="0aec2-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="0aec2-122">屬性</span><span class="sxs-lookup"><span data-stu-id="0aec2-122">Property</span></span>|<span data-ttu-id="0aec2-123">類型</span><span class="sxs-lookup"><span data-stu-id="0aec2-123">Type</span></span>|<span data-ttu-id="0aec2-124">說明</span><span class="sxs-lookup"><span data-stu-id="0aec2-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="0aec2-125">firstName</span><span class="sxs-lookup"><span data-stu-id="0aec2-125">firstName</span></span>|<span data-ttu-id="0aec2-126">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-126">string</span></span>|<span data-ttu-id="0aec2-127">目前使用者的名字。</span><span class="sxs-lookup"><span data-stu-id="0aec2-127">First name of the current user.</span></span>|  
|<span data-ttu-id="0aec2-128">lastName</span><span class="sxs-lookup"><span data-stu-id="0aec2-128">lastName</span></span>|<span data-ttu-id="0aec2-129">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-129">string</span></span>|<span data-ttu-id="0aec2-130">目前使用者的姓氏。</span><span class="sxs-lookup"><span data-stu-id="0aec2-130">Last name of the current user.</span></span>|  
|<span data-ttu-id="0aec2-131">companyName</span><span class="sxs-lookup"><span data-stu-id="0aec2-131">companyName</span></span>|<span data-ttu-id="0aec2-132">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-132">string</span></span>|<span data-ttu-id="0aec2-133">目前使用者的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="0aec2-133">The company name of the current user.</span></span>|  
|<span data-ttu-id="0aec2-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="0aec2-134">addresserEmail</span></span>|<span data-ttu-id="0aec2-135">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-135">string</span></span>|<span data-ttu-id="0aec2-136">目前使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0aec2-136">Email address of the current user.</span></span>|  
|<span data-ttu-id="0aec2-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="0aec2-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="0aec2-138">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-138">string</span></span>|<span data-ttu-id="0aec2-139">相對 URL，可前往檢視目前使用者的分析。</span><span class="sxs-lookup"><span data-stu-id="0aec2-139">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="0aec2-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="0aec2-140">subscriptions</span></span>|<span data-ttu-id="0aec2-141">[訂用帳戶](api-management-template-data-model-reference.md#Subscription)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="0aec2-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="0aec2-142">目前使用者的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0aec2-142">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="0aec2-143">應用程式所需</span><span class="sxs-lookup"><span data-stu-id="0aec2-143">applications</span></span>|<span data-ttu-id="0aec2-144">[應用程式](api-management-template-data-model-reference.md#Application)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="0aec2-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="0aec2-145">目前使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0aec2-145">The applications of the current user.</span></span>|  
|<span data-ttu-id="0aec2-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="0aec2-146">changePasswordUrl</span></span>|<span data-ttu-id="0aec2-147">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-147">string</span></span>|<span data-ttu-id="0aec2-148">相對 URL，可前往變更目前使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="0aec2-148">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="0aec2-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="0aec2-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="0aec2-150">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-150">string</span></span>|<span data-ttu-id="0aec2-151">相對 URL，可前往變更目前使用者的名稱和電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0aec2-151">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="0aec2-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="0aec2-152">canChangePassword</span></span>|<span data-ttu-id="0aec2-153">布林值</span><span class="sxs-lookup"><span data-stu-id="0aec2-153">boolean</span></span>|<span data-ttu-id="0aec2-154">目前使用者是否可以變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="0aec2-154">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="0aec2-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="0aec2-155">isSystemUser</span></span>|<span data-ttu-id="0aec2-156">布林值</span><span class="sxs-lookup"><span data-stu-id="0aec2-156">boolean</span></span>|<span data-ttu-id="0aec2-157">目前使用者是否是其中一個內建[群組](api-management-key-concepts.md#groups)的成員。</span><span class="sxs-lookup"><span data-stu-id="0aec2-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="0aec2-158">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="0aec2-158">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="0aec2-159"><a name="Subscriptions"></a> 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0aec2-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="0aec2-160">**訂用帳戶**範本可讓您自訂開發人員入口網站中 [使用者設定檔] 頁面的訂用帳戶區段。</span><span class="sxs-lookup"><span data-stu-id="0aec2-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="0aec2-161">![使用者訂用帳戶頁面](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM 使用者訂用帳戶頁面")</span><span class="sxs-lookup"><span data-stu-id="0aec2-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="0aec2-162">預設範本</span><span class="sxs-lookup"><span data-stu-id="0aec2-162">Default template</span></span>  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="0aec2-163">控制</span><span class="sxs-lookup"><span data-stu-id="0aec2-163">Controls</span></span>  
 <span data-ttu-id="0aec2-164">此範本可能會使用下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="0aec2-164">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="0aec2-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="0aec2-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="0aec2-166">資料模型</span><span class="sxs-lookup"><span data-stu-id="0aec2-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0aec2-167">[設定檔](#Profile)、[應用程式](#Applications)、[訂用帳戶](#Subscriptions)範本共用相同的資料模型，並接收相同的範本資料。</span><span class="sxs-lookup"><span data-stu-id="0aec2-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="0aec2-168">屬性</span><span class="sxs-lookup"><span data-stu-id="0aec2-168">Property</span></span>|<span data-ttu-id="0aec2-169">類型</span><span class="sxs-lookup"><span data-stu-id="0aec2-169">Type</span></span>|<span data-ttu-id="0aec2-170">說明</span><span class="sxs-lookup"><span data-stu-id="0aec2-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="0aec2-171">firstName</span><span class="sxs-lookup"><span data-stu-id="0aec2-171">firstName</span></span>|<span data-ttu-id="0aec2-172">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-172">string</span></span>|<span data-ttu-id="0aec2-173">目前使用者的名字。</span><span class="sxs-lookup"><span data-stu-id="0aec2-173">First name of the current user.</span></span>|  
|<span data-ttu-id="0aec2-174">lastName</span><span class="sxs-lookup"><span data-stu-id="0aec2-174">lastName</span></span>|<span data-ttu-id="0aec2-175">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-175">string</span></span>|<span data-ttu-id="0aec2-176">目前使用者的姓氏。</span><span class="sxs-lookup"><span data-stu-id="0aec2-176">Last name of the current user.</span></span>|  
|<span data-ttu-id="0aec2-177">companyName</span><span class="sxs-lookup"><span data-stu-id="0aec2-177">companyName</span></span>|<span data-ttu-id="0aec2-178">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-178">string</span></span>|<span data-ttu-id="0aec2-179">目前使用者的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="0aec2-179">The company name of the current user.</span></span>|  
|<span data-ttu-id="0aec2-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="0aec2-180">addresserEmail</span></span>|<span data-ttu-id="0aec2-181">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-181">string</span></span>|<span data-ttu-id="0aec2-182">目前使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0aec2-182">Email address of the current user.</span></span>|  
|<span data-ttu-id="0aec2-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="0aec2-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="0aec2-184">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-184">string</span></span>|<span data-ttu-id="0aec2-185">相對 URL，可前往檢視目前使用者的分析。</span><span class="sxs-lookup"><span data-stu-id="0aec2-185">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="0aec2-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="0aec2-186">subscriptions</span></span>|<span data-ttu-id="0aec2-187">[訂用帳戶](api-management-template-data-model-reference.md#Subscription)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="0aec2-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="0aec2-188">目前使用者的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0aec2-188">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="0aec2-189">應用程式所需</span><span class="sxs-lookup"><span data-stu-id="0aec2-189">applications</span></span>|<span data-ttu-id="0aec2-190">[應用程式](api-management-template-data-model-reference.md#Application)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="0aec2-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="0aec2-191">目前使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0aec2-191">The applications of the current user.</span></span>|  
|<span data-ttu-id="0aec2-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="0aec2-192">changePasswordUrl</span></span>|<span data-ttu-id="0aec2-193">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-193">string</span></span>|<span data-ttu-id="0aec2-194">相對 URL，可前往變更目前使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="0aec2-194">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="0aec2-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="0aec2-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="0aec2-196">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-196">string</span></span>|<span data-ttu-id="0aec2-197">相對 URL，可前往變更目前使用者的名稱和電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0aec2-197">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="0aec2-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="0aec2-198">canChangePassword</span></span>|<span data-ttu-id="0aec2-199">布林值</span><span class="sxs-lookup"><span data-stu-id="0aec2-199">boolean</span></span>|<span data-ttu-id="0aec2-200">目前使用者是否可以變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="0aec2-200">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="0aec2-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="0aec2-201">isSystemUser</span></span>|<span data-ttu-id="0aec2-202">布林值</span><span class="sxs-lookup"><span data-stu-id="0aec2-202">boolean</span></span>|<span data-ttu-id="0aec2-203">目前使用者是否是其中一個內建[群組](api-management-key-concepts.md#groups)的成員。</span><span class="sxs-lookup"><span data-stu-id="0aec2-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="0aec2-204">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="0aec2-204">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="0aec2-205"><a name="Applications"></a> 應用程式</span><span class="sxs-lookup"><span data-stu-id="0aec2-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="0aec2-206">**應用程式**範本可讓您自訂開發人員入口網站中 [使用者設定檔] 頁面的訂用帳戶區段。</span><span class="sxs-lookup"><span data-stu-id="0aec2-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="0aec2-207">![使用者帳戶的應用程式頁面](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM 使用者帳戶的應用程式頁面")</span><span class="sxs-lookup"><span data-stu-id="0aec2-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="0aec2-208">預設範本</span><span class="sxs-lookup"><span data-stu-id="0aec2-208">Default template</span></span>  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="0aec2-209">控制</span><span class="sxs-lookup"><span data-stu-id="0aec2-209">Controls</span></span>  
 <span data-ttu-id="0aec2-210">此範本可能會使用下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="0aec2-210">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="0aec2-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="0aec2-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="0aec2-212">資料模型</span><span class="sxs-lookup"><span data-stu-id="0aec2-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0aec2-213">[設定檔](#Profile)、[應用程式](#Applications)、[訂用帳戶](#Subscriptions)範本共用相同的資料模型，並接收相同的範本資料。</span><span class="sxs-lookup"><span data-stu-id="0aec2-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="0aec2-214">屬性</span><span class="sxs-lookup"><span data-stu-id="0aec2-214">Property</span></span>|<span data-ttu-id="0aec2-215">類型</span><span class="sxs-lookup"><span data-stu-id="0aec2-215">Type</span></span>|<span data-ttu-id="0aec2-216">說明</span><span class="sxs-lookup"><span data-stu-id="0aec2-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="0aec2-217">firstName</span><span class="sxs-lookup"><span data-stu-id="0aec2-217">firstName</span></span>|<span data-ttu-id="0aec2-218">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-218">string</span></span>|<span data-ttu-id="0aec2-219">目前使用者的名字。</span><span class="sxs-lookup"><span data-stu-id="0aec2-219">First name of the current user.</span></span>|  
|<span data-ttu-id="0aec2-220">lastName</span><span class="sxs-lookup"><span data-stu-id="0aec2-220">lastName</span></span>|<span data-ttu-id="0aec2-221">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-221">string</span></span>|<span data-ttu-id="0aec2-222">目前使用者的姓氏。</span><span class="sxs-lookup"><span data-stu-id="0aec2-222">Last name of the current user.</span></span>|  
|<span data-ttu-id="0aec2-223">companyName</span><span class="sxs-lookup"><span data-stu-id="0aec2-223">companyName</span></span>|<span data-ttu-id="0aec2-224">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-224">string</span></span>|<span data-ttu-id="0aec2-225">目前使用者的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="0aec2-225">The company name of the current user.</span></span>|  
|<span data-ttu-id="0aec2-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="0aec2-226">addresserEmail</span></span>|<span data-ttu-id="0aec2-227">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-227">string</span></span>|<span data-ttu-id="0aec2-228">目前使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0aec2-228">Email address of the current user.</span></span>|  
|<span data-ttu-id="0aec2-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="0aec2-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="0aec2-230">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-230">string</span></span>|<span data-ttu-id="0aec2-231">相對 URL，可前往檢視目前使用者的分析。</span><span class="sxs-lookup"><span data-stu-id="0aec2-231">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="0aec2-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="0aec2-232">subscriptions</span></span>|<span data-ttu-id="0aec2-233">[訂用帳戶](api-management-template-data-model-reference.md#Subscription)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="0aec2-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="0aec2-234">目前使用者的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0aec2-234">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="0aec2-235">應用程式所需</span><span class="sxs-lookup"><span data-stu-id="0aec2-235">applications</span></span>|<span data-ttu-id="0aec2-236">[應用程式](api-management-template-data-model-reference.md#Application)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="0aec2-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="0aec2-237">目前使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0aec2-237">The applications of the current user.</span></span>|  
|<span data-ttu-id="0aec2-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="0aec2-238">changePasswordUrl</span></span>|<span data-ttu-id="0aec2-239">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-239">string</span></span>|<span data-ttu-id="0aec2-240">相對 URL，可前往變更目前使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="0aec2-240">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="0aec2-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="0aec2-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="0aec2-242">字串</span><span class="sxs-lookup"><span data-stu-id="0aec2-242">string</span></span>|<span data-ttu-id="0aec2-243">相對 URL，可前往變更目前使用者的名稱和電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0aec2-243">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="0aec2-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="0aec2-244">canChangePassword</span></span>|<span data-ttu-id="0aec2-245">布林值</span><span class="sxs-lookup"><span data-stu-id="0aec2-245">boolean</span></span>|<span data-ttu-id="0aec2-246">目前使用者是否可以變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="0aec2-246">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="0aec2-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="0aec2-247">isSystemUser</span></span>|<span data-ttu-id="0aec2-248">布林值</span><span class="sxs-lookup"><span data-stu-id="0aec2-248">boolean</span></span>|<span data-ttu-id="0aec2-249">目前使用者是否是其中一個內建[群組](api-management-key-concepts.md#groups)的成員。</span><span class="sxs-lookup"><span data-stu-id="0aec2-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="0aec2-250">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="0aec2-250">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="0aec2-251"><a name="UpdateAccountInfo"></a> 更新帳戶資訊</span><span class="sxs-lookup"><span data-stu-id="0aec2-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="0aec2-252">**更新帳戶資訊**範本可讓您自訂開發人員入口網站中的 [更新帳戶資訊] 頁面。</span><span class="sxs-lookup"><span data-stu-id="0aec2-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span></span>  
  
 <span data-ttu-id="0aec2-253">![使用者帳戶資訊頁面開發人員入口網站範本](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM 使用者帳戶資訊頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="0aec2-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="0aec2-254">預設範本</span><span class="sxs-lookup"><span data-stu-id="0aec2-254">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a><span data-ttu-id="0aec2-255">控制</span><span class="sxs-lookup"><span data-stu-id="0aec2-255">Controls</span></span>  
 <span data-ttu-id="0aec2-256">此範本可能不使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="0aec2-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="0aec2-257">資料模型</span><span class="sxs-lookup"><span data-stu-id="0aec2-257">Data model</span></span>  
 <span data-ttu-id="0aec2-258">[使用者帳戶資訊](api-management-template-data-model-reference.md#UserAccountInfo)實體。</span><span class="sxs-lookup"><span data-stu-id="0aec2-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="0aec2-259">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="0aec2-259">Sample template data</span></span>  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a><span data-ttu-id="0aec2-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0aec2-260">Next steps</span></span>
<span data-ttu-id="0aec2-261">如需有關使用範本的詳細資訊，請參閱[如何使用範本自訂 API 管理開發人員入口網站](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="0aec2-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>