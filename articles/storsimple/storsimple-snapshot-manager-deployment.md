---
title: "部署 StorSimple Snapshot Manager | Microsoft Docs"
description: "了解如何下載及安裝 StorSimple Snapshot Manager MMC 嵌入式管理單元，來管理 StorSimple 資料保護和備份功能。"
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
ms.openlocfilehash: cde355381b0d726a1ab340bc4230b2dc8f6e2c56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-storsimple-snapshot-manager-mmc-snap-in"></a><span data-ttu-id="5bed1-103">部署 StorSimple Snapshot Manager MMC 嵌入式管理單元</span><span class="sxs-lookup"><span data-stu-id="5bed1-103">Deploy the StorSimple Snapshot Manager MMC snap-in</span></span>

## <a name="overview"></a><span data-ttu-id="5bed1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5bed1-104">Overview</span></span>
<span data-ttu-id="5bed1-105">StorSimple Snapshot Manager 是 Microsoft Management Console (MMC) 嵌入式管理單元，可在 Microsoft Azure StorSimple 環境中簡化資料保護和備份管理。</span><span class="sxs-lookup"><span data-stu-id="5bed1-105">The StorSimple Snapshot Manager is a Microsoft Management Console (MMC) snap-in that simplifies data protection and backup management in a Microsoft Azure StorSimple environment.</span></span> <span data-ttu-id="5bed1-106">利用 StorSimple Snapshot Manager，您可以管理 Microsoft Azure StorSimple 內部部署和雲端儲存體，就好像是完全整合的儲存系統，並藉此簡化備份和還原程序並降低成本。</span><span class="sxs-lookup"><span data-stu-id="5bed1-106">With StorSimple Snapshot Manager, you can manage Microsoft Azure StorSimple on-premises and cloud storage as if it were a fully integrated storage system, thus simplifying backup and restore processes and reducing costs.</span></span> 

<span data-ttu-id="5bed1-107">本教學課程描述組態需求，以及安裝、移除及升級 StorSimple Snapshot Manager 的程序。</span><span class="sxs-lookup"><span data-stu-id="5bed1-107">This tutorial describes configuration requirements, as well as procedures for installing, removing, and upgrading StorSimple Snapshot Manager.</span></span>

> [!NOTE]
> * <span data-ttu-id="5bed1-108">您無法使用 StorSimple Snapshot Manager 來管理 Microsoft Azure StorSimple Virtual Arrays (也稱為 StorSimple 內部部署虛擬裝置)。</span><span class="sxs-lookup"><span data-stu-id="5bed1-108">You cannot use StorSimple Snapshot Manager to manage Microsoft Azure StorSimple Virtual Arrays (also known as StorSimple on-premises virtual devices).</span></span>
> * <span data-ttu-id="5bed1-109">如果您打算在 StorSimple 裝置上安裝 StorSimple Update 2，在 **安裝 StorSimple Update 2 之前**，請務必下載最新版的 StorSimple Snapshot Manager 並安裝它。</span><span class="sxs-lookup"><span data-stu-id="5bed1-109">If you plan to install StorSimple Update 2 on your StorSimple device, be sure to download the latest version of StorSimple Snapshot Manager and install it **before you install StorSimple Update 2**.</span></span> <span data-ttu-id="5bed1-110">最新版的 StorSimple Snapshot Manager 具回溯相容性，可搭配 Microsoft Azure StorSimple 的所有發行版本使用。</span><span class="sxs-lookup"><span data-stu-id="5bed1-110">The latest version of StorSimple Snapshot Manager is backward compatible and works with all released versions of Microsoft Azure StorSimple.</span></span> <span data-ttu-id="5bed1-111">如果您使用的是舊版的 StorSimple Snapshot Manager，您必須更新它 (安裝新版本前不需解除安裝舊版)。</span><span class="sxs-lookup"><span data-stu-id="5bed1-111">If you are using the previous version of StorSimple Snapshot Manager, you will need to update it (you do not need to uninstall the previous version before you install the new version).</span></span>


## <a name="storsimple-snapshot-manager-installation"></a><span data-ttu-id="5bed1-112">StorSimple Snapshot Manager 安裝</span><span class="sxs-lookup"><span data-stu-id="5bed1-112">StorSimple Snapshot Manager installation</span></span>
<span data-ttu-id="5bed1-113">StorSimple Snapshot Manager 可以安裝在執行 Windows Server 2008 R2 SP1、Windows Server 2012 或 Windows Server 2012 R2 作業系統的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5bed1-113">StorSimple Snapshot Manager can be installed on computers that are running the Windows Server 2008 R2 SP1, Windows Server 2012, or Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="5bed1-114">在執行 Windows 2008 R2 的伺服器上，您也必須安裝 Windows Server 2008 SP1 和 Windows Management Framework 3.0。</span><span class="sxs-lookup"><span data-stu-id="5bed1-114">On servers running Windows 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0.</span></span>

