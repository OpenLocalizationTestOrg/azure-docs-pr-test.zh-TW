---
title: "aaaSQL 伺服器在 Azure 虛擬機器常見問題集 |Microsoft 文件"
description: "本文提供的解答 toofrequently 的 Azure Vm 上執行 SQL Server 相關常見問題。"
services: virtual-machines-windows
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: v-shysun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a8777bf765dcc69f433aa1fb59eb94929caab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Azure 虛擬機器上 SQL Server 的常見問題集
本主題提供的答案 toosome hello 的最常見的問題，需執行[Azure 虛擬機器上的 SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/)。

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>常見問題集

1. **如何使用 SQL Server 建立 Azure 虛擬機器？**

    hello 最簡單的解決方案是 toocreate 包含 SQL Server 虛擬機器。 如需註冊 Azure，並建立從 hello 入口網站的 SQL VM 的教學課程，請參閱[hello Azure 入口網站中的 SQL Server 虛擬機器佈建](virtual-machines-windows-portal-sql-server-provision.md)。 您可以選取使用授權，支付每分鐘 SQL Server 的虛擬機器映像，或者您可以使用映像，可讓您 toobring 您自己的 SQL Server 授權。 您也可以手動在 VM 上安裝 SQL Server 和重複使用內部部署授權 hello 選項。 如果您自備授權，必須具備 [Azure 上透過軟體保證的授權流動性](https://azure.microsoft.com/pricing/license-mobility/)。 如需詳細資訊，請參閱 [SQL Server Azure VM 的定價指導方針](virtual-machines-windows-sql-server-pricing-guidance.md)。

1. **Hello SQL Vm 與 hello SQL Database 服務之間的差異為何？**

    從概念上來說，在 Azure 虛擬機器上執行 SQL Server 與在遠端資料中心中執行 SQL Server 並沒什麼不同。 對比之下， [SQL Database](../../../sql-database/sql-database-technical-overview.md) 可提供資料庫即服務的功能。 使用 SQL 資料庫時，您沒有存取 toohello 機器主控您的資料庫。 如需完整的比較，請參閱 [選擇雲端 SQL Server 選項：Azure SQL (PaaS) Database 或 Azure VM 上的 SQL Server (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md)。

1. **我要如何移轉我的內部部署 SQL Server 資料庫 toohello 雲端？**

    首先，請使用 SQL Server 執行個體來建立 Azure 虛擬機器。 然後將移轉您的內部部署資料庫 toothat 執行個體。 資料移轉策略，請參閱[移轉 Azure VM 中的伺服器的 SQL Server 資料庫 tooSQL](virtual-machines-windows-migrate-sql.md)。

1. **可以安裝 SQL Server 的第二個執行個體上 hello 相同 VM？可以變更 hello 預設執行個體已安裝的功能嗎？**

    是。 hello SQL Server 安裝媒體位於 hello 上的資料夾中**C**磁碟機。 執行**Setup.exe**從該位置 tooadd 新 SQL Server 執行個體或 SQL Server 上 hello toochange 其他安裝功能。 請注意，某些功能，例如自動備份，自動修補和 Azure 金鑰保存庫整合，只對 hello 預設執行個體。

1. **我可以解除安裝 SQL Server hello 預設執行個體嗎？**

    是。 但有一些考量。 Hello 上一個答案，依賴 hello 功能中所述[SQL Server IaaS 代理程式延伸模組](virtual-machines-windows-sql-server-agent-extension.md)只 hello 預設執行個體上操作。 如果您解除安裝 hello 預設執行個體，hello 延伸模組會持續 toolook，並可能會產生事件記錄檔錯誤。 這些錯誤會從下列兩個來源的 hello: **Microsoft SQL Server 認證管理**和**Microsoft SQL Server IaaS Agent**。 其中一個 hello 錯誤可能是類似 toohello 下列：
    
        A network-related or instance-specific error occurred while establishing a connection tooSQL Server. hello server was not found or was not accessible. 
        
    如果您決定 toouninstall hello 預設執行個體，同時解除安裝 hello [SQL Server IaaS 代理程式延伸模組](virtual-machines-windows-sql-server-agent-extension.md)以及。

1. **如何升級 tooa 新版本/版的 hello Azure VM 中的 SQL Server？**

    目前，在 Azure VM 中執行的 SQL Server 不提供任何就地升級。 使用所需的 hello SQL Server 版本/版時，建立新的 Azure 虛擬機器，然後再移轉資料庫 toohello 新的伺服器使用標準[資料移轉技術](virtual-machines-windows-migrate-sql.md)。

1. **如何在 Azure VM 上安裝 SQL Server 授權版本？**

    有兩種方式 toodo 這。 您可以佈建一個 hello[支援授權的虛擬機器映像](virtual-machines-windows-sql-server-iaas-overview.md#BYOL)。 另一個選項是 toocopy hello SQL Server 安裝媒體 tooa Windows Server VM，，然後在 hello VM 上安裝 SQL Server。 基於授權原因，您必須具備 [Azure 上透過軟體保證的授權流動性](https://azure.microsoft.com/pricing/license-mobility/)。 如需詳細資訊，請參閱 [SQL Server Azure VM 的定價指導方針](virtual-machines-windows-sql-server-pricing-guidance.md)。

1. **我可以變更 VM toouse 我自己的 SQL Server 授權如果所建立的其中一個 hello 隨用隨付圖庫映像嗎？**

    否。 您可以切換支付每分鐘授權 toousing 從自己的授權。 建立新 Azure 虛擬機器使用其中一種 hello [BYOL 映像](virtual-machines-windows-sql-server-iaas-overview.md#BYOL)，然後再移轉資料庫 toohello 新的伺服器使用標準[資料移轉技術](virtual-machines-windows-migrate-sql.md)。

1. **Azure VM 上是否支援 SQL Server 容錯移轉叢集執行個體 (FCI)？**

   是。 您可以[建立 Windows 容錯移轉叢集 Windows Server 2016 上](virtual-machines-windows-portal-sql-create-failover-cluster.md)及 hello 叢集存放區用於儲存空間直接存取 (S2D)。 或者，您可以使用 [Azure 虛擬機器中的 SQL Server 的高可用性和災害復原](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions)中所述的協力廠商叢集或儲存體解決方案。

1. **如果只待命/容錯移轉使用是否有 toopay toolicense Azure VM 上的 SQL Server？**

    您不需要 toopay toolicense 一個 SQL Server 參與為被動的次要複本在 HA 部署中，如果您擁有軟體保證和中所述，使用的授權流動性[虛擬機器授權常見問題集](http://azure.microsoft.com/pricing/licensing-faq/)。

1. **如何將更新和 Service Pack 套用到 SQL Server VM 上？**

    虛擬機器可讓您控制 hello 主機電腦，包括何時及如何套用更新。 Hello 作業系統，您可以手動套用 windows 更新，或者您可以啟用排程的服務呼叫[自動修補](virtual-machines-windows-sql-automated-patching.md)。 自動修補會安裝任何標示為重要的更新，包括該類別目錄中的 SQL Server 更新。 伺服器必須手動安裝其他選用的更新 tooSQL。

1. **它是不會顯示 hello （適用於 Windows 2008 R2 範例 + SQL Server 2012） 的虛擬機器映像庫中的組態設定可能 tooset 嗎？**

    否。 針對包含 SQL Server 虛擬機器圖庫映像，您必須選取其中一個 hello 提供映像。

1. **如何在 Azure VM 上安裝 SQL 資料工具？**

     下載並安裝從 hello SQL Data tools [Microsoft SQL Server Data Tools-Business Intelligence for Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=42313)。

## <a name="resources"></a>資源

如需 SQL Server 在 Azure 虛擬機器的概觀，請觀看影片，hello [Azure VM 是 SQL Server 2016 hello 最佳平台](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016)。 您也可以在 hello 主題中，取得絕佳的簡介[Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)。

其他資源包括：

* [佈建 hello Azure 入口網站中的 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)
* [移轉資料庫 tooSQL Azure VM 上的伺服器](virtual-machines-windows-migrate-sql.md)
* [Azure 虛擬機器中的 SQL Server 高可用性和災害復原](virtual-machines-windows-sql-high-availability-dr.md)
* [Azure 虛擬機器中的 SQL Server 效能最佳做法](virtual-machines-windows-sql-performance.md)
* [Azure 虛擬機器中的 SQL Server 應用程式模式和開發策略](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 