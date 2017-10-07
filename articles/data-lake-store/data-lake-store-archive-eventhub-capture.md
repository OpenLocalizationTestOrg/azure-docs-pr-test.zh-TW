---
title: "從事件中心至 Azure Data Lake Store aaaCapture 資料 |Microsoft 文件"
description: "使用 Azure Data Lake Store toocapture 資料，從事件中樞"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a><span data-ttu-id="fb363-103">使用 Azure Data Lake Store toocapture 資料，從事件中樞</span><span class="sxs-lookup"><span data-stu-id="fb363-103">Use Azure Data Lake Store toocapture data from Event Hubs</span></span>

<span data-ttu-id="fb363-104">了解 Azure 事件中樞所收到 toouse Azure Data Lake Store toocapture 資料的方式。</span><span class="sxs-lookup"><span data-stu-id="fb363-104">Learn how toouse Azure Data Lake Store toocapture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb363-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="fb363-105">Prerequisites</span></span>

* <span data-ttu-id="fb363-106">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="fb363-106">**An Azure subscription**.</span></span> <span data-ttu-id="fb363-107">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="fb363-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="fb363-108">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="fb363-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="fb363-109">如需有關指示 toocreate 一個，請參閱[開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="fb363-109">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="fb363-110">**事件中樞命名空間**。</span><span class="sxs-lookup"><span data-stu-id="fb363-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="fb363-111">如需相關指示，請參閱[建立事件中樞命名空間](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace)。</span><span class="sxs-lookup"><span data-stu-id="fb363-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="fb363-112">請確定 hello Data Lake Store 帳戶和 hello 事件中樞命名空間位於 hello 相同的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fb363-112">Make sure hello Data Lake Store account and hello Event Hubs namespace are in hello same Azure subscription.</span></span>


## <a name="assign-permissions-tooevent-hubs"></a><span data-ttu-id="fb363-113">指派權限 tooEvent 集線器</span><span class="sxs-lookup"><span data-stu-id="fb363-113">Assign permissions tooEvent Hubs</span></span>

<span data-ttu-id="fb363-114">在本節中，您可以建立 hello 帳戶內您要從事件中樞 toocapture hello 資料所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="fb363-114">In this section, you create a folder within hello account where you want toocapture hello data from Event Hubs.</span></span> <span data-ttu-id="fb363-115">您也指派權限 tooEvent 中心，讓它可以將資料寫入 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fb363-115">You also assign permissions tooEvent Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="fb363-116">開啟您想要從事件中樞 toocapture 資料，然後按一下其中 hello Data Lake Store 帳戶**資料總管**。</span><span class="sxs-lookup"><span data-stu-id="fb363-116">Open hello Data Lake Store account where you want toocapture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="fb363-117">![Data Lake Store 資料總管](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store 資料總管")</span><span class="sxs-lookup"><span data-stu-id="fb363-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="fb363-118">按一下**新資料夾**，然後輸入您要 toocapture hello 資料所在的資料夾的名稱。</span><span class="sxs-lookup"><span data-stu-id="fb363-118">Click **New Folder** and then enter a name for folder where you want toocapture hello data.</span></span>

    <span data-ttu-id="fb363-119">![在 Data Lake Store 中建立新的資料夾](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "在 Data Lake Store 中建立新的資料夾")</span><span class="sxs-lookup"><span data-stu-id="fb363-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="fb363-120">指派在 hello 根目錄的 hello 資料湖存放區的權限。</span><span class="sxs-lookup"><span data-stu-id="fb363-120">Assign permissions at hello root of hello Data Lake Store.</span></span> 

    <span data-ttu-id="fb363-121">a.</span><span class="sxs-lookup"><span data-stu-id="fb363-121">a.</span></span> <span data-ttu-id="fb363-122">按一下**資料總管**選取的 hello Data Lake Store 帳戶的 hello 根目錄，然後按一下**存取**。</span><span class="sxs-lookup"><span data-stu-id="fb363-122">Click **Data Explorer**, select hello root of hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="fb363-123">![為 Data Lake Store 根目錄指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "為 Data Lake Store 根目錄指派權限")</span><span class="sxs-lookup"><span data-stu-id="fb363-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="fb363-124">b.</span><span class="sxs-lookup"><span data-stu-id="fb363-124">b.</span></span> <span data-ttu-id="fb363-125">在 [存取] 下，依序按一下 [新增] 和 [選取使用者或群組]，然後搜尋 `Microsoft.EventHubs`。</span><span class="sxs-lookup"><span data-stu-id="fb363-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="fb363-126">![為 Data Lake Store 根目錄指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "為 Data Lake Store 根目錄指派權限")</span><span class="sxs-lookup"><span data-stu-id="fb363-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="fb363-127">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="fb363-127">Click **Select**.</span></span>

    <span data-ttu-id="fb363-128">c.</span><span class="sxs-lookup"><span data-stu-id="fb363-128">c.</span></span> <span data-ttu-id="fb363-129">在 [指派權限] 下，按一下 [選取權限]。</span><span class="sxs-lookup"><span data-stu-id="fb363-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="fb363-130">設定**權限**太**Execute**。</span><span class="sxs-lookup"><span data-stu-id="fb363-130">Set **Permissions** too**Execute**.</span></span> <span data-ttu-id="fb363-131">設定**加入**太**這個資料夾和所有子系**。</span><span class="sxs-lookup"><span data-stu-id="fb363-131">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="fb363-132">設定**加入做為**太**的存取權限項目和預設權限項目**。</span><span class="sxs-lookup"><span data-stu-id="fb363-132">Set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="fb363-133">![為 Data Lake Store 根目錄指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "為 Data Lake Store 根目錄指派權限")</span><span class="sxs-lookup"><span data-stu-id="fb363-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="fb363-134">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fb363-134">Click **OK**.</span></span>

