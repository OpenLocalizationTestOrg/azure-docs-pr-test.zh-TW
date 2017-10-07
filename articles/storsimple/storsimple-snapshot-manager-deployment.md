---
title: "aaaDeploy StorSimple Snapshot Manager |Microsoft 文件"
description: "了解 toodownload 並安裝 hello StorSimple Snapshot Manager MMC 嵌入式管理單元來管理 StorSimple 資料保護和備份功能。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a><span data-ttu-id="0c0ac-103">部署 StorSimple Snapshot Manager MMC 嵌入式管理單元的 hello</span><span class="sxs-lookup"><span data-stu-id="0c0ac-103">Deploy hello StorSimple Snapshot Manager MMC snap-in</span></span>

## <a name="overview"></a><span data-ttu-id="0c0ac-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0c0ac-104">Overview</span></span>
<span data-ttu-id="0c0ac-105">hello StorSimple Snapshot Manager 是 Microsoft Management Console (MMC) 嵌入式管理單元，可簡化資料保護和備份管理在 Microsoft Azure StorSimple 環境中。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-105">hello StorSimple Snapshot Manager is a Microsoft Management Console (MMC) snap-in that simplifies data protection and backup management in a Microsoft Azure StorSimple environment.</span></span> <span data-ttu-id="0c0ac-106">利用 StorSimple Snapshot Manager，您可以管理 Microsoft Azure StorSimple 內部部署和雲端儲存體，就好像是完全整合的儲存系統，並藉此簡化備份和還原程序並降低成本。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-106">With StorSimple Snapshot Manager, you can manage Microsoft Azure StorSimple on-premises and cloud storage as if it were a fully integrated storage system, thus simplifying backup and restore processes and reducing costs.</span></span> 

<span data-ttu-id="0c0ac-107">本教學課程描述組態需求，以及安裝、移除及升級 StorSimple Snapshot Manager 的程序。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-107">This tutorial describes configuration requirements, as well as procedures for installing, removing, and upgrading StorSimple Snapshot Manager.</span></span>

> [!NOTE]
> * <span data-ttu-id="0c0ac-108">您無法使用 StorSimple Snapshot Manager toomanage Microsoft Azure StorSimple 虛擬陣列 （也稱為 StorSimple 內部部署虛擬裝置）。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-108">You cannot use StorSimple Snapshot Manager toomanage Microsoft Azure StorSimple Virtual Arrays (also known as StorSimple on-premises virtual devices).</span></span>
> * <span data-ttu-id="0c0ac-109">如果您計劃您的 StorSimple 裝置 tooinstall StorSimple Update 2，可確定 toodownload hello 最新版的 StorSimple Snapshot Manager，並將它安裝**安裝 StorSimple Update 2 之前**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-109">If you plan tooinstall StorSimple Update 2 on your StorSimple device, be sure toodownload hello latest version of StorSimple Snapshot Manager and install it **before you install StorSimple Update 2**.</span></span> <span data-ttu-id="0c0ac-110">hello 最新版本的 StorSimple Snapshot Manager 的回溯相容性，以及適用於所有的 Microsoft Azure StorSimple 的發行版本。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-110">hello latest version of StorSimple Snapshot Manager is backward compatible and works with all released versions of Microsoft Azure StorSimple.</span></span> <span data-ttu-id="0c0ac-111">如果您使用 hello 舊版的 StorSimple Snapshot Manager，您必須 tooupdate it （您不需要 toouninstall hello 先前版本再安裝新版本的 hello）。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-111">If you are using hello previous version of StorSimple Snapshot Manager, you will need tooupdate it (you do not need toouninstall hello previous version before you install hello new version).</span></span>


## <a name="storsimple-snapshot-manager-installation"></a><span data-ttu-id="0c0ac-112">StorSimple Snapshot Manager 安裝</span><span class="sxs-lookup"><span data-stu-id="0c0ac-112">StorSimple Snapshot Manager installation</span></span>
<span data-ttu-id="0c0ac-113">StorSimple Snapshot Manager 可以安裝在執行 hello Windows Server 2008 R2 SP1、 Windows Server 2012 或 Windows Server 2012 R2 作業系統的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-113">StorSimple Snapshot Manager can be installed on computers that are running hello Windows Server 2008 R2 SP1, Windows Server 2012, or Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="0c0ac-114">在執行 Windows 2008 R2 的伺服器上，您也必須安裝 Windows Server 2008 SP1 和 Windows Management Framework 3.0。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-114">On servers running Windows 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0.</span></span>

