---
title: "aaaConfigure MPIO StorSimple Linux 主機上的 |Microsoft 文件"
description: "執行 CentOS 6.6 StorSimple 連接 tooa Linux 主機上設定 MPIO"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="15d7e-103">在執行 CentOS 的 StorSimple 主機上設定 MPIO</span><span class="sxs-lookup"><span data-stu-id="15d7e-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="15d7e-104">本文說明 hello 步驟需要的 tooconfigure 多重路徑 IO (MPIO)，在 Centos 6.6 主機伺服器上。</span><span class="sxs-lookup"><span data-stu-id="15d7e-104">This article explains hello steps required tooconfigure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="15d7e-105">hello 主機伺服器是高可用性，透過 iSCSI 啟動器連線的 tooyour Microsoft Azure StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="15d7e-105">hello host server is connected tooyour Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="15d7e-106">它會描述詳細 hello 自動探索多重路徑裝置和 hello 特定的設定，只為 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="15d7e-106">It describes in detail hello automatic discovery of multipath devices and hello specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="15d7e-107">此程序是 StorSimple 8000 系列裝置的適用 tooall hello 模型。</span><span class="sxs-lookup"><span data-stu-id="15d7e-107">This procedure is applicable tooall hello models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="15d7e-108">此程序無法用於 StorSimple 虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="15d7e-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="15d7e-109">如需詳細資訊，請參閱如何 tooconfigure 裝載虛擬裝置的伺服器。</span><span class="sxs-lookup"><span data-stu-id="15d7e-109">For more information, see how tooconfigure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="15d7e-110">關於多重路徑</span><span class="sxs-lookup"><span data-stu-id="15d7e-110">About multipathing</span></span>
<span data-ttu-id="15d7e-111">hello 多重路徑功能可讓您 tooconfigure 主機伺服器與存放裝置之間的多個 I/O 路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-111">hello multipathing feature allows you tooconfigure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="15d7e-112">這些 I/O 路徑是可包含不同纜線、開關、網路介面及控制站的實體 SAN 連線。</span><span class="sxs-lookup"><span data-stu-id="15d7e-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="15d7e-113">多重路徑彙總 hello I/O 路徑 tooconfigure 與 hello 彙總路徑的所有相關聯的新裝置。</span><span class="sxs-lookup"><span data-stu-id="15d7e-113">Multipathing aggregates hello I/O paths, tooconfigure a new device that is associated with all of hello aggregated paths.</span></span>

<span data-ttu-id="15d7e-114">多重路徑 hello 目的是一體兩面：</span><span class="sxs-lookup"><span data-stu-id="15d7e-114">hello purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="15d7e-115">**高可用性**: hello I/O 路徑 （例如，纜線、 參數、 網路介面或控制站） 的任何項目失敗時，它會提供替代路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-115">**High availability**: It provides an alternate path if any element of hello I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="15d7e-116">**負載平衡**： 根據您的儲存體裝置 hello 組態，它可以改善 hello 效能偵測 hello I/O 路徑上的負載，並以動態方式重新平衡負載。</span><span class="sxs-lookup"><span data-stu-id="15d7e-116">**Load balancing**: Depending on hello configuration of your storage device, it can improve hello performance by detecting loads on hello I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="15d7e-117">關於多重路徑元件</span><span class="sxs-lookup"><span data-stu-id="15d7e-117">About multipathing components</span></span>
<span data-ttu-id="15d7e-118">Linux 中的多重路徑是由核心元件和下列的使用者空間元件所組成。</span><span class="sxs-lookup"><span data-stu-id="15d7e-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="15d7e-119">**核心**: hello 主要元件是 hello*裝置對應工具*，排列 I/O，並支援容錯移轉路徑與路徑群組。</span><span class="sxs-lookup"><span data-stu-id="15d7e-119">**Kernel**: hello main component is hello *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="15d7e-120">**使用者空間**： 這些是*多重路徑工具*可用於管理多重路徑裝置藉由指示 hello 裝置-多重路徑對應程式模組哪些 toodo。</span><span class="sxs-lookup"><span data-stu-id="15d7e-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing hello device-mapper multipath module what toodo.</span></span> <span data-ttu-id="15d7e-121">hello 工具包含：</span><span class="sxs-lookup"><span data-stu-id="15d7e-121">hello tools consist of:</span></span>
   
   * <span data-ttu-id="15d7e-122">**Multipath**︰列出及設定多重路徑的裝置。</span><span class="sxs-lookup"><span data-stu-id="15d7e-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="15d7e-123">**Multipathd**： 執行多重路徑和監視 hello 路徑的精靈。</span><span class="sxs-lookup"><span data-stu-id="15d7e-123">**Multipathd**: daemon that executes multipath and monitors hello paths.</span></span>
   * <span data-ttu-id="15d7e-124">**Devmap 名稱**: devmaps 提供有意義的裝置名稱 tooudev。</span><span class="sxs-lookup"><span data-stu-id="15d7e-124">**Devmap-name**: provides a meaningful device-name tooudev for devmaps.</span></span>
   * <span data-ttu-id="15d7e-125">**Kpartx**： 對應線性 devmaps toodevice 分割 toomake 多重路徑對應可分割。</span><span class="sxs-lookup"><span data-stu-id="15d7e-125">**Kpartx**: maps linear devmaps toodevice partitions toomake multipath maps partitionable.</span></span>
   * <span data-ttu-id="15d7e-126">**Multipath.conf**： 組態檔是使用的 toooverwrite hello 內建組態資料表的多重路徑服務精靈。</span><span class="sxs-lookup"><span data-stu-id="15d7e-126">**Multipath.conf**: configuration file for multipath daemon that is used toooverwrite hello built-in configuration table.</span></span>

