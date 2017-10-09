---
title: "更新 StorSimple Virtual Array 0.6 aaaInstall |Microsoft 文件"
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
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 2ccd1b5fc1957c35ebec35aa947d331b3ff05464
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a><span data-ttu-id="98fa7-103">在 StorSimple Virtual Array 上安裝 Update 0.6</span><span class="sxs-lookup"><span data-stu-id="98fa7-103">Install Update 0.6 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="98fa7-104">概觀</span><span class="sxs-lookup"><span data-stu-id="98fa7-104">Overview</span></span>

<span data-ttu-id="98fa7-105">本文說明 hello 步驟需要的 tooinstall 更新 0.6 StorSimple 虛擬陣列透過 hello 本機 web UI 中和透過 hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="98fa7-105">This article describes hello steps required tooinstall Update 0.6 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="98fa7-106">您最新的 StorSimple Virtual Array 套用 hello 軟體更新或 hotfix tookeep。</span><span class="sxs-lookup"><span data-stu-id="98fa7-106">You apply hello software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="98fa7-107">在套用更新之前，我們建議您採取 hello 磁碟區或離線 hello 上的共用裝載第一次，然後 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="98fa7-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="98fa7-108">這樣可以讓資料損毀的可能性降至最低。</span><span class="sxs-lookup"><span data-stu-id="98fa7-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="98fa7-109">Hello 磁碟區或共用離線之後，您也應該採取手動 hello 裝置的備份。</span><span class="sxs-lookup"><span data-stu-id="98fa7-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="98fa7-110">更新 0.6 對應太**10.0.10293.0**在裝置上的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="98fa7-110">Update 0.6 corresponds too**10.0.10293.0** software version on your device.</span></span> <span data-ttu-id="98fa7-111">如需此更新中新功能的資訊，請移至太[0.6 更新的版本資訊](storsimple-virtual-array-update-06-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="98fa7-111">For information on what is new in this update, go too[Release notes for Update 0.6](storsimple-virtual-array-update-06-release-notes.md).</span></span>
>
> - <span data-ttu-id="98fa7-112">如果您正在更新 0.2 或更新版本中，我們建議您安裝 hello 透過 hello Azure 入口網站的更新。</span><span class="sxs-lookup"><span data-stu-id="98fa7-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="98fa7-113">如果您執行 Update 0.1 或 GA 軟體版本，您必須使用透過 hello 本機 web UI tooinstall 更新 0.6 hello hotfix 方法。</span><span class="sxs-lookup"><span data-stu-id="98fa7-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.6.</span></span>
>
> - <span data-ttu-id="98fa7-114">請記住，安裝更新或 Hotfix 會重新啟動您的裝置。</span><span class="sxs-lookup"><span data-stu-id="98fa7-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="98fa7-115">指定 hello StorSimple Virtual Array 是單一節點的裝置、 任何進行中的 I/O 中斷和您的裝置會發生停機。</span><span class="sxs-lookup"><span data-stu-id="98fa7-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="98fa7-116">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="98fa7-116">Use hello Azure portal</span></span>

<span data-ttu-id="98fa7-117">如果 0.2 和更新版本，請執行更新，我們建議您安裝透過 hello Azure 入口網站的更新。</span><span class="sxs-lookup"><span data-stu-id="98fa7-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="98fa7-118">hello 入口網站的程序需要 hello 使用者 tooscan、 下載及安裝 hello 的更新。</span><span class="sxs-lookup"><span data-stu-id="98fa7-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="98fa7-119">此程序接受 toocomplete 大約 7 分鐘。</span><span class="sxs-lookup"><span data-stu-id="98fa7-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="98fa7-120">執行 hello 下列步驟 tooinstall hello 更新或 hotfix。</span><span class="sxs-lookup"><span data-stu-id="98fa7-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="98fa7-121">Hello 之後安裝已完成，請移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="98fa7-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="98fa7-122">選取**裝置**然後選取並按一下您剛才更新 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="98fa7-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="98fa7-123">跳過**設定 > 管理 > 裝置更新**。</span><span class="sxs-lookup"><span data-stu-id="98fa7-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="98fa7-124">hello 顯示軟體版本應為**10.0.10293.0**。</span><span class="sxs-lookup"><span data-stu-id="98fa7-124">hello displayed software version should be **10.0.10293.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="98fa7-125">使用 hello 本機 web UI</span><span class="sxs-lookup"><span data-stu-id="98fa7-125">Use hello local web UI</span></span>

