---
title: "aaaIntroduction tooData 工廠，資料整合服務 |Microsoft 文件"
description: "了解 Azure Data Factory 是什麼：一項雲端資料整合服務，用來協調以及自動移動和轉換資料。"
keywords: "資料整合、雲端資料整合、azure data factory 是什麼"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: cec68cb5-ca0d-473b-8ae8-35de949a009e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 4cc30515315efc938951057743ff8eb3701214ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-data-factory"></a>簡介 tooAzure Data Factory 
## <a name="what-is-azure-data-factory"></a>Azure 資料處理站是什麼？
中巨量資料的 hello world，方式是現有資料中運用商務？ 它是藉由使用參考資料，從內部部署資料來源或其他不同的資料來源產生 hello 雲端中的可能 tooenrich 資料嗎？ 例如，遊戲公司會收集許多遊戲 hello 雲端中所產生的記錄。 想 tooanalyze toocustomer 喜好設定、 人口統計資料、 使用方式行為這些記錄檔 toogain insights 等 tooidentify 向上銷售和交叉銷售機會，開發新的絕佳功能 toodrive 業務成長，並提供更好的體驗toocustomers。 

tooanalyze 這些記錄檔，hello 公司需要 toouse hello 參考資料，例如客戶資訊、 遊戲的資訊，行銷在內部部署資料存放區中的活動資訊。 因此，hello 公司想 tooingest hello 雲端資料存放區中的記錄資料與參考資料，從 hello 在內部部署資料存放區。 然後，利用 Hadoop hello 處理 hello 資料雲端 (Azure HDInsight)，並發行到雲端資料倉儲，例如 Azure SQL 資料倉儲或內部部署資料的資料存放區，例如 SQL Server 的 hello 結果。 它想要這個工作流程 toorun 每週一次。 

需要的是允許的工作流程，可以使用現有的計算服務，例如 Hadoop，內嵌資料從內部部署和雲端資料存放區和轉換或處理序的資料及發行 hello 結果 tooan 內部部署的 hello 公司 toocreate 的平台或 BI 應用程式 tooconsume 的雲端資料儲存區。 

![Data Factory 概觀](media/data-factory-introduction/what-is-azure-data-factory.png) 

Azure Data Factory 是這種案例的 hello 平台。 它是**以雲端為基礎的資料整合服務，可讓您 toocreate 資料驅動型工作流程中 hello 雲端來協調及自動化資料移動及轉換資料**。 使用 Azure Data Factory，您可以建立及排程資料驅動型工作流程 （稱為管線），內嵌來自不同資料存放區的資料、 處理序/轉換 hello 資料使用計算服務，例如 Azure HDInsight Hadoop Spark，Azure 資料湖分析和 Azure Machine Learning 中，並將輸出資料 toodata 存放區，例如 Azure SQL 資料倉儲的商務智慧 (BI) 應用程式 tooconsume 發行。  

它與其說是傳統的擷取-轉換-和-載入 (ETL) 平台，還不如說是擷取並載入 (EL) 而後轉換並載入 (TL) 平台。 hello 轉換的使用計算服務會 tootransform/處理序資料，而不是直接 tooperform 轉換像 hello 的加入衍生的資料行，計算的資料列，排序資料等的數目。 

目前，在 Azure Data Factory，hello 資料取用，且所產生的工作流程會**時間切割資料**（每小時、 每天、 每週、 等等）。 例如，管線可以讀取輸入資料、處理資料，以及每天產生一次輸出資料。 您也可以只執行一次工作流程。  
  

## <a name="how-does-it-work"></a>運作方式 
Azure Data Factory 中的 hello 管線 （資料驅動型工作流程） 通常會執行下列三個步驟的 hello:

![Azure Data Factory 的三個階段](media/data-factory-introduction/three-information-production-stages.png)

### <a name="connect-and-collect"></a>連線及收集
企業會有位於不同來源的各類型資料。 hello 建置資訊生產系統中的第一個步驟是 tooconnect tooall hello 所需的資料來源和處理，SaaS 服務，例如檔案共用、 FTP、 web 服務，並移動 hello 資料視 tooa 集中式位置後續處理程序。

