---
title: "匯出工作的 Azure 匯入/匯出 aaaCreate |Microsoft 文件"
description: "了解 toocreate 匯出的 hello Microsoft Azure 匯入/匯出服務的工作。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a><span data-ttu-id="d8798-103">建立匯出工作的 hello Azure 匯入/匯出服務</span><span class="sxs-lookup"><span data-stu-id="d8798-103">Creating an export job for hello Azure Import/Export service</span></span>
<span data-ttu-id="d8798-104">建立匯出工作使用 hello REST API 的 hello Microsoft Azure 匯入/匯出服務包括 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d8798-104">Creating an export job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="d8798-105">選取 hello blob tooexport。</span><span class="sxs-lookup"><span data-stu-id="d8798-105">Selecting hello blobs tooexport.</span></span>

-   <span data-ttu-id="d8798-106">取得寄送位置。</span><span class="sxs-lookup"><span data-stu-id="d8798-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="d8798-107">建立 hello 匯出工作。</span><span class="sxs-lookup"><span data-stu-id="d8798-107">Creating hello export job.</span></span>

-   <span data-ttu-id="d8798-108">傳送您的空磁碟機 tooMicrosoft 透過支援的貨運服務。</span><span class="sxs-lookup"><span data-stu-id="d8798-108">Shipping your empty drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="d8798-109">使用 hello 封裝資訊更新 hello 匯出作業。</span><span class="sxs-lookup"><span data-stu-id="d8798-109">Updating hello export job with hello package information.</span></span>

-   <span data-ttu-id="d8798-110">從 Microsoft 接收 hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="d8798-110">Receiving hello drives back from Microsoft.</span></span>

 <span data-ttu-id="d8798-111">請參閱[使用 hello Windows Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](storage-import-export-service.md)概觀 hello 匯入/匯出服務和教學課程示範如何 toouse hello [Azure 入口網站](https://portal.azure.com/)toocreate 及管理匯入和匯出工作。</span><span class="sxs-lookup"><span data-stu-id="d8798-111">See [Using hello Windows Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="selecting-blobs-tooexport"></a><span data-ttu-id="d8798-112">選取 blob tooexport</span><span class="sxs-lookup"><span data-stu-id="d8798-112">Selecting blobs tooexport</span></span>
 <span data-ttu-id="d8798-113">toocreate 匯出工作，您將需要 tooprovide 的 tooexport 從儲存體帳戶的 blob 清單。</span><span class="sxs-lookup"><span data-stu-id="d8798-113">toocreate an export job, you will need tooprovide a list of blobs that you want tooexport from your storage account.</span></span> <span data-ttu-id="d8798-114">有幾種方式 tooselect blob toobe 匯出：</span><span class="sxs-lookup"><span data-stu-id="d8798-114">There are a few ways tooselect blobs toobe exported:</span></span>

-   <span data-ttu-id="d8798-115">您可以使用相對 blob 路徑 tooselect 單一 blob 和其所有快照集。</span><span class="sxs-lookup"><span data-stu-id="d8798-115">You can use a relative blob path tooselect a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="d8798-116">您可以使用相對 blob 路徑 tooselect 單一 blob 但排除其快照集。</span><span class="sxs-lookup"><span data-stu-id="d8798-116">You can use a relative blob path tooselect a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="d8798-117">您可以使用相對 blob 路徑和快照集時間 tooselect 單一快照集。</span><span class="sxs-lookup"><span data-stu-id="d8798-117">You can use a relative blob path and a snapshot time tooselect a single snapshot.</span></span>

-   <span data-ttu-id="d8798-118">可以使用 blob 前置詞 tooselect 所有 blob 和快照集，以指定前置詞的 hello。</span><span class="sxs-lookup"><span data-stu-id="d8798-118">You can use a blob prefix tooselect all blobs and snapshots with hello given prefix.</span></span>

-   <span data-ttu-id="d8798-119">您可以匯出所有 blob 和快照 hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="d8798-119">You can export all blobs and snapshots in hello storage account.</span></span>

 <span data-ttu-id="d8798-120">如需有關指定 blob tooexport，請參閱 < hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)作業。</span><span class="sxs-lookup"><span data-stu-id="d8798-120">For more information about specifying blobs tooexport, see hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="d8798-121">取得寄送位置</span><span class="sxs-lookup"><span data-stu-id="d8798-121">Obtaining your shipping location</span></span>
