---
title: "aaaList 所有的 Azure 匯入/匯出工作 |MicrosoftDocs"
description: "深入了解如何 toolist hello Azure 匯入/匯出服務的所有訂用帳戶中的工作。"
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
ms.openlocfilehash: 0e12bf3dc3f2084a1987ac362cf8d1041059543c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enumerating-jobs-in-hello-azure-importexport-service"></a><span data-ttu-id="6c7f5-103">列舉 hello Azure 匯入/匯出服務中的工作</span><span class="sxs-lookup"><span data-stu-id="6c7f5-103">Enumerating jobs in hello Azure Import/Export service</span></span>
<span data-ttu-id="6c7f5-104">tooenumerate 所有作業中的訂用帳戶中，而呼叫 hello[列出工作](/rest/api/storageimportexport/jobs#Jobs_List)作業。</span><span class="sxs-lookup"><span data-stu-id="6c7f5-104">tooenumerate all jobs in a subscription, call hello [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) operation.</span></span> <span data-ttu-id="6c7f5-105">`List Jobs`傳回清單的工作，以及下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="6c7f5-105">`List Jobs` returns a list of jobs as well as hello following attributes:</span></span>

-   <span data-ttu-id="6c7f5-106">hello （匯入或匯出） 的工作類型</span><span class="sxs-lookup"><span data-stu-id="6c7f5-106">hello type of job (Import or Export)</span></span>

-   <span data-ttu-id="6c7f5-107">hello 目前的工作狀態</span><span class="sxs-lookup"><span data-stu-id="6c7f5-107">hello current job state</span></span>

-   <span data-ttu-id="6c7f5-108">hello 作業相關聯的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6c7f5-108">hello job's associated storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c7f5-109">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c7f5-109">Next steps</span></span>

* [<span data-ttu-id="6c7f5-110">使用 hello 匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="6c7f5-110">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
