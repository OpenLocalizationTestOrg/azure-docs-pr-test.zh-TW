---
title: "Azure Stack 儲存體：差異與考量"
description: "了解「Azure Stack 儲存體」與「Azure 儲存體」之間的差異，以及 Azure Stack 部署考量。"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: xiaofmao
ms.openlocfilehash: 381950321ac3a5ea8a43b76f3fba868da4be4682
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="azure-stack-storage-differences-and-considerations"></a><span data-ttu-id="6df47-103">Azure Stack 儲存體：差異與考量</span><span class="sxs-lookup"><span data-stu-id="6df47-103">Azure Stack Storage: Differences and considerations</span></span>

<span data-ttu-id="6df47-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="6df47-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="6df47-105">「Azure Stack 儲存體」是 Microsoft Azure Stack 中的一組儲存體雲端服務。</span><span class="sxs-lookup"><span data-stu-id="6df47-105">Azure Stack Storage is the set of storage cloud services in Microsoft Azure Stack.</span></span> <span data-ttu-id="6df47-106">「Azure Stack 儲存體」使用與 Azure 一致的語意來提供 Blob、資料表、佇列及帳戶管理功能。</span><span class="sxs-lookup"><span data-stu-id="6df47-106">Azure Stack Storage provides blob, table, queue, and account management functionality with Azure-consistent semantics.</span></span>

<span data-ttu-id="6df47-107">此文章摘要說明「Azure Stack 儲存體」與「Azure 儲存體」的已知差異。</span><span class="sxs-lookup"><span data-stu-id="6df47-107">This article summarizes the known Azure Stack Storage differences from Azure Storage.</span></span> <span data-ttu-id="6df47-108">此外，也摘要說明您部署 Azure Stack 時要記住的其他考量。</span><span class="sxs-lookup"><span data-stu-id="6df47-108">It also summarizes other considerations to keep in mind when you deploy Azure Stack.</span></span> <span data-ttu-id="6df47-109">若要深入了解 Azure Stack 與 Azure 之間的大致差異，請參閱[主要考量](azure-stack-considerations.md)主題。</span><span class="sxs-lookup"><span data-stu-id="6df47-109">To learn about high-level differences between Azure Stack and Azure, see the [Key considerations](azure-stack-considerations.md) topic.</span></span>

## <a name="cheat-sheet-storage-differences"></a><span data-ttu-id="6df47-110">速查表：儲存體差異</span><span class="sxs-lookup"><span data-stu-id="6df47-110">Cheat sheet: Storage differences</span></span>

