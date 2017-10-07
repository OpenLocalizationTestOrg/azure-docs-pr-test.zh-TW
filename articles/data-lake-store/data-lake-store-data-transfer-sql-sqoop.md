---
title: "資料湖存放區和 Sqoop Azure SQL database 之間的 aaaCopy 資料 |Microsoft 文件"
description: "使用 Azure SQL Database 與資料湖存放區之間的 Sqoop toocopy 資料"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a>使用 Sqoop 在 Data Lake Store 和 Azure SQL Database 之間複製資料
深入了解如何 toouse Apache Sqoop tooimport 和匯出資料與 Azure SQL Database 資料湖存放區。

## <a name="what-is-sqoop"></a>什麼是 Sqoop？
巨量資料應用程式是處理非結構化和半結構化資料 (例如記錄和檔案)，很自然的一個選擇。 不過，可能也有需要 tooprocess 結構化資料儲存在關聯式資料庫中。

[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html)是設計工具 tootransfer 關聯式資料庫和巨量資料儲存機制，例如資料湖存放區之間的資料。 您可以使用它從關聯式資料庫管理系統 (RDBMS) 例如 Azure SQL Database 的 tooimport 資料至資料湖存放區。 您可以再轉換和分析使用巨量資料工作負載的 hello 資料然後回 RDBMS 匯出 hello 資料。 在本教學課程中，您可以使用 Azure SQL Database 為您關聯式資料庫 tooimport/從匯出。

## <a name="prerequisites"></a>必要條件
在開始這份文件之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure Data Lake Store 帳戶**。 如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)
* **Azure HDInsight 叢集**與存取 tooa Data Lake Store 帳戶。 請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。 本文假設您已使用 Data Lake Store 存取 HDInsight Linux 叢集。
* **Azure SQL Database**。 如需有關指示 toocreate 一個，請參閱[建立 Azure SQL database](../sql-database/sql-database-get-started.md)

## <a name="do-you-learn-fast-with-videos"></a>使用影片快速學習？
[觀賞此視訊](https://mix.office.com/watch/1butcdjxmu114)如何與 Azure 儲存體 Blob 資料湖存放區使用 DistCp toocopy 資料。

## <a name="create-sample-tables-in-hello-azure-sql-database"></a>在 hello Azure SQL Database 中建立範例資料表
1. toostart，hello Azure SQL Database 中建立兩個範例資料表。 使用[SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md)或 Visual Studio tooconnect toohello Azure SQL Database 執行的 hello 然後遵從查詢。

    **建立 Table1**

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    **建立 Table2**

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. 在 **Table1**中，新增一些範例資料。 保留 **Table2** 空白。 我們從 **Table1** 匯入資料至 Data Lake Store。 然後，我們會從 Data Lake Store 將資料匯出到 **Table2**。 執行下列程式碼片段的 hello。

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a>從與 HDInsight 叢集使用 Sqoop 存取 tooData 湖存放區
HDInsight 叢集已有可用的 hello Sqoop 封裝。 如果您已設定 hello HDInsight 叢集 toouse 資料湖存放區做為額外的存放裝置，您可以使用關聯式資料庫 （在此範例中，Azure SQL Database） 之間 （不含任何組態變更） 的 Sqoop tooimport/匯出資料和資料湖存放區帳戶。

1. 此教學課程中，我們假設您建立 Linux 叢集，因此您應該使用 SSH tooconnect toohello 叢集。 請參閱[連接 tooa 以 Linux 為基礎的 HDInsight 叢集](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)。
2. 請確認您是否可以從 hello 叢集存取 hello Data Lake Store 帳戶。 執行 hello hello SSH 提示字元中的下列命令：

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    這樣應該會提供一份 hello Data Lake Store 帳戶中的檔案/資料夾。

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a>從 Azure SQL Database 將資料匯入至 Data Lake Store
1. 瀏覽 toohello 目錄有可用 Sqoop 封裝。 一般而言，這會在 `/usr/hdp/<version>/sqoop/bin`。
2. Hello 資料匯入**Table1**到 hello Data Lake Store 帳戶。 使用下列語法的 hello:

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    請注意， **sql 資料庫的伺服器名稱**預留位置代表 hello hello hello Azure SQL 資料庫正在執行的伺服器的名稱。 **sql 資料庫名稱**預留位置代表 hello 實際資料庫名稱。

    例如，


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. 確認資料已該 hello 轉移 toohello Data Lake Store 帳戶。 執行下列命令的 hello:

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    您應該會看到下列輸出的 hello。


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    每個**一部分-m-*** 檔案對應 tooa hello 來源資料表中的資料列**Table1**。 您可以檢視 hello 內容 hello 組件-m-* 檔案 tooverify。


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a>從 Data Lake Store 將資料匯出到 Azure SQL Database
1. Data Lake Store 帳戶 toohello 空白資料表，從匯出 hello 資料**Table2**，hello Azure SQL Database 中。 使用下列語法的 hello。

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    例如，


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. 請確認該 hello 資料已上傳 toohello SQL Database 的資料表。 使用[SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md)或 Visual Studio tooconnect toohello Azure SQL Database 執行的 hello 然後遵從查詢。

        SELECT * FROM TABLE2

    這應該 hello 遵循輸出。

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a>使用 Sqoop 時的效能考量

如需效能微調您的 Sqoop 工作 toocopy 資料 tooData 湖存放區，請參閱[Sqoop 效能文件](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)。

## <a name="see-also"></a>另請參閱
* [從 Azure 儲存體 Blob tooData 湖存放區複製資料](data-lake-store-copy-data-azure-storage-blob.md)
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
* [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配 Data Lake Store 使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)
