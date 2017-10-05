---
title: "為 StorSimple 裝置設定 MPIO | Microsoft Docs"
description: "描述如何針對與執行 Windows Server 2012 R2 的主機連線的 StorSimple 裝置設定多重路徑 I/O。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 9fe3fa3a2df63d111de742ecb48b1469aad543cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multipath-io-for-your-storsimple-device"></a><span data-ttu-id="54973-103">為 StorSimple 裝置設定多重路徑 I/O</span><span class="sxs-lookup"><span data-stu-id="54973-103">Configure Multipath I/O for your StorSimple device</span></span>

<span data-ttu-id="54973-104">本教學課程說明您應在執行 Windows Server 2012 R2 並與 StorSimple 實體裝置連接的主機上，據以安裝和使用多重路徑 I/O (MPIO) 功能的步驟。</span><span class="sxs-lookup"><span data-stu-id="54973-104">This tutorial describes the steps you should follow to install and use the Multipath I/O (MPIO) feature on a host running Windows Server 2012 R2 and connected to a StorSimple physical device.</span></span> <span data-ttu-id="54973-105">本文中的指導僅適用於 StorSimple 8000 系列實體裝置。</span><span class="sxs-lookup"><span data-stu-id="54973-105">The guidance in this article applies to StorSimple 8000 series physical devices only.</span></span> <span data-ttu-id="54973-106">StorSimple 雲端設備目前不支援 MPIO。</span><span class="sxs-lookup"><span data-stu-id="54973-106">MPIO is currently not supported on a StorSimple Cloud Appliance.</span></span>

