---
title: "主機上的 aaaConfigure MPIO 連接 tooStorSimple 虛擬陣列 |Microsoft 文件"
description: "描述如何 tooconfigure 多重路徑 I/O (MPIO) 為您的 StorSimple Virtual Array 連接 tooa 主機執行 Windows Server 2012 R2。"
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
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a><span data-ttu-id="cb2e6-103">Hello StorSimple Virtual Array 的 Windows Server 主機上設定多重路徑 I/O</span><span class="sxs-lookup"><span data-stu-id="cb2e6-103">Configure Multipath I/O on Windows Server host for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="cb2e6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="cb2e6-104">Overview</span></span>
<span data-ttu-id="cb2e6-105">本文說明如何在您的 Windows Server 主機上的 tooinstall 多重路徑 I/O 功能 (MPIO) 套用特定的組態設定，僅限 StorSimple 磁碟區，然後確認 MPIO StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-105">This article describes how tooinstall Multipath I/O feature (MPIO) on your Windows Server host, apply specific configuration settings for StorSimple-only volumes, and then verify MPIO for StorSimple volumes.</span></span> <span data-ttu-id="cb2e6-106">hello 程序假設您的 StorSimple 1200 虛擬陣列，具有兩個網路介面是兩個網路介面連接的 tooa Windows Server 主機。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-106">hello procedure assumes that your StorSimple 1200 Virtual Array with two network interfaces is connected tooa Windows Server host with two network interfaces.</span></span> <span data-ttu-id="cb2e6-107">本文中所包含的 hello 資訊適用於 toohello 虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-107">hello information contained in this article applies only toohello virtual array.</span></span> <span data-ttu-id="cb2e6-108">如需 StorSimple 8000 系列裝置的資訊，請移太[設定 MPIO StorSimple 主機](storsimple-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-108">For information on StorSimple 8000 series devices, go too[Configure MPIO for StorSimple host](storsimple-configure-mpio-windows-server.md).</span></span> 

