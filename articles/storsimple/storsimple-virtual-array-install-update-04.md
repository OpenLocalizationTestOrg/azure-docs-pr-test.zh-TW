---
title: "StorSimple Virtual Array aaaInstall 更新 |Microsoft 文件"
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
ms.date: 02/07/2017
ms.author: alkohli
ms.openlocfilehash: 6165b305fb0d404b404cf3a11dd0ade2f2f13b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-04-on-your-storsimple-virtual-array"></a><span data-ttu-id="b7da2-103">在您的 StorSimple Virtual Array 上安裝 Update 0.4</span><span class="sxs-lookup"><span data-stu-id="b7da2-103">Install Update 0.4 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="b7da2-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b7da2-104">Overview</span></span>

<span data-ttu-id="b7da2-105">本文說明 hello 步驟需要的 tooinstall 更新 0.4 StorSimple 虛擬陣列透過 hello 本機 web UI 中和透過 hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="b7da2-105">This article describes hello steps required tooinstall Update 0.4 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="b7da2-106">您需要 tooapply 軟體更新或 hotfix tookeep StorSimple 虛擬陣列最新狀態。</span><span class="sxs-lookup"><span data-stu-id="b7da2-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="b7da2-107">請記住，安裝更新或 Hotfix 會重新啟動您的裝置。</span><span class="sxs-lookup"><span data-stu-id="b7da2-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="b7da2-108">指定 hello StorSimple Virtual Array 是單一節點的裝置、 任何進行中的 I/O 中斷和您的裝置會發生停機。</span><span class="sxs-lookup"><span data-stu-id="b7da2-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="b7da2-109">在套用更新之前，我們建議您採取 hello 磁碟區或離線 hello 上的共用裝載第一次，然後 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="b7da2-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="b7da2-110">這樣可以讓資料損毀的可能性降至最低。</span><span class="sxs-lookup"><span data-stu-id="b7da2-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7da2-111">如果您執行 Update 0.1 或 GA 軟體版本，您必須使用透過 hello 本機 web UI tooinstall update 0.3 hello hotfix 方法。</span><span class="sxs-lookup"><span data-stu-id="b7da2-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="b7da2-112">如果您正在更新 0.2 或更新版本中，我們建議您安裝 hello 透過 hello Azure 入口網站的更新。</span><span class="sxs-lookup"><span data-stu-id="b7da2-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span>
 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="b7da2-113">使用 hello 本機 web UI</span><span class="sxs-lookup"><span data-stu-id="b7da2-113">Use hello local web UI</span></span>

<span data-ttu-id="b7da2-114">使用 hello 本機 web UI 時，有兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="b7da2-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="b7da2-115">下載 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="b7da2-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="b7da2-116">安裝 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="b7da2-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="b7da2-117">下載 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="b7da2-117">Download hello update or hello hotfix</span></span>

<span data-ttu-id="b7da2-118">執行 hello hello Microsoft Update 類別目錄中的下列步驟 toodownload hello 軟體更新。</span><span class="sxs-lookup"><span data-stu-id="b7da2-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="b7da2-119">toodownload hello update 或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="b7da2-119">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="b7da2-120">啟動 Internet Explorer 並瀏覽過[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="b7da2-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="b7da2-121">如果這是您第一次使用 hello Microsoft Update 類別目錄，在此電腦上，按一下**安裝**時提示的 tooinstall hello Microsoft Update 類別目錄的附加元件。</span><span class="sxs-lookup"><span data-stu-id="b7da2-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="b7da2-122">在 hello hello Microsoft Update 類別目錄的搜尋方塊中輸入 hello 知識庫 (KB) 號碼要 toodownload 的 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="b7da2-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="b7da2-123">針對 Update 0.4 輸入 **3216577**，然後按一下搜尋。</span><span class="sxs-lookup"><span data-stu-id="b7da2-123">Enter **3216577** for Update 0.4, and then click **Search**.</span></span>
   
    <span data-ttu-id="b7da2-124">hello hotfix 清單會出現，例如**StorSimple 虛擬陣列更新 0.4**。</span><span class="sxs-lookup"><span data-stu-id="b7da2-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.4**.</span></span>
   
    ![搜尋目錄](./media/storsimple-virtual-array-install-update-04/download1.png)

4. <span data-ttu-id="b7da2-126">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="b7da2-126">Click **Add**.</span></span> <span data-ttu-id="b7da2-127">hello 更新已新增 toohello 籃。</span><span class="sxs-lookup"><span data-stu-id="b7da2-127">hello update is added toohello basket.</span></span>

5. <span data-ttu-id="b7da2-128">按一下 [ **檢視購物籃**]。</span><span class="sxs-lookup"><span data-stu-id="b7da2-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="b7da2-129">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="b7da2-129">Click **Download**.</span></span> <span data-ttu-id="b7da2-130">指定或**瀏覽**所在 hello 下載 tooappear tooa 本機位置。</span><span class="sxs-lookup"><span data-stu-id="b7da2-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="b7da2-131">hello 下載更新 toohello 指定的位置，並放在名稱為 「 hello 更新相同的 hello 與子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="b7da2-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="b7da2-132">hello 資料夾也可以複製的 tooa 從 hello 裝置的網路共用。</span><span class="sxs-lookup"><span data-stu-id="b7da2-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

7. <span data-ttu-id="b7da2-133">開啟 hello 複製資料夾，您應該會看到 Microsoft Update 獨立封裝檔案`WindowsTH-KB3011067-x64`。</span><span class="sxs-lookup"><span data-stu-id="b7da2-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="b7da2-134">這個檔案是使用的 tooinstall hello 更新或 hotfix。</span><span class="sxs-lookup"><span data-stu-id="b7da2-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="b7da2-135">安裝 hello 更新或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="b7da2-135">Install hello update or hello hotfix</span></span>

