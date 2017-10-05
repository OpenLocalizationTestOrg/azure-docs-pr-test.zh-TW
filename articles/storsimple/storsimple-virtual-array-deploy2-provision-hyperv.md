---
title: "在 Hyper-V 中佈建 StorSimple Virtual Array | Microsoft Docs"
description: "這是 StorSimple Virtual Array 部署中的第二個教學課程，說明在 Hyper-V 中佈建虛擬陣列。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bad431c8958f7d381bb9c0410caa3a57c6e75c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a><span data-ttu-id="f2ef7-103">部署 StorSimple Virtual Array：在 Hyper-V 中佈建</span><span class="sxs-lookup"><span data-stu-id="f2ef7-103">Deploy StorSimple Virtual Array - Provision in Hyper-V</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a><span data-ttu-id="f2ef7-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f2ef7-104">Overview</span></span>
<span data-ttu-id="f2ef7-105">本教學課程說明如何在執行 Windows Server 2012 R2、Windows Server 2012 或 Windows Server 2008 R2 之 Hyper-V 的主機系統上佈建 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-105">This tutorial describes how to provision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <span data-ttu-id="f2ef7-106">本文適用於在 Azure 入口網站及 Microsoft Azure 政府服務雲端部署 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-106">This article applies to the deployment of StorSimple Virtual Arrays in Azure portal and Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="f2ef7-107">您需要有系統管理員權限，才能佈建及設定虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-107">You need administrator privileges to provision and configure a virtual array.</span></span> <span data-ttu-id="f2ef7-108">佈建及初始安裝程序可能需要大約 10 分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-108">The provisioning and initial setup can take around 10 minutes to complete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="f2ef7-109">佈建的必要條件</span><span class="sxs-lookup"><span data-stu-id="f2ef7-109">Provisioning prerequisites</span></span>
<span data-ttu-id="f2ef7-110">此處提供在執行 Windows Server 2012 R2、Windows Server 2012 或 Windows Server 2008 R2 之 Hyper-V 的主機系統上佈建虛擬陣列的必要條件。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-110">Here you will find the prerequisites to provision a virtual array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="f2ef7-111">StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="f2ef7-111">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="f2ef7-112">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="f2ef7-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="f2ef7-113">您已完成 [準備入口網站以使用 StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md)中的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-113">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="f2ef7-114">您已經從 Azure 入口網站下載適用於 Hyper-V 的虛擬陣列映像。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-114">You have downloaded the virtual array image for Hyper-V from the Azure portal.</span></span> <span data-ttu-id="f2ef7-115">如需詳細資訊，請參閱[準備入口網站以使用 StorSimple Virtual Array 指南](storsimple-virtual-array-deploy1-portal-prep.md)的**步驟 3︰下載虛擬陣列映像**。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-115">For more information, see **Step 3: Download the virtual array image** of [Prepare the portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f2ef7-116">StorSimple Virtual Array 上執行的軟體只能搭配 Storsimple 裝置管理員服務來使用。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-116">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span></span>
  >
  >

