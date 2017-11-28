---
title: "建立 Azure 匯入/匯出的匯出作業 | Microsoft Docs"
description: "了解如何建立 Microsoft Azure 匯入/匯出服務的匯出作業。"
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
ms.openlocfilehash: bdeac373aa8270bd9de8f135ec7166d744fd83ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-export-job-for-the-azure-importexport-service"></a><span data-ttu-id="ca0c9-103">建立 Azure 匯入/匯出服務的匯出作業</span><span class="sxs-lookup"><span data-stu-id="ca0c9-103">Creating an export job for the Azure Import/Export service</span></span>
<span data-ttu-id="ca0c9-104">使用 REST API 建立 Microsoft Azure 匯入/匯出服務的匯出作業包含下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="ca0c9-104">Creating an export job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="ca0c9-105">選取要匯出的 blob。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-105">Selecting the blobs to export.</span></span>

-   <span data-ttu-id="ca0c9-106">取得寄送位置。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="ca0c9-107">建立匯出作業。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-107">Creating the export job.</span></span>

-   <span data-ttu-id="ca0c9-108">透過支援的貨運服務將您的空磁碟機寄送給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-108">Shipping your empty drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="ca0c9-109">使用封裝資訊更新匯出作業。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-109">Updating the export job with the package information.</span></span>

