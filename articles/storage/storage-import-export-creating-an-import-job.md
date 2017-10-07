---
title: "匯入工作的 Azure 匯入/匯出 aaaCreate |Microsoft 文件"
description: "深入了解如何 toocreate hello Microsoft Azure 匯入/匯出服務的匯入。"
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
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a><span data-ttu-id="b0b97-103">建立 hello Azure 匯入/匯出服務的匯入工作</span><span class="sxs-lookup"><span data-stu-id="b0b97-103">Creating an import job for hello Azure Import/Export service</span></span>

<span data-ttu-id="b0b97-104">建立使用 hello REST API 的 hello Microsoft Azure 匯入/匯出服務匯入工作包括下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b0b97-104">Creating an import job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="b0b97-105">準備磁碟機以 hello Azure 匯入/匯出工具。</span><span class="sxs-lookup"><span data-stu-id="b0b97-105">Preparing drives with hello Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="b0b97-106">取得 hello 位置 toowhich tooship hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="b0b97-106">Obtaining hello location toowhich tooship hello drive.</span></span>

-   <span data-ttu-id="b0b97-107">建立 hello 匯入工作。</span><span class="sxs-lookup"><span data-stu-id="b0b97-107">Creating hello import job.</span></span>

-   <span data-ttu-id="b0b97-108">傳送嗨光碟機 tooMicrosoft 透過支援的貨運服務。</span><span class="sxs-lookup"><span data-stu-id="b0b97-108">Shipping hello drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="b0b97-109">使用 傳送詳細資料的 hello 更新 hello 匯入作業。</span><span class="sxs-lookup"><span data-stu-id="b0b97-109">Updating hello import job with hello shipping details.</span></span>

 <span data-ttu-id="b0b97-110">請參閱[使用 hello Microsoft Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](storage-import-export-service.md)概觀 hello 匯入/匯出服務和教學課程示範如何 toouse hello [Azure 入口網站](https://portal.azure.com/)toocreate 及管理匯入和匯出工作。</span><span class="sxs-lookup"><span data-stu-id="b0b97-110">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure  portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a><span data-ttu-id="b0b97-111">使用 Azure 匯入/匯出工具 hello 準備磁碟機</span><span class="sxs-lookup"><span data-stu-id="b0b97-111">Preparing drives with hello Azure Import/Export Tool</span></span>

<span data-ttu-id="b0b97-112">匯入工作的 hello 步驟 tooprepare 磁碟機是 hello 相同您要建立 hello jobvia hello 入口網站或透過 hello REST API。</span><span class="sxs-lookup"><span data-stu-id="b0b97-112">hello steps tooprepare drives for an import job are hello same whether you create hello jobvia hello portal or via hello REST API.</span></span>

<span data-ttu-id="b0b97-113">以下是磁碟機準備的簡要概觀。</span><span class="sxs-lookup"><span data-stu-id="b0b97-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="b0b97-114">請參閱 toohello [Azure 匯入 ExportTool 參考](storage-import-export-tool-how-to-v1.md)如需完整指示。</span><span class="sxs-lookup"><span data-stu-id="b0b97-114">Refer toohello [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="b0b97-115">您可以下載 Azure 匯入/匯出工具 hello[這裡](http://go.microsoft.com/fwlink/?LinkID=301900)。</span><span class="sxs-lookup"><span data-stu-id="b0b97-115">You can download hello Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="b0b97-116">準備您的磁碟機包含︰</span><span class="sxs-lookup"><span data-stu-id="b0b97-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="b0b97-117">用來識別 hello 資料 toobe 匯入。</span><span class="sxs-lookup"><span data-stu-id="b0b97-117">Identifying hello data toobe imported.</span></span>

-   <span data-ttu-id="b0b97-118">識別 Windows Azure 儲存體中的 hello 目的地 blob。</span><span class="sxs-lookup"><span data-stu-id="b0b97-118">Identifying hello destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="b0b97-119">在使用 hello Azure 匯入/匯出工具 toocopy 資料 tooone 或多個硬碟。</span><span class="sxs-lookup"><span data-stu-id="b0b97-119">Using hello Azure Import/Export Tool toocopy your data tooone or more hard drives.</span></span>

 <span data-ttu-id="b0b97-120">已準備好為其 hello Azure 匯入/匯出工具也會針對每個 hello 磁碟機產生資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="b0b97-120">hello Azure Import/Export Tool will also generate a manifest file for each of hello drives as it is prepared.</span></span> <span data-ttu-id="b0b97-121">資訊清單檔案包含︰</span><span class="sxs-lookup"><span data-stu-id="b0b97-121">A manifest file contains:</span></span>

-   <span data-ttu-id="b0b97-122">列舉所有要上傳並從這些檔案 tooblobs hello 對應的 hello 檔案中。</span><span class="sxs-lookup"><span data-stu-id="b0b97-122">An enumeration of all hello files intended for upload and hello mappings from these files tooblobs.</span></span>

-   <span data-ttu-id="b0b97-123">每個檔案的 hello 區段的總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="b0b97-123">Checksums of hello segments of each file.</span></span>

-   <span data-ttu-id="b0b97-124">Hello 與每個 blob 的中繼資料和屬性 tooassociate 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b0b97-124">Information about hello metadata and properties tooassociate with each blob.</span></span>

-   <span data-ttu-id="b0b97-125">列出的 hello 動作 tootake hello 正在上傳的 blob 有相同的名稱，為 hello 容器中現有的 blob。</span><span class="sxs-lookup"><span data-stu-id="b0b97-125">A listing of hello action tootake if a blob that is being uploaded has hello same name as an existing blob in hello container.</span></span> <span data-ttu-id="b0b97-126">可能的選項包括： a） 檔案，覆寫 hello blob hello、 b） 保留 hello 現有 blob 和略過上傳 hello 檔案、 c） 新增後置詞 toohello 名稱，使它不會使用其他檔案衝突。</span><span class="sxs-lookup"><span data-stu-id="b0b97-126">Possible options are: a) overwrite hello blob with hello file, b) keep hello existing blob and skip uploading hello file, c) append a suffix toohello name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="b0b97-127">取得寄送位置</span><span class="sxs-lookup"><span data-stu-id="b0b97-127">Obtaining your shipping location</span></span>

