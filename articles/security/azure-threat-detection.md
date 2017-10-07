---
title: "aaaAzure 進階威脅偵測 |Microsoft 文件"
description: "了解 Identity Protection 及其功能。"
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 63e2c541fd4ce2c571af9d5845c9a9bd4b03b2a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-advanced-threat-detection"></a>Azure 進階威脅偵測
## <a name="introduction"></a>簡介

### <a name="overview"></a>概觀

Microsoft 開發了一系列的技術白皮書、 安全性概觀、 最佳做法和檢查清單 tooassist Azure 客戶關於 hello 各種可用的安全性相關功能與周圍的 hello Azure 平台。 hello 廣度及深度方面的主題範圍，並定期更新。 這份文件摘要 hello 遵循抽象 > 一節中為該系列的一部分。

### <a name="azure-platform"></a>Azure 平台

Azure 是作業系統的公用雲端服務平台支援的程式設計語言、 架構、 工具、 資料庫和裝置 hello 最大範圍的選取範圍。
它支援下列程式設計語言的 hello:
-   透過 Docker 整合執行 Linux 容器。
-   使用 JavaScript、Python、.NET、PHP、Java 和 Node.js 建置應用程式。
-   建置 iOS、Android 和 Windows 裝置的後端。

Azure 公用雲端服務支援相同的技術數百萬的開發人員和 IT 專業人員已經依賴和信任的 hello。

當您移轉 tooa 與組織的公用雲端時，該組織是負責 tooprotect 您的資料，並提供安全性和 hello 系統周圍的控管。

從裝載吸引數百萬的客戶同時 hello 設備 tooapplications 設計 azure 的基礎結構，並提供的企業符合安全性需求的可信任基礎。 Azure 提供廣泛的選項 tooconfigure 與自訂安全性 toomeet hello 需求的應用程式部署。 本文件可協助您符合這些需求。

### <a name="abstract"></a>摘要

Microsoft Azure 透過 Azure Active Directory、Azure Operations Management Suite (OMS) 及 Azure 資訊安全中心等服務，來提供內建的進階威脅偵測功能。 安全性服務和功能，這個集合會提供簡單又快速的方式 toounderstand 為什麼您的 Azure 部署中。

這份技術白皮書將引導您 hello 「 Microsoft Azure 方法 」 向潛在威脅的弱點可能會診斷和分析 hello 風險與 hello 惡意活動為目標的伺服器和其他 Azure 資源相關聯。 這可協助您識別 tooidentify hello 方法，而且的弱點可能會管理與最佳化方案 hello Azure 平台及客戶對向安全性服務和技術。

這份技術白皮書著重在 Azure 平台和客戶對向控制項 hello 技術，並不會嘗試 tooaddress Sla 定價模型和 DevOps 作法的考量。

## <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

![Azure Active Directory Identity Protection](./media/azure-threat-detection/azure-threat-detection-fig1.png)


[Azure Active Directory 識別身分保護](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)是一項功能的 hello [Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) hello 風險事件和潛在的弱點可能會影響您的組織的概觀會提供您的版本身分識別。 Microsoft 有已保護的雲端式身分識別以來，和與 Azure AD Identity Protection Microsoft 提供這些相同的保護系統可用 tooenterprise 客戶。 Identity Protection 使用現有 Azure AD 的異常偵測功能 (可透過 [Azure AD 的異常活動報告](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports)取得)，並引進可即時偵測異常的新風險事件類型。

自動調整的機器學習演算法和啟發學習法 toodetect 異常可能表示身分識別已遭洩漏的風險事件，則會使用識別身分保護。 使用這項資料，識別身分保護會產生報表和警示可讓您 tooinvestigate 這些風險事件，並採取適當的補救或補救動作。

但是，Azure Active Directory Identity Protection 不只是監視和報告工具而已。 根據風險事件，Identity Protection 會計算每位使用者的使用者風險層級，讓您 tooconfigure 風險為基礎的原則保護 tooautomatically hello 您組織的身分識別。

這些風險型原則，請在加法 tooother[條件式存取控制](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)提供由 Azure Active Directory 和[EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)、 可以自動封鎖或提供彈性的修復動作，包括密碼重設以及強制多因素驗證。

### <a name="identity-protections-capabilities"></a>Identity Protection 的功能