4. <span data-ttu-id="fb363-135">指派您要 toocapture 資料 Data Lake Store 帳戶的 hello 資料夾的權限。</span><span class="sxs-lookup"><span data-stu-id="fb363-135">Assign permissions for hello folder under Data Lake Store account where you want toocapture data.</span></span>

    <span data-ttu-id="fb363-136">a.</span><span class="sxs-lookup"><span data-stu-id="fb363-136">a.</span></span> <span data-ttu-id="fb363-137">按一下**資料總管**選取 hello Data Lake Store 帳戶中的 hello 資料夾，然後按**存取**。</span><span class="sxs-lookup"><span data-stu-id="fb363-137">Click **Data Explorer**, select hello folder in hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="fb363-138">![為 Data Lake Store 資料夾指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "為 Data Lake Store 資料夾指派權限")</span><span class="sxs-lookup"><span data-stu-id="fb363-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="fb363-139">b.</span><span class="sxs-lookup"><span data-stu-id="fb363-139">b.</span></span> <span data-ttu-id="fb363-140">在 [存取] 下，依序按一下 [新增] 和 [選取使用者或群組]，然後搜尋 `Microsoft.EventHubs`。</span><span class="sxs-lookup"><span data-stu-id="fb363-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="fb363-141">![為 Data Lake Store 資料夾指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "為 Data Lake Store 資料夾指派權限")</span><span class="sxs-lookup"><span data-stu-id="fb363-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="fb363-142">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="fb363-142">Click **Select**.</span></span>

    <span data-ttu-id="fb363-143">c.</span><span class="sxs-lookup"><span data-stu-id="fb363-143">c.</span></span> <span data-ttu-id="fb363-144">在 [指派權限] 下，按一下 [選取權限]。</span><span class="sxs-lookup"><span data-stu-id="fb363-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="fb363-145">設定**權限**太**讀取、 寫入、**和**Execute**。</span><span class="sxs-lookup"><span data-stu-id="fb363-145">Set **Permissions** too**Read, Write,** and **Execute**.</span></span> <span data-ttu-id="fb363-146">設定**加入**太**這個資料夾和所有子系**。</span><span class="sxs-lookup"><span data-stu-id="fb363-146">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="fb363-147">最後，設定**加入做為**太**的存取權限項目和預設權限項目**。</span><span class="sxs-lookup"><span data-stu-id="fb363-147">Finally, set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="fb363-148">![為 Data Lake Store 資料夾指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "為 Data Lake Store 資料夾指派權限")</span><span class="sxs-lookup"><span data-stu-id="fb363-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="fb363-149">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fb363-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a><span data-ttu-id="fb363-150">設定事件中心 toocapture 資料 tooData 湖存放區</span><span class="sxs-lookup"><span data-stu-id="fb363-150">Configure Event Hubs toocapture data tooData Lake Store</span></span>

