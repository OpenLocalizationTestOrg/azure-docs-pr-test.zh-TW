---
title: "使用 Azure Site Recovery 檢閱 Hyper-V 對 Azure 複寫的必要條件 (不含 System Center VMM) | Microsoft Docs"
description: "描述使用 Azure Site Recovery 設定內部部署 Hyper-V VM 對 Azure 的複寫、容錯移轉和復原之必要條件"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: cbb5d3598ef91512991d7d1e9f854eb12980752b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="step-2-review-the-prerequisites-for-hyper-v-without-vmm-to-azure-replication"></a><span data-ttu-id="2f9f3-103">步驟 2：檢閱 Hyper-V (不含 VMM) 對 Azure 複寫的必要條件</span><span class="sxs-lookup"><span data-stu-id="2f9f3-103">Step 2: Review the prerequisites for Hyper-V (without VMM) to Azure replication</span></span>

<span data-ttu-id="2f9f3-104">資料表中會摘要列出必要條件。</span><span class="sxs-lookup"><span data-stu-id="2f9f3-104">The prerequisites are summarized in the table.</span></span>


<span data-ttu-id="2f9f3-105">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="2f9f3-105">**Prerequisite**</span></span> | <span data-ttu-id="2f9f3-106">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="2f9f3-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="2f9f3-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="2f9f3-107">**Azure**</span></span> | <span data-ttu-id="2f9f3-108">了解 [Azure 需求](site-recovery-prereq.md#azure-requirements)。</span><span class="sxs-lookup"><span data-stu-id="2f9f3-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="2f9f3-109">**內部部署伺服器**</span><span class="sxs-lookup"><span data-stu-id="2f9f3-109">**On-premises servers**</span></span> | <span data-ttu-id="2f9f3-110">[深入了解](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm)內部部署 Hyper-V 主機的需求。</span><span class="sxs-lookup"><span data-stu-id="2f9f3-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for the on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="2f9f3-111">**內部部署 Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="2f9f3-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="2f9f3-112">您想要複寫的 VM 應該執行[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)，也要符合 [Azure 必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="2f9f3-112">VMs you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="2f9f3-113">**Azure URL**</span><span class="sxs-lookup"><span data-stu-id="2f9f3-113">**Azure URLs**</span></span> | <span data-ttu-id="2f9f3-114">Hyper-V 主機需要存取這些 URL：</span><span class="sxs-lookup"><span data-stu-id="2f9f3-114">Hyper-V hosts need access to these URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="2f9f3-115">如果您有以 IP 位址為基礎的防火牆規則，請確定這些規則允許對 Azure 的通訊。</span><span class="sxs-lookup"><span data-stu-id="2f9f3-115">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span><br/></br> <span data-ttu-id="2f9f3-116">允許 [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)和 HTTPS (443) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="2f9f3-116">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="2f9f3-117">允許訂用帳戶的 Azure 區域和美國西部使用 IP 位址範圍 (用於存取控制和身分識別管理)。</span><span class="sxs-lookup"><span data-stu-id="2f9f3-117">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="2f9f3-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2f9f3-118">Next steps</span></span>

- <span data-ttu-id="2f9f3-119">如果您要進行完整部署，請移至[步驟 3：規劃容量](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="2f9f3-119">If you're doing a full deployment, go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="2f9f3-120">如果您要進行簡單的測試部署，請移至[步驟 4：規劃網路](hyper-v-site-walkthrough-network.md)。</span><span class="sxs-lookup"><span data-stu-id="2f9f3-120">If you're doing a simple test deployment, go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
