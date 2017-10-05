---
title: "在 Azure 區域之間移轉 Azure IaaS VM | Microsoft Docs"
description: "使用 Azure Site Recovery，將 Azure IaaS 虛擬機器從一個 Azure 區域移轉到另一個區域。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: ef2972c077a2b1dd2b2fd6ce53cc6560520ea870
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="6103f-103">使用 Azure Site Recovery 在 Azure 區域之間移轉 Azure IaaS 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6103f-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="6103f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="6103f-104">Overview</span></span>
<span data-ttu-id="6103f-105">歡迎使用 Azure Site Recovery！</span><span class="sxs-lookup"><span data-stu-id="6103f-105">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="6103f-106">如果您想要在 Azure 區域之間移轉 Azure VM，請使用本文。</span><span class="sxs-lookup"><span data-stu-id="6103f-106">Use this article if you want to migrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="6103f-107">開始之前，請注意：</span><span class="sxs-lookup"><span data-stu-id="6103f-107">Before you start, note that:</span></span>

* <span data-ttu-id="6103f-108">Azure 建立和處理資源的部署模型有二種：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="6103f-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="6103f-109">Azure 也有兩個入口網站 – 支援傳統部署模型的 Azure 傳統入口網站，以及支援兩種部署模型的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6103f-109">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="6103f-110">無論您是在 Resource Manager 還是傳統中設定 Site Recovery，基本的移轉步驟都是相同的。</span><span class="sxs-lookup"><span data-stu-id="6103f-110">The basic steps for migration are the same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="6103f-111">不過本文中的 UI 指示和螢幕擷取畫面都是和 Azure 入口網站相關。</span><span class="sxs-lookup"><span data-stu-id="6103f-111">However the UI instructions and screenshots in this article are relevant for the Azure portal.</span></span>
* <span data-ttu-id="6103f-112">**目前您只能從一個區域移轉到另一個區域。您可以將 VM 從一個 Azure 區域容錯移轉至另一個，但是無法將它們容錯移轉回來。**</span><span class="sxs-lookup"><span data-stu-id="6103f-112">**Currently you can only migrate from one region to another. You can fail over VMs from one Azure region to another, but you can't fail them back again.**</span></span>

<span data-ttu-id="6103f-113">在這篇文章下方或 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)中張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="6103f-113">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6103f-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="6103f-114">Prerequisites</span></span>
<span data-ttu-id="6103f-115">以下是您針對此部署所需要的項目︰</span><span class="sxs-lookup"><span data-stu-id="6103f-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="6103f-116">**IaaS 虛擬機器**：您想要移轉的 VM。</span><span class="sxs-lookup"><span data-stu-id="6103f-116">**IaaS virtual machines**: The VMs you want to migrate.</span></span> <span data-ttu-id="6103f-117">您可以將那些 VM 視為實體機器來移轉它們。</span><span class="sxs-lookup"><span data-stu-id="6103f-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="6103f-118">部署步驟</span><span class="sxs-lookup"><span data-stu-id="6103f-118">Deployment steps</span></span>
<span data-ttu-id="6103f-119">本節描述新 Azure 入口網站中的部署步驟。</span><span class="sxs-lookup"><span data-stu-id="6103f-119">This section describes the deployment steps in the new Azure portal.</span></span>

1. <span data-ttu-id="6103f-120">[建立保存庫](site-recovery-vmware-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="6103f-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="6103f-121">[啟用複寫](site-recovery-vmware-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="6103f-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="6103f-122">針對您想要移轉的虛擬機器啟用複寫，並選擇 Azure 做為來源。</span><span class="sxs-lookup"><span data-stu-id="6103f-122">Enable replication for the VMs you want to migrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="6103f-123">[ 執行非計劃性容錯移轉](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="6103f-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="6103f-124">初始複寫完成之後，您可以執行從一個 Azure 區域到另一個區域的非計劃性容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="6103f-124">After initial replication is complete, you can run an unplanned failover from one Azure region to another.</span></span> <span data-ttu-id="6103f-125">(選擇性) 您可以建立復原計劃並執行非計劃性容錯移轉，在區域與區域之間移轉多部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6103f-125">Optionally, you can create a recovery plan and run an unplanned failover, to migrate multiple virtual machines between regions.</span></span> <span data-ttu-id="6103f-126">[深入了解](site-recovery-create-recovery-plans.md) 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="6103f-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6103f-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6103f-127">Next steps</span></span>
<span data-ttu-id="6103f-128">在 [什麼是 Azure Site Recovery？](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6103f-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
