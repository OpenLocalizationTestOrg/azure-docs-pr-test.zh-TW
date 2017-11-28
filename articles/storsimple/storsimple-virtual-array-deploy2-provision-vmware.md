---
title: "在 VMware 中佈建 StorSimple Virtual Array | Microsoft Docs"
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
ms.openlocfilehash: 118521a127b2e4b765efabdbdde71605440d81c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a><span data-ttu-id="a0f6f-103">部署 StorSimple Virtual Array：在 VMware 中佈建</span><span class="sxs-lookup"><span data-stu-id="a0f6f-103">Deploy StorSimple Virtual Array - Provision in VMware</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a><span data-ttu-id="a0f6f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a0f6f-104">Overview</span></span>
<span data-ttu-id="a0f6f-105">本教學課程說明如何在執行 VMware ESXi 5.5 及更新版本 的主機系統上佈建及連線到 StorSimple 虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-105">This tutorial describes how to provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span> <span data-ttu-id="a0f6f-106">本文適用於在 Azure 入口網站及 Microsoft Azure 政府服務雲端部署 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-106">This article applies to the deployment of StorSimple Virtual Arrays in Azure portal and the Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="a0f6f-107">您需要有系統管理員權限，才能佈建並連接至虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-107">You need administrator privileges to provision and connect to a virtual device.</span></span> <span data-ttu-id="a0f6f-108">佈建及初始安裝程序可能需要大約 10 分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-108">The provisioning and initial setup can take around 10 minutes to complete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="a0f6f-109">佈建的必要條件</span><span class="sxs-lookup"><span data-stu-id="a0f6f-109">Provisioning prerequisites</span></span>
<span data-ttu-id="a0f6f-110">在執行 VMware ESXi 5.5 及更新版本的主機系統上佈建虛擬裝置的必要條件如下。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-110">The prerequisites to provision a virtual device on a host system running VMware ESXi 5.5 and above, are as follows.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="a0f6f-111">StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="a0f6f-111">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="a0f6f-112">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="a0f6f-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="a0f6f-113">您已完成 [準備入口網站以使用 StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md)中的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-113">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="a0f6f-114">您已經從 Azure 入口網站下載適用於 VMware 的虛擬裝置映像。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-114">You have downloaded the virtual device image for VMware from the Azure portal.</span></span> <span data-ttu-id="a0f6f-115">如需詳細資訊，請參閱[準備入口網站以使用 StorSimple Virtual Array 指南](storsimple-virtual-array-deploy1-portal-prep.md)的**步驟 3︰下載虛擬裝置映像**。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-115">For more information, see **Step 3: Download the virtual device image** of [Prepare the portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

### <a name="for-the-storsimple-virtual-device"></a><span data-ttu-id="a0f6f-116">對於 StorSimple 虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="a0f6f-116">For the StorSimple virtual device</span></span>
<span data-ttu-id="a0f6f-117">在您部署虛擬裝置之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="a0f6f-117">Before you deploy a virtual device, make sure that:</span></span>

* <span data-ttu-id="a0f6f-118">您可以存取執行 Hyper-V (2008 R2 或更新版本)，且可用來佈建裝置的主機系統。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-118">You have access to a host system running Hyper-V (2008 R2 or later) that can be used to a provision a device.</span></span>
* <span data-ttu-id="a0f6f-119">主機系統能夠把下列資源專門用來佈建虛擬裝置：</span><span class="sxs-lookup"><span data-stu-id="a0f6f-119">The host system is able to dedicate the following resources to provision your virtual device:</span></span>

  * <span data-ttu-id="a0f6f-120">至少 4 顆核心。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-120">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="a0f6f-121">至少 8 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-121">At least 8 GB of RAM.</span></span> <span data-ttu-id="a0f6f-122">若計畫將虛擬陣列設定為檔案伺服器，8 GB 支援 2 百萬個以下的檔案。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-122">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="a0f6f-123">您需要 16 GB RAM 才能支援 2 - 4 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-123">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="a0f6f-124">一個網路介面。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-124">One network interface.</span></span>
  * <span data-ttu-id="a0f6f-125">供系統資料使用的 500 GB 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-125">A 500 GB virtual disk for system data.</span></span>

### <a name="for-the-network-in-datacenter"></a><span data-ttu-id="a0f6f-126">對於資料中心的網路</span><span class="sxs-lookup"><span data-stu-id="a0f6f-126">For the network in datacenter</span></span>
<span data-ttu-id="a0f6f-127">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="a0f6f-127">Before you begin, make sure that:</span></span>