<span data-ttu-id="54973-107">Microsoft 為 Windows Server 中的多重路徑 I/O (MPIO) 功能建立支援，協助建立高可用性、容錯的 SAN 組態。</span><span class="sxs-lookup"><span data-stu-id="54973-107">Microsoft built support for the Multipath I/O (MPIO) feature in Windows Server to help build highly available, fault-tolerant SAN configurations.</span></span> <span data-ttu-id="54973-108">MPIO 使用備援實體路徑元件 — 配接器、纜線以及交換器 — 以在伺服器與存放裝置之間建立邏輯路徑。</span><span class="sxs-lookup"><span data-stu-id="54973-108">MPIO uses redundant physical path components — adapters, cables, and switches — to create logical paths between the server and the storage device.</span></span> <span data-ttu-id="54973-109">如果元件故障而導致邏輯路徑失敗，多重路徑邏輯使用替代的 I/O 路徑，讓應用程式仍然可以存取其資料。</span><span class="sxs-lookup"><span data-stu-id="54973-109">If there is a component failure, causing a logical path to fail, multipathing logic uses an alternate path for I/O so that applications can still access their data.</span></span> <span data-ttu-id="54973-110">此外，依照您的設定，MPIO 也能藉由重新平衡所有路徑的負載來改善效能。</span><span class="sxs-lookup"><span data-stu-id="54973-110">Additionally depending on your configuration, MPIO can also improve performance by rebalancing the load across all these paths.</span></span> <span data-ttu-id="54973-111">如需詳細資訊，請參閱 [MPIO 概觀](https://technet.microsoft.com/library/cc725907.aspx "MPIO 概觀 and features")。</span><span class="sxs-lookup"><span data-stu-id="54973-111">For more information, see [MPIO overview](https://technet.microsoft.com/library/cc725907.aspx "MPIO overview and features").</span></span>

<span data-ttu-id="54973-112">您應該為 StorSimple 裝置設定 MPIO，才能獲得高可用性的 StorSimple 方案。</span><span class="sxs-lookup"><span data-stu-id="54973-112">For the high-availability of your StorSimple solution, MPIO should be configured on your StorSimple device.</span></span> <span data-ttu-id="54973-113">當您在執行 Windows Server 2012 R2 的主機伺服器上安裝 MPIO 時，伺服器才能容許連結、網路或介面失敗。</span><span class="sxs-lookup"><span data-stu-id="54973-113">When MPIO is installed on your host servers running Windows Server 2012 R2, the servers can then tolerate a link, network, or interface failure.</span></span>

## <a name="mpio-configuration-summary"></a><span data-ttu-id="54973-114">MPIO 設定摘要</span><span class="sxs-lookup"><span data-stu-id="54973-114">MPIO configuration summary</span></span>

<span data-ttu-id="54973-115">MPIO 是 Windows 伺服器預設不會安裝的選擇性功能。</span><span class="sxs-lookup"><span data-stu-id="54973-115">MPIO is an optional feature on Windows Server and is not installed by default.</span></span> <span data-ttu-id="54973-116">您應該透過伺服器管理員將它安裝為功能。</span><span class="sxs-lookup"><span data-stu-id="54973-116">It should be installed as a feature through Server Manager.</span></span>

<span data-ttu-id="54973-117">請依照下列步驟在 StorSimple 裝置上設定 MPIO：</span><span class="sxs-lookup"><span data-stu-id="54973-117">Follow these steps to configure MPIO on your StorSimple device:</span></span>

* <span data-ttu-id="54973-118">步驟 1：在 Windows Server 主機上安裝 MPIO</span><span class="sxs-lookup"><span data-stu-id="54973-118">Step 1: Install MPIO on the Windows Server host</span></span>
* <span data-ttu-id="54973-119">步驟 2：為 StorSimple 磁碟區設定 MPIO </span><span class="sxs-lookup"><span data-stu-id="54973-119">Step 2: Configure MPIO for StorSimple volumes</span></span>
* <span data-ttu-id="54973-120">步驟 3：在主機上掛接 StorSimple 磁碟區</span><span class="sxs-lookup"><span data-stu-id="54973-120">Step 3: Mount StorSimple volumes on the host</span></span>
* <span data-ttu-id="54973-121">步驟 4：設定 MPIO 以獲得高可用性與負載平衡</span><span class="sxs-lookup"><span data-stu-id="54973-121">Step 4: Configure MPIO for high availability and load balancing</span></span>

<span data-ttu-id="54973-122">上述步驟會在下列各節討論。</span><span class="sxs-lookup"><span data-stu-id="54973-122">Each of the preceding steps is discussed in the following sections.</span></span>

## <a name="step-1-install-mpio-on-the-windows-server-host"></a><span data-ttu-id="54973-123">步驟 1：在 Windows Server 主機上安裝 MPIO</span><span class="sxs-lookup"><span data-stu-id="54973-123">Step 1: Install MPIO on the Windows Server host</span></span>

<span data-ttu-id="54973-124">若要在 Windows Server 主機上安裝這項功能，請完成下列程序。</span><span class="sxs-lookup"><span data-stu-id="54973-124">To install this feature on your Windows Server host, complete the following procedure.</span></span>

#### <a name="to-install-mpio-on-the-host"></a><span data-ttu-id="54973-125">若要在主機上安裝 MPIO</span><span class="sxs-lookup"><span data-stu-id="54973-125">To install MPIO on the host</span></span>

1. <span data-ttu-id="54973-126">在 Windows Server 主機上開啟 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="54973-126">Open Server Manager on your Windows Server host.</span></span> <span data-ttu-id="54973-127">根據預設，伺服器管理員會在 Administrators 群組成員登入執行 Windows Server 2012 R2 或 Windows Server 2012 的電腦時啟動。</span><span class="sxs-lookup"><span data-stu-id="54973-127">By default, Server Manager starts when a member of the Administrators group logs on to a computer that is running Windows Server 2012 R2 or Windows Server 2012.</span></span> <span data-ttu-id="54973-128">如果尚未開啟 [伺服器管理員]，請按一下 [開始] > [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="54973-128">If the Server Manager is not already open, click **Start > Server Manager**.</span></span>
   
   ![伺服器管理員](./media/storsimple-configure-mpio-windows-server/IC740997.png)

2. <span data-ttu-id="54973-130">按一下 [伺服器管理員] > [儀表板] > [新增角色及功能]。</span><span class="sxs-lookup"><span data-stu-id="54973-130">Click **Server Manager > Dashboard > Add roles and features**.</span></span> <span data-ttu-id="54973-131">這樣會啟動 [新增角色及功能]  精靈。</span><span class="sxs-lookup"><span data-stu-id="54973-131">This starts the **Add Roles and Features** wizard.</span></span>
   
   ![新增角色及功能精靈 1](./media/storsimple-configure-mpio-windows-server/IC740998.png)
3. <span data-ttu-id="54973-133">在 [新增角色及功能] 精靈中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="54973-133">In the **Add Roles and Features** wizard, perform the following steps:</span></span>
   
   1. <span data-ttu-id="54973-134">在 [開始之前] 頁面中按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="54973-134">On the **Before you begin** page, click **Next**.</span></span>
   2. <span data-ttu-id="54973-135">在 [選取安裝類型] 頁面上，接受 [角色型或功能型安裝] 的預設值。</span><span class="sxs-lookup"><span data-stu-id="54973-135">On the **Select installation type** page, accept the default setting of **Role-based or feature-based** installation.</span></span> <span data-ttu-id="54973-136">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="54973-136">Click **Next**.</span></span>
   
       ![新增角色及功能精靈 2](./media/storsimple-configure-mpio-windows-server/IC740999.png)
   3. <span data-ttu-id="54973-138">在 [選取目的地伺服器] 頁面上，選擇 [從伺服器集區選取伺服器]。</span><span class="sxs-lookup"><span data-stu-id="54973-138">On the **Select destination server** page, choose **Select a server from the server pool**.</span></span> <span data-ttu-id="54973-139">應該會自動探索主機伺服器。</span><span class="sxs-lookup"><span data-stu-id="54973-139">Your host server should be discovered automatically.</span></span> <span data-ttu-id="54973-140">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="54973-140">Click **Next**.</span></span>
   4. <span data-ttu-id="54973-141">在 [選取伺服器角色] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="54973-141">On the **Select server roles** page, click **Next**.</span></span>
   5. <span data-ttu-id="54973-142">在 [選取功能] 頁面上，選取 [多重路徑 I/O]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="54973-142">On the **Select features** page, select **Multipath I/O**, and click **Next**.</span></span>
   
       ![新增角色及功能精靈 5](./media/storsimple-configure-mpio-windows-server/IC741000.png)
   6. <span data-ttu-id="54973-144">在 [確認安裝選項] 頁面上，確認選取項目，然後選取 [需要時自動重新啟動目的地伺服器]，如下所示。</span><span class="sxs-lookup"><span data-stu-id="54973-144">On the **Confirm installation selections** page, confirm the selection, and then select **Restart the destination server automatically if required**, as shown below.</span></span> <span data-ttu-id="54973-145">按一下 [Install] 。</span><span class="sxs-lookup"><span data-stu-id="54973-145">Click **Install**.</span></span>
   
       ![新增角色及功能精靈 8](./media/storsimple-configure-mpio-windows-server/IC741001.png)
   7. <span data-ttu-id="54973-147">完成安裝時，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="54973-147">You are notified when the installation is complete.</span></span> <span data-ttu-id="54973-148">按一下 [關閉]  即可關閉精靈。</span><span class="sxs-lookup"><span data-stu-id="54973-148">Click **Close** to close the wizard.</span></span>
   
       ![新增角色及功能精靈 9](./media/storsimple-configure-mpio-windows-server/IC741002.png)

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a><span data-ttu-id="54973-150">步驟 2：為 StorSimple 磁碟區設定 MPIO </span><span class="sxs-lookup"><span data-stu-id="54973-150">Step 2: Configure MPIO for StorSimple volumes</span></span>

<span data-ttu-id="54973-151">您必須設定 MPIO 才能識別 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="54973-151">MPIO must be configured to identify StorSimple volumes.</span></span> <span data-ttu-id="54973-152">若要設定 MPIO 以辨識 StorSimple 磁碟區，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="54973-152">To configure MPIO to recognize StorSimple volumes, perform the following steps.</span></span>

#### <a name="to-configure-mpio-for-storsimple-volumes"></a><span data-ttu-id="54973-153">若要為 StorSimple 磁碟區設定 MPIO </span><span class="sxs-lookup"><span data-stu-id="54973-153">To configure MPIO for StorSimple volumes</span></span>

1. <span data-ttu-id="54973-154">開啟 [MPIO 設定] 。</span><span class="sxs-lookup"><span data-stu-id="54973-154">Open the **MPIO configuration**.</span></span> <span data-ttu-id="54973-155">按一下 [伺服器管理員] > [儀表板] > [工具] > [MPIO]。</span><span class="sxs-lookup"><span data-stu-id="54973-155">Click **Server Manager > Dashboard > Tools > MPIO**.</span></span>
2. <span data-ttu-id="54973-156">在 [MPIO 內容] 對話方塊中，選取 [探索多重路徑] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="54973-156">In the **MPIO Properties** dialog box, select the **Discover Multi-Paths** tab.</span></span>
3. <span data-ttu-id="54973-157">選取 [新增 iSCSI 裝置支援]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="54973-157">Select **Add support for iSCSI devices**, and then click **Add**.</span></span>  
   <span data-ttu-id="54973-158">![MPIO 內容探索多重路徑](./media/storsimple-configure-mpio-windows-server/IC741003.png)</span><span class="sxs-lookup"><span data-stu-id="54973-158">![MPIO Properties Discover Multi Paths](./media/storsimple-configure-mpio-windows-server/IC741003.png)</span></span>
4. <span data-ttu-id="54973-159">當系統提示您將伺服器重新開機。</span><span class="sxs-lookup"><span data-stu-id="54973-159">Reboot the server when prompted.</span></span>
5. <span data-ttu-id="54973-160">在 [MPIO 內容] 對話方塊中，按一下 [MPIO 裝置] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="54973-160">In the **MPIO Properties** dialog box, click the **MPIO Devices** tab.</span></span> <span data-ttu-id="54973-161">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="54973-161">Click **Add**.</span></span>
    </br><span data-ttu-id="54973-162">![MPIO 內容 MPIO 裝置](./media/storsimple-configure-mpio-windows-server/IC741004.png)</span><span class="sxs-lookup"><span data-stu-id="54973-162">![MPIO Properties MPIO Devices](./media/storsimple-configure-mpio-windows-server/IC741004.png)</span></span>
6. <span data-ttu-id="54973-163">在 [新增 MPIO 支援] 對話方塊的 [裝置硬體識別碼] 下，輸入您的裝置序號。</span><span class="sxs-lookup"><span data-stu-id="54973-163">In the **Add MPIO Support** dialog box, under **Device Hardware ID**, enter your device serial number.</span></span> <span data-ttu-id="54973-164">若要取得裝置序號，請存取您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="54973-164">To get the device serial number, access your StorSimple Device Manager service.</span></span> <span data-ttu-id="54973-165">瀏覽至 [裝置] > [儀表板]。</span><span class="sxs-lookup"><span data-stu-id="54973-165">Navigate to **Devices > Dashboard**.</span></span> <span data-ttu-id="54973-166">裝置序號會顯示在裝置儀表板右邊的 [快速概覽] 窗格。</span><span class="sxs-lookup"><span data-stu-id="54973-166">The device serial number is displayed in the right **Quick Glance** pane of the device dashboard.</span></span>
    </br>
    <span data-ttu-id="54973-167">![新增 MPIO 支援](./media/storsimple-configure-mpio-windows-server/IC741005.png)</span><span class="sxs-lookup"><span data-stu-id="54973-167">![Add MPIO Support](./media/storsimple-configure-mpio-windows-server/IC741005.png)</span></span>
7. <span data-ttu-id="54973-168">當系統提示您將伺服器重新開機。</span><span class="sxs-lookup"><span data-stu-id="54973-168">Reboot the server when prompted.</span></span>

## <a name="step-3-mount-storsimple-volumes-on-the-host"></a><span data-ttu-id="54973-169">步驟 3：在主機上掛接 StorSimple 磁碟區</span><span class="sxs-lookup"><span data-stu-id="54973-169">Step 3: Mount StorSimple volumes on the host</span></span>

<span data-ttu-id="54973-170">在 Windows 伺服器上設定 MPIO 之後，就能掛接在 StorSimple 裝置上建立的磁碟區，並可以利用 MPIO 獲得備援。</span><span class="sxs-lookup"><span data-stu-id="54973-170">After MPIO is configured on Windows Server, volume(s) created on the StorSimple device can be mounted and can then take advantage of MPIO for redundancy.</span></span> <span data-ttu-id="54973-171">若要掛接磁碟區，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="54973-171">To mount a volume, perform the following steps.</span></span>

#### <a name="to-mount-volumes-on-the-host"></a><span data-ttu-id="54973-172">若要在主機上掛接磁碟區</span><span class="sxs-lookup"><span data-stu-id="54973-172">To mount volumes on the host</span></span>

1. <span data-ttu-id="54973-173">在 Windows Server 主機上，開啟 [iSCSI 啟動器內容]  視窗。</span><span class="sxs-lookup"><span data-stu-id="54973-173">Open the **iSCSI Initiator Properties** window on the Windows Server host.</span></span> <span data-ttu-id="54973-174">按一下 [伺服器管理員] > [儀表板] > [工具] > [iSCSI 啟動器]。</span><span class="sxs-lookup"><span data-stu-id="54973-174">Click **Server Manager > Dashboard > Tools > iSCSI Initiator**.</span></span>
2. <span data-ttu-id="54973-175">在 [iSCSI 啟動器內容] 對話方塊中，按一下 [探索] 索引標籤，然後按一下 [搜尋目標入口]。</span><span class="sxs-lookup"><span data-stu-id="54973-175">In the **iSCSI Initiator Properties** dialog box, click the Discovery tab, and then click **Discover Target Portal**.</span></span>
3. <span data-ttu-id="54973-176">在 [搜尋目標入口] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="54973-176">In the **Discover Target Portal** dialog box, perform the following steps:</span></span>
   
   1. <span data-ttu-id="54973-177">輸入 StorSimple 裝置的 DATA 連接埠 IP 位址 (例如，輸入 DATA 0)。</span><span class="sxs-lookup"><span data-stu-id="54973-177">Enter the IP address of the DATA port of your StorSimple device (for example, enter DATA 0).</span></span>
   2. <span data-ttu-id="54973-178">按一下 [確定] 以返回 [iSCSI 啟動器內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="54973-178">Click **OK** to return to the **iSCSI Initiator Properties** dialog box.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="54973-179">**如果您使用私人網路進行 iSCSI 連線，請輸入連線到私人網路的 DATA 連接埠 IP 位址。**</span><span class="sxs-lookup"><span data-stu-id="54973-179">**If you are using a private network for iSCSI connections, enter the IP address of the DATA port that is connected to the private network.**</span></span>
    
4. <span data-ttu-id="54973-180">在裝置上針對第二個網路介面 (例如，DATA 1) 重複步驟 2-3 。</span><span class="sxs-lookup"><span data-stu-id="54973-180">Repeat steps 2-3 for a second network interface (for example, DATA 1) on your device.</span></span> <span data-ttu-id="54973-181">請記住，您應該為 iSCSI 啟用這些介面。</span><span class="sxs-lookup"><span data-stu-id="54973-181">Keep in mind that these interfaces should be enabled for iSCSI.</span></span> <span data-ttu-id="54973-182">如需詳細資訊，請參閱[修改網路介面](storsimple-8000-modify-device-config.md#modify-network-interfaces)。</span><span class="sxs-lookup"><span data-stu-id="54973-182">For more information, see [Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>
5. <span data-ttu-id="54973-183">在 [iSCSI 啟動器內容] 對話方塊中，選取 [目標] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="54973-183">Select the **Targets** tab in the **iSCSI Initiator Properties** dialog box.</span></span> <span data-ttu-id="54973-184">您應該會在 [探索到的目標] 下看到 StorSimple 裝置目標 IQN。</span><span class="sxs-lookup"><span data-stu-id="54973-184">You should see the StorSimple device target IQN under **Discovered Targets**.</span></span>

   ![iSCSI 啟動器內容目標索引標籤](./media/storsimple-configure-mpio-windows-server/IC741007.png)
   
6. <span data-ttu-id="54973-186">按一下 [連接]  ，以與 StorSimple 裝置建立 iSCSI 工作階段。</span><span class="sxs-lookup"><span data-stu-id="54973-186">Click **Connect** to establish an iSCSI session with your StorSimple device.</span></span> <span data-ttu-id="54973-187">[連線到目標] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="54973-187">A **Connect to Target** dialog box appears.</span></span>
7. <span data-ttu-id="54973-188">在 [連線到目標] 對話方塊中，選取 [啟用多重路徑] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="54973-188">In the **Connect to Target** dialog box, select the **Enable multi-path** check box.</span></span> <span data-ttu-id="54973-189">按一下 [進階] 。</span><span class="sxs-lookup"><span data-stu-id="54973-189">Click **Advanced**.</span></span>
8. <span data-ttu-id="54973-190">在 [進階設定] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="54973-190">In the **Advanced Settings** dialog box, perform the following steps:</span></span>
   
   1. <span data-ttu-id="54973-191">在 [本機介面卡] 下拉式清單中，選取 [Microsoft iSCSI 啟動器]。</span><span class="sxs-lookup"><span data-stu-id="54973-191">On the **Local Adapter** drop-down list, select **Microsoft iSCSI Initiator**.</span></span>
   2. <span data-ttu-id="54973-192">在 [啟動器 IP]  下拉式清單中，選取主機的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="54973-192">On the **Initiator IP** drop-down list, select the IP address of the host.</span></span>
   3. <span data-ttu-id="54973-193">在 [目標入口 IP]  下拉式清單中，選取裝置介面的 IP。</span><span class="sxs-lookup"><span data-stu-id="54973-193">On the **Target Portal** IP drop-down list, select the IP of device interface.</span></span>
   4. <span data-ttu-id="54973-194">按一下 [確定] 以返回 [iSCSI 啟動器內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="54973-194">Click **OK** to return to the **iSCSI Initiator Properties** dialog box.</span></span>
9. <span data-ttu-id="54973-195">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="54973-195">Click **Properties**.</span></span> <span data-ttu-id="54973-196">在 [內容] 對話方塊中，按一下 [新增工作階段]。</span><span class="sxs-lookup"><span data-stu-id="54973-196">In the **Properties** dialog box, click **Add Session**.</span></span>
10. <span data-ttu-id="54973-197">在 [連線到目標] 對話方塊中，選取 [啟用多重路徑] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="54973-197">In the **Connect to Target** dialog box, select the **Enable multi-path** check box.</span></span> <span data-ttu-id="54973-198">按一下 [進階] 。</span><span class="sxs-lookup"><span data-stu-id="54973-198">Click **Advanced**.</span></span>
11. <span data-ttu-id="54973-199">在 [進階設定]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="54973-199">In the **Advanced Settings** dialog box:</span></span>

    1. <span data-ttu-id="54973-200">在 [本機介面卡]  下拉式清單中，選取 [Microsoft iSCSI 啟動器]。</span><span class="sxs-lookup"><span data-stu-id="54973-200">On the **Local adapter** drop-down list, select Microsoft iSCSI Initiator.</span></span>
    2. <span data-ttu-id="54973-201">在 [啟動器 IP]  下拉式清單中，選取對應到主機的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="54973-201">On the **Initiator IP** drop-down list, select the IP address corresponding to the host.</span></span> <span data-ttu-id="54973-202">在此情況下，您是將裝置上的兩個網路介面連線到主機上的單一網路介面。</span><span class="sxs-lookup"><span data-stu-id="54973-202">In this case, you are connecting two network interfaces on the device to a single network interface on the host.</span></span> <span data-ttu-id="54973-203">因此，這個介面會和第一個工作階段提供的相同。</span><span class="sxs-lookup"><span data-stu-id="54973-203">Therefore, this interface is the same as that provided for the first session.</span></span>
    3. <span data-ttu-id="54973-204">在 [目標入口 IP]  下拉式清單中，為裝置上啟用的第二個資料介面選取 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="54973-204">On the **Target Portal IP** drop-down list, select the IP address for the second data interface enabled on the device.</span></span>
    4. <span data-ttu-id="54973-205">按一下 [確定]  以返回 [iSCSI 啟動器內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="54973-205">Click **OK** to return to the iSCSI Initiator Properties dialog box.</span></span> <span data-ttu-id="54973-206">您完成將第二個工作階段新增到目標。</span><span class="sxs-lookup"><span data-stu-id="54973-206">You have added a second session to the target.</span></span>
12. <span data-ttu-id="54973-207">藉由瀏覽至 [伺服器管理員] > [儀表板] > [電腦管理]，來開啟 [電腦管理]。</span><span class="sxs-lookup"><span data-stu-id="54973-207">Open **Computer Management** by navigating to **Server Manager > Dashboard > Computer Management**.</span></span> <span data-ttu-id="54973-208">在左窗格中，按一下 [存放裝置] > [磁碟管理]。</span><span class="sxs-lookup"><span data-stu-id="54973-208">In the left pane, click **Storage > Disk Management**.</span></span> <span data-ttu-id="54973-209">在 StorSimple 裝置上建立且是此主機可以看見的磁碟區，在 [磁碟管理] 下會顯示為新磁碟。</span><span class="sxs-lookup"><span data-stu-id="54973-209">The volume created on the StorSimple device that are visible to this host appears under **Disk Management** as new disk(s).</span></span>
13. <span data-ttu-id="54973-210">初始化磁碟，並建立新的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="54973-210">Initialize the disk and create a new volume.</span></span> <span data-ttu-id="54973-211">在格式化程序期間，選取 64 KB 的區塊大小。</span><span class="sxs-lookup"><span data-stu-id="54973-211">During the format process, select a block size of 64 KB.</span></span>
    
    ![磁碟管理](./media/storsimple-configure-mpio-windows-server/IC741008.png)
14. <span data-ttu-id="54973-213">在 [磁碟管理] 下，於 [磁碟] 按一下滑鼠右鍵，然後選取 [內容]。</span><span class="sxs-lookup"><span data-stu-id="54973-213">Under **Disk Management**, right-click the **Disk** and select **Properties**.</span></span>
15. <span data-ttu-id="54973-214">在 [StorSimple 模型 #### 多重路徑磁碟裝置內容] 對話方塊中，按一下 [MPIO] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="54973-214">In the StorSimple Model #### **Multi-Path Disk Device Properties** dialog box, click the **MPIO** tab.</span></span>
    
    ![StorSimple 8100 多重路徑磁碟 DeviceProp。](./media/storsimple-configure-mpio-windows-server/IC741009.png)
16. <span data-ttu-id="54973-216">在 [DSM 名稱] 區段中，按一下 [詳細資料] 並確認參數已設定為預設參數。</span><span class="sxs-lookup"><span data-stu-id="54973-216">In the **DSM Name** section, click **Details** and verify that the parameters are set to the default parameters.</span></span> <span data-ttu-id="54973-217">預設參數如下：</span><span class="sxs-lookup"><span data-stu-id="54973-217">The default parameters are:</span></span>
    
    * <span data-ttu-id="54973-218">路徑確認期間 = 30</span><span class="sxs-lookup"><span data-stu-id="54973-218">Path Verify Period = 30</span></span>
    * <span data-ttu-id="54973-219">重試計數 = 3</span><span class="sxs-lookup"><span data-stu-id="54973-219">Retry Count = 3</span></span>
    * <span data-ttu-id="54973-220">PDO 移除期間 = 20</span><span class="sxs-lookup"><span data-stu-id="54973-220">PDO Remove Period = 20</span></span>
    * <span data-ttu-id="54973-221">重試間隔 = 1</span><span class="sxs-lookup"><span data-stu-id="54973-221">Retry Interval = 1</span></span>
    * <span data-ttu-id="54973-222">啟用路徑確認 = 未選取。</span><span class="sxs-lookup"><span data-stu-id="54973-222">Path Verify Enabled = Unchecked.</span></span>

> [!NOTE]
> <span data-ttu-id="54973-223">**請不要修改預設的參數。**</span><span class="sxs-lookup"><span data-stu-id="54973-223">**Do not modify the default parameters.**</span></span>


## <a name="step-4-configure-mpio-for-high-availability-and-load-balancing"></a><span data-ttu-id="54973-224">步驟 4：設定 MPIO 以獲得高可用性與負載平衡</span><span class="sxs-lookup"><span data-stu-id="54973-224">Step 4: Configure MPIO for high availability and load balancing</span></span>

<span data-ttu-id="54973-225">多個工作階段必須以手動方式加入以宣告不同的路徑，才能獲得以多重路徑為基礎的高可用性與負載平衡。</span><span class="sxs-lookup"><span data-stu-id="54973-225">For multi-path based high availability and load balancing, multiple sessions must be manually added to declare the different paths available.</span></span> <span data-ttu-id="54973-226">比方說，如果主機有兩個介面連接到 SAN，而裝置也有兩個介面連接到 SAN，那麼您需要以正確的路徑排列組合設定四個工作階段 (如果每個 DATA 介面與主機介面都位在不同的 IP 子網路且不可路由時，將只需要兩個工作階段)。</span><span class="sxs-lookup"><span data-stu-id="54973-226">For example, if the host has two interfaces connected to SAN and the device has two interfaces connected to SAN, then you need four sessions configured with proper path permutations (only two sessions will be required if each DATA interface and host interface is on a different IP subnet and is not routable).</span></span>

<span data-ttu-id="54973-227">「我們建議您在裝置和應用程式主機之間至少有 8 個作用中的平行工作階段。」</span><span class="sxs-lookup"><span data-stu-id="54973-227">**We recommend that you have at least 8 active parallel sessions between the device and your application host.**</span></span> <span data-ttu-id="54973-228">這可藉由在 Windows Server 系統上啟用 4 個網路介面來達成。</span><span class="sxs-lookup"><span data-stu-id="54973-228">This can be achieved by enabling 4 network interfaces on your Windows Server system.</span></span> <span data-ttu-id="54973-229">在 Windows Server 主機上的硬體或作業系統層級上，透過網路虛擬化技術使用實體網路介面或虛擬介面。</span><span class="sxs-lookup"><span data-stu-id="54973-229">Use physical network interfaces or virtual interfaces via network virtualization technologies on the hardware or operating system level on your Windows Server host.</span></span> <span data-ttu-id="54973-230">透過在裝置上使用這兩個網路介面，此設定將會有 8 個作用中的工作階段。</span><span class="sxs-lookup"><span data-stu-id="54973-230">With the two network interfaces on the device, this configuration would result in 8 active sessions.</span></span> <span data-ttu-id="54973-231">這項設定有助於將裝置和雲端輸送量最佳化。</span><span class="sxs-lookup"><span data-stu-id="54973-231">This configuration helps optimize the device and cloud throughput.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54973-232">**建議您不要混合使用 1 GbE 與 10 GbE 網路介面。如果您使用兩個網路介面，這兩個介面的類型應要完全相同。**</span><span class="sxs-lookup"><span data-stu-id="54973-232">**We recommend that you do not mix 1 GbE and 10 GbE network interfaces. If you use two network interfaces, both interfaces should be the identical type.**</span></span>

<span data-ttu-id="54973-233">下列程序描述有兩個網路介面的 StorSimple 裝置連接到有兩個網路介面的主機時，要如何新增工作階段。</span><span class="sxs-lookup"><span data-stu-id="54973-233">The following procedure describes how to add sessions when a StorSimple device with two network interfaces is connected to a host with two network interfaces.</span></span> <span data-ttu-id="54973-234">這只會為您提供 4 個工作階段。</span><span class="sxs-lookup"><span data-stu-id="54973-234">This gives you only 4 sessions.</span></span> <span data-ttu-id="54973-235">使用這個與具有兩個連接到具有四個網路介面之主機的網路介面的 StorSimple 裝置所使用的相同程序。</span><span class="sxs-lookup"><span data-stu-id="54973-235">Use this same procedure with a StorSimple device with two network interfaces connected to a host with four network interfaces.</span></span> <span data-ttu-id="54973-236">您必須設定 8 個工作階段，而不是此處所述的 4 個工作階段。</span><span class="sxs-lookup"><span data-stu-id="54973-236">You will need to configure 8 instead of the 4 sessions described here.</span></span>

### <a name="to-configure-mpio-for-high-availability-and-load-balancing"></a><span data-ttu-id="54973-237">若要設定 MPIO 以獲得高可用性與負載平衡</span><span class="sxs-lookup"><span data-stu-id="54973-237">To configure MPIO for high availability and load balancing</span></span>

1. <span data-ttu-id="54973-238">若要探索目標：在 [iSCSI 啟動器內容] 對話方塊的 [探索] 索引標籤中，然後按一下 [探索入口]。</span><span class="sxs-lookup"><span data-stu-id="54973-238">Perform a discovery of the target: in the **iSCSI Initiator Properties** dialog box, on the **Discovery** tab, click **Discover Portal**.</span></span>
2. <span data-ttu-id="54973-239">在 [連線到目標]  對話方塊中，輸入其中一個裝置網路介面的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="54973-239">In the **Connect to Target** dialog box, enter the IP address of one of the device network interfaces.</span></span>
3. <span data-ttu-id="54973-240">按一下 [確定] 以返回 [iSCSI 啟動器內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="54973-240">Click **OK** to return to the **iSCSI Initiator Properties** dialog box.</span></span>
4. <span data-ttu-id="54973-241">在 [iSCSI 啟動器內容] 對話方塊中，選取 [目標] 索引標籤，反白探索到的目標，然後按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="54973-241">In the **iSCSI Initiator Properties** dialog box, select the **Targets** tab, highlight the discovered target, and then click **Connect**.</span></span> <span data-ttu-id="54973-242">[連線到目標]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="54973-242">The **Connect to Target** dialog box appears.</span></span>
5. <span data-ttu-id="54973-243">在 [連線到目標]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="54973-243">In the **Connect to Target** dialog box:</span></span>
   
   1. <span data-ttu-id="54973-244">保留 [將此連線新增到我的最愛目標清單]  預設選取的目標設定。</span><span class="sxs-lookup"><span data-stu-id="54973-244">Leave the default selected target setting for **Add this connection** to the list of favorite targets.</span></span> <span data-ttu-id="54973-245">這樣一來，這部電腦每次重新啟動時，裝置都會自動嘗試重新連線。</span><span class="sxs-lookup"><span data-stu-id="54973-245">This makes the device automatically attempt to restart the connection every time this computer restarts.</span></span>
   2. <span data-ttu-id="54973-246">選取 [啟用多重路徑]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="54973-246">Select the **Enable multi-path** check box.</span></span>
   3. <span data-ttu-id="54973-247">按一下 [進階] 。</span><span class="sxs-lookup"><span data-stu-id="54973-247">Click **Advanced**.</span></span>
6. <span data-ttu-id="54973-248">在 [進階設定]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="54973-248">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="54973-249">在 [本機介面卡] 下拉式清單中，選取 [Microsoft iSCSI 啟動器]。</span><span class="sxs-lookup"><span data-stu-id="54973-249">On the **Local Adapter** drop-down list, select **Microsoft iSCSI Initiator**.</span></span>
   2. <span data-ttu-id="54973-250">在 [啟動器 IP]  下拉式清單中，選取主機的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="54973-250">On the **Initiator IP** drop-down list, select the IP address of the host.</span></span>
   3. <span data-ttu-id="54973-251">在 [目標入口 IP]  下拉式清單中，為裝置上啟用的資料介面選取 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="54973-251">On the **Target Portal IP** drop-down list, select the IP address of the data interface enabled on the device.</span></span>
   4. <span data-ttu-id="54973-252">按一下 [確定]  以返回 [iSCSI 啟動器內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="54973-252">Click **OK** to return to the iSCSI Initiator Properties dialog box.</span></span>
7. <span data-ttu-id="54973-253">按一下 [內容] 並在 [內容] 對話方塊中，按一下 [新增工作階段]。</span><span class="sxs-lookup"><span data-stu-id="54973-253">Click **Properties**, and in the **Properties** dialog box, click **Add Session**.</span></span>
8. <span data-ttu-id="54973-254">在 [連線到目標] 對話方塊中，選取 [啟用多重路徑] 核取方塊，然後按一下 [進階]。</span><span class="sxs-lookup"><span data-stu-id="54973-254">In the **Connect to Target** dialog box, select the **Enable multi-path** check box, and then click **Advanced**.</span></span>
9. <span data-ttu-id="54973-255">在 [進階設定]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="54973-255">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="54973-256">在 [本機介面卡] 下拉式清單中，選取 [Microsoft iSCSI 啟動器]。</span><span class="sxs-lookup"><span data-stu-id="54973-256">On the **Local adapter** drop-down list, select **Microsoft iSCSI Initiator**.</span></span>
   2. <span data-ttu-id="54973-257">在 [啟動器 IP]  下拉式清單中，選取對應到主機上第二個介面的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="54973-257">On the **Initiator IP** drop-down list, select the IP address corresponding to the second interface on the host.</span></span>
   3. <span data-ttu-id="54973-258">在 [目標入口 IP]  下拉式清單中，為裝置上啟用的第二個資料介面選取 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="54973-258">On the **Target Portal IP** drop-down list, select the IP address for the second data interface enabled on the device.</span></span>
   4. <span data-ttu-id="54973-259">按一下 [確定] 以返回 [iSCSI 啟動器內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="54973-259">Click **OK** to return to the **iSCSI Initiator Properties** dialog box.</span></span> <span data-ttu-id="54973-260">您現已完成將第二個工作階段新增到目標。</span><span class="sxs-lookup"><span data-stu-id="54973-260">You have now added a second session to the target.</span></span>
10. <span data-ttu-id="54973-261">重複步驟 8-10，將其他工作階段 (路徑) 新增到目標。</span><span class="sxs-lookup"><span data-stu-id="54973-261">Repeat Steps 8-10 to add additional sessions (paths) to the target.</span></span> <span data-ttu-id="54973-262">主機上有兩個介面且裝置上也有兩個，您總共可以新增四個工作階段。</span><span class="sxs-lookup"><span data-stu-id="54973-262">With two interfaces on the host and two on the device, you can add a total of four sessions.</span></span>
11. <span data-ttu-id="54973-263">在新增所需的工作階段 (路徑) 之後，請在 [iSCSI 啟動器內容] 對話方塊中，選取目標，然後按一下 [內容]。</span><span class="sxs-lookup"><span data-stu-id="54973-263">After adding the desired sessions (paths), in the **iSCSI Initiator Properties** dialog box, select the target and click **Properties**.</span></span> <span data-ttu-id="54973-264">在 [內容]  對話方塊的 [工作階段] 索引標籤中，針對可能的路徑排列組合記下其對應的四個工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="54973-264">On the Sessions tab of the **Properties** dialog box, note the four session identifiers that correspond to the possible path permutations.</span></span> <span data-ttu-id="54973-265">若要取消工作階段，請選取工作階段識別碼旁邊的核取方塊，然後按一下 [中斷連線] 。</span><span class="sxs-lookup"><span data-stu-id="54973-265">To cancel a session, select the check box next to a session identifier, and then click **Disconnect**.</span></span>
12. <span data-ttu-id="54973-266">若要檢視工作階段內顯示的裝置，請選取 [裝置]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="54973-266">To view devices presented within sessions, select the **Devices** tab.</span></span> <span data-ttu-id="54973-267">若要為選取的裝置設定 MPIO 原則，請按一下 [MPIO] 。</span><span class="sxs-lookup"><span data-stu-id="54973-267">To configure the MPIO policy for a selected device, click **MPIO**.</span></span> <span data-ttu-id="54973-268">[裝置詳細資料] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="54973-268">The **Device Details** dialog box appears.</span></span> <span data-ttu-id="54973-269">在 [MPIO] 索引標籤上，您可以選取適當 [負載平衡原則] 設定。</span><span class="sxs-lookup"><span data-stu-id="54973-269">On the **MPIO** tab, you can select the appropriate **Load Balance Policy** settings.</span></span> <span data-ttu-id="54973-270">您也可以檢視 [使用中] 或 [待命] 路徑類型。</span><span class="sxs-lookup"><span data-stu-id="54973-270">You can also view the **Active** or **Standby** path type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54973-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54973-271">Next steps</span></span>

<span data-ttu-id="54973-272">深入了解[使用 StorSimple 裝置管理員服務修改 StorSimple 裝置設定](storsimple-8000-modify-device-config.md)。</span><span class="sxs-lookup"><span data-stu-id="54973-272">Learn more about [using the StorSimple Device Manager service to modify your StorSimple device configuration](storsimple-8000-modify-device-config.md).</span></span>

