---
title: "aaaModify 頁面內容的 hello 開發人員入口網站在 Azure API 管理 |Microsoft 文件"
description: "了解 tooedit 頁面在 Azure API 管理中的 hello 開發人員入口網站上的內容。"
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
ms.openlocfilehash: fd5a854e900d9512518643e593b1b59a0952621f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-content-and-layout-of-pages-on-hello-developer-portal-in-azure-api-management"></a>修改 hello 內容和在 Azure API 管理中的 hello 開發人員入口網站上的頁面配置
在 Azure API 管理有三種基本方式 toocustomize hello 開發人員入口網站：

* [編輯 hello 內容的靜態網頁和頁面配置項目][ modify-content-layout] （在本指南說明）
* [更新用於跨 hello 開發人員入口網站的頁面元素的 hello 樣式][customize-styles]
* [修改用於頁面 hello 入口網站所產生的 hello 範本][ portal-templates] （例如應用程式開發介面文件、 產品、 使用者驗證等）

## <a name="page-structure"> </a>開發人員入口網站頁面的結構

hello 開發人員入口網站為基礎的內容管理系統。 hello 版面配置的每一頁會根據一組稱為 widget 的小型的頁面元素建置：

![開發人員入口網站頁面結構][api-management-customization-widget-structure]

所有 Widget 都是可編輯的。 
* hello 核心內容特定 tooeach 個別頁面位於 hello 「 內容 」 widget。 編輯頁面表示編輯 hello 這個小工具內容。
* 所有的頁面配置項目會包含與 hello 剩餘的 widget。 Toothese widget 所做的變更會套用 tooall 頁面。 它們會參考的 tooas"配置 widget"。

在日常頁面編輯一個通常只會修改 hello 內容 widget 會有不同的內容，各頁面的。

## <a name="modify-layout-widget"></a>修改配置 widget 的 hello 內容

Hello 開發人員入口網站中的內容有修改透過 hello 發行者入口網站可從 hello Azure 入口網站存取。 tooreach，按一下 **發行者入口網站**從 API 管理執行個體的 hello 服務工具列。

![發行者入口網站][api-management-management-console]

tooedit hello 內容的 widget 中，按一下**Widget**從 hello**開發人員入口網站**hello 左邊功能表上的。 針對此範例可讓您修改 hello 標頭 widget hello 內容。 選取 hello**標頭**hello 清單中的 widget。

![Widgets header][api-management-widgets-header]

hello hello 標頭內容時，才能從 hello 內編輯**主體**欄位。 變更為所需的 hello 文字，然後按一下**儲存**hello hello 頁底端。

您現在應該能夠 toosee hello 新標頭 hello 開發人員入口網站內的每一頁上。

> tooopen hello 開發人員入口網站，在 hello 發行者入口網站中，按一下**開發人員入口網站**在 hello 頂端列中。
> 
> 

## <a name="edit-page-contents"></a>編輯 hello 頁面內容

toosee hello 清單中的所有現有的內容頁面，按一下**內容**從 hello**開發人員入口網站**hello 發行者入口網站中的功能表。

![Manage content][api-management-customization-manage-content]

按一下 hello ** 褖畫惎**頁面 tooedit 在 hello 的 hello 開發人員入口網站的首頁上顯示的內容。 變更 hello 想，必要時，預覽，然後按一下**立即發行**toomake 它們可見 tooeveryone。

> hello 首頁上會使用特殊的版面配置，好讓它在 hello 最上方的橫幅 toodisplay。 此橫幅，則無法編輯從 hello**內容**> 一節。 tooedit 此橫幅，按一下**Widget**從 hello**開發人員入口網站**功能表上，選取**首頁**從 hello**目前的圖層**下拉式清單清單，然後再開啟 hello**橫幅**hello 下的項目**功能 > 一節**。 此 widget hello 內容是可編輯，就像任何其他網頁。
> 
> 

## <a name="next-steps"> </a>後續步驟
* [更新用於跨 hello 開發人員入口網站的頁面元素的 hello 樣式][customize-styles]
* [修改用於頁面 hello 入口網站所產生的 hello 範本][ portal-templates] （例如應用程式開發介面文件、 產品、 使用者驗證等）

[Structure of developer portal pages]: #page-structure
[Modifying hello contents of a layout widget]: #modify-layout-widget
[Edit hello contents of a page]: #edit-page-contents
[Next steps]: #next-steps

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customization-widget-structure]: ./media/api-management-modify-content-layout/portal-widget-structure.png
[api-management-management-console]: ./media/api-management-modify-content-layout/api-management-management-console.png
[api-management-widgets-header]: ./media/api-management-modify-content-layout/api-management-widgets-header.png
[api-management-customization-manage-content]: ./media/api-management-modify-content-layout/api-management-customization-manage-content.png
