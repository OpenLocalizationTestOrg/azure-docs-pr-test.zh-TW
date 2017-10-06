---
title: "aaaFailover 群組和作用中地理複寫的 Azure SQL Database |Microsoft 文件"
description: "自動容錯移轉群組與作用中地理複寫可讓您的資料庫中任何 hello Azure 資料中心和 autoomatically 中斷的 hello 事件中的容錯移轉的 toosetup 4 複本。"
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2a29f657-82fb-4283-9a83-e14a144bfd93
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 07/10/2017
ms.author: sashan
ms.openlocfilehash: 7a39af8505624c0f19c5abccff051af836b1f9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-failover-groups-and-active-geo-replication"></a>概觀︰容錯移轉群組和主動式異地複寫
作用中地理複寫可讓您向上 toofour 可讀取的次要資料庫在 hello tooconfigure 相同或不同資料中心位置 （地區）。 次要資料庫可用來查詢和在 hello 案例中的資料中心中斷或 hello 無法 tooconnect toohello 主要資料庫的容錯移轉。 hello 應用程式的 hello 使用者必須手動起始 hello 容錯移轉。 容錯移轉之後，hello 新主要複本會有不同的連接端點。 

> [!NOTE]
> 主動式異地複寫可供所有區域之所有服務層中的所有資料庫使用。
>  

Azure SQL Database 自動容錯移轉群組 （預覽版） 是 SQL Database 功能，特別設計 tooautomatically 管理地理複寫 」 關係、 連接及大規模的容錯移轉。 Hello 客戶獲得 hello 能力 tooautomatically 之後地區的災難性失敗或其他非計劃的事件，SQL Database 服務會導致完整或部分遺失的 hello, 復原 hello 次要區域中的多個相關的資料庫hello 主要區域中的可用性。 此外，他們可以使用 hello 可讀取次要資料庫 toooffload 唯讀工作負載。  因為自動容錯移轉群組包含多個資料庫，因此必須設定 hello 主要伺服器上。 主要和次要伺服器都必須在 hello 相同訂用帳戶。 自動容錯移轉群組支援 hello 群組 tooonly 一部次要伺服器位於不同的區域中的所有資料庫的複寫。 作用中地理複寫，不含自動容錯移轉群組，可讓向上 too4 次要資料庫的任何區域中。

如果您使用作用中地理複寫和任何主要資料庫失敗，原因或只需要 toobe，使其離線，您可以起始容錯移轉 tooany 的次要資料庫。 所有其他次要資料庫啟動的 tooone hello 次要資料庫的容錯移轉時，會自動連結的 toohello 新主要複本。 如果您使用自動容錯移轉群組 （預覽） toomanage 資料庫復原和任何會影響一個或多個自動容錯移轉中的 hello 群組結果中的 hello 資料庫的中斷。 您可以設定 hello 自動容錯移轉原則以最符合您應用程式的需求，或者您可以退出，並使用手動啟動。 此外，自動容錯移轉群組 (預覽版) 還提供在容錯移轉期間仍保持不變的讀寫和唯讀接聽程式端點。 無論您是使用手動或自動容錯移轉啟用，容錯移轉會在 hello 群組 tooprimary 切換所有次要資料庫。 Hello 資料庫容錯移轉完成之後，hello DNS 記錄是自動更新的 tooredirect hello 端點 toohello 新區域。

您可以使用主動式異地複寫管理伺服器上或彈性集區中個別資料庫或一組資料庫的複寫和容錯移轉。 您可以使用 hello [Azure 入口網站](sql-database-geo-replication-portal.md)， [PowerShell](sql-database-geo-replication-powershell.md)， [TRANSACT-SQL](sql-database-geo-replication-transact-sql.md)，或使用 hello [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx)。 容錯移轉之後，確定已 hello 新主要複本上設定您的伺服器和資料庫的 hello 驗證需求。 如需詳細資訊，請參閱 [災害復原後的 SQL Database 安全性](sql-database-geo-replication-security-config.md)。 這適用於這兩個 tooactive 地理複寫 」 和 「 自動容錯移轉群組 （預覽）。

