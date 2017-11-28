---
title: Microsoft Azure StorSimple Data Manager UI | Microsoft Docs
description: "說明如何使用 StorSimple Data Manager 服務 UI (私人預覽)"
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
ms.openlocfilehash: 53a8599df2c647613122cd791b680e2e658586b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-using-the-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="d84d5-103">使用 StorSimple Data Manager 服務 UI 來管理 (私人預覽)</span><span class="sxs-lookup"><span data-stu-id="d84d5-103">Manage using the StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="d84d5-104">本文說明如何使用 StorSimple Data Manager UI，對 StorSimple 8000 系列裝置上的資料執行資料轉換。</span><span class="sxs-lookup"><span data-stu-id="d84d5-104">This article explains how you can use the StorSimple Data Manager UI to perform data transformation on data residing on the StorSimple 8000 series devices.</span></span> <span data-ttu-id="d84d5-105">然後，轉換後的資料就可供其他 Azure 服務取用，例如 Azure 媒體服務、Azure HDInsight、Azure Machine Learning 和 Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="d84d5-105">The transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="d84d5-106">使用 StorSimple 資料轉換</span><span class="sxs-lookup"><span data-stu-id="d84d5-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="d84d5-107">StorSimple Data Manager 是可讓您具現化資料轉換的資源。</span><span class="sxs-lookup"><span data-stu-id="d84d5-107">The StorSimple Data Manager is the resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="d84d5-108">資料轉換服務可讓您將資料從 StorSimple 內部部署裝置移至 Azure 儲存體中的 blob。</span><span class="sxs-lookup"><span data-stu-id="d84d5-108">The Data Transformation service lets you move data from your StorSimple on-premises device to blobs in Azure storage.</span></span> <span data-ttu-id="d84d5-109">因此，針對您的 StorSimple 裝置和您想要移至儲存體帳戶的資料，您必須在工作流程中指定詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d84d5-109">Hence, in workflow you need to specify the details about your StorSimple device and the data of interest that you want to move to the storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="d84d5-110">建立 StorSimple Data Manager 服務</span><span class="sxs-lookup"><span data-stu-id="d84d5-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="d84d5-111">執行下列步驟來建立 StorSimple Data Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="d84d5-111">Perform the following steps to create a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="d84d5-112">若要建立 StorSimple Data Manager 服務，請移至 [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="d84d5-112">To create a StorSimple Data Manager service, go to [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="d84d5-113">按一下 **+** 圖示，並搜尋 StorSimple Data Manager。</span><span class="sxs-lookup"><span data-stu-id="d84d5-113">Click the **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="d84d5-114">按一下您的 StorSimple Data Manager 服務，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="d84d5-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="d84d5-115">如果您的訂用帳戶已啟用來建立此服務，您會看到下列刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d84d5-115">If your subscription is enabled for creating this service, you see the following blade.</span></span>

    ![建立 StorSimple Data Managers 資源](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="d84d5-117">輸入後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="d84d5-117">Enter the inputs and click **Create**.</span></span> <span data-ttu-id="d84d5-118">指定的位置要用來裝載您的儲存體帳戶和 StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="d84d5-118">The specified location should be the one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="d84d5-119">目前，僅支援美國西部和西歐區域。</span><span class="sxs-lookup"><span data-stu-id="d84d5-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="d84d5-120">因此，您的 StorSimple Manager 服務、資料管理員服務和相關聯的儲存體帳戶，都必須位於上述支援的區域。</span><span class="sxs-lookup"><span data-stu-id="d84d5-120">Hence, your StorSimple Manager service, Data Manager service, and the associated storage account should all be in the preceding supported regions.</span></span> <span data-ttu-id="d84d5-121">需要一分鐘的時間來建立服務。</span><span class="sxs-lookup"><span data-stu-id="d84d5-121">It takes about a minute to create the service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="d84d5-122">建立資料轉換作業定義</span><span class="sxs-lookup"><span data-stu-id="d84d5-122">Create a data transformation job definition</span></span>

<span data-ttu-id="d84d5-123">在 StorSimple Data Manager 服務中，您需要建立資料轉換作業定義。</span><span class="sxs-lookup"><span data-stu-id="d84d5-123">Within a StorSimple Data Manager service, you need to create a data transformation job definition.</span></span> <span data-ttu-id="d84d5-124">針對您想要以原生格式移至儲存體帳戶的資料，作業定義指定其詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d84d5-124">A job definition specifies details of the data that you are interested in moving into a storage account in the native format.</span></span> 

<span data-ttu-id="d84d5-125">執行下列步驟來建立新的資料轉換作業定義。</span><span class="sxs-lookup"><span data-stu-id="d84d5-125">Perform the following steps to create a new data transformation job definition.</span></span>

1.  <span data-ttu-id="d84d5-126">瀏覽至您所建立的服務。</span><span class="sxs-lookup"><span data-stu-id="d84d5-126">Navigate to the service that you created.</span></span> <span data-ttu-id="d84d5-127">按一下 [+ 作業定義]。</span><span class="sxs-lookup"><span data-stu-id="d84d5-127">Click **+ Job Definition**.</span></span>

    ![按一下 [+ 作業定義]](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="d84d5-129">新的作業定義刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d84d5-129">The new job definition blade opens up.</span></span> <span data-ttu-id="d84d5-130">指定作業定義名稱，然後按一下 [來源]。</span><span class="sxs-lookup"><span data-stu-id="d84d5-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="d84d5-131">在 [設定資料來源] 刀鋒視窗中，指定您的 StorSimple 裝置和感興趣資料的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d84d5-131">In the **Configure data source** blade, specify the details of your StorSimple device and the data of interest.</span></span>

    ![建立作業定義](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="d84d5-133">由於這是新的資料管理員服務，尚未設定任何資料儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d84d5-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="d84d5-134">若要新增您的 StorSimple Manager 做為資料儲存機制，請在資料儲存機制下拉式清單中按一下 [新增]，然後按一下 [新增資料儲存機制]。</span><span class="sxs-lookup"><span data-stu-id="d84d5-134">To add your StorSimple Manager as a data repository, click **Add new** in the data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="d84d5-135">選擇 [StorSimple 8000 系列 Manager] 做為儲存機制類型，然後輸入 **StorSimple Manager** 的屬性。</span><span class="sxs-lookup"><span data-stu-id="d84d5-135">Choose **StorSimple 8000 series Manager** as the repository type and enter the properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="d84d5-136">在 [資源識別碼] 欄位中，您必須輸入 StorSimple Manager 註冊金鑰中 **:** 前面的數字。</span><span class="sxs-lookup"><span data-stu-id="d84d5-136">For the **Resource Id** field, you need to enter the number before the **:** in the registration key of your StorSimple manager.</span></span>

    ![建立資料來源](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="d84d5-138">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d84d5-138">Click **OK** when done.</span></span> <span data-ttu-id="d84d5-139">這樣會儲存您的資料儲存機制，而且此 StorSimple Manager 可以重複使用在其他作業定義中，不需要再次輸入這些參數。</span><span class="sxs-lookup"><span data-stu-id="d84d5-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="d84d5-140">按一下 [確定] 後，經過幾秒，StorSimple Manager 就會出現在下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="d84d5-140">It takes a few seconds after you click **OK** for the StorSimple Manager to show up in the dropdown.</span></span>

6.  <span data-ttu-id="d84d5-141">在 [設定資料來源] 刀鋒視窗中，輸入您感興趣的資料所在的裝置名稱和磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="d84d5-141">In the **Configure data source** blade, enter the device name and the volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="d84d5-142">在 [篩選] 子區段中，輸入您感興趣的資料所在的根目錄 (此欄位的開頭應該為 `\`)。</span><span class="sxs-lookup"><span data-stu-id="d84d5-142">In the **Filter** subsection, enter the root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="d84d5-143">您也可以在這裡新增任何檔案篩選。</span><span class="sxs-lookup"><span data-stu-id="d84d5-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="d84d5-144">資料轉換服務會處理透過快照推送至 Azure 的資料。</span><span class="sxs-lookup"><span data-stu-id="d84d5-144">The data transformation service works on the data that is pushed up to the Azure via snapshots.</span></span> <span data-ttu-id="d84d5-145">執行此作業時，您可以選擇每次執行此作業時進行備份 (以處理最新資料)，或使用雲端中存在的最新備份 (如果您正在使用一些保存資料)。</span><span class="sxs-lookup"><span data-stu-id="d84d5-145">When running this job, you can choose to take a backup every time this job is run (to work on latest data) or to use the last existing backup in the cloud (if you are working on some archived data).</span></span>

    ![新增資料來源詳細資料](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="d84d5-147">接下來，必須設定「目標」設定。</span><span class="sxs-lookup"><span data-stu-id="d84d5-147">Next, the Target settings need to be configured.</span></span> <span data-ttu-id="d84d5-148">有 2 種支援的目標 – Azure 儲存體帳戶和 Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="d84d5-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="d84d5-149">選擇儲存體帳戶，將檔案放入該帳戶中的 blob。</span><span class="sxs-lookup"><span data-stu-id="d84d5-149">Choose storage accounts to put files into blobs in that account.</span></span> <span data-ttu-id="d84d5-150">選擇媒體服務帳戶，將檔案放入該帳戶中的資產。</span><span class="sxs-lookup"><span data-stu-id="d84d5-150">Choose media services account to put files into assets in that account.</span></span> <span data-ttu-id="d84d5-151">同樣地，我們需要新增儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d84d5-151">Again, we need to add a repository.</span></span> <span data-ttu-id="d84d5-152">在下拉式清單中，選取 [新增]，然後選取 [進行設定]。</span><span class="sxs-lookup"><span data-stu-id="d84d5-152">In the dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![建立資料接收](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="d84d5-154">在這裡，您可以選取想要新增的儲存機制類型，以及與儲存機制相關聯的其他參數。</span><span class="sxs-lookup"><span data-stu-id="d84d5-154">Here, you can select the type of repository you want to add and the other parameters associated with the repository.</span></span> <span data-ttu-id="d84d5-155">在這兩種情況下，執行此作業時都會建立儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="d84d5-155">In both cases, a storage queue is created when the job runs.</span></span> <span data-ttu-id="d84d5-156">此佇列中會填入已轉換的 blob 備妥時的相關訊息。</span><span class="sxs-lookup"><span data-stu-id="d84d5-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="d84d5-157">此佇列的名稱與作業定義的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="d84d5-157">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="d84d5-158">如果您選取 [媒體服務] 做為儲存機制類型，則您也可以輸入建立佇列的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="d84d5-158">If you select **Media Services** as the repo type, then you can also enter storage account credentials where the queue is created.</span></span>

    ![新增資料接收詳細資料](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="d84d5-160">新增資料儲存機制之後 (需要幾秒鐘)，您在 [目標帳戶名稱] 的下拉式清單中會看到此儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d84d5-160">After adding the data repository (which takes a few seconds), you will find the repo in the dropdown in the **Target account name**.</span></span>  <span data-ttu-id="d84d5-161">選擇您需要的目標。</span><span class="sxs-lookup"><span data-stu-id="d84d5-161">Choose the target that you need.</span></span>

12. <span data-ttu-id="d84d5-162">按一下 [確定] 來建立作業定義。</span><span class="sxs-lookup"><span data-stu-id="d84d5-162">Click **OK** to create the job definition.</span></span> <span data-ttu-id="d84d5-163">現在已設定作業定義。</span><span class="sxs-lookup"><span data-stu-id="d84d5-163">Your job definition is now set up.</span></span> <span data-ttu-id="d84d5-164">您可以透過 UI 來多次使用此作業定義。</span><span class="sxs-lookup"><span data-stu-id="d84d5-164">You can use this job definition multiple times via the UI.</span></span>

    ![新增作業定義](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-the-job-definition"></a><span data-ttu-id="d84d5-166">執行作業定義</span><span class="sxs-lookup"><span data-stu-id="d84d5-166">Run the job definition</span></span>

<span data-ttu-id="d84d5-167">每當您需要將資料從 StorSimple 移至您在作業定義中指定的儲存體帳戶時，您必須叫用它。</span><span class="sxs-lookup"><span data-stu-id="d84d5-167">Whenever you need to move data from StorSimple to the storage account that you have specified in the job definition, you will need to invoke it.</span></span> <span data-ttu-id="d84d5-168">每次叫用作業時變更參數會比較有彈性。</span><span class="sxs-lookup"><span data-stu-id="d84d5-168">There is some flexibility in changing the parameters every time you invoke the job.</span></span> <span data-ttu-id="d84d5-169">步驟如下：</span><span class="sxs-lookup"><span data-stu-id="d84d5-169">The steps are as follows:</span></span>

1. <span data-ttu-id="d84d5-170">選取您的 StorSimple Data Manager 服務，然後移至 [監視]。</span><span class="sxs-lookup"><span data-stu-id="d84d5-170">Select your StorSimple Data Manager service and go to **Monitoring**.</span></span> <span data-ttu-id="d84d5-171">按一下 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="d84d5-171">Click **Run Now**.</span></span>

    ![Trigger job definition](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="d84d5-173">選擇您想要執行的作業定義。</span><span class="sxs-lookup"><span data-stu-id="d84d5-173">Choose the job definition that you want to run.</span></span> <span data-ttu-id="d84d5-174">按一下 [回合設定]，修改您可能想針對這次作業執行來變更的任何設定。</span><span class="sxs-lookup"><span data-stu-id="d84d5-174">Click **Run settings** to modify any settings that you might want to change for this job run.</span></span>

    ![執行作業設定](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="d84d5-176">按一下 [確定]，然後按一下 [執行] 來啟動您的作業。</span><span class="sxs-lookup"><span data-stu-id="d84d5-176">Click **OK** and then click **Run** to launch your job.</span></span> <span data-ttu-id="d84d5-177">若要監視此作業，請移至 StorSimple Data Manager 的 [作業] 頁面。</span><span class="sxs-lookup"><span data-stu-id="d84d5-177">To monitor this job, go to the **Jobs** page in your StorSimple Data Manager.</span></span>

    ![作業清單及狀態](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="d84d5-179">除了在 [作業] 刀鋒視窗中監視，您也可以聆聽儲存體佇列，每次有檔案從 StorSimple 移至儲存體帳戶時就會加入訊息。</span><span class="sxs-lookup"><span data-stu-id="d84d5-179">In addition to monitoring in the **Jobs** blade, you can also listen on the storage queue where a message is added every time a file is moved from StorSimple to the storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d84d5-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d84d5-180">Next steps</span></span>

<span data-ttu-id="d84d5-181">[使用 .NET SDK 啟動 StorSimple Data Manager 作業](storsimple-data-manager-dotnet-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="d84d5-181">[Use .NET SDK to launch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>