<span data-ttu-id="b0b97-128">在建立匯入工作之前，您需要 tooobtain 寄送地點名稱和地址的呼叫 hello[列出位置](/rest/api/storageimportexport/listlocations)作業。</span><span class="sxs-lookup"><span data-stu-id="b0b97-128">Before creating an import job, you need tooobtain a shipping location name and address by calling hello [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="b0b97-129">`List Locations` 會傳回位置及其郵寄地址的清單。</span><span class="sxs-lookup"><span data-stu-id="b0b97-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="b0b97-130">您可以從 hello 傳回清單中選取位置並寄送您的硬碟機 toothat 地址。</span><span class="sxs-lookup"><span data-stu-id="b0b97-130">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="b0b97-131">您也可以使用 hello`Get Location`作業 tooobtain hello 直接傳送的特定位置的位址。</span><span class="sxs-lookup"><span data-stu-id="b0b97-131">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

 <span data-ttu-id="b0b97-132">請遵循以下 tooobtain hello 傳送位置 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="b0b97-132">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="b0b97-133">識別 hello hello 位置的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="b0b97-133">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="b0b97-134">這個值可以找到 hello**位置**hello 儲存體帳戶的欄位**儀表板**hello Azure 入口網站或使用 hello 服務管理 API 作業的查詢中[取得儲存體帳戶屬性](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)。</span><span class="sxs-lookup"><span data-stu-id="b0b97-134">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello Azure portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="b0b97-135">擷取可用 tooprocess hello 位置這個儲存體帳戶呼叫 hello`Get Location`作業。</span><span class="sxs-lookup"><span data-stu-id="b0b97-135">Retrieve hello location that is available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="b0b97-136">如果 hello `AlternateLocations` hello 位置包含 hello 位置本身，則無妨 toouse 這個位置。</span><span class="sxs-lookup"><span data-stu-id="b0b97-136">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="b0b97-137">否則，呼叫 hello`Get Location`使用其中一個 hello 替代位置，然後再次的作業。</span><span class="sxs-lookup"><span data-stu-id="b0b97-137">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="b0b97-138">維護可能暫時關閉 hello 原始位置。</span><span class="sxs-lookup"><span data-stu-id="b0b97-138">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-import-job"></a><span data-ttu-id="b0b97-139">建立 hello 匯入工作</span><span class="sxs-lookup"><span data-stu-id="b0b97-139">Creating hello import job</span></span>
<span data-ttu-id="b0b97-140">toocreate hello 匯入工作，呼叫 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)作業。</span><span class="sxs-lookup"><span data-stu-id="b0b97-140">toocreate hello import job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="b0b97-141">您需要下列資訊 tooprovide hello:</span><span class="sxs-lookup"><span data-stu-id="b0b97-141">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="b0b97-142">Hello 工作的名稱。</span><span class="sxs-lookup"><span data-stu-id="b0b97-142">A name for hello job.</span></span>

