---
title: "在 HYPER-V 中的 StorSimple Virtual Array aaaProvision |Microsoft 文件"
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
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a><span data-ttu-id="5a039-103">部署 StorSimple Virtual Array：在 Hyper-V 中佈建</span><span class="sxs-lookup"><span data-stu-id="5a039-103">Deploy StorSimple Virtual Array - Provision in Hyper-V</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a><span data-ttu-id="5a039-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5a039-104">Overview</span></span>
<span data-ttu-id="5a039-105">本教學課程說明如何 tooprovision StorSimple 虛擬陣列在 Windows Server 2012 R2、 Windows Server 2012 或 Windows Server 2008 R2 上執行 HYPER-V 的主機系統上。</span><span class="sxs-lookup"><span data-stu-id="5a039-105">This tutorial describes how tooprovision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <span data-ttu-id="5a039-106">本文適用於 StorSimple 虛擬陣列在 Azure 入口網站和 Microsoft Azure 政府雲端中的 toohello 部署。</span><span class="sxs-lookup"><span data-stu-id="5a039-106">This article applies toohello deployment of StorSimple Virtual Arrays in Azure portal and Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="5a039-107">您需要系統管理員權限 tooprovision，及設定的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="5a039-107">You need administrator privileges tooprovision and configure a virtual array.</span></span> <span data-ttu-id="5a039-108">hello 佈建和初始設定可能需要約為 10 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="5a039-108">hello provisioning and initial setup can take around 10 minutes toocomplete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="5a039-109">佈建的必要條件</span><span class="sxs-lookup"><span data-stu-id="5a039-109">Provisioning prerequisites</span></span>
<span data-ttu-id="5a039-110">這裡您將找到 hello 必要條件 tooprovision 虛擬陣列在 Windows Server 2012 R2、 Windows Server 2012 或 Windows Server 2008 R2 上執行 HYPER-V 的主機系統上。</span><span class="sxs-lookup"><span data-stu-id="5a039-110">Here you will find hello prerequisites tooprovision a virtual array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span>

