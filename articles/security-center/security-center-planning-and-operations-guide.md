---
title: "aaaSecurity Center 計劃與作業指南 |Microsoft 文件"
description: "這份文件可協助您 tooplan 之前採用 Azure 資訊安全中心和每日作業考量。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Azure 資訊安全中心規劃和操作指南
此指南適用於資訊技術 (IT) 專業人員、 IT 架構設計人員、 資訊安全性分析師和其組織打算 toouse Azure 資訊安全中心的雲端系統管理員。

>[!NOTE] 
>從開始早期年 6 月 2017年，資訊安全中心將會使用 hello Microsoft Monitoring Agent toocollect 及儲存資料。 請參閱[Azure 安全性 Center 平台移轉](security-center-platform-migration.md)toolearn 更多。 本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。
>

## <a name="planning-guide"></a>規劃指南
本指南涵蓋了一組步驟和工作，您可以依照的 toooptimize 貴用戶使用的資訊安全中心會根據您組織的安全性需求和雲端管理模型。 資訊安全中心 tootake 充分利用，是重要 toounderstand 方式不同的個人或小組在您的組織使用 hello 服務 toomeet 安全開發和作業、 監視、 控管，和事件回應需求。 hello 主要區域 tooconsider 規劃 toouse 資訊安全中心時如下：

* 安全性角色和存取控制
* 安全性原則和建議
* 資料收集和儲存
* 持續安全性監視
* 事件回應

在 hello 下一步 區段中，您將學習如何 tooplan 這些區域的每個及套用這些建議，根據您的需求。

> [!NOTE]
> 讀取[常見問題集 (FAQ) 的 Azure 資訊安全中心](security-center-faq.md)的 hello 設計和規劃階段期間也很有用的常見問題清單。
> 

## <a name="security-roles-and-access-controls"></a>安全性角色和存取控制
根據 hello 大小和您組織的結構，多個個人和小組可以使用資訊安全中心 tooperform 不同安全性相關的工作。 在下列圖表中的 hello 有虛構人物代表其個別角色和安全性責任的範例：