<span data-ttu-id="cb2e6-109">在 Windows Server 可協助建置高可用性、 容錯儲存體設定中的 hello MPIO 功能。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-109">hello MPIO feature in Windows Server helps build highly available, fault-tolerant storage configurations.</span></span> <span data-ttu-id="cb2e6-110">MPIO 使用備援實體路徑元件，配接器、 纜線和交換器 — toocreate hello 伺服器與 hello 存放裝置之間的邏輯路徑。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-110">MPIO uses redundant physical path components — adapters, cables, and switches — toocreate logical paths between hello server and hello storage device.</span></span> <span data-ttu-id="cb2e6-111">如果沒有元件故障，造成邏輯路徑 toofail，則多重路徑邏輯會使用替代路徑 i/o，讓應用程式仍然可以存取其資料。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-111">If there is a component failure, causing a logical path toofail, multipathing logic uses an alternate path for I/O so that applications can still access their data.</span></span> <span data-ttu-id="cb2e6-112">此外根據您的設定 MPIO 也可以改善效能的重新平衡所有這些路徑中的 hello 負載。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-112">Additionally depending on your configuration, MPIO can also improve performance by re-balancing hello load across all these paths.</span></span> <span data-ttu-id="cb2e6-113">如需詳細資訊，請參閱 [MPIO 概觀](https://technet.microsoft.com/library/cc725907.aspx "MPIO 概觀 and features")。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-113">For more information, see [MPIO overview](https://technet.microsoft.com/library/cc725907.aspx "MPIO overview and features").</span></span>

<span data-ttu-id="cb2e6-114">Hello 高可用性的 StorSimple 解決方案，請在 hello Windows Server 主機已連線 tooyour StorSimple Virtual Array （模型 1200年） 上設定 MPIO。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-114">For hello high-availability of your StorSimple solution, configure MPIO on hello Windows Server hosts connected tooyour StorSimple Virtual Array (model 1200).</span></span> <span data-ttu-id="cb2e6-115">hello 主機伺服器時，然後可容許連結、 網路或介面失效。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-115">hello host servers can then tolerate a link, network, or interface failure.</span></span> 

<span data-ttu-id="cb2e6-116">您將需要這些步驟 tooconfigure MPIO toofollow:</span><span class="sxs-lookup"><span data-stu-id="cb2e6-116">You will need toofollow these steps tooconfigure MPIO:</span></span> 

* <span data-ttu-id="cb2e6-117">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="cb2e6-117">Configuration prerequisites</span></span>
* <span data-ttu-id="cb2e6-118">步驟 1： 安裝 MPIO hello Windows Server 主機上</span><span class="sxs-lookup"><span data-stu-id="cb2e6-118">Step 1: Install MPIO on hello Windows Server host</span></span>
* <span data-ttu-id="cb2e6-119">步驟 2：為 StorSimple 磁碟區設定 MPIO </span><span class="sxs-lookup"><span data-stu-id="cb2e6-119">Step 2: Configure MPIO for StorSimple volumes</span></span>
* <span data-ttu-id="cb2e6-120">步驟 3: Hello 主機上的掛接 StorSimple 磁碟區</span><span class="sxs-lookup"><span data-stu-id="cb2e6-120">Step 3: Mount StorSimple volumes on hello host</span></span>

<span data-ttu-id="cb2e6-121">Hello 下列各節討論 hello 上述步驟。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-121">Each of hello above steps is discussed in hello following sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb2e6-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="cb2e6-122">Prerequisites</span></span>
<span data-ttu-id="cb2e6-123">本節詳述 hello hello Windows Server 主機和虛擬陣列的組態先決條件。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-123">This section details hello configuration prerequisites for hello Windows Server host and your virtual array.</span></span>

### <a name="on-windows-server-host"></a><span data-ttu-id="cb2e6-124">在 Windows Server 主機上</span><span class="sxs-lookup"><span data-stu-id="cb2e6-124">On Windows Server host</span></span>
* <span data-ttu-id="cb2e6-125">確定 Windows Server 主機已啟用 2 個網路介面。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-125">Make sure that your Windows Server host has 2 network interfaces enabled.</span></span>

### <a name="on-storsimple-virtual-array"></a><span data-ttu-id="cb2e6-126">在 StorSimple Virtual Array 上</span><span class="sxs-lookup"><span data-stu-id="cb2e6-126">On StorSimple Virtual Array</span></span>
* <span data-ttu-id="cb2e6-127">hello 虛擬陣列應該設定為 iSCSI 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-127">hello virtual array should be configured as an iSCSI server.</span></span> <span data-ttu-id="cb2e6-128">詳細資訊，請參閱 toolearn[設定 iSCSI 伺服器的虛擬陣列](storsimple-virtual-array-deploy3-iscsi-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-128">toolearn more, see [set up virtual array as an iSCSI server](storsimple-virtual-array-deploy3-iscsi-setup.md).</span></span> <span data-ttu-id="cb2e6-129">Hello 陣列上應該啟用一或多個網路介面。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-129">One or more network interfaces should be enabled on hello array.</span></span>   
* <span data-ttu-id="cb2e6-130">hello 虛擬陣列上的網路介面應該從 hello Windows Server 主機。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-130">hello network interfaces on your virtual array should be reachable from hello Windows Server host.</span></span>
* <span data-ttu-id="cb2e6-131">應該在 StorSimple Virtual Array 上建立一或多個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-131">One or more volumes should be created on your StorSimple Virtual Array.</span></span> <span data-ttu-id="cb2e6-132">詳細資訊，請參閱 toolearn[加入磁碟區](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)StorSimple 虛擬陣列上。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-132">toolearn more, see [Add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) on your StorSimple Virtual Array.</span></span> <span data-ttu-id="cb2e6-133">在此程序中，我們會 hello 虛擬陣列上建立 3 磁碟區 （1 在本機固定，2 分層磁碟區所示下方）。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-133">In this procedure, we created 3 volumes (1 locally pinned and 2 tiered volumes as shown below) on hello virtual array.</span></span>
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a><span data-ttu-id="cb2e6-135">StorSimple Virtual Array 的硬體設定</span><span class="sxs-lookup"><span data-stu-id="cb2e6-135">Hardware configuration for StorSimple Virtual Array</span></span>
<span data-ttu-id="cb2e6-136">hello 圖顯示 hello 硬體組態的高可用性和負載平衡您的 Windows Server 主機和 StorSimple Virtual Array 這個程序中的多重路徑。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-136">hello figure below shows hello hardware configuration for high availability and load-balancing multipathing for your Windows Server host and StorSimple Virtual Array used in this procedure.</span></span>

![mpio 硬體組態](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

<span data-ttu-id="cb2e6-138">Hello 前圖所示：</span><span class="sxs-lookup"><span data-stu-id="cb2e6-138">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="cb2e6-139">在 Hyper-V 上佈建的 StorSimple Virtual Array 是設定為 iSCSI 伺服器的單一節點作用中裝置。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-139">Your StorSimple Virtual Array provisioned on Hyper-V is a single node active device configured as an iSCSI server.</span></span>
* <span data-ttu-id="cb2e6-140">陣列上已啟用兩個虛擬網路介面。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-140">Two virtual network interfaces are enabled on your array.</span></span> <span data-ttu-id="cb2e6-141">在本機 web UI 虛擬陣列 hello，確認 啟用瀏覽過的兩個網路介面**網路設定**如下所示：</span><span class="sxs-lookup"><span data-stu-id="cb2e6-141">In hello local web UI of your virtual array, verify that two network interfaces are enabled by navigating too**Network Settings** as shown below:</span></span>
  
    ![在 1200 上啟用的網路介面](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    <span data-ttu-id="cb2e6-143">請注意 hello IPv4 位址的 hello 啟用網路介面 （乙太網路，預設的乙太網路 2），並儲存供稍後使用 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-143">Note hello IPv4 addresses of hello enabled network interfaces (Ethernet, Ethernet 2 by default) and save for later use on hello host.</span></span>
* <span data-ttu-id="cb2e6-144">Windows Server 主機已啟用 2 個網路介面。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-144">Two network interfaces are enabled on your Windows Server host.</span></span> <span data-ttu-id="cb2e6-145">Hello 主機和陣列的連接的介面是否位於 hello 相同子網路，則會有 4 個路徑可用。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-145">If hello connected interfaces for host and array are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="cb2e6-146">這是此程序中的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-146">This was hello case in this procedure.</span></span> <span data-ttu-id="cb2e6-147">不過，如果 hello 陣列和主機介面上的每個網路介面是不同的 IP 子網路上 （且無法路由傳送），則只有 2 路徑會提供。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-147">However, if each network interface on hello array and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span>

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a><span data-ttu-id="cb2e6-148">步驟 1： 安裝 MPIO hello Windows Server 主機上</span><span class="sxs-lookup"><span data-stu-id="cb2e6-148">Step 1: Install MPIO on hello Windows Server host</span></span>
<span data-ttu-id="cb2e6-149">MPIO 是 Windows 伺服器預設不會安裝的選擇性功能。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-149">MPIO is an optional feature on Windows Server and is not installed by default.</span></span> <span data-ttu-id="cb2e6-150">您應該透過伺服器管理員將它安裝為功能。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-150">It should be installed as a feature through Server Manager.</span></span> <span data-ttu-id="cb2e6-151">tooinstall 這項功能在 Windows Server 主機上，完成下列程序 hello。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-151">tooinstall this feature on your Windows Server host, complete hello following procedure.</span></span>

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a><span data-ttu-id="cb2e6-152">步驟 2：為 StorSimple 磁碟區設定 MPIO </span><span class="sxs-lookup"><span data-stu-id="cb2e6-152">Step 2: Configure MPIO for StorSimple volumes</span></span>
<span data-ttu-id="cb2e6-153">MPIO 必須設定 toobe tooidentify StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-153">MPIO needs toobe configured tooidentify StorSimple volumes.</span></span> <span data-ttu-id="cb2e6-154">tooconfigure MPIO toorecognize StorSimple 磁碟區，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-154">tooconfigure MPIO toorecognize StorSimple volumes, perform hello following steps.</span></span>

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a><span data-ttu-id="cb2e6-155">步驟 3: Hello 主機上的掛接 StorSimple 磁碟區</span><span class="sxs-lookup"><span data-stu-id="cb2e6-155">Step 3: Mount StorSimple volumes on hello host</span></span>
<span data-ttu-id="cb2e6-156">Windows Server 上設定 MPIO 後，建立 hello StorSimple 陣列上的磁碟區即可掛接，然後可利用 MPIO 的備援。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-156">After MPIO is configured on Windows Server, volume(s) created on hello StorSimple array can be mounted and can then take advantage of MPIO for redundancy.</span></span> <span data-ttu-id="cb2e6-157">toomount 磁碟區，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-157">toomount a volume, perform hello following steps.</span></span>

#### <a name="toomount-volumes-on-hello-host"></a><span data-ttu-id="cb2e6-158">toomount hello 主機上的磁碟區</span><span class="sxs-lookup"><span data-stu-id="cb2e6-158">toomount volumes on hello host</span></span>
1. <span data-ttu-id="cb2e6-159">開啟 hello **iSCSI 啟動器屬性**hello Windows Server 主機上的視窗。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-159">Open hello **iSCSI Initiator Properties** window on hello Windows Server host.</span></span> <span data-ttu-id="cb2e6-160">跳過**伺服器管理員 > 儀表板 > 工具 > iSCSI 啟動器**。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-160">Go too**Server Manager > Dashboard > Tools > iSCSI Initiator**.</span></span>
2. <span data-ttu-id="cb2e6-161">在 hello **iSCSI 啟動器屬性**對話方塊中，按一下 **探索**，然後按一下**探索目標入口網站**。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-161">In hello **iSCSI Initiator Properties** dialog box, click **Discovery**, and then click **Discover Target Portal**.</span></span>
3. <span data-ttu-id="cb2e6-162">在 hello**探索目標入口網站**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="cb2e6-162">In hello **Discover Target Portal** dialog box, do hello following:</span></span>
   
    1. <span data-ttu-id="cb2e6-163">在您的 StorSimple Virtual Array 輸入 hello 的 hello 第一個啟用的網路介面的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-163">Enter hello IP address of hello first enabled network interface on your StorSimple Virtual Array.</span></span> <span data-ttu-id="cb2e6-164">根據預設，這會是 **乙太網路**。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-164">By default, this would be **Ethernet**.</span></span> 
    2. <span data-ttu-id="cb2e6-165">按一下**確定**tooreturn toohello **iSCSI 啟動器屬性** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-165">Click **OK** tooreturn toohello **iSCSI Initiator Properties** dialog box.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="cb2e6-166">如果您使用私人網路進行 iSCSI 連線，請輸入 hello hello DATA 連接埠是連接的 toohello 私人網路的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-166">If you are using a private network for iSCSI connections, enter hello IP address of hello DATA port that is connected toohello private network.</span></span>
     
4. <span data-ttu-id="cb2e6-167">在陣列上針對第二個網路介面 (例如，乙太網路 2) 重複步驟 2-3 。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-167">Repeat steps 2-3 for a second network interface (for example, Ethernet 2) on your array.</span></span> 
5. <span data-ttu-id="cb2e6-168">選取 hello**目標** 索引標籤中 hello **iSCSI 啟動器屬性** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-168">Select hello **Targets** tab in hello **iSCSI Initiator Properties** dialog box.</span></span> <span data-ttu-id="cb2e6-169">針對虛擬陣列，您應該將每個磁碟區表面視為**探索到的目標**之下的目標。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-169">For your virtual array, you should see each volume surface as a target under **Discovered Targets**.</span></span> <span data-ttu-id="cb2e6-170">在此情況下，會發現三個目標 （對應 toothree 磁碟區）。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-170">In this case, three targets (corresponding toothree volumes) would be discovered.</span></span>
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. <span data-ttu-id="cb2e6-172">按一下**連接**tooestablish 與 StorSimple 虛擬陣列的 iSCSI 工作階段。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-172">Click **Connect** tooestablish an iSCSI session with your StorSimple Virtual Array.</span></span> <span data-ttu-id="cb2e6-173">A**連接 tooTarget**對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-173">A **Connect tooTarget** dialog box will appear.</span></span> <span data-ttu-id="cb2e6-174">選取 hello**啟用多重路徑**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-174">Select hello **Enable multi-path** check box.</span></span> <span data-ttu-id="cb2e6-175">按一下 [進階] 。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-175">Click **Advanced**.</span></span>
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. <span data-ttu-id="cb2e6-177">在 hello**進階設定**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="cb2e6-177">In hello **Advanced Settings** dialog box, do hello following:</span></span>                                        
   
    1. <span data-ttu-id="cb2e6-178">在 hello**本機介面卡**下拉式清單中，選取**Microsoft iSCSI 啟動器**。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-178">On hello **Local Adapter** drop-down list, select **Microsoft iSCSI Initiator**.</span></span>
    2. <span data-ttu-id="cb2e6-179">在 hello**啟動器 IP**下拉式清單中，選取 hello hello 主機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-179">On hello **Initiator IP** drop-down list, select hello IP address of hello host.</span></span>
    3. <span data-ttu-id="cb2e6-180">在 hello**目標入口網站**IP 下拉式清單中，選取 hello IP 的陣列介面。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-180">On hello **Target Portal** IP drop-down list, select hello IP of array interface.</span></span>
    4. <span data-ttu-id="cb2e6-181">按一下**確定**tooreturn toohello **iSCSI 啟動器屬性** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-181">Click **OK** tooreturn toohello **iSCSI Initiator Properties** dialog box.</span></span>
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. <span data-ttu-id="cb2e6-183">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-183">Click **Properties**.</span></span> 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. <span data-ttu-id="cb2e6-185">在 hello**屬性**對話方塊中，按一下 **新增工作階段**。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-185">In hello **Properties** dialog box, click **Add Session**.</span></span>
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. <span data-ttu-id="cb2e6-187">在 hello**連接 tooTarget**對話方塊中，選取 hello**啟用多重路徑**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-187">In hello **Connect tooTarget** dialog box, select hello **Enable multi-path** check box.</span></span> <span data-ttu-id="cb2e6-188">按一下 [進階] 。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-188">Click **Advanced**.</span></span>
11. <span data-ttu-id="cb2e6-189">在 hello**進階設定**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="cb2e6-189">In hello **Advanced Settings** dialog box:</span></span>                                        
    
    1. <span data-ttu-id="cb2e6-190">在 hello**本機介面卡**下拉式清單中，選取 Microsoft iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-190">On hello **Local adapter** drop-down list, select Microsoft iSCSI Initiator.</span></span>

    2. <span data-ttu-id="cb2e6-191">在 hello**啟動器 IP**下拉式清單中，選取 hello IP 位址對應 toohello 主機。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-191">On hello **Initiator IP** drop-down list, select hello IP address corresponding toohello host.</span></span> <span data-ttu-id="cb2e6-192">在此情況下，您所連接 hello 陣列 tooa hello 主機上的單一網路介面上的兩個網路介面。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-192">In this case, you are connecting two network interfaces on hello array tooa single network interface on hello host.</span></span> <span data-ttu-id="cb2e6-193">因此，這個介面是 hello 相同的 hello 提供第一個工作階段。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-193">Therefore, this interface is hello same as that provided for hello first session.</span></span>

    3. <span data-ttu-id="cb2e6-194">在 hello**目標入口網站 IP**下拉式清單中，選取 hello hello hello 陣列上啟用第二個資料介面的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-194">On hello **Target Portal IP** drop-down list, select hello IP address for hello second data interface enabled on hello array.</span></span>

    4. <span data-ttu-id="cb2e6-195">按一下**確定**tooreturn toohello iSCSI 啟動器屬性 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-195">Click **OK** tooreturn toohello iSCSI Initiator Properties dialog box.</span></span> <span data-ttu-id="cb2e6-196">您已加入第二個工作階段 toohello 目標。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-196">You have added a second session toohello target.</span></span>
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. <span data-ttu-id="cb2e6-198">Hello 中加入想要的 hello 工作階段 （路徑） 之後, **iSCSI 啟動器屬性**對話方塊中，選取 hello 目標，然後按 **屬性**。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-198">After adding hello desired sessions (paths), in hello **iSCSI Initiator Properties** dialog box, select hello target and click **Properties**.</span></span> <span data-ttu-id="cb2e6-199">Hello hello 工作階段 索引標籤上**屬性**對話方塊中，注意 hello 四個工作階段識別碼對應 toohello 可能的路徑排列組合。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-199">On hello Sessions tab of hello **Properties** dialog box, note hello four session identifiers that correspond toohello possible path permutations.</span></span> <span data-ttu-id="cb2e6-200">工作階段，toocancel 選取 hello 核取方塊，下一步 tooa 工作階段識別碼，然後按一下**中斷連線**。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-200">toocancel a session, select hello check box next tooa session identifier, and then click **Disconnect**.</span></span>

    6. <span data-ttu-id="cb2e6-201">顯示在工作階段中，選取 hello tooview 裝置**裝置** 索引標籤 tooconfigure hello MPIO 原則，是選取的裝置，請按一下**MPIO**。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-201">tooview devices presented within sessions, select hello **Devices** tab. tooconfigure hello MPIO policy for a selected device, click **MPIO**.</span></span>

    7. <span data-ttu-id="cb2e6-202">hello**詳細資料**對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-202">hello **Details** dialog box will appear.</span></span> <span data-ttu-id="cb2e6-203">在 hello **MPIO**索引標籤上，您可以選取適當的 hello**負載平衡原則**設定。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-203">On hello **MPIO** tab, you can select hello appropriate **Load Balance Policy** settings.</span></span> <span data-ttu-id="cb2e6-204">您也可以檢視 hello **Active**或**待命**路徑類型。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-204">You can also view hello **Active** or **Standby** path type.</span></span>
12. <span data-ttu-id="cb2e6-205">重複步驟 8-11 tooadd 額外的工作階段 （路徑） toohello 目標。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-205">Repeat steps 8-11 tooadd additional sessions (paths) toohello target.</span></span> <span data-ttu-id="cb2e6-206">Hello 主機上的兩個介面和 hello 虛擬陣列上的兩個，您就可以新增每個目標的四個工作階段總數。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-206">With two interfaces on hello host and two on hello virtual array, you can add a total of four sessions for each target.</span></span> 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. <span data-ttu-id="cb2e6-208">您將需要 toorepeat 步驟執行，每個磁碟區 （做為目標的介面）。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-208">You will need toorepeat these steps for each volume (surfaces as a target).</span></span>
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. <span data-ttu-id="cb2e6-210">開啟**電腦管理**瀏覽過**伺服器管理員 > 儀表板 > 電腦管理**。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-210">Open **Computer Management** by navigating too**Server Manager > Dashboard > Computer Management**.</span></span> <span data-ttu-id="cb2e6-211">在 hello 左窗格中，按一下 **存放裝置 > 磁碟管理**。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-211">In hello left pane, click **Storage > Disk Management**.</span></span> <span data-ttu-id="cb2e6-212">hello hello StorSimple Virtual Array 上建立磁碟區會顯示 toothis 主機會出現在**磁碟管理**為新磁碟。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-212">hello volume(s) created on hello StorSimple Virtual Array that are visible toothis host will appear under **Disk Management** as new disk(s).</span></span>
15. <span data-ttu-id="cb2e6-213">初始化 hello 磁碟，並建立新的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-213">Initialize hello disk and create a new volume.</span></span> <span data-ttu-id="cb2e6-214">在 hello 格式過程中，選取 64 KB 的配置單位大小 (AUS)。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-214">During hello format process, select an allocation unit size (AUS) of 64 KB.</span></span> <span data-ttu-id="cb2e6-215">所有與 hello 可用的磁碟區重複 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-215">Repeat hello process for all hello available volumes.</span></span>
    
    ![磁碟管理](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. <span data-ttu-id="cb2e6-217">在下**磁碟管理**，以滑鼠右鍵按一下 hello**磁碟**選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-217">Under **Disk Management**, right-click hello **Disk** and select **Properties**.</span></span>
17. <span data-ttu-id="cb2e6-218">在 [hello**多重路徑磁碟裝置屬性**對話方塊方塊中，按一下 hello **MPIO** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-218">In hello **Multi-Path Disk Device Properties** dialog box, click hello **MPIO** tab.</span></span>
    
    ![磁碟屬性](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. <span data-ttu-id="cb2e6-220">在 hello **DSM 名稱**區段中，按一下**詳細資料**並確認已設定 hello 參數 toohello 預設參數。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-220">In hello **DSM Name** section, click **Details** and verify that hello parameters are set toohello default parameters.</span></span> <span data-ttu-id="cb2e6-221">hello 預設參數為：</span><span class="sxs-lookup"><span data-stu-id="cb2e6-221">hello default parameters are:</span></span>
    
    * <span data-ttu-id="cb2e6-222">路徑確認期間 = 30</span><span class="sxs-lookup"><span data-stu-id="cb2e6-222">Path Verify Period = 30</span></span>
    * <span data-ttu-id="cb2e6-223">重試計數 = 3</span><span class="sxs-lookup"><span data-stu-id="cb2e6-223">Retry Count = 3</span></span>
    * <span data-ttu-id="cb2e6-224">PDO 移除期間 = 20</span><span class="sxs-lookup"><span data-stu-id="cb2e6-224">PDO Remove Period = 20</span></span>
    * <span data-ttu-id="cb2e6-225">重試間隔 = 1</span><span class="sxs-lookup"><span data-stu-id="cb2e6-225">Retry Interval = 1</span></span>
    * <span data-ttu-id="cb2e6-226">啟用路徑確認 = 未選取。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-226">Path Verify Enabled = Unchecked.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="cb2e6-227">**請勿修改 hello 預設參數。**</span><span class="sxs-lookup"><span data-stu-id="cb2e6-227">**Do not modify hello default parameters.**</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="cb2e6-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb2e6-228">Next steps</span></span>
<span data-ttu-id="cb2e6-229">深入了解[使用您的 StorSimple Virtual Array hello StorSimple 裝置管理員服務 tooadminister](storsimple-virtual-array-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="cb2e6-229">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span>

