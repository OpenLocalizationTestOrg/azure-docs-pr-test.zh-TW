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
ms.date: 06/22/2017
ms.author: xiaofmao
ms.openlocfilehash: beb2d26afb8ddc5e85b1828c71de5cbd9e678fe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-stack-storage-differences-and-considerations"></a><span data-ttu-id="82eaf-103">Azure Stack 儲存體：差異與考量</span><span class="sxs-lookup"><span data-stu-id="82eaf-103">Azure Stack Storage: Differences and considerations</span></span>
<span data-ttu-id="82eaf-104">「Azure Stack 儲存體」是 Microsoft Azure Stack 中的一組儲存體雲端服務。</span><span class="sxs-lookup"><span data-stu-id="82eaf-104">Azure Stack Storage is the set of storage cloud services in Microsoft Azure Stack.</span></span> <span data-ttu-id="82eaf-105">「Azure Stack 儲存體」使用與 Azure 一致的語意來提供 Blob、資料表、佇列及帳戶管理功能。</span><span class="sxs-lookup"><span data-stu-id="82eaf-105">Azure Stack Storage provides blob, table, queue, and account management functionality with Azure-consistent semantics.</span></span>

<span data-ttu-id="82eaf-106">此文章摘要說明「Azure Stack 儲存體」與「Azure 儲存體」的已知差異。</span><span class="sxs-lookup"><span data-stu-id="82eaf-106">This article summarizes the known Azure Stack Storage differences from Azure Storage.</span></span> <span data-ttu-id="82eaf-107">此外，也摘要說明您部署 Azure Stack 時要記住的其他考量。</span><span class="sxs-lookup"><span data-stu-id="82eaf-107">It also summarizes other considerations to keep in mind when you deploy Azure Stack.</span></span> <span data-ttu-id="82eaf-108">若要深入了解 Azure Stack 與 Azure 之間的大致差異，請參閱[主要考量](azure-stack-considerations.md)主題。</span><span class="sxs-lookup"><span data-stu-id="82eaf-108">To learn about high-level differences between Azure Stack and Azure, see the [Key considerations](azure-stack-considerations.md) topic.</span></span>

## <a name="cheat-sheet-storage-differences"></a><span data-ttu-id="82eaf-109">速查表：儲存體差異</span><span class="sxs-lookup"><span data-stu-id="82eaf-109">Cheat sheet: Storage differences</span></span>

