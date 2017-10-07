---
title: "aaa\"在 Azure API 管理的使用者設定檔範本 |Microsoft 文件 」"
description: "了解 hello 開發人員入口網站在 Azure API 管理中的 hello 使用者設定檔的 toocustomize hello 內容頁面的方式。"
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
ms.openlocfilehash: c8f153b310221164809acf58e4af236928ceb41d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="80e4f-103">Azure API 管理中的使用者設定檔範本</span><span class="sxs-lookup"><span data-stu-id="80e4f-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="80e4f-104">Azure API 管理提供 hello 能力 toocustomize hello 網頁內容的開發人員入口網站使用的一組設定其內容的範本。</span><span class="sxs-lookup"><span data-stu-id="80e4f-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="80e4f-105">使用[DotLiquid](http://dotliquidmarkup.org/)語法和 hello 您選擇的編輯器例如[針對設計人員 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers)，和一組提供的當地語系化[字串資源](api-management-template-resources.md#strings)， [字符資源](api-management-template-resources.md#glyphs)，和[頁面控制項](api-management-page-controls.md)，視使用這些範本，您會有很大的彈性 tooconfigure hello 網頁內容的 hello。</span><span class="sxs-lookup"><span data-stu-id="80e4f-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="80e4f-106">本節中的 hello 範本允許您 toocustomize hello 網頁內容的 hello 使用者設定檔在 hello 開發人員入口網站中。</span><span class="sxs-lookup"><span data-stu-id="80e4f-106">hello templates in this section allow you toocustomize hello content of hello User profile pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="80e4f-107">設定檔</span><span class="sxs-lookup"><span data-stu-id="80e4f-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="80e4f-108">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="80e4f-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="80e4f-109">應用程式</span><span class="sxs-lookup"><span data-stu-id="80e4f-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="80e4f-110">更新帳戶資訊</span><span class="sxs-lookup"><span data-stu-id="80e4f-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="80e4f-111">預設範本範例隨附的 hello 下列文件，但主旨 toochange 到期 toocontinuous 增強功能。</span><span class="sxs-lookup"><span data-stu-id="80e4f-111">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="80e4f-112">您可以檢視 hello 開發人員入口網站中的 hello 即時預設範本，藉由瀏覽 toohello 需要個別的範本。</span><span class="sxs-lookup"><span data-stu-id="80e4f-112">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="80e4f-113">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。</span><span class="sxs-lookup"><span data-stu-id="80e4f-113">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="80e4f-114"><a name="Profile"></a> 設定檔</span><span class="sxs-lookup"><span data-stu-id="80e4f-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="80e4f-115">hello**設定檔**範本可讓您在 hello 開發人員入口網站中的 hello 使用者設定檔頁面的 toocustomize hello 使用者設定檔區段。</span><span class="sxs-lookup"><span data-stu-id="80e4f-115">hello **profile** template allows you toocustomize hello user profile section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="80e4f-116">![使用者設定檔頁面](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM 使用者設定檔頁面")</span><span class="sxs-lookup"><span data-stu-id="80e4f-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="80e4f-117">預設範本</span><span class="sxs-lookup"><span data-stu-id="80e4f-117">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="80e4f-118">控制</span><span class="sxs-lookup"><span data-stu-id="80e4f-118">Controls</span></span>  
 <span data-ttu-id="80e4f-119">此範本可能不使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="80e4f-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="80e4f-120">資料模型</span><span class="sxs-lookup"><span data-stu-id="80e4f-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="80e4f-121">hello[設定檔](#Profile)，[應用程式](#Applications)，和[訂閱](#Subscriptions)範本會共用相同的資料模型，並收到 hello hello 相同的範本資料。</span><span class="sxs-lookup"><span data-stu-id="80e4f-121">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="80e4f-122">屬性</span><span class="sxs-lookup"><span data-stu-id="80e4f-122">Property</span></span>|<span data-ttu-id="80e4f-123">類型</span><span class="sxs-lookup"><span data-stu-id="80e4f-123">Type</span></span>|<span data-ttu-id="80e4f-124">說明</span><span class="sxs-lookup"><span data-stu-id="80e4f-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="80e4f-125">firstName</span><span class="sxs-lookup"><span data-stu-id="80e4f-125">firstName</span></span>|<span data-ttu-id="80e4f-126">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-126">string</span></span>|<span data-ttu-id="80e4f-127">Hello 目前使用者的名字。</span><span class="sxs-lookup"><span data-stu-id="80e4f-127">First name of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-128">lastName</span><span class="sxs-lookup"><span data-stu-id="80e4f-128">lastName</span></span>|<span data-ttu-id="80e4f-129">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-129">string</span></span>|<span data-ttu-id="80e4f-130">Hello 目前使用者的姓氏。</span><span class="sxs-lookup"><span data-stu-id="80e4f-130">Last name of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-131">companyName</span><span class="sxs-lookup"><span data-stu-id="80e4f-131">companyName</span></span>|<span data-ttu-id="80e4f-132">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-132">string</span></span>|<span data-ttu-id="80e4f-133">hello hello 目前使用者的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="80e4f-133">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="80e4f-134">addresserEmail</span></span>|<span data-ttu-id="80e4f-135">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-135">string</span></span>|<span data-ttu-id="80e4f-136">Hello 目前使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="80e4f-136">Email address of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="80e4f-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="80e4f-138">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-138">string</span></span>|<span data-ttu-id="80e4f-139">Hello 目前使用者的相對 URL tooview 分析。</span><span class="sxs-lookup"><span data-stu-id="80e4f-139">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="80e4f-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="80e4f-140">subscriptions</span></span>|<span data-ttu-id="80e4f-141">[訂用帳戶](api-management-template-data-model-reference.md#Subscription)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="80e4f-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="80e4f-142">hello hello 目前使用者的訂閱。</span><span class="sxs-lookup"><span data-stu-id="80e4f-142">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="80e4f-143">應用程式所需</span><span class="sxs-lookup"><span data-stu-id="80e4f-143">applications</span></span>|<span data-ttu-id="80e4f-144">[應用程式](api-management-template-data-model-reference.md#Application)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="80e4f-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="80e4f-145">hello 目前使用者的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="80e4f-145">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="80e4f-146">changePasswordUrl</span></span>|<span data-ttu-id="80e4f-147">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-147">string</span></span>|<span data-ttu-id="80e4f-148">hello 相對 URL toochange hello 目前使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="80e4f-148">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="80e4f-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="80e4f-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="80e4f-150">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-150">string</span></span>|<span data-ttu-id="80e4f-151">hello 相對 URL toochange hello 名稱與 hello 目前使用者的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="80e4f-151">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="80e4f-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="80e4f-152">canChangePassword</span></span>|<span data-ttu-id="80e4f-153">布林值</span><span class="sxs-lookup"><span data-stu-id="80e4f-153">boolean</span></span>|<span data-ttu-id="80e4f-154">是否 hello 目前的使用者可以變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="80e4f-154">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="80e4f-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="80e4f-155">isSystemUser</span></span>|<span data-ttu-id="80e4f-156">布林值</span><span class="sxs-lookup"><span data-stu-id="80e4f-156">boolean</span></span>|<span data-ttu-id="80e4f-157">Hello 目前使用者是否為其中一個 hello 內建成員[群組](api-management-key-concepts.md#groups)。</span><span class="sxs-lookup"><span data-stu-id="80e4f-157">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="80e4f-158">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="80e4f-158">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="80e4f-159"><a name="Subscriptions"></a> 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="80e4f-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="80e4f-160">hello**訂閱**範本可讓您 toocustomize hello 訂閱 區段中的 hello 開發人員入口網站中的 hello 使用者設定檔頁面。</span><span class="sxs-lookup"><span data-stu-id="80e4f-160">hello **Subscriptions** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="80e4f-161">![使用者訂用帳戶頁面](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM 使用者訂用帳戶頁面")</span><span class="sxs-lookup"><span data-stu-id="80e4f-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="80e4f-162">預設範本</span><span class="sxs-lookup"><span data-stu-id="80e4f-162">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="80e4f-163">控制</span><span class="sxs-lookup"><span data-stu-id="80e4f-163">Controls</span></span>  
 <span data-ttu-id="80e4f-164">此範本可能會使用 hello 下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="80e4f-164">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="80e4f-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="80e4f-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="80e4f-166">資料模型</span><span class="sxs-lookup"><span data-stu-id="80e4f-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="80e4f-167">hello[設定檔](#Profile)，[應用程式](#Applications)，和[訂閱](#Subscriptions)範本會共用相同的資料模型，並收到 hello hello 相同的範本資料。</span><span class="sxs-lookup"><span data-stu-id="80e4f-167">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="80e4f-168">屬性</span><span class="sxs-lookup"><span data-stu-id="80e4f-168">Property</span></span>|<span data-ttu-id="80e4f-169">類型</span><span class="sxs-lookup"><span data-stu-id="80e4f-169">Type</span></span>|<span data-ttu-id="80e4f-170">說明</span><span class="sxs-lookup"><span data-stu-id="80e4f-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="80e4f-171">firstName</span><span class="sxs-lookup"><span data-stu-id="80e4f-171">firstName</span></span>|<span data-ttu-id="80e4f-172">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-172">string</span></span>|<span data-ttu-id="80e4f-173">Hello 目前使用者的名字。</span><span class="sxs-lookup"><span data-stu-id="80e4f-173">First name of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-174">lastName</span><span class="sxs-lookup"><span data-stu-id="80e4f-174">lastName</span></span>|<span data-ttu-id="80e4f-175">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-175">string</span></span>|<span data-ttu-id="80e4f-176">Hello 目前使用者的姓氏。</span><span class="sxs-lookup"><span data-stu-id="80e4f-176">Last name of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-177">companyName</span><span class="sxs-lookup"><span data-stu-id="80e4f-177">companyName</span></span>|<span data-ttu-id="80e4f-178">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-178">string</span></span>|<span data-ttu-id="80e4f-179">hello hello 目前使用者的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="80e4f-179">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="80e4f-180">addresserEmail</span></span>|<span data-ttu-id="80e4f-181">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-181">string</span></span>|<span data-ttu-id="80e4f-182">Hello 目前使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="80e4f-182">Email address of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="80e4f-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="80e4f-184">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-184">string</span></span>|<span data-ttu-id="80e4f-185">Hello 目前使用者的相對 URL tooview 分析。</span><span class="sxs-lookup"><span data-stu-id="80e4f-185">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="80e4f-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="80e4f-186">subscriptions</span></span>|<span data-ttu-id="80e4f-187">[訂用帳戶](api-management-template-data-model-reference.md#Subscription)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="80e4f-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="80e4f-188">hello hello 目前使用者的訂閱。</span><span class="sxs-lookup"><span data-stu-id="80e4f-188">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="80e4f-189">應用程式所需</span><span class="sxs-lookup"><span data-stu-id="80e4f-189">applications</span></span>|<span data-ttu-id="80e4f-190">[應用程式](api-management-template-data-model-reference.md#Application)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="80e4f-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="80e4f-191">hello 目前使用者的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="80e4f-191">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="80e4f-192">changePasswordUrl</span></span>|<span data-ttu-id="80e4f-193">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-193">string</span></span>|<span data-ttu-id="80e4f-194">hello 相對 URL toochange hello 目前使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="80e4f-194">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="80e4f-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="80e4f-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="80e4f-196">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-196">string</span></span>|<span data-ttu-id="80e4f-197">hello 相對 URL toochange hello 名稱與 hello 目前使用者的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="80e4f-197">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="80e4f-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="80e4f-198">canChangePassword</span></span>|<span data-ttu-id="80e4f-199">布林值</span><span class="sxs-lookup"><span data-stu-id="80e4f-199">boolean</span></span>|<span data-ttu-id="80e4f-200">是否 hello 目前的使用者可以變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="80e4f-200">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="80e4f-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="80e4f-201">isSystemUser</span></span>|<span data-ttu-id="80e4f-202">布林值</span><span class="sxs-lookup"><span data-stu-id="80e4f-202">boolean</span></span>|<span data-ttu-id="80e4f-203">Hello 目前使用者是否為其中一個 hello 內建成員[群組](api-management-key-concepts.md#groups)。</span><span class="sxs-lookup"><span data-stu-id="80e4f-203">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="80e4f-204">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="80e4f-204">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="80e4f-205"><a name="Applications"></a> 應用程式</span><span class="sxs-lookup"><span data-stu-id="80e4f-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="80e4f-206">hello**應用程式**範本可讓您 toocustomize hello 訂閱 區段中的 hello 開發人員入口網站中的 hello 使用者設定檔頁面。</span><span class="sxs-lookup"><span data-stu-id="80e4f-206">hello **Applications** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="80e4f-207">![使用者帳戶的應用程式頁面](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM 使用者帳戶的應用程式頁面")</span><span class="sxs-lookup"><span data-stu-id="80e4f-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="80e4f-208">預設範本</span><span class="sxs-lookup"><span data-stu-id="80e4f-208">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="80e4f-209">控制</span><span class="sxs-lookup"><span data-stu-id="80e4f-209">Controls</span></span>  
 <span data-ttu-id="80e4f-210">此範本可能會使用 hello 下列[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="80e4f-210">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="80e4f-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="80e4f-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="80e4f-212">資料模型</span><span class="sxs-lookup"><span data-stu-id="80e4f-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="80e4f-213">hello[設定檔](#Profile)，[應用程式](#Applications)，和[訂閱](#Subscriptions)範本會共用相同的資料模型，並收到 hello hello 相同的範本資料。</span><span class="sxs-lookup"><span data-stu-id="80e4f-213">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="80e4f-214">屬性</span><span class="sxs-lookup"><span data-stu-id="80e4f-214">Property</span></span>|<span data-ttu-id="80e4f-215">類型</span><span class="sxs-lookup"><span data-stu-id="80e4f-215">Type</span></span>|<span data-ttu-id="80e4f-216">說明</span><span class="sxs-lookup"><span data-stu-id="80e4f-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="80e4f-217">firstName</span><span class="sxs-lookup"><span data-stu-id="80e4f-217">firstName</span></span>|<span data-ttu-id="80e4f-218">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-218">string</span></span>|<span data-ttu-id="80e4f-219">Hello 目前使用者的名字。</span><span class="sxs-lookup"><span data-stu-id="80e4f-219">First name of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-220">lastName</span><span class="sxs-lookup"><span data-stu-id="80e4f-220">lastName</span></span>|<span data-ttu-id="80e4f-221">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-221">string</span></span>|<span data-ttu-id="80e4f-222">Hello 目前使用者的姓氏。</span><span class="sxs-lookup"><span data-stu-id="80e4f-222">Last name of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-223">companyName</span><span class="sxs-lookup"><span data-stu-id="80e4f-223">companyName</span></span>|<span data-ttu-id="80e4f-224">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-224">string</span></span>|<span data-ttu-id="80e4f-225">hello hello 目前使用者的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="80e4f-225">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="80e4f-226">addresserEmail</span></span>|<span data-ttu-id="80e4f-227">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-227">string</span></span>|<span data-ttu-id="80e4f-228">Hello 目前使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="80e4f-228">Email address of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="80e4f-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="80e4f-230">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-230">string</span></span>|<span data-ttu-id="80e4f-231">Hello 目前使用者的相對 URL tooview 分析。</span><span class="sxs-lookup"><span data-stu-id="80e4f-231">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="80e4f-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="80e4f-232">subscriptions</span></span>|<span data-ttu-id="80e4f-233">[訂用帳戶](api-management-template-data-model-reference.md#Subscription)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="80e4f-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="80e4f-234">hello hello 目前使用者的訂閱。</span><span class="sxs-lookup"><span data-stu-id="80e4f-234">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="80e4f-235">應用程式所需</span><span class="sxs-lookup"><span data-stu-id="80e4f-235">applications</span></span>|<span data-ttu-id="80e4f-236">[應用程式](api-management-template-data-model-reference.md#Application)實體的集合。</span><span class="sxs-lookup"><span data-stu-id="80e4f-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="80e4f-237">hello 目前使用者的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="80e4f-237">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="80e4f-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="80e4f-238">changePasswordUrl</span></span>|<span data-ttu-id="80e4f-239">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-239">string</span></span>|<span data-ttu-id="80e4f-240">hello 相對 URL toochange hello 目前使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="80e4f-240">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="80e4f-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="80e4f-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="80e4f-242">字串</span><span class="sxs-lookup"><span data-stu-id="80e4f-242">string</span></span>|<span data-ttu-id="80e4f-243">hello 相對 URL toochange hello 名稱與 hello 目前使用者的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="80e4f-243">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="80e4f-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="80e4f-244">canChangePassword</span></span>|<span data-ttu-id="80e4f-245">布林值</span><span class="sxs-lookup"><span data-stu-id="80e4f-245">boolean</span></span>|<span data-ttu-id="80e4f-246">是否 hello 目前的使用者可以變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="80e4f-246">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="80e4f-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="80e4f-247">isSystemUser</span></span>|<span data-ttu-id="80e4f-248">布林值</span><span class="sxs-lookup"><span data-stu-id="80e4f-248">boolean</span></span>|<span data-ttu-id="80e4f-249">Hello 目前使用者是否為其中一個 hello 內建成員[群組](api-management-key-concepts.md#groups)。</span><span class="sxs-lookup"><span data-stu-id="80e4f-249">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="80e4f-250">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="80e4f-250">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="80e4f-251"><a name="UpdateAccountInfo"></a> 更新帳戶資訊</span><span class="sxs-lookup"><span data-stu-id="80e4f-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="80e4f-252">hello **Uodate 帳戶資訊**範本可讓您 toocustomize hello**更新帳戶資訊**hello 開發人員入口網站中的頁面。</span><span class="sxs-lookup"><span data-stu-id="80e4f-252">hello **Uodate account info** template allows you toocustomize hello **Update account information** page in hello developer portal.</span></span>  
  
 <span data-ttu-id="80e4f-253">![使用者帳戶資訊頁面開發人員入口網站範本](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM 使用者帳戶資訊頁面開發人員入口網站範本")</span><span class="sxs-lookup"><span data-stu-id="80e4f-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="80e4f-254">預設範本</span><span class="sxs-lookup"><span data-stu-id="80e4f-254">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="80e4f-255">控制</span><span class="sxs-lookup"><span data-stu-id="80e4f-255">Controls</span></span>  
 <span data-ttu-id="80e4f-256">此範本可能不使用任何[頁面控制項](api-management-page-controls.md)。</span><span class="sxs-lookup"><span data-stu-id="80e4f-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="80e4f-257">資料模型</span><span class="sxs-lookup"><span data-stu-id="80e4f-257">Data model</span></span>  
 <span data-ttu-id="80e4f-258">[使用者帳戶資訊](api-management-template-data-model-reference.md#UserAccountInfo)實體。</span><span class="sxs-lookup"><span data-stu-id="80e4f-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="80e4f-259">範例範本資料</span><span class="sxs-lookup"><span data-stu-id="80e4f-259">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="80e4f-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="80e4f-260">Next steps</span></span>
<span data-ttu-id="80e4f-261">如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](api-management-developer-portal-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="80e4f-261">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
