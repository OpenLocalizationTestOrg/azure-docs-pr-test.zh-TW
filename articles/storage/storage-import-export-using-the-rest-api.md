---
title: "使用 Azure 匯入/匯出服務 REST API | Microsoft Docs"
description: "了解可以使用 Azure 匯入/匯出服務 REST API 在何處尋找資源，包括使用說明及參考資料。"
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
ms.openlocfilehash: e4f5ca289f4bd87574e448d37a1154b222f221f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-service-rest-api"></a><span data-ttu-id="4d6d2-103">了解如何使用 Azure 匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="4d6d2-103">Using the Azure Import/Export service REST API</span></span>

<span data-ttu-id="4d6d2-104">Microsoft Azure 匯入/匯出服務會公開 REST API，以啟用程式設計方式控制匯入/匯出作業。</span><span class="sxs-lookup"><span data-stu-id="4d6d2-104">The Microsoft Azure Import/Export service exposes a REST API to enable programmatic control of import/export jobs.</span></span> <span data-ttu-id="4d6d2-105">您可以使用 REST API 來執行您可以使用 [Azure 入口網站](https://portal.azure.com/)執行的所有匯入/匯出作業。</span><span class="sxs-lookup"><span data-stu-id="4d6d2-105">You can use the REST API to perform all of the import/export operations that you can perform with the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="4d6d2-106">此外，您可以使用 REST API 來執行某些細微作業，例如查詢作業的完成百分比，這些作業目前在傳統入口網站中無法使用。</span><span class="sxs-lookup"><span data-stu-id="4d6d2-106">Additionally, you can use the REST API to perform certain granular operations, such as querying the percentage completion of a job, which are not currently available in the classic portal.</span></span>

<span data-ttu-id="4d6d2-107">請參閱[使用 Microsoft Azure 匯入/匯出服務將資料移轉至 Blob 儲存體](storage-import-export-service.md)以取得匯入/匯出服務概觀及示範如何使用傳統入口網站建立和管理匯入與匯出作業的教學課程。</span><span class="sxs-lookup"><span data-stu-id="4d6d2-107">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the classic portal to create and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="4d6d2-108">服務端點</span><span class="sxs-lookup"><span data-stu-id="4d6d2-108">Service endpoints</span></span>

<span data-ttu-id="4d6d2-109">Azure 匯入/匯出服務是 Azure Resource Manager 的資源提供者，並在下列 HTTPS 端點提供一組 REST API 以管理匯入/匯出作業︰</span><span class="sxs-lookup"><span data-stu-id="4d6d2-109">The Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at the following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="4d6d2-110">版本控制</span><span class="sxs-lookup"><span data-stu-id="4d6d2-110">Versioning</span></span>

<span data-ttu-id="4d6d2-111">匯入/匯出服務的要求必須指定 `api-version` 參數並將其值設定為 `2016-11-01`。</span><span class="sxs-lookup"><span data-stu-id="4d6d2-111">Requests to the Import/Export service must specify the `api-version` parameter and set its value to `2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="4d6d2-112">匯入/匯出服務作業</span><span class="sxs-lookup"><span data-stu-id="4d6d2-112">Import/Export service operations</span></span>

[<span data-ttu-id="4d6d2-113">建立匯入作業</span><span class="sxs-lookup"><span data-stu-id="4d6d2-113">Creating an import job</span></span>](storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="4d6d2-114">建立匯出作業</span><span class="sxs-lookup"><span data-stu-id="4d6d2-114">Creating an export job</span></span>](storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="4d6d2-115">擷取作業的狀態資訊</span><span class="sxs-lookup"><span data-stu-id="4d6d2-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="4d6d2-116">列舉作業</span><span class="sxs-lookup"><span data-stu-id="4d6d2-116">Enumerating jobs</span></span>](storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="4d6d2-117">取消和刪除作業</span><span class="sxs-lookup"><span data-stu-id="4d6d2-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="4d6d2-118">備份磁碟機資訊清單</span><span class="sxs-lookup"><span data-stu-id="4d6d2-118">Backing Up drive manifests</span></span>](storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="4d6d2-119">匯入/匯出作業的診斷和錯誤復原</span><span class="sxs-lookup"><span data-stu-id="4d6d2-119">Diagnostics and error recovery for Import/Export jobs</span></span>](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="4d6d2-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d6d2-120">Next steps</span></span>

* [<span data-ttu-id="4d6d2-121">儲存體匯入/匯出 REST</span><span class="sxs-lookup"><span data-stu-id="4d6d2-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