-   <span data-ttu-id="b0b97-143">hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="b0b97-143">hello storage account name.</span></span>

-   <span data-ttu-id="b0b97-144">hello 傳送 hello 上一個步驟中取得的位置名稱。</span><span class="sxs-lookup"><span data-stu-id="b0b97-144">hello shipping location name, obtained from hello previous step.</span></span>

-   <span data-ttu-id="b0b97-145">作業類型 (匯入)。</span><span class="sxs-lookup"><span data-stu-id="b0b97-145">A job type (Import).</span></span>

-   <span data-ttu-id="b0b97-146">hello 傳回位址 hello 匯入作業完成之後，傳送 hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="b0b97-146">hello return address where hello drives should be sent after hello import job has completed.</span></span>

-   <span data-ttu-id="b0b97-147">hello hello 作業中的磁碟機清單。</span><span class="sxs-lookup"><span data-stu-id="b0b97-147">hello list of drives in hello job.</span></span> <span data-ttu-id="b0b97-148">每個磁碟機，您必須加入 hello 下列 hello 磁碟機準備步驟期間取得的資訊：</span><span class="sxs-lookup"><span data-stu-id="b0b97-148">For each drive, you must include hello following information that was obtained during hello drive preparation step:</span></span>

    -   <span data-ttu-id="b0b97-149">hello 磁碟機識別碼</span><span class="sxs-lookup"><span data-stu-id="b0b97-149">hello drive Id</span></span>

    -   <span data-ttu-id="b0b97-150">hello BitLocker 金鑰</span><span class="sxs-lookup"><span data-stu-id="b0b97-150">hello BitLocker key</span></span>

    -   <span data-ttu-id="b0b97-151">hello hello 硬碟機上的資訊清單檔案相對路徑</span><span class="sxs-lookup"><span data-stu-id="b0b97-151">hello manifest file relative path on hello hard drive</span></span>

    -   <span data-ttu-id="b0b97-152">hello Base16 編碼資訊清單檔案的 MD5 雜湊</span><span class="sxs-lookup"><span data-stu-id="b0b97-152">hello Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="b0b97-153">寄送您的磁碟機</span><span class="sxs-lookup"><span data-stu-id="b0b97-153">Shipping your drives</span></span>
<span data-ttu-id="b0b97-154">您必須提供您取自 hello 先前步驟中，您的磁碟機 toohello 地址，而且您必須提供 hello 匯入/匯出服務以 hello 追蹤 hello 封裝的數目。</span><span class="sxs-lookup"><span data-stu-id="b0b97-154">You must ship your drives toohello address that you obtained from hello previous step, and you must provide hello Import/Export service with hello tracking number of hello package.</span></span>

> [!NOTE]
>  <span data-ttu-id="b0b97-155">您必須透過支援的貨運服務公司 (會提供您的包裹追蹤號碼) 寄送您的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="b0b97-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-import-job-with-your-shipping-information"></a><span data-ttu-id="b0b97-156">使用 出貨資訊更新 hello 匯入作業</span><span class="sxs-lookup"><span data-stu-id="b0b97-156">Updating hello import job with your shipping information</span></span>
<span data-ttu-id="b0b97-157">取得追蹤號碼之後，請呼叫 hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update)作業 tooupdate hello 傳送貨運公司名稱、 hello hello 作業的追蹤號碼與退貨 hello 承運業者帳戶號碼。</span><span class="sxs-lookup"><span data-stu-id="b0b97-157">After you have your tracking number, call hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation tooupdate hello shipping carrier name, hello tracking number for hello job, and hello carrier account number for return shipping.</span></span> <span data-ttu-id="b0b97-158">您可以選擇指定磁碟機和出貨日期以及 hello 的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="b0b97-158">You can optionally specify hello number of drives and hello shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0b97-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b0b97-159">Next steps</span></span>

* [<span data-ttu-id="b0b97-160">使用 hello 匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="b0b97-160">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