作用中地理複寫會運用 hello [Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)技術的 SQL Server tooasynchronously 複寫 hello 主要資料庫 tooa 次要資料庫上使用 read committed 快照集隔離 (RCSI) 已認可的交易。 自動容錯移轉群組提供在作用中地理複寫，但使用相同的非同步複寫機制 hello 之上 hello 群組語意。 在任何指定的時間點，而 hello 次要資料庫可能稍微落後主要資料庫的 hello、 hello 次要資料保證 toonever 有部分的交易。 跨區域備援可讓您免於永久遺失的整個資料中心或部分天災、 災難性人為錯誤或惡意行為造成資料中心的應用程式 tooquickly 復原。 hello 特定 RPO 的資料，請參閱[業務續航力概觀](sql-database-business-continuity.md)。

hello 下圖顯示範例的作用中地理複寫設定，在 hello 美國中北部區域的主要和次要 hello 美國中南部區域中。

![異地複寫關聯性](./media/sql-database-active-geo-replication/geo-replication-relationship.png)

Hello 次要資料庫是可讀取的因為它們可能會報告工作，例如使用的 toooffload 唯讀工作負載。 如果您使用的作用中地理複寫，很可能 toocreate hello 次要資料庫在 hello 相同地區具有 hello 主要伺服器上，但它不會增加 hello 應用程式的恢復功能 toocatastrophic 失敗。 如果您使用自動容錯移轉群組 (預覽版)，則一律要在不同區域中建立次要資料庫。

此外 toodisaster 復原作用中地理複寫可用於下列案例的 hello:

* **資料庫移轉**： 您可以使用作用中地理複寫 toomigrate 將資料庫從一部伺服器 tooanother 線上以最少的停機時間。
* **應用程式升級**：您可以在應用程式升級期間建立額外的次要資料庫做為容錯回復複本。

tooachieve 真正的業務連續性，請新增資料中心之間的資料庫備援是屬於 hello 方案。 嚴重的失敗需要的所有元件構成 hello 服務和任何相依的服務復原之後復原應用程式 （服務） 端對端。 這些元件的範例包括 hello 用戶端軟體 （例如，含自訂 JavaScript 的瀏覽器）、 web 前端、 儲存及 DNS。 很重要的所有元件為彈性 toohello 相同的失敗，而且 hello 復原時間目標 (RTO) 的應用程式內變為可用。 因此，您需要 tooidentify 所有相依的服務，並了解 hello 保證與它們所提供的功能。 然後，您必須採取服務函式期間 hello 它所依賴的 hello 服務的容錯移轉的適當的步驟，tooensure。 如需有關設計災害復原解決方案的詳細資訊，請參閱[使用主動式異地複寫設計災害復原的雲端解決方案](sql-database-designing-cloud-solutions-for-disaster-recovery.md)。

## <a name="active-geo-replication-capabilities"></a>主動式異地複寫功能
hello 作用中地理複寫功能提供下列基本功能的 hello:
* **自動非同步複寫**： 您只能藉由新增 tooan 現有的資料庫建立次要資料庫。 次要的 hello 可由任何 Azure SQL Database 伺服器中。 一旦建立，hello 次要資料庫會填入 hello hello 主要資料庫從複製的資料。 這個程序稱為植入。 建立並植入次要資料庫之後，更新 toohello 主要資料庫會以非同步方式自動複寫 toohello 次要資料庫。 非同步複寫表示複寫的 toohello 次要資料庫之前，會 hello 主要資料庫上認可交易。 
* **可讀取次要資料庫**： 應用程式可以存取的次要資料庫的唯讀作業使用 hello 相同或不同的安全性主體用於存取 hello 主要資料庫。 hello 次要資料庫在運作，快照集隔離 hello 次要上執行的查詢不延遲模式 tooensure 複寫的主要 hello hello 更新 （重新顯示記錄檔）。

   > [!NOTE]
   > 如果沒有結構描述更新接收 hello 需要 hello 次要資料庫的結構描述鎖定的主要 hello 次要資料庫上 hello 記錄重新執行就會延遲。 
   > 

* **多個可讀取次要複本**： 兩個或多個次要資料庫增加備援和保護 hello 主要資料庫和應用程式層級。 如果存在多個次要資料庫，即使其中一個 hello 次要資料庫失敗 hello 應用程式仍受到保護。 如果只有一個次要資料庫，但又失敗，系統會公開 hello 應用程式建立新的次要資料庫之前 toohigher 風險。

   > [!NOTE]
   > 如果您使用作用中地理複寫 toobuild 全域散發的應用程式需要 tooprovide 唯讀存取 toodata 超過 4 區域中的，您可以建立次要的次要資料庫 （稱為鏈結的程序）。 如此一來您就可以達到幾乎無限擴充的資料庫複寫。 此外，鏈結可減少 hello 的 hello 主要資料庫複寫的額外負荷。 hello 代價是 hello 最分葉的次要資料庫上的 hello 增加的複寫延遲。 . 
   >

