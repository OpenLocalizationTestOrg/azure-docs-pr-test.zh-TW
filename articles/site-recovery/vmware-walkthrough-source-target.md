---
title: "hello 來源和目標與 Azure Site Recovery 的 VMware 複寫 tooAzure aaaSet |Microsoft 文件"
description: "摘要說明 hello 步驟 tooset VMware Vm tooAzure 儲存體與 Azure Site Recovery 的複寫的來源和目標設定"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a><span data-ttu-id="5b437-103">步驟 8: Hello 來源和目標 VMware 複寫 tooAzure 設定</span><span class="sxs-lookup"><span data-stu-id="5b437-103">Step 8: Set up hello source and target for VMware replication tooAzure</span></span>

<span data-ttu-id="5b437-104">本文說明如何 tooconfigure 來源和目標設定複寫時 VMware 虛擬機器 tooAzure，使用內部 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="5b437-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="5b437-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="5b437-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="5b437-106">設定 hello 來源環境</span><span class="sxs-lookup"><span data-stu-id="5b437-106">Set up hello source environment</span></span>

<span data-ttu-id="5b437-107">設定 hello 組態伺服器、 其註冊 hello 保存庫，以及探索 Vm。</span><span class="sxs-lookup"><span data-stu-id="5b437-107">Set up hello configuration server, register it in hello vault, and discover VMs.</span></span>