| <span data-ttu-id="82eaf-110">功能</span><span class="sxs-lookup"><span data-stu-id="82eaf-110">Feature</span></span> | <span data-ttu-id="82eaf-111">Azure (全域)</span><span class="sxs-lookup"><span data-stu-id="82eaf-111">Azure (global)</span></span> | <span data-ttu-id="82eaf-112">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="82eaf-112">Azure Stack</span></span> |
| --- | --- | --- |
|<span data-ttu-id="82eaf-113">檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="82eaf-113">File storage</span></span>|<span data-ttu-id="82eaf-114">支援雲端式 SMB 檔案共用</span><span class="sxs-lookup"><span data-stu-id="82eaf-114">Cloud-based SMB file shares supported</span></span>|<span data-ttu-id="82eaf-115">尚不支援</span><span class="sxs-lookup"><span data-stu-id="82eaf-115">Not yet supported</span></span>
|<span data-ttu-id="82eaf-116">待用資料加密</span><span class="sxs-lookup"><span data-stu-id="82eaf-116">Data at rest encryption</span></span>|<span data-ttu-id="82eaf-117">256 位元 AES 加密</span><span class="sxs-lookup"><span data-stu-id="82eaf-117">256-bit AES encryption</span></span>|<span data-ttu-id="82eaf-118">尚不支援</span><span class="sxs-lookup"><span data-stu-id="82eaf-118">Not yet supported</span></span>
|<span data-ttu-id="82eaf-119">儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="82eaf-119">Storage account type</span></span>|<span data-ttu-id="82eaf-120">一般用途和 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="82eaf-120">General-purpose and Azure Blob storage accounts</span></span>|<span data-ttu-id="82eaf-121">僅一般用途</span><span class="sxs-lookup"><span data-stu-id="82eaf-121">General-purpose only</span></span>
|<span data-ttu-id="82eaf-122">複寫選項</span><span class="sxs-lookup"><span data-stu-id="82eaf-122">Replication options</span></span>|<span data-ttu-id="82eaf-123">本地備援儲存體、異地備援儲存體、讀取權限異地備援儲存體，以及區域備援儲存體</span><span class="sxs-lookup"><span data-stu-id="82eaf-123">Locally redundant storage, geo-redundant storage, read-access geo-redundant storage, and zone-redundant storage</span></span>|<span data-ttu-id="82eaf-124">本地備援儲存體</span><span class="sxs-lookup"><span data-stu-id="82eaf-124">Locally redundant storage</span></span>
|<span data-ttu-id="82eaf-125">進階儲存體</span><span class="sxs-lookup"><span data-stu-id="82eaf-125">Premium storage</span></span>|<span data-ttu-id="82eaf-126">完全支援</span><span class="sxs-lookup"><span data-stu-id="82eaf-126">Fully supported</span></span>|<span data-ttu-id="82eaf-127">可佈建，但無效能限制或保證</span><span class="sxs-lookup"><span data-stu-id="82eaf-127">Can be provisioned, but no performance limit or guarantee</span></span>
|<span data-ttu-id="82eaf-128">受控磁碟</span><span class="sxs-lookup"><span data-stu-id="82eaf-128">Managed disks</span></span>|<span data-ttu-id="82eaf-129">支援進階和標準</span><span class="sxs-lookup"><span data-stu-id="82eaf-129">Premium and standard supported</span></span>|<span data-ttu-id="82eaf-130">尚不支援</span><span class="sxs-lookup"><span data-stu-id="82eaf-130">Not yet supported</span></span>
|<span data-ttu-id="82eaf-131">Blob 名稱</span><span class="sxs-lookup"><span data-stu-id="82eaf-131">Blob name</span></span>|<span data-ttu-id="82eaf-132">1,024 個字元 (2,048 個位元組)</span><span class="sxs-lookup"><span data-stu-id="82eaf-132">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="82eaf-133">880 個字元 (1,760 個位元組)</span><span class="sxs-lookup"><span data-stu-id="82eaf-133">880 characters (1,760 bytes)</span></span>
|<span data-ttu-id="82eaf-134">區塊 Blob 大小上限</span><span class="sxs-lookup"><span data-stu-id="82eaf-134">Block blob max size</span></span>|<span data-ttu-id="82eaf-135">4.75 TB (100 MB X 50,000 個區塊)</span><span class="sxs-lookup"><span data-stu-id="82eaf-135">4.75 TB (100 MB X 50,000 blocks)</span></span>|<span data-ttu-id="82eaf-136">50,000 x 4 MB (約為 195 GB)</span><span class="sxs-lookup"><span data-stu-id="82eaf-136">50,000 X 4 MB (approx. 195 GB)</span></span>
|<span data-ttu-id="82eaf-137">分頁 Blob 增量快照複製</span><span class="sxs-lookup"><span data-stu-id="82eaf-137">Page blob incremental snapshot copy</span></span>|<span data-ttu-id="82eaf-138">支援進階和標準 Azure 分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="82eaf-138">Premium and standard Azure page blobs supported</span></span>|<span data-ttu-id="82eaf-139">尚不支援</span><span class="sxs-lookup"><span data-stu-id="82eaf-139">Not yet supported</span></span>
|<span data-ttu-id="82eaf-140">分頁 Blob 大小上限</span><span class="sxs-lookup"><span data-stu-id="82eaf-140">Page blob max size</span></span>|<span data-ttu-id="82eaf-141">8 TB</span><span class="sxs-lookup"><span data-stu-id="82eaf-141">8 TB</span></span>|<span data-ttu-id="82eaf-142">1 TB</span><span class="sxs-lookup"><span data-stu-id="82eaf-142">1 TB</span></span>
|<span data-ttu-id="82eaf-143">分頁 Blob 分頁大小</span><span class="sxs-lookup"><span data-stu-id="82eaf-143">Page blob page size</span></span>|<span data-ttu-id="82eaf-144">512 個位元組</span><span class="sxs-lookup"><span data-stu-id="82eaf-144">512 bytes</span></span>|<span data-ttu-id="82eaf-145">4 KB</span><span class="sxs-lookup"><span data-stu-id="82eaf-145">4 KB</span></span>
|<span data-ttu-id="82eaf-146">資料表分割區索引鍵和資料列索引鍵大小</span><span class="sxs-lookup"><span data-stu-id="82eaf-146">Table partition key and row key size</span></span>|<span data-ttu-id="82eaf-147">1,024 個字元 (2,048 個位元組)</span><span class="sxs-lookup"><span data-stu-id="82eaf-147">1,024 characters (2,048 bytes)</span></span>|<span data-ttu-id="82eaf-148">400 個字元 (800 個位元組)</span><span class="sxs-lookup"><span data-stu-id="82eaf-148">400 characters (800 bytes)</span></span>