### <a name="about-hello-multipathconf-configuration-file"></a><span data-ttu-id="15d7e-127">有關 hello multipath.conf 組態檔</span><span class="sxs-lookup"><span data-stu-id="15d7e-127">About hello multipath.conf configuration file</span></span>
<span data-ttu-id="15d7e-128">hello 設定檔`/etc/multipath.conf`使許多 hello 多重路徑功能使用者可設定。</span><span class="sxs-lookup"><span data-stu-id="15d7e-128">hello configuration file `/etc/multipath.conf` makes many of hello multipathing features user-configurable.</span></span> <span data-ttu-id="15d7e-129">hello`multipath`命令和 hello 的核心服務精靈`multipathd`使用此檔案中找到的資訊。</span><span class="sxs-lookup"><span data-stu-id="15d7e-129">hello `multipath` command and hello kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="15d7e-130">只有在 hello 多重路徑裝置 hello 組態期間參考 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="15d7e-130">hello file is consulted only during hello configuration of hello multipath devices.</span></span> <span data-ttu-id="15d7e-131">請確定已進行所有變更，然後再執行 hello`multipath`命令。</span><span class="sxs-lookup"><span data-stu-id="15d7e-131">Make sure that all changes are made before you run hello `multipath` command.</span></span> <span data-ttu-id="15d7e-132">如果您修改 hello 檔案之後，您會需要 toostop 並啟動 multipathd hello 變更 tootake 效果的一次。</span><span class="sxs-lookup"><span data-stu-id="15d7e-132">If you modify hello file afterwards, you will need toostop and start multipathd again for hello changes tootake effect.</span></span>

<span data-ttu-id="15d7e-133">hello multipath.conf 有五個區段：</span><span class="sxs-lookup"><span data-stu-id="15d7e-133">hello multipath.conf has five sections:</span></span>

