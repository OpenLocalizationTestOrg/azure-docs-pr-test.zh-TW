---
title: "aaaHow tooMigrate] 和 [發行 Web 應用程式 tooan Azure 雲端服務從 Visual Studio |Microsoft 文件"
description: "深入了解如何 toomigrate 和使用 Visual Studio 發行您的 web 應用程式 tooan Azure 雲端服務。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: a2832c37d2ebdbc1e69a307d16b65b1c87e9070c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-migrate-and-publish-a-web-application-tooan-azure-cloud-service-from-visual-studio"></a>如何： 移轉並發行 Web 應用程式 tooan Azure 雲端服務，從 Visual Studio
tootake 利用 hello 裝載服務和延展性的 Azure，您可能會想 toomigrate 和發行您的 web 應用程式 tooan Azure 雲端服務。 您可以使用幾乎不需要變更 tooyour 現有的應用程式，在 Azure 中執行 web 應用程式。

> [!NOTE]
> 本主題是關於部署 toocloud 服務，不 tooweb 站台。 如需部署 tooweb 站台資訊，請參閱[部署在 Azure App Service web 應用程式](app-service-web/web-sites-deploy.md)。
>
>

如需所支援的 Visual C# 和 Visual Basic 特定範本的清單，請參閱 hello 節**支援的專案範本**本主題稍後。

您必須先從 Visual Studio 啟用 Azure 的 Web 應用程式。 hello 下列圖例顯示加入部署 Azure 專案 toouse hello 的關鍵步驟 toopublish 現有的 web 應用程式。 此程序加入具有所需的 hello web 角色 tooyour 方案之 Azure 專案。 根據您的 web 專案的 hello 型別，hello 專案屬性中的組件也會更新如果 hello 服務封裝還需要其他組件的部署。

![發行 Web 應用程式 tooMicrosoft Azure](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC748917.png)

> [!NOTE]
> hello**轉換**，**轉換 tooAzure 雲端服務專案**命令才會顯示在方案中的 hello web 專案。 例如，hello 命令不適用於您的方案中的 Silverlight 專案。
> 當您建立服務封裝，或發行應用程式 tooAzure 時，則可能會發生警告或錯誤。 這些警告和錯誤可以協助您部署 tooAzure 之前修正的問題。 例如，您可能會收到遺失組件的警告。 如需有關如何 tootreat 任何警告視為錯誤，請參閱[使用 Visual Studio 設定 Azure 雲端服務專案](vs-azure-tools-configuring-an-azure-project.md)。 如果您建置應用程式中，執行此程式碼使用 hello 計算模擬器在本機或發行 tooAzure，您可能會看到下列錯誤 hello 中的 hello**錯誤清單**視窗： **hello 指定路徑，檔案名稱，或兩者都太長**. 因為 hello hello 完整的 Azure 專案名稱長度太長，就會發生此錯誤。 hello hello 專案名稱，包括 hello 完整路徑長度不能超過 146 個字元。 比方說，這是 hello 完整專案名稱，包括針對 Silverlight 應用程式所建立的 Azure 專案的檔案路徑： `c:\users\<user name>\documents\visual studio 2015\Projects\SilverlightApplication4\SilverlightApplication4.Web.Azure.ccproj`。 您可能必須 toomove 您的方案 tooa 不同目錄具有較短路徑 tooreduce hello hello 完整的專案名稱的長度。
>
>

toomigrate 及發行 web 應用程式 tooAzure 從 Visual Studio，請遵循下列步驟。