* <span data-ttu-id="a0f6f-128">您已經檢閱部署 StorSimple 虛擬裝置的網路需求，且已經根據需求設定資料中心的網路。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-128">You have reviewed the networking requirements to deploy a StorSimple virtual device and configured the datacenter network as per the requirements.</span></span> 

## <a name="step-by-step-provisioning"></a><span data-ttu-id="a0f6f-129">佈建的逐步指示</span><span class="sxs-lookup"><span data-stu-id="a0f6f-129">Step-by-step provisioning</span></span>
<span data-ttu-id="a0f6f-130">若要佈建並連接至虛擬裝置，您必須執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a0f6f-130">To provision and connect to a virtual device, you need to perform the following steps:</span></span>

1. <span data-ttu-id="a0f6f-131">確認主機系統有足夠的資源來符合最低的虛擬裝置需求。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-131">Ensure that the host system has sufficient resources to meet the minimum virtual device requirements.</span></span>
2. <span data-ttu-id="a0f6f-132">在 Hypervisor 中佈建虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-132">Provision a virtual device in your hypervisor.</span></span>
3. <span data-ttu-id="a0f6f-133">啟動虛擬裝置，並取得 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-133">Start the virtual device and get the IP address.</span></span>

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a><span data-ttu-id="a0f6f-134">步驟 1：確認主機系統符合最低的虛擬裝置需求</span><span class="sxs-lookup"><span data-stu-id="a0f6f-134">Step 1: Ensure host system meets minimum virtual device requirements</span></span>
<span data-ttu-id="a0f6f-135">若要建立虛擬裝置，您將需要：</span><span class="sxs-lookup"><span data-stu-id="a0f6f-135">To create a virtual device, you will need:</span></span>

* <span data-ttu-id="a0f6f-136">能夠存取執行 VMware ESXi 伺服器 5.5 及更新版本的主機系統。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-136">Access to a host system running VMware ESXi Server 5.5 and above.</span></span>
* <span data-ttu-id="a0f6f-137">您系統上的 VMware vSphere 用戶端，以便管理 ESXi 主機。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-137">VMware vSphere client on your system to manage the ESXi host.</span></span>

  * <span data-ttu-id="a0f6f-138">至少 4 顆核心。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-138">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="a0f6f-139">至少 8 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-139">At least 8 GB of RAM.</span></span> <span data-ttu-id="a0f6f-140">若計畫將虛擬陣列設定為檔案伺服器，8 GB 支援 2 百萬個以下的檔案。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-140">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="a0f6f-141">您需要 16 GB RAM 才能支援 2 - 4 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-141">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="a0f6f-142">網路介面，且已連線到能夠將流量路由至網際網路的網路。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-142">One network interface connected to the network capable of routing traffic to Internet.</span></span> <span data-ttu-id="a0f6f-143">網際網路頻寬應該至少要有 5 Mbps，以便讓裝置能夠發揮最大功能。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-143">The minimum Internet bandwidth should be 5 Mbps to allow for optimal working of the device.</span></span>
  * <span data-ttu-id="a0f6f-144">供資料使用的 500 GB 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-144">A 500 GB virtual disk for data.</span></span>

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a><span data-ttu-id="a0f6f-145">步驟 2：在 Hypervisor 中佈建虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="a0f6f-145">Step 2: Provision a virtual device in hypervisor</span></span>
<span data-ttu-id="a0f6f-146">請執行下列步驟，以便在您的 Hypervisor 中佈建虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-146">Perform the following steps to provision a virtual device in your hypervisor.</span></span>

1. <span data-ttu-id="a0f6f-147">複製您系統中的虛擬裝置映像。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-147">Copy the virtual device image on your system.</span></span> <span data-ttu-id="a0f6f-148">您已透過 Azure 入口網站下載這個虛擬映像。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-148">You downloaded this virtual image through the Azure portal.</span></span>

   1. <span data-ttu-id="a0f6f-149">請確定您已下載最新的映像檔。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-149">Ensure that you have downloaded the latest image file.</span></span> <span data-ttu-id="a0f6f-150">如果您稍早下載過映像，請再下載一次，確定您擁有最新映像。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-150">If you downloaded the image earlier, download it again to ensure you have the latest image.</span></span> <span data-ttu-id="a0f6f-151">最新映像具有兩個檔案 (而不是一個)。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-151">The latest image has two files (instead of one).</span></span>
   2. <span data-ttu-id="a0f6f-152">請記下您複製映像的位置，因為稍後會在程序中使用此映像。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-152">Make a note of the location where you copied the image as you are using this image later in the procedure.</span></span>