![角色](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

資訊安全中心可讓這些人員 toomeet 這些不同的責任。 例如：

**Jeff (雲端工作負載擁有者)**

* 管理雲端工作負載和其相關的資源
* 負責根據公司的安全性原則來實作和維護保護

**Ellen (CISO/CIO)**

* 負責所有 hello 公司的安全性課題
* 在雲端工作負載間想 toounderstand hello 公司的安全性狀態
* 需要 toobe 主要攻擊和風險的通知

**David (IT 安全性)**

* 設定公司安全性原則 tooensure hello 適當保護就定位
* 監控安全性原則的遵循狀態
* 產生報告以供主管或稽核人員使用

**Judy (安全性作業)**

* 監視及回應 toosecurity 警示 24/7
* 呈報 tooCloud 工作負載擁有人或 IT 安全性分析師

**Sam (安全性分析師)**

* 調查攻擊
* 使用雲端工作負載擁有者 tooapply 補救 

資訊安全中心使用[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)，這樣會提供[內建角色](../active-directory/role-based-access-built-in-roles.md)toousers、 群組和服務在 Azure 中的可獲指派。 當使用者開啟資訊安全中心時，只看到資訊相關的 tooresources 他們擁有存取權。 這表示 hello 使用者獲指派擁有者、 參與者或讀取器 toohello 訂用帳戶或資源群組的資源屬於 hello 角色。 在加法 toothese 角色中，有兩個特定的資訊安全中心角色：

- **安全性讀取器**： 所屬 toothis 角色的使用者是無法 tooview 權限 tooSecurity 中心，其包含建議、 警示、 原則和健全狀況，不過它無法 toomake 無法變更。
- **安全性管理員**： 相同安全性讀取器，但它也可以更新 hello 安全性原則，關閉建議和警示。

hello 上面所述的資訊安全中心角色不需要存取 Azure 儲存體、 Web 和行動裝置、 或物聯網等的 tooother 服務區域。  

> [!NOTE]
> 使用者需要 toobe 至少一個訂用帳戶、 資源群組擁有者或參與者 toobe 無法 toosee 在 Azure 中的資訊安全中心。 
> 
> 

使用 hello 人物代表 hello 上圖中，會需要下列的 RBAC hello 中說明：

**Jeff (雲端工作負載擁有者)**

* 資源群組擁有者/共同作業者

**David (IT 安全性)**

* 訂用帳戶擁有者/共同作業者或安全性管理員

**Judy (安全性作業)**

* 訂用帳戶的讀取器或安全性讀取器 tooview 警示
* 訂用帳戶擁有者/共同作業者或安全性系統管理員需要 toodismiss 警示

**Sam (安全性分析師)**

* 訂用帳戶的讀取器 tooview 警示
* 訂用帳戶擁有者/共同作業者需要 toodismiss 警示
* 可能需要存取 toohello 工作區

其他一些重要資訊 tooconsider:

* 只有訂用帳戶擁有者/參與者和安全性管理員可以編輯安全性原則
* 只有訂用帳戶和資源群組擁有者和參與者可以套用資源的安全性建議

在規劃使用 RBAC 資訊安全中心的存取控制，是確定 toounderstand 者組織中使用資訊安全中心。 以及他們會執行的工作，然後據此設定 RBAC。

> [!NOTE]
> 我們建議您將指派 hello 最寬鬆的角色所需的使用者 toocomplete 其工作。 例如，只需要 tooview hello 資源的安全性狀態的資訊，但未採取任何動作，例如套用建議，或編輯原則，使用者應該指派 hello 讀取者角色。
> 
> 

## <a name="security-policies-and-recommendations"></a>安全性原則和建議
安全性原則定義中指定的 hello 資源的建議使用的控制項 hello 組訂用帳戶。 資訊安全中心，您定義原則根據 tooyour 公司的安全性需求與 hello 類型的應用程式或 hello 資料的機密性。

會自動啟用 hello 訂用帳戶層級中的原則傳播 tooall hello 訂用帳戶內的資源群組中 hello 下列圖表所示：

![安全性原則](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> 如果您需要的 tooreview 哪些原則已變更，您可以使用[Azure 稽核記錄檔](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/)。 原則變更一定都會記錄在 Azure 稽核記錄檔中。
> 
> 

### <a name="security-recommendations"></a>安全性建議
然後再設定安全性原則，請檢閱每個 hello[安全性建議](security-center-recommendations.md)，並判斷是否這些原則適用於各種不同的訂用帳戶和資源群組。 它也是重要的 toounderstand tooaddress 應該採取哪些動作[安全性建議](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations)以及組織中負責監視新的建議和製作 hello 所需的步驟。

資訊安全中心會建議您針對您的 Azure 訂用帳戶提供安全性連絡人詳細資料。 這項資訊將供 Microsoft toocontact 您如果 hello Microsoft Security Response Center (MSRC) 探索非法或未經授權的合作對象已存取您的客戶資料。 讀取[提供安全性 Azure 資訊安全中心中的連絡人詳細資料](security-center-provide-security-contact-details.md)如需有關如何 tooenable 這項建議。

## <a name="data-collection-and-storage"></a>資料收集和儲存
Azure 資訊安全中心使用 hello Microsoft Monitoring Agent – 這是使用相同的代理程式的 hello Operations Management Suite，記錄分析服務 – toocollect 安全性資料，從您的虛擬機器的 hello。 從這個代理程式收集的資料會儲存在 Log Analytics 工作區中。

### <a name="agent"></a>代理程式

在 hello 安全性原則已啟用資料收集之後，hello Microsoft Monitoring Agent (如[Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents)或[Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) 已安裝在所有支援的 Azure Vm，然後建立任何新的。  如果 VM 已經有 Microsoft Monitoring Agent 安裝，hello hello Azure 資訊安全中心會利用目前的 hello 安裝代理程式。 hello 代理程式的程序是設計的 toobe 非侵入性功能，並對 VM 效能變得很小的影響。

Microsoft Monitoring Agent 的 Windows hello 需要使用 TCP 連接埠 443。 請參閱 hello[疑難排解文章](security-center-troubleshooting-guide.md)如需詳細資訊。

如果您想要有 toodisable 資料收集在某個時間點，可以在 hello 安全性原則中關閉它。 不過，hello Microsoft Monitoring Agent 可能會由其他 Azure 管理和監視服務，hello 代理程式將不會自動解除安裝，因為當您關閉資訊安全中心中的資料收集。 您可以手動解除安裝 hello 代理程式所需。

> [!NOTE]
> 一份支援的 Vm，讀取 hello toofind[常見問題集 (FAQ) 的 Azure 資訊安全中心](security-center-faq.md)。
> 

### <a name="workspace"></a>工作區

從 Microsoft Monitoring Agent （代表 Azure 資訊安全中心） 會儲存在現有記錄分析 workspace(s) hello 收集的資料與相關聯 Azure 訂用帳戶或新 workspace(s)，納入帳戶 hello hello VM 的地理。 

在 hello Azure 入口網站，您可以瀏覽 toosee 記錄分析工作區，包括任何 Azure 資訊安全中心所建立的清單。 將會針對新的工作區建立相關的資源群組。 兩者都會遵照此命名慣例： 

* 工作區：*DefaultWorkspace-[subscription-ID]-[geo]*
* 資源群組：*DefaultResouceGroup-[geo]*

若為 Azure 資訊安全中心所建立的工作區，資料會保留 30 天。 結束工作區，保留根據 hello 工作區的定價層。

> [!NOTE]
> Microsoft 會進行這項資料的強式承諾 tooprotect hello 隱私與安全性。 Microsoft 遵守 toostrict 相容性與安全性指導方針 — 從 toooperating 服務撰寫程式碼。 如需資料處理和隱私權的詳細資訊，請閱讀 [Azure 資訊安全中心資料安全性](security-center-data-security.md)。
> 

## <a name="ongoing-security-monitoring"></a>持續安全性監視
初始設定和應用程式的資訊安全中心建議之後, hello 下一個步驟的考量資訊安全中心操作程序。

從 Azure 入口網站，您可以按一下 hello tooaccess 資訊安全中心**瀏覽**和型別**資訊安全中心**在 hello**篩選**欄位。 hello hello 使用者取得會根據 toothese 套用篩選的檢視，下方的 hello 範例顯示定址的許多問題 toobe 環境：

![儀表板](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> 資訊安全中心不會干擾一般作業程序，則被動會監視您的部署，並提供您啟用 hello 安全性原則為基礎的建議。

當您第一次選擇 toouse 資訊安全中心進行目前的 Azure 環境時，請確定您檢閱所有的建議，可依 hello**建議**磚或每個資源 (**計算****網路**，**儲存體與資料**，**應用程式**)。

一旦您解決所有建議，hello**防止**區段應為綠色的已解決的所有資源。 持續不斷的監控此時可更輕鬆因為您將會僅依據採取動作 hello 資源安全性健康情況及建議磚中的變更。

hello**偵測**區段是更反應式，這些問題可能是發生現在，或發生在過去的 hello 所偵測的資訊安全中心控制項和第 3 個合作對象系統所發出的警示。 hello 安全性警示磚會顯示代表每一天，以及其 hello 不同嚴重性分類 （低、 中高） 之間的分佈中找不到的威脅偵測警示的 hello 數目的長條圖。 如需有關安全性警示的詳細資訊，請閱讀[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)。

> [!NOTE]
> 您也可以利用 Microsoft Power BI toovisualize 資訊安全中心資料。 請閱讀 [使用 Power BI 從 Azure 資訊安全中心的資料取得見解](security-center-powerbi.md)。
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>監視新的或已變更的資源
大多數 Azure 環境是動態的，包含定期上下波動的新資源、組態或變更等。資訊安全中心可協助確保您擁有 hello 安全性狀態，這些新的資源可視性。

當您新增新的資源 （Vm、 SQL 資料庫） tooyour Azure 環境時，資訊安全中心會自動探索這些資源，並開始 toomonitor 它們的安全性。 這也包括 PaaS Web 角色和背景工作角色。 如果已啟用資料收集在 hello[安全性原則](security-center-policies.md)、 其他監視功能將會自動啟用您的虛擬機器。

![主要領域](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. 針對虛擬機器，按一下 [預防] 區段下的 [計算]。 啟用資料或相關的建議的任何問題會發生在 hello**概觀** 索引標籤和**監視建議**> 一節。
2. 檢視 hello**建議**toosee 什麼，如果有的話，已辨識 hello 新資源的安全性風險。
3. 是非常普遍，當新的 Vm 加入 tooyour 環境時，只有 hello 一開始安裝作業系統。 hello 資源擁有者可能需要一些時間 toodeploy 將這些 Vm 所使用的其他應用程式。  在理想情況下，您應該知道此工作負載的 hello 最終的目的。 它即將 toobe 應用程式伺服器嗎？ 根據此新的工作負載會持續 toobe，您可以啟用適當的 hello**安全性原則**，這是此工作流程中的 hello 第三個步驟。
4. 當新的資源加入 tooyour Azure 環境時，很可能在新的警示會顯示在 hello**安全性警示**磚。 一律驗證此磚中是否有新警示，並採取根據 tooSecurity 中心建議的動作。

您也會想 tooregularly 監視 hello 狀態現有資源 tooidentify 的組態變更已建立的安全性風險，建議的基準，以及安全性警示從漂移。 在 hello 資訊安全中心儀表板開始。 從該處，您會有三個主要區域 tooreview 持續。

![作業](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. hello**防止**區段面板提供您快速存取 tooyour 重要資源。 使用此選項 toomonitor 計算、 網路、 儲存體及資料和應用程式。
2. hello**建議**面板可讓您 tooreview 資訊安全中心建議。 持續監視期間可能會發現您不需要每日，這是正常現象，因為定址在 hello 初始資訊安全中心設定的所有建議的建議。 基於這個理由，您可能沒有新的資訊在本節中每一天，只需要 tooaccess 視它。
3. hello**偵測**區段可能會非常頻繁或非常不頻繁的基礎上變更。 請隨時檢閱安全性警示，並根據資訊安全中心的建議採取動作。

## <a name="incident-response"></a>事件回應
資訊安全中心會偵測並警示您 toothreats 發生。 組織應該為新的安全性警示來監視和採取動作為所需 tooinvestigate 進一步或補救 hello 攻擊。 如需資訊安全中心威脅偵測運作方式的詳細資訊，請閱讀 [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)。

雖然本文不會有 hello 意圖 tooassist 您建立自己的事件回應計劃，我們 toouse Microsoft Azure 安全性回應 hello 雲端生命週期中的為 hello 基礎事件回應階段。 hello 下列圖表顯示 hello 階段：

![可疑的活動](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> 您可以使用 hello 美國國家標準與技術局 (NIST)[電腦安全性事件處理指南](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf)參考 tooassist 為您建置自己。
> 

您可以使用安全性中心警示期間 hello 下列階段：

* **偵測**︰識別一或多個資源中的可疑活動。 
* **評估**： 執行 hello 初始評估 tooobtain hello 可疑活動的詳細資訊。
* **診斷**： 使用 hello 補救步驟 tooconduct hello 技術的程序 tooaddress hello 問題。

每個安全性警示提供的資訊，可以用 toobetter 瞭解 hello 攻擊的 hello 本質，並建議可能的補救措施。 某些警示也會提供連結 tooeither 更多的資訊或 tooother 來源 Azure 中的資訊。 您可以使用 hello 做進一步研究和 toobegin 降低所提供的資訊，您也可以搜尋儲存在您的工作區的安全性相關資料。

hello 下例示範可疑的 RDP 活動正在進行中：

![可疑的活動](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

如您所見，此刀鋒視窗會顯示有關 hello 時間 hello 攻擊發生、 hello 來源主機名稱、 hello 目標 VM 和也會提供建議步驟。 在某些情況下 hello hello 攻擊的來源資訊可能是空的。 如需有關這類行為的詳細資訊，請閱讀 [Azure 資訊安全中心警示中的缺少來源資訊](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) 。

在 hello [tooLeverage 如何 hello Azure 資訊安全中心 & Microsoft Operations Management Suite 事件回應](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703)視訊可以看到可協助您 toounderstand 如何使用資訊安全中心，在每個部分示範其中的一個階段。

> [!NOTE]
> 讀取[Leveraging Azure 資訊安全中心事件回應](security-center-incident-response.md)如需 toouse 資訊安全中心功能 tooassist 您期間事件回應程序的詳細資訊。 
> 
> 

## <a name="see-also"></a>另請參閱
在本文件中，您學到如何 tooplan 資訊安全中心採用。 toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [管理及回應 toosecurity Azure 資訊安全中心警示](security-center-managing-and-responding-alerts.md)
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)— 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)— 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。

