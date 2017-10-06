---
title: "aaaRolling 應用程式升級 Azure SQL Database |Microsoft 文件"
description: "深入了解如何 toouse Azure SQL Database 的地理複寫 toosupport 線上升級您的雲端應用程式。"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 58f42859-1e37-463c-a3d8-a3ca2e867148
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/16/2016
ms.author: sashan
ms.openlocfilehash: 18c56300916d129bff141624cc5c416b500408d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-rolling-upgrades-of-cloud-applications-using-sql-database-active-geo-replication"></a>使用 SQL Database 主動式異地複寫管理雲端應用程式的輪流升級
> [!NOTE]
> [作用中異地複寫](sql-database-geo-replication-overview.md)現在可供所有層中的所有資料庫使用。
> 

深入了解如何 toouse[地理複寫](sql-database-geo-replication-overview.md)中 SQL Database tooenable 輪流升級的雲端應用程式。 因為升級是干擾性作業，它應該是您商務持續性規劃與設計的一部分。 在本文探討兩個不同的方法，來協調 hello 的升級程序，並討論 hello 優點和缺點的每個選項。 基於本文章的 hello 我們會使用當做其資料層的 web 站台連線的 tooa 單一資料庫所組成的簡單應用程式。 我們的目標是 tooupgrade 1 上的版本而不會大幅影響 hello 應用程式 tooversion 2 hello 使用者體驗。 

評估 hello 升級選項時，您應該考慮下列因素的 hello:

* 升級期間對應用程式可用性的影響。 多久 hello 應用程式函式可能會限制或降級。
* 能力 tooroll 備份，以防升級失敗。
* Hello 應用程式不相關的重大錯誤 hello 升級期間發生的弱點。
* 總金額成本。  這包括額外的備援性和 hello hello 升級程序所用的暫存元件的遞增成本。 

## <a name="upgrading-applications-that-rely-on-database-backups-for-disaster-recovery"></a>升級依賴資料庫備份以進行災害復原的應用程式
如果您的應用程式依賴自動資料庫備份，並針對嚴重損壞修復使用異地還原，則通常是部署的 tooa 單一 Azure 區域。 在此情況下 hello 升級程序牽涉到建立備份的所有應用程式元件部署參與 hello 升級。 您會利用 Azure Traffic Manager (WATM) 與 hello 容錯移轉設定檔 toominimize hello 使用者中斷。  hello 下列圖表說明 hello 操作環境之前 toohello 升級程序。 hello 端點<i>contoso 1.azurewebsites.net</i>表示需要升級 toobe hello 應用程式的生產環境位置。 tooenable hello 能力 tooroll 回 hello 升級，您需要建立階段插槽 hello 應用程式的完整同步處理複本。 hello 下列步驟是必要的 tooprepare hello hello 升級應用程式：

1. 建立 hello 升級階段位置。 建立次要資料庫 (1)，並部署相同網站中 hello toodo 相同 Azure 區域。 如果在完成植入處理程序的 hello，監視 hello 次要 toosee。
2. 在 WATM 中建立容錯移轉設定檔，<i>contoso-1.azurewebsites.net</i> 作為線上端點，<i>contoso-2.azurewebsites.net</i> 作為離線端點。 

> [!NOTE]
> 請注意 hello 準備步驟並不會影響 hello hello 生產位置中的應用程式，它可以在完整存取權限模式下運作。
>  

![SQL Database「異地複寫」組態。 雲端災害復原。](media/sql-database-manage-application-rolling-upgrade/Option1-1.png)

Hello 準備步驟完成 hello 應用程式已準備好 hello 實際升級。 hello 下列圖表說明 hello 升級程序中所包含的 hello 步驟。 

1. Hello 主要資料庫設定 hello 生產位置 tooread-僅限模式中 (3)。 這樣會保證該 hello hello 應用程式 (V1) 的實際執行個體將因此防止 hello hello V1 與 V2 資料庫執行個體之間的資料不一致的 hello 升級期間維持唯讀狀態。  
2. 中斷連線 hello 次要資料庫使用 hello 計劃的終止模式 (4)。 它會建立 hello 主要資料庫完全同步處理獨立複本。 此資料庫將會升級。
3. 開啟 hello tooread 寫模式，主要資料庫，並執行 hello 階段插槽 (5) 中的 hello 升級指令碼。     

![SQL Database 異地複寫組態。 雲端災害復原。](media/sql-database-manage-application-rolling-upgrade/Option1-2.png)