* **支援彈性集區資料庫**：您可以為任何彈性集區中的任何資料庫設定主動式異地複寫。 hello 次要資料庫可以是另一個彈性集區中。 一般的資料庫，次要 hello 可以彈性集區，而且相同，反之亦然 hello 只要 hello 服務層。 
* **Hello 次要資料庫可設定的效能層級**： 次要資料庫可以使用建立 hello 較低效能層級主要。 主要與次要資料庫所需 toohave hello 相同服務層。 這個選項不是建議應用程式使用高資料庫寫入活動因為 hello 增加的複寫延遲會增加容錯移轉之後的 hello 大量的資料遺失風險。 此外，容錯移轉 hello 應用程式的效能會受到影響之前 hello 新主要就升級的 tooa 較高的效能層級。 hello Azure 入口網站上的記錄 IO 百分比圖表提供很好的方式 tooestimate hello 所需要的 toosustain hello 複寫負載的 hello 次要的最少的效能層級。 例如，如果主要資料庫是 P6 (1000 DTU) 和其記錄 IO 百分比為 50 %hello 次要需要至少 toobe P4 (500 DTU)。 您也可以擷取 hello 記錄 IO 資料使用[sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)或[sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)資料庫檢視。  如需有關 hello SQL Database 效能層級的詳細資訊，請參閱[SQL Database 選項及效能](sql-database-service-tiers.md)。 
* **使用者控制的容錯移轉和容錯回復**:，次要資料庫可以明確 hello 應用程式或 hello 使用者隨時都能切換的 toohello 主要角色。 實際中斷 hello 期間 「 非計劃 」 選項應，其立即升級次要 toobe hello 主要。 Hello 失敗的主要復原和可用時同樣地，hello 系統自動標記 hello 復原主要為次要資料庫並使它與 hello 新主要複本的最新狀態。 由於複寫 toohello 非同步本質，少量資料可能會遺失未規劃的容錯移轉期間如果主要無法在複寫 hello 最新變更 toohello 次要前。 當多個次要複本與主要容錯移轉時，hello 系統會自動重新設定 hello 複寫關聯性和連結 hello 新剩餘的次要複本 toohello 升級主要而不需要使用者介入。 降低 hello 中斷造成 hello 容錯移轉之後，它可能會希望 tooreturn hello 應用程式 toohello 主要區域。 toodo hello 容錯移轉命令，應以 hello 叫用 「 計劃 」 選項。 
* **保持認證和防火牆規則的同步**： 我們建議使用[資料庫防火牆規則](sql-database-firewall-configure.md)地理複寫的資料庫，這些規則可以複寫 hello 資料庫 tooensure 與所有次要資料庫有hello hello 主要相同的防火牆規則。 這種方法可以降低對的客戶 toomanually 設定及維護主控同時 hello 主要與次要資料庫伺服器上的防火牆規則的 hello 需求。 同樣地，使用[自主資料庫使用者](sql-database-manage-logins.md)資料存取可確保主要與次要資料庫一律具有相同的使用者認證，因此容錯移轉期間，沒有任何中斷的 hello 與登入到期 toomismatches 和密碼。 Hello 加入[Azure Active Directory](../active-directory/active-directory-whatis.md)，客戶可以管理使用者存取 tooboth 主要和次要資料庫，以及消除 hello 需要完全管理資料庫中的認證。

## <a name="auto-failover-group-capabilities"></a>自動容錯移轉群組功能

自動容錯移轉群組功能支援群組層級的複寫和自動容錯移轉，提供強大的主動式異地複寫抽象概念。 此外，它會移除 hello 您不再需要 toochange hello SQL 連接字串在容錯移轉之後提供 hello 其他接聽程式端點。 

