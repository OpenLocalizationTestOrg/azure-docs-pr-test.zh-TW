---
title: "aaaUse 案例的客戶程式碼剖析"
description: "了解 Azure Data Factory 的使用的資料驅動的 toocreate 工作流程 （管線） tooprofile 遊戲客戶的方式。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 47f5e77242366c80cce2a2db65e3c696505b3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---customer-profiling"></a>使用案例 - 客戶分析
Azure Data Factory 是許多使用服務 tooimplement hello 解決方案加速器 Cortana 智慧套件。  如需 Cortana Intelligence 的詳細資訊，請瀏覽 [Cortana Intelligence 套件](http://www.microsoft.com/cortanaanalytics)。 我們在本文件說明簡單的使用案例的 toohelp 開始了解如何 Azure Data Factory 可以解決常見分析的問題。

## <a name="scenario"></a>案例
Contoso 是為多個平台建立遊戲的遊戲公司，包含遊戲主機、手持裝置與個人電腦 (PC)。 因為播放程式播放這些遊戲，大量的記錄檔資料會產生追蹤 hello 使用模式、 遊戲樣式和 hello 使用者喜好設定。  結合人口統計的地區和產品的資料，Contoso 可以執行分析 tooguide 如何 tooenhance 玩家的體驗和升級的目標以及遊戲中購買。 

Contoso 的目標是根據其播放程式的 hello 遊戲記錄 tooidentify 向上銷售/交叉銷售商機加入令人信服功能 toodrive 業務成長和提供更好的體驗 toocustomers。 在此使用案例中，我們使用遊戲公司做為企業範例。 hello 公司想 toooptimize 根據玩家的行為及其遊戲。 這些原則套用想 tooengage tooany 商務周圍其產品和服務客戶，並增強其客戶的經驗。

在此解決方案中，Contoso 希望 tooevaluate hello 有效性的行銷活動，它最近已啟動。 我們開始 hello 未經處理的遊戲記錄檔，處理程序和擴充它們與地理位置資料、 聯結與廣告參考資料，最後將其複製到 Azure SQL Database tooanalyze hello 活動造成影響。

## <a name="deploy-solution"></a>部署解決方案
所有您需要 tooaccess，試用這個簡單的使用案例是[Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)、 [Azure Blob 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)，和[Azure SQL Database](../sql-database/sql-database-get-started.md)。 部署程式碼剖析管線就會從 hello hello 客戶**範例管線**的 data factory 的 hello 首頁上並排顯示。

1. 建立 Data Factory 或開啟現有的 Data Factory。 請參閱[從 Blob 儲存體 tooSQL 資料庫使用 Data Factory 複製資料](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)如步驟 toocreate data factory。
2. 在 hello **DATA FACTORY** hello data factory，刀鋒視窗中按一下 hello**範例管線**磚。

    ![範例管線圖格](./media/data-factory-samples/SamplePipelinesTile.png)
3. 在 hello**範例管線**刀鋒視窗中，按一下 hello**客戶程式碼剖析**想 toodeploy。

    ![範例管線刀鋒視窗](./media/data-factory-samples/SampleTile.png)
4. 指定 hello 範例的組態設定。 例如，您的 Azure 儲存體帳戶名稱和金鑰、Azure SQL 伺服器名稱、資料庫、使用者 ID 和密碼。

    ![範例刀鋒視窗](./media/data-factory-samples/SampleBlade.png)
5. 您指定 hello 組態設定完成之後，請按一下**建立**toocreate/部署 hello 範例管線與連結的服務/資料表 hello 管線所使用。
6. 您會看到部署的 hello 狀態 hello 範例磚，在您按一下先前 hello**範例管線**刀鋒視窗。

    ![部署狀態](./media/data-factory-samples/DeploymentStatus.png)
7. 當您看到 hello**部署成功**hello 磚 hello 範例中，關閉 hello 訊息**範例管線**刀鋒視窗。  
8. 在**DATA FACTORY**您刀鋒視窗中，查看已連結的服務、 資料集和管線新增 tooyour 資料 factory。  

    ![Data Factory 刀鋒視窗](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a>解決方案概觀
這個簡單的使用案例可以用做為範例，如何使用 Azure Data Factory tooingest、 準備、 轉換、 分析，並將資料發行。

![端對端工作流程](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

此圖說明 hello 資料管線之後出現的樣子 hello 在 Azure 入口網站已部署。

1. hello **PartitionGameLogsPipeline**從 blob 儲存體讀取 hello 未經處理的遊戲事件，並建立根據年、 月和日的資料分割。
2. hello **EnrichGameLogsPipeline**聯結與地理程式碼參考資料的資料分割遊戲事件，並藉由對應 IP 位址 toohello 相對應的地理位置豐富 hello 資料。
3. hello **AnalyzeMarketingCampaignPipeline**管線使用豐富的 hello 資料，並處理以 hello 廣告資料 toocreate hello 最終輸出包含行銷活動效果。

在此範例中，資料處理站會是複製輸入的資料、 轉換和處理 hello 資料，並輸出 hello 最終資料 tooan Azure SQL Database 的使用的 tooorchestrate 活動。  您也可以視覺化的資料管線 hello 網路、 管理它們，和監視其狀態從 hello UI。

## <a name="benefits"></a>優點
藉由最佳化其使用者設定檔的分析，並符合商務目標、 遊戲公司無法 tooquickly 收集的使用模式，並分析 hello 行銷活動最佳化其效能。

