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
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="f3b7b-105">Azure 監視器跨平台 CLI 1.0 快速入門範例</span><span class="sxs-lookup"><span data-stu-id="f3b7b-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="f3b7b-106">此發行項會顯示範例命令列介面 (CLI) 命令 toohelp 您存取 Azure 監視功能。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-106">This article shows you sample command-line interface (CLI) commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="f3b7b-107">Azure 監視器可讓您 tooAutoScale 雲端服務、 虛擬機器和 Web 應用程式和 toosend 警示通知或呼叫 web Url 根據設定的遙測資料的值。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-107">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="f3b7b-108">Azure 的監視是 hello 所謂 「 Azure Insights"的新名稱，直到 2016 年 9 月 25 日。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-108">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="f3b7b-109">不過，hello 命名空間，因此下列 hello 命令仍包含 hello"見解"。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-109">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f3b7b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f3b7b-110">Prerequisites</span></span>
<span data-ttu-id="f3b7b-111">如果您尚未安裝 hello Azure CLI，請參閱[安裝 hello Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-111">If you haven't already installed hello Azure CLI, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="f3b7b-112">如果您是熟悉使用 Azure CLI，您可以深入了解[使用 hello for Mac、 Linux 及 Windows Azure 資源管理員使用 Azure CLI](../xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="f3b7b-113">在 Windows 中，請從 hello 安裝 npm [Node.js 網站](https://nodejs.org/)。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-113">In Windows, install npm from hello [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="f3b7b-114">Hello 安裝完成之後，以系統管理員身分執行的權限使用 CMD.exe 執行 hello 下列從 npm 安裝所在的 hello 資料夾：</span><span class="sxs-lookup"><span data-stu-id="f3b7b-114">After you complete hello installation, using CMD.exe with Run As Administrator privileges, execute hello following from hello folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="f3b7b-115">接下來，瀏覽 tooany 資料夾/位置並在 hello 命令列中輸入：</span><span class="sxs-lookup"><span data-stu-id="f3b7b-115">Next, navigate tooany folder/location you want and type at hello command-line:</span></span>

```console
azure help
```

## <a name="log-in-tooazure"></a><span data-ttu-id="f3b7b-116">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="f3b7b-116">Log in tooAzure</span></span>
<span data-ttu-id="f3b7b-117">hello 第一個步驟是 toologin tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-117">hello first step is toologin tooyour Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="f3b7b-118">執行此命令後，您在 toosign 透過 hello 囉 」 畫面上的指示。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-118">After running this command, you have toosign in via hello instructions on hello screen.</span></span> <span data-ttu-id="f3b7b-119">之後，您會看到您的帳戶、TenantId 和預設的訂用帳戶識別碼。所有命令的預設訂閱 hello 內容中都運作。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in hello context of your default subscription.</span></span>

<span data-ttu-id="f3b7b-120">您目前的訂閱，下列命令使用 hello toolist hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-120">toolist hello details of your current subscription, use hello following command.</span></span>

```console
azure account show
```

<span data-ttu-id="f3b7b-121">toochange 工作內容 tooa 不同訂用帳戶，下列命令使用 hello。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-121">toochange working context tooa different subscription, use hello following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="f3b7b-122">toouse Azure 資源管理員和 Azure 監視器命令，您需要在 Azure Resource Manager 模式 toobe。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-122">toouse Azure Resource Manager and Azure Monitor commands, you need toobe in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="f3b7b-123">tooview 所有支援 Azure 監視器命令清單，請執行下列 hello。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-123">tooview a list of all supported Azure Monitor commands, perform hello following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="f3b7b-124">檢視訂用帳戶的活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="f3b7b-124">View activity log for a subscription</span></span>
<span data-ttu-id="f3b7b-125">tooview 一份活動記錄事件，執行下列 hello。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-125">tooview a list of activity log events, perform hello following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="f3b7b-126">請嘗試下列 tooview hello 所有可用的選項。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-126">Try hello following tooview all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="f3b7b-127">以下是範例 toolist 記錄由 resourceGroup</span><span class="sxs-lookup"><span data-stu-id="f3b7b-127">Here is an example toolist logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="f3b7b-128">由呼叫者的範例 toolist 記錄檔</span><span class="sxs-lookup"><span data-stu-id="f3b7b-128">Example toolist logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="f3b7b-129">呼叫端上的資源類型，請在開始和結束日期的範例 toolist 記錄檔</span><span class="sxs-lookup"><span data-stu-id="f3b7b-129">Example toolist logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="f3b7b-130">使用警示</span><span class="sxs-lookup"><span data-stu-id="f3b7b-130">Work with alerts</span></span>
<span data-ttu-id="f3b7b-131">您可以使用警示 hello 區段 toowork hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-131">You can use hello information in hello section toowork with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="f3b7b-132">取得資源群組中的警示規則</span><span class="sxs-lookup"><span data-stu-id="f3b7b-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="f3b7b-133">建立度量警示規則</span><span class="sxs-lookup"><span data-stu-id="f3b7b-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="f3b7b-134">建立 WebTest 警示規則</span><span class="sxs-lookup"><span data-stu-id="f3b7b-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="f3b7b-135">刪除警示規則</span><span class="sxs-lookup"><span data-stu-id="f3b7b-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="f3b7b-136">記錄檔的設定檔</span><span class="sxs-lookup"><span data-stu-id="f3b7b-136">Log profiles</span></span>
<span data-ttu-id="f3b7b-137">使用此記錄檔的設定檔的區段 toowork hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-137">Use hello information in this section toowork with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="f3b7b-138">取得記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="f3b7b-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="f3b7b-139">新增沒有保留期的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="f3b7b-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="f3b7b-140">移除記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="f3b7b-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="f3b7b-141">新增有保留期的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="f3b7b-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="f3b7b-142">新增有保留期與 EventHub 的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="f3b7b-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="f3b7b-143">診斷</span><span class="sxs-lookup"><span data-stu-id="f3b7b-143">Diagnostics</span></span>
<span data-ttu-id="f3b7b-144">使用診斷設定以這個區段 toowork hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-144">Use hello information in this section toowork with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="f3b7b-145">取得診斷設定</span><span class="sxs-lookup"><span data-stu-id="f3b7b-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="f3b7b-146">停用診斷設定</span><span class="sxs-lookup"><span data-stu-id="f3b7b-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="f3b7b-147">啟用沒有保留期的診斷設定</span><span class="sxs-lookup"><span data-stu-id="f3b7b-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="f3b7b-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="f3b7b-148">Autoscale</span></span>
<span data-ttu-id="f3b7b-149">使用自動調整規模設定具有此區段 toowork hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-149">Use hello information in this section toowork with autoscale settings.</span></span> <span data-ttu-id="f3b7b-150">這些範例需要 toomodify。</span><span class="sxs-lookup"><span data-stu-id="f3b7b-150">You need toomodify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="f3b7b-151">取得資源群組的自動調整設定</span><span class="sxs-lookup"><span data-stu-id="f3b7b-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="f3b7b-152">依名稱取得資源群組中的自動調整設定</span><span class="sxs-lookup"><span data-stu-id="f3b7b-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="f3b7b-153">設定自動調整設定</span><span class="sxs-lookup"><span data-stu-id="f3b7b-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