<span data-ttu-id="fb363-151">在本節中，您會在事件中樞命名空間內建立事件中樞。</span><span class="sxs-lookup"><span data-stu-id="fb363-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="fb363-152">您也可以設定 hello 事件中心 toocapture 資料 tooan Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fb363-152">You also configure hello Event Hub toocapture data tooan Azure Data Lake Store account.</span></span> <span data-ttu-id="fb363-153">本節假設您已建立事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="fb363-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="fb363-154">從 hello**概觀**窗格中的 hello 事件中樞命名空間中，按一下  **+ 事件中心**。</span><span class="sxs-lookup"><span data-stu-id="fb363-154">From hello **Overview** pane of hello Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="fb363-155">![建立事件中樞](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "建立事件中樞")</span><span class="sxs-lookup"><span data-stu-id="fb363-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="fb363-156">提供的值 hello 如下 tooconfigure 事件中心 toocapture 資料 tooData 湖存放區。</span><span class="sxs-lookup"><span data-stu-id="fb363-156">Provide hello following values tooconfigure Event Hubs toocapture data tooData Lake Store.</span></span>

    <span data-ttu-id="fb363-157">![建立事件中樞](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "建立事件中樞")</span><span class="sxs-lookup"><span data-stu-id="fb363-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="fb363-158">a.</span><span class="sxs-lookup"><span data-stu-id="fb363-158">a.</span></span> <span data-ttu-id="fb363-159">提供 hello 事件中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="fb363-159">Provide a name for hello Event Hub.</span></span>
    
    <span data-ttu-id="fb363-160">b.</span><span class="sxs-lookup"><span data-stu-id="fb363-160">b.</span></span> <span data-ttu-id="fb363-161">此教學課程中，設定**資料分割計數**和**訊息保留**toohello 預設值。</span><span class="sxs-lookup"><span data-stu-id="fb363-161">For this tutorial, set **Partition Count** and **Message Retention** toohello default values.</span></span>
    
    <span data-ttu-id="fb363-162">c.</span><span class="sxs-lookup"><span data-stu-id="fb363-162">c.</span></span> <span data-ttu-id="fb363-163">設定**擷取**太**上**。</span><span class="sxs-lookup"><span data-stu-id="fb363-163">Set **Capture** too**On**.</span></span> <span data-ttu-id="fb363-164">設定 hello**時段**(頻率 toocapture) 和**視窗大小**(資料大小 toocapture)。</span><span class="sxs-lookup"><span data-stu-id="fb363-164">Set hello **Time Window** (how frequently toocapture) and **Size Window** (data size toocapture).</span></span> 
    
    <span data-ttu-id="fb363-165">d.</span><span class="sxs-lookup"><span data-stu-id="fb363-165">d.</span></span> <span data-ttu-id="fb363-166">如**擷取提供者**，選取**Azure Data Lake Store**和 hello 選取 hello 您稍早建立的資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="fb363-166">For **Capture Provider**, select **Azure Data Lake Store** and hello select hello Data Lake Store you created earlier.</span></span> <span data-ttu-id="fb363-167">如**資料湖路徑**，輸入 hello hello hello Data Lake Store 帳戶中建立的資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="fb363-167">For **Data Lake Path**, enter hello name of hello folder you created in hello Data Lake Store account.</span></span> <span data-ttu-id="fb363-168">您只需要 tooprovide hello 相對路徑 toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fb363-168">You only need tooprovide hello relative path toohello folder.</span></span>

    <span data-ttu-id="fb363-169">e.</span><span class="sxs-lookup"><span data-stu-id="fb363-169">e.</span></span> <span data-ttu-id="fb363-170">保留 hello**範例擷取檔案名稱格式**toohello 預設值。</span><span class="sxs-lookup"><span data-stu-id="fb363-170">Leave hello **Sample capture file name formats** toohello default value.</span></span> <span data-ttu-id="fb363-171">此選項可控制 hello 建立 hello 擷取資料夾下的資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="fb363-171">This option governs hello folder structure that is created under hello capture folder.</span></span>

    <span data-ttu-id="fb363-172">f.</span><span class="sxs-lookup"><span data-stu-id="fb363-172">f.</span></span> <span data-ttu-id="fb363-173">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fb363-173">Click **Create**.</span></span>