<span data-ttu-id="d8798-122">在建立匯出工作之前，您需要 tooobtain 寄送地點名稱和地址的呼叫 hello[取得位置](https://portal.azure.com)或[列出位置](/rest/api/storageimportexport/listlocations)作業。</span><span class="sxs-lookup"><span data-stu-id="d8798-122">Before creating an export job, you need tooobtain a shipping location name and address by calling hello [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="d8798-123">`List Locations` 會傳回位置及其郵寄地址的清單。</span><span class="sxs-lookup"><span data-stu-id="d8798-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="d8798-124">您可以從 hello 傳回清單中選取位置並寄送您的硬碟機 toothat 地址。</span><span class="sxs-lookup"><span data-stu-id="d8798-124">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="d8798-125">您也可以使用 hello`Get Location`作業 tooobtain hello 直接傳送的特定位置的位址。</span><span class="sxs-lookup"><span data-stu-id="d8798-125">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

<span data-ttu-id="d8798-126">請遵循以下 tooobtain hello 傳送位置 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="d8798-126">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="d8798-127">識別 hello hello 位置的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="d8798-127">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="d8798-128">這個值可以找到 hello**位置**hello 儲存體帳戶的欄位**儀表板**hello 傳統入口網站或使用 hello 服務管理 API 作業的查詢中[取得儲存體帳戶屬性](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)。</span><span class="sxs-lookup"><span data-stu-id="d8798-128">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello classic portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="d8798-129">擷取 hello 位置的可用 tooprocess 這個儲存體帳戶呼叫 hello`Get Location`作業。</span><span class="sxs-lookup"><span data-stu-id="d8798-129">Retrieve hello location that are available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="d8798-130">如果 hello `AlternateLocations` hello 位置包含 hello 位置本身，則無妨 toouse 這個位置。</span><span class="sxs-lookup"><span data-stu-id="d8798-130">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="d8798-131">否則，呼叫 hello`Get Location`使用其中一個 hello 替代位置，然後再次的作業。</span><span class="sxs-lookup"><span data-stu-id="d8798-131">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="d8798-132">維護可能暫時關閉 hello 原始位置。</span><span class="sxs-lookup"><span data-stu-id="d8798-132">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-export-job"></a><span data-ttu-id="d8798-133">建立 hello 匯出工作</span><span class="sxs-lookup"><span data-stu-id="d8798-133">Creating hello export job</span></span>
 <span data-ttu-id="d8798-134">toocreate hello 匯出工作，呼叫 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)作業。</span><span class="sxs-lookup"><span data-stu-id="d8798-134">toocreate hello export job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="d8798-135">您需要下列資訊 tooprovide hello:</span><span class="sxs-lookup"><span data-stu-id="d8798-135">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="d8798-136">Hello 工作的名稱。</span><span class="sxs-lookup"><span data-stu-id="d8798-136">A name for hello job.</span></span>

-   <span data-ttu-id="d8798-137">hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="d8798-137">hello storage account name.</span></span>

-   <span data-ttu-id="d8798-138">hello 傳送 hello 上一個步驟中取得的位置名稱。</span><span class="sxs-lookup"><span data-stu-id="d8798-138">hello shipping location name, obtained in hello previous step.</span></span>

-   <span data-ttu-id="d8798-139">作業類型 (匯出)。</span><span class="sxs-lookup"><span data-stu-id="d8798-139">A job type (Export).</span></span>

-   <span data-ttu-id="d8798-140">hello 傳回位址 hello 匯出作業完成之後，傳送 hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="d8798-140">hello return address where hello drives should be sent after hello export job has completed.</span></span>

