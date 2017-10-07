---
title: "從 AWS tooAzure aaaMigrate Vm |Microsoft 文件"
description: "本文說明如何 toomigrate 虛擬機器正在執行中使用 Azure Site Recovery 的 Amazon Web Services (AWS) tooAzure。"
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a><span data-ttu-id="b0616-103">將在 Amazon Web Services (AWS) tooAzure 與 Azure Site Recovery 的虛擬機器移轉</span><span class="sxs-lookup"><span data-stu-id="b0616-103">Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery</span></span>

<span data-ttu-id="b0616-104">本文說明如何 toomigrate AWS Windows 執行個體 tooAzure 虛擬機器以 hello [Azure Site Recovery](site-recovery-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="b0616-104">This article describes how toomigrate AWS Windows instances tooAzure virtual machines with hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="b0616-105">移轉實際上就是從 AWS tooAzure 的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b0616-105">Migration is effectively a failover from AWS tooAzure.</span></span> <span data-ttu-id="b0616-106">您不能容錯回復機器 tooAWS，而且沒有任何進行中的複寫。</span><span class="sxs-lookup"><span data-stu-id="b0616-106">You can't failback machines tooAWS, and there's no ongoing replication.</span></span> <span data-ttu-id="b0616-107">本文描述 hello hello Azure 入口網站中針對移轉的步驟，並為基礎的 hello 指示[複寫實體機器 tooAzure](site-recovery-vmware-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="b0616-107">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for [replicating a physical machine tooAzure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="b0616-108">將任何註解或問題張貼在本文中，或在 hello hello 下方[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="b0616-108">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="b0616-109">受支援的作業系統</span><span class="sxs-lookup"><span data-stu-id="b0616-109">Supported operating systems</span></span>

<span data-ttu-id="b0616-110">使用的 toomigrate EC2 情況下執行任何 hello 下列作業系統時，可能是站台復原：</span><span class="sxs-lookup"><span data-stu-id="b0616-110">Site Recovery can be used toomigrate EC2 instances running any of hello following operating systems:</span></span>

- <span data-ttu-id="b0616-111">Windows (僅 64 位元)</span><span class="sxs-lookup"><span data-stu-id="b0616-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="b0616-112">Windows Server 2008 R2 SP1+ (僅限 Citrix PV 驅動程式或 AWS PV 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="b0616-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="b0616-113">**不支援執行 RedHat PV 驅動程式的執行個體**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b0616-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="b0616-114">Linux (僅 64 位元)</span><span class="sxs-lookup"><span data-stu-id="b0616-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="b0616-115">Red Hat Enterprise Linux 6.7 (只有 HVM 虛擬化執行個體)</span><span class="sxs-lookup"><span data-stu-id="b0616-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0616-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="b0616-116">Prerequisites</span></span>

<span data-ttu-id="b0616-117">以下是您針對此部署所需要的項目︰</span><span class="sxs-lookup"><span data-stu-id="b0616-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="b0616-118">**設定伺服器**： 執行 Windows Server 2012 R2 的 Amazon EC2 VM 部署為 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="b0616-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as hello configuration server.</span></span> <span data-ttu-id="b0616-119">根據預設，hello （處理序伺服器和主要目標伺服器） 的其他 Azure Site Recovery 元件會安裝部署 hello 組態伺服器時。</span><span class="sxs-lookup"><span data-stu-id="b0616-119">By default, hello other Azure Site Recovery components (process server and master target server) are installed when you deploy hello configuration server.</span></span> <span data-ttu-id="b0616-120">本文描述 hello hello Azure 入口網站中針對移轉的步驟，並為基礎的 hello 指示[進一步了解](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="b0616-120">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="b0616-121">**EC2 執行個體**: hello 的 toomigrate Amazon EC2 虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="b0616-121">**EC2 instances**: hello Amazon EC2 virtual machines instances that you want toomigrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="b0616-122">部署步驟</span><span class="sxs-lookup"><span data-stu-id="b0616-122">Deployment steps</span></span>

1. <span data-ttu-id="b0616-123">建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="b0616-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="b0616-124">hello 安全性群組 EC2 的執行個體應該有您想 toomigrate 和您計劃 toodeploy hello 組態伺服器的 hello 執行個體的 hello EC2 執行個體之間設定的規則 tooallow 通訊。</span><span class="sxs-lookup"><span data-stu-id="b0616-124">hello Security Group of your EC2 instances should have rules configured tooallow communication between hello EC2 instance that you want toomigrate, and hello instance on which you plan toodeploy hello Configuration Server.</span></span>

3. <span data-ttu-id="b0616-125">在 hello 相同 Amazon 虛擬私人雲端與您 EC2 執行個體，部署 ASR 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="b0616-125">On hello same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="b0616-126">請參閱 hello VMware / 實體 tooAzure 組態伺服器部署需求的必要條件。</span><span class="sxs-lookup"><span data-stu-id="b0616-126">Refer hello VMware / Physical tooAzure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="b0616-128">一旦設定伺服器是部署在 AWS，並註冊您的復原服務保存庫，您應該看到 hello 組態伺服器和處理序伺服器在 Site Recovery 基礎結構，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b0616-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see hello configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="b0616-130">您已部署的 hello 組態伺服器之後 (它可能會為其佔用 too15 minustes tooappear)，驗證，它可以您想 toomigrate 通訊與 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="b0616-130">After you've deployed hello configuration server (it might take up too15 minustes for it tooappear), validate that it can communicate with hello VMs that you want toomigrate.</span></span>

6. <span data-ttu-id="b0616-131">[設定複寫設定](site-recovery-setup-replication-settings-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="b0616-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="b0616-132">啟用複寫： hello 想 toomigrate Vm 為啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="b0616-132">Enable replication: Enable replication for hello VMs you want toomigrate.</span></span> <span data-ttu-id="b0616-133">您可以探索使用 hello 私用 IP 位址，您可以從 hello EC2 主控台取得 hello EC2 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b0616-133">You can discover hello EC2 instances using hello private IP addresses, which you can get from hello EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="b0616-135">一旦 hello EC2 執行個體已受保護且 hello 複寫 tooAzure 已完成，[執行測試容錯移轉](site-recovery-test-failover-to-azure.md)toovalidate 在 Azure 中的應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="b0616-135">Once hello EC2 instances have been protected and hello replication tooAzure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) toovalidate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="b0616-137">從 AWS tooAzure 執行容錯移轉，為每個 VM。</span><span class="sxs-lookup"><span data-stu-id="b0616-137">Run a Failover from AWS tooAzure for each VM.</span></span> <span data-ttu-id="b0616-138">（選擇性） 您可以建立復原計劃及執行容錯移轉時，toomigrate AWS tooAzure 從多部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b0616-138">Optionally, you can create a recovery plan and run a Failover, toomigrate multiple virtual machines from AWS tooAzure.</span></span> <span data-ttu-id="b0616-139">[深入了解](site-recovery-create-recovery-plans.md) 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="b0616-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="b0616-140">如需移轉，您不需要 toocommit 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b0616-140">For migration, you don't need toocommit a failover.</span></span> <span data-ttu-id="b0616-141">相反地，您可以選取 hello 完成移轉選項要為每一部機器 toomigrate。</span><span class="sxs-lookup"><span data-stu-id="b0616-141">Instead, you select hello Complete Migration option for each machine you want toomigrate.</span></span> <span data-ttu-id="b0616-142">hello 完成移轉動作完成 hello 移轉程序、 移除 hello 機器的複寫和停止計費 hello 機器的 Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="b0616-142">hello Complete Migration action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

    ![移轉](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="b0616-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b0616-144">Next steps</span></span>

- <span data-ttu-id="b0616-145">[準備移轉的機器 tooenable 複寫](site-recovery-azure-to-azure-after-migration.md)tooanother 嚴重損壞修復所需的區域。</span><span class="sxs-lookup"><span data-stu-id="b0616-145">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="b0616-146">[複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="b0616-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