Data Factory 沒有企業必須建置自訂的資料移動元件，或撰寫自訂服務 toointegrate，這些資料來源和處理。 它是高度耗費資源和固定 toointegrate 和維護這類系統中，且它通常缺少 hello 企業等級監視和警示和 hello 控制項可以提供完整受管理的服務。

使用 Data Factory 中，您可以使用 hello 複製活動在資料管線 toomove 資料從這兩個內部部署和雲端來源資料存放區 tooa 集中化資料存放區進行進一步的分析 hello 雲端中。 例如，您可以使用 Azure Data Lake Analytics 計算服務稍後收集 Azure Data Lake Store 和轉換 hello 資料中的資料。 或者，收集 Azure Blob 儲存體中的資料，之後使用 Azure HDInsight Hadoop 叢集來轉換資料。

### <a name="transform-and-enrich"></a>轉換及擴充
一旦資料存在於 hello 雲端中的集中式的資料存放區中，您會想 hello 收集資料 toobe 處理，或藉由計算服務，例如 HDInsight Hadoop、 Spark、 Data Lake Analytics 和機器學習轉換。 您想 tooreliably 產生轉換資料，可維護且受控制的排程 toofeed 生產環境使用信任的資料。 

### <a name="publish"></a>發佈 
已轉換將資料傳送 hello 雲端 tooon 內部部署來源，例如 SQL Server，或將它放在您的雲端儲存體耗用量的來源由商業智慧 (BI) 和分析工具和其他應用程式。

## <a name="key-components"></a>重要元件
Azure 訂用帳戶可能會有一或多個 Azure Data Factory 執行個體 (或資料處理站)。 Azure Data Factory 是由四個主要元件可一起運作 tooprovide hello 平台，您可以撰寫步驟 toomove 和轉換資料的資料驅動型工作流程所組成。 

### <a name="pipeline"></a>管線
資料處理站可以有一或多個管線。 管線是一組活動。 同時，在管線中的 hello 活動執行的工作。 例如，管線無法包含一組活動的內嵌資料從 Azure blob，而然後 HDInsight 叢集 toopartition hello 資料上執行 Hive 查詢。 此設定的 hello 好處是該 hello 管線可讓您 toomanage hello 活動為一組，而不是每個個別。 例如，您可以部署和獨立排程 hello 管線，而不是 hello 活動。 

### <a name="activity"></a>活動
管線可以有一或多個活動。 活動定義 hello 動作 tooperform 對您的資料。 例如，您可以使用複製活動 toocopy 資料從一個資料存放區 tooanother 資料存放區。 同樣地，您可能使用 Hive 活動，其在 Azure HDInsight 叢集 tootransform 上執行 Hive 查詢或分析資料。 Data Factory 支援兩種活動類型︰資料移動活動和資料轉換活動。

### <a name="data-movement-activities"></a>資料移動活動
Data Factory 中的複製活動會將資料從來源資料存放區 tooa 接收資料存放區。 Data Factory 支援下列資料存放區的 hello。 從任何來源的資料可以寫入 tooany 接收。 按一下 資料存放區 toolearn 如何 toocopy 資料 tooand 從該存放區。

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

如需詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)文章。

### <a name="data-transformation-activities"></a>資料轉換活動
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

如需詳細資訊，請參閱[資料轉換活動](data-factory-data-transformation-activities.md)文章。

### <a name="custom-net-activities"></a>自訂 .NET 活動
如果您需要 toomove 資料/從資料存放區的複製活動不支援，或使用您自己的邏輯轉換資料，建立**自訂.NET 活動**。 如需有關建立及使用自訂活動的詳細資料，請參閱 [在 Azure Data Factory 管線中使用自訂活動](data-factory-use-custom-activities.md)。

### <a name="datasets"></a>資料集
活動可取得零或多個資料集作為輸入，並取得一或多個資料集作為輸出。 資料集代表 hello 資料存放區，這只是點，或參考您程式活動中要 toouse 做為輸入或輸出的 hello 資料內的資料結構。 例如，Azure Blob 資料集 hello Azure Blob 儲存體中的 hello 管線應該讀取 hello 資料指定 hello blob 容器和資料夾。 或者，Azure SQL 資料表資料集指定 hello 資料表 toowhich hello 輸出資料寫入 hello 活動。 