### <a name="for-hello-storsimple-device-manager-service"></a><span data-ttu-id="5a039-111">Hello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="5a039-111">For hello StorSimple Device Manager service</span></span>
<span data-ttu-id="5a039-112">在您開始前，請確定：</span><span class="sxs-lookup"><span data-stu-id="5a039-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="5a039-113">您已完成所有 hello 步驟[準備 hello 入口網站，供 StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md)。</span><span class="sxs-lookup"><span data-stu-id="5a039-113">You have completed all hello steps in [Prepare hello portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="5a039-114">您已下載之 HYPER-V 的 hello 虛擬陣列映像從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5a039-114">You have downloaded hello virtual array image for Hyper-V from hello Azure portal.</span></span> <span data-ttu-id="5a039-115">如需詳細資訊，請參閱**步驟 3： 下載 hello 虛擬陣列影像**的[準備 hello 入口網站的 StorSimple Virtual Array 指南](storsimple-virtual-array-deploy1-portal-prep.md)。</span><span class="sxs-lookup"><span data-stu-id="5a039-115">For more information, see **Step 3: Download hello virtual array image** of [Prepare hello portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5a039-116">hello StorSimple Virtual Array 上所執行的 hello 軟體只能搭配 hello StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="5a039-116">hello software running on hello StorSimple Virtual Array may only be used with hello StorSimple Device Manager service.</span></span>
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a><span data-ttu-id="5a039-117">Hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="5a039-117">For hello StorSimple Virtual Array</span></span>
<span data-ttu-id="5a039-118">在您部署虛擬陣列之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="5a039-118">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="5a039-119">您必須執行 HYPER-V 的 Windows Server 2008 R2 或更新版本，可以是使用的 tooa 佈建的裝置存取 tooa 主機系統。</span><span class="sxs-lookup"><span data-stu-id="5a039-119">You have access tooa host system running Hyper-V on Windows Server 2008 R2 or later that can be used tooa provision a device.</span></span>
* <span data-ttu-id="5a039-120">hello 主機系統是無法 toodedicate hello 下列資源 tooprovision 虛擬陣列：</span><span class="sxs-lookup"><span data-stu-id="5a039-120">hello host system is able toodedicate hello following resources tooprovision your virtual array:</span></span>

  * <span data-ttu-id="5a039-121">至少 4 顆核心。</span><span class="sxs-lookup"><span data-stu-id="5a039-121">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="5a039-122">至少 8 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="5a039-122">At least 8 GB of RAM.</span></span> <span data-ttu-id="5a039-123">如果您計劃 tooconfigure hello 虛擬與檔案伺服器陣列，8 GB 支援小於 2 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="5a039-123">If you plan tooconfigure hello virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="5a039-124">您需要 16 GB RAM toosupport 2-4 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="5a039-124">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
  * <span data-ttu-id="5a039-125">一個網路介面。</span><span class="sxs-lookup"><span data-stu-id="5a039-125">One network interface.</span></span>
  * <span data-ttu-id="5a039-126">供資料使用的 500 GB 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="5a039-126">A 500 GB virtual disk for data.</span></span>

### <a name="for-hello-network-in-hello-datacenter"></a><span data-ttu-id="5a039-127">Hello 資料中心中的 hello 網路</span><span class="sxs-lookup"><span data-stu-id="5a039-127">For hello network in hello datacenter</span></span>
<span data-ttu-id="5a039-128">在開始之前，請檢閱網路需求 toodeploy StorSimple Virtual Array hello，並適當地設定 hello 資料中心網路。</span><span class="sxs-lookup"><span data-stu-id="5a039-128">Before you begin, review hello networking requirements toodeploy a StorSimple Virtual Array and configure hello datacenter network appropriately.</span></span> <span data-ttu-id="5a039-129">如需詳細資訊，請參閱 [StorSimple Virtual Array 網路需求](storsimple-ova-system-requirements.md#networking-requirements)。</span><span class="sxs-lookup"><span data-stu-id="5a039-129">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span></span>

## <a name="step-by-step-provisioning"></a><span data-ttu-id="5a039-130">佈建的逐步指示</span><span class="sxs-lookup"><span data-stu-id="5a039-130">Step-by-step provisioning</span></span>
<span data-ttu-id="5a039-131">tooprovision 和 tooa 虛擬陣列連接，您需要下列步驟 tooperform hello:</span><span class="sxs-lookup"><span data-stu-id="5a039-131">tooprovision and connect tooa virtual array, you need tooperform hello following steps:</span></span>

1. <span data-ttu-id="5a039-132">請確認 hello 主機系統有足夠的資源 toomeet hello 的最小的虛擬陣列需求。</span><span class="sxs-lookup"><span data-stu-id="5a039-132">Ensure that hello host system has sufficient resources toomeet hello minimum virtual array requirements.</span></span>
2. <span data-ttu-id="5a039-133">在 Hypervisor 中佈建虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="5a039-133">Provision a virtual array in your hypervisor.</span></span>
3. <span data-ttu-id="5a039-134">啟動 hello 虛擬陣列，並取得 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5a039-134">Start hello virtual array and get hello IP address.</span></span>

<span data-ttu-id="5a039-135">Hello 下列各節將說明每個步驟。</span><span class="sxs-lookup"><span data-stu-id="5a039-135">Each of these steps is explained in hello following sections.</span></span>

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a><span data-ttu-id="5a039-136">步驟 1： 確定 hello 主機系統符合最低虛擬陣列需求</span><span class="sxs-lookup"><span data-stu-id="5a039-136">Step 1: Ensure that hello host system meets minimum virtual array requirements</span></span>
<span data-ttu-id="5a039-137">toocreate 虛擬陣列，您需要：</span><span class="sxs-lookup"><span data-stu-id="5a039-137">toocreate a virtual array, you need:</span></span>

* <span data-ttu-id="5a039-138">Windows Server 2012 R2、 Windows Server 2012 或 Windows Server 2008 R2 SP1 上安裝的 hello HYPER-V 角色。</span><span class="sxs-lookup"><span data-stu-id="5a039-138">hello Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span></span>
* <span data-ttu-id="5a039-139">Microsoft Windows 用戶端上的 Microsoft HYPER-V 管理員連接 toohello 主機。</span><span class="sxs-lookup"><span data-stu-id="5a039-139">Microsoft Hyper-V Manager on a Microsoft Windows client connected toohello host.</span></span>

<span data-ttu-id="5a039-140">請確定該 hello 基礎的硬體 （主機系統） 建立 hello 虛擬陣列可以 toodedicate hello 下列資源 tooyour 虛擬陣列：</span><span class="sxs-lookup"><span data-stu-id="5a039-140">Make sure that hello underlying hardware (host system) on which you are creating hello virtual array is able toodedicate hello following resources tooyour virtual array:</span></span>

* <span data-ttu-id="5a039-141">至少 4 顆核心。</span><span class="sxs-lookup"><span data-stu-id="5a039-141">A minimum of 4 cores.</span></span>
* <span data-ttu-id="5a039-142">至少 8 GB 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="5a039-142">At least 8 GB of RAM.</span></span> <span data-ttu-id="5a039-143">如果您計劃 tooconfigure hello 虛擬與檔案伺服器陣列，8 GB 支援小於 2 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="5a039-143">If you plan tooconfigure hello virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="5a039-144">您需要 16 GB RAM toosupport 2-4 百萬個檔案。</span><span class="sxs-lookup"><span data-stu-id="5a039-144">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
* <span data-ttu-id="5a039-145">一個網路介面。</span><span class="sxs-lookup"><span data-stu-id="5a039-145">One network interface.</span></span>
* <span data-ttu-id="5a039-146">供系統資料使用的 500 GB 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="5a039-146">A 500 GB virtual disk for system data.</span></span>

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a><span data-ttu-id="5a039-147">步驟 2：在 Hypervisor 中佈建虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="5a039-147">Step 2: Provision a virtual array in hypervisor</span></span>
<span data-ttu-id="5a039-148">執行下列步驟 tooprovision 您的 hypervisor 中的裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="5a039-148">Perform hello following steps tooprovision a device in your hypervisor.</span></span>

#### <a name="tooprovision-a-virtual-array"></a><span data-ttu-id="5a039-149">tooprovision 虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="5a039-149">tooprovision a virtual array</span></span>
1. <span data-ttu-id="5a039-150">在 Windows Server 主機上，複製 hello 虛擬陣列映像 tooa 本機磁碟機。</span><span class="sxs-lookup"><span data-stu-id="5a039-150">On your Windows Server host, copy hello virtual array image tooa local drive.</span></span> <span data-ttu-id="5a039-151">您透過 hello Azure 入口網站下載此映像 （VHD 或 VHDX）。</span><span class="sxs-lookup"><span data-stu-id="5a039-151">You downloaded this image (VHD or VHDX) through hello Azure portal.</span></span> <span data-ttu-id="5a039-152">記下您稍後在 hello 程序中使用此映像時，會複製 hello 映像的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="5a039-152">Make a note of hello location where you copied hello image as you are using this image later in hello procedure.</span></span>
2. <span data-ttu-id="5a039-153">開啟 [伺服器管理員] 。</span><span class="sxs-lookup"><span data-stu-id="5a039-153">Open **Server Manager**.</span></span> <span data-ttu-id="5a039-154">在 hello 頂端的右上角，按一下 **工具**選取**HYPER-V 管理員**。</span><span class="sxs-lookup"><span data-stu-id="5a039-154">In hello top right corner, click **Tools** and select **Hyper-V Manager**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   <span data-ttu-id="5a039-155">如果您執行 Windows Server 2008 R2，開啟 HYPER-V 管理員 hello。</span><span class="sxs-lookup"><span data-stu-id="5a039-155">If you are running Windows Server 2008 R2, open hello Hyper-V Manager.</span></span> <span data-ttu-id="5a039-156">在 [伺服器管理員] 中，按一下 [角色] > [Hyper-V] > [Hyper-V 管理員]。</span><span class="sxs-lookup"><span data-stu-id="5a039-156">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span></span>
3. <span data-ttu-id="5a039-157">在**HYPER-V 管理員**hello 範圍窗格中，在您系統節點 tooopen hello 內容功能表中，以滑鼠右鍵按一下，然後按**新增** > **虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="5a039-157">In **Hyper-V Manager**, in hello scope pane, right-click your system node tooopen hello context menu, and then click **New** > **Virtual Machine**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. <span data-ttu-id="5a039-158">在 hello**開始之前**hello 新的虛擬機器精靈 頁面按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5a039-158">On hello **Before you begin** page of hello New Virtual Machine Wizard, click **Next**.</span></span>
5. <span data-ttu-id="5a039-159">在 hello**指定名稱和位置**頁面上，提供**名稱**的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="5a039-159">On hello **Specify name and location** page, provide a **Name** for your virtual array.</span></span> <span data-ttu-id="5a039-160">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5a039-160">Click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. <span data-ttu-id="5a039-161">在 hello**指定世代**頁面上，選擇 hello 映像的裝置類型，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5a039-161">On hello **Specify generation** page, choose hello device image type, and then click **Next**.</span></span> <span data-ttu-id="5a039-162">如果您使用的是 Windows Server 2008 R2，則不會出現此頁面。</span><span class="sxs-lookup"><span data-stu-id="5a039-162">This page doesn't appear if you're using Windows Server 2008 R2.</span></span>

   * <span data-ttu-id="5a039-163">如果您已下載適用於 Windows Server 2012 或更新版本的 .vhdx 映像，請選擇 [第 2 代]  。</span><span class="sxs-lookup"><span data-stu-id="5a039-163">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span></span>
   * <span data-ttu-id="5a039-164">如果您已下載適用於 Windows Server 2008 R2 或更新版本的 .vhd 映像，請選擇 [第 1 代]  。</span><span class="sxs-lookup"><span data-stu-id="5a039-164">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. <span data-ttu-id="5a039-165">在 hello**指派記憶體**頁面上，指定**啟動記憶體**的至少**8192 MB**，不要啟用動態記憶體 」，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5a039-165">On hello **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. <span data-ttu-id="5a039-166">在 hello**設定網路功能**頁面上，指定連接的 toohello 網際網路 hello 虛擬交換器，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5a039-166">On hello **Configure networking** page, specify hello virtual switch that is connected toohello Internet and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. <span data-ttu-id="5a039-167">在 hello**連接虛擬硬碟**頁面上，選擇**使用現有的虛擬硬碟**指定 hello hello 虛擬陣列映像 （.vhdx 或.vhd） 的位置，然後按**下一步**.</span><span class="sxs-lookup"><span data-stu-id="5a039-167">On hello **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify hello location of hello virtual array image (.vhdx or .vhd), and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. <span data-ttu-id="5a039-168">檢閱 hello**摘要**，然後按一下**完成**toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5a039-168">Review hello **Summary** and then click **Finish** toocreate hello virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. <span data-ttu-id="5a039-169">toomeet hello 最低需求，您需要 4 個核心。</span><span class="sxs-lookup"><span data-stu-id="5a039-169">toomeet hello minimum requirements, you need 4 cores.</span></span> <span data-ttu-id="5a039-170">tooadd 4 個虛擬處理器，選取在主機系統中 hello **HYPER-V 管理員**視窗。</span><span class="sxs-lookup"><span data-stu-id="5a039-170">tooadd 4 virtual processors, select your host system in hello **Hyper-V Manager** window.</span></span> <span data-ttu-id="5a039-171">在 hello 右窗格中的 hello 清單下**虛擬機器**，找出您剛才建立的 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5a039-171">In hello right-pane under hello list of **Virtual Machines**, locate hello virtual machine you just created.</span></span> <span data-ttu-id="5a039-172">選取並以滑鼠右鍵按一下 hello 機器名稱，然後選取**設定**。</span><span class="sxs-lookup"><span data-stu-id="5a039-172">Select and right-click hello machine name and select **Settings**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. <span data-ttu-id="5a039-173">在 hello**設定**頁面上，在 hello 左窗格中，按一下**處理器**。</span><span class="sxs-lookup"><span data-stu-id="5a039-173">On hello **Settings** page, in hello left-pane, click **Processor**.</span></span> <span data-ttu-id="5a039-174">在 hello 右窗格中，設定**的虛擬處理器數量**too4 （或以上）。</span><span class="sxs-lookup"><span data-stu-id="5a039-174">In hello right-pane, set **number of virtual processors** too4 (or more).</span></span> <span data-ttu-id="5a039-175">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="5a039-175">Click **Apply**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. <span data-ttu-id="5a039-176">toomeet hello 最低需求，您也需要 tooadd 500 GB 虛擬資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="5a039-176">toomeet hello minimum requirements, you also need tooadd a 500 GB virtual data disk.</span></span> <span data-ttu-id="5a039-177">在 hello**設定**頁面：</span><span class="sxs-lookup"><span data-stu-id="5a039-177">In hello **Settings** page:</span></span>

    1. <span data-ttu-id="5a039-178">Hello 左窗格中，選取**SCSI 控制器**。</span><span class="sxs-lookup"><span data-stu-id="5a039-178">In hello left pane, select **SCSI Controller**.</span></span>
    2. <span data-ttu-id="5a039-179">Hello 右窗格中，選取**硬碟機**按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="5a039-179">In hello right pane, select **Hard Drive,** and click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. <span data-ttu-id="5a039-180">在 hello**硬碟**頁面上，選取 hello**虛擬硬碟**選項，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="5a039-180">On hello **Hard drive** page, select hello **Virtual hard disk** option and click **New**.</span></span> <span data-ttu-id="5a039-181">hello**新的虛擬硬碟精靈**啟動。</span><span class="sxs-lookup"><span data-stu-id="5a039-181">hello **New Virtual Hard Disk Wizard** starts.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. <span data-ttu-id="5a039-182">在 hello**開始之前**的 hello 新增虛擬硬碟精靈 頁面上按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5a039-182">On hello **Before you begin** page of hello New Virtual Hard Disk Wizard, click **Next**.</span></span>
16. <span data-ttu-id="5a039-183">在 [hello**選擇磁碟格式] 頁面上**，接受預設選項 hello **VHDX**格式。</span><span class="sxs-lookup"><span data-stu-id="5a039-183">On hello **Choose Disk Format page**, accept hello default option of **VHDX** format.</span></span> <span data-ttu-id="5a039-184">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5a039-184">Click **Next**.</span></span> <span data-ttu-id="5a039-185">如果您執行的是 Windows Server 2008 R2，則不會出現此畫面。</span><span class="sxs-lookup"><span data-stu-id="5a039-185">This screen is not presented if running Windows Server 2008 R2.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. <span data-ttu-id="5a039-186">在 [hello**選擇磁碟類型] 頁面上**，設定與虛擬硬碟類型**動態擴充**（建議選項）。</span><span class="sxs-lookup"><span data-stu-id="5a039-186">On hello **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span></span> <span data-ttu-id="5a039-187">**固定大小**磁碟運作，但您可能需要 toowait 很長的時間。</span><span class="sxs-lookup"><span data-stu-id="5a039-187">**Fixed size** disk would work but you may need toowait a long time.</span></span> <span data-ttu-id="5a039-188">我們建議您不要使用 hello **Differencing**選項。</span><span class="sxs-lookup"><span data-stu-id="5a039-188">We recommend that you do not use hello **Differencing** option.</span></span> <span data-ttu-id="5a039-189">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5a039-189">Click **Next**.</span></span> <span data-ttu-id="5a039-190">在 Windows Server 2012 R2 和 Windows Server 2012，**動態擴充**是 hello 預設選項，而在 Windows Server 2008 R2，hello 預設為**固定大小**。</span><span class="sxs-lookup"><span data-stu-id="5a039-190">In Windows Server 2012 R2 and Windows Server 2012, **Dynamically expanding** is hello default option whereas in Windows Server 2008 R2, hello default is **Fixed size**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. <span data-ttu-id="5a039-191">在 hello**指定名稱和位置**頁面上，提供**名稱**以及**位置**（您可以瀏覽 tooone） hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="5a039-191">On hello **Specify Name and Location** page, provide a **name** as well as **location** (you can browse tooone) for hello data disk.</span></span> <span data-ttu-id="5a039-192">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5a039-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. <span data-ttu-id="5a039-193">在 hello**設定磁碟**頁面上，選取 hello 選項**建立新的空白虛擬硬碟磁碟**，並指定做為 hello 大小**500 GB** （或以上）。</span><span class="sxs-lookup"><span data-stu-id="5a039-193">On hello **Configure Disk** page, select hello option **Create a new blank virtual hard disk** and specify hello size as **500 GB** (or more).</span></span> <span data-ttu-id="5a039-194">Hello 最低需求 500 GB 時，一律可以佈建較大的磁碟。</span><span class="sxs-lookup"><span data-stu-id="5a039-194">While 500 GB is hello minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="5a039-195">請注意，您無法擴充或縮減 hello 磁碟一次佈建。</span><span class="sxs-lookup"><span data-stu-id="5a039-195">Note that you cannot expand or shrink hello disk once provisioned.</span></span> <span data-ttu-id="5a039-196">如需 hello 大小磁碟 tooprovision 的詳細資訊，檢閱 hello hello 調整大小 > 一節[最佳做法文件](storsimple-ova-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="5a039-196">For more information on hello size of disk tooprovision, review hello sizing section in hello [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="5a039-197">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5a039-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. <span data-ttu-id="5a039-198">在 hello**摘要**頁面上，檢閱您的虛擬資料磁碟的 hello 詳細資料，按一下 如果符合，**完成**toocreate hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="5a039-198">On hello **Summary** page, review hello details of your virtual data disk and if satisfied, click **Finish** toocreate hello disk.</span></span> <span data-ttu-id="5a039-199">hello 精靈關閉，而加入 tooyour 機器的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="5a039-199">hello wizard closes and a virtual hard disk is added tooyour machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. <span data-ttu-id="5a039-200">傳回 toohello**設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="5a039-200">Return toohello **Settings** page.</span></span> <span data-ttu-id="5a039-201">按一下**確定**tooclose hello**設定**頁面上，並傳回 tooHyper HYPER-V 管理員 視窗。</span><span class="sxs-lookup"><span data-stu-id="5a039-201">Click **OK** tooclose hello **Settings** page and return tooHyper-V Manager window.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a><span data-ttu-id="5a039-202">步驟 3： 啟動 hello 虛擬陣列，並取得 hello IP</span><span class="sxs-lookup"><span data-stu-id="5a039-202">Step 3: Start hello virtual array and get hello IP</span></span>
<span data-ttu-id="5a039-203">執行下列步驟 toostart hello 虛擬陣列，並連接 tooit。</span><span class="sxs-lookup"><span data-stu-id="5a039-203">Perform hello following steps toostart your virtual array and connect tooit.</span></span>

#### <a name="toostart-hello-virtual-array"></a><span data-ttu-id="5a039-204">toostart hello 虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="5a039-204">toostart hello virtual array</span></span>
1. <span data-ttu-id="5a039-205">啟動 hello 虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="5a039-205">Start hello virtual array.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. <span data-ttu-id="5a039-206">Hello 裝置正在執行之後，請選取裝置 hello、 以滑鼠右鍵按一下，然後選取**連接**。</span><span class="sxs-lookup"><span data-stu-id="5a039-206">After hello device is running, select hello device, right click, and select **Connect**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. <span data-ttu-id="5a039-207">您可能必須 toowait 5-10 分鐘讓裝置 hello toobe，準備好。</span><span class="sxs-lookup"><span data-stu-id="5a039-207">You may have toowait 5-10 minutes for hello device toobe ready.</span></span> <span data-ttu-id="5a039-208">狀態訊息會顯示 hello 主控台 tooindicate hello 進度。</span><span class="sxs-lookup"><span data-stu-id="5a039-208">A status message is displayed on hello console tooindicate hello progress.</span></span> <span data-ttu-id="5a039-209">Hello 裝置已經備妥之後，請繼續太**動作**。</span><span class="sxs-lookup"><span data-stu-id="5a039-209">After hello device is ready, go too**Action**.</span></span> <span data-ttu-id="5a039-210">按`Ctrl + Alt + Delete`toolog toohello 虛擬陣列中的。</span><span class="sxs-lookup"><span data-stu-id="5a039-210">Press `Ctrl + Alt + Delete` toolog in toohello virtual array.</span></span> <span data-ttu-id="5a039-211">hello 預設使用者為*StorSimpleAdmin* hello 預設密碼為*Password1*。</span><span class="sxs-lookup"><span data-stu-id="5a039-211">hello default user is *StorSimpleAdmin* and hello default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. <span data-ttu-id="5a039-212">基於安全性理由，hello 裝置系統管理員密碼到期 hello 第一次登入時。</span><span class="sxs-lookup"><span data-stu-id="5a039-212">For security reasons, hello device administrator password expires at hello first logon.</span></span> <span data-ttu-id="5a039-213">您已提示的 toochange hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="5a039-213">You are prompted toochange hello password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   <span data-ttu-id="5a039-214">請輸入至少包含 8 個字元的密碼。</span><span class="sxs-lookup"><span data-stu-id="5a039-214">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="5a039-215">hello 密碼必須符合至少下列 4 個需求的 hello 超出 3： 大寫字母、 小寫、 數字及特殊字元。</span><span class="sxs-lookup"><span data-stu-id="5a039-215">hello password must satisfy at least 3 out of hello following 4 requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="5a039-216">重新輸入 hello 密碼 tooconfirm 它。</span><span class="sxs-lookup"><span data-stu-id="5a039-216">Reenter hello password tooconfirm it.</span></span> <span data-ttu-id="5a039-217">會通知您該 hello 密碼已變更。</span><span class="sxs-lookup"><span data-stu-id="5a039-217">You are notified that hello password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. <span data-ttu-id="5a039-218">已成功變更 hello 密碼之後，可能會重新啟動 hello 虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="5a039-218">After hello password is successfully changed, hello virtual array may restart.</span></span> <span data-ttu-id="5a039-219">等候 hello 裝置 toostart。</span><span class="sxs-lookup"><span data-stu-id="5a039-219">Wait for hello device toostart.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    <span data-ttu-id="5a039-220">hello 的 hello 裝置的 Windows PowerShell 主控台會顯示進度列並。</span><span class="sxs-lookup"><span data-stu-id="5a039-220">hello Windows PowerShell console of hello device is displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. <span data-ttu-id="5a039-221">步驟 6 至 8 僅適用於在非 DHCP 環境中開機的情況。</span><span class="sxs-lookup"><span data-stu-id="5a039-221">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="5a039-222">如果您是在 DHCP 環境，然後略過這些步驟，並移 toostep 9。</span><span class="sxs-lookup"><span data-stu-id="5a039-222">If you are in a DHCP environment, then skip these steps and go toostep 9.</span></span> <span data-ttu-id="5a039-223">如果您已啟動您的裝置，在非 DHCP 環境中，您會看到下列畫面 hello。</span><span class="sxs-lookup"><span data-stu-id="5a039-223">If you booted up your device in non-DHCP environment, you will see hello following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    <span data-ttu-id="5a039-224">接著，設定 hello 網路。</span><span class="sxs-lookup"><span data-stu-id="5a039-224">Next, configure hello network.</span></span>
7. <span data-ttu-id="5a039-225">使用 hello`Get-HcsIpAddress`命令在您的虛擬陣列上啟用 toolist hello 網路介面。</span><span class="sxs-lookup"><span data-stu-id="5a039-225">Use hello `Get-HcsIpAddress` command toolist hello network interfaces enabled on your virtual array.</span></span> <span data-ttu-id="5a039-226">如果您的裝置具有單一網路介面啟用，hello 預設指派名稱 toothis 介面是`Ethernet`。</span><span class="sxs-lookup"><span data-stu-id="5a039-226">If your device has a single network interface enabled, hello default name assigned toothis interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. <span data-ttu-id="5a039-227">使用 hello `Set-HcsIpAddress` cmdlet tooconfigure hello 網路。</span><span class="sxs-lookup"><span data-stu-id="5a039-227">Use hello `Set-HcsIpAddress` cmdlet tooconfigure hello network.</span></span> <span data-ttu-id="5a039-228">請參閱下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a039-228">See hello following example:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. <span data-ttu-id="5a039-229">Hello 初始設定完成後，已開機 hello 裝置之後，您會看到 hello 裝置橫幅文字。</span><span class="sxs-lookup"><span data-stu-id="5a039-229">After hello initial setup is complete and hello device has booted up, you will see hello device banner text.</span></span> <span data-ttu-id="5a039-230">請記下 hello IP 位址，然後顯示 hello 橫幅文字 toomanage hello 裝置中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="5a039-230">Make a note of hello IP address and hello URL displayed in hello banner text toomanage hello device.</span></span> <span data-ttu-id="5a039-231">使用此 IP 位址 tooconnect toohello web UI，您的虛擬陣列和 hello 完成本機安裝及註冊。</span><span class="sxs-lookup"><span data-stu-id="5a039-231">Use this IP address tooconnect toohello web UI of your virtual array and complete hello local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. <span data-ttu-id="5a039-232">（選擇性）只有當您要部署您的裝置 hello 政府雲端中執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="5a039-232">(Optional) Perform this step only if you are deploying your device in hello Government Cloud.</span></span> <span data-ttu-id="5a039-233">您現在將在您的裝置上啟用 hello 美國聯邦資訊處理標準 (FIPS) 模式。</span><span class="sxs-lookup"><span data-stu-id="5a039-233">You will now enable hello United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="5a039-234">hello FIPS 140 標準會定義核准 hello 保護機密資料的美國聯邦政府電腦系統所使用的密碼編譯演算法。</span><span class="sxs-lookup"><span data-stu-id="5a039-234">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span>

    1. <span data-ttu-id="5a039-235">tooenable hello FIPS 模式中，執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a039-235">tooenable hello FIPS mode, run hello following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="5a039-236">重新啟動您的裝置之後您已經啟用 hello FIPS 模式，以便 hello 密碼編譯的驗證才會生效。</span><span class="sxs-lookup"><span data-stu-id="5a039-236">Reboot your device after you have enabled hello FIPS mode so that hello cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="5a039-237">您可以在您的裝置上啟用或停用 FIPS 模式。</span><span class="sxs-lookup"><span data-stu-id="5a039-237">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="5a039-238">不支援 FIPS 和非 FIPS 模式之間交替 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="5a039-238">Alternating hello device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="5a039-239">如果您的裝置不符合 hello 最低設定需求，您會看到下列錯誤 hello 橫幅文字 （如下所示） 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="5a039-239">If your device does not meet hello minimum configuration requirements, you see hello following error in hello banner text (shown below).</span></span> <span data-ttu-id="5a039-240">修改 hello 裝置設定，使 hello 機器有足夠的資源 toomeet hello 最低需求。</span><span class="sxs-lookup"><span data-stu-id="5a039-240">Modify hello device configuration so that hello machine has adequate resources toomeet hello minimum requirements.</span></span> <span data-ttu-id="5a039-241">然後，您可以重新啟動，並連接 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="5a039-241">You can then restart and connect toohello device.</span></span> <span data-ttu-id="5a039-242">在 toohello 最低設定需求，請參閱[步驟 1： 確定 hello 主機系統符合最低虛擬陣列需求](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements)。</span><span class="sxs-lookup"><span data-stu-id="5a039-242">Refer toohello minimum configuration requirements in [Step 1: Ensure that hello host system meets minimum virtual array requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

<span data-ttu-id="5a039-243">如果您使用 hello 本機 web UI 的 hello 初始設定期間所面對任何其他錯誤，請參閱 toohello 下列工作流程：</span><span class="sxs-lookup"><span data-stu-id="5a039-243">If you face any other error during hello initial configuration using hello local web UI, refer toohello following workflows:</span></span>

* <span data-ttu-id="5a039-244">也會執行診斷測試[疑難排解 web UI 安裝](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors)。</span><span class="sxs-lookup"><span data-stu-id="5a039-244">Run diagnostic tests too[troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="5a039-245">[產生記錄檔封裝及檢視記錄檔](storsimple-ova-web-ui-admin.md#generate-a-log-package)。</span><span class="sxs-lookup"><span data-stu-id="5a039-245">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a039-246">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a039-246">Next steps</span></span>
* [<span data-ttu-id="5a039-247">Set up your StorSimple Virtual Array as a file server (將 StorSimple 虛擬陣列設定為檔案伺服器)</span><span class="sxs-lookup"><span data-stu-id="5a039-247">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="5a039-248">Set up your StorSimple Virtual Array as an iSCSI server (將 StorSimple 虛擬陣列設定為 iSCSI 伺服器)</span><span class="sxs-lookup"><span data-stu-id="5a039-248">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)
