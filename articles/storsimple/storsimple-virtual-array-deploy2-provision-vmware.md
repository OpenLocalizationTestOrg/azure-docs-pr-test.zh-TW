---
title: "在 VMware 中的 StorSimple Virtual Array aaaProvision |Microsoft 文件"
description: "部署 StorSimple Virtual Array 的第二個教學課程，內容為如何在 VMware 中佈建虛擬裝置。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a><span data-ttu-id="9baa0-103">部署 StorSimple Virtual Array：在 VMware 中佈建</span><span class="sxs-lookup"><span data-stu-id="9baa0-103">Deploy StorSimple Virtual Array - Provision in VMware</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a><span data-ttu-id="9baa0-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9baa0-104">Overview</span></span>
<span data-ttu-id="9baa0-105">這個教學課程描述如何 tooprovision 並連接 tooa StorSimple Virtual Array 和更新版本上執行 VMware ESXi 5.5 主機系統。</span><span class="sxs-lookup"><span data-stu-id="9baa0-105">This tutorial describes how tooprovision and connect tooa StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span> <span data-ttu-id="9baa0-106">本文適用於 StorSimple 虛擬陣列在 Azure 入口網站和 Microsoft Azure 政府雲端 hello toohello 部署。</span><span class="sxs-lookup"><span data-stu-id="9baa0-106">This article applies toohello deployment of StorSimple Virtual Arrays in Azure portal and hello Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="9baa0-107">您需要系統管理員權限 tooprovision，並連線 tooa 虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="9baa0-107">You need administrator privileges tooprovision and connect tooa virtual device.</span></span> <span data-ttu-id="9baa0-108">hello 佈建和初始設定可能需要約為 10 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="9baa0-108">hello provisioning and initial setup can take around 10 minutes toocomplete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="9baa0-109">佈建的必要條件</span><span class="sxs-lookup"><span data-stu-id="9baa0-109">Provisioning prerequisites</span></span>
<span data-ttu-id="9baa0-110">hello 必要條件 tooprovision 執行 VMware ESXi 5.5 主機系統上的虛擬裝置，而且上面，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9baa0-110">hello prerequisites tooprovision a virtual device on a host system running VMware ESXi 5.5 and above, are as follows.</span></span>

