---
title: "使用 DPM 將工作負載備份至 Azure 入口網站 | Microsoft Docs"
description: "使用 Azure 備份服務來備份 DPM 伺服器的簡介"
services: backup
documentationcenter: 
author: adigan
manager: nkolli
editor: 
keywords: "System Center Data Protection Manager, Data Protection Manager, DPM 備份"
ms.assetid: c8c322cf-f5eb-422c-a34c-04a4801bfec7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: 3422c8d57bdd786ce5d1a41fbb4c12cc4efffddd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="preparing-to-back-up-workloads-to-azure-with-dpm"></a><span data-ttu-id="90e6f-104">準備使用 DPM 將工作負載備份到 Azure</span><span class="sxs-lookup"><span data-stu-id="90e6f-104">Preparing to back up workloads to Azure with DPM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90e6f-105">Azure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="90e6f-105">Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)
> * [<span data-ttu-id="90e6f-106">SCDPM</span><span class="sxs-lookup"><span data-stu-id="90e6f-106">SCDPM</span></span>](backup-azure-dpm-introduction.md)
> * [<span data-ttu-id="90e6f-107">Azure 備份伺服器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="90e6f-107">Azure Backup Server (Classic)</span></span>](backup-azure-microsoft-azure-backup-classic.md)
> * [<span data-ttu-id="90e6f-108">SCDPM (傳統)</span><span class="sxs-lookup"><span data-stu-id="90e6f-108">SCDPM (Classic)</span></span>](backup-azure-dpm-introduction-classic.md)
>
>

<span data-ttu-id="90e6f-109">本文簡介如何使用 Microsoft Azure 備份來保護 System Center Data Protection Manager (DPM) 伺服器和工作負載。</span><span class="sxs-lookup"><span data-stu-id="90e6f-109">This article provides an introduction to using Microsoft Azure Backup to protect your System Center Data Protection Manager (DPM) servers and workloads.</span></span> <span data-ttu-id="90e6f-110">在閱讀本文後，您將了解：</span><span class="sxs-lookup"><span data-stu-id="90e6f-110">By reading it, you’ll understand:</span></span>

* <span data-ttu-id="90e6f-111">Azure DPM 伺服器備份的運作方式</span><span class="sxs-lookup"><span data-stu-id="90e6f-111">How Azure DPM server backup works</span></span>
* <span data-ttu-id="90e6f-112">使備份流暢的必要條件</span><span class="sxs-lookup"><span data-stu-id="90e6f-112">The prerequisites to achieve a smooth backup experience</span></span>
* <span data-ttu-id="90e6f-113">遇到的一般錯誤以及如何排除</span><span class="sxs-lookup"><span data-stu-id="90e6f-113">The typical errors encountered and how to deal with them</span></span>
* <span data-ttu-id="90e6f-114">支援的案例</span><span class="sxs-lookup"><span data-stu-id="90e6f-114">Supported scenarios</span></span>

