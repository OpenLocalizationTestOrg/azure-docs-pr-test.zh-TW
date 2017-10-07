---
title: "aaaSQL (PaaS) 資料庫與Hello Vm (IaaS) 雲端中的 SQL Server |Microsoft 文件"
description: "了解哪種的雲端 SQL Server 選項適合您的應用程式: (PaaS) 的 Azure SQL Database 或在 hello 雲端 Azure 虛擬機器上的 SQL Server。"
services: sql-database, virtual-machines
keywords: "SQL Server 雲端，在 hello 雲端中，PaaS 資料庫的 SQL Server 雲端的 SQL Server，DBaaS"
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cjgronlund
ms.assetid: 7467f422-b77d-4b60-9cb5-0f1ec17ec565
ms.service: sql-database
ms.custom: DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: carlrab
ms.openlocfilehash: 1b462a9a822d04dc5deb8422ed505a5d09279253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-cloud-sql-server-option-azure-sql-paas-database-or-sql-server-on-azure-vms-iaas"></a>選擇雲端 SQL Server 選項：Azure SQL (PaaS) Database 或 Azure VM 上的 SQL Server (IaaS)
Azure 有兩個選項可在 Microsoft Azure 主控 SQL Server 工作負載：

* [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)： 的 SQL 資料庫原生 toohello 雲端，也就是平台即服務 (PaaS) 資料庫或資料庫最適合用於軟體做為服務 (SaaS) 應用程式開發的服務 (DBaaS)。 它提供與大部分 SQL Server 功能的相容性。 如需 PaaS 的詳細資訊，請參閱 [何謂 PaaS](https://azure.microsoft.com/overview/what-is-paas/)。
* [Azure 虛擬機器上的 SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/)： 安裝及裝載於 Azure，也稱為基礎結構即服務 (IaaS) 上執行的 hello 雲端 Windows 伺服器虛擬機器 (Vm) 上的 SQL Server。
  Azure 虛擬機器上的 SQL Server 已最佳化，適合用來移轉現有的 SQL Server 應用程式。 所有 hello 版本和 SQL Server 的版本可用。 它提供與 SQL Server，允許您 toohost 的 100%相容性為多個資料庫為必要且正在執行的跨資料庫交易。 它能完整控制 SQL Server 和 Windows。

了解每個選項如何融入 hello Microsoft 資料平台，以及取得說明相符 hello 右選項 tooyour 商務需求。 無論您排定優先順序節省成本或晚於所有其他項目最基本的管理，這篇文章能夠幫助您決定哪種方法提供對您最關心的 hello 商務需求。

## <a name="microsofts-data-platform"></a>Microsoft 的資料平台
Hello 第一件事 toounderstand 在 Azure 與內部部署 SQL Server 資料庫的任何討論中的其中一個是您可以使用它。 Microsoft 資料平台會利用 SQL Server 技術，使其可在跨內部部署實體機器、私人雲端環境、協力廠商代管的私人雲端環境，和公用雲端中使用。 Azure 虛擬機器上的 SQL Server 可讓您透過在內部部署和雲端主控部署的組合 toomeet 唯一且不同的商務需求時使用這些跨 hello 組相同的伺服器產品，開發工具和專業知識環境。

   ![雲端 SQL Server 選項： hello 雲端中的 IaaS 或 SaaS SQL 上的 SQL server 資料庫。](./media/sql-database-paas-vs-sql-server-iaas/SQLIAAS_SQL_Server_Cloud_Continuum.png)

Hello 圖表所示，每個供應項目可以是依區別 hello 層級，您可以對 hello 基礎結構 （在 hello X 軸） 管理的資料庫層級的彙總及自動化 （在 hello Y 軸） 來達成的成本效益的 hello 程度。

應用程式時，就有一個四個基本選項可供裝載 hello hello 應用程式的 SQL Server 組件：

* 非虛擬化實體機器上的 SQL Server
* 內部部署虛擬機器中的 SQL Server (私人雲端)
* Azure 虛擬機器中的 SQL Server (Microsoft 公用雲端)
* Azure SQL Database (Microsoft 公用雲端)

在下列各節的 hello，您了解 SQL Server hello Microsoft 公用雲端中： Azure SQL Database 和 Azure Vm 上的 SQL Server。 此外，還會探討常見的商業動機，以判斷哪一個選項最符合應用程式需求。

## <a name="a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms"></a>仔細看看 Azure SQL Database 和 Azure VM 上的 SQL Server
**Azure SQL Database**是關聯式資料庫做為服務 (DBaaS) hello hello 業界類別所處的 Azure 雲端中裝載*軟體做為服務 (SaaS)*和*平台做為服務(PaaS)*. [SQL Database](sql-database-technical-overview.md) 會建立在 Microsoft 所擁有、代管及維護的標準化硬體和軟體上。 使用 SQL 資料庫時，您可以直接使用內建的特性與功能的 hello 服務上開發。 當使用 SQL 資料庫中，隨用隨付與選項 tooscale 增加或放大的更佳的能力，不中斷。

**Azure 虛擬機器 (Vm) 上的 SQL Server**落在 hello 業界類別*基礎結構做為服務 (IaaS)*並可讓您 toorun SQL Server hello 雲端中虛擬機器內。 類似 tooSQL 資料庫，它是內建擁有、 主控和 Microsoft 維護的標準化硬體上。 在 VM 上使用 SQL Server 時，您可以隨收隨付以取得已經包含在 SQL Server 映像中的 SQL Server 授權或者輕鬆使用現有的授權。 您也可以輕鬆地向向上/向下和暫停/繼續 hello VM 所需。

一般而言，這兩個 SQL 選項適合用於不同的用途：

* **Azure SQL Database**整體成本是最佳化的 tooreduce toohello 佈建和管理多個資料庫的最小值。 它可以降低進行中的管理成本，因為您沒有 toomanage 任何虛擬機器、 作業系統或資料庫軟體。 您不需要 toomanage 升級高可用性，或[備份](sql-database-automated-backups.md)。 一般情況下，Azure SQL Database 可以大幅增加使用單一的管理資料庫的 hello 數目 IT 或開發資源。
* **Azure Vm 上執行的 SQL Server**已針對移轉現有的應用程式 tooAzure 或擴充現有的內部部署混合式部署中的應用程式 toohello 雲端最佳化。 此外，您可以在虛擬機器 toodevelop 使用 SQL Server，並測試傳統的 SQL Server 應用程式。 透過在 Azure Vm 上的 SQL Server，您會在專用的 SQL Server 執行個體和以雲端為基礎的 VM 有 hello 完整系統管理權限。 當組織已有 IT 資源可用 toomaintain hello 虛擬機器時，它是完美的選擇。 這些功能可讓您 toobuild 高度自訂的系統 tooaddress 您的應用程式特定的效能和可用性需求。

hello 下表摘要說明 hello 的 SQL Database 和 Azure Vm 上的 SQL Server 的主要特性：

| **最適合：** | **Azure SQL Database** | **Azure 虛擬機器中的 SQL Server** |
| --- | --- | --- |
|  |開發與行銷階段有時間限制的新雲端式設計應用程式。 |需要快速移轉 toohello 雲端最少變更的現有應用程式。 快速開發和測試案例時不想讓 toobuy 內部非實際執行 SQL Server 的硬體。 |
|  | 需要 hello 資料庫內建的高可用性、 災害復原和升級的團隊。 |可以設定和管理高可用性、災害復原及修補 SQL Server 的團隊。 某些所提供的自動化功能大幅簡化了這部分。 | |
|  | 不要 toomanage hello 基礎作業系統和組態設定的團隊。 |您需要包含完整系統管理權限的自訂環境。 | |
|  | 資料庫的總 too4 TB 或可能是資料庫較大[水平或垂直分割](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling)使用向外延展模式。 |SQL Server 執行個體與向上 too64 TB 的儲存體。 hello 執行個體可以支援所需的資料庫。 | |
|  | [建置軟體即服務 (SaaS) 應用程式](sql-database-design-patterns-multi-tenancy-saas-applications.md)。 |移轉和建置企業和混合式應用程式。 | |
|  | | |
| **資源：** |您不想 tooemploy IT 資源的設定和管理 hello 基礎基礎結構，但想 toofocus hello 應用程式層上的。 |您有一些設定和管理的 IT 資源。 某些所提供的自動化功能大幅簡化了這部分。 |
| **擁有權的總成本：** |排除硬體成本，並降低管理成本。 |排除硬體成本。 |
| **業務持續性︰** |加法 toobuilt 中容錯基礎結構功能，在 Azure SQL Database 提供的功能，例如[自動化備份](sql-database-automated-backups.md)，[時間點還原](sql-database-recovery-using-backups.md#point-in-time-restore)，[異地還原](sql-database-recovery-using-backups.md#geo-restore)，和[作用中地理複寫](sql-database-geo-replication-overview.md)tooincrease 業務持續性。 如需詳細資訊，請參閱 [SQL Database 業務持續性概觀](sql-database-business-continuity.md)。 |Azure VM 上的 SQL Server 可讓您設定高可用性和災害復原解決方案，以滿足您資料庫的特定需求。 因此，您可以有已針對您的應用程式進行高度最佳化的系統。 您可以視需要自我測試並執行容錯移轉。 如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 高可用性和災害復原](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md)。 |
| **混合式雲端：** |您的內部部署應用程式可以存取 Azure SQL Database 中的資料。 |使用 Azure Vm 上的 SQL Server，您可以有部分在 hello 雲端中執行的應用程式，並部分在內部。 例如，您可以擴充您的內部部署網路和 Active Directory 網域 toohello 雲端透過[Azure 虛擬網路](../virtual-network/virtual-networks-overview.md)。 此外，您可以使用 [Azure 中的 SQL Server 資料檔案](http://msdn.microsoft.com/library/dn385720.aspx)，將內部部署資料檔案儲存在 Azure 儲存體中。 如需詳細資訊，請參閱[簡介 tooSQL Server 2014 混合雲端](http://msdn.microsoft.com/library/dn606154.aspx)。 |
|  | 支援[SQL Server 異動複寫](https://msdn.microsoft.com/library/mt589530.aspx)做為訂閱者 tooreplicate 資料。 |完全支援[SQL Server 異動複寫](https://msdn.microsoft.com/library/mt589530.aspx)， [AlwaysOn 可用性群組](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md)，Integration Services 和記錄傳送 tooreplicate 資料。 此外也完全支援傳統的 SQL Server 備份 | |
|  | | |

## <a name="business-motivations-for-choosing-azure-sql-database-or-sql-server-on-azure-vms"></a>選擇 Azure VM 上的 Azure SQL Database 或 SQL Server 時的商業動機
### <a name="cost"></a>成本
正在 strapped 現金，啟動還是緊密預算條件約束，受限於資金下的運作方式建立公司小組通常 hello 主要驅動程式時決定如何 toohost 您的資料庫。 在本節中，您了解 hello 計費和授權與 Azure 中的基本概念視為兩個關聯式資料庫選項 toothese: SQL Database 和 Azure Vm 上的 SQL Server。 您也了解計算 hello 總應用程式的成本。

#### <a name="billing-and-licensing-basics"></a>計費和授權基本概念
**SQL Database**銷售 toocustomers 為服務時，不具有授權。  [Azure VM 上的 SQL Server](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md) 銷售包含您以每分鐘支付的授權。 如果您有現有的授權也可以使用。  

目前， **SQL Database**是適用於數個服務層，全部都是會根據 hello 服務層和效能層級您選擇以固定費率每小時計費。 此外，傳出的網際網路流量也會以一般 [資料傳輸費率](https://azure.microsoft.com/pricing/details/data-transfers/)計費。 hello Basic、 Standard、 Premium 和 RS Premium 服務層是設計 toodeliver 可預測的效能與多個效能層級 toomatch 應用程式的尖峰需求。 您可以變更服務層和效能層級 toomatch 應用程式的各種的輸送量需求之間。 如果您的資料庫具有高交易式磁碟區和需求 toosupport 許多並行使用者，我們建議 hello Premium 服務層。 Hello hello 目前支援的服務層上的最新資訊，請參閱[Azure SQL Database 服務層](sql-database-service-tiers.md)。 您也可以建立[彈性集區](sql-database-elastic-pool.md)tooshare 效能資料庫執行個體之間的資源。

與**SQL Database**，hello 資料庫軟體會自動設定、 修補，並升級 microsoft，系統管理的成本。 此外，它 [內建的備份](sql-database-automated-backups.md) 功能可協助您達到有效節省成本，尤其是當您擁有為數眾多的資料庫時效果更為顯著。

與**Azure Vm 上的 SQL Server**，您可以使用任何 hello 平台提供 SQL Server 映像 （其中包括授權），或將您的 SQL Server 授權。 所有的 hello 支援的 SQL Server 版本 (2008R2、 2012年、 2014年、 2016年) 和 （Developer、 Express、 Web、 Standard、 Enterprise） 的版本可用。 此外，將帶您-擁有的授權版本 (BYOL) 的 hello 映像使用。 當使用 Azure 提供映像的 hello，hello 營運成本會依 hello VM 大小與 hello 您選擇的 SQL Server 版本而定。 不論 VM 大小或 SQL Server 版本，您必須支付每分鐘授權成本的 SQL Server 和 Windows Server 以及 hello hello VM 磁碟的 Azure 儲存體成本。 hello 每分鐘計費選項可讓您視需要而不購買加入 SQL Server 授權久 toouse SQL Server。 如果您將自己的 SQL Server 授權 tooAzure，您必須支付 Windows Server 和只有儲存體成本。 如需採用自己的授權的詳細資訊，請參閱 [Azure 上透過軟體保證的授權機動性](https://azure.microsoft.com/pricing/license-mobility/)。

#### <a name="calculating-hello-total-application-cost"></a>計算成本 hello 總應用程式
當您開始使用雲端平台時，執行您的應用程式中的 hello 成本包含 hello 開發和管理成本，加上 hello 公用雲端平台服務成本。

以下是 hello Azure Vm 上執行 SQL Database 和 SQL Server 中的應用程式的詳細的成本計算：

**使用 Azure SQL Database 時：**

*應用程式的總成本 = 降到最低的系統管理成本 + 軟體開發成本 + SQL Database 服務成本*

**使用 Azure VM 上的 SQL Server 時：**

*應用程式的總成本 = 大幅縮減的軟體開發成本 + 系統管理成本 + SQL Server 與 Windows Server 授權成本 + Azure 儲存體成本*

如需定價的詳細資訊，請參閱下列資源的 hello:

* [SQL Database 定價](https://azure.microsoft.com/pricing/details/sql-database/)
* [SQL](https://azure.microsoft.com/pricing/details/virtual-machines/#sql) 和 [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#windows) 的[虛擬機器價格](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Azure 價格計算機](https://azure.microsoft.com/pricing/calculator/)

> [!NOTE]
> SQL Server 上有一小部分不適用於或無法使用於 SQL Database 的功能。 如需詳細資訊，請參閱 [SQL Database 功能](sql-database-features.md)和 [SQL Database Transact-SQL 資訊](sql-database-transact-sql-information.md)。 如果您要移動現有的 SQL Server 方案 toohello 雲端，請參閱[移轉 SQL 資料庫的 SQL Server 資料庫 tooAzure](sql-database-cloud-migrate.md)。 當您移轉現有內部部署 SQL Server 應用程式 tooSQL 資料庫時，請考慮更新 hello 應用程式 tootake 利用 hello 雲端服務提供的功能。 例如，您可以考慮使用[Azure Web 應用程式服務](https://azure.microsoft.com/services/app-service/web/)或[Azure 雲端服務](https://azure.microsoft.com/services/cloud-services/)toohost 您應用程式層 tooincrease 成本效益。
> 
> 

### <a name="administration"></a>系統管理
對許多企業來說，hello 決策 tootransition tooa 雲端服務是像很多關於卸載複雜性管理，因為它的成本。 與**SQL Database**，Microsoft 會管理 hello 基礎硬體。 Microsoft 會自動複寫所有資料 tooprovide 高可用性、 設定和升級 hello 資料庫軟體、 管理負載平衡，並且沒有透明容錯移轉伺服器失敗時。 您可以繼續 tooadminister 您的資料庫，但您不需要再 toomanage hello database engine、 伺服器作業系統或硬體。  您可以繼續的項目的範例 tooadminister 包括資料庫和登入、 索引和查詢微調和稽核和安全性。

與**Azure Vm 上的 SQL Server**，您擁有 hello 作業系統和 SQL Server 執行個體組態的完整控制權。 Vm，則由 tooyou toodecide tooupdate/升級 hello 作業的系統和資料庫軟體，而且時 tooinstall 任何額外的軟體，例如防毒程式。 某些自動化的功能可提供 toodramatically 簡化修補、 備份和高可用性。 此外，您可以控制 hello hello VM 大小、 hello 磁碟數目和其存放裝置設定。 Azure 可讓您的 VM，視 toochange hello 大小。 如需相關資料，請參閱 [Azure 的虛擬機器和雲端服務大小](../virtual-machines/windows/sizes.md)。 

### <a name="service-level-agreement-sla"></a>服務等級協定 (SLA)
對於許多 IT 部門而言，達到服務等級協定 (SLA) 的正常運作時間義務是首要任務。 在本節中，我們查看 SLA 適用於 tooeach 資料庫裝載選項。

對於 **SQL Database** 基本、標準和進階 RS 服務層，Microsoft 提供 99.99% 的可用性 SLA。 Hello 最新的資訊，請參閱[服務等級協定](https://azure.microsoft.com/support/legal/sla/sql-database/)。 Hello 最新版 SQL Database 服務層和 hello 支援業務續航力計畫的資訊，請參閱[服務層](sql-database-service-tiers.md)。

如**Azure Vm 上執行的 SQL Server**，Microsoft 提供的可用性 SLA 是 99.95%涵蓋只 hello 虛擬機器。 本 SLA 並未涵蓋 hello 程序 （例如 SQL Server) hello VM 上執行，而且需要您裝載的可用性設定組中的至少兩個 VM 執行個體。 Hello 最新的資訊，請參閱 hello [VM SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)。 資料庫高可用性 (HA) Vm 內，您應該設定 hello 支援高可用性選項的其中一個在 SQL Server，例如[AlwaysOn 可用性群組](http://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx)。 使用支援的高可用性選項不會提供額外的 SLA，但可讓您 tooachieve > 99.99%資料庫可用性。

### <a name="market"></a>時間 toomarket
**SQL Database**是 hello 絕佳的解決方案，針對雲端設計應用程式開發人員生產力和快速時間市場而言非常重要。 以程式設計方式 DBA 類似的功能，它是適合雲端架構設計人員和開發人員會它降低 hello 需要管理基礎作業系統 hello 和資料庫。 例如，您可以使用 hello [REST API](http://msdn.microsoft.com/library/azure/dn505719.aspx)和[PowerShell Cmdlet](http://msdn.microsoft.com/library/mt740629.aspx) tooautomate 和管理針對擁有成千上萬個資料庫的系統管理作業。 這類功能[彈性集區](sql-database-elastic-pool.md)允許您 toofocus hello 應用程式層和更快交付解決方案 toohello 市場。

**Azure Vm 上執行的 SQL Server**是完美的如果您現有的或新的應用程式需要大型資料庫，彼此相關的資料庫，或存取 SQL Server 或 Windows 中的 tooall 功能。 它也是調整當您想 toomigrate 現有內部部署應用程式和資料庫做為 tooAzure-是。 您不需要 toochange hello 簡報、 應用程式，以及資料層級，因為您節省時間和預算投入重新架構您現有的方案。 相反地，您可以專注在移轉您的所有方案 tooAzure，在此情況下可能需要 hello Azure 平台的一些效能最佳化。 如需詳細資訊，請參閱 [Azure 虛擬機器中 SQL Server 的效能最佳作法](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)。

## <a name="summary"></a>摘要
本文探討了 SQL Database 和 Azure 虛擬機器 (VM) 上的 SQL Server，並討論可能會影響您的決策的常見商業動因。 hello 以下是您 tooconsider 建議的摘要：

如果是下列情形，請選擇 **Azure SQL Database** ：

* 您已建立新雲端應用程式 tootake 優點 hello 成本的節省空間及效能最佳化，雲端服務提供。 這種方法會提供管理完善的雲端服務的 hello 優點，可協助降低初始時間上市，而且可以提供長期的成本最佳化。
* 您想要 toohave Microsoft 執行一般的管理作業，在您的資料庫和資料庫需要更強的可用性 Sla。

如果是下列情形，請選擇 [Azure VM 上的 SQL Server]  ：

* 您有現有的內部部署應用程式您想 toomigrate 或擴充 toohello 雲端，或如果您想 toobuild 企業應用程式超過 4 TB。 此方法提供 100 %sql 相容性，大型資料庫的容量，完整控制 SQL Server 和 Windows 和安全通道 tooon 內部部署的 hello 的好處。 這個方法可以降低開發和修改現有應用程式的成本。
* 您有現有的 IT 資源，且最終可以擁有修補、備份和資料庫高可用性。 請注意，某些自動化功能大幅簡化了這些作業。 

## <a name="next-steps"></a>後續步驟
* 請參閱[第一個 Azure SQL Database](sql-database-get-started-portal.md) tooget 開始使用 SQL Database。
* 請參閱 [SQL Database 價格](https://azure.microsoft.com/pricing/details/sql-database/)。
* 請參閱[佈建 Azure 中的 SQL Server 虛擬機器](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md)tooget 開始使用 Azure Vm 上的 SQL Server。

