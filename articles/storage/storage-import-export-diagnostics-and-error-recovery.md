---
title: "Azure 匯入匯出作業的診斷和錯誤復原 | Microsoft Docs"
description: "了解如何啟用 Microsoft Azure 匯入/匯出服務作業的詳細資訊記錄。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 0068aae9d6780aa41a070db0eb191d0d5a165d21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="70478-103">Azure 匯入/匯出作業的診斷和錯誤復原</span><span class="sxs-lookup"><span data-stu-id="70478-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="70478-104">針對每個已處理的磁碟機，Azure 匯入/匯出服務會在相關聯的儲存體帳戶中建立錯誤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="70478-104">For each drive processed, the Azure Import/Export service creates an error log in the associated storage account.</span></span> <span data-ttu-id="70478-105">您也可以在呼叫 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 或 [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 作業時，將 `LogLevel` 屬性設定為 `Verbose` 來啟用詳細資訊記錄。</span><span class="sxs-lookup"><span data-stu-id="70478-105">You can also enable verbose logging by setting the `LogLevel` property to `Verbose` when calling the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="70478-106">根據預設，記錄會寫入名為 `waimportexport` 的容器。</span><span class="sxs-lookup"><span data-stu-id="70478-106">By default, logs are written to a container named `waimportexport`.</span></span> <span data-ttu-id="70478-107">您可以在呼叫 `Put Job` 或 `Update Job Properties` 作業時，設定 `DiagnosticsPath` 屬性以指定不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="70478-107">You can specify a different name by setting the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="70478-108">記錄會使用下列的命名慣例儲存為區塊 blob︰`waies/jobname_driveid_timestamp_logtype.xml`。</span><span class="sxs-lookup"><span data-stu-id="70478-108">The logs are stored as block blobs with the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="70478-109">您可以藉由呼叫 [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) 作業來擷取工作的記錄 URI。</span><span class="sxs-lookup"><span data-stu-id="70478-109">You can retrieve the URI of the logs for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="70478-110">會針對每個磁碟機在 `VerboseLogUri` 屬性中傳回詳細資訊記錄檔的 URI，而在 `ErrorLogUri` 屬性中會傳回錯誤記錄檔的 URI。</span><span class="sxs-lookup"><span data-stu-id="70478-110">The URI for the verbose log is returned in the `VerboseLogUri` property for each drive, while the URI for the error log is returned in the `ErrorLogUri` property.</span></span>

<span data-ttu-id="70478-111">您可以使用記錄資料來識別下列問題。</span><span class="sxs-lookup"><span data-stu-id="70478-111">You can use the logging data to identify the following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="70478-112">磁碟機錯誤</span><span class="sxs-lookup"><span data-stu-id="70478-112">Drive errors</span></span>

<span data-ttu-id="70478-113">下列項目會歸類為磁碟機錯誤：</span><span class="sxs-lookup"><span data-stu-id="70478-113">The following items are classified as drive errors:</span></span>

-   <span data-ttu-id="70478-114">存取或讀取資訊清單檔案中的錯誤</span><span class="sxs-lookup"><span data-stu-id="70478-114">Errors in accessing or reading the manifest file</span></span>

-   <span data-ttu-id="70478-115">不正確的 BitLocker 金鑰</span><span class="sxs-lookup"><span data-stu-id="70478-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="70478-116">磁碟機讀取/寫入錯誤</span><span class="sxs-lookup"><span data-stu-id="70478-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="70478-117">Blob 錯誤</span><span class="sxs-lookup"><span data-stu-id="70478-117">Blob errors</span></span>

<span data-ttu-id="70478-118">下列項目會歸類為 blob 錯誤：</span><span class="sxs-lookup"><span data-stu-id="70478-118">The following items are classified as blob errors:</span></span>

-   <span data-ttu-id="70478-119">不正確或衝突的 blob 或名稱</span><span class="sxs-lookup"><span data-stu-id="70478-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="70478-120">遺失的檔案</span><span class="sxs-lookup"><span data-stu-id="70478-120">Missing files</span></span>

-   <span data-ttu-id="70478-121">找不到 Blob</span><span class="sxs-lookup"><span data-stu-id="70478-121">Blob not found</span></span>

-   <span data-ttu-id="70478-122">截斷的檔案 (磁碟上的檔案小於資訊清單中所指定的)</span><span class="sxs-lookup"><span data-stu-id="70478-122">Truncated files (the files on the disk are smaller than specified in the manifest)</span></span>

-   <span data-ttu-id="70478-123">損毀的檔案內容 (適用於匯入工作，偵測到與 MD5 總和檢查碼不符)</span><span class="sxs-lookup"><span data-stu-id="70478-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="70478-124">損毀的 blob 中繼資料和屬性檔 (偵測到與 MD5 總和檢查碼不符)</span><span class="sxs-lookup"><span data-stu-id="70478-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="70478-125">blob 屬性及/或中繼資料檔案的結構描述不正確</span><span class="sxs-lookup"><span data-stu-id="70478-125">Incorrect schema for the blob properties and/or metadata files</span></span>

<span data-ttu-id="70478-126">在某些情況下，匯入或匯出作業的某些部分無法順利完成，而整個工作仍然會完成。</span><span class="sxs-lookup"><span data-stu-id="70478-126">There may be cases where some parts of an import or export job do not complete successfully, while the overall job still completes.</span></span> <span data-ttu-id="70478-127">在此情況下，您可以透過網路上傳或下載遺漏的資料片段，或可以建立新的作業來傳送資料。</span><span class="sxs-lookup"><span data-stu-id="70478-127">In this case, you can either upload or download the missing pieces of the data over network, or you can create a new job to transfer the data.</span></span> <span data-ttu-id="70478-128">請參閱 [Azure 匯入/匯出工具參考](storage-import-export-tool-how-to-v1.md)，以了解如何透過網路修復資料。</span><span class="sxs-lookup"><span data-stu-id="70478-128">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) to learn how to repair the data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70478-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70478-129">Next steps</span></span>

* [<span data-ttu-id="70478-130">使用匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="70478-130">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
