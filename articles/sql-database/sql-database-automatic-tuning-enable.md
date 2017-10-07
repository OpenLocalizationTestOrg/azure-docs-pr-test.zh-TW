---
title: "自動調整的 Azure SQL Database aaaEnable |Microsoft 文件"
description: "您可以輕鬆在 Azure SQL Database 上啟用自動調整。"
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a>啟用自動微調

Azure SQL Database 是一種自動受管理的資料服務，不斷地監視您的查詢並找出您可以執行工作負載效能 tooimprove hello 動作。 您可以檢閱建議並加以手動套用，或讓 Azure SQL Database 自動套用矯正措施 - 這稱為**模式**。 自動調整，可以在 hello 伺服器或 hello 資料庫層級啟用。

## <a name="enable-automatic-tuning-on-server"></a>在伺服器上啟用自動調整

tooenable 自動調整 Azure SQL Database 伺服器上瀏覽 Azure 入口網站，然後選取 toohello server**自動微調**hello 功能表中。 選取 hello tooenable 再選取的自動調整選項**套用**:

![伺服器](./media/sql-database-automatic-tuning-enable/server.png)

自動微調伺服器上的選項會套用的 tooall hello 伺服器上的資料庫。 根據預設，所有資料庫會都繼承其父伺服器中的 hello 設定，但是這可以覆寫並個別指定每個資料庫。

## <a name="configure-automatic-tuning-on-database"></a>在資料庫上設定自動調整

hello Azure 入口網站可讓您 tooindividually 每個資料庫上指定 hello 自動調整設定。

> [!NOTE]
> hello 一般建議是 toomanage hello 自動調整設定伺服器層級是相同的組態設定可以在每個資料庫自動套用的 hello。 設定自動調整個別的資料庫上如果 hello 資料庫位於不同的其他人 hello 相同的伺服器。
>

tooenable 自動調整的單一資料庫上，瀏覽 toohello hello Azure 入口網站中的資料庫然後再選取**自動微調**。 您可以設定單一資料庫 tooinherit hello 從 hello 資料庫選取 hello 核取方塊，或您可以個別指定資料庫的 「 hello 」 組態設定。

![資料庫](./media/sql-database-automatic-tuning-enable/database.png)

一旦您選取適當的設定後，按一下 [套用]。

## <a name="next-steps"></a>後續步驟
* 讀取 hello[自動調整的發行項](sql-database-automatic-tuning.md)toolearn 深入了解自動調整，以及它如何協助您改善您的效能。
* 如需 Azure SQL Database 效能建議的概觀，請參閱[效能建議](sql-database-advisor.md)。
* 請參閱[查詢效能深入資訊](sql-database-query-performance.md)toolearn 有關檢視 hello 您排名最前面的查詢效能影響。
