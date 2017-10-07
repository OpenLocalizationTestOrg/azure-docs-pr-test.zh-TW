---
title: "aaaGet 入門 node.js 的 Azure 搜尋 |Microsoft 文件"
description: "逐步了解如何使用 Node.js 作為程式設計語言，在 Azure 的雲端託管搜尋服務上建置搜尋應用程式。"
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>開始在 Node.js 中使用 Azure 搜尋服務
> [!div class="op_single_selector"]
> * [入口網站](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

了解如何自訂 Node.js toobuild 搜尋應用程式，使用 Azure 搜尋的搜尋經驗。 本教學課程使用 hello [Azure 搜尋服務 REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello 物件和作業在此練習中使用。

我們使用[Node.js](https://Nodejs.org)及 NPM，[適文字 3](http://www.sublimetext.com/3)，和 Windows 8.1 toodevelop 上的 Windows PowerShell 並測試這段程式碼。

toorun 此範例中，您必須擁有 Azure 搜尋服務，您可以申請中 hello [Azure 入口網站](https://portal.azure.com)。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)如需逐步指示。

## <a name="about-hello-data"></a>關於 hello 資料
此範例應用程式會使用資料 hello[美國地理服務 (USG)](http://geonames.usgs.gov/domestic/download_data.htm)、 篩選上 hello 羅德島狀態 tooreduce hello 資料集的大小。 我們將使用此資料 toobuild 傳回例如醫院和學校，以及地理功能，例如資料流、 湖泊、 和 summits 地標建築物的搜尋應用程式。

在此應用程式，hello **DataIndexer**建置程式，並載入 hello 索引使用[索引子](https://msdn.microsoft.com/library/azure/dn798918.aspx)建構，擷取 hello 篩選 USG 從公開的 Azure SQL Database 的資料集。 認證和連接資訊 toohello 線上資料來源提供 hello 程式碼中。 不需要進一步設定。

> [!NOTE]
> 我們在 hello 免費定價層的 hello 10000 文件限制此資料集 toostay 套用篩選。 如果您使用 hello 標準層，這項限制不適用。 如需各個定價層的容量詳細資料，請參閱 [搜尋服務限制](search-limits-quotas-capacity.md)。
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>尋找 hello 服務名稱和您的 Azure 搜尋服務的 api 金鑰
建立 hello 服務之後，傳回 toohello 入口 tooget hello URL 或`api-key`。 連線 tooyour 搜尋服務需要您有兩個 hello 的 URL 和`api-key`tooauthenticate hello 呼叫。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 跳躍列中，按一下**搜尋服務**toolist 所有 Azure 搜尋服務佈都建您的訂用帳戶。
3. 選取您想要 toouse hello 服務。
4. Hello 服務儀表板，您應該會看到磚，以便於重要資訊，例如 hello 索引鍵圖示來存取 hello 系統管理金鑰。
5. 將複製 hello 服務 URL、 管理金鑰和查詢索引鍵。 您所有的三個稍後需要時新增 toohello config.js 檔案。

## <a name="download-hello-sample-files"></a>下載檔案的 hello 範例
使用下列方法 toodownload hello 範例 hello 的其中一個。

1. 跳過[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo)。
2. 按一下**Download ZIP**，儲存 hello.zip 檔案，然後將它包含的所有 hello 檔案都解壓縮。

所有後續的檔案修改及執行陳述式都會用到此資料夾中的檔案。

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a>更新 hello config.js。 方法為使用您的搜尋服務 URL 及 API 金鑰
使用 hello URL 和更早版本，您所複製的 api 金鑰指定組態檔中的 hello URL、 管理金鑰，並查詢索引鍵。

系統管理金鑰可將服務作業的完整控制權限授與給您，包括建立或刪除索引，以及載入文件。 相較之下，查詢索引鍵是唯讀作業，通常是供連接 tooAzure 搜尋的用戶端應用程式。

在此範例中，我們可以包括 hello 查詢索引鍵 toohelp 強化 hello 最佳作法是在用戶端應用程式中使用 hello 查詢索引鍵。

下列螢幕擷取畫面顯示 hello **config.js**開啟文字編輯器中，以 hello demarcated，讓您可以查看其中 tooupdate hello 檔案以 hello 值相關的項目都適用於您的搜尋服務。

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a>裝載執行階段環境的 hello 範例
hello 範例需要 HTTP 伺服器，您可以安裝全域使用 npm。

Hello，下列命令使用的 PowerShell 視窗。

1. 瀏覽包含 hello toohello 資料夾**package.json**檔案。
2. 輸入 `npm install`。
3. 輸入 `npm install -g http-server`。

## <a name="build-hello-index-and-run-hello-application"></a>建立 hello 索引並執行 hello 應用程式
1. 輸入 `npm run indexDocuments`。
2. 輸入 `npm run build`。
3. 輸入 `npm run start_server`。
4. 將您的瀏覽器導向至 `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>搜尋 USGS 資料
hello USG 資料集包含相關 toohello 狀態的羅德島的記錄。 如果您按一下**搜尋**上是空的搜尋 方塊中，您取得 hello 排行前 50 名項目，hello 預設值。

輸入的搜尋詞彙提供 hello 搜尋引擎一些 toogo 上。 試著輸入區域名稱。 「 Roger Williams 」 已羅德島 hello 第一個管理員。 許多公園、建築物和學校都是以他的姓名命名。

![][9]

此外，您也可以試著使用這些字詞：

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>後續步驟
這是根據 Node.js 和 hello USG 資料集 hello 第一個 Azure 搜尋教學課程。 經過一段時間，我們將會延長此教學課程 toodemonstrate 您可能會想 toouse 自訂方案中的其他搜尋功能。

如果您已有一些 Azure 搜尋服務的背景知識，可以利用此範例做為試用建議工具 (預先輸入或自動完成查詢)、篩選及多面向導覽的跳板。 您也可以藉由加入計數和批次的文件，以便使用者可以透過 hello 結果頁改善 hello 搜尋結果頁面時。

新 tooAzure 搜尋嗎？ 我們建議您嘗試其他教學課程 toodevelop 了解您可以建立。 請瀏覽我們[文件頁面](https://azure.microsoft.com/documentation/services/search/)toofind 更多資源。 您也可以檢視中的 hello 連結我們[影片和教學課程清單](search-video-demo-tutorial-list.md)tooaccess 的詳細資訊。

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
