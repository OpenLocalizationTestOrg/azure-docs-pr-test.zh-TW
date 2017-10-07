---
title: "aaaMove 資料-資料管理閘道器 |Microsoft 文件"
description: "設定內部部署與 hello 之間的資料閘道 toomove 資料雲端。 使用資料管理閘道器在 Azure Data Factory toomove 您的資料。"
keywords: "資料閘道器, 資料整合, 移動資料, 閘道認證"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a>在內部部署來源和資料管理閘道與 hello 雲端之間移動資料
本文提供使用 Data Factory 整合內部部署資料存放區與雲端資料存放區資料的概觀。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件和其他資料處理站核心概念文件：[資料集](data-factory-create-datasets.md)和[管線](data-factory-create-pipelines.md)。

## <a name="data-management-gateway"></a>資料管理閘道
您必須將資料從內部部署資料存放區移動您在內部部署機器 tooenable 上安裝資料管理閘道器。 hello 閘道可以安裝在相同電腦做為 hello 資料存放區或不同電腦上，只要 hello 閘道可以連接 toohello 資料存放區的 hello。

> [!IMPORTANT]
> 如需資料管理閘道的詳細資料，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 一文。 

hello 下列逐步解說將示範如何 toocreate data factory 管線，將資料從內部部署移**SQL Server**資料庫 tooan Azure blob 儲存體。 Hello 逐步解說中，您可以安裝並設定 hello 資料管理閘道器電腦上。

## <a name="walkthrough-copy-on-premises-data-toocloud"></a>逐步解說： 將複製內部部署資料 toocloud
在此逐步解說中您不要 hello 下列步驟： 

1. 建立資料處理站。
2. 建立資料管理閘道。 
3. 為來源和接收的資料存放區建立已連結的服務。
4. 建立資料集 toorepresent 輸入和輸出資料。
5. 複製活動 toomove hello 資料以建立管線。

## <a name="prerequisites-for-hello-tutorial"></a>Hello 教學課程的必要條件
開始本逐步解說之前，您必須具備下列必要條件 hello:

* **Azure 訂用帳戶**。  如果您沒有訂用帳戶，則只需要幾分鐘的時間就可以建立免費試用帳戶。 請參閱 hello[免費試用版](http://azure.microsoft.com/pricing/free-trial/)文件以取得詳細資料。
* **Azure 儲存體帳戶**。 您使用做為 hello blob 儲存體**目的地/接收器**資料儲存在本教學課程。 如果您沒有 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)步驟 toocreate 其中一個發行項。
* **SQL Server**。 在本教學課程中，您會使用內部部署 SQL 資料庫作為**來源**資料存放區。 

