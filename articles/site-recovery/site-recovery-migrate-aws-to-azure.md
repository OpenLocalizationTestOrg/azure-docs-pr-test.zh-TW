---
title: "將 VM 從 AWS 移轉到 Azure| Microsoft Docs"
description: "本文說明如何使用 Azure Site Recovery 將 Amazon Web Services (AWS) 中執行的虛擬機器移轉至 Azure。"
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
ms.openlocfilehash: b3c0727a279649f4f7dae30d41027129ce5b04ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-to-azure-with-azure-site-recovery"></a><span data-ttu-id="482f5-103">使用 Azure Site Recovery 將 Amazon Web Services (AWS) 中的虛擬機器移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="482f5-103">Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery</span></span>

<span data-ttu-id="482f5-104">本文說明如何使用 [Azure Site Recovery](site-recovery-overview.md) 服務將 AWS Windows 執行個體移轉到 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="482f5-104">This article describes how to migrate AWS Windows instances to Azure virtual machines with the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="482f5-105">移轉實際上是從 AWS 容錯移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="482f5-105">Migration is effectively a failover from AWS to Azure.</span></span> <span data-ttu-id="482f5-106">您無法從機器容錯移轉至 AWS，且不會進行複寫。</span><span class="sxs-lookup"><span data-stu-id="482f5-106">You can't failback machines to AWS, and there's no ongoing replication.</span></span> <span data-ttu-id="482f5-107">本文說明在 Azure 入口網站中進行移轉的步驟，且是以[將實體機器複寫到 Azure](site-recovery-vmware-to-azure.md)的指示為基礎。</span><span class="sxs-lookup"><span data-stu-id="482f5-107">This article describes the steps for migration in the Azure portal, and are based on the instructions for [replicating a physical machine to Azure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="482f5-108">請在這篇文章下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="482f5-108">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="482f5-109">受支援的作業系統</span><span class="sxs-lookup"><span data-stu-id="482f5-109">Supported operating systems</span></span>

<span data-ttu-id="482f5-110">Site Recovery 可用於移轉執行下列任何作業系統的 EC2 執行個體：</span><span class="sxs-lookup"><span data-stu-id="482f5-110">Site Recovery can be used to migrate EC2 instances running any of the following operating systems:</span></span>

- <span data-ttu-id="482f5-111">Windows (僅 64 位元)</span><span class="sxs-lookup"><span data-stu-id="482f5-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="482f5-112">Windows Server 2008 R2 SP1+ (僅限 Citrix PV 驅動程式或 AWS PV 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="482f5-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="482f5-113">**不支援執行 RedHat PV 驅動程式的執行個體**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="482f5-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="482f5-114">Linux (僅 64 位元)</span><span class="sxs-lookup"><span data-stu-id="482f5-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="482f5-115">Red Hat Enterprise Linux 6.7 (只有 HVM 虛擬化執行個體)</span><span class="sxs-lookup"><span data-stu-id="482f5-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="482f5-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="482f5-116">Prerequisites</span></span>

<span data-ttu-id="482f5-117">以下是您針對此部署所需要的項目︰</span><span class="sxs-lookup"><span data-stu-id="482f5-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="482f5-118">**組態伺服器**︰執行 Windows Server 2012 R2 的 Amazon EC2 VM 部署為組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="482f5-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as the configuration server.</span></span> <span data-ttu-id="482f5-119">根據預設，當您部署設定伺服器時，會安裝其他 Azure Site Recovery 元件 (處理序伺服器和主要目標伺服器)。</span><span class="sxs-lookup"><span data-stu-id="482f5-119">By default, the other Azure Site Recovery components (process server and master target server) are installed when you deploy the configuration server.</span></span> <span data-ttu-id="482f5-120">本文說明在 Azure 入口網站中進行移轉的步驟，且是以[進一步了解](site-recovery-components.md)的指示為基礎</span><span class="sxs-lookup"><span data-stu-id="482f5-120">This article describes the steps for migration in the Azure portal, and are based on the instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="482f5-121">**EC2 執行個體**︰您想要移轉的 Amazon EC2 虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="482f5-121">**EC2 instances**: The Amazon EC2 virtual machines instances that you want to migrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="482f5-122">部署步驟</span><span class="sxs-lookup"><span data-stu-id="482f5-122">Deployment steps</span></span>

1. <span data-ttu-id="482f5-123">建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="482f5-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="482f5-124">EC2 執行個體的安全性群組應該有設定的規則，允許您要移轉的 EC2 執行個體與您打算部署設定伺服器的執行個體之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="482f5-124">The Security Group of your EC2 instances should have rules configured to allow communication between the EC2 instance that you want to migrate, and the instance on which you plan to deploy the Configuration Server.</span></span>

3. <span data-ttu-id="482f5-125">在與 EC2 執行個體相同的 Amazon 虛擬私人雲端上，部署 Azure Site Recovery 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="482f5-125">On the same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="482f5-126">關於組態伺服器部署需求，請參閱 Azure 的 VMware/實體必要條件。</span><span class="sxs-lookup"><span data-stu-id="482f5-126">Refer the VMware / Physical to Azure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="482f5-128">一旦將組態伺服器部署在 AWS 中，並向您的復原服務保存庫註冊後，您應該會在 Site Recovery 基礎結構下看到組態伺服器和處理序伺服器，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="482f5-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see the configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="482f5-130">部署組態伺服器之後 (可能需要長達 15 分鐘才會出現)，請驗證該伺服器否能夠與您要移轉的 VM 通訊。</span><span class="sxs-lookup"><span data-stu-id="482f5-130">After you've deployed the configuration server (it might take up to 15 minustes for it to appear), validate that it can communicate with the VMs that you want to migrate.</span></span>

6. <span data-ttu-id="482f5-131">[設定複寫設定](site-recovery-setup-replication-settings-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="482f5-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="482f5-132">啟用複寫：針對您想要移轉的 VM 啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="482f5-132">Enable replication: Enable replication for the VMs you want to migrate.</span></span> <span data-ttu-id="482f5-133">您可以使用可從 EC2 主控台取得的私人 IP 位址探索 EC2 執行個體。</span><span class="sxs-lookup"><span data-stu-id="482f5-133">You can discover the EC2 instances using the private IP addresses, which you can get from the EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="482f5-135">一旦 EC2 執行個體已受保護，且複寫至 Azure 完成後，在 Azure 中[執行測試容錯移轉](site-recovery-test-failover-to-azure.md)來驗證您的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="482f5-135">Once the EC2 instances have been protected and the replication to Azure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) to validate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="482f5-137">為每個 VM 執行從 AWS 容錯移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="482f5-137">Run a Failover from AWS to Azure for each VM.</span></span> <span data-ttu-id="482f5-138">(選擇性) 您可以建立復原計劃並執行容錯移轉，將多部虛擬機器從 AWS 移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="482f5-138">Optionally, you can create a recovery plan and run a Failover, to migrate multiple virtual machines from AWS to Azure.</span></span> <span data-ttu-id="482f5-139">[深入了解](site-recovery-create-recovery-plans.md) 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="482f5-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="482f5-140">若是進行移轉，您不需要認可容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="482f5-140">For migration, you don't need to commit a failover.</span></span> <span data-ttu-id="482f5-141">相反地，您要為所要移轉的每一部機器選取 [完成移轉] 選項。</span><span class="sxs-lookup"><span data-stu-id="482f5-141">Instead, you select the Complete Migration option for each machine you want to migrate.</span></span> <span data-ttu-id="482f5-142">[完成移轉] 動作會完成移轉程序、移除機器的複寫，並停止該機器的 Site Recovery 計費。</span><span class="sxs-lookup"><span data-stu-id="482f5-142">The Complete Migration action finishes up the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

    ![移轉](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="482f5-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="482f5-144">Next steps</span></span>

- <span data-ttu-id="482f5-145">[準備已移轉的機器，以便複寫](site-recovery-azure-to-azure-after-migration.md)至其他區域以因應災害復原的需要。</span><span class="sxs-lookup"><span data-stu-id="482f5-145">[Prepare migrated machines to enable replication](site-recovery-azure-to-azure-after-migration.md) to another region for disaster recovery needs.</span></span>
- <span data-ttu-id="482f5-146">[複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="482f5-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
