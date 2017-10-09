---
title: "監視自動調整規模常見標準 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: 372a40d72d7a6c22c5ff854b1460ec8a3b7ed1d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a><span data-ttu-id="132f7-103">Azure 監視器自動調整的常用度量</span><span class="sxs-lookup"><span data-stu-id="132f7-103">Azure Monitor autoscaling common metrics</span></span>
<span data-ttu-id="132f7-104">Azure 監視的自動調整可讓您執行的執行個體 tooscale hello 數目向上或向下根據遙測資料 （度量）。</span><span class="sxs-lookup"><span data-stu-id="132f7-104">Azure Monitor autoscaling allows you tooscale hello number of running instances up or down, based on telemetry data (metrics).</span></span> <span data-ttu-id="132f7-105">本文件說明常見的度量，您可能想 toouse。</span><span class="sxs-lookup"><span data-stu-id="132f7-105">This document describes common metrics that you might want toouse.</span></span> <span data-ttu-id="132f7-106">在 hello Azure 入口網站雲端服務和伺服器陣列而言，您可以選擇由 hello 資源 tooscale hello 公制。</span><span class="sxs-lookup"><span data-stu-id="132f7-106">In hello Azure portal  for Cloud Services and Server Farms, you can choose hello metric of hello resource tooscale by.</span></span> <span data-ttu-id="132f7-107">不過，您也可以選擇不同的資源 tooscale 的任何度量。</span><span class="sxs-lookup"><span data-stu-id="132f7-107">However, you can also choose any metric from a different resource tooscale by.</span></span>

