---
title: "Azure StorSimple Data Manager UI aaaMicrosoft |Microsoft 文件"
description: "描述如何 toouse StorSimple Data Manager 服務 UI （私人預覽中）"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="881df-103">管理使用 hello StorSimple Data Manager 服務 UI （私人預覽中）</span><span class="sxs-lookup"><span data-stu-id="881df-103">Manage using hello StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="881df-104">本文說明如何使用 hello StorSimple Data Manager UI tooperform 資料轉換，以及在 hello StorSimple 8000 系列裝置上的資料。</span><span class="sxs-lookup"><span data-stu-id="881df-104">This article explains how you can use hello StorSimple Data Manager UI tooperform data transformation on data residing on hello StorSimple 8000 series devices.</span></span> <span data-ttu-id="881df-105">hello 已轉換的資料然後可供其他 Azure 服務，例如 Azure Media Services、 Azure HDInsight、 Azure Machine Learning 中，與 Azure 搜尋。</span><span class="sxs-lookup"><span data-stu-id="881df-105">hello transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="881df-106">使用 StorSimple 資料轉換</span><span class="sxs-lookup"><span data-stu-id="881df-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="881df-107">hello StorSimple Data Manager 是 hello 資源內的資料轉換，才能執行個體化。</span><span class="sxs-lookup"><span data-stu-id="881df-107">hello StorSimple Data Manager is hello resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="881df-108">hello 資料轉換服務可讓您將資料從 Azure 儲存體中您 StorSimple 內部部署裝置 tooblobs 移。</span><span class="sxs-lookup"><span data-stu-id="881df-108">hello Data Transformation service lets you move data from your StorSimple on-premises device tooblobs in Azure storage.</span></span> <span data-ttu-id="881df-109">因此，工作流程中您需要 toospecify hello 詳細資料有關的 toomove toohello 儲存體帳戶的感興趣的 StorSimple 裝置與 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="881df-109">Hence, in workflow you need toospecify hello details about your StorSimple device and hello data of interest that you want toomove toohello storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="881df-110">建立 StorSimple Data Manager 服務</span><span class="sxs-lookup"><span data-stu-id="881df-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="881df-111">執行下列步驟 toocreate StorSimple Data Manager 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="881df-111">Perform hello following steps toocreate a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="881df-112">toocreate StorSimple Data Manager 服務，跳過[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="881df-112">toocreate a StorSimple Data Manager service, go too[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="881df-113">按一下 hello  **+** 圖示，並搜尋 StorSimple Data Manager。</span><span class="sxs-lookup"><span data-stu-id="881df-113">Click hello **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="881df-114">按一下您的 StorSimple Data Manager 服務，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="881df-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="881df-115">如果您的訂用帳戶已啟用建立此服務，您會看到下列刀鋒視窗中的 hello。</span><span class="sxs-lookup"><span data-stu-id="881df-115">If your subscription is enabled for creating this service, you see hello following blade.</span></span>

    ![建立 StorSimple Data Managers 資源](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="881df-117">輸入 hello 輸入，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="881df-117">Enter hello inputs and click **Create**.</span></span> <span data-ttu-id="881df-118">hello 指定位置應該在裝載您的儲存體帳戶和您的 StorSimple Manager 服務的其中一個 hello。</span><span class="sxs-lookup"><span data-stu-id="881df-118">hello specified location should be hello one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="881df-119">目前，僅支援美國西部和西歐區域。</span><span class="sxs-lookup"><span data-stu-id="881df-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="881df-120">因此，您的 StorSimple Manager 服務、 Data Manager 服務和 hello 相關聯儲存體帳戶應該都是在 hello 上述支援的地區。</span><span class="sxs-lookup"><span data-stu-id="881df-120">Hence, your StorSimple Manager service, Data Manager service, and hello associated storage account should all be in hello preceding supported regions.</span></span> <span data-ttu-id="881df-121">它會每分鐘 toocreate hello 服務相關。</span><span class="sxs-lookup"><span data-stu-id="881df-121">It takes about a minute toocreate hello service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="881df-122">建立資料轉換作業定義</span><span class="sxs-lookup"><span data-stu-id="881df-122">Create a data transformation job definition</span></span>

<span data-ttu-id="881df-123">在 StorSimple Data Manager 服務中，您需要 toocreate 資料轉換作業定義。</span><span class="sxs-lookup"><span data-stu-id="881df-123">Within a StorSimple Data Manager service, you need toocreate a data transformation job definition.</span></span> <span data-ttu-id="881df-124">工作定義會指定您有興趣將移到 hello 原生格式的儲存體帳戶的 hello 資料的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="881df-124">A job definition specifies details of hello data that you are interested in moving into a storage account in hello native format.</span></span> 

<span data-ttu-id="881df-125">執行下列步驟 toocreate 新的資料轉換作業定義的 hello。</span><span class="sxs-lookup"><span data-stu-id="881df-125">Perform hello following steps toocreate a new data transformation job definition.</span></span>

1.  <span data-ttu-id="881df-126">瀏覽 toohello 您建立的服務。</span><span class="sxs-lookup"><span data-stu-id="881df-126">Navigate toohello service that you created.</span></span> <span data-ttu-id="881df-127">按一下 [+ 作業定義]。</span><span class="sxs-lookup"><span data-stu-id="881df-127">Click **+ Job Definition**.</span></span>

    ![按一下 [+ 作業定義]](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="881df-129">hello 新工作定義 刀鋒視窗會開啟。</span><span class="sxs-lookup"><span data-stu-id="881df-129">hello new job definition blade opens up.</span></span> <span data-ttu-id="881df-130">指定作業定義名稱，然後按一下 [來源]。</span><span class="sxs-lookup"><span data-stu-id="881df-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="881df-131">在 hello**設定資料來源**刀鋒視窗中，指定您的 StorSimple 裝置 hello 詳細資料和 hello 感興趣的資料。</span><span class="sxs-lookup"><span data-stu-id="881df-131">In hello **Configure data source** blade, specify hello details of your StorSimple device and hello data of interest.</span></span>

    ![建立作業定義](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="881df-133">由於這是新的資料管理員服務，尚未設定任何資料儲存機制。</span><span class="sxs-lookup"><span data-stu-id="881df-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="881df-134">您的 StorSimple Manager 做為資料儲存機制中，按一下 tooadd**加入新**在 hello 資料儲存機制的下拉式清單中，然後按一下**新增資料儲存機制**。</span><span class="sxs-lookup"><span data-stu-id="881df-134">tooadd your StorSimple Manager as a data repository, click **Add new** in hello data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="881df-135">選擇**StorSimple 8000 系列管理員**hello 儲存機制為輸入，並輸入 hello 屬性您**StorSimple Manager**。</span><span class="sxs-lookup"><span data-stu-id="881df-135">Choose **StorSimple 8000 series Manager** as hello repository type and enter hello properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="881df-136">Hello**資源識別碼**欄位，您需要 tooenter hello 號碼之前 hello **:**在您的 StorSimple manager 的 hello 登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="881df-136">For hello **Resource Id** field, you need tooenter hello number before hello **:** in hello registration key of your StorSimple manager.</span></span>

    ![建立資料來源](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="881df-138">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="881df-138">Click **OK** when done.</span></span> <span data-ttu-id="881df-139">這樣會儲存您的資料儲存機制，而且此 StorSimple Manager 可以重複使用在其他作業定義中，不需要再次輸入這些參數。</span><span class="sxs-lookup"><span data-stu-id="881df-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="881df-140">花幾秒後按一下**確定**hello 上的 StorSimple Manager tooshow hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="881df-140">It takes a few seconds after you click **OK** for hello StorSimple Manager tooshow up in hello dropdown.</span></span>

6.  <span data-ttu-id="881df-141">在 hello**設定資料來源**刀鋒視窗中，輸入 hello 裝置名稱和 hello 具有您感興趣的資料磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="881df-141">In hello **Configure data source** blade, enter hello device name and hello volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="881df-142">在 hello**篩選**子區段中，輸入 hello 根目錄，其中包含您感興趣的資料 (此欄位的開頭應`\`)。</span><span class="sxs-lookup"><span data-stu-id="881df-142">In hello **Filter** subsection, enter hello root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="881df-143">您也可以在這裡新增任何檔案篩選。</span><span class="sxs-lookup"><span data-stu-id="881df-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="881df-144">hello 資料轉換服務適用於快照集透過推入總 toohello Azure 的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="881df-144">hello data transformation service works on hello data that is pushed up toohello Azure via snapshots.</span></span> <span data-ttu-id="881df-145">當執行此作業，您可以選擇 tootake 備份每次執行此作業時 (toowork 上最新的資料) 或 toouse hello hello 雲端中的最後一個現有備份，（如果您正在針對某些封存的資料）。</span><span class="sxs-lookup"><span data-stu-id="881df-145">When running this job, you can choose tootake a backup every time this job is run (toowork on latest data) or toouse hello last existing backup in hello cloud (if you are working on some archived data).</span></span>

    ![新增資料來源詳細資料](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="881df-147">接下來，hello 目標設定必須設定 toobe。</span><span class="sxs-lookup"><span data-stu-id="881df-147">Next, hello Target settings need toobe configured.</span></span> <span data-ttu-id="881df-148">有 2 種支援的目標 – Azure 儲存體帳戶和 Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="881df-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="881df-149">選擇 儲存體帳戶 tooput 檔案中該帳戶的 blob。</span><span class="sxs-lookup"><span data-stu-id="881df-149">Choose storage accounts tooput files into blobs in that account.</span></span> <span data-ttu-id="881df-150">選擇 media services 帳戶 tooput 檔案中該帳戶的資產。</span><span class="sxs-lookup"><span data-stu-id="881df-150">Choose media services account tooput files into assets in that account.</span></span> <span data-ttu-id="881df-151">同樣地，我們需要 tooadd 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="881df-151">Again, we need tooadd a repository.</span></span> <span data-ttu-id="881df-152">在 hello 下拉式清單中，選取**新增**然後**設定**。</span><span class="sxs-lookup"><span data-stu-id="881df-152">In hello dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![建立資料接收](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="881df-154">在這裡，您可以選取您想要 tooadd 和 hello 與 hello 儲存機制相關聯的其他參數的儲存機制的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="881df-154">Here, you can select hello type of repository you want tooadd and hello other parameters associated with hello repository.</span></span> <span data-ttu-id="881df-155">在這兩種情況下，hello 工作執行時，會建立儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="881df-155">In both cases, a storage queue is created when hello job runs.</span></span> <span data-ttu-id="881df-156">此佇列中會填入已轉換的 blob 備妥時的相關訊息。</span><span class="sxs-lookup"><span data-stu-id="881df-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="881df-157">hello 這個佇列名稱是 hello 與 hello hello 工作定義名稱相同。</span><span class="sxs-lookup"><span data-stu-id="881df-157">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="881df-158">如果您選取**Media Services** hello 儲存機制類型，然後您也可以輸入儲存體帳戶認證建立 hello 佇列的位置。</span><span class="sxs-lookup"><span data-stu-id="881df-158">If you select **Media Services** as hello repo type, then you can also enter storage account credentials where hello queue is created.</span></span>

    ![新增資料接收詳細資料](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="881df-160">在新增之後 hello 資料儲存機制 （這需要幾秒鐘），您會發現 hello 儲存機制中 hello hello 下拉式清單中**目標帳戶名稱**。</span><span class="sxs-lookup"><span data-stu-id="881df-160">After adding hello data repository (which takes a few seconds), you will find hello repo in hello dropdown in hello **Target account name**.</span></span>  <span data-ttu-id="881df-161">選擇您需要的 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="881df-161">Choose hello target that you need.</span></span>

12. <span data-ttu-id="881df-162">按一下**確定**toocreate hello 工作定義。</span><span class="sxs-lookup"><span data-stu-id="881df-162">Click **OK** toocreate hello job definition.</span></span> <span data-ttu-id="881df-163">現在已設定作業定義。</span><span class="sxs-lookup"><span data-stu-id="881df-163">Your job definition is now set up.</span></span> <span data-ttu-id="881df-164">您可以使用多次透過 hello UI 這個工作定義。</span><span class="sxs-lookup"><span data-stu-id="881df-164">You can use this job definition multiple times via hello UI.</span></span>

    ![新增作業定義](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a><span data-ttu-id="881df-166">執行 hello 工作定義</span><span class="sxs-lookup"><span data-stu-id="881df-166">Run hello job definition</span></span>

<span data-ttu-id="881df-167">每當您需要從 hello 工作定義中所指定的 StorSimple toohello 儲存體帳戶的 toomove 資料時，您將需要 tooinvoke 它。</span><span class="sxs-lookup"><span data-stu-id="881df-167">Whenever you need toomove data from StorSimple toohello storage account that you have specified in hello job definition, you will need tooinvoke it.</span></span> <span data-ttu-id="881df-168">在每次叫用 hello 作業變更 hello 參數沒有些許的彈性空間。</span><span class="sxs-lookup"><span data-stu-id="881df-168">There is some flexibility in changing hello parameters every time you invoke hello job.</span></span> <span data-ttu-id="881df-169">hello 步驟如下所示：</span><span class="sxs-lookup"><span data-stu-id="881df-169">hello steps are as follows:</span></span>

1. <span data-ttu-id="881df-170">選取您的 StorSimple Data Manager 服務，並移過**監視**。</span><span class="sxs-lookup"><span data-stu-id="881df-170">Select your StorSimple Data Manager service and go too**Monitoring**.</span></span> <span data-ttu-id="881df-171">按一下 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="881df-171">Click **Run Now**.</span></span>

    ![Trigger job definition](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="881df-173">選擇 hello 工作定義您想 toorun。</span><span class="sxs-lookup"><span data-stu-id="881df-173">Choose hello job definition that you want toorun.</span></span> <span data-ttu-id="881df-174">按一下**回合設定**toomodify 您可能希望 toochange 執行此作業的任何設定。</span><span class="sxs-lookup"><span data-stu-id="881df-174">Click **Run settings** toomodify any settings that you might want toochange for this job run.</span></span>

    ![執行作業設定](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="881df-176">按一下**確定**，然後按一下**執行**toolaunch 您的工作。</span><span class="sxs-lookup"><span data-stu-id="881df-176">Click **OK** and then click **Run** toolaunch your job.</span></span> <span data-ttu-id="881df-177">toomonitor 此作業，請移 toohello**作業**頁面中您 StorSimple 資料管理員。</span><span class="sxs-lookup"><span data-stu-id="881df-177">toomonitor this job, go toohello **Jobs** page in your StorSimple Data Manager.</span></span>

    ![作業清單及狀態](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="881df-179">在加法 toomonitoring 在 hello**作業**刀鋒視窗中，您也可以聆聽 hello 訊息加入每次從 StorSimple toohello 儲存體帳戶移動檔案的儲存體佇列上。</span><span class="sxs-lookup"><span data-stu-id="881df-179">In addition toomonitoring in hello **Jobs** blade, you can also listen on hello storage queue where a message is added every time a file is moved from StorSimple toohello storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="881df-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="881df-180">Next steps</span></span>

<span data-ttu-id="881df-181">[使用.NET SDK toolaunch StorSimple Data Manager 作業](storsimple-data-manager-dotnet-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="881df-181">[Use .NET SDK toolaunch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>
