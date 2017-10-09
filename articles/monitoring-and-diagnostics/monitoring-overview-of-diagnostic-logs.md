---
title: "Azure 診斷記錄檔的 aaaOverview |Microsoft 文件"
description: "了解 Azure 診斷的記錄檔是什麼，以及您可以如何使用這些 toounderstand 事件內的 Azure 資源發生。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>收集並取用來自 Azure 資源的記錄資料

## <a name="what-are-azure-resource-diagnostic-logs"></a>什麼是 Azure 資源診斷記錄
**Azure 資源層級的診斷記錄檔**是由資源發出記錄檔，提供豐富、 且經常 hello 該資源的作業有關的資料。 這些記錄檔的 hello 內容會因資源類型。 例如，網路安全性群組規則計數器和 Key Vault 稽核是其中兩種資源記錄類別。

資源層級的診斷記錄檔不同 hello[活動記錄檔](monitoring-overview-activity-logs.md)。 hello 活動記錄檔提供深入了解您訂用帳戶使用資源管理員，例如，建立虛擬機器，或刪除邏輯應用程式中的資源執行的 hello 操作。 hello 活動記錄檔是訂用帳戶層級記錄檔。 資源層級診斷記錄可讓您深入探索在該資源本身內所執行的作業，例如從 Key Vault 取得密碼。

資源層級診斷記錄也與客體 OS 層級診斷記錄不同。 客體 OS 診斷記錄是由虛擬機器內執行的代理程式或其他支援的資源類型所收集的記錄。 資源層級的診斷記錄檔需要 hello Azure 平台本身，從任何代理程式並擷取特定資源的資料，而客體作業系統層級的診斷記錄檔擷取 hello 作業系統和虛擬機器上執行的應用程式的資料。

並非所有資源都支援 hello 資源此處所述的診斷記錄檔的新的類型。 本文章包含哪些資源類型支援 hello 新資源層級診斷記錄檔的區段清單。

