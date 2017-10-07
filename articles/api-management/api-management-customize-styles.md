---
title: "在 Azure API 管理中的 hello 開發人員入口網站中的 aaaCustomize 樣式 |Microsoft 文件"
description: "了解 toomodify hello 樣式 hello 開發人員入口網站在 Azure API 管理中任何頁面使用的方式。"
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: aaaa86527992ba43e64eab5fd35c7f57b573c812
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-styling-of-hello-developer-portal-in-azure-api-management"></a>自訂 hello 開發人員入口網站在 Azure API 管理中的 hello 的樣式
在 Azure API 管理有三種基本方式 toocustomize hello 開發人員入口網站：

* [編輯 hello 內容的靜態網頁和頁面配置項目][modify-content-layout]
* [更新用於跨 hello 開發人員入口網站的頁面元素的 hello 樣式][ customize-styles] （在本指南說明）
* [修改用於頁面 hello 入口網站所產生的 hello 範本][ portal-templates] （例如應用程式開發介面文件、 產品、 使用者驗證等）

## <a name="change-headers-styling"></a>變更 hello 的頁面元素的樣式

hello 色彩、 字型、 大小、 間距及任何網頁 hello 入口網站上的其他樣式相關項目是由定義樣式規則。 

編輯 hello 樣式規則由 hello**開發人員入口網站**時以系統管理員身分登入。 那里 tooget 先開啟 hello Azure 入口網站，然後按一下 **發行者入口網站**從 API 管理執行個體的 hello 服務工具列。

![發行者入口網站][api-management-management-console]

然後按一下 **開發人員入口網站**上 hello 右上方。 

![Hello 發行者入口網站上的開發人員入口網站連結][api-management-pp-dp-link]

tooopen hello 自訂工具列將滑鼠移 hello 自訂圖示 （或選取它），然後按一下 「 樣式 」 從 hello 工具列。

![自訂工具列][api-management-customization-toolbar-button]

有兩個主要的方式編輯樣式規則-您可以查看的任何地方使用的所有 hello 樣式規則的 hello 清單會依預設會顯示和修改樣式，如有需要或者您可以選擇**選取 hello 頁面上的項目**然後按一下 hello 頁面 toosee 唯一 hello 的樣式項目上的任何位置。

![Customization toolbar][api-management-customization-toolbar]

按一下 hello**選取 hello 頁面上的項目**此範例中的選項。  項目現在會反白顯示您將滑鼠停留在它們與 hello 滑鼠 toosignify 開始編輯您已按下的哪些項目樣式。 移動 hello 滑鼠移過 hello 文字中 （通常您會有 hello 公司名稱這裡） hello 標頭，然後按一下它。 一組具名和分類的樣式規則會出現在 hello 樣式編輯器。 每個規則表示 hello 選元素的樣式屬性。 例如，對於 hello 上方所選的標頭文字，hello hello 文字大小位於@font-size-h1hello 字型名稱的 hello 與替代方案時@headings-font-family。

> 如果您已熟悉[啟動程序][bootstrap]，這些規則，實際上是[LESS 變數，] [ LESS variables]內 hello hello 所使用的啟動程序主題開發人員入口網站。
> 
> 

我們來變更 hello hello 標題文字色彩。 選取 hello 項目在 hello  **@headings-color** 欄位，然後輸入**#000000**。 這是 hello 黑色 hello 色彩的十六進位碼。 當您這麼做，您可以看到色彩正方形指標會出現在 hello 文字方塊中的 hello 結尾。 如果您按一下此指標時，色彩選擇器可讓您 toochoose 色彩。

![Color picker][api-management-customization-toolbar-color-picker]

當您進行，但會顯示只有 tooadministrators，變更會即時預覽。 toomake 這些變更看 tooeveryone 中，按一下 hello**發行**按鈕 hello 樣式編輯器中，並確認 hello 的變更。

![Publish menu][api-management-customization-toolbar-publish-form]

> toochange hello 樣式規則，套用 tooany 其他項目在 hello 頁面上，遵循 hello 相同的 hello 標頭所為您的程序。 按一下**選取 hello 頁面上的項目**從 hello 樣式編輯器、 選取 hello 您感興趣的項目和修改 hello 螢幕上顯示 hello 樣式規則的 hello 值開始。
> 
> 


## <a name="next-steps"> </a>後續步驟
* 了解 toocustomize hello 內容的開發人員入口網站頁面使用的方式[開發人員入口網站範本](api-management-developer-portal-templates.md)。

[Change hello styling of hello headers]: #change-headers-styling
[Next steps]: #next-steps

[Azure Classic Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./media/api-management-customize-styles/api-management-management-console.png
[api-management-pp-dp-link]: ./media/api-management-customize-styles/api-management-pp-dp-link.png
[api-management-customization-toolbar-button]: ./media/api-management-customize-styles/api-management-customization-toolbar-button.png
[api-management-customization-toolbar]: ./media/api-management-customize-styles/api-management-customization-toolbar.png
[api-management-customization-toolbar-color-picker]: ./media/api-management-customize-styles/api-management-customization-toolbar-color-picker.png
[api-management-customization-toolbar-publish-form]: ./media/api-management-customize-styles/api-management-customization-toolbar-publish-form.png

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[bootstrap]: http://getbootstrap.com/
[LESS variables]: http://getbootstrap.com/css/
