---
title: "aaaAzure 監視器 CLI 1.0 快速入門範例。 | Microsoft Docs"
description: "Azure 監視器功能的範例 CLI 1.0 命令。 Azure 監視 Microsoft Azure 服務可讓您 toosend 警示通知，呼叫的 web Url 會根據設定的遙測資料，並自動調整規模的雲端服務、 虛擬機器和 Web 應用程式的值。"
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a>Azure 監視器跨平台 CLI 1.0 快速入門範例
此發行項會顯示範例命令列介面 (CLI) 命令 toohelp 您存取 Azure 監視功能。 Azure 監視器可讓您 tooAutoScale 雲端服務、 虛擬機器和 Web 應用程式和 toosend 警示通知或呼叫 web Url 根據設定的遙測資料的值。

> [!NOTE]
> Azure 的監視是 hello 所謂 「 Azure Insights"的新名稱，直到 2016 年 9 月 25 日。 不過，hello 命名空間，因此下列 hello 命令仍包含 hello"見解"。
> 
> 

## <a name="prerequisites"></a>必要條件
如果您尚未安裝 hello Azure CLI，請參閱[安裝 hello Azure CLI](../cli-install-nodejs.md)。 如果您是熟悉使用 Azure CLI，您可以深入了解[使用 hello for Mac、 Linux 及 Windows Azure 資源管理員使用 Azure CLI](../xplat-cli-azure-resource-manager.md)。

在 Windows 中，請從 hello 安裝 npm [Node.js 網站](https://nodejs.org/)。 Hello 安裝完成之後，以系統管理員身分執行的權限使用 CMD.exe 執行 hello 下列從 npm 安裝所在的 hello 資料夾：

```console
npm install azure-cli --global
```

接下來，瀏覽 tooany 資料夾/位置並在 hello 命令列中輸入：

```console
azure help
```

## <a name="log-in-tooazure"></a>登入 tooAzure
hello 第一個步驟是 toologin tooyour Azure 帳戶。

```console
azure login
```

執行此命令後，您在 toosign 透過 hello 囉 」 畫面上的指示。 之後，您會看到您的帳戶、TenantId 和預設的訂用帳戶識別碼。所有命令的預設訂閱 hello 內容中都運作。

您目前的訂閱，下列命令使用 hello toolist hello 詳細資料。

```console
azure account show
```

toochange 工作內容 tooa 不同訂用帳戶，下列命令使用 hello。

```console
azure account set "subscription ID or subscription name"
```

toouse Azure 資源管理員和 Azure 監視器命令，您需要在 Azure Resource Manager 模式 toobe。

```console
azure config mode arm
```

tooview 所有支援 Azure 監視器命令清單，請執行下列 hello。

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a>檢視訂用帳戶的活動記錄檔
tooview 一份活動記錄事件，執行下列 hello。

```console
azure insights logs list [options]
```

請嘗試下列 tooview hello 所有可用的選項。

```console
azure insights logs list -help
```

以下是範例 toolist 記錄由 resourceGroup

```console
azure insights logs list --resourceGroup "myrg1"
```

由呼叫者的範例 toolist 記錄檔

```console
azure insights logs list --caller "myname@company.com"
```

呼叫端上的資源類型，請在開始和結束日期的範例 toolist 記錄檔

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a>使用警示
您可以使用警示 hello 區段 toowork hello 資訊。

### <a name="get-alert-rules-in-a-resource-group"></a>取得資源群組中的警示規則
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a>建立度量警示規則
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a>建立 WebTest 警示規則
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a>刪除警示規則
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a>記錄檔的設定檔
使用此記錄檔的設定檔的區段 toowork hello 資訊。

### <a name="get-a-log-profile"></a>取得記錄檔設定檔
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a>新增沒有保留期的記錄檔設定檔
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>移除記錄檔設定檔
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a>新增有保留期的記錄檔設定檔
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a>新增有保留期與 EventHub 的記錄檔設定檔
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a>診斷
使用診斷設定以這個區段 toowork hello 資訊。

### <a name="get-a-diagnostic-setting"></a>取得診斷設定
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a>停用診斷設定
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a>啟用沒有保留期的診斷設定
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a>Autoscale
使用自動調整規模設定具有此區段 toowork hello 資訊。 這些範例需要 toomodify。

### <a name="get-autoscale-settings-for-a-resource-group"></a>取得資源群組的自動調整設定
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a>依名稱取得資源群組中的自動調整設定
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a>設定自動調整設定
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