![資源診斷記錄與其他類型的記錄 ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>資源層級診斷記錄的用途
以下是一些您可以執行與資源的診斷記錄檔的 hello 事項：

![資源診斷記錄的邏輯位置](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* 將它們儲存 tooa [**儲存體帳戶**](monitoring-archive-diagnostic-logs.md)稽核或手動檢查。 您可以指定 hello 保留時間 （以天為單位），使用**資源的診斷設定**。
* [它們進行串流處理太**事件中心**](monitoring-stream-diagnostic-logs-to-event-hubs.md)來擷取第三方服務或自訂的分析解決方案，例如 power Bi。
* 以 [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md) 分析記錄檔

您可以使用儲存體帳戶，或不在事件中樞命名空間 hello 相同訂用帳戶，因為 hello 發出記錄檔的其中一個。 將設定 hello 設定的 hello 使用者必須擁有 hello 適當 RBAC 存取 tooboth 訂用帳戶。

## <a name="resource-diagnostic-settings"></a>資源診斷設定
非計算資源的資源診斷記錄是使用資源診斷設定來設定的。 資源的**資源診斷設定**可控制：

* 資源診斷記錄和計量傳送至何處 (儲存體帳戶、事件中樞和/或 OMS Log Analytics)。
* 傳送何種記錄類別，以及是否也會傳送計量資料。
* 每個記錄類別應該在儲存體帳戶中保留多久
    - 保留期為 0 天表示會永遠保留記錄。 否則，hello 值可以是任意數目的 1 到 2147483647 之間的天數。
    - 如果設定保留原則，但記錄檔儲存體帳戶中已停用儲存 （例如，如果只選取事件中心 或 OMS 選項），hello 保留原則會有任何作用。
    - 保留原則套用的每日，因此在 hello 結束日 (UTC) 的記錄從 hello 天現在超出 hello 保留原則會刪除。 例如，如果您在一天的保留原則，hello 從今天 hello 日開始時 hello hello 天前昨天的記錄檔會刪除。

透過 hello hello Azure 入口網站中的資源的診斷設定，透過 Azure PowerShell 和 CLI 命令，或透過 hello，輕鬆地設定這些設定[Azure 監視 REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx)。

> [!WARNING]
> 診斷記錄檔和度量的 hello 客體 OS 層的計算資源 （例如，Vm 或服務的網狀架構） 使用[設定與選取的輸出的不同機制](../azure-diagnostics.md)。
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a>如何 tooenable 收集資源的診斷記錄檔
啟用資源的診斷記錄檔的集合[一部分 Resource Manager 範本中建立資源](./monitoring-enable-diagnostic-logs-using-template.md)或之後從該資源的 hello 入口網站頁面中建立資源。 您也可以啟用在任何時間點，使用 Azure PowerShell 或 CLI 命令，或使用 hello Azure 監視 REST API 的集合。

> [!TIP]
> 這些可能不適用直接 tooevery 資源。 請參閱下方的這個頁面 toounderstand 特殊步驟，可能需支付 toocertain 資源類型 hello hello 結構描述連結。
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a>啟用收集資源 hello 入口網站中的診斷記錄檔
您可以開始收集資源 hello Azure 中的診斷記錄移 tooa 特定資源或瀏覽 tooAzure 監視器建立資源之後，入口網站。 tooenable 這透過 Azure 監視：

1. 在 hello [Azure 入口網站](http://portal.azure.com)，瀏覽 tooAzure 監視器，然後按一下 **診斷設定**

    ![Azure 監視器的監視區段](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. 選擇性地篩選資源群組或資源類型的 hello 清單，然後按一下 hello 資源，您想要 tooset 診斷設定。

3. 如果您選取的 hello 資源上有沒有設定，您必須提示的 toocreate 設定。 按一下「開啟診斷」。

   ![新增診斷設定 - 無現有的設定](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   如果 hello 資源上的現有設定，您會看到已設定此資源上設定的清單。 按一下「新增診斷設定」。

   ![新增診斷設定 - 現有的設定](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. 提供設定名稱，請檢查 hello 方塊，每個目的地 toowhich，toosend 資料，然後設定哪些資源是用於每個目的地。 （選擇性） 設定的天數 tooretain 數，這些記錄檔使用 hello**保留 （天）**滑桿 （只適用 toohello 儲存體帳戶目的地）。 保留的天數零會無限期儲存 hello 記錄檔。
   
   ![新增診斷設定 - 現有的設定](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. 按一下 [儲存] 。

在幾分鐘之後, hello 新設定會出現在清單中的這個資源，設定診斷記錄檔傳送 toohello 會指定目的地，只要產生新的事件資料。

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>透過 PowerShell 啟用資源診斷記錄的收集
透過 Azure PowerShell，下列命令使用 hello 資源診斷的記錄檔的 tooenable 集合：

tooenable 儲存體的診斷記錄檔儲存體帳戶，使用此命令：

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

hello 儲存體帳戶識別碼 hello 資源識別碼 hello 儲存體帳戶 toowhich 想 toosend hello 記錄檔。

tooenable 串流的診斷記錄檔 tooan 事件中樞，使用此命令：

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

hello 服務匯流排規則識別碼是這種格式的字串： `{Service Bus resource ID}/authorizationrules/{key name}`。

tooenable 傳送的診斷記錄檔 tooa 記錄分析工作區中，使用此命令：

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

您可以取得您記錄分析工作區中使用下列命令的 hello hello 資源識別碼：

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

您可以結合這些參數 tooenable 多個輸出選項。

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a>透過 CLI 啟用資源診斷記錄的收集
tooenable 集合資源 hello Azure CLI 透過診斷記錄檔的使用 hello 下列命令：

tooenable 儲存體的診斷記錄檔儲存體帳戶，使用此命令：

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

hello 儲存體帳戶識別碼 hello 資源識別碼 hello 儲存體帳戶 toowhich 想 toosend hello 記錄檔。

tooenable 串流的診斷記錄檔 tooan 事件中樞，使用此命令：

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

hello 服務匯流排規則識別碼是這種格式的字串： `{Service Bus resource ID}/authorizationrules/{key name}`。

tooenable 傳送的診斷記錄檔 tooa 記錄分析工作區中，使用此命令：

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

您可以結合這些參數 tooenable 多個輸出選項。

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>透過 REST API 啟用資源診斷記錄的收集
toochange 診斷設定使用 hello Azure 監視 REST API，請參閱[這份文件](https://msdn.microsoft.com/library/azure/dn931931.aspx)。

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a>管理資源 hello 入口網站中的診斷設定
請確定所有資源皆已設定了診斷設定。 瀏覽過**監視器**hello 入口網站與開啟中**診斷設定**。

![Hello 入口網站中的診斷記錄檔 刀鋒視窗](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

您可能必須 tooclick 「 多個服務 」 toofind hello 監視器 > 一節。

您可以在此處檢視和篩選診斷啟用後，才支援診斷設定 toosee 的所有資源。 您也可以 toosee 向下鑽研，如果在資源上設定多個設定，並檢查哪一個儲存體帳戶、 事件中樞命名空間，及/或資料流向的記錄分析工作區。

![入口網站中的診斷記錄結果](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

新增診斷的設定會顯示 hello 診斷設定檢視中，您可以在其中啟用、 停用，或修改您的診斷設定 hello 選取資源。

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>資源診斷記錄支援的服務、類別和結構描述
[請參閱本文章](monitoring-diagnostic-logs-schema.md)如需支援的服務和 hello 記錄檔分類使用這些服務結構描述的完整清單。

## <a name="next-steps"></a>後續步驟

* [串流處理資源的診斷記錄檔太**事件中心**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [變更資源使用 hello Azure 監視 REST API 的診斷設定](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [使用 Log Analytics 分析來自 Azure 儲存體的記錄](../log-analytics/log-analytics-azure-storage.md)
