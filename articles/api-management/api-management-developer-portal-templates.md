---
title: "aaaCustomize hello API 管理開發人員入口網站使用範本-Azure |Microsoft 文件"
description: "了解如何 toocustomize hello Azure API 管理開發人員入口網站使用範本。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: a195675b-f7d0-4fc9-90bf-860e6f17ccf7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: b00d5f1534e9466f30ff3920e7aae048feb8b8c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-hello-azure-api-management-developer-portal-using-templates"></a>如何 toocustomize hello Azure API 管理開發人員入口網站使用範本

在 Azure API 管理有三種基本方式 toocustomize hello 開發人員入口網站：

* [編輯 hello 內容的靜態網頁和頁面配置項目][modify-content-layout]
* [更新用於跨 hello 開發人員入口網站的頁面元素的 hello 樣式][customize-styles]
* [修改用於頁面 hello 入口網站所產生的 hello 範本][ portal-templates] （在本指南說明）

範本是使用的 toocustomize hello 系統產生的開發人員入口網站頁面 （例如應用程式開發介面文件、 產品、 使用者驗證等） 的內容。 使用[DotLiquid](http://dotliquidmarkup.org/)語法，與提供的一系列的當地語系化的字串資源、 圖示和頁面控制項適當地，您會有很大的彈性 tooconfigure hello 網頁內容的 hello。

## <a name="developer-portal-templates-overview"></a>開發人員入口網站範本概觀
編輯範本由 hello**開發人員入口網站**時以系統管理員身分登入。 那里 tooget 先開啟 hello Azure 入口網站，然後按一下 **發行者入口網站**從 API 管理執行個體的 hello 服務工具列。

![發行者入口網站][api-management-management-console]

然後按一下 **開發人員入口網站**上 hello 右上方。 

![開發人員入口網站功能表][api-management-developer-portal-menu]

tooaccess hello 開發人員入口網站範本中，按一下 hello 自訂 hello 左的 toodisplay hello 自訂功能表上的圖示，然後按一下**範本**。

![開發人員入口網站範本][api-management-customize-menu]

hello 範本清單會顯示數種類別涵蓋 hello hello 開發人員入口網站中的不同頁面的範本。 每個範本都不同，但 hello 步驟 tooedit 它們和發行 hello 變更 hello 相同。 tooedit 範本，請按一下 hello hello 範本名稱。

![開發人員入口網站範本][api-management-templates-menu]

按一下範本會引導您 toohello 開發人員入口網站頁面是由該範本所自訂的。 在此範例 hello**產品清單**範本會顯示。 hello**產品清單**範本控制項哈囉 」 畫面 hello 紅色矩形所指定的區域。 

![產品清單範本][api-management-developer-portal-templates-overview]

某些範本，例如 hello**使用者設定檔**範本自訂 hello 的不同部分相同的頁面。 

![使用者設定檔範本][api-management-user-profile-templates]

對於每個開發人員入口網站範本的 hello 編輯器具有兩個區段顯示在 hello hello 頁面底部。 hello 左側顯示 hello 編輯 hello 範本 窗格並 hello 右側顯示 hello hello 範本資料模型。 

hello 樣板編輯 窗格包含可控制 hello 外觀和行為 hello hello 開發人員入口網站中的對應頁面 hello 標記。 hello 範本中的 hello 標記使用 hello [DotLiquid](http://dotliquidmarkup.org/)語法。 常用的 DotLiquid 編輯器是 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers)。 在編輯期間的任何所做的變更 toohello 範本會顯示在即時 hello 瀏覽器，但是不可見的 tooyour 客戶直到您[儲存](#to-save-a-template)和[發行](#to-publish-a-template)hello 範本。

![範本標記][api-management-template]

hello**範本資料**窗格提供的指引 toohello 資料可供使用特定範本中的 hello 實體模型。 它可提供本指南顯示 hello hello 開發人員入口網站中目前顯示的即時資料。 您可以展開 hello 樣板窗格，依序按一下 hello hello 右上角的矩形中 hello**範本資料**窗格。

![範本資料模型][api-management-template-data]

Hello 前一個範例中有兩個產品顯示 hello 開發人員入口網站中，擷取自 hello 資料顯示在 hello**範本資料**窗格 hello 下列範例所示。

```json
{
    "Paging": {
        "Page": 1,
        "PageSize": 10,
        "TotalItemCount": 2,
        "ShowAll": false,
        "PageCount": 1
    },
    "Filtering": {
        "Pattern": null,
        "Placeholder": "Search products"
    },
    "Products": [
        {
            "Id": "56ec64c380ed850042060001",
            "Title": "Starter",
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",
            "Terms": "",
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        },
        {
            "Id": "56ec64c380ed850042060002",
            "Title": "Unlimited",
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",
            "Terms": null,
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        }
    ]
}
```

hello 中的 hello 標記**產品清單**範本處理程序透過 hello 集合產品 toodisplay 資訊和連結 tooeach 個別產品的反覆 hello 資料 tooprovide hello 預期輸出。 請注意 hello`<search-control>`和`<page-control>`hello 標記中的項目。 這些控制 hello 顯示 hello 搜尋及分頁處理 hello 頁面上的控制項。 `ProductsStrings|PageTitleProducts`是包含 hello 的當地語系化的字串參考`h2`hello 頁面的標頭文字。 如需字串資源、頁面控制項和開發人員入口網站範本可用圖示的清單，請參閱 [API 管理開發人員入口網站範本參考](api-management-developer-portal-templates-reference.md)。

```html
<search-control></search-control>
<div class="row">
    <div class="col-md-9">
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>
    </div>
</div>
<div class="row">
    <div class="col-md-12">
    {% if products.size > 0 %}
    <ul class="list-unstyled">
    {% for product in products %}
        <li>
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>
            {{product.description}}
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

## <a name="toosave-a-template"></a>toosave 範本
toosave 範本，請按一下 儲存在 hello 範本編輯器。

![儲存範本][api-management-save-template]

在發行後才 hello 開發人員入口網站中儲存的變更。

## <a name="toopublish-a-template"></a>toopublish 範本
儲存的範本可以個別或一起發佈。 toopublish 個別範本中，按一下 發佈 hello 範本編輯器中。

![發佈範本][api-management-publish-template]

按一下**是**tooconfirm 並進行即時 hello 開發人員入口網站上的 hello 範本。

![確認發佈][api-management-publish-template-confirm]

toopublish 所有目前已取消發佈的範本版本中，按一下**發行**hello 範本清單中。 星號 hello 範本名稱後面指定了未發行的範本。 在此範例中，hello**產品清單**和**產品**正發佈的範本。

![發佈範本][api-management-publish-templates]

按一下**發行自訂**tooconfirm。

![確認發佈][api-management-publish-customizations]

新發行的範本是立即在 hello 開發人員入口網站中有效。

## <a name="toorevert-a-template-toohello-previous-version"></a>toorevert 範本 toohello 先前的版本
toorevert 範本 toohello 先前已發佈的版本中，按一下 還原 hello 範本編輯器中。

![還原範本][api-management-revert-template]

按一下**是**tooconfirm。

![確認][api-management-revert-template-confirm]

hello 先前已發行的版的範本位於 hello 開發人員入口網站，一旦 hello 還原作業已完成。

## <a name="toorestore-a-template-toohello-default-version"></a>toorestore 範本 toohello 預設版本
還原範本 tootheir 預設版本為兩步驟程序。 必須還原第一個 hello 範本，並還原 hello 版本必須先發行。

toorestore 單一範本 toohello 預設版本中，按一下 還原 hello 範本編輯器中。

![還原範本][api-management-reset-template]

按一下**是**tooconfirm。

![確認][api-management-reset-template-confirm]

所有的範本 tootheir 預設版本，按一下 toorestore**還原預設範本**hello 範本清單上。

![還原範本][api-management-restore-templates]

hello 還原的範本必須再個別或全部由發行中的 hello 步驟[toopublish 範本](#to-publish-a-template)。

## <a name="next-steps"></a>後續步驟
如需開發人員入口網站範本、字串資源、圖示和頁面控制項的參考資訊，請參閱 [API 管理開發人員入口網站範本參考](api-management-developer-portal-templates-reference.md)。

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customize-menu]: ./media/api-management-developer-portal-templates/api-management-customize-menu.png
[api-management-templates-menu]: ./media/api-management-developer-portal-templates/api-management-templates-menu.png
[api-management-developer-portal-templates-overview]: ./media/api-management-developer-portal-templates/api-management-developer-portal-templates-overview.png
[api-management-template]: ./media/api-management-developer-portal-templates/api-management-template.png
[api-management-template-data]: ./media/api-management-developer-portal-templates/api-management-template-data.png
[api-management-developer-portal-menu]: ./media/api-management-developer-portal-templates/api-management-developer-portal-menu.png
[api-management-management-console]: ./media/api-management-developer-portal-templates/api-management-management-console.png
[api-management-browse]: ./media/api-management-developer-portal-templates/api-management-browse.png
[api-management-user-profile-templates]: ./media/api-management-developer-portal-templates/api-management-user-profile-templates.png
[api-management-save-template]: ./media/api-management-developer-portal-templates/api-management-save-template.png
[api-management-publish-template]: ./media/api-management-developer-portal-templates/api-management-publish-template.png
[api-management-publish-template-confirm]: ./media/api-management-developer-portal-templates/api-management-publish-template-confirm.png
[api-management-publish-templates]: ./media/api-management-developer-portal-templates/api-management-publish-templates.png
[api-management-publish-customizations]: ./media/api-management-developer-portal-templates/api-management-publish-customizations.png
[api-management-revert-template]: ./media/api-management-developer-portal-templates/api-management-revert-template.png
[api-management-revert-template-confirm]: ./media/api-management-developer-portal-templates/api-management-revert-template-confirm.png
[api-management-reset-template]: ./media/api-management-developer-portal-templates/api-management-reset-template.png
[api-management-reset-template-confirm]: ./media/api-management-developer-portal-templates/api-management-reset-template-confirm.png
[api-management-restore-templates]: ./media/api-management-developer-portal-templates/api-management-restore-templates.png







