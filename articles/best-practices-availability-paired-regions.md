---
title: "業務持續性和災害復原 (BCDR)：Azure 配對的區域 | Microsoft Docs"
description: "了解 Azure 區域配對，以確保當資料中心發生故障時應用程式可復原。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: c2d0a21c-2564-4d42-991a-bc31723f61a4
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/11/2017
ms.author: raynew
ms.openlocfilehash: 394f353837433e241e4da6f4accdb5eaa24bae46
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="business-continuity-and-disaster-recovery-bcdr-azure-paired-regions"></a>業務持續性和災害復原 (BCDR)：Azure 配對的區域

## <a name="what-are-paired-regions"></a>什麼是配對的區域？

Azure 能在世界各地多個地理位置運作。 Azure 地理位置是包含至少一個 Azure 區域的已定義世界區域。 Azure 區域是包含一或多個資料中心之地理位置內的區域。

每個 Azure 區域都會與相同地理位置內的另一個區域配對，以共同形成區域配對。 例外狀況是巴西南部，此區域會與其所在地理位置外的區域配對。

![AzureGeography](./media/best-practices-availability-paired-regions/GeoRegionDataCenter.png)

圖 1 – Azure 區域配對圖表

| [地理位置] | 配對的區域 |  |
|:--- |:--- |:--- |
| 亞洲 |東亞 |東南亞 |
| 澳大利亞 |澳洲東部 |澳大利亞東南部 |
| 加拿大 |加拿大中部 |加拿大東部 |
| 中國 |中國北部 |中國東部|
| 印度 |印度中部 |印度南部 |
| 印度 |西部可以 (1) |印度南部 |
| 日本 |日本東部 |日本西部 |
| 韓國 |韓國中部 |韓國南部 |
| 北美洲 |美國中北部 |美國中南部 |
| 北美洲 |美國東部 |美國西部 |
| 北美洲 |美國東部 2 |美國中部 |
| 北美洲 |美國西部 2 |美國中西部 |
| 歐洲 |北歐 |西歐 |
| 日本 |日本東部 |日本西部 |
| 巴西 |巴西南部 (2) |美國中南部 |
| 美國政府 |美國 Gov 稍後 (3) |美國政府維吉尼亞州 |
| 美國政府 |美國 Gov 維吉尼亞州 (4) |美國政府德克薩斯州 |
| 美國政府 |美國政府亞利桑那州 |美國政府德克薩斯州 |
| 美國國防部 |美國 DoD 東部 |美國國防部中央 |
| 英國 |英國西部 |英國南部 |
| 德國 |德國中部 |德國東北部 |

表 1 - Azure 區域配對對應表

- > （由於搭配另一個區域中只有一個方向，1） 西印度是不同。 西部可以次要區域是印度南部及印度，但印度南部及印度的次要區域印度中部。
- > （2） 巴西南部是唯一的因為它搭配自己的地理位置以外的區域。 巴西南部的次要地區是美國中南部，但是美國中南部的次要地區並不是巴西南部。
- > （3） 美國 Gov 稍後的次要區域是美國 Gov 維吉尼亞州，但美國 Gov 維吉尼亞次要區域不是美國 Gov 稍後。
- > （4） 美國 Gov 維吉尼亞州的次要區域是美國 Gov 德州但美國 Gov 德州次要區域不是美國 Gov 維吉尼亞州。


我們建議您複寫跨區域配對的工作負載，以善用 Azure 的隔離與可用性原則。 例如，預定的 Azure 系統更新會跨配對區域循序部署 (並非同時)。 這表示即使面臨罕見的更新錯誤事件，兩個區域也不會同時受到影響。 此外，若遭遇少見的廣泛中斷事件，就能至少優先復原所有配對中的其中一個區域。

## <a name="an-example-of-paired-regions"></a>配對的區域範例
以下的圖 2 顯示使用地區配對以進行災害復原的假設應用程式。 綠色的數字強調了三項 Azure 服務 (Azure 計算、儲存體和資料庫) 的跨區域活動，以及這些服務設定為跨區域複寫的方式。 橘色數字則強調跨配對區域部署的獨特優點。

![配對區域優點概觀](./media/best-practices-availability-paired-regions/PairedRegionsOverview2.png)

圖 2 – 假設的 Azure 區域配對

## <a name="cross-region-activities"></a>跨區域活動
如圖 2 所示。

![PaaS](./media/best-practices-availability-paired-regions/1Green.png) **Azure 運算 (PaaS)**：您必須佈建額外的運算資源，以便確保發生嚴重損壞時資源可在其他區域中使用。 如需詳細資訊，請參閱 [Azure 復原技術指導](resiliency/resiliency-technical-guidance.md)。

![儲存體](./media/best-practices-availability-paired-regions/2Green.png) **Azure 儲存體**：建立 Azure 儲存體帳戶時，預設會設定異地備援儲存體 (GRS)。 使用 GRS 時，系統會在主要區域內將您的資料自動複寫三次，並在配對區域中複寫三次。 如需詳細資訊，請參閱 [Azure 儲存體備援選項](storage/common/storage-redundancy.md)。

![Azure SQL](./media/best-practices-availability-paired-regions/3Green.png) **Azure SQL Database**：使用 Azure SQL 標準異地複寫，您就可以設定交易至配對區域的非同步複寫。 使用高階異地複寫，您就可以設定複寫至世界上任何區域。不過，我們建議您在配對區域中，為大部分的災害復原案例部署這些資源。 如需詳細資訊，請參閱 [Azure SQL Database 中的異地複寫](sql-database/sql-database-geo-replication-overview.md)。

![Resource Manager](./media/best-practices-availability-paired-regions/4Green.png) **Azure Resource Manager**：Resource Manager 原本就會跨區域提供服務管理元件的邏輯隔離。 這表示某個區域中的邏輯失敗不太可能會影響另一個區域。

## <a name="benefits-of-paired-regions"></a>配對區域的優點
如圖 2 所示。  

![隔離](./media/best-practices-availability-paired-regions/5Orange.png)
**實體隔離**：在可能的情況下，Azure 會偏好區域配對中的資料中心之間距離至少要相隔 300 英哩，但是這在所有地理位置中並不實際也不可能。 實體資料中心分隔能夠降低自然災害、社會動亂、電力中斷或實體網路中斷同時影響兩個區域的可能性。 隔離會受限於地理位置內的條件約束 (地理位置大小、電源/網路基礎結構可用性、法規等等)。  

![複寫](./media/best-practices-availability-paired-regions/6Orange.png)
**平台提供的複寫**：異地備援儲存體之類的部分服務會提供自動複寫到配對的區域。

![復原](./media/best-practices-availability-paired-regions/7Orange.png)
**區域復原順序**：若發生廣泛中斷事件，會優先復原所有配對中的一個區域。 跨配對區域部署的應用程式能夠保障其中一個區域優先復原。 如果應用程式部署到未成對的區域，復原可能會延遲 – 所選的區域可能會復原最後兩個最糟的情況。

![更新](./media/best-practices-availability-paired-regions/8Orange.png)
**循序更新**：預定的 Azure 系統更新會循序發行至配對的區域 (並非同時)，以便在出現罕見的不正確更新時，將停機時間、錯誤影響和邏輯故障的影響降到最低。

![資料](./media/best-practices-availability-paired-regions/9Orange.png)
**資料常駐地** - 區域會駐留在相同的地理位置之內形成配對 (巴西南部除外)，以符合資料常駐地之稅務和執法管轄區的要求。
