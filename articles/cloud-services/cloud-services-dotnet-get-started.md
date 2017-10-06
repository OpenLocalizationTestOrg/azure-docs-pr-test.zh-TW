---
title: "開始使用 Azure 雲端服務和 ASP.NET 的 aaaGet |Microsoft 文件"
description: "深入了解如何 toocreate 使用 ASP.NET MVC 和 Azure 的多層式應用程式。 hello 應用程式會在雲端服務中，使用 web 角色和背景工作角色執行。 它使用 Entity Framework、SQL Database 及 Azure 儲存體佇列和 Blob。"
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a>開始使用 Azure 雲端服務和 ASP.NET

## <a name="overview"></a>概觀
本教學課程示範如何 toocreate 多層.NET 應用程式與 ASP.NET MVC 前端伺服器上，並將其部署 tooan [Azure 雲端服務](cloud-services-choose-me.md)。 hello 應用程式會使用[Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279)，hello [Azure Blob 服務](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)，和 hello [Azure 佇列服務](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern)。 您可以[下載 hello Visual Studio 專案](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)從 MSDN Code Gallery hello。

hello 教學課程會示範如何 toobuild 和執行 hello 本機應用程式，如何 toodeploy 它 tooAzure 和執行中的 hello 雲端，以及如何 toobuild 從頭它。 您可以啟動從頭建置和執行 hello 測試並部署步驟之後，如果您偏好。

## <a name="contoso-ads-application"></a>Contoso Ads 應用程式
hello 應用程式是廣告電子佈告欄。 使用者透過輸入文字和上傳影像來建立廣告。 使用者可以查看清單的廣告以縮圖影像，以及使用者可以看見 hello 完整大小的影像時，它們會選取 ad toosee hello 詳細資料。

![Ad list](./media/cloud-services-dotnet-get-started/list.png)

hello 應用程式會使用 hello[佇列為主的工作模式](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern)toooff 負載 hello CPU 運算密集工作建立縮圖 tooa 後端程序。

## <a name="alternative-architecture-websites-and-webjobs"></a>替代架構：網站和 WebJobs
本教學課程示範如何 toorun 前端和後端 Azure 中雲端服務。 替代方式是在前端 toorun hello [Azure 網站](/services/web-sites/)並用 hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) hello 後端 （目前處於預覽階段） 功能。 使用 WebJobs 教學課程中，請參閱[hello Azure WebJobs SDK 快速入門](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)。 如資訊如何 toochoose hello 服務最符合您的案例，請參閱 < [Azure 網站、 雲端服務和虛擬機器的比較](../app-service-web/choose-web-site-cloud-service-vm.md)。

## <a name="what-youll-learn"></a>您將學到什麼
* 如何 tooenable 電腦所安裝的 Azure 開發 hello Azure SDK。
* 如何 toocreate Visual Studio 將雲端服務專案，使用 ASP.NET MVC web 角色和背景工作角色。
* 如何 tootest hello 雲端服務專案在本機，使用 hello Azure 儲存體模擬器。
* 如何 toopublish hello 雲端專案 tooan Azure 雲端服務，並測試使用的 Azure 儲存體帳戶。
* 如何 tooupload 檔案，並將其儲存在 hello Azure Blob 服務。
* 如何 toouse hello Azure 佇列服務各層之間的通訊。

## <a name="prerequisites"></a>必要條件
hello 教學課程假設您已了解[Azure 的基本概念的雲端服務](cloud-services-choose-me.md)例如*web 角色*和*背景工作角色*術語。  它也假設您知道如何與 toowork [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)或[Web Form](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) Visual Studio 中的專案。 hello 範例應用程式使用 MVC 中，但大部分的 hello 教學課程也適用於 tooWeb 表單。

您可以執行 Azure 訂用帳戶中，未使用在本機的 hello 應用程式，但是您將需要一個 toodeploy hello 應用程式 toohello 雲端。 如果您沒有這類帳戶，可以[啟用自己的 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668)或是[申請免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668)。

hello 教學課程的指示運作 hello 下列產品的其中一種：

* Visual Studio 2013
* Visual Studio 2015
* Visual Studio 2017

如果您沒有下列其中一種，Visual Studio 可能會自動安裝時安裝 hello Azure SDK。

## <a name="application-architecture"></a>應用程式架構
hello 應用程式會儲存在 SQL 資料庫中，使用 Entity Framework Code First toocreate hello 資料表和存取 hello 資料廣告。 每個廣告，hello 資料庫存放區兩個 Url，一個用於 hello 完整大小的影像，另一個用於 hello 縮圖。

![Ad table](./media/cloud-services-dotnet-get-started/adtable.png)

當使用者上傳映像時，hello 前端執行的 web 角色中會儲存中的 hello 映像[Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)，而且會儲存點 toohello blob 的 url hello 資料庫中的 hello ad 資訊。 在 hello 相同時間，它會將訊息 tooan Azure 佇列。 定期執行背景工作角色中的後端程序就會輪詢 hello 新訊息的佇列。 新的訊息出現時，hello 背景工作角色建立該映像的縮圖，並更新 hello 該廣告的縮圖 URL 資料庫欄位。 hello 下列圖表顯示 hello 部分 hello 應用程式互動的方式。

