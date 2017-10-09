---
title: "aaaOperations Management Suite (OMS) 的概觀 |Microsoft 文件"
description: "Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。  本文說明 OMS 的 hello 值、 識別 hello 不同的服務和包含在 OMS 中供應項目，並提供連結 tootheir 詳細內容。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: bwren
ms.openlocfilehash: ec3fe6d82aec46d1f715a4338f126e79e04a9147
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Operations Management Suite (OMS) 是什麼？
本文章提供簡介 tooOperations Management Suite (OMS) 包括 hello 商務價值，它會提供 hello 服務及管理方案、 它包含，以及 hello 供應項目封裝在一起的不同服務的簡短概觀，解決方案。  連結會包含在 toohello 詳細部署和使用每個服務和解決方案的文件集。

## <a name="from-on-premises-toohello-cloud"></a>從內部部署 toohello 雲端
Microsoft 一直以來都提供用於管理企業環境的產品。  2007 中，多項產品都會合併到 hello System Center 管理產品套件。  這包含 Configuration Manager 會提供諸如軟體發佈和清查，Operations Manager 提供主動式監視的系統和應用程式，包括 runbook tooautomate 手動程序的 Orchestrator 功能與 Data Protection Manager 備份及復原重要資料。

移動 toohello 雲端更多的運算資源，與 System Center 產品會獲得更多的雲端功能，例如 Operations Manager 和 Orchestrator 管理 Azure 中的資源。  其基本上仍設計成內部部署解決方案，而且需要大量投資於內部部署管理環境的部署和維護。  toocompletely 運用 hello 雲端，並支援未來的應用程式，新的方法 toomanagement 所需。

## <a name="introducing-operations-management-suite"></a>Microsoft Operations Management Suite 簡介
Operations Management Suite (也稱為 OMS) 是從 hello 開始 hello 雲端中所設計的管理服務的集合。  OMS 元件完全裝載於 Azure 中，而不會部署和管理內部部署資源。  需要進行的設定很少，您可以在幾分鐘內完成啟動並執行。  

- **部署的成本和複雜度最低。**  因為所有 hello 元件和 oms 的資料都會儲存在 Azure 中，最長可能會與 hello 複雜度而投資在短時間內執行內部元件。
- **標尺 toocloud 層級。**  您沒有 tooworry 需支付您不需要的計算資源，或有關儲存體空間用盡自 hello 雲端可讓您僅針對您實際使用，並會輕易地調整您需要的 tooany 負載 toopay。  您可以藉由管理少數資源 tooget 啟動開始，然後再擴充 tooyour 整個環境。
- **善用 hello 最新的功能。**  OMS 服務中的功能會持續進行新增和更新。  您經常會有存取 toohello 最新的功能沒有任何需求 toodeploy 更新。
- **整合式服務。**  雖然每個 hello OMS 服務自行提供重要的值，它們可一起運作 toosolve 複雜管理案例。  例如，在 Azure 自動化 runbook 可能磁碟機與 Azure Site Recovery 的容錯移轉程序，然後再登資訊 tooLog 分析 toogenerate 警示。
- **總體知識。**  在 OMS 中的管理解決方案持續有存取 toohello 最新的資訊。  hello 安全性和稽核 」 解決方案，例如可以執行使用 hello 最新威脅偵測 hello 世界各地的威脅分析。
- **隨處存取。**  透過瀏覽器隨處存取管理環境。  Hello OMS 應用程式安裝您的智慧型手機 tooyour 監視資料時，可供存取。

### <a name="is-it-just-for-hello-cloud"></a>它只是針對 hello 雲端？
只是因為執行的 OMS 服務並不表示 hello 雲端，無法有效地管理您的內部部署環境。  將代理程式放在任何 Windows 或 Linux 電腦，您的資料中心，並將傳送資料 tooLog 從雲端或內部部署服務所收集的分析，以及其他所有資料分析。  使用 Azure Backup 和 Azure Site Recovery tooleverage hello 雲端備份和高可用性的內部部署資源。  
Hello 雲端中的 Runbook 通常無法存取您的內部部署資源，但您可以在一個或多部電腦上安裝代理程式太將要裝載您的資料中心中的 runbook。  當您啟動 runbook 時，您只指定您要讓 toorun hello 雲端或在本機的背景工作上。

## <a name="hybrid-management-with-system-center"></a>使用 System Center 的混合式管理
如果您有現有的 System Center 安裝，您可以將這些元件與 OMS 服務 tooprovide 混合式解決方案整合這兩個您內部部署和雲端環境運用 hello 相對專精之處的每個產品。  連接您現有 Operations Manager 管理群組 tooLog 分析 tooanalyze 管理代理程式 hello 雲端中。  使用現有的備份程序與 Data Protection Manager toobackup 資料 toohello 雲端。  