## <a name="enable-a-web-application-for-deployment-tooazure"></a>啟用 Web 應用程式的部署 tooAzure
### <a name="tooenable-a-web-application-for-deployment-tooazure"></a>tooenable 部署 tooAzure 的 web 應用程式
1. tooenable web 應用程式部署 tooAzure，將快顯功能表開啟 hello web 專案的方案，然後選擇 加入 Azure 部署專案。

    發生下列動作的 hello:

   * Azure 的專案呼叫`<name of hello web project>.Azure`加入 toohello 應用程式方案。
   * Hello web 專案的 web 角色加入 toothis Azure 專案。
   * hello**複製到本機**屬性設 tootrue MVC 2、 MVC 3、 MVC 4 和 Silverlight 商務應用程式所需的任何組件。 這會將這些部署所使用的組件 toohello 服務封裝。

   > [!IMPORTANT]
   > 如果您有其他組件或檔案所需的此 web 應用程式，您必須手動設定這些檔案的 hello 內容。 如需有關如何 tooset 這些屬性，請參閱資訊 hello 區段**hello 服務封裝中的包含檔**本文稍後。
   >
   > [!NOTE]
   > 如果特定 web 專案的 web 角色已經存在於 Azure hello 方案中專案**轉換**，**轉換 tooAzure 雲端服務專案**不會顯示 hello 這個 web 專案的捷徑功能表.
   >
   >

   如果您有 web 應用程式中的多個 web 專案，而且您想 toocreate web 角色的每個 web 專案，您必須在每個 web 專案的這個程序執行 hello 步驟。 這麼做會為每個 Web 角色建立個別的 Azure 專案。 您就可以個別發佈每一個 Web 專案。 或者，您可以在 web 應用程式中手動新增另一個 web 角色 tooan 現有的 Azure 專案。 toodo hello，開啟 hello 快顯功能表**角色**資料夾在 Azure 專案中，選擇**新增**，然後**方案中的 Web 角色專案**，選擇 hello 專案 tooadd 網路角色，然後選擇 [hello**確定**] 按鈕。

## <a name="use-an-azure-sql-database-for-your-application"></a>將 Azure SQL Database 用於應用程式
如果您的 web 應用程式會使用未在 hello 內部部署的 SQL Server 資料庫的連接字串，您必須變更此連接字串 toouse SQL Database 的執行個體 Azure 託管改為。

