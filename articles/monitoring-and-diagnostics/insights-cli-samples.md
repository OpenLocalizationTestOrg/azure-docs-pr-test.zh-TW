---
title: "Azure 監視器 CLI 1.0 快速入門範例。 | Microsoft Docs"
description: "Azure 監視器功能的範例 CLI 1.0 命令。 Azure 監視器是一項 Microsoft Azure 服務，可讓您根據設定的遙測資料值、自動調整雲端服務、虛擬機器和 Web Apps，傳送警示通知或呼叫 Web URL。"
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
ms.openlocfilehash: ec4512500dc3c77a40d2ebd1e6b460d5bb005811
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="07b7f-105">Azure 監視器跨平台 CLI 1.0 快速入門範例</span><span class="sxs-lookup"><span data-stu-id="07b7f-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="07b7f-106">本文說明可協助您存取 Azure 監視器 功能的命令列介面 (CLI) 命令範例。</span><span class="sxs-lookup"><span data-stu-id="07b7f-106">This article shows you sample command-line interface (CLI) commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="07b7f-107">Azure 監視器可讓您根據設定的遙測資料值、自動調整雲端服務、虛擬機器和 Web Apps，以及傳送警示通知，或呼叫 Web URL。</span><span class="sxs-lookup"><span data-stu-id="07b7f-107">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="07b7f-108">自 2016 年 9 月 25 日起，「Azure 監視器」是以前所謂「Azure Insights」的新名稱。</span><span class="sxs-lookup"><span data-stu-id="07b7f-108">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="07b7f-109">不過，命名空間和下列命令中仍有 "insights"。</span><span class="sxs-lookup"><span data-stu-id="07b7f-109">However, the namespaces and thus the commands below still contain the "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="07b7f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="07b7f-110">Prerequisites</span></span>
<span data-ttu-id="07b7f-111">如果您尚未安裝 Azure CLI，請參閱 [安裝 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="07b7f-111">If you haven't already installed the Azure CLI, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="07b7f-112">若您不熟悉 Azure CLI，可閱讀 [搭配使用 Mac、Linux 和 Windows 適用的 Azure CLI 與 Azure Resource Manager](../xplat-cli-azure-resource-manager.md)以深入了解。</span><span class="sxs-lookup"><span data-stu-id="07b7f-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="07b7f-113">在 Windows 中，從 [Node.js 網站](https://nodejs.org/)安裝 npm。</span><span class="sxs-lookup"><span data-stu-id="07b7f-113">In Windows, install npm from the [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="07b7f-114">以「以系統管理員身分執行」權限使用 CMD.exe 完成安裝後，從安裝 npm 的資料夾中執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="07b7f-114">After you complete the installation, using CMD.exe with Run As Administrator privileges, execute the following from the folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="07b7f-115">接下來，瀏覽至您想要的資料夾/位置，在命令列輸入︰</span><span class="sxs-lookup"><span data-stu-id="07b7f-115">Next, navigate to any folder/location you want and type at the command-line:</span></span>

```console
azure help
```

## <a name="log-in-to-azure"></a><span data-ttu-id="07b7f-116">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="07b7f-116">Log in to Azure</span></span>
<span data-ttu-id="07b7f-117">第一步是登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="07b7f-117">The first step is to login to your Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="07b7f-118">執行此命令之後，您必須透過螢幕上的指示來登入。</span><span class="sxs-lookup"><span data-stu-id="07b7f-118">After running this command, you have to sign in via the instructions on the screen.</span></span> <span data-ttu-id="07b7f-119">之後，您會看到您的帳戶、TenantId 和預設的訂用帳戶識別碼。所有命令都會在您的預設訂用帳戶內容中運作。</span><span class="sxs-lookup"><span data-stu-id="07b7f-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in the context of your default subscription.</span></span>

<span data-ttu-id="07b7f-120">若要列出目前訂用帳戶的詳細資料，使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="07b7f-120">To list the details of your current subscription, use the following command.</span></span>

```console
azure account show
```

<span data-ttu-id="07b7f-121">若要將使用中的內容變更為其他訂用帳戶，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="07b7f-121">To change working context to a different subscription, use the following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="07b7f-122">若要使用 Azure Resource Manager 和 Azure 監視器命令，您必須處於 Azure Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="07b7f-122">To use Azure Resource Manager and Azure Monitor commands, you need to be in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="07b7f-123">若要檢視所有支援的 Azure 監視器命令清單，執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="07b7f-123">To view a list of all supported Azure Monitor commands, perform the following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="07b7f-124">檢視訂用帳戶的活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="07b7f-124">View activity log for a subscription</span></span>
<span data-ttu-id="07b7f-125">若要檢視活動記錄檔事件的清單，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="07b7f-125">To view a list of activity log events, perform the following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="07b7f-126">嘗試下列命令以檢視所有可用的選項。</span><span class="sxs-lookup"><span data-stu-id="07b7f-126">Try the following to view all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="07b7f-127">以下是依 resourceGroup 列出記錄檔清單的範例</span><span class="sxs-lookup"><span data-stu-id="07b7f-127">Here is an example to list logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="07b7f-128">依 caller 列出記錄檔的範例</span><span class="sxs-lookup"><span data-stu-id="07b7f-128">Example to list logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="07b7f-129">依 caller 列出開始與結束日期之間在資源類型上的記錄檔的範例</span><span class="sxs-lookup"><span data-stu-id="07b7f-129">Example to list logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="07b7f-130">使用警示</span><span class="sxs-lookup"><span data-stu-id="07b7f-130">Work with alerts</span></span>
<span data-ttu-id="07b7f-131">您可以在此區段中運用資訊來使用警示。</span><span class="sxs-lookup"><span data-stu-id="07b7f-131">You can use the information in the section to work with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="07b7f-132">取得資源群組中的警示規則</span><span class="sxs-lookup"><span data-stu-id="07b7f-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="07b7f-133">建立度量警示規則</span><span class="sxs-lookup"><span data-stu-id="07b7f-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="07b7f-134">建立 WebTest 警示規則</span><span class="sxs-lookup"><span data-stu-id="07b7f-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="07b7f-135">刪除警示規則</span><span class="sxs-lookup"><span data-stu-id="07b7f-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="07b7f-136">記錄檔的設定檔</span><span class="sxs-lookup"><span data-stu-id="07b7f-136">Log profiles</span></span>
<span data-ttu-id="07b7f-137">在此區段中運用資訊來使用記錄檔的設定檔。</span><span class="sxs-lookup"><span data-stu-id="07b7f-137">Use the information in this section to work with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="07b7f-138">取得記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="07b7f-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="07b7f-139">新增沒有保留期的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="07b7f-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="07b7f-140">移除記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="07b7f-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="07b7f-141">新增有保留期的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="07b7f-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="07b7f-142">新增有保留期與 EventHub 的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="07b7f-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="07b7f-143">診斷</span><span class="sxs-lookup"><span data-stu-id="07b7f-143">Diagnostics</span></span>
<span data-ttu-id="07b7f-144">在此區段中運用資訊來使用診斷設定。</span><span class="sxs-lookup"><span data-stu-id="07b7f-144">Use the information in this section to work with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="07b7f-145">取得診斷設定</span><span class="sxs-lookup"><span data-stu-id="07b7f-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="07b7f-146">停用診斷設定</span><span class="sxs-lookup"><span data-stu-id="07b7f-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="07b7f-147">啟用沒有保留期的診斷設定</span><span class="sxs-lookup"><span data-stu-id="07b7f-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="07b7f-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="07b7f-148">Autoscale</span></span>
<span data-ttu-id="07b7f-149">利用此區段中的資訊來使用自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="07b7f-149">Use the information in this section to work with autoscale settings.</span></span> <span data-ttu-id="07b7f-150">您必須修改這些範例。</span><span class="sxs-lookup"><span data-stu-id="07b7f-150">You need to modify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="07b7f-151">取得資源群組的自動調整設定</span><span class="sxs-lookup"><span data-stu-id="07b7f-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="07b7f-152">依名稱取得資源群組中的自動調整設定</span><span class="sxs-lookup"><span data-stu-id="07b7f-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="07b7f-153">設定自動調整設定</span><span class="sxs-lookup"><span data-stu-id="07b7f-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
