---
title: "Azure 匯入/匯出工作的 aaaDiagnostics 和錯誤復原 |Microsoft 文件"
description: "深入了解如何 tooenable 詳細資訊記錄的 Microsoft Azure 匯入/匯出服務作業。"
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
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="a4ad5-103">Azure 匯入/匯出作業的診斷和錯誤復原</span><span class="sxs-lookup"><span data-stu-id="a4ad5-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="a4ad5-104">處理每個磁碟機，hello Azure 匯入/匯出服務會建立錯誤記錄檔相關聯的 hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="a4ad5-104">For each drive processed, hello Azure Import/Export service creates an error log in hello associated storage account.</span></span> <span data-ttu-id="a4ad5-105">您也可以設定 hello 啟用詳細資訊記錄`LogLevel`屬性太`Verbose`時呼叫 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)或[Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update)作業。</span><span class="sxs-lookup"><span data-stu-id="a4ad5-105">You can also enable verbose logging by setting hello `LogLevel` property too`Verbose` when calling hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="a4ad5-106">根據預設，記錄檔寫入名為 tooa 容器`waimportexport`。</span><span class="sxs-lookup"><span data-stu-id="a4ad5-106">By default, logs are written tooa container named `waimportexport`.</span></span> <span data-ttu-id="a4ad5-107">您可以指定不同的名稱設定 hello`DiagnosticsPath`屬性時呼叫 hello`Put Job`或`Update Job Properties`作業。</span><span class="sxs-lookup"><span data-stu-id="a4ad5-107">You can specify a different name by setting hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="a4ad5-108">hello 記錄檔會儲存為區塊 blob 以 hello 遵循命名慣例： `waies/jobname_driveid_timestamp_logtype.xml`。</span><span class="sxs-lookup"><span data-stu-id="a4ad5-108">hello logs are stored as block blobs with hello following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="a4ad5-109">您可以擷取由呼叫 hello hello hello 作業的記錄檔的 URI [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get)作業。</span><span class="sxs-lookup"><span data-stu-id="a4ad5-109">You can retrieve hello URI of hello logs for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="a4ad5-110">hello 詳細資訊記錄檔的 hello URI 會傳回在 hello`VerboseLogUri`屬性每個磁碟機，而 hello 錯誤記錄檔的 hello URI 會傳回在 hello`ErrorLogUri`屬性。</span><span class="sxs-lookup"><span data-stu-id="a4ad5-110">hello URI for hello verbose log is returned in hello `VerboseLogUri` property for each drive, while hello URI for hello error log is returned in hello `ErrorLogUri` property.</span></span>

<span data-ttu-id="a4ad5-111">您可以使用記錄資料 tooidentify hello 下列問題的 hello。</span><span class="sxs-lookup"><span data-stu-id="a4ad5-111">You can use hello logging data tooidentify hello following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="a4ad5-112">磁碟機錯誤</span><span class="sxs-lookup"><span data-stu-id="a4ad5-112">Drive errors</span></span>

<span data-ttu-id="a4ad5-113">hello 下列項目分類為磁碟機錯誤：</span><span class="sxs-lookup"><span data-stu-id="a4ad5-113">hello following items are classified as drive errors:</span></span>

-   <span data-ttu-id="a4ad5-114">資訊清單檔案的存取或讀取 hello 的錯誤</span><span class="sxs-lookup"><span data-stu-id="a4ad5-114">Errors in accessing or reading hello manifest file</span></span>

-   <span data-ttu-id="a4ad5-115">不正確的 BitLocker 金鑰</span><span class="sxs-lookup"><span data-stu-id="a4ad5-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="a4ad5-116">磁碟機讀取/寫入錯誤</span><span class="sxs-lookup"><span data-stu-id="a4ad5-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="a4ad5-117">Blob 錯誤</span><span class="sxs-lookup"><span data-stu-id="a4ad5-117">Blob errors</span></span>

<span data-ttu-id="a4ad5-118">hello 下列項目分類為 blob 錯誤：</span><span class="sxs-lookup"><span data-stu-id="a4ad5-118">hello following items are classified as blob errors:</span></span>

-   <span data-ttu-id="a4ad5-119">不正確或衝突的 blob 或名稱</span><span class="sxs-lookup"><span data-stu-id="a4ad5-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="a4ad5-120">遺失的檔案</span><span class="sxs-lookup"><span data-stu-id="a4ad5-120">Missing files</span></span>

-   <span data-ttu-id="a4ad5-121">找不到 Blob</span><span class="sxs-lookup"><span data-stu-id="a4ad5-121">Blob not found</span></span>

-   <span data-ttu-id="a4ad5-122">截斷 （hello 磁碟上的 hello 檔案則小於 hello 資訊清單中指定） 的檔案</span><span class="sxs-lookup"><span data-stu-id="a4ad5-122">Truncated files (hello files on hello disk are smaller than specified in hello manifest)</span></span>

-   <span data-ttu-id="a4ad5-123">損毀的檔案內容 (適用於匯入工作，偵測到與 MD5 總和檢查碼不符)</span><span class="sxs-lookup"><span data-stu-id="a4ad5-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="a4ad5-124">損毀的 blob 中繼資料和屬性檔 (偵測到與 MD5 總和檢查碼不符)</span><span class="sxs-lookup"><span data-stu-id="a4ad5-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="a4ad5-125">不正確的結構描述的 hello blob 屬性及/或中繼資料檔案</span><span class="sxs-lookup"><span data-stu-id="a4ad5-125">Incorrect schema for hello blob properties and/or metadata files</span></span>

<span data-ttu-id="a4ad5-126">可能有其中一些組件的匯入或匯出工作無法順利完成，hello 整體工作仍然完成時的情況。</span><span class="sxs-lookup"><span data-stu-id="a4ad5-126">There may be cases where some parts of an import or export job do not complete successfully, while hello overall job still completes.</span></span> <span data-ttu-id="a4ad5-127">在此情況下，您可以上傳或下載 hello 遺漏 hello 資料透過網路，或您可以建立新的工作 tootransfer hello 資料。</span><span class="sxs-lookup"><span data-stu-id="a4ad5-127">In this case, you can either upload or download hello missing pieces of hello data over network, or you can create a new job tootransfer hello data.</span></span> <span data-ttu-id="a4ad5-128">請參閱 hello [Azure 匯入/匯出工具參考](storage-import-export-tool-how-to-v1.md)toolearn toorepair hello 資料透過網路的方式。</span><span class="sxs-lookup"><span data-stu-id="a4ad5-128">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) toolearn how toorepair hello data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4ad5-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4ad5-129">Next steps</span></span>

* [<span data-ttu-id="a4ad5-130">使用 hello 匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="a4ad5-130">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