| <span data-ttu-id="6df47-111">功能</span><span class="sxs-lookup"><span data-stu-id="6df47-111">Feature</span></span> | <span data-ttu-id="6df47-112">Azure (全域)</span><span class="sxs-lookup"><span data-stu-id="6df47-112">Azure (global)</span></span> | <span data-ttu-id="6df47-113">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6df47-113">Azure Stack</span></span> |
| --- | --- | --- |
|<span data-ttu-id="6df47-114">檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="6df47-114">File storage</span></span>|<span data-ttu-id="6df47-115">支援雲端式 SMB 檔案共用</span><span class="sxs-lookup"><span data-stu-id="6df47-115">Cloud-based SMB file shares supported</span></span>|<span data-ttu-id="6df47-116">尚不支援</span><span class="sxs-lookup"><span data-stu-id="6df47-116">Not yet supported</span></span>
|<span data-ttu-id="6df47-117">待用資料加密</span><span class="sxs-lookup"><span data-stu-id="6df47-117">Data at rest encryption</span></span>|<span data-ttu-id="6df47-118">256 位元 AES 加密</span><span class="sxs-lookup"><span data-stu-id="6df47-118">256-bit AES encryption</span></span>|<span data-ttu-id="6df47-119">尚不支援</span><span class="sxs-lookup"><span data-stu-id="6df47-119">Not yet supported</span></span>
|<span data-ttu-id="6df47-120">儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="6df47-120">Storage account type</span></span>|<span data-ttu-id="6df47-121">一般用途和 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6df47-121">General-purpose and Azure Blob storage accounts</span></span>|<span data-ttu-id="6df47-122">僅一般用途</span><span class="sxs-lookup"><span data-stu-id="6df47-122">General-purpose only</span></span>
|<span data-ttu-id="6df47-123">複寫選項</span><span class="sxs-lookup"><span data-stu-id="6df47-123">Replication options</span></span>|<span data-ttu-id="6df47-124">本地備援儲存體、異地備援儲存體、讀取權限異地備援儲存體，以及區域備援儲存體</span><span class="sxs-lookup"><span data-stu-id="6df47-124">Locally redundant storage, geo-redundant storage, read-access geo-redundant storage, and zone-redundant storage</span></span>|<span data-ttu-id="6df47-125">本地備援儲存體</span><span class="sxs-lookup"><span data-stu-id="6df47-125">Locally redundant storage</span></span>
|<span data-ttu-id="6df47-126">進階儲存體</span><span class="sxs-lookup"><span data-stu-id="6df47-126">Premium storage</span></span>|<span data-ttu-id="6df47-127">完全支援</span><span class="sxs-lookup"><span data-stu-id="6df47-127">Fully supported</span></span>|<span data-ttu-id="6df47-128">可佈建，但無效能限制或保證</span><span class="sxs-lookup"><span data-stu-id="6df47-128">Can be provisioned, but no performance limit or guarantee</span></span>
|<span data-ttu-id="6df47-129">受控磁碟</span><span class="sxs-lookup"><span data-stu-id="6df47-129">Managed disks</span></span>|<span data-ttu-id="6df47-130">支援進階和標準</span><span class="sxs-lookup"><span data-stu-id="6df47-130">Premium and standard supported</span></span>|<span data-ttu-id="6df47-131">尚不支援</span><span class="sxs-lookup"><span data-stu-id="6df47-131">Not yet supported</span></span>
|<span data-ttu-id="6df47-132">Blob 名稱</span><span class="sxs-lookup"><span data-stu-id="6df47-132">Blob name</span></span>|<span data-ttu-id="6df47-133">1,024 個字元 (2,048 個位元組)</span><span class="sxs-lookup"><span data-stu-id="6df47-133">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="6df47-134">880 個字元 (1,760 個位元組)</span><span class="sxs-lookup"><span data-stu-id="6df47-134">880 characters (1,760 bytes)</span></span>
|<span data-ttu-id="6df47-135">區塊 Blob 大小上限</span><span class="sxs-lookup"><span data-stu-id="6df47-135">Block blob max size</span></span>|<span data-ttu-id="6df47-136">4.75 TB (100 MB X 50,000 個區塊)</span><span class="sxs-lookup"><span data-stu-id="6df47-136">4.75 TB (100 MB X 50,000 blocks)</span></span>|<span data-ttu-id="6df47-137">50,000 x 4 MB (約為 195 GB)</span><span class="sxs-lookup"><span data-stu-id="6df47-137">50,000 X 4 MB (approx. 195 GB)</span></span>
|<span data-ttu-id="6df47-138">分頁 Blob 增量快照複製</span><span class="sxs-lookup"><span data-stu-id="6df47-138">Page blob incremental snapshot copy</span></span>|<span data-ttu-id="6df47-139">支援進階和標準 Azure 分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="6df47-139">Premium and standard Azure page blobs supported</span></span>|<span data-ttu-id="6df47-140">尚不支援</span><span class="sxs-lookup"><span data-stu-id="6df47-140">Not yet supported</span></span>
|<span data-ttu-id="6df47-141">分頁 Blob 大小上限</span><span class="sxs-lookup"><span data-stu-id="6df47-141">Page blob max size</span></span>|<span data-ttu-id="6df47-142">8 TB</span><span class="sxs-lookup"><span data-stu-id="6df47-142">8 TB</span></span>|<span data-ttu-id="6df47-143">1 TB</span><span class="sxs-lookup"><span data-stu-id="6df47-143">1 TB</span></span>
|<span data-ttu-id="6df47-144">分頁 Blob 分頁大小</span><span class="sxs-lookup"><span data-stu-id="6df47-144">Page blob page size</span></span>|<span data-ttu-id="6df47-145">512 個位元組</span><span class="sxs-lookup"><span data-stu-id="6df47-145">512 bytes</span></span>|<span data-ttu-id="6df47-146">4 KB</span><span class="sxs-lookup"><span data-stu-id="6df47-146">4 KB</span></span>
|<span data-ttu-id="6df47-147">資料表分割區索引鍵和資料列索引鍵大小</span><span class="sxs-lookup"><span data-stu-id="6df47-147">Table partition key and row key size</span></span>|<span data-ttu-id="6df47-148">1,024 個字元 (2,048 個位元組)</span><span class="sxs-lookup"><span data-stu-id="6df47-148">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="6df47-149">400 個字元 (800 個位元組)</span><span class="sxs-lookup"><span data-stu-id="6df47-149">400 characters (800 bytes)</span></span>

### <a name="metrics"></a><span data-ttu-id="6df47-150">度量</span><span class="sxs-lookup"><span data-stu-id="6df47-150">Metrics</span></span>
<span data-ttu-id="6df47-151">儲存體度量也有一些差異：</span><span class="sxs-lookup"><span data-stu-id="6df47-151">There are also some differences with storage metrics:</span></span>
* <span data-ttu-id="6df47-152">儲存體度量中的交易資料並不區分內部或外部網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="6df47-152">The transaction data in storage metrics does not differentiate internal or external network bandwidth.</span></span>
* <span data-ttu-id="6df47-153">儲存體度量中的交易資料並不包含虛擬機器對所掛接磁碟的存取。</span><span class="sxs-lookup"><span data-stu-id="6df47-153">The transaction data in storage metrics does not include virtual machine access to the mounted disks.</span></span>

## <a name="api-version"></a><span data-ttu-id="6df47-154">API 版本</span><span class="sxs-lookup"><span data-stu-id="6df47-154">API version</span></span>
<span data-ttu-id="6df47-155">使用「Azure Stack 儲存體」時支援下列版本：</span><span class="sxs-lookup"><span data-stu-id="6df47-155">The following versions are supported with Azure Stack Storage:</span></span>

* <span data-ttu-id="6df47-156">Azure 儲存體資料服務：[2015-04-05 REST API 版本](https://docs.microsoft.com/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="6df47-156">Azure Storage data services: [2015-04-05 REST API version](https://docs.microsoft.com/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span></span>
* <span data-ttu-id="6df47-157">Azure 儲存體管理服務：[2015-05-01-preview、2015-06-15 及 2016-01-01](https://docs.microsoft.com/rest/api/storagerp/?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="6df47-157">Azure Storage management services: [2015-05-01-preview, 2015-06-15, and 2016-01-01](https://docs.microsoft.com/rest/api/storagerp/?redirectedfrom=MSDN)</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6df47-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6df47-158">Next steps</span></span>

* [<span data-ttu-id="6df47-159">開始使用 Azure Stack 儲存體開發工具</span><span class="sxs-lookup"><span data-stu-id="6df47-159">Get started with Azure Stack Storage development tools</span></span>](azure-stack-storage-dev.md)
* [<span data-ttu-id="6df47-160">Azure Stack 儲存體簡介</span><span class="sxs-lookup"><span data-stu-id="6df47-160">Introduction to Azure Stack Storage</span></span>](azure-stack-storage-overview.md)

