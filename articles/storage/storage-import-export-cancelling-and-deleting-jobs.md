---
title: "取消及刪除 Azure 匯入/匯出作業 | Microsoft Docs"
description: "了解如何取消及刪除 Microsoft Azure 匯入/匯出服務的作業。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e0a7ff391e5a03ed563912dea54c7cfe73111bcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="89f52-103">取消及刪除 Azure 匯入/匯出作業</span><span class="sxs-lookup"><span data-stu-id="89f52-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="89f52-104">您可以藉由呼叫 [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 作業並將 `CancelRequested` 元素設定為 `true`，要求作業為 `Packaging` 狀態之前將它取消。</span><span class="sxs-lookup"><span data-stu-id="89f52-104">You can request that a job be cancelled before it is in the `Packaging` state by calling the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="89f52-105">會儘可能將作業取消。</span><span class="sxs-lookup"><span data-stu-id="89f52-105">The job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="89f52-106">如果磁碟機正在傳輸資料，即使已經要求取消，資料可能會繼續傳送。</span><span class="sxs-lookup"><span data-stu-id="89f52-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="89f52-107">已取消的作業會移到 `Completed` 狀態並保留 90 天，屆時則會刪除。</span><span class="sxs-lookup"><span data-stu-id="89f52-107">A cancelled job will move to the `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="89f52-108">若要刪除作業，在傳送作業之前請先呼叫 [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) 作業，(也就是處於 `Creating` 狀態時)。</span><span class="sxs-lookup"><span data-stu-id="89f52-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (*i.e.*, while the job is in the `Creating` state).</span></span> <span data-ttu-id="89f52-109">您也可以在作業為 `Completed` 狀態時將它刪除。</span><span class="sxs-lookup"><span data-stu-id="89f52-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="89f52-110">在刪除作業之後，便無法再透過 REST API 或 Azure 入口網站存取其資訊和狀態。</span><span class="sxs-lookup"><span data-stu-id="89f52-110">After a job has been deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89f52-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89f52-111">Next steps</span></span>

* [<span data-ttu-id="89f52-112">使用匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="89f52-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