Azure Active Directory Identity Protection 不只是監視和報告工具而已。 tooprotect 貴組織的身分識別，您可以設定在達到指定的風險層級時，自動回應 toodetected 問題的風險為基礎原則。 這些原則，除了 tooother 條件式存取 Azure Active Directory 和 EMS 所提供的控制項，可以自動封鎖或起始自動調整的修復動作，包括密碼重設以及強制多因素驗證。

Hello 方式 Azure 識別身分保護可幫助的一些範例保護您的帳戶，並識別包括：

[偵測風險事件和有風險的帳戶：](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#detection)
-   使用機器學習服務和啟發式規則偵測六種風險事件類型
-   計算使用者風險層級
-   提供自訂的建議 tooimprove 透過的弱點可能會反白顯示整體的安全性狀態

[調查風險事件：](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#investigation)
-   傳送風險事件的通知
-   使用相關和內容資訊來調查風險事件
-   提供基本工作流程 tootrack 調查
-   讓您輕鬆存取 tooremediation 動作，例如密碼重設

[以風險為基礎的條件式存取原則：](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#risky-sign-ins)
-   原則 toomitigate 風險登入所封鎖登入，或要求多重要素驗證挑戰。
-   原則 tooblock 或安全風險的使用者帳戶
-   原則 toorequire 使用者 tooregister 的多重要素驗證

### <a name="azure-ad-privileged-identity-management-pim"></a>Azure AD Privileged Identity Management (PIM)

利用 [Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure)，

![Azure AD 特殊權限身分識別管理](./media/azure-threat-detection/azure-threat-detection-fig2.png)

您可以管理、控制及監視組織內的存取。 這包括存取 tooresources 在 Azure AD 和 Office 365 或 Microsoft Intune 等其他 Microsoft online services。

Azure AD Privileged Identity Management 可協助您：

-   取得警示和報告 Azure AD 系統管理員和"just-in-time"系統管理存取權 tooMicrosoft 線上服務，例如 Office 365 和 Intune

-   取得有關系統管理員存取記錄與系統管理員指派變更的報告

-   取得警示存取 tooa 特殊權限角色

## <a name="microsoft-operations-management-suite-oms"></a>Microsoft Operations Management Suite (OMS)

[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。 因為 OMS 實作為雲端型服務，所以您對基礎結構服務進行最小的投資就可以快速啟動並執行它。 新的安全性功能會自動提供，以節省持續維護和升級成本。

此外 tooproviding 重要服務在其本身，OMS 可以整合 System Center 元件這類[System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) tooextend 現有的安全性管理投資 hello 到雲端。 System Center 和 OMS 可一起運作的 tooprovide 完整的混合式管理體驗。

### <a name="holistic-security-and-compliance-posture"></a>整體安全性與合規性狀態

hello [OMS 安全性和稽核儀表板](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started)讓您完整檢視您組織的 IT 安全性狀況，針對值得您注意的問題使用內建的搜尋查詢。 hello 安全性和稽核儀表板是所有項目 hello 主畫面相關 toosecurity 在 OMS 中。 會提供在電腦的 hello 安全性狀態的高層級深入。 它也包含 hello 能力 tooview hello 過去 24 小時、 7 天的所有事件或任何其他自訂的時間範圍。

OMS 儀表板幫助您快速且輕鬆地了解 hello 全部都在 IT 作業，包括 hello 內容內的所有環境的整體安全性狀況： 軟體更新評估、 反惡意程式碼評估和設定基準。 此外，安全性記錄檔資料會立即存取 toostreamline hello 安全性與相容性稽核程序。

hello OMS 安全性和稽核儀表板分為四個主要類別：

![OMS 安全性和稽核儀表板](./media/azure-threat-detection/azure-threat-detection-fig3.jpg)

-   **安全性網域：**在這個區域中，您將無法 toofurther 探索安全性記錄一段時間，存取惡意程式碼評估、 更新評估、 網路安全性、 身分識別和存取資訊、 電腦與安全性事件並能快速地存取 tooAzure 資訊安全中心儀表板。

-   **值得注意的問題：**此選項可讓您 tooquickly 識別作用中問題的 hello 數目和 hello 這些問題的嚴重性。

-   **偵測 （預覽）：**可讓您透過視覺化安全性警示，因為它們對您的資源進行的 tooidentify 攻擊的模式。

-   **威脅情報：**可讓您所視覺化的具有惡意連出 IP 流量、 hello 惡意之威脅類型，以及顯示這些 Ip 所在的對應伺服器 hello 總數的 tooidentify 攻擊的模式。

-   **常見安全性查詢：**這個選項提供您一份 hello 最常見安全性查詢，您可以使用 toomonitor 您的環境。 當您按一下其中一個這些查詢中時，它會開啟刀鋒視窗中搜尋 hello 與 hello 該查詢的結果。

### <a name="insight-and-analytics"></a>深入解析與分析
Hello 中央的[記錄分析](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)是 hello OMS 儲存機制裝載在 hello Azure 雲端。

![深入解析與分析](./media/azure-threat-detection/azure-threat-detection-fig4.png)

到 hello 儲存機制從所設定的資料來源和加入解決方案 tooyour 訂用帳戶連線來源收集資料。

![訂用帳戶](./media/azure-threat-detection/azure-threat-detection-fig5.png)

資料來源和解決方案將每個建立自己的屬性集，但可能仍然會分析一起查詢 toohello 儲存機制中不同的記錄類型。 這可讓您 toouse hello 與不同類型的資料相同的工具和方法 toowork 收集不同的來源。


大部分的記錄分析與您互動都是透過 hello OMS 入口網站，它會在任何瀏覽器中執行，並提供您存取 tooconfiguration 設定和與多個工具 tooanalyze 在收集的資料上運作。 從 hello 入口網站，您可以使用[記錄搜尋](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches)建構查詢 tooanalyze 收集資料，其中[儀表板](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards)，您可利用圖形檢視最有價值的搜尋，以及自訂[解決方案](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions)，這兩個提供額外的功能和分析工具。

![分析工具](./media/azure-threat-detection/azure-threat-detection-fig6.png)

解決方案會將功能 tooLog 分析。 這些主要在 hello 雲端中執行，並且提供 hello OMS 儲存機制所收集的資料分析。 它們也必須定義新記錄類型 toobe 收集可分析記錄搜尋而 hello OMS 儀表板中的 hello 方案所提供的其他使用者介面。
hello 安全性和稽核是這類解決方案的範例。



### <a name="automation--control-alert-on-security-configuration-drifts"></a>自動化與控制︰有關安全性設定漂移的警示

Azure 自動化可自動化管理程序，使用 PowerShell 為基礎且在 hello Azure 雲端中執行的 runbook。 也可以在您本機資料中心 toomanage 本機資源的伺服器上，執行 Runbook。 Azure 自動化會使用 PowerShell DSC (Desired State Configuration) 來提供設定管理。

![Azure 自動化](./media/azure-threat-detection/azure-threat-detection-fig7.png)

您可以建立和管理裝載於 Azure 的 DSC 資源並將其套用 toocloud 和內部系統 toodefine 和自動強制執行其設定或取得報表漂移時即 toohelp 確保安全性設定保留原則內。

## <a name="azure-security-center"></a>Azure 資訊安全中心

Azure 資訊安全中心可協助保護您的 Azure 資源。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理。 Hello 在服務內，您就可以 toodefine 原則不只是針對您 Azure 訂用帳戶，同時也針對[資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)，使您能夠更細微。

![Azure 資訊安全中心](./media/azure-threat-detection/azure-threat-detection-fig8.png)

Microsoft 安全性研究人員經常位於 hello lookout 的威脅。 他們有存取 tooan 以免受到擴充獲得 Microsoft 的全域存在 hello 雲端和內部部署中的遙測。 這個寬到達的各種集合的資料集可讓 Microsoft toodiscover 新的攻擊模式和趨勢跨越其內部消費者和企業產品，以及其線上服務。

因此，資訊安全中心可以在攻擊者發行新的和日益複雜的攻擊時，快速地更新其偵測演算法。 這種方法可協助您跟上瞬息萬變的威脅環境。

![資訊安全中心](./media/azure-threat-detection/azure-threat-detection-fig9.jpg)

資訊安全中心威脅偵測的運作方式自動收集您的 Azure 資源、 hello 網路和連線的交易夥伴方案中的 安全性資訊。  它會分析這項資訊相互關聯多個來源，tooidentify 威脅的資訊。
安全性警示的優先順序資訊安全中心以及如何 tooremediate hello 威脅的建議。

資訊安全中心會運用進階安全性分析，其遠勝於以簽章為基礎的方法。 巨量資料中的突破和[機器學習](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/)技術都使用的 tooevaluate 事件 hello 整個雲端網狀架構 – 偵測會是不可能 tooidentify 使用手動方法，並預測 hello 的威脅演進而來的攻擊。 這些安全性分析包含下列 hello。

### <a name="threat-intelligence"></a>威脅情報

Microsoft 有大量全域威脅情報。
遙測中傳送多個來源，例如 Azure、 Office 365、 Microsoft CRM online、 Microsoft Dynamics AX、 outlook.com、 MSN.com、 hello Microsoft 數位犯罪單元 (DCU)，以及 Microsoft Security Response Center (MSRC)。

![威脅情報](./media/azure-threat-detection/azure-threat-detection-fig10.jpg)

研究人員也會收到威脅情報資訊主要雲端服務提供者之間共用，並從第三方訂閱 toothreat intelligence 摘要。 Azure 資訊安全中心可以使用此資訊 tooalert 您 toothreats 從已知不良執行者。 部分範例包括：

-   **另外 hello 電源 Machine Learning-** Azure 資訊安全中心具有存取 tooa 大量資料的相關雲端網路活動，它可以是使用目標 Azure 部署 toodetect 威脅。 例如：

-   **破解強制偵測-**機器學習服務使用的 toocreate 歷程記錄模式的遠端存取嘗試，好讓它 toodetect 暴力攻擊針對 SSH、 RDP 和 SQL 連接埠。

-   **傳出 DDoS 和殭屍網路偵測**-目標雲端資源的攻擊的常見目標是 toouse hello 選計算能力的這些資源 tooexecute 其他攻擊。

-   **新的行為分析伺服器和 Vm-**一旦伺服器或虛擬機器遭到入侵，攻擊者時避免偵測，確保持續性，因此不可以用各種不同的技術 tooexecute 惡意程式碼在該系統上安全性控制。

-   **Azure SQL Database 威脅偵測-** for Azure SQL Database，識別異常資料庫活動異常和潛在危險的威脅偵測嘗試 tooaccess 或利用資料庫。

### <a name="behavioral-analytics"></a>行為分析

行為分析是一種技術，分析和比較資料 tooa 收集的已知的模式。 不過，這些模式並非簡單的簽章。 它們是透過套用的 toomassive 資料集的複雜的機器學習演算法決定。

![行為分析](./media/azure-threat-detection/azure-threat-detection-fig11.jpg)


它們也能透過專業分析師仔細分析惡意行為來判定。 Azure 資訊安全中心可以使用行為分析 tooidentify 洩漏資源，根據分析的虛擬機器記錄檔、 虛擬網路裝置記錄檔、 網狀架構的記錄檔、 損毀傾印和其他來源。

此外，沒有與其他支援廣泛的行銷活動的辨識項的訊號 toocheck 相互關聯。 此相互關聯可協助建立洩露的指標與一致的 tooidentify 事件。

部分範例包括：
-   **可疑的處理序執行：**攻擊者可以用數種技術 tooexecute 惡意軟體偵測。 比方說，攻擊者可能會讓惡意程式碼 hello 合法的系統檔案相同的名稱，但將這些檔案放在替代位置，使用名稱，非常類似良性的檔案或遮罩 hello 的則為 true 的副檔名。 資訊安全中心模型的處理序行為 」 和 「 監視處理這類執行 toodetect 極端值。

-   **隱藏惡意程式碼和入侵嘗試：**複雜的惡意程式碼可以避開傳統的反惡意程式碼產品永遠不會寫入 toodisk 或加密儲存在磁碟上的軟體元件。 不過，這類惡意程式碼可以時偵測到使用記憶體分析 hello 惡意程式碼必須保留記憶體 toofunction 追蹤。 軟體損毀，損毀傾印會擷取 hello hello 損毀時的記憶體部分。 藉由分析 hello 記憶體 hello 損毀傾印中的，Azure 資訊安全中心可以偵測技術軟體中使用 tooexploit 弱點，存取機密資料，並暗中保存內遭入侵的電腦而不會影響 hello 效能您的電腦。

-   **橫向移動和內部探察：** toopersist 遭盜用的網路和找出/蒐集寶貴資料中，攻擊者通常會嘗試從入侵的 hello 此舉 toomove 內機器 tooothers hello 相同的網路。 資訊安全中心會監視程序，並登入活動 toodiscover 嘗試 tooexpand hello 在網路內，例如遠端命令執行、 網路探查和帳戶列舉的攻擊者的一席之地。

-   **惡意的 PowerShell 指令碼：** PowerShell 可以由攻擊者 tooexecute 惡意程式碼在目標虛擬機器上用於各種用途。 資訊安全中心會檢查 PowerShell 活動，以找到可疑活動的證明。

-   **傳出攻擊：**攻擊者通常目標雲端資源，以 hello 目標使用那些資源 toomount 其他攻擊。 遭盜用的虛擬機器，例如，可能使用的 toolaunch 暴力攻擊其他虛擬機器、 傳送垃圾郵件，或掃描開啟的連接埠與 hello 網際網路上的其他裝置。 藉由套用機器學習 toonetwork 流量，資訊安全中心可以偵測何時輸出網路通訊超過 hello 範數。 當 垃圾郵件、 資訊安全中心也與相互關聯不尋常的電子郵件流量從 Office 365 toodetermine 智慧 hello 郵件是否可能讓或 hello 的合法電子郵件行銷活動的結果。

### <a name="anomaly-detection"></a>異常偵測

Azure 資訊安全中心也會使用異常偵測 tooidentify 威脅。 在對比 toobehavioral analytics 中 （這取決於衍生自大型資料集的已知模式），異常偵測更 」 個人化 」，將著重於特定 tooyour 部署的基準。 機器學習服務是套用的 toodetermine 一般活動，為您的部署，然後再規則便會產生的 toodefine 極端值條件可代表安全性事件。 範例如下：

-   **輸入 RDP/SSH 暴力密碼破解攻擊**︰您的部署中可能包含每天都有許多登入的繁忙虛擬機器，以及有少量或任何登入的其他虛擬機器。 Azure 資訊安全中心可以判斷這些虛擬機器的基準登入活動，並使用機器學習 toodefine 周圍 hello 正常的登入活動。 如果沒有任何差異，與 hello 基準定義登入相關的特性，則可能會產生警示的。 同樣地，機器學習服務會判斷何者值得關注。

### <a name="continuous-threat-intelligence-monitoring"></a>連續威脅情報監視

Azure 資訊安全中心的運作方式與安全性研究與資料科學團隊整個 hello world hello 威脅大環境中的變更持續監視。 這包括下列 initiatives hello:

-   **威脅情報監視**︰威脅情報包含關於現有或新興威脅的機制、指標、影響和可採取動作的建議。 這項資訊會共用 hello 安全性社群中，而且 Microsoft 會持續監視 threat intelligence 摘要內部和外部來源。

-   **訊號共用**︰共用和分析 Microsoft 的資訊安全小組對於各種雲端和內部部署服務、伺服器及用戶端端點裝置組合所提供的深入見解。

-   **Microsoft 資訊安全專家**︰持續與擅長特殊資訊安全領域 (例如鑑識與 Web 攻擊偵測) 的 Microsoft 團隊攜手合作。

-   **偵測微調：**演算法會針對實際的客戶資料集來執行和安全性研究人員會使用客戶 toovalidate hello 結果。 True 和 false 肯定是使用的 toorefine 機器學習演算法。

這些合併的工作做為目標，在全新且改善了偵測，您可以立即獲益於-您 tootake 的任何動作。

## <a name="advanced-threat-detection-features---other-azure-services"></a>進階威脅偵測功能：其他 Azure 服務

### <a name="virtual-machine-microsoft-antimalware"></a>虛擬機器︰Microsoft Antimalware

[Microsoft 反惡意程式碼](https://docs.microsoft.com/azure/security/azure-security-antimalware)Azure 為應用程式和租用戶環境的單一代理程式解決方案，設計 toorun hello 背景需要人為介入。 您可以部署根據您的應用程式工作負載，與其中一個基本安全依預設的 hello 需求或進階自訂組態，包括監視反惡意程式碼的保護。 Azure 的反惡意程式碼是適用於 Azure 虛擬機器的安全性選項，而且會自動安裝在所有的 Azure PaaS 虛擬機器上。

**Azure toodeploy 和啟用 Microsoft 反惡意程式碼應用程式的功能**

#### <a name="microsoft-antimalware-core-features"></a>Microsoft Antimalware 核心功能

-   **即時保護-**監視雲端服務和虛擬機器 toodetect 和封鎖惡意程式碼執行的活動。

-   **排程掃描-**目標掃描 toodetect 惡意程式碼，包括正在執行的程式會定期執行。

-   **惡意程式碼補救**：自動針對偵測到的惡意程式碼採取行動，例如，刪除或隔離惡意檔案，以及清除惡意的登錄項目。

-   **簽章更新-**自動安裝 hello 最新保護 （防毒定義） 的簽章 tooensure 保護是最新的預先決定的頻率。

-   **反惡意程式碼引擎的更新-**自動更新 hello Microsoft 反惡意程式碼引擎。

-   **反惡意程式碼的平台更新 –**自動更新 hello Microsoft 反惡意程式碼的平台。

-   **作用中保護-**遙測中繼資料會報告有關偵測到的威脅和可疑資源 tooMicrosoft Azure tooensure 快速回應 toohello 進化的威脅架構之下，以及啟用透過即時同步的簽章傳遞hello Microsoft Active Protection 系統 (MAPS)。

-   **範例報表-**提供和報表範例 toohello Microsoft 反惡意程式碼服務 toohelp 精簡 hello 服務和啟用疑難排解。

-   **排除項目 –**可讓應用程式和服務系統管理員 tooconfigure 某些檔案時，處理程序，以及磁碟機 tooexclude，其保護和效能及/或其他原因而進行掃描。

-   **反惡意程式碼的事件集合-** hello 反惡意程式碼服務健全狀況、 可疑活動，以及在 hello 作業系統事件記錄檔中所採取的修復動作記錄，並會加以收集到 hello 客戶的 Azure 儲存體帳戶。

### <a name="azure-sql-database-threat-detection"></a>Azure SQL Database 威脅偵測

[Azure SQL Database 威脅偵測](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)是 hello Azure SQL Database 服務內建的新安全性智慧功能。 解決 hello 時鐘 toolearn，設定檔，並偵測的異常資料庫活動、 Azure SQL Database 威脅偵測識別潛在的威脅 toohello 資料庫。

資訊安全人員或其他指定的系統管理員可以在發生可疑的資料庫活動時立即取得通知。 每個通知提供 hello 可疑活動的詳細資料，並建議 toofurther 調查並降低 hello 威脅的方式。

目前，Azure SQL Database 威脅偵測會偵測潛在的弱點與 SQL 插入式攻擊，以及異常的資料庫存取模式。

在收到威脅偵測電子郵件通知時，使用者即無法 toonavigate 和檢視 hello 相關的稽核記錄 hello mail 開啟稽核檢視器和/或預先設定顯示 hello 相關的稽核的稽核 Excel 範本中使用 hello 深層連結周圍 hello 事件時間的 hello 可疑根據 toohello 下列記錄：
-   Hello/具有資料庫伺服器 hello 的異常資料庫活動的稽核儲存體

-   相關的稽核儲存體資料表所使用的 hello 時間 hello 事件 toowrite 稽核記錄檔

-   稽核記錄的 hello hello 事件，就會發生因為下列小時。

-   Hello 事件時間的 hello （某些偵測選擇性） 在稽核記錄類似的事件識別碼

SQL Database 威脅偵測器會使用 hello 遵循偵測方法的其中一個：

-   **決定性偵測 –** hello SQL 用戶端查詢，以符合已知的攻擊中偵測到可疑的模式 （規則為基礎）。 這種方法具有高偵測和低誤判，不過受限於涵蓋範圍，因為它的 「 不可部分完成的偵測 「 hello 類別目錄內。

-   **Behavioural 偵測 –**瑕疵異常的活動，也就是找不到在 hello 過去 30 天的 hello 資料庫異常行為。  SQL 用戶端異常活動的範例可以是失敗的登入查詢及大量解壓縮的資料，不尋常的標準查詢不熟悉的 IP 位址使用 tooaccess hello 資料庫的增量

### <a name="application-gateway-web-application-firewall"></a>應用程式閘道 Web 應用程式防火牆

[Web 應用程式防火牆](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall)是一項功能[Azure 應用程式閘道](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview)tooweb 應用程式使用標準的應用程式閘道提供保護[應用程式傳遞控制](https://kemptechnologies.com/in/application-delivery-controllers)函式。 Web 應用程式防火牆會保護它們對大部分的 hello [OWASP 前 10 個常見的 web 弱點](https://www.owasp.org/index.php/Top_10_2010-Main)

![應用程式閘道 Web 應用程式防火牆](./media/azure-threat-detection/azure-threat-detection-fig13.png)

-   SQL 插入式攻擊保護

-   跨網站指令碼保護

-   常見 Web 攻擊保護，例如命令插入式攻擊、HTTP 要求走私、HTTP 回應分割和遠端檔案包含攻擊

-   防範 HTTP 通訊協定違規

-   防範 HTTP 通訊協定異常行為，例如遺漏主機使用者代理程式和接受標頭

-   防範 Bot、編目程式和掃描器

-   偵測一般應用程式錯誤組態 (也就是 Apache、IIS 等)

在應用程式閘道設定 WAF 提供下列好處 tooyou hello:

-   保護您的 web 應用程式 web 的弱點可能會與沒有修改 toobackend 程式碼的攻擊。

-   保護多個 web 應用程式閘道後方相同時間 hello 應用程式。 應用程式閘道支援所有會保護 web 攻擊，單一閘道後方 too20 網站上裝載。

-   使用應用程式閘道 WAF 記錄所產生的即時報告，監視 Web 應用程式對抗攻擊。

-   特定相容性的控制項需要所有的網際網路對向結束點 toobe 受 WAF 方案。 使用已啟用 WAF 的應用程式閘道，您就可以符合這些法務遵循需求。

### <a name="anomaly-detection--an-api-built-with-azure-machine-learning"></a>異常偵測：使用 Azure Machine Learning 建置的 API

異常偵測是使用 Azure Machine Learning 建置的 API，在時間序列資料中偵測不同類型的異常模式時非常有用。 hello API 指派分數 tooeach 資料點 hello 時間序列，它可以用來產生警示，異常監視透過儀表板，或使用票證系統進行連接。

hello[異常偵測 API](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api)可以偵測到下列的異常類型對時間序列資料的 hello:

-   **升高和畫 Dip:**比方說，監視 hello 登入失敗 tooa 服務數目或簽出的電子商務網站中的數字、 不尋常的尖峰或 dip 無法指出安全性攻擊或服務中斷的情況。

-   **上升和下滑趨勢**：例如，監視計算期間的記憶體使用量時，縮小可用的記憶體大小表示可能發生記憶體流失；監視服務佇列長度時，持續上升的趨勢可能代表發生基本的軟體問題。

-   **層級變更，以及動態值的範圍中的變更：**比方說，層級中服務的延遲之後變更的服務升級或之後升級會有趣 toomonitor 較低層級的例外狀況。

hello 機器學習型應用程式開發介面可讓：

-   **彈性和強大偵測：** hello 異常偵測模型讓使用者 tooconfigure 敏感度設定，並偵測異常行為在季節性和非季節性的資料集之間。 使用者可以較不調整 hello 異常偵測模型 toomake hello 偵測應用程式開發介面，或更為敏感的相應 tootheir 需求。 這表示偵測 hello 資料與不季節性模式中的較少或多個顯示異常狀況。

-   **可擴充且適時偵測：** hello 傳統方式使用存在專家定義域知識所設定的閾值監視會以動態方式變更資料集的成本高同時不可擴充 toomillions。 學到此應用程式開發介面中的 hello 異常偵測模型，模型將自動調整歷程記錄和即時資料。

-   **主動且可採取動作的偵測**：緩慢的趨勢和層級變更偵測可應用於早期異常偵測。 早期 hello 偵測到異常訊號可以使用的 toodirect 人類 tooinvestigate 和處理 hello 問題區域。  此外，還可以在此異常偵測 API 服務之上，開發根本原因分析模型和警示工具。

hello 異常偵測應用程式開發介面是各種不同的案例，就如同服務健全狀況和 KPI 監視 IoT、 效能監視和網路流量監視效能和效率解決方案。 以下提供一些常見案例，此 API 在這類案例中非常實用：
- IT 部門需要及時的工具 tootrack 事件、 錯誤代碼、 使用量記錄和效能 （CPU、 記憶體等）。

-   線上商務網站想 tootrack 客戶活動、 網頁檢視中，按一下、 等等。

-   公用程式的公司都想 tootrack 耗用量上限、 汽油、 電力，以及其他資源。

-   設備/建置管理服務想 toomonitor 溫度、 溼氣、 流量，等等。

-   IoT/製造商想要在時間序列 toomonitor toouse 感應器資料工作流程、 品質，等等。

-   服務提供者，例如撥接中心需要 toomonitor 服務要求趨勢，事件的磁碟區，等候佇列長度，依此類推。

-   商務分析群組想 toomonitor 商務 Kpi （例如銷售的磁碟區，客戶 sentiments，定價） 即時異常移動。

### <a name="cloud-app-security"></a>Cloud App Security

[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security)是 hello Microsoft Cloud Security 堆疊的重要元件。 它是全方位的解決方案，可協助您的組織，當您移動 tootake 充分善用 hello 承諾的雲端應用程式，但讓您控制，透過改良的活動可見度。 此外，它也有助於提高 hello 保護重要資料的所有雲端應用程式。

使用工具，協助找出陰影 IT、 評估風險、 強制執行原則、 調查活動，並停止威脅，您的組織更安全地移 toohello 雲端同時保有重要資料的控制項。

<table style="width:100%">
 <tr>
   <td>探索</td>
   <td>利用 Cloud App Security 來揭露影子 IT。 藉由探索雲端環境中的應用程式、活動、使用者、資料和檔案，來取得可見度。 探索已連接的第三方應用程式 tooyour 雲端。</td>
 </tr>
 <tr>
   <td>調查</td>
   <td>調查雲端應用程式使用雲端鑑識調查工具 toodeep 探討至有風險的應用程式、 特定的使用者及網路中的檔案。 找 hello 資料從雲端收集模式。 產生報表 toomonitor 您的雲端。</td>

 </tr>
 <tr>
   <td>控制</td>
   <td>Tooachieve 充分控制網路雲端流量設定原則和警示來降低風險。 使用 Cloud App Security toomigrate 您使用者 toosafe，保障的雲端應用程式的替代方案。</td>

 </tr>
 <tr>
   <td>Protect</td>
   <td>使用 Cloud App Security toosanction 或禁止的應用程式、 強制執行資料外洩防護、 控制 」 權限和共用，並產生自訂報告和警示。</td>

 </tr>
 <tr>
   <td>控制</td>
   <td>Tooachieve 充分控制網路雲端流量設定原則和警示來降低風險。 使用 Cloud App Security toomigrate 您使用者 toosafe，保障的雲端應用程式的替代方案。</td>

 </tr>
</table>


![Cloud App Security](./media/azure-threat-detection/azure-threat-detection-fig14.png)

Cloud App Security 會透過下列方式來整合您雲端的可見性

-   使用 Cloud Discovery toomap、 找出您的雲端環境並 hello 您的組織使用的雲端應用程式。


-   批准和禁止您雲端中的應用程式。



-   使用易於部署的應用程式連接器，利用提供者 API 來取得您所連接之應用程式的可見度和控管。

-   透過設定，接著持續微調原則，協助您持續進行控制。

在從這些來源收集資料，Cloud App Security 會在 hello 資料中執行複雜的分析。 立即 tooanomalous 活動會提醒您，並讓您深入掌握雲端環境。 您可以在 Cloud App Security 中設定的原則，並使用它 tooprotect 雲端環境中的所有項目。

## <a name="third-party-atd-capabilities-through-azure-marketplace"></a>透過 Azure Marketplace 提供的協力廠商 ATD 功能

### <a name="web-application-firewall"></a>Web 應用程式防火牆

Web 應用程式防火牆會檢查輸入的 Web 流量和並封鎖 SQL 插入、跨網站指令碼、惡意程式碼上傳和應用程式 DDoS，以及目標為您 Web 應用程式的其他攻擊。 它也會檢驗 hello 回應 hello 後端 web 伺服器中的資料遺失防護 (DLP)。 hello 整合式的存取控制引擎可讓系統管理員 toocreate 細微的存取控制原則驗證、 授權和帳戶處理 (AAA)，提供增強式驗證的組織和使用者控制項。

**重點摘要：**
-   偵測並封鎖 SQL 插入、跨網站指令碼、惡意程式碼上傳、應用程式 DDoS 或針對您應用程式的任何其他攻擊。

-   驗證和存取控制。

-   掃描傳出流量 toodetect 敏感性資料，並可以加上遮罩或封鎖 hello 資訊外洩。

-   加速使用功能，例如快取、 壓縮和其他流量最佳化的 web 應用程式內容的 hello 傳遞。

以下是 Azure Market Place 中可用的 Web 應用程式防火牆範例：

[Barracuda Web 應用程式防火牆、 虛擬 Web 應用程式防火牆 Brocade (Brocade vWAF)、 Imperva SecureSphere 和 hello ThreatSTOP IP 防火牆。](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)

## <a name="next-steps"></a>後續步驟

- [Azure 資訊安全中心的偵測功能](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)

Azure 資訊安全中心的進階的偵測功能可協助 tooidentify 目標 Microsoft Azure 資源的作用中威脅，並提供您使用 hello insights 需要 toorespond 快速。

- [Azure SQL Database 威脅偵測 (英文)](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)

Azure SQL Database 威脅偵測協助處理潛在威脅 tootheir 資料庫相關的考量。
