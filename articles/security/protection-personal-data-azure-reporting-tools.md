---
title: "aaaDocument 保護個人資料與 Azure 報告工具 |Microsoft 文件"
description: "如何 toouse Azure 的 reporting services 與技術 toohelp 保護隱私權的個人資料。"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a>使用 Azure 報告工具記載個人資料的保護

本文將討論如何 toouse Azure reporting services，技術 toohelp 保護隱私權的個人資料。

## <a name="scenario"></a>案例

大型出航公司搬遷後 hello 美國，展開在 hello 地中海、 Adriatic，與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。 toohelp 這些工作，它所取得數個較小的出航行位於義大利，德國、 丹麥和 hello 英國

hello 公司使用 Microsoft Azure 的處理和儲存的公司資料。 其中包含其全球客戶群的名稱、地址、電話號碼和信用卡資訊等個人識別資訊。 它也會包含在所有位置的傳統的人力資源資訊，例如地址、 電話號碼、 稅務識別碼和醫療公司員工的相關資訊。 hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫，其中包含與目前和過去的客戶的個人資訊 tootrack 關聯性。

位於 hello 世界各地的公司員工存取 hello 網路從 hello 公司遠端辦公室和旅行代理程式已存取 toosome 公司資源。

## <a name="problem-statement"></a>問題陳述

hello 公司必須保護員工和客戶的個人資料的多層式的安全性策略，使用 Azure 管理和安全性功能 tooimpose 嚴格的控制存取 tooand 處理的個人資料，而必須透過 hello 的隱私權無法 toodemonstrate 其保護測量 toointernal 和外部的稽核員。

## <a name="company-goal"></a>公司目標

其深度防禦的安全性策略的一部分，它是公司目標 tootrack 的個人資料，所有存取 tooand 處理，並確保的個人資料的適當的隱私權保護的文件中的位置以及如何使用。

## <a name="solutions"></a>解決方案

Microsoft Azure 提供完整的監視、 記錄和診斷工具 toohelp 追蹤和記錄活動以及存取和處理個人資料、 地理資料流程的資料，以及第三方存取 toopersonal 資料相關聯的事件。 由於 hello 雲端中的個人資料的安全性是共同的責任，Microsoft 也有提供客戶：

- 其自己處理客戶資料的詳細資訊

- 由 Microsoft 管理的安全性措施

- 其傳送客戶資料的位置和方式

- Microsoft 自有隱私權檢閱程序的詳細資料

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 是 Microsoft 的雲端式、多租用戶目錄和身分識別管理服務。 服務的登入 hello 和稽核報告功能提供您詳細的登入和應用程式使用方式活動資訊 toohelp 監視，並確保適當的存取權 toocustomers 和員工的個人資料。

活動報告類型有兩種︰

- hello[稽核活動報告記錄檔](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)提供系統活動/工作的詳細的記錄

- hello[登入活動報表/記錄檔](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins)顯示您已執行 hello 稽核報表中列出的每個活動的人員

您可以同時使用兩個 hello，追蹤 hello 歷程記錄的每個已執行的工作，以及每個執行之人員。 這兩種報告均可自訂和篩選。

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a>如何存取 hello 稽核和安全性記錄檔？

hello 稽核及安全性記錄檔可以存取從 hello Active Directory 入口網站以三個不同的方式： 透過 hello**活動**> 一節 (選取**稽核記錄檔**或**登入**)，或從**使用者和群組**或**企業應用程式**下**管理**Active Directory 中。 報表也可以存取透過 hello Azure Active Directory 報告 API。 

1. 在 hello Azure 入口網站，選取  **Azure Active Directory。**

2. 在 hello**活動**區段中，選取**稽核記錄檔。**

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. 藉由按一下自訂 hello 清單檢視**資料行**hello 工具列中。

4.  選取的項目 hello 清單檢視 toosee 中所有可用的詳細資訊。

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

Azure Active Directory 報告還包含兩種類型的安全性報告：[標幟為有風險的使用者]和 [有風險的登入]，這可協助您監視 Azure 環境中的潛在風險。

如需 hello 報告服務的詳細資訊，請參閱[Azure Active Directory 報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)

請瀏覽[Azure Active Directory 活動報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports)針對更多有關使用 Azure Active Directory 中的 hello 報表的特性。 這個網站包含更多詳細瞭解 tooaccess 並用[稽核記錄活動報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)和[登入活動報表](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins)hello 入口網站中。 它也包含[標幟為有風險的使用者](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk)和[有風險的登入](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins)安全性報告的相關資訊。

請瀏覽 hello [Azure Active Directory 稽核應用程式開發介面參考](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference)站台，如需有關如何 tooconnect tooAzure 目錄以程式設計方式報告。