> [!NOTE]
> <span data-ttu-id="90e6f-115">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="90e6f-115">Azure has two deployment models for creating and working with resources: [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="90e6f-116">本文提供的資訊和程序可供還原使用 Resource Manager 模型部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="90e6f-116">This article provides the information and procedures for restoring VMs deployed using the Resource Manager model.</span></span>
>
>

<span data-ttu-id="90e6f-117">System Center DPM 會備份檔案和應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="90e6f-117">System Center DPM backs up file and application data.</span></span> <span data-ttu-id="90e6f-118">備份到 DPM 的資料可以儲存在磁帶、磁碟上，或使用 Microsoft Azure 備份來備份到 Azure。</span><span class="sxs-lookup"><span data-stu-id="90e6f-118">Data backed up to DPM can be stored on tape, on disk, or backed up to Azure with Microsoft Azure Backup.</span></span> <span data-ttu-id="90e6f-119">DPM 與 Azure 備份的互動方式如下：</span><span class="sxs-lookup"><span data-stu-id="90e6f-119">DPM interacts with Azure Backup as follows:</span></span>

* <span data-ttu-id="90e6f-120">**DPM 部署為實體伺服器或內部部署虛擬機器** — 如果 DPM 部署為實體伺服器或內部部署 Hyper-V 虛擬機器，除了備份到磁碟和磁帶上，您還可以將資料備份到復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="90e6f-120">**DPM deployed as a physical server or on-premises virtual machine** — If DPM is deployed as a physical server or as an on-premises Hyper-V virtual machine you can back up data to a Recovery Services vault in addition to disk and tape backup.</span></span>
* <span data-ttu-id="90e6f-121">**DPM 部署為 Azure 虛擬機器** — 從 System Center 2012 R2 Update 3 開始，DPM 可以部署為 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="90e6f-121">**DPM deployed as an Azure virtual machine** — From System Center 2012 R2 with Update 3, DPM can be deployed as an Azure virtual machine.</span></span> <span data-ttu-id="90e6f-122">如果 DPM 部署為 Azure 虛擬機器，您可以將資料備份到連接至 DPM Azure 虛擬機器的 Azure 磁碟，或者您也可以將資料備份到復原服務保存庫以卸載資料儲存體。</span><span class="sxs-lookup"><span data-stu-id="90e6f-122">If DPM is deployed as an Azure virtual machine you can back up data to Azure disks attached to the DPM Azure virtual machine, or you can offload the data storage by backing it up to a Recovery Services vault.</span></span>

## <a name="why-backup-from-dpm-to-azure"></a><span data-ttu-id="90e6f-123">為什麼要從 DPM 備份到 Azure？</span><span class="sxs-lookup"><span data-stu-id="90e6f-123">Why backup from DPM to Azure?</span></span>
<span data-ttu-id="90e6f-124">使用 Azure 備份來備份 DPM 伺服器的商業利益包括：</span><span class="sxs-lookup"><span data-stu-id="90e6f-124">The business benefits of using Azure Backup for backing up DPM servers include:</span></span>

* <span data-ttu-id="90e6f-125">在內部部署 DPM 部署中，您可以使用 Azure 來替代長期的磁帶部署。</span><span class="sxs-lookup"><span data-stu-id="90e6f-125">For on-premises DPM deployment, you can use Azure as an alternative to long-term deployment to tape.</span></span>
* <span data-ttu-id="90e6f-126">在 Azure 的 DPM 部署中，Azure 備份可讓您卸載 Azure 磁碟中的儲存體，並在復原服務保存庫中儲存較舊的資料，而將較新的資料儲存在磁碟上以進行擴充。</span><span class="sxs-lookup"><span data-stu-id="90e6f-126">For DPM deployments in Azure, Azure Backup allows you to offload storage from the Azure disk, allowing you to scale up by storing older data in Recovery Services vault and new data on disk.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90e6f-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="90e6f-127">Prerequisites</span></span>
<span data-ttu-id="90e6f-128">如下所示讓 Azure 備份做好備份 DPM 資料的準備：</span><span class="sxs-lookup"><span data-stu-id="90e6f-128">Prepare Azure Backup to back up DPM data as follows:</span></span>

1. <span data-ttu-id="90e6f-129">**建立復原服務保存庫** — 在 Azure 入口網站中建立保存庫。</span><span class="sxs-lookup"><span data-stu-id="90e6f-129">**Create a Recovery Services vault** — Create a vault in Azure portal.</span></span>
2. <span data-ttu-id="90e6f-130">**下載保存庫認證** — 下載用來向復原服務保存庫註冊 DPM 伺服器的認證。</span><span class="sxs-lookup"><span data-stu-id="90e6f-130">**Download vault credentials** — Download the credentials which you use to register the DPM server to Recovery Services vault.</span></span>
3. <span data-ttu-id="90e6f-131">**安裝 Azure 備份代理程式** — 從 Azure 備份，在每一部 DPM 伺服器上安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="90e6f-131">**Install the Azure Backup Agent** — From Azure Backup, install the agent on each DPM server.</span></span>
4. <span data-ttu-id="90e6f-132">**註冊伺服器** — 向 [復原服務保存庫] 註冊 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="90e6f-132">**Register the server** — Register the DPM server to Recovery Services vault.</span></span>

### <a name="1-create-a-recovery-services-vault"></a><span data-ttu-id="90e6f-133">1.建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="90e6f-133">1. Create a recovery services vault</span></span>
<span data-ttu-id="90e6f-134">若要建立復原服務保存庫：</span><span class="sxs-lookup"><span data-stu-id="90e6f-134">To create a recovery services vault:</span></span>

1. <span data-ttu-id="90e6f-135">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="90e6f-135">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="90e6f-136">在 [中樞] 功能表上按一下 [瀏覽]，然後在資源清單中輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="90e6f-136">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="90e6f-137">當您開始輸入時，清單將會根據您輸入的文字進行篩選。</span><span class="sxs-lookup"><span data-stu-id="90e6f-137">As you begin typing, the list will filter based on your input.</span></span> <span data-ttu-id="90e6f-138">按一下 [復原服務保存庫] 。</span><span class="sxs-lookup"><span data-stu-id="90e6f-138">Click **Recovery Services vault**.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-dpm-introduction/open-recovery-services-vault.png)

    <span data-ttu-id="90e6f-140">隨即會顯示 [復原服務保存庫] 清單。</span><span class="sxs-lookup"><span data-stu-id="90e6f-140">The list of Recovery Services vaults is displayed.</span></span>
3. <span data-ttu-id="90e6f-141">在 [復原服務保存庫] 功能表上，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="90e6f-141">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![建立復原服務保存庫的步驟 2](./media/backup-azure-dpm-introduction/rs-vault-menu.png)

    <span data-ttu-id="90e6f-143">[復原服務保存庫] 刀鋒視窗隨即開啟，並提示您提供 [名稱]、[訂用帳戶]、[資源群組] 和 [位置]。</span><span class="sxs-lookup"><span data-stu-id="90e6f-143">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![建立復原服務保存庫的步驟 5](./media/backup-azure-dpm-introduction/rs-vault-attributes.png)
