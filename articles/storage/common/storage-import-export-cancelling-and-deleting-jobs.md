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
ms.openlocfilehash: 1e989c72fc03697bf6d2e515ff53003703665d1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="bd975-103">取消及刪除 Azure 匯入/匯出作業</span><span class="sxs-lookup"><span data-stu-id="bd975-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="bd975-104">若要要求讓作業在進入 `Packaging` 狀態之前予以取消，請呼叫 [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 作業並將 `CancelRequested` 元素設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="bd975-104">To request that a job be canceled before it is in the `Packaging` state, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="bd975-105">系統會盡可能地取消作業。</span><span class="sxs-lookup"><span data-stu-id="bd975-105">The job is canceled on a best-effort basis.</span></span> <span data-ttu-id="bd975-106">如果磁碟機正在傳輸資料，即使已經要求取消，資料可能會繼續傳送。</span><span class="sxs-lookup"><span data-stu-id="bd975-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="bd975-107">取消的作業會進入 `Completed` 狀態並保留 90 天，90 天過後就會遭到刪除。</span><span class="sxs-lookup"><span data-stu-id="bd975-107">A canceled job is moved to the `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="bd975-108">若要刪除作業，在傳送作業之前請先呼叫 [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) 作業，(也就是當作業處於 `Creating` 狀態時)。</span><span class="sxs-lookup"><span data-stu-id="bd975-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (that is, while the job is in the `Creating` state).</span></span> <span data-ttu-id="bd975-109">您也可以在作業為 `Completed` 狀態時將它刪除。</span><span class="sxs-lookup"><span data-stu-id="bd975-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="bd975-110">作業遭到刪除後，便無法再透過 REST API 或 Azure 入口網站存取其資訊和狀態。</span><span class="sxs-lookup"><span data-stu-id="bd975-110">After a job is deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd975-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd975-111">Next steps</span></span>

* [<span data-ttu-id="bd975-112">使用匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="bd975-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
