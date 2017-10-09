---
title: "aaaData 原廠使用案例-產品建議"
description: "了解使用 Azure Data Factory 以及其他服務所實作的使用案例。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6f1523c7-46c3-4b8d-9ed6-b847ae5ec4ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d7912965fe4762d64e8ca3c28381ea6187f36631
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---product-recommendations"></a>使用案例 - 產品建議
Azure Data Factory 是許多使用服務 tooimplement hello 解決方案加速器 Cortana 智慧套件。  請參閱 [Cortana Intelligence 套件](http://www.microsoft.com/cortanaanalytics) 頁面以了解這個套件的詳細資料。 在本文中，我們描述 Azure 使用者已經使用 Azure Data Factory 和其他 Cortana Intelligence 元件服務解決與實作的常見使用案例。

## <a name="scenario"></a>案例
線上零售商通常想 tooentice 其客戶 toopurchase 產品最有可能 toobe 感興趣，並因此最有可能 toobuy 它們呈現它們的產品。 tooaccomplish，線上零售商需要 toocustomize 他們的使用者的線上使用經驗的該特定使用者使用個人化的產品的建議。 這些個人化的建議事項 toobe 依據其目前和歷史購物行為資料，產品資訊、 進行新導入品牌，並且產品及客戶的分割資料。  此外，它們可以提供根據分析，其結合的所有使用者的整體使用狀況行為的 hello 使用者產品建議。

這些零售商的 hello 目標是使用者按一下為銷售轉換 toooptimize 並獲得更高的銷售營收。  他們透過根據客戶興趣和動作提供關聯式、以行為為基礎的產品建議來達成此轉換。 針對這個使用案例，我們會使用線上零售商作為範例，以其客戶想 toooptimize 的企業。 不過，這些原則套用想 tooengage tooany 商務周圍其產品和服務客戶，和加強客戶購買體驗個人化的產品建議。

## <a name="challenges"></a>挑戰
有許多挑戰該線上零售商字體時嘗試 tooimplement 這種類型的使用案例。 

首先，必須 ingested 不同大小和形狀的資料從多個資料來源，這兩個內部部署和 hello 雲端中。 此資料包括產品資料、 客戶歷年行為資料，以及使用者資料，如 hello 使用者瀏覽 hello 線上零售站台。 

第二，必須合理及準確計算和預測個人化的產品建議。 此外 tooproduct、 品牌和客戶問題和瀏覽器資料線上零售商也會需要 hello 最佳產品建議 hello 判斷在過去的購買 toofactor tooinclude 客戶回函 hello 使用者。 

第三，hello 建議必須立即交付項目 toohello 使用者 tooprovide 順暢瀏覽和購買體驗，並提供 hello 最新的和相關建議。 

最後，零售商 toomeasure hello 效益的方法需要藉由追蹤整體向上銷售和交叉銷售的銷售按一下要轉換的成功，並調整 tootheir 未來的建議。

## <a name="solution-overview"></a>解決方案概觀
此範例使用案例已被實際的 Azure 使用者透過使用 Azure Data Factory 及其他 Cortana Intelligence 元件服務 (包括 [HDInsight](https://azure.microsoft.com/services/hdinsight/) 和 [Power BI](https://powerbi.microsoft.com/)) 來解決並實作。

hello 線上零售店會做為其資料儲存選項，整個 hello 工作流程中使用 Azure Blob 存放區、 內部部署 SQL server、 Azure SQL DB、 和關聯式資料超市。  hello blob 存放區包含客戶資訊、 客戶行為資料和產品資訊的資料。 資料包含產品品牌資訊和產品類別目錄的 hello 產品資訊會儲存在內部部署 SQL 資料倉儲中。 

所有的 hello 資料結合，送入 hello 使用者瀏覽 hello hello 網站上的目錄中的產品時，根據客戶興趣和動作，產品建議系統 toodeliver 個人化的建議。 hello 客戶也會看到 toohello 產品正在查看根據整體網站使用模式不相關的 tooany 一位使用者相關的產品。

![使用案例圖](./media/data-factory-product-reco-usecase/diagram-1.png)

未經處理的 web 記錄檔 （gb） 會產生每日從 hello 線上零售商的網站為半結構化檔案。 hello 原始 web 記錄檔和 hello 客戶及產品類別目錄資訊是內嵌定期到 Azure Blob 儲存體使用做為服務的 Data Factory 的全域部署的資料移動。 hello 天 hello 原始記錄檔是長期儲存的 blob 儲存體中的分割 （依據年和月）。  [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/)大規模使用 Hive 和 Pig 指令碼的存放區並處理 hello 內嵌的記錄是 hello blob 中使用的 toopartition hello 未經處理的記錄檔。 hello 分割的 web 記錄資料，然後處理的 tooextract hello 輸入需要的機器學習建議系統 toogenerate hello 個人化產品建議。

hello hello 機器學習，在此範例中使用的建議系統是開放原始碼機器學習建議平台從[Apache 砲象兵](http://mahout.apache.org/)。  任何[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)或自訂的模型可套用的 toohello 案例。  hello 砲象兵模型是使用的 toopredict hello 與之間文字相似度 hello 整體使用量模式為基礎的網站上的項目 hello 個別使用者為基礎的 toogenerate hello 個人化的建議。

最後，個人化的產品建議 hello 結果集是移動的 tooa 關聯式資料超市以供取用 hello 零售商的網站。  hello 結果集可能也直接從 blob 儲存體用來存取其他應用程式，或移 tooadditional 存放區，以獲得其他取用者與使用案例。

## <a name="benefits"></a>優點
藉由最佳化其產品建議策略，並符合商務目標、 hello 解決方案符合 hello 線上零售店的推銷和行銷目標。 此外，它們可以 toooperationalize 而且有效率、 可靠且具成本效益的方式管理 hello 產品建議工作流程。 hello 方法可便於他們 tooupdate 其模型並微調其銷售按一下要轉換的成功次數的 hello 量值為基礎的效果。 藉由使用 Azure Data Factory，能夠 tooabandon 其耗時又昂貴的手動雲端資源管理和它們移動 tooon 視需要管理雲端資源。 因此，無法 toosave 時間、 金錢，和它們減少其時間 toosolution 部署。 資料歷程檢視和操作的服務健全狀況變得簡單 toovisualize 和疑難排解 hello 直覺式的 Data Factory 監視及管理 UI 可從 hello Azure 入口網站。 其解決方案可以立即排程並在受管理，如此可靠地產生及傳遞 toousers，已完成的資料和資料和處理相依性會自動管理需要人為介入。

藉由提供此個人化的購物體驗，hello 線上零售店建立競爭力、 吸引人的客戶體驗，因此增加銷售和整體客戶滿意度。

