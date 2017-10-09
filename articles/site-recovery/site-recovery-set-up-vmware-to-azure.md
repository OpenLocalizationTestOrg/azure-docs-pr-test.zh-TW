---
title: "設定 hello 來源環境 (VMware tooAzure) |Microsoft 文件"
description: "本文說明如何 tooset 上您在內部部署環境 toostart 複寫 VMware 虛擬機器 tooAzure。"
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a><span data-ttu-id="81e7e-103">設定 hello 來源環境 (VMware tooAzure)</span><span class="sxs-lookup"><span data-stu-id="81e7e-103">Set up hello source environment (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="81e7e-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="81e7e-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="81e7e-105">實體 tooAzure</span><span class="sxs-lookup"><span data-stu-id="81e7e-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="81e7e-106">本文說明如何 tooset 上您在內部部署環境 toostart 複寫虛擬機器正在執行 VMware tooAzure 上。</span><span class="sxs-lookup"><span data-stu-id="81e7e-106">This article describes how tooset up your on-premises environment toostart replicating virtual machines running on VMware tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81e7e-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="81e7e-107">Prerequisites</span></span>

<span data-ttu-id="81e7e-108">hello 文件假設您已經建立：</span><span class="sxs-lookup"><span data-stu-id="81e7e-108">hello article assumes that you have already created:</span></span>
- <span data-ttu-id="81e7e-109">復原服務保存庫中 hello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="81e7e-109">A Recovery Services Vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="81e7e-110">您 VMware vCenter 中可用來進行[自動探索](./site-recovery-vmware-to-azure.md)的專用帳戶。</span><span class="sxs-lookup"><span data-stu-id="81e7e-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="81e7e-111">哪些 tooinstall hello 組態伺服器上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="81e7e-111">A virtual machine on which tooinstall hello configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="81e7e-112">組態伺服器最低需求</span><span class="sxs-lookup"><span data-stu-id="81e7e-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="81e7e-113">hello 設定伺服器軟體應該部署在高可用性的 VMware 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="81e7e-113">hello configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="81e7e-114">hello 下表列出 hello 最低硬體、 軟體和組態伺服器的網路需求。</span><span class="sxs-lookup"><span data-stu-id="81e7e-114">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="81e7e-115">Hello 組態伺服器不支援 HTTPS 為基礎的 proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="81e7e-115">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="81e7e-116">選擇您的保護目標</span><span class="sxs-lookup"><span data-stu-id="81e7e-116">Choose your protection goals</span></span>

1. <span data-ttu-id="81e7e-117">在 hello Azure 入口網站，移 toohello**復原服務**保存庫刀鋒視窗，並選取您的保存庫。</span><span class="sxs-lookup"><span data-stu-id="81e7e-117">In hello Azure portal, go toohello **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="81e7e-118">在 hello hello 保存庫的資源功能表上，前往 太**入門** > **Site Recovery** > **步驟 1： 準備基礎結構** > **保護目標**。</span><span class="sxs-lookup"><span data-stu-id="81e7e-118">On hello resource menu of hello vault, go too**Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![選擇目標](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="81e7e-120">在**保護目標**，選取**tooAzure**，然後選擇 **是的與 VMware vSphere Hypervisor**。</span><span class="sxs-lookup"><span data-stu-id="81e7e-120">In **Protection goal**, select **tooAzure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="81e7e-121">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="81e7e-121">Then click **OK**.</span></span>

    ![選擇目標](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="81e7e-123">設定 hello 來源環境</span><span class="sxs-lookup"><span data-stu-id="81e7e-123">Set up hello source environment</span></span>
<span data-ttu-id="81e7e-124">設定 hello 來源環境牽涉到兩個主要的活動：</span><span class="sxs-lookup"><span data-stu-id="81e7e-124">Setting up hello source environment involves two main activities:</span></span>

- <span data-ttu-id="81e7e-125">安裝組態伺服器並向 Site Recovery 服務註冊。</span><span class="sxs-lookup"><span data-stu-id="81e7e-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="81e7e-126">探索您的內部部署虛擬機器連線站台復原 tooyour 在內部部署 VMware vCenter 或 vSphere EXSi 主機。</span><span class="sxs-lookup"><span data-stu-id="81e7e-126">Discover your on-premises virtual machines by connecting Site Recovery tooyour on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="81e7e-127">步驟 1：安裝及註冊組態伺服器</span><span class="sxs-lookup"><span data-stu-id="81e7e-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="81e7e-128">按一下 [步驟 1：準備基礎結構]  >  [來源]。</span><span class="sxs-lookup"><span data-stu-id="81e7e-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="81e7e-129">在**準備來源**，如果您不需要設定伺服器，按一下  **+ 設定伺服器**tooadd 其中一個。</span><span class="sxs-lookup"><span data-stu-id="81e7e-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

    ![設定來源](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="81e7e-131">在 hello**新增伺服器**刀鋒視窗中，請檢查**組態伺服器**會出現在**伺服器類型**。</span><span class="sxs-lookup"><span data-stu-id="81e7e-131">On hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="81e7e-132">下載 hello Site Recovery 整合安裝程式安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="81e7e-132">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="81e7e-133">下載 hello 保存庫註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="81e7e-133">Download hello vault registration key.</span></span> <span data-ttu-id="81e7e-134">當您執行整合安裝程式時，您會需要 hello 註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="81e7e-134">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="81e7e-135">hello 金鑰有效期為您產生它之後的五天。</span><span class="sxs-lookup"><span data-stu-id="81e7e-135">hello key is valid for five days after you generate it.</span></span>

    ![設定來源](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="81e7e-137">在您使用當作 hello 組態伺服器 hello 機器上執行**Azure Site Recovery 整合安裝**tooinstall hello 組態伺服器、 hello 處理序伺服器和 hello 主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="81e7e-137">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="81e7e-138">執行 Azure Site Recovery 統一安裝</span><span class="sxs-lookup"><span data-stu-id="81e7e-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="81e7e-139">如果您電腦的系統時鐘 hello 時間不同於當地時間超過五分鐘，組態伺服器註冊將會失敗。</span><span class="sxs-lookup"><span data-stu-id="81e7e-139">Configuration server registration fails if hello time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="81e7e-140">同步處理您的系統時鐘與[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)開始 hello 安裝之前。</span><span class="sxs-lookup"><span data-stu-id="81e7e-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="81e7e-141">hello 組態伺服器可以透過命令列安裝。</span><span class="sxs-lookup"><span data-stu-id="81e7e-141">hello configuration server can be installed via command line.</span></span> <span data-ttu-id="81e7e-142">如需詳細資訊，請參閱[安裝 hello 設定伺服器使用命令列工具](http://aka.ms/installconfigsrv)。</span><span class="sxs-lookup"><span data-stu-id="81e7e-142">For more information, see [Installing hello configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a><span data-ttu-id="81e7e-143">新增自動探索的 hello VMware 帳戶</span><span class="sxs-lookup"><span data-stu-id="81e7e-143">Add hello VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="81e7e-144">步驟 2：新增 vCenter</span><span class="sxs-lookup"><span data-stu-id="81e7e-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="81e7e-145">在內部部署環境中執行 tooallow Azure Site Recovery toodiscover 虛擬機器，您需要 tooconnect，您的 VMware vCenter Server 或 vSphere ESXi 主機與 Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="81e7e-145">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="81e7e-146">選取**+ vCenter** toostart VMware vCenter server 或 VMware vSphere ESXi 主機連接。</span><span class="sxs-lookup"><span data-stu-id="81e7e-146">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="81e7e-147">常見問題</span><span class="sxs-lookup"><span data-stu-id="81e7e-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="81e7e-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81e7e-148">Next steps</span></span>
<span data-ttu-id="81e7e-149">在 Azure 中[設定您的目標環境](./site-recovery-prepare-target-vmware-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="81e7e-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