* **容錯移轉群組**︰可以在不同區域 (主要和次要伺服器) 的兩部伺服器之間建立一或多個容錯移轉群組。 每個群組可包含一或多個資料庫，以防所有或部分的主要資料庫變成無法使用，因為 tooan 中斷 hello 主要區域中，做為一個單位復原。  
* **主要伺服器**： 裝載 hello hello 容錯移轉群組中的主要資料庫的伺服器。
* **次要伺服器**： 裝載 hello hello 容錯移轉群組中的次要資料庫的伺服器。 hello 次要伺服器不能在 hello 與 hello 主要伺服器相同的區域。
* **加入資料庫 toofailover 群組**： 您可以放在伺服器中的多個資料庫，或在彈性集區至 hello 相同容錯移轉群組。 如果您新增獨立資料庫 toohello 群組時，它會自動建立次要資料庫使用 hello 相同的版本和效能層級。 如果 hello 主要資料庫是彈性集區中，次要 hello 會自動建立 hello 彈性集區中以 hello 相同名稱。 如果您新增已包含 hello 次要伺服器中的 次要資料庫的資料庫，hello 群組都會繼承，地理複寫。

   > [!NOTE]
   > 將已有不是 hello 容錯移轉群組一部分的伺服器中的 次要資料庫的資料庫時，hello 次要伺服器中建立新的次要資料庫。 
   >

* **容錯移轉群組讀取寫入接聽程式**： 做為格式正確的 DNS CNAME 記錄**&lt;容錯移轉-群組-名稱&gt;。.database.windows.net** ，以指 toohello 目前的主要伺服器 URL。 它允許 hello 讀寫 SQL 應用程式時容錯移轉之後變更 hello 主要 tootransparently 重新連線 toohello 主要資料庫。 
* **容錯移轉群組唯讀接聽程式**： 做為格式正確的 DNS CNAME 記錄**&lt;容錯移轉-群組-名稱&gt;。 secondary.database.windows.net** ，以指 toohello 次要伺服器的 URL。 它允許 hello 唯讀 tootransparently 連接的 SQL 應用程式使用 hello toohello 次要資料庫，指定負載平衡規則。 您可以選擇指定是否您想 hello 唯讀流量 toobe 自動重新導向 toohello 主要伺服器無法使用 hello 次要伺服器時。
* **自動容錯移轉原則**： 根據預設，使用自動容錯移轉原則設定 hello 容錯移轉群組。 一旦偵測到 hello 失敗 hello 系統會觸發容錯移轉。 如果您想從 hello 應用程式的 toocontrol hello 容錯移轉工作流程時，您可以關閉自動容錯移轉。 
* **手動容錯移轉**： 您可以在任何時間，而不管 hello 自動容錯移轉設定為何，手動起始容錯移轉。 如果自動容錯移轉原則無法設定的手動容錯移轉是必要的 toorecover hello 容錯移轉群組中的資料庫。 您可以起始強制或易用容錯移轉 (具有完整的資料同步處理)。 hello 後者可能是使用的 toorelocate hello active server toohello 主要區域。 完成容錯移轉時 hello DNS 記錄將會自動更新的 tooensure 連線 toohello 正確的伺服器。
* **會遺失資料的寬限期內**： 因為 hello 主要與次要資料庫已同步處理使用非同步複寫 hello 容錯移轉可能會導致資料遺失。 您可以自訂 hello 自動容錯移轉原則 tooreflect 應用程式的容錯 toodata 遺失。 藉由設定**GracePeriodWithDataLossHours**，您可以控制 hello 系統初始化 tooresult 可能資料遺失的 hello 容錯移轉之前等候的時間長度。 

   > [!NOTE]
   > 當系統偵測到 hello 群組中的 hello 資料庫均仍保持線上狀態 （例如，hello 中斷只影響 hello 服務控制平面），它會立即啟動 hello 容錯移轉，不論 hello 值的完整資料同步處理 （好記的容錯移轉）設定**GracePeriodWithDataLossHours**。 此行為可確保在 hello 復原期間會遺失任何資料。 hello 寬限期在易記的容錯移轉不可能時，才會生效。 Hello 中斷降低 hello 寬限期到期之前，如果未啟用 hello 容錯移轉。
   >

* **多個容錯移轉群組**： 您可以設定多個容錯移轉群組 hello 同一對伺服器的容錯移轉期間 toocontrol hello 標尺。 每個群組分別進行容錯移轉。 如果您的多租用戶應用程式使用彈性集區，您可以使用此功能 toomix 主要與次要資料庫中每個集區。 這種方式可以減少在 hello 影響的中斷 tooonly hello 租用戶的下半部。

## <a name="best-practices-of-building-highly-available-service"></a>建置高可用性服務的最佳作法