1. <span data-ttu-id="5b437-108">按一下 [Site Recovery] > [步驟 1: 準備基礎結構] > [來源]。</span><span class="sxs-lookup"><span data-stu-id="5b437-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="5b437-109">如果您沒有設定伺服器，請按一下 [+設定伺服器]。</span><span class="sxs-lookup"><span data-stu-id="5b437-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="5b437-110">在 [新增伺服器] 中，檢查 [設定伺服器] 是否出現在 [伺服器類型] 中。</span><span class="sxs-lookup"><span data-stu-id="5b437-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="5b437-111">下載 hello Site Recovery 整合安裝程式安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="5b437-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="5b437-112">下載 hello 保存庫註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="5b437-112">Download hello vault registration key.</span></span> <span data-ttu-id="5b437-113">您會在執行統一安裝時用到此金鑰。</span><span class="sxs-lookup"><span data-stu-id="5b437-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="5b437-114">hello 金鑰有效期為您產生它之後的五天。</span><span class="sxs-lookup"><span data-stu-id="5b437-114">hello key is valid for five days after you generate it.</span></span>

   ![設定來源](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="5b437-116">Hello 保存庫中註冊伺服器 hello 組態</span><span class="sxs-lookup"><span data-stu-id="5b437-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="5b437-117">請勿 hello 下列之前啟動，然後執行整合安裝 tooinstall hello 組態伺服器、 hello 處理序伺服器，以及 hello 主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="5b437-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span>
    - <span data-ttu-id="5b437-118">透過影片快速建立概念</span><span class="sxs-lookup"><span data-stu-id="5b437-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="5b437-119">在 hello 組態伺服器 VM，請確定該 hello 系統時鐘與同步[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)。</span><span class="sxs-lookup"><span data-stu-id="5b437-119">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="5b437-120">應該相符。</span><span class="sxs-lookup"><span data-stu-id="5b437-120">It should match.</span></span> <span data-ttu-id="5b437-121">如果快慢誤差 15 分鐘，安裝可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="5b437-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="5b437-122">以本機系統管理員身分 hello 組態伺服器 VM 上執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="5b437-122">Run setup as a Local Administrator on hello configuration server VM.</span></span>
    - <span data-ttu-id="5b437-123">請確定 hello VM 上啟用 TLS 1.0。</span><span class="sxs-lookup"><span data-stu-id="5b437-123">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="5b437-124">也可以安裝 hello 組態伺服器[hello 命令列從](http://aka.ms/installconfigsrv)。</span><span class="sxs-lookup"><span data-stu-id="5b437-124">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-toovmware-servers"></a><span data-ttu-id="5b437-125">TooVMware 伺服器連線</span><span class="sxs-lookup"><span data-stu-id="5b437-125">Connect tooVMware servers</span></span>

<span data-ttu-id="5b437-126">在內部部署環境中執行 tooallow Azure Site Recovery toodiscover 虛擬機器，您需要 tooconnect，您的 VMware vCenter Server 或 vSphere ESXi 主機與 Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="5b437-126">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="5b437-127">在開始之前，請注意下列 hello:</span><span class="sxs-lookup"><span data-stu-id="5b437-127">Note hello following before you start:</span></span>

- <span data-ttu-id="5b437-128">如果您新增 hello vCenter server 或不具有系統管理員權限的帳戶的 vSphere 主機 tooSite 復原 hello 伺服器上，hello 帳戶必須啟用這些權限：</span><span class="sxs-lookup"><span data-stu-id="5b437-128">If you add hello vCenter server or vSphere hosts tooSite Recovery with an account without administrator privileges on hello server, hello account needs these privileges enabled:</span></span>
    - <span data-ttu-id="5b437-129">資料中心、資料存放區、資料夾、主機、網路、資源、虛擬機器、vSphere 分散式交換器。</span><span class="sxs-lookup"><span data-stu-id="5b437-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="5b437-130">hello vCenter server 必須儲存檢視的權限。</span><span class="sxs-lookup"><span data-stu-id="5b437-130">hello vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="5b437-131">當您新增 VMware 伺服器 tooSite 復原時，可能需要 15 分鐘或更長，tooappear hello 入口網站中的。</span><span class="sxs-lookup"><span data-stu-id="5b437-131">When you add VMware servers tooSite Recovery, it can take 15 minutes or longer for them tooappear in hello portal.</span></span>

### <a name="add-hello-account-for-automatic-discovery"></a><span data-ttu-id="5b437-132">新增自動探索的 hello 帳戶</span><span class="sxs-lookup"><span data-stu-id="5b437-132">Add hello account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="5b437-133">設定連線</span><span class="sxs-lookup"><span data-stu-id="5b437-133">Set up a connection</span></span>

<span data-ttu-id="5b437-134">連接 tooservers，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5b437-134">Connect tooservers as follows:</span></span>

1. <span data-ttu-id="5b437-135">選取**+ vCenter** toostart VMware vCenter server 或 VMware vSphere ESXi 主機連接。</span><span class="sxs-lookup"><span data-stu-id="5b437-135">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="5b437-136">在**新增 vCenter**指定 hello vSphere 主機或 vCenter 伺服器，好記名稱，然後指定 hello IP 位址或 hello 伺服器的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="5b437-136">In **Add vCenter**, specify a friendly name for hello vSphere host or vCenter server, and then specify hello IP address or FQDN of hello server.</span></span>
3. <span data-ttu-id="5b437-137">除非您的 VMware 伺服器在不同的通訊埠上的要求設定的 toolisten 保留 hello 連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="5b437-137">Leave hello port as 443 unless your VMware servers are configured toolisten for requests on a different port.</span></span> <span data-ttu-id="5b437-138">選取 tooconnect toohello VMware vCenter 或 vSphere ESXi 伺服器 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b437-138">Select hello account that is tooconnect toohello VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="5b437-139">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5b437-139">Click **OK**.</span></span>
4. <span data-ttu-id="5b437-140">站台復原連接 tooVMware 伺服器使用 hello 指定設定，並探索 Vm。</span><span class="sxs-lookup"><span data-stu-id="5b437-140">Site Recovery connects tooVMware servers using hello specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="5b437-141">如果您要加入的伺服器或主控件以 hello vCenter 或主機伺服器沒有系統管理員權限的帳戶，請確定 hello 帳戶已啟用這些權限： 資料中心、 資料存放區、 資料夾、 主機、 網路、 虛擬機器的資源，並vSphere 分散式交換器。</span><span class="sxs-lookup"><span data-stu-id="5b437-141">If you're adding a server or host with an account that doesn't have administrator privileges on hello vCenter or host server, make sure that hello account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="5b437-142">此外，hello VMware vCenter server 必須啟用權限的 hello 儲存檢視表。</span><span class="sxs-lookup"><span data-stu-id="5b437-142">In addition, hello VMware vCenter server needs hello Storage Views privilege enabled.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="5b437-143">Hello 目標環境設定</span><span class="sxs-lookup"><span data-stu-id="5b437-143">Set up hello target environment</span></span>

<span data-ttu-id="5b437-144">您設定 hello 目標環境之前，請確定您有 Azure 儲存體帳戶和虛擬網路設定。</span><span class="sxs-lookup"><span data-stu-id="5b437-144">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="5b437-145">按一下**準備基礎結構** > **目標**，並選取 hello 想 toouse 的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b437-145">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="5b437-146">指定目標部署模型是以 Resource Manager 為基礎或傳統。</span><span class="sxs-lookup"><span data-stu-id="5b437-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="5b437-147">Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。</span><span class="sxs-lookup"><span data-stu-id="5b437-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![目標](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="5b437-149">如果您尚未建立儲存體帳戶或網路，按一下**+ 儲存體帳戶**或**+ 網路**，toocreate 資源管理員帳戶或網路內嵌。</span><span class="sxs-lookup"><span data-stu-id="5b437-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b437-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b437-150">Next steps</span></span>

<span data-ttu-id="5b437-151">跳過[步驟 9： 設定複寫原則](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="5b437-151">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
