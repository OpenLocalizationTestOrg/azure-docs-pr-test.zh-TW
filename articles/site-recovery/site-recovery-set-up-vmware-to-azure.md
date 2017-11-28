---
title: "設定來源環境 (從 VMware 到 Azure) | Microsoft Docs"
description: "此文章說明如何設定您的內部部署環境，以開始將 VMware 虛擬機器複寫到 Azure。"
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: a2fabc56463c8cbf0b8a76b7a84369ed8e535486
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-the-source-environment-vmware-to-azure"></a><span data-ttu-id="33fa1-103">設定來源環境 (從 VMware 到 Azure)</span><span class="sxs-lookup"><span data-stu-id="33fa1-103">Set up the source environment (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33fa1-104">VMware 至 Azure</span><span class="sxs-lookup"><span data-stu-id="33fa1-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="33fa1-105">實體至 Azure</span><span class="sxs-lookup"><span data-stu-id="33fa1-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="33fa1-106">此文章說明如何設定您的內部部署環境，以開始將在 VMware 上執行的虛擬機器複寫到 Azure。</span><span class="sxs-lookup"><span data-stu-id="33fa1-106">This article describes how to set up your on-premises environment to start replicating virtual machines running on VMware to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33fa1-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="33fa1-107">Prerequisites</span></span>

