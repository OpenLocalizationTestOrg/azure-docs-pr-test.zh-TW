---
title: "與 Azure 儲存體搭配使用的工具 | Microsoft Docs"
description: "可讓您檢視 Azure 儲存體資料並與其互動的工具清單。"
services: storage
documentationcenter: 
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: e4748642-98c4-437e-b0ed-4f9641c2e894
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: dineshmurthy
ms.openlocfilehash: 620efda06d8225b21b6bb9b104b79061ebb6515c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="3cf2f-103">Azure 儲存體用戶端工具</span><span class="sxs-lookup"><span data-stu-id="3cf2f-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="3cf2f-104">Azure 儲存體的使用者經常想要能夠使用 Azure 儲存體用戶端工具，檢視他們資料或與其互動。</span><span class="sxs-lookup"><span data-stu-id="3cf2f-104">Users of Azure Storage frequently want to be able to view/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="3cf2f-105">我們在下表中列出幾個可讓您這麼做的工具。</span><span class="sxs-lookup"><span data-stu-id="3cf2f-105">In the tables below, we list a number of tools that allow you to do this.</span></span> <span data-ttu-id="3cf2f-106">如果該區塊可以列舉及/或存取資料抽象，我們便在該區塊中放一個 "X"。</span><span class="sxs-lookup"><span data-stu-id="3cf2f-106">We put an "X" in each block if it provides the ability to either enumerate and/or access the data abstraction.</span></span> <span data-ttu-id="3cf2f-107">下表也會顯示該工具是否免費提供。</span><span class="sxs-lookup"><span data-stu-id="3cf2f-107">The table also shows if the tools is free or not.</span></span> <span data-ttu-id="3cf2f-108">「試用」表示有免費試用版，但完整產品並非免費。</span><span class="sxs-lookup"><span data-stu-id="3cf2f-108">"Trial" indicates that there is a free trial, but the full product is not free.</span></span> <span data-ttu-id="3cf2f-109">「Y/N」表示有某個版本可供免費使用，而另一個版本則需購買使用。</span><span class="sxs-lookup"><span data-stu-id="3cf2f-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="3cf2f-110">我們只提供可用的 Azure 儲存體用戶端工具的快照。</span><span class="sxs-lookup"><span data-stu-id="3cf2f-110">We've only provided a snapshot of the available Azure Storage client tools.</span></span> <span data-ttu-id="3cf2f-111">這些工具在功能上可能會繼續發展及成長。</span><span class="sxs-lookup"><span data-stu-id="3cf2f-111">These tools may continue to evolve and grow in functionality.</span></span> <span data-ttu-id="3cf2f-112">如果有修正或更新，請留言讓我們知道。</span><span class="sxs-lookup"><span data-stu-id="3cf2f-112">If there are corrections or updates, please leave a comment to let us know.</span></span> <span data-ttu-id="3cf2f-113">如果您知道有應該在這裡的工具，也請留言讓我們知道，我們很樂意將它們加入。</span><span class="sxs-lookup"><span data-stu-id="3cf2f-113">The same is true if you know of tools that ought to be here - we'd be happy to add them.</span></span>