### <a name="for-the-storsimple-virtual-array"></a><span data-ttu-id="f2ef7-117">StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="f2ef7-117">For the StorSimple Virtual Array</span></span>
<span data-ttu-id="f2ef7-118">在您部署虛擬陣列之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="f2ef7-118">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="f2ef7-119">您可以存取可用來佈建裝置、在 Windows Server 2008 R2 或更新版本上執行 Hyper-V 的主機系統。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-119">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later that can be used to a provision a device.</span></span>
* <span data-ttu-id="f2ef7-120">主機系統能夠把下列資源專門用來佈建虛擬陣列：</span><span class="sxs-lookup"><span data-stu-id="f2ef7-120">The host system is able to dedicate the following resources to provision your virtual array:</span></span>

  * <span data-ttu-id="f2ef7-121">至少 4 顆核心。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-121">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="f2ef7-122">至少 8 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-122">At least 8 GB of RAM.</span></span> <span data-ttu-id="f2ef7-123">若計畫將虛擬陣列設定為檔案伺服器，8 GB 支援 2 百萬個以下的檔案。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-123">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="f2ef7-124">您需要 16 GB RAM 才能支援 2 - 4 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-124">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="f2ef7-125">一個網路介面。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-125">One network interface.</span></span>
  * <span data-ttu-id="f2ef7-126">供資料使用的 500 GB 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-126">A 500 GB virtual disk for data.</span></span>

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="f2ef7-127">針對資料中心內的網路</span><span class="sxs-lookup"><span data-stu-id="f2ef7-127">For the network in the datacenter</span></span>
<span data-ttu-id="f2ef7-128">開始之前，請檢閱部署 StorSimple Virtual Array 的網路需求，並適當地設定資料中心網路。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-128">Before you begin, review the networking requirements to deploy a StorSimple Virtual Array and configure the datacenter network appropriately.</span></span> <span data-ttu-id="f2ef7-129">如需詳細資訊，請參閱 [StorSimple Virtual Array 網路需求](storsimple-ova-system-requirements.md#networking-requirements)。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-129">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span></span>

## <a name="step-by-step-provisioning"></a><span data-ttu-id="f2ef7-130">佈建的逐步指示</span><span class="sxs-lookup"><span data-stu-id="f2ef7-130">Step-by-step provisioning</span></span>
<span data-ttu-id="f2ef7-131">若要佈建並連接至虛擬陣列，您必須執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f2ef7-131">To provision and connect to a virtual array, you need to perform the following steps:</span></span>

1. <span data-ttu-id="f2ef7-132">確定主機系統有足夠的資源符合最低的虛擬陣列需求。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-132">Ensure that the host system has sufficient resources to meet the minimum virtual array requirements.</span></span>
2. <span data-ttu-id="f2ef7-133">在 Hypervisor 中佈建虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-133">Provision a virtual array in your hypervisor.</span></span>
3. <span data-ttu-id="f2ef7-134">啟動虛擬陣列並取得 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-134">Start the virtual array and get the IP address.</span></span>

<span data-ttu-id="f2ef7-135">我們會在下列各節解釋這些步驟。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-135">Each of these steps is explained in the following sections.</span></span>

## <a name="step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements"></a><span data-ttu-id="f2ef7-136">步驟 1：確定主機系統符合最低的虛擬陣列需求</span><span class="sxs-lookup"><span data-stu-id="f2ef7-136">Step 1: Ensure that the host system meets minimum virtual array requirements</span></span>
<span data-ttu-id="f2ef7-137">若要建立虛擬陣列，您需要︰</span><span class="sxs-lookup"><span data-stu-id="f2ef7-137">To create a virtual array, you need:</span></span>

* <span data-ttu-id="f2ef7-138">安裝在 Windows Server 2012 R2、Windows Server 2012 或 Windows Server 2008 R2 SP1 上的 Hyper-V 角色。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-138">The Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span></span>
* <span data-ttu-id="f2ef7-139">在已連線至主機的 Microsoft Windows 用戶端上的 Microsoft Hyper-V 管理員。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-139">Microsoft Hyper-V Manager on a Microsoft Windows client connected to the host.</span></span>

<span data-ttu-id="f2ef7-140">請確定您要建立虛擬陣列的基礎硬體 (主機系統) 能夠把下列資源專門提供給虛擬陣列來使用：</span><span class="sxs-lookup"><span data-stu-id="f2ef7-140">Make sure that the underlying hardware (host system) on which you are creating the virtual array is able to dedicate the following resources to your virtual array:</span></span>

