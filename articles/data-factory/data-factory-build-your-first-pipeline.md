---
title: "Data Factory 教學課程︰第一個資料管線 | Microsoft Docs"
description: "此 Azure Data Factory 教學課程會示範如何 toocreate 和排程處理使用 Hive 資料的資料處理站上的指令碼的 Hadoop 叢集。"
services: data-factory
keywords: "azure data factory 教學課程, hadoop 叢集, hadoop hive"
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: ed9c0ade4500d4ac1f7c2c2312c1fa675e0b1f02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-pipeline-tootransform-data-using-hadoop-cluster"></a>教學課程： 建立第一個管線 tootransform 資料使用 Hadoop 叢集
> [!div class="op_single_selector"]
> * [概觀和必要條件](data-factory-build-your-first-pipeline.md)
> * [Azure 入口網站](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager 範本](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

在本教學課程中，您會使用資料管線建立您的第一個 Azure Data Factory。 hello 管線的 Azure HDInsight (Hadoop) 叢集 tooproduce 輸出資料上執行 Hive 指令碼轉換輸入的資料。  

本文章提供概觀和 hello 教學課程的必要條件。 完成 hello 必要條件之後，您可以使用其中一種下列 Sdk 工具/hello hello 教學課程： Azure 入口網站，Visual Studio、 PowerShell、 REST API 資源管理員範本。 選取其中一個 hello 選項 hello hello 開頭 （或） 連結的下拉式清單中使用這些選項的其中一個本文章 toodo hello 教學課程的 hello 結尾。    

## <a name="tutorial-overview"></a>教學課程概觀
在本教學課程中，您要執行 hello 下列步驟：

1. 建立 **Data Factory**。 資料處理站可以包含一或多個資料管線，可移動和轉換資料。 

    在本教學課程中，您可以建立 hello data factory 中的一個管線。 
2. 建立 **管線**。 管線可以有一或多個活動 (範例︰複製活動、HDInsight Hive 活動)。 這個範例會使用 hello HDInsight Hive 活動在 HDInsight Hadoop 叢集上執行 Hive 指令碼。 hello 指令碼會先建立參考 hello 原始 web 記錄資料儲存在 Azure blob 儲存體中的資料表和資料分割再依據年和月 hello 未經處理資料。

    在本教學課程，hello 管線會使用 Azure HDInsight Hadoop 叢集上執行 Hive 查詢 hello Hive 活動 tootransform 資料。 
3. 建立 **連結服務**。 您可以建立連結的服務 toolink 資料存放區或計算服務 toohello data factory。 資料存放區，例如 Azure 儲存體保存 hello 管線中的輸入/輸出資料的活動。 計算服務 (例如 HDInsight Hadoop 叢集) 會處理/轉換資料。

    在本教學課程中，您會建立兩個「連結服務」：**Azure 儲存體** 和 **Azure HDInsight**。 hello Azure 儲存體連結服務連結保存 hello 輸入/輸出資料 toohello 資料處理站的 Azure 儲存體帳戶。 Azure HDInsight 連結服務連結是使用的 tootransform 資料 toohello 資料處理站的 Azure HDInsight 叢集。 
3. 建立輸入和輸出 **資料集**。 輸入資料集代表 hello hello 管線中活動的輸入和輸出資料集代表 hello hello 活動的輸出。

    在此教學課程、 hello 輸入和輸出資料集指定位置的輸入和輸出資料中的 hello Azure Blob 儲存體。 hello Azure 儲存體連結服務指定 Azure 儲存體帳戶使用。 輸入資料集指定 hello 輸入的檔案的位置而輸出資料集指定 hello 輸出檔案會放置於其中。 


請參閱[簡介 tooAzure Data Factory](data-factory-introduction.md)的 Azure Data Factory 的發行項的詳細概觀。
  
以下是 hello**圖表檢視**您在本教學課程中建立的 hello 範例資料處理站。 **MyFirstPipeline** 有一個 Hive 類型的活動，可接收 **AzureBlobInput** 資料集做為輸入，並輸出 **AzureBlobOutput** 資料集。 

![Data Factory 教學課程中的圖表檢視](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


在本教學課程， **inputdata**資料夾 hello **adfgetstarted** Azure blob 容器包含一個名為 input.log 的檔案。 此記錄檔包含三個月的項目，分別是：2016 年 1 月、2 月和 3 月。 以下是每個月 hello 範例資料列 hello 輸入檔中。 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

HDInsight Hive 活動與 hello 管線處理 hello 檔案時，hello 活動執行 Hive 指令碼 hello HDInsight 叢集上的資料分割輸入資料，依年份和月份。 hello 指令碼會建立三個包含每個月中的項目與檔案的輸出資料夾。  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

Hello 範例列如上所示，從 hello 第一次一個 （具有 2016年-01-01) toohello 000000_0 檔案以寫入 hello 月 = 1 的資料夾。 同樣地，hello 第二個 toohello 檔案以寫入 hello 月 = 2 的資料夾和 hello 其中一個第三個撰寫 toohello 檔案的 hello 月 = 3 資料夾。  

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須具備下列必要條件 hello:

1. **Azure 訂用帳戶** - 如果您沒有 Azure 訂用帳戶，只需要幾分鐘就可以建立免費試用帳戶。 請參閱 hello[免費試用](https://azure.microsoft.com/pricing/free-trial/)如何取得免費的試用帳戶上的發行項。
2. **Azure 儲存體**– 您將 hello 資料儲存在本教學課程使用一般用途的標準 Azure 儲存體帳戶。 如果您沒有通用標準的 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)發行項。 建立 hello 儲存體帳戶之後，記下 hello**帳戶名稱**和**便捷鍵**。 請參閱 [檢視、複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys)。
3. 下載並檢閱 hello Hive 查詢檔案 (**HQL**) 位於： [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql)。 此查詢來轉換輸入的資料 tooproduce 輸出資料。 
4. 下載並檢閱 hello 範例輸入的檔 (**input.log**) 位於： [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)
5. 在您的 Azure Blob 儲存體中建立名為 **adfgetstarted** 的 Blob 容器。 
6. 上傳**partitionweblogs.hql**檔案 toohello**指令碼**資料夾中 hello **adfgetstarted**容器。 使用類似 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)的工具。 
7. 上傳**input.log**檔案 toohello **inputdata**資料夾中 hello **adfgetstarted**容器。 

完成 hello 必要條件之後，選取其中一個 hello Sdk 工具/toodo hello 教學課程： 

- [Azure 入口網站](data-factory-build-your-first-pipeline-using-editor.md)
- [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
- [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
- [Resource Manager 範本](data-factory-build-your-first-pipeline-using-arm.md)
- [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

Azure 入口網站和 Visual Studio 可讓您透過 GUI 建置資料處理站。 而 PowerShell、Resource Manager 範本和 REST API，則可讓您選擇以撰寫指令碼/程式碼的方式來建置資料處理站。

> [!NOTE]
> 在此教學課程中的 hello 資料管線轉換輸入的資料 tooproduce 輸出資料。 它不會複製資料來源建立資料存放區 tooa 目的地資料存放區。 如需如何使用 Azure Data Factory，toocopy 資料，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。
> 
> 您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱[在 Data Factory 中排程和執行](data-factory-scheduling-and-execution.md)。 





  
