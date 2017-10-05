---
title: "透過入口網站啟用 Azure 事件中樞擷取功能 | Microsoft Docs"
description: "使用 Azure 入口網站啟用事件中樞擷取功能。"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a><span data-ttu-id="14d9d-103">使用 Azure 入口網站啟用事件中樞擷取功能</span><span class="sxs-lookup"><span data-stu-id="14d9d-103">Enable Event Hubs Capture using the Azure portal</span></span>

<span data-ttu-id="14d9d-104">您可以使用 [Azure 入口網站](https://portal.azure.com)，在建立事件中樞時設定擷取功能。</span><span class="sxs-lookup"><span data-stu-id="14d9d-104">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="14d9d-105">您可以將資料擷取至 Azure [Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)容器或 [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="14d9d-105">You can either capture the data to an Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or to an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-to-an-azure-storage-account"></a><span data-ttu-id="14d9d-106">將資料擷取至 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="14d9d-106">Capture data to an Azure Storage account</span></span>  

<span data-ttu-id="14d9d-107">當您建立事件中樞時，您可以按一下來啟用擷取**上**按鈕**建立事件中樞**入口網站的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="14d9d-107">When you create an event hub, you can enable Capture by clicking the **On** button in the **Create Event Hub** portal blade.</span></span> <span data-ttu-id="14d9d-108">然後按一下 [擷取提供者] 方塊中的 [Azure 儲存體]，以指定儲存體帳戶和容器。</span><span class="sxs-lookup"><span data-stu-id="14d9d-108">You then specify a Storage Account and container by clicking **Azure Storage** in the **Capture Provider** box.</span></span> <span data-ttu-id="14d9d-109">事件中樞擷取會對儲存體使用服務對服務驗證，因此您不需要指定儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="14d9d-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need to specify a storage connection string.</span></span> <span data-ttu-id="14d9d-110">資源選擇器會自動選取儲存體帳戶的資源 URI。</span><span class="sxs-lookup"><span data-stu-id="14d9d-110">The resource picker selects the resource URI for your storage account automatically.</span></span> <span data-ttu-id="14d9d-111">如果您使用 Azure Resource Manager，您必須以字串形式明確提供此 URI。</span><span class="sxs-lookup"><span data-stu-id="14d9d-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="14d9d-112">預設時間範圍為 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="14d9d-112">The default time window is 5 minutes.</span></span> <span data-ttu-id="14d9d-113">最小值是 1，最大值是 15。</span><span class="sxs-lookup"><span data-stu-id="14d9d-113">The minimum value is 1, the maximum 15.</span></span> <span data-ttu-id="14d9d-114">**大小** 範圍為 10-500 MB。</span><span class="sxs-lookup"><span data-stu-id="14d9d-114">The **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a><span data-ttu-id="14d9d-115">將資料擷取至 Azure Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="14d9d-115">Capture data to an Azure Data Lake Store account</span></span>

<span data-ttu-id="14d9d-116">若要將資料擷取至 Azure Data Lake Store，請建立 Data Lake Store 帳戶及事件中樞：</span><span class="sxs-lookup"><span data-stu-id="14d9d-116">To capture data to Azure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="14d9d-117">建立 Azure Data Lake Store 帳戶和資料夾</span><span class="sxs-lookup"><span data-stu-id="14d9d-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="14d9d-118">遵循[使用 Azure 入口網站開始使用 Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md) 中的指示，建立 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="14d9d-118">Create a Data Lake Store account, following the instructions in [Get started with Azure Data Lake Store using the Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="14d9d-119">遵循[在 Azure Data Lake Store 帳戶中建立資料夾](../data-lake-store/data-lake-store-get-started-portal.md#createfolder)一節中的指示，在此帳戶下建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="14d9d-119">Create a folder under this account, following the instructions in the [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="14d9d-120">在 [Data Lake Store 帳戶] 刀鋒視窗中，按一下**資料總管**。</span><span class="sxs-lookup"><span data-stu-id="14d9d-120">In the Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="14d9d-121">按一下 [存取]。</span><span class="sxs-lookup"><span data-stu-id="14d9d-121">Click **Access**.</span></span>
5. <span data-ttu-id="14d9d-122">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="14d9d-122">Click **Add**.</span></span>
6. <span data-ttu-id="14d9d-123">在 [依姓名或電子郵件搜尋] 方塊中輸入 **Microsoft.EventHubs**，然後選取此選項。</span><span class="sxs-lookup"><span data-stu-id="14d9d-123">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="14d9d-124">[權限] 索引標籤隨即出現。</span><span class="sxs-lookup"><span data-stu-id="14d9d-124">The **Permissions** tab appears.</span></span> <span data-ttu-id="14d9d-125">設定權限，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="14d9d-125">Set the permissions as shown in the following figure:</span></span>

    ![][6]

8. <span data-ttu-id="14d9d-126">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="14d9d-126">Click **OK**.</span></span>
9. <span data-ttu-id="14d9d-127">現在，瀏覽至目標資料夾，然後按一下資料夾名稱，以在根資料夾中建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="14d9d-127">Now, create a folder in the root folder by browsing to the target folder and clicking on the folder name.</span></span>
10. <span data-ttu-id="14d9d-128">按一下 [存取]。</span><span class="sxs-lookup"><span data-stu-id="14d9d-128">Click **Access**.</span></span>
11. <span data-ttu-id="14d9d-129">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="14d9d-129">Click **Add**.</span></span>
12. <span data-ttu-id="14d9d-130">在 [依姓名或電子郵件搜尋] 方塊中輸入 **Microsoft.EventHubs**，然後選取此選項。</span><span class="sxs-lookup"><span data-stu-id="14d9d-130">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="14d9d-131">[權限] 索引標籤再次出現。</span><span class="sxs-lookup"><span data-stu-id="14d9d-131">The **Permissions** tab appears again.</span></span> <span data-ttu-id="14d9d-132">設定權限，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="14d9d-132">Set the permissions as shown in the following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="14d9d-133">建立事件中心</span><span class="sxs-lookup"><span data-stu-id="14d9d-133">Create an event hub</span></span>

1. <span data-ttu-id="14d9d-134">請注意，事件中樞必須位於與您剛建立之 Azure Data Lake Store 相同的 Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="14d9d-134">Note that the event hub must be in the same Azure subscription as the Azure Data Lake Store you just created.</span></span> <span data-ttu-id="14d9d-135">建立事件中樞中，按一下**上**按鈕底下**擷取**中**建立事件中樞**入口網站的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="14d9d-135">Create the event hub, clicking the **On** button under **Capture** in the **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="14d9d-136">在**建立事件中樞**入口刀鋒視窗中，選取**Azure Data Lake Store**從**擷取提供者**方塊。</span><span class="sxs-lookup"><span data-stu-id="14d9d-136">In the **Create Event Hub** portal blade, select **Azure Data Lake Store** from the **Capture Provider** box.</span></span>
3. <span data-ttu-id="14d9d-137">在 [選取 Data Lake Store] 中，指定您先前建立的 Data Lake Store 帳戶，以及在 [Data Lake 路徑] 欄位中，輸入您建立之資料資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="14d9d-137">In **Select Data Lake Store**, specify the Data Lake Store account you created previously, and in the **Data Lake Path** field, enter the path to the data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="14d9d-138">在現有的事件中樞上新增或設定擷取功能</span><span class="sxs-lookup"><span data-stu-id="14d9d-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="14d9d-139">您可以在位於事件中樞命名空間的現有事件中樞上設定擷取功能。</span><span class="sxs-lookup"><span data-stu-id="14d9d-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="14d9d-140">若要在現有事件中樞上啟用擷取功能，或變更您的擷取設定，請按一下命名空間以載入 [基本資訊] 刀鋒視窗，然後按一下您要啟用或變更擷取設定的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="14d9d-140">To enable Capture on an existing event hub, or to change your Capture settings, click the namespace to load the **Essentials** blade, then click the event hub for which you want to enable or change the Capture setting.</span></span> <span data-ttu-id="14d9d-141">最後，按一下 **屬性**開啟刀鋒視窗的區段，然後編輯擷取設定下, 圖所示：</span><span class="sxs-lookup"><span data-stu-id="14d9d-141">Finally, click the **Properties** section of the open blade and then edit the Capture settings, as shown in the following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="14d9d-142">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="14d9d-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="14d9d-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="14d9d-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="14d9d-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14d9d-144">Next steps</span></span>

<span data-ttu-id="14d9d-145">您也可以透過 Azure Resource Manager 範本來設定事件中樞擷取。</span><span class="sxs-lookup"><span data-stu-id="14d9d-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="14d9d-146">如需詳細資訊，請參閱[使用 Azure Resource Manager 範本啟用擷取功能](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)。</span><span class="sxs-lookup"><span data-stu-id="14d9d-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