-   <span data-ttu-id="d8798-141">hello 的 blob （或 blob 首碼） 清單 toobe 匯出。</span><span class="sxs-lookup"><span data-stu-id="d8798-141">hello list of blobs (or blob prefixes) toobe exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="d8798-142">寄送您的磁碟機</span><span class="sxs-lookup"><span data-stu-id="d8798-142">Shipping your drives</span></span>
 <span data-ttu-id="d8798-143">接著，使用的磁碟機需要 toosend，根據您已選取 toobe 匯出的 hello blob hello Azure 匯入/匯出工具 toodetermine hello 數目並 hello 磁碟機大小。</span><span class="sxs-lookup"><span data-stu-id="d8798-143">Next, use hello Azure Import/Export Tool toodetermine hello number of drives you need toosend, based on hello blobs you have selected toobe exported and hello drive size.</span></span> <span data-ttu-id="d8798-144">請參閱 hello [Azure 匯入/匯出工具參考](storage-import-export-tool-how-to-v1.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d8798-144">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="d8798-145">封裝在單一封裝 hello 磁碟機，並將它們寄送 toohello hello 中取得的地址稍早步驟。</span><span class="sxs-lookup"><span data-stu-id="d8798-145">Package hello drives in a single package and ship them toohello address obtained in hello earlier step.</span></span> <span data-ttu-id="d8798-146">請注意 hello 追蹤您的封裝進行 hello 下一個步驟的數目。</span><span class="sxs-lookup"><span data-stu-id="d8798-146">Note hello tracking number of your package for hello next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="d8798-147">您必須透過支援的貨運服務公司 (會提供您的包裹追蹤號碼) 寄送您的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="d8798-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-export-job-with-your-package-information"></a><span data-ttu-id="d8798-148">使用您的封裝資訊更新 hello 匯出作業</span><span class="sxs-lookup"><span data-stu-id="d8798-148">Updating hello export job with your package information</span></span>
 <span data-ttu-id="d8798-149">取得追蹤號碼之後，請呼叫 hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update)作業 tooupdated hello 電信業者名稱和追蹤號碼 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="d8798-149">After you have your tracking number, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation tooupdated hello carrier name and tracking number for hello job.</span></span> <span data-ttu-id="d8798-150">您可以選擇性地指定 hello 磁碟機數目、 hello 傳回位址及 hello 寄送日期。</span><span class="sxs-lookup"><span data-stu-id="d8798-150">You can optionally specify hello number of drives, hello return address, and hello shipping date as well.</span></span>

## <a name="receiving-hello-package"></a><span data-ttu-id="d8798-151">收到 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="d8798-151">Receiving hello package</span></span>
 <span data-ttu-id="d8798-152">匯出作業處理完成之後，您的磁碟機將會傳回 tooyou 與加密的資料。</span><span class="sxs-lookup"><span data-stu-id="d8798-152">After your export job has been processed, your drives will be returned tooyou with your encrypted data.</span></span> <span data-ttu-id="d8798-153">您可以針對每個由呼叫 hello hello 磁碟機擷取 hello BitLocker 金鑰[Get Job](/rest/api/storageimportexport/jobs#Jobs_Get)作業。</span><span class="sxs-lookup"><span data-stu-id="d8798-153">You can retrieve hello BitLocker key for each of hello drives by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="d8798-154">然後您就可以解除鎖定使用 hello 金鑰 hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="d8798-154">You can then unlock hello drive using hello key.</span></span> <span data-ttu-id="d8798-155">hello 每個磁碟機上的磁碟機資訊清單檔包含 hello hello 磁碟機，以及 hello 原始 blob 位址上的每個檔案的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="d8798-155">hello drive manifest file on each drive contains hello list of files on hello drive, as well as hello original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8798-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8798-156">Next steps</span></span>

* [<span data-ttu-id="d8798-157">使用 hello 匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="d8798-157">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