### <a name="linked-services"></a>連結的服務
連結的服務非常類似連接字串，定義所需的 Data Factory tooconnect tooexternal 資源 hello 連接資訊中。 將它這種方式-連結的服務定義 hello 連線 toohello 資料來源和資料集代表 hello hello 資料結構。 例如，Azure 儲存體連結服務指定連線字串 tooconnect toohello Azure 儲存體帳戶。 此外，Azure Blob 資料集指定 hello blob 容器和包含 hello 資料 hello 資料夾。   

Data Factory 中的連結服務，有兩個用途：

* toorepresent**資料存放區**包括但不是限於在內部部署 SQL Server、 Oracle 資料庫、 檔案共用或 Azure Blob 儲存體帳戶。 請參閱 hello[資料移動活動](#data-movement-activities)部分支援的資料存放區的清單。
* toorepresent**計算資源**可以裝載 hello 活動執行的。 例如，hello HDInsightHive 活動 HDInsight Hadoop 叢集上執行。 如需支援的計算環境清單，請參閱[資料轉換活動](#data-transformation-activities)一節。

### <a name="relationship-between-data-factory-entities"></a>Data Factory 實體之間的關聯性
![圖表︰Data Factory 概觀 (雲端資料整合服務) - 重要概念](./media/data-factory-introduction/data-integration-service-key-concepts.png)
**圖 2.** 資料集、活動、管線和連結服務之間的關聯性。

## <a name="supported-regions"></a>支援區域
目前，您可以建立 data factory 中 hello**美國西部**，**美國東部**，和**北歐**區域。 不過，資料處理站可以存取資料存放區，並計算其他資料存放區之間的 Azure 區域 toomove 資料中的服務或處理程序使用的資料計算服務。

Azure Data Factory 本身不會儲存任何資料。 它可讓您建立資料驅動型工作流程 tooorchestrate 之間資料移動的[支援資料存放區](#data-movement-activities)和處理的資料使用[計算服務](#data-transformation-activities)內部或其他區域中環境。 它也可讓您太[監視和管理工作流程](data-factory-monitor-manage-pipelines.md)同時以程式設計方式使用和 UI 機制。

即使 Data Factory 僅提供**美國西部**，**美國東部**，和**北歐**區域，電源 hello Data Factory 中的資料移動的 hello 服務可供使用[全域](data-factory-data-movement-activities.md#global)數個區域中。 如果資料存放區是在防火牆後面，則[資料管理閘道器](data-factory-move-data-between-onprem-and-cloud.md)改為安裝在內部部署環境移動 hello 資料中。

如需範例，讓我們假設您的計算環境 (例如 Azure HDInsight 叢集和 Azure 機器學習服務) 即將用盡西歐區域的資源。 您可以建立和使用 Azure Data Factory 中的執行個體北歐和使用它 tooschedule 作業在西歐中計算環境。 毫秒幾個 Data Factory tootrigger hello 作業於您的運算環境，但不會變更執行 hello 作業上您的運算環境的 hello 時間。

## <a name="get-started-with-creating-a-pipeline"></a>開始建立管線
您可以使用這些工具或 Api toocreate 資料管線的其中一個 Azure Data Factory 中： 

- Azure 入口網站
- Visual Studio
- PowerShell
- .NET API
- REST API
- Azure Resource Manager 範本。 

toolearn 資料 toobuild data factory 管線的方式，請依照下列 hello 遵循教學課程中的逐步指示：

| 教學課程 | 說明 |
| --- | --- |
| [在兩個雲端資料存放區之間移動資料](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) |在本教學課程中，您建立 data factory 管線，**移動資料**從 Blob 儲存體 tooSQL 資料庫。 |
| [使用 Hadoop 叢集轉換資料](data-factory-build-your-first-pipeline.md) |在本教學課程中，您會在 Azure HDInsight (Hadoop) 叢集上執行 Hive 指令碼，以建立您的第一個 Azure Data Factory 與用來 **處理資料** 的資料管線。 |
| [使用資料管理閘道，在內部部署資料存放區與雲端資料存放區之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) |在此教學課程中，您建立具有管線的 data factory 的**移動資料**從**內部**SQL Server 資料庫 tooan Azure blob。 Hello 逐步解說中，您可以安裝並設定 hello 資料管理閘道器電腦上。 |
