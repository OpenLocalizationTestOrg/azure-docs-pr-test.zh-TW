---
title: "aaaProtect 個人資料與 Azure 資訊安全中心 |Microsoft 文件"
description: "使用 Azure 資訊安全中心保護個人資料"
services: security
documentationcenter: na
author: Barclayn
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
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a>保護個人資料免受入侵和攻擊：Azure 資訊安全中心

本文將協助您了解如何 toouse Azure 資訊安全中心 tooprotect 個人資料與破壞，攻擊。

## <a name="scenario"></a>案例 

大型出航公司搬遷後在 hello 美國，展開在 hello 地中海與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。 toohelp 中這些工作，它所取得數個較小的出航行位於義大利、 德國、 丹麥和 hello 英國

hello 公司使用 Microsoft Azure toostore 公司資料 hello 雲端中。 其中包含名稱、地址、電話號碼和信用卡資訊等個人識別資訊。 它也包含類似如下的人力資源資訊：

- 位址
- 電話號碼
- 稅務識別編號
- 醫療資訊

hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫。 位於 hello 世界各地的公司員工存取 hello 網路從 hello 公司遠端辦公室和旅行代理程式已存取 toosome 公司資源。
個人資料會傳送 hello 網路中，這些位置與 hello Microsoft 資料中心之間。

## <a name="problem-statement"></a>問題陳述

hello 公司是擔心 hello 威脅的攻擊，在他們的 Azure 資源上。 他們想 tooprevent 公開客戶的和員工的個人資料 toounauthorized 人員。 他們想防止和回應/修復所造成，以及與其雲端資源有效地 toomonitor hello 持續安全性的指引。
他們需要堅強的防線來抵禦今日複雜且有組織的攻擊者。

## <a name="company-goal"></a>公司目標

其中一個 hello 公司的目標是客戶和員工的個人資料 tooensure hello 隱私權保護不受威脅。 其目標是 toorespond 立即的缺口 toomitigate toosigns hello 影響。 它需要 tooassess hello 目前的安全性狀態的方式、 識別易受攻擊的組態，並進行補救。

## <a name="solutions"></a>解決方案

Microsoft Azure 資訊安全中心 (ASC) 提供了整合式安全性監控和原則管理解決方案。 它提供威脅預防、偵測及回應功能，簡單易用又有效。

### <a name="prevention"></a>預防

ASC 有助於讓您 tooset 安全性原則，以避免破壞，提供在 just-in-time 存取，並實作安全性建議。

安全性原則會定義控制項中指定的 hello 資源的建議 hello 組訂用帳戶。 在可以存取使用的 toolock 輸入的流量 tooyour Azure Vm，降低暴露 tooattacks 關閉。 安全性建議會分析您的 Azure 資源 hello 安全性狀態後建立 ASC。

#### <a name="how-do-i-set-security-policies-in-asc"></a>如何在 ASC 設定安全性原則？

您可以為每個訂用帳戶設定安全性原則。 toomodify 安全性原則，您必須是擁有者或參與者的訂用帳戶。 在 hello Azure 入口網站，請勿 hello 遵循：

1. 選取**原則**hello ASC 儀表板中。

2. 選取您想要 tooenable hello 原則 hello 訂用帳戶。

3. 選擇**防止原則**tooconfigure 每個訂閱的原則。 **從虛擬機器收集資料**應該設定太**上。**

4. 在 hello**防止原則**選項中，選取**上**hello 訂用帳戶相關的 tooenable hello 安全性建議。

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

如需詳細指示，以及每個可啟用的 hello 原則建議的說明，請參閱[Azure 資訊安全中心中設定安全性原則](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies)。

#### <a name="how-do-i-configure-just-in-time-access-jit"></a>如何設定 Just-In-Time (JIT) 存取？

啟用 JIT 時，資訊安全中心鎖定輸入的流量 tooyour Azure Vm 建立 NSG 規則。 您選取 hello 連接埠上 hello VM toowhich 輸入的流量會鎖定。 toouse JIT 存取，請執行下列 hello:

