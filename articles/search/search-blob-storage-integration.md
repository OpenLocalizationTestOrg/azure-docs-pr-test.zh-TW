---
title: "aaaAdding Azure 搜尋 tooBlob 儲存體 |Microsoft 文件"
description: "使用 hello Azure 搜尋 HTTP 的 REST API 的程式碼中建立索引。"
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: a3801790067bf169693b500e83799286b7387a77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="searching-blob-storage-with-azure-search"></a>使用 Azure 搜尋服務搜尋 Blob 儲存體

搜尋在各種 hello Azure Blob 儲存體中的內容類型可能很困難的問題 toosolve。 不過，您可以建立索引，並搜尋 hello 使用 Azure 搜尋中按幾下滑鼠 Blob 的內容。 在 Blob 儲存體上搜尋需要佈建 Azure 搜尋服務。 hello 各種服務限制，以及可以找到上 hello 的定價層的 Azure 搜尋[定價頁面](https://aka.ms/azspricing)。

## <a name="what-is-azure-search"></a>何謂 Azure 搜尋服務？
[Azure 搜尋](https://aka.ms/whatisazsearch)是一種搜尋解決方案，能輕鬆針對開發人員 tooadd 強固的全文檢索搜尋體驗 tooweb 和行動應用程式。 為服務，Azure 搜尋會移除 hello 需要 toomanage 供應項目時的任何搜尋基礎結構[99.9%正常運作 SLA](https://aka.ms/azuresearchsla)。

透過 56 種語言的進階支援，Azure 搜尋服務可以分析您的內容，並以智慧方式處理特定語言結構建構。 Azure 搜尋也提供 hello 工具 toobuild 豐富的搜尋使用者經驗。 它是簡單 tooadd 功能，例如多面向導覽、 typeahead 搜尋建議和使用 Azure Search 點擊反白顯示 toouser 介面。 toolearn 有關 Azure 搜尋功能，您可以閱讀 hello 服務[文件](https://aka.ms/azsearchdocs)。

## <a name="crack-open-and-search-through-hello-content-of-enterprise-document-formats"></a>萃取開啟和企業文件格式的 hello 內容進行搜尋
支援[文件擷取](https://aka.ms/azsblobindexer)Azure Blob 儲存體，Azure 搜尋可以建立索引的各種檔案類型儲存在 blob 中的 hello 內容：
- PDF
- Microsoft Office：DOCX/DOC、XLSX/XLS、PPTX/PPT、MSG (Outlook 電子郵件)
- HTML
- 純文字檔案

藉由擷取文字和這些檔案類型的中繼資料，很容易 toosearch 跨多個檔案格式具有單一查詢 toofind hello 最相關的文件不論類型為何。 所編製索引的 Microsoft Office 文件、 Pdf、 和電子郵件、 其可能 toobuild hello 內容和 hello 中繼資料使用 Blob 儲存體和 Azure 搜尋的強大的企業內容管理解決方案。

## <a name="search-through-your-blob-metadata"></a>搜尋您的 Blob 中繼資料
常見的案例，可透過任何內容類型的 blob 輕鬆 toosort 是 tooindex hello 自訂的使用者定義的 blob 中繼資料，以及 hello 系統內容每個 blob。 如此一來，每個 blob 資訊編製索引不論 hello 的文件以 hello blob，因此您可以輕鬆地排序和 facet 的型別所有的 Blob 儲存體內容。

[深入了解如何編製 Blob 中繼資料的索引。](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a>影像搜尋
Azure 搜尋的全文檢索搜尋、 多面向導覽和排序功能現在可以儲存在 blob 中的映像套用的 toohello 中繼資料。

如果這些映像預先處理使用 hello[電腦願景 API](https://www.microsoft.com/cognitive-services/computer-vision-api)從 Microsoft 的認知的服務，則在每個映像，包括 OCR 及手寫辨識中找到可能 tooindex hello 視覺內容。 我們努力加入 OCR 和其他映像處理功能直接 tooAzure 搜尋中，如果您有興趣使用這些功能請提交要求上我們[UserVoice](https://aka.ms/azsuv)或[電子郵件給我們](mailto:azscustquestions@microsoft.com)。

## <a name="index-and-search-through-json-blobs"></a>檢索和搜尋 JSON Blob
Azure 搜尋可以是在包含 JSON 的 blob 中找到設定的 tooextract 結構化內容。 Azure 搜尋可以讀取 JSON blob 及 hello 結構化內容剖析成 hello Azure 搜尋文件的適當的欄位。 Azure 搜尋也可以包含 JSON 物件的陣列，並對應每個項目 tooa 個別 Azure 搜尋文件的 blob。

請注意，JSON 剖析並非目前可透過 hello 入口網站設定。 [深入了解 Azure 搜尋服務中的 JSON 剖析。](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a>快速入門
Azure 搜尋可以直接從 hello Blob 儲存體入口網站 刀鋒視窗 tooblobs 新增。

![](./media/search-blob-storage-integration/blob-blade.png)

按一下 hello 「 新增 Azure 搜尋 」 選項會啟動的流程，您可以在其中選取現有的 Azure 搜尋服務或建立新的服務。 如果您建立新的服務，您將會跳脫儲存體帳戶的入口網站經驗。 您將需要 toore-瀏覽 toohello 存放裝置的入口網站 刀鋒視窗，並重新選取 hello 「 新增 Azure 搜尋 」 選項，您可以在其中選取 hello 現有的服務。

### <a name="next-steps"></a>後續步驟
深入了解 hello Azure 搜尋 Blob 索引子中完整 hello[文件](https://aka.ms/azsblobindexer)。
