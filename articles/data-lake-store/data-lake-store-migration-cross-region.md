---
title: "Data Lake Store 跨區域移轉 aaaAzure |Microsoft 文件"
description: "了解 Azure Data Lake Store 跨區域移轉指引。"
services: data-lake-store
documentationcenter: 
author: swums
manager: amitkul
editor: swums
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/27/2017
ms.author: stewu
ms.openlocfilehash: 561ac821c1bd555886035867678cb685997564eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-data-lake-store-across-regions"></a>跨區域移轉 Data Lake Store

Azure 資料湖存放區可用時在新的區域中，您可以選擇 toodo 一次移轉，tootake hello 新區域的優點。 當您計劃，並完成 hello 移轉，請了解哪些 tooconsider。

## <a name="prerequisites"></a>必要條件

* **Azure 訂用帳戶**。 如需詳細資訊，請參閱[立即建立免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。
* **兩個不同區域中的 Data Lake Store 帳戶**。 如需詳細資訊，請參閱[開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)。
* **Azure Data Factory**。 如需詳細資訊，請參閱[簡介 tooAzure Data Factory](../data-factory/data-factory-introduction.md)。


## <a name="migration-considerations"></a>移轉考量

首先，識別最適合您的應用程式寫入、 讀取，或處理資料的資料湖存放區中的 hello 移轉策略。 當您選擇的策略時，請考慮您的應用程式可用性需求，以及在移轉期間發生的 hello 停機時間。 例如，最簡單的方式可能 toouse hello"增益 shift 」 雲端移轉模型。 這種方法，您暫停 hello 應用程式中現有的區域時，所有資料複製 toohello 新區域。 Hello 複製程序完成時，您會繼續在 hello 新區域中，您的應用程式，然後再刪除 hello 舊的 Data Lake Store 帳戶。 需要 hello 移轉期間的停機時間。

tooreduce 停機時間，您可能會立即開始擷取 hello 新的區域中的新資料。 當您擁有 hello 所需的最小資料時，請在 hello 新區域中執行應用程式。 Hello 背景中繼續閱讀 hello 新區域 toocopy hello 現有 Data Lake Store 帳戶 toohello 新 Data Lake Store 帳戶從較舊的資料。 使用這種方法，您可以進行 hello 交換器 toohello 新區域與短停機時間。 已複製所有的 hello 較舊的資料，刪除舊 Data Lake Store 帳戶 hello。

規劃移轉時，其他的重要詳細資料 tooconsider 如下：

* **資料量**。 hello （以 gb 為單位，hello 數目檔案和資料夾，以及等等） 的資料數量會影響 hello 時間和 hello 移轉所需的資源。

* **Data Lake Store 帳戶名稱**。 hello 新的區域中 hello 新帳戶名稱必須是全域唯一的。 例如，您的舊 Data Lake Store 帳戶在美國東部 2 的 hello 名稱可能是 contosoeastus2.azuredatalakestore.net。 您可能會將歐盟北部的新 Data Lake Store 帳戶命名為 contosonortheu.azuredatalakestore.net。

* **工具**。 我們建議您改用 hello [Azure 資料 Factory 複製活動](../data-factory/data-factory-azure-datalake-connector.md)toocopy Data Lake Store 檔案。 Data Factory 支援高效能與可靠性的資料移動。 請注意，只有 hello 資料夾階層和 hello 檔案的內容，會複製 Data Factory。 您需要 toomanually 套用任何您在 hello 舊帳戶 toohello 新帳戶中使用的存取控制清單 (Acl)。 如需詳細資訊，包括效能目標最佳狀況案例中，請參閱 hello[複製活動效能及微調指南](../data-factory/data-factory-copy-activity-performance.md)。 如果您想要更快速地複製的資料，您可能需要 toouse 其他雲端資料移動的單位。 AdlCopy 等其他工具不支援在區域之間複製資料。  

* **頻寬費用**。 適用[頻寬費用](https://azure.microsoft.com/en-us/pricing/details/bandwidth/)，因為資料會傳出 Azure 區域。

* **資料的 ACL**。 套用 Acl toofiles 和資料夾，以保護您 hello 新區域的資料。 如需詳細資訊，請參閱[在 Azure Data Lake Store 中保護資料](data-lake-store-secure-data.md)。 我們建議您使用 hello 移轉 tooupdate，並調整您的 Acl。 您可能想 toouse 類似 tooyour 目前設定。 您可以檢視所套用的 tooany 檔案使用 hello Azure 入口網站的 hello Acl [PowerShell cmdlet](/powershell/module/azurerm.datalakestore/get-azurermdatalakestoreitempermission)，或 Sdk。  

* **分析服務的位置**。 為了達到最佳效能，您的分析服務，例如 Azure Data Lake Analytics 或 Azure HDInsight 應該在 hello 與您的資料相同的區域。  

## <a name="next-steps"></a>後續步驟
* [Azure Data Lake Store 概觀](data-lake-store-overview.md)
