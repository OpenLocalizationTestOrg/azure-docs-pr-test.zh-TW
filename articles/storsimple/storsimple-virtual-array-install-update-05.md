---
title: "在 StorSimple Virtual Array 上安裝 Update 0.5 | Microsoft Docs"
description: "描述如何透過 StorSimple Virtual Array Web UI，使用 Azure 入口網站和 Hotfix 方法套用更新"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c47da5b90c16e2d5b5709e2a6affc026238b9468
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="98af1-103">在 StorSimple Virtual Array 上安裝 Update 0.5</span><span class="sxs-lookup"><span data-stu-id="98af1-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="98af1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="98af1-104">Overview</span></span>

<span data-ttu-id="98af1-105">此文章說明透過本機 Web UI 和透過 Azure 入口網站在 StorSimple Virtual Array 上安裝 Update 0.5 時所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="98af1-105">This article describes the steps required to install Update 0.5 on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="98af1-106">您需要套用軟體更新或 Hotfix，以便讓您的 StorSimple Virtual Array 保持在最新狀態。</span><span class="sxs-lookup"><span data-stu-id="98af1-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="98af1-107">套用更新之前，建議您先讓主機上的磁碟區或共用離線，再讓裝置離線。</span><span class="sxs-lookup"><span data-stu-id="98af1-107">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="98af1-108">這樣可以讓資料損毀的可能性降至最低。</span><span class="sxs-lookup"><span data-stu-id="98af1-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="98af1-109">磁碟區或共用離線之後，您也應該手動備份裝置。</span><span class="sxs-lookup"><span data-stu-id="98af1-109">After the volumes or shares are offline, you should also take a manual backup of the device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="98af1-110">Update 0.5 對應至您裝置上的 10.0.10290.0 軟體版本。</span><span class="sxs-lookup"><span data-stu-id="98af1-110">Update 0.5 corresponds to **10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="98af1-111">如需此更新中新功能的資訊，請移至 [Update 0.5 的版本資訊 (英文)](storsimple-virtual-array-update-05-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="98af1-111">For information on what is new in this update, go to [Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="98af1-112">如果您執行的是 Update 0.2 或更新版本，建議您透過 Azure 入口網站安裝更新。</span><span class="sxs-lookup"><span data-stu-id="98af1-112">If you are running Update 0.2 or later, we recommend that you install the updates via the Azure portal.</span></span> <span data-ttu-id="98af1-113">如果您正在執行 Update 0.1 或 GA 軟體版本，您就必須透過本機 Web UI 使用 Hotfix 方法來安裝 Update 0.5。</span><span class="sxs-lookup"><span data-stu-id="98af1-113">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install Update 0.5.</span></span>
>
> - <span data-ttu-id="98af1-114">請記住，安裝更新或 Hotfix 會重新啟動您的裝置。</span><span class="sxs-lookup"><span data-stu-id="98af1-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="98af1-115">假設 StorSimple Virtual Array 是單一節點裝置，就會中斷任何進行中的 I/O，裝置也會停機。</span><span class="sxs-lookup"><span data-stu-id="98af1-115">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="98af1-116">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="98af1-116">Use the Azure portal</span></span>

<span data-ttu-id="98af1-117">如果執行 Update 0.2 或更新版本，建議您透過 Azure 入口網站安裝更新。</span><span class="sxs-lookup"><span data-stu-id="98af1-117">If running Update 0.2 and later, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="98af1-118">入口網站的程序需要使用者掃描、下載然後安裝更新。</span><span class="sxs-lookup"><span data-stu-id="98af1-118">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="98af1-119">此程序需要大約 7 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="98af1-119">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="98af1-120">請執行下列步驟以安裝更新或 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="98af1-120">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="98af1-121">安裝完成後，請移至 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="98af1-121">After the installation is complete, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="98af1-122">選取 [裝置]，然後選取並按一下您剛剛更新的裝置。</span><span class="sxs-lookup"><span data-stu-id="98af1-122">Select **Devices** and then select and click the device you just updated.</span></span> <span data-ttu-id="98af1-123">移至 [設定] > [管理] > [裝置更新]。</span><span class="sxs-lookup"><span data-stu-id="98af1-123">Go to **Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="98af1-124">顯示的軟體版本應該是 10.0.10290.0。</span><span class="sxs-lookup"><span data-stu-id="98af1-124">The displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-the-local-web-ui"></a><span data-ttu-id="98af1-125">使用本機 Web UI</span><span class="sxs-lookup"><span data-stu-id="98af1-125">Use the local web UI</span></span>

<span data-ttu-id="98af1-126">使用本機 Web UI 時有兩個步驟︰</span><span class="sxs-lookup"><span data-stu-id="98af1-126">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="98af1-127">下載更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="98af1-127">Download the update or the hotfix</span></span>
* <span data-ttu-id="98af1-128">安裝更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="98af1-128">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="98af1-129">下載更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="98af1-129">Download the update or the hotfix</span></span>

<span data-ttu-id="98af1-130">請執行下列步驟，從 Microsoft Update Catalog 下載軟體更新。</span><span class="sxs-lookup"><span data-stu-id="98af1-130">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="98af1-131">下載更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="98af1-131">To download the update or the hotfix</span></span>

1. <span data-ttu-id="98af1-132">啟動 Internet Explorer 並瀏覽至 [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="98af1-132">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="98af1-133">如果這是您第一次在此電腦上使用 Microsoft Update Catalog，請在系統提示您安裝 Microsoft Update Catalog 附加元件時，按一下 [安裝]  。</span><span class="sxs-lookup"><span data-stu-id="98af1-133">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="98af1-134">在 Microsoft Update Catalog 的搜尋方塊中，輸入您要下載的 Hotfix 知識庫 (KB) 編號。</span><span class="sxs-lookup"><span data-stu-id="98af1-134">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="98af1-135">輸入 **4021576** (適用於 Update 0.5)，然後按一下 [搜尋]。</span><span class="sxs-lookup"><span data-stu-id="98af1-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="98af1-136">此時會顯示 Hotfix 清單，例如 StorSimple Virtual Array Update 0.5。</span><span class="sxs-lookup"><span data-stu-id="98af1-136">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![搜尋目錄](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="98af1-138">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="98af1-138">Click **Download**.</span></span> 

5. <span data-ttu-id="98af1-139">您應該會看到下載兩個檔案，分別是 .msu 與 .cab 檔案。</span><span class="sxs-lookup"><span data-stu-id="98af1-139">You should see two files to download, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="98af1-140">將這兩個檔案一一下載至資料夾。</span><span class="sxs-lookup"><span data-stu-id="98af1-140">Download each of those files to a folder.</span></span> <span data-ttu-id="98af1-141">資料夾也可以複製到裝置可連線的網路共用位置。</span><span class="sxs-lookup"><span data-stu-id="98af1-141">The folder can also be copied to a network share that is reachable from the device.</span></span>

6. <span data-ttu-id="98af1-142">開啟檔案所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="98af1-142">Open the folder where the files are located.</span></span>
    <span data-ttu-id="98af1-143">![封裝中的檔案](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="98af1-143">![Files in the package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="98af1-144">您會看見：</span><span class="sxs-lookup"><span data-stu-id="98af1-144">You see:</span></span>
    -  <span data-ttu-id="98af1-145">Microsoft Update 獨立封裝檔案`WindowsTH-KB3011067-x64`。</span><span class="sxs-lookup"><span data-stu-id="98af1-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="98af1-146">此檔案用來更新裝置軟體。</span><span class="sxs-lookup"><span data-stu-id="98af1-146">This file is used to update the device software.</span></span>
    - <span data-ttu-id="98af1-147">Geneva 監視代理程式封裝檔案`GenevaMonitoringAgentPackageInstaller`。</span><span class="sxs-lookup"><span data-stu-id="98af1-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="98af1-148">此檔案用於更新「監視與診斷」服務 (MDS) 代理程式。</span><span class="sxs-lookup"><span data-stu-id="98af1-148">This file is used to update the Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="98af1-149">按兩下 cab 檔案。</span><span class="sxs-lookup"><span data-stu-id="98af1-149">Double-click the cab file.</span></span> <span data-ttu-id="98af1-150">隨即顯示 .msi。</span><span class="sxs-lookup"><span data-stu-id="98af1-150">A .msi is displayed.</span></span> <span data-ttu-id="98af1-151">選取檔案，按一下滑鼠右鍵，然後按一下 [擷取] 以擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="98af1-151">Select the file, right-click, and then **Extract** the file.</span></span> <span data-ttu-id="98af1-152">您將使用.msi 檔案更新代理程式。</span><span class="sxs-lookup"><span data-stu-id="98af1-152">You will use the _.msi_ file to update the agent.</span></span>

        ![擷取 MDS 代理程式更新檔案](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="98af1-154">安裝更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="98af1-154">Install the update or the hotfix</span></span>

<span data-ttu-id="98af1-155">安裝更新或 Hotfix 之前，請確定更新或 Hotfix 已下載至您主機的本機上，或是可透過網路共用存取。</span><span class="sxs-lookup"><span data-stu-id="98af1-155">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="98af1-156">請使用此方法在執行 GA 或 Update 0.1 軟體版本的裝置上安裝更新。</span><span class="sxs-lookup"><span data-stu-id="98af1-156">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="98af1-157">此程序需時不到 2 分鐘。</span><span class="sxs-lookup"><span data-stu-id="98af1-157">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="98af1-158">請執行下列步驟以安裝更新或 Hotfix。</span><span class="sxs-lookup"><span data-stu-id="98af1-158">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="98af1-159">安裝更新或 Hotfix</span><span class="sxs-lookup"><span data-stu-id="98af1-159">To install the update or the hotfix</span></span>

1. <span data-ttu-id="98af1-160">在本機 Web UI 中，移至 [維護]  >  [軟體更新]。</span><span class="sxs-lookup"><span data-stu-id="98af1-160">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="98af1-162">在 [更新檔案路徑] 中，輸入更新或 Hotfix 的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="98af1-162">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="98af1-163">如果更新或 Hotfix 的安裝檔案是放在網路共用上，您也可以瀏覽至該檔案。</span><span class="sxs-lookup"><span data-stu-id="98af1-163">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="98af1-164">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="98af1-164">Click **Apply**.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="98af1-166">此時會顯示警告。</span><span class="sxs-lookup"><span data-stu-id="98af1-166">A warning is displayed.</span></span> <span data-ttu-id="98af1-167">如果這是單一節點裝置，在套用更新後，裝置就會重新啟動而會有停機時間。</span><span class="sxs-lookup"><span data-stu-id="98af1-167">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="98af1-168">按一下核取圖示。</span><span class="sxs-lookup"><span data-stu-id="98af1-168">Click the check icon.</span></span>
   
   ![更新裝置](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="98af1-170">更新會開始進行。</span><span class="sxs-lookup"><span data-stu-id="98af1-170">The update starts.</span></span> <span data-ttu-id="98af1-171">成功更新裝置之後，裝置就會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="98af1-171">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="98af1-172">在這段持續時間會無法存取本機 UI。</span><span class="sxs-lookup"><span data-stu-id="98af1-172">The local UI is not accessible in this duration.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="98af1-174">重新啟動完成後，您就會進入 [登入] 頁面。</span><span class="sxs-lookup"><span data-stu-id="98af1-174">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="98af1-175">若要確認裝置軟體是否已更新，請在本機 Web UI 中，移至 [維護]  >  [軟體更新]。</span><span class="sxs-lookup"><span data-stu-id="98af1-175">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="98af1-176">顯示的軟體版本應該是 10.0.0.0.0.10290.0 (適用於 Update 0.5)。</span><span class="sxs-lookup"><span data-stu-id="98af1-176">The displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="98af1-177">我們在本機 Web UI 和 Azure 入口網站中回報軟體版本的方式略有不同。</span><span class="sxs-lookup"><span data-stu-id="98af1-177">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="98af1-178">例如，本機 Web UI 會回報 10.0.0.0.0.10290，而相同版本在 Azure 入口網站則會回報為 10.0.10290.0。</span><span class="sxs-lookup"><span data-stu-id="98af1-178">For example, the local web UI reports **10.0.0.0.0.10290** and the Azure portal reports **10.0.10290.0** for the same version.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="98af1-180">下一個步驟是更新 MDS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="98af1-180">The next step is to update the MDS agent.</span></span> <span data-ttu-id="98af1-181">在 [軟體更新] 頁面上，移至 [更新檔案路徑]，然後瀏覽至 `GenevaMonitoringAgentPackageInstaller.msi` 檔案。</span><span class="sxs-lookup"><span data-stu-id="98af1-181">In the **Software Update** page, go to the **Update file path** and browse to the `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="98af1-182">重複步驟 2 至 4。</span><span class="sxs-lookup"><span data-stu-id="98af1-182">Repeat steps 2-4.</span></span> <span data-ttu-id="98af1-183">虛擬陣列重新啟動之後，登入本機 Web UI。</span><span class="sxs-lookup"><span data-stu-id="98af1-183">After the virtual array restarts, sign into the local web UI.</span></span>

<span data-ttu-id="98af1-184">更新現已完成。</span><span class="sxs-lookup"><span data-stu-id="98af1-184">The update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98af1-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98af1-185">Next steps</span></span>

<span data-ttu-id="98af1-186">深入了解 [administering your StorSimple Virtual Array (管理 StorSimple Virtual Array)](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="98af1-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