<span data-ttu-id="33fa1-108">此文章假設您已經建立：</span><span class="sxs-lookup"><span data-stu-id="33fa1-108">The article assumes that you have already created:</span></span>
- <span data-ttu-id="33fa1-109">[Azure 入口網站](http://portal.azure.com "Azure 入口網站")中的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="33fa1-109">A Recovery Services Vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="33fa1-110">您 VMware vCenter 中可用來進行[自動探索](./site-recovery-vmware-to-azure.md)的專用帳戶。</span><span class="sxs-lookup"><span data-stu-id="33fa1-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="33fa1-111">可供安裝組態伺服器的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="33fa1-111">A virtual machine on which to install the configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="33fa1-112">組態伺服器最低需求</span><span class="sxs-lookup"><span data-stu-id="33fa1-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="33fa1-113">組態伺服器軟體應該部署在具有高可用性的 VMware 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="33fa1-113">The configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="33fa1-114">下表列出組態伺服器的最低硬體、軟體與網路需求。</span><span class="sxs-lookup"><span data-stu-id="33fa1-114">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="33fa1-115">組態伺服器不支援 HTTPS 型 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="33fa1-115">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="33fa1-116">選擇您的保護目標</span><span class="sxs-lookup"><span data-stu-id="33fa1-116">Choose your protection goals</span></span>

1. <span data-ttu-id="33fa1-117">在 Azure 入口網站中，移至 [復原服務] 保存庫刀鋒視窗，然後選取您的保存庫。</span><span class="sxs-lookup"><span data-stu-id="33fa1-117">In the Azure portal, go to the **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="33fa1-118">在保存庫的 [資源] 功能表上，移至 [快速入門] > [Site Recovery] > [步驟 1: 準備基礎結構] > [保護目標]。</span><span class="sxs-lookup"><span data-stu-id="33fa1-118">On the resource menu of the vault, go to **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![選擇目標](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="33fa1-120">在 [保護目標] 中選取 [至 Azure (To Azure)]，然後選擇 [是，使用 VMware vSphere Hypervisor (Yes, with VMware vSphere Hypervisor)]。</span><span class="sxs-lookup"><span data-stu-id="33fa1-120">In **Protection goal**, select **To Azure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="33fa1-121">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="33fa1-121">Then click **OK**.</span></span>

    ![選擇目標](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="33fa1-123">設定來源環境</span><span class="sxs-lookup"><span data-stu-id="33fa1-123">Set up the source environment</span></span>
<span data-ttu-id="33fa1-124">設定來源環境涉及兩個主要活動：</span><span class="sxs-lookup"><span data-stu-id="33fa1-124">Setting up the source environment involves two main activities:</span></span>

- <span data-ttu-id="33fa1-125">安裝組態伺服器並向 Site Recovery 服務註冊。</span><span class="sxs-lookup"><span data-stu-id="33fa1-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="33fa1-126">將 Site Recovery 連接到內部部署 VMware vCenter 或 vSphere EXSi 主機以探索內部部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="33fa1-126">Discover your on-premises virtual machines by connecting Site Recovery to your on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="33fa1-127">步驟 1：安裝及註冊組態伺服器</span><span class="sxs-lookup"><span data-stu-id="33fa1-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="33fa1-128">按一下 [步驟 1：準備基礎結構]  >  [來源]。</span><span class="sxs-lookup"><span data-stu-id="33fa1-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="33fa1-129">在 [準備來源] 中，如果您沒有組態伺服器，請按一下 [+組態伺服器] 來新增一部組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="33fa1-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

    ![設定來源](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="33fa1-131">在 [新增伺服器] 刀鋒視窗中，檢查 [組態伺服器] 是否出現在 [伺服器類型] 中。</span><span class="sxs-lookup"><span data-stu-id="33fa1-131">On the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="33fa1-132">下載 Site Recovery 統一安裝的安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="33fa1-132">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="33fa1-133">下載保存庫註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="33fa1-133">Download the vault registration key.</span></span> <span data-ttu-id="33fa1-134">執行「整合安裝」時，您需要該註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="33fa1-134">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="33fa1-135">該金鑰在產生後會維持 5 天有效。</span><span class="sxs-lookup"><span data-stu-id="33fa1-135">The key is valid for five days after you generate it.</span></span>

    ![設定來源](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="33fa1-137">在作為組態伺服器的電腦上，執行「Azure Site Recovery 整合安裝」，以安裝組態伺服器、處理伺服器和主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="33fa1-137">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="33fa1-138">執行 Azure Site Recovery 統一安裝</span><span class="sxs-lookup"><span data-stu-id="33fa1-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="33fa1-139">如果您電腦系統時鐘的時間與當地時間差五分鐘以上，組態伺服器註冊將會失敗。</span><span class="sxs-lookup"><span data-stu-id="33fa1-139">Configuration server registration fails if the time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="33fa1-140">開始安裝之前，請先將系統時鐘與[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)同步。</span><span class="sxs-lookup"><span data-stu-id="33fa1-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="33fa1-141">您可以透過命令列安裝組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="33fa1-141">The configuration server can be installed via command line.</span></span> <span data-ttu-id="33fa1-142">如需詳細資訊，請參閱[使用命令列工具安裝組態伺服器](http://aka.ms/installconfigsrv)。</span><span class="sxs-lookup"><span data-stu-id="33fa1-142">For more information, see [Installing the configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-the-vmware-account-for-automatic-discovery"></a><span data-ttu-id="33fa1-143">新增用於自動探索的 VMware 帳戶</span><span class="sxs-lookup"><span data-stu-id="33fa1-143">Add the VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="33fa1-144">步驟 2：新增 vCenter</span><span class="sxs-lookup"><span data-stu-id="33fa1-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="33fa1-145">若要允許 Azure Site Recovery 探索在您內部部署環境中執行的虛擬機器，您必須將 VMware vCenter Server 或 vSphere ESXi 主機與 Site Recovery 連接。</span><span class="sxs-lookup"><span data-stu-id="33fa1-145">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="33fa1-146">選取 [+vCenter] 來開始連接 VMware vCenter Server 或 VMware vSphere ESXi 主機。</span><span class="sxs-lookup"><span data-stu-id="33fa1-146">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="33fa1-147">常見問題</span><span class="sxs-lookup"><span data-stu-id="33fa1-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="33fa1-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33fa1-148">Next steps</span></span>
<span data-ttu-id="33fa1-149">在 Azure 中[設定您的目標環境](./site-recovery-prepare-target-vmware-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="33fa1-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
