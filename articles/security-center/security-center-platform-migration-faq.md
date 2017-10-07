---
title: "aaaSecurity Center 平台移轉常見問題集 |Microsoft 文件"
description: "此常見問題集解答 hello Azure 資訊安全中心平台移轉有關的問題。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a>資訊安全中心平台移轉常見問題集
Azure 資訊安全中心早期年 6 月 2017，開始使用 hello Microsoft Monitoring Agent toocollect 和存放區資料。 詳細資訊，請參閱 toolearn [Azure 安全性 Center 平台移轉](security-center-platform-migration.md)。 此常見問題集解答 hello 平台移轉有關的問題。

## <a name="data-collection-agents-and-workspaces"></a>資料收集、代理程式及工作區

### <a name="how-is-data-collected"></a>資料如何收集？
資訊安全中心會使用您的 Vm 所傳來 hello Microsoft Monitoring Agent toocollect 安全性資料。 hello 安全性資料包含有關安全性組態，也就是使用的 tooidentify 弱點，以及安全性事件，也就是使用的 toodetect 威脅的資訊。 Hello 代理程式所收集的資料會儲存在現有的記錄分析工作區連線 toohello VM 或新的資訊安全中心所建立的工作區中。 當資訊安全中心會建立新的工作區時，hello 地理位置的 hello VM 會列入考量。

> [!NOTE]
> hello Microsoft Monitoring Agent 是由 hello Operations Management Suite (OMS)、 記錄分析服務和 System Center Operations Manager (SCOM) hello 使用相同的代理程式。
>
>

當 hello 啟用資料收集，第一次，或移轉訂用帳戶時，資訊安全中心檢查 toosee hello Microsoft Monitoring Agent 已安裝為 Azure Vm 的每個擴充功能。 如果未安裝 Microsoft Monitoring Agent hello，資訊安全中心將會：

- 在 hello VM 上安裝 hello Microsoft Monitoring agent
   - 已建立，資訊安全中心的工作區存在於相同的地理位置為 hello VM，hello 的 hello 代理程式已連線的 toothis 工作區
   - 如果工作區不存在，資訊安全中心會建立新的資源群組和預設工作區中的地理位置，並連接 hello 代理程式 toothat 工作區。 hello hello 工作區和資源群組的命名慣例如下：

       工作區：DefaultWorkspace-[subscription-ID]-[geo]

       資源群組：DefaultResouceGroup-[geo]
- 安裝資訊安全中心方案上 hello 工作區

hello hello 工作區的位置根據 hello 的 hello VM 的位置。 詳細資訊，請參閱 toolearn[資料安全性](security-center-data-security.md)。

> [!NOTE]
> 先前 tooplatform 移轉的資訊安全中心收集安全性資料從您的 Vm 使用 hello Azure 監視的代理程式和資料儲存在儲存體帳戶。 Hello 平台進行移轉之後，資訊安全中心會使用 Microsoft Monitoring Agent hello 和工作區 toocollect 和市集 hello 相同的資料。 hello 移轉之後，就可以移除 hello 儲存體帳戶。
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a>收費 hello 資訊安全中心所建立的工作區上的 OMS 記錄分析的嗎？
否。 資訊安全中心所建立的工作區雖然設定以每節點之 OMS 計費，但實際上不會產生 OMS 費用。 資訊安全中心計費會永遠根據您的資訊安全中心安全性原則和 hello 解決方案安裝在工作區：

- **免費層次**– 資訊安全中心 hello 'SecurityCenterFree' 方案安裝 hello 預設工作區上。 您不必再支付 hello 免費層。
- **標準層**– 資訊安全中心安裝 hello 'SecurityCenterFree' 和 'Security' 方案 hello 預設工作區。

