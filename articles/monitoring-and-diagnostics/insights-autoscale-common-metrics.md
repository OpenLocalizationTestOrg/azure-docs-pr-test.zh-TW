---
title: "Azure 監視器自動調整的常用度量 | Microsoft Docs"
description: "了解哪些度量常用於自動調整您的雲端服務、虛擬機器和 Web Apps。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 189b2a13-01c8-4aca-afd5-90711903ca59
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/6/2016
ms.author: ancav
ms.openlocfilehash: 240a230d09680672ccd5316470a87d047fab9fd1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a><span data-ttu-id="50403-103">Azure 監視器自動調整的常用度量</span><span class="sxs-lookup"><span data-stu-id="50403-103">Azure Monitor autoscaling common metrics</span></span>
<span data-ttu-id="50403-104">Azure 監視器的自動調整可讓您根據遙測資料 (度量) 增加或減少執行中執行個體的數目。</span><span class="sxs-lookup"><span data-stu-id="50403-104">Azure Monitor autoscaling allows you to scale the number of running instances up or down, based on telemetry data (metrics).</span></span> <span data-ttu-id="50403-105">本文件說明您可能會使用的常用度量。</span><span class="sxs-lookup"><span data-stu-id="50403-105">This document describes common metrics that you might want to use.</span></span> <span data-ttu-id="50403-106">在 Azure 的雲端服務和伺服器陣列入口網站中，您可以選擇要作為調整依據的資源度量。</span><span class="sxs-lookup"><span data-stu-id="50403-106">In the Azure portal  for Cloud Services and Server Farms, you can choose the metric of the resource to scale by.</span></span> <span data-ttu-id="50403-107">不過，您也可以選擇其他資源的任何度量來做為調整依據。</span><span class="sxs-lookup"><span data-stu-id="50403-107">However, you can also choose any metric from a different resource to scale by.</span></span>

