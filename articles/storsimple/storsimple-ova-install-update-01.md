---
title: "在 StorSimple Virtual Array 上安裝更新 | Microsoft Docs"
description: "描述如何透過 StorSimple Virtual Array Web UI，使用入口網站和 Hotfix 方法套用更新"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: bccb0d49c1959a690d513961c32d946763385a87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="b57d6-103">在 StorSimple Virtual Array 上安裝更新</span><span class="sxs-lookup"><span data-stu-id="b57d6-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="b57d6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b57d6-104">Overview</span></span>
<span data-ttu-id="b57d6-105">本文說明透過本機 Web UI 和透過 Azure 傳統入口網站，在 StorSimple Virtual Array 上安裝更新時所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="b57d6-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure classic portal.</span></span> <span data-ttu-id="b57d6-106">您需要套用軟體更新或 Hotfix，以便讓您的 StorSimple Virtual Array 保持在最新狀態。</span><span class="sxs-lookup"><span data-stu-id="b57d6-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="b57d6-107">請記住，安裝更新或 Hotfix 會重新啟動您的裝置。</span><span class="sxs-lookup"><span data-stu-id="b57d6-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="b57d6-108">假設 StorSimple Virtual Array 是單一節點裝置，就會中斷任何進行中的 I/O，裝置也會停機。</span><span class="sxs-lookup"><span data-stu-id="b57d6-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="b57d6-109">套用更新之前，建議您先讓主機上的磁碟區或共用離線，再讓裝置離線。</span><span class="sxs-lookup"><span data-stu-id="b57d6-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="b57d6-110">這樣可以讓資料損毀的可能性降至最低。</span><span class="sxs-lookup"><span data-stu-id="b57d6-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b57d6-111">如果您正在執行 Update 0.1 或 GA 軟體版本，您就必須透過本機 Web UI 使用 Hotfix 方法來安裝 Update 0.3。</span><span class="sxs-lookup"><span data-stu-id="b57d6-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="b57d6-112">如果您執行的是 Update 0.2，建議您透過 Azure 傳統入口網站安裝更新。</span><span class="sxs-lookup"><span data-stu-id="b57d6-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
> 
> 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="b57d6-113">使用本機 Web UI</span><span class="sxs-lookup"><span data-stu-id="b57d6-113">Use the local web UI</span></span>
<span data-ttu-id="b57d6-114">使用本機 Web UI 時有兩個步驟︰</span><span class="sxs-lookup"><span data-stu-id="b57d6-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="b57d6-115">下載更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="b57d6-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="b57d6-116">安裝更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="b57d6-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="b57d6-117">下載更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="b57d6-117">Download the update or the hotfix</span></span>
<span data-ttu-id="b57d6-118">請執行下列步驟，從 Microsoft Update Catalog 下載軟體更新。</span><span class="sxs-lookup"><span data-stu-id="b57d6-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="b57d6-119">下載更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="b57d6-119">To download the update or the hotfix</span></span>
1. <span data-ttu-id="b57d6-120">啟動 Internet Explorer 並瀏覽至 [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="b57d6-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="b57d6-121">如果這是您第一次在此電腦上使用 Microsoft Update Catalog，請在系統提示您安裝 Microsoft Update Catalog 附加元件時，按一下 [安裝]  。</span><span class="sxs-lookup"><span data-stu-id="b57d6-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="b57d6-122">在 Microsoft Update Catalog 的搜尋方塊中，輸入您要下載的 Hotfix 知識庫 (KB) 編號。</span><span class="sxs-lookup"><span data-stu-id="b57d6-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="b57d6-123">輸入 **3182061** (適用於 Update 0.3)，然後按一下 [搜尋]。</span><span class="sxs-lookup"><span data-stu-id="b57d6-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="b57d6-124">此時會顯示 Hotfix 清單，例如 **StorSimple Virtual Array Update 0.3**。</span><span class="sxs-lookup"><span data-stu-id="b57d6-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![搜尋目錄](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="b57d6-126">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="b57d6-126">Click **Add**.</span></span> <span data-ttu-id="b57d6-127">更新便會新增到購物籃中。</span><span class="sxs-lookup"><span data-stu-id="b57d6-127">The update is added to the basket.</span></span>
5. <span data-ttu-id="b57d6-128">按一下 [ **檢視購物籃**]。</span><span class="sxs-lookup"><span data-stu-id="b57d6-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="b57d6-129">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="b57d6-129">Click **Download**.</span></span> <span data-ttu-id="b57d6-130">指定或「瀏覽」  至您想要儲存下載項目的本機位置。</span><span class="sxs-lookup"><span data-stu-id="b57d6-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="b57d6-131">更新便會下載到指定的位置，並放在與更新名稱相同的子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="b57d6-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="b57d6-132">資料夾也可以複製到裝置可連線的網路共用位置。</span><span class="sxs-lookup"><span data-stu-id="b57d6-132">The folder can also be copied to a network share that is reachable from the device.</span></span>
7. <span data-ttu-id="b57d6-133">開啟已複製的資料夾，您應該會看到 Microsoft Update 獨立封裝檔案 `WindowsTH-KB3011067-x64`。</span><span class="sxs-lookup"><span data-stu-id="b57d6-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="b57d6-134">此檔案是用來安裝更新或 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="b57d6-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="b57d6-135">安裝更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="b57d6-135">Install the update or the hotfix</span></span>
<span data-ttu-id="b57d6-136">安裝更新或 Hotfix 之前，請確定更新或 Hotfix 已下載至您主機的本機上，或是可透過網路共用存取。</span><span class="sxs-lookup"><span data-stu-id="b57d6-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="b57d6-137">請使用此方法在執行 GA 或 Update 0.1 軟體版本的裝置上安裝更新。</span><span class="sxs-lookup"><span data-stu-id="b57d6-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="b57d6-138">此程序需時不到 2 分鐘。</span><span class="sxs-lookup"><span data-stu-id="b57d6-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="b57d6-139">請執行下列步驟以安裝更新或 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="b57d6-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="b57d6-140">安裝更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="b57d6-140">To install the update or the hotfix</span></span>
1. <span data-ttu-id="b57d6-141">在本機 Web UI 中，移至 [維護]  >  [軟體更新]。</span><span class="sxs-lookup"><span data-stu-id="b57d6-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![更新裝置](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="b57d6-143">在 [更新檔案路徑] 中，輸入更新或 Hotfix 的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="b57d6-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="b57d6-144">如果更新或 Hotfix 的安裝檔案是放在網路共用上，您也可以瀏覽至該檔案。</span><span class="sxs-lookup"><span data-stu-id="b57d6-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="b57d6-145">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="b57d6-145">Click **Apply**.</span></span>
   
    ![更新裝置](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="b57d6-147">此時會顯示警告。</span><span class="sxs-lookup"><span data-stu-id="b57d6-147">A warning is displayed.</span></span> <span data-ttu-id="b57d6-148">如果這是單一節點裝置，在套用更新後，裝置就會重新啟動而會有停機時間。</span><span class="sxs-lookup"><span data-stu-id="b57d6-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="b57d6-149">按一下核取圖示。</span><span class="sxs-lookup"><span data-stu-id="b57d6-149">Click the check icon.</span></span>
   
   ![更新裝置](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="b57d6-151">更新會開始進行。</span><span class="sxs-lookup"><span data-stu-id="b57d6-151">The update starts.</span></span> <span data-ttu-id="b57d6-152">成功更新裝置之後，裝置就會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="b57d6-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="b57d6-153">在這段持續時間會無法存取本機 UI。</span><span class="sxs-lookup"><span data-stu-id="b57d6-153">The local UI is not accessible in this duration.</span></span>
   
    ![更新裝置](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="b57d6-155">重新啟動完成後，您就會進入 [登入] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b57d6-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="b57d6-156">若要確認裝置軟體是否已更新，請在本機 Web UI 中，移至 [維護]  >  [軟體更新]。</span><span class="sxs-lookup"><span data-stu-id="b57d6-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="b57d6-157">顯示的軟體版本應該是 **10.0.0.0.0.10288.0** (適用於 Update 0.3)。</span><span class="sxs-lookup"><span data-stu-id="b57d6-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b57d6-158">我們在本機 Web UI 和 Azure 傳統入口網站中回報軟體版本的方式略有不同。</span><span class="sxs-lookup"><span data-stu-id="b57d6-158">We report the software versions in a slightly different way in the local web UI and the Azure classic portal.</span></span> <span data-ttu-id="b57d6-159">例如，本機 Web UI 會回報 **10.0.0.0.0.10288**，而相同版本在 Azure 傳統入口網站則會回報為 **10.0.10288.0**。</span><span class="sxs-lookup"><span data-stu-id="b57d6-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure classic portal reports **10.0.10288.0** for the same version.</span></span> 
   > 
   > 
   
    ![更新裝置](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="b57d6-161">使用 Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="b57d6-161">Use the Azure classic portal</span></span>
<span data-ttu-id="b57d6-162">如果執行 Update 0.2，建議您透過 Azure 傳統入口網站安裝更新。</span><span class="sxs-lookup"><span data-stu-id="b57d6-162">If running Update 0.2, we recommend that you install updates through the Azure classic portal.</span></span> <span data-ttu-id="b57d6-163">入口網站的程序需要使用者掃描、下載然後安裝更新。</span><span class="sxs-lookup"><span data-stu-id="b57d6-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="b57d6-164">此程序需要大約 7 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="b57d6-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="b57d6-165">請執行下列步驟以安裝更新或 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="b57d6-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="b57d6-166">安裝完成後 (以作業狀態 100% 表示)，請移至 [裝置] > [維護] > [軟體更新]。</span><span class="sxs-lookup"><span data-stu-id="b57d6-166">After the installation is complete (as indicated by job status at 100 %), go to **Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="b57d6-167">顯示的軟體版本應該是 10.0.10288.0。</span><span class="sxs-lookup"><span data-stu-id="b57d6-167">The displayed software version should be 10.0.10288.0.</span></span>

![更新裝置](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="b57d6-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b57d6-169">Next steps</span></span>
<span data-ttu-id="b57d6-170">深入了解 [administering your StorSimple Virtual Array (管理 StorSimple Virtual Array)](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="b57d6-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