2. <span data-ttu-id="a0f6f-153">使用 vSphere 用戶端登入 ESXi 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-153">Log in to the ESXi server using the vSphere client.</span></span> <span data-ttu-id="a0f6f-154">您需要有系統管理員權限，才能建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-154">You need to have administrator privileges to create a virtual machine.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. <span data-ttu-id="a0f6f-155">在 vSphere 用戶端中，選取左窗格 [詳細目錄] 區段中的 [ESXi 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-155">In the vSphere client, in the inventory section in the left pane, select the ESXi Server.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. <span data-ttu-id="a0f6f-156">將 VMDK 上傳至 ESXi 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-156">Upload the VMDK to the ESXi server.</span></span> <span data-ttu-id="a0f6f-157">瀏覽至右窗格中的 [組態]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-157">Navigate to the **Configuration** tab in the right pane.</span></span> <span data-ttu-id="a0f6f-158">選取 [硬體] 下方的 [儲存體]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-158">Under **Hardware**, select **Storage**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. <span data-ttu-id="a0f6f-159">在右窗格的 [資料存放區] 下方，選取您要上傳 VMDK 的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-159">In the right pane, under **Datastores**, select the datastore where you want to upload the VMDK.</span></span> <span data-ttu-id="a0f6f-160">資料存放區必須要有足夠的可用空間來容納作業系統和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-160">The datastore must have enough free space for the OS and data disks.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. <span data-ttu-id="a0f6f-161">按一下滑鼠右鍵並選取 [瀏覽資料存放區]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-161">Right-click and select **Browse Datastore**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. <span data-ttu-id="a0f6f-162">畫面會出現 [資料存放區瀏覽器]  視窗。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-162">A **Datastore Browser** window appears.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. <span data-ttu-id="a0f6f-163">在工具列上，按一下 ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) 圖示來建立新資料夾。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-163">In the tool bar, click ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) icon to create a new folder.</span></span> <span data-ttu-id="a0f6f-164">然後指定資料夾的名稱，並把該名稱記下來。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-164">Specify the folder name and make a note of it.</span></span> <span data-ttu-id="a0f6f-165">您稍後在建立虛擬機器時，將會使用該資料夾名稱 (建議的最佳做法)。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-165">You will use this folder name later when creating a virtual machine (recommended best practice).</span></span> <span data-ttu-id="a0f6f-166">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-166">Click **OK**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. <span data-ttu-id="a0f6f-167">[資料存放區瀏覽器] 的左窗格中會出現新的資料夾。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-167">The new folder appears in the left pane of the **Datastore Browser**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. <span data-ttu-id="a0f6f-168">按一下 [上傳] 圖示 ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png)，然後選取 [上傳檔案]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-168">Click the Upload icon ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) and select **Upload File**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. <span data-ttu-id="a0f6f-169">瀏覽並指向您已下載的 VMDK 檔案。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-169">Browse and point to the VMDK files that you downloaded.</span></span> <span data-ttu-id="a0f6f-170">有兩個檔案。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-170">There are two files.</span></span> <span data-ttu-id="a0f6f-171">選取要上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-171">Select a file to upload.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. <span data-ttu-id="a0f6f-172">按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-172">Click **Open**.</span></span> <span data-ttu-id="a0f6f-173">就會開始將 VMDK 檔案上傳至指定的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-173">The upload of the VMDK file to the specified datastore starts.</span></span> <span data-ttu-id="a0f6f-174">檔案可能需要幾分鐘的時間才能上傳完畢。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-174">It may take several minutes for the file to upload.</span></span>
13. <span data-ttu-id="a0f6f-175">上傳完成之後，檔案就會出現在資料存放區裡您所建立的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-175">After the upload is complete, you see the file in the datastore in the folder you created.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    <span data-ttu-id="a0f6f-176">現在將第二個 VMDK 檔案上傳至相同的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-176">Now upload the second VMDK file to the same datastore.</span></span>
14. <span data-ttu-id="a0f6f-177">返回 vSphere 用戶端視窗。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-177">Return to the vSphere client window.</span></span> <span data-ttu-id="a0f6f-178">在選取 ESXi 伺服器之後按一下滑鼠右鍵，然後選取 [新增虛擬機器] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-178">With ESXi server selected, right-click and select **New Virtual Machine**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. <span data-ttu-id="a0f6f-179">畫面會出限 [建立新虛擬機器]  視窗。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-179">A **Create New Virtual Machine** window will appear.</span></span> <span data-ttu-id="a0f6f-180">在 [設定] 頁面上，選取 [自訂] 選項。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-180">On the **Configuration** page, select the **Custom** option.</span></span> <span data-ttu-id="a0f6f-181">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-181">Click **Next**.</span></span>
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. <span data-ttu-id="a0f6f-182">在 [名稱和位置] 頁面上，指定虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-182">On the **Name and Location** page, specify the name of your virtual machine.</span></span> <span data-ttu-id="a0f6f-183">這個名稱應該與您之前在步驟 8 中指定的資料夾名稱 (建議的最佳做法) 相同。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-183">This name should match the folder name (recommended best practice) you specified earlier in Step 8.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. <span data-ttu-id="a0f6f-184">在 [儲存體]  頁面上，選取您要用來佈建虛擬機器的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-184">On the **Storage** page, select a datastore you want to use to provision your VM.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. <span data-ttu-id="a0f6f-185">在 [虛擬機器版本] 頁面上，選取 [虛擬機器版本: 8]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-185">On the **Virtual Machine Version** page, select **Virtual Machine Version: 8**.</span></span> <span data-ttu-id="a0f6f-186">支援第 8 版到第 11 版。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-186">Versions 8 to 11 are all supported.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. <span data-ttu-id="a0f6f-187">在 [客體作業系統] 頁面上，將 [客體作業系統] 選取為 [Windows]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-187">On the **Guest Operating System** page, select the **Guest Operating System** as **Windows**.</span></span> <span data-ttu-id="a0f6f-188">而對於 [版本]，請從下拉式清單中選取 [Microsoft Windows Server 2012 (64 位元)]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-188">For **Version**, from the dropdown list, select **Microsoft Windows Server 2012 (64-bit)**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. <span data-ttu-id="a0f6f-189">在 [CPU] 頁面上，調整 [虛擬通訊端的數目] 和 [每個虛擬通訊端的核心數目]，以便讓 [核心總數] 至少為 4。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-189">On the **CPUs** page, adjust the **Number of virtual sockets** and **Number of cores per virtual socket** so that the **Total number of cores** is 4 (or more).</span></span> <span data-ttu-id="a0f6f-190">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-190">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. <span data-ttu-id="a0f6f-191">在 [記憶體]  頁面上，將 RAM 指定為至少為 8 GB。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-191">On the **Memory** page, specify 8 GB (or more) of RAM.</span></span> <span data-ttu-id="a0f6f-192">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. <span data-ttu-id="a0f6f-193">在 [網路]  頁面上，指定網路介面的數目。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-193">On the **Network** page, specify the number of the network interfaces.</span></span> <span data-ttu-id="a0f6f-194">最低需求是一個網路介面。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-194">The minimum requirement is one network interface.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. <span data-ttu-id="a0f6f-195">在 [SCSI 控制器] 頁面上，接受預設的 [LSI Logic SAS 控制器]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-195">On the **SCSI Controller** page, accept the default **LSI Logic SAS controller**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. <span data-ttu-id="a0f6f-196">在 [選取磁碟] 頁面上，選擇 [使用現有的虛擬硬碟]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-196">On the **Select a Disk** page, choose **Use an existing virtual disk**.</span></span> <span data-ttu-id="a0f6f-197">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. <span data-ttu-id="a0f6f-198">在 [選取現有的磁碟] 頁面的 [磁碟檔案路徑] 下方，按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-198">On the **Select Existing Disk** page, under **Disk File Path**, click **Browse**.</span></span> <span data-ttu-id="a0f6f-199">這會開啟 [瀏覽資料存放區]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-199">This opens a **Browse Datastores** dialog.</span></span> <span data-ttu-id="a0f6f-200">瀏覽至您之前上傳 VMDK 的位置。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-200">Navigate to the location where you uploaded the VMDK.</span></span> <span data-ttu-id="a0f6f-201">因為您最初上傳回的兩個檔案已合併，所以您現在於資料存放區中只會看到一個檔案。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-201">You now see only one file in the datastore as the two files that you initially uploaded have been merged.</span></span> <span data-ttu-id="a0f6f-202">選取檔案，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-202">Select the file and click **OK**.</span></span> <span data-ttu-id="a0f6f-203">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-203">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. <span data-ttu-id="a0f6f-204">在 [進階選項] 頁面上，接受預設值並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-204">On the **Advanced Options** page, accept the default and click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. <span data-ttu-id="a0f6f-205">在 [準備完成]  頁面上，檢閱與新的虛擬機器相關的所有設定。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-205">On the **Ready to Complete** page, review all the settings associated with the new virtual machine.</span></span> <span data-ttu-id="a0f6f-206">選取 [在完成之前編輯虛擬機器的設定]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-206">Check **Edit the virtual machine settings before completion**.</span></span> <span data-ttu-id="a0f6f-207">按一下 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-207">Click **Continue**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. <span data-ttu-id="a0f6f-208">在 [虛擬機器屬性] 頁面的 [硬體] 索引標籤上尋找裝置的硬體。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-208">On the **Virtual Machines Properties** page, in the **Hardware** tab, locate the device hardware.</span></span> <span data-ttu-id="a0f6f-209">選取 [新增硬碟] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-209">Select **New Hard Disk**.</span></span> <span data-ttu-id="a0f6f-210">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-210">Click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. <span data-ttu-id="a0f6f-211">您會看到 [新增硬體] 視窗。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-211">You see a **Add Hardware** window.</span></span> <span data-ttu-id="a0f6f-212">在 [裝置類型] 頁面的 [選擇您想要新增的裝置類型] 下方，選取 [硬碟] 並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-212">On the **Device Type** page, under **Choose the type of device you wish to add**, select **Hard Disk**, and click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. <span data-ttu-id="a0f6f-213">在 [選取磁碟] 頁面上，選擇 [建立新的虛擬磁碟]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-213">On the **Select a Disk** page, choose **Create a new virtual disk**.</span></span> <span data-ttu-id="a0f6f-214">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-214">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. <span data-ttu-id="a0f6f-215">在 [建立磁碟] 頁面上，將 [磁碟大小] 變更為至少 500 GB。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-215">On the **Create a Disk** page, change the **Disk Size** to 500 GB (or more).</span></span> <span data-ttu-id="a0f6f-216">500 GB 是最低需求，您永遠可以佈建更大的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-216">While 500 GB is the minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="a0f6f-217">請注意，佈建之後您無法擴充或縮小磁碟。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-217">Note that you cannot expand or shrink the disk once provisioned.</span></span> <span data-ttu-id="a0f6f-218">如需有關要佈建之磁碟大小的詳細資訊，請檢閱[最佳作法文件](storsimple-ova-best-practices.md)中的＜調整大小＞一節。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-218">For more information on the size of disk to provision, review the sizing section in the [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="a0f6f-219">在 [磁碟佈建] 下方，選取 [精簡佈建]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-219">Under **Disk Provisioning**, select **Thin Provision**.</span></span> <span data-ttu-id="a0f6f-220">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-220">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. <span data-ttu-id="a0f6f-221">在 [進階選項]  頁面上，接受預設值。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-221">On the **Advanced Options** page, accept the default.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. <span data-ttu-id="a0f6f-222">在 [準備完成]  頁面上，檢閱磁碟的各個選項。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-222">On the **Ready to Complete** page, review the disk options.</span></span> <span data-ttu-id="a0f6f-223">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-223">Click **Finish**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. <span data-ttu-id="a0f6f-224">返回 [虛擬機器屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-224">Return to the Virtual Machine Properties page.</span></span> <span data-ttu-id="a0f6f-225">您的虛擬機器已新增一個硬碟。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-225">A new hard disk is added to your virtual machine.</span></span> <span data-ttu-id="a0f6f-226">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-226">Click **Finish**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. <span data-ttu-id="a0f6f-227">在右窗格中選取您的虛擬機器，然後瀏覽至 [摘要]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-227">With your virtual machine selected in the right pane, navigate to the **Summary** tab.</span></span> <span data-ttu-id="a0f6f-228">請檢閱您虛擬機器的設定。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-228">Review the settings for your virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

<span data-ttu-id="a0f6f-229">您的虛擬機器已成功佈建。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-229">Your virtual machine is now provisioned.</span></span> <span data-ttu-id="a0f6f-230">下一個步驟是啟動該虛擬機器，然後取得 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-230">The next step is to power on this machine and get the IP address.</span></span>

## <a name="step-3-start-the-virtual-device-and-get-the-ip"></a><span data-ttu-id="a0f6f-231">步驟 3：啟動虛擬裝置，並取得 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a0f6f-231">Step 3: Start the virtual device and get the IP</span></span>
<span data-ttu-id="a0f6f-232">請執行下列步驟來啟動您的虛擬裝置，並連線到該虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-232">Perform the following steps to start your virtual device and connect to it.</span></span>

#### <a name="to-start-the-virtual-device"></a><span data-ttu-id="a0f6f-233">啟動虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="a0f6f-233">To start the virtual device</span></span>
1. <span data-ttu-id="a0f6f-234">啟動虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-234">Start the virtual device.</span></span> <span data-ttu-id="a0f6f-235">在 vSphere 設定管理員中，選取左窗格中您的裝置，然後按一下滑鼠右鍵來開啟操作功能表。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-235">In the vSphere Configuration Manager, in the left pane, select your device and right-click to bring up the context menu.</span></span> <span data-ttu-id="a0f6f-236">選取 [電源]，然後選取 [開啟電源]。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-236">Select **Power** and then select **Power on**.</span></span> <span data-ttu-id="a0f6f-237">此時您的虛擬機器應該會開機。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-237">This should power on your virtual machine.</span></span> <span data-ttu-id="a0f6f-238">您可以在 vSphere 用戶端的 [最近的工作]  窗格底部檢視狀態。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-238">You can view the status in the bottom **Recent Tasks** pane of the vSphere client.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. <span data-ttu-id="a0f6f-239">安裝工作將需要幾分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-239">The setup tasks will take a few minutes to complete.</span></span> <span data-ttu-id="a0f6f-240">當裝置開始運作時，瀏覽至 [主控台]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-240">Once the device is running, navigate to the **Console** tab.</span></span> <span data-ttu-id="a0f6f-241">傳送 Ctrl+Alt+Delete 來登入裝置。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-241">Send Ctrl+Alt+Delete to log in to the device.</span></span> <span data-ttu-id="a0f6f-242">或者，您可以讓游標指向主控台視窗，然後按下 Ctrl+Alt+Insert。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-242">Alternatively, you can point the cursor on the console window and press Ctrl+Alt+Insert.</span></span> <span data-ttu-id="a0f6f-243">預設使用者為 *StorSimpleAdmin*，預設密碼為 *Password1*。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-243">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. <span data-ttu-id="a0f6f-244">基於安全性理由，裝置系統管理員密碼會在第一次登入時過期。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-244">For security reasons, the device administrator password expires at the first logon.</span></span> <span data-ttu-id="a0f6f-245">系統會提示您變更密碼。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-245">You are prompted to change the password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. <span data-ttu-id="a0f6f-246">請輸入至少包含 8 個字元的密碼。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-246">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="a0f6f-247">密碼必須包含下列 4 個需求中的 3 個：大寫、小寫、數字和特殊字元。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-247">The password must contain 3 out of 4 of these requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="a0f6f-248">請重新輸入密碼來加以確認。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-248">Reenter the password to confirm it.</span></span> <span data-ttu-id="a0f6f-249">系統將會通知您密碼已經變更。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-249">You will be notified that the password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. <span data-ttu-id="a0f6f-250">密碼變更成功之後，裝置可能會重新開機。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-250">After the password is successfully changed, the virtual device may reboot.</span></span> <span data-ttu-id="a0f6f-251">請等待裝置開機完畢。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-251">Wait for the reboot to complete.</span></span> <span data-ttu-id="a0f6f-252">畫面可能會出現裝置的 Windows PowerShell 主控台及進度列。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-252">The Windows PowerShell console of the device may be displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. <span data-ttu-id="a0f6f-253">步驟 6 至 8 僅適用於在非 DHCP 環境中開機的情況。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-253">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="a0f6f-254">如果您是在 DHCP 環境中，請略過這些步驟並前往步驟 9。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-254">If you are in a DHCP environment, then skip these steps and go to step 9.</span></span> <span data-ttu-id="a0f6f-255">如果您是在非 DHCP 環境中讓裝置開機，您會看到下列畫面。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-255">If you booted up your device in non-DHCP environment, you will see the following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   <span data-ttu-id="a0f6f-256">接著，設定網路。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-256">Next, configure the network.</span></span>
7. <span data-ttu-id="a0f6f-257">使用 `Get-HcsIpAddress` 命令來列出虛擬裝置上已啟用的網路介面。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-257">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual device.</span></span> <span data-ttu-id="a0f6f-258">如果您的裝置有已啟用的單一網路介面，系統指派給該介面的預設名稱會是 `Ethernet`。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-258">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. <span data-ttu-id="a0f6f-259">使用 `Set-HcsIpAddress` Cmdlet 來設定網路。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-259">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span></span> <span data-ttu-id="a0f6f-260">範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="a0f6f-260">An example is shown below:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. <span data-ttu-id="a0f6f-261">初始安裝程序完成，且裝置已開機之後，您將會看到裝置橫幅文字。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-261">After the initial setup is complete and the device has booted up, you will see the device banner text.</span></span> <span data-ttu-id="a0f6f-262">請記下 IP 位址及橫幅文字中的 URL，以便管理裝置。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-262">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span></span> <span data-ttu-id="a0f6f-263">您將使用此 IP 位址連線到虛擬裝置的 Web UI，以及完成本機安裝和註冊程序。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-263">You will use this IP address to connect to the web UI of your virtual device and complete the local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. <span data-ttu-id="a0f6f-264">(選擇性) 只有當您要在政府服務雲端部署裝置時，才執行這個步驟。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-264">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span></span> <span data-ttu-id="a0f6f-265">您現在將在您的裝置上啟用美國聯邦資訊處理標準 (FIPS) 模式。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-265">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="a0f6f-266">FIPS 140 標準定義核准美國聯邦政府電腦系統所使用的密碼編譯演算法來保護機密資料。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-266">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span>

    1. <span data-ttu-id="a0f6f-267">若要啟用 FIPS 模式，請執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="a0f6f-267">To enable the FIPS mode, run the following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="a0f6f-268">在您啟用 FIPS 模式之後，重新啟動您的裝置，讓密碼編譯驗證生效。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-268">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="a0f6f-269">您可以在您的裝置上啟用或停用 FIPS 模式。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-269">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="a0f6f-270">不支援在 FIPS 和非 FIPS 模式之間替換裝置。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-270">Alternating the device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="a0f6f-271">如果裝置不符合最低設定需求，橫幅文字中會出現錯誤訊息 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-271">If your device does not meet the minimum configuration requirements, you will see an error in the banner text (shown below).</span></span> <span data-ttu-id="a0f6f-272">您必須修改裝置設定，讓裝置有足夠的資源來符合最低需求。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-272">You will need to modify the device configuration so that it has adequate resources to meet the minimum requirements.</span></span> <span data-ttu-id="a0f6f-273">然後您就可以將裝置重新啟動，並連線到該裝置。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-273">You can then restart and connect to the device.</span></span> <span data-ttu-id="a0f6f-274">請參閱 [步驟 1：確認主機系統符合最低的虛擬裝置需求](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements)中的最低組態需求。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-274">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual device requirements](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

<span data-ttu-id="a0f6f-275">如果您在使用本機 Web UI 進行初始設定時碰到其他任何錯誤，請參閱下列工作流程：</span><span class="sxs-lookup"><span data-stu-id="a0f6f-275">If you face any other error during the initial configuration using the local web UI, refer to the following workflows:</span></span>

* <span data-ttu-id="a0f6f-276">執行診斷測試來 [疑難排解 Web UI 安裝程式錯誤](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors)。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-276">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="a0f6f-277">[產生記錄檔封裝及檢視記錄檔](storsimple-ova-web-ui-admin.md#generate-a-log-package)。</span><span class="sxs-lookup"><span data-stu-id="a0f6f-277">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0f6f-278">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0f6f-278">Next steps</span></span>
* [<span data-ttu-id="a0f6f-279">Set up your StorSimple Virtual Array as a file server (將 StorSimple 虛擬陣列設定為檔案伺服器)</span><span class="sxs-lookup"><span data-stu-id="a0f6f-279">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="a0f6f-280">Set up your StorSimple Virtual Array as an iSCSI server (將 StorSimple 虛擬陣列設定為 iSCSI 伺服器)</span><span class="sxs-lookup"><span data-stu-id="a0f6f-280">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)