> [!IMPORTANT]
> 您的訂用帳戶必須啟用 toouse SQL 資料庫。 如果您從 hello 存取您的訂用帳戶[Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，您可以判斷您的訂用帳戶提供了哪些服務。 hello 下列指示適用於發行 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。 如果您使用 hello [Azure 入口網站](http://portal.microsoft.com)，略過 toohello 下一個程序。
>
>

### <a name="toouse-a-sql-database-instance-in-your-web-role-for-your-connection-string"></a>toouse web 角色的連接字串中的 SQL Database 執行個體
1. SQL Database 的執行個體中 hello toocreate [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，hello 下列文章中的 hello 步驟：[建立 SQL Database 伺服器](http://go.microsoft.com/fwlink/?LinkId=225109)。

   > [!NOTE]
   > 當您針對 SQL Database 執行個體設定 hello 防火牆規則時，您必須選取 hello**允許此伺服器的其他 Azure 服務 tooaccess**核取方塊。
   >
   >
2. 執行個體的連接字串，SQL Database toouse toocreate 步驟 hello hello hello 下列文章中的後續一節：[建立 SQL Database](http://go.microsoft.com/fwlink/?LinkId=225110)。
3. toocopy hello ADO.NET 連接字串 toouse 的連接字串，執行下列步驟在 hello hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。  

   1. 選擇 hello**資料庫**按鈕，然後再開啟 hello hello 訂用帳戶，您使用 toocreate SQL Database 執行個體的節點。
   2. toodisplay hello 可用的執行個體的 SQL 資料庫選擇 hello **SQL 資料庫**節點。
   3. hello 資料庫 toodisplay hello 屬性選擇 hello 資料庫。 hello**屬性**檢視會顯示。

      > [!NOTE]
      > 如果 hello**屬性**檢視不會出現，您可能需要 tooopen 它使用 hello 分割線。
      >
      >
   4. toodisplay hello 的連接字串，請選擇 hello 省略符號 （...） 按鈕的下一個 tooView。

      hello**連接字串** 對話方塊隨即出現。
   5. toocopy hello ADO.NET 連接字串中，反白顯示 hello 文字，然後選擇 hello Ctrl + C 鍵。
   6. tooclose hello 對話方塊方塊中，選擇 hello**關閉** 按鈕。
4. tooreplace hello 連線可以字串 hello web.config 檔案 toouse 中 SQL Database 的這個執行個體、 開啟 hello web.config 檔案，反白顯示 hello 現有連接字串的項目，然後選擇 hello Ctrl + V 鍵。 hello hello SQL Database 執行個體的 ADO.NET 連接字串會取代 hello 現有的連接字串。
5. 您也必須加入 hello 參數`MultipleActiveResultSets=True`toohello 連接字串。 hello 連接字串應該具有下列格式的 hello:

    ```
    connectionString=”Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"
    ```
6. （選擇性）替代方法 toochanging hello 連接字串直接 hello web.config 檔案中是 tooadd 區段為一個 hello web.config 轉換檔案，視您使用 toocreate 服務套件 hello 組建組態而定。 開啟 hello Web.Debug.Config 檔案或 hello Web.Release.Config 檔案。 新增下列區段到這個檔案的 hello:

    ```
    XMLCopy<connectionStrings><addname="DefaultConnection"connectionString="Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"xdt:Transform="SetAttributes"xdt:Locator="Match(name)"/></connectionStrings>
    ```
7. 儲存修改過的 hello 檔案，並重新發行應用程式。

### <a name="toouse-an-instance-of-sql-database-by-using-hello-azure-classic-portal"></a>toouse 使用 hello Azure 傳統入口網站的 SQL Database 執行個體
1. 在 [hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，選擇 hello SQL Database] 節點。

   * 如果您想 toouse SQL Database 的 hello 執行個體，請選擇 tooopen 它。
   * 如果您尚未建立任何執行個體，選擇 hello 適當連結，然後再建立執行個體。
2. 您開啟或建立的資料庫執行個體之後，請選擇 hello**連接字串**連結。
3. 在 hello hello 頁面底部，選擇 hello 連結 tooconfigure 防火牆設定，並接受 hello 預設值或設定您需要的 hello 值。
4. 複製 hello ADO.NET 連接字串、 貼入您的 web.config 檔案中透過 hello 舊資料庫連接字串 hello 在內部部署，而且確定 tooadd `MultipleActiveResultSets=True`。

## <a name="publish-a-web-application-tooazure"></a>發行 Web 應用程式 tooAzure
### <a name="toopublish-a-web-application-tooazure"></a>Web 應用程式 tooAzure toopublish
1. tootest hello 應用程式中使用 hello Azure 計算模擬器的 hello 本機開發環境中，開啟 hello hello Azure 的捷徑功能表 hello web 角色專案，並選擇**設定為啟始專案**。 接下來選擇 [偵錯]、[開始偵錯] \(鍵盤：**F5**)。

    hello**開始 hello Azure 偵錯環境**對話方塊隨即開啟並 hello 瀏覽器中啟動 hello 應用程式。 如需如何 toostart 每個輸入 hello 中的 web 應用程式的特定詳細資料計算模擬器，請參閱本節中的 hello 資料表。
2. 您的應用程式 toopublish tooAzure 的 hello 服務 tooset，您必須擁有 Microsoft 帳戶和 Azure 訂用帳戶。 使用 hello 步驟 hello 遵循您的服務主題 tooset:[準備 toopublish 或部署 Azure 應用程式從 Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md)。
3. toopublish hello web 應用程式 tooAzure 開啟 hello hello web 專案的捷徑功能表，然後選擇 **發行 tooAzure**。

    hello**發行 Azure 應用程式**對話方塊隨即開啟，Visual Studio 開啟 hello 部署程序。 如需如何 toopublish hello 應用程式的詳細資訊，請參閱 hello 節**發行 Azure 應用程式，從 Visual Studio**中[發行雲端服務使用 hello Azure Tools](vs-azure-tools-publishing-a-cloud-service.md)。

   > [!NOTE]
   > 您也可以發佈 hello 從 hello Azure 專案的 web 應用程式。 toodo，開啟 hello hello Azure 專案的捷徑功能表，然後選擇 **發行**。
   >
   >
4. toosee hello 部署的 hello 進度，您可以檢視 hello **Azure 活動記錄檔**視窗。 Hello 部署程序啟動時，會自動顯示此記錄檔。 您可以展開 hello 活動記錄檔中的 hello 明細項目 tooshow 詳細的資訊，如 hello 下列圖例所示：

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)
5. （選擇性） toocancel hello 部署程序，開啟 hello 活動記錄檔中的 hello hello 明細項目捷徑功能表，然後選擇 **取消並移除**。 這會停止 hello 部署程序，並從 Azure 刪除 hello 部署環境。

   > [!NOTE]
   > tooremove 之後這個部署環境已部署，您必須使用 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。
   >
   >
6. （選擇性）Visual Studio 啟動角色執行個體後，會自動顯示在 hello hello 部署環境**Azure 計算**節點**Cloud Explorer**或**伺服器總管**. 從這裡您可以檢視 hello hello 個別角色執行個體狀態。

    hello 如下圖所示 hello 中的角色執行個體**伺服器總管**仍在 hello Initializing 狀態時：

    ![VST_DeployComputeNode](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744134.png)
7. tooaccess 應用程式部署之後，選擇 hello 箭頭下一步 tooyour 部署的狀態時**已完成**會出現在 hello **Azure 活動記錄檔**。 這顯示在 Azure 中的 hello web 應用程式的 URL。 請參閱下表以取得的 hello 詳細如何 toostart 特定類型 web 應用程式，從 Azure 的 hello。

    hello 下表列出 hello toostart 特定 web 應用程式，從 Azure 或 toorun 或偵錯 web 應用程式使用 hello Azure 計算模擬器在本機的方式詳細資料：

   | Web 應用程式類型 | 執行/偵錯在本機使用 hello 計算模擬器 | 在 Azure 中執行 |
   | --- | --- | --- |
   | ASP.NET Web 應用程式 |在 hello 功能表列上選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |選擇顯示 hello hello 的 URL 超連結**部署** 索引標籤的 hello **Azure 活動記錄檔**tooload hello 起始頁 hello 瀏覽器中的。 |
   | ASP.NET MVC 2 Web 應用程式 |在 hello 功能表列上選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |選擇顯示 hello hello 的 URL 超連結**部署** 索引標籤的 hello **Azure 活動記錄檔**tooload hello 起始頁 hello 瀏覽器中的。 |
   | ASP.NET MVC 3 Web 應用程式 |在 hello 功能表列上選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |選擇顯示 hello hello 的 URL 超連結**部署** 索引標籤的 hello **Azure 活動記錄檔**tooload hello 起始頁 hello 瀏覽器中的。 |
   | ASP.NET MVC 4 Web 應用程式 |在 hello 功能表列上選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |選擇顯示 hello hello 的 URL 超連結**部署** 索引標籤的 hello **Azure 活動記錄檔**tooload hello 起始頁 hello 瀏覽器中的。 |
   | ASP.NET 空白 Web 應用程式 |您必須設定為 hello 起始頁 web 專案的應用程式中加入.aspx 網頁。 然後 hello 功能表列上，選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |如果您有預設的.aspx 網頁應用程式中，選擇顯示 hello hello 的 URL 超連結**部署** 索引標籤的 hello **Azure 活動記錄檔**和 hello 瀏覽器中載入此頁面。 如果您有不同的.aspx 網頁，您需要使用下列格式的 url 的 hello toonavigate toothis 特定頁面：`<url for deployment>/<name of page>.aspx` |
   | Silverlight 應用程式 |在 hello 功能表列上選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |您使用下列格式的 url 的 hello 的應用程式需要 toonavigate toohello 特定頁面：`<url for deployment>/<name of page>.aspx` |
   | Silverlight 商務應用程式 |在 hello 功能表列上選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |您使用下列格式的 url 的 hello 的應用程式需要 toonavigate toohello 特定頁面：`<url for deployment>/<name of page>.aspx` |
   | Silverlight 瀏覽應用程式 |在 hello 功能表列上選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |您使用下列格式的 url 的 hello 的應用程式需要 toonavigate toohello 特定頁面：`<url for deployment>/<name of page>.aspx` |
   | WCF 服務應用程式 |Hello 啟動 WCF 服務專案頁面中的，您必須設定 hello.svc 檔案。 然後 hello 功能表列上，選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |您需要您的應用程式使用下列格式的 url 的 hello toonavigate toohello svc 檔案：`<url for deployment>/<name of service file>.svc` |
   | WCF 工作流程服務應用程式 |Hello 啟動 WCF 服務專案頁面中的，您必須設定 hello.svc 檔案。 然後 hello 功能表列上，選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |您需要您的應用程式使用下列格式的 url 的 hello toonavigate toohello svc 檔案：`<url for deployment>/<name of service file>.svc` |
   | ASP.NET 動態實體 |在 hello 功能表列上選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |您必須更新 hello 連接字串 （請參閱下一節）。 您也會使用下列格式的 url 的 hello 的應用程式需要 toonavigate toohello 特定頁面：`<url for deployment>/<name of page>.aspx` |
   | ASP.NET 動態資料 Linq tooSQL |在 hello 功能表列上選擇 **偵錯**，**開始偵錯**(鍵盤： 選擇 hello **F5**索引鍵。)。 |您必須依照此程序中的 hello 步驟： 使用 SQL Azure 資料庫應用程式 （請參閱本主題中的前一節）。 您也會使用下列格式的 url 的 hello 的應用程式需要 toonavigate toohello 特定頁面：`<url for deployment>/<name of page>.aspx` |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>更新 ASP.NET 動態實體的連接字串
### <a name="tooupdate-a-connection-string-for-aspnet-dynamic-entities"></a>tooUpdate ASP.NET 動態實體連接字串
1. toocreate SQL Azure 資料庫可用於 ASP.NET 動態實體 web 應用程式，請遵循 hello 程序中的 hello 步驟**應用程式使用 SQL Azure 資料庫**稍早在本主題。
2. 加入 hello 資料表和欄位 hello 這個資料庫所需[Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。
3. 這種類型的應用程式的 hello 連接字串具有下列格式 hello web.config 檔案中的 hello:  

    ```
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    更新 hello *connectionString*值以 hello SQL Azure 資料庫的 ADO.NET 連接字串，如下所示：

    ```
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```
4. toosave hello web.config 檔案，以您所做 toohello 連接字串 hello 功能表列上的選擇的 hello 變更**檔案**，**儲存 web.config**。

## <a name="supported-project-templates"></a>支援的專案範本
toopublish web 應用程式 tooAzure，hello 應用程式必須使用其中一個 hello 專案範本的 C# 或 Visual Basic 中 hello 下表所列。

| 專案範本群組 | 專案範本 |
| --- | --- |
| Web |ASP.NET Web 應用程式 |
| Web |ASP.NET MVC 2 Web 應用程式 |
| Web |ASP.NET MVC 3 Web 應用程式 |
| Web |ASP.NET MVC4 Web 應用程式 |
| Web |ASP.NET 空白 Web 應用程式 |
| Web |ASP.NET MVC 2 空白 Web 應用程式 |
| Web |ASP.NET 動態資料實體 Web 應用程式 |
| Web |ASP.NET 動態資料 Linq tooSQL Web 應用程式 |
| Silverlight |Silverlight 應用程式 |
| Silverlight |Silverlight 商務應用程式 |
| Silverlight |Silverlight 瀏覽應用程式 |
| WCF |WCF 服務應用程式 |
| WCF |WCF 工作流程服務應用程式 |
| 工作流程 |WCF 工作流程服務應用程式 |

## <a name="next-steps"></a>後續步驟
如需發佈的詳細資訊，請參閱[準備 tooPublish 或部署 Azure 應用程式從 Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md)。 另請參閱 [設定具名的驗證認證](vs-azure-tools-setting-up-named-authentication-credentials.md)。