toobuild 高可用性的服務使用 Azure SQL database hello 客戶應該遵循這些指導方針：
- **使用容錯移轉群組**︰可以在位於不同區域 (主要和次要伺服器) 的兩部伺服器之間建立一或多個容錯移轉群組。 每個群組可包含一或多個資料庫，以防所有或部分的主要資料庫變成無法使用，因為 tooan 中斷 hello 主要區域中，做為一個單位復原。 hello 容錯移轉群組會建立相同服務做為 hello 主要目標的 hello 地理次要資料庫。 如果您將加入現有異地複寫關聯性 toohello 容錯移轉群組請確定 hello 地理-次要複本已設定相同服務等級目標為 hello 與 hello 主要。
- **使用針對 OLTP 工作負載的讀取寫入接聽程式**： 在執行 OLTP 作業使用**&lt;容錯移轉-群組-名稱&gt;。.database.windows.net**當 hello 伺服器 URL 和 hello 連線將會自動導向的 toohello 主要。 Hello 容錯移轉之後，不會變更此 URL。  
請注意 hello 容錯移轉牽涉到更新 DNS 記錄，所以 hello 用戶端連接會重新導向的 toohello 新主要 hello 用戶端之後，才 DNS 快取重新整理的 hello。
- **用於唯讀工作負載的唯讀狀態的接聽程式**： 如果您有邏輯上隔離的唯讀工作負載的容錯 toocertain 過時的資料，您可以使用 hello 次要資料庫中 hello 應用程式。 唯讀的工作階段使用**&lt;容錯移轉-群組-名稱&gt;。 secondary.database.windows.net**當 hello 伺服器 URL 和 hello 連接將會自動導向的 toohello 次要。 也建議您使用 **ApplicationIntent=ReadOnly**，在連接字串中表示讀取意圖。 
- **準備效能降低的**: hello 其餘 hello 應用程式或使用其他服務與 SQL 容錯移轉決策無關。 hello 應用程式可能是"mixed"的一個區域，在另一個部分中的部分元件。 tooavoid hello 變差，確保 hello DR 區域中的 hello 多餘的應用程式部署，並遵循本文章中的 hello 指導方針。  
請注意 hello DR 區域中的 hello 應用程式沒有 toouse 不同的連接字串。  
- **準備資料遺失的**： 如果沒有零的資料遺失 toohello 我們知識的最佳偵測到發生中斷時，如果 SQL 自動觸發讀寫容錯移轉。 否則，它會等候您所指定的 hello 週期**GracePeriodWithDataLossHours**。 如果您指定了 **GracePeriodWithDataLossHours**，請做好可能會遺失資料的心理準備。 服務中斷期間，Azure 一般會傾向維持可用性。 如果您無法容忍遺失資料，請確定 tooset **GracePeriodWithDataLossHours** tooa 夠大的數目，例如 24 小時。 


## <a name="upgrading-or-downgrading-a-primary-database"></a>升級或降級主要資料庫
您可以升級或降級的主要資料庫 tooa 不同的效能層級 （hello 內相同服務層） 而不中斷連線的任何次要資料庫。 升級時，我們建議您先升級 hello 次要資料庫，然後再升級 hello 主要。 降級時，會反向 hello 順序： 首先，降級 hello 主要和再降級 hello 次要資料庫。 當您升級或降級 hello 資料庫 tooa 不同服務層會強制執行這項建議。 

> [!NOTE]
> 如果您為 hello 容錯移轉群組組態的一部分建立次要資料庫不是建議的 toodowngrade hello 次要資料庫。 這是 tooensure 您的資料層擁有足夠的容量 tooprocess 您的一般工作負載後啟動容錯移轉。 
>

## <a name="preventing-hello-loss-of-critical-data"></a>防止 hello 遺失重要資料
由於廣域網路的 toohello 高延遲，連續複製採用非同步複寫機制。 如果發生失敗，非同步複寫導致部分資料遺失是無法避免的。 不過，有些應用程式可能會要求資料不能遺失。 tooprotect 這些重大更新、 應用程式開發人員可以呼叫 hello [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx)認可 hello 交易之後立即系統程序。 呼叫**sp_wait_for_database_copy_sync**區塊 hello 呼叫執行緒，直到 hello 最後認可的交易已經傳送 toohello 次要資料庫。 不過，它不會等候傳送嗨交易 toobe 重新執行，而且在次要 hello 認可。 **sp_wait_for_database_copy_sync**是已設定領域的 tooa 特定的連續複製連結。 具有 hello 連接權限 toohello 主要資料庫的任何使用者都可以呼叫此程序。

