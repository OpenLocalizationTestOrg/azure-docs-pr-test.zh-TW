---
title: "更新 StorSimple Virtual Array 0.5 aaaInstall |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Virtual Array web UI tooapply 更新使用 hello Azure 入口網站與 hotfix 方法"
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
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="baf6c-103">在 StorSimple Virtual Array 上安裝 Update 0.5</span><span class="sxs-lookup"><span data-stu-id="baf6c-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="baf6c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="baf6c-104">Overview</span></span>

<span data-ttu-id="baf6c-105">本文說明 hello 步驟需要的 tooinstall 更新 0.5 StorSimple 虛擬陣列透過 hello 本機 web UI 中和透過 hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="baf6c-105">This article describes hello steps required tooinstall Update 0.5 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="baf6c-106">您需要 tooapply 軟體更新或 hotfix tookeep StorSimple 虛擬陣列最新狀態。</span><span class="sxs-lookup"><span data-stu-id="baf6c-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="baf6c-107">在套用更新之前，我們建議您採取 hello 磁碟區或離線 hello 上的共用裝載第一次，然後 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="baf6c-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="baf6c-108">這樣可以讓資料損毀的可能性降至最低。</span><span class="sxs-lookup"><span data-stu-id="baf6c-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="baf6c-109">Hello 磁碟區或共用離線之後，您也應該採取手動 hello 裝置的備份。</span><span class="sxs-lookup"><span data-stu-id="baf6c-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="baf6c-110">更新 0.5 會對應太**10.0.10290.0**在裝置上的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="baf6c-110">Update 0.5 corresponds too**10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="baf6c-111">如需此更新中新功能的資訊，請移至太[0.5 更新的版本資訊](storsimple-virtual-array-update-05-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="baf6c-111">For information on what is new in this update, go too[Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="baf6c-112">如果您正在更新 0.2 或更新版本中，我們建議您安裝 hello 透過 hello Azure 入口網站的更新。</span><span class="sxs-lookup"><span data-stu-id="baf6c-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="baf6c-113">如果您執行 Update 0.1 或 GA 軟體版本，您必須使用透過 hello 本機 web UI tooinstall 更新 0.5 hello hotfix 方法。</span><span class="sxs-lookup"><span data-stu-id="baf6c-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.5.</span></span>
>
> - <span data-ttu-id="baf6c-114">請記住，安裝更新或 Hotfix 會重新啟動您的裝置。</span><span class="sxs-lookup"><span data-stu-id="baf6c-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="baf6c-115">指定 hello StorSimple Virtual Array 是單一節點的裝置、 任何進行中的 I/O 中斷和您的裝置會發生停機。</span><span class="sxs-lookup"><span data-stu-id="baf6c-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="baf6c-116">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="baf6c-116">Use hello Azure portal</span></span>

<span data-ttu-id="baf6c-117">如果 0.2 和更新版本，請執行更新，我們建議您安裝透過 hello Azure 入口網站的更新。</span><span class="sxs-lookup"><span data-stu-id="baf6c-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="baf6c-118">hello 入口網站的程序需要 hello 使用者 tooscan、 下載及安裝 hello 的更新。</span><span class="sxs-lookup"><span data-stu-id="baf6c-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="baf6c-119">此程序接受 toocomplete 大約 7 分鐘。</span><span class="sxs-lookup"><span data-stu-id="baf6c-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="baf6c-120">執行 hello 下列步驟 tooinstall hello 更新或 hotfix。</span><span class="sxs-lookup"><span data-stu-id="baf6c-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="baf6c-121">Hello 之後安裝已完成，請移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="baf6c-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="baf6c-122">選取**裝置**然後選取並按一下您剛才更新 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="baf6c-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="baf6c-123">跳過**設定 > 管理 > 裝置更新**。</span><span class="sxs-lookup"><span data-stu-id="baf6c-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="baf6c-124">hello 顯示軟體版本應為**10.0.10290.0**。</span><span class="sxs-lookup"><span data-stu-id="baf6c-124">hello displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="baf6c-125">使用 hello 本機 web UI</span><span class="sxs-lookup"><span data-stu-id="baf6c-125">Use hello local web UI</span></span>

<span data-ttu-id="baf6c-126">使用 hello 本機 web UI 時，有兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="baf6c-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="baf6c-127">下載 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="baf6c-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="baf6c-128">安裝 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="baf6c-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="baf6c-129">下載 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="baf6c-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="baf6c-130">執行 hello hello Microsoft Update 類別目錄中的下列步驟 toodownload hello 軟體更新。</span><span class="sxs-lookup"><span data-stu-id="baf6c-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="baf6c-131">toodownload hello update 或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="baf6c-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="baf6c-132">啟動 Internet Explorer 並瀏覽過[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="baf6c-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="baf6c-133">如果這是您第一次使用 hello Microsoft Update 類別目錄，在此電腦上，按一下**安裝**時提示的 tooinstall hello Microsoft Update 類別目錄的附加元件。</span><span class="sxs-lookup"><span data-stu-id="baf6c-133">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="baf6c-134">在 hello hello Microsoft Update 類別目錄的搜尋方塊中輸入 hello 知識庫 (KB) 號碼要 toodownload 的 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="baf6c-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="baf6c-135">輸入 **4021576** (適用於 Update 0.5)，然後按一下搜尋。</span><span class="sxs-lookup"><span data-stu-id="baf6c-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="baf6c-136">hello hotfix 清單會出現，例如**StorSimple 虛擬陣列更新 0.5**。</span><span class="sxs-lookup"><span data-stu-id="baf6c-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![搜尋目錄](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="baf6c-138">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="baf6c-138">Click **Download**.</span></span> 

5. <span data-ttu-id="baf6c-139">您應該會看到兩個檔案 toodownload， *.msu*和*.cab*檔案。</span><span class="sxs-lookup"><span data-stu-id="baf6c-139">You should see two files toodownload, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="baf6c-140">下載每個這些檔案 tooa 資料夾。</span><span class="sxs-lookup"><span data-stu-id="baf6c-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="baf6c-141">hello 資料夾也可以複製的 tooa 從 hello 裝置的網路共用。</span><span class="sxs-lookup"><span data-stu-id="baf6c-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="baf6c-142">開啟 hello hello 檔案所在資料夾。</span><span class="sxs-lookup"><span data-stu-id="baf6c-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="baf6c-143">![Hello 套件中的檔案](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="baf6c-143">![Files in hello package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="baf6c-144">您會看見：</span><span class="sxs-lookup"><span data-stu-id="baf6c-144">You see:</span></span>
    -  <span data-ttu-id="baf6c-145">Microsoft Update 獨立封裝檔案`WindowsTH-KB3011067-x64`。</span><span class="sxs-lookup"><span data-stu-id="baf6c-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="baf6c-146">這個檔案是使用的 tooupdate hello 裝置軟體。</span><span class="sxs-lookup"><span data-stu-id="baf6c-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="baf6c-147">Geneva 監視代理程式封裝檔案`GenevaMonitoringAgentPackageInstaller`。</span><span class="sxs-lookup"><span data-stu-id="baf6c-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="baf6c-148">這個檔案是使用的 tooupdate hello 監視和診斷服務 (MDS) 代理程式。</span><span class="sxs-lookup"><span data-stu-id="baf6c-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="baf6c-149">按兩下 hello 封包檔。</span><span class="sxs-lookup"><span data-stu-id="baf6c-149">Double-click hello cab file.</span></span> <span data-ttu-id="baf6c-150">隨即顯示 .msi。</span><span class="sxs-lookup"><span data-stu-id="baf6c-150">A .msi is displayed.</span></span> <span data-ttu-id="baf6c-151">選取 hello 檔案按一下滑鼠右鍵，然後**擷取**hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="baf6c-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="baf6c-152">您將使用 hello _.msi_檔案 tooupdate hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="baf6c-152">You will use hello _.msi_ file tooupdate hello agent.</span></span>

        ![擷取 MDS 代理程式更新檔案](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="baf6c-154">安裝 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="baf6c-154">Install hello update or hello hotfix</span></span>

<span data-ttu-id="baf6c-155">先前 toohello 更新或 hotfix 安裝，請確定您擁有 hello 更新，或 hello hotfix 下載您的主機上的本機或透過網路共用。</span><span class="sxs-lookup"><span data-stu-id="baf6c-155">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="baf6c-156">執行 GA 的裝置上使用這個方法會 tooinstall 更新或更新 0.1 軟體版本。</span><span class="sxs-lookup"><span data-stu-id="baf6c-156">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="baf6c-157">此程序接受不超過 2 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="baf6c-157">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="baf6c-158">執行 hello 下列步驟 tooinstall hello 更新或 hotfix。</span><span class="sxs-lookup"><span data-stu-id="baf6c-158">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="baf6c-159">tooinstall hello update 或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="baf6c-159">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="baf6c-160">在本機 web UI hello，移過**維護** > **軟體更新**。</span><span class="sxs-lookup"><span data-stu-id="baf6c-160">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="baf6c-162">在**更新檔案路徑**、 輸入 hello hello 更新的檔案名稱或 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="baf6c-162">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="baf6c-163">如果放在網路共用上，您也可以瀏覽 toohello 更新或 hotfix 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="baf6c-163">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="baf6c-164">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="baf6c-164">Click **Apply**.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="baf6c-166">此時會顯示警告。</span><span class="sxs-lookup"><span data-stu-id="baf6c-166">A warning is displayed.</span></span> <span data-ttu-id="baf6c-167">指定這是單一節點裝置之後套用 hello 更新，hello 裝置重新啟動，且沒有停機時間。</span><span class="sxs-lookup"><span data-stu-id="baf6c-167">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="baf6c-168">按一下 [hello] 核取圖示。</span><span class="sxs-lookup"><span data-stu-id="baf6c-168">Click hello check icon.</span></span>
   
   ![更新裝置](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="baf6c-170">hello 更新開始。</span><span class="sxs-lookup"><span data-stu-id="baf6c-170">hello update starts.</span></span> <span data-ttu-id="baf6c-171">已成功更新 hello 裝置之後，它會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="baf6c-171">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="baf6c-172">hello 本機 UI 不能存取在此期間。</span><span class="sxs-lookup"><span data-stu-id="baf6c-172">hello local UI is not accessible in this duration.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="baf6c-174">Hello 重新啟動完成之後，即會進入 toohello**登入**頁面。</span><span class="sxs-lookup"><span data-stu-id="baf6c-174">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="baf6c-175">更新 hello 裝置軟體，在 hello 本機 web UI，tooverify 移過**維護** > **軟體更新**。</span><span class="sxs-lookup"><span data-stu-id="baf6c-175">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="baf6c-176">hello 顯示軟體版本應為**10.0.0.0.0.10290.0**更新 0.5。</span><span class="sxs-lookup"><span data-stu-id="baf6c-176">hello displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="baf6c-177">我們稍有不同的方式，在 hello 本機 web UI 中會報告 hello 軟體版本及 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="baf6c-177">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="baf6c-178">例如，hello 本機 web UI 報告**10.0.0.0.0.10290** hello Azure 入口網站的報表和**10.0.10290.0** hello 相同版本。</span><span class="sxs-lookup"><span data-stu-id="baf6c-178">For example, hello local web UI reports **10.0.0.0.0.10290** and hello Azure portal reports **10.0.10290.0** for hello same version.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="baf6c-180">hello 下一個步驟是 tooupdate hello MDS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="baf6c-180">hello next step is tooupdate hello MDS agent.</span></span> <span data-ttu-id="baf6c-181">在 hello**軟體更新**頁面上，移 toohello**更新檔案路徑**並瀏覽 toohello`GenevaMonitoringAgentPackageInstaller.msi`檔案。</span><span class="sxs-lookup"><span data-stu-id="baf6c-181">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="baf6c-182">重複步驟 2 至 4。</span><span class="sxs-lookup"><span data-stu-id="baf6c-182">Repeat steps 2-4.</span></span> <span data-ttu-id="baf6c-183">Hello 虛擬陣列重新啟動之後，登入 hello 本機 web UI。</span><span class="sxs-lookup"><span data-stu-id="baf6c-183">After hello virtual array restarts, sign into hello local web UI.</span></span>

<span data-ttu-id="baf6c-184">hello 更新現在已完成。</span><span class="sxs-lookup"><span data-stu-id="baf6c-184">hello update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="baf6c-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="baf6c-185">Next steps</span></span>

<span data-ttu-id="baf6c-186">深入了解 [administering your StorSimple Virtual Array (管理 StorSimple Virtual Array)](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="baf6c-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

