---
title: "Azure 的區域之間 aaaMigrate Azure IaaS Vm |Microsoft 文件"
description: "使用 Azure Site Recovery toomigrate Azure IaaS 虛擬機器從一個 Azure 區域 tooanother。"
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
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="3d019-103">使用 Azure Site Recovery 在 Azure 區域之間移轉 Azure IaaS 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="3d019-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="3d019-104">概觀</span><span class="sxs-lookup"><span data-stu-id="3d019-104">Overview</span></span>
<span data-ttu-id="3d019-105">歡迎使用 tooAzure Site Recovery ！</span><span class="sxs-lookup"><span data-stu-id="3d019-105">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="3d019-106">如果您想 toomigrate Azure Vm 之間的 Azure 區域，請使用本文章。</span><span class="sxs-lookup"><span data-stu-id="3d019-106">Use this article if you want toomigrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="3d019-107">開始之前，請注意：</span><span class="sxs-lookup"><span data-stu-id="3d019-107">Before you start, note that:</span></span>

* <span data-ttu-id="3d019-108">Azure 建立和處理資源的部署模型有二種：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="3d019-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="3d019-109">Azure 也有兩個入口網站 – hello Azure 傳統入口網站支援 hello 傳統部署模型，與 hello Azure 入口網站支援這兩種部署模型。</span><span class="sxs-lookup"><span data-stu-id="3d019-109">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="3d019-110">hello 基本步驟移轉為 hello 相同是否您在資源管理員 」 或 「 傳統中設定站台復原。</span><span class="sxs-lookup"><span data-stu-id="3d019-110">hello basic steps for migration are hello same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="3d019-111">不過 hello UI 指示和本文中的螢幕擷取畫面相關 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3d019-111">However hello UI instructions and screenshots in this article are relevant for hello Azure portal.</span></span>
* <span data-ttu-id="3d019-112">**目前您可以只從移轉一個區域 tooanother。您可以從一個 Azure 區域 tooanother，容錯移轉 Vm，但您無法回復它們一次。**</span><span class="sxs-lookup"><span data-stu-id="3d019-112">**Currently you can only migrate from one region tooanother. You can fail over VMs from one Azure region tooanother, but you can't fail them back again.**</span></span>

<span data-ttu-id="3d019-113">將任何註解或問題張貼在本文中，或在 hello hello 下方[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="3d019-113">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d019-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="3d019-114">Prerequisites</span></span>
<span data-ttu-id="3d019-115">以下是您針對此部署所需要的項目︰</span><span class="sxs-lookup"><span data-stu-id="3d019-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="3d019-116">**IaaS 虛擬機器**: hello 想 toomigrate 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="3d019-116">**IaaS virtual machines**: hello VMs you want toomigrate.</span></span> <span data-ttu-id="3d019-117">您可以將那些 VM 視為實體機器來移轉它們。</span><span class="sxs-lookup"><span data-stu-id="3d019-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="3d019-118">部署步驟</span><span class="sxs-lookup"><span data-stu-id="3d019-118">Deployment steps</span></span>
<span data-ttu-id="3d019-119">本章節描述 hello hello 新版 Azure 入口網站中的部署步驟。</span><span class="sxs-lookup"><span data-stu-id="3d019-119">This section describes hello deployment steps in hello new Azure portal.</span></span>

1. <span data-ttu-id="3d019-120">[建立保存庫](site-recovery-vmware-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="3d019-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="3d019-121">[啟用複寫](site-recovery-vmware-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="3d019-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="3d019-122">啟用複寫 hello toomigrate，並選擇做為來源的 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="3d019-122">Enable replication for hello VMs you want toomigrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="3d019-123">[ 執行非計劃性容錯移轉](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="3d019-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="3d019-124">完成初始複寫之後，您可以從一個 Azure 區域 tooanother 執行未規劃的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="3d019-124">After initial replication is complete, you can run an unplanned failover from one Azure region tooanother.</span></span> <span data-ttu-id="3d019-125">（選擇性） 您可以建立復原計劃及執行非計劃性容錯移轉 toomigrate 區域之間的多部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3d019-125">Optionally, you can create a recovery plan and run an unplanned failover, toomigrate multiple virtual machines between regions.</span></span> <span data-ttu-id="3d019-126">[深入了解](site-recovery-create-recovery-plans.md) 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="3d019-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d019-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d019-127">Next steps</span></span>
<span data-ttu-id="3d019-128">在 [什麼是 Azure Site Recovery？](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3d019-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