- <span data-ttu-id="15d7e-134">**系統層級的預設值** *(defaults)*：您可以覆寫系統層級預設值。</span><span class="sxs-lookup"><span data-stu-id="15d7e-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="15d7e-135">**黑名單裝置** *（黑名單）*： 您可以指定不受裝置對應工具的裝置 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="15d7e-135">**Blacklisted devices** *(blacklist)*: You can specify hello list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="15d7e-136">**列入封鎖清單例外狀況** *(blacklist_exceptions)*： 您可以識別視為多重路徑裝置，即使 hello 黑名單中所列的特定裝置 toobe。</span><span class="sxs-lookup"><span data-stu-id="15d7e-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices toobe treated as multipath devices even if listed in hello blacklist.</span></span>
- <span data-ttu-id="15d7e-137">**設定特定的儲存體控制器** *（裝置）*： 您可以指定將會套用的 toodevices 廠商和產品資訊的組態設定。</span><span class="sxs-lookup"><span data-stu-id="15d7e-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied toodevices that have Vendor and Product information.</span></span>
- <span data-ttu-id="15d7e-138">**裝置特定設定** *(multipaths)*： 您可以使用此區段 toofine 微調 hello 組態設定的個別 Lun。</span><span class="sxs-lookup"><span data-stu-id="15d7e-138">**Device specific settings** *(multipaths)*: You can use this section toofine-tune hello configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a><span data-ttu-id="15d7e-139">StorSimple 連接的 tooLinux 主機上設定多重路徑</span><span class="sxs-lookup"><span data-stu-id="15d7e-139">Configure multipathing on StorSimple connected tooLinux host</span></span>
<span data-ttu-id="15d7e-140">StorSimple 裝置連線 tooa Linux 主機可以設定為高可用性及負載平衡。</span><span class="sxs-lookup"><span data-stu-id="15d7e-140">A StorSimple device connected tooa Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="15d7e-141">例如，如果 hello Linux 主機有兩個介面連接的 toohello SAN 和 hello 裝置有兩個介面連接 toohello SAN 上的這些介面的這類 hello 相同子網路，則會有 4 個路徑可用。</span><span class="sxs-lookup"><span data-stu-id="15d7e-141">For example, if hello Linux host has two interfaces connected toohello SAN and hello device has two interfaces connected toohello SAN such that these interfaces are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="15d7e-142">不過，如果 hello 裝置和主機介面上的每個 DATA 介面是不同的 IP 子網路上 （且無法路由傳送），則只有 2 路徑會提供。</span><span class="sxs-lookup"><span data-stu-id="15d7e-142">However, if each DATA interface on hello device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="15d7e-143">您可以設定多重路徑 tooautomatically 探索所有的 hello 可用的路徑、 選擇這些路徑的負載平衡演算法、 套用特定的組態設定，僅限 StorSimple 磁碟區，然後啟用並驗證多重路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-143">You can configure multipathing tooautomatically discover all hello available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="15d7e-144">hello 下列程序描述如何 tooconfigure 多重路徑有兩個網路介面的 StorSimple 裝置時使用兩個網路介面連接的 tooa 主機。</span><span class="sxs-lookup"><span data-stu-id="15d7e-144">hello following procedure describes how tooconfigure multipathing when a StorSimple device with two network interfaces is connected tooa host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15d7e-145">必要條件</span><span class="sxs-lookup"><span data-stu-id="15d7e-145">Prerequisites</span></span>
<span data-ttu-id="15d7e-146">本節詳述 hello CentOS 伺服器與您的 StorSimple 裝置的組態先決條件。</span><span class="sxs-lookup"><span data-stu-id="15d7e-146">This section details hello configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="15d7e-147">在 CentOS 主機上</span><span class="sxs-lookup"><span data-stu-id="15d7e-147">On CentOS host</span></span>
1. <span data-ttu-id="15d7e-148">確定 CentOS 主機已啟用 2 個網路介面。</span><span class="sxs-lookup"><span data-stu-id="15d7e-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="15d7e-149">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="15d7e-150">hello 下列範例顯示 hello 時輸出兩張網路介面 (`eth0`和`eth1`) 存在於 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="15d7e-150">hello following example shows hello output when two network interfaces (`eth0` and `eth1`) are present on hello host.</span></span>
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. <span data-ttu-id="15d7e-151">在 CentOS 伺服器上安裝 *iSCSI-initiator-utils* 。</span><span class="sxs-lookup"><span data-stu-id="15d7e-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="15d7e-152">執行下列步驟 tooinstall hello *iSCSI 啟動器-公用程式*。</span><span class="sxs-lookup"><span data-stu-id="15d7e-152">Perform hello following steps tooinstall *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="15d7e-153">以 `root` 身分登入到 CentOS 主機。</span><span class="sxs-lookup"><span data-stu-id="15d7e-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="15d7e-154">安裝 hello *iSCSI 啟動器-公用程式*。</span><span class="sxs-lookup"><span data-stu-id="15d7e-154">Install hello *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="15d7e-155">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="15d7e-156">之後 hello *iSCSI 啟動器-公用程式*已順利安裝，請啟動 hello iSCSI 服務。</span><span class="sxs-lookup"><span data-stu-id="15d7e-156">After hello *iSCSI-Initiator-utils* is successfully installed, start hello iSCSI service.</span></span> <span data-ttu-id="15d7e-157">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="15d7e-158">上的情況下，`iscsid`可能不會實際啟動並 hello`--force`可能需要的選項</span><span class="sxs-lookup"><span data-stu-id="15d7e-158">On occasions, `iscsid` may not actually start and hello `--force` option may be needed</span></span>
   4. <span data-ttu-id="15d7e-159">iSCSI 啟動器已啟用在開機時，使用 hello tooensure`chkconfig`命令 tooenable hello 服務。</span><span class="sxs-lookup"><span data-stu-id="15d7e-159">tooensure that your iSCSI initiator is enabled during boot time, use hello `chkconfig` command tooenable hello service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="15d7e-160">tooverify，但是該已正確地安裝程式中，執行 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="15d7e-160">tooverify that that it was properly setup, run hello command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="15d7e-161">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="15d7e-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="15d7e-162">從 hello 上述範例中，您可以看到 iSCSI 環境，將執行層級 2、 3、 4 和 5 上開機時執行。</span><span class="sxs-lookup"><span data-stu-id="15d7e-162">From hello above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="15d7e-163">安裝 *device-mapper-multipath*。</span><span class="sxs-lookup"><span data-stu-id="15d7e-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="15d7e-164">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="15d7e-165">hello 安裝將會啟動。</span><span class="sxs-lookup"><span data-stu-id="15d7e-165">hello installation will start.</span></span> <span data-ttu-id="15d7e-166">型別**Y** toocontinue 出現確認提示時。</span><span class="sxs-lookup"><span data-stu-id="15d7e-166">Type **Y** toocontinue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="15d7e-167">在 StorSimple 裝置上</span><span class="sxs-lookup"><span data-stu-id="15d7e-167">On StorSimple device</span></span>