如果已成功完成 hello 升級現在您已經準備就緒 tooswitch hello 終端使用者接移 toohello 複製 hello 應用程式。 它現在會變成 hello hello 應用程式的生產環境位置。  這牽涉到在 hello 下列圖表所示的幾個步驟。

1. 太切換 hello WATM 設定檔中的 hello 線上端點<i>contoso 2.azurewebsites.net</i>，hello 網站 (6) 的點 toohello V2 版本。 現在已成為 hello 生產位置以 hello V2 應用程式，且 hello 使用者流量導向的 tooit。  
2. 如果您不再需要 hello V1 應用程式元件，因此您可以安全地移除 (7)。   

![SQL Database 異地複寫組態。 雲端災害復原。](media/sql-database-manage-application-rolling-upgrade/Option1-3.png)

是否 hello 升級程序不成功，例如因為 tooan hello 升級指令碼中的錯誤 hello 階段位置應視為入侵。 tooroll 回 hello 應用程式 toohello 升級前狀態您只需還原 hello hello 生產位置 toofull access 中的應用程式。 hello 下圖會顯示 hello 所需的步驟。    

1. 設定 hello 資料庫複製 tooread 寫入模式 (8)。 這將會還原 hello 完整 V1 hello 生產位置中的功能。
2. 執行 hello 根本原因分析，並移除 hello 階段插槽 (9) 中的 hello 危害元件。 

此時 hello 應用程式可完整運作，並可以重複 hello 升級步驟。

> [!NOTE]
> hello 復原則不需要變更 WATM 設定檔中的因為它已經點太<i>contoso 1.azurewebsites.net</i>為 hello 主動端點。
> 
> 

![SQL Database 異地複寫組態。 雲端災害復原。](media/sql-database-manage-application-rolling-upgrade/Option1-4.png)

hello 金鑰**利用**這個選項是您可以升級的應用程式在單一區域，使用一組簡單的步驟。 hello 貨幣成本 hello 升級為較低。 主要的 hello**權衡取捨**是，如果 hello 升級 hello 復原 toohello 升級前狀態期間發生嚴重失敗將會包含不同的區域和還原 hello 資料庫中的 hello 應用程式重新部署使用地理還原的備份。 此程序將產生顯著的停機時間。   

## <a name="upgrading-applications-that-rely-on-database-geo-replication-for-disaster-recovery"></a>升級依賴資料庫異地複寫來進行災害復原的應用程式
如果您的應用程式會利用業務續航力的地理複寫，則部署的 tooat 至少兩個不同的區域與主要區域中作用中的部署和備份區域中的待命部署。 此外 toohello 因素先前所述，hello 升級程序必須保證：

* hello 應用程式隨時 hello 升級程序期間保持受保護的嚴重失敗
* hello hello 應用程式的地理備援元件會升級以平行方式與 hello 作用中的元件

tooachieve 這些目標，您會利用 Azure Traffic Manager (WATM) 使用 hello 容錯移轉設定檔與一個使用中，三個的備份端點。  hello 下列圖表說明 hello 操作環境之前 toohello 升級程序。 hello 網站<i>contoso 1.azurewebsites.net</i>和<i>contoso dr.azurewebsites.net</i>完整地理備援代表 hello 應用程式的生產環境位置。 tooenable hello 能力 tooroll 回 hello 升級，您需要建立階段插槽 hello 應用程式的完整同步處理複本。 您需要 tooensure hello 應用程式可以快速地復原以防 hello 升級程序期間發生嚴重失敗，因為 hello 階段位置需要 toobe 異地備援以及。 hello 下列步驟是必要的 tooprepare hello hello 升級應用程式：

1. 建立 hello 升級階段位置。 建立次要資料庫 (1) 和部署的 hello hello 網站的相同複本的 toodo 相同 Azure 區域。 如果在完成植入處理程序的 hello，監視 hello 次要 toosee。
2. 建立 hello 階段插槽中的異地備援的次要資料庫，藉由地理複寫 hello 次要資料庫 toohello 備份區域 （稱為 「 串連地理複寫 」）。 請監視 hello 備份次要 toosee hello 植入處理程序是否已完成 (3)。
3. 建立 hello 備份區域中的 hello 網站上的待命副本，並連結到 toohello 地理備援次要資料庫 (4)。  
4. 新增 hello 其他端點<i>contoso 2.azurewebsites.net</i>和<i>contoso 3.azurewebsites.net</i> toohello 容錯移轉設定檔中 WATM 為離線的端點 (5)。 

> [!NOTE]
> 請注意 hello 準備步驟並不會影響 hello hello 生產位置中的應用程式，它可以在完整存取權限模式下運作。
> 
> 