4. <span data-ttu-id="90e6f-145">在 [名稱] 中，輸入易記名稱來識別保存庫。</span><span class="sxs-lookup"><span data-stu-id="90e6f-145">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="90e6f-146">必須是 Azure 訂用帳戶中唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="90e6f-146">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="90e6f-147">輸入包含 2 到 50 個字元的名稱。</span><span class="sxs-lookup"><span data-stu-id="90e6f-147">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="90e6f-148">該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="90e6f-148">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>
5. <span data-ttu-id="90e6f-149">按一下 [訂用帳戶]  以查看可用的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="90e6f-149">Click **Subscription** to see the available list of subscriptions.</span></span> <span data-ttu-id="90e6f-150">如果您不確定要使用哪個訂用帳戶，請使用預設 (或建議) 的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="90e6f-150">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="90e6f-151">只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。</span><span class="sxs-lookup"><span data-stu-id="90e6f-151">There will be multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>
6. <span data-ttu-id="90e6f-152">按一下 [資源群組] 以查看可用的資源群組清單，或按一下 [新增] 以建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="90e6f-152">Click **Resource group** to see the available list of Resource groups, or click **New** to create a new Resource group.</span></span> <span data-ttu-id="90e6f-153">如需資源群組的完整資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="90e6f-153">For complete information on Resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
7. <span data-ttu-id="90e6f-154">按一下 [位置]  以選取保存庫的地理區域。</span><span class="sxs-lookup"><span data-stu-id="90e6f-154">Click **Location** to select the geographic region for the vault.</span></span>
8. <span data-ttu-id="90e6f-155">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="90e6f-155">Click **Create**.</span></span> <span data-ttu-id="90e6f-156">要等復原服務保存庫建立好，可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="90e6f-156">It can take a while for the Recovery Services vault to be created.</span></span> <span data-ttu-id="90e6f-157">請監視入口網站右上方區域中的狀態通知。</span><span class="sxs-lookup"><span data-stu-id="90e6f-157">Monitor the status notifications in the upper right-hand area in the portal.</span></span>
   <span data-ttu-id="90e6f-158">保存庫一旦建立好，就會在入口網站中開啟。</span><span class="sxs-lookup"><span data-stu-id="90e6f-158">Once your vault is created, it opens in the portal.</span></span>

### <a name="set-storage-replication"></a><span data-ttu-id="90e6f-159">設定儲存體複寫</span><span class="sxs-lookup"><span data-stu-id="90e6f-159">Set Storage Replication</span></span>
<span data-ttu-id="90e6f-160">儲存體複寫選項有異地備援儲存體和本地備援儲存體可供您選擇。</span><span class="sxs-lookup"><span data-stu-id="90e6f-160">The storage replication option allows you to choose between geo-redundant storage and locally redundant storage.</span></span> <span data-ttu-id="90e6f-161">根據預設，保存庫具有異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="90e6f-161">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="90e6f-162">如果這是您的主要備份，請讓選項繼續設定為異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="90e6f-162">Leave the option set to geo-redundant storage if this is your primary backup.</span></span> <span data-ttu-id="90e6f-163">如果您想要更便宜但不持久的選項，請選擇本地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="90e6f-163">Choose locally redundant storage if you want a cheaper option that isn't quite as durable.</span></span> <span data-ttu-id="90e6f-164">在 [Azure 儲存體複寫概觀](../storage/common/storage-redundancy.md)中，深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本地備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存體選項。</span><span class="sxs-lookup"><span data-stu-id="90e6f-164">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in the [Azure Storage replication overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="90e6f-165">若要編輯儲存體複寫設定︰</span><span class="sxs-lookup"><span data-stu-id="90e6f-165">To edit the storage replication setting:</span></span>

