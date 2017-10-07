---
title: "aaaMonitor 作業、 事件和計數器 Nsg |Microsoft 文件"
description: "深入了解如何 tooenable 計數器、 事件和操作記錄 Nsg"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="9fc05-103">網路安全性群組 (NSG) 的記錄檔分析</span><span class="sxs-lookup"><span data-stu-id="9fc05-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="9fc05-104">您可以啟用下列診斷記錄檔分類的 Nsg hello:</span><span class="sxs-lookup"><span data-stu-id="9fc05-104">You can enable hello following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="9fc05-105">**事件：**包含哪些 nsg 規則會套用的 tooVMs 和 MAC 位址為基礎的執行個體角色的項目。</span><span class="sxs-lookup"><span data-stu-id="9fc05-105">**Event:** Contains entries for which NSG rules are applied tooVMs and instance roles based on MAC address.</span></span> <span data-ttu-id="9fc05-106">hello 狀態，這些規則會收集每隔 60 秒。</span><span class="sxs-lookup"><span data-stu-id="9fc05-106">hello status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="9fc05-107">**規則計數器：**包含項目多少次每個 NSG 規則會套用的 toodeny 或允許流量。</span><span class="sxs-lookup"><span data-stu-id="9fc05-107">**Rule counter:** Contains entries for how many times each NSG rule is applied toodeny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="9fc05-108">診斷記錄檔只可供透過 hello Azure Resource Manager 部署模型所部署的 Nsg。</span><span class="sxs-lookup"><span data-stu-id="9fc05-108">Diagnostic logs are only available for NSGs deployed through hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="9fc05-109">您無法啟用診斷記錄的 Nsg 透過 hello 傳統部署模型部署。</span><span class="sxs-lookup"><span data-stu-id="9fc05-109">You cannot enable diagnostic logging for NSGs deployed through hello classic deployment model.</span></span> <span data-ttu-id="9fc05-110">進一步了解的 hello 兩個模型，參考 hello[了解 Azure 部署模型](../resource-manager-deployment-model.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="9fc05-110">For a better understanding of hello two models, reference hello [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="9fc05-111">預設會啟用透過任何一個 Azure 部署模型所建立之 NSG 的活動記錄 (先前稱為稽核或操作的記錄檔)。</span><span class="sxs-lookup"><span data-stu-id="9fc05-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="9fc05-112">toodetermine 哪些作業已完成 Nsg hello 活動記錄檔中尋找項目包含下列資源類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="9fc05-112">toodetermine which operations were completed on NSGs in hello activity log, look for entries that contain hello following resource types:</span></span> 

- <span data-ttu-id="9fc05-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="9fc05-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="9fc05-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="9fc05-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="9fc05-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="9fc05-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="9fc05-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="9fc05-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="9fc05-117">讀取 hello [hello Azure 活動記錄檔的概觀](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)文章 toolearn 更多關於活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9fc05-117">Read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article toolearn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="9fc05-118">啟用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="9fc05-118">Enable diagnostic logging</span></span>

<span data-ttu-id="9fc05-119">您必須啟用診斷記錄*每個*NSG 想 toocollect 資料。</span><span class="sxs-lookup"><span data-stu-id="9fc05-119">Diagnostic logging must be enabled for *each* NSG you want toocollect data for.</span></span> <span data-ttu-id="9fc05-120">hello[概觀的 Azure 診斷記錄檔](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)篇文章說明可以傳送診斷記錄檔的位置。</span><span class="sxs-lookup"><span data-stu-id="9fc05-120">hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="9fc05-121">如果您沒有現有的 NSG，完成 hello 步驟 hello[建立網路安全性群組](virtual-networks-create-nsg-arm-pportal.md)文章 toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="9fc05-121">If you don't have an existing NSG, complete hello steps in hello [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article toocreate one.</span></span> <span data-ttu-id="9fc05-122">您可以啟用診斷記錄使用任何下列方法 hello NSG:</span><span class="sxs-lookup"><span data-stu-id="9fc05-122">You can enable NSG diagnostic logging using any of hello following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="9fc05-123">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9fc05-123">Azure portal</span></span>

