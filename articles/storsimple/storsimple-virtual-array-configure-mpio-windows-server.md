---
title: "設定連接至 StorSimple Virtual Array 之主機上的 MPIO | Microsoft Docs"
description: "說明如何針對與執行 Windows Server 2012 R2 的主機連接的 StorSimple Virtual Array 設定多重路徑 I/O (MPIO)。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: c75c6ed40754aee964e2b68f4f569dc1422507f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-the-storsimple-virtual-array"></a><span data-ttu-id="e6d72-103">在 Windows Server 主機上設定 StorSimple Virtual Array 的多重路徑 I/O</span><span class="sxs-lookup"><span data-stu-id="e6d72-103">Configure Multipath I/O on Windows Server host for the StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="e6d72-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e6d72-104">Overview</span></span>
<span data-ttu-id="e6d72-105">本文說明如何在 Windows Server 主機上安裝多重路徑 I/O 功能 (MPIO)，套用僅限 StorSimple 磁碟區的特定組態設定，然後確認 StorSimple 磁碟區的 MPIO。</span><span class="sxs-lookup"><span data-stu-id="e6d72-105">This article describes how to install Multipath I/O feature (MPIO) on your Windows Server host, apply specific configuration settings for StorSimple-only volumes, and then verify MPIO for StorSimple volumes.</span></span> <span data-ttu-id="e6d72-106">此程序假設具有兩個網路介面的 StorSimple 1200 Virtual Array 連接至具有兩個網路介面的 Windows Server 主機。</span><span class="sxs-lookup"><span data-stu-id="e6d72-106">The procedure assumes that your StorSimple 1200 Virtual Array with two network interfaces is connected to a Windows Server host with two network interfaces.</span></span> <span data-ttu-id="e6d72-107">本文中所包含的資訊僅適用於虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="e6d72-107">The information contained in this article applies only to the virtual array.</span></span> <span data-ttu-id="e6d72-108">如需 StorSimple 8000 系列裝置的資訊，請移至 [設定 StorSimple 主機的 MPIO](storsimple-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="e6d72-108">For information on StorSimple 8000 series devices, go to [Configure MPIO for StorSimple host](storsimple-configure-mpio-windows-server.md).</span></span> 

<span data-ttu-id="e6d72-109">Windows Server 中的 MPIO 功能可協助建置高可用性、容錯的儲存體組態。</span><span class="sxs-lookup"><span data-stu-id="e6d72-109">The MPIO feature in Windows Server helps build highly available, fault-tolerant storage configurations.</span></span> <span data-ttu-id="e6d72-110">MPIO 使用備援實體路徑元件 — 配接器、纜線以及交換器 — 以在伺服器與存放裝置之間建立邏輯路徑。</span><span class="sxs-lookup"><span data-stu-id="e6d72-110">MPIO uses redundant physical path components — adapters, cables, and switches — to create logical paths between the server and the storage device.</span></span> <span data-ttu-id="e6d72-111">如果元件故障而導致邏輯路徑失敗，多重路徑邏輯使用替代的 I/O 路徑，讓應用程式仍然可以存取其資料。</span><span class="sxs-lookup"><span data-stu-id="e6d72-111">If there is a component failure, causing a logical path to fail, multipathing logic uses an alternate path for I/O so that applications can still access their data.</span></span> <span data-ttu-id="e6d72-112">此外，依照您的設定，MPIO 也能藉由重新平衡所有路徑的負載來改善效能。</span><span class="sxs-lookup"><span data-stu-id="e6d72-112">Additionally depending on your configuration, MPIO can also improve performance by re-balancing the load across all these paths.</span></span> <span data-ttu-id="e6d72-113">如需詳細資訊，請參閱 [MPIO 概觀](https://technet.microsoft.com/library/cc725907.aspx "MPIO 概觀 and features")。</span><span class="sxs-lookup"><span data-stu-id="e6d72-113">For more information, see [MPIO overview](https://technet.microsoft.com/library/cc725907.aspx "MPIO overview and features").</span></span>

<span data-ttu-id="e6d72-114">為了讓 StorSimple 解決方案發揮高可用性，請在連接至 StorSimple Virtual Array (型號 1200) 的 Windows Server 主機上設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="e6d72-114">For the high-availability of your StorSimple solution, configure MPIO on the Windows Server hosts connected to your StorSimple Virtual Array (model 1200).</span></span> <span data-ttu-id="e6d72-115">主機伺服器隨即可容許連結、網路或介面失敗。</span><span class="sxs-lookup"><span data-stu-id="e6d72-115">The host servers can then tolerate a link, network, or interface failure.</span></span> 

<span data-ttu-id="e6d72-116">您必須依照下列步驟設定 MPIO：</span><span class="sxs-lookup"><span data-stu-id="e6d72-116">You will need to follow these steps to configure MPIO:</span></span> 

* <span data-ttu-id="e6d72-117">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="e6d72-117">Configuration prerequisites</span></span>
* <span data-ttu-id="e6d72-118">步驟 1：在 Windows Server 主機上安裝 MPIO</span><span class="sxs-lookup"><span data-stu-id="e6d72-118">Step 1: Install MPIO on the Windows Server host</span></span>
* <span data-ttu-id="e6d72-119">步驟 2：為 StorSimple 磁碟區設定 MPIO </span><span class="sxs-lookup"><span data-stu-id="e6d72-119">Step 2: Configure MPIO for StorSimple volumes</span></span>
* <span data-ttu-id="e6d72-120">步驟 3：在主機上掛接 StorSimple 磁碟區</span><span class="sxs-lookup"><span data-stu-id="e6d72-120">Step 3: Mount StorSimple volumes on the host</span></span>

<span data-ttu-id="e6d72-121">上述步驟會在下列各節討論。</span><span class="sxs-lookup"><span data-stu-id="e6d72-121">Each of the above steps is discussed in the following sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6d72-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="e6d72-122">Prerequisites</span></span>
<span data-ttu-id="e6d72-123">本節將詳細說明 Windows Server 主機和虛擬陣列的組態必要條件。</span><span class="sxs-lookup"><span data-stu-id="e6d72-123">This section details the configuration prerequisites for the Windows Server host and your virtual array.</span></span>

### <a name="on-windows-server-host"></a><span data-ttu-id="e6d72-124">在 Windows Server 主機上</span><span class="sxs-lookup"><span data-stu-id="e6d72-124">On Windows Server host</span></span>
* <span data-ttu-id="e6d72-125">確定 Windows Server 主機已啟用 2 個網路介面。</span><span class="sxs-lookup"><span data-stu-id="e6d72-125">Make sure that your Windows Server host has 2 network interfaces enabled.</span></span>

### <a name="on-storsimple-virtual-array"></a><span data-ttu-id="e6d72-126">在 StorSimple Virtual Array 上</span><span class="sxs-lookup"><span data-stu-id="e6d72-126">On StorSimple Virtual Array</span></span>
* <span data-ttu-id="e6d72-127">虛擬陣列應該設定為 iSCSI 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6d72-127">The virtual array should be configured as an iSCSI server.</span></span> <span data-ttu-id="e6d72-128">若要深入了解，請參閱[將虛擬陣列設定為 iSCSI 伺服器](storsimple-virtual-array-deploy3-iscsi-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="e6d72-128">To learn more, see [set up virtual array as an iSCSI server](storsimple-virtual-array-deploy3-iscsi-setup.md).</span></span> <span data-ttu-id="e6d72-129">應該在陣列上啟用一或多個網路介面。</span><span class="sxs-lookup"><span data-stu-id="e6d72-129">One or more network interfaces should be enabled on the array.</span></span>   
* <span data-ttu-id="e6d72-130">虛擬陣列上的網路介面應該可從 Windows Server 主機觸達。</span><span class="sxs-lookup"><span data-stu-id="e6d72-130">The network interfaces on your virtual array should be reachable from the Windows Server host.</span></span>
* <span data-ttu-id="e6d72-131">應該在 StorSimple Virtual Array 上建立一或多個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e6d72-131">One or more volumes should be created on your StorSimple Virtual Array.</span></span> <span data-ttu-id="e6d72-132">若要深入了解，請參閱在 StorSimple Virtual Array 上[新增磁碟區](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)。</span><span class="sxs-lookup"><span data-stu-id="e6d72-132">To learn more, see [Add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) on your StorSimple Virtual Array.</span></span> <span data-ttu-id="e6d72-133">在此程序中，我們在虛擬陣列上建立 3 個磁碟區 (1 個固定在本機的磁碟區，2 個階層式磁碟區，如下所示)。</span><span class="sxs-lookup"><span data-stu-id="e6d72-133">In this procedure, we created 3 volumes (1 locally pinned and 2 tiered volumes as shown below) on the virtual array.</span></span>
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a><span data-ttu-id="e6d72-135">StorSimple Virtual Array 的硬體設定</span><span class="sxs-lookup"><span data-stu-id="e6d72-135">Hardware configuration for StorSimple Virtual Array</span></span>
<span data-ttu-id="e6d72-136">下圖顯示讓此程序中使用的 Windows Server 主機和 StorSimple Virtual Array 達到高可用性和平衡負載多重路徑的硬體設定。</span><span class="sxs-lookup"><span data-stu-id="e6d72-136">The figure below shows the hardware configuration for high availability and load-balancing multipathing for your Windows Server host and StorSimple Virtual Array used in this procedure.</span></span>

![mpio 硬體組態](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

<span data-ttu-id="e6d72-138">如上圖所示：</span><span class="sxs-lookup"><span data-stu-id="e6d72-138">As shown in the preceding figure:</span></span>

* <span data-ttu-id="e6d72-139">在 Hyper-V 上佈建的 StorSimple Virtual Array 是設定為 iSCSI 伺服器的單一節點作用中裝置。</span><span class="sxs-lookup"><span data-stu-id="e6d72-139">Your StorSimple Virtual Array provisioned on Hyper-V is a single node active device configured as an iSCSI server.</span></span>
* <span data-ttu-id="e6d72-140">陣列上已啟用兩個虛擬網路介面。</span><span class="sxs-lookup"><span data-stu-id="e6d72-140">Two virtual network interfaces are enabled on your array.</span></span> <span data-ttu-id="e6d72-141">在虛擬陣列的本機 Web UI 中，瀏覽至 [網路設定] 來確認已啟用兩個網路介面，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e6d72-141">In the local web UI of your virtual array, verify that two network interfaces are enabled by navigating to **Network Settings** as shown below:</span></span>
  
    ![在 1200 上啟用的網路介面](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    <span data-ttu-id="e6d72-143">請記下啟用之網路介面 (乙太網路，預設為乙太網路 2) 的 IPv4 位址，並加以儲存供稍後在主機上使用。</span><span class="sxs-lookup"><span data-stu-id="e6d72-143">Note the IPv4 addresses of the enabled network interfaces (Ethernet, Ethernet 2 by default) and save for later use on the host.</span></span>
* <span data-ttu-id="e6d72-144">Windows Server 主機已啟用 2 個網路介面。</span><span class="sxs-lookup"><span data-stu-id="e6d72-144">Two network interfaces are enabled on your Windows Server host.</span></span> <span data-ttu-id="e6d72-145">如果主機和陣列的連接介面位於相同的子網路上，將會有 4 個路徑可用。</span><span class="sxs-lookup"><span data-stu-id="e6d72-145">If the connected interfaces for host and array are on the same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="e6d72-146">在此程序中是這個情況。</span><span class="sxs-lookup"><span data-stu-id="e6d72-146">This was the case in this procedure.</span></span> <span data-ttu-id="e6d72-147">不過，如果陣列和主機介面上的每個網路介面位於不同的 IP 子網路上 (且不可路由傳送)，則只有 2 個路徑可用。</span><span class="sxs-lookup"><span data-stu-id="e6d72-147">However, if each network interface on the array and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span>

## <a name="step-1-install-mpio-on-the-windows-server-host"></a><span data-ttu-id="e6d72-148">步驟 1：在 Windows Server 主機上安裝 MPIO</span><span class="sxs-lookup"><span data-stu-id="e6d72-148">Step 1: Install MPIO on the Windows Server host</span></span>
<span data-ttu-id="e6d72-149">MPIO 是 Windows 伺服器預設不會安裝的選擇性功能。</span><span class="sxs-lookup"><span data-stu-id="e6d72-149">MPIO is an optional feature on Windows Server and is not installed by default.</span></span> <span data-ttu-id="e6d72-150">您應該透過伺服器管理員將它安裝為功能。</span><span class="sxs-lookup"><span data-stu-id="e6d72-150">It should be installed as a feature through Server Manager.</span></span> <span data-ttu-id="e6d72-151">若要在 Windows Server 主機上安裝這項功能，請完成下列程序。</span><span class="sxs-lookup"><span data-stu-id="e6d72-151">To install this feature on your Windows Server host, complete the following procedure.</span></span>

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a><span data-ttu-id="e6d72-152">步驟 2：為 StorSimple 磁碟區設定 MPIO </span><span class="sxs-lookup"><span data-stu-id="e6d72-152">Step 2: Configure MPIO for StorSimple volumes</span></span>
<span data-ttu-id="e6d72-153">您必須設定 MPIO 才能識別 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e6d72-153">MPIO needs to be configured to identify StorSimple volumes.</span></span> <span data-ttu-id="e6d72-154">若要設定 MPIO 以辨識 StorSimple 磁碟區，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="e6d72-154">To configure MPIO to recognize StorSimple volumes, perform the following steps.</span></span>

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-the-host"></a><span data-ttu-id="e6d72-155">步驟 3：在主機上掛接 StorSimple 磁碟區</span><span class="sxs-lookup"><span data-stu-id="e6d72-155">Step 3: Mount StorSimple volumes on the host</span></span>
<span data-ttu-id="e6d72-156">在 Windows 伺服器上設定 MPIO 之後，就能掛接在 StorSimple 陣列上建立的磁碟區，並可以利用 MPIO 獲得備援。</span><span class="sxs-lookup"><span data-stu-id="e6d72-156">After MPIO is configured on Windows Server, volume(s) created on the StorSimple array can be mounted and can then take advantage of MPIO for redundancy.</span></span> <span data-ttu-id="e6d72-157">若要掛接磁碟區，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="e6d72-157">To mount a volume, perform the following steps.</span></span>

#### <a name="to-mount-volumes-on-the-host"></a><span data-ttu-id="e6d72-158">若要在主機上掛接磁碟區</span><span class="sxs-lookup"><span data-stu-id="e6d72-158">To mount volumes on the host</span></span>
1. <span data-ttu-id="e6d72-159">在 Windows Server 主機上，開啟 [iSCSI 啟動器內容]  視窗。</span><span class="sxs-lookup"><span data-stu-id="e6d72-159">Open the **iSCSI Initiator Properties** window on the Windows Server host.</span></span> <span data-ttu-id="e6d72-160">移至 [伺服器管理員] > [儀表板] > [工具] > [iSCSI 啟動器]。</span><span class="sxs-lookup"><span data-stu-id="e6d72-160">Go to **Server Manager > Dashboard > Tools > iSCSI Initiator**.</span></span>
2. <span data-ttu-id="e6d72-161">在 [iSCSI 啟動器 - 內容] 對話方塊中，按一下 [探索]，然後按一下 [搜尋目標入口]。</span><span class="sxs-lookup"><span data-stu-id="e6d72-161">In the **iSCSI Initiator Properties** dialog box, click **Discovery**, and then click **Discover Target Portal**.</span></span>
3. <span data-ttu-id="e6d72-162">在 [搜尋目標入口]  對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="e6d72-162">In the **Discover Target Portal** dialog box, do the following:</span></span>
   
    1. <span data-ttu-id="e6d72-163">輸入 StorSimple Virtual Array 上第一個啟用的網路介面的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e6d72-163">Enter the IP address of the first enabled network interface on your StorSimple Virtual Array.</span></span> <span data-ttu-id="e6d72-164">根據預設，這會是 **乙太網路**。</span><span class="sxs-lookup"><span data-stu-id="e6d72-164">By default, this would be **Ethernet**.</span></span> 
    2. <span data-ttu-id="e6d72-165">按一下 [確定] 以返回 [iSCSI 啟動器內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e6d72-165">Click **OK** to return to the **iSCSI Initiator Properties** dialog box.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="e6d72-166">如果您使用私人網路進行 iSCSI 連線，請輸入連線到私人網路的 DATA 連接埠 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e6d72-166">If you are using a private network for iSCSI connections, enter the IP address of the DATA port that is connected to the private network.</span></span>
     
4. <span data-ttu-id="e6d72-167">在陣列上針對第二個網路介面 (例如，乙太網路 2) 重複步驟 2-3 。</span><span class="sxs-lookup"><span data-stu-id="e6d72-167">Repeat steps 2-3 for a second network interface (for example, Ethernet 2) on your array.</span></span> 
5. <span data-ttu-id="e6d72-168">在 [iSCSI 啟動器內容] 對話方塊中，選取 [目標] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e6d72-168">Select the **Targets** tab in the **iSCSI Initiator Properties** dialog box.</span></span> <span data-ttu-id="e6d72-169">針對虛擬陣列，您應該將每個磁碟區表面視為**探索到的目標**之下的目標。</span><span class="sxs-lookup"><span data-stu-id="e6d72-169">For your virtual array, you should see each volume surface as a target under **Discovered Targets**.</span></span> <span data-ttu-id="e6d72-170">在此情況下，會發現三個目標 (對應到三個磁碟區)。</span><span class="sxs-lookup"><span data-stu-id="e6d72-170">In this case, three targets (corresponding to three volumes) would be discovered.</span></span>
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. <span data-ttu-id="e6d72-172">按一下 [連接]，與您的 StorSimple Virtual Array 建立 iSCSI 工作階段。</span><span class="sxs-lookup"><span data-stu-id="e6d72-172">Click **Connect** to establish an iSCSI session with your StorSimple Virtual Array.</span></span> <span data-ttu-id="e6d72-173">[連線到目標]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="e6d72-173">A **Connect to Target** dialog box will appear.</span></span> <span data-ttu-id="e6d72-174">選取 [啟用多重路徑]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e6d72-174">Select the **Enable multi-path** check box.</span></span> <span data-ttu-id="e6d72-175">按一下 [進階] 。</span><span class="sxs-lookup"><span data-stu-id="e6d72-175">Click **Advanced**.</span></span>
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. <span data-ttu-id="e6d72-177">在 [進階設定]  對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="e6d72-177">In the **Advanced Settings** dialog box, do the following:</span></span>                                        
   
    1. <span data-ttu-id="e6d72-178">在 [本機介面卡] 下拉式清單中，選取 [Microsoft iSCSI 啟動器]。</span><span class="sxs-lookup"><span data-stu-id="e6d72-178">On the **Local Adapter** drop-down list, select **Microsoft iSCSI Initiator**.</span></span>
    2. <span data-ttu-id="e6d72-179">在 [啟動器 IP]  下拉式清單中，選取主機的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e6d72-179">On the **Initiator IP** drop-down list, select the IP address of the host.</span></span>
    3. <span data-ttu-id="e6d72-180">在 [目標入口 IP]  下拉式清單中，選取陣列介面的 IP。</span><span class="sxs-lookup"><span data-stu-id="e6d72-180">On the **Target Portal** IP drop-down list, select the IP of array interface.</span></span>
    4. <span data-ttu-id="e6d72-181">按一下 [確定] 以返回 [iSCSI 啟動器內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e6d72-181">Click **OK** to return to the **iSCSI Initiator Properties** dialog box.</span></span>
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. <span data-ttu-id="e6d72-183">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="e6d72-183">Click **Properties**.</span></span> 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. <span data-ttu-id="e6d72-185">在 [內容] 對話方塊中，按一下 [新增工作階段]。</span><span class="sxs-lookup"><span data-stu-id="e6d72-185">In the **Properties** dialog box, click **Add Session**.</span></span>
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. <span data-ttu-id="e6d72-187">在 [連線到目標] 對話方塊中，選取 [啟用多重路徑] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e6d72-187">In the **Connect to Target** dialog box, select the **Enable multi-path** check box.</span></span> <span data-ttu-id="e6d72-188">按一下 [進階] 。</span><span class="sxs-lookup"><span data-stu-id="e6d72-188">Click **Advanced**.</span></span>
11. <span data-ttu-id="e6d72-189">在 [進階設定]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="e6d72-189">In the **Advanced Settings** dialog box:</span></span>                                        
    
    1. <span data-ttu-id="e6d72-190">在 [本機介面卡]  下拉式清單中，選取 [Microsoft iSCSI 啟動器]。</span><span class="sxs-lookup"><span data-stu-id="e6d72-190">On the **Local adapter** drop-down list, select Microsoft iSCSI Initiator.</span></span>

    2. <span data-ttu-id="e6d72-191">在 [啟動器 IP]  下拉式清單中，選取對應到主機的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e6d72-191">On the **Initiator IP** drop-down list, select the IP address corresponding to the host.</span></span> <span data-ttu-id="e6d72-192">在此情況下，您會將陣列上的兩個網路介面連線到主機上的單一網路介面。</span><span class="sxs-lookup"><span data-stu-id="e6d72-192">In this case, you are connecting two network interfaces on the array to a single network interface on the host.</span></span> <span data-ttu-id="e6d72-193">因此，這個介面會和第一個工作階段提供的相同。</span><span class="sxs-lookup"><span data-stu-id="e6d72-193">Therefore, this interface is the same as that provided for the first session.</span></span>

    3. <span data-ttu-id="e6d72-194">在 [目標入口 IP]  下拉式清單中，為陣列上啟用的第二個資料介面選取 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e6d72-194">On the **Target Portal IP** drop-down list, select the IP address for the second data interface enabled on the array.</span></span>

    4. <span data-ttu-id="e6d72-195">按一下 [確定]  以返回 [iSCSI 啟動器內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e6d72-195">Click **OK** to return to the iSCSI Initiator Properties dialog box.</span></span> <span data-ttu-id="e6d72-196">您完成將第二個工作階段新增到目標。</span><span class="sxs-lookup"><span data-stu-id="e6d72-196">You have added a second session to the target.</span></span>
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. <span data-ttu-id="e6d72-198">在新增所需的工作階段 (路徑) 之後，請在 [iSCSI 啟動器內容] 對話方塊中，選取目標，然後按一下 [內容]。</span><span class="sxs-lookup"><span data-stu-id="e6d72-198">After adding the desired sessions (paths), in the **iSCSI Initiator Properties** dialog box, select the target and click **Properties**.</span></span> <span data-ttu-id="e6d72-199">在 [內容]  對話方塊的 [工作階段] 索引標籤中，針對可能的路徑排列組合記下其對應的四個工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="e6d72-199">On the Sessions tab of the **Properties** dialog box, note the four session identifiers that correspond to the possible path permutations.</span></span> <span data-ttu-id="e6d72-200">若要取消工作階段，請選取工作階段識別碼旁邊的核取方塊，然後按一下 [中斷連線] 。</span><span class="sxs-lookup"><span data-stu-id="e6d72-200">To cancel a session, select the check box next to a session identifier, and then click **Disconnect**.</span></span>

    6. <span data-ttu-id="e6d72-201">若要檢視工作階段內顯示的裝置，請選取 [裝置]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e6d72-201">To view devices presented within sessions, select the **Devices** tab.</span></span> <span data-ttu-id="e6d72-202">若要為選取的裝置設定 MPIO 原則，請按一下 [MPIO] 。</span><span class="sxs-lookup"><span data-stu-id="e6d72-202">To configure the MPIO policy for a selected device, click **MPIO**.</span></span>

    7. <span data-ttu-id="e6d72-203">[詳細資料] 對話方塊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="e6d72-203">The **Details** dialog box will appear.</span></span> <span data-ttu-id="e6d72-204">在 [MPIO] 索引標籤上，您可以選取適當 [負載平衡原則] 設定。</span><span class="sxs-lookup"><span data-stu-id="e6d72-204">On the **MPIO** tab, you can select the appropriate **Load Balance Policy** settings.</span></span> <span data-ttu-id="e6d72-205">您也可以檢視 [使用中] 或 [待命] 路徑類型。</span><span class="sxs-lookup"><span data-stu-id="e6d72-205">You can also view the **Active** or **Standby** path type.</span></span>
12. <span data-ttu-id="e6d72-206">重複步驟 8-11，將其他工作階段 (路徑) 新增到目標。</span><span class="sxs-lookup"><span data-stu-id="e6d72-206">Repeat steps 8-11 to add additional sessions (paths) to the target.</span></span> <span data-ttu-id="e6d72-207">主機上有兩個介面且虛擬陣列上也有兩個，您總共可以為每個目標新增四個工作階段。</span><span class="sxs-lookup"><span data-stu-id="e6d72-207">With two interfaces on the host and two on the virtual array, you can add a total of four sessions for each target.</span></span> 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. <span data-ttu-id="e6d72-209">您必須為每個磁碟區重複這些步驟 (表面做為目標)。</span><span class="sxs-lookup"><span data-stu-id="e6d72-209">You will need to repeat these steps for each volume (surfaces as a target).</span></span>
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. <span data-ttu-id="e6d72-211">藉由瀏覽至 [伺服器管理員] > [儀表板] > [電腦管理]，來開啟 [電腦管理]。</span><span class="sxs-lookup"><span data-stu-id="e6d72-211">Open **Computer Management** by navigating to **Server Manager > Dashboard > Computer Management**.</span></span> <span data-ttu-id="e6d72-212">在左窗格中，按一下 [存放裝置] > [磁碟管理]。</span><span class="sxs-lookup"><span data-stu-id="e6d72-212">In the left pane, click **Storage > Disk Management**.</span></span> <span data-ttu-id="e6d72-213">在 StorSimple Virtual Array 上建立且可讓此主機看見的磁碟區，在 [磁碟管理] 下會顯示為新磁碟。</span><span class="sxs-lookup"><span data-stu-id="e6d72-213">The volume(s) created on the StorSimple Virtual Array that are visible to this host will appear under **Disk Management** as new disk(s).</span></span>
15. <span data-ttu-id="e6d72-214">初始化磁碟，並建立新的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e6d72-214">Initialize the disk and create a new volume.</span></span> <span data-ttu-id="e6d72-215">在格式化程序期間，選取 64 KB 的配置單位大小 (AUS)。</span><span class="sxs-lookup"><span data-stu-id="e6d72-215">During the format process, select an allocation unit size (AUS) of 64 KB.</span></span> <span data-ttu-id="e6d72-216">對所有可用的磁碟區重複此程序。</span><span class="sxs-lookup"><span data-stu-id="e6d72-216">Repeat the process for all the available volumes.</span></span>
    
    ![磁碟管理](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. <span data-ttu-id="e6d72-218">在 [磁碟管理] 下，於 [磁碟] 按一下滑鼠右鍵，然後選取 [內容]。</span><span class="sxs-lookup"><span data-stu-id="e6d72-218">Under **Disk Management**, right-click the **Disk** and select **Properties**.</span></span>
17. <span data-ttu-id="e6d72-219">在 [多重路徑磁碟裝置內容] 對話方塊中，按一下 [MPIO] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e6d72-219">In the **Multi-Path Disk Device Properties** dialog box, click the **MPIO** tab.</span></span>
    
    ![磁碟屬性](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. <span data-ttu-id="e6d72-221">在 [DSM 名稱] 區段中，按一下 [詳細資料] 並確認參數已設定為預設參數。</span><span class="sxs-lookup"><span data-stu-id="e6d72-221">In the **DSM Name** section, click **Details** and verify that the parameters are set to the default parameters.</span></span> <span data-ttu-id="e6d72-222">預設參數如下：</span><span class="sxs-lookup"><span data-stu-id="e6d72-222">The default parameters are:</span></span>
    
    * <span data-ttu-id="e6d72-223">路徑確認期間 = 30</span><span class="sxs-lookup"><span data-stu-id="e6d72-223">Path Verify Period = 30</span></span>
    * <span data-ttu-id="e6d72-224">重試計數 = 3</span><span class="sxs-lookup"><span data-stu-id="e6d72-224">Retry Count = 3</span></span>
    * <span data-ttu-id="e6d72-225">PDO 移除期間 = 20</span><span class="sxs-lookup"><span data-stu-id="e6d72-225">PDO Remove Period = 20</span></span>
    * <span data-ttu-id="e6d72-226">重試間隔 = 1</span><span class="sxs-lookup"><span data-stu-id="e6d72-226">Retry Interval = 1</span></span>
    * <span data-ttu-id="e6d72-227">啟用路徑確認 = 未選取。</span><span class="sxs-lookup"><span data-stu-id="e6d72-227">Path Verify Enabled = Unchecked.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e6d72-228">**請不要修改預設的參數。**</span><span class="sxs-lookup"><span data-stu-id="e6d72-228">**Do not modify the default parameters.**</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="e6d72-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6d72-229">Next steps</span></span>
<span data-ttu-id="e6d72-230">深入了解[使用 StorSimple 裝置管理員服務管理 StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="e6d72-230">Learn more about [using the StorSimple Device Manager service to administer your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span>