![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a>下載並執行已完成的 hello 方案
1. 下載並解壓縮 hello[完成方案](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)。
2. 啟動 Visual Studio。
3. 從 hello**檔案**功能表中選擇 **開啟專案**，瀏覽 toowhere 下載 hello 方案，並開啟 hello 方案檔。
4. 按 CTRL + SHIFT + B toobuild hello 方案。

    根據預設，Visual Studio 會自動還原 hello NuGet 套件的內容，其中未包含在 hello *.zip*檔案。 如果未還原 hello 套件，安裝這些手動移 toohello**管理方案的 NuGet 套件** 對話方塊，然後按一下 hello**還原**在 hello 右上方的按鈕。
5. 在**方案總管 中**，請確定**ContosoAdsCloudService**選取為 hello 啟始專案。
6. 如果您使用 Visual Studio 2015 或更新版本中，變更 hello 應用程式中的 hello SQL Server 連接字串*Web.config*檔案 hello ContosoAdsWeb 專案並在 hello *ServiceConfiguration.Local.cscfg* hello ContosoAdsCloudService 專案檔。 在每個案例中，變更 」 (localdb) \v11.0 」 太 」 (localdb) \MSSQLLocalDB"。
7. 按 CTRL + F5 toorun hello 應用程式。

    當您在本機執行雲端服務專案時，Visual Studio 自動叫用 hello Azure*計算模擬器*和 Azure*儲存體模擬器*。 hello 計算模擬器會使用您的電腦資源 toosimulate hello web 角色和背景工作角色環境。 hello 儲存體模擬器會使用[SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx)資料庫 toosimulate Azure 雲端儲存體。

    hello 第一次執行雲端服務專案所需約一分鐘 hello 模擬器 toostart 組成。 模擬器啟動完成時，hello 預設瀏覽器會開啟 toohello 應用程式的首頁。

    ![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/home.png)
8. 按一下 [建立廣告]。
9. 輸入一些測試資料，並選取*.jpg* tooupload 的映像，然後按一下**建立**。

    ![Create page](./media/cloud-services-dotnet-get-started/create.png)

    hello 應用程式 toohello 索引頁面上，但它不會顯示 hello 新 ad 縮圖，因為該處理尚未尚未發生。
10. 稍候片刻，然後重新整理 hello 索引頁面 toosee hello 縮圖。

     ![索引頁面](./media/cloud-services-dotnet-get-started/list.png)
11. 按一下**詳細資料**ad toosee hello 全尺寸映像。

     ![Details page](./media/cloud-services-dotnet-get-started/details.png)

您已完全在本機電腦沒有連線 toohello 雲端上執行 hello 應用程式。 hello 儲存體模擬器儲存 hello 佇列和 SQL Server Express LocalDB 資料庫和 hello 應用程式中的 blob 資料儲存在另一個 LocalDB 資料庫 hello ad 資料。 Entity Framework Code First 自動建立的 hello ad 資料庫 hello hello web 應用程式嘗試 tooaccess 的第一次它。

Hello 下列區段中，您需要設定 hello 方案 toouse Azure 雲端資源的佇列、 blob 和 hello 應用程式資料庫 hello 雲端中執行時進行。 如果您想要在本機 toocontinue toorun，但使用雲端儲存體和資料庫資源，您可以執行。 它是只需設定連接字串，您會看到如何 toodo。

## <a name="deploy-hello-application-tooazure"></a>部署 hello 應用程式 tooAzure
您將會執行 hello 遵循 hello 雲端中的步驟 toorun hello 應用程式：

* 建立 Azure 雲端服務。
* 建立 Azure SQL Database。
* 建立 Azure 儲存體帳戶。
* 在 Azure 中執行時設定 hello 方案 toouse Azure SQL database。
* 在 Azure 中執行時設定 hello 方案 toouse Azure 儲存體帳戶。
* 將 hello 專案 tooyour Azure 雲端服務部署。

### <a name="create-an-azure-cloud-service"></a>建立 Azure 雲端服務
Azure 雲端服務是 hello 環境 hello 應用程式將執行。

1. 在瀏覽器中，開啟 hello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [新增] > [計算] > [雲端服務]。

3. 在 hello DNS 名稱輸入方塊中，輸入 hello 雲端服務的 URL 前置詞。

    這個 URL 有 toobe 唯一。  如果您選擇的 hello 前置詞已在使用，您會收到錯誤訊息。
4. 指定 hello 服務的新資源群組。 按一下**建立新**然後 hello 資源群組輸入方塊中，例如 CS_contososadsRG 輸入的名稱。

5. 選擇您想 toodeploy hello 應用程式的 hello 地區。

    此欄位會指定將託管您的雲端服務的資料中心。 對於生產應用程式中，您應選擇 hello 區域最接近 tooyour 客戶。 此教學課程中，選擇 hello 區域最接近 tooyou。
5. 按一下 [建立] 。

    在下列映像的 hello，雲端服務會建立以 hello URL CSvccontosoads.cloudapp.net。

    ![New Cloud Service](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a>建立 Azure SQL 資料庫
Hello 應用程式執行時 hello 雲端中，它會使用以雲端為基礎的資料庫。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **新增 > 資料庫 > SQL Database**。
2. 在 hello**資料庫名稱**方塊中，輸入*contosoads*。
3. 在 hello**資源群組**，按一下 **使用現有**與選取的 hello hello 雲端服務所使用的資源群組。
4. 在 hello 下列映像，按一下 **伺服器-設定必要的設定**和**建立新的伺服器**。

    ![通道 toodatabase 伺服器](./media/cloud-services-dotnet-get-started/newdb.png)

    或者，如果您訂用帳戶已經有伺服器，您可以從 hello 下拉式清單中選取該伺服器。
5. 在 hello**伺服器名稱**方塊中，輸入*csvccontosodbserver*。

6. 輸入系統管理員的 [登入名稱] 和 [密碼]。

    如果您選取了 [建立新伺服器]，則不要在此輸入現有的名稱和密碼。 您正在輸入的新名稱和密碼，您正在定義現在 toouse 稍後當您存取 hello 資料庫。 如果您選取您先前建立的伺服器時，會提示您已經建立 hello 密碼 toohello 系統管理使用者帳戶。
7. 選擇 hello 相同**位置**您選擇 hello 雲端服務。

    當 hello 雲端服務和資料庫位於不同的資料中心 （不同的區域），延遲會增加，您將支付 hello 資料中心外部的頻寬。 資料中心內的頻寬則是免費的。
8. 請檢查**允許 azure 服務 tooaccess 伺服器**。
9. 按一下**選取**hello 新伺服器。

    ![新的 SQL Database 伺服器](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. 按一下 [建立] 。

### <a name="create-an-azure-storage-account"></a>建立 Azure 儲存體帳戶
Azure 儲存體帳戶提供佇列和 blob 資料儲存在 hello 雲端中的資源。

在真實世界應用程式中，您一般會為應用程式資料與記錄資料建立不同的帳戶，以及為測試資料與生產資料建立不同的帳戶。 在本教學課程中，您只會使用一個帳戶。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **新增 > 儲存體 > 儲存體帳戶-blob、 檔案、 資料表、 佇列**。
2. 在 hello**名稱**方塊中，輸入的 URL 前置詞。

    您在 [hello] 方塊下，請參閱此前置詞加上 hello 文字將 hello 唯一 URL tooyour 儲存體帳戶。 如果已經被其他人使用您輸入的 hello 前置詞，您就必須 toochoose 在不同的前置詞。
3. 設定 hello**部署模型**太*傳統*。

4. 設定 hello**複寫**下拉式清單也列出**本機備援儲存體**。

    儲存體帳戶啟用地理複寫時，儲存的 hello 內容 hello 主要位置中發生重大災害時，就會為複寫的 tooa 次要資料中心 tooenable 容錯移轉。 地理區域複寫會引發額外成本。 針對測試和開發的帳戶，您通常不想要 toopay 地理複寫。 如需詳細資訊，請參閱 [建立、管理或刪除儲存體帳戶](../storage/common/storage-create-storage-account.md)。

5. 在 hello**資源群組**，按一下 **使用現有**與選取的 hello hello 雲端服務所使用的資源群組。
6. 設定 hello**位置**下拉式選單 toohello 您選擇 hello 雲端服務的相同地區。

    Hello 雲端服務和儲存體帳戶位於不同的資料中心 （不同的區域），延遲會增加，您將支付 hello 資料中心外部的頻寬。 資料中心內的頻寬則是免費的。

    Azure 同質群組提供機制 toominimize hello 之間的距離資料中心，以降低延遲的資源。 本教學課程不會使用同質群組。 如需詳細資訊，請參閱[如何 tooCreate 親和性群組在 Azure 中](http://msdn.microsoft.com/library/jj156209.aspx)。
7. 按一下 [建立] 。

    ![New storage account](./media/cloud-services-dotnet-get-started/newstorage.png)

    Hello 映像，在儲存體帳戶會建立具有 hello URL `csvccontosoads.core.windows.net`。

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a>在 Azure 中執行時設定 hello 方案 toouse Azure SQL database
hello web 專案 hello 背景工作角色專案各有自己的資料庫連接字串和每個需求 toopoint toohello Azure SQL database 在 Azure 中的 hello 應用程式執行時。

您將使用[Web.config 轉換](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations)hello web 角色和 hello 背景工作角色的雲端服務環境設定。

> [!NOTE]
> 在這一節和 hello 下一節中，您可以將專案檔中的認證來儲存。 [請勿將敏感性資料儲存在公用原始程式碼存放庫](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)。
>
>

1. 在 hello ContosoAdsWeb 專案中，開啟 hello *Web.Release.config* hello 應用程式轉換檔*Web.config*檔案中，刪除 hello 註解區塊包含`<connectionStrings>`項目，並貼上下列程式碼，其所在位置的 hello。

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    保留 hello 檔案開啟以供編輯。
2. 在 hello [Azure 入口網站](https://portal.azure.com)，按一下  **SQL 資料庫**hello 左窗格中，按一下 在此教學課程中，您所建立的 hello 資料庫，然後按一下**顯示連接字串**。

    ![Show connection strings](./media/cloud-services-dotnet-get-started/showcs.png)

    hello 入口網站會顯示以 hello 密碼預留位置的連接字串。

    ![連接字串](./media/cloud-services-dotnet-get-started/connstrings.png)
3. 在 hello *Web.Release.config*轉換檔案，請刪除`{connectionstring}`在其位置 hello ADO.NET 連接字串 hello Azure 入口網站中貼上。
4. 您貼入 hello hello 連接字串中*Web.Release.config*轉換檔案，請取代`{your_password_here}`與您建立新 SQL database hello 的 hello 密碼。
5. 儲存 hello 檔案。  
6. 選取並複製 hello 連接字串 （不含 hello 周圍的引號)，用於 hello 設定 hello 背景工作角色專案的步驟。
7. 在**方案總管 中**下**角色**hello 雲端服務專案中，以滑鼠右鍵按一下**ContosoAdsWorker** ，然後按一下**屬性**.

    ![Role properties](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. 按一下 hello**設定** 索引標籤。
9. 變更**服務組態**太**雲端**。
10. 選取 hello**值**欄位 hello`ContosoAdsDbConnectionString`設定，然後再貼上您所複製的 hello hello 教學課程的上一節的 hello 連接字串。

     ![Database connection string for worker role](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. 儲存您的變更。  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a>在 Azure 中執行時設定 hello 方案 toouse Azure 儲存體帳戶
Hello web 角色專案和 hello 背景工作角色專案的 azure 儲存體帳戶連接字串會儲存在 hello 雲端服務專案中的環境設定。 對於每個專案，一組個別的 hello 應用程式會在本機執行時使用的設定 toobe 和 hello 雲端中執行。 您要更新的 web 和背景工作角色專案 hello 雲端環境的設定。

1. 在**方案總管 中**，以滑鼠右鍵按一下**ContosoAdsWeb**下**角色**在 hello **ContosoAdsCloudService**專案，然後再按一下**屬性**。

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. 按一下 hello**設定**] 索引標籤。在 [hello**服務組態**下拉式清單方塊中，選擇**雲端**。

    ![Cloud configuration](./media/cloud-services-dotnet-get-started/sccloud.png)
3. 選取 hello **StorageConnectionString**項目，而且您會看到省略符號 (**...**) hello 右尾 hello 按鈕。 按一下 hello 省略符號按鈕 tooopen hello**建立儲存體帳戶連接字串** 對話方塊。

    ![Open Connection String Create box](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. 在 hello**建立儲存體連接字串**對話方塊中，按一下 **訂用帳戶**，選擇您先前建立的 hello 儲存體帳戶，然後按一下**確定**。 如果您尚未登入，將提示您輸入 Azure 帳戶憑證。

    ![Create Storage Connection String](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. 儲存您的變更。
6. 後續 hello 相同程序與您用於 hello`StorageConnectionString`連接字串 tooset hello`Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString`連接字串。

    此連接字串用於記錄。
7. 後續 hello 相同程序與您用於 hello **ContosoAdsWeb**角色 tooset hello 這兩個連接字串**ContosoAdsWorker**角色。 別忘了 tooset**服務組態**太**雲端**。

您已設定使用 Visual Studio UI hello hello 角色環境設定會儲存在下列檔案 hello ContosoAdsCloudService 專案中的 hello:

* *ServiceDefinition.csdef* -定義 hello 設定名稱。
* *ServiceConfiguration.Cloud.cscfg* -hello 雲端中的 hello 應用程式執行時提供值。
* *ServiceConfiguration.Local.cscfg* -hello 應用程式在本機上執行提供的值。

比方說，hello ServiceDefinition.csdef 包含 hello 下列定義：

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

和 hello *ServiceConfiguration.Cloud.cscfg*檔案包含您輸入的這些設定，在 Visual Studio 中的 hello 值。

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

hello`<Instances>`設定指定 hello Azure 將 hello 背景工作角色執行程式碼的虛擬機器數目。 hello[後續步驟](#next-steps)章節包含有關向外延展的雲端服務，連結 toomore 資訊

### <a name="deploy-hello-project-tooazure"></a>部署 hello 專案 tooAzure
1. 在**方案總管] 中**，以滑鼠右鍵按一下 hello **ContosoAdsCloudService**雲端專案，然後選取 [**發行**。

   ![Publish menu](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. 在 [hello**登入**hello 的步驟**發行 Azure 應用程式**精靈] 中，按一下**下一步**。

    ![Sign in step](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. 在 [hello**設定**步驟 hello 精靈] 中，按一下**下一步**。

    ![Settings step](./media/cloud-services-dotnet-get-started/pubsettings.png)

    hello hello 中的預設設定**進階**索引標籤會顯示在此教學課程正常。 Hello 進階 索引標籤的相關資訊，請參閱[發行 Azure 應用程式精靈](http://msdn.microsoft.com/library/hh535756.aspx)。
4. 在 hello**摘要**步驟中，按一下 **發行**。

    ![Summary step](./media/cloud-services-dotnet-get-started/pubsummary.png)

   hello **Azure 活動記錄檔**視窗在 Visual Studio 中開啟。
5. 按一下 hello 向右箭號圖示 tooexpand hello 部署詳細資料。

    hello 部署可能會佔用 too5 分鐘或更多 toocomplete。

    ![Azure Activity Log window](./media/cloud-services-dotnet-get-started/waal.png)
6. Hello 部署狀態完成時，按一下 hello **Web 應用程式 URL** toostart hello 應用程式。
7. 您現在可以測試 hello 應用程式所建立、 檢視和編輯某些廣告，如同您在本機執行 hello 應用程式時。

> [!NOTE]
> 當您完成測試、 刪除或停止 hello 雲端服務。 即使您不使用 hello 雲端服務，它持費用，因為它會保留虛擬機器資源。 如果您讓它保持執行，找到您 URL 的任何人都可以建立和檢視廣告。 在 hello [Azure 入口網站](https://portal.azure.com)，移 toohello**概觀**標籤為您的雲端服務，然後按一下hello**刪除**hello hello 頁頂端的按鈕。 如果您只想 tootemporarily 防止其他人無法存取 hello 站台，按一下 **停止**改為。 在此情況下，費用將繼續 tooaccrue。 當您不再需要它們時，您可以依照類似的程序 toodelete hello SQL 資料庫和儲存體帳戶。
>
>

## <a name="create-hello-application-from-scratch"></a>從頭開始建立 hello 應用程式
如果尚未下載[hello 完成應用程式](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)，請立刻進行升級。 您將下載的 hello 專案將檔案複製到 hello 新專案。

建立 hello Contoso 廣告應用程式包括 hello 下列步驟：

* 建立雲端服務 Visual Studio 方案。
* 更新和加入 NuGet 封裝。
* 設定專案參考。
* 設定連接字串。
* 加入程式碼檔案。

建立 hello 方案之後，您將檢閱 hello 的程式碼的唯一 toocloud 服務專案和 Azure blob 和佇列。

### <a name="create-a-cloud-service-visual-studio-solution"></a>建立雲端服務 Visual Studio 方案
1. 在 Visual Studio 中，選擇 **新專案**從 hello**檔案**功能表。
2. Hello hello 左窗格中**新專案**對話方塊方塊中，展開  **Visual C#**選擇**雲端**範本，然後選擇 hello **Azure 雲端服務**範本。
3. 命名 hello 專案和方案 ContosoAdsCloudService，，然後按一下**確定**。

    ![New Project](./media/cloud-services-dotnet-get-started/newproject.png)
4. 在 hello**新的 Azure 雲端服務**對話方塊方塊中，加入 web 角色和背景工作角色。 命名 hello web 角色 ContosoAdsWeb，並命名為 hello ContosoAdsWorker 的背景工作角色。 （hello 右窗格 toochange hello 預設 hello 角色名稱中使用 hello 鉛筆圖示）。

    ![New Cloud Service Project](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. 當您看到 hello**新增 ASP.NET 專案**hello web 角色 對話方塊選擇 hello MVC 範本，然後按一下**變更驗證**。

    ![變更驗證](./media/cloud-services-dotnet-get-started/chgauth.png)
6. 在 hello**變更驗證**對話方塊方塊中，選擇**非驗證**，然後按一下**確定**。

    ![不需要驗證](./media/cloud-services-dotnet-get-started/noauth.png)
7. 在 [hello**新增 ASP.NET 專案**] 對話方塊中，按一下**確定**。
8. 在**方案總管] 中**，以滑鼠右鍵按一下 hello 方案 （不是其中一個 hello 專案），然後選擇 [**新增為新的專案**。
9. 在 hello**加入新的專案**對話方塊方塊中，選擇**Windows**下**Visual C#**在 hello 左的窗格，然後按一下hello**類別庫**範本。  
10. 名稱 hello 專案*ContosoAdsCommon*，然後按一下**確定**。

    您需要 tooreference hello Entity Framework 內容和 hello 資料模型從 web 和背景工作角色專案。 或者，可以在 hello web 角色專案中定義 hello EF 相關類別，從 hello 背景工作角色專案參考該專案。 但在 hello 的替代方法，您的背景工作角色專案必須參考 tooweb 組件，它不需要。

### <a name="update-and-add-nuget-packages"></a>更新和加入 NuGet 封裝
1. 開啟 hello**管理 NuGet 封裝**hello 解決方案的對話方塊。
2. 在 hello hello 視窗頂端，選取**更新**。
3. 尋找 hello *WindowsAzure.Storage*封裝，以及是否 hello 清單中，選取它，然後選取 hello 專案 tooupdate web 和背景工作，然後按一下**更新**。

    hello 儲存體用戶端程式庫會比 Visual Studio 專案範本，更頻繁地更新，所以您通常會發現該 hello 版本中更新新建立的專案需求 toobe。
4. 在 hello hello 視窗頂端，選取**瀏覽**。
5. 尋找 hello *EntityFramework* NuGet 封裝，並將它安裝在所有的三個專案。
6. 尋找 hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet 封裝，並將它安裝在 hello 背景工作角色專案。

### <a name="set-project-references"></a>設定專案參考
1. 在 hello ContosoAdsWeb 專案設定參考 toohello ContosoAdsCommon 專案。 Hello ContosoAdsWeb 專案中，以滑鼠右鍵按一下，然後按一下**參考** - **加入參考**。 在 hello**參考管理員**對話方塊中，選取**方案 – 專案**hello 左窗格中，選取**ContosoAdsCommon**，然後按一下**確定**.
2. 在 hello ContosoAdsWorker 專案設定參考 toohello ContosAdsCommon 專案。

    ContosoAdsCommon 將包含 hello Entity Framework 資料模型和內容類別，這將會使用這兩個 hello 前端和後端。
3. 在 hello ContosoAdsWorker 專案中，設定參照太`System.Drawing`。

    Hello 後端 tooconvert 映像 toothumbnails 會使用這個組件。

### <a name="configure-connection-strings"></a>設定連接字串
在本節中，您將針對本機測試用途來設定 Azure 儲存體和 SQL 連接字串。 hello hello 教學課程中先前的部署指示會說明如何 tooset hello 連線字串 hello 應用程式執行時發生 hello 雲端中。

1. 在 hello ContosoAdsWeb 專案、 開啟 hello 應用程式 Web.config 檔案，並插入 hello 下列`connectionStrings`hello 之後的項目`configSections`項目。

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    如果您使用 Visual Studio 2015 或更新版本，將 "v11.0" 取代為 "MSSQLLocalDB"。
2. 儲存您的變更。
3. 在 hello ContosoAdsCloudService 專案中，以滑鼠右鍵按一下底下的 ContosoAdsWeb**角色**，然後按一下**屬性**。

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. 在 [hello **ContosAdsWeb [角色]**屬性] 視窗中，按一下 hello**設定**索引標籤，然後再按一下**加入設定**。

    保留**服務組態**設定得**所有組態**。
5. 新增名為 *StorageConnectionString*的設定。 設定**類型**太*ConnectionString*，並設定**值**太*UseDevelopmentStorage = true*。

    ![New connection string](./media/cloud-services-dotnet-get-started/scall.png)
6. 儲存您的變更。
7. 後續 hello 相同的程序 tooadd hello ContosoAdsWorker 角色內容中的儲存體連接字串。
8. 仍在 hello **ContosoAdsWorker [角色]**屬性 視窗中，加入另一個連接字串：

   * 名稱：ContosoAdsDbConnectionString
   * 類型：字串
   * 的值： 貼上 hello 相同 hello web 角色專案使用的連接字串。 （適用於 Visual Studio 2013 的 hello 下列範例。 別忘了 toochange hello 資料來源如果複製此範例中，而您使用 Visual Studio 2015 或更新版本。）

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a>加入程式碼檔案
本節中，您將複製程式碼檔案從下載的 hello 方案到 hello 新方案。 hello 下列各節將顯示，並說明此程式碼的關鍵部分。

tooadd 檔案 tooa 專案或資料夾、 以滑鼠右鍵按一下 hello 專案或資料夾並按一下**新增** - **現有項目**。 選取您想要然後按一下 hello 檔案**新增**。 如果系統詢問您是否想 tooreplace 現有檔案，按一下**是**。

1. 在 hello ContosoAdsCommon 專案中，刪除 hello *Class1.cs*檔案，然後在其位置 hello 加入*Ad.cs*和*ContosoAdscontext.cs* hello 中的檔案已經下載專案。
2. 在 hello ContosoAdsWeb 專案中，新增 hello hello 下載專案中的下列檔案。

   * *Global.asax.cs*。  
   * 在 hello *_layout.cshtml*資料夾：  *\_Layout.cshtml*。
   * 在 hello *Views\Home*資料夾： *Index.cshtml*。
   * 在 hello*控制器*資料夾： *AdController.cs*。
   * 在 hello *Views\Ad*資料夾 （第一次建立 hello 資料夾）： 五個*.cshtml*檔案。
3. 在 hello ContosoAdsWorker 專案中，加入*WorkerRole.cs* hello 從已經下載專案。

您現在可以建置及執行 hello 應用程式，如稍早在 hello 教學課程中所指示和 hello 應用程式會使用本機資料庫和儲存體模擬器的資源。

hello 下列各節說明 hello 程式碼與相關的 tooworking hello Azure 環境、 blob 和佇列。 本教學課程並未說明如何 toocreate MVC 控制器和檢視表使用 scaffolding toowrite Entity Framework 程式碼的運作方式與 SQL Server 資料庫或 ASP.NET 4.5 中非同步程式設計的 hello 基本概念。 如需這些主題的資訊，請參閱下列資源的 hello:

* [開始使用 MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [開始使用 EF 6 和 MVC 5](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* [在.NET 4.5 簡介 tooasynchronous 程式設計](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async)。

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
hello Ad.cs 檔案定義 ad 類別列舉和廣告資訊的 POCO 實體類別。

```csharp
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
```

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
hello ContosoAdsContext 類別指定 hello Ad 類別用於 DbSet 集合，其中 Entity Framework 會將儲存在 SQL 資料庫。

```csharp
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
```

hello 類別有兩個建構函式。 第一次 hello 它們正由 hello web 專案，並指定 hello hello Web.config 檔案中儲存的連接字串的名稱。 hello 第二個建構函式可讓您 toopass hello 實際的連接字串使用 hello 背景工作角色專案，因為它沒有 Web.config 檔中。 之前看到這個連接字串的儲存位置，而您會看到如何 hello 程式碼會擷取 hello 連接字串時，它會具現化 hello DbContext 類別。

### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
程式碼從 hello 呼叫`Application_Start`方法會建立*映像*blob 容器和*映像*排入佇列，如果它們不存在。 這可確保，每當您開始使用新的儲存體帳戶，或開始使用新的電腦上的 hello 儲存體模擬器，hello 所需的 blob 容器和佇列將會自動建立。

使用從 hello hello 儲存體連接字串 hello 程式碼取得存取 toohello 儲存體帳戶*.cscfg*檔案。

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

然後它會取得參考 toohello*映像*blob 容器時，如果它不存在，並設定存取權限 hello 新的容器建立 hello 容器。 根據預設，新的容器只允許用戶端與儲存體帳戶認證 tooaccess blob。 hello 網站需要 hello blob toobe 公開，讓它可以顯示使用該點 toohello 映像 blob Url 的映像。

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

類似的程式碼取得參考 toohello*映像*佇列，並建立新的佇列。 在此情況下，即不需要變更權限。

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - \_Layout.cshtml
hello *_Layout.cshtml*檔案設定中 hello 頁首和頁尾，hello 應用程式名稱，並建立"廣告 」 功能表項目。

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
hello *Views\Home\Index.cshtml*檔案 hello 首頁上顯示類別目錄連結。 hello 連結傳遞 hello 整數值的 hello `Category` querystring 變數 toohello 廣告索引頁面中的列舉。

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
在 hello *AdController.cs*檔案、 hello 建構函式呼叫 hello`InitializeStorage`方法 toocreate Azure 儲存體用戶端程式庫物件，提供應用程式開發介面使用的 blob 和佇列。

然後 hello 程式碼會取得參考 toohello*映像*blob 容器，如稍早在您所見*Global.asax.cs*。 在執行該動作時，它會設定適用 Web 應用程式的預設 [重試原則](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) 。 hello 預設指數型輪詢重試原則無法停止回應 hello web 應用程式的時間超過一分鐘上重複的重試的暫時性錯誤。 此處指定的 hello 重試原則會等待三秒鐘之後每個嘗試向上 toothree 嘗試。

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

類似的程式碼取得參考 toohello*映像*佇列。

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

大部分的 hello 控制器程式碼是使用 Entity Framework 資料模型使用 DbContext 類別的一般。 例外狀況為 hello HttpPost`Create`方法，這個方法會將檔案上傳，並將它儲存在 blob 儲存體。 hello 模型繫結器提供[HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello 方法的物件。

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

如果 hello 使用者選取檔案 tooupload，hello 程式碼會 hello 檔案上傳、 將它儲存在 blob，並更新 hello Ad 資料庫記錄點 toohello blob 的 URL。

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

hello 沒有 hello 上傳的程式碼處於 hello`UploadAndSaveBlobAsync`方法。 它會建立 GUID hello blob、 上傳和儲存 hello 檔案，並傳回參考 toohello 儲存 blob。

```csharp
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
```

之後 hello HttpPost`Create`方法上傳 blob 並更新 hello 資料庫，它會建立佇列訊息 tooinform 該映像可供轉換 tooa 縮圖的後端程序。

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

hello 碼 hello HttpPost`Edit`方法很類似，不同之處在於如果 hello 使用者選取新的映像檔必須先刪除任何存在的 blob。

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

hello 下一個範例顯示當您刪除廣告時，會刪除 blob 的 hello 程式碼。

```csharp
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
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml 和 Details.cshtml
hello *Index.cshtml*檔案就會顯示以 hello 的縮圖，其他的 ad 資料。

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

hello *Details.cshtml*檔案會顯示 hello 完整大小的影像。

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml 和 Edit.cshtml
hello *Create.cshtml*和*Edit.cshtml*檔案會指定表單編碼可讓 hello 控制器 tooget hello`HttpPostedFileBase`物件。

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

`<input>`項目會告知 hello 瀏覽器 tooprovide 檔案選取對話方塊。

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a>ContosoAdsWorker - WorkerRole.cs - OnStart 方法
hello Azure 背景工作角色環境呼叫 hello`OnStart`方法在 hello`WorkerRole`類別時快速入門 hello 背景工作角色，而且它會呼叫 hello`Run`方法時 hello`OnStart`方法完成。

hello`OnStart`方法取得 hello 資料庫連接字串從 hello *.cscfg*檔案，並將其傳遞 toohello Entity Framework DbContext 類別。 hello SQLClient 提供者會根據預設，使用的因此 hello 提供者並沒有指定 toobe。

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

在這之後，hello 方法會取得參考 toohello 儲存體帳戶，並建立 hello blob 容器和佇列，如果不存在。 hello 的程式碼是您已經在 hello web 角色中所看到的類似 toowhat`Application_Start`方法。

### <a name="contosoadsworker---workerrolecs---run-method"></a>ContosoAdsWorker - WorkerRole.cs - Run 方法
hello`Run`呼叫方法時，hello`OnStart`方法完成初始設定工作。 hello 方法執行時造成無限迴圈，監看新的佇列訊息，並到達時加以處理。

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

在 hello 迴圈的每個反覆項目，如果找不到任何佇列訊息，hello 程式睡眠第二個。 這樣可避免產生過多 CPU 時間和儲存體交易成本 hello 背景工作角色。 hello Microsoft 客戶諮詢小組的開發人員忘記 tooinclude，告知劇本部署 tooproduction，而且留下休假時。 在他回之後，他監督成本超過 hello 休假時。

有時 hello 訊息內容的佇列將導致處理錯誤。 這稱為*有害訊息*，以及如果您只記錄錯誤並重新啟動 hello 迴圈，您可以不斷地嘗試 tooprocess 該訊息。  因此 hello catch 區塊包含 if 陳述式會檢查 toosee 多少次 hello 應用程式已嘗試 tooprocess hello 目前的訊息，而且如果它已超過 5 次，hello 訊息從 hello 佇列中刪除。

`ProcessQueueMessage` 。

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

這段程式碼讀取 hello 資料庫 tooget hello 影像 URL，將轉換 hello 影像 tooa 縮圖、 hello 縮圖會將儲存在 blob、 hello 縮圖的 blob URL，以更新 hello 資料庫並刪除 hello 佇列訊息。

> [!NOTE]
> hello hello 中的程式碼`ConvertImageToThumbnailJPG`方法為了簡單起見 hello System.Drawing 命名空間中使用類別。 不過，此命名空間中的 hello 類別針對搭配 Windows Form 使用所設計。 不支援將它們用於 Windows 或 ASP.NET 服務。 如需映像處理選項的詳細資訊，請參閱[動態映像產生](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx)和[深入調整映像大小](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na)。
>
>

## <a name="troubleshooting"></a>疑難排解
如果項目無法運作時遵循 hello 指示在本教學課程中，以下是一些常見錯誤及如何 tooresolve 它們。

### <a name="serviceruntimeroleenvironmentexception"></a>ServiceRuntime.RoleEnvironmentException
hello`RoleEnvironment`當您在 Azure 中執行應用程式，或當您執行使用 hello Azure 計算模擬器在本機，物件由 Azure 提供。  如果您在本機執行時，您會收到這個錯誤，，請確定您已設定 hello ContosoAdsCloudService 專案為 hello 啟始專案。 這會設定 hello 專案 toorun 使用 hello Azure 計算模擬器。

Hello 應用程式會使用 hello Azure RoleEnvironment 的 hello 事項之一是 tooget hello 連接字串值儲存在 hello *.cscfg*檔案，所以此例外狀況的另一個原因是遺漏的連接字串。 請確定在 hello ContosoAdsWeb 專案中，建立同時雲端的 hello StorageConnectionString 設定與本機設定，而且您 hello ContosoAdsWorker 專案中建立這兩種設定這兩個連接字串。 如果您這樣做**全部尋找**搜尋為 StorageConnectionString hello 整個方案中，您應該會看到它 9 次 6 檔案中。

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a>無法覆寫 tooport xxx。 低於最小值的新連接埠，對通訊協定 http 允許的值為 8080
請嘗試變更 hello hello web 專案所使用的連接埠號碼。 Hello ContosoAdsWeb 專案中，以滑鼠右鍵按一下，然後按一下**屬性**。 按一下 hello **Web**索引標籤，然後再變更 hello hello 連接埠號碼**專案 Url**設定。

可能會解決 hello 問題的另一個替代方式，請參閱下列章節的 hello。

### <a name="other-errors-when-running-locally"></a>在本機執行時的其他錯誤
預設的新雲端服務專案會使用 hello Azure 計算模擬器的 express toosimulate hello Azure 環境。 這是輕量版的 hello 完整計算模擬器，並在某些條件 hello 完整模擬器時 hello express 版本並不會。  

toochange hello 專案 toouse hello 完整模擬器，hello ContosoAdsCloudService 專案中，以滑鼠右鍵按一下，然後按一下**屬性**。 在 hello**屬性**視窗中按一下 hello **Web**索引標籤，然後再按一下 hello**使用完整模擬器**選項按鈕。

順序與 hello 完整模擬器的 toorun hello 應用程式，您必須 tooopen Visual Studio 系統管理員權限。

## <a name="next-steps"></a>後續步驟
hello Contoso 廣告應用程式具有刻意保留簡單快速入門教學課程。 比方說，它不會實作[相依性插入](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection)或 hello[儲存機制和單位運作模式](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo)，不是[介面用於記錄](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log)，它不會使用[EF Code First 移轉](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application)toomanage 資料模型變更或[EF 連接恢復功能](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)toomanage 暫時性網路錯誤，等等。

以下是一些雲端服務的範例應用程式示範多個實際的編碼方式，從較不複雜 toomore 複雜：

* [PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31)。 在概念上類似 tooContoso 廣告但實作更多功能和多個真實世界的編碼方式。
* [具有表格、佇列和 Blob 的 Azure 雲端服務多層式應用程式](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36)。 介紹 Azure 儲存體資料表以及 Blob 和佇列。 根據較舊版本的 hello Azure SDK for.NET，將需要與 hello 目前的版本部分修改 toowork。
* [Microsoft Azure 中的雲端服務基礎](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 完整範例，示範各種不同的最佳作法，hello Microsoft Patterns and Practices 團隊所產生。

如需 hello 雲端開發的一般資訊，請參閱[建置真實世界雲端應用程式與 Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction)。

介紹影片 tooAzure 存放裝置的最佳作法和模式，請參閱[Microsoft Azure 儲存體-最佳作法與模式新](http://channel9.msdn.com/Events/Build/2014/3-628)。

如需詳細資訊，請參閱下列資源的 hello:

* [Azure 雲端服務第 1 部分：簡介](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [如何 toomanage 雲端服務](cloud-services-how-to-manage.md)
* [Azure 儲存體](/documentation/services/storage/)
* [如何 toochoose 雲端服務提供者](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