<span data-ttu-id="5bed1-115">在您安裝或升級 Microsoft Management Console (MMC) 的 StorSimple Snapshot Manager 嵌入式管理單元之前，請確定已正確設定 Microsoft Azure StorSimple 裝置及主機伺服器。</span><span class="sxs-lookup"><span data-stu-id="5bed1-115">Before you install or upgrade the StorSimple Snapshot Manager snap-in for the Microsoft Management Console (MMC), make sure that the Microsoft Azure StorSimple device and host server are configured correctly.</span></span>

## <a name="configure-prerequisites"></a><span data-ttu-id="5bed1-116">設定必要條件</span><span class="sxs-lookup"><span data-stu-id="5bed1-116">Configure prerequisites</span></span>
<span data-ttu-id="5bed1-117">下列步驟提供在安裝 StorSimple Snapshot Manager 之前必須完成之組態工作的高階概觀。</span><span class="sxs-lookup"><span data-stu-id="5bed1-117">The following steps provide a high-level overview of configuration tasks that you must complete before you install the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="5bed1-118">如需完整的 Microsoft Azure StorSimple 組態和安裝資訊，包括系統需求和逐步指示，請參閱 [部署您的內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="5bed1-118">For complete Microsoft Azure StorSimple configuration and setup information, including system requirements and step-by-step instructions, see [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5bed1-119">在您開始之前，請檢閱[部署您的內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)中的[部署設定檢查清單](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist)和[部署必要條件](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="5bed1-119">Before you begin, review the [Deployment configuration checklist](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) and and [Deployment prerequisites](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a><span data-ttu-id="5bed1-120">安裝 StorSimple Snapshot Manager 之前</span><span class="sxs-lookup"><span data-stu-id="5bed1-120">Before you install StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="5bed1-121">打開包裝、掛接和連接 Microsoft Azure StorSimple 裝置，如[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)或[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)所述。</span><span class="sxs-lookup"><span data-stu-id="5bed1-121">Unpack, mount, and connect the Microsoft Azure StorSimple device as described in [Install your StorSimple 8100 device](storsimple-8100-hardware-installation.md) or [Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>
2. <span data-ttu-id="5bed1-122">請確定主機電腦正在執行下列其中一個作業系統：</span><span class="sxs-lookup"><span data-stu-id="5bed1-122">Make sure that your host computer is running one of the following operating systems:</span></span>
   
   * <span data-ttu-id="5bed1-123">Windows Server 2008 R2 (在執行 Windows 2008 R2 的伺服器上，您也必須安裝 Windows Server 2008 SP1 和 Windows Management Framework 3.0)</span><span class="sxs-lookup"><span data-stu-id="5bed1-123">Windows Server 2008 R2 (on servers running Windows 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0)</span></span>
   * <span data-ttu-id="5bed1-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="5bed1-124">Windows Server 2012</span></span>
   * <span data-ttu-id="5bed1-125">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5bed1-125">Windows Server 2012 R2</span></span>
     
     <span data-ttu-id="5bed1-126">對於 StorSimple 虛擬裝置，主機必須是 Microsoft Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5bed1-126">For a StorSimple virtual device, the host must be a Microsoft Azure Virtual Machine.</span></span>
3. <span data-ttu-id="5bed1-127">請確定您符合所有的 Microsoft Azure StorSimple 組態需求。</span><span class="sxs-lookup"><span data-stu-id="5bed1-127">Make sure that you meet all the Microsoft Azure StorSimple configuration requirements.</span></span> <span data-ttu-id="5bed1-128">如需詳細資料，請移至 [部署必要條件](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="5bed1-128">For details, go to [Deployment prerequisites](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).</span></span>
4. <span data-ttu-id="5bed1-129">將裝置連接至主機並執行初始組態。</span><span class="sxs-lookup"><span data-stu-id="5bed1-129">Connect the device to the host and perform the initial configuration.</span></span> <span data-ttu-id="5bed1-130">如需詳細資料，請移至 [部署步驟](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps)。</span><span class="sxs-lookup"><span data-stu-id="5bed1-130">For details, go to [Deployment steps](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).</span></span>
5. <span data-ttu-id="5bed1-131">在裝置上建立磁碟區，將它們指派給主機，並確認主機可以掛接和使用它們。</span><span class="sxs-lookup"><span data-stu-id="5bed1-131">Create volumes on the device, assign them to the host, and verify that the host can mount and use them.</span></span> <span data-ttu-id="5bed1-132">StorSimple Snapshot Manager 支援下列類型的磁碟區：</span><span class="sxs-lookup"><span data-stu-id="5bed1-132">StorSimple Snapshot Manager supports the following types of volumes:</span></span>
   
   * <span data-ttu-id="5bed1-133">基本磁碟區</span><span class="sxs-lookup"><span data-stu-id="5bed1-133">Basic volumes</span></span>
   * <span data-ttu-id="5bed1-134">簡單磁碟區</span><span class="sxs-lookup"><span data-stu-id="5bed1-134">Simple volumes</span></span>
   * <span data-ttu-id="5bed1-135">動態磁碟區</span><span class="sxs-lookup"><span data-stu-id="5bed1-135">Dynamic volumes</span></span>
   * <span data-ttu-id="5bed1-136">鏡像動態磁碟區 (RAID 1)</span><span class="sxs-lookup"><span data-stu-id="5bed1-136">Mirrored dynamic volumes (RAID 1)</span></span>
   * <span data-ttu-id="5bed1-137">叢集共用磁碟區</span><span class="sxs-lookup"><span data-stu-id="5bed1-137">Cluster-shared volumes</span></span>
     
     <span data-ttu-id="5bed1-138">如需在 StorSimple 裝置或 StorSimple 虛擬裝置上建立磁碟區的詳細資訊，請移至[部署您的內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)中的[步驟 6：建立磁碟區](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)。</span><span class="sxs-lookup"><span data-stu-id="5bed1-138">For information about creating volumes on the StorSimple device or StorSimple virtual device, go to [Step 6: Create a volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume), in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

## <a name="install-a-new-storsimple-snapshot-manager"></a><span data-ttu-id="5bed1-139">安裝新的 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="5bed1-139">Install a new StorSimple Snapshot Manager</span></span>
<span data-ttu-id="5bed1-140">安裝 StorSimple Snapshot Manager 之前，請確定您在 StorSimple 裝置或 StorSimple 虛擬裝置上建立的磁碟區會掛接、初始化和格式化，如 [設定必要條件](#configure-prerequisites)中所述。</span><span class="sxs-lookup"><span data-stu-id="5bed1-140">Before installing StorSimple Snapshot Manager, make sure that the volumes you created on the StorSimple device or StorSimple virtual device are mounted, initialized, and formatted as described in [Configure prerequisites](#configure-prerequisites).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="5bed1-141">對於 StorSimple 虛擬裝置，主機必須是 Microsoft Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5bed1-141">For a StorSimple virtual device, the host must be a Microsoft Azure Virtual Machine.</span></span> 
> * <span data-ttu-id="5bed1-142">主機必須執行 Windows 2008 R2、Windows Server 2012 或 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="5bed1-142">The host must be running Windows 2008 R2, Windows Server 2012, or Windows Server 2012 R2.</span></span> <span data-ttu-id="5bed1-143">如果您的伺服器執行 Windows Server 2008 R2，您也必須安裝 Windows Server 2008 SP1 和 Windows Management Framework 3.0。</span><span class="sxs-lookup"><span data-stu-id="5bed1-143">If your server is running Windows Server 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0.</span></span>
> * <span data-ttu-id="5bed1-144">將裝置連接至 StorSimple Snapshot Manager 之前，您必須設定從主機到 StorSimple 裝置的 iSCSI 連接。</span><span class="sxs-lookup"><span data-stu-id="5bed1-144">You must configure an iSCSI connection from the host to the StorSimple device before you can connect the device to StorSimple Snapshot Manager.</span></span>

<span data-ttu-id="5bed1-145">請遵循下列步驟來完成 StorSimple Snapshot Manager 的全新安裝。</span><span class="sxs-lookup"><span data-stu-id="5bed1-145">Follow these steps to complete a fresh installation of StorSimple Snapshot Manager.</span></span> <span data-ttu-id="5bed1-146">如果您要安裝升級，請至 [升級或重新安裝 StorSimple Snapshot Manager](#upgrade-or-reinstall-storsimple-snapshot-manager)。</span><span class="sxs-lookup"><span data-stu-id="5bed1-146">If you are installing an upgrade, go to [Upgrade or reinstall StorSimple Snapshot Manager](#upgrade-or-reinstall-storsimple-snapshot-manager).</span></span>

* <span data-ttu-id="5bed1-147">步驟 1：安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="5bed1-147">Step 1: Install StorSimple Snapshot Manager</span></span> 
* <span data-ttu-id="5bed1-148">步驟 2：連接 StorSimple Snapshot Manager 和裝置</span><span class="sxs-lookup"><span data-stu-id="5bed1-148">Step 2: Connect StorSimple Snapshot Manager to a device</span></span> 
* <span data-ttu-id="5bed1-149">步驟 3：確認裝置的連接</span><span class="sxs-lookup"><span data-stu-id="5bed1-149">Step 3: Verify the connection to the device</span></span> 

### <a name="step-1-install-storsimple-snapshot-manager"></a><span data-ttu-id="5bed1-150">步驟 1：安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="5bed1-150">Step 1: Install StorSimple Snapshot Manager</span></span>
<span data-ttu-id="5bed1-151">使用下列步驟來安裝 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5bed1-151">Use the following steps to install StorSimple Snapshot Manager.</span></span>

#### <a name="to-install-storsimple-snapshot-manager"></a><span data-ttu-id="5bed1-152">安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="5bed1-152">To install StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="5bed1-153">下載 StorSimple Snapshot Manager 軟體 (移至 Microsoft 下載中心的 [StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) ) 並將軟體儲存在本機主機上。</span><span class="sxs-lookup"><span data-stu-id="5bed1-153">Download the StorSimple Snapshot Manager software (go to [StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) in the Microsoft Download Center) and save it locally on the host.</span></span>
2. <span data-ttu-id="5bed1-154">在檔案總管中，以滑鼠右鍵按一下壓縮的資料夾，然後按一下 [ **全部解壓縮**]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-154">In File Explorer, right-click the compressed folder, and then click **Extract all**.</span></span>
3. <span data-ttu-id="5bed1-155">在 [解壓縮壓縮 (壓縮) 資料夾] 視窗的 [選取目的地並解壓縮檔案] 方塊中，輸入或瀏覽至您想要解壓縮檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="5bed1-155">In the **Extract Compressed (Zipped) Folders** window, in the **Select a destination and extract files** box, type or browse to the path where you would like to file to be extracted.</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="5bed1-156">您必須在 C: 磁碟機上安裝 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5bed1-156">You must install StorSimple Snapshot Manager on the C: drive.</span></span>
    
4. <span data-ttu-id="5bed1-157">選取 [完成時顯示解壓縮檔案] 核取方塊，然後再按一下 [解壓縮]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-157">Select the **Show extracted files when complete** check box, and then click **Extract**.</span></span>
   
    ![解壓縮檔案對話方塊](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. <span data-ttu-id="5bed1-159">解壓縮完成時，目的地資料夾會隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="5bed1-159">When the extraction is finished, the destination folder opens.</span></span> <span data-ttu-id="5bed1-160">按兩下出現在目的地資料夾中的應用程式安裝圖示。</span><span class="sxs-lookup"><span data-stu-id="5bed1-160">Double-click the application setup icon that appears in the destination folder.</span></span>
6. <span data-ttu-id="5bed1-161">當**安裝成功**訊息出現時，按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-161">When the **Setup Successful** message appears, click **Close**.</span></span> <span data-ttu-id="5bed1-162">您應該會在桌面上看到 StorSimple Snapshot Manager 圖示。</span><span class="sxs-lookup"><span data-stu-id="5bed1-162">You should see the StorSimple Snapshot Manager icon on your desktop.</span></span>
   
    ![桌面圖示](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-to-a-device"></a><span data-ttu-id="5bed1-164">步驟 2：連接 StorSimple Snapshot Manager 和裝置</span><span class="sxs-lookup"><span data-stu-id="5bed1-164">Step 2: Connect StorSimple Snapshot Manager to a device</span></span>
<span data-ttu-id="5bed1-165">使用下列步驟連接 StorSimple Snapshot Manager 和 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="5bed1-165">Use the following steps to connect StorSimple Snapshot Manager to a StorSimple device.</span></span>

#### <a name="to-connect-storsimple-snapshot-manager-to-a-device"></a><span data-ttu-id="5bed1-166">連接 StorSimple Snapshot Manager 和裝置</span><span class="sxs-lookup"><span data-stu-id="5bed1-166">To connect StorSimple Snapshot Manager to a device</span></span>
1. <span data-ttu-id="5bed1-167">按一下桌面上的 StorSimple Snapshot Manager 圖示。</span><span class="sxs-lookup"><span data-stu-id="5bed1-167">Click the StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="5bed1-168">StorSimple Snapshot Manager 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="5bed1-168">The StorSimple Snapshot Manager window appears.</span></span> <span data-ttu-id="5bed1-169">此視窗包含 [範圍] 窗格、[結果] 窗格和 [動作] 窗格。</span><span class="sxs-lookup"><span data-stu-id="5bed1-169">The window contains a **Scope** pane, a **Results** pane, and an **Actions** pane.</span></span> 
   
    ![StorSimple Snapshot Manager 使用者介面](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * <span data-ttu-id="5bed1-171">[ **範圍** ] 窗格 (左窗格) 包含在樹狀結構中組織的節點清單。</span><span class="sxs-lookup"><span data-stu-id="5bed1-171">The **Scope** pane (the left pane) contains a list of nodes organized in a tree structure.</span></span> <span data-ttu-id="5bed1-172">您可以展開一些節點來選取檢視或與該節點相關的特定資料。</span><span class="sxs-lookup"><span data-stu-id="5bed1-172">You can expand some nodes to select a view or specific data related to that node.</span></span> <span data-ttu-id="5bed1-173">按一下箭頭圖示來展開或摺疊節點。</span><span class="sxs-lookup"><span data-stu-id="5bed1-173">Click the arrow icon to expand or collapse a node.</span></span> <span data-ttu-id="5bed1-174">以滑鼠右鍵按一下 [ **範圍** ] 窗格中的項目，以查看該項目之可用動作的清單。</span><span class="sxs-lookup"><span data-stu-id="5bed1-174">Right-click an item in the **Scope** pane to see a list of available actions for that item.</span></span>
   * <span data-ttu-id="5bed1-175">[結果] 窗格 (中央窗格) 包含您在 [範圍] 窗格中選取之節點、檢視或資料的相關詳細狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="5bed1-175">The **Results** pane (the center pane) contains detailed status information about the node, view, or data that you selected in the **Scope** pane.</span></span>
   * <span data-ttu-id="5bed1-176">[動作] 窗格會列出您在 [範圍] 窗格中選取的節點、檢視或資料上可以執行的作業。</span><span class="sxs-lookup"><span data-stu-id="5bed1-176">The **Actions** pane lists the operations that you can perform on the node, view, or data that you selected in the **Scope** pane.</span></span>
     
     <span data-ttu-id="5bed1-177">如需 StorSimple Snapshot Manager 使用者介面的完整描述，請參閱 [StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="5bed1-177">For a complete description of the StorSimple Snapshot Manager user interface, see [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>
2. <span data-ttu-id="5bed1-178">在 [範圍] 窗格中，以滑鼠右鍵按一下 [裝置] 節點，然後按一下 [設定裝置]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-178">In the **Scope** pane, right-click the **Devices** node, and then click **Configure a device**.</span></span> <span data-ttu-id="5bed1-179">[ **設定裝置** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="5bed1-179">The **Configure a Device** dialog box appears.</span></span>
   
    ![設定裝置](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. <span data-ttu-id="5bed1-181">在 [ **裝置** ] 清單方塊中，選取 Microsoft Azure StorSimple 裝置或虛擬裝置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bed1-181">In the **Device** list box, select the IP address of the Microsoft Azure StorSimple device or virtual device.</span></span> <span data-ttu-id="5bed1-182">在 [密碼] 文字方塊中，輸入您在 Azure 入口網站中為裝置建立的 StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="5bed1-182">In the **Password** text box, type the StorSimple Snapshot Manager password that you created for the device in the Azure portal.</span></span> <span data-ttu-id="5bed1-183">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5bed1-183">Click **OK**.</span></span>
4. <span data-ttu-id="5bed1-184">StorSimple Snapshot Manager 會搜尋您所識別的裝置。</span><span class="sxs-lookup"><span data-stu-id="5bed1-184">StorSimple Snapshot Manager searches for the device that you identified.</span></span> <span data-ttu-id="5bed1-185">如果裝置可供使用，StorSimple Snapshot Manager 會新增連接。</span><span class="sxs-lookup"><span data-stu-id="5bed1-185">If the device is available, StorSimple Snapshot Manager adds a connection.</span></span> <span data-ttu-id="5bed1-186">您可以 [確認裝置連接](#to-verify-the-connection) 以確認連接已成功新增。</span><span class="sxs-lookup"><span data-stu-id="5bed1-186">You can [verify the connection to the device](#to-verify-the-connection) to confirm that the connection was added successfully.</span></span>
   
    <span data-ttu-id="5bed1-187">如果由於任何原因而無法使用裝置，StorSimple Snapshot Manager 會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5bed1-187">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> <span data-ttu-id="5bed1-188">按一下 [確定] 以關閉錯誤訊息，然後按一下 [取消] 以關閉 [設定裝置] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5bed1-188">Click **OK** to close the error message, and then click **Cancel** to close the **Configure a Device** dialog box.</span></span>
5. <span data-ttu-id="5bed1-189">當它連接到裝置時，StorSimple Snapshot Manager 會匯入為該裝置設定的每個磁碟區群組，前提是磁碟區群組具有相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="5bed1-189">When it connects to a device, StorSimple Snapshot Manager imports each volume group configured for that device, provided that the volume group has associated backups.</span></span> <span data-ttu-id="5bed1-190">不會匯入沒有相關聯備份的磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="5bed1-190">Volume groups that do not have associated backups are not imported.</span></span> <span data-ttu-id="5bed1-191">此外，不會匯入為磁碟區群組建立的備份原則。</span><span class="sxs-lookup"><span data-stu-id="5bed1-191">Additionally, backup policies that were created for a volume group are not imported.</span></span> <span data-ttu-id="5bed1-192">若要查看匯入的群組，請以滑鼠右鍵按一下 [範圍] 窗格中最上層的 [磁碟區群組] 節點，然後按一下 [切換匯入的群組]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-192">To see the imported groups, right-click the top-most **Volume Groups** node in the **Scope** pane, and click **Toggle imported groups**.</span></span>

### <a name="step-3-verify-the-connection-to-the-device"></a><span data-ttu-id="5bed1-193">步驟 3：確認裝置的連接</span><span class="sxs-lookup"><span data-stu-id="5bed1-193">Step 3: Verify the connection to the device</span></span>
<span data-ttu-id="5bed1-194">使用下列步驟來確認 StorSimple Snapshot Manager 已連接至 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="5bed1-194">Use the following steps to verify that StorSimple Snapshot Manager is connected to the StorSimple device.</span></span>

#### <a name="to-verify-the-connection"></a><span data-ttu-id="5bed1-195">確認連接</span><span class="sxs-lookup"><span data-stu-id="5bed1-195">To verify the connection</span></span>
1. <span data-ttu-id="5bed1-196">在 [範圍] 窗格中，按一下 [裝置] 節點。</span><span class="sxs-lookup"><span data-stu-id="5bed1-196">In the **Scope** pane, click the **Devices** node.</span></span>
   
    ![StorSimple Snapshot Manager 裝置狀態](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. <span data-ttu-id="5bed1-198">檢查 [ **結果** ] 窗格：</span><span class="sxs-lookup"><span data-stu-id="5bed1-198">Check the **Results** pane:</span></span> 
   
   * <span data-ttu-id="5bed1-199">如果裝置圖示上出現綠色指標和且 [狀態] 資料行顯示為 [可用]，表示裝置已連接。</span><span class="sxs-lookup"><span data-stu-id="5bed1-199">If a green indicator appears on the device icon and **Available** appears in the **Status** column, then the device is connected.</span></span> 
   * <span data-ttu-id="5bed1-200">如果裝置圖示上出現紅色指標，且 [ **狀態** ] 資料行中顯示為無法使用，表示裝置未連接。</span><span class="sxs-lookup"><span data-stu-id="5bed1-200">If a red indicator appears on the device icon and Unavailable appears in the **Status** column, then the device is not connected.</span></span> 
   * <span data-ttu-id="5bed1-201">如果 [狀態] 資料行中顯示為 [正在重新整理]，表示 StorSimple Snapshot Manager 正在擷取磁碟區群組及連接裝置的相關聯備份。</span><span class="sxs-lookup"><span data-stu-id="5bed1-201">If **Refreshing** appears in the **Status** column, then StorSimple Snapshot Manager is retrieving volume groups and associated backups for a connected device.</span></span>

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a><span data-ttu-id="5bed1-202">升級或重新安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="5bed1-202">Upgrade or reinstall StorSimple Snapshot Manager</span></span>
<span data-ttu-id="5bed1-203">您應該先完全解除安裝 StorSimple Snapshot Manager 之後再升級或重新安裝軟體。</span><span class="sxs-lookup"><span data-stu-id="5bed1-203">You should uninstall StorSimple Snapshot Manager completely before you upgrade or reinstall the software.</span></span> 

<span data-ttu-id="5bed1-204">重新安裝 StorSimple Snapshot Manager 之前，請在主機電腦上備份現有的 StorSimple Snapshot Manager 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5bed1-204">Before reinstalling StorSimple Snapshot Manager, back up the existing StorSimple Snapshot Manager database on the host computer.</span></span> <span data-ttu-id="5bed1-205">這會儲存備份原則及組態資訊，以便您可以輕易地從備份還原這項資料。</span><span class="sxs-lookup"><span data-stu-id="5bed1-205">This saves the backup policies and configuration information so that you can easily restore this data from backup.</span></span>

<span data-ttu-id="5bed1-206">如果您要升級或重新安裝 StorSimple Snapshot Manager，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5bed1-206">Follow these steps if you are upgrading or reinstalling StorSimple Snapshot Manager:</span></span>

* <span data-ttu-id="5bed1-207">步驟 1：解除安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="5bed1-207">Step 1: Uninstall StorSimple Snapshot Manager</span></span> 
* <span data-ttu-id="5bed1-208">步驟 2：備份 StorSimple Snapshot Manager 資料庫</span><span class="sxs-lookup"><span data-stu-id="5bed1-208">Step 2: Back up the StorSimple Snapshot Manager database</span></span> 
* <span data-ttu-id="5bed1-209">步驟 3：重新安裝 StorSimple Snapshot Manager 並還原資料庫</span><span class="sxs-lookup"><span data-stu-id="5bed1-209">Step 3: Reinstall StorSimple Snapshot Manager and restore the database</span></span> 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a><span data-ttu-id="5bed1-210">步驟 1：解除安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="5bed1-210">Step 1: Uninstall StorSimple Snapshot Manager</span></span>
<span data-ttu-id="5bed1-211">使用下列步驟來解除安裝 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5bed1-211">Use the following steps to uninstall StorSimple Snapshot Manager.</span></span>

#### <a name="to-uninstall-storsimple-snapshot-manager"></a><span data-ttu-id="5bed1-212">解除安裝 StorSimple Snapshot Manager</span><span class="sxs-lookup"><span data-stu-id="5bed1-212">To uninstall StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="5bed1-213">在主機電腦上，開啟 [控制台]，按一下 [程式]，然後按一下 [程式和功能]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-213">On the host computer, open the **Control Panel**, click **Programs**, and then click **Programs and Features**.</span></span>
2. <span data-ttu-id="5bed1-214">在左窗格中，按一下 [ **解除安裝或變更程式**]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-214">In the left pane, click **Uninstall or change a program**.</span></span>
3. <span data-ttu-id="5bed1-215">以滑鼠右鍵按一下 [StorSimple Snapshot Manager]，然後按一下 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-215">Right-click **StorSimple Snapshot Manager**, and then click **Uninstall**.</span></span>
4. <span data-ttu-id="5bed1-216">這樣會啟動 StorSimple Snapshot Manager 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="5bed1-216">This starts the StorSimple Snapshot Manager Setup program.</span></span> <span data-ttu-id="5bed1-217">按一下 [修改安裝程式]，然後按一下 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-217">Click **Modify Setup**, and then click **Uninstall**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5bed1-218">如果有任何 MMC 程序在背景執行，例如 StorSimple Snapshot Manager 或磁碟管理，解除安裝將會失敗，而且在您嘗試解除安裝程式之前，您會收到關閉所有 MMC 執行個體的訊息。</span><span class="sxs-lookup"><span data-stu-id="5bed1-218">If there are any MMC processes running in the background, such as StorSimple Snapshot Manager or Disk Management, the uninstall will fail and you will receive a message to close all instances of MMC before you attempt to uninstall the program.</span></span> <span data-ttu-id="5bed1-219">選取 [自動關閉應用程式，並嘗試在安裝完成後重新啟動]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-219">Select **Automatically close applications and attempt to restart them after setup is complete**, and then click **OK**.</span></span>
   > 
   > 
5. <span data-ttu-id="5bed1-220">解除安裝程序完成時， **安裝成功** 訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="5bed1-220">When the uninstall process is finished, a **Setup Successful** message appears.</span></span> <span data-ttu-id="5bed1-221">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="5bed1-221">Click **Close**.</span></span>

### <a name="step-2-back-up-the-storsimple-snapshot-manager-database"></a><span data-ttu-id="5bed1-222">步驟 2：備份 StorSimple Snapshot Manager 資料庫</span><span class="sxs-lookup"><span data-stu-id="5bed1-222">Step 2: Back up the StorSimple Snapshot Manager database</span></span>
<span data-ttu-id="5bed1-223">使用下列步驟建立和儲存 StorSimple Snapshot Manager 資料庫的複本。</span><span class="sxs-lookup"><span data-stu-id="5bed1-223">Use the following steps to create and save a copy of the StorSimple Snapshot Manager database.</span></span>

#### <a name="to-back-up-the-database"></a><span data-ttu-id="5bed1-224">備份資料庫</span><span class="sxs-lookup"><span data-stu-id="5bed1-224">To back up the database</span></span>
1. <span data-ttu-id="5bed1-225">停止 Microsoft StorSimple 管理服務：</span><span class="sxs-lookup"><span data-stu-id="5bed1-225">Stop the Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="5bed1-226">啟動伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="5bed1-226">Start Server Manager.</span></span>
   2. <span data-ttu-id="5bed1-227">在伺服器管理員儀表板的 [工具] 功能表上，選取 [服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-227">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="5bed1-228">在 [服務] 頁面上，選取 [Microsoft StorSimple 管理服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-228">On the **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="5bed1-229">在右窗格的 [Microsoft StorSimple 管理服務] 之下，按一下 [停止服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-229">In the right pane, under **Microsoft StorSimple Management Service**, click **Stop the service**.</span></span>
      
        ![停止 StorSimple 裝置管理員服務](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. <span data-ttu-id="5bed1-231">瀏覽至 C:\ProgramData\Microsoft\StorSimple\BACatalog。</span><span class="sxs-lookup"><span data-stu-id="5bed1-231">Browse to C:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="5bed1-232">ProgramData 是隱藏的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5bed1-232">ProgramData is a hidden folder.</span></span>
  
3. <span data-ttu-id="5bed1-233">尋找目錄 XML 檔案、複製檔案，並將複本儲存在安全位置或雲端中。</span><span class="sxs-lookup"><span data-stu-id="5bed1-233">Find the catalog XML file, copy the file, and store the copy in a safe location or in the cloud.</span></span>
   
    ![StorSimple 備份目錄檔案](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. <span data-ttu-id="5bed1-235">重新啟動 Microsoft StorSimple 管理服務：</span><span class="sxs-lookup"><span data-stu-id="5bed1-235">Restart the Microsoft StorSimple Management Service:</span></span> 
   
   1. <span data-ttu-id="5bed1-236">在伺服器管理員儀表板的 [工具] 功能表上，選取 [服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-236">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="5bed1-237">在 [服務] 頁面上，選取 [Microsoft StorSimple 管理服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-237">On the **Services** page, select the **Microsoft StorSimple Management Servic**e.</span></span>
   3. <span data-ttu-id="5bed1-238">在右窗格的 [Microsoft StorSimple 管理服務] 之下，按一下 [重新啟動服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-238">In the right pane, under **Microsoft StorSimple Management Service**, click **Restart the service**.</span></span> 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-the-database"></a><span data-ttu-id="5bed1-239">步驟 3：重新安裝 StorSimple Snapshot Manager 並還原資料庫</span><span class="sxs-lookup"><span data-stu-id="5bed1-239">Step 3: Reinstall StorSimple Snapshot Manager and restore the database</span></span>
<span data-ttu-id="5bed1-240">如果要重新安裝 StorSimple Snapshot Manager，請遵循 [安裝新的 StorSimple Snapshot Manager](#install-a-new-storsimple-snapshot-manager)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="5bed1-240">To reinstall StorSimple Snapshot Manager, follow the steps in [Install a new StorSimple Snapshot Manager](#install-a-new-storsimple-snapshot-manager).</span></span> <span data-ttu-id="5bed1-241">然後，使用下列程序來還原 StorSimple Snapshot Manager 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5bed1-241">Then, use the following procedure to restore the StorSimple Snapshot Manager database.</span></span>

#### <a name="to-restore-the-database"></a><span data-ttu-id="5bed1-242">還原資料庫</span><span class="sxs-lookup"><span data-stu-id="5bed1-242">To restore the database</span></span>
1. <span data-ttu-id="5bed1-243">停止 Microsoft StorSimple 管理服務：</span><span class="sxs-lookup"><span data-stu-id="5bed1-243">Stop the Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="5bed1-244">啟動伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="5bed1-244">Start Server Manager.</span></span>
   2. <span data-ttu-id="5bed1-245">在伺服器管理員儀表板的 [工具] 功能表上，選取 [服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-245">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="5bed1-246">在 [服務] 頁面上，選取 [Microsoft StorSimple 管理服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-246">On the **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="5bed1-247">在右窗格的 [Microsoft StorSimple 管理服務] 之下，按一下 [停止服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-247">In the right pane, under **Microsoft StorSimple Management Service**, click **Stop the service**.</span></span>
2. <span data-ttu-id="5bed1-248">瀏覽至 C:\ProgramData\Microsoft\StorSimple\BACatalog。</span><span class="sxs-lookup"><span data-stu-id="5bed1-248">Browse to C:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5bed1-249">ProgramData 是隱藏的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5bed1-249">ProgramData is a hidden folder.</span></span>
   > 
   > 
3. <span data-ttu-id="5bed1-250">刪除目錄 XML 檔案，並以您稍早儲存的版本取代它。</span><span class="sxs-lookup"><span data-stu-id="5bed1-250">Delete the catalog XML file, and replace it with the version that you saved earlier.</span></span>
4. <span data-ttu-id="5bed1-251">重新啟動 Microsoft StorSimple 管理服務：</span><span class="sxs-lookup"><span data-stu-id="5bed1-251">Restart the Microsoft StorSimple Management Service:</span></span> 
   
   1. <span data-ttu-id="5bed1-252">在伺服器管理員儀表板的 [工具] 功能表上，選取 [服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-252">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="5bed1-253">在 [服務] 頁面上，選取 [Microsoft StorSimple 管理服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-253">On the **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   3. <span data-ttu-id="5bed1-254">在右窗格的 [Microsoft StorSimple 管理服務] 之下，按一下 [重新啟動服務]。</span><span class="sxs-lookup"><span data-stu-id="5bed1-254">In the right pane, under **Microsoft StorSimple Management Service**, click **Restart the service**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bed1-255">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5bed1-255">Next steps</span></span>
* <span data-ttu-id="5bed1-256">若要深入了解 StorSimple Snapshot Manager，請移至 [什麼是 StorSimple Snapshot Manager？](storsimple-what-is-snapshot-manager.md)</span><span class="sxs-lookup"><span data-stu-id="5bed1-256">To learn more about StorSimple Snapshot Manager, go to [What is StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md).</span></span>
* <span data-ttu-id="5bed1-257">若要深入了解 StorSimple Snapshot Manager 使用者介面，請移至 [StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md)</span><span class="sxs-lookup"><span data-stu-id="5bed1-257">To learn more about the StorSimple Snapshot Manager user interface, go to [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>
* <span data-ttu-id="5bed1-258">若要深入了解如何使用 StorSimple Snapshot Manager，請移至 [使用 StorSimple Snapshot Manager 來管理您的 StorSimple 解決方案](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="5bed1-258">To learn more about using StorSimple Snapshot Manager, go to [Use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>