-   <span data-ttu-id="ca0c9-110">從 Microsoft 接收磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-110">Receiving the drives back from Microsoft.</span></span>

 <span data-ttu-id="ca0c9-111">請參閱[使用 Windows Azure 匯入/匯出服務將資料移轉至 Blob 儲存體](storage-import-export-service.md)以取得匯入/匯出服務概觀及示範如何使用 [Azure 入口網站](https://portal.azure.com/)建立和管理匯入與匯出作業的教學課程。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-111">See [Using the Windows Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="selecting-blobs-to-export"></a><span data-ttu-id="ca0c9-112">選取要匯出的 blob</span><span class="sxs-lookup"><span data-stu-id="ca0c9-112">Selecting blobs to export</span></span>
 <span data-ttu-id="ca0c9-113">若要建立匯出作業，您必須提供您要從儲存體帳戶匯出的 blob 清單。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-113">To create an export job, you will need to provide a list of blobs that you want to export from your storage account.</span></span> <span data-ttu-id="ca0c9-114">有幾種方式可選取要匯出的 blob：</span><span class="sxs-lookup"><span data-stu-id="ca0c9-114">There are a few ways to select blobs to be exported:</span></span>

-   <span data-ttu-id="ca0c9-115">您可以使用相對 blob 路徑選取單一 blob 和其所有快照。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-115">You can use a relative blob path to select a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="ca0c9-116">您可以使用相對 blob 路徑選取單一 blob，但其快照除外。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-116">You can use a relative blob path to select a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="ca0c9-117">您可以使用相對 blob 路徑和快照時間選取單一快照。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-117">You can use a relative blob path and a snapshot time to select a single snapshot.</span></span>

-   <span data-ttu-id="ca0c9-118">您可以使用 blob 首碼選取所有的 blob 和具有指定前置詞的快照。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-118">You can use a blob prefix to select all blobs and snapshots with the given prefix.</span></span>

-   <span data-ttu-id="ca0c9-119">您可以匯出儲存體帳戶中所有的 blob 和快照。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-119">You can export all blobs and snapshots in the storage account.</span></span>

 <span data-ttu-id="ca0c9-120">如需指定要匯出之 blob 的詳細資訊，請參閱 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 作業。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-120">For more information about specifying blobs to export, see the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="ca0c9-121">取得寄送位置</span><span class="sxs-lookup"><span data-stu-id="ca0c9-121">Obtaining your shipping location</span></span>
<span data-ttu-id="ca0c9-122">在建立匯出作業之前，您需要藉由呼叫 [Get Location](https://portal.azure.com) 或 [List Locations](/rest/api/storageimportexport/listlocations) 作業來取得寄送位置名稱和地址。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-122">Before creating an export job, you need to obtain a shipping location name and address by calling the [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="ca0c9-123">`List Locations` 會傳回位置及其郵寄地址的清單。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="ca0c9-124">您可以從傳回的清單中選取位置，並將您的硬碟寄送至該地址。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-124">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="ca0c9-125">您也可以使用 `Get Location` 作業來直接取得特定位置的寄送地址。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-125">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

<span data-ttu-id="ca0c9-126">請遵循下列步驟來取得寄送位置︰</span><span class="sxs-lookup"><span data-stu-id="ca0c9-126">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="ca0c9-127">識別儲存體帳戶位置的名稱。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-127">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="ca0c9-128">您可以在傳統入口網站中儲存體帳戶「儀表板」上的 [位置] 欄位下找到此值，或使用服務管理 API 作業[取得儲存體帳戶屬性](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)來查詢此值。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-128">This value can be found under the **Location** field on the storage account's **Dashboard** in the classic portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="ca0c9-129">藉由呼叫 `Get Location` 作業來擷取可用來處理此儲存體帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-129">Retrieve the location that are available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="ca0c9-130">如果位置的 `AlternateLocations` 屬性包含位置本身，則可以使用此位置。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-130">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="ca0c9-131">否則，使用其中一個替代位置再次呼叫 `Get Location` 作業。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-131">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="ca0c9-132">原始位置可能暫時關閉進行維護。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-132">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-export-job"></a><span data-ttu-id="ca0c9-133">建立匯出作業</span><span class="sxs-lookup"><span data-stu-id="ca0c9-133">Creating the export job</span></span>
 <span data-ttu-id="ca0c9-134">若要建立匯出作業，請呼叫 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 作業。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-134">To create the export job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="ca0c9-135">您必須提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="ca0c9-135">You will need to provide the following information:</span></span>

-   <span data-ttu-id="ca0c9-136">作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-136">A name for the job.</span></span>

-   <span data-ttu-id="ca0c9-137">儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-137">The storage account name.</span></span>

-   <span data-ttu-id="ca0c9-138">在上一個步驟中取得的寄送位置名稱。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-138">The shipping location name, obtained in the previous step.</span></span>

-   <span data-ttu-id="ca0c9-139">作業類型 (匯出)。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-139">A job type (Export).</span></span>

-   <span data-ttu-id="ca0c9-140">在匯出作業完成之後要傳送磁碟機的傳回位址。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-140">The return address where the drives should be sent after the export job has completed.</span></span>

-   <span data-ttu-id="ca0c9-141">要匯出的 blob (或 blob 前置詞) 清單。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-141">The list of blobs (or blob prefixes) to be exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="ca0c9-142">寄送您的磁碟機</span><span class="sxs-lookup"><span data-stu-id="ca0c9-142">Shipping your drives</span></span>
 <span data-ttu-id="ca0c9-143">接下來，根據您選取要匯出的 blob 和磁碟機大小，使用 Azure 匯入/匯出工具來判斷需要傳送的磁碟機數目。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-143">Next, use the Azure Import/Export Tool to determine the number of drives you need to send, based on the blobs you have selected to be exported and the drive size.</span></span> <span data-ttu-id="ca0c9-144">如需詳細資訊，請參閱 [Azure 匯入/匯出工具參考](storage-import-export-tool-how-to-v1.md)。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-144">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="ca0c9-145">將磁碟機封裝在單一包裹中，並將它們寄送至先前步驟中所取得的地址。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-145">Package the drives in a single package and ship them to the address obtained in the earlier step.</span></span> <span data-ttu-id="ca0c9-146">下一個步驟中請注意您的包裹追蹤號碼。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-146">Note the tracking number of your package for the next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="ca0c9-147">您必須透過支援的貨運服務公司 (會提供您的包裹追蹤號碼) 寄送您的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-export-job-with-your-package-information"></a><span data-ttu-id="ca0c9-148">使用包裹資訊更新匯出作業</span><span class="sxs-lookup"><span data-stu-id="ca0c9-148">Updating the export job with your package information</span></span>
 <span data-ttu-id="ca0c9-149">在您取得追蹤號碼之後，請呼叫 [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 作業以更新貨運公司名稱和作業的追蹤號碼。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-149">After you have your tracking number, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation to updated the carrier name and tracking number for the job.</span></span> <span data-ttu-id="ca0c9-150">您可以選擇性指定磁碟機數目、寄件者地址及寄送日期。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-150">You can optionally specify the number of drives, the return address, and the shipping date as well.</span></span>

## <a name="receiving-the-package"></a><span data-ttu-id="ca0c9-151">接收包裹</span><span class="sxs-lookup"><span data-stu-id="ca0c9-151">Receiving the package</span></span>
 <span data-ttu-id="ca0c9-152">匯出作業處理完成之後，會將您的磁碟機退回給您，並包含您的加密資料。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-152">After your export job has been processed, your drives will be returned to you with your encrypted data.</span></span> <span data-ttu-id="ca0c9-153">您也可以藉由呼叫 [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) 作業來擷取每個磁碟機的 BitLocker 金鑰。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-153">You can retrieve the BitLocker key for each of the drives by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="ca0c9-154">然後您就可以使用金鑰來解除鎖定磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-154">You can then unlock the drive using the key.</span></span> <span data-ttu-id="ca0c9-155">每個磁碟機上的磁碟機資訊清單檔案包含磁碟機上的檔案清單，以及每個檔案的原始 blob 位址。</span><span class="sxs-lookup"><span data-stu-id="ca0c9-155">The drive manifest file on each drive contains the list of files on the drive, as well as the original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca0c9-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca0c9-156">Next steps</span></span>

* [<span data-ttu-id="ca0c9-157">使用匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="ca0c9-157">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