### <a name="metrics"></a><span data-ttu-id="82eaf-149">度量</span><span class="sxs-lookup"><span data-stu-id="82eaf-149">Metrics</span></span>
<span data-ttu-id="82eaf-150">儲存體度量也有一些差異：</span><span class="sxs-lookup"><span data-stu-id="82eaf-150">There are also some differences with storage metrics:</span></span>
* <span data-ttu-id="82eaf-151">儲存體度量中的交易資料並不區分內部或外部網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="82eaf-151">The transaction data in storage metrics does not differentiate internal or external network bandwidth.</span></span>
* <span data-ttu-id="82eaf-152">儲存體度量中的交易資料並不包含虛擬機器對所掛接磁碟的存取。</span><span class="sxs-lookup"><span data-stu-id="82eaf-152">The transaction data in storage metrics does not include virtual machine access to the mounted disks.</span></span>

## <a name="api-version"></a><span data-ttu-id="82eaf-153">API 版本</span><span class="sxs-lookup"><span data-stu-id="82eaf-153">API version</span></span>
<span data-ttu-id="82eaf-154">使用「Azure Stack 儲存體」時支援下列版本：</span><span class="sxs-lookup"><span data-stu-id="82eaf-154">The following versions are supported with Azure Stack Storage:</span></span>

* <span data-ttu-id="82eaf-155">Azure 儲存體資料服務：[2015-04-05 REST API 版本](https://docs.microsoft.com/en-us/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="82eaf-155">Azure Storage data services: [2015-04-05 REST API version](https://docs.microsoft.com/en-us/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)</span></span>
* <span data-ttu-id="82eaf-156">Azure 儲存體管理服務：[2015-05-01-preview、2015-06-15 及 2016-01-01](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="82eaf-156">Azure Storage management services: [2015-05-01-preview, 2015-06-15, and 2016-01-01](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN)</span></span> 

## <a name="next-steps"></a><span data-ttu-id="82eaf-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82eaf-157">Next steps</span></span>

* [<span data-ttu-id="82eaf-158">開始使用 Azure Stack 儲存體開發工具</span><span class="sxs-lookup"><span data-stu-id="82eaf-158">Get started with Azure Stack Storage development tools</span></span>](azure-stack-storage-dev.md)
* [<span data-ttu-id="82eaf-159">Azure Stack 儲存體簡介</span><span class="sxs-lookup"><span data-stu-id="82eaf-159">Introduction to Azure Stack Storage</span></span>](azure-stack-storage-overview.md)

