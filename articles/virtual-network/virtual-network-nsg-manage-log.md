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
# <a name="log-analytics-for-network-security-groups-nsgs"></a>網路安全性群組 (NSG) 的記錄檔分析

您可以啟用下列診斷記錄檔分類的 Nsg hello:

* **事件：**包含哪些 nsg 規則會套用的 tooVMs 和 MAC 位址為基礎的執行個體角色的項目。 hello 狀態，這些規則會收集每隔 60 秒。
* **規則計數器：**包含項目多少次每個 NSG 規則會套用的 toodeny 或允許流量。

> [!NOTE]
> 診斷記錄檔只可供透過 hello Azure Resource Manager 部署模型所部署的 Nsg。 您無法啟用診斷記錄的 Nsg 透過 hello 傳統部署模型部署。 進一步了解的 hello 兩個模型，參考 hello[了解 Azure 部署模型](../resource-manager-deployment-model.md)發行項。

預設會啟用透過任何一個 Azure 部署模型所建立之 NSG 的活動記錄 (先前稱為稽核或操作的記錄檔)。 toodetermine 哪些作業已完成 Nsg hello 活動記錄檔中尋找項目包含下列資源類型的 hello: 

- Microsoft.ClassicNetwork/networkSecurityGroups 
- Microsoft.ClassicNetwork/networkSecurityGroups/securityRules
- Microsoft.Network/networkSecurityGroups
- Microsoft.Network/networkSecurityGroups/securityRules 

讀取 hello [hello Azure 活動記錄檔的概觀](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)文章 toolearn 更多關於活動記錄檔。 

## <a name="enable-diagnostic-logging"></a>啟用診斷記錄

您必須啟用診斷記錄*每個*NSG 想 toocollect 資料。 hello[概觀的 Azure 診斷記錄檔](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)篇文章說明可以傳送診斷記錄檔的位置。 如果您沒有現有的 NSG，完成 hello 步驟 hello[建立網路安全性群組](virtual-networks-create-nsg-arm-pportal.md)文章 toocreate 其中一個。 您可以啟用診斷記錄使用任何下列方法 hello NSG:

### <a name="azure-portal"></a>Azure 入口網站

toouse hello 入口 tooenable 記錄，登入 toohello[入口網站](https://portal.azure.com)。 按一下 [更多服務]，然後輸入網路安全性群組。 選取您想要記錄的 tooenable NSG hello。 遵循非計算中的資源 hello hello 指示[啟用 hello 入口網站中的診斷記錄檔](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)發行項。 選取 **NetworkSecurityGroupEvent**、**NetworkSecurityGroupRuleCounter**，或兩種類別的記錄檔。

### <a name="powershell"></a>PowerShell

記錄、 toouse PowerShell tooenable 遵循 hello hello 指示[啟用診斷記錄檔，透過 PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)發行項。 評估 hello 下列資訊，才能從 hello 文件中輸入命令：

- 您可以判斷 hello 的 hello 值 toouse`-ResourceId`參數取代 hello 遵循 [文字]，視需要，然後輸入 hello 命令`Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`。 hello 識別碼 hello 命令輸出看起來太*/subscriptions/ [訂用帳戶 Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*。
- 如果您只想 toocollect 資料從記錄檔分類加入`-Categories [category]`toohello hello 文件，其中類別目錄為中的 hello 命令結尾*NetworkSecurityGroupEvent*或*NetworkSecurityGroupRuleCounter*. 如果您不使用 hello`-Categories`參數，資料收集已啟用記錄類別目錄。

### <a name="azure-command-line-interface-cli"></a>Azure 命令列介面 (CLI)

toouse hello CLI tooenable 記錄，請遵循 hello 中的 hello 指示[啟用診斷記錄檔，透過 CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)發行項。 評估 hello 下列資訊，才能從 hello 文件中輸入命令：

- 您可以判斷 hello 的 hello 值 toouse`-ResourceId`參數取代 hello 遵循 [文字]，視需要，然後輸入 hello 命令`azure network nsg show [resource-group-name] [nsg-name]`。 hello 識別碼 hello 命令輸出看起來太*/subscriptions/ [訂用帳戶 Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*。
- 如果您只想 toocollect 資料從記錄檔分類加入`-Categories [category]`toohello hello 文件，其中類別目錄為中的 hello 命令結尾*NetworkSecurityGroupEvent*或*NetworkSecurityGroupRuleCounter*. 如果您不使用 hello`-Categories`參數，資料收集已啟用記錄類別目錄。

## <a name="logged-data"></a>記錄的資料

兩個記錄皆會以 JSON 格式資料寫入。 hello 特定資料寫入每個記錄類型會列於下列各節的 hello:

### <a name="event-log"></a>事件記錄檔
此記錄包含有關哪些 NSG 規則會套用的 tooVMs 和雲端服務角色執行個體，根據 MAC 位址的資訊。 下列範例資料的 hello 會記錄每個事件：

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

### <a name="rule-counter-log"></a>規則計數器記錄檔

此記錄檔包含每個規則套用 tooresources 相關資訊。 hello 下列的範例資料會記錄每次套用規則時：

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

## <a name="view-and-analyze-logs"></a>檢視及分析記錄檔

toolearn tooview 活動記錄資料，如何讀取 hello [hello Azure 活動記錄檔的概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)發行項。 toolearn tooview 診斷記錄資料，如何讀取 hello[概觀的 Azure 診斷記錄檔](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)發行項。 如果您傳送診斷資料 tooLog 分析，您可以使用 hello [Azure 網路安全性群組分析](../log-analytics/log-analytics-azure-networking-analytics.md)增強 insights （預覽版） 管理解決方案。 
