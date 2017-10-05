---
title: "使用 Azure 匯入/匯出工具 - v1 | Microsoft Docs"
description: "了解如何使用匯入/匯出工具來準備硬碟機，以進行匯入作業、修復匯入作業或修復匯出作業。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f77535bb-d577-438a-bdd3-e15a82e0c543
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/15/2017
ms.author: muralikk
ms.openlocfilehash: 67bdfa8c2cd0f8314c82e2b334a3fa3a5c520c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-tool-v1"></a><span data-ttu-id="03e87-103">使用 Azure 匯入匯出工具 (v1)</span><span class="sxs-lookup"><span data-stu-id="03e87-103">Using the Azure Import/Export Tool (v1)</span></span>

<span data-ttu-id="03e87-104">Azure 匯入/匯出工具 (WAImportExport.exe) 是用來建立及管理 Azure 匯入/匯出服務的作業，可讓您將大量資料傳入或傳出 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="03e87-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="03e87-105">本文件適用於 v1 的 Azure 匯入/匯出工具。</span><span class="sxs-lookup"><span data-stu-id="03e87-105">This documentation is for v1 of the Azure Import/Export Tool.</span></span> <span data-ttu-id="03e87-106">如需使用最新版本工具的相關資訊，請參閱[使用 Azure 匯入/匯出工具](storage-import-export-tool-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="03e87-106">For information about using the most recent version of the tool, please see [Using the Azure Import/Export Tool](storage-import-export-tool-how-to.md).</span></span>

<span data-ttu-id="03e87-107">在這些文章中，您將了解如何使用工具執行下列操作︰</span><span class="sxs-lookup"><span data-stu-id="03e87-107">In these articles, you will see how to use the tool to do the following:</span></span>

- <span data-ttu-id="03e87-108">安裝並設定匯入/匯出工具。</span><span class="sxs-lookup"><span data-stu-id="03e87-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="03e87-109">準備硬碟機進行將資料從您的磁碟機匯入 Azure Blob 儲存體的作業。</span><span class="sxs-lookup"><span data-stu-id="03e87-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="03e87-110">使用複製記錄檔檢閱作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="03e87-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="03e87-111">修復匯入作業。</span><span class="sxs-lookup"><span data-stu-id="03e87-111">Repair an import job.</span></span> 
- <span data-ttu-id="03e87-112">修復匯出作業。</span><span class="sxs-lookup"><span data-stu-id="03e87-112">Repair an export job.</span></span> 
- <span data-ttu-id="03e87-113">如果您在程序期間發生問題，請疑難排解 Azure 匯入/匯出工具。</span><span class="sxs-lookup"><span data-stu-id="03e87-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="03e87-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03e87-114">Next steps</span></span>

* [<span data-ttu-id="03e87-115">設定 WAImportExport 工具</span><span class="sxs-lookup"><span data-stu-id="03e87-115">Setting up the WAImportExport tool</span></span>](storage-import-export-tool-how-to.md)