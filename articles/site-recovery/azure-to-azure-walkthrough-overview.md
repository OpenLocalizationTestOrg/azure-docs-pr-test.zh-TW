---
title: "Azure 的區域之間的 Azure Vm aaaReplicate |Microsoft 文件 '"
description: "摘要說明 hello 步驟需要的 tooreplicate Azure Vm 與 hello Azure 入口網站中的 hello Azure Site Recovery 服務的 Azure 區域之間"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="ce0d7-103">使用 Azure Site Recovery 在區域之間椱寫 Azure VM</span><span class="sxs-lookup"><span data-stu-id="ce0d7-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="ce0d7-104">本文章提供 Azure 虛擬機器 (Vm) 在一個 Azure 區域 tooAzure Vm 位於不同的區域中的 hello 步驟需要 tooreplicate 的概觀。</span><span class="sxs-lookup"><span data-stu-id="ce0d7-104">This article provides an overview of hello steps required tooreplicate Azure virtual machines (VMs) in one Azure region tooAzure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="ce0d7-105">Azure VM 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="ce0d7-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="ce0d7-106">在這份文件或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="ce0d7-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="ce0d7-107">步驟 1：檢閱架構</span><span class="sxs-lookup"><span data-stu-id="ce0d7-107">Step 1: Review architecture</span></span>

<span data-ttu-id="ce0d7-108">在開始部署之前，檢閱 hello 案例架構和您需要 toodeploy hello 元件。</span><span class="sxs-lookup"><span data-stu-id="ce0d7-108">Before you start deployment, review hello scenario architecture, and hello components you need toodeploy.</span></span>

<span data-ttu-id="ce0d7-109">跳過[步驟 1： 檢閱 hello 架構](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="ce0d7-109">Go too[Step 1: Review hello architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="ce0d7-110">步驟 2：檢閱必要條件</span><span class="sxs-lookup"><span data-stu-id="ce0d7-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="ce0d7-111">請檢查您擁有 hello Azure 位置，包括訂用帳戶、 虛擬網路、 儲存體帳戶和 VM 需求中的必要條件。</span><span class="sxs-lookup"><span data-stu-id="ce0d7-111">Check that you have hello Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="ce0d7-112">跳過[步驟 2： 確認必要條件和限制](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="ce0d7-112">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="ce0d7-113">步驟 3：規劃網路服務</span><span class="sxs-lookup"><span data-stu-id="ce0d7-113">Step 3: Plan networking</span></span>

<span data-ttu-id="ce0d7-114">請檢查要 tooreplicate，以及從內部部署連線所設定的 Azure Vm 上的傳出連線已設定。</span><span class="sxs-lookup"><span data-stu-id="ce0d7-114">Check that outbound connectivity is set up on Azure VMs you want tooreplicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="ce0d7-115">跳過[步驟 4： 規劃的網路功能](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="ce0d7-115">Go too[Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="ce0d7-116">步驟 4：建立保存庫</span><span class="sxs-lookup"><span data-stu-id="ce0d7-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="ce0d7-117">您需要註冊復原服務保存庫 tooorchestrate tooset 和管理複寫，並指定 hello 來源地區。</span><span class="sxs-lookup"><span data-stu-id="ce0d7-117">You need tooset up a Recovery Services vault tooorchestrate and manage replication, and specify hello source region.</span></span>

<span data-ttu-id="ce0d7-118">跳過[步驟 4： 建立保存庫](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="ce0d7-118">Go too[Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="ce0d7-119">步驟 5：啟用複寫</span><span class="sxs-lookup"><span data-stu-id="ce0d7-119">Step 5: Enable replication</span></span>


<span data-ttu-id="ce0d7-120">tooenable 複寫，您設定目標位置設定，設定複寫原則，並選取您想 tooreplicate hello Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="ce0d7-120">tooenable replication, you configure target location settings, set up a replication policy, and select hello Azure VMs that you want tooreplicate.</span></span> <span data-ttu-id="ce0d7-121">啟用之後，就會發生 hello VM 的初始複寫。</span><span class="sxs-lookup"><span data-stu-id="ce0d7-121">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="ce0d7-122">跳過[步驟 5： 啟用複寫](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ce0d7-122">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="ce0d7-123">步驟 6：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="ce0d7-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="ce0d7-124">初始複寫完成，並執行差異複寫之後，您可以執行測試容錯移轉 toomake 確定一切如預期運作。</span><span class="sxs-lookup"><span data-stu-id="ce0d7-124">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="ce0d7-125">跳過[步驟 6： 執行測試容錯移轉](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="ce0d7-125">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