![SQL Database 異地複寫組態。 雲端災害復原。](media/sql-database-manage-application-rolling-upgrade/Option2-1.png)

一旦 hello 準備步驟完成時，就有一個 hello 階段位置可供 hello 升級。 hello 下列圖表說明 hello 升級步驟。

1. Hello 主要資料庫設定 hello 生產位置 tooread-僅限模式中 (6)。 這樣會保證該 hello hello 應用程式 (V1) 的實際執行個體將因此防止 hello hello V1 與 V2 資料庫執行個體之間的資料不一致的 hello 升級期間維持唯讀狀態。  
2. 中斷連接次要資料庫的 hello hello 中相同的區域使用 hello 計劃的終止模式 (7)。 它會建立完全同步處理的獨立 hello 主要資料庫，就會自動變成 hello 終止後的主要副本。 此資料庫將會升級。
3. 在 hello 階段插槽 tooread 寫入模式下開啟 hello 主要資料庫，並執行 hello 升級指令碼 (8)。    

![SQL Database 異地複寫組態。 雲端災害復原。](media/sql-database-manage-application-rolling-upgrade/Option2-2.png)

如果已成功完成 hello 升級現在您已經準備就緒 tooswitch hello 使用者 toohello V2 hello 應用程式版本。 hello 下列圖表說明 hello 所需的步驟。

1. 太切換 hello WATM 設定檔中的 hello 作用中端點<i>contoso 2.azurewebsites.net</i>，現在點 toohello V2 hello 網站 (9) 版本。 它現在成為生產位置以 hello V2 應用程式，且使用者流量導向的 tooit。 
2. 如果您不再需要 hello V1 應用程式，這樣您就可以安全地移除它 （10 和 11）。  

![SQL Database 異地複寫組態。 雲端災害復原。](media/sql-database-manage-application-rolling-upgrade/Option2-3.png)

是否 hello 升級程序不成功，例如因為 tooan hello 升級指令碼中的錯誤 hello 階段位置應視為入侵。 tooroll 回 hello 應用程式 toohello 升級前狀態您只需還原 toousing hello 應用程式具有完整存取權的 hello 生產位置中。 hello 下圖會顯示 hello 所需的步驟。    

1. 設定 hello hello 生產位置 tooread 寫入模式 (12) 的主要資料庫複本。 這將會還原 hello 完整 V1 hello 生產位置中的功能。
2. 執行 hello 根本原因分析，並移除 hello 階段插槽 （13 與 14） 中的 hello 危害元件。 

此時 hello 應用程式可完整運作，並可以重複 hello 升級步驟。

> [!NOTE]
> hello 復原則不需要變更 WATM 設定檔中的因為它已經點太<i>contoso 1.azurewebsites.net</i>為 hello 主動端點。
> 
> 

![SQL Database 異地複寫組態。 雲端災害復原。](media/sql-database-manage-application-rolling-upgrade/Option2-4.png)

hello 金鑰**利用**這個選項時，您可以升級 hello 應用程式和其異地備援複本，以平行方式而不會危害您的業務續航力 hello 升級期間。 主要的 hello**權衡取捨**是它需要的每個應用程式元件的雙重備援性，因此造成 貨幣成本較高。 它也涉及更複雜的工作流程。 

## <a name="summary"></a>摘要
hello 兩個升級方法 hello 文章所述的相同複雜性和 hello 貨幣成本，但它們都著重於最小化 hello 時間 hello 終端使用者限制為只能在 tooread 上執行的操作。 直接由 hello hello 升級指令碼期間定義該時間。 它不依賴 hello 資料庫大小、 hello 服務層您選擇 hello 網站組態，您無法輕鬆地控制其他因素。 這是因為所有的 hello 準備步驟彼此分離時 hello 升級步驟可以完成而不會影響 hello 實際執行應用程式。 hello 效率 hello 升級指令碼是 hello 決定在升級期間的 hello 使用者體驗的關鍵因素。 因此可以改善 hello 最佳方式是集中建立盡可能有效率 hello 升級指令碼工作。  

## <a name="next-steps"></a>後續步驟
* 如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)。
* toolearn 有關自動化 Azure SQL Database 備份，請參閱[SQL 資料庫自動備份](sql-database-automated-backups.md)。
* toolearn 有關使用自動的備份進行復原，請參閱[從自動備份中還原資料庫](sql-database-recovery-using-backups.md)。
* toolearn 有關更快速的復原選項，請參閱[作用中地理複寫](sql-database-geo-replication-overview.md)。


