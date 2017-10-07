---
title: "從 Blob 儲存體 tooSQL 資料庫-Azure aaaCopy 資料 |Microsoft 文件"
description: "本教學課程會示範如何 toouse 複製活動中的 Azure Data Factory 管線 toocopy 從 Blob 儲存體 tooSQL 資料庫的資料。"
keywords: "blob sql, blob 儲存體, 資料複製"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a>教學課程： 將資料從 Blob 儲存體 tooSQL 使用 Data Factory 的資料庫複製
> [!div class="op_single_selector"]
> * [概觀和必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [複製精靈](data-factory-copy-data-wizard-tutorial.md)
> * [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager 範本](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

在本教學課程中，您可以建立 data factory 管線 toocopy 資料從 Blob 儲存體 tooSQL 資料庫。

hello 複製活動會在 Azure Data Factory 中執行 hello 資料移動。 此活動是由全域可用的服務所提供，可以使用安全、可靠及可調整的方式，在各種不同的資料存放區之間複製資料。 請參閱[資料移動活動](data-factory-data-movement-activities.md)hello 複製活動的詳細資料的發行項。  

> [!NOTE]
> Hello Data Factory 服務的詳細概觀，請參閱 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項。
>
>

## <a name="prerequisites-for-hello-tutorial"></a>Hello 教學課程的必要條件
開始本教學課程之前，您必須具備下列必要條件 hello:

* **Azure 訂用帳戶**。  如果您沒有訂用帳戶，則只需要幾分鐘的時間就可以建立免費試用帳戶。 請參閱 hello[免費試用版](http://azure.microsoft.com/pricing/free-trial/)文件以取得詳細資料。
* **Azure 儲存體帳戶**。 您使用做為 hello blob 儲存體**來源**資料儲存在本教學課程。 如果您沒有 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)步驟 toocreate 其中一個發行項。
* **Azure SQL Database**。 在本教學課程中，您會使用 Azure SQL Database 做為 **目的地** 資料存放區。 如果您沒有 Azure SQL database 可讓您在 hello 教學課程，請參閱[如何 toocreate 及設定 Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate 其中一個。
* **SQL Server 2012/2014 或 Visual Studio 2013**。 您可以使用 SQL Server Management Studio 或 Visual Studio toocreate 範例資料庫和 tooview hello 結果資料 hello 資料庫中。  

## <a name="collect-blob-storage-account-name-and-key"></a>收集 Blob 儲存體帳戶名稱和金鑰
您需要 hello 帳戶名稱和帳戶金鑰，您的 Azure 儲存體帳戶 toodo 本教學課程。 記下 Azure 儲存體帳戶的**帳戶名稱**和**帳戶金鑰**。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下**更多服務**上 hello 功能表，然後選取左**儲存體帳戶**。

    ![瀏覽 - 儲存體帳戶](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. 在 [hello**儲存體帳戶**刀鋒視窗中，選取 hello **Azure 儲存體帳戶**的 toouse 在本教學課程。
4. 選取 [設定] 底下的 [存取金鑰] 連結。
5. 按一下**複製**（圖像） 下一步按鈕太**儲存體帳戶名稱**文字並儲存/貼上它某處 (例如： 文字檔案中)。
6. 重複上一個步驟 toocopy hello 」 或 「 記下 hello **key1**。

    ![儲存體存取金鑰](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. 按一下 [關閉所有 hello 刀鋒視窗**X**。

## <a name="collect-sql-server-database-user-names"></a>收集 SQL Server、資料庫、使用者名稱
本教學課程需要的 Azure SQL server、 資料庫和使用者 toodo hello 名稱。 記下 Azure SQL Database 的**伺服器**、**資料庫**和**使用者**名稱。

1. 在 [hello **Azure 入口網站**，按一下 [**更多服務**上 hello，然後選取**SQL 資料庫**。
2. 在 [hello **SQL 資料庫刀鋒視窗**，選取 hello**資料庫**的 toouse 在本教學課程。 記下 hello**資料庫名稱**。  
3. 在 [hello **SQL database**刀鋒視窗中，按一下 [**屬性**下**設定**。
4. 記下 hello 值**伺服器名稱**和**SERVER 系統管理員登入**。
5. 按一下 [關閉所有 hello 刀鋒視窗**X**。

## <a name="allow-azure-services-tooaccess-sql-server"></a>允許 Azure 服務 tooaccess SQL server
請確認**tooAzure 服務允許存取**設定**ON** Azure SQL server 讓該 hello Data Factory 服務能夠存取您的 Azure SQL server。 tooverify 並開啟此設定，下列步驟 hello:

1. 按一下**更多服務**hello 左側，按一下中樞**SQL 伺服器**。
2. 選取您的伺服器，然後按一下 [設定] 下的 [防火牆]。
3. 在 [hello**防火牆設定**刀鋒視窗中，按一下**ON**如**tooAzure 服務允許存取**。
4. 按一下 [關閉所有 hello 刀鋒視窗**X**。

## <a name="prepare-blob-storage-and-sql-database"></a>準備 Blob 儲存體和 SQL Database
現在，執行備妥您的 Azure blob 儲存體和 Azure SQL database hello 教學課程步驟的 hello:  

1. 啟動 [記事本]。 複製下列文字的 hello，並將它儲存成**emp.txt**太**C:\ADFGetStarted**硬碟機上的資料夾。

    ```
    John, Doe
    Jane, Doe
    ```
2. 使用工具，例如[Azure 儲存體總管](http://storageexplorer.com/)toocreate hello **adftutorial**容器和 tooupload hello **emp.txt**檔案 toohello 容器。

    ![Azure 儲存體總管。 從 Blob 儲存體 tooSQL 資料庫複製資料](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. 使用下列 SQL 指令碼 toocreate hello 的 hello **emp**您 Azure SQL Database 中的資料表。  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    **如果您有 SQL Server 2012/2014 安裝在電腦上：**遵循指示從[管理 Azure SQL Database 使用 SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour SQL Azure 伺服器，然後執行 hello SQL 指令碼。 本文使用 hello[傳統 Azure 入口網站](http://manage.windowsazure.com)，不 hello[新版 Azure 入口網站](https://portal.azure.com)，Azure SQL 伺服器的 tooconfigure 防火牆。

    如果您的用戶端不允許 tooaccess hello Azure SQL server，您需要 tooconfigure 防火牆 tooallow 存取您 Azure SQL server 從您的電腦 （IP 位址）。 請參閱[本文](../sql-database/sql-database-configure-firewall-settings.md)步驟 tooconfigure hello 防火牆 Azure SQL server。

## <a name="create-a-data-factory"></a>建立 Data Factory
您已完成 hello 必要條件。 您可以建立使用下列方式 hello 其中的資料處理站。 按一下其中一個 hello 頂端或 hello 連結 tooperform hello 教學課程的 hello 下拉式清單中的 hello 選項。     

* [複製精靈](data-factory-copy-data-wizard-tutorial.md)
* [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
* [Azure Resource Manager 範本](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
* [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> 在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。 它不會轉換輸入的資料 tooproduce 輸出資料。 如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立第一個管線 tootransform 資料使用 Hadoop 叢集](data-factory-build-your-first-pipeline.md)。
> 
> 您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱[在 Data Factory 中排程和執行](data-factory-scheduling-and-execution.md)。 