> [!NOTE]
> **sp_wait_for_database_copy_sync** 可避免在容錯移轉之後資料遺失，但是不保證讀取權限會完整同步。 hello 所造成的延遲**sp_wait_for_database_copy_sync**程序呼叫可能會很顯著，而在 hello 呼叫 hello 時間取決於 hello hello 交易記錄檔大小。 
> 

## <a name="programmatically-managing-failover-groups-and-active-geo-replication"></a>以程式設計方式管理容錯移轉群組和主動式異地複寫
如前所述，自動容錯移轉群組 （預覽） 和作用中地理複寫也可使用 Azure PowerShell 以程式設計方式，和 hello REST API。 hello 下表描述可用的命令 hello 集。

**Azure 資源管理員 API 和以角色為基礎的安全性**： 作用中地理複寫包含一組 Azure 資源管理員 Api 進行管理，包括 hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/)和[AzurePowerShell 指令程式](https://docs.microsoft.com/powershell/azure/overview)。 這些 Api 需要 hello 使用的資源群組，並支援以角色為基礎的安全性 (RBAC)。 如需有關如何 tooimplement 存取角色的詳細資訊，請參閱[所有存取控制](../active-directory/role-based-access-control-what-is.md)。

> [!NOTE]
> 只有在使用以 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 為基礎的 [Azure SQL REST API](https://msdn.microsoft.com/library/azure/mt163571.aspx) 和 [Azure SQL Database PowerShell Cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx) 時，才支援主動式異地複寫的許多新功能。 hello [（傳統） REST API](https://msdn.microsoft.com/library/azure/dn505719.aspx)和[Azure SQL Database （傳統） cmdlet](https://msdn.microsoft.com/library/azure/dn546723.aspx)支援回溯相容性，因此使用的 hello 建議使用 Azure Resource Manager 為基礎的 API。 
> 

## <a name="manage-sql-database-failover-using-using-transact-sql"></a>管理 SQL database 容錯移轉使用 TRANSACT-SQL

| 命令 | 說明 |
| --- | --- |
| [ALTER DATABASE (Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) |新增次要 ON SERVER 引數 toocreate 次要資料庫用於現有的資料庫，並開始資料複寫 |
| [ALTER DATABASE (Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) |使用容錯移轉或 FORCE_FAILOVER_ALLOW_DATA_LOSS tooswitch 次要資料庫 toobe 主要 tooinitiate 容錯移轉 |
| [ALTER DATABASE (Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) |使用移除次要 ON SERVER tooterminate SQL Database 與 hello 指定的次要資料庫之間的資料複寫。 |
| [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx) |傳回 hello Azure SQL Database 邏輯伺服器上的每個資料庫的所有現有複寫連結的相關資訊。 |
| [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx) |取得 hello 上次複寫的時間、 上次複寫延遲，以及其他相關資訊 hello 複寫連結指定的 SQL 資料庫。 |
| [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx) |會顯示 hello 包括 hello hello 複寫連結狀態的所有資料庫作業的狀態。 |
| [sp_wait_for_database_copy_sync (Azure SQL Database)](https://msdn.microsoft.com/library/dn467644.aspx) |會導致 hello 應用程式 toowait，直到所有已認可的交易都複寫及認可 hello 作用中次要資料庫為止。 |
|  | |

## <a name="manage-sql-database-failover-using-using-powershell"></a>SQL 資料庫容錯移轉使用使用 PowerShell 管理

| Cmdlet | 說明 |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |取得一或多個資料庫。 |
| [New-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary) |針對現有資料庫建立次要資料庫並開始資料複寫。 |
| [Set-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary) |切換次要資料庫 toobe 主要 tooinitiate 容錯移轉。 |
| [Remove-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) |終止 SQL Database 與 hello 指定的次要資料庫之間的資料複寫。 |
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) |取得 Azure SQL Database 與資源群組或 SQL Server 之間的 hello 異地複寫連結。 |
| [New-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   此命令會建立容錯移轉群組，並同時在主要和次要伺服器上註冊|
| [Remove-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/remove-azurermsqldatabasefailovergroup) | 移除 hello 伺服器 hello 容錯移轉群組，並刪除所有包含的次要資料庫 hello 群組 |
| [Get-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/get-azurermsqldatabasefailovergroup) | 擷取 hello 容錯移轉群組組態 |
| [Set-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   修改 hello hello 容錯移轉群組組態 |
| [Switch-AzureRMSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/switch-azurermsqldatabasefailovergroup) | 觸發程序的 hello 容錯移轉群組 toohello 次要伺服器的容錯移轉 |
|  | |

> [!IMPORTANT]
> 如需範例指令碼，請參閱[使用作用中異地複寫設定單一資料庫並進行容錯移轉](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)、[使用作用中異地複寫設定集區資料庫並進行容錯移轉](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md)和[設定單一資料庫的容錯移轉群組並進行容錯移轉] \(預覽\) (scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md。
>

## <a name="manage-sql-database-failover-using-hello-rest-api"></a>管理 SQL database 容錯移轉使用 hello REST API
| API | 說明 |
| --- | --- |
| [Create or Update Database (createMode=Restore)](/rest/api/sql/Databases/CreateOrUpdate) |建立、更新或還原主要或次要資料庫。 |
| [取得建立或更新資料庫狀態](/rest/api/sql/Databases/CreateOrUpdate) |建立作業期間傳回 hello 狀態。 |
| [將次要資料庫設定為主要資料庫 (計劃性容錯移轉)](https://docs.microsoft.com/rest/api/sql/replicationlinkss#ReplicationLinks_Failover) |設定哪些複本資料庫是主要由從目前主要複本資料庫 hello 容錯移轉。 |
| [將次要資料庫設定為主要資料庫 (非計劃的容錯移轉)](https://docs.microsoft.com/rest/api/sql/replicationlinks#ReplicationLinks_FailoverAllowDataLoss) |設定哪些複本資料庫是主要由從目前主要複本資料庫 hello 容錯移轉。 這項作業可能會導致資料遺失。 |
| [取得複寫連結](/rest/api/sql/replicationlinks/get) |取得異地複寫關聯性中指定 SQL Database 的特定複寫連結。 它會擷取 hello hello sys.geo_replication_links 目錄檢視中顯示的資訊。 |
| [複寫連結 - 依資料庫列示](/rest/api/sql/replicationlinks/listbydatabase) | 取得異地複寫關聯性中指定 SQL Database 的所有複寫連結。 它會擷取 hello hello sys.geo_replication_links 目錄檢視中顯示的資訊。 |
| [刪除複寫連結](/rest/api/sql/databases/delete) | 刪除資料庫複寫連結。 無法在容錯移轉期間進行。 |
| [建立或更新容錯移轉群組]/rest/api/sql/failovergroups/createorupdate) | 建立或更新容錯移轉群組 |
| [刪除容錯移轉群組](/rest/api/sql/failovergroups/delete) | Hello 容錯移轉群組移除伺服器 hello |
| [容錯移轉 (計劃性)](/rest/api/sql/failovergroups/failover) | 從目前的主要伺服器 toothis 伺服器 hello 容錯移轉。 |
| [強制容錯移轉允許資料遺失](/rest/api/sql/failovergroups/forcefailoverallowdataloss) |從目前的主要伺服器 toothis 伺服器 hello ails 透過。 這項作業可能會導致資料遺失。 |
| [取得容錯移轉群組](/rest/api/sql/failovergroups/get) | 取得容錯移轉群組。 |
| [依伺服器列出容錯移轉群組](/rest/api/sql/failovergroups/listbyserver) | 列出在伺服器中的 hello 容錯移轉群組。 |
| [更新容錯移轉群組](/rest/api/sql/failovergroups/update) | 更新容錯移轉群組。 |
|  | |

## <a name="next-steps"></a>後續步驟
* 如需範例指令碼，請參閱：
   - [使用作用中異地複寫設定單一資料庫並進行容錯移轉](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
   - [使用作用中異地複寫設定集區資料庫並進行容錯移轉](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md)
   - [設定單一資料庫的容錯移轉群組並進行容錯移轉 (預覽)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md)
* 如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)
* toolearn 有關自動化 Azure SQL Database 備份，請參閱[SQL 資料庫自動備份](sql-database-automated-backups.md)。
* toolearn 有關使用自動的備份進行復原，請參閱[hello 服務起始的備份還原的資料庫](sql-database-recovery-using-backups.md)。
* toolearn 有關驗證需求，針對新的主要伺服器和資料庫，請參閱[後嚴重損壞修復的 SQL Database 安全性](sql-database-geo-replication-security-config.md)。