## <a name="oms-services"></a>OMS 服務
OMS hello 核心功能是由一組在 Azure 中執行的服務提供。  每個服務提供特定的管理功能，以及您可以結合服務 tooachieve 不同管理案例。

|| 服務 | 說明 |
|:--|:--|:--|
| ![Log Analytics](media/operations-management-suite-overview/icon-log-analytics.png) | Log Analytics | 監視和分析 hello 可用性和不同的資源，包括實體和虛擬機器的效能。 |
| ![Azure 自動化](media/operations-management-suite-overview/icon-automation.png) | 自動化 | 讓手動程序自動化，並強制設定實體和虛擬機器。 |
| ![Azure 備份](media/operations-management-suite-overview/icon-backup.png) | 備份 | 備份及還原重要資料。 |
| ![Azure Site Recovery](media/operations-management-suite-overview/icon-site-recovery.png) | 站台復原 | 為重要應用程式提供高可用性。 |

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) 藉由將受控資源中的資料收集到中央儲存機制，以提供 OMS 監視服務。  這項資料可能包括事件、 效能資料或透過 hello API 提供的自訂資料。 一旦收集完成，就有一個 hello 資料適用於警示和分析，並匯出。  這個方法可讓您從各種來源 tooconsolidate 資料讓您可以從您的 Azure 服務結合資料與現有的內部部署環境。  它會從 hello，讓所有動作都都會使用 tooall 種類的資料，該資料上採取的動作也會明確分隔 hello hello 資料集合。  

![Log Analytics 概觀](media/operations-management-suite-overview/overview-log-analytics.png)

#### <a name="collecting-data"></a>收集資料
有各種不同的方式，您可以將資料帶入記錄分析 tooanalyze hello 儲存機制。

- **Windows 或 Linux 電腦和虛擬機器。**  您在上安裝 Microsoft Monitoring Agent hello [Windows](../log-analytics/log-analytics-windows-agents.md)和[Linux](../log-analytics/log-analytics-linux-agents.md)電腦或您想要從 toocollect 資料的虛擬機器。  hello 代理程式將會自動下載從定義事件和效能資料 toocollect 的記錄分析設定。  您可以輕鬆地安裝 hello 代理程式，使用 hello Azure 入口網站在 Azure 中執行的虛擬機器上。  如果您有現有的 Operations Manager 環境，您可以連接 hello 管理群組 tooLog 分析，並自動開始收集資料，從所有現有的代理程式。
- **Azure 服務。**  記錄分析會收集的遙測[Azure 診斷和監視 Azure](../log-analytics/log-analytics-azure-storage.md)到 hello 儲存機制，讓您可以監視 Azure 資源。
- **資料收集器 API。**  Log Analytics 具有[可供從任何用戶端填入資料的 REST API](../log-analytics/log-analytics-data-collector-api.md)。  這可讓您從協力廠商應用程式的 toocollect 資料或實作自訂管理案例。  常見的方法是 toouse Azure 自動化 toocollect 資料中的 runbook，然後使用 hello 資料收集器 API toowrite 它 toohello 儲存機制。

#### <a name="reporting-and-analyzing-data"></a>報告及分析資料
記錄分析包含功能強大的查詢語言 tooextract 資料儲存在 hello 儲存機制。  因為所有來源的資料都會儲存為記錄，您可以分析單一查詢中多個來源的資料。
  
此外 tooad 臨機操作分析記錄分析會提供多個方式 tooreport 和分析查詢的資料。

- **檢視和儀表板。**  [檢視](../log-analytics/log-analytics-view-designer.md)和[儀表板](../log-analytics/log-analytics-dashboards.md)視覺化 hello hello 入口網站中的查詢的結果。  管理解決方案通常會包含分析 hello 方案的 hello 資料的檢視。  您也可以建立您自己的自訂檢視 tooanalyze 資料，並讓您自訂的入口網站中便於使用。
- **匯出。**  您有 hello 選項 tooexport hello 任何查詢結果，讓您可以分析此封裝外部記錄分析。  您甚至可以太排程定期匯出[Power BI](../log-analytics/log-analytics-powerbi.md)提供強大的視覺效果與分析功能。
- **記錄搜尋 API。**  Log Analytics 具有[可供從任何用戶端收集資料的 REST API](../log-analytics/log-analytics-log-search-api.md)。  這可讓您收集 hello 儲存機制中資料的 tooprogrammatically 工作或從其他監視工具存取它。