如需詳細資訊，請參閱[資訊安全中心價格](https://azure.microsoft.com/pricing/details/security-center/)。 hello 定價頁面位址變更 toosecurity 資料存放區，並在 2017 年 6 月計算按比例分配計費啟動。

> [!NOTE]
> hello OMS 定價層的資訊安全中心所建立的工作區不會影響帳單資訊安全中心。
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a>可以刪除 hello 資訊安全中心所建立的預設工作區嗎？
**建議您不要刪除 hello 預設工作區。** 資訊安全中心使用 hello 預設工作區 toostore 安全性資料從您的 Vm。  如果您刪除工作區中，資訊安全中心，而且無法 toocollect 這項資料的一些安全性建議，且無法使用警示

toorecover 移除 hello hello Vm 連接的 toohello 刪除工作區上的 Microsoft Monitoring Agent。 資訊安全中心重新安裝 hello 代理程式，並建立新的預設工作區。

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a>如果做為擴充 hello VM 上已安裝 hello Microsoft Monitoring Agent 嗎？
資訊安全中心不會覆寫現有的連線 toouser 工作區。 資訊安全中心的存放區安全性資料 hello hello 工作區中的 VM 從已連線。

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a>如果我有 Microsoft Monitoring Agent 安裝 hello 機器上，但不是能作為擴充功能？
如果 hello Microsoft Monitoring Agent 直接安裝在 hello VM （不是 Azure 擴充功能）、 資訊安全中心不會安裝 Microsoft Monitoring Agent hello 和安全性監視的內容會受到限制。

### <a name="what-is-hello-impact-of-removing-these-extensions"></a>移除這些擴充功能的 hello 影響為何？
如果您要移除 hello Microsoft 監視功能延伸模組，資訊安全中心不是 hello VM 可以 toocollect 安全性資料，而且某些安全性建議和警示是無法使用。 24 小時內，資訊安全中心會決定 hello VM 遺漏 hello 延伸模組，並重新安裝 hello 延伸模組。

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a>如何停止 hello 自動代理程式安裝和工作區建立？
您可以關閉資料收集 hello 安全性原則中訂用帳戶，但不是建議這樣。 關閉資料收集會限制資訊安全中心的建議和警示。 資料收集都需要訂閱 hello 標準定價層。 toodisable 資料收集：

1. 如果您的訂用帳戶設定為 hello 標準層，開啟 hello 該訂用帳戶的安全性原則，然後選取 hello**免費**層。

   ![定價層 ][1]

2. 接下來，會關閉選取的資料收集**關閉**上 hello**安全性原則-資料收集**刀鋒視窗。

   ![資料收集][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>我要如何移除資訊安全中心安裝的 OMS 擴充功能？
您可以手動移除 hello Microsoft Monitoring Agent。 關閉資料收集會限制資訊安全中心的建議和警示，所以不建議您這麼做。

> [!NOTE]
> 如果已啟用資料收集，資訊安全中心將會重新安裝 hello 代理程式之後您將它移除。  您必須手動移除 hello 代理程式之前，先 toodisable 資料收集。 請參閱[如何停止 hello 自動代理程式安裝和工作區建立？](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?)如需停用資料收集的指示。
>
>

toomanually 移除 hello 代理程式：

1.  在 hello 入口網站中，開啟**記錄分析**。
2.  在 hello 記錄分析刀鋒視窗中，選取工作區：
3.  選取您不想 toomonitor，並選取每個 VM**中斷連線**。

   ![移除 hello 代理程式][3]

> [!NOTE]
> 如果 Linux VM 已經有不含副檔名的 OMS 代理程式，移除 hello 延伸模組會移除 hello 代理程式和 hello 客戶有 tooreinstall 它。
>
>

## <a name="existing-oms-customers"></a>現有的 OMS 客戶

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>資訊安全中心是否會覆寫任何虛擬機器及工作區之間現有的連線？
如果 VM 已經有 hello 安裝為 Azure 擴充功能的 Microsoft Monitoring Agent，資訊安全中心不會覆寫 hello 現有工作區的連接。 相反地，資訊安全中心會使用 hello 現有的工作區。

資訊安全中心方案上 hello 工作區中安裝如果不存在，且 hello 方案套用只有 toohello 相關 Vm。 當您加入方案時，它會自動部署預設 tooall Windows 和 Linux 代理程式連接的 tooyour 記錄分析工作區。 [方案目標](../operations-management-suite/operations-management-suite-solution-targeting.md)，這是一項 OMS 功能，可讓您 tooapply 範圍 tooyour 解決方案。

如果 hello Microsoft Monitoring Agent 直接安裝上 hello VM （不是 Azure 擴充功能）、 資訊安全中心不會安裝 Microsoft Monitoring Agent hello 和安全性監視會受到限制。

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a>如果我認為 hello 資料平台移轉中斷其中一個 Vm 我和我的工作區之間的 hello 連線我該怎麼辦？
這種情況不應發生。 如果還是會發生，然後[建立 Azure 支援人員要求](../azure-supportability/how-to-create-azure-support-request.md)而且包含下列詳細資料的 hello:

- hello Azure 資源識別碼 hello 影響 VM
- hello Azure 資源識別碼 hello hello 的連線已中斷之前，請先 hello 延伸上設定的工作區
- hello 代理程式和先前已安裝的版本

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a>資訊安全中心是否會在我現有的 OMS 工作區上安裝解決方案？ Hello 的計費方式有哪些？
資訊安全中心識別 VM 是已連接的 tooa 建立工作區，資訊安全中心 」 可根據 tooyour 定價層此工作區的解決方案。 hello 解決方案透過相關的 Azure Vm，會套用只有 toohello[方案目標](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)，因此 hello 計費會維持為 hello 相同。

- **免費層次**– 資訊安全中心 hello 'SecurityCenterFree' 方案安裝 hello 工作區上。 您不必再支付 hello 免費層。
- **標準層**– 資訊安全中心安裝 hello 'SecurityCenterFree' 和 'Security' 方案 hello 工作區。

   ![預設工作區的解決方案][4]

> [!NOTE]
> hello 'Security' 方案中記錄分析是 hello 安全性和稽核解決方案在 OMS 中。
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a>在 我的環境中已經有工作區，可以如何使用它們 toocollect 安全性資料嗎？
如果 VM 已經有 hello 安裝為 Azure 擴充功能的 Microsoft Monitoring Agent，資訊安全中心會使用 hello 現有連線的工作區。 資訊安全中心方案上 hello 工作區中安裝如果不存在，而且 hello 方案套用只有 toohello 相關 Vm 透過[方案目標](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)。

資訊安全中心進行安裝時 hello Microsoft Monitoring Agent 在 Vm 上，它會使用 hello 預設 workspace(s) 資訊安全中心所建立。 推出客戶將能夠 tooconfigure 哪些 workspace(s) 可用。

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a>我的工作區上已經有安全性解決方案。 Hello 的計費方式有哪些？
hello 安全性和稽核解決方案是使用的 tooenable 安全性中心標準層功能的 Azure Vm。 如果工作區上已安裝 hello 安全性和稽核解決方案，資訊安全中心會使用 hello 現有的方案。 收費不會改變。

## <a name="next-steps"></a>後續步驟
toolearn 解 hello 資訊安全中心平台移轉，請參閱

- [Azure 資訊安全中心平台移轉](security-center-platform-migration.md)
- [Azure 資訊安全中心疑難排解指南](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