<span data-ttu-id="b7da2-136">先前 toohello 更新或 hotfix 安裝，請確定您擁有 hello 更新，或 hello hotfix 下載您的主機上的本機或透過網路共用。</span><span class="sxs-lookup"><span data-stu-id="b7da2-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="b7da2-137">執行 GA 的裝置上使用這個方法會 tooinstall 更新或更新 0.1 軟體版本。</span><span class="sxs-lookup"><span data-stu-id="b7da2-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="b7da2-138">此程序接受不超過 2 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="b7da2-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="b7da2-139">執行 hello 下列步驟 tooinstall hello 更新或 hotfix。</span><span class="sxs-lookup"><span data-stu-id="b7da2-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="b7da2-140">tooinstall hello update 或 hello hotfix</span><span class="sxs-lookup"><span data-stu-id="b7da2-140">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="b7da2-141">在本機 web UI hello，移過**維護** > **軟體更新**。</span><span class="sxs-lookup"><span data-stu-id="b7da2-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="b7da2-143">在**更新檔案路徑**、 輸入 hello hello 更新的檔案名稱或 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="b7da2-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="b7da2-144">如果放在網路共用上，您也可以瀏覽 toohello 更新或 hotfix 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="b7da2-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="b7da2-145">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="b7da2-145">Click **Apply**.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="b7da2-147">此時會顯示警告。</span><span class="sxs-lookup"><span data-stu-id="b7da2-147">A warning is displayed.</span></span> <span data-ttu-id="b7da2-148">指定這是單一節點裝置之後套用 hello 更新，hello 裝置重新啟動，且沒有停機時間。</span><span class="sxs-lookup"><span data-stu-id="b7da2-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="b7da2-149">按一下 [hello] 核取圖示。</span><span class="sxs-lookup"><span data-stu-id="b7da2-149">Click hello check icon.</span></span>
   
   ![更新裝置](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="b7da2-151">hello 更新開始。</span><span class="sxs-lookup"><span data-stu-id="b7da2-151">hello update starts.</span></span> <span data-ttu-id="b7da2-152">已成功更新 hello 裝置之後，它會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="b7da2-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="b7da2-153">hello 本機 UI 不能存取在此期間。</span><span class="sxs-lookup"><span data-stu-id="b7da2-153">hello local UI is not accessible in this duration.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="b7da2-155">Hello 重新啟動完成之後，即會進入 toohello**登入**頁面。</span><span class="sxs-lookup"><span data-stu-id="b7da2-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="b7da2-156">更新 hello 裝置軟體，在 hello 本機 web UI，tooverify 移過**維護** > **軟體更新**。</span><span class="sxs-lookup"><span data-stu-id="b7da2-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="b7da2-157">hello 顯示軟體版本應為**10.0.0.0.0.10289.0**更新 0.4。</span><span class="sxs-lookup"><span data-stu-id="b7da2-157">hello displayed software version should be **10.0.0.0.0.10289.0** for Update 0.4.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b7da2-158">我們稍有不同的方式，在 hello 本機 web UI 中會報告 hello 軟體版本及 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b7da2-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="b7da2-159">例如，hello 本機 web UI 報告**10.0.0.0.0.10289** hello Azure 入口網站的報表和**10.0.10289.0** hello 相同版本。</span><span class="sxs-lookup"><span data-stu-id="b7da2-159">For example, hello local web UI reports **10.0.0.0.0.10289** and hello Azure portal reports **10.0.10289.0** for hello same version.</span></span>
   
    ![更新裝置](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a><span data-ttu-id="b7da2-161">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b7da2-161">Use hello Azure portal</span></span>

<span data-ttu-id="b7da2-162">如果 0.2 和更新版本，請執行更新，我們建議您安裝透過 hello Azure 入口網站的更新。</span><span class="sxs-lookup"><span data-stu-id="b7da2-162">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="b7da2-163">hello 入口網站的程序需要 hello 使用者 tooscan、 下載及安裝 hello 的更新。</span><span class="sxs-lookup"><span data-stu-id="b7da2-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="b7da2-164">此程序接受 toocomplete 大約 7 分鐘。</span><span class="sxs-lookup"><span data-stu-id="b7da2-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="b7da2-165">執行 hello 下列步驟 tooinstall hello 更新或 hotfix。</span><span class="sxs-lookup"><span data-stu-id="b7da2-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="b7da2-166">Hello 之後安裝已完成 （示依工作狀態在 100%），請移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="b7da2-166">After hello installation is complete (as indicated by job status at 100 %), go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="b7da2-167">選取**裝置**然後選取並按一下您想要從裝置連接的 toothis 服務的 hello 清單 tooupdate hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="b7da2-167">Select **Devices** and then select and click hello device you want tooupdate from hello list of devices connected toothis service.</span></span> <span data-ttu-id="b7da2-168">在 hello**設定**刀鋒視窗中，跳過**管理**區段，然後選取**裝置更新**。</span><span class="sxs-lookup"><span data-stu-id="b7da2-168">In hello **Settings** blade, go too**Manage** section and select **Device updates**.</span></span> <span data-ttu-id="b7da2-169">hello 顯示軟體版本應為**10.0.10289.0**。</span><span class="sxs-lookup"><span data-stu-id="b7da2-169">hello displayed software version should be **10.0.10289.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b7da2-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7da2-170">Next steps</span></span>

<span data-ttu-id="b7da2-171">深入了解 [administering your StorSimple Virtual Array (管理 StorSimple Virtual Array)](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="b7da2-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