<span data-ttu-id="3cf2f-114">**Microsoft Azure 儲存體用戶端工具**</span><span class="sxs-lookup"><span data-stu-id="3cf2f-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="3cf2f-115">Azure 儲存體用戶端工具</span><span class="sxs-lookup"><span data-stu-id="3cf2f-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-116">區塊 Blob</span><span class="sxs-lookup"><span data-stu-id="3cf2f-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-117">分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="3cf2f-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-118">附加 Blob</span><span class="sxs-lookup"><span data-stu-id="3cf2f-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-119">資料表</span><span class="sxs-lookup"><span data-stu-id="3cf2f-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-120">佇列</span><span class="sxs-lookup"><span data-stu-id="3cf2f-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-121">檔案</span><span class="sxs-lookup"><span data-stu-id="3cf2f-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-122">免費</span><span class="sxs-lookup"><span data-stu-id="3cf2f-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="3cf2f-123">平台</span><span class="sxs-lookup"><span data-stu-id="3cf2f-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-124">Web</span><span class="sxs-lookup"><span data-stu-id="3cf2f-124">Web</span></span></td>
    <td><span data-ttu-id="3cf2f-125">Windows</span><span class="sxs-lookup"><span data-stu-id="3cf2f-125">Windows</span></span></td>
    <td><span data-ttu-id="3cf2f-126">OSX</span><span class="sxs-lookup"><span data-stu-id="3cf2f-126">OSX</span></span></td>
    <td><span data-ttu-id="3cf2f-127">Linux</span><span class="sxs-lookup"><span data-stu-id="3cf2f-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure 入口網站</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="3cf2f-129">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-129">X</span></span></td>
    <td><span data-ttu-id="3cf2f-130">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-130">X</span></span></td>
    <td><span data-ttu-id="3cf2f-131">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-131">X</span></span></td>
    <td><span data-ttu-id="3cf2f-132">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-132">X</span></span></td>
    <td><span data-ttu-id="3cf2f-133">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-133">X</span></span></td>
    <td><span data-ttu-id="3cf2f-134">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-134">X</span></span></td>
    <td><span data-ttu-id="3cf2f-135">Y</span><span class="sxs-lookup"><span data-stu-id="3cf2f-135">Y</span></span></td>
    <td><span data-ttu-id="3cf2f-136">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-137"><a href="http://storageexplorer.com/">Microsoft Azure 儲存體總管</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="3cf2f-138">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-138">X</span></span></td>
    <td><span data-ttu-id="3cf2f-139">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-139">X</span></span></td>
    <td><span data-ttu-id="3cf2f-140">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-140">X</span></span></td>
    <td><span data-ttu-id="3cf2f-141">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-141">X</span></span></td>
    <td><span data-ttu-id="3cf2f-142">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-142">X</span></span></td>
    <td><span data-ttu-id="3cf2f-143">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-143">X</span></span></td>
    <td><span data-ttu-id="3cf2f-144">Y</span><span class="sxs-lookup"><span data-stu-id="3cf2f-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-145">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-145">X</span></span></td>
    <td><span data-ttu-id="3cf2f-146">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-146">X</span></span></td>
    <td><span data-ttu-id="3cf2f-147">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio 伺服器總管</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="3cf2f-149">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-149">X</span></span></td>
    <td><span data-ttu-id="3cf2f-150">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-150">X</span></span></td>
    <td><span data-ttu-id="3cf2f-151">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-151">X</span></span></td>
    <td><span data-ttu-id="3cf2f-152">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-152">X</span></span></td>
    <td><span data-ttu-id="3cf2f-153">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-154">Y</span><span class="sxs-lookup"><span data-stu-id="3cf2f-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-155">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="3cf2f-156">**協力廠商 Azure 儲存體工具**</span><span class="sxs-lookup"><span data-stu-id="3cf2f-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="3cf2f-157">我們尚未驗證下列協力廠商工具所宣稱的功能或品質，且其清單並不代表 Microsoft 背書。</span><span class="sxs-lookup"><span data-stu-id="3cf2f-157">We have not verified the functionality or quality claimed by the following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="3cf2f-158">Azure 儲存體用戶端工具</span><span class="sxs-lookup"><span data-stu-id="3cf2f-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-159">區塊 Blob</span><span class="sxs-lookup"><span data-stu-id="3cf2f-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-160">分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="3cf2f-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-161">附加 Blob</span><span class="sxs-lookup"><span data-stu-id="3cf2f-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-162">資料表</span><span class="sxs-lookup"><span data-stu-id="3cf2f-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-163">佇列</span><span class="sxs-lookup"><span data-stu-id="3cf2f-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-164">檔案</span><span class="sxs-lookup"><span data-stu-id="3cf2f-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="3cf2f-165">免費</span><span class="sxs-lookup"><span data-stu-id="3cf2f-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="3cf2f-166">平台</span><span class="sxs-lookup"><span data-stu-id="3cf2f-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-167">Web</span><span class="sxs-lookup"><span data-stu-id="3cf2f-167">Web</span></span></td>
    <td><span data-ttu-id="3cf2f-168">Windows</span><span class="sxs-lookup"><span data-stu-id="3cf2f-168">Windows</span></span></td>
    <td><span data-ttu-id="3cf2f-169">OSX</span><span class="sxs-lookup"><span data-stu-id="3cf2f-169">OSX</span></span></td>
    <td><span data-ttu-id="3cf2f-170">Linux</span><span class="sxs-lookup"><span data-stu-id="3cf2f-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-171"><a href="http://www.cloudportam.com/">Cloud Portam (英文)</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="3cf2f-172">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-172">X</span></span></td>
    <td><span data-ttu-id="3cf2f-173">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-173">X</span></span></td>
    <td><span data-ttu-id="3cf2f-174">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-174">X</span></span></td>
    <td><span data-ttu-id="3cf2f-175">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-175">X</span></span></td>
    <td><span data-ttu-id="3cf2f-176">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-176">X</span></span></td>
    <td><span data-ttu-id="3cf2f-177">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-177">X</span></span></td>
    <td><span data-ttu-id="3cf2f-178">試用版</span><span class="sxs-lookup"><span data-stu-id="3cf2f-178">Trial</span></span></td>
    <td><span data-ttu-id="3cf2f-179">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata：Azure Management Studio (英文)</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="3cf2f-181">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-181">X</span></span></td>
    <td><span data-ttu-id="3cf2f-182">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-182">X</span></span></td>
    <td><span data-ttu-id="3cf2f-183">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-183">X</span></span></td>
    <td><span data-ttu-id="3cf2f-184">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-184">X</span></span></td>
    <td><span data-ttu-id="3cf2f-185">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-185">X</span></span></td>
    <td><span data-ttu-id="3cf2f-186">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-186">X</span></span></td>
    <td><span data-ttu-id="3cf2f-187">試用版</span><span class="sxs-lookup"><span data-stu-id="3cf2f-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-188">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata：Azure 總管 (英文)</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="3cf2f-190">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-190">X</span></span></td>
    <td><span data-ttu-id="3cf2f-191">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-191">X</span></span></td>
    <td><span data-ttu-id="3cf2f-192">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-193">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-193">X</span></span></td>
    <td><span data-ttu-id="3cf2f-194">Y</span><span class="sxs-lookup"><span data-stu-id="3cf2f-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-195">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure 儲存體總管</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="3cf2f-197">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-197">X</span></span></td>
    <td><span data-ttu-id="3cf2f-198">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-199">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-199">X</span></span></td>
    <td><span data-ttu-id="3cf2f-200">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-201">Y</span><span class="sxs-lookup"><span data-stu-id="3cf2f-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-202">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry 總管 (英文)</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="3cf2f-204">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-204">X</span></span></td>
    <td><span data-ttu-id="3cf2f-205">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-206">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-206">X</span></span></td>
    <td><span data-ttu-id="3cf2f-207">Y/N</span><span class="sxs-lookup"><span data-stu-id="3cf2f-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-208">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine (英文)</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="3cf2f-210">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-210">X</span></span></td>
    <td><span data-ttu-id="3cf2f-211">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-212">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-212">X</span></span></td>
    <td><span data-ttu-id="3cf2f-213">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-214">試用版</span><span class="sxs-lookup"><span data-stu-id="3cf2f-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-215">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-216"><a href="http://clumsyleaf.com">ClumsyLeaf：AzureXplorer、CloudXplorer、TableXplorer (英文)</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="3cf2f-217">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-217">X</span></span></td>
    <td><span data-ttu-id="3cf2f-218">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-218">X</span></span></td>
    <td><span data-ttu-id="3cf2f-219">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-219">X</span></span></td>
    <td><span data-ttu-id="3cf2f-220">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-220">X</span></span></td>
    <td><span data-ttu-id="3cf2f-221">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-221">X</span></span></td>
    <td><span data-ttu-id="3cf2f-222">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-222">X</span></span></td>
    <td><span data-ttu-id="3cf2f-223">Y</span><span class="sxs-lookup"><span data-stu-id="3cf2f-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-224">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud (英文)</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="3cf2f-226">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-227">試用版</span><span class="sxs-lookup"><span data-stu-id="3cf2f-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-228">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-229"><a href="http://storageexplorer.codeplex.com/">Azure Web 儲存體總管 (英文)</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="3cf2f-230">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-230">X</span></span></td>
    <td><span data-ttu-id="3cf2f-231">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-232">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-232">X</span></span></td>
    <td><span data-ttu-id="3cf2f-233">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-234">Y</span><span class="sxs-lookup"><span data-stu-id="3cf2f-234">Y</span></span></td>
    <td><span data-ttu-id="3cf2f-235">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="3cf2f-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="3cf2f-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="3cf2f-237">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-237">X</span></span></td>
    <td><span data-ttu-id="3cf2f-238">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="3cf2f-239">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-239">X</span></span></td>
    <td><span data-ttu-id="3cf2f-240">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-240">X</span></span></td>
    <td><span data-ttu-id="3cf2f-241">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-241">X</span></span></td>
    <td><span data-ttu-id="3cf2f-242">試用版</span><span class="sxs-lookup"><span data-stu-id="3cf2f-242">Trial</span></span></td>
    <td><span data-ttu-id="3cf2f-243">X</span><span class="sxs-lookup"><span data-stu-id="3cf2f-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
