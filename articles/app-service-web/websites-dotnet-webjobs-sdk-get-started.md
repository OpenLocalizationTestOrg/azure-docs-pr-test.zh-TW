---
title: "Azure App Service 中的.NET WebJob aaaCreate |Microsoft 文件"
description: "使用 ASP.NET MVC 和 Azure 建立多層式應用程式。 hello 前端執行 web 應用程式在 Azure 應用程式服務，並且 hello 在後端執行的 webjob。 hello 應用程式會使用 Entity Framework、 SQL Database 和 Azure 儲存體佇列和 blob。"
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>在 Azure App Service 中建立 .NET WebJob
本教學課程示範 toowrite 簡單的多層式 ASP.NET MVC 5 應用程式使用 hello 的程式碼[WebJobs SDK](websites-dotnet-webjobs-sdk.md)。

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

hello 目的 hello [WebJobs SDK](websites-webjobs-resources.md) toosimplify hello 程式碼，您可以執行的 WebJob，例如映像處理、 佇列的處理、 RSS 彙總、 檔案維護的一般工作為撰寫，且傳送電子郵件。 hello WebJobs SDK 有內建的功能，使用 Azure 儲存體和 Service Bus、 工作排程和處理錯誤，以及許多其他常見的案例。 此外，它擁有設計 toobe 可擴充，而且沒有[擴充功能的開放原始碼儲存機制](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)。

hello 範例應用程式是廣告電子佈告欄。 使用者可以上傳映像，以廣告，並後端程序轉換 hello 映像 toothumbnails 資料。 hello ad 清單頁面會顯示 hello 縮圖、 和 hello ad 詳細資料頁面會顯示 hello 完整大小的影像。 以下為螢幕擷取畫面：