<span data-ttu-id="50403-108">Azure 監視器自動調整僅適用於[虛擬機器擴展集](https://azure.microsoft.com/services/virtual-machine-scale-sets/)、[雲端服務](https://azure.microsoft.com/services/cloud-services/)和 [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="50403-108">Azure Monitor autoscale applies only to [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="50403-109">其他 Azure 服務使用不同的調整方法。</span><span class="sxs-lookup"><span data-stu-id="50403-109">Other Azure services use different scaling methods.</span></span>

## <a name="compute-metrics-for-resource-manager-based-vms"></a><span data-ttu-id="50403-110">針對以 Resource Manager 為基礎的 VM 來計算度量</span><span class="sxs-lookup"><span data-stu-id="50403-110">Compute metrics for Resource Manager-based VMs</span></span>
<span data-ttu-id="50403-111">根據預設，以 Resource Manager 為基礎的虛擬機器和虛擬機器擴展集會發出基本 (主機層級) 的度量。</span><span class="sxs-lookup"><span data-stu-id="50403-111">By default, Resource Manager-based Virtual Machines and Virtual Machine Scale Sets emit basic (host-level) metrics.</span></span> <span data-ttu-id="50403-112">此外，當您設定 Azure VM 和 VMSS 的診斷資料收集時，Azure 診斷擴充也會發出客體 OS 效能計數器 (通常稱為「客體 OS 度量」)。</span><span class="sxs-lookup"><span data-stu-id="50403-112">In addition, when you configure diagnostics data collection for an Azure VM and VMSS,  the Azure diagnostic extension also emits guest-OS performance counters (commonly known as "guest-OS metrics").</span></span>  <span data-ttu-id="50403-113">您在自動調整規則中使用所有這些度量。</span><span class="sxs-lookup"><span data-stu-id="50403-113">You use all these metrics in autoscale rules.</span></span>

<span data-ttu-id="50403-114">您可以使用 `Get MetricDefinitions` API/PoSH/CLI 來檢視 VMSS 資源的可用度量。</span><span class="sxs-lookup"><span data-stu-id="50403-114">You can use the `Get MetricDefinitions` API/PoSH/CLI to view the metrics available for your VMSS resource.</span></span>

<span data-ttu-id="50403-115">如果您使用 VM 擴展集，而且發現特定度量沒有列出來，可能是您的診斷擴充功能已「停用」它。</span><span class="sxs-lookup"><span data-stu-id="50403-115">If you're using VM scale sets and you don't see a particular metric listed, then it is likely *disabled* in your diagnostics extension.</span></span>

<span data-ttu-id="50403-116">如果特定度量沒有取樣或以您想要的頻率傳輸，您可以更新診斷的組態設定。</span><span class="sxs-lookup"><span data-stu-id="50403-116">If a particular metric is not being sampled or transferred at the frequency you want, you can update the diagnostics configuration.</span></span>

<span data-ttu-id="50403-117">如果發生上述任一種情況，請檢閱 PowerShell 相關的[使用 PowerShell 在執行 Windows 的虛擬機器中啟用 Azure 診斷](../virtual-machines/windows/ps-extensions-diagnostics.md)，設定和更新 Azure VM 診斷擴充以啟用該度量。</span><span class="sxs-lookup"><span data-stu-id="50403-117">If either preceding case is true, then review [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md) about PowerShell to configure and update your Azure VM Diagnostics extension to enable the metric.</span></span> <span data-ttu-id="50403-118">該文章也包含診斷組態檔的範例。</span><span class="sxs-lookup"><span data-stu-id="50403-118">That article also includes a sample diagnostics configuration file.</span></span>

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a><span data-ttu-id="50403-119">以 Resource Manager 為基礎的 Windows 和 Linux VM 的主機度量</span><span class="sxs-lookup"><span data-stu-id="50403-119">Host metrics for Resource Manager-based Windows and Linux VMs</span></span>
<span data-ttu-id="50403-120">在 Windows 和 Linux 執行個體中，根據預設會針對 Azure VM 和 VMSS 發出下列的主機層級度量。</span><span class="sxs-lookup"><span data-stu-id="50403-120">The following host-level metrics are emitted by default for Azure VM and VMSS in both Windows and Linux instances.</span></span> <span data-ttu-id="50403-121">這些度量描述您的 Azure VM，然而是從 Azure VM 主機收集，而不是透過客體 VM 上安裝的代理程式收集。</span><span class="sxs-lookup"><span data-stu-id="50403-121">These metrics describe your Azure VM, but are collected from the Azure VM host rather than via agent installed on the guest VM.</span></span> <span data-ttu-id="50403-122">您可以在自動調整規則中使用這些度量。</span><span class="sxs-lookup"><span data-stu-id="50403-122">You may use these metrics in autoscaling rules.</span></span>

- [<span data-ttu-id="50403-123">以 Resource Manager 為基礎的 Windows 和 Linux VM 的主機度量</span><span class="sxs-lookup"><span data-stu-id="50403-123">Host metrics for Resource Manager-based Windows and Linux VMs</span></span>](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [<span data-ttu-id="50403-124">以 Resource Manager 為基礎的 Windows 和 Linux VM 擴展集的主機度量</span><span class="sxs-lookup"><span data-stu-id="50403-124">Host metrics for Resource Manager-based Windows and Linux VM Scale Sets</span></span>](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a><span data-ttu-id="50403-125">客體 OS 度量以 Resource Manager 為基礎的 Windows VM</span><span class="sxs-lookup"><span data-stu-id="50403-125">Guest OS metrics Resource Manager-based Windows VMs</span></span>
<span data-ttu-id="50403-126">在 Azure 中建立 VM 時會使用診斷擴充來啟用診斷。</span><span class="sxs-lookup"><span data-stu-id="50403-126">When you create a VM in Azure, diagnostics is enabled by using the Diagnostics extension.</span></span> <span data-ttu-id="50403-127">診斷擴充會發出一組取自 VM 內的度量。</span><span class="sxs-lookup"><span data-stu-id="50403-127">The diagnostics extension emits a set of metrics taken from inside of the VM.</span></span> <span data-ttu-id="50403-128">這表示您可以關閉自動調整依預設不發出的度量。</span><span class="sxs-lookup"><span data-stu-id="50403-128">This means you can autoscale off of metrics that are not emitted by default.</span></span>

<span data-ttu-id="50403-129">您可以在 PowerShell 中使用下列命令產生度量清單。</span><span class="sxs-lookup"><span data-stu-id="50403-129">You can generate a list of the metrics by using the following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="50403-130">您可以建立下列度量的警示：</span><span class="sxs-lookup"><span data-stu-id="50403-130">You can create an alert for the following metrics:</span></span>

| <span data-ttu-id="50403-131">度量名稱</span><span class="sxs-lookup"><span data-stu-id="50403-131">Metric Name</span></span> | <span data-ttu-id="50403-132">單位</span><span class="sxs-lookup"><span data-stu-id="50403-132">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="50403-133">\Processor(_Total)\% Processor Time</span><span class="sxs-lookup"><span data-stu-id="50403-133">\Processor(_Total)\% Processor Time</span></span> |<span data-ttu-id="50403-134">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-134">Percent</span></span> |
| <span data-ttu-id="50403-135">\Processor(_Total)\% Privileged Time</span><span class="sxs-lookup"><span data-stu-id="50403-135">\Processor(_Total)\% Privileged Time</span></span> |<span data-ttu-id="50403-136">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-136">Percent</span></span> |
| <span data-ttu-id="50403-137">\Processor(_Total)\% User Time</span><span class="sxs-lookup"><span data-stu-id="50403-137">\Processor(_Total)\% User Time</span></span> |<span data-ttu-id="50403-138">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-138">Percent</span></span> |
| <span data-ttu-id="50403-139">\Processor Information(_Total)\Processor Frequency</span><span class="sxs-lookup"><span data-stu-id="50403-139">\Processor Information(_Total)\Processor Frequency</span></span> |<span data-ttu-id="50403-140">Count</span><span class="sxs-lookup"><span data-stu-id="50403-140">Count</span></span> |
| <span data-ttu-id="50403-141">\System\Processes</span><span class="sxs-lookup"><span data-stu-id="50403-141">\System\Processes</span></span> |<span data-ttu-id="50403-142">Count</span><span class="sxs-lookup"><span data-stu-id="50403-142">Count</span></span> |
| <span data-ttu-id="50403-143">\Process(_Total)\Thread Count</span><span class="sxs-lookup"><span data-stu-id="50403-143">\Process(_Total)\Thread Count</span></span> |<span data-ttu-id="50403-144">Count</span><span class="sxs-lookup"><span data-stu-id="50403-144">Count</span></span> |
| <span data-ttu-id="50403-145">\Process(_Total)\Handle Count</span><span class="sxs-lookup"><span data-stu-id="50403-145">\Process(_Total)\Handle Count</span></span> |<span data-ttu-id="50403-146">Count</span><span class="sxs-lookup"><span data-stu-id="50403-146">Count</span></span> |
| <span data-ttu-id="50403-147">\Memory\% Committed Bytes In Use</span><span class="sxs-lookup"><span data-stu-id="50403-147">\Memory\% Committed Bytes In Use</span></span> |<span data-ttu-id="50403-148">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-148">Percent</span></span> |
| <span data-ttu-id="50403-149">\Memory\Available Bytes</span><span class="sxs-lookup"><span data-stu-id="50403-149">\Memory\Available Bytes</span></span> |<span data-ttu-id="50403-150">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-150">Bytes</span></span> |
| <span data-ttu-id="50403-151">\Memory\Committed Bytes</span><span class="sxs-lookup"><span data-stu-id="50403-151">\Memory\Committed Bytes</span></span> |<span data-ttu-id="50403-152">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-152">Bytes</span></span> |
| <span data-ttu-id="50403-153">\Memory\Commit Limit</span><span class="sxs-lookup"><span data-stu-id="50403-153">\Memory\Commit Limit</span></span> |<span data-ttu-id="50403-154">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-154">Bytes</span></span> |
| <span data-ttu-id="50403-155">\Memory\Pool Paged Bytes</span><span class="sxs-lookup"><span data-stu-id="50403-155">\Memory\Pool Paged Bytes</span></span> |<span data-ttu-id="50403-156">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-156">Bytes</span></span> |
| <span data-ttu-id="50403-157">\Memory\Pool Nonpaged Bytes</span><span class="sxs-lookup"><span data-stu-id="50403-157">\Memory\Pool Nonpaged Bytes</span></span> |<span data-ttu-id="50403-158">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-158">Bytes</span></span> |
| <span data-ttu-id="50403-159">\PhysicalDisk(_Total)\% Disk Time</span><span class="sxs-lookup"><span data-stu-id="50403-159">\PhysicalDisk(_Total)\% Disk Time</span></span> |<span data-ttu-id="50403-160">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-160">Percent</span></span> |
| <span data-ttu-id="50403-161">\PhysicalDisk(_Total)\% Disk Read Time</span><span class="sxs-lookup"><span data-stu-id="50403-161">\PhysicalDisk(_Total)\% Disk Read Time</span></span> |<span data-ttu-id="50403-162">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-162">Percent</span></span> |
| <span data-ttu-id="50403-163">\PhysicalDisk(_Total)\% Disk Write Time</span><span class="sxs-lookup"><span data-stu-id="50403-163">\PhysicalDisk(_Total)\% Disk Write Time</span></span> |<span data-ttu-id="50403-164">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-164">Percent</span></span> |
| <span data-ttu-id="50403-165">\PhysicalDisk(_Total)\每秒的磁碟傳輸數</span><span class="sxs-lookup"><span data-stu-id="50403-165">\PhysicalDisk(_Total)\Disk Transfers/sec</span></span> |<span data-ttu-id="50403-166">每秒計數</span><span class="sxs-lookup"><span data-stu-id="50403-166">CountPerSecond</span></span> |
| <span data-ttu-id="50403-167">\PhysicalDisk(_Total)\Disk Reads/sec</span><span class="sxs-lookup"><span data-stu-id="50403-167">\PhysicalDisk(_Total)\Disk Reads/sec</span></span> |<span data-ttu-id="50403-168">每秒計數</span><span class="sxs-lookup"><span data-stu-id="50403-168">CountPerSecond</span></span> |
| <span data-ttu-id="50403-169">\PhysicalDisk(_Total)\Disk Writes/sec</span><span class="sxs-lookup"><span data-stu-id="50403-169">\PhysicalDisk(_Total)\Disk Writes/sec</span></span> |<span data-ttu-id="50403-170">每秒計數</span><span class="sxs-lookup"><span data-stu-id="50403-170">CountPerSecond</span></span> |
| <span data-ttu-id="50403-171">\PhysicalDisk(_Total)\Disk Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="50403-171">\PhysicalDisk(_Total)\Disk Bytes/sec</span></span> |<span data-ttu-id="50403-172">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="50403-172">BytesPerSecond</span></span> |
| <span data-ttu-id="50403-173">\PhysicalDisk(_Total)\Disk Read Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="50403-173">\PhysicalDisk(_Total)\Disk Read Bytes/sec</span></span> |<span data-ttu-id="50403-174">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="50403-174">BytesPerSecond</span></span> |
| <span data-ttu-id="50403-175">\PhysicalDisk(_Total)\Disk Write Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="50403-175">\PhysicalDisk(_Total)\Disk Write Bytes/sec</span></span> |<span data-ttu-id="50403-176">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="50403-176">BytesPerSecond</span></span> |
| <span data-ttu-id="50403-177">\PhysicalDisk(_Total)\Avg.</span><span class="sxs-lookup"><span data-stu-id="50403-177">\PhysicalDisk(_Total)\Avg.</span></span> <span data-ttu-id="50403-178">磁碟佇列長度</span><span class="sxs-lookup"><span data-stu-id="50403-178">Disk Queue Length</span></span> |<span data-ttu-id="50403-179">Count</span><span class="sxs-lookup"><span data-stu-id="50403-179">Count</span></span> |
| <span data-ttu-id="50403-180">\PhysicalDisk(_Total)\Avg.</span><span class="sxs-lookup"><span data-stu-id="50403-180">\PhysicalDisk(_Total)\Avg.</span></span> <span data-ttu-id="50403-181">磁碟讀取佇列長度</span><span class="sxs-lookup"><span data-stu-id="50403-181">Disk Read Queue Length</span></span> |<span data-ttu-id="50403-182">Count</span><span class="sxs-lookup"><span data-stu-id="50403-182">Count</span></span> |
| <span data-ttu-id="50403-183">\PhysicalDisk(_Total)\Avg.</span><span class="sxs-lookup"><span data-stu-id="50403-183">\PhysicalDisk(_Total)\Avg.</span></span> <span data-ttu-id="50403-184">磁碟寫入佇列長度</span><span class="sxs-lookup"><span data-stu-id="50403-184">Disk Write Queue Length</span></span> |<span data-ttu-id="50403-185">Count</span><span class="sxs-lookup"><span data-stu-id="50403-185">Count</span></span> |
| <span data-ttu-id="50403-186">\LogicalDisk(_Total)\% Free Space</span><span class="sxs-lookup"><span data-stu-id="50403-186">\LogicalDisk(_Total)\% Free Space</span></span> |<span data-ttu-id="50403-187">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-187">Percent</span></span> |
| <span data-ttu-id="50403-188">\LogicalDisk(_Total)\Free Megabytes</span><span class="sxs-lookup"><span data-stu-id="50403-188">\LogicalDisk(_Total)\Free Megabytes</span></span> |<span data-ttu-id="50403-189">Count</span><span class="sxs-lookup"><span data-stu-id="50403-189">Count</span></span> |

### <a name="guest-os-metrics-linux-vms"></a><span data-ttu-id="50403-190">客體 OS 度量 Linux VM</span><span class="sxs-lookup"><span data-stu-id="50403-190">Guest OS metrics Linux VMs</span></span>
<span data-ttu-id="50403-191">當您在 Azure 中建立 VM 時，根據預設會使用診斷擴充來啟用診斷。</span><span class="sxs-lookup"><span data-stu-id="50403-191">When you create a VM in Azure, diagnostics is enabled by default by using Diagnostics extension.</span></span>

<span data-ttu-id="50403-192">您可以在 PowerShell 中使用下列命令產生度量清單。</span><span class="sxs-lookup"><span data-stu-id="50403-192">You can generate a list of the metrics by using the following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 <span data-ttu-id="50403-193">您可以建立下列度量的警示：</span><span class="sxs-lookup"><span data-stu-id="50403-193">You can create an alert for the following metrics:</span></span>

| <span data-ttu-id="50403-194">度量名稱</span><span class="sxs-lookup"><span data-stu-id="50403-194">Metric Name</span></span> | <span data-ttu-id="50403-195">單位</span><span class="sxs-lookup"><span data-stu-id="50403-195">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="50403-196">\Memory\AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="50403-196">\Memory\AvailableMemory</span></span> |<span data-ttu-id="50403-197">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-197">Bytes</span></span> |
| <span data-ttu-id="50403-198">\Memory\PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="50403-198">\Memory\PercentAvailableMemory</span></span> |<span data-ttu-id="50403-199">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-199">Percent</span></span> |
| <span data-ttu-id="50403-200">\Memory\UsedMemory</span><span class="sxs-lookup"><span data-stu-id="50403-200">\Memory\UsedMemory</span></span> |<span data-ttu-id="50403-201">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-201">Bytes</span></span> |
| <span data-ttu-id="50403-202">\Memory\PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="50403-202">\Memory\PercentUsedMemory</span></span> |<span data-ttu-id="50403-203">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-203">Percent</span></span> |
| <span data-ttu-id="50403-204">\Memory\PercentUsedByCache</span><span class="sxs-lookup"><span data-stu-id="50403-204">\Memory\PercentUsedByCache</span></span> |<span data-ttu-id="50403-205">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-205">Percent</span></span> |
| <span data-ttu-id="50403-206">\Memory\PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="50403-206">\Memory\PagesPerSec</span></span> |<span data-ttu-id="50403-207">每秒計數</span><span class="sxs-lookup"><span data-stu-id="50403-207">CountPerSecond</span></span> |
| <span data-ttu-id="50403-208">\Memory\PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="50403-208">\Memory\PagesReadPerSec</span></span> |<span data-ttu-id="50403-209">每秒計數</span><span class="sxs-lookup"><span data-stu-id="50403-209">CountPerSecond</span></span> |
| <span data-ttu-id="50403-210">\Memory\PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="50403-210">\Memory\PagesWrittenPerSec</span></span> |<span data-ttu-id="50403-211">每秒計數</span><span class="sxs-lookup"><span data-stu-id="50403-211">CountPerSecond</span></span> |
| <span data-ttu-id="50403-212">\Memory\AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="50403-212">\Memory\AvailableSwap</span></span> |<span data-ttu-id="50403-213">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-213">Bytes</span></span> |
| <span data-ttu-id="50403-214">\Memory\PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="50403-214">\Memory\PercentAvailableSwap</span></span> |<span data-ttu-id="50403-215">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-215">Percent</span></span> |
| <span data-ttu-id="50403-216">\Memory\UsedSwap</span><span class="sxs-lookup"><span data-stu-id="50403-216">\Memory\UsedSwap</span></span> |<span data-ttu-id="50403-217">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-217">Bytes</span></span> |
| <span data-ttu-id="50403-218">\Memory\PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="50403-218">\Memory\PercentUsedSwap</span></span> |<span data-ttu-id="50403-219">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-219">Percent</span></span> |
| <span data-ttu-id="50403-220">\Processor\PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="50403-220">\Processor\PercentIdleTime</span></span> |<span data-ttu-id="50403-221">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-221">Percent</span></span> |
| <span data-ttu-id="50403-222">\Processor\PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="50403-222">\Processor\PercentUserTime</span></span> |<span data-ttu-id="50403-223">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-223">Percent</span></span> |
| <span data-ttu-id="50403-224">\Processor\PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="50403-224">\Processor\PercentNiceTime</span></span> |<span data-ttu-id="50403-225">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-225">Percent</span></span> |
| <span data-ttu-id="50403-226">\Processor\PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="50403-226">\Processor\PercentPrivilegedTime</span></span> |<span data-ttu-id="50403-227">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-227">Percent</span></span> |
| <span data-ttu-id="50403-228">\Processor\PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="50403-228">\Processor\PercentInterruptTime</span></span> |<span data-ttu-id="50403-229">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-229">Percent</span></span> |
| <span data-ttu-id="50403-230">\Processor\PercentDPCTime</span><span class="sxs-lookup"><span data-stu-id="50403-230">\Processor\PercentDPCTime</span></span> |<span data-ttu-id="50403-231">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-231">Percent</span></span> |
| <span data-ttu-id="50403-232">\Processor\PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="50403-232">\Processor\PercentProcessorTime</span></span> |<span data-ttu-id="50403-233">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-233">Percent</span></span> |
| <span data-ttu-id="50403-234">\Processor\PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="50403-234">\Processor\PercentIOWaitTime</span></span> |<span data-ttu-id="50403-235">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-235">Percent</span></span> |
| <span data-ttu-id="50403-236">\PhysicalDisk\BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="50403-236">\PhysicalDisk\BytesPerSecond</span></span> |<span data-ttu-id="50403-237">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="50403-237">BytesPerSecond</span></span> |
| <span data-ttu-id="50403-238">\PhysicalDisk\ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="50403-238">\PhysicalDisk\ReadBytesPerSecond</span></span> |<span data-ttu-id="50403-239">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="50403-239">BytesPerSecond</span></span> |
| <span data-ttu-id="50403-240">\PhysicalDisk\WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="50403-240">\PhysicalDisk\WriteBytesPerSecond</span></span> |<span data-ttu-id="50403-241">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="50403-241">BytesPerSecond</span></span> |
| <span data-ttu-id="50403-242">\PhysicalDisk\TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="50403-242">\PhysicalDisk\TransfersPerSecond</span></span> |<span data-ttu-id="50403-243">每秒計數</span><span class="sxs-lookup"><span data-stu-id="50403-243">CountPerSecond</span></span> |
| <span data-ttu-id="50403-244">\PhysicalDisk\ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="50403-244">\PhysicalDisk\ReadsPerSecond</span></span> |<span data-ttu-id="50403-245">每秒計數</span><span class="sxs-lookup"><span data-stu-id="50403-245">CountPerSecond</span></span> |
| <span data-ttu-id="50403-246">\PhysicalDisk\WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="50403-246">\PhysicalDisk\WritesPerSecond</span></span> |<span data-ttu-id="50403-247">每秒計數</span><span class="sxs-lookup"><span data-stu-id="50403-247">CountPerSecond</span></span> |
| <span data-ttu-id="50403-248">\PhysicalDisk\AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="50403-248">\PhysicalDisk\AverageReadTime</span></span> |<span data-ttu-id="50403-249">秒</span><span class="sxs-lookup"><span data-stu-id="50403-249">Seconds</span></span> |
| <span data-ttu-id="50403-250">\PhysicalDisk\AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="50403-250">\PhysicalDisk\AverageWriteTime</span></span> |<span data-ttu-id="50403-251">秒</span><span class="sxs-lookup"><span data-stu-id="50403-251">Seconds</span></span> |
| <span data-ttu-id="50403-252">\PhysicalDisk\AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="50403-252">\PhysicalDisk\AverageTransferTime</span></span> |<span data-ttu-id="50403-253">秒</span><span class="sxs-lookup"><span data-stu-id="50403-253">Seconds</span></span> |
| <span data-ttu-id="50403-254">\PhysicalDisk\AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="50403-254">\PhysicalDisk\AverageDiskQueueLength</span></span> |<span data-ttu-id="50403-255">Count</span><span class="sxs-lookup"><span data-stu-id="50403-255">Count</span></span> |
| <span data-ttu-id="50403-256">\NetworkInterface\BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="50403-256">\NetworkInterface\BytesTransmitted</span></span> |<span data-ttu-id="50403-257">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-257">Bytes</span></span> |
| <span data-ttu-id="50403-258">\NetworkInterface\BytesReceived</span><span class="sxs-lookup"><span data-stu-id="50403-258">\NetworkInterface\BytesReceived</span></span> |<span data-ttu-id="50403-259">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-259">Bytes</span></span> |
| <span data-ttu-id="50403-260">\NetworkInterface\PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="50403-260">\NetworkInterface\PacketsTransmitted</span></span> |<span data-ttu-id="50403-261">Count</span><span class="sxs-lookup"><span data-stu-id="50403-261">Count</span></span> |
| <span data-ttu-id="50403-262">\NetworkInterface\PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="50403-262">\NetworkInterface\PacketsReceived</span></span> |<span data-ttu-id="50403-263">Count</span><span class="sxs-lookup"><span data-stu-id="50403-263">Count</span></span> |
| <span data-ttu-id="50403-264">\NetworkInterface\BytesTotal</span><span class="sxs-lookup"><span data-stu-id="50403-264">\NetworkInterface\BytesTotal</span></span> |<span data-ttu-id="50403-265">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-265">Bytes</span></span> |
| <span data-ttu-id="50403-266">\NetworkInterface\TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="50403-266">\NetworkInterface\TotalRxErrors</span></span> |<span data-ttu-id="50403-267">Count</span><span class="sxs-lookup"><span data-stu-id="50403-267">Count</span></span> |
| <span data-ttu-id="50403-268">\NetworkInterface\TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="50403-268">\NetworkInterface\TotalTxErrors</span></span> |<span data-ttu-id="50403-269">Count</span><span class="sxs-lookup"><span data-stu-id="50403-269">Count</span></span> |
| <span data-ttu-id="50403-270">\NetworkInterface\TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="50403-270">\NetworkInterface\TotalCollisions</span></span> |<span data-ttu-id="50403-271">Count</span><span class="sxs-lookup"><span data-stu-id="50403-271">Count</span></span> |

## <a name="commonly-used-web-server-farm-metrics"></a><span data-ttu-id="50403-272">常用的 Web (伺服器陣列) 度量</span><span class="sxs-lookup"><span data-stu-id="50403-272">Commonly used Web (Server Farm) metrics</span></span>
<span data-ttu-id="50403-273">您也可以根據常用的 Web 伺服器度量 (如 Http 佇列長度) 執行自動調整。</span><span class="sxs-lookup"><span data-stu-id="50403-273">You can also perform autoscale based on common web server metrics such as the Http queue length.</span></span> <span data-ttu-id="50403-274">它的計量名稱是 **HttpQueueLength**。</span><span class="sxs-lookup"><span data-stu-id="50403-274">It's metric name is **HttpQueueLength**.</span></span>  <span data-ttu-id="50403-275">下一節會列出可用的伺服器陣列 (Web Apps) 度量。</span><span class="sxs-lookup"><span data-stu-id="50403-275">The following section lists available server farm (Web Apps) metrics.</span></span>

### <a name="web-apps-metrics"></a><span data-ttu-id="50403-276">Web Apps 度量</span><span class="sxs-lookup"><span data-stu-id="50403-276">Web Apps metrics</span></span>
<span data-ttu-id="50403-277">您可以在 PowerShell 中使用下列命令產生 Web Apps 清單。</span><span class="sxs-lookup"><span data-stu-id="50403-277">You can generate a list of the Web Apps metrics by using the following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="50403-278">您可以針對這些度量發出警示通知或以其為調整依據。</span><span class="sxs-lookup"><span data-stu-id="50403-278">You can alert on or scale by these metrics.</span></span>

| <span data-ttu-id="50403-279">度量名稱</span><span class="sxs-lookup"><span data-stu-id="50403-279">Metric Name</span></span> | <span data-ttu-id="50403-280">單位</span><span class="sxs-lookup"><span data-stu-id="50403-280">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="50403-281">CpuPercentage</span><span class="sxs-lookup"><span data-stu-id="50403-281">CpuPercentage</span></span> |<span data-ttu-id="50403-282">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-282">Percent</span></span> |
| <span data-ttu-id="50403-283">MemoryPercentage</span><span class="sxs-lookup"><span data-stu-id="50403-283">MemoryPercentage</span></span> |<span data-ttu-id="50403-284">百分比</span><span class="sxs-lookup"><span data-stu-id="50403-284">Percent</span></span> |
| <span data-ttu-id="50403-285">DiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="50403-285">DiskQueueLength</span></span> |<span data-ttu-id="50403-286">Count</span><span class="sxs-lookup"><span data-stu-id="50403-286">Count</span></span> |
| <span data-ttu-id="50403-287">HttpQueueLength</span><span class="sxs-lookup"><span data-stu-id="50403-287">HttpQueueLength</span></span> |<span data-ttu-id="50403-288">Count</span><span class="sxs-lookup"><span data-stu-id="50403-288">Count</span></span> |
| <span data-ttu-id="50403-289">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="50403-289">BytesReceived</span></span> |<span data-ttu-id="50403-290">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-290">Bytes</span></span> |
| <span data-ttu-id="50403-291">BytesSent</span><span class="sxs-lookup"><span data-stu-id="50403-291">BytesSent</span></span> |<span data-ttu-id="50403-292">位元組</span><span class="sxs-lookup"><span data-stu-id="50403-292">Bytes</span></span> |

## <a name="commonly-used-storage-metrics"></a><span data-ttu-id="50403-293">常用的儲存體度量</span><span class="sxs-lookup"><span data-stu-id="50403-293">Commonly used Storage metrics</span></span>
<span data-ttu-id="50403-294">您可以「儲存體佇列長度」做為調整依據，它是儲存體佇列中的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="50403-294">You can scale by Storage queue length, which is the number of messages in the storage queue.</span></span> <span data-ttu-id="50403-295">儲存體佇列長度是特殊度量，臨界值是每個執行個體的訊息數。</span><span class="sxs-lookup"><span data-stu-id="50403-295">Storage queue length is a special metric and the threshold is the number of messages per instance.</span></span> <span data-ttu-id="50403-296">比方說，如果有兩個執行個體，且臨界值設定為 100，當佇列中的訊息總數為 200 時，將會進行調整。</span><span class="sxs-lookup"><span data-stu-id="50403-296">For example, if there are two instances and if the threshold is set to 100, scaling occurs when the total number of messages in the queue is 200.</span></span> <span data-ttu-id="50403-297">可能每個執行個體有 100 個訊息、120 和 80 個訊息，或合計最多 200 個或更多訊息的其他任何組合。</span><span class="sxs-lookup"><span data-stu-id="50403-297">That can be 100 messages per instance, 120 and 80, or any other combination that adds up to 200 or more.</span></span>

<span data-ttu-id="50403-298">在 Azure 入口網站的 [設定] 刀鋒視窗中進行此設定。</span><span class="sxs-lookup"><span data-stu-id="50403-298">Configure this setting in the Azure portal in the **Settings** blade.</span></span> <span data-ttu-id="50403-299">若使用 VM 擴展集，您可以更新 Resource Manager 範本中的自動調整設定，改為使用 metricName 作為 ApproximateMessageCount，並傳遞儲存體佇列的識別碼作為 *metricResourceUri*。</span><span class="sxs-lookup"><span data-stu-id="50403-299">For VM scale sets, you can update the Autoscale setting in the Resource Manager template to use *metricName* as *ApproximateMessageCount* and pass the ID of the storage queue as *metricResourceUri*.</span></span>

<span data-ttu-id="50403-300">例如，使用傳統儲存體帳戶時，自動調整設定 metricTrigger 會包含：</span><span class="sxs-lookup"><span data-stu-id="50403-300">For example, with a Classic Storage Account the autoscale setting metricTrigger would include:</span></span>

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

<span data-ttu-id="50403-301">使用 (非傳統) 儲存體帳戶時，metricTrigger 會包含：</span><span class="sxs-lookup"><span data-stu-id="50403-301">For a (non-classic) storage account, the metricTrigger would include:</span></span>

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a><span data-ttu-id="50403-302">常用的服務匯流排衡量標準</span><span class="sxs-lookup"><span data-stu-id="50403-302">Commonly used Service Bus metrics</span></span>
<span data-ttu-id="50403-303">您可以依服務匯流排佇列長度做為調整依據，它是服務匯流排佇列中的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="50403-303">You can scale by Service Bus queue length, which is the number of messages in the Service Bus queue.</span></span> <span data-ttu-id="50403-304">服務匯流排長度是特殊度量，臨界值是每個執行個體的訊息數。</span><span class="sxs-lookup"><span data-stu-id="50403-304">Service Bus queue length is a special metric and the threshold is the number of messages per instance.</span></span> <span data-ttu-id="50403-305">比方說，如果有兩個執行個體，且臨界值設定為 100，當佇列中的訊息總數為 200 時，將會進行調整。</span><span class="sxs-lookup"><span data-stu-id="50403-305">For example, if there are two instances and if the threshold is set to 100, scaling occurs when the total number of messages in the queue is 200.</span></span> <span data-ttu-id="50403-306">可能每個執行個體有 100 個訊息、120 和 80 個訊息，或合計最多 200 個或更多訊息的其他任何組合。</span><span class="sxs-lookup"><span data-stu-id="50403-306">That can be 100 messages per instance, 120 and 80, or any other combination that adds up to 200 or more.</span></span>

<span data-ttu-id="50403-307">若使用 VM 擴展集，您可以更新 Resource Manager 範本中的自動調整設定，改為使用 metricName 作為 ApproximateMessageCount，並傳遞儲存體佇列的識別碼作為 *metricResourceUri*。</span><span class="sxs-lookup"><span data-stu-id="50403-307">For VM scale sets, you can update the Autoscale setting in the Resource Manager template to use *metricName* as *ApproximateMessageCount* and pass the ID of the storage queue as *metricResourceUri*.</span></span>

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> <span data-ttu-id="50403-308">若使用服務匯流排，資源群組的概念不存在，但 Azure Resource Manager 會建立每個區域的預設資源群組。</span><span class="sxs-lookup"><span data-stu-id="50403-308">For Service Bus, the resource group concept does not exist but Azure Resource Manager creates a default resource group per region.</span></span> <span data-ttu-id="50403-309">此資源群組通常是 'Default-ServiceBus-[region]' 的格式。</span><span class="sxs-lookup"><span data-stu-id="50403-309">The resource group is usually in the 'Default-ServiceBus-[region]' format.</span></span> <span data-ttu-id="50403-310">例如，'Default-ServiceBus-EastUS'、'Default-ServiceBus-WestUS'、'Default-ServiceBus-AustraliaEast' 等。</span><span class="sxs-lookup"><span data-stu-id="50403-310">For example, 'Default-ServiceBus-EastUS', 'Default-ServiceBus-WestUS', 'Default-ServiceBus-AustraliaEast' etc.</span></span>
>
>