<span data-ttu-id="132f7-108">Azure 監視的自動調整規模太只適用於[虛擬機器擴展集](https://azure.microsoft.com/services/virtual-machine-scale-sets/)，[雲端服務](https://azure.microsoft.com/services/cloud-services/)，和[應用程式服務-Web 應用程式](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="132f7-108">Azure Monitor autoscale applies only too[Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="132f7-109">其他 Azure 服務使用不同的調整方法。</span><span class="sxs-lookup"><span data-stu-id="132f7-109">Other Azure services use different scaling methods.</span></span>

## <a name="compute-metrics-for-resource-manager-based-vms"></a><span data-ttu-id="132f7-110">針對以 Resource Manager 為基礎的 VM 來計算度量</span><span class="sxs-lookup"><span data-stu-id="132f7-110">Compute metrics for Resource Manager-based VMs</span></span>
<span data-ttu-id="132f7-111">根據預設，以 Resource Manager 為基礎的虛擬機器和虛擬機器擴展集會發出基本 (主機層級) 的度量。</span><span class="sxs-lookup"><span data-stu-id="132f7-111">By default, Resource Manager-based Virtual Machines and Virtual Machine Scale Sets emit basic (host-level) metrics.</span></span> <span data-ttu-id="132f7-112">此外，當您設定的 Azure VM，以及 VMSS 收集診斷資料，hello Azure 診斷擴充功能也會發出 （通常稱為 「 客體 OS 度量 」） 的客體 OS 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="132f7-112">In addition, when you configure diagnostics data collection for an Azure VM and VMSS,  hello Azure diagnostic extension also emits guest-OS performance counters (commonly known as "guest-OS metrics").</span></span>  <span data-ttu-id="132f7-113">您在自動調整規則中使用所有這些度量。</span><span class="sxs-lookup"><span data-stu-id="132f7-113">You use all these metrics in autoscale rules.</span></span>

<span data-ttu-id="132f7-114">您可以使用 hello `Get MetricDefinitions` API/PoSH CLI tooview hello 度量可用於 VMSS 資源。</span><span class="sxs-lookup"><span data-stu-id="132f7-114">You can use hello `Get MetricDefinitions` API/PoSH/CLI tooview hello metrics available for your VMSS resource.</span></span>

<span data-ttu-id="132f7-115">如果您使用 VM 擴展集，而且發現特定度量沒有列出來，可能是您的診斷擴充功能已「停用」它。</span><span class="sxs-lookup"><span data-stu-id="132f7-115">If you're using VM scale sets and you don't see a particular metric listed, then it is likely *disabled* in your diagnostics extension.</span></span>

<span data-ttu-id="132f7-116">如果特定的度量不被取樣或在傳送嗨您想要的頻率，您可以更新 hello 診斷組態。</span><span class="sxs-lookup"><span data-stu-id="132f7-116">If a particular metric is not being sampled or transferred at hello frequency you want, you can update hello diagnostics configuration.</span></span>

<span data-ttu-id="132f7-117">如果任一上述的情況下為 true，則請檢閱[執行 Windows 的虛擬機器中使用 PowerShell tooenable Azure 診斷](../virtual-machines/windows/ps-extensions-diagnostics.md)有關 PowerShell tooconfigure 和更新您的 Azure VM 診斷延伸模組 tooenable hello 度量。</span><span class="sxs-lookup"><span data-stu-id="132f7-117">If either preceding case is true, then review [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md) about PowerShell tooconfigure and update your Azure VM Diagnostics extension tooenable hello metric.</span></span> <span data-ttu-id="132f7-118">該文章也包含診斷組態檔的範例。</span><span class="sxs-lookup"><span data-stu-id="132f7-118">That article also includes a sample diagnostics configuration file.</span></span>

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a><span data-ttu-id="132f7-119">以 Resource Manager 為基礎的 Windows 和 Linux VM 的主機度量</span><span class="sxs-lookup"><span data-stu-id="132f7-119">Host metrics for Resource Manager-based Windows and Linux VMs</span></span>
<span data-ttu-id="132f7-120">下列主機層級度量的 hello 會發出預設 Azure VM 和 VMSS Windows 和 Linux 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="132f7-120">hello following host-level metrics are emitted by default for Azure VM and VMSS in both Windows and Linux instances.</span></span> <span data-ttu-id="132f7-121">這些度量會描述您的 Azure VM，但會收集從 hello Azure VM 的主機，而不是透過 hello 客體 VM 上安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="132f7-121">These metrics describe your Azure VM, but are collected from hello Azure VM host rather than via agent installed on hello guest VM.</span></span> <span data-ttu-id="132f7-122">您可以在自動調整規則中使用這些度量。</span><span class="sxs-lookup"><span data-stu-id="132f7-122">You may use these metrics in autoscaling rules.</span></span>

- [<span data-ttu-id="132f7-123">以 Resource Manager 為基礎的 Windows 和 Linux VM 的主機度量</span><span class="sxs-lookup"><span data-stu-id="132f7-123">Host metrics for Resource Manager-based Windows and Linux VMs</span></span>](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [<span data-ttu-id="132f7-124">以 Resource Manager 為基礎的 Windows 和 Linux VM 擴展集的主機度量</span><span class="sxs-lookup"><span data-stu-id="132f7-124">Host metrics for Resource Manager-based Windows and Linux VM Scale Sets</span></span>](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a><span data-ttu-id="132f7-125">客體 OS 度量以 Resource Manager 為基礎的 Windows VM</span><span class="sxs-lookup"><span data-stu-id="132f7-125">Guest OS metrics Resource Manager-based Windows VMs</span></span>
<span data-ttu-id="132f7-126">當您在 Azure 中建立 VM 時，診斷會啟用使用 hello 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="132f7-126">When you create a VM in Azure, diagnostics is enabled by using hello Diagnostics extension.</span></span> <span data-ttu-id="132f7-127">hello 診斷延伸模組會發出一組取自 hello VM 內的度量。</span><span class="sxs-lookup"><span data-stu-id="132f7-127">hello diagnostics extension emits a set of metrics taken from inside of hello VM.</span></span> <span data-ttu-id="132f7-128">這表示您可以關閉自動調整依預設不發出的度量。</span><span class="sxs-lookup"><span data-stu-id="132f7-128">This means you can autoscale off of metrics that are not emitted by default.</span></span>

<span data-ttu-id="132f7-129">您可以使用下列命令在 PowerShell 中的 hello 產生 hello 度量的清單。</span><span class="sxs-lookup"><span data-stu-id="132f7-129">You can generate a list of hello metrics by using hello following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="132f7-130">您可以建立 hello 下列度量的警示：</span><span class="sxs-lookup"><span data-stu-id="132f7-130">You can create an alert for hello following metrics:</span></span>

| <span data-ttu-id="132f7-131">度量名稱</span><span class="sxs-lookup"><span data-stu-id="132f7-131">Metric Name</span></span> | <span data-ttu-id="132f7-132">單位</span><span class="sxs-lookup"><span data-stu-id="132f7-132">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="132f7-133">\Processor(_Total)\% Processor Time</span><span class="sxs-lookup"><span data-stu-id="132f7-133">\Processor(_Total)\% Processor Time</span></span> |<span data-ttu-id="132f7-134">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-134">Percent</span></span> |
| <span data-ttu-id="132f7-135">\Processor(_Total)\% Privileged Time</span><span class="sxs-lookup"><span data-stu-id="132f7-135">\Processor(_Total)\% Privileged Time</span></span> |<span data-ttu-id="132f7-136">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-136">Percent</span></span> |
| <span data-ttu-id="132f7-137">\Processor(_Total)\% User Time</span><span class="sxs-lookup"><span data-stu-id="132f7-137">\Processor(_Total)\% User Time</span></span> |<span data-ttu-id="132f7-138">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-138">Percent</span></span> |
| <span data-ttu-id="132f7-139">\Processor Information(_Total)\Processor Frequency</span><span class="sxs-lookup"><span data-stu-id="132f7-139">\Processor Information(_Total)\Processor Frequency</span></span> |<span data-ttu-id="132f7-140">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-140">Count</span></span> |
| <span data-ttu-id="132f7-141">\System\Processes</span><span class="sxs-lookup"><span data-stu-id="132f7-141">\System\Processes</span></span> |<span data-ttu-id="132f7-142">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-142">Count</span></span> |
| <span data-ttu-id="132f7-143">\Process(_Total)\Thread Count</span><span class="sxs-lookup"><span data-stu-id="132f7-143">\Process(_Total)\Thread Count</span></span> |<span data-ttu-id="132f7-144">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-144">Count</span></span> |
| <span data-ttu-id="132f7-145">\Process(_Total)\Handle Count</span><span class="sxs-lookup"><span data-stu-id="132f7-145">\Process(_Total)\Handle Count</span></span> |<span data-ttu-id="132f7-146">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-146">Count</span></span> |
| <span data-ttu-id="132f7-147">\Memory\% Committed Bytes In Use</span><span class="sxs-lookup"><span data-stu-id="132f7-147">\Memory\% Committed Bytes In Use</span></span> |<span data-ttu-id="132f7-148">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-148">Percent</span></span> |
| <span data-ttu-id="132f7-149">\Memory\Available Bytes</span><span class="sxs-lookup"><span data-stu-id="132f7-149">\Memory\Available Bytes</span></span> |<span data-ttu-id="132f7-150">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-150">Bytes</span></span> |
| <span data-ttu-id="132f7-151">\Memory\Committed Bytes</span><span class="sxs-lookup"><span data-stu-id="132f7-151">\Memory\Committed Bytes</span></span> |<span data-ttu-id="132f7-152">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-152">Bytes</span></span> |
| <span data-ttu-id="132f7-153">\Memory\Commit Limit</span><span class="sxs-lookup"><span data-stu-id="132f7-153">\Memory\Commit Limit</span></span> |<span data-ttu-id="132f7-154">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-154">Bytes</span></span> |
| <span data-ttu-id="132f7-155">\Memory\Pool Paged Bytes</span><span class="sxs-lookup"><span data-stu-id="132f7-155">\Memory\Pool Paged Bytes</span></span> |<span data-ttu-id="132f7-156">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-156">Bytes</span></span> |
| <span data-ttu-id="132f7-157">\Memory\Pool Nonpaged Bytes</span><span class="sxs-lookup"><span data-stu-id="132f7-157">\Memory\Pool Nonpaged Bytes</span></span> |<span data-ttu-id="132f7-158">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-158">Bytes</span></span> |
| <span data-ttu-id="132f7-159">\PhysicalDisk(_Total)\% Disk Time</span><span class="sxs-lookup"><span data-stu-id="132f7-159">\PhysicalDisk(_Total)\% Disk Time</span></span> |<span data-ttu-id="132f7-160">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-160">Percent</span></span> |
| <span data-ttu-id="132f7-161">\PhysicalDisk(_Total)\% Disk Read Time</span><span class="sxs-lookup"><span data-stu-id="132f7-161">\PhysicalDisk(_Total)\% Disk Read Time</span></span> |<span data-ttu-id="132f7-162">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-162">Percent</span></span> |
| <span data-ttu-id="132f7-163">\PhysicalDisk(_Total)\% Disk Write Time</span><span class="sxs-lookup"><span data-stu-id="132f7-163">\PhysicalDisk(_Total)\% Disk Write Time</span></span> |<span data-ttu-id="132f7-164">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-164">Percent</span></span> |
| <span data-ttu-id="132f7-165">\PhysicalDisk(_Total)\每秒的磁碟傳輸數</span><span class="sxs-lookup"><span data-stu-id="132f7-165">\PhysicalDisk(_Total)\Disk Transfers/sec</span></span> |<span data-ttu-id="132f7-166">每秒計數</span><span class="sxs-lookup"><span data-stu-id="132f7-166">CountPerSecond</span></span> |
| <span data-ttu-id="132f7-167">\PhysicalDisk(_Total)\Disk Reads/sec</span><span class="sxs-lookup"><span data-stu-id="132f7-167">\PhysicalDisk(_Total)\Disk Reads/sec</span></span> |<span data-ttu-id="132f7-168">每秒計數</span><span class="sxs-lookup"><span data-stu-id="132f7-168">CountPerSecond</span></span> |
| <span data-ttu-id="132f7-169">\PhysicalDisk(_Total)\Disk Writes/sec</span><span class="sxs-lookup"><span data-stu-id="132f7-169">\PhysicalDisk(_Total)\Disk Writes/sec</span></span> |<span data-ttu-id="132f7-170">每秒計數</span><span class="sxs-lookup"><span data-stu-id="132f7-170">CountPerSecond</span></span> |
| <span data-ttu-id="132f7-171">\PhysicalDisk(_Total)\Disk Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="132f7-171">\PhysicalDisk(_Total)\Disk Bytes/sec</span></span> |<span data-ttu-id="132f7-172">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-172">BytesPerSecond</span></span> |
| <span data-ttu-id="132f7-173">\PhysicalDisk(_Total)\Disk Read Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="132f7-173">\PhysicalDisk(_Total)\Disk Read Bytes/sec</span></span> |<span data-ttu-id="132f7-174">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-174">BytesPerSecond</span></span> |
| <span data-ttu-id="132f7-175">\PhysicalDisk(_Total)\Disk Write Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="132f7-175">\PhysicalDisk(_Total)\Disk Write Bytes/sec</span></span> |<span data-ttu-id="132f7-176">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-176">BytesPerSecond</span></span> |
| <span data-ttu-id="132f7-177">\PhysicalDisk(_Total)\Avg.磁碟佇列長度</span><span class="sxs-lookup"><span data-stu-id="132f7-177">\PhysicalDisk(_Total)\Avg. Disk Queue Length</span></span> |<span data-ttu-id="132f7-178">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-178">Count</span></span> |
| <span data-ttu-id="132f7-179">\PhysicalDisk(_Total)\Avg.磁碟讀取佇列長度</span><span class="sxs-lookup"><span data-stu-id="132f7-179">\PhysicalDisk(_Total)\Avg. Disk Read Queue Length</span></span> |<span data-ttu-id="132f7-180">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-180">Count</span></span> |
| <span data-ttu-id="132f7-181">\PhysicalDisk(_Total)\Avg.磁碟寫入佇列長度</span><span class="sxs-lookup"><span data-stu-id="132f7-181">\PhysicalDisk(_Total)\Avg. Disk Write Queue Length</span></span> |<span data-ttu-id="132f7-182">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-182">Count</span></span> |
| <span data-ttu-id="132f7-183">\LogicalDisk(_Total)\% Free Space</span><span class="sxs-lookup"><span data-stu-id="132f7-183">\LogicalDisk(_Total)\% Free Space</span></span> |<span data-ttu-id="132f7-184">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-184">Percent</span></span> |
| <span data-ttu-id="132f7-185">\LogicalDisk(_Total)\Free Megabytes</span><span class="sxs-lookup"><span data-stu-id="132f7-185">\LogicalDisk(_Total)\Free Megabytes</span></span> |<span data-ttu-id="132f7-186">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-186">Count</span></span> |

### <a name="guest-os-metrics-linux-vms"></a><span data-ttu-id="132f7-187">客體 OS 度量 Linux VM</span><span class="sxs-lookup"><span data-stu-id="132f7-187">Guest OS metrics Linux VMs</span></span>
<span data-ttu-id="132f7-188">當您在 Azure 中建立 VM 時，根據預設會使用診斷擴充來啟用診斷。</span><span class="sxs-lookup"><span data-stu-id="132f7-188">When you create a VM in Azure, diagnostics is enabled by default by using Diagnostics extension.</span></span>

<span data-ttu-id="132f7-189">您可以使用下列命令在 PowerShell 中的 hello 產生 hello 度量的清單。</span><span class="sxs-lookup"><span data-stu-id="132f7-189">You can generate a list of hello metrics by using hello following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 <span data-ttu-id="132f7-190">您可以建立 hello 下列度量的警示：</span><span class="sxs-lookup"><span data-stu-id="132f7-190">You can create an alert for hello following metrics:</span></span>

| <span data-ttu-id="132f7-191">度量名稱</span><span class="sxs-lookup"><span data-stu-id="132f7-191">Metric Name</span></span> | <span data-ttu-id="132f7-192">單位</span><span class="sxs-lookup"><span data-stu-id="132f7-192">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="132f7-193">\Memory\AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="132f7-193">\Memory\AvailableMemory</span></span> |<span data-ttu-id="132f7-194">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-194">Bytes</span></span> |
| <span data-ttu-id="132f7-195">\Memory\PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="132f7-195">\Memory\PercentAvailableMemory</span></span> |<span data-ttu-id="132f7-196">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-196">Percent</span></span> |
| <span data-ttu-id="132f7-197">\Memory\UsedMemory</span><span class="sxs-lookup"><span data-stu-id="132f7-197">\Memory\UsedMemory</span></span> |<span data-ttu-id="132f7-198">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-198">Bytes</span></span> |
| <span data-ttu-id="132f7-199">\Memory\PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="132f7-199">\Memory\PercentUsedMemory</span></span> |<span data-ttu-id="132f7-200">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-200">Percent</span></span> |
| <span data-ttu-id="132f7-201">\Memory\PercentUsedByCache</span><span class="sxs-lookup"><span data-stu-id="132f7-201">\Memory\PercentUsedByCache</span></span> |<span data-ttu-id="132f7-202">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-202">Percent</span></span> |
| <span data-ttu-id="132f7-203">\Memory\PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="132f7-203">\Memory\PagesPerSec</span></span> |<span data-ttu-id="132f7-204">每秒計數</span><span class="sxs-lookup"><span data-stu-id="132f7-204">CountPerSecond</span></span> |
| <span data-ttu-id="132f7-205">\Memory\PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="132f7-205">\Memory\PagesReadPerSec</span></span> |<span data-ttu-id="132f7-206">每秒計數</span><span class="sxs-lookup"><span data-stu-id="132f7-206">CountPerSecond</span></span> |
| <span data-ttu-id="132f7-207">\Memory\PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="132f7-207">\Memory\PagesWrittenPerSec</span></span> |<span data-ttu-id="132f7-208">每秒計數</span><span class="sxs-lookup"><span data-stu-id="132f7-208">CountPerSecond</span></span> |
| <span data-ttu-id="132f7-209">\Memory\AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="132f7-209">\Memory\AvailableSwap</span></span> |<span data-ttu-id="132f7-210">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-210">Bytes</span></span> |
| <span data-ttu-id="132f7-211">\Memory\PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="132f7-211">\Memory\PercentAvailableSwap</span></span> |<span data-ttu-id="132f7-212">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-212">Percent</span></span> |
| <span data-ttu-id="132f7-213">\Memory\UsedSwap</span><span class="sxs-lookup"><span data-stu-id="132f7-213">\Memory\UsedSwap</span></span> |<span data-ttu-id="132f7-214">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-214">Bytes</span></span> |
| <span data-ttu-id="132f7-215">\Memory\PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="132f7-215">\Memory\PercentUsedSwap</span></span> |<span data-ttu-id="132f7-216">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-216">Percent</span></span> |
| <span data-ttu-id="132f7-217">\Processor\PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="132f7-217">\Processor\PercentIdleTime</span></span> |<span data-ttu-id="132f7-218">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-218">Percent</span></span> |
| <span data-ttu-id="132f7-219">\Processor\PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="132f7-219">\Processor\PercentUserTime</span></span> |<span data-ttu-id="132f7-220">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-220">Percent</span></span> |
| <span data-ttu-id="132f7-221">\Processor\PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="132f7-221">\Processor\PercentNiceTime</span></span> |<span data-ttu-id="132f7-222">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-222">Percent</span></span> |
| <span data-ttu-id="132f7-223">\Processor\PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="132f7-223">\Processor\PercentPrivilegedTime</span></span> |<span data-ttu-id="132f7-224">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-224">Percent</span></span> |
| <span data-ttu-id="132f7-225">\Processor\PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="132f7-225">\Processor\PercentInterruptTime</span></span> |<span data-ttu-id="132f7-226">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-226">Percent</span></span> |
| <span data-ttu-id="132f7-227">\Processor\PercentDPCTime</span><span class="sxs-lookup"><span data-stu-id="132f7-227">\Processor\PercentDPCTime</span></span> |<span data-ttu-id="132f7-228">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-228">Percent</span></span> |
| <span data-ttu-id="132f7-229">\Processor\PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="132f7-229">\Processor\PercentProcessorTime</span></span> |<span data-ttu-id="132f7-230">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-230">Percent</span></span> |
| <span data-ttu-id="132f7-231">\Processor\PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="132f7-231">\Processor\PercentIOWaitTime</span></span> |<span data-ttu-id="132f7-232">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-232">Percent</span></span> |
| <span data-ttu-id="132f7-233">\PhysicalDisk\BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="132f7-233">\PhysicalDisk\BytesPerSecond</span></span> |<span data-ttu-id="132f7-234">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-234">BytesPerSecond</span></span> |
| <span data-ttu-id="132f7-235">\PhysicalDisk\ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="132f7-235">\PhysicalDisk\ReadBytesPerSecond</span></span> |<span data-ttu-id="132f7-236">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-236">BytesPerSecond</span></span> |
| <span data-ttu-id="132f7-237">\PhysicalDisk\WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="132f7-237">\PhysicalDisk\WriteBytesPerSecond</span></span> |<span data-ttu-id="132f7-238">每秒位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-238">BytesPerSecond</span></span> |
| <span data-ttu-id="132f7-239">\PhysicalDisk\TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="132f7-239">\PhysicalDisk\TransfersPerSecond</span></span> |<span data-ttu-id="132f7-240">每秒計數</span><span class="sxs-lookup"><span data-stu-id="132f7-240">CountPerSecond</span></span> |
| <span data-ttu-id="132f7-241">\PhysicalDisk\ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="132f7-241">\PhysicalDisk\ReadsPerSecond</span></span> |<span data-ttu-id="132f7-242">每秒計數</span><span class="sxs-lookup"><span data-stu-id="132f7-242">CountPerSecond</span></span> |
| <span data-ttu-id="132f7-243">\PhysicalDisk\WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="132f7-243">\PhysicalDisk\WritesPerSecond</span></span> |<span data-ttu-id="132f7-244">每秒計數</span><span class="sxs-lookup"><span data-stu-id="132f7-244">CountPerSecond</span></span> |
| <span data-ttu-id="132f7-245">\PhysicalDisk\AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="132f7-245">\PhysicalDisk\AverageReadTime</span></span> |<span data-ttu-id="132f7-246">秒</span><span class="sxs-lookup"><span data-stu-id="132f7-246">Seconds</span></span> |
| <span data-ttu-id="132f7-247">\PhysicalDisk\AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="132f7-247">\PhysicalDisk\AverageWriteTime</span></span> |<span data-ttu-id="132f7-248">秒</span><span class="sxs-lookup"><span data-stu-id="132f7-248">Seconds</span></span> |
| <span data-ttu-id="132f7-249">\PhysicalDisk\AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="132f7-249">\PhysicalDisk\AverageTransferTime</span></span> |<span data-ttu-id="132f7-250">秒</span><span class="sxs-lookup"><span data-stu-id="132f7-250">Seconds</span></span> |
| <span data-ttu-id="132f7-251">\PhysicalDisk\AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="132f7-251">\PhysicalDisk\AverageDiskQueueLength</span></span> |<span data-ttu-id="132f7-252">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-252">Count</span></span> |
| <span data-ttu-id="132f7-253">\NetworkInterface\BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="132f7-253">\NetworkInterface\BytesTransmitted</span></span> |<span data-ttu-id="132f7-254">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-254">Bytes</span></span> |
| <span data-ttu-id="132f7-255">\NetworkInterface\BytesReceived</span><span class="sxs-lookup"><span data-stu-id="132f7-255">\NetworkInterface\BytesReceived</span></span> |<span data-ttu-id="132f7-256">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-256">Bytes</span></span> |
| <span data-ttu-id="132f7-257">\NetworkInterface\PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="132f7-257">\NetworkInterface\PacketsTransmitted</span></span> |<span data-ttu-id="132f7-258">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-258">Count</span></span> |
| <span data-ttu-id="132f7-259">\NetworkInterface\PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="132f7-259">\NetworkInterface\PacketsReceived</span></span> |<span data-ttu-id="132f7-260">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-260">Count</span></span> |
| <span data-ttu-id="132f7-261">\NetworkInterface\BytesTotal</span><span class="sxs-lookup"><span data-stu-id="132f7-261">\NetworkInterface\BytesTotal</span></span> |<span data-ttu-id="132f7-262">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-262">Bytes</span></span> |
| <span data-ttu-id="132f7-263">\NetworkInterface\TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="132f7-263">\NetworkInterface\TotalRxErrors</span></span> |<span data-ttu-id="132f7-264">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-264">Count</span></span> |
| <span data-ttu-id="132f7-265">\NetworkInterface\TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="132f7-265">\NetworkInterface\TotalTxErrors</span></span> |<span data-ttu-id="132f7-266">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-266">Count</span></span> |
| <span data-ttu-id="132f7-267">\NetworkInterface\TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="132f7-267">\NetworkInterface\TotalCollisions</span></span> |<span data-ttu-id="132f7-268">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-268">Count</span></span> |

## <a name="commonly-used-web-server-farm-metrics"></a><span data-ttu-id="132f7-269">常用的 Web (伺服器陣列) 度量</span><span class="sxs-lookup"><span data-stu-id="132f7-269">Commonly used Web (Server Farm) metrics</span></span>
<span data-ttu-id="132f7-270">您也可以執行一般的 web 伺服器度量，例如 hello Http 佇列長度為基礎的自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="132f7-270">You can also perform autoscale based on common web server metrics such as hello Http queue length.</span></span> <span data-ttu-id="132f7-271">它的計量名稱是 **HttpQueueLength**。</span><span class="sxs-lookup"><span data-stu-id="132f7-271">It's metric name is **HttpQueueLength**.</span></span>  <span data-ttu-id="132f7-272">hello 之後 > 一節列出可用的伺服器陣列 （Web 應用程式） 度量資訊。</span><span class="sxs-lookup"><span data-stu-id="132f7-272">hello following section lists available server farm (Web Apps) metrics.</span></span>

### <a name="web-apps-metrics"></a><span data-ttu-id="132f7-273">Web Apps 度量</span><span class="sxs-lookup"><span data-stu-id="132f7-273">Web Apps metrics</span></span>
<span data-ttu-id="132f7-274">您可以使用下列命令在 PowerShell 中的 hello 產生一份 hello Web 應用程式的度量。</span><span class="sxs-lookup"><span data-stu-id="132f7-274">You can generate a list of hello Web Apps metrics by using hello following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="132f7-275">您可以針對這些度量發出警示通知或以其為調整依據。</span><span class="sxs-lookup"><span data-stu-id="132f7-275">You can alert on or scale by these metrics.</span></span>

| <span data-ttu-id="132f7-276">度量名稱</span><span class="sxs-lookup"><span data-stu-id="132f7-276">Metric Name</span></span> | <span data-ttu-id="132f7-277">單位</span><span class="sxs-lookup"><span data-stu-id="132f7-277">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="132f7-278">CpuPercentage</span><span class="sxs-lookup"><span data-stu-id="132f7-278">CpuPercentage</span></span> |<span data-ttu-id="132f7-279">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-279">Percent</span></span> |
| <span data-ttu-id="132f7-280">MemoryPercentage</span><span class="sxs-lookup"><span data-stu-id="132f7-280">MemoryPercentage</span></span> |<span data-ttu-id="132f7-281">百分比</span><span class="sxs-lookup"><span data-stu-id="132f7-281">Percent</span></span> |
| <span data-ttu-id="132f7-282">DiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="132f7-282">DiskQueueLength</span></span> |<span data-ttu-id="132f7-283">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-283">Count</span></span> |
| <span data-ttu-id="132f7-284">HttpQueueLength</span><span class="sxs-lookup"><span data-stu-id="132f7-284">HttpQueueLength</span></span> |<span data-ttu-id="132f7-285">Count</span><span class="sxs-lookup"><span data-stu-id="132f7-285">Count</span></span> |
| <span data-ttu-id="132f7-286">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="132f7-286">BytesReceived</span></span> |<span data-ttu-id="132f7-287">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-287">Bytes</span></span> |
| <span data-ttu-id="132f7-288">BytesSent</span><span class="sxs-lookup"><span data-stu-id="132f7-288">BytesSent</span></span> |<span data-ttu-id="132f7-289">位元組</span><span class="sxs-lookup"><span data-stu-id="132f7-289">Bytes</span></span> |

## <a name="commonly-used-storage-metrics"></a><span data-ttu-id="132f7-290">常用的儲存體度量</span><span class="sxs-lookup"><span data-stu-id="132f7-290">Commonly used Storage metrics</span></span>
<span data-ttu-id="132f7-291">您可以調整的儲存體佇列長度是 hello hello 儲存體佇列中的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="132f7-291">You can scale by Storage queue length, which is hello number of messages in hello storage queue.</span></span> <span data-ttu-id="132f7-292">儲存體佇列長度是特殊的度量且 hello 臨界值為 hello 訊息，每個執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="132f7-292">Storage queue length is a special metric and hello threshold is hello number of messages per instance.</span></span> <span data-ttu-id="132f7-293">比方說，如果有兩個執行個體，而且 hello 閾值設定 too100，調整時發生 hello 總 hello 佇列中的訊息數目為 200。</span><span class="sxs-lookup"><span data-stu-id="132f7-293">For example, if there are two instances and if hello threshold is set too100, scaling occurs when hello total number of messages in hello queue is 200.</span></span> <span data-ttu-id="132f7-294">可以是每個執行個體的 100 個訊息、 120 和 80，或任何其他的組合加總 too200 或多個。</span><span class="sxs-lookup"><span data-stu-id="132f7-294">That can be 100 messages per instance, 120 and 80, or any other combination that adds up too200 or more.</span></span>

<span data-ttu-id="132f7-295">設定此設定，在 hello Azure 入口網站中 hello**設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="132f7-295">Configure this setting in hello Azure portal in hello **Settings** blade.</span></span> <span data-ttu-id="132f7-296">針對 VM 規模集，您可以更新 hello 自動調整規模設定中 hello 資源管理員範本 toouse *metricName*為*ApproximateMessageCount*並傳遞 hello 識別碼 hello 儲存體佇列，做為*metricResourceUri*。</span><span class="sxs-lookup"><span data-stu-id="132f7-296">For VM scale sets, you can update hello Autoscale setting in hello Resource Manager template toouse *metricName* as *ApproximateMessageCount* and pass hello ID of hello storage queue as *metricResourceUri*.</span></span>

<span data-ttu-id="132f7-297">例如，以傳統的儲存體帳戶 hello 包含自動調整規模設定 metricTrigger:</span><span class="sxs-lookup"><span data-stu-id="132f7-297">For example, with a Classic Storage Account hello autoscale setting metricTrigger would include:</span></span>

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

<span data-ttu-id="132f7-298">（非傳統） 儲存體帳戶，會包含 hello metricTrigger:</span><span class="sxs-lookup"><span data-stu-id="132f7-298">For a (non-classic) storage account, hello metricTrigger would include:</span></span>

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a><span data-ttu-id="132f7-299">常用的服務匯流排衡量標準</span><span class="sxs-lookup"><span data-stu-id="132f7-299">Commonly used Service Bus metrics</span></span>
<span data-ttu-id="132f7-300">您可以調整服務匯流排佇列長度是 hello hello 服務匯流排佇列中的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="132f7-300">You can scale by Service Bus queue length, which is hello number of messages in hello Service Bus queue.</span></span> <span data-ttu-id="132f7-301">服務匯流排佇列長度是特殊的度量和 hello 臨界值是每個執行個體訊息的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="132f7-301">Service Bus queue length is a special metric and hello threshold is hello number of messages per instance.</span></span> <span data-ttu-id="132f7-302">比方說，如果有兩個執行個體，而且 hello 閾值設定 too100，調整時發生 hello 總 hello 佇列中的訊息數目為 200。</span><span class="sxs-lookup"><span data-stu-id="132f7-302">For example, if there are two instances and if hello threshold is set too100, scaling occurs when hello total number of messages in hello queue is 200.</span></span> <span data-ttu-id="132f7-303">可以是每個執行個體的 100 個訊息、 120 和 80，或任何其他的組合加總 too200 或多個。</span><span class="sxs-lookup"><span data-stu-id="132f7-303">That can be 100 messages per instance, 120 and 80, or any other combination that adds up too200 or more.</span></span>

<span data-ttu-id="132f7-304">針對 VM 規模集，您可以更新 hello 自動調整規模設定中 hello 資源管理員範本 toouse *metricName*為*ApproximateMessageCount*並傳遞 hello 識別碼 hello 儲存體佇列，做為*metricResourceUri*。</span><span class="sxs-lookup"><span data-stu-id="132f7-304">For VM scale sets, you can update hello Autoscale setting in hello Resource Manager template toouse *metricName* as *ApproximateMessageCount* and pass hello ID of hello storage queue as *metricResourceUri*.</span></span>

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> <span data-ttu-id="132f7-305">服務匯流排的 hello 資源群組概念不存在，但 Azure 資源管理員會建立每個區域的預設資源群組。</span><span class="sxs-lookup"><span data-stu-id="132f7-305">For Service Bus, hello resource group concept does not exist but Azure Resource Manager creates a default resource group per region.</span></span> <span data-ttu-id="132f7-306">hello 資源群組通常是 hello '預設值-ServiceBus-[region]' 格式。</span><span class="sxs-lookup"><span data-stu-id="132f7-306">hello resource group is usually in hello 'Default-ServiceBus-[region]' format.</span></span> <span data-ttu-id="132f7-307">例如，'Default-ServiceBus-EastUS'、'Default-ServiceBus-WestUS'、'Default-ServiceBus-AustraliaEast' 等。</span><span class="sxs-lookup"><span data-stu-id="132f7-307">For example, 'Default-ServiceBus-EastUS', 'Default-ServiceBus-WestUS', 'Default-ServiceBus-AustraliaEast' etc.</span></span>
>
>
