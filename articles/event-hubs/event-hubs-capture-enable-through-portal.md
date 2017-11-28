---
title: "事件中心擷取 aaaAzure 啟用透過入口網站 |Microsoft 文件"
description: "啟用使用 hello Azure 入口網站的 hello 事件中心擷取功能。"
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
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a><span data-ttu-id="dffdd-103">啟用事件中心擷取使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dffdd-103">Enable Event Hubs Capture using hello Azure portal</span></span>

<span data-ttu-id="dffdd-104">您可以在 hello 事件中心建立期間使用 hello 設定擷取[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="dffdd-104">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dffdd-105">您可以任一擷取 hello 資料 tooan Azure [Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)容器或 tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)帳戶。</span><span class="sxs-lookup"><span data-stu-id="dffdd-105">You can either capture hello data tooan Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-tooan-azure-storage-account"></a><span data-ttu-id="dffdd-106">擷取資料 tooan Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="dffdd-106">Capture data tooan Azure Storage account</span></span>  

<span data-ttu-id="dffdd-107">當您建立事件中樞時，您可以按一下 hello 啟用擷取**上**按鈕在 hello**建立事件中樞**入口網站的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="dffdd-107">When you create an event hub, you can enable Capture by clicking hello **On** button in hello **Create Event Hub** portal blade.</span></span> <span data-ttu-id="dffdd-108">然後依序按一下中指定的儲存體帳戶和容器**Azure 儲存體**在 hello**擷取提供者**方塊。</span><span class="sxs-lookup"><span data-stu-id="dffdd-108">You then specify a Storage Account and container by clicking **Azure Storage** in hello **Capture Provider** box.</span></span> <span data-ttu-id="dffdd-109">事件中心擷取使用儲存體服務對服務驗證，因為您不需要 toospecify 儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="dffdd-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need toospecify a storage connection string.</span></span> <span data-ttu-id="dffdd-110">hello 資源選擇器會自動選取儲存體帳戶的 hello 資源 URI。</span><span class="sxs-lookup"><span data-stu-id="dffdd-110">hello resource picker selects hello resource URI for your storage account automatically.</span></span> <span data-ttu-id="dffdd-111">如果您使用 Azure Resource Manager，您必須以字串形式明確提供此 URI。</span><span class="sxs-lookup"><span data-stu-id="dffdd-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="dffdd-112">hello 預設時間間隔為 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="dffdd-112">hello default time window is 5 minutes.</span></span> <span data-ttu-id="dffdd-113">hello 最小值為 1，最多 15 hello。</span><span class="sxs-lookup"><span data-stu-id="dffdd-113">hello minimum value is 1, hello maximum 15.</span></span> <span data-ttu-id="dffdd-114">hello**大小**視窗有 10-500 MB 的範圍。</span><span class="sxs-lookup"><span data-stu-id="dffdd-114">hello **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a><span data-ttu-id="dffdd-115">擷取資料 tooan Azure Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="dffdd-115">Capture data tooan Azure Data Lake Store account</span></span>

<span data-ttu-id="dffdd-116">toocapture 資料 tooAzure 資料湖存放區，您建立的 Data Lake Store 帳戶，以及事件中心：</span><span class="sxs-lookup"><span data-stu-id="dffdd-116">toocapture data tooAzure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="dffdd-117">建立 Azure Data Lake Store 帳戶和資料夾</span><span class="sxs-lookup"><span data-stu-id="dffdd-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="dffdd-118">建立 Data Lake Store 帳戶中的 hello 指示[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](../data-lake-store/data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="dffdd-118">Create a Data Lake Store account, following hello instructions in [Get started with Azure Data Lake Store using hello Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="dffdd-119">此帳戶時，遵照 hello 中的 hello 底下建立資料夾[Azure Data Lake Store 帳戶中建立資料夾](../data-lake-store/data-lake-store-get-started-portal.md#createfolder)> 一節。</span><span class="sxs-lookup"><span data-stu-id="dffdd-119">Create a folder under this account, following hello instructions in hello [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="dffdd-120">在 hello Data Lake Store 帳戶刀鋒視窗中，按一下 **資料總管**。</span><span class="sxs-lookup"><span data-stu-id="dffdd-120">In hello Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="dffdd-121">按一下 [存取]。</span><span class="sxs-lookup"><span data-stu-id="dffdd-121">Click **Access**.</span></span>
5. <span data-ttu-id="dffdd-122">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="dffdd-122">Click **Add**.</span></span>
6. <span data-ttu-id="dffdd-123">在 hello**依名稱或電子郵件搜尋**方塊中，輸入**Microsoft.EventHubs** ，然後選取此選項。</span><span class="sxs-lookup"><span data-stu-id="dffdd-123">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="dffdd-124">hello**權限**索引標籤會出現。</span><span class="sxs-lookup"><span data-stu-id="dffdd-124">hello **Permissions** tab appears.</span></span> <span data-ttu-id="dffdd-125">設定 hello 權限，hello 遵循圖所示：</span><span class="sxs-lookup"><span data-stu-id="dffdd-125">Set hello permissions as shown in hello following figure:</span></span>

    ![][6]

8. <span data-ttu-id="dffdd-126">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="dffdd-126">Click **OK**.</span></span>
9. <span data-ttu-id="dffdd-127">現在，建立資料夾 hello 根資料夾中，瀏覽 toohello 目標資料夾，然後按一下 hello 資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="dffdd-127">Now, create a folder in hello root folder by browsing toohello target folder and clicking on hello folder name.</span></span>
10. <span data-ttu-id="dffdd-128">按一下 [存取]。</span><span class="sxs-lookup"><span data-stu-id="dffdd-128">Click **Access**.</span></span>
11. <span data-ttu-id="dffdd-129">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="dffdd-129">Click **Add**.</span></span>
12. <span data-ttu-id="dffdd-130">在 hello**依名稱或電子郵件搜尋**方塊中，輸入**Microsoft.EventHubs** ，然後選取此選項。</span><span class="sxs-lookup"><span data-stu-id="dffdd-130">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="dffdd-131">hello**權限**索引標籤會出現一次。</span><span class="sxs-lookup"><span data-stu-id="dffdd-131">hello **Permissions** tab appears again.</span></span> <span data-ttu-id="dffdd-132">設定 hello 權限，hello 遵循圖所示：</span><span class="sxs-lookup"><span data-stu-id="dffdd-132">Set hello permissions as shown in hello following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="dffdd-133">建立事件中心</span><span class="sxs-lookup"><span data-stu-id="dffdd-133">Create an event hub</span></span>

1. <span data-ttu-id="dffdd-134">請注意該 hello 事件中心必須位於 hello 相同 Azure 訂用帳戶 hello 您剛才建立的 Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="dffdd-134">Note that hello event hub must be in hello same Azure subscription as hello Azure Data Lake Store you just created.</span></span> <span data-ttu-id="dffdd-135">建立 hello 事件中心按一下 hello**上**按鈕底下**擷取**在 hello**建立事件中樞**入口網站的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="dffdd-135">Create hello event hub, clicking hello **On** button under **Capture** in hello **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="dffdd-136">在 hello**建立事件中樞**入口刀鋒視窗中，選取**Azure Data Lake Store**從 hello**擷取提供者**方塊。</span><span class="sxs-lookup"><span data-stu-id="dffdd-136">In hello **Create Event Hub** portal blade, select **Azure Data Lake Store** from hello **Capture Provider** box.</span></span>
3. <span data-ttu-id="dffdd-137">在**選取 Data Lake Store**，指定 hello Data Lake Store 帳戶的密碼之前，而且 hello**資料湖路徑**欄位中，輸入您所建立的 hello 路徑 toohello 資料資料夾。</span><span class="sxs-lookup"><span data-stu-id="dffdd-137">In **Select Data Lake Store**, specify hello Data Lake Store account you created previously, and in hello **Data Lake Path** field, enter hello path toohello data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="dffdd-138">在現有的事件中樞上新增或設定擷取功能</span><span class="sxs-lookup"><span data-stu-id="dffdd-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="dffdd-139">您可以在位於事件中樞命名空間的現有事件中樞上設定擷取功能。</span><span class="sxs-lookup"><span data-stu-id="dffdd-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="dffdd-140">tooenable 擷取現有的事件中心或 toochange 上擷取設定，請按一下 hello 命名空間 tooload hello **Essentials**刀鋒視窗中，然後按一下您想 tooenable 或變更 hello 擷取設定 hello 事件中心。</span><span class="sxs-lookup"><span data-stu-id="dffdd-140">tooenable Capture on an existing event hub, or toochange your Capture settings, click hello namespace tooload hello **Essentials** blade, then click hello event hub for which you want tooenable or change hello Capture setting.</span></span> <span data-ttu-id="dffdd-141">最後，按一下 hello**屬性**hello 區段開啟刀鋒視窗並再編輯 hello 擷取設定，hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="dffdd-141">Finally, click hello **Properties** section of hello open blade and then edit hello Capture settings, as shown in hello following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="dffdd-142">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="dffdd-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="dffdd-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="dffdd-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="dffdd-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dffdd-144">Next steps</span></span>

<span data-ttu-id="dffdd-145">您也可以透過 Azure Resource Manager 範本來設定事件中樞擷取。</span><span class="sxs-lookup"><span data-stu-id="dffdd-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="dffdd-146">如需詳細資訊，請參閱[使用 Azure Resource Manager 範本啟用擷取功能](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)。</span><span class="sxs-lookup"><span data-stu-id="dffdd-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