<span data-ttu-id="15d7e-168">您的 StorSimple 裝置應該︰</span><span class="sxs-lookup"><span data-stu-id="15d7e-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="15d7e-169">至少有兩個介面已啟用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="15d7e-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="15d7e-170">兩個介面會在您的 StorSimple 裝置上啟用 iSCSI tooverify 執行 hello hello StorSimple 裝置的 Azure 傳統入口網站中所述步驟：</span><span class="sxs-lookup"><span data-stu-id="15d7e-170">tooverify that two interfaces are iSCSI-enabled on your StorSimple device, perform hello following steps in hello Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="15d7e-171">登入您的 StorSimple 裝置 hello 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="15d7e-171">Log into hello classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="15d7e-172">選取您的 StorSimple Manager 服務，請按一下**裝置**選擇 hello 特定 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="15d7e-172">Select your StorSimple Manager service, click **Devices** and choose hello specific StorSimple device.</span></span> <span data-ttu-id="15d7e-173">按一下**設定**和確認 hello 網路介面設定。</span><span class="sxs-lookup"><span data-stu-id="15d7e-173">Click **Configure** and verify hello network interface settings.</span></span> <span data-ttu-id="15d7e-174">下面顯示的螢幕擷取畫面包含已啟用 iSCSI 的兩個網路介面。</span><span class="sxs-lookup"><span data-stu-id="15d7e-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="15d7e-175">以下 DATA 2 和 DATA 3 兩個 10 GbE 介面都已啟用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="15d7e-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![MPIO StorSimple DATA 2 設定](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple DATA 3 設定](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="15d7e-178">在 hello**設定**頁面</span><span class="sxs-lookup"><span data-stu-id="15d7e-178">In hello **Configure** page</span></span>
     
     1. <span data-ttu-id="15d7e-179">確定這兩個網路介面都已啟用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="15d7e-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="15d7e-180">hello**具備 iSCSI 功能**欄位應該設定太**是**。</span><span class="sxs-lookup"><span data-stu-id="15d7e-180">hello **iSCSI enabled** field should be set too**Yes**.</span></span>
     2. <span data-ttu-id="15d7e-181">請確定 hello 網路介面有 hello 相同的速度，都應該是 1 GbE 或 10 GbE。</span><span class="sxs-lookup"><span data-stu-id="15d7e-181">Ensure that hello network interfaces have hello same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="15d7e-182">請注意 hello IPv4 位址的 hello iSCSI 啟用的介面，並儲存供稍後使用 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="15d7e-182">Note hello IPv4 addresses of hello iSCSI-enabled interfaces and save for later use on hello host.</span></span>
* <span data-ttu-id="15d7e-183">應該從 hello CentOS 伺服器 hello StorSimple 裝置上的 iSCSI 介面。</span><span class="sxs-lookup"><span data-stu-id="15d7e-183">hello iSCSI interfaces on your StorSimple device should be reachable from hello CentOS server.</span></span>
      <span data-ttu-id="15d7e-184">tooverify，您必須在主機伺服器上的 tooprovide hello IP 位址，您的 StorSimple iSCSI 的網路介面。</span><span class="sxs-lookup"><span data-stu-id="15d7e-184">tooverify this, you need tooprovide hello IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="15d7e-185">hello 所使用的命令和 hello DATA2 與對應的輸出 (10.126.162.25) 和 DATA3 (10.126.162.26) 如下所示：</span><span class="sxs-lookup"><span data-stu-id="15d7e-185">hello commands used and hello corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="15d7e-186">硬體組態</span><span class="sxs-lookup"><span data-stu-id="15d7e-186">Hardware configuration</span></span>
<span data-ttu-id="15d7e-187">我們建議您連接 hello 兩個 iSCSI 網路介面上不同的路徑，以獲得備援。</span><span class="sxs-lookup"><span data-stu-id="15d7e-187">We recommend that you connect hello two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="15d7e-188">hello 圖顯示 hello 建議的硬體組態的高可用性和負載平衡 CentOS 伺服器和 StorSimple 裝置的多重路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-188">hello figure below shows hello recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![StorSimple tooLinux 主機的 MPIO 硬體設定](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="15d7e-190">Hello 前圖所示：</span><span class="sxs-lookup"><span data-stu-id="15d7e-190">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="15d7e-191">StorSimple 裝置處於具有兩個控制器的主動-被動組態中。</span><span class="sxs-lookup"><span data-stu-id="15d7e-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="15d7e-192">兩個 SAN 交換器會連接的 tooyour 裝置控制器。</span><span class="sxs-lookup"><span data-stu-id="15d7e-192">Two SAN switches are connected tooyour device controllers.</span></span>
* <span data-ttu-id="15d7e-193">兩個 iSCSI 啟動器會在 StorSimple 裝置上啟用。</span><span class="sxs-lookup"><span data-stu-id="15d7e-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="15d7e-194">CentOS 主機已啟用 2 個網路介面。</span><span class="sxs-lookup"><span data-stu-id="15d7e-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="15d7e-195">如果 hello 主應用程式和資料的介面為可路由傳送，上述組態的 hello 會產生您裝置和 hello 主機之間的 4 個不同的路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-195">hello above configuration will yield 4 separate paths between your device and hello host if hello host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="15d7e-196">建議您不要對多重路徑功能混合使用 1 GbE 與 10 GbE 網路介面。</span><span class="sxs-lookup"><span data-stu-id="15d7e-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="15d7e-197">使用兩個網路介面，這兩個 hello 介面應該 hello 相同型別。</span><span class="sxs-lookup"><span data-stu-id="15d7e-197">When using two network interfaces, both hello interfaces should be hello identical type.</span></span>
> * <span data-ttu-id="15d7e-198">在您的 StorSimple 裝置上，DATA0、DATA1、DATA4 和 DATA5 為 1 GbE 介面，而 DATA2 和 DATA3 則為 10 GbE 網路介面。</span><span class="sxs-lookup"><span data-stu-id="15d7e-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="15d7e-199">組態步驟</span><span class="sxs-lookup"><span data-stu-id="15d7e-199">Configuration steps</span></span>
<span data-ttu-id="15d7e-200">多重路徑的 hello 組態步驟將包含設定自動探索，指定 hello 負載平衡演算法 toouse，啟用多重路徑及最後驗證 hello 組態 hello 可用的路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-200">hello configuration steps for multipathing involve configuring hello available paths for automatic discovery, specifying hello load-balancing algorithm toouse, enabling multipathing and finally verifying hello configuration.</span></span> <span data-ttu-id="15d7e-201">每個步驟是在 hello 下列各節中詳細討論。</span><span class="sxs-lookup"><span data-stu-id="15d7e-201">Each of these steps is discussed in detail in hello following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="15d7e-202">步驟 1：為自動探索設定多重路徑</span><span class="sxs-lookup"><span data-stu-id="15d7e-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="15d7e-203">hello 多重路徑支援的裝置可以自動探索並設定。</span><span class="sxs-lookup"><span data-stu-id="15d7e-203">hello multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="15d7e-204">初始化 `/etc/multipath.conf` 檔案。</span><span class="sxs-lookup"><span data-stu-id="15d7e-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="15d7e-205">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="15d7e-206">hello 上述命令會建立`sample/etc/multipath.conf`檔案。</span><span class="sxs-lookup"><span data-stu-id="15d7e-206">hello above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="15d7e-207">啟動多重路徑服務。</span><span class="sxs-lookup"><span data-stu-id="15d7e-207">Start multipath service.</span></span> <span data-ttu-id="15d7e-208">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="15d7e-209">您會看到下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="15d7e-209">You will see hello following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="15d7e-210">啟用多重路徑的自動探索。</span><span class="sxs-lookup"><span data-stu-id="15d7e-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="15d7e-211">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="15d7e-212">這將會修改預設值區段 hello 您`multipath.conf`如下所示：</span><span class="sxs-lookup"><span data-stu-id="15d7e-212">This will modify hello defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="15d7e-213">步驟 2：為 StorSimple 磁碟區設定多重路徑</span><span class="sxs-lookup"><span data-stu-id="15d7e-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="15d7e-214">根據預設，所有的裝置會黑色 hello multipath.conf 檔案中所列，並將被略過。</span><span class="sxs-lookup"><span data-stu-id="15d7e-214">By default, all devices are black listed in hello multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="15d7e-215">您必須從 StorSimple 裝置的磁碟區 toocreate 黑名單例外狀況 tooallow 多重路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-215">You will need toocreate blacklist exceptions tooallow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="15d7e-216">編輯 hello`/etc/mulitpath.conf`檔案。</span><span class="sxs-lookup"><span data-stu-id="15d7e-216">Edit hello `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="15d7e-217">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="15d7e-218">Hello multipath.conf 檔案中，找出 hello blacklist_exceptions 區段。</span><span class="sxs-lookup"><span data-stu-id="15d7e-218">Locate hello blacklist_exceptions section in hello multipath.conf file.</span></span> <span data-ttu-id="15d7e-219">您的 StorSimple 裝置需要 toobe 列為黑名單例外，這一節。</span><span class="sxs-lookup"><span data-stu-id="15d7e-219">Your StorSimple device needs toobe listed as a blacklist exception in this section.</span></span> <span data-ttu-id="15d7e-220">您可以取消註解相關程式碼行中此檔案 toomodify 它 （使用僅限 hello 特定模型的 hello 您使用的裝置） 如下所示：</span><span class="sxs-lookup"><span data-stu-id="15d7e-220">You can uncomment relevant lines in this file toomodify it as shown below (use only hello specific model of hello device you are using):</span></span>
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="15d7e-221">步驟 3：設定循環配置資源多重路徑</span><span class="sxs-lookup"><span data-stu-id="15d7e-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="15d7e-222">此負載平衡演算法會使用所有 hello 可用 multipaths toohello 主動控制站以平衡且循環配置資源的方式。</span><span class="sxs-lookup"><span data-stu-id="15d7e-222">This load-balancing algorithm uses all hello available multipaths toohello active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="15d7e-223">編輯 hello`/etc/multipath.conf`檔案。</span><span class="sxs-lookup"><span data-stu-id="15d7e-223">Edit hello `/etc/multipath.conf` file.</span></span> <span data-ttu-id="15d7e-224">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="15d7e-225">在 hello`defaults`區段，集合 hello`path_grouping_policy`太`multibus`。</span><span class="sxs-lookup"><span data-stu-id="15d7e-225">Under hello `defaults` section, set hello `path_grouping_policy` too`multibus`.</span></span> <span data-ttu-id="15d7e-226">hello`path_grouping_policy`指定 hello 預設路徑群組原則 tooapply toounspecified multipaths。</span><span class="sxs-lookup"><span data-stu-id="15d7e-226">hello `path_grouping_policy` specifies hello default path grouping policy tooapply toounspecified multipaths.</span></span> <span data-ttu-id="15d7e-227">hello 預設值區段看起來如下所示。</span><span class="sxs-lookup"><span data-stu-id="15d7e-227">hello defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="15d7e-228">hello 的最常見的值`path_grouping_policy`包括：</span><span class="sxs-lookup"><span data-stu-id="15d7e-228">hello most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="15d7e-229">failover = 每一個優先順序群組 1 個路徑</span><span class="sxs-lookup"><span data-stu-id="15d7e-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="15d7e-230">multibus = 1 個優先順序群組中的所有有效路徑</span><span class="sxs-lookup"><span data-stu-id="15d7e-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="15d7e-231">步驟 4：啟用多重路徑</span><span class="sxs-lookup"><span data-stu-id="15d7e-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="15d7e-232">重新啟動 hello`multipathd`服務精靈。</span><span class="sxs-lookup"><span data-stu-id="15d7e-232">Restart hello `multipathd` daemon.</span></span> <span data-ttu-id="15d7e-233">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="15d7e-234">hello 輸出將會如下所示：</span><span class="sxs-lookup"><span data-stu-id="15d7e-234">hello output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="15d7e-235">步驟 5：驗證多重路徑</span><span class="sxs-lookup"><span data-stu-id="15d7e-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="15d7e-236">先確定的 iSCSI 連線建立 hello StorSimple 裝置，如下所示：</span><span class="sxs-lookup"><span data-stu-id="15d7e-236">First make sure that iSCSI connection is established with hello StorSimple device as follows:</span></span>
   
   <span data-ttu-id="15d7e-237">a.</span><span class="sxs-lookup"><span data-stu-id="15d7e-237">a.</span></span> <span data-ttu-id="15d7e-238">探索您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="15d7e-238">Discover your StorSimple device.</span></span> <span data-ttu-id="15d7e-239">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="15d7e-240">當 DATA0 IP 位址是 10.126.162.25 和輸出的 iSCSI 流量的 hello StorSimple 裝置上開啟連接埠 3260 hello 輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="15d7e-240">hello output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on hello StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="15d7e-241">複製 hello 您 StorSimple 裝置的 IQN `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`，從上述輸出中的 hello。</span><span class="sxs-lookup"><span data-stu-id="15d7e-241">Copy hello IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from hello preceding output.</span></span>

   <span data-ttu-id="15d7e-242">b.</span><span class="sxs-lookup"><span data-stu-id="15d7e-242">b.</span></span> <span data-ttu-id="15d7e-243">使用目標 IQN toohello 裝置連線。</span><span class="sxs-lookup"><span data-stu-id="15d7e-243">Connect toohello device using target IQN.</span></span> <span data-ttu-id="15d7e-244">hello StorSimple 裝置在 hello iSCSI 目標。</span><span class="sxs-lookup"><span data-stu-id="15d7e-244">hello StorSimple device is hello iSCSI target here.</span></span> <span data-ttu-id="15d7e-245">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="15d7e-246">hello 下列範例顯示輸出與目標 IQN 的`iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`。</span><span class="sxs-lookup"><span data-stu-id="15d7e-246">hello following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="15d7e-247">hello 輸出會指出您已成功在裝置上連線 toohello 兩個已啟用 iSCSI 的網路介面。</span><span class="sxs-lookup"><span data-stu-id="15d7e-247">hello output indicates that you have successfully connected toohello two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="15d7e-248">如果您看到只有一部主機的介面和以下兩個路徑，則您需要 tooenable 這兩個主機上的 hello 介面供 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="15d7e-248">If you see only one host interface and two paths here, then you need tooenable both hello interfaces on host for iSCSI.</span></span> <span data-ttu-id="15d7e-249">您可以依照 hello[詳細 Linux 文件中的指示](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html)。</span><span class="sxs-lookup"><span data-stu-id="15d7e-249">You can follow hello [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="15d7e-250">磁碟區是公開的 toohello CentOS 伺服器 hello 的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="15d7e-250">A volume is exposed toohello CentOS server from hello StorSimple device.</span></span> <span data-ttu-id="15d7e-251">如需詳細資訊，請參閱[步驟 6： 建立磁碟區](storsimple-deployment-walkthrough.md#step-6-create-a-volume)透過 hello StorSimple 裝置上的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="15d7e-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="15d7e-252">請確認 hello 可用的路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-252">Verify hello available paths.</span></span> <span data-ttu-id="15d7e-253">輸入：</span><span class="sxs-lookup"><span data-stu-id="15d7e-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="15d7e-254">hello 下列範例會顯示兩個網路介面的 hello 輸出在 StorSimple 裝置連線的 tooa 單一主機網路介面上使用兩個可用的路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-254">hello following example shows hello output for two network interfaces on a StorSimple device connected tooa single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="15d7e-255">多重路徑疑難排解</span><span class="sxs-lookup"><span data-stu-id="15d7e-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="15d7e-256">如果您在多重路徑設定期間遇到任何問題，請參閱本節所提供的一些實用秘訣。</span><span class="sxs-lookup"><span data-stu-id="15d7e-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="15d7e-257">問：</span><span class="sxs-lookup"><span data-stu-id="15d7e-257">Q.</span></span> <span data-ttu-id="15d7e-258">我看不到中的 hello 變更`multipath.conf`生效的檔案。</span><span class="sxs-lookup"><span data-stu-id="15d7e-258">I do not see hello changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="15d7e-259">A.</span><span class="sxs-lookup"><span data-stu-id="15d7e-259">A.</span></span> <span data-ttu-id="15d7e-260">如果您進行了任何變更 toohello`multipath.conf`檔案中，您將需要 toorestart hello 多重路徑服務。</span><span class="sxs-lookup"><span data-stu-id="15d7e-260">If you have made any changes toohello `multipath.conf` file, you will need toorestart hello multipathing service.</span></span> <span data-ttu-id="15d7e-261">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="15d7e-261">Type hello following command:</span></span>

    service multipathd restart

<span data-ttu-id="15d7e-262">問：</span><span class="sxs-lookup"><span data-stu-id="15d7e-262">Q.</span></span> <span data-ttu-id="15d7e-263">我已啟用 hello StorSimple 裝置上的兩個網路介面和 hello 主機上的兩個網路介面。</span><span class="sxs-lookup"><span data-stu-id="15d7e-263">I have enabled two network interfaces on hello StorSimple device and two network interfaces on hello host.</span></span> <span data-ttu-id="15d7e-264">當我列出 hello 可用的路徑時，請看只有兩個路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-264">When I list hello available paths, I see only two paths.</span></span> <span data-ttu-id="15d7e-265">我所期望 toosee 四個可用的路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-265">I expected toosee four available paths.</span></span>

<span data-ttu-id="15d7e-266">A.</span><span class="sxs-lookup"><span data-stu-id="15d7e-266">A.</span></span> <span data-ttu-id="15d7e-267">確定 hello 兩個路徑都在 hello 上相同的子網路和路由傳送。</span><span class="sxs-lookup"><span data-stu-id="15d7e-267">Make sure that hello two paths are on hello same subnet and routable.</span></span> <span data-ttu-id="15d7e-268">如果 hello 網路介面位於不同的 Vlan，且無法路由傳送，您會看到只有兩個路徑。</span><span class="sxs-lookup"><span data-stu-id="15d7e-268">If hello network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="15d7e-269">其中一種方式 tooverify 這是 toomake 確定可連線從 hello StorSimple 裝置上的網路介面的這兩個 hello 主機介面。</span><span class="sxs-lookup"><span data-stu-id="15d7e-269">One way tooverify this is toomake sure that you can reach both hello host interfaces from a network interface on hello StorSimple device.</span></span> <span data-ttu-id="15d7e-270">您必須太[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)為這項驗證僅可透過支援工作階段。</span><span class="sxs-lookup"><span data-stu-id="15d7e-270">You will need too[contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="15d7e-271">問：</span><span class="sxs-lookup"><span data-stu-id="15d7e-271">Q.</span></span> <span data-ttu-id="15d7e-272">當我列出可用的路徑時，我看不到任何輸出。</span><span class="sxs-lookup"><span data-stu-id="15d7e-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="15d7e-273">A.</span><span class="sxs-lookup"><span data-stu-id="15d7e-273">A.</span></span> <span data-ttu-id="15d7e-274">一般而言，看不到任何多重路徑的路徑建議問題與 hello 多重路徑精靈，並最有可能是任何在此處的問題在於 hello`multipath.conf`檔案。</span><span class="sxs-lookup"><span data-stu-id="15d7e-274">Typically, not seeing any multipathed paths suggests a problem with hello multipathing daemon, and it’s most likely that any problem here lies in hello `multipath.conf` file.</span></span>

<span data-ttu-id="15d7e-275">也很值得，就可以看到某些磁碟連接 toohello 目標之後為無回應 hello 多重路徑清單也可能表示您不需要任何磁碟。</span><span class="sxs-lookup"><span data-stu-id="15d7e-275">It would also be worth checking that you can actually see some disks after connecting toohello target, as no response from hello multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="15d7e-276">使用下列命令 toorescan hello SCSI 匯流排的 hello:</span><span class="sxs-lookup"><span data-stu-id="15d7e-276">Use hello following command toorescan hello SCSI bus:</span></span>
  
    <span data-ttu-id="15d7e-277">`$ rescan-scsi-bus.sh ` (屬於 sg3_utils 封包)</span><span class="sxs-lookup"><span data-stu-id="15d7e-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="15d7e-278">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="15d7e-278">Type hello following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="15d7e-279">或</span><span class="sxs-lookup"><span data-stu-id="15d7e-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="15d7e-280">這些將傳回最近新增磁碟的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="15d7e-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="15d7e-281">toodetermine 是否 StorSimple 磁碟時，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="15d7e-281">toodetermine whether it is a StorSimple disk, use hello following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="15d7e-282">這會傳回一個字串，判斷它是否為 StorSimple 磁碟。</span><span class="sxs-lookup"><span data-stu-id="15d7e-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="15d7e-283">有一個比較不可能的可能原因也可能是 iscsid pid 過時。</span><span class="sxs-lookup"><span data-stu-id="15d7e-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="15d7e-284">使用 hello iSCSI 工作階段中的下列關閉的命令 toolog hello:</span><span class="sxs-lookup"><span data-stu-id="15d7e-284">Use hello following command toolog off from hello iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="15d7e-285">重複此命令在 hello iSCSI 目標，也就是您的 StorSimple 裝置上的所有連接的 hello 網路介面。</span><span class="sxs-lookup"><span data-stu-id="15d7e-285">Repeat this command for all hello connected network interfaces on hello iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="15d7e-286">一旦您已登出所有 hello iSCSI 工作階段，請使用 hello iSCSI 目標 IQN tooreestablish hello iSCSI 工作階段。</span><span class="sxs-lookup"><span data-stu-id="15d7e-286">Once you have logged off from all hello iSCSI sessions, use hello iSCSI target IQN tooreestablish hello iSCSI session.</span></span> <span data-ttu-id="15d7e-287">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="15d7e-287">Type hello following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="15d7e-288">問：</span><span class="sxs-lookup"><span data-stu-id="15d7e-288">Q.</span></span> <span data-ttu-id="15d7e-289">我不確定我的裝置是否已列入允許清單。</span><span class="sxs-lookup"><span data-stu-id="15d7e-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="15d7e-290">A.</span><span class="sxs-lookup"><span data-stu-id="15d7e-290">A.</span></span> <span data-ttu-id="15d7e-291">tooverify 您的裝置是否在允許清單中，使用下列疑難排解互動式命令 hello:</span><span class="sxs-lookup"><span data-stu-id="15d7e-291">tooverify whether your device is whitelisted, use hello following troubleshooting interactive command:</span></span>

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


<span data-ttu-id="15d7e-292">如需詳細資訊，請移至太[使用多重路徑的互動式命令進行疑難排解](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html)。</span><span class="sxs-lookup"><span data-stu-id="15d7e-292">For more information, go too[use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="15d7e-293">有用的命令清單</span><span class="sxs-lookup"><span data-stu-id="15d7e-293">List of useful commands</span></span>
| <span data-ttu-id="15d7e-294">在系統提示您進行確認時，輸入 </span><span class="sxs-lookup"><span data-stu-id="15d7e-294">Type</span></span> | <span data-ttu-id="15d7e-295">命令</span><span class="sxs-lookup"><span data-stu-id="15d7e-295">Command</span></span> | <span data-ttu-id="15d7e-296">說明</span><span class="sxs-lookup"><span data-stu-id="15d7e-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15d7e-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="15d7e-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="15d7e-298">啟動 iSCSI 服務</span><span class="sxs-lookup"><span data-stu-id="15d7e-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="15d7e-299">停止 iSCSI 服務</span><span class="sxs-lookup"><span data-stu-id="15d7e-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="15d7e-300">重新啟動 iSCSI 服務</span><span class="sxs-lookup"><span data-stu-id="15d7e-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="15d7e-301">探索在指定的 hello 上可用的目標位址</span><span class="sxs-lookup"><span data-stu-id="15d7e-301">Discover available targets on hello specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="15d7e-302">登入 toohello iSCSI 目標</span><span class="sxs-lookup"><span data-stu-id="15d7e-302">Log in toohello iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="15d7e-303">登出 hello iSCSI 目標</span><span class="sxs-lookup"><span data-stu-id="15d7e-303">Log out from hello iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="15d7e-304">列印 iSCSI 啟動器名稱</span><span class="sxs-lookup"><span data-stu-id="15d7e-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="15d7e-305">請檢查 hello hello iSCSI 工作階段與 hello 主機上探索到的磁碟區的狀態</span><span class="sxs-lookup"><span data-stu-id="15d7e-305">Check hello state of hello iSCSI session and volume discovered on hello host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="15d7e-306">顯示所有 hello 主機與 hello StorSimple 裝置之間建立的 hello iSCSI 工作階段</span><span class="sxs-lookup"><span data-stu-id="15d7e-306">Shows all hello iSCSI sessions established between hello host and hello StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="15d7e-307">**多重路徑**</span><span class="sxs-lookup"><span data-stu-id="15d7e-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="15d7e-308">啟動多重路徑 daemon</span><span class="sxs-lookup"><span data-stu-id="15d7e-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="15d7e-309">停止多重路徑 daemon</span><span class="sxs-lookup"><span data-stu-id="15d7e-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="15d7e-310">重新啟動多重路徑 daemon</span><span class="sxs-lookup"><span data-stu-id="15d7e-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="15d7e-311">或</span><span class="sxs-lookup"><span data-stu-id="15d7e-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="15d7e-312">在開機時啟用多重路徑精靈 toostart</span><span class="sxs-lookup"><span data-stu-id="15d7e-312">Enable multipath daemon toostart at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="15d7e-313">啟動 hello 互動式主控台進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="15d7e-313">Start hello interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="15d7e-314">列出多重路徑連接和裝置</span><span class="sxs-lookup"><span data-stu-id="15d7e-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="15d7e-315">在 `/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="15d7e-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="15d7e-316">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15d7e-316">Next steps</span></span>
<span data-ttu-id="15d7e-317">當您要在 Linux 主機上設定 MPIO，您可能也需要 toorefer toohello 遵循 CentoS 6.6 文件：</span><span class="sxs-lookup"><span data-stu-id="15d7e-317">As you are configuring MPIO on Linux host, you may also need toorefer toohello following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="15d7e-318">在 CentOS 上設定 MPIO</span><span class="sxs-lookup"><span data-stu-id="15d7e-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="15d7e-319">Linux 訓練指南</span><span class="sxs-lookup"><span data-stu-id="15d7e-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