![Ad list](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

此範例應用程式能夠與 [Azure 佇列](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) 和 [Azure Blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage) 搭配使用。 hello 教學課程會示範如何 toodeploy hello 應用程式太[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)和[Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279)。

## <a id="prerequisites"></a>必要條件
hello 教學課程假設您已經知道如何與 toowork [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) Visual Studio 中的專案。

hello 教學課程原始寫入 Visual Studio 2013，但可以搭配 Visual Studio 的更新版本。 如果您使用 Visual Studio 2015 或 2017年，記下您在本機執行 hello 應用程式之前，您必須變更 hello `Data Source` hello Web.config 和 App.config 檔案中的 hello SQL Server LocalDB 連接字串的一部分`Data Source=(localdb)\v11.0`太`Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>您必須擁有 Azure 帳戶 toocomplete 本教學課程：
>
> * 您可以[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)： 取得信用額度，您可以使用 tootry 出支付 Azure 服務，以及它們甚至用完之後，您可以讓 hello 的帳戶，並使用免費的 Azure 服務，例如網站。 永遠不會將向您的信用卡，除非您明確地變更您的設定，並詢問 toobe 收費。
> * 您可以[啟用 Visual Studio 訂閱者的每月 Azure 額度](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)：您的訂用帳戶每個月都會提供額度，供您用在付費 Azure 服務。
>
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
>
>

## <a id="learn"></a>您將學到什麼
hello 教學課程會示範如何 toodo hello 下列工作：

* （僅適用於 Visual Studio 2013 和 2015年使用者） 安裝 hello Azure SDK 來啟用 Azure 的開發電腦。
* 建立部署 hello 相關聯的 web 專案時，會自動部署 Azure webjob 的主控台應用程式專案。
* 測試 hello 開發電腦上本機 WebJobs SDK 後的端。
* 應用程式服務中發佈 WebJobs 後端 tooa web 應用程式的應用程式。
* 上傳檔案，並將它們儲存在 hello Azure Blob 服務。
* 使用 Azure 儲存體佇列和 blob 的 hello Azure WebJobs SDK toowork。

## <a id="contosoads"></a>應用程式架構
hello 範例應用程式使用 hello[佇列為主的工作模式](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern)toooff 負載 hello CPU 運算密集工作建立縮圖 tooa 後端處理程序。

hello 應用程式會儲存在 SQL 資料庫中，使用 Entity Framework Code First toocreate hello 資料表和存取 hello 資料廣告。 對於每個廣告，hello 資料庫會儲存兩個 Url： 一個用於 hello 完整大小的影像，一個用於 hello 縮圖。

![Ad table](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

使用者當上傳的影像、 hello web 應用程式儲存中的 hello 映像[Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)，而且會儲存點 toohello blob 的 url hello 資料庫中的 hello ad 資訊。 在 hello 相同時間，它會將訊息 tooan Azure 佇列。 執行 Azure webjob 的後端程序，在 hello WebJobs SDK 輪詢 hello 新訊息的佇列。 新的訊息出現時，hello WebJob 建立該映像的縮圖，並更新 hello 該廣告的縮圖 URL 資料庫欄位。 以下是顯示 hello 部分 hello 應用程式之間的互動圖表：

![Contoso Ads architecture](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
hello 教學課程指示適用於 tooAzure SDK for.NET 2.7.1 或更新版本。

## <a id="storage"></a>建立 Azure 儲存體帳戶
Azure 儲存體帳戶提供佇列和 blob 資料儲存在 hello 雲端中的資源。 它也可供 hello WebJobs SDK toostore 記錄資料 hello 儀表板。

在實際應用程式中，您通常會為應用程式資料與記錄資料建立不同的帳戶，並為測試資料與生產資料建立不同的帳戶。 在本教學課程中，您只會使用一個帳戶。

1. 開啟 hello**伺服器總管**Visual Studio 中的視窗。
2. 以滑鼠右鍵按一下 hello **Azure**節點，然後再按一下**連接 tooMicrosoft Azure 訂用帳戶...**.
   
   ![連接 tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. 使用您的 Azure 認證登入。
4. 以滑鼠右鍵按一下**儲存體**底下 hello Azure 的節點，然後按一下**建立儲存體帳戶**。
   
   ![建立儲存體帳戶](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. 在 [hello**建立儲存體帳戶**] 對話方塊中，輸入 hello 儲存體帳戶的名稱。

    hello 名稱必須是必須是唯一的 (沒有其他的 Azure 儲存體帳戶可以有 hello 相同的名稱)。 如果您輸入的 hello 名稱已在使用中，您會得到機會 toochange 它。

    hello 儲存體帳戶將會是 URL tooaccess *{name}*。.core.windows.net。
6. 設定 hello**地區或同質群組**下拉式選單 toohello 區域最接近 tooyou。

    此設定會指定哪個 Azure 資料中心將會主控您的儲存體帳戶。 對於本教學課程，您的選擇將不會造成顯著的差異。 不過，生產環境 web 應用程式中，您希望您的 web 伺服器和您在 hello 的儲存體帳戶 toobe 相同區域 toominimize 延遲和資料輸出費用。 hello web 應用程式 （您將在稍後建立） 的資料中心應該接近盡可能 toohello 瀏覽器存取的順序 toominimize 延遲 hello web 應用程式。
7. 設定 hello**複寫**下拉式清單也列出**本機備援**。

    儲存體帳戶啟用地理複寫時，儲存的 hello 內容是複寫的 tooa 次要資料中心 tooenable 容錯移轉 toothat 位置發生重大災害 hello 主要位置中。 地理區域複寫會引發額外成本。 針對測試和開發的帳戶，您通常不想要 toopay 地理複寫。 如需詳細資訊，請參閱 [建立、管理或刪除儲存體帳戶](../storage/common/storage-create-storage-account.md)。
8. 按一下 [建立] 。

    ![New storage account](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>下載 hello 應用程式
1. 下載並解壓縮 hello[完成方案](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)。
2. 啟動 Visual Studio。
3. 從 hello**檔案**功能表中選擇 **開啟 > 專案/方案**，瀏覽 toowhere 下載 hello 方案，並開啟 hello 方案檔。
4. 按 CTRL + SHIFT + B toobuild hello 方案。

    根據預設，Visual Studio 會自動還原 hello NuGet 套件的內容，其中未包含在 hello *.zip*檔案。 如果未還原 hello 套件，安裝這些手動移 toohello**管理方案的 NuGet 套件**對話方塊，然後按一下 hello**還原**在 hello 右上方的按鈕。
5. 在**方案總管 中**，請確定**ContosoAdsWeb**選取為 hello 啟始專案。

## <a id="configurestorage"></a>設定 hello 應用程式 toouse 儲存體帳戶
1. 開啟 hello 應用程式*Web.config* hello ContosoAdsWeb 專案中的檔案。

    hello 檔案包含 SQL 連接字串和處理的 blob 和佇列的 Azure 儲存體連接字串。

    hello SQL 連接字串指向 tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx)資料庫。

    hello 儲存體連接字串是具有預留位置 hello 儲存體帳戶名稱和存取金鑰的範例。 您會使用連接字串具有 hello 名稱和儲存體帳戶金鑰取代。  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    hello 儲存體連接字串是預設名稱為 AzureWebJobsStorage 因為這是使用 WebJobs SDK 的 hello 名稱 hello。 hello hello Azure 環境中有 tooset 只能有一個連接字串值，因此這裡使用相同的名稱。
2. 在**伺服器總管**，以滑鼠右鍵按一下 儲存體帳戶下 hello**儲存體**節點，然後再按一下**屬性**。

    ![按一下 [儲存體帳戶] 屬性](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. 在 hello**屬性**視窗中，按一下 **儲存體帳戶金鑰**，然後按一下hello 省略符號。

    ![儲存體帳戶金鑰](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. 複製 hello**連接字串**。

    ![[儲存體帳戶金鑰] 對話方塊](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. 取代 hello 儲存體連接字串中 hello *Web.config* hello 您剛才複製的連接字串的檔案。 請確定您選取的所有項目在 hello 引號內，但不是包括 hello 引號之前貼。
6. 開啟 hello *App.config* hello ContosoAdsWebJob 專案中的檔案。

    此檔案有兩個儲存體連接字串，一個供應用程式使用，另一個供記錄使用。 您可以對應用程式資料和記錄使用不同的儲存體帳戶，以及您可以 [對資料使用多個儲存體帳戶](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)。 在本教學課程中，您將使用單一儲存體帳戶。 hello 連接字串具有 hello 儲存體帳戶金鑰的預留位置。

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    根據預設，hello WebJobs SDK 會尋找名為 AzureWebJobsStorage 和 AzureWebJobsDashboard 的連接字串。 或者，您可以[hello 連接字串儲存，但是您想要傳入明確 toohello`JobHost`物件](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config)。
7. 這兩個儲存體連接字串取代為您之前複製的 hello 連接字串。
8. 儲存您的變更。

## <a id="run"></a>在本機執行 hello 應用程式
1. toostart hello web 前端的 hello 應用程式，請按 CTRL + F5。

    hello 預設瀏覽器會開啟 toohello 首頁。 (hello web 專案會執行，因為您取消了 hello 啟始專案。)

    ![Contoso Ads home page](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. toostart hello WebJob 後端的 hello 應用程式，以滑鼠右鍵按一下中的 hello ContosoAdsWebJob 專案**方案總管 中**，然後按一下**偵錯** > **開始新執行個體**.

    主控台應用程式視窗開啟，並顯示表示 hello WebJobs SDK JobHost 物件已開始 toorun 記錄訊息。

    ![執行主控台應用程式視窗中顯示該 hello 後端](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. 在您的瀏覽器中按一下 [建立廣告]。
4. 輸入一些測試資料、 選取映像 tooupload，，然後按一下**建立**。

    ![Create page](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    hello 應用程式 toohello 索引頁面上，但它不會顯示 hello 新 ad 縮圖，因為該處理尚未尚未發生。

    同時之後簡短等候, hello 主控台應用程式視窗中的記錄訊息會顯示佇列訊息被接收，而且已經處理。

    ![Console application window showing that a queue message has been processed](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. 您會看到 hello hello 主控台應用程式視窗中的記錄訊息之後，重新整理 hello 索引頁面 toosee hello 縮圖。

    ![索引頁面](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. 按一下**詳細資料**ad toosee hello 全尺寸映像。

    ![Details page](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

您已在您的本機電腦上執行 hello 應用程式和使用 SQL Server 資料庫位於您的電腦，但它會使用佇列和 blob 中 hello 雲端。 在下列章節的 hello 您將執行 hello 應用程式 hello 雲端中使用的雲端資料庫，以及雲端 blob 和佇列。  

## <a id="runincloud"></a>在 hello 雲端中執行 hello 應用程式
您將會執行 hello 遵循 hello 雲端中的步驟 toorun hello 應用程式：

* 部署 tooWeb 應用程式。 Visual Studio 會在 App Service 和 SQL 資料庫執行個體中自動建立新的 Web 應用程式。
* 設定 hello web 應用程式 toouse Azure SQL database 與儲存體帳戶。

您已建立一些廣告時 hello 雲端中執行之後，您會檢視 hello WebJobs SDK 儀表板 toosee hello 豐富的監視功能，它有 toooffer。

### <a name="deploy-tooweb-apps"></a>部署 tooWeb 應用程式

1. 關閉 hello 瀏覽器和 hello 主控台應用程式視窗。
2. Hello 中的 hello 步驟[發行 SQL Database 的 tooAzure](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) > 一節。
3. 完成部署的 hello 步驟之後，繼續這篇文章中的 hello 其餘工作。

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a>設定 hello web 應用程式 toouse Azure SQL database 與儲存體帳戶
安全性最佳作法是太[避免讓儲存在儲存機制中的程式碼來源檔案中的連接字串等機密資訊](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)。 Azure 提供的方式 toodo 的： 您可以在 hello Azure 環境中，設定連接字串和其他設定值，以及 ASP.NET 組態應用程式開發介面會自動挑選這些值在 Azure 中的 hello 應用程式執行時。 您也可以使用在 Azure 中設定這些值**伺服器總管**、 hello Azure 網站、 Windows PowerShell 或 hello 跨平台命令列介面。 如需詳細資訊，請參閱 [應用程式字串與連接字串的運作方式](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。

在本節中，您會使用**伺服器總管**tooset 連接字串值，在 Azure 中的。

1. 在 伺服器總管 中，於 Azure > App Service > {您的資源群組} 下的 Web 應用程式上按一下滑鼠右鍵，然後按一下檢視設定。

    hello **Azure Web 應用程式**hello 上開啟的視窗**組態** 索引標籤。
2. Hello DefaultConnection 連接字串 toohello 名稱變更 hello 名稱您選擇在 hello 設定 hello SQL database 時[發行 SQL Database 的 tooAzure](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database)發行項。

    Azure 會自動建立此連接字串，當您建立 hello web 應用程式與相關聯的資料庫，所以它已有 hello 正確的連接字串值。 您要變更只 hello 名稱 toowhat 尋找您的程式碼。
3. 新增兩個新的連接字串，將他們命名為 AzureWebJobsStorage 和 AzureWebJobsDashboard。 設定得 hello 資料庫類型**自訂**，和集合 hello 連接字串值 toohello 相同的值，您使用稍早 hello *Web.config*和*App.config*檔案。 （請確定您包含 hello 整個連接字串中，不只是 hello 存取金鑰，並不會包含 hello 引號）。

    Hello WebJobs SDK，一個應用程式資料，一個用於記錄會使用這些連接字串。 如稍早所見，hello web 前端的程式碼也會使用應用程式資料的其中一個 hello。
4. 按一下 [儲存] 。

    ![Azure 入口網站中的連接字串](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. 在**伺服器總管**hello web 應用程式，以滑鼠右鍵按一下，然後按**停止**。
6. Hello web 應用程式停止之後，再次以滑鼠右鍵按一下 hello web 應用程式，然後按一下**啟動**。

   當您發行，但它會停止進行組態變更時，會自動啟動 hello WebJob。 toorestart，您可以重新啟動 hello web 應用程式，或在 hello 中重新啟動 hello WebJob [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)。 它通常建議的 toorestart hello web 應用程式之後設定變更時。
7. 重新整理已 hello web 應用程式 URL，其網址列中的 hello 瀏覽器視窗。

    hello 首頁會出現。
8. 建立 ad，您可以如同時您[執行 hello 應用程式在本機](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally)。

   下一開始的縮圖，顯示 hello 索引頁面。
9. 幾秒之後重新整理 hello 頁面並 hello 縮圖出現。

   如果未出現 hello 縮圖，您可能會有 toowait 約一分鐘 hello WebJob toorestart。 如果一段時間之後，您仍然看 hello 縮圖，當您重新整理 hello] 頁面上，[hello WebJob 可能不會自動啟動。 在此情況下，移 toohello**應用程式服務**刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com/)，找出您的 web 應用程式，然後按一下**啟動**。

### <a name="view-hello-webjobs-sdk-dashboard"></a>檢視 hello WebJobs SDK 儀表板
1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取 hello**應用程式服務刀鋒視窗**，找出您的 web 應用程式，並選取**WebJobs**。
3. 選取 hello**記錄** 索引標籤。

    ![記錄索引標籤](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    新的瀏覽器索引標籤會開啟 toohello WebJobs SDK 儀表板。 hello 儀表板會顯示該 hello web 工作正在執行，並顯示您的程式碼 WebJobs SDK 所觸發的 hello 函式的清單。
4. 按一下其中一個執行有關的 hello 函式 toosee 詳細資料。

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    hello **Replay 函式**此頁面上的按鈕會導致 hello WebJobs SDK framework toocall hello 函式一次，並可提供您機會 toochange hello 傳遞資料 toohello 函式第一次。

> [!NOTE]
> 當您完成測試，請考慮刪除 hello web 應用程式、 儲存體帳戶和您的 SQL Database 執行個體。 hello web 應用程式是免費的但 hello SQL 儲存體帳戶和資料庫執行個體都會產生費用 (雖然 toohello 較小，因為最小)。 此外，如果您離開 hello web 應用程式執行時，您的 URL 會尋找任何人可以建立及檢視廣告。 
>
>

### <a name="delete-your-web-app"></a>刪除 Web 應用程式
在 hello 入口網站中，移 toohello**應用程式服務**刀鋒視窗中，找出並選取您的 web 應用程式，然後按一下**刪除**。 如果您只想 tootemporarily 防止其他人從存取 hello web 應用程式，請按一下**停止**改為。 在此情況下，費用將繼續 tooaccrue hello SQL 資料庫和儲存體帳戶。

### <a name="delete-your-storage-account"></a>刪除儲存體帳戶
toodelete 儲存體帳戶，請參閱[刪除儲存體帳戶](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account)。 

### <a name="delete-your-database"></a>刪除資料庫
toodelete SQL 資料庫，請參閱 hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/)文件。

## <a id="create"></a>從頭開始建立 hello 應用程式
本節中，您將會執行下列工作 hello:

* 使用 Web 專案建立 Visual Studio 方案。
* 加入類別庫專案 hello 資料 hello 前端及後端之間共用的存取層。
* 使用 WebJobs 部署啟用加入 hello 後端中，主控台應用程式專案。
* 新增 NuGet 封裝。
* 設定專案參考。
* 複製應用程式程式碼和組態檔案從您使用過 hello hello 教學課程的上一節中的 hello 下載應用程式。
* 檢閱 hello hello 程式碼部分與 Azure blob 和佇列並 hello WebJobs SDK。

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>使用 Web 專案和類別庫專案建立 Visual Studio 方案
1. 在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]。
2. 在 [hello**新專案**] 對話方塊中，選擇**Visual C#** > **Web** > **ASP.NET Web 應用程式 (.NET Framework)**.
3. Hello 專案 ContosoAdsWeb、 hello 方案 ContosoAdsWebJobsSDK 命名 (變更 hello 方案名稱，如果您要將它放置在 hello hello 與相同的資料夾會下載解決方案)，然後按一下**確定**。

    ![New Project](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. 在 hello**新的 ASP.NET Web 應用程式** 對話方塊中，選擇 hello MVC 範本，並選取 **變更驗證**。

    ![變更驗證](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. 在 hello**變更驗證** 對話方塊中，選擇**非驗證**，然後按一下**確定**。

    ![不需要驗證](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. 在 [hello**新的 ASP.NET Web 應用程式**] 對話方塊中，按一下**確定**。

    Visual Studio 建立 hello 方案和 hello web 專案。
7. 在**方案總管] 中**，以滑鼠右鍵按一下 hello 方案 （不 hello 專案），然後選擇 [**新增** > **新專案**。
8. 在 [hello**加入新的專案**] 對話方塊中，選擇**Visual C#** > **的傳統 Windows 桌面** > **類別程式庫 (.NET架構）**範本。  
9. 名稱 hello 專案*ContosoAdsCommon*，然後按一下**確定**。

    這個專案會包含 hello Entity Framework 內容和 hello 資料模型的這兩個 hello 前端和後端將會使用。 或者，可以在 hello web 專案中定義 hello EF 相關類別，從 hello WebJob 專案參考該專案。 但是，然後在 WebJob 專案必須參考 tooweb 組件，它不需要。

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>新增已啟用 WebJobs 部署的主控台應用程式專案
1. Hello web 專案 （非 hello 方案或 hello 類別庫專案），以滑鼠右鍵按一下，然後按一下**新增** > **新增 Azure WebJob 專案**。

    ![New Azure WebJob Project menu selection](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. 在 hello**新增 Azure WebJob**  對話方塊中，輸入這兩個 hello ContosoAdsWebJob**專案名稱**和 hello **WebJob 名稱**。 保留**模式執行的 WebJob**設定得**持續執行**。
3. 按一下 [確定] 。

   Visual Studio 建立主控台應用程式所設定的 toodeploy webjob 每當您將部署的 hello web 專案。 它會執行下列工作建立 hello 專案後的 hello toodo:

   * 加入*webjob 發行 settings.json* hello WebJob 專案屬性 資料夾中的檔案。
   * 加入*webjobs list.json* hello web 專案屬性 資料夾中的檔案。
   * Hello Microsoft.Web.WebJobs.Publish NuGet 封裝安裝在 hello WebJob 專案中。

   如需有關這些變更的詳細資訊，請參閱[如何使用 Visual Studio toodeploy WebJobs](websites-dotnet-deploy-webjobs.md)。

### <a name="add-nuget-packages"></a>新增 NuGet 封裝
WebJob 專案的 hello 新專案範本會自動安裝 hello WebJobs SDK 的 NuGet 套件[Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs)及其相依項目。

其中一個 hello hello WebJob 專案中自動安裝 WebJobs SDK 相依性是 hello Azure 儲存體用戶端程式庫 (SCL)。 不過，您需要 tooadd 它 toohello web 專案 toowork 使用 blob 和佇列。

1. 開啟 hello**管理 NuGet 封裝**hello 解決方案的對話方塊。
2. Hello 左窗格中，選取**安裝封裝**。
3. 尋找 hello *Azure 儲存體*封裝，然後按一下**管理**。
4. 在 hello**選取專案** 方塊中，選取 hello **ContosoAdsWeb**核取方塊，然後**確定**。

    所有的三個專案使用 hello Entity Framework toowork SQL 資料庫中的資料。
5. Hello 左窗格中，選取**線上**。
6. 尋找 hello *EntityFramework* NuGet 封裝，並將它安裝在所有的三個專案。

### <a name="set-project-references"></a>設定專案參考
Web 和 WebJob 專案，使用 hello SQL 資料庫，因此兩者都必須參考 toohello ContosoAdsCommon 專案。

1. 在 hello ContosoAdsWeb 專案設定參考 toohello ContosoAdsCommon 專案。 (Hello ContosoAdsWeb 專案中，以滑鼠右鍵按一下，然後按一下**新增** > **參考**。 
2. 在 hello**參考管理員**對話方塊中，選取**專案** > **方案** > **ContosoAdsCommon**，然後按一下**確定**。)
   
    hello WebJob 專案必須參考使用映像以及存取連接字串。

4. 在 hello ContosoAdsWebJob 專案中，設定參照太`System.Drawing`和`System.Configuration`。

### <a name="add-code-and-configuration-files"></a>新增程式碼和組態檔
本教學課程不會顯示如何太[建立 MVC 控制器和檢視使用 scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)、 如何太[撰寫適用於 SQL Server 資料庫的 Entity Framework 程式碼](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)，或[hello 的基本概念非同步程式設計中 ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async)。 因此，所有會維持為 toodo 是從下載的 hello 方案到 hello 新解決方案的複製程式碼和組態檔。 這麼做之後，hello 下列各節顯示並說明 hello 程式碼的關鍵部分。

tooadd 檔案 tooa 專案或資料夾、 以滑鼠右鍵按一下 hello 專案或資料夾並按一下**新增** > **現有項目**。 選取 hello 檔案和按一下**新增**。 如果系統詢問您是否想 tooreplace 現有檔案，按一下**是**。

1. 在 hello ContosoAdsCommon 專案中，刪除 hello *Class1.cs*檔案，然後加入下列檔案從下載的 hello 專案及其位置 hello 中。

   * *Ad.cs*
   * *ContosoAdscontext.cs*
   * BlobInformation.cs
2. 在 hello ContosoAdsWeb 專案中，新增 hello hello 下載專案中的下列檔案。

   * *Web.config*
   * *Global.asax.cs*  
   * 在 hello*控制器*資料夾： *AdController.cs*
   * 在 hello *_layout.cshtml*資料夾： *_Layout.cshtml*檔案
   * 在 hello *Views\Home*資料夾： *Index.cshtml*
   * 在 hello *Views\Ad*資料夾 （第一次建立 hello 資料夾）： 五個*.cshtml*檔案
3. 在 hello ContosoAdsWebJob 專案中，新增 hello hello 下載專案中的下列檔案。

   * *App.config* (也變更 hello 檔案類型篩選**所有檔案**)
   * *Program.cs*
   * *Functions.cs*

您現在可以建置、 執行及部署如稍早在 hello 教學課程中所指示的 hello 應用程式。 您這麼做之前，不過，停止 hello 仍在執行部署到 hello 第一個 web 應用程式中的 WebJob。 否則，該 WebJob 會處理在本機建立的佇列訊息或由執行新的 web 應用程式中的 hello 應用程式，因為所有使用 hello 相同儲存體帳戶。

## <a id="code"></a>檢閱 hello 應用程式程式碼
hello 下列各節說明 hello 程式碼相關的 tooworking 以 hello WebJobs SDK 和 Azure 儲存體 blob 和佇列。

> [!NOTE]
> 如 hello 程式碼特定 toohello WebJobs SDK，請移至 toohello [Program.cs 和 Functions.cs](#programcs)區段。
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
hello Ad.cs 檔案定義 ad 類別列舉和廣告資訊的 POCO 實體類別。

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
hello ContosoAdsContext 類別指定 hello Ad 類別用於 DbSet 集合，其中 Entity Framework 將儲存在 SQL 資料庫。

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

hello 類別有兩個建構函式。 hello 首先 hello web 專案中，使用，並指定連接字串儲存在 hello Web.config 檔案或 hello Azure 執行階段環境的 hello 名稱。 hello 第二個建構函式可讓您 toopass hello 實際的連接字串中。 是因為它沒有 Web.config 檔需要 hello WebJob 專案。 之前看到這個連接字串的儲存位置，而您會看到如何 hello 程式碼會擷取 hello 連接字串時，它會具現化 hello DbContext 類別。

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon - BlobInformation.cs
hello`BlobInformation`類別是使用的 toostore 佇列訊息中的映像 blob 資訊。

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
程式碼從 hello 呼叫`Application_Start`方法會建立*映像*blob 容器和*映像*排入佇列，如果它們不存在。 這可確保每當您開始使用新的儲存體帳戶，hello 必要的 blob 容器和佇列會自動建立。

使用從 hello hello 儲存體連接字串 hello 程式碼取得存取 toohello 儲存體帳戶*Web.config*檔案或 Azure 執行階段環境。

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

然後，它會取得參考 toohello*映像*blob 容器時，如果它不存在，並設定存取權限 hello 新的容器建立 hello 容器。 根據預設，新的容器允許透過儲存體帳戶認證 tooaccess blob 的用戶端。 hello web 應用程式需要 hello blob toobe 公開，讓它可以顯示使用該點 toohello 映像 blob Url 的映像。

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

類似的程式碼取得參考 toohello *thumbnailrequest*佇列，並建立新的佇列。 在此情況下，即不需要變更權限。

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - _Layout.cshtml
hello *_Layout.cshtml*檔案設定中 hello 頁首和頁尾，hello 應用程式名稱，並建立"廣告 」 功能表項目。

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
hello *Views\Home\Index.cshtml*檔案 hello 首頁上顯示類別目錄連結。 hello 連結傳遞 hello 整數值的 hello `Category` querystring 變數 toohello 廣告索引頁面中的列舉。

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
在 hello *AdController.cs*檔案、 hello 建構函式呼叫 hello`InitializeStorage`方法 toocreate Azure 儲存體用戶端程式庫物件，提供應用程式開發介面使用的 blob 和佇列。

然後，hello 程式碼會取得參考 toohello*映像*blob 容器，如稍早在您所見*Global.asax.cs*。 在執行該動作時，它會設定適用 Web 應用程式的預設 [重試原則](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) 。 hello 預設指數型輪詢重試原則無法停止回應 hello web 應用程式的時間超過一分鐘上重複的重試的暫時性錯誤。 此處指定的 hello 重試原則會等待三秒鐘之後每個嘗試向上 toothree 嘗試。

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

類似的程式碼取得參考 toohello*映像*佇列。

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

大部分的 hello 控制器程式碼是使用 Entity Framework 資料模型使用 DbContext 類別的一般。 例外狀況為 hello HttpPost`Create`方法，這個方法會將檔案上傳，並將它儲存在 blob 儲存體。 hello 模型繫結器提供[HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello 方法的物件。

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

如果 hello 使用者選取檔案 tooupload，hello 程式碼會 hello 檔案上傳、 將它儲存在 blob，並更新 hello Ad 資料庫記錄點 toohello blob 的 URL。

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

hello 沒有 hello 上傳的程式碼處於 hello`UploadAndSaveBlobAsync`方法。 它會建立 GUID hello blob、 上傳和儲存 hello 檔案，並傳回參考 toohello 儲存 blob。

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

之後 hello HttpPost`Create`方法上傳 blob 並更新 hello 資料庫，它會建立佇列訊息 tooinform hello 後端程序映像可供轉換 tooa 縮圖。

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

hello 碼 hello HttpPost`Edit`方法很類似，不同之處在於如果 hello 使用者選取新的映像檔，必須刪除此 ad 已存在的任何 blob。

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

以下是當您刪除廣告時，會刪除 blob 的 hello 程式碼：

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml 和 Details.cshtml
hello *Index.cshtml*檔案就會顯示以 hello 的縮圖，其他的 ad 資料：

        <img  src="@Html.Raw(item.ThumbnailURL)" />

hello *Details.cshtml*檔案會顯示 hello 完整大小的影像：

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml 和 Edit.cshtml
hello *Create.cshtml*和*Edit.cshtml*檔案會指定表單編碼可讓 hello 控制器 tooget hello`HttpPostedFileBase`物件。

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

`<input>`項目會告知 hello 瀏覽器 tooprovide 檔案選取對話方塊。

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
當 hello WebJob 啟動 hello`Main`方法呼叫 hello WebJobs SDK`JobHost.RunAndBlock`方法 toobegin 觸發的函式 hello 目前執行緒上執行。

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail 方法
接收佇列訊息時，hello WebJobs SDK 會呼叫這個方法。 hello 方法會建立縮圖，並將 hello 縮圖 hello 資料庫中的 URL。

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* hello`QueueTrigger`屬性會指示 hello WebJobs SDK toocall 這個方法 hello thumbnailrequest 佇列上收到一封新郵件時。

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    hello `BlobInformation` hello 佇列訊息中的物件是自動還原序列化成 hello`blobInfo`參數。 Hello 方法完成時，就會刪除 hello 佇列訊息。 如果在完成之前，hello 方法失敗，則不會刪除 hello 佇列訊息;在 10 分鐘租用到期之後，hello 訊息會是發行的 toobe 再度收取和處理。 如果某個訊息總是導致例外狀況，則不會無限制地重複此順序。 Hello 訊息 5 失敗嘗試 tooprocess 訊息之後，是移動的 tooa 佇列名為 {queuename}-有害。 hello 的嘗試次數上限是可設定的。
* 兩個 hello`Blob`屬性提供的繫結的 tooblobs 物件： 一個 toohello 現有映像的 blob 和一個 tooa 新縮圖 blob hello 方法建立。

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    Blob 名稱來自於屬性的 hello `BlobInformation` hello 佇列郵件中收到的物件 (`BlobName`和`BlobNameWithoutExtension`)。 tooget hello 完整功能 hello 儲存體用戶端程式庫，您可以使用 hello`CloudBlockBlob`類別 toowork 與 blob。 如果您想 tooreuse 撰寫程式碼都已使用 toowork`Stream`物件，您可以使用 hello`Stream`類別。

如需有關如何 toowrite 函式都使用 WebJobs SDK 屬性，請參閱下列資源的 hello:

* [如何 toouse Azure 佇列儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [如何 toouse Azure blob 儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [如何 toouse Azure 資料表儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [如何 toouse Azure 服務匯流排與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * 如果您的 web 應用程式在多個 Vm 上執行，將會同時執行多個 WebJobs，在某些情況下這會導致 hello 相同資料進行處理多次。 如果您使用 hello 內建佇列、 blob 和 Service Bus 觸發程序，這是不發生問題。 hello SDK 可確保您的函式將會一次處理的每個訊息或 blob。
> * 如需有關資訊 tooimplement 正常關機，請參閱[正常關機](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful)。
> * hello hello 中的程式碼`ConvertImageToThumbnailJPG`（未顯示） 的方法會使用類別中 hello`System.Drawing`為了簡單起見命名空間。 不過，此命名空間中的 hello 類別針對搭配 Windows Form 使用所設計。 不支援將它們用於 Windows 或 ASP.NET 服務。 如需映像處理選項的詳細資訊，請參閱[動態映像產生](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx)和[深入調整映像大小](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na)。
>
>

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已經看到 hello WebJobs SDK 用於後端處理簡單多層式應用程式。 如要進一步了解 ASP.NET 多層式應用程式和 WebJobs，請參考本節所提供的一些建議。

### <a name="missing-features"></a>遺漏的功能
hello 應用程式已經過簡化，快速入門教學課程。 在真實世界的應用程式就會實作[相依性插入](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection)和 hello[儲存機制和單位運作模式](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo)，使用[記錄介面](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log)，使用[EF Code First 移轉](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application)toomanage 資料模型變更，並使用[EF 連接恢復功能](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)toomanage 暫時性的網路錯誤。

### <a name="scaling-webjobs"></a>調整 WebJob 的規模
WebJobs hello 內容 web 應用程式中執行而且無法擴充分開。 比方說，如果您有一個標準的 web 應用程式執行個體，您只有一個執行個體背景程序執行，且使用部分 hello 伺服器的資源 （CPU、 記憶體等），否則將會使用 tooserve web 內容。

如果流量會因日或每週的時間，而且 hello 後端處理中，您需要可等候 toodo，您無法在低流量的時間排程 WebJobs toorun。 如果 hello 負載仍為該方案太高，您可以在不同的 web 應用程式專用的 webjob 執行 hello 後端，針對該目的項目。 接著您可以擴充後端 Web 應用程式，而不會影響到前端 Web 應用程式。

如需詳細資訊，請參閱 [調整 WebJob](websites-webjobs-resources.md#scale)。

### <a name="avoiding-web-app-timeout-shut-downs"></a>避免關機時 Web 應用程式逾時
toomake 確定您的 WebJobs 會一直執行，而且在您 web 應用程式的所有執行個體上執行，您有 tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx)功能。

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a>使用 hello 之外 WebJobs WebJobs SDK
Azure 在 WebJob 中使用 WebJobs SDK hello 的程式沒有 toorun。 它可以在本機執行，也可以在如雲端服務背景工作角色或 Windows 服務等其他環境中執行。 不過，您可以透過 Azure web 應用程式只能存取 hello WebJobs SDK 儀表板。 toouse hello 儀表板有 tooconnect hello web 應用程式 toohello 儲存您所使用的帳戶設定 hello AzureWebJobsDashboard 連接字串 hello**設定**hello 傳統入口網站 索引標籤。 然後，您可以使用下列 URL 的 hello 取得 toohello 儀表板：

https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions

如需詳細資訊，請參閱[儀表板取得以 hello WebJobs SDK 的本機開發](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx)，但請注意，它會顯示舊的連接字串名稱。

### <a name="more-webjobs-documentation"></a>其他 WebJobs 文件
如需詳細資訊，請參閱 [Azure WebJobs 文件資源](http://go.microsoft.com/fwlink/?LinkId=390226)。