<span data-ttu-id="0c0ac-115">您安裝或升級 hello StorSimple Snapshot Manager 嵌入式管理單元 hello Microsoft Management Console (MMC) 之前，請確定該 hello Microsoft Azure StorSimple 裝置及主機伺服器已正確設定。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-115">Before you install or upgrade hello StorSimple Snapshot Manager snap-in for hello Microsoft Management Console (MMC), make sure that hello Microsoft Azure StorSimple device and host server are configured correctly.</span></span>

## <a name="configure-prerequisites"></a><span data-ttu-id="0c0ac-116">設定必要條件</span><span class="sxs-lookup"><span data-stu-id="0c0ac-116">Configure prerequisites</span></span>
<span data-ttu-id="0c0ac-117">hello 下列步驟提供的組態工作的高階概觀，您必須完成才能安裝 hello StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-117">hello following steps provide a high-level overview of configuration tasks that you must complete before you install hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="0c0ac-118">如需完整的 Microsoft Azure StorSimple 組態和安裝資訊，包括系統需求和逐步指示，請參閱 [部署您的內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-118">For complete Microsoft Azure StorSimple configuration and setup information, including system requirements and step-by-step instructions, see [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c0ac-119">在開始之前，檢閱 hello[部署組態檢查清單](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist)和[部署必要條件](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites)中[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-119">Before you begin, review hello [Deployment configuration checklist](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) and and [Deployment prerequisites](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a><span data-ttu-id="0c0ac-120">安裝 StorSimple Snapshot Manager 之前</span><span class="sxs-lookup"><span data-stu-id="0c0ac-120">Before you install StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="0c0ac-121">打開包裝、 裝載和連接 hello Microsoft Azure StorSimple 裝置中所述[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)或[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-121">Unpack, mount, and connect hello Microsoft Azure StorSimple device as described in [Install your StorSimple 8100 device](storsimple-8100-hardware-installation.md) or [Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>
2. <span data-ttu-id="0c0ac-122">請確定您的主機電腦正在執行下列作業系統的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="0c0ac-122">Make sure that your host computer is running one of hello following operating systems:</span></span>
   
   * <span data-ttu-id="0c0ac-123">Windows Server 2008 R2 (在執行 Windows 2008 R2 的伺服器上，您也必須安裝 Windows Server 2008 SP1 和 Windows Management Framework 3.0)</span><span class="sxs-lookup"><span data-stu-id="0c0ac-123">Windows Server 2008 R2 (on servers running Windows 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0)</span></span>
   * <span data-ttu-id="0c0ac-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0c0ac-124">Windows Server 2012</span></span>
   * <span data-ttu-id="0c0ac-125">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0c0ac-125">Windows Server 2012 R2</span></span>
     
     <span data-ttu-id="0c0ac-126">StorSimple 虛擬裝置 hello 主機必須是 Microsoft Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-126">For a StorSimple virtual device, hello host must be a Microsoft Azure Virtual Machine.</span></span>
3. <span data-ttu-id="0c0ac-127">請確定您符合所有的 hello Microsoft Azure StorSimple 設定需求。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-127">Make sure that you meet all hello Microsoft Azure StorSimple configuration requirements.</span></span> <span data-ttu-id="0c0ac-128">如需詳細資訊，請移至太[部署必要條件](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-128">For details, go too[Deployment prerequisites](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).</span></span>
4. <span data-ttu-id="0c0ac-129">連接 hello 裝置 toohello 主機並執行 hello 初始設定。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-129">Connect hello device toohello host and perform hello initial configuration.</span></span> <span data-ttu-id="0c0ac-130">如需詳細資訊，請移至太[部署步驟](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-130">For details, go too[Deployment steps](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).</span></span>
5. <span data-ttu-id="0c0ac-131">Hello 裝置上建立磁碟區、 將它們指派 toohello 主機，並確認該 hello 主機可以裝載和使用它們。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-131">Create volumes on hello device, assign them toohello host, and verify that hello host can mount and use them.</span></span> <span data-ttu-id="0c0ac-132">StorSimple Snapshot Manager 支援下列類型的磁碟區的 hello:</span><span class="sxs-lookup"><span data-stu-id="0c0ac-132">StorSimple Snapshot Manager supports hello following types of volumes:</span></span>
   
   * <span data-ttu-id="0c0ac-133">基本磁碟區</span><span class="sxs-lookup"><span data-stu-id="0c0ac-133">Basic volumes</span></span>
   * <span data-ttu-id="0c0ac-134">簡單磁碟區</span><span class="sxs-lookup"><span data-stu-id="0c0ac-134">Simple volumes</span></span>
   * <span data-ttu-id="0c0ac-135">動態磁碟區</span><span class="sxs-lookup"><span data-stu-id="0c0ac-135">Dynamic volumes</span></span>
   * <span data-ttu-id="0c0ac-136">鏡像動態磁碟區 (RAID 1)</span><span class="sxs-lookup"><span data-stu-id="0c0ac-136">Mirrored dynamic volumes (RAID 1)</span></span>
   * <span data-ttu-id="0c0ac-137">叢集共用磁碟區</span><span class="sxs-lookup"><span data-stu-id="0c0ac-137">Cluster-shared volumes</span></span>
     
     <span data-ttu-id="0c0ac-138">Hello StorSimple 裝置或 StorSimple 虛擬裝置上建立磁碟區的相關資訊，請太[步驟 6： 建立磁碟區](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)，請在[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-138">For information about creating volumes on hello StorSimple device or StorSimple virtual device, go too[Step 6: Create a volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume), in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

## <a name="install-a-new-storsimple-snapshot-manager"></a><span data-ttu-id="0c0ac-139">安裝新的 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="0c0ac-139">Install a new StorSimple Snapshot Manager</span></span>
<span data-ttu-id="0c0ac-140">安裝 StorSimple Snapshot Manager 之前, 請確定您建立 hello StorSimple 裝置或 StorSimple 虛擬裝置的 hello 磁碟區會掛接、 初始化，且格式中所述[設定必要條件](#configure-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-140">Before installing StorSimple Snapshot Manager, make sure that hello volumes you created on hello StorSimple device or StorSimple virtual device are mounted, initialized, and formatted as described in [Configure prerequisites](#configure-prerequisites).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="0c0ac-141">StorSimple 虛擬裝置 hello 主機必須是 Microsoft Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-141">For a StorSimple virtual device, hello host must be a Microsoft Azure Virtual Machine.</span></span> 
> * <span data-ttu-id="0c0ac-142">hello 主機必須執行 Windows 2008 R2、 Windows Server 2012 或 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-142">hello host must be running Windows 2008 R2, Windows Server 2012, or Windows Server 2012 R2.</span></span> <span data-ttu-id="0c0ac-143">如果您的伺服器執行 Windows Server 2008 R2，您也必須安裝 Windows Server 2008 SP1 和 Windows Management Framework 3.0。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-143">If your server is running Windows Server 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0.</span></span>
> * <span data-ttu-id="0c0ac-144">您可以連接 hello 裝置 tooStorSimple Snapshot Manager 之前，您必須設定從 hello 主機 toohello StorSimple 裝置的 iSCSI 連線。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-144">You must configure an iSCSI connection from hello host toohello StorSimple device before you can connect hello device tooStorSimple Snapshot Manager.</span></span>

<span data-ttu-id="0c0ac-145">請遵循這些步驟 toocomplete StorSimple Snapshot Manager 的全新安裝。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-145">Follow these steps toocomplete a fresh installation of StorSimple Snapshot Manager.</span></span> <span data-ttu-id="0c0ac-146">如果您要安裝升級，請移至太[升級或重新安裝 StorSimple Snapshot Manager](#upgrade-or-reinstall-storsimple-snapshot-manager)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-146">If you are installing an upgrade, go too[Upgrade or reinstall StorSimple Snapshot Manager](#upgrade-or-reinstall-storsimple-snapshot-manager).</span></span>

* <span data-ttu-id="0c0ac-147">步驟 1：安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="0c0ac-147">Step 1: Install StorSimple Snapshot Manager</span></span> 
* <span data-ttu-id="0c0ac-148">步驟 2: StorSimple Snapshot Manager tooa 裝置連線</span><span class="sxs-lookup"><span data-stu-id="0c0ac-148">Step 2: Connect StorSimple Snapshot Manager tooa device</span></span> 
* <span data-ttu-id="0c0ac-149">步驟 3： 確認 hello 連線 toohello 裝置</span><span class="sxs-lookup"><span data-stu-id="0c0ac-149">Step 3: Verify hello connection toohello device</span></span> 

### <a name="step-1-install-storsimple-snapshot-manager"></a><span data-ttu-id="0c0ac-150">步驟 1：安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="0c0ac-150">Step 1: Install StorSimple Snapshot Manager</span></span>
<span data-ttu-id="0c0ac-151">使用下列步驟 tooinstall StorSimple Snapshot Manager hello。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-151">Use hello following steps tooinstall StorSimple Snapshot Manager.</span></span>

#### <a name="tooinstall-storsimple-snapshot-manager"></a><span data-ttu-id="0c0ac-152">tooinstall StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="0c0ac-152">tooinstall StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="0c0ac-153">下載 hello StorSimple Snapshot Manager 軟體 (跳過[StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) hello Microsoft 下載中心中) 並將它儲存在本機 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-153">Download hello StorSimple Snapshot Manager software (go too[StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) in hello Microsoft Download Center) and save it locally on hello host.</span></span>
2. <span data-ttu-id="0c0ac-154">在檔案總管 中，hello 壓縮的資料夾，以滑鼠右鍵按一下，然後按一下**擷取所有**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-154">In File Explorer, right-click hello compressed folder, and then click **Extract all**.</span></span>
3. <span data-ttu-id="0c0ac-155">在 hello**解壓縮壓縮 (Zipped) 資料夾**視窗中的，於 hello**選取目的地並解壓縮檔案**方塊中，輸入或瀏覽您要擷取的 toofile toobe toohello 路徑。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-155">In hello **Extract Compressed (Zipped) Folders** window, in hello **Select a destination and extract files** box, type or browse toohello path where you would like toofile toobe extracted.</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="0c0ac-156">您必須安裝 StorSimple Snapshot Manager hello c： 磁碟機上。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-156">You must install StorSimple Snapshot Manager on hello C: drive.</span></span>
    
4. <span data-ttu-id="0c0ac-157">選取 hello**顯示解壓縮的檔案時完成**核取方塊，然後**擷取**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-157">Select hello **Show extracted files when complete** check box, and then click **Extract**.</span></span>
   
    ![解壓縮檔案對話方塊](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. <span data-ttu-id="0c0ac-159">Hello 解壓縮完成時，會開啟 hello 目的地資料夾。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-159">When hello extraction is finished, hello destination folder opens.</span></span> <span data-ttu-id="0c0ac-160">按兩下 hello 應用程式安裝圖示會出現在 hello 目的地資料夾。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-160">Double-click hello application setup icon that appears in hello destination folder.</span></span>
6. <span data-ttu-id="0c0ac-161">當 hello**安裝成功**訊息出現時，按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-161">When hello **Setup Successful** message appears, click **Close**.</span></span> <span data-ttu-id="0c0ac-162">您應該在桌面上會看到 hello StorSimple Snapshot Manager 圖示。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-162">You should see hello StorSimple Snapshot Manager icon on your desktop.</span></span>
   
    ![桌面圖示](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a><span data-ttu-id="0c0ac-164">步驟 2: StorSimple Snapshot Manager tooa 裝置連線</span><span class="sxs-lookup"><span data-stu-id="0c0ac-164">Step 2: Connect StorSimple Snapshot Manager tooa device</span></span>
<span data-ttu-id="0c0ac-165">使用下列步驟 tooconnect StorSimple Snapshot Manager tooa StorSimple 裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-165">Use hello following steps tooconnect StorSimple Snapshot Manager tooa StorSimple device.</span></span>

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a><span data-ttu-id="0c0ac-166">tooconnect StorSimple Snapshot Manager tooa 裝置</span><span class="sxs-lookup"><span data-stu-id="0c0ac-166">tooconnect StorSimple Snapshot Manager tooa device</span></span>
1. <span data-ttu-id="0c0ac-167">按一下桌面上的 hello StorSimple Snapshot Manager 圖示。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-167">Click hello StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="0c0ac-168">hello StorSimple Snapshot Manager 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-168">hello StorSimple Snapshot Manager window appears.</span></span> <span data-ttu-id="0c0ac-169">hello 視窗包含**範圍** 窗格中，**結果** 窗格中，和**動作**窗格。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-169">hello window contains a **Scope** pane, a **Results** pane, and an **Actions** pane.</span></span> 
   
    ![StorSimple Snapshot Manager 使用者介面](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * <span data-ttu-id="0c0ac-171">hello**範圍**窗格 （hello 左窗格） 包含組織樹狀結構中的節點清單。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-171">hello **Scope** pane (hello left pane) contains a list of nodes organized in a tree structure.</span></span> <span data-ttu-id="0c0ac-172">您可以展開一些節點 tooselect 檢視或特定的資料相關的 toothat 節點。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-172">You can expand some nodes tooselect a view or specific data related toothat node.</span></span> <span data-ttu-id="0c0ac-173">按一下 hello 箭號圖示 tooexpand 或摺疊節點。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-173">Click hello arrow icon tooexpand or collapse a node.</span></span> <span data-ttu-id="0c0ac-174">以滑鼠右鍵按一下項目在 hello**範圍**窗格 toosee 該項目的可用動作的清單。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-174">Right-click an item in hello **Scope** pane toosee a list of available actions for that item.</span></span>
   * <span data-ttu-id="0c0ac-175">hello**結果**窗格 （hello 中央窗格） 包含 hello 節點、 檢視表或您在 hello 中選取的資料相關的詳細的狀態資訊**範圍**窗格。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-175">hello **Results** pane (hello center pane) contains detailed status information about hello node, view, or data that you selected in hello **Scope** pane.</span></span>
   * <span data-ttu-id="0c0ac-176">hello**動作**窗格會列出您可以在 hello 節點、 檢視表或您在 hello 中選取的資料執行的 hello 作業**範圍**窗格。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-176">hello **Actions** pane lists hello operations that you can perform on hello node, view, or data that you selected in hello **Scope** pane.</span></span>
     
     <span data-ttu-id="0c0ac-177">Hello StorSimple Snapshot Manager 使用者介面的完整說明，請參閱[StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-177">For a complete description of hello StorSimple Snapshot Manager user interface, see [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>
2. <span data-ttu-id="0c0ac-178">在 hello**範圍**窗格中，以滑鼠右鍵按一下 hello**裝置**節點，然後再按一下**設定裝置**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-178">In hello **Scope** pane, right-click hello **Devices** node, and then click **Configure a device**.</span></span> <span data-ttu-id="0c0ac-179">hello**設定裝置** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-179">hello **Configure a Device** dialog box appears.</span></span>
   
    ![設定裝置](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. <span data-ttu-id="0c0ac-181">在 hello**裝置**清單方塊中，選取 hello hello Microsoft Azure StorSimple 裝置的虛擬裝置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-181">In hello **Device** list box, select hello IP address of hello Microsoft Azure StorSimple device or virtual device.</span></span> <span data-ttu-id="0c0ac-182">在 hello**密碼**文字方塊中，您建立 hello 裝置 hello Azure 入口網站中的型別 hello StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-182">In hello **Password** text box, type hello StorSimple Snapshot Manager password that you created for hello device in hello Azure portal.</span></span> <span data-ttu-id="0c0ac-183">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-183">Click **OK**.</span></span>
4. <span data-ttu-id="0c0ac-184">StorSimple Snapshot Manager 搜尋您所識別的 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-184">StorSimple Snapshot Manager searches for hello device that you identified.</span></span> <span data-ttu-id="0c0ac-185">如果使用 hello 裝置，StorSimple Snapshot Manager 就會加入連接。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-185">If hello device is available, StorSimple Snapshot Manager adds a connection.</span></span> <span data-ttu-id="0c0ac-186">您可以[確認 hello 連線 toohello 裝置](#to-verify-the-connection)hello 連線的 tooconfirm 成功加入。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-186">You can [verify hello connection toohello device](#to-verify-the-connection) tooconfirm that hello connection was added successfully.</span></span>
   
    <span data-ttu-id="0c0ac-187">如果因為任何原因無法使用 hello 裝置，StorSimple Snapshot Manager 就會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-187">If hello device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> <span data-ttu-id="0c0ac-188">按一下**確定**tooclose hello 錯誤訊息，然後按一下**取消**tooclose hello**設定裝置** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-188">Click **OK** tooclose hello error message, and then click **Cancel** tooclose hello **Configure a Device** dialog box.</span></span>
5. <span data-ttu-id="0c0ac-189">連接 tooa 裝置之後，StorSimple Snapshot Manager 匯入該裝置，設定每個磁碟區群組，前提是 hello 磁碟區群組有相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-189">When it connects tooa device, StorSimple Snapshot Manager imports each volume group configured for that device, provided that hello volume group has associated backups.</span></span> <span data-ttu-id="0c0ac-190">不會匯入沒有相關聯備份的磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-190">Volume groups that do not have associated backups are not imported.</span></span> <span data-ttu-id="0c0ac-191">此外，不會匯入為磁碟區群組建立的備份原則。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-191">Additionally, backup policies that were created for a volume group are not imported.</span></span> <span data-ttu-id="0c0ac-192">toosee hello 匯入的群組，以滑鼠右鍵按一下 hello 最上層**磁碟區群組**節點 hello**範圍** 窗格中，然後按一下**切換匯入的群組**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-192">toosee hello imported groups, right-click hello top-most **Volume Groups** node in hello **Scope** pane, and click **Toggle imported groups**.</span></span>

### <a name="step-3-verify-hello-connection-toohello-device"></a><span data-ttu-id="0c0ac-193">步驟 3： 確認 hello 連線 toohello 裝置</span><span class="sxs-lookup"><span data-stu-id="0c0ac-193">Step 3: Verify hello connection toohello device</span></span>
<span data-ttu-id="0c0ac-194">使用下列步驟 tooverify StorSimple Snapshot Manager 是連接的 toohello StorSimple 裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-194">Use hello following steps tooverify that StorSimple Snapshot Manager is connected toohello StorSimple device.</span></span>

#### <a name="tooverify-hello-connection"></a><span data-ttu-id="0c0ac-195">tooverify hello 連線</span><span class="sxs-lookup"><span data-stu-id="0c0ac-195">tooverify hello connection</span></span>
1. <span data-ttu-id="0c0ac-196">在 [hello**範圍**] 窗格中，按一下 hello**裝置**節點。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-196">In hello **Scope** pane, click hello **Devices** node.</span></span>
   
    ![StorSimple Snapshot Manager 裝置狀態](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. <span data-ttu-id="0c0ac-198">檢查 hello**結果**窗格：</span><span class="sxs-lookup"><span data-stu-id="0c0ac-198">Check hello **Results** pane:</span></span> 
   
   * <span data-ttu-id="0c0ac-199">如果在 hello 裝置圖示上出現綠色指示器和**可用**會出現在 hello**狀態**資料行，然後 hello 裝置已連線。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-199">If a green indicator appears on hello device icon and **Available** appears in hello **Status** column, then hello device is connected.</span></span> 
   * <span data-ttu-id="0c0ac-200">如果在 hello 裝置圖示上出現紅色指示器，且無法使用出現在 hello**狀態**資料行，然後 hello 裝置未連線。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-200">If a red indicator appears on hello device icon and Unavailable appears in hello **Status** column, then hello device is not connected.</span></span> 
   * <span data-ttu-id="0c0ac-201">如果**正在重新整理**會出現在 hello**狀態**資料行，然後 StorSimple Snapshot Manager 正在擷取磁碟區群組和連接的裝置相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-201">If **Refreshing** appears in hello **Status** column, then StorSimple Snapshot Manager is retrieving volume groups and associated backups for a connected device.</span></span>

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a><span data-ttu-id="0c0ac-202">升級或重新安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="0c0ac-202">Upgrade or reinstall StorSimple Snapshot Manager</span></span>
<span data-ttu-id="0c0ac-203">您應該完全解除安裝 StorSimple Snapshot Manager 才能升級或重新安裝 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-203">You should uninstall StorSimple Snapshot Manager completely before you upgrade or reinstall hello software.</span></span> 

<span data-ttu-id="0c0ac-204">重新安裝 StorSimple Snapshot Manager 之前, 備份 hello 現有 StorSimple Snapshot Manager 資料庫 hello 主機電腦上。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-204">Before reinstalling StorSimple Snapshot Manager, back up hello existing StorSimple Snapshot Manager database on hello host computer.</span></span> <span data-ttu-id="0c0ac-205">這會儲存 hello 備份原則和組態資訊，以便您可以輕鬆地從備份還原此資料。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-205">This saves hello backup policies and configuration information so that you can easily restore this data from backup.</span></span>

<span data-ttu-id="0c0ac-206">如果您要升級或重新安裝 StorSimple Snapshot Manager，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0c0ac-206">Follow these steps if you are upgrading or reinstalling StorSimple Snapshot Manager:</span></span>

* <span data-ttu-id="0c0ac-207">步驟 1：解除安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="0c0ac-207">Step 1: Uninstall StorSimple Snapshot Manager</span></span> 
* <span data-ttu-id="0c0ac-208">步驟 2： 備份 hello StorSimple Snapshot Manager 資料庫</span><span class="sxs-lookup"><span data-stu-id="0c0ac-208">Step 2: Back up hello StorSimple Snapshot Manager database</span></span> 
* <span data-ttu-id="0c0ac-209">步驟 3： 重新安裝 StorSimple Snapshot Manager 及 hello 資料庫還原</span><span class="sxs-lookup"><span data-stu-id="0c0ac-209">Step 3: Reinstall StorSimple Snapshot Manager and restore hello database</span></span> 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a><span data-ttu-id="0c0ac-210">步驟 1：解除安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="0c0ac-210">Step 1: Uninstall StorSimple Snapshot Manager</span></span>
<span data-ttu-id="0c0ac-211">使用下列步驟 toouninstall StorSimple Snapshot Manager hello。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-211">Use hello following steps toouninstall StorSimple Snapshot Manager.</span></span>

#### <a name="toouninstall-storsimple-snapshot-manager"></a><span data-ttu-id="0c0ac-212">toouninstall StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="0c0ac-212">toouninstall StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="0c0ac-213">Hello 主機電腦上，開啟 hello**控制台**，按一下 **程式**，然後按一下**程式和功能**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-213">On hello host computer, open hello **Control Panel**, click **Programs**, and then click **Programs and Features**.</span></span>
2. <span data-ttu-id="0c0ac-214">在 hello 左窗格中，按一下 **解除安裝或變更程式**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-214">In hello left pane, click **Uninstall or change a program**.</span></span>
3. <span data-ttu-id="0c0ac-215">以滑鼠右鍵按一下 StorSimple Snapshot Manager，然後按一下解除安裝。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-215">Right-click **StorSimple Snapshot Manager**, and then click **Uninstall**.</span></span>
4. <span data-ttu-id="0c0ac-216">這樣會啟動 hello StorSimple Snapshot Manager 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-216">This starts hello StorSimple Snapshot Manager Setup program.</span></span> <span data-ttu-id="0c0ac-217">按一下 修改安裝程式，然後按一下解除安裝。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-217">Click **Modify Setup**, and then click **Uninstall**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0c0ac-218">如果有 hello 背景中執行任何 MMC 程序，例如 StorSimple Snapshot Manager 或磁碟管理，hello 解除安裝會失敗，而且您會收到訊息 tooclose MMC 之前的所有執行個體就會嘗試 toouninstall hello 程式。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-218">If there are any MMC processes running in hello background, such as StorSimple Snapshot Manager or Disk Management, hello uninstall will fail and you will receive a message tooclose all instances of MMC before you attempt toouninstall hello program.</span></span> <span data-ttu-id="0c0ac-219">選取**自動關閉應用程式，並嘗試的 toorestart 它們在安裝後完成**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-219">Select **Automatically close applications and attempt toorestart them after setup is complete**, and then click **OK**.</span></span>
   > 
   > 
5. <span data-ttu-id="0c0ac-220">當 hello 解除安裝程序完成，**安裝成功**會出現訊息。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-220">When hello uninstall process is finished, a **Setup Successful** message appears.</span></span> <span data-ttu-id="0c0ac-221">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-221">Click **Close**.</span></span>

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a><span data-ttu-id="0c0ac-222">步驟 2： 備份 hello StorSimple Snapshot Manager 資料庫</span><span class="sxs-lookup"><span data-stu-id="0c0ac-222">Step 2: Back up hello StorSimple Snapshot Manager database</span></span>
<span data-ttu-id="0c0ac-223">使用下列步驟 toocreate hello 和儲存一份 hello StorSimple Snapshot Manager 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-223">Use hello following steps toocreate and save a copy of hello StorSimple Snapshot Manager database.</span></span>

#### <a name="tooback-up-hello-database"></a><span data-ttu-id="0c0ac-224">tooback hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="0c0ac-224">tooback up hello database</span></span>
1. <span data-ttu-id="0c0ac-225">停止 Microsoft StorSimple 管理服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="0c0ac-225">Stop hello Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="0c0ac-226">啟動伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-226">Start Server Manager.</span></span>
   2. <span data-ttu-id="0c0ac-227">在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-227">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="0c0ac-228">在 hello**服務**頁面上，選取**Microsoft StorSimple 管理服務**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-228">On hello **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="0c0ac-229">在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下 **停止 hello 服務**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-229">In hello right pane, under **Microsoft StorSimple Management Service**, click **Stop hello service**.</span></span>
      
        ![停止 hello StorSimple 裝置管理員服務](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. <span data-ttu-id="0c0ac-231">瀏覽 tooC:\ProgramData\Microsoft\StorSimple\BACatalog。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-231">Browse tooC:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0c0ac-232">ProgramData 是隱藏的資料夾。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-232">ProgramData is a hidden folder.</span></span>
  
3. <span data-ttu-id="0c0ac-233">尋找 hello 類別目錄 XML 檔案，複製 hello 檔案，並存放區 hello 複製在安全的位置或 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-233">Find hello catalog XML file, copy hello file, and store hello copy in a safe location or in hello cloud.</span></span>
   
    ![StorSimple 備份目錄檔案](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. <span data-ttu-id="0c0ac-235">重新啟動 Microsoft StorSimple 管理服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="0c0ac-235">Restart hello Microsoft StorSimple Management Service:</span></span> 
   
   1. <span data-ttu-id="0c0ac-236">在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-236">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="0c0ac-237">在 hello**服務**頁面上，選取 hello **Microsoft StorSimple 管理服務**e。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-237">On hello **Services** page, select hello **Microsoft StorSimple Management Servic**e.</span></span>
   3. <span data-ttu-id="0c0ac-238">在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下  **hello 服務重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-238">In hello right pane, under **Microsoft StorSimple Management Service**, click **Restart hello service**.</span></span> 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a><span data-ttu-id="0c0ac-239">步驟 3： 重新安裝 StorSimple Snapshot Manager 及 hello 資料庫還原</span><span class="sxs-lookup"><span data-stu-id="0c0ac-239">Step 3: Reinstall StorSimple Snapshot Manager and restore hello database</span></span>
<span data-ttu-id="0c0ac-240">tooreinstall StorSimple Snapshot Manager，請依照下列中的 hello 步驟[安裝新的 StorSimple Snapshot Manager](#install-a-new-storsimple-snapshot-manager)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-240">tooreinstall StorSimple Snapshot Manager, follow hello steps in [Install a new StorSimple Snapshot Manager](#install-a-new-storsimple-snapshot-manager).</span></span> <span data-ttu-id="0c0ac-241">然後，使用下列程序 toorestore hello StorSimple Snapshot Manager 資料庫的 hello。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-241">Then, use hello following procedure toorestore hello StorSimple Snapshot Manager database.</span></span>

#### <a name="toorestore-hello-database"></a><span data-ttu-id="0c0ac-242">toorestore hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="0c0ac-242">toorestore hello database</span></span>
1. <span data-ttu-id="0c0ac-243">停止 Microsoft StorSimple 管理服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="0c0ac-243">Stop hello Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="0c0ac-244">啟動伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-244">Start Server Manager.</span></span>
   2. <span data-ttu-id="0c0ac-245">在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-245">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="0c0ac-246">在 hello**服務**頁面上，選取**Microsoft StorSimple 管理服務**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-246">On hello **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="0c0ac-247">在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下 **停止 hello 服務**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-247">In hello right pane, under **Microsoft StorSimple Management Service**, click **Stop hello service**.</span></span>
2. <span data-ttu-id="0c0ac-248">瀏覽 tooC:\ProgramData\Microsoft\StorSimple\BACatalog。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-248">Browse tooC:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0c0ac-249">ProgramData 是隱藏的資料夾。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-249">ProgramData is a hidden folder.</span></span>
   > 
   > 
3. <span data-ttu-id="0c0ac-250">刪除 hello 類別目錄 XML 檔案，然後您稍早儲存的 hello 版本取代它。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-250">Delete hello catalog XML file, and replace it with hello version that you saved earlier.</span></span>
4. <span data-ttu-id="0c0ac-251">重新啟動 Microsoft StorSimple 管理服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="0c0ac-251">Restart hello Microsoft StorSimple Management Service:</span></span> 
   
   1. <span data-ttu-id="0c0ac-252">在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-252">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="0c0ac-253">在 hello**服務**頁面上，選取**Microsoft StorSimple 管理服務**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-253">On hello **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   3. <span data-ttu-id="0c0ac-254">在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下  **hello 服務重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-254">In hello right pane, under **Microsoft StorSimple Management Service**, click **Restart hello service**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c0ac-255">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c0ac-255">Next steps</span></span>
* <span data-ttu-id="0c0ac-256">toolearn 更多關於 StorSimple Snapshot Manager，跳過[什麼是 StorSimple Snapshot Manager？](storsimple-what-is-snapshot-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-256">toolearn more about StorSimple Snapshot Manager, go too[What is StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md).</span></span>
* <span data-ttu-id="0c0ac-257">進一步了解 hello StorSimple Snapshot Manager 使用者介面，toolearn 移過[StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-257">toolearn more about hello StorSimple Snapshot Manager user interface, go too[StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>
* <span data-ttu-id="0c0ac-258">進一步了解使用 StorSimple Snapshot Manager，toolearn 移過[使用 StorSimple Snapshot Manager tooadminister 您於 StorSimple 解決方案](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="0c0ac-258">toolearn more about using StorSimple Snapshot Manager, go too[Use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>

