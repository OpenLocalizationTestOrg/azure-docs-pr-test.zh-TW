---
title: "aaaUsing hello Azure 匯入/匯出服務 REST API |Microsoft 文件"
description: "了解 toofind 資源使用 hello Azure 匯入/匯出服務 REST API，包括這兩種方式 tooand 參考資料的位置。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: a01c170b1bc9c2b2ce9086d39de78a39fafb2c8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a><span data-ttu-id="b27c4-103">使用 hello Azure 匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="b27c4-103">Using hello Azure Import/Export service REST API</span></span>

<span data-ttu-id="b27c4-104">hello Microsoft Azure 匯入/匯出服務會公開 REST API tooenable 以程式設計方式控制匯入/匯出工作。</span><span class="sxs-lookup"><span data-stu-id="b27c4-104">hello Microsoft Azure Import/Export service exposes a REST API tooenable programmatic control of import/export jobs.</span></span> <span data-ttu-id="b27c4-105">您可以使用 hello REST API tooperform hello 的所有匯入/匯出作業，您可以執行以 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b27c4-105">You can use hello REST API tooperform all of hello import/export operations that you can perform with hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="b27c4-106">此外，您可以使用 hello REST API tooperform 特定精細的作業，例如查詢 hello 百分比完成的工作，不是目前可用 hello 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b27c4-106">Additionally, you can use hello REST API tooperform certain granular operations, such as querying hello percentage completion of a job, which are not currently available in hello classic portal.</span></span>

<span data-ttu-id="b27c4-107">請參閱[使用 hello Microsoft Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](storage-import-export-service.md)hello 匯入/匯出服務，並示範如何 toouse hello 傳統入口網站 toocreate 及管理匯入的教學課程的概觀和匯出工作。</span><span class="sxs-lookup"><span data-stu-id="b27c4-107">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello classic portal toocreate and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="b27c4-108">服務端點</span><span class="sxs-lookup"><span data-stu-id="b27c4-108">Service endpoints</span></span>

<span data-ttu-id="b27c4-109">hello Azure 匯入/匯出服務是 Azure 資源管理員的資源提供者，並提供一組 REST Api 在下列 HTTPS 端點，以管理匯入/匯出工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="b27c4-109">hello Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at hello following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="b27c4-110">版本控制</span><span class="sxs-lookup"><span data-stu-id="b27c4-110">Versioning</span></span>

<span data-ttu-id="b27c4-111">要求 toohello 匯入/匯出服務必須指定 hello`api-version`參數並將其值設定為太`2016-11-01`。</span><span class="sxs-lookup"><span data-stu-id="b27c4-111">Requests toohello Import/Export service must specify hello `api-version` parameter and set its value too`2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="b27c4-112">匯入/匯出服務作業</span><span class="sxs-lookup"><span data-stu-id="b27c4-112">Import/Export service operations</span></span>

[<span data-ttu-id="b27c4-113">建立匯入作業</span><span class="sxs-lookup"><span data-stu-id="b27c4-113">Creating an import job</span></span>](storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="b27c4-114">建立匯出作業</span><span class="sxs-lookup"><span data-stu-id="b27c4-114">Creating an export job</span></span>](storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="b27c4-115">擷取作業的狀態資訊</span><span class="sxs-lookup"><span data-stu-id="b27c4-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="b27c4-116">列舉作業</span><span class="sxs-lookup"><span data-stu-id="b27c4-116">Enumerating jobs</span></span>](storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="b27c4-117">取消和刪除作業</span><span class="sxs-lookup"><span data-stu-id="b27c4-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="b27c4-118">備份磁碟機資訊清單</span><span class="sxs-lookup"><span data-stu-id="b27c4-118">Backing Up drive manifests</span></span>](storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="b27c4-119">匯入/匯出作業的診斷和錯誤復原</span><span class="sxs-lookup"><span data-stu-id="b27c4-119">Diagnostics and error recovery for Import/Export jobs</span></span>](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="b27c4-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b27c4-120">Next steps</span></span>

* [<span data-ttu-id="b27c4-121">儲存體匯入/匯出 REST</span><span class="sxs-lookup"><span data-stu-id="b27c4-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