#### <a name="alerting"></a>警示
Log Analytics 可以在偵測到問題時[主動警示](../log-analytics/log-analytics-alerts.md)您，或採取矯正動作。  如同 Log Analytics 中的所有其他分析，這是透過記錄搜尋完成。  這項搜尋執行定期的排程，以及如果 hello 結果符合特定準則，則會建立警示。

![Log Analytics 警示](media/operations-management-suite-overview/overview-alerts.png)

此外 toocreating hello 記錄分析儲存機制中的警示記錄，警示可以採取下列動作的 hello。

- **電子郵件。**  傳送電子郵件 tooproactively 通知您偵測到的問題。
- **Runbook。**  Log Analytics 中的警示可以在 Azure 自動化中啟動 Runbook。  這通常是 tooattempt toocorrect hello 偵測到問題。  hello runbook 可以啟動在 hello hello 雲端中的問題，在 Azure 或另一個雲端，或它的大小寫無法啟動之問題的實體或虛擬機器上的本機代理程式。
- **Webhook。**  警示可以啟動 webhook，並將它從 hello hello 記錄搜尋結果傳遞資料。  這可讓與另一個警示系統，例如外部服務整合，或是它可能會嘗試 tootake 的外部網站的更正動作。

### <a name="azure-automation"></a>Azure 自動化
[Azure 自動化](http://azure.microsoft.com/documentation/services/automation)提供程序自動化和設定管理 tooOMS。  它會自動執行的手動程序，並協助 tooenforce 實體和虛擬的電腦組態。  

#### <a name="process-automation"></a>程序自動化
Azure 自動化可使用以 PowerShell 指令碼或 PowerShell 工作流程為基礎的 [Runbook](../automation/automation-runbook-types.md)，讓手動程序自動化。  它也支援可以共用多個 runbook 與認證和連接可讓您可能需要進行驗證 runbook 的 toostore 加密資訊之間的變數，例如 runbook 的資產。
Runbook 提供程序自動化的 hello hello 套件中的其他服務。  由於每個的 hello 可以存取其他服務使用 PowerShell 或 REST API，您可以建立 runbook tooperform 收集記錄分析中的管理資料，或初始化 Azure backup 備份這類功能。

##### <a name="accessing-resources"></a>存取資源
由於 Runbook 是以 PowerShell 為基礎，所以可管理任何可利用 PowerShell Cmdlet 存取的資源。  當您[載入模組](../automation/automation-integration-modules.md)到您的自動化帳戶，它會變成可用 tooall 該帳戶中的 runbook。 
 
當 hello 雲端中執行的 runbook 時，他們可以從 hello 雲端存取任何可存取的資源。  這可能是您的 Azure 訂用帳戶中的資源、其他雲端 (例如 Amazon Web Services (AWS)) 中的資源，或可透過 REST API 存取的服務。  Hello 雲端中的 Runbook 未執行任何認證，但它們可以利用自動化資產，例如認證、 連接和存取憑證 tooauthenticate tooresources。

您的資料中心中的資源最有可能無法存取從 hello 雲端中執行的 runbook。  您可以安裝一個或多個[Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md)您的資料中心雖然 toorun runbook 需要存取 toolocal 資源。  當您啟動 runbook 時，您可以指定它應該要執行 hello 雲端或在特定的背景工作。

![Azure 自動化 Runbook](media/operations-management-suite-overview/overview-runbooks.png)

##### <a name="starting-a-runbook"></a>啟動 Runbook
Runbook 可以[透過多種方法啟動](../automation/automation-starting-a-runbook.md)，以便包含在各種管理案例中。  

- **Azure 入口網站。**  如同其他 Azure 服務，您可以從 hello Azure 入口網站，管理 Azure 自動化。  此外 toostarting runbook，您可以匯入或撰寫您自己。
- **已排程。**  您可以定期排程的 runbook toostart。  這可讓您 tooautomatically 重複的一般管理程序或收集資料 tooLog 分析。
- **PowerShell 和 API。**  您可以啟動 runbook，然後傳遞它們需要從 PowerShell cmdlet 的參數資訊，或 hello Azure 自動化 REST API。  
- **Webhook。**  可以針對任何 runbook，好讓它建立 webhook toobe 啟動從外部應用程式或網站。
- **Log Analytics 警示。**  記錄分析中的警示可以自動啟動 hello 警示所識別的 runbook tooattempt toocorrect hello 問題。

#### <a name="configuration-management"></a>組態管理
[PowerShell 預期狀態設定 (DSC)](../automation/automation-dsc-overview.md)是 Windows PowerShell 可讓您 toodeploy 並強制執行 hello 組態的實體和虛擬機器的管理平台。  Azure 自動化管理 DSC 設定，並提供 hello 雲端中的提取伺服器的代理程式可以存取所需的 tooretrieve 組態。

![Azure 自動化 DSC](media/operations-management-suite-overview/overview-dsc.png)

### <a name="azure-backup-and-azure-site-recovery"></a>Azure 備份和 Azure Site Recovery
Azure 備份和 Azure Site Recovery 構成 toobusiness 續航力和災難復原。  它們都各自具有幫助您 tooensure 應用程式在發生中斷，而且系統再次上線時，傳回 toonormal 作業仍然可用的功能。  Toohello 復原點目標 (Rpo) 和復原時間目標 (Rto) 定義為您的組織，「 參與 」 這兩項服務。 您 rpo hello 可接受的限制，在其中的資料無法使用期間中斷，而且 hello RTO 限制 hello 可接受的時間量以其服務或應用程式無法使用期間發生中斷。

#### <a name="azure-backup"></a>Azure 備份
[Azure 備份](http://azure.microsoft.com/documentation/services/backup)可提供 OMS 的資料備份和還原服務。  它可保護您的應用程式資料並保留數年，而您完全不必投入資本投資，並且只需要最少的營運成本。  它可以備份資料從 SQL Server 和 SharePoint 等加法 tooapplication 工作負載中的實體和虛擬 Windows 伺服器。  它也可用於由 System Center Data Protection Manager (DPM) 保護 tooreplicate 資料 tooAzure 備援及長期儲存。

Azure 備份中受保護的資料會儲存在位於特定地理區域的備份保存庫中。 hello 資料會複寫在 hello 相同的區域，並根據 hello 保存庫類型，也可能是複寫的 tooanother 區域進一步提供恢復功能。

Azure 備份有三種基本案例。

- **具有 Azure 備份代理程式的 Windows 電腦。** 備份檔案和資料夾從任何 Windows server 或用戶端直接 tooyour Azure 備份保存庫。<br><br>![具有 Azure 備份代理程式的 Windows 電腦](media/operations-management-suite-overview/overview-backup-01.png)
- **System Center Data Protection Manager (DPM) 或 Microsoft Azure 備份伺服器。** 利用 DPM 或 Microsoft Azure 備份伺服器 toobackup 檔案和資料夾在加法 tooapplication 工作負載，例如 SQL 和 SharePoint toolocal 儲存體中，然後複寫 tooyour Azure 備份保存庫。 在 Hyper-V 或 VMware 上支援 Windows 和 Linux 虛擬機器。<br><br>![System Center Data Protection Manager (DPM) 或 Microsoft Azure 備份伺服器](media/operations-management-suite-overview/overview-backup-02.png)
- **Azure 虛擬機器擴充功能。** 備份 Windows 或 Linux 虛擬機器 Azure tooyour Azure 備份保存庫。<br><br>![Azure 虛擬機器擴充功能。](media/operations-management-suite-overview/overview-backup-03.png)



#### <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)可藉由協調複寫在內部虛擬和實體機器 tooAzure 或 tooa 次要站台提供業務續航力。 如果您主要站台無法使用，您容錯移轉 toohello 次要位置，讓使用者可以繼續工作，並傳回系統傳回 tooworking 順序時，才會失敗。 

Azure Site Recovery 可為伺服器和應用程式提供高可用性。  它是計算 tooyour 業務續航力和災害復原 (BCDR) 策略可藉由協調複寫、 容錯移轉和復原的內部部署 HYPER-V 虛擬機器、 VMware 虛擬機器和實體 Windows/Linux 伺服器。 您可以複製機器 tooa 次要資料中心，或將它們複製 tooAzure 擴充您的資料中心。 Site Recovery 也提供工作負載的簡單容錯移轉和復原。 它會與災害復原機制 (例如 SQL Server AlwaysOn) 整合，並提供復原計劃輕鬆容錯移轉跨多部電腦分層的工作負載。

Azure Site Recovery 有三種基本複寫案例。

- **Hyper-V 虛擬機器的複寫。**  如果 VMM 雲端中管理 HYPER-V 虛擬機器，您就可以複寫 tooa 次要資料中心或 tooAzure 儲存體。 複寫 tooAzure 是透過安全的網際網路連線。 複寫 tooa 次要資料中心是透過 hello LAN。  若為 HYPER-V 虛擬機器不由 VMM 管理，您只能複寫 tooAzure 儲存體。 複寫 tooAzure 是透過安全的網際網路連線。<br><br>![Hyper-V 虛擬機器的複寫](media/operations-management-suite-overview/overview-siterecovery-hyperv.png)
- **VMware 虛擬機器的複寫。**  您可以將 VMware 虛擬機器 tooa 次要資料中心執行 VMware 或 tooAzure 儲存體的複寫。 透過站對站 VPN、 Azure ExpressRoute 或是安全的網際網路連線，就會發生複寫 tooAzure。 複寫 tooa 次要資料中心發生 hello InMage Scout 資料通道。<br><br>![VMware 虛擬機器的複寫](media/operations-management-suite-overview/overview-siterecovery-vmware.png)
- **實體 Windows 和 Linux 伺服器的複寫。**  您可以將實體伺服器 tooa 次要資料中心或 tooAzure 儲存體的複寫。 透過站對站 VPN、 Azure ExpressRoute 或是安全的網際網路連線，就會發生複寫 tooAzure。 複寫 tooa 次要資料中心發生 hello InMage Scout 資料通道。 Azure Site Recovery 有一項 OMS 解決方案會顯示統計資料，但是您必須使用 hello Azure 入口網站進行任何作業。<br><br>![實體 Windows 和 Linux 伺服器的複寫](media/operations-management-suite-overview/overview-siterecovery-physical.png)


Site Recovery 會將元資料儲存到位於特定地理 Azure 區域的保存庫中。 不會儲存複寫的資料 hello Site Recovery 服務。

## <a name="management-solutions"></a>管理解決方案
[管理解決方案](operations-management-suite-solutions.md)是預先封裝的邏輯集合，可利用一或多項 OMS 服務實作特定管理案例。  從 Microsoft 和協力廠商，您可以在 OMS 中輕鬆地加入您的投資 tooyour Azure 訂用帳戶 tooincrease hello 值可使用不同的解決方案。  為協力廠商可以建立您自己的解決方案 toosupport 應用程式和服務，並提供他們 toousers 透過 hello Azure Marketplace 或快速入門範本。

利用多個服務 tooprovide 其他功能的解決方案的理想範例為 hello[更新管理解決方案](oms-solution-update-management.md)。  這個解決方案有關 Windows 和 Linux toocollect 必要更新每個代理程式上使用 hello 記錄分析代理程式。  它會寫入此資料 toohello 記錄分析儲存機制，包含儀表板與分析它。  當您建立部署時，Azure 自動化中的 runbook 會使用的 tooinstall 需要更新。  您管理整個 hello 入口網站中的程序，而不需 tooworry 關於 hello 基礎詳細資料。

![方案](media/operations-management-suite-overview/overview-solution.png)

一或多個下列函式的 hello，可能會執行大部分的解決方案。

- 收集其他資訊。  Log Analytics 會從用戶端和服務收集各種資料，包括事件和效能資料。  管理解決方案通常使用 Azure 自動化 runbook，收集無法從其他資料來源取得的額外資訊。
- 提供所收集資訊的其他分析。  管理解決方案包含儀表板和檢視，可提供資料的分析和視覺效果。  讓您 toodrill hello 至這些連結後 toopredefined 記錄搜尋詳細資料。  它們也可能已收集到 hello 儲存機制，例如搜尋的模式，表示威脅的安全性事件之間的資料執行分析。
- 新增功能。  Microsoft 所提供的某些解決方案可能是根據 hello 的 hello 核心服務 tooprovide 其他功能的功能。  服務對應，例如提供它自己的主控台 toodiscover，並將對應伺服器和即時的程序相依性。
解決方案會定期加入 tooOMS 由 Microsoft 和協力廠商可讓您 toocontinuously 增加 hello 投資的價值。  您可以瀏覽 Microsoft 解決方案透過 hello 方案目錄 hello OMS 入口網站中或瀏覽並安裝並安裝 Microsoft 和協力廠商解決方案，透過 Azure Marketplace hello hello Azure 入口網站中。  

![方案庫](media/operations-management-suite-overview/solution-gallery.png)


## <a name="next-steps"></a>後續步驟
* 了解 [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)。
* 了解 [Azure 自動化](../automation/automation-intro.md)。
* 了解 [Azure 備份](http://azure.microsoft.com/documentation/services/backup)。
* 了解 [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)。
* 探索 hello[解決方案，可](../log-analytics/log-analytics-add-solutions.md)hello 不同 OMS 提供項目中。 

