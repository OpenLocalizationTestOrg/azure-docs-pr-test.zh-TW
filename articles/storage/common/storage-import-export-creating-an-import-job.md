---
title: "建立 Azure 匯入/匯出的匯入作業 | Microsoft Docs"
description: "了解如何建立 Microsoft Azure 匯入/匯出服務的匯入。"
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d373d2a0e601f2796719fc5efb8761f276ab24d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-import-job-for-the-azure-importexport-service"></a><span data-ttu-id="13631-103">建立 Azure 匯入/匯出服務的匯入作業</span><span class="sxs-lookup"><span data-stu-id="13631-103">Creating an import job for the Azure Import/Export service</span></span>

<span data-ttu-id="13631-104">使用 REST API 建立 Microsoft Azure 匯入/匯出服務的匯入作業包含下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="13631-104">Creating an import job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="13631-105">利用 Azure 匯入/匯出工具來準備磁碟機。</span><span class="sxs-lookup"><span data-stu-id="13631-105">Preparing drives with the Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="13631-106">取得要寄送磁碟機的位置。</span><span class="sxs-lookup"><span data-stu-id="13631-106">Obtaining the location to which to ship the drive.</span></span>

-   <span data-ttu-id="13631-107">建立匯入作業。</span><span class="sxs-lookup"><span data-stu-id="13631-107">Creating the import job.</span></span>

-   <span data-ttu-id="13631-108">透過支援的貨運服務將磁碟機寄送給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="13631-108">Shipping the drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="13631-109">使用出貨詳細資料更新匯入工作。</span><span class="sxs-lookup"><span data-stu-id="13631-109">Updating the import job with the shipping details.</span></span>

 <span data-ttu-id="13631-110">請參閱[使用 Microsoft Azure 匯入/匯出服務將資料移轉至 Blob 儲存體](storage-import-export-service.md)以取得匯入/匯出服務概觀及示範如何使用 [Azure 入口網站](https://portal.azure.com/)建立和管理匯入與匯出作業的教學課程。</span><span class="sxs-lookup"><span data-stu-id="13631-110">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure  portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-the-azure-importexport-tool"></a><span data-ttu-id="13631-111">準備具有 Azure 匯入/匯出工具的磁碟機</span><span class="sxs-lookup"><span data-stu-id="13631-111">Preparing drives with the Azure Import/Export Tool</span></span>

<span data-ttu-id="13631-112">無論您是透過入口網站或透過 REST API 建立作業，準備匯入作業的磁碟機步驟都相同。</span><span class="sxs-lookup"><span data-stu-id="13631-112">The steps to prepare drives for an import job are the same whether you create the jobvia the portal or via the REST API.</span></span>

<span data-ttu-id="13631-113">以下是磁碟機準備的簡要概觀。</span><span class="sxs-lookup"><span data-stu-id="13631-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="13631-114">請參閱 [Azure 匯入匯出工具參考](storage-import-export-tool-how-to-v1.md)以取得完整指示。</span><span class="sxs-lookup"><span data-stu-id="13631-114">Refer to the [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="13631-115">您可以在[這裡](http://go.microsoft.com/fwlink/?LinkID=301900)下載 Azure 匯入/匯出工具。</span><span class="sxs-lookup"><span data-stu-id="13631-115">You can download the Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="13631-116">準備您的磁碟機包含︰</span><span class="sxs-lookup"><span data-stu-id="13631-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="13631-117">識別要匯入的資料。</span><span class="sxs-lookup"><span data-stu-id="13631-117">Identifying the data to be imported.</span></span>

-   <span data-ttu-id="13631-118">在 Windows Azure 儲存體中識別目的地 blob。</span><span class="sxs-lookup"><span data-stu-id="13631-118">Identifying the destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="13631-119">使用 Azure 匯入/匯出工具，將資料複製到一或多個硬碟。</span><span class="sxs-lookup"><span data-stu-id="13631-119">Using the Azure Import/Export Tool to copy your data to one or more hard drives.</span></span>

 <span data-ttu-id="13631-120">Azure 匯入/匯出工具也會在備妥時，針對每個磁碟機產生資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="13631-120">The Azure Import/Export Tool will also generate a manifest file for each of the drives as it is prepared.</span></span> <span data-ttu-id="13631-121">資訊清單檔案包含︰</span><span class="sxs-lookup"><span data-stu-id="13631-121">A manifest file contains:</span></span>

-   <span data-ttu-id="13631-122">適用於上傳和從這些檔案對應至 blob 的所有檔案之列舉型別。</span><span class="sxs-lookup"><span data-stu-id="13631-122">An enumeration of all the files intended for upload and the mappings from these files to blobs.</span></span>

-   <span data-ttu-id="13631-123">每個檔案區段的總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="13631-123">Checksums of the segments of each file.</span></span>

-   <span data-ttu-id="13631-124">與每個 blob 相關聯的中繼資料及內容的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="13631-124">Information about the metadata and properties to associate with each blob.</span></span>

-   <span data-ttu-id="13631-125">如果要上傳的 blob 與容器中現有的 blob 具有相同名稱時，要採取的動作清單。</span><span class="sxs-lookup"><span data-stu-id="13631-125">A listing of the action to take if a blob that is being uploaded has the same name as an existing blob in the container.</span></span> <span data-ttu-id="13631-126">可能的選項包括︰a) 以 blob 覆寫檔案、b) 保留現有的 blob 並略過上傳檔案、c) 在名稱後面附加尾碼，使它不會與其他檔案衝突。</span><span class="sxs-lookup"><span data-stu-id="13631-126">Possible options are: a) overwrite the blob with the file, b) keep the existing blob and skip uploading the file, c) append a suffix to the name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="13631-127">取得寄送位置</span><span class="sxs-lookup"><span data-stu-id="13631-127">Obtaining your shipping location</span></span>