### <a name="log-analytics"></a>Log Analytics

[記錄分析](https://azure.microsoft.com/services/log-analytics/)可以[收集資料，從 Azure 監視器](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage)toocorrelate 它與其他資料，並提供其他的分析。 Azure 監視器可收集和分析 Azure 環境的監視資料。 

Log Analytics 中的分析工具 (例如記錄搜尋、檢視和解決方案) 可處理所有收集的資料，進而為您提供整個環境的集中式分析。 記錄分析可彙總並分析 Windows 事件記錄檔、 IIS 記錄檔，以及可協助偵測潛在可能會公開的個人資料 toounauthorized 使用者的個人資料缺口的 Syslog。

#### <a name="how-do-i-use-log-analytics"></a>如何使用 Log Analytics？

您可以透過 hello OMS 入口網站或 hello Azure 入口網站，從任何網頁瀏覽器存取記錄分析。 記錄分析包含查詢語言 tooquickly 擷取和彙總 hello 儲存機制中的資料。 您可以建立及儲存的記錄搜尋 toodirectly 分析 hello 入口網站中的資料。

toocreate hello Azure 入口網站中的記錄分析工作區 hello 遵循：

1. 選取**記錄分析**hello 清單中的 hello Marketplace 中的服務。

2. 選取**建立、**指定 hello 的 OMS 工作區的名稱、 您的訂用帳戶、 資源群組、 位置，然後在定價層。

3. 按一下**確定**toodisplay 的工作區清單。

4. 選取工作區 toosee 其詳細資料。

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

請瀏覽 hello[記錄分析文件](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)toolearn 更多關於 hello 服務。

瀏覽 hello[開始記錄分析工作區使用](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)教學課程 toocreate 評估工作區，並了解如何 toouse hello 服務 hello 基本概念。

請瀏覽下列如需特定資訊的網頁上以 hello tooconnect toouse 記錄分析的記錄檔的 hello 上面所述：

[Log Analytics 中的 Windows 事件記錄資料來源](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[Log Analytics 中的 IIS 記錄](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[Log Analytics 中的 Syslog 資料來源](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a>Azure 監視器/Azure 活動記錄 

[Azure 監視器](https://azure.microsoft.com/services/monitor/)可針對 Microsoft Azure 中的大多數服務提供基本等級的基礎結構計量與記錄。
監視可協助您 toogain 深入了解有關 Azure 應用程式。 Azure 監視依賴 hello Azure 診斷延伸模組 （Windows 或 Linux） 來收集大部分的應用程式層級度量和記錄檔。 [hello Azure 活動記錄檔](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)是 hello 資源，您可以檢視的 Azure 監視的其中一個。 它會追蹤每個 API 呼叫，並提供有關在 [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) 中發生之活動的豐富資訊。
您可以在 hello Azure 基礎結構所偵測到您資源的相關資訊的搜尋 hello （先前稱為操作或稽核記錄檔） 的活動記錄檔。 

雖然許多 hello 資訊記錄在 hello 活動記錄檔與 tooperformance 和服務的健全狀況，也沒有為資料的相關的 tooprotection 的資訊。 使用 hello 活動記錄檔，您可以決定 hello 」 功能，對象、 及何時"的任何寫入作業 (PUT、 POST、 DELETE) 在您的 Azure 訂用帳戶中的 hello 資源。

例如，它提供的記錄，當系統管理員刪除網路安全性群組，因而可能影響到 hello 保護個人資料。 活動記錄項目會儲存在 Azure 監視器中長達 90 天。

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a>如何使用 Azure 監視器所收集的 hello 資料？

有的方式 toouse hello 資料 hello 活動記錄檔中的數字和其他監視 Azure 資源。

- 您可以串流處理實際的行中的 hello 資料 tooother 位置。

- 您可以儲存 hello 資料較長的時間週期，比 hello 預設值，使用[Azure 儲存體帳戶](https://docs.microsoft.com/azure/storage/common/storage-introduction)和設定保留原則。

- 您可以視覺化 hello 圖形和圖表中的資料，使用 hello [Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)， [Azure Application Insights](https://azure.microsoft.com/services/application-insights/)， [Microsoft PowerBI](https://powerbi.microsoft.com/)，或協力廠商視覺效果工具。

- 您可以查詢使用 hello Azure 監視 REST API，CLI 命令的 hello 資料[PowerShell](https://docs.microsoft.com/powershell/) cmdlet，或 hello.NET SDK。

開始使用 Azure 監視器 tooget 選取**更服務**hello Azure 入口網站中。

1. 向下捲動太**監視器**在 hello**監視及管理**> 一節。

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  監視器開啟 hello**活動記錄檔**檢視。

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

您可以建立及儲存查詢的一般篩選器，然後 pin hello 最重要查詢 tooa 入口網站儀表板，就一定會知道是否發生符合您準則的事件。

1. 您可以篩選 hello 檢視資源群組、 timespan 和事件類別目錄。

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. 然後將依序按一下 hello 查詢 tooa 入口網站儀表板釘選**Pin**  按鈕。 這可協助您在服務上建立作業資料的單一資訊來源。 hello 查詢的結果數目將會顯示名稱和 hello 儀表板上。

您可以也使用 hello 監視器 tooview 標準所有 Azure 資源、 設定診斷設定和警示，並搜尋 hello 記錄檔。 如需有關如何 toouse hello Azure 監視器和活動記錄檔，請參閱[開始使用 Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started)。

### <a name="azure-diagnostics"></a>Azure 診斷 

在 Azure 中的 hello 診斷功能可讓來自多個來源的資料集合。 hello Windows 事件記錄檔，其中包括 hello 安全性記錄檔，可以追蹤和記錄的個人資料的保護特別有用。 hello 安全性記錄檔會在登入成功和失敗事件，以及權限的變更、 偵測模式表示特定類型的攻擊、 安全性相關原則變更、 安全性群組成員資格變更，以及執行更多的追蹤。

例如，事件識別碼 4695 提醒您嘗試 toohello unprotection 可稽核的受保護資料。 這與 toohello 資料保護 API (DPAPI)，它可以幫助 tooprotect 資料，例如私用的索引鍵、 預存的認證和其他機密資訊。

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a>如何啟用適用於 Windows Vm 的 hello 診斷延伸模組？

您可以針對 Windows VM，所以當 toocollect 記錄資料使用 PowerShell tooenable hello 診斷延伸模組。 這麼做的 hello 步驟取決於您的部署模型上使用 （「 資源管理員 」 或 「 傳統 」）。 tooenable hello 的診斷延伸模組透過 hello Resource Manager 部署模型所建立的現有 VM，您可以使用 hello[組 AzureRMVMDiagnosticsExtension PowerShell cmdlet](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1)。

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

*\$diagnosticsconfig_path* hello 路徑 toohello 檔案包含在 XML 中的 hello 診斷組態。 如需詳細啟用 Azure 診斷 VM 上的指示，請參閱[執行 Windows 的虛擬機器中使用 PowerShell tooenable Azure 診斷。](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)

hello Azure 診斷擴充功能可以傳送嗨收集資料 tooan Azure 儲存體帳戶，或傳送 tooservices 例如 Application Insights。 然後您可以使用 hello 資料稽核。

#### <a name="how-do-i-store-and-view-diagnostic-data"></a>如何儲存和檢視診斷資料？

它是重要的 tooremember 的診斷資料不會永久儲存除非 toohello Microsoft Azure 儲存體模擬器] 或 [tooAzure 儲存體傳輸。 toostore 和檢視診斷資料，在 Azure 儲存體，請遵循下列步驟：

1. Hello ServiceConfiguration.cscfg 檔案中指定的儲存體帳戶。 Hello Blob 服務或 hello 表格服務，根據 hello 資料類型而定，可以使用 azure 診斷。 Windows 事件記錄會以資料表格式儲存。

2. 傳送嗨資料。 您可以透過 hello 設定檔要求 tootransfer hello 診斷資料。 SDK 2.4 及之前，您也可以進行 hello 要求以程式設計的方式。

3. 檢視使用的 hello 資料[Azure 儲存體總管](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)，[伺服器總管](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage)在 Visual Studio 中，或[Azure 診斷管理員](https://www.cerebrata.com/products/azure-diagnostics-manager)Azure Management Studio 中。

如需有關如何 tooperform 每個步驟執行，請參閱[Azure 儲存體中的儲存和檢視診斷資料。](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)

### <a name="azure-storage-analytics"></a>Azure 儲存體分析 

儲存體分析記錄成功和失敗的要求 tooa 儲存體服務的詳細的資訊。 這項資訊可以使用的 toomonitor 個別要求，可協助您撰寫存取 toopersonal 資料儲存在 hello 服務中。 不過，根據預設，儲存體帳戶不會啟用儲存體分析記錄功能。 您可以在 hello Azure 入口網站中加以啟用。

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a>如何設定儲存體帳戶的監視？

tooconfigure 監視儲存體帳戶，下列 hello:

1. 選取**儲存體帳戶**hello Azure 入口網站，然後選取您想要 toomonitor hello 帳戶 hello 名稱。

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. 在 hello**監視**區段中，選取**診斷。**

3.  選取 hello**類型**的度量資料想 toomonitor 為每個服務 （Blob、 資料表檔案）。 tooinstruct Azure 儲存體 toosave 診斷記錄檔的讀取、 寫入和刪除要求 hello blob、 資料表和佇列服務，請選取**Blob 記錄檔時，資料表記錄**和**佇列記錄檔。**

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. 使用 hello 滑桿在 hello 下方，設定 hello**保留**原則天數 （1 – 365 值）。 Hello 預設值是七天。

5. 選取**儲存**tooapply hello 組態設定。

儲存體記錄的記錄項目包含下列個別要求的相關資訊的 hello:

- 時間資訊，例如開始時間、端對端延遲和伺服器延遲。

- Hello 例如 hello 作業類型的儲存體作業的詳細資訊，儲存體物件 hello 用戶端 hello hello 索引鍵是存取、 成功或失敗，以及傳回 toohello 用戶端 hello HTTP 狀態碼。

- 例如 hello 類型驗證 hello 用戶端使用的驗證詳細資料。

- 並行存取資訊，例如 hello ETag 值和上次修改時間戳記。

- hello 的 hello 要求和回應訊息的大小。

如需詳細指示 tooenable 儲存體分析記錄，請參閱[監視 hello Azure 入口網站的儲存體帳戶。](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)

### <a name="azure-security-center"></a>Azure 資訊安全中心 

[Azure 資訊安全中心](https://azure.microsoft.com/services/security-center/)監視器 hello 順序 tooprevent 在您的 Azure 資源的安全性狀態和偵測到威脅，並提供回應的建議。 它會提供數種方式 toohelp 文件您保護 hello 隱私權的個人資料的安全措施。

安全性健康情況監視可協助您確保符合安全性原則的規範。 安全性監視是稽核時，不符合組織的標準或最佳作法 tooidentify 系統資源的主動式策略。 您可以監視下列資源的 hello hello 安全性狀態：

- 計算 (虛擬機器和雲端服務)

- 網路 (虛擬網路)

- 儲存體和資料 (伺服器和資料庫稽核和威脅偵測、TDE、儲存體加密)

- 應用程式 (潛在安全性問題)

在任何兩個分類中的安全性問題，可能會造成威脅 toohello 隱私權的個人資料。

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a>如何檢視我的 Azure 資源 hello 安全性狀態？

資訊安全中心定期分析您的 Azure 資源 hello 安全性狀態。 您可以檢視任何潛在的安全性漏洞，它會識別在 hello**防止**hello 儀表板的區段。

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. 在 hello**防止**區段中，選取 hello**計算**磚。 您會在這裡看到**概觀，**以及 hello**虛擬機器**列出的所有 Vm，而且其安全性狀態，並 hello**雲端服務**web 和背景工作角色的清單由資訊安全中心的監視。

2. 在 hello**概觀**索引標籤中，第二個建議 tooview 的詳細資訊。

3. 在 hello**虛擬機器**索引標籤上，選取 VM tooview 其他詳細資料。

Azure 資訊安全中心中啟用資料收集時，hello Microsoft Monitoring Agent 會自動佈建所有現有和新的任何支援的已部署之虛擬機器。 從這個代理程式收集的資料會儲存在與您的訂用帳戶相關聯的現有 [Log Analytics](https://azure.microsoft.com/services/log-analytics/) 工作區或新的工作區中。

資訊安全中心所提供的[威脅情報報告](https://docs.microsoft.com/azure/security-center/security-center-threat-report)。 這些可讓您 toohelp 分辨 hello 攻擊者的身分識別、 目標、 目前和歷史攻擊活動和的策略，工具和程序使用的有用資訊。 還包含緩和與修復資訊。

這些威脅報告 hello 主要用途是 toohelp 您 toorespond 有效 toohello 立即威脅和說明 take 之後測量 toomitigate hello 問題。 當您在文件您進行報告和稽核事件的回應，hello 報表中的 hello 資訊可以也很有用。

hello 威脅智慧報表會顯示。PDF 格式，透過 hello 中的連結存取**報表**欄位 hello**可疑的處理程序執行**刀鋒視窗中的每個 Azure 資訊安全中心中的安全性警示。

如需有關並用 tooview hello Threat Intelligence 報告的詳細資訊，請參閱[Azure 安全性中心 Threat Intelligence 報告。](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

## <a name="next-steps"></a>後續步驟：

[開始使用 hello Azure Active Directory 報告 API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[什麼是 Log Analytics？](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[Microsoft Azure 中的監視概觀](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[簡介 toohello Azure 活動記錄檔 （影片）](https://azure.microsoft.com/resources/videos/intro-activity-log/)
