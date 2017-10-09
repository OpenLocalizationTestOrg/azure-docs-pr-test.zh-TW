---
title: "使用 Azure 搜尋在 Java 中啟動 aaaGet |Microsoft 文件"
description: "如何 toobuild 託管雲端搜尋上為您的程式語言中使用 Java 的 Azure 應用程式。"
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a>開始在 Java 中使用 Azure 搜尋服務
> [!div class="op_single_selector"]
> * [入口網站](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

了解如何自訂 Java toobuild 搜尋應用程式，使用 Azure 搜尋的搜尋經驗。 本教學課程使用 hello [Azure 搜尋服務 REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello 物件和作業在此練習中使用。

toorun 此範例中，您必須擁有 Azure 搜尋服務，您可以申請中 hello [Azure 入口網站](https://portal.azure.com)。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)如需逐步指示。

我們使用下列軟體 toobuild hello，並測試這個範例：

* [Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar)。 是確定 toodownload hello EE 版本。 其中一個 hello 驗證步驟需要只在這個版本中找到的功能。
* [JDK 8u40。](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Apache Tomcat 8.0。](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a>關於 hello 資料
此範例應用程式會使用資料 hello[美國地理服務 (USG)](http://geonames.usgs.gov/domestic/download_data.htm)、 篩選上 hello 羅德島狀態 tooreduce hello 資料集的大小。 我們將使用此資料 toobuild 傳回例如醫院和學校，以及地理功能，例如資料流、 湖泊、 和 summits 地標建築物的搜尋應用程式。

在此應用程式，hello **SearchServlet.java**建置程式，並載入 hello 索引使用[索引子](https://msdn.microsoft.com/library/azure/dn798918.aspx)建構，擷取 hello 篩選 USG 從公開的 Azure SQL Database 的資料集。 Hello 程式碼中提供預先定義的認證和連接資訊 toohello 線上資料來源。 關於資料存取，不需要進一步設定。

> [!NOTE]
> 我們在 hello 免費定價層的 hello 10000 文件限制此資料集 toostay 套用篩選。 如果您使用 hello 標準層，不會套用此限制，以及您可以修改這個程式碼 toouse 更大的資料集。 如需各個定價層的容量詳細資料，請參閱 [限制和條件約束](search-limits-quotas-capacity.md)。
> 
> 

## <a name="about-hello-program-files"></a>關於 hello 程式檔案
hello 下列清單說明相關 toothis 範例的 hello 檔案。

* Search.jsp： 提供 hello 使用者介面
* SearchServlet.java： 提供的方法 （類似 tooa 控制站在 MVC 中）
* SearchServiceClient.java：處理 HTTP 要求
* SearchServiceHelper.java：提供靜態方法的協助程式類別
* Document.java： 提供 hello 資料模型
* config.properties： 設定 hello 搜尋服務 URL 和 api 金鑰
* Pom.xml：Maven 相依性

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>尋找 hello 服務名稱和您的 Azure 搜尋服務的 api 金鑰
所有對 Azure 搜尋 REST API 呼叫會要求您提供 hello 服務 URL 和 api 金鑰。 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 跳躍列中，按一下**搜尋服務**toolist hello Azure 搜尋服務的所有訂用帳戶佈建。
3. 選取您想要 toouse hello 服務。
4. Hello 服務儀表板上，您會看到磚，以便於基本資訊以及 hello 索引鍵圖示來存取 hello 系統管理金鑰。
   
      ![][3]
5. 複製 hello 服務 URL 和管理金鑰。 您需要這些更新版本中，當新增 toohello **config.properties**檔案。

## <a name="download-hello-sample-files"></a>下載檔案的 hello 範例
1. 跳過[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) GitHub 上。
2. 按一下**Download ZIP**儲存 hello.zip 檔案 toodisk，，然後將它包含的所有 hello 檔案都解壓縮。 請考慮擷取 hello 檔案至您的 Java 工作區 toomake 它更容易 toofind hello 專案更新版本。
3. hello 範例檔案是唯讀的。 以滑鼠右鍵按一下資料夾內容和清除 hello 唯讀屬性。

所有後續的檔案修改及執行陳述式都會用到此資料夾中的檔案。  

## <a name="import-project"></a>匯入專案
1. 在 Eclipse 中，選擇 [檔案] > [匯入] > [一般] > [將現有專案匯入工作區]。
   
    ![][4]
2. 在**選取根目錄**，瀏覽 toohello 包含範例檔案的資料夾。 選取包含 hello.project 資料夾 hello 資料夾。 hello 專案應該會出現在 hello**專案**為選定項目清單。
   
    ![][12]
3. 按一下 [完成] 。
4. 使用**Project Explorer** tooview 和編輯 hello 檔案。 如果它尚未開啟，請按一下**視窗** > **顯示檢視** > **Project Explorer**或使用 hello 捷徑 tooopen 它。

## <a name="configure-hello-service-url-and-api-key"></a>設定 hello 服務 URL 和 api 金鑰
1. 在**Project Explorer**，連按兩下**config.properties** tooedit hello 組態設定包含 hello 伺服器名稱和 api 金鑰。
2. Toohello 稍早在本文中，其中 hello 中找到 hello 服務 URL 和 api 金鑰中的步驟，請參閱[Azure 入口網站](https://portal.azure.com)，現在您將在輸入 tooget hello 值**config.properties**。
3. 在**config.properties**，「 Api 金鑰 」 取代為您的服務的 hello api 金鑰。 接下來，服務名稱 （使用的 hello URL http://servicename.search.windows.net hello 第一個元件） 會取代 「 服務名稱 」 hello 中相同的檔案。
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a>設定專案，建置和執行階段環境的 hello
1. 在 Eclipse 中，在 [專案總管] 中，以滑鼠右鍵按一下 hello 專案 >**屬性** > **專案 Facet**。
2. 選取 [Dynamic Web Module (動態網路模組)]、[Java] 及 [JavaScript]。
   
    ![][6]
3. 按一下 [套用] 。
4. 選取 [視窗] > [喜好設定] > [伺服器] > [執行階段環境] > [新增..]。
5. 展開 Apache 並選取您先前安裝的 hello Apache Tomcat 伺服器 hello 版本。 我們的系統安裝了第 8 版。
   
    ![][7]
6. 在 hello 下一個頁面上，指定 hello Tomcat 安裝目錄。 在 Windows 電腦中，這通常為 C:\Program Files\Apache Software Foundation\Tomcat *版本*。
7. 按一下 [完成] 。
8. 選取 [視窗] > [喜好設定] > [Java] > [已安裝的 JRE] > [新增]。
9. 在 [Add JRE (新增 JRE)] 中，選取 [Standard VM (標準 VM)]。
10. 按一下 [下一步] 。
11. 在 [JRE Definition (JRE 定義)] 的 [JRE home (JRE 主資料夾)] 中按一下 [Directory (目錄)] 。
12. 瀏覽過**Program Files** > **Java**並選取您先前安裝的 JDK hello。 它是 hello JRE 重要 tooselect hello JDK。
13. 在安裝 JREs，選擇 hello **JDK**。 您的設定應該看起來類似 toohello 下列螢幕擷取畫面。
    
    ![][9]
14. （選擇性） 選取**視窗** > **網頁瀏覽器** > **Internet Explorer** tooopen hello 應用程式，在外部瀏覽器視窗中的。 使用外部瀏覽器可給您更好的 Web 應用程式體驗。
    
    ![][8]

您現在已完成 hello 組態工作。 接下來，您會建置並執行 hello 專案。

## <a name="build-hello-project"></a>建置 hello 專案
1. 在 專案總管 hello 專案名稱上按一下滑鼠右鍵，然後選擇 **執行身分** > **Maven 建置...** tooconfigure hello 專案。
   
    ![][10]
2. 在 Edit Configuration (編輯組態) 的 Goals (目標) 中輸入 "clean install"，然後按一下Run (執行) 。

狀態訊息會輸出 toohello 主控台視窗。 您應該會看到建置成功指示 hello 建立專案時不會發生錯誤。

## <a name="run-hello-app"></a>執行 hello 應用程式
在最後一個步驟中，您將在本機伺服器執行階段環境中執行 hello 應用程式。

如果尚未您尚未在 Eclipse 中指定的伺服器執行階段環境，您將先需要 toodo。

1. 在 Project Explorer 中，展開 [WebContent] 。
2. 以滑鼠右鍵依序按一下 [Search.jsp] > [執行身分] > [在伺服器上執行]。 選取 hello Apache Tomcat 伺服器，然後按一下**執行**。

> [!TIP]
> 如果您使用非預設工作區 toostore 您的專案，您將需要 toomodify**執行設定**toopoint toohello 專案位置 tooavoid 伺服器啟動時的錯誤。 在 [專案總管] 中，以滑鼠右鍵依序按一下 [Search.jsp] > [執行身分] > [執行組態]。 選取 hello Apache Tomcat 伺服器。 按一下 [Arguments (引數)] 。 按一下**工作區**或**檔案系統**包含 hello 專案 tooset hello 資料夾。
> 
> 

當您執行 hello 應用程式時，您應該會看到瀏覽器視窗中，輸入條款提供搜尋方塊。

等候約 1 分鐘後，再按一下**搜尋**toogive hello 服務時間 toocreate 和負載 hello 索引。 如果您收到 HTTP 404 錯誤，您只需要 toowait 稍微較長的時間後再重試。

## <a name="search-on-usgs-data"></a>搜尋 USGS 資料
hello USG 資料集包含相關 toohello 狀態的羅德島的記錄。 如果您按一下**搜尋**上是空的搜尋 方塊中，您會取得 hello 排行前 50 名項目，hello 預設值。

輸入的搜尋詞彙，將 hello 搜尋引擎一些 toogo 上。 試著輸入區域名稱。 「 Roger Williams 」 已羅德島 hello 第一個管理員。 許多公園、建築物和學校都是以他的姓名命名。

![][11]

此外，您也可以試著使用這些字詞：

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>後續步驟
這是根據 Java 和 hello USG 資料集 hello 第一個 Azure 搜尋教學課程。 經過一段時間，我們將會延長此教學課程 toodemonstrate 您可能會想 toouse 自訂方案中的其他搜尋功能。

如果您已經有一些背景，在 Azure 搜尋中，可用於此範例為 springboard 進一步的實驗，或許加強 hello[搜尋頁面](search-pagination-page-layout.md)，或實作[多面向導覽](search-faceted-navigation.md)。 您也可以藉由加入計數和批次的文件，以便使用者可以透過 hello 結果頁改善 hello 搜尋結果頁面時。

新 tooAzure 搜尋嗎？ 我們建議您嘗試其他教學課程 toodevelop 了解您可以建立。 請瀏覽我們[文件頁面](https://azure.microsoft.com/documentation/services/search/)toofind 更多資源。 您也可以檢視中的 hello 連結我們[影片和教學課程清單](search-video-demo-tutorial-list.md)tooaccess 的詳細資訊。

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
