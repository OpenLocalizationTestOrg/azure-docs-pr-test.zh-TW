---
title: "aaa 適用於 Windows Vm 在 Azure 中 VM 保留維護 |Microsoft 文件"
description: "針對記憶體保留更新的就地 VM 移轉。"
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: b798f0afd9d8dc60ca8a78f7cc77435a0ddc76fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a><span data-ttu-id="2bf93-103">搭配就地 VM 移轉的 VM 保留維護</span><span class="sxs-lookup"><span data-stu-id="2bf93-103">VM preserving maintenance with In-place VM migration</span></span>

<span data-ttu-id="2bf93-104">雖然 hello 的大部分更新不有任何影響 toohosted Vm，有些情況是其中更新 toocomponents 或服務會導致最少的干擾 toorunning Vm （不含 hello 虛擬機器的完整重新開機）。</span><span class="sxs-lookup"><span data-stu-id="2bf93-104">While hello majority of updates have no impact toohosted VMs, there are cases where updates toocomponents or services result in minimal interference toorunning VMs (without a full reboot of hello virtual machine).</span></span>

<span data-ttu-id="2bf93-105">這些更新是透過可進行就地即時移轉 (也稱為「記憶體保留更新」) 的技術來完成。</span><span class="sxs-lookup"><span data-stu-id="2bf93-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="2bf93-106">在更新 hello 主機時，hello 虛擬機器被放入 「 暫停 」 狀態，雖然 hello 必要更新和修補程式，適用於裝載環境 （例如基礎作業系統） 的 hello 保留在 RAM 而 hello 記憶體。</span><span class="sxs-lookup"><span data-stu-id="2bf93-106">When updating hello host, hello virtual machine is placed into a “paused” state, preserving hello memory in RAM, while hello hosting environment (e.g. the underlying operating system) applies hello necessary updates and patches.</span></span>
<span data-ttu-id="2bf93-107">然後在暫停的 30 秒內繼續 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2bf93-107">hello virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="2bf93-108">繼續之後, hello hello 虛擬機器的時鐘會自動同步處理。</span><span class="sxs-lookup"><span data-stu-id="2bf93-108">After resuming, hello clock of hello virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="2bf93-109">並非所有的更新可以使用這項機制，來部署，但在短暫的延遲期間，指定部署更新，在此方式可大幅減少影響 toovirtual 機器。</span><span class="sxs-lookup"><span data-stu-id="2bf93-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact toovirtual machines.</span></span>

<span data-ttu-id="2bf93-110">多重執行個體更新 (可用性設定組中的 VM) 一次只會套用到一個更新網域。</span><span class="sxs-lookup"><span data-stu-id="2bf93-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="2bf93-111">這些更新對某些應用程式的影響可能比對其他應用程式更大。</span><span class="sxs-lookup"><span data-stu-id="2bf93-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="2bf93-112">應用程式執行即時事件處理、 媒體串流處理或轉碼或高輸送量網路案例，例如，可能無法設計的 tootolerate 暫停 30 秒。</span><span class="sxs-lookup"><span data-stu-id="2bf93-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed tootolerate a 30 second pause.</span></span> <span data-ttu-id="2bf93-113">虛擬機器中執行的應用程式可以了解即將推出的更新呼叫 hello[排程的事件](../virtual-machines-scheduled-events.md)API 的 hello [Azure 中繼資料服務](../virtual-machines-instancemetadataservice-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2bf93-113">Applications running in a virtual machine can learn about upcoming updates by calling hello [Scheduled Events](../virtual-machines-scheduled-events.md) API of hello [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
