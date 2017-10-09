---
title: "aaaVertically 向 Azure 虛擬機器規模集 |Microsoft 文件"
description: "Toovertically 如何回應 toomonitoring 警示與 Azure 自動化中調整虛擬機器"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a>使用虛擬機器擴展集垂直自動調整
本文說明如何 toovertically 調整 Azure[虛擬機器擴展集](https://azure.microsoft.com/services/virtual-machine-scale-sets/)不論是否重新佈建。 不在擴展集 Vm 的垂直調整，請參閱太[垂直調整 Azure 虛擬機器與 Azure 自動化](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

垂直縮放比例，也稱為*向上延展*和*向下調整*，增加或減少回應 tooa 工作負載中的虛擬機器 (VM) 大小的方式。 比較此[水平延展](virtual-machine-scale-sets-autoscale-overview.md)，也稱為 tooas*向外延展*和*縮放*其中更改 hello Vm 數目視 hello 工作負載而定。

重新佈建表示移除現有的 VM，並以新的 VM 取代它。 當您增加或減少中虛擬機器擴展集 Vm 的 hello 大小時，在某些情況下您想 tooresize 現有的 Vm 並保留您的資料，而在其他情況下，您需要 toodeploy hello 新大小的新 Vm。 本文件涵蓋這兩種情況。

在下列情況下，垂直調整可能十分有用︰

* 內建在虛擬機器上的服務使用量過低 (例如在週末)。 減少 hello VM 大小可以降低每月成本。
* 增加而不需要建立其他 Vm 的 VM 大小 toocope 以較大的要求。

您可以設定垂直縮放比例 toobe 觸發根據從您的 虛擬機器擴展集的度量根據警示。 Hello 警示啟動時引發的 webhook runbook 可以調整您的標尺以便設定向上或向下該觸發程序。 您可以依照下列步驟來設定垂直調整︰

1. 使用執行身分功能來建立 Azure 自動化帳戶。
2. 將 VM 擴展集的 Azure 自動化垂直調整大小 Runbook 匯入訂用帳戶
3. 加入 webhook tooyour runbook。
4. 新增虛擬機器擴展集使用 webhook 通知警示 tooyour。

> [!NOTE]
> 垂直自動調整只能在特定範圍的 VM 大小內進行。 然後再決定從一個 tooanother tooscale 比較 hello 規格的每個的大小 （高的數字並不一定代表較大的 VM 大小）。 您可以選擇 tooscale 之間 hello 遵循組的大小：
> 
> | 成對的調整 VM 大小 |  |
> | --- | --- |
> | Standard_A0 |Standard_A11 |
> | 標準_D1 |標準_D14 |
> | Standard_DS1 |Standard_DS14 |
> | Standard_D1v2 |Standard_D15v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a>使用執行身分功能來建立 Azure 自動化帳戶
您需要 toodo hello 第一件事是建立 Azure 自動化帳戶將裝載 hello runbook 使用 tooscale hello VM 規模調整集合執行個體。 最近[Azure 自動化](https://azure.microsoft.com/services/automation/)導入了 hello 「 執行身分帳戶 」 功能會自動執行 hello runbook 上代表使用者很容易讓 hello 服務主體的設定。 閱讀更多關於此 hello 的下列文件中：

* [使用 Azure 執行身分帳戶驗證 Runbook](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>將 Azure 自動化垂直調整大小 Runbook 匯入訂用帳戶
hello runbook 需要 toovertically hello Azure 自動化 Runbook 資源庫中已發行您的 VM 規模集的小數位數。 這篇文章中的步驟 tooimport 到您的訂用帳戶遵循 hello:

* [Azure 自動化的 Runbook 和模組資源庫](../automation/automation-runbook-gallery.md)

從 hello Runbook 功能表中選擇 hello 瀏覽圖庫選項：

![匯入的 Runbook toobe][runbooks]

會顯示 hello 需要 toobe 匯入的 runbook。 選取 根據您是否要垂直縮放比例重新佈建含 hello runbook:

![Runbook 資源庫][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a>加入 webhook tooyour runbook
您已匯入 hello runbook 之後您將需要 tooadd webhook toohello runbook，如此可藉由從虛擬機器擴展集警示。 這篇文章描述 hello 的 webhook 建立您的 Runbook 的詳細資料：

* [Azure 自動化 Webhook](../automation/automation-webhooks.md)

> [!NOTE]
> 請確定您複製之後才關閉 hello webhook 對話方塊，將會需要這個 hello 下一節中的 hello webhook URI。
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a>新增虛擬機器擴展集警示 tooyour
以下是 PowerShell 指令碼會顯示如何 tooadd 警示 tooa VM 規模調整集合。 Toohello 遵循 hello 度量 toofire hello 警示文章 tooget hello 名稱上，請參閱： [Azure 監視自動調整常見標準](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)。

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> 它會建議 tooconfigure 合理的時間視窗 hello 警示順序 tooavoid 觸發垂直縮放比例，以及任何相關聯的服務中斷，太過頻繁。 請考慮至少 20-30 分鐘以上的時段。 請考慮水平縮放比例，如果您需要 tooavoid 中斷任何項目。
> 
> 

如需有關如何 toocreate 警示，請參閱下列文章 toohello 的詳細資訊：

* [Azure 監視器 PowerShell 快速入門範例](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [Azure 監視器跨平台 CLI 快速入門範例](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a>摘要
這篇文章示範簡單的垂直調整範例。 藉助這些建置組塊 (自動化帳戶、Runbook、Webhook、警示)，您可以連接各式各樣的事件與一組自訂的動作。

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