<span data-ttu-id="98fa7-126">使用 hello 本機 web UI 時，有兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="98fa7-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="98fa7-127">下載 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="98fa7-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="98fa7-128">安裝 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="98fa7-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="98fa7-129">下載 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="98fa7-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="98fa7-130">執行 hello hello Microsoft Update 類別目錄中的下列步驟 toodownload hello 軟體更新。</span><span class="sxs-lookup"><span data-stu-id="98fa7-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="98fa7-131">toodownload hello update 或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="98fa7-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="98fa7-132">啟動 Internet Explorer 並瀏覽過[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="98fa7-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="98fa7-133">如果您使用 Microsoft Update 類別目錄 hello hello 第一次在這部電腦上，按一下**安裝**時提示的 tooinstall hello Microsoft Update 類別目錄的附加元件。</span><span class="sxs-lookup"><span data-stu-id="98fa7-133">If you are using hello Microsoft Update Catalog for hello first time on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="98fa7-134">在 hello hello Microsoft Update 類別目錄的搜尋方塊中輸入 hello 知識庫 (KB) 號碼要 toodownload 的 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="98fa7-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="98fa7-135">輸入 **4023268** (適用於 Update 0.6)，然後按一下搜尋。</span><span class="sxs-lookup"><span data-stu-id="98fa7-135">Enter **4023268** for Update 0.6, and then click **Search**.</span></span>
   
    <span data-ttu-id="98fa7-136">hello hotfix 清單會出現，例如**StorSimple 虛擬陣列更新 0.6**。</span><span class="sxs-lookup"><span data-stu-id="98fa7-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.6**.</span></span>
   
    ![搜尋目錄](./media/storsimple-virtual-array-install-update-06/download1.png)

4. <span data-ttu-id="98fa7-138">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="98fa7-138">Click **Download**.</span></span>

5. <span data-ttu-id="98fa7-139">您應該會看到五個檔案 toodownload。</span><span class="sxs-lookup"><span data-stu-id="98fa7-139">You should see five files toodownload.</span></span> <span data-ttu-id="98fa7-140">下載每個這些檔案 tooa 資料夾。</span><span class="sxs-lookup"><span data-stu-id="98fa7-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="98fa7-141">hello 資料夾也可以複製的 tooa 從 hello 裝置的網路共用。</span><span class="sxs-lookup"><span data-stu-id="98fa7-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="98fa7-142">開啟 hello hello 檔案所在資料夾。</span><span class="sxs-lookup"><span data-stu-id="98fa7-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="98fa7-143">![Hello 套件中的檔案](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span><span class="sxs-lookup"><span data-stu-id="98fa7-143">![Files in hello package](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span></span>

    <span data-ttu-id="98fa7-144">您會看見：</span><span class="sxs-lookup"><span data-stu-id="98fa7-144">You see:</span></span>
    -  <span data-ttu-id="98fa7-145">Microsoft Update 獨立封裝檔案`WindowsTH-KB3011067-x64`。</span><span class="sxs-lookup"><span data-stu-id="98fa7-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="98fa7-146">這個檔案是使用的 tooupdate hello 裝置軟體。</span><span class="sxs-lookup"><span data-stu-id="98fa7-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="98fa7-147">Geneva 監視代理程式封裝檔案`GenevaMonitoringAgentPackageInstaller`。</span><span class="sxs-lookup"><span data-stu-id="98fa7-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="98fa7-148">這個檔案是使用的 tooupdate hello 監視和診斷服務 (MDS) 代理程式。</span><span class="sxs-lookup"><span data-stu-id="98fa7-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="98fa7-149">按兩下 hello 封包檔。</span><span class="sxs-lookup"><span data-stu-id="98fa7-149">Double-click hello cab file.</span></span> <span data-ttu-id="98fa7-150">隨即顯示 _.msi_。</span><span class="sxs-lookup"><span data-stu-id="98fa7-150">A _.msi_ is displayed.</span></span> <span data-ttu-id="98fa7-151">選取 hello 檔案按一下滑鼠右鍵，然後**擷取**hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="98fa7-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="98fa7-152">使用 hello _.msi_檔案 tooupdate hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="98fa7-152">You use hello _.msi_ file tooupdate hello agent.</span></span>

        ![擷取 MDS 代理程式更新檔案](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > <span data-ttu-id="98fa7-154">如果您執行 StorSimple 更新 0.5 (0.0.10293.0) 不需要 tooupdate hello MDS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="98fa7-154">You do not need tooupdate hello MDS agent if you are running StorSimple Update 0.5 (0.0.10293.0).</span></span>

    - <span data-ttu-id="98fa7-155">包含 Windows 重大安全性更新的三個檔案：`windows8.1-kb4012213-x64`、`windows8.1-kb3205400-x64` 和 `windows8.1-kb4019213-x64`。</span><span class="sxs-lookup"><span data-stu-id="98fa7-155">Three files that contain critical Windows security updates, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span>


### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="98fa7-156">安裝 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="98fa7-156">Install hello update or hello hotfix</span></span>

<span data-ttu-id="98fa7-157">先前 toohello 更新或 hotfix 安裝，請確定您擁有 hello 更新，或 hello hotfix 下載您的主機上的本機或透過網路共用。</span><span class="sxs-lookup"><span data-stu-id="98fa7-157">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="98fa7-158">執行 GA 的裝置上使用這個方法會 tooinstall 更新或更新 0.1 軟體版本。</span><span class="sxs-lookup"><span data-stu-id="98fa7-158">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="98fa7-159">此程序會取用大約 12 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="98fa7-159">This procedure takes approximately 12 minutes toocomplete.</span></span> <span data-ttu-id="98fa7-160">執行 hello 下列步驟 tooinstall hello 更新或 hotfix。</span><span class="sxs-lookup"><span data-stu-id="98fa7-160">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="98fa7-161">tooinstall hello update 或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="98fa7-161">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="98fa7-162">在本機 web UI hello，移過**維護** > **軟體更新**。</span><span class="sxs-lookup"><span data-stu-id="98fa7-162">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="98fa7-163">記下您所執行的 hello 軟體版本。</span><span class="sxs-lookup"><span data-stu-id="98fa7-163">Make a note of hello software version that you are running.</span></span> <span data-ttu-id="98fa7-164">如果您正在**10.0.10290.0**，您不需要 tooupdate hello MDS 代理程式在步驟 6。</span><span class="sxs-lookup"><span data-stu-id="98fa7-164">If you are running **10.0.10290.0**, you do not need tooupdate hello MDS agent in step 6.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="98fa7-166">在**更新檔案路徑**、 輸入 hello hello 更新的檔案名稱或 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="98fa7-166">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="98fa7-167">如果放在網路共用上，您也可以瀏覽 toohello 更新或 hotfix 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="98fa7-167">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="98fa7-168">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="98fa7-168">Click **Apply**.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="98fa7-170">此時會顯示警告。</span><span class="sxs-lookup"><span data-stu-id="98fa7-170">A warning is displayed.</span></span> <span data-ttu-id="98fa7-171">指定的 hello 虛擬陣列是單一節點裝置之後套用 hello 更新，hello 裝置重新啟動，且沒有停機時間。</span><span class="sxs-lookup"><span data-stu-id="98fa7-171">Given hello virtual array is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="98fa7-172">按一下 [hello] 核取圖示。</span><span class="sxs-lookup"><span data-stu-id="98fa7-172">Click hello check icon.</span></span>
   
   ![更新裝置](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="98fa7-174">hello 更新開始。</span><span class="sxs-lookup"><span data-stu-id="98fa7-174">hello update starts.</span></span> <span data-ttu-id="98fa7-175">已成功更新 hello 裝置之後，它會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="98fa7-175">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="98fa7-176">hello 本機 UI 不能存取在此期間。</span><span class="sxs-lookup"><span data-stu-id="98fa7-176">hello local UI is not accessible in this duration.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="98fa7-178">Hello 重新啟動完成之後，即會進入 toohello**登入**頁面。</span><span class="sxs-lookup"><span data-stu-id="98fa7-178">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="98fa7-179">更新 hello 裝置軟體，在 hello 本機 web UI，tooverify 移過**維護** > **軟體更新**。</span><span class="sxs-lookup"><span data-stu-id="98fa7-179">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="98fa7-180">hello 顯示軟體版本應為**10.0.0.0.0.10293**更新 0.6。</span><span class="sxs-lookup"><span data-stu-id="98fa7-180">hello displayed software version should be **10.0.0.0.0.10293** for Update 0.6.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="98fa7-181">我們稍有不同的方式，在 hello 本機 web UI 中會報告 hello 軟體版本及 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="98fa7-181">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="98fa7-182">例如，hello 本機 web UI 報告**10.0.0.0.0.10293** hello Azure 入口網站的報表和**10.0.10293.0** hello 相同版本。</span><span class="sxs-lookup"><span data-stu-id="98fa7-182">For example, hello local web UI reports **10.0.0.0.0.10293** and hello Azure portal reports **10.0.10293.0** for hello same version.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. <span data-ttu-id="98fa7-184">如果套用此更新前執行的是 StorSimple Virtual Array Update 0.5 (**10.0.10290.0**)，請跳過此步驟。</span><span class="sxs-lookup"><span data-stu-id="98fa7-184">Skip this step if you were running StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) before you applied this update.</span></span> <span data-ttu-id="98fa7-185">開始 tooupdate 前，您可以進行步驟 1 中的 hello 軟體版本的附註。</span><span class="sxs-lookup"><span data-stu-id="98fa7-185">You made a note of hello software version in step 1 before you began tooupdate.</span></span> <span data-ttu-id="98fa7-186">如果之前執行的是 Update 0.5，MDS 代理程式已經是最新版。</span><span class="sxs-lookup"><span data-stu-id="98fa7-186">If you were running Update 0.5, your MDS agent is already up-to-date .</span></span>

    <span data-ttu-id="98fa7-187">如果您正在執行軟體版本先前 tooUpdate 0.5，hello 為您的下一個步驟是 tooupdate hello MDS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="98fa7-187">If you are running a software version prior tooUpdate 0.5, hello next step for you is tooupdate hello MDS agent.</span></span> <span data-ttu-id="98fa7-188">在 hello**軟體更新**頁面上，移 toohello**更新檔案路徑**並瀏覽 toohello`GenevaMonitoringAgentPackageInstaller.msi`檔案。</span><span class="sxs-lookup"><span data-stu-id="98fa7-188">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="98fa7-189">重複步驟 2 至 4。</span><span class="sxs-lookup"><span data-stu-id="98fa7-189">Repeat steps 2-4.</span></span> <span data-ttu-id="98fa7-190">Hello 虛擬陣列重新啟動之後，登入 hello 本機 web UI。</span><span class="sxs-lookup"><span data-stu-id="98fa7-190">After hello virtual array restarts, sign into hello local web UI.</span></span>

7. <span data-ttu-id="98fa7-191">重複步驟 2-4 tooinstall hello Windows 安全性修正使用檔案`windows8.1-kb4012213-x64`，`windows8.1-kb3205400-x64`，和`windows8.1-kb4019213-x64`。</span><span class="sxs-lookup"><span data-stu-id="98fa7-191">Repeat step 2-4 tooinstall hello Windows security fixes using files `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span> <span data-ttu-id="98fa7-192">hello 虛擬陣列會在每次安裝之後，您需要 toosign 入 hello 本機 web UI。</span><span class="sxs-lookup"><span data-stu-id="98fa7-192">hello virtual array restarts after each install and you need toosign into hello local web UI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98fa7-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98fa7-193">Next steps</span></span>

<span data-ttu-id="98fa7-194">深入了解 [administering your StorSimple Virtual Array (管理 StorSimple Virtual Array)](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="98fa7-194">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