1. <span data-ttu-id="90e6f-166">選取保存庫以開啟保存庫儀表板和 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="90e6f-166">Select your vault to open the vault dashboard and the Settings blade.</span></span> <span data-ttu-id="90e6f-167">如果 [設定] 刀鋒視窗未開啟，請按一下保存庫儀表板中的 [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="90e6f-167">If the **Settings** blade doesn't open, click **All settings** in the vault dashboard.</span></span>
2. <span data-ttu-id="90e6f-168">在 [設定] 刀鋒視窗上按一下 [備份基礎結構]  >  [備份設定]，開啟 [備份設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="90e6f-168">On the **Settings** blade, click **Backup Infrastructure** > **Backup Configuration** to open the **Backup Configuration** blade.</span></span> <span data-ttu-id="90e6f-169">在 [備份設定]  刀鋒視窗上，選擇保存庫的儲存體複寫選項。</span><span class="sxs-lookup"><span data-stu-id="90e6f-169">On the **Backup Configuration** blade, choose the storage replication option for your vault.</span></span>

    ![備份保存庫的清單](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    <span data-ttu-id="90e6f-171">選擇好保存庫的儲存體選項後，就可以開始建立 VM 與保存庫的關聯。</span><span class="sxs-lookup"><span data-stu-id="90e6f-171">After choosing the storage option for your vault, you are ready to associate the VM with the vault.</span></span> <span data-ttu-id="90e6f-172">若要開始關聯，請探索及註冊 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="90e6f-172">To begin the association, you should discover and register the Azure virtual machines.</span></span>

### <a name="2-download-vault-credentials"></a><span data-ttu-id="90e6f-173">2.下載保存庫認證</span><span class="sxs-lookup"><span data-stu-id="90e6f-173">2. Download vault credentials</span></span>
<span data-ttu-id="90e6f-174">保存庫認證檔是入口網站針對每個備份保存庫所產生的憑證。</span><span class="sxs-lookup"><span data-stu-id="90e6f-174">The vault credentials file is a certificate generated by the portal for each backup vault.</span></span> <span data-ttu-id="90e6f-175">入口網站接著會將公開金鑰上傳至「存取控制服務」(ACS)。</span><span class="sxs-lookup"><span data-stu-id="90e6f-175">The portal then uploads the public key to the Access Control Service (ACS).</span></span> <span data-ttu-id="90e6f-176">憑證的私密金鑰可供使用者作為工作流程的一部分，屬於電腦註冊工作流程中的指定輸入。</span><span class="sxs-lookup"><span data-stu-id="90e6f-176">The private key of the certificate is made available to the user as part of the workflow which is given as an input in the machine registration workflow.</span></span> <span data-ttu-id="90e6f-177">這會對電腦進行驗證，以便將備份資料傳送至 Azure 備份服務中的已識別保存庫。</span><span class="sxs-lookup"><span data-stu-id="90e6f-177">This authenticates the machine to send backup data to an identified vault in the Azure Backup service.</span></span>

<span data-ttu-id="90e6f-178">保存庫認證僅在註冊工作流程期間使用。</span><span class="sxs-lookup"><span data-stu-id="90e6f-178">The vault credential is used only during the registration workflow.</span></span> <span data-ttu-id="90e6f-179">使用者應自行負責，並確保保存庫認證檔不會遭到破解。</span><span class="sxs-lookup"><span data-stu-id="90e6f-179">It is the user’s responsibility to ensure that the vault credentials file is not compromised.</span></span> <span data-ttu-id="90e6f-180">保存庫認證檔落入任何惡意使用者的手中，則可用來針對相同的保存庫註冊其他電腦。</span><span class="sxs-lookup"><span data-stu-id="90e6f-180">If it falls in the hands of any rogue-user, the vault credentials file can be used to register other machines against the same vault.</span></span> <span data-ttu-id="90e6f-181">不過，當使用屬於客戶的複雜密碼來加密備份資料時，現有的備份資料不會遭到洩漏。</span><span class="sxs-lookup"><span data-stu-id="90e6f-181">However, as the backup data is encrypted using a passphrase which belongs to the customer, existing backup data cannot be compromised.</span></span> <span data-ttu-id="90e6f-182">若要減輕這個問題，保存庫認證設在 48 小時後過期。</span><span class="sxs-lookup"><span data-stu-id="90e6f-182">To mitigate this concern, vault credentials are set to expire in 48hrs.</span></span> <span data-ttu-id="90e6f-183">您可以下載復原服務的保存庫認證，次數不受限制，但僅最新的保存庫認證檔可在註冊工作流程期間提供使用。</span><span class="sxs-lookup"><span data-stu-id="90e6f-183">You can download the vault credentials of a recovery services any number of times – but only the latest vault credential file is applicable during the registration workflow.</span></span>

<span data-ttu-id="90e6f-184">保存庫認證檔會透過安全通道，從 Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="90e6f-184">The vault credential file is downloaded through a secure channel from the Azure portal.</span></span> <span data-ttu-id="90e6f-185">Azure 備份服務不會知道憑證的私密金鑰，且私密金鑰不會保存在入口網站或服務中。</span><span class="sxs-lookup"><span data-stu-id="90e6f-185">The Azure Backup service is unaware of the private key of the certificate and the private key is not persisted in the portal or the service.</span></span> <span data-ttu-id="90e6f-186">使用下列步驟將保存庫認證檔下載至本機電腦。</span><span class="sxs-lookup"><span data-stu-id="90e6f-186">Use the following steps to download the vault credential file to a local machine.</span></span>

1. <span data-ttu-id="90e6f-187">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="90e6f-187">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="90e6f-188">開啟要註冊 DPM 電腦的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="90e6f-188">Open Recovery Services vault to which to which you want to register DPM machine.</span></span>
3. <span data-ttu-id="90e6f-189">根據預設，[設定] 刀鋒視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="90e6f-189">Settings blade opens up by default.</span></span> <span data-ttu-id="90e6f-190">如果該刀鋒視窗未開啟，請在保存庫儀表板上按一下 [設定]  ，以開啟 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="90e6f-190">If it is closed, click on **Settings** on vault dashboard to open the settings blade.</span></span> <span data-ttu-id="90e6f-191">在 [設定] 刀鋒視窗中，按一下 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="90e6f-191">In Settings blade, click on **Properties**.</span></span>

    ![開啟 [保存庫] 刀鋒視窗](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
4. <span data-ttu-id="90e6f-193">在 [屬性] 頁面中，按一下 [備份認證] 下方的 [下載]。</span><span class="sxs-lookup"><span data-stu-id="90e6f-193">On the Properties page, click **Download** under **Backup Credentials**.</span></span> <span data-ttu-id="90e6f-194">入口網站會產生可供下載的保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="90e6f-194">The  portal generates the vault credential file, which is made available for download.</span></span>

    ![下載](./media/backup-azure-dpm-introduction/vault-credentials.png)

<span data-ttu-id="90e6f-196">入口網站會使用保存庫名稱和目前日期的組合來產生保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="90e6f-196">The portal will generate a vault credential using a combination of the vault name and the current date.</span></span> <span data-ttu-id="90e6f-197">按一下 [ **儲存** ] 將保存庫認證下載至本機帳戶的下載資料夾，或從 [儲存] 功能表中選取 [另存新檔]，以指定保存庫認證的位置。</span><span class="sxs-lookup"><span data-stu-id="90e6f-197">Click **Save** to download the vault credentials to the local account's downloads folder, or select Save As from the Save menu to specify a location for the vault credentials.</span></span> <span data-ttu-id="90e6f-198">產生檔案需要一分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="90e6f-198">It will take up to a minute for the file to be generated.</span></span>

### <a name="note"></a><span data-ttu-id="90e6f-199">注意</span><span class="sxs-lookup"><span data-stu-id="90e6f-199">Note</span></span>
* <span data-ttu-id="90e6f-200">請確定保存庫認證檔儲存在可從電腦存取的位置。</span><span class="sxs-lookup"><span data-stu-id="90e6f-200">Ensure that the vault credentials file is saved in a location which can be accessed from your machine.</span></span> <span data-ttu-id="90e6f-201">如果它儲存在檔案共用/SMB，請檢查存取權限。</span><span class="sxs-lookup"><span data-stu-id="90e6f-201">If it is stored in a file share/SMB, check for the access permissions.</span></span>
* <span data-ttu-id="90e6f-202">保存庫認證檔僅在註冊工作流程期間使用。</span><span class="sxs-lookup"><span data-stu-id="90e6f-202">The vault credentials file is used only during the registration workflow.</span></span>
* <span data-ttu-id="90e6f-203">保存庫認證檔會在 48 小時後過期，並且可以從入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="90e6f-203">The vault credentials file expires after 48hrs and can be downloaded from the portal.</span></span>

### <a name="3-install-backup-agent"></a><span data-ttu-id="90e6f-204">3.安裝備份代理程式</span><span class="sxs-lookup"><span data-stu-id="90e6f-204">3. Install Backup Agent</span></span>
<span data-ttu-id="90e6f-205">建立 Azure 備份保存庫之後，您的每部 Windows 電腦 (Windows Server、Windows 用戶端、System Center Data Protection Manager 伺服器，或 Azure 備份伺服器電腦) 上應該安裝代理程式，以便讓您將資料和應用程式備份至 Azure。</span><span class="sxs-lookup"><span data-stu-id="90e6f-205">After creating the Azure Backup vault, an agent should be installed on each of your Windows machines (Windows Server, Windows client, System Center Data Protection Manager server, or Azure Backup Server machine) that enables back up of data and applications to Azure.</span></span>

1. <span data-ttu-id="90e6f-206">開啟要註冊 DPM 電腦的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="90e6f-206">Open Recovery Services vault to which to which you want to register DPM machine.</span></span>
2. <span data-ttu-id="90e6f-207">根據預設，[設定] 刀鋒視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="90e6f-207">Settings blade opens up by default.</span></span> <span data-ttu-id="90e6f-208">如果該刀鋒視窗未開啟，請按一下 [設定]  以開啟 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="90e6f-208">If it is closed, click on **Settings** to open the settings blade.</span></span> <span data-ttu-id="90e6f-209">在 [設定] 刀鋒視窗中，按一下 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="90e6f-209">In Settings blade, click on **Properties**.</span></span>

    ![開啟 [保存庫] 刀鋒視窗](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
3. <span data-ttu-id="90e6f-211">在 [設定] 頁面中，按一下 [Azure 備份代理程式] 下方的 [下載]。</span><span class="sxs-lookup"><span data-stu-id="90e6f-211">On the Settings page, click **Download** under **Azure Backup Agent**.</span></span>

    ![下載](./media/backup-azure-dpm-introduction/azure-backup-agent.png)

   <span data-ttu-id="90e6f-213">代理程式下載完成後，按兩下 MARSAgentInstaller.exe 來啟動 Azure 備份代理程式的安裝。</span><span class="sxs-lookup"><span data-stu-id="90e6f-213">Once the agent is downloaded, double click MARSAgentInstaller.exe to launch the installation of the Azure Backup agent.</span></span> <span data-ttu-id="90e6f-214">選擇安裝資料夾和代理程式所需要的暫存資料夾。</span><span class="sxs-lookup"><span data-stu-id="90e6f-214">Choose the installation folder and scratch folder required for the agent.</span></span> <span data-ttu-id="90e6f-215">指定的快取位置必須至少包含備份資料大小 5%的可用空間。</span><span class="sxs-lookup"><span data-stu-id="90e6f-215">The cache location specified must have free space which is at least 5% of the backup data.</span></span>
4. <span data-ttu-id="90e6f-216">若您使用 Proxy 伺服器連接至網際網路，請在 [ **Proxy 組態** ] 畫面上，輸入 Proxy 伺服器詳細資料。</span><span class="sxs-lookup"><span data-stu-id="90e6f-216">If you use a proxy server to connect to the internet, in the **Proxy configuration** screen, enter the proxy server details.</span></span> <span data-ttu-id="90e6f-217">若您使用已驗證的 Proxy，請在此畫面中輸入使用者名稱和密碼的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="90e6f-217">If you use an authenticated proxy, enter the user name and password details in this screen.</span></span>
5. <span data-ttu-id="90e6f-218">Azure 備份代理程式會安裝 .NET Framework 4.5 和 Windows PowerShell (若尚未安裝) 來完成安裝。</span><span class="sxs-lookup"><span data-stu-id="90e6f-218">The Azure Backup agent installs .NET Framework 4.5 and Windows PowerShell (if it’s not available already) to complete the installation.</span></span>
6. <span data-ttu-id="90e6f-219">安裝代理程式之後， 請 **關閉** 視窗。</span><span class="sxs-lookup"><span data-stu-id="90e6f-219">Once the agent is installed, **Close** the window.</span></span>

   ![關閉](../../includes/media/backup-install-agent/dpm_FinishInstallation.png)
7. <span data-ttu-id="90e6f-221">若要向保存庫**註冊 DPM 伺服器**，請在 [管理] 索引標籤中，按一下 [線上]。</span><span class="sxs-lookup"><span data-stu-id="90e6f-221">To **Register the DPM Server** to the vault, in the **Management** tab, Click on **Online**.</span></span> <span data-ttu-id="90e6f-222">接著，選取 [註冊] 。</span><span class="sxs-lookup"><span data-stu-id="90e6f-222">Then, select **Register**.</span></span> <span data-ttu-id="90e6f-223">隨即會開啟 [註冊設定] 精靈。</span><span class="sxs-lookup"><span data-stu-id="90e6f-223">It will open the Register Setup Wizard.</span></span>
8. <span data-ttu-id="90e6f-224">若您使用 Proxy 伺服器連接至網際網路，請在 [ **Proxy 組態** ] 畫面上，輸入 Proxy 伺服器詳細資料。</span><span class="sxs-lookup"><span data-stu-id="90e6f-224">If you use a proxy server to connect to the internet, in the **Proxy configuration** screen, enter the proxy server details.</span></span> <span data-ttu-id="90e6f-225">若您使用已驗證的 Proxy，請在此畫面中輸入使用者名稱和密碼的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="90e6f-225">If you use an authenticated proxy, enter the user name and password details in this screen.</span></span>

    ![Proxy 組態](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Proxy.png)
9. <span data-ttu-id="90e6f-227">在保存庫認證畫面中，瀏覽並選取先前已下載的保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="90e6f-227">In the vault credentials screen, browse to and select the vault credentials file which was previously downloaded.</span></span>

    ![保存庫認證](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Credentials.jpg)

    <span data-ttu-id="90e6f-229">保存庫認證檔僅於 48 小時內有效 (從入口網站下載後起算)。</span><span class="sxs-lookup"><span data-stu-id="90e6f-229">The vault credentials file is valid only for 48 hrs (after it’s downloaded from the portal).</span></span> <span data-ttu-id="90e6f-230">如果您在此畫面中遇到任何錯誤 (例如，「提供的保存庫認證檔已過期」)，請登入 Azure 入口網站，並再次下載保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="90e6f-230">If you encounter any error in this screen (for example, “Vault credentials file provided has expired”), login to the Azure portal and download the vault credentials file again.</span></span>

    <span data-ttu-id="90e6f-231">請確定保存庫認證檔位於可透過設定應用程式存取的位置。</span><span class="sxs-lookup"><span data-stu-id="90e6f-231">Ensure that the vault credentials file is available in a location which can be accessed by the setup application.</span></span> <span data-ttu-id="90e6f-232">如果您遇到存取權相關的錯誤，請將保存庫認證檔複製至此電腦中的暫存位置並重試作業。</span><span class="sxs-lookup"><span data-stu-id="90e6f-232">If you encounter access related errors, copy the vault credentials file to a temporary location in this machine and retry the operation.</span></span>

    <span data-ttu-id="90e6f-233">如果您遇到無效的保存庫認證錯誤 (例如，「提供的保存庫認證無效」)，檔案可能損毀或沒有復原服務所關聯的最新認證。</span><span class="sxs-lookup"><span data-stu-id="90e6f-233">If you encounter an invalid vault credential error (for example, “Invalid vault credentials provided") the file is either corrupted or does not have the latest credentials associated with the recovery service.</span></span> <span data-ttu-id="90e6f-234">從入口網站下載新的保存庫認證檔後重試作業。</span><span class="sxs-lookup"><span data-stu-id="90e6f-234">Retry the operation after downloading a new vault credential file from the portal.</span></span> <span data-ttu-id="90e6f-235">若使用者在 Azure 入口網站中連續快速地按下 [ **下載保存庫認證** ] 選項，則通常會看見此錯誤。</span><span class="sxs-lookup"><span data-stu-id="90e6f-235">This error is typically seen if the user clicks on the **Download vault credential** option in the Azure portal, in quick succession.</span></span> <span data-ttu-id="90e6f-236">在此情況下，僅第二個保存庫認證檔為有效。</span><span class="sxs-lookup"><span data-stu-id="90e6f-236">In this case, only the second vault credential file is valid.</span></span>
10. <span data-ttu-id="90e6f-237">若要控制工作期間以及非工作期間的網路頻寬使用，您可以在 [節流設定]  畫面中，設定頻寬使用限制，並定義工作與非工作時間。</span><span class="sxs-lookup"><span data-stu-id="90e6f-237">To control the usage of network bandwidth during work, and non-work hours, in the **Throttling Setting** screen, you can set the bandwidth usage limits and define the work and non-work hours.</span></span>

    ![節流設定](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Throttling.png)
11. <span data-ttu-id="90e6f-239">在 [復原資料夾設定]  畫面上，瀏覽將暫存從 Azure 所下載檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="90e6f-239">In the **Recovery Folder Setting** screen, browse for the folder where the files downloaded from Azure will be temporarily staged.</span></span>

    ![復原資料夾設定](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_RecoveryFolder.png)
12. <span data-ttu-id="90e6f-241">在 [ **加密設定** ] 畫面中，您可以產生複雜密碼或提供複雜密碼 (最少 16 個字元)。</span><span class="sxs-lookup"><span data-stu-id="90e6f-241">In the **Encryption setting** screen, you can either generate a passphrase or provide a passphrase (minimum of 16 characters).</span></span> <span data-ttu-id="90e6f-242">請記得將複雜密碼存放在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="90e6f-242">Remember to save the passphrase in a secure location.</span></span>

    ![加密](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Encryption.png)

    > [!WARNING]
    > <span data-ttu-id="90e6f-244">如果遺失或忘記複雜密碼，Microsoft 將無法協助您復原備份資料。</span><span class="sxs-lookup"><span data-stu-id="90e6f-244">If the passphrase is lost or forgotten; Microsoft cannot help in recovering the backup data.</span></span> <span data-ttu-id="90e6f-245">加密複雜密碼為使用者所有，Microsoft 將不會看到使用者所使用的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="90e6f-245">The end user owns the encryption passphrase and Microsoft does not have visibility into the passphrase used by the end user.</span></span> <span data-ttu-id="90e6f-246">請將檔案儲存在安全的位置，在復原作業期間需要該檔案。</span><span class="sxs-lookup"><span data-stu-id="90e6f-246">Please save the file in a secure location as it is required during a recovery operation.</span></span>
    >
    >
13. <span data-ttu-id="90e6f-247">一旦您按一下 [註冊]  按鈕，電腦即成功註冊至保存庫，且現在您已準備好開始備份至 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="90e6f-247">Once you click the **Register** button, the machine is registered successfully to the vault and you are now ready to start backing up to Microsoft Azure.</span></span>
14. <span data-ttu-id="90e6f-248">當使用 Data Protection Manager 時，您可以修改註冊工作流程期間所指定的設定，方法是選取 [管理] 索引標籤下的 [線上]，接著按一下 [設定] 選項。</span><span class="sxs-lookup"><span data-stu-id="90e6f-248">When using Data Protection Manager, you can modify the settings specified during the registration workflow by clicking the **Configure** option by selecting **Online** under the **Management** Tab.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="90e6f-249">需求 (和限制)</span><span class="sxs-lookup"><span data-stu-id="90e6f-249">Requirements (and limitations)</span></span>
* <span data-ttu-id="90e6f-250">DPM 可以做為實體伺服器或 System Center 2012 SP1 或 System Center 2012 R2 上安裝的 HYPER-V 虛擬機器來執行。</span><span class="sxs-lookup"><span data-stu-id="90e6f-250">DPM can be running as a physical server or a Hyper-V virtual machine installed on System Center 2012 SP1 or System Center 2012 R2.</span></span> <span data-ttu-id="90e6f-251">它也可以做為 System Center 2012 R2 (至少含 DPM 2012 R2 更新彙總套件 3) 上執行的 Azure 虛擬機器，或 System Center 2012 R2 (至少含更新彙總套件 5) 上執行之 VMWare 中的 Windows 虛擬機器來執行。</span><span class="sxs-lookup"><span data-stu-id="90e6f-251">It can also be running as an Azure virtual machine running on System Center 2012 R2 with at least DPM 2012 R2 Update Rollup 3 or a Windows virtual machine in VMWare running on System Center 2012 R2 with at least Update Rollup 5.</span></span>
* <span data-ttu-id="90e6f-252">如果您使用 System Center 2012 SP1 來執行 DPM，則應該安裝 System Center Data Protection Manager SP1 的更新彙總套件 2。</span><span class="sxs-lookup"><span data-stu-id="90e6f-252">If you’re running DPM with System Center 2012 SP1 you should install Update Roll up 2 for System Center Data Protection Manager SP1.</span></span> <span data-ttu-id="90e6f-253">要有此軟體才能安裝 Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="90e6f-253">This is required before you can install the Azure Backup Agent.</span></span>
* <span data-ttu-id="90e6f-254">DPM 伺服器應該已安裝 Windows PowerShell 和 .Net Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="90e6f-254">The DPM server should have Windows PowerShell and .Net Framework 4.5 installed.</span></span>
* <span data-ttu-id="90e6f-255">DPM 可以將大部分的工作負載備份至 Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="90e6f-255">DPM can back up most workloads to Azure Backup.</span></span> <span data-ttu-id="90e6f-256">如需所支援項目的完整清單，請參閱下面的 Azure 備份支援項目。</span><span class="sxs-lookup"><span data-stu-id="90e6f-256">For a full list of what’s supported see the Azure Backup support items below.</span></span>
* <span data-ttu-id="90e6f-257">使用 [複製到磁帶] 選項無法復原 Azure 備份中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="90e6f-257">Data stored in Azure Backup can’t be recovered with the “copy to tape” option.</span></span>
* <span data-ttu-id="90e6f-258">您需要已啟用 Azure 備份功能的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="90e6f-258">You’ll need an Azure account with the Azure Backup feature enabled.</span></span> <span data-ttu-id="90e6f-259">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="90e6f-259">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="90e6f-260">請閱讀 [Azure 備份定價](https://azure.microsoft.com/pricing/details/backup/)。</span><span class="sxs-lookup"><span data-stu-id="90e6f-260">Read about [Azure Backup pricing](https://azure.microsoft.com/pricing/details/backup/).</span></span>
* <span data-ttu-id="90e6f-261">要使用 Azure 備份，就必須在您想要備份的伺服器上安裝 Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="90e6f-261">Using Azure Backup requires the Azure Backup Agent to be installed on the servers you want to back up.</span></span> <span data-ttu-id="90e6f-262">每個伺服器必須至少具有所要備份之資料大小的 5 % 做為本機可用儲存空間。</span><span class="sxs-lookup"><span data-stu-id="90e6f-262">Each server must have at least 5 % of the size of the data that is being backed up, available as local free storage.</span></span> <span data-ttu-id="90e6f-263">例如，備份 100GB 的資料時，在臨時位置中至少需要 5 GB 的可用空間。</span><span class="sxs-lookup"><span data-stu-id="90e6f-263">For example, backing up 100 GB of data requires a minimum of 5 GB of free space in the scratch location.</span></span>
* <span data-ttu-id="90e6f-264">資料會儲存在 Azure 保存庫儲存體中。</span><span class="sxs-lookup"><span data-stu-id="90e6f-264">Data will be stored in the Azure vault storage.</span></span> <span data-ttu-id="90e6f-265">可以備份至 Azure 備份保存庫的資料數量沒有限制，但是資料來源 (例如虛擬機器或資料庫) 的大小不應超過 54400 GB。</span><span class="sxs-lookup"><span data-stu-id="90e6f-265">There’s no limit to the amount of data you can back up to an Azure Backup vault but the size of a data source (for example a virtual machine or database) shouldn’t exceed 54400 GB.</span></span>

<span data-ttu-id="90e6f-266">下列檔案類型可支援備份至 Azure：</span><span class="sxs-lookup"><span data-stu-id="90e6f-266">These file types are supported for back up to Azure:</span></span>

* <span data-ttu-id="90e6f-267">加密 (僅限完整備份)</span><span class="sxs-lookup"><span data-stu-id="90e6f-267">Encrypted (Full backups only)</span></span>
* <span data-ttu-id="90e6f-268">壓縮 (支援增量備份)</span><span class="sxs-lookup"><span data-stu-id="90e6f-268">Compressed (Incremental backups supported)</span></span>
* <span data-ttu-id="90e6f-269">疏鬆 (支援增量備份)</span><span class="sxs-lookup"><span data-stu-id="90e6f-269">Sparse (Incremental backups supported)</span></span>
* <span data-ttu-id="90e6f-270">壓縮和疏鬆 (視為疏鬆來處理)</span><span class="sxs-lookup"><span data-stu-id="90e6f-270">Compressed and sparse (Treated as Sparse)</span></span>

<span data-ttu-id="90e6f-271">下列為不支援的類型：</span><span class="sxs-lookup"><span data-stu-id="90e6f-271">And these are unsupported:</span></span>

* <span data-ttu-id="90e6f-272">不支援區分大小寫的檔案系統上的伺服器。</span><span class="sxs-lookup"><span data-stu-id="90e6f-272">Servers on case-sensitive file systems aren’t supported.</span></span>
* <span data-ttu-id="90e6f-273">硬式連結 (略過)</span><span class="sxs-lookup"><span data-stu-id="90e6f-273">Hard links (Skipped)</span></span>
* <span data-ttu-id="90e6f-274">重新分析點 (略過)</span><span class="sxs-lookup"><span data-stu-id="90e6f-274">Reparse points (Skipped)</span></span>
* <span data-ttu-id="90e6f-275">加密和壓縮 (略過)</span><span class="sxs-lookup"><span data-stu-id="90e6f-275">Encrypted and compressed (Skipped)</span></span>
* <span data-ttu-id="90e6f-276">加密和疏鬆 (略過)</span><span class="sxs-lookup"><span data-stu-id="90e6f-276">Encrypted and sparse (Skipped)</span></span>
* <span data-ttu-id="90e6f-277">壓縮資料流</span><span class="sxs-lookup"><span data-stu-id="90e6f-277">Compressed stream</span></span>
* <span data-ttu-id="90e6f-278">疏鬆資料流</span><span class="sxs-lookup"><span data-stu-id="90e6f-278">Sparse stream</span></span>

> [!NOTE]
> <span data-ttu-id="90e6f-279">從 System Center 2012 DPM SP1 開始，您可以使用 Microsoft Azure 備份將受到 DPM 保護的工作負載備份至 Azure。</span><span class="sxs-lookup"><span data-stu-id="90e6f-279">From in System Center 2012 DPM with SP1 onwards you can backup up workloads protected by DPM to Azure using Microsoft Azure Backup.</span></span>
>
>