### <a name="for-hello-storsimple-device-manager-service"></a><span data-ttu-id="9baa0-111">Hello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="9baa0-111">For hello StorSimple Device Manager service</span></span>
<span data-ttu-id="9baa0-112">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="9baa0-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="9baa0-113">您已完成所有 hello 步驟[準備 hello 入口網站，供 StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md)。</span><span class="sxs-lookup"><span data-stu-id="9baa0-113">You have completed all hello steps in [Prepare hello portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="9baa0-114">您已下載適用於 VMware 的 hello 虛擬裝置映像從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9baa0-114">You have downloaded hello virtual device image for VMware from hello Azure portal.</span></span> <span data-ttu-id="9baa0-115">如需詳細資訊，請參閱**步驟 3： 下載 hello 虛擬裝置映像**的[準備 hello 入口網站的 StorSimple Virtual Array 指南](storsimple-virtual-array-deploy1-portal-prep.md)。</span><span class="sxs-lookup"><span data-stu-id="9baa0-115">For more information, see **Step 3: Download hello virtual device image** of [Prepare hello portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

### <a name="for-hello-storsimple-virtual-device"></a><span data-ttu-id="9baa0-116">Hello StorSimple 虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="9baa0-116">For hello StorSimple virtual device</span></span>
<span data-ttu-id="9baa0-117">在您部署虛擬裝置之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="9baa0-117">Before you deploy a virtual device, make sure that:</span></span>

* <span data-ttu-id="9baa0-118">您必須執行 HYPER-V 的存取 tooa 主機系統 (2008 R2 或更新版本)，可以是使用的 tooa 佈建裝置。</span><span class="sxs-lookup"><span data-stu-id="9baa0-118">You have access tooa host system running Hyper-V (2008 R2 or later) that can be used tooa provision a device.</span></span>
* <span data-ttu-id="9baa0-119">hello 主機系統是無法 toodedicate hello 下列資源 tooprovision 虛擬裝置：</span><span class="sxs-lookup"><span data-stu-id="9baa0-119">hello host system is able toodedicate hello following resources tooprovision your virtual device:</span></span>

  * <span data-ttu-id="9baa0-120">至少 4 顆核心。</span><span class="sxs-lookup"><span data-stu-id="9baa0-120">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="9baa0-121">至少 8 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="9baa0-121">At least 8 GB of RAM.</span></span> <span data-ttu-id="9baa0-122">如果您計劃 tooconfigure hello 虛擬與檔案伺服器陣列，8 GB 支援小於 2 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="9baa0-122">If you plan tooconfigure hello virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="9baa0-123">您需要 16 GB RAM toosupport 2-4 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="9baa0-123">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
  * <span data-ttu-id="9baa0-124">一個網路介面。</span><span class="sxs-lookup"><span data-stu-id="9baa0-124">One network interface.</span></span>
  * <span data-ttu-id="9baa0-125">供系統資料使用的 500 GB 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="9baa0-125">A 500 GB virtual disk for system data.</span></span>

### <a name="for-hello-network-in-datacenter"></a><span data-ttu-id="9baa0-126">資料中心中的 hello 網路</span><span class="sxs-lookup"><span data-stu-id="9baa0-126">For hello network in datacenter</span></span>
<span data-ttu-id="9baa0-127">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="9baa0-127">Before you begin, make sure that:</span></span>

* <span data-ttu-id="9baa0-128">您已檢閱網路需求 toodeploy hello StorSimple 虛擬裝置並設定的 hello hello 需求依據的資料中心網路。</span><span class="sxs-lookup"><span data-stu-id="9baa0-128">You have reviewed hello networking requirements toodeploy a StorSimple virtual device and configured hello datacenter network as per hello requirements.</span></span> 

## <a name="step-by-step-provisioning"></a><span data-ttu-id="9baa0-129">佈建的逐步指示</span><span class="sxs-lookup"><span data-stu-id="9baa0-129">Step-by-step provisioning</span></span>
<span data-ttu-id="9baa0-130">tooprovision 和 tooa 虛擬裝置連線，您需要下列步驟 tooperform hello:</span><span class="sxs-lookup"><span data-stu-id="9baa0-130">tooprovision and connect tooa virtual device, you need tooperform hello following steps:</span></span>

1. <span data-ttu-id="9baa0-131">請確認 hello 主機系統有足夠的資源 toomeet hello 最低虛擬裝置需求。</span><span class="sxs-lookup"><span data-stu-id="9baa0-131">Ensure that hello host system has sufficient resources toomeet hello minimum virtual device requirements.</span></span>
2. <span data-ttu-id="9baa0-132">在 Hypervisor 中佈建虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="9baa0-132">Provision a virtual device in your hypervisor.</span></span>
3. <span data-ttu-id="9baa0-133">啟動 hello 虛擬裝置及取得 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9baa0-133">Start hello virtual device and get hello IP address.</span></span>

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a><span data-ttu-id="9baa0-134">步驟 1：確認主機系統符合最低的虛擬裝置需求</span><span class="sxs-lookup"><span data-stu-id="9baa0-134">Step 1: Ensure host system meets minimum virtual device requirements</span></span>
<span data-ttu-id="9baa0-135">toocreate 虛擬裝置，您將需要：</span><span class="sxs-lookup"><span data-stu-id="9baa0-135">toocreate a virtual device, you will need:</span></span>

* <span data-ttu-id="9baa0-136">存取 tooa 主機系統執行 VMware ESXi Server 5.5 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="9baa0-136">Access tooa host system running VMware ESXi Server 5.5 and above.</span></span>
* <span data-ttu-id="9baa0-137">系統 toomanage hello ESXi 主機上的 VMware vSphere client。</span><span class="sxs-lookup"><span data-stu-id="9baa0-137">VMware vSphere client on your system toomanage hello ESXi host.</span></span>

  * <span data-ttu-id="9baa0-138">至少 4 顆核心。</span><span class="sxs-lookup"><span data-stu-id="9baa0-138">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="9baa0-139">至少 8 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="9baa0-139">At least 8 GB of RAM.</span></span> <span data-ttu-id="9baa0-140">如果您計劃 tooconfigure hello 虛擬與檔案伺服器陣列，8 GB 支援小於 2 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="9baa0-140">If you plan tooconfigure hello virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="9baa0-141">您需要 16 GB RAM toosupport 2-4 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="9baa0-141">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
  * <span data-ttu-id="9baa0-142">一個網路介面連接能夠路由流量 tooInternet toohello 網路。</span><span class="sxs-lookup"><span data-stu-id="9baa0-142">One network interface connected toohello network capable of routing traffic tooInternet.</span></span> <span data-ttu-id="9baa0-143">hello 最小的網際網路頻寬應為 5 Mbps tooallow hello 裝置的最佳處理。</span><span class="sxs-lookup"><span data-stu-id="9baa0-143">hello minimum Internet bandwidth should be 5 Mbps tooallow for optimal working of hello device.</span></span>
  * <span data-ttu-id="9baa0-144">供資料使用的 500 GB 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="9baa0-144">A 500 GB virtual disk for data.</span></span>

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a><span data-ttu-id="9baa0-145">步驟 2：在 Hypervisor 中佈建虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="9baa0-145">Step 2: Provision a virtual device in hypervisor</span></span>
<span data-ttu-id="9baa0-146">執行下列步驟 tooprovision 中您的 hypervisor 的虛擬裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="9baa0-146">Perform hello following steps tooprovision a virtual device in your hypervisor.</span></span>

1. <span data-ttu-id="9baa0-147">複製您的系統上的 hello 虛擬裝置映像。</span><span class="sxs-lookup"><span data-stu-id="9baa0-147">Copy hello virtual device image on your system.</span></span> <span data-ttu-id="9baa0-148">您下載 hello Azure 入口網站透過這個虛擬映像。</span><span class="sxs-lookup"><span data-stu-id="9baa0-148">You downloaded this virtual image through hello Azure portal.</span></span>

   1. <span data-ttu-id="9baa0-149">請確定您已下載 hello 最新的映像檔。</span><span class="sxs-lookup"><span data-stu-id="9baa0-149">Ensure that you have downloaded hello latest image file.</span></span> <span data-ttu-id="9baa0-150">如果您先前下載 hello 映像，請再次下載 tooensure 您擁有 hello 最新的映像。</span><span class="sxs-lookup"><span data-stu-id="9baa0-150">If you downloaded hello image earlier, download it again tooensure you have hello latest image.</span></span> <span data-ttu-id="9baa0-151">hello 最新的映像有兩個檔案 （而非一個）。</span><span class="sxs-lookup"><span data-stu-id="9baa0-151">hello latest image has two files (instead of one).</span></span>
   2. <span data-ttu-id="9baa0-152">記下您稍後在 hello 程序中使用此映像時，會複製 hello 映像的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="9baa0-152">Make a note of hello location where you copied hello image as you are using this image later in hello procedure.</span></span>

2. <span data-ttu-id="9baa0-153">登入 toohello ESXi 伺服器使用 hello vSphere 用戶端。</span><span class="sxs-lookup"><span data-stu-id="9baa0-153">Log in toohello ESXi server using hello vSphere client.</span></span> <span data-ttu-id="9baa0-154">您需要 toohave 系統管理員權限 toocreate 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9baa0-154">You need toohave administrator privileges toocreate a virtual machine.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. <span data-ttu-id="9baa0-155">在 hello vSphere 中用戶端 hello 清查區段 hello 左窗格中，選取 hello ESXi 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9baa0-155">In hello vSphere client, in hello inventory section in hello left pane, select hello ESXi Server.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. <span data-ttu-id="9baa0-156">上傳 hello VMDK toohello ESXi 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9baa0-156">Upload hello VMDK toohello ESXi server.</span></span> <span data-ttu-id="9baa0-157">瀏覽 toohello**組態**hello 右窗格中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9baa0-157">Navigate toohello **Configuration** tab in hello right pane.</span></span> <span data-ttu-id="9baa0-158">選取 [硬體] 下方的 [儲存體]。</span><span class="sxs-lookup"><span data-stu-id="9baa0-158">Under **Hardware**, select **Storage**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. <span data-ttu-id="9baa0-159">在 hello 右窗格中，在**Datastores**，選取 hello tooupload hello VMDK 所在的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9baa0-159">In hello right pane, under **Datastores**, select hello datastore where you want tooupload hello VMDK.</span></span> <span data-ttu-id="9baa0-160">hello 資料存放區必須有足夠的可用空間的 hello OS 和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="9baa0-160">hello datastore must have enough free space for hello OS and data disks.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. <span data-ttu-id="9baa0-161">按一下滑鼠右鍵並選取 [瀏覽資料存放區]。</span><span class="sxs-lookup"><span data-stu-id="9baa0-161">Right-click and select **Browse Datastore**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. <span data-ttu-id="9baa0-162">畫面會出現 [資料存放區瀏覽器]  視窗。</span><span class="sxs-lookup"><span data-stu-id="9baa0-162">A **Datastore Browser** window appears.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. <span data-ttu-id="9baa0-163">在 [hello] 工具列上，按一下 [![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png)圖示 toocreate 新的資料夾。</span><span class="sxs-lookup"><span data-stu-id="9baa0-163">In hello tool bar, click ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) icon toocreate a new folder.</span></span> <span data-ttu-id="9baa0-164">指定 hello 資料夾名稱，然後記下它。</span><span class="sxs-lookup"><span data-stu-id="9baa0-164">Specify hello folder name and make a note of it.</span></span> <span data-ttu-id="9baa0-165">您稍後在建立虛擬機器時，將會使用該資料夾名稱 (建議的最佳做法)。</span><span class="sxs-lookup"><span data-stu-id="9baa0-165">You will use this folder name later when creating a virtual machine (recommended best practice).</span></span> <span data-ttu-id="9baa0-166">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-166">Click **OK**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. <span data-ttu-id="9baa0-167">hello 新資料夾會出現在 [hello] 的左窗格 hello**資料存放區的瀏覽器**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-167">hello new folder appears in hello left pane of hello **Datastore Browser**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. <span data-ttu-id="9baa0-168">按一下 hello 上載圖示![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png)選取**上傳檔案**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-168">Click hello Upload icon ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) and select **Upload File**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. <span data-ttu-id="9baa0-169">您所下載的瀏覽和點 toohello VMDK 檔案。</span><span class="sxs-lookup"><span data-stu-id="9baa0-169">Browse and point toohello VMDK files that you downloaded.</span></span> <span data-ttu-id="9baa0-170">有兩個檔案。</span><span class="sxs-lookup"><span data-stu-id="9baa0-170">There are two files.</span></span> <span data-ttu-id="9baa0-171">選取檔案 tooupload。</span><span class="sxs-lookup"><span data-stu-id="9baa0-171">Select a file tooupload.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. <span data-ttu-id="9baa0-172">按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-172">Click **Open**.</span></span> <span data-ttu-id="9baa0-173">hello VMDK 檔案 toohello hello 上的傳指定的資料存放區開始。</span><span class="sxs-lookup"><span data-stu-id="9baa0-173">hello upload of hello VMDK file toohello specified datastore starts.</span></span> <span data-ttu-id="9baa0-174">可能需要幾分鐘的時間 hello 檔案 tooupload。</span><span class="sxs-lookup"><span data-stu-id="9baa0-174">It may take several minutes for hello file tooupload.</span></span>
13. <span data-ttu-id="9baa0-175">Hello 上傳完成之後，您會看到您所建立的 hello 資料夾中的 hello 資料存放區中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9baa0-175">After hello upload is complete, you see hello file in hello datastore in hello folder you created.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    <span data-ttu-id="9baa0-176">現在上傳 hello 第二個 VMDK 檔案 toohello 相同的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9baa0-176">Now upload hello second VMDK file toohello same datastore.</span></span>
14. <span data-ttu-id="9baa0-177">傳回 toohello vSphere 用戶端視窗。</span><span class="sxs-lookup"><span data-stu-id="9baa0-177">Return toohello vSphere client window.</span></span> <span data-ttu-id="9baa0-178">在選取 ESXi 伺服器之後按一下滑鼠右鍵，然後選取 [新增虛擬機器] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-178">With ESXi server selected, right-click and select **New Virtual Machine**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. <span data-ttu-id="9baa0-179">畫面會出限 [建立新虛擬機器]  視窗。</span><span class="sxs-lookup"><span data-stu-id="9baa0-179">A **Create New Virtual Machine** window will appear.</span></span> <span data-ttu-id="9baa0-180">在 hello**組態**頁面上，選取 hello**自訂**選項。</span><span class="sxs-lookup"><span data-stu-id="9baa0-180">On hello **Configuration** page, select hello **Custom** option.</span></span> <span data-ttu-id="9baa0-181">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-181">Click **Next**.</span></span>
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. <span data-ttu-id="9baa0-182">在 hello**名稱和位置**頁面上，指定 hello 您的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="9baa0-182">On hello **Name and Location** page, specify hello name of your virtual machine.</span></span> <span data-ttu-id="9baa0-183">這個名稱應該符合您稍早在步驟 8 中指定 hello 資料夾名稱 （建議的最佳作法）。</span><span class="sxs-lookup"><span data-stu-id="9baa0-183">This name should match hello folder name (recommended best practice) you specified earlier in Step 8.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. <span data-ttu-id="9baa0-184">在 hello**儲存體**頁面上，選取您想要 toouse tooprovision VM 的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="9baa0-184">On hello **Storage** page, select a datastore you want toouse tooprovision your VM.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. <span data-ttu-id="9baa0-185">在 hello**虛擬機器版本**頁面上，選取**虛擬機器版本： 8**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-185">On hello **Virtual Machine Version** page, select **Virtual Machine Version: 8**.</span></span> <span data-ttu-id="9baa0-186">所有支援的版本 8 too11。</span><span class="sxs-lookup"><span data-stu-id="9baa0-186">Versions 8 too11 are all supported.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. <span data-ttu-id="9baa0-187">在 hello**客體作業系統**頁面上，選取 hello**客體作業系統**為**Windows**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-187">On hello **Guest Operating System** page, select hello **Guest Operating System** as **Windows**.</span></span> <span data-ttu-id="9baa0-188">如**版本**，從 hello 下拉式清單中，選取**Microsoft Windows Server 2012 （64 位元）**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-188">For **Version**, from hello dropdown list, select **Microsoft Windows Server 2012 (64-bit)**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. <span data-ttu-id="9baa0-189">在 hello **Cpu**頁面上，調整 hello**虛擬通訊端數目**和**的每個虛擬通訊端的核心數目**讓的 hello**核心總數**是 4 個 （或以上）。</span><span class="sxs-lookup"><span data-stu-id="9baa0-189">On hello **CPUs** page, adjust hello **Number of virtual sockets** and **Number of cores per virtual socket** so that hello **Total number of cores** is 4 (or more).</span></span> <span data-ttu-id="9baa0-190">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-190">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. <span data-ttu-id="9baa0-191">在 hello**記憶體**頁面上，指定 8 GB （或以上） 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="9baa0-191">On hello **Memory** page, specify 8 GB (or more) of RAM.</span></span> <span data-ttu-id="9baa0-192">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. <span data-ttu-id="9baa0-193">在 hello**網路**頁面上，指定 hello hello 網路介面的數目。</span><span class="sxs-lookup"><span data-stu-id="9baa0-193">On hello **Network** page, specify hello number of hello network interfaces.</span></span> <span data-ttu-id="9baa0-194">hello 最低需求是一個網路介面。</span><span class="sxs-lookup"><span data-stu-id="9baa0-194">hello minimum requirement is one network interface.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. <span data-ttu-id="9baa0-195">在 hello **SCSI 控制器**頁面上，接受預設 hello **LSI 邏輯 SAS 控制器**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-195">On hello **SCSI Controller** page, accept hello default **LSI Logic SAS controller**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. <span data-ttu-id="9baa0-196">在 hello**選取磁碟**頁面上，選擇**使用現有的虛擬磁碟**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-196">On hello **Select a Disk** page, choose **Use an existing virtual disk**.</span></span> <span data-ttu-id="9baa0-197">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. <span data-ttu-id="9baa0-198">在 hello**選取現有的磁碟**頁面的 **磁碟檔案路徑**，按一下 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-198">On hello **Select Existing Disk** page, under **Disk File Path**, click **Browse**.</span></span> <span data-ttu-id="9baa0-199">這會開啟 [瀏覽資料存放區]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9baa0-199">This opens a **Browse Datastores** dialog.</span></span> <span data-ttu-id="9baa0-200">瀏覽您上傳 hello VMDK toohello 位置。</span><span class="sxs-lookup"><span data-stu-id="9baa0-200">Navigate toohello location where you uploaded hello VMDK.</span></span> <span data-ttu-id="9baa0-201">為合併的 hello 一開始上傳的兩個檔案，現在可以看到 hello 資料存放區中的只能有一個檔案。</span><span class="sxs-lookup"><span data-stu-id="9baa0-201">You now see only one file in hello datastore as hello two files that you initially uploaded have been merged.</span></span> <span data-ttu-id="9baa0-202">選取 hello 檔案，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-202">Select hello file and click **OK**.</span></span> <span data-ttu-id="9baa0-203">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-203">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. <span data-ttu-id="9baa0-204">在 hello**進階選項**頁面上，接受預設值 hello，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-204">On hello **Advanced Options** page, accept hello default and click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. <span data-ttu-id="9baa0-205">在 hello**準備 tooComplete**頁面上，檢閱與 hello 新的虛擬機器相關聯的所有 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="9baa0-205">On hello **Ready tooComplete** page, review all hello settings associated with hello new virtual machine.</span></span> <span data-ttu-id="9baa0-206">請檢查**編輯 hello 虛擬機器設定完成前的**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-206">Check **Edit hello virtual machine settings before completion**.</span></span> <span data-ttu-id="9baa0-207">按一下 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="9baa0-207">Click **Continue**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. <span data-ttu-id="9baa0-208">在 hello**虛擬機器屬性** 頁面的 hello**硬體**索引標籤上，找出 hello 裝置硬體。</span><span class="sxs-lookup"><span data-stu-id="9baa0-208">On hello **Virtual Machines Properties** page, in hello **Hardware** tab, locate hello device hardware.</span></span> <span data-ttu-id="9baa0-209">選取 [新增硬碟] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-209">Select **New Hard Disk**.</span></span> <span data-ttu-id="9baa0-210">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9baa0-210">Click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. <span data-ttu-id="9baa0-211">您會看到 [新增硬體] 視窗。</span><span class="sxs-lookup"><span data-stu-id="9baa0-211">You see a **Add Hardware** window.</span></span> <span data-ttu-id="9baa0-212">Hello 上**裝置類型**頁面的 **選擇 hello 類型的裝置想 tooadd**，選取**硬碟**，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-212">On hello **Device Type** page, under **Choose hello type of device you wish tooadd**, select **Hard Disk**, and click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. <span data-ttu-id="9baa0-213">在 hello**選取磁碟**頁面上，選擇**建立新的虛擬磁碟**。</span><span class="sxs-lookup"><span data-stu-id="9baa0-213">On hello **Select a Disk** page, choose **Create a new virtual disk**.</span></span> <span data-ttu-id="9baa0-214">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-214">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. <span data-ttu-id="9baa0-215">在 hello**建立磁碟**頁面上，變更 hello**磁碟大小**too500 GB （或以上）。</span><span class="sxs-lookup"><span data-stu-id="9baa0-215">On hello **Create a Disk** page, change hello **Disk Size** too500 GB (or more).</span></span> <span data-ttu-id="9baa0-216">Hello 最低需求 500 GB 時，一律可以佈建較大的磁碟。</span><span class="sxs-lookup"><span data-stu-id="9baa0-216">While 500 GB is hello minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="9baa0-217">請注意，您無法擴充或縮減 hello 磁碟一次佈建。</span><span class="sxs-lookup"><span data-stu-id="9baa0-217">Note that you cannot expand or shrink hello disk once provisioned.</span></span> <span data-ttu-id="9baa0-218">如需 hello 大小磁碟 tooprovision 的詳細資訊，檢閱 hello hello 調整大小 > 一節[最佳做法文件](storsimple-ova-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="9baa0-218">For more information on hello size of disk tooprovision, review hello sizing section in hello [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="9baa0-219">在 [磁碟佈建] 下方，選取 [精簡佈建]。</span><span class="sxs-lookup"><span data-stu-id="9baa0-219">Under **Disk Provisioning**, select **Thin Provision**.</span></span> <span data-ttu-id="9baa0-220">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-220">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. <span data-ttu-id="9baa0-221">在 hello**進階選項**頁面上，接受預設 hello。</span><span class="sxs-lookup"><span data-stu-id="9baa0-221">On hello **Advanced Options** page, accept hello default.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. <span data-ttu-id="9baa0-222">在 hello**準備 tooComplete**頁面上，檢閱 hello 磁碟的選項。</span><span class="sxs-lookup"><span data-stu-id="9baa0-222">On hello **Ready tooComplete** page, review hello disk options.</span></span> <span data-ttu-id="9baa0-223">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-223">Click **Finish**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. <span data-ttu-id="9baa0-224">傳回 toohello 虛擬機器內容頁面。</span><span class="sxs-lookup"><span data-stu-id="9baa0-224">Return toohello Virtual Machine Properties page.</span></span> <span data-ttu-id="9baa0-225">新的硬碟加入 tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9baa0-225">A new hard disk is added tooyour virtual machine.</span></span> <span data-ttu-id="9baa0-226">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="9baa0-226">Click **Finish**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. <span data-ttu-id="9baa0-227">Hello 右窗格中選取您的虛擬機器，以瀏覽 toohello**摘要** 索引標籤。檢閱您的虛擬機器的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="9baa0-227">With your virtual machine selected in hello right pane, navigate toohello **Summary** tab. Review hello settings for your virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

<span data-ttu-id="9baa0-228">您的虛擬機器已成功佈建。</span><span class="sxs-lookup"><span data-stu-id="9baa0-228">Your virtual machine is now provisioned.</span></span> <span data-ttu-id="9baa0-229">hello 下一個步驟是 toopower 這部電腦上的，取得 hello 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9baa0-229">hello next step is toopower on this machine and get hello IP address.</span></span>

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a><span data-ttu-id="9baa0-230">步驟 3： 啟動 hello 虛擬裝置及取得 hello IP</span><span class="sxs-lookup"><span data-stu-id="9baa0-230">Step 3: Start hello virtual device and get hello IP</span></span>
<span data-ttu-id="9baa0-231">執行下列步驟 toostart hello 虛擬裝置，並連接 tooit。</span><span class="sxs-lookup"><span data-stu-id="9baa0-231">Perform hello following steps toostart your virtual device and connect tooit.</span></span>

#### <a name="toostart-hello-virtual-device"></a><span data-ttu-id="9baa0-232">toostart hello 虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="9baa0-232">toostart hello virtual device</span></span>
1. <span data-ttu-id="9baa0-233">啟動 hello 虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="9baa0-233">Start hello virtual device.</span></span> <span data-ttu-id="9baa0-234">在 hello vSphere Configuration Manager hello 左窗格中，選取您的裝置，toobring hello 內容功能表上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="9baa0-234">In hello vSphere Configuration Manager, in hello left pane, select your device and right-click toobring up hello context menu.</span></span> <span data-ttu-id="9baa0-235">選取 [電源]，然後選取 [開啟電源]。</span><span class="sxs-lookup"><span data-stu-id="9baa0-235">Select **Power** and then select **Power on**.</span></span> <span data-ttu-id="9baa0-236">此時您的虛擬機器應該會開機。</span><span class="sxs-lookup"><span data-stu-id="9baa0-236">This should power on your virtual machine.</span></span> <span data-ttu-id="9baa0-237">您可以在 hello 右下檢視 hello 狀態**最近工作**hello vSphere 用戶端的窗格。</span><span class="sxs-lookup"><span data-stu-id="9baa0-237">You can view hello status in hello bottom **Recent Tasks** pane of hello vSphere client.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. <span data-ttu-id="9baa0-238">hello 安裝工作需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="9baa0-238">hello setup tasks will take a few minutes toocomplete.</span></span> <span data-ttu-id="9baa0-239">Hello 裝置開始執行之後，瀏覽 toohello**主控台** 索引標籤。傳送 Ctrl + Alt + Delete toolog toohello 裝置中。</span><span class="sxs-lookup"><span data-stu-id="9baa0-239">Once hello device is running, navigate toohello **Console** tab. Send Ctrl+Alt+Delete toolog in toohello device.</span></span> <span data-ttu-id="9baa0-240">或者，您可以指向 hello hello 主控台視窗上的資料指標，然後按下 Ctrl + Alt + Insert。</span><span class="sxs-lookup"><span data-stu-id="9baa0-240">Alternatively, you can point hello cursor on hello console window and press Ctrl+Alt+Insert.</span></span> <span data-ttu-id="9baa0-241">hello 預設使用者為*StorSimpleAdmin* hello 預設密碼為*Password1*。</span><span class="sxs-lookup"><span data-stu-id="9baa0-241">hello default user is *StorSimpleAdmin* and hello default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. <span data-ttu-id="9baa0-242">基於安全性理由，hello 裝置系統管理員密碼到期 hello 第一次登入時。</span><span class="sxs-lookup"><span data-stu-id="9baa0-242">For security reasons, hello device administrator password expires at hello first logon.</span></span> <span data-ttu-id="9baa0-243">您已提示的 toochange hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="9baa0-243">You are prompted toochange hello password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. <span data-ttu-id="9baa0-244">請輸入至少包含 8 個字元的密碼。</span><span class="sxs-lookup"><span data-stu-id="9baa0-244">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="9baa0-245">hello 密碼必須包含 3 超出 4 個需求： 大寫字母、 小寫、 數字及特殊字元。</span><span class="sxs-lookup"><span data-stu-id="9baa0-245">hello password must contain 3 out of 4 of these requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="9baa0-246">重新輸入 hello 密碼 tooconfirm 它。</span><span class="sxs-lookup"><span data-stu-id="9baa0-246">Reenter hello password tooconfirm it.</span></span> <span data-ttu-id="9baa0-247">系統會通知您該 hello 密碼已變更。</span><span class="sxs-lookup"><span data-stu-id="9baa0-247">You will be notified that hello password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. <span data-ttu-id="9baa0-248">已成功變更 hello 密碼之後，可能要重新啟動 hello 虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="9baa0-248">After hello password is successfully changed, hello virtual device may reboot.</span></span> <span data-ttu-id="9baa0-249">等候 hello 重新開機 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="9baa0-249">Wait for hello reboot toocomplete.</span></span> <span data-ttu-id="9baa0-250">hello Windows PowerShell 主控台中的 hello 裝置可能會顯示進度列以及。</span><span class="sxs-lookup"><span data-stu-id="9baa0-250">hello Windows PowerShell console of hello device may be displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. <span data-ttu-id="9baa0-251">步驟 6 至 8 僅適用於在非 DHCP 環境中開機的情況。</span><span class="sxs-lookup"><span data-stu-id="9baa0-251">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="9baa0-252">如果您是在 DHCP 環境，然後略過這些步驟，並移 toostep 9。</span><span class="sxs-lookup"><span data-stu-id="9baa0-252">If you are in a DHCP environment, then skip these steps and go toostep 9.</span></span> <span data-ttu-id="9baa0-253">如果您已啟動您的裝置，在非 DHCP 環境中，您會看到下列畫面 hello。</span><span class="sxs-lookup"><span data-stu-id="9baa0-253">If you booted up your device in non-DHCP environment, you will see hello following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   <span data-ttu-id="9baa0-254">接著，設定 hello 網路。</span><span class="sxs-lookup"><span data-stu-id="9baa0-254">Next, configure hello network.</span></span>
7. <span data-ttu-id="9baa0-255">使用 hello`Get-HcsIpAddress`命令 toolist hello 網路介面啟用虛擬裝置上。</span><span class="sxs-lookup"><span data-stu-id="9baa0-255">Use hello `Get-HcsIpAddress` command toolist hello network interfaces enabled on your virtual device.</span></span> <span data-ttu-id="9baa0-256">如果您的裝置具有單一網路介面啟用，hello 預設指派名稱 toothis 介面是`Ethernet`。</span><span class="sxs-lookup"><span data-stu-id="9baa0-256">If your device has a single network interface enabled, hello default name assigned toothis interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. <span data-ttu-id="9baa0-257">使用 hello `Set-HcsIpAddress` cmdlet tooconfigure hello 網路。</span><span class="sxs-lookup"><span data-stu-id="9baa0-257">Use hello `Set-HcsIpAddress` cmdlet tooconfigure hello network.</span></span> <span data-ttu-id="9baa0-258">範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="9baa0-258">An example is shown below:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. <span data-ttu-id="9baa0-259">Hello 初始設定完成後，已開機 hello 裝置之後，您會看到 hello 裝置橫幅文字。</span><span class="sxs-lookup"><span data-stu-id="9baa0-259">After hello initial setup is complete and hello device has booted up, you will see hello device banner text.</span></span> <span data-ttu-id="9baa0-260">請記下 hello IP 位址，然後顯示 hello 橫幅文字 toomanage hello 裝置中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="9baa0-260">Make a note of hello IP address and hello URL displayed in hello banner text toomanage hello device.</span></span> <span data-ttu-id="9baa0-261">您將使用此 IP 位址 tooconnect toohello web UI 您虛擬裝置並完成 hello 本機安裝及註冊。</span><span class="sxs-lookup"><span data-stu-id="9baa0-261">You will use this IP address tooconnect toohello web UI of your virtual device and complete hello local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. <span data-ttu-id="9baa0-262">（選擇性）只有當您要部署您的裝置 hello 政府雲端中執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="9baa0-262">(Optional) Perform this step only if you are deploying your device in hello Government Cloud.</span></span> <span data-ttu-id="9baa0-263">您現在將在您的裝置上啟用 hello 美國聯邦資訊處理標準 (FIPS) 模式。</span><span class="sxs-lookup"><span data-stu-id="9baa0-263">You will now enable hello United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="9baa0-264">hello FIPS 140 標準會定義核准 hello 保護機密資料的美國聯邦政府電腦系統所使用的密碼編譯演算法。</span><span class="sxs-lookup"><span data-stu-id="9baa0-264">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span>

    1. <span data-ttu-id="9baa0-265">tooenable hello FIPS 模式中，執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="9baa0-265">tooenable hello FIPS mode, run hello following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="9baa0-266">重新啟動您的裝置之後您已經啟用 hello FIPS 模式，以便 hello 密碼編譯的驗證才會生效。</span><span class="sxs-lookup"><span data-stu-id="9baa0-266">Reboot your device after you have enabled hello FIPS mode so that hello cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="9baa0-267">您可以在您的裝置上啟用或停用 FIPS 模式。</span><span class="sxs-lookup"><span data-stu-id="9baa0-267">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="9baa0-268">不支援 FIPS 和非 FIPS 模式之間交替 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="9baa0-268">Alternating hello device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="9baa0-269">如果您的裝置不符合 hello 最低設定需求，您會看到 hello 橫幅文字 （如下所示） 中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="9baa0-269">If your device does not meet hello minimum configuration requirements, you will see an error in hello banner text (shown below).</span></span> <span data-ttu-id="9baa0-270">您必須 toomodify hello 裝置設定，使其具有足夠的資源 toomeet hello 最低需求。</span><span class="sxs-lookup"><span data-stu-id="9baa0-270">You will need toomodify hello device configuration so that it has adequate resources toomeet hello minimum requirements.</span></span> <span data-ttu-id="9baa0-271">然後，您可以重新啟動，並連接 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="9baa0-271">You can then restart and connect toohello device.</span></span> <span data-ttu-id="9baa0-272">在 toohello 最低設定需求，請參閱[步驟 1： 確定 hello 主機系統符合最低虛擬裝置需求](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements)。</span><span class="sxs-lookup"><span data-stu-id="9baa0-272">Refer toohello minimum configuration requirements in [Step 1: Ensure that hello host system meets minimum virtual device requirements](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

<span data-ttu-id="9baa0-273">如果您使用 hello 本機 web UI 的 hello 初始設定期間所面對任何其他錯誤，請參閱 toohello 下列工作流程：</span><span class="sxs-lookup"><span data-stu-id="9baa0-273">If you face any other error during hello initial configuration using hello local web UI, refer toohello following workflows:</span></span>

* <span data-ttu-id="9baa0-274">也會執行診斷測試[疑難排解 web UI 安裝](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors)。</span><span class="sxs-lookup"><span data-stu-id="9baa0-274">Run diagnostic tests too[troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="9baa0-275">[產生記錄檔封裝及檢視記錄檔](storsimple-ova-web-ui-admin.md#generate-a-log-package)。</span><span class="sxs-lookup"><span data-stu-id="9baa0-275">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9baa0-276">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9baa0-276">Next steps</span></span>
* [<span data-ttu-id="9baa0-277">Set up your StorSimple Virtual Array as a file server (將 StorSimple 虛擬陣列設定為檔案伺服器)</span><span class="sxs-lookup"><span data-stu-id="9baa0-277">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="9baa0-278">Set up your StorSimple Virtual Array as an iSCSI server (將 StorSimple 虛擬陣列設定為 iSCSI 伺服器)</span><span class="sxs-lookup"><span data-stu-id="9baa0-278">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)
