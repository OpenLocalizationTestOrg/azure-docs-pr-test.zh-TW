---
title: "在 Azure 資訊安全中心 aaaDetection 功能 |Microsoft 文件"
description: "這份文件可協助您 toounderstand Azure 資訊安全中心偵測功能的運作方式。"
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 4c5599cc-99a1-430f-895f-601615ef12a0
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: d8001cc2acdd0026bd9b3596bbdfec56f8874513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-detection-capabilities"></a>Azure 資訊安全中心的偵測功能
本文討論 Azure 資訊安全中心的進階的偵測功能，這有助於識別目標 Microsoft Azure 資源的作用中威脅，並提供您使用 hello insights 需要 toorespond 快速。

> [!NOTE]
> 進階的偵測 hello 標準層的 Azure 資訊安全中心中可用。 提供 60 天的免費試用。 您可以從 hello hello 中的定價層級選擇升級[安全性原則](security-center-policies.md)。 請瀏覽[資訊安全中心頁面](https://azure.microsoft.com/pricing/details/security-center/)toolearn 更多關於定價。 
> 
> 

## <a name="responding-tootodays-threats"></a>回應 tootoday 的威脅
中已有重大變更 hello 威脅架構之下透過 hello 最後 20 年。 在過去的 hello，公司通常只有 tooworry 有關個別的攻擊者大多是想要查看 「 它們無法執行的動作 」 的網站損毀。 現今的攻擊者更加複雜且有組織性。 他們通常會有特定的財務和策略性目標。 他們也擁有更多的資源可用 toothem，因為它們可能會由民族狀態或有組織的犯罪經費。

這種方法導致 tooan 前所未有的專業 hello 攻擊者陣序規範中。 他們不再對 Web 竄改感興趣。 它們是特定商務、 政治或軍事位置現在竊取資訊、 財務帳戶，以及私用資料 – 可以使用全部都是有興趣 toogenerate 現金 tooleverage hello 開啟市場上。 更多關於財務目標的這些攻擊者比 hello 攻擊者違反網路 toodo 損害 tooinfrastructure 和人員。

為了回應，組織通常會部署各種點解決方案，專注於尋找已知的攻擊簽章的防禦 hello 企業周邊或端點。 這些解決方案通常 toogenerate 大量的要求安全性分析師 tootriage 和調查低精確度警示。 大部分的組織沒有 hello 時間，甚至 unaddressed 知識 toorespond toothese 警示 – 很多。  同時，攻擊者進化其方法 toosubvert 許多的簽章防禦措施及[調整 toocloud 環境](https://azure.microsoft.com/blog/detecting-threats-with-azure-security-center/)。 新的方法都需要的 toomore 快速找出新威脅，並加速偵測和回應。 

## <a name="how-azure-security-center-detects-and-responds-toothreats"></a>Azure 資訊安全中心如何偵測及回應 toothreats
Microsoft 安全性研究人員經常位於 hello lookout 的威脅。 他們有存取 tooan 以免受到擴充獲得 Microsoft 的全域存在 hello 雲端和內部部署中的遙測。 這個寬到達的各種集合的資料集可讓 Microsoft toodiscover 新的攻擊模式和趨勢跨越其內部消費者和企業產品，以及其線上服務。 因此，資訊安全中心可以在攻擊者發行新的和日益複雜的攻擊時，快速地更新其偵測演算法。 這種方法可協助您跟上瞬息萬變的威脅環境。 

資訊安全中心威脅偵測的運作方式自動收集您的 Azure 資源、 hello 網路和連線的交易夥伴方案中的 安全性資訊。 它會分析這項資訊通常相互關聯多個來源，tooidentify 威脅的資訊。 安全性警示的優先順序資訊安全中心以及如何 tooremediate hello 威脅的建議。

![資訊安全中心的資料收集和呈現](./media/security-center-detection-capabilities/security-center-detection-capabilities-fig1.png)

資訊安全中心會運用進階安全性分析，其遠勝於以簽章為基礎的方法。 巨量資料中的突破和[機器學習](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/)技術跨 hello 整個雲端網狀架構 – 偵測會是不可能 tooidentify 使用手動方法，並預測 hello 的威脅是運用 tooevaluate 事件演進而來的攻擊。 這些安全性分析包括︰ 

* **整合威脅情報**： 尋找已知的不良執行者運用 Microsoft 產品和服務，從全域的威脅情報 hello Microsoft 數位犯罪單元 (DCU)，如 hello Microsoft Security Response Center (MSRC) 和外部摘要。
* **行為分析**： 適用於已知的模式 toodiscover 惡意行為。 
* **異常偵測**： 使用統計分析 toobuild 歷程記錄的基準。 它會提醒上偏離已建立符合 tooa 潛在的攻擊誘因的基準。

### <a name="threat-intelligence"></a>威脅情報
Microsoft 有大量全域威脅情報。 遙測中的資料流程來自多個來源，例如 Azure、 Office 365、 Microsoft CRM online、 Microsoft Dynamics AX、 outlook.com、 MSN.com、 hello Microsoft 數位犯罪單元 (DCU) 和 Microsoft Security Response Center (MSRC)。 研究人員也會收到威脅情報資訊主要雲端服務提供者之間共用，並從第三方訂閱 toothreat intelligence 摘要。 Azure 資訊安全中心可以使用此資訊 tooalert 您 toothreats 從已知不良執行者。 部分範例包括：

* **連出通訊 tooa 惡意 IP 位址**： 輸出流量 tooa 已知殭屍網路或 darknet 可能表示您的資源已遭洩漏，攻擊者嘗試 tooexecute 它命令對系統或 exfiltrate 資料。 Azure 資訊安全中心比較網路流量 tooMicrosoft 的全域威脅資料庫，並提醒您，如果它偵測到通訊 tooa 惡意 IP 位址。

## <a name="behavioral-analytics"></a>行為分析
行為分析是一種技術，分析和比較資料 tooa 收集的已知的模式。 不過，這些模式並非簡單的簽章。 它們是透過套用的 toomassive 資料集的複雜的機器學習演算法決定。 它們也能透過專業分析師仔細分析惡意行為來判定。 Azure 資訊安全中心可以使用行為分析 tooidentify 洩漏資源，根據分析的虛擬機器記錄檔、 虛擬網路裝置記錄檔、 網狀架構的記錄檔、 損毀傾印和其他來源。 

此外，沒有與其他支援廣泛的行銷活動的辨識項的訊號 toocheck 相互關聯。 此相互關聯可協助建立洩露的指標與一致的 tooidentify 事件。 部分範例包括：

* **可疑的處理序執行**： 攻擊者可以用數種技術 tooexecute 惡意軟體偵測。 比方說，攻擊者可能會讓惡意程式碼 hello 合法的系統檔案相同的名稱，但將這些檔案放在替代位置，使用的名稱，是非常類似的 tooa 良性檔案或遮罩 hello 的則為 true 的副檔名。 資訊安全中心模型的處理序行為 」 和 「 監視處理這類執行 toodetect 極端值。  
* **隱藏惡意程式碼和入侵嘗試**： 複雜的惡意程式碼永遠不會寫入 toodisk 或加密儲存在磁碟上的軟體元件是可以 tooevade 傳統的反惡意程式碼產品。  不過，這類惡意程式碼可以時偵測到使用記憶體分析 hello 惡意程式碼必須保留在記憶體中順序 toofunction 的追蹤。 軟體損毀，損毀傾印會擷取 hello hello 損毀時的記憶體部分。  藉由分析 hello 損毀傾印中的 hello 記憶體，Azure 資訊安全中心可以偵測技術軟體中使用 tooexploit 弱點、 存取機密資料，並對暗中保存中毒的電腦，而不會影響 hello 效能您的電腦。
* **橫向移動和內部探查**: toopersist 遭盜用的網路和找出/蒐集寶貴資料中，攻擊者通常會嘗試從入侵的 hello 此舉 toomove 內機器 tooothers hello 相同的網路。 資訊安全中心會監視程序，並登入活動中順序 toodiscover 嘗試 tooexpand hello 網路，例如遠端命令執行網路探查和帳戶列舉中的攻擊者的一席之地。
* **惡意的 PowerShell 指令碼**： 攻擊者 tooexecute 惡意程式碼在目標虛擬機器上正在使用 PowerShell 的各種用途。 資訊安全中心會檢查 PowerShell 活動，以找到可疑活動的證明。 
* **傳出攻擊**： 攻擊者通常目標雲端資源，以 hello 目標使用那些資源 toomount 其他攻擊。 遭盜用的虛擬機器，例如，可能會使用的 toolaunch 暴力攻擊其他虛擬機器、 傳送垃圾郵件，或掃描開啟的連接埠和其他裝置上的 hello 網際網路。 藉由套用機器學習 toonetwork 流量，資訊安全中心可以偵測何時輸出網路通訊超過 hello 範數。 在的垃圾郵件 hello 情況下，資訊安全中心也與相互關聯不尋常的電子郵件流量從 Office 365 toodetermine 智慧 hello 郵件是否可能讓或 hello 的合法電子郵件行銷活動的結果。  

### <a name="anomaly-detection"></a>異常偵測
Azure 資訊安全中心也會使用異常偵測 tooidentify 威脅。 在對比 toobehavioral analytics 中 （這取決於衍生自大型資料集的已知模式），異常偵測更 」 個人化 」，將著重於特定 tooyour 部署的基準。 機器學習服務是套用的 toodetermine 一般活動，為您的部署，然後再規則便會產生的 toodefine 極端值條件可代表安全性事件。 範例如下：

* **輸入 RDP/SSH 暴力密碼破解攻擊**︰您的部署中可能包含每天都有大量登入的繁忙虛擬機器，以及有極少量或無任何登入的其他虛擬機器。 Azure 資訊安全中心可以判斷這些虛擬機器的基準登入活動，並使用機器學習 toodefine 什麼超出正常登入活動。 如果差異極大 hello 基準 hello 登入的數目或 hello 一天的時間 hello 登入，或從哪些 hello 登入要求的 hello 位置或其他登入相關的特性，則可能會產生警示。 同樣地，機器學習服務會判斷何者值得關注。

## <a name="continuous-threat-intelligence-monitoring"></a>連續威脅情報監視
Azure 資訊安全中心的運作方式安全性研究和資料科學中，用來持續監視變更 hello 威脅架構之下的小組。 這包括下列 initiatives hello:

* **威脅情報監視**︰威脅情報包含有關現有或新興威脅的機制、指標、影響和可採取動作的建議。 這項資訊會共用 hello 安全性社群中，而且 Microsoft 會持續監視 threat intelligence 摘要內部和外部來源。
* **訊號共用**︰共用和分析 Microsoft 的資訊安全小組對於各種雲端和內部部署服務、伺服器和用戶端端點裝置組合的所提供的深入見解。 
* **Microsoft 資訊安全專家**︰持續與擅長特殊資訊安全領域 (例如鑑識與 Web 攻擊偵測) 的 Microsoft 團隊攜手合作。
* **偵測微調**： 演算法會針對實際的客戶資料集來執行和安全性研究人員會使用客戶 toovalidate hello 結果。 True 和 false 肯定是使用的 toorefine 機器學習演算法。

這些合併的工作做為目標，在全新且改善了偵測，您可以立即獲益於-您 tootake 的任何動作。

## <a name="see-also"></a>另請參閱
在本文件中，您學會 tooAzure 資訊安全中心偵測功能的運作方式。 toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [Azure 資訊安全中心規劃和操作指南](security-center-planning-and-operations-guide.md)
* [管理及回應 toosecurity Azure 資訊安全中心警示](security-center-managing-and-responding-alerts.md)
* [Azure 資訊安全中心不同類型的安全性警示](security-center-alerts-type.md)
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)— 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)— 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。