1. 選取 hello**時間 VM 存取磚中的恰好**hello ASC 刀鋒視窗上。

2. 選取 hello**建議** 索引標籤。

3. 在下**Vm**，選取您想 tooenable hello Vm。 這會使核取記號下一步 tooa VM。 
4. 在 VM 上選取 [啟用 JIT]。
5. 選取 [ **儲存**]。

然後您就可以看到 ASC 建議啟用 JIT hello 預設連接埠。 您也可以加入，並設定新的連接埠，您想要只在時間方案 tooenable hello。 hello**階段 VM 存取中的恰好**hello 資訊安全中心中的磚會顯示 hello 設定 JIT 權限的 Vm 數目。 它也會顯示 hello 核准的存取提出的要求數目 hello 在過去一週。

![](media/protect-personal-data-azure-security-center/jit-vm.png)

如需有關指示 toodo，以及其他有關恰好階段存取，請參閱[管理只在時間中使用的虛擬機器存取權。](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

#### <a name="how-do-i-implement-asc-security-recommendations"></a>如何實作 ASC 安全性建議？

當資訊安全中心識別潛在的安全性弱點時，它會建立建議。 hello 建議會引導您完成設定所需的 hello 控制項的 hello 程序。 
1. 選取 hello**建議**hello ASC 儀表板上的磚。

2. 檢視會顯示以資料表格式，其中每一行代表一個建議的 hello 建議。

3. toofilter 建議選取**篩選**並選取您想 toosee hello 嚴重性和狀態值。

4. toodismiss 不適用的建議，您可以以滑鼠右鍵按一下並選取**解除。**

5. 評估應該先套用的建議。

6. 適用於 hello 建議的優先順序。

如需可能的建議和逐步解說如何 tooapply 每個，請參閱[管理 Azure 資訊安全中心中的安全性建議。](https://docs.microsoft.com/azure/security-center/security-center-recommendations)

### <a name="detection-and-response"></a>偵測和回應

偵測和回應會一起使用，因為您之後想要 toorespond 盡快偵測到威脅。
ASC 威脅偵測的運作方式自動收集您的 Azure 資源、 hello 網路和連線的交易夥伴方案中的 安全性資訊。 ASC 可以在攻擊者發行新的和日益複雜的攻擊時，快速地更新其偵測演算法。 如需 ASC 威脅偵測運作方式的詳細資訊，請參閱 [Azure 資訊安全中心的偵測功能](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)。

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a>如何管理及回應 toosecurity 警示？

優先順序的安全性警示的清單會顯示在資訊安全中心，以及 hello 資訊需要 tooquickly 調查 hello 問題。 資訊安全中心也包含如何建議 tooremediate 攻擊。 您的安全性警示，執行下列的 hello toomanage:

1. 選取 hello**安全性警示**磚 hello ASC 儀表板中。 這會顯示每個警示的詳細資料。

2. 根據日期、 狀態和嚴重性，toofilter 警示選取**篩選**，然後選取您想要 toosee hello 值。

3. toorespond tooan 警示，請選取它並檢閱 hello 的詳細資訊，然後選取遭到攻擊的 hello 資源。

4. 在 [hello**描述**] 欄位中，您會看到的詳細資訊，包括建議的修復。

![](media/protect-personal-data-azure-security-center/security-alerts.png)

如需詳細指示回應 toosecurity 警示，請參閱[中 Azure 資訊安全中心的管理，而且有回應 toosecurity 警示。](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)

取得進一步的協助調查安全性警示，hello 公司可以有它自己的 SIEM 解決方案，整合 ASC 警示使用[Azure 記錄檔整合](https://aka.ms/AzLog)。

#### <a name="how-do-i-manage-security-incidents"></a>如何管理安全性事件？

在 ASC 中，安全性事件是符合攻擊鏈模式之資源的所有警示彙總。 事件會顯示 hello 相關警示清單，可讓您 tooobtain 每次出現的詳細資訊。 事件會出現在 安全性警示磚的 hello 和刀鋒視窗。

tooreview 及管理安全性事件，請執行下列 hello:

1. 選取 hello**安全性警示**磚。 如果偵測到安全性事件時，它會顯示 hello 安全性警示圖表下方。 它會有不同於其他警示的圖示。

2. 選取 hello 事件 toosee 此安全性事件相關的更多詳細資料。 包含其完整描述，其嚴重性、 其目前狀態、 遭受攻擊的 hello 資源，hello 修復步驟 hello 事件的詳細資訊和 hello 已包含在此事件的警示。

您可以篩選 toosee**事件只**，**警示只**，或**兩者**。

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a>如何存取 hello Threat Intelligence 報表？

ASC 會分析來自多個來源 tooidentify 威脅的資訊。 tooassist 事件回應小組調查並補救威脅，資訊安全中心包含威脅智慧報表，其中包含已偵測到的 hello 威脅的相關資訊。

資訊安全中心有三種威脅報告，不同攻擊會提供不同的報告。
可用的 hello 報告為：

- 群組活動報告︰提供攻擊者、其目標和策略的深入探討。

- 活動報告︰著重說明特定攻擊活動的詳細資料。

- 威脅的摘要報告： 涵蓋 hello 先前的兩個報表中的所有項目。

這種類型的資訊是很有幫助 hello 事件回應程序期間，當 hello 攻擊的進行中調查 toounderstand hello 來源時，hello 攻擊者的動機和哪些 toodo toomitigate 這個問題接下來。

1. tooaccess hello 威脅情報回報，請執行下列 hello:

2. 選取 hello**安全性警示**hello ASC 儀表板上的磚。

3. 選取您想要的 tooobtain hello 安全性警示的詳細資訊。

4. 在 hello**報表**欄位中，按一下 hello 連結 toohello threat intelligence 報表。

5. 這會開啟 hello PDF 檔案，您可以下載。

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

如需 hello ASC threat intelligence 報告的詳細資訊，請參閱[Azure 安全性中心 Threat Intelligence 報告。](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

### <a name="assessment"></a>評量

toohelp 與測試、 評估和評估安全性狀態，ASC 提供整合的弱點可能會評估與 Qualys 雲端代理程式，其虛擬機器的建議元件的一部分。

hello Qualys 代理程式回報的弱點可能會資料 toohello Qualys 管理平台，然後將傳送的弱點可能會和狀況監控資料回 tooASC。 hello 的弱點可能會評估解決方案會顯示在 hello 建議 tooadd**建議**hello ASC 儀表板上的刀鋒視窗。

Hello 目標 VM 上安裝 hello 的弱點可能會評估解決方案後，資訊安全中心掃描 hello VM toodetect 和識別系統和應用程式的安全性弱點。 偵測到問題會顯示在下面的 hello**虛擬機器建議**選項。

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a>如何實作弱點評量解決方案？ 

如果虛擬機器尚未部署整合式弱點評量解決方案，資訊安全中心會建議予以安裝。

1. Hello ASC 儀表板 上 hello**建議**刀鋒視窗中，選取**新增的弱點可能會評估解決方案。**

2. 選取您想要 tooinstall hello 的弱點可能會評估解決方案的 hello Vm。

3. 按一下 [Install on [number of] VMs] \(安裝在 [數目] 部 VM 上)。

4. Hello Azure Marketplace 中或之下，選取夥伴方案**使用現有的方案，**選取**Qualys。**

5. 您可以開啟 hello 的自動更新設定開啟或關閉在 hello**協力廠商解決方案**刀鋒視窗。

如需有關的進一步指示 tooimplement 的弱點可能會評估解決方案，請參閱[Azure 資訊安全中心中的弱點可能會評估。](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)

## <a name="next-steps"></a>後續步驟

- [Azure 資訊安全中心快速入門指南](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [簡介 tooAzure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [整合 Azure 資訊安全中心警示與 Azure 記錄整合](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [Boost Azure Security Center with Integrated Vulnerability Assessment](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/) (利用整合式弱點評量增強 Azure 資訊安全中心)
