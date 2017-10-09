---
title: "aaaCancel 和刪除 Azure 匯入/匯出作業 |Microsoft 文件"
description: "了解如何 toocancel 和 delete 作業 hello Microsoft Azure 匯入/匯出服務。"
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
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="aee6c-103">取消及刪除 Azure 匯入/匯出作業</span><span class="sxs-lookup"><span data-stu-id="aee6c-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="aee6c-104">toorequest，工作會取消之前位於 hello`Packaging`狀態，則會呼叫 hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update)作業和集中 hello`CancelRequested`項目太`true`。</span><span class="sxs-lookup"><span data-stu-id="aee6c-104">toorequest that a job be canceled before it is in hello `Packaging` state, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="aee6c-105">會取消 hello 工作，以最佳方式為基礎。</span><span class="sxs-lookup"><span data-stu-id="aee6c-105">hello job is canceled on a best-effort basis.</span></span> <span data-ttu-id="aee6c-106">如果磁碟機中傳送資料的 hello 程序，資料可能會繼續 toobe 轉移，即使已經要求取消之後也一樣。</span><span class="sxs-lookup"><span data-stu-id="aee6c-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="aee6c-107">已取消的作業是移動的 toohello`Completed`狀態，並保留 90 天，此時就會刪除。</span><span class="sxs-lookup"><span data-stu-id="aee6c-107">A canceled job is moved toohello `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="aee6c-108">toodelete 作業呼叫 hello[刪除作業](/rest/api/storageimportexport/jobs#Jobs_Delete)作業之前已出貨 hello 作業 (hello hello 工作進行時，也就是`Creating`狀態)。</span><span class="sxs-lookup"><span data-stu-id="aee6c-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (that is, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="aee6c-109">您也可以在 hello 時刪除作業`Completed`狀態。</span><span class="sxs-lookup"><span data-stu-id="aee6c-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="aee6c-110">已刪除的工作之後，其資訊和狀態便無法再存取透過 hello REST API 或 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="aee6c-110">After a job is deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aee6c-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aee6c-111">Next steps</span></span>

* [<span data-ttu-id="aee6c-112">使用 hello 匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="aee6c-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
