---
title: "業務持續性和災害復原 (BCDR)：Azure 配對的區域 | Microsoft Docs"
description: "了解 Azure 地區的配對，tooensure 應用程式有彈性地在資料中心失敗時。"
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
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 68a3a33a8e768c72fa296d42c9ab97049232d169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="business-continuity-and-disaster-recovery-bcdr-azure-paired-regions"></a>業務持續性和災害復原 (BCDR)：Azure 配對的區域

## <a name="what-are-paired-regions"></a>什麼是配對的區域？

Azure hello 世界各地的多個地理位置中的運作方式。 Azure 的地理位置是定義的區域的 hello world 包含至少一個 Azure 區域。 Azure 區域是包含一或多個資料中心之地理位置內的區域。

每個 Azure 區域搭配另一個地區內 hello 一起進行地區組的相同地理位置。 hello 例外狀況是巴西南部配對與外部其地理區域。

![AzureGeography](./media/best-practices-availability-paired-regions/GeoRegionDataCenter.png)

圖 1 – Azure 區域配對圖表

| [地理位置] | 配對的區域 |  |
|:--- |:--- |:--- |
| 亞洲 |東亞 |東南亞 |
| 澳大利亞 |澳洲東部 |澳大利亞東南部 |
| 加拿大 |加拿大中部 |加拿大東部 |
| 中國 |中國北部 |中國東部|
| 印度 |印度中部 |印度南部 |
| 日本 |日本東部 |日本西部 |
| 韓國 |韓國中部 |韓國南部 |
| 北美洲 |美國中北部 |美國中南部 |
| 北美洲 |美國東部 |美國西部 |
| 北美洲 |美國東部 2 |美國中部 |
| 北美洲 |美國西部 2 |美國中西部 |
| 歐洲 |北歐 |西歐 |
| 日本 |日本東部 |日本西部 |
| 巴西 |巴西南部 (1) |美國中南部 |
| 美國政府 |美國政府愛荷華州 |美國政府維吉尼亞州 |
| 美國政府 |美國政府維吉尼亞州 |美國政府德克薩斯州 |
| 美國政府 |美國政府德克薩斯州 |美國政府亞利桑那州 |
| 美國政府 |美國政府亞利桑那州 |美國政府德克薩斯州 |
| 英國 |英國西部 |英國南部 |
| 德國 |德國中部 |德國東北部 |

表 1 - Azure 區域配對對應表

> (1) 巴西南部與其他區域的不同點在於，其與自身地理位置以外的區域配對。 巴西南部的次要地區是美國中南部，但是美國中南部的次要地區並不是巴西南部。


我們建議您從 Azure 的隔離和可用性原則的區域組 toobenefit 跨複寫工作負載。 比方說，計劃 Azure 系統更新會以循序方式部署 (不是在 hello 同時) 配對區域上。 這表示，即使在 hello 罕見事件中的故障的更新，兩個區域不會影響同時。 此外，在 hello 罕見事件中廣泛中斷的至少一個超出每一對區域的復原已設定優先權。

## <a name="an-example-of-paired-regions"></a>配對的區域範例
下方圖 2 顯示嚴重損壞修復使用 hello 地區組假設性應用程式。 綠色 hello 數字的反白顯示 hello 跨地區活動的三個 Azure 服務 （Azure compute、 儲存體，和資料庫），它們是如何設定 tooreplicate 跨區域。 hello 的配對區域跨部署的唯一優點是 hello 橙色數字的反白顯示。

![配對區域優點概觀](./media/best-practices-availability-paired-regions/PairedRegionsOverview2.png)

圖 2 – 假設的 Azure 區域配對

## <a name="cross-region-activities"></a>跨區域活動
為參照的 tooin 圖 2。

![PaaS](./media/best-practices-availability-paired-regions/1Green.png) **Azure 計算 (PaaS)** – 您必須佈建額外的計算資源事先 tooensure 可用資源中另一個區域發生嚴重損壞。 如需詳細資訊，請參閱 [Azure 復原技術指導](resiliency/resiliency-technical-guidance.md)。

![儲存體](./media/best-practices-availability-paired-regions/2Green.png) **Azure 儲存體**：建立 Azure 儲存體帳戶時，預設會設定異地備援儲存體 (GRS)。 使用 GRS 時，您的資料會自動複寫三次在 hello 主要區域中，以及三次 hello 配對區域中。 如需詳細資訊，請參閱 [Azure 儲存體備援選項](storage/common/storage-redundancy.md)。

![Azure SQL](./media/best-practices-availability-paired-regions/3Green.png) **Azure SQL Database** – 與 Azure SQL 標準地理複寫，您可以設定非同步方式複寫交易 tooa 配對區域。 Premium 異地複寫，您可以設定複寫 tooany 區域中的 hello world;不過，我們建議您部署這些資源中大部分的嚴重損壞修復案例的配對區域。 如需詳細資訊，請參閱 [Azure SQL Database 中的異地複寫](sql-database/sql-database-geo-replication-overview.md)。

![Resource Manager](./media/best-practices-availability-paired-regions/4Green.png) **Azure Resource Manager**：Resource Manager 原本就會跨區域提供服務管理元件的邏輯隔離。 這表示一個區域中的邏輯失敗是比較不可能 tooimpact 另一個。

## <a name="benefits-of-paired-regions"></a>配對區域的優點
為參照的 tooin 圖 2。  

![隔離](./media/best-practices-availability-paired-regions/5Orange.png)
**實體隔離**：在可能的情況下，Azure 會偏好區域配對中的資料中心之間距離至少要相隔 300 英哩，但是這在所有地理位置中並不實際也不可能。 實體資料中心隔離降低 hello 可能性自然災害、 動盪、 電源中斷或同時影響這兩個區域的實體網路中斷。 隔離是主體 toohello 條件約束內 hello 地理 （地理區大小、 電源/網路基礎結構可用性、 法規等等）。  

![複寫](./media/best-practices-availability-paired-regions/6Orange.png)
**平台提供複寫**-某些服務，例如地理備援儲存體提供自動複寫 toohello 配對的區域。

![復原](./media/best-practices-availability-paired-regions/7Orange.png)
**區域復原順序**– hello 廣泛的中斷事件中的一個區域復原已設定優先權超出每一對。 配對區域跨部署的應用程式，都一定的 toohave 的其中一個 hello 區域復原優先順序。 如果應用程式部署到未成對的區域，復原可能會延遲 – 中最差的案例 hello 選的區域 hello 復原最後兩個 toobe hello。

![更新](./media/best-practices-availability-paired-regions/8Orange.png)
**連續更新**– 計劃 Azure 系統都會回復更新 toopaired 區，以循序方式 (不是在 hello 同時) toominimize 停機時間，hello 作用中的 bug 和 hello 罕見事件中的邏輯失敗不正確的更新。

![資料](./media/best-practices-availability-paired-regions/9Orange.png)
**資料 residency** – 區域位於 hello 相同地理位置做為其配對 （有 hello 例外狀況的巴西南部） 順序 toomeet 資料 residency 需求進行稅金和法律強制管轄區中。