* <span data-ttu-id="f2ef7-141">至少 4 顆核心。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-141">A minimum of 4 cores.</span></span>
* <span data-ttu-id="f2ef7-142">至少 8 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-142">At least 8 GB of RAM.</span></span> <span data-ttu-id="f2ef7-143">若計畫將虛擬陣列設定為檔案伺服器，8 GB 支援 2 百萬個以下的檔案。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-143">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="f2ef7-144">您需要 16 GB RAM 才能支援 2 - 4 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-144">You need 16 GB RAM to support 2 - 4 million files.</span></span>
* <span data-ttu-id="f2ef7-145">一個網路介面。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-145">One network interface.</span></span>
* <span data-ttu-id="f2ef7-146">供系統資料使用的 500 GB 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-146">A 500 GB virtual disk for system data.</span></span>

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a><span data-ttu-id="f2ef7-147">步驟 2：在 Hypervisor 中佈建虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="f2ef7-147">Step 2: Provision a virtual array in hypervisor</span></span>
<span data-ttu-id="f2ef7-148">請執行下列步驟，以便在您的 Hypervisor 中佈建裝置。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-148">Perform the following steps to provision a device in your hypervisor.</span></span>

#### <a name="to-provision-a-virtual-array"></a><span data-ttu-id="f2ef7-149">若要佈建虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="f2ef7-149">To provision a virtual array</span></span>
1. <span data-ttu-id="f2ef7-150">在 Windows Server 主機上，將虛擬陣列映像複製到本機磁碟機。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-150">On your Windows Server host, copy the virtual array image to a local drive.</span></span> <span data-ttu-id="f2ef7-151">您已透過 Azure 入口網站下載此映像 (VHD 或 VHDX)。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-151">You downloaded this image (VHD or VHDX) through the Azure portal.</span></span> <span data-ttu-id="f2ef7-152">請記下您複製映像的位置，因為稍後會在程序中使用此映像。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-152">Make a note of the location where you copied the image as you are using this image later in the procedure.</span></span>
2. <span data-ttu-id="f2ef7-153">開啟 [伺服器管理員] 。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-153">Open **Server Manager**.</span></span> <span data-ttu-id="f2ef7-154">按一下右上角的 [工具]，然後選取 [Hyper-V 管理員]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-154">In the top right corner, click **Tools** and select **Hyper-V Manager**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   <span data-ttu-id="f2ef7-155">如果您執行的是 Windows Server 2008 R2，請開啟「Hyper-V 管理員」。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-155">If you are running Windows Server 2008 R2, open the Hyper-V Manager.</span></span> <span data-ttu-id="f2ef7-156">在 [伺服器管理員] 中，按一下 [角色] > [Hyper-V] > [Hyper-V 管理員]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-156">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span></span>
3. <span data-ttu-id="f2ef7-157">在 [Hyper-V 管理員] 的範圍窗格中，於您的系統節點上按一下滑鼠右鍵以開啟操作功能表，然後按一下 [新增]  >  [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-157">In **Hyper-V Manager**, in the scope pane, right-click your system node to open the context menu, and then click **New** > **Virtual Machine**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. <span data-ttu-id="f2ef7-158">在「新增虛擬機器精靈」的 [開始之前] 頁面上，按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-158">On the **Before you begin** page of the New Virtual Machine Wizard, click **Next**.</span></span>
5. <span data-ttu-id="f2ef7-159">在 [指定名稱和位置] 頁面上，提供虛擬陣列的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-159">On the **Specify name and location** page, provide a **Name** for your virtual array.</span></span> <span data-ttu-id="f2ef7-160">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-160">Click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. <span data-ttu-id="f2ef7-161">在 [指定世代] 頁面上，選擇裝置映像類型，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-161">On the **Specify generation** page, choose the device image type, and then click **Next**.</span></span> <span data-ttu-id="f2ef7-162">如果您使用的是 Windows Server 2008 R2，則不會出現此頁面。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-162">This page doesn't appear if you're using Windows Server 2008 R2.</span></span>

   * <span data-ttu-id="f2ef7-163">如果您已下載適用於 Windows Server 2012 或更新版本的 .vhdx 映像，請選擇 [第 2 代]  。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-163">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span></span>
   * <span data-ttu-id="f2ef7-164">如果您已下載適用於 Windows Server 2008 R2 或更新版本的 .vhd 映像，請選擇 [第 1 代]  。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-164">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. <span data-ttu-id="f2ef7-165">在 [指派記憶體] 頁面上，至少指定 **8192 MB** 的「啟動記憶體」，請勿啟用動態記憶體，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-165">On the **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. <span data-ttu-id="f2ef7-166">在 [設定網路功能] 頁面上，指定連線到網際網路的虛擬交換器，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-166">On the **Configure networking** page, specify the virtual switch that is connected to the Internet and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. <span data-ttu-id="f2ef7-167">在 [連接虛擬硬碟] 頁面上，選擇 [使用現有的虛擬硬碟]，指定虛擬陣列映像 (.vhdx 或.vhd) 的位置，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-167">On the **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify the location of the virtual array image (.vhdx or .vhd), and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. <span data-ttu-id="f2ef7-168">檢閱「摘要」，然後按一下 [結束] 來建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-168">Review the **Summary** and then click **Finish** to create the virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. <span data-ttu-id="f2ef7-169">您需要 4 顆核心才能符合最低需求。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-169">To meet the minimum requirements, you need 4 cores.</span></span> <span data-ttu-id="f2ef7-170">若要新增 4 顆虛擬處理器，請在 [Hyper-V 管理員] 視窗中選取您的主機系統。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-170">To add 4 virtual processors, select your host system in the **Hyper-V Manager** window.</span></span> <span data-ttu-id="f2ef7-171">在右窗格中的 [虛擬機器] 清單下，找出您剛才建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-171">In the right-pane under the list of **Virtual Machines**, locate the virtual machine you just created.</span></span> <span data-ttu-id="f2ef7-172">選取虛擬機器的名稱並按一下滑鼠右鍵，然後選取 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-172">Select and right-click the machine name and select **Settings**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. <span data-ttu-id="f2ef7-173">在 [設定] 頁面上，按一下左窗格中的 [處理器]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-173">On the **Settings** page, in the left-pane, click **Processor**.</span></span> <span data-ttu-id="f2ef7-174">在右窗格中，將 [虛擬處理器數目] 設定為 4 (或更多)。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-174">In the right-pane, set **number of virtual processors** to 4 (or more).</span></span> <span data-ttu-id="f2ef7-175">按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-175">Click **Apply**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. <span data-ttu-id="f2ef7-176">您也必須新增 500 GB 的虛擬資料磁碟，才能符合最低需求。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-176">To meet the minimum requirements, you also need to add a 500 GB virtual data disk.</span></span> <span data-ttu-id="f2ef7-177">在 [設定] 頁面中：</span><span class="sxs-lookup"><span data-stu-id="f2ef7-177">In the **Settings** page:</span></span>

    1. <span data-ttu-id="f2ef7-178">在左窗格中，選取 [SCSI 控制器]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-178">In the left pane, select **SCSI Controller**.</span></span>
    2. <span data-ttu-id="f2ef7-179">在右窗格中，選取 [硬碟]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-179">In the right pane, select **Hard Drive,** and click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. <span data-ttu-id="f2ef7-180">在 [硬碟] 頁面上，選取 [虛擬硬碟] 選項，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-180">On the **Hard drive** page, select the **Virtual hard disk** option and click **New**.</span></span> <span data-ttu-id="f2ef7-181">[新增虛擬硬碟精靈] 會啟動。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-181">The **New Virtual Hard Disk Wizard** starts.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. <span data-ttu-id="f2ef7-182">在「新增虛擬硬碟精靈」的 [開始之前] 頁面上，按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-182">On the **Before you begin** page of the New Virtual Hard Disk Wizard, click **Next**.</span></span>
16. <span data-ttu-id="f2ef7-183">在 [選擇磁碟格式] 頁面上，接受 [VHDX] 格式預設選項。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-183">On the **Choose Disk Format page**, accept the default option of **VHDX** format.</span></span> <span data-ttu-id="f2ef7-184">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-184">Click **Next**.</span></span> <span data-ttu-id="f2ef7-185">如果您執行的是 Windows Server 2008 R2，則不會出現此畫面。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-185">This screen is not presented if running Windows Server 2008 R2.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. <span data-ttu-id="f2ef7-186">在 [選擇磁碟類型] 頁面上，將虛擬硬碟類型設定為 [動態擴充] \(建議選項)。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-186">On the **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span></span> <span data-ttu-id="f2ef7-187">[固定大小] 磁碟可以運作，但您可能需要等待很長一段時間。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-187">**Fixed size** disk would work but you may need to wait a long time.</span></span> <span data-ttu-id="f2ef7-188">建議您不要使用 [差異]  選項。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-188">We recommend that you do not use the **Differencing** option.</span></span> <span data-ttu-id="f2ef7-189">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-189">Click **Next**.</span></span> <span data-ttu-id="f2ef7-190">在 Windows Server 2012 R2 和 Windows Server 2012 中，[動態擴充] 是預設選項，而在 Windows Server 2008 R2 中，預設值是 [固定大小]。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-190">In Windows Server 2012 R2 and Windows Server 2012, **Dynamically expanding** is the default option whereas in Windows Server 2008 R2, the default is **Fixed size**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. <span data-ttu-id="f2ef7-191">在 [指定名稱和位置] 頁面上，提供資料磁碟的「名稱」和「位置」(您可以瀏覽至該位置)。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-191">On the **Specify Name and Location** page, provide a **name** as well as **location** (you can browse to one) for the data disk.</span></span> <span data-ttu-id="f2ef7-192">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. <span data-ttu-id="f2ef7-193">在「設定磁碟」頁面上，選取 [建立新的空白虛擬硬碟] 選項，然後將大小指定為 **500 GB** (或更多)。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-193">On the **Configure Disk** page, select the option **Create a new blank virtual hard disk** and specify the size as **500 GB** (or more).</span></span> <span data-ttu-id="f2ef7-194">500 GB 是最低需求，您永遠可以佈建更大的磁碟。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-194">While 500 GB is the minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="f2ef7-195">請注意，佈建之後您無法擴充或縮小磁碟。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-195">Note that you cannot expand or shrink the disk once provisioned.</span></span> <span data-ttu-id="f2ef7-196">如需有關要佈建之磁碟大小的詳細資訊，請檢閱[最佳作法文件](storsimple-ova-best-practices.md)中的＜調整大小＞一節。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-196">For more information on the size of disk to provision, review the sizing section in the [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="f2ef7-197">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. <span data-ttu-id="f2ef7-198">在 [摘要] 頁面上，檢閱虛擬資料磁碟的詳細資料，如果您對這些資料感到滿意，請按一下 [完成] 來建立磁碟。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-198">On the **Summary** page, review the details of your virtual data disk and if satisfied, click **Finish** to create the disk.</span></span> <span data-ttu-id="f2ef7-199">精靈會關閉，虛擬硬碟會新增至您的電腦。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-199">The wizard closes and a virtual hard disk is added to your machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. <span data-ttu-id="f2ef7-200">返回 [設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-200">Return to the **Settings** page.</span></span> <span data-ttu-id="f2ef7-201">按一下 [確定] 來關閉「設定」頁面並返回 [Hyper-V 管理員] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-201">Click **OK** to close the **Settings** page and return to Hyper-V Manager window.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-the-virtual-array-and-get-the-ip"></a><span data-ttu-id="f2ef7-202">步驟 3：啟動虛擬陣列並取得 IP</span><span class="sxs-lookup"><span data-stu-id="f2ef7-202">Step 3: Start the virtual array and get the IP</span></span>
<span data-ttu-id="f2ef7-203">請執行下列步驟來啟動並連接至虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-203">Perform the following steps to start your virtual array and connect to it.</span></span>

#### <a name="to-start-the-virtual-array"></a><span data-ttu-id="f2ef7-204">若要啟動虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="f2ef7-204">To start the virtual array</span></span>
1. <span data-ttu-id="f2ef7-205">啟動虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-205">Start the virtual array.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. <span data-ttu-id="f2ef7-206">當裝置開始執行之後，選取裝置並按一下滑鼠右鍵，然後選取 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-206">After the device is running, select the device, right click, and select **Connect**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. <span data-ttu-id="f2ef7-207">您可能需要等待 5 至 10 分鐘，裝置才會準備就緒。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-207">You may have to wait 5-10 minutes for the device to be ready.</span></span> <span data-ttu-id="f2ef7-208">主控台會顯示狀態訊息以表明進度。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-208">A status message is displayed on the console to indicate the progress.</span></span> <span data-ttu-id="f2ef7-209">裝置就緒之後，請前往 [動作] 。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-209">After the device is ready, go to **Action**.</span></span> <span data-ttu-id="f2ef7-210">按 `Ctrl + Alt + Delete` 來登入虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-210">Press `Ctrl + Alt + Delete` to log in to the virtual array.</span></span> <span data-ttu-id="f2ef7-211">預設使用者為 *StorSimpleAdmin*，預設密碼為 *Password1*。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-211">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. <span data-ttu-id="f2ef7-212">基於安全性理由，裝置系統管理員密碼會在第一次登入時過期。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-212">For security reasons, the device administrator password expires at the first logon.</span></span> <span data-ttu-id="f2ef7-213">系統會提示您變更密碼。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-213">You are prompted to change the password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   <span data-ttu-id="f2ef7-214">請輸入至少包含 8 個字元的密碼。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-214">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="f2ef7-215">密碼必須至少符合下列 4 個需求中的 3 個：大寫、小寫、數字和特殊字元。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-215">The password must satisfy at least 3 out of the following 4 requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="f2ef7-216">請重新輸入密碼來加以確認。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-216">Reenter the password to confirm it.</span></span> <span data-ttu-id="f2ef7-217">系統會通知您密碼已經變更。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-217">You are notified that the password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. <span data-ttu-id="f2ef7-218">成功變更密碼之後，虛擬陣列可能會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-218">After the password is successfully changed, the virtual array may restart.</span></span> <span data-ttu-id="f2ef7-219">請等待裝置啟動。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-219">Wait for the device to start.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    <span data-ttu-id="f2ef7-220">畫面會出現裝置的 Windows PowerShell 主控台及進度列。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-220">The Windows PowerShell console of the device is displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. <span data-ttu-id="f2ef7-221">步驟 6 至 8 僅適用於在非 DHCP 環境中開機的情況。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-221">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="f2ef7-222">如果您是在 DHCP 環境中，請略過這些步驟並前往步驟 9。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-222">If you are in a DHCP environment, then skip these steps and go to step 9.</span></span> <span data-ttu-id="f2ef7-223">如果您是在非 DHCP 環境中讓裝置開機，您會看到下列畫面。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-223">If you booted up your device in non-DHCP environment, you will see the following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    <span data-ttu-id="f2ef7-224">接著，設定網路。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-224">Next, configure the network.</span></span>
7. <span data-ttu-id="f2ef7-225">使用 `Get-HcsIpAddress` 命令來列出虛擬陣列上已啟用的網路介面。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-225">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual array.</span></span> <span data-ttu-id="f2ef7-226">如果您的裝置有已啟用的單一網路介面，系統指派給該介面的預設名稱會是 `Ethernet`。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-226">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. <span data-ttu-id="f2ef7-227">使用 `Set-HcsIpAddress` Cmdlet 來設定網路。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-227">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span></span> <span data-ttu-id="f2ef7-228">請參閱下列範例：</span><span class="sxs-lookup"><span data-stu-id="f2ef7-228">See the following example:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. <span data-ttu-id="f2ef7-229">初始安裝程序完成，且裝置已開機之後，您將會看到裝置橫幅文字。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-229">After the initial setup is complete and the device has booted up, you will see the device banner text.</span></span> <span data-ttu-id="f2ef7-230">請記下 IP 位址及橫幅文字中的 URL，以便管理裝置。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-230">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span></span> <span data-ttu-id="f2ef7-231">使用此 IP 位址連接至虛擬陣列的 Web UI，並完成本機設定和註冊。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-231">Use this IP address to connect to the web UI of your virtual array and complete the local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. <span data-ttu-id="f2ef7-232">(選擇性) 只有當您要在政府服務雲端部署裝置時，才執行這個步驟。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-232">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span></span> <span data-ttu-id="f2ef7-233">您現在將在您的裝置上啟用美國聯邦資訊處理標準 (FIPS) 模式。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-233">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="f2ef7-234">FIPS 140 標準定義核准美國聯邦政府電腦系統所使用的密碼編譯演算法來保護機密資料。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-234">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span>

    1. <span data-ttu-id="f2ef7-235">若要啟用 FIPS 模式，請執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="f2ef7-235">To enable the FIPS mode, run the following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="f2ef7-236">在您啟用 FIPS 模式之後，重新啟動您的裝置，讓密碼編譯驗證生效。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-236">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="f2ef7-237">您可以在您的裝置上啟用或停用 FIPS 模式。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-237">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="f2ef7-238">不支援在 FIPS 和非 FIPS 模式之間替換裝置。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-238">Alternating the device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="f2ef7-239">如果裝置不符合最低設定需求，橫幅文字中會出現下列錯誤 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-239">If your device does not meet the minimum configuration requirements, you see the following error in the banner text (shown below).</span></span> <span data-ttu-id="f2ef7-240">請修改裝置設定，讓電腦有足夠的資源符合最低需求。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-240">Modify the device configuration so that the machine has adequate resources to meet the minimum requirements.</span></span> <span data-ttu-id="f2ef7-241">然後您就可以將裝置重新啟動，並連線到該裝置。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-241">You can then restart and connect to the device.</span></span> <span data-ttu-id="f2ef7-242">請參閱[步驟 1：確定主機系統符合最低的虛擬陣列需求](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements)中的最低設定需求。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-242">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual array requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

<span data-ttu-id="f2ef7-243">如果您在使用本機 Web UI 進行初始設定時碰到其他任何錯誤，請參閱下列工作流程：</span><span class="sxs-lookup"><span data-stu-id="f2ef7-243">If you face any other error during the initial configuration using the local web UI, refer to the following workflows:</span></span>

* <span data-ttu-id="f2ef7-244">執行診斷測試來 [疑難排解 Web UI 安裝程式錯誤](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors)。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-244">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="f2ef7-245">[產生記錄檔封裝及檢視記錄檔](storsimple-ova-web-ui-admin.md#generate-a-log-package)。</span><span class="sxs-lookup"><span data-stu-id="f2ef7-245">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2ef7-246">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2ef7-246">Next steps</span></span>
* [<span data-ttu-id="f2ef7-247">Set up your StorSimple Virtual Array as a file server (將 StorSimple 虛擬陣列設定為檔案伺服器)</span><span class="sxs-lookup"><span data-stu-id="f2ef7-247">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="f2ef7-248">Set up your StorSimple Virtual Array as an iSCSI server (將 StorSimple 虛擬陣列設定為 iSCSI 伺服器)</span><span class="sxs-lookup"><span data-stu-id="f2ef7-248">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)
