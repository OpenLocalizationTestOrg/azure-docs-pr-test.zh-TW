---
title: "所有 Azure 匯入/匯出作業的清單 | MicrosoftDocs"
description: "了解如何列出訂用帳戶中所有「Azure 匯入/匯出」服務作業的清單。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f2e619be-1bbd-4a54-9472-9e2f70a83b64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 1977bfc0e516088310f45ecdd960287eeed2c2d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enumerating-jobs-in-the-azure-importexport-service"></a><span data-ttu-id="8ef0b-103">列舉 Azure 匯入/匯出服務中的作業</span><span class="sxs-lookup"><span data-stu-id="8ef0b-103">Enumerating jobs in the Azure Import/Export service</span></span>
<span data-ttu-id="8ef0b-104">若要列舉訂用帳戶中的所有作業，請呼叫 [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List)作業。</span><span class="sxs-lookup"><span data-stu-id="8ef0b-104">To enumerate all jobs in a subscription, call the [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) operation.</span></span> <span data-ttu-id="8ef0b-105">`List Jobs` 會傳回一份作業以及下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="8ef0b-105">`List Jobs` returns a list of jobs as well as the following attributes:</span></span>

-   <span data-ttu-id="8ef0b-106">作業的類型 (匯入或匯出)</span><span class="sxs-lookup"><span data-stu-id="8ef0b-106">The type of job (Import or Export)</span></span>

-   <span data-ttu-id="8ef0b-107">目前的作業狀態</span><span class="sxs-lookup"><span data-stu-id="8ef0b-107">The current job state</span></span>

-   <span data-ttu-id="8ef0b-108">作業的相關聯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8ef0b-108">The job's associated storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ef0b-109">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ef0b-109">Next steps</span></span>

* [<span data-ttu-id="8ef0b-110">使用匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="8ef0b-110">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
