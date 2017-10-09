---
title: "SQL server 在 Azure 虛擬機器 aaaOverview |Microsoft 文件"
description: "深入了解如何 toorun 完全在 Azure 虛擬機器上的 SQL Server 版本。 取得直接連結 tooall SQL Server VM 映像和相關的內容。"
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: 07be567c76f4435961592fc0872fe41cd45bd79d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-sql-server-on-azure-virtual-machines"></a>Azure 虛擬機器上的 SQL Server 概觀
本主題描述 Azure 虛擬機器 (Vm) 上執行 SQL Server 的選項，連同[連結 tooportal 映像](#option-1-create-a-sql-vm-with-per-minute-licensing)和概觀[一般工作](#manage-your-sql-vm)。

> [!NOTE]
> 如果您已經熟悉 SQL Server，而且只想的 toosee 如何 toodeploy SQL Server VM，請參閱[hello Azure 入口網站中的 SQL Server 虛擬機器佈建](virtual-machines-windows-portal-sql-server-provision.md)。
> 
> 

## <a name="overview"></a>概觀
如果您是資料庫管理員或開發人員，Azure Vm 提供方式 toomove 您在內部部署 SQL Server 工作負載和應用程式 toohello 雲端。 hello 下列影片提供 SQL Server 的 Azure Vm 的技術概觀。

> [!VIDEO https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016/player]
> 
> 

hello 視訊涵蓋下列區域的 hello:

| 時間 | 領域 |
| --- | --- |
| 00:21 |何謂 Azure VM？ |
| 01:45 |安全性 |
| 02:50 |連線能力 |
| 03:30 |儲存體可靠性和效能 |
| 05:20 |VM 大小 |
| 05:54 |高可用性和 SLA |
| 07:30 |組態支援 |
| 08:00 |監視 |
| 08:32 |示範︰建立 SQL Server 2016 VM |

> [!NOTE]
> hello 視訊著重於 SQL Server 2016，但許多版本的 SQL Server，包括 2012年、 2014、 2016年和 Azure 提供的 VM 映像。 
> 
> 

## <a name="scenarios"></a>案例
有許多原因可能會在 Azure 中選擇 toohost 您的資料。 如果您的應用程式移 tooAzure，它可改善效能 tooalso 移動 hello 資料。 但是還有其他好處。 您會自動擁有存取 toomultiple 資料中心全域的目前狀態和災害復原。 hello 資料也是高度安全且持久的。

在 Azure VM 上執行的 SQL Server，是用來將關聯式資料儲存到 Azure 的選項之一。 它在數個案例中是很好的選擇。 比方說，您可以 tooconfigure hello Azure VM 做為可能 tooan 在內部部署 SQL Server 機器類似。 或者，您可能想 toorun 其他應用程式與服務 hello 相同的資料庫伺服器。 有兩個主要資源可協助您思考更多的案例和考量︰

* [Azure 虛擬機器上的 SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/)提供 Azure Vm 上使用 SQL Server 的 hello 最佳案例的概觀。 
* [選擇雲端 SQL Server 選項：Azure SQL (PaaS) Database 或 Azure VM 上的 SQL Server (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md) 可提供 SQL Database 和在 VM 上執行之 SQL Server 的完整比較。

## <a name="create-a-new-sql-vm"></a>建立新的 SQL VM
hello 以下各節提供 Azure 入口網站的直接連結 toohello hello SQL Server 虛擬機器圖庫映像。 根據您選取的 hello 映像，您可以每分鐘根據 SQL Server 授權成本任一工資或您可以將自己的授權 (BYOL)。

尋找在 hello 教學課程中，建立新的 SQL VM 的逐步指引[hello Azure 入口網站中的 SQL Server 虛擬機器佈建](virtual-machines-windows-portal-sql-server-provision.md)。 此外，請檢閱 hello [SQL Server Vm 的效能最佳做法](virtual-machines-windows-sql-performance.md)，其中說明如何 tooselect hello 適當的機器大小和其他功能可用在佈建期間。

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a>選項 1︰利用每分鐘授權建立 SQL VM
hello 下表提供 hello 最新 SQL Server 映像 hello 虛擬機器映像庫中的矩陣。 按一下任何連結 toobegin，使用您指定的版本、 版本與作業系統中建立新的 SQL VM。 

> [!TIP]
> toounderstand hello VM 和 SQL 定價這些映像，請參閱[定價指導方針 SQL Server 的 Azure Vm](virtual-machines-windows-sql-server-pricing-guidance.md)。

| 版本 | 作業系統 | 版本 |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)、[Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)、[Web](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)、[Express](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016)、[Developer](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2)、[Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2)、[Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2)、[Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2)、[Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |

此外 toothis 清單中，SQL Server 版本和作業系統的其他組合使用。 Hello Azure 入口網站中尋找透過 marketplace 搜尋其他映像。 

## <a id="BYOL"></a> 選項 2︰利用現有授權建立 SQL VM
您也可以自備授權 (BYOL)。 在此案例中，您只需支付 hello VM 沒有 SQL Server 授權的任何額外費用。 toouse 自己的授權使用的 SQL Server 版本、 版本及以下作業系統的 hello 矩陣。 在 hello 入口網站，這些映像名稱前面會加上**{BYOL}**。

> [!TIP]
> 長期下來，自備授權可以讓您節省連續生產工作負載的成本。 如需詳細資訊，請參閱 [SQL Server Azure VM 的定價指導方針](virtual-machines-windows-sql-server-pricing-guidance.md)。

| 版本 | 作業系統 | 版本 |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)、[Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2EnterpriseWindowsServer2012R2)、[Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2)、[Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

此外 toothis 清單中，SQL Server 版本和作業系統的其他組合使用。 Hello Azure 入口網站 （搜尋"{BYOL} SQL Server"） 中尋找透過 marketplace 搜尋其他映像。

> [!IMPORTANT]
> toouse BYOL VM 映像，您必須具有與 Enterprise 合約[透過 Azure 軟體保證提供授權流動性](https://azure.microsoft.com/pricing/license-mobility/)。 您也需要有效的授權要 toouse 為 hello 版本/版本的 SQL Server。 您必須[提供 hello 必要 BYOL 資訊 tooMicrosoft](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf)內**10**天數佈建您的 VM。 

> [!NOTE]
> 不可能 toochange hello 授權模型的支付每分鐘的 SQL Server VM toouse 自己的授權。 在此情況下，您必須建立新的 BYOL VM 和移轉資料庫 toohello 新的 VM。 

## <a name="manage-your-sql-vm"></a>管理您的 SQL VM
佈建之後您的 SQL Server VM 之後，有幾個選用的管理工作。 在許多方面，您設定和管理 SQL Server 的方式，完全如同您管理內部部署 SQL Server 執行個體。 不過，某些工作是特定 tooAzure。 hello 下列各節反白顯示部分與連結 toomore 資訊這些區域。

### <a name="connect-toohello-vm"></a>連接 toohello VM
Hello 最基本的管理步驟之一是透過工具，例如 SQL Server Management Studio (SSMS) tooconnect tooyour SQL Server VM。 如需有關如何 tooconnect tooyour 新的 SQL Server VM，請參閱指示[連接 tooa 在 Azure 上的 SQL Server 虛擬機器](virtual-machines-windows-sql-connect.md)。

### <a name="migrate-your-data"></a>遷移資料
如果您有現有的資料庫，您會想 toomove 該 toohello 新提供的 SQL VM。 如需移轉選項與指引的清單，請參閱[移轉資料庫 tooSQL Azure VM 上的 Server](virtual-machines-windows-migrate-sql.md)。

### <a name="configure-high-availability"></a>設定高可用性
如果您需要高可用性，請考慮設定 SQL Server 可用性群組。 這牽涉到虛擬網路中多個 Azure VM。 hello Azure 入口網站已設定此設定為您的範本。 如需詳細資訊，請參閱 [在 Azure Resource Manager 虛擬機器中設定 AlwaysOn 可用性群組](virtual-machines-windows-portal-sql-alwayson-availability-groups.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 如果您想 toomanually 設定您的可用性群組和相關聯的接聽程式，請參閱[Azure VM 中設定 AlwaysOn 可用性群組](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)。

如需其他高可用性注意事項，請參閱 [Azure 虛擬機器中的 SQL Server 高可用性和災害復原](virtual-machines-windows-sql-high-availability-dr.md)。

### <a name="back-up-your-data"></a>備份您的資料
Azure Vm 可以充分利用[自動備份](virtual-machines-windows-sql-automated-backup.md)會以定期建立資料庫的 tooblob 儲存體的備份。 您也可以手動使用此技術。 如需詳細資訊，請參閱 [使用 Azure 儲存體進行 SQL Server 備份與還原](virtual-machines-windows-use-storage-sql-server-backup-restore.md)。 如需所有備份與還原選項的概觀，請參閱 [Azure 虛擬機器中的 SQL Server 備份和還原](virtual-machines-windows-sql-backup-recovery.md)。

### <a name="automate-updates"></a>自動更新
可以使用 azure Vm[自動修補](virtual-machines-windows-sql-automated-patching.md)tooschedule 安裝重要的 windows 和 SQL Server 的維護視窗會自動更新。

### <a name="customer-experience-improvement-program-ceip"></a>客戶經驗改進計畫 (CEIP)
預設會啟用 hello 客戶經驗改進計畫 (CEIP)。 這會定期傳送報表 tooMicrosoft toohelp 改善 SQL Server。 沒有任何管理工作，所需要的 CEIP，除非您想 toodisable 之後佈建。 您可以自訂，或使用遠端桌面連接 toohello VM 停用 hello CEIP。 然後執行 hello **SQL Server 錯誤和使用方式報表**公用程式。 請遵循 hello 指示 toodisable 報告。 

如需詳細資訊，請參閱 hello hello CEIP 部分[接受授權條款](https://msdn.microsoft.com/library/ms143343.aspx)主題。 

## <a name="next-steps"></a>後續步驟

如需定價的問題，請參閱[定價指導方針 SQL Server 的 Azure Vm](virtual-machines-windows-sql-server-pricing-guidance.md)和 hello [Azure 定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)。 選取您的目標版本的 SQL Server 中 hello **OS/軟體**清單。 然後檢視 hello 不同大小的虛擬機器的價格。

其他問題？ 首先，請參閱 hello [Azure 虛擬機器常見問題集 > 的 SQL Server](virtual-machines-windows-sql-server-iaas-faq.md)。 但是，也加入您的問題或意見 toohello 底部的任何 SQL VM 主題 toointeract 與 Microsoft 和 hello 社群。