<span data-ttu-id="13631-128">在建立匯入作業之前，您需要藉由呼叫 [List Locations](/rest/api/storageimportexport/listlocations) 作業來取得寄送位置名稱和地址。</span><span class="sxs-lookup"><span data-stu-id="13631-128">Before creating an import job, you need to obtain a shipping location name and address by calling the [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="13631-129">`List Locations` 會傳回位置及其郵寄地址的清單。</span><span class="sxs-lookup"><span data-stu-id="13631-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="13631-130">您可以從傳回的清單中選取位置，並將您的硬碟寄送至該地址。</span><span class="sxs-lookup"><span data-stu-id="13631-130">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="13631-131">您也可以使用 `Get Location` 作業來直接取得特定位置的寄送地址。</span><span class="sxs-lookup"><span data-stu-id="13631-131">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

 <span data-ttu-id="13631-132">請遵循下列步驟來取得寄送位置︰</span><span class="sxs-lookup"><span data-stu-id="13631-132">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="13631-133">識別儲存體帳戶位置的名稱。</span><span class="sxs-lookup"><span data-stu-id="13631-133">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="13631-134">您可以在 Azure 入口網站中儲存體帳戶「儀表板」上的 [位置] 欄位下找到此值，或使用服務管理 API 作業[取得儲存體帳戶屬性](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)來查詢此值。</span><span class="sxs-lookup"><span data-stu-id="13631-134">This value can be found under the **Location** field on the storage account's **Dashboard** in the Azure portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="13631-135">藉由呼叫 `Get Location` 作業來擷取可用來處理此儲存體帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="13631-135">Retrieve the location that is available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="13631-136">如果位置的 `AlternateLocations` 屬性包含位置本身，則可以使用此位置。</span><span class="sxs-lookup"><span data-stu-id="13631-136">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="13631-137">否則，使用其中一個替代位置再次呼叫 `Get Location` 作業。</span><span class="sxs-lookup"><span data-stu-id="13631-137">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="13631-138">原始位置可能暫時關閉進行維護。</span><span class="sxs-lookup"><span data-stu-id="13631-138">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-import-job"></a><span data-ttu-id="13631-139">建立匯入作業</span><span class="sxs-lookup"><span data-stu-id="13631-139">Creating the import job</span></span>
<span data-ttu-id="13631-140">若要建立匯入作業，請呼叫 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 作業。</span><span class="sxs-lookup"><span data-stu-id="13631-140">To create the import job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="13631-141">您必須提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="13631-141">You will need to provide the following information:</span></span>

-   <span data-ttu-id="13631-142">作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="13631-142">A name for the job.</span></span>

-   <span data-ttu-id="13631-143">儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="13631-143">The storage account name.</span></span>

-   <span data-ttu-id="13631-144">從上一個步驟中取得的寄送位置名稱。</span><span class="sxs-lookup"><span data-stu-id="13631-144">The shipping location name, obtained from the previous step.</span></span>

-   <span data-ttu-id="13631-145">作業類型 (匯入)。</span><span class="sxs-lookup"><span data-stu-id="13631-145">A job type (Import).</span></span>

-   <span data-ttu-id="13631-146">在匯入作業完成之後要傳送磁碟機的傳回位址。</span><span class="sxs-lookup"><span data-stu-id="13631-146">The return address where the drives should be sent after the import job has completed.</span></span>

-   <span data-ttu-id="13631-147">在作業中的磁碟機清單。</span><span class="sxs-lookup"><span data-stu-id="13631-147">The list of drives in the job.</span></span> <span data-ttu-id="13631-148">針對每個磁碟機，您必須包含下列磁碟機準備步驟期間取得的資訊︰</span><span class="sxs-lookup"><span data-stu-id="13631-148">For each drive, you must include the following information that was obtained during the drive preparation step:</span></span>

    -   <span data-ttu-id="13631-149">磁碟機識別碼</span><span class="sxs-lookup"><span data-stu-id="13631-149">The drive Id</span></span>

    -   <span data-ttu-id="13631-150">BitLocker 金鑰</span><span class="sxs-lookup"><span data-stu-id="13631-150">The BitLocker key</span></span>

    -   <span data-ttu-id="13631-151">硬碟上的資訊清單檔案相對路徑</span><span class="sxs-lookup"><span data-stu-id="13631-151">The manifest file relative path on the hard drive</span></span>

    -   <span data-ttu-id="13631-152">Base16 編碼資訊清單檔案 MD5 雜湊</span><span class="sxs-lookup"><span data-stu-id="13631-152">The Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="13631-153">寄送您的磁碟機</span><span class="sxs-lookup"><span data-stu-id="13631-153">Shipping your drives</span></span>
<span data-ttu-id="13631-154">您必須將磁碟機寄送到從上一個步驟取得的地址，且您必須提供具有包裹追蹤號碼的匯入/匯出服務。</span><span class="sxs-lookup"><span data-stu-id="13631-154">You must ship your drives to the address that you obtained from the previous step, and you must provide the Import/Export service with the tracking number of the package.</span></span>

> [!NOTE]
>  <span data-ttu-id="13631-155">您必須透過支援的貨運服務公司 (會提供您的包裹追蹤號碼) 寄送您的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="13631-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-import-job-with-your-shipping-information"></a><span data-ttu-id="13631-156">使用出貨資料更新匯入作業</span><span class="sxs-lookup"><span data-stu-id="13631-156">Updating the import job with your shipping information</span></span>
<span data-ttu-id="13631-157">在您取得追蹤號碼之後，請呼叫 [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) 作業以更新貨運公司名稱、作業的追蹤號碼和退貨的貨運公司帳戶號碼。</span><span class="sxs-lookup"><span data-stu-id="13631-157">After you have your tracking number, call the [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation to update the shipping carrier name, the tracking number for the job, and the carrier account number for return shipping.</span></span> <span data-ttu-id="13631-158">您可以選擇性指定磁碟機數目及寄送日期。</span><span class="sxs-lookup"><span data-stu-id="13631-158">You can optionally specify the number of drives and the shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13631-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13631-159">Next steps</span></span>

* [<span data-ttu-id="13631-160">使用匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="13631-160">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