## <a name="create-data-factory"></a>建立 Data Factory
在此步驟中，您可以使用 hello Azure Data Factory 執行個體名為的 Azure 入口網站 toocreate **ADFTutorialOnPremDF**。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 依序按一下 [+ 新增]、[智慧 + 分析] 及 [Data Factory]。

   ![新增->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. 在 hello**新的 data factory**頁面上，輸入**ADFTutorialOnPremDF** hello 名稱。

    ![新增 tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > hello hello Azure data factory 的名稱必須是全域唯一的。 如果您收到 hello 錯誤： **Data factory 名稱"ADFTutorialOnPremDF"不是使用**、 變更 hello hello data factory (例如，yournameADFTutorialOnPremDF) 名稱，然後再次嘗試重新建立。 執行此教學課程中的其餘步驟時，請使用此名稱來取代 ADFTutorialOnPremDF。
   >
   > hello hello data factory 名稱可能會註冊為**DNS** hello 未來中的名稱，因此公開可見。
   >
   >
4. 選取 hello **Azure 訂用帳戶**您想要建立 hello 資料 factory toobe。
5. 請選取現有的 **資源群組** ，或建立資源群組。 Hello 教學課程中，建立名為的資源群組： **ADFTutorialResourceGroup**。
6. 按一下**建立**上 hello**新的 data factory**頁面。

   > [!IMPORTANT]
   > toocreate Data Factory 執行個體，您必須是成員的 hello[資料 Factory 參與者](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor)hello 訂用帳戶/資源群組層級角色。
   >
   >
7. 建立完成之後，您會看到 hello **Data Factory**頁面 hello 下列影像所示：

   ![Data Factory 首頁](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a>建立閘道
1. 在 hello **Data Factory**頁面上，按一下**作者及部署**磚 toolaunch hello**編輯器**hello data factory。

    ![[製作和部署] 磚](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. 在 hello Data Factory 編輯器中，按一下  **...多個**在 hello 工具列，然後按一下**新的資料閘道**。 或者，您可以以滑鼠右鍵按一下**資料閘道**在 hello 樹狀檢視中，然後按一下**新的資料閘道**。

   ![工具列上的 [新增資料閘道]](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. 在 hello**建立**頁面上，輸入**adftutorialgateway** hello**名稱**，然後按一下**確定**。     

    ![[建立閘道] 頁面](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > 本逐步解說中，您可以建立 hello 邏輯閘道與只有一個節點 （在內部部署 Windows 電腦）。 您可以向外延展資料管理閘道將多部在內部部署電腦與 hello 閘道產生關聯。 您可以增加可在節點上同時執行的資料移動作業數目來進行相應增加。 這項功能也適用於具有單一節點的邏輯閘道。 如需得詳細資料，請參閱[在 Azure Data Factory 中調整資料管理閘道](data-factory-data-management-gateway-high-availability-scalability.md)一文。  
4. 在 hello**設定**頁面上，按一下**直接在這部電腦上安裝**。 這個動作 hello hello 閘道的安裝套件下載、 安裝、 設定和註冊 hello hello 電腦上的閘道。  

   > [!NOTE]
   > 使用 Internet Explorer 或 Microsoft ClickOnce 相容的 Web 瀏覽器。
   >
   > 如果您使用 Chrome，請移至 toohello [Chrome web store](https://chrome.google.com/webstore/)、 搜尋與"ClickOnce"關鍵字、 選擇其中一個 hello ClickOnce 擴充功能，及安裝它。
   >
   > 請勿 hello 相同 Firefox （安裝增益集）。 按一下**開啟功能表**hello 工具列上的按鈕 (**三條水平線**hello 右上角)，按一下 **附加元件**、 搜尋與"ClickOnce"關鍵字，選擇其中一個 helloClickOnce 擴充功能，並安裝它。    
   >
   >

    ![閘道 - [設定] 頁面](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    這種方式是最簡單的方式 （一種單鍵） toodownload hello、 安裝、 設定及登錄一個單一步驟中的 hello 閘道。 您可以看到 hello **Microsoft 資料管理閘道組態管理員**應用程式安裝在電腦上。 您也可以尋找 hello 可執行檔**ConfigManager.exe** hello 資料夾中： **C:\Program Files\Microsoft 資料管理 Gateway\2.0\Shared**。

    您可以同時下載和使用此頁面中的 hello 連結，以手動方式安裝閘道及顯示 hello 中的 hello 金鑰進行註冊**新金鑰**文字方塊。

    請參閱[資料管理閘道器](data-factory-data-management-gateway.md)發行項的所有 hello hello 閘道的相關詳細資料。

   > [!NOTE]
   > 您必須是 hello 本機電腦 tooinstall 的系統管理員，並已成功設定 hello 資料管理閘道器。 您可以加入其他使用者 toohello**資料管理閘道使用者**本機 Windows 群組。 hello 這個群組的成員可以使用 hello 資料管理閘道組態管理員工具 tooconfigure hello 閘道。
   >
   >
5. 等候數分鐘，或等候直至您看見 hello 下通知訊息：

    ![閘道安裝成功](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. 在電腦上啟動**資料管理閘道組態管理員**應用程式。 在 hello**搜尋**視窗中，輸入**資料管理閘道器**tooaccess 此公用程式。 您也可以尋找 hello 可執行檔**ConfigManager.exe** hello 資料夾中： **C:\Program Files\Microsoft 資料管理 Gateway\2.0\Shared**

    ![閘道器組態管理員](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. 確認您有看到 `adftutorialgateway is connected toohello cloud service` 訊息。 hello hello 底部顯示狀態列**連接 toohello 雲端服務**連同**綠色核取記號**。

    在 hello**首頁**索引標籤上，您也可以執行下列作業 hello:

   * **註冊**具有索引鍵從 hello 使用 hello 註冊按鈕的 Azure 入口網站的閘道。
   * **停止**hello 閘道機器上執行的資料管理閘道主機服務。
   * **更新排程**toobe hello 一天的特定時間安裝。
   * 檢視何時 hello 閘道**上次更新**。
   * 指定可以在安裝更新 toohello 閘道的時間。
8. 切換 toohello**設定**hello 中所指定的索引 hello 憑證**憑證**區段是 hello 在內部部署資料存放區，您指定 hello 入口網站上的使用的 tooencrypt/解密憑證。 （選擇性）按一下**變更**toouse 您自己的憑證而。 根據預設，hello 閘道會使用 hello 憑證由 hello Data Factory 服務自動產生。

    ![閘道器憑證組態](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    您也可以執行下列動作上 hello hello**設定** 索引標籤：

   * 檢視或匯出 hello hello 閘道使用的憑證。
   * 變更 hello hello 閘道使用的 HTTPS 端點。    
   * 設定 hello 閘道使用的 HTTP proxy toobe。     
9. （選擇性）切換 toohello**診斷**索引標籤上，檢查 hello**啟用詳細資訊記錄**選項，如果您想 tooenable 詳細資訊記錄，您可以搭配 tootroubleshoot 任何問題 hello 閘道。 hello 記錄資訊位於**事件檢視器**下**Applications and Services Logs** -> **資料管理閘道器**節點。

    ![[診斷] 索引標籤](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    您也可以執行下列動作，在 hello hello**診斷** 索引標籤：

   * 使用**測試連接**區段 tooan 在內部部署資料來源使用 hello 閘道。
   * 按一下**檢視記錄檔**toosee hello 資料管理閘道會記錄在事件檢視器 視窗中。
   * 按一下**傳送記錄檔**tooupload zip 檔案的最後七天 tooMicrosoft toofacilitate 問題的疑難排解您的記錄檔。
10. 在 hello**診斷**索引標籤上，在 hello**測試連接**區段中，選取**SqlServer** hello 類型 hello 資料存放區中，輸入 hello hello 資料庫伺服器的名稱，名稱hello 資料庫，指定驗證類型，輸入使用者名稱和密碼，然後按一下**測試**tootest hello 閘道是否可連接 toohello 資料庫。
11. 交換器 toohello 網頁瀏覽器，在 hello **Azure 入口網站**，按一下  **確定**上 hello**設定**頁面，然後在 hello**新的資料閘道**頁面。
12. 您應該會看到**adftutorialgateway**下**資料閘道**hello hello 左側的樹狀檢視中。  如果您按一下它，您應該會看到 hello 相關聯的 JSON。

## <a name="create-linked-services"></a>建立連結的服務
在此步驟中，您會建立兩個連結服務：**AzureStorageLinkedService** 和 **SqlServerLinkedService**。 hello **SqlServerLinkedService**連結在內部部署 SQL Server 資料庫和 hello **AzureStorageLinkedService**連結的服務連結的 Azure blob 存放區 toohello 資料 factory。 您稍後在 hello 在內部部署 SQL Server 資料庫 toohello Azure blob 存放區中的資料複製本逐步解說中建立管線。

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a>加入連結的服務 tooan 在內部部署 SQL Server 資料庫
1. 在 hello **Data Factory 編輯器**，按一下 **新建資料存放區**hello 工具列，然後選取**SQL Server**。

   ![新增 SQL Server 連結服務](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. 在 hello **JSON 編輯器**上 hello 右，請勿 hello 下列步驟：

   1. Hello **gatewayName**，指定**adftutorialgateway**。    
   2. 在 hello **connectionString**，執行下列步驟 hello:    

      1. 如**servername**，輸入裝載 hello SQL Server 資料庫的 hello 伺服器 hello 名稱。
      2. 如**databasename**，輸入 hello hello 資料庫名稱。
      3. 按一下**加密**hello 工具列上的按鈕。 您會看見 hello 認證管理員應用程式。

         ![認證管理員應用程式](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. 在 hello**設定認證**對話方塊中，指定驗證類型、 使用者名稱和密碼，然後按一下**確定**。 Hello 連線成功時，如果 hello 加密認證儲存在 hello JSON 和 hello 對話框會關閉。
      5. 關閉 hello 空的瀏覽器索引標籤啟動 hello 對話方塊中，如果它不會自動關閉並取回 toohello 索引標籤以 hello Azure 入口網站。

         這些認證會在 hello 閘道機器上，**加密**服務擁有使用 hello Data Factory 的認證。 如果您想改為與 hello 資料管理閘道器相關聯的 toouse hello 憑證，請參閱[安全地設定認證](#set-credentials-and-security)。    
   3. 按一下**部署**hello 命令列 toodeploy hello 連結的 SQL Server 服務。 您應該會看到 hello 樹狀檢視中的 hello 連結服務。

      ![Hello 樹狀檢視中的 SQL Server 連結服務](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a>新增 Azure 儲存體帳戶的連結服務
1. 在 hello **Data Factory 編輯器**，按一下 **新建資料存放區**在 hello 命令列，然後按一下**Azure 儲存體**。
2. 輸入您的 Azure 儲存體帳戶 hello hello 名稱**帳戶名稱**。
3. 輸入您的 Azure 儲存體帳戶的 hello 金鑰 hello**帳戶金鑰**。
4. 按一下**部署**toodeploy hello **AzureStorageLinkedService**。

## <a name="create-datasets"></a>建立資料集
在此步驟中，您需要建立輸入和輸出資料集代表 hello 複製作業的輸入和輸出資料 (在內部部署 SQL Server 資料庫 = > Azure blob 儲存體)。 然後再建立資料集，請勿 hello （hello 清單之後的詳細的步驟） 的步驟：

* 建立了名為**emp**在 hello 您加入成為連結的服務 toohello data factory 的 SQL Server 資料庫，並插入幾個範例到 hello 資料表的項目。
* 建立名為的 blob 容器**adftutorial**在 hello Azure blob 儲存體帳戶，您加入成為連結的服務 toohello data factory。

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a>在內部部署 SQL Server 準備 hello 教學課程
1. 您所指定的 hello 內部部署 SQL Server 的 hello 資料庫中已連結的服務 (**SqlServerLinkedService**)，使用下列 SQL 指令碼 toocreate hello hello **emp** hello 資料庫資料表中的。

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. Hello 資料表中插入一些範例：

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a>建立輸入資料集

1. 在 hello **Data Factory 編輯器**，按一下  **...多個**，按一下 **新的資料集**hello 命令列，以及按一下**SQL Server 資料表**。
2. Hello 右窗格中的 hello JSON 替換成下列文字的 hello:

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   請注意下列點 hello:

   * **型別**設定得**SqlServerTable**。
   * **tableName**設定得**emp**。
   * **linkedServiceName**設定得**SqlServerLinkedService** （您必須建立此連結的服務稍早在本逐步解說中）。。
   * 對於不由 Azure Data Factory 中的另一個管線產生輸入資料集，您必須設定**外部**太**true**。 它代表 hello 輸入的資料而產生外部 toohello Azure Data Factory 服務。 您可以選擇性地指定外部資料原則使用 hello **externalData** hello 中的項目**原則**> 一節。    

   如需 JSON 屬性的詳細資訊，請參閱[在 SQL Server 來回移動資料](data-factory-sqlserver-connector.md)。
3. 按一下**部署**hello 命令列 toodeploy hello 資料集上。  

### <a name="create-output-dataset"></a>建立輸出資料集

1. 在 hello **Data Factory 編輯器**，按一下 **新的資料集**在 hello 命令列，然後按一下**Azure Blob 儲存體**。
2. Hello 右窗格中的 hello JSON 替換成下列文字的 hello:

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   請注意下列點 hello:

   * **型別**設定得**AzureBlob**。
   * **linkedServiceName**設定得**AzureStorageLinkedService** （您已在步驟 2 中建立這項連結的服務）。
   * **folderPath**設定得**adftutorial/outfromonpremdf** outfromonpremdf 所在 hello adftutorial 容器中的 hello 資料夾。 建立 hello **adftutorial**容器不存在時。
   * hello**可用性**設定得**每小時**(**頻率**設定得**小時**和**間隔**太設定**1**)。  hello Data Factory 服務會產生輸出的資料配量每小時 hello **emp** hello Azure SQL Database 中的資料表。

   如果您未指定**fileName**如**輸出資料表**，hello 中的 hello 產生檔案**folderPath** hello 下列格式命名： 資料。<Guid>。txt (例如:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt。)。

   tooset **folderPath**和**fileName**動態根據 hello **SliceStart**時間，請使用 hello partitionedBy 屬性。 在下列範例的 hello，folderPath 使用年、 月和日 hello SliceStart （hello 正在處理的配量的開始時間） 並檔名使用來自 hello SliceStart 的小時。 例如，如果正在產生配量 2014-10-20T08:00:00，hello folderName 設定 toowikidatagateway/wikisampledataout/2014年/10/20 而且 hello fileName 設定 too08.csv。

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    如需 JSON 屬性的詳細資訊，請參閱[在 Azure Blob 儲存體來回移動資料](data-factory-azure-blob-connector.md)。
3. 按一下**部署**hello 命令列 toodeploy hello 資料集上。 確認您看到兩個 hello 樹狀檢視中的 hello 資料集。  

## <a name="create-pipeline"></a>建立管線
在此步驟中，您會建立一個**管線**，其中包含一個使用 **EmpOnPremSQLTable** 做為輸入和 **OutputBlobTable** 做為輸出的**複製活動**。

1. 在 [Data Factory 編輯器] 中，按一下 **[...更多]** 和 [新增管線]。
2. Hello 右窗格中的 hello JSON 替換成下列文字的 hello:    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > 取代 hello hello 值**啟動**屬性以 hello 目前的日期和**結束**以 hello 隔天的值。
   >
   >

   請注意下列點 hello:

   * 在 [hello 活動] 區段中，沒有只有活動其**類型**設定得**複製**。
   * **輸入**hello 活動設定太**EmpOnPremSQLTable**和**輸出**hello 活動設定太**OutputBlobTable**。
   * 在 [hello **typeProperties** ] 區段中， **SqlSource**指定為 hello**來源類型**和 * * BlobSink * * 指定為 hello**接收器類型**.
   * SQL 查詢`select * from emp`指定 hello **sqlReaderQuery**屬性**SqlSource**。

   開始和結束日期時間都必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。 例如：2014-10-14T16:32:41Z。 hello**結束**時間是選擇性的但我們在本教學課程中使用它。

   如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時**"。 無限期地指定 toorun hello 管線**9/9/9999**為 hello hello 值**結束**屬性。

   您正在定義 hello 的持續時間中的 hello 處理資料配量會根據 hello**可用性**已針對每個 Azure Data Factory 資料集定義的屬性。

   在 hello 範例中，有 24 資料配量每個資料配量會每小時產生。        
3. 按一下**部署**hello 命令列 toodeploy hello 資料集 （資料表是矩形的資料集）。 確認 [hello] 下的樹狀結構檢視中顯示該 hello 管線**管線**節點。  
4. 現在，按一下  **X**兩次 tooclose hello 頁面 tooget 後 toohello **Data Factory**頁面 hello **ADFTutorialOnPremDF**。

**恭喜！** 您已成功建立 Azure data factory、 連結的服務、 資料集和管線和排程的 hello 管線。

#### <a name="view-hello-data-factory-in-a-diagram-view"></a>在圖表檢視中檢視 hello 資料 factory
1. 在 hello **Azure 入口網站**，按一下 **圖表**hello hello 首頁上並排顯示**ADFTutorialOnPremDF**資料 factory。 ：

    ![圖表連結](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. 您應該會看到 hello 圖表類似 toohello 下列映像：

    ![圖表檢視](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    您可以放大、 縮小，縮放 too100%、 縮放 toofit、 自動位置的管線和資料集，並顯示歷程資訊 （反白顯示選取項目的上游及下游項目）。  您可以為其按兩下物件 （輸入/輸出資料集或管線） toosee 屬性。

## <a name="monitor-pipeline"></a>監視管線
在此步驟中，您可以使用 hello Azure 入口網站的 toomonitor Azure data factory 中運作。 您也可以使用 PowerShell cmdlet toomonitor 資料集和管線。 如需監視的詳細資料，請參閱 [監視和管理管線](data-factory-monitor-manage-pipelines.md)。

1. 在 hello 圖表中，按兩下**EmpOnPremSQLTable**。  

    ![EmpOnPremSQLTable 配量](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. 請注意，所有的 hello 資料配量上位於**準備**hello 過去在 hello 管線持續時間 （開始時間 tooend 時間），所以狀態。 它也是因為您已插入 hello SQL Server 資料庫中的 hello 資料就會有所有 hello 時間。 確認任何扇區顯示在 hello**問題配量**hello 底部的區段。 所有 hello 配量中，都按一下 tooview**查看更多**hello hello 清單底端的配量。
3. 現在，在 hello**資料集**頁面上，按一下**OutputBlobTable**。

    ![OputputBlobTable 配量](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. 按一下 從 hello 清單的任何資料分割，您應該會看見 hello**資料配量**頁面。 您會看到活動已執行 hello 配量。 您通常只會看到一個活動執行。  

    ![資料配量刀鋒視窗](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    如果 hello 配量不在 hello**準備**狀態，您可以看到未就緒，並封鎖 hello hello 中執行的目前配量的 hello 上游配量**未就緒的上游配量**清單。
5. 按一下 hello**活動執行**從 hello 清單在 hello 底部 toosee**活動執行詳細資料**。

   ![[活動執行詳細資料] 頁面](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   您會看到資訊，例如輸送量、 期間與 hello 閘道使用 tootransfer hello 資料。
6. 按一下**X** tooclose 所有 hello 直到您的頁面
7. hello 取回 toohello 首頁**ADFTutorialOnPremDF**。
8. (選擇性) 依序按一下 [管線] 及 [ADFTutorialOnPremDF]，然後深入檢視輸入資料表 (**已使用**) 或輸出資料集 (**已產生**)。
9. 使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)tooverify blob/檔案建立的每個小時。

   ![Azure 儲存體總管](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a>後續步驟
* 請參閱[資料管理閘道器](data-factory-data-management-gateway.md)發行項的所有 hello hello 資料管理閘道器的詳細資料。
* 請參閱[資料複製到 Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn 有關 toouse 複製活動 toomove 資料從來源資料如何儲存 tooa 接收資料存放區。