## <a name="test-hello-setup"></a><span data-ttu-id="fb363-174">測試 hello 安裝程式</span><span class="sxs-lookup"><span data-stu-id="fb363-174">Test hello setup</span></span>

<span data-ttu-id="fb363-175">您現在可以傳送資料 toohello Azure 事件中心，以測試 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="fb363-175">You can now test hello solution by sending data toohello Azure Event Hub.</span></span> <span data-ttu-id="fb363-176">請遵循指示 hello[傳送事件 tooAzure 事件中心](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md)。</span><span class="sxs-lookup"><span data-stu-id="fb363-176">Follow hello instructions at [Send events tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="fb363-177">一旦您開始傳送嗨資料，您會看到 hello 資料反映資料湖存放區中，使用您指定的資料夾結構 hello 集。</span><span class="sxs-lookup"><span data-stu-id="fb363-177">Once you start sending hello data, you see hello data reflected in Data Lake Store using hello folder structure you specified.</span></span> <span data-ttu-id="fb363-178">比方說，您看到的資料夾結構，如下列螢幕擷取畫面，您的資料湖存放區中的 hello 中所示。</span><span class="sxs-lookup"><span data-stu-id="fb363-178">For example, you see a folder structure, as shown in hello following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="fb363-179">![Data Lake Store 中的事件中樞資料範例](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Data Lake Store 中的事件中樞資料範例")</span><span class="sxs-lookup"><span data-stu-id="fb363-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="fb363-180">即使您沒有訊息傳送至事件中心，事件中心會寫入 hello Data Lake Store 帳戶只 hello 標頭的空檔案。</span><span class="sxs-lookup"><span data-stu-id="fb363-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just hello headers into hello Data Lake Store account.</span></span> <span data-ttu-id="fb363-181">hello 檔案會寫入在 hello 相同建立 hello 事件中心時您所提供的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="fb363-181">hello files are written at hello same time interval that you provided while creating hello Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="fb363-182">分析 Data Lake 存放區中的資料</span><span class="sxs-lookup"><span data-stu-id="fb363-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="fb363-183">資料湖存放區中 hello 資料之後，您可以執行分析作業 tooprocess 和無暇 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="fb363-183">Once hello data is in Data Lake Store, you can run analytical jobs tooprocess and crunch hello data.</span></span> <span data-ttu-id="fb363-184">請參閱[USQL Avro 範例](https://github.com/Azure/usql/tree/master/Examples/AvroExamples)如何 toodo 此使用 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="fb363-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how toodo this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="fb363-185">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fb363-185">See also</span></span>
* [<span data-ttu-id="fb363-186">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="fb363-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="fb363-187">從 Azure 儲存體 Blob tooData 湖存放區複製資料</span><span class="sxs-lookup"><span data-stu-id="fb363-187">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