<span data-ttu-id="9fc05-124">toouse hello 入口 tooenable 記錄，登入 toohello[入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9fc05-124">toouse hello portal tooenable logging, login toohello [portal](https://portal.azure.com).</span></span> <span data-ttu-id="9fc05-125">按一下 [更多服務]，然後輸入網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="9fc05-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="9fc05-126">選取您想要記錄的 tooenable NSG hello。</span><span class="sxs-lookup"><span data-stu-id="9fc05-126">Select hello NSG you want tooenable logging for.</span></span> <span data-ttu-id="9fc05-127">遵循非計算中的資源 hello hello 指示[啟用 hello 入口網站中的診斷記錄檔](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)發行項。</span><span class="sxs-lookup"><span data-stu-id="9fc05-127">Follow hello instructions for non-compute resources in hello [Enable diagnostic logs in hello portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="9fc05-128">選取 **NetworkSecurityGroupEvent**、**NetworkSecurityGroupRuleCounter**，或兩種類別的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9fc05-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="9fc05-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fc05-129">PowerShell</span></span>

<span data-ttu-id="9fc05-130">記錄、 toouse PowerShell tooenable 遵循 hello hello 指示[啟用診斷記錄檔，透過 PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)發行項。</span><span class="sxs-lookup"><span data-stu-id="9fc05-130">toouse PowerShell tooenable logging, follow hello instructions in hello [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="9fc05-131">評估 hello 下列資訊，才能從 hello 文件中輸入命令：</span><span class="sxs-lookup"><span data-stu-id="9fc05-131">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="9fc05-132">您可以判斷 hello 的 hello 值 toouse`-ResourceId`參數取代 hello 遵循 [文字]，視需要，然後輸入 hello 命令`Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`。</span><span class="sxs-lookup"><span data-stu-id="9fc05-132">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="9fc05-133">hello 識別碼 hello 命令輸出看起來太*/subscriptions/ [訂用帳戶 Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*。</span><span class="sxs-lookup"><span data-stu-id="9fc05-133">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="9fc05-134">如果您只想 toocollect 資料從記錄檔分類加入`-Categories [category]`toohello hello 文件，其中類別目錄為中的 hello 命令結尾*NetworkSecurityGroupEvent*或*NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="9fc05-134">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="9fc05-135">如果您不使用 hello`-Categories`參數，資料收集已啟用記錄類別目錄。</span><span class="sxs-lookup"><span data-stu-id="9fc05-135">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="9fc05-136">Azure 命令列介面 (CLI)</span><span class="sxs-lookup"><span data-stu-id="9fc05-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="9fc05-137">toouse hello CLI tooenable 記錄，請遵循 hello 中的 hello 指示[啟用診斷記錄檔，透過 CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)發行項。</span><span class="sxs-lookup"><span data-stu-id="9fc05-137">toouse hello CLI tooenable logging, follow hello instructions in hello [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="9fc05-138">評估 hello 下列資訊，才能從 hello 文件中輸入命令：</span><span class="sxs-lookup"><span data-stu-id="9fc05-138">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="9fc05-139">您可以判斷 hello 的 hello 值 toouse`-ResourceId`參數取代 hello 遵循 [文字]，視需要，然後輸入 hello 命令`azure network nsg show [resource-group-name] [nsg-name]`。</span><span class="sxs-lookup"><span data-stu-id="9fc05-139">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="9fc05-140">hello 識別碼 hello 命令輸出看起來太*/subscriptions/ [訂用帳戶 Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*。</span><span class="sxs-lookup"><span data-stu-id="9fc05-140">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="9fc05-141">如果您只想 toocollect 資料從記錄檔分類加入`-Categories [category]`toohello hello 文件，其中類別目錄為中的 hello 命令結尾*NetworkSecurityGroupEvent*或*NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="9fc05-141">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="9fc05-142">如果您不使用 hello`-Categories`參數，資料收集已啟用記錄類別目錄。</span><span class="sxs-lookup"><span data-stu-id="9fc05-142">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="9fc05-143">記錄的資料</span><span class="sxs-lookup"><span data-stu-id="9fc05-143">Logged data</span></span>

<span data-ttu-id="9fc05-144">兩個記錄皆會以 JSON 格式資料寫入。</span><span class="sxs-lookup"><span data-stu-id="9fc05-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="9fc05-145">hello 特定資料寫入每個記錄類型會列於下列各節的 hello:</span><span class="sxs-lookup"><span data-stu-id="9fc05-145">hello specific data written for each log type is listed in hello following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="9fc05-146">事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="9fc05-146">Event log</span></span>
<span data-ttu-id="9fc05-147">此記錄包含有關哪些 NSG 規則會套用的 tooVMs 和雲端服務角色執行個體，根據 MAC 位址的資訊。</span><span class="sxs-lookup"><span data-stu-id="9fc05-147">This log contains information about which NSG rules are applied tooVMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="9fc05-148">下列範例資料的 hello 會記錄每個事件：</span><span class="sxs-lookup"><span data-stu-id="9fc05-148">hello following example data is logged for each event:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a><span data-ttu-id="9fc05-149">規則計數器記錄檔</span><span class="sxs-lookup"><span data-stu-id="9fc05-149">Rule counter log</span></span>

<span data-ttu-id="9fc05-150">此記錄檔包含每個規則套用 tooresources 相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9fc05-150">This log contains information about each rule applied tooresources.</span></span> <span data-ttu-id="9fc05-151">hello 下列的範例資料會記錄每次套用規則時：</span><span class="sxs-lookup"><span data-stu-id="9fc05-151">hello following example data is logged each time a rule is applied:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a><span data-ttu-id="9fc05-152">檢視及分析記錄檔</span><span class="sxs-lookup"><span data-stu-id="9fc05-152">View and analyze logs</span></span>

<span data-ttu-id="9fc05-153">toolearn tooview 活動記錄資料，如何讀取 hello [hello Azure 活動記錄檔的概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="9fc05-153">toolearn how tooview activity log data, read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="9fc05-154">toolearn tooview 診斷記錄資料，如何讀取 hello[概觀的 Azure 診斷記錄檔](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="9fc05-154">toolearn how tooview diagnostic log data, read hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="9fc05-155">如果您傳送診斷資料 tooLog 分析，您可以使用 hello [Azure 網路安全性群組分析](../log-analytics/log-analytics-azure-networking-analytics.md)增強 insights （預覽版） 管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="9fc05-155">If you send diagnostics data tooLog Analytics, you can use hello [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
