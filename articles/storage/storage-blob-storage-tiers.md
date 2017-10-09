---
title: "cool aaaAzure blob 儲存體 |Microsoft 文件"
description: "Azure Blob 儲存體的儲存層會根據存取模式，為物件資料提供具成本效益的儲存體。 hello 酷炫的儲存層最適合用於較不常存取的資料。"
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: eb33ed4f-1b17-4fd6-82e2-8d5372800eef
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/05/2017
ms.author: mihauss
ms.openlocfilehash: 56fae3fdae31a6958ebae01fd96a0366e70ae938
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-and-cool-storage-tiers"></a><span data-ttu-id="0c798-104">Azure Blob 儲存體︰經常性存取與非經常性存取儲存層</span><span class="sxs-lookup"><span data-stu-id="0c798-104">Azure Blob Storage: Hot and cool storage tiers</span></span>
## <a name="overview"></a><span data-ttu-id="0c798-105">概觀</span><span class="sxs-lookup"><span data-stu-id="0c798-105">Overview</span></span>
<span data-ttu-id="0c798-106">Azure 儲存體會為 Blob 物件儲存體提供兩個儲存層，所以您可根據您的資料使用方式，以最符合成本效益的方式進行儲存。</span><span class="sxs-lookup"><span data-stu-id="0c798-106">Azure Storage offers two storage tiers for Blob object storage so that you can store your data most cost-effectively depending on how you use it.</span></span> <span data-ttu-id="0c798-107">hello Azure**熱儲存層**最適合用於儲存經常存取的資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-107">hello Azure **hot storage tier** is optimized for storing data that is accessed frequently.</span></span> <span data-ttu-id="0c798-108">hello Azure**酷炫的儲存層**最適合用於儲存，而且不常存取長時間執行的資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-108">hello Azure **cool storage tier** is optimized for storing data that is infrequently accessed and long-lived.</span></span> <span data-ttu-id="0c798-109">Hello 酷炫的儲存層中的資料可容許較低的可用性，但仍需要高持久性和類似的時間來存取和輸送量特性做為熱資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-109">Data in hello cool storage tier can tolerate slightly lower availability, but still requires high durability and similar time-to-access and throughput characteristics as hot data.</span></span> <span data-ttu-id="0c798-110">對於非經常性存取資料而言，稍微較低的可用性 SLA 和更高的存取成本是可接受的取捨，可讓儲存體成本降低許多。</span><span class="sxs-lookup"><span data-stu-id="0c798-110">For cool data a slightly lower availability SLA and higher access costs are acceptable trade-offs for much lower storage costs.</span></span>

<span data-ttu-id="0c798-111">現在，指數的速度成長 hello 雲端中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-111">Today, data stored in hello cloud is growing at an exponential pace.</span></span> <span data-ttu-id="0c798-112">擴充的儲存體需要成本 toomanage，很有幫助 tooorganize 資料為基礎的屬性，例如存取頻率和規劃的保留期限。</span><span class="sxs-lookup"><span data-stu-id="0c798-112">toomanage costs for your expanding storage needs, it's helpful tooorganize your data based on attributes like frequency-of-access and planned retention period.</span></span> <span data-ttu-id="0c798-113">Hello 雲端中儲存的資料可能會不同方面如何產生、 處理，並存取其存留期。</span><span class="sxs-lookup"><span data-stu-id="0c798-113">Data stored in hello cloud can be different in terms of how it is generated, processed, and accessed over its lifetime.</span></span> <span data-ttu-id="0c798-114">有些資料在其存留期內會積極地存取及修改。</span><span class="sxs-lookup"><span data-stu-id="0c798-114">Some data is actively accessed and modified throughout its lifetime.</span></span> <span data-ttu-id="0c798-115">某些資料存取常見問題及早在其存留期間，存取卸除大幅 hello 資料年齡為。</span><span class="sxs-lookup"><span data-stu-id="0c798-115">Some data is accessed frequently early in its lifetime, with access dropping drastically as hello data ages.</span></span> <span data-ttu-id="0c798-116">某些資料 hello 定域機組中維持閒置很少是，如果曾，存取一次儲存。</span><span class="sxs-lookup"><span data-stu-id="0c798-116">Some data remains idle in hello cloud and is rarely, if ever, accessed once stored.</span></span>

<span data-ttu-id="0c798-117">上述每個資料存取案例均受惠於針對特定存取模式最佳化的差異化儲存層。</span><span class="sxs-lookup"><span data-stu-id="0c798-117">Each of these data access scenarios described above benefits from a differentiated tier of storage that is optimized for a particular access pattern.</span></span> <span data-ttu-id="0c798-118">Hello 引入的作用中且酷炫的儲存層，使用 Azure Blob 儲存體現在解決這需要使用不同的儲存層會分隔定價模型。</span><span class="sxs-lookup"><span data-stu-id="0c798-118">With hello introduction of hot and cool storage tiers, Azure Blob storage now addresses this need for differentiated storage tiers with separate pricing models.</span></span>

## <a name="blob-storage-accounts"></a><span data-ttu-id="0c798-119">Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0c798-119">Blob storage accounts</span></span>
<span data-ttu-id="0c798-120">**Blob 儲存體帳戶** 是特殊的儲存體帳戶，可將非結構化資料儲存為 Azure 儲存體中的 Blob (物件)。</span><span class="sxs-lookup"><span data-stu-id="0c798-120">**Blob storage accounts** are specialized storage accounts for storing your unstructured data as blobs (objects) in Azure Storage.</span></span> <span data-ttu-id="0c798-121">使用 Blob 儲存體帳戶，您現在可以選擇之間作用中且酷炫的儲存層 toostore cool 較低的儲存體成本，較不常存取的資料和更經常存取的存放區的低成本的存取熱資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-121">With Blob storage accounts, you can now choose between hot and cool storage tiers toostore your less frequently accessed cool data at a lower storage cost, and store more frequently accessed hot data at a lower access cost.</span></span> <span data-ttu-id="0c798-122">Blob 儲存體帳戶是類似 tooyour 現有一般用途的儲存體帳戶共用所有 hello 絕佳的持續性、 可用性、 延展性和效能的功能，您使用，包括區塊 blob 的 100 %api 一致性以及附加 blob。</span><span class="sxs-lookup"><span data-stu-id="0c798-122">Blob storage accounts are similar tooyour existing general-purpose storage accounts and share all hello great durability, availability, scalability, and performance features that you use today, including 100% API consistency for block blobs and append blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="0c798-123">Blob 儲存體帳戶僅支援區塊和附加 Blob，不支援分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="0c798-123">Blob storage accounts support only block and append blobs, and not page blobs.</span></span>
> 
> 

<span data-ttu-id="0c798-124">Blob 儲存體帳戶公開 hello**存取層**屬性，可讓您 toospecify hello 儲存層做**作用**或**Cool**根據 hello 資料儲存在 hello帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-124">Blob storage accounts expose hello **Access Tier** attribute, which allows you toospecify hello storage tier as **Hot** or **Cool** depending on hello data stored in hello account.</span></span> <span data-ttu-id="0c798-125">如果沒有在 hello 使用量模式中的資料變更，您也可以切換這些儲存層，在任何時間之間。</span><span class="sxs-lookup"><span data-stu-id="0c798-125">If there is a change in hello usage pattern of your data, you can also switch between these storage tiers at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="0c798-126">變更 hello 儲存層可能會導致產生額外費用。</span><span class="sxs-lookup"><span data-stu-id="0c798-126">Changing hello storage tier may result in additional charges.</span></span> <span data-ttu-id="0c798-127">請參閱 hello[定價和計費](storage-blob-storage-tiers.md#pricing-and-billing)> 一節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-127">Please see hello [Pricing and Billing](storage-blob-storage-tiers.md#pricing-and-billing) section for more details.</span></span>
> 
> 

<span data-ttu-id="0c798-128">Hello 熱儲存層的範例使用案例包括：</span><span class="sxs-lookup"><span data-stu-id="0c798-128">Example usage scenarios for hello hot storage tier include:</span></span>

* <span data-ttu-id="0c798-129">在使用中或預期的 toobe （從讀取和寫入） 經常存取的資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-129">Data that is in active use or expected toobe accessed (read from and written to) frequently.</span></span>
* <span data-ttu-id="0c798-130">分段進行處理和最終移轉 toohello 酷炫的儲存層的資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-130">Data that is staged for processing and eventual migration toohello cool storage tier.</span></span>

<span data-ttu-id="0c798-131">Hello 酷炫的儲存層的範例使用案例包括：</span><span class="sxs-lookup"><span data-stu-id="0c798-131">Example usage scenarios for hello cool storage tier include:</span></span>

* <span data-ttu-id="0c798-132">備份、封存和災害復原資料集。</span><span class="sxs-lookup"><span data-stu-id="0c798-132">Backup, archival and disaster recovery datasets.</span></span>
* <span data-ttu-id="0c798-133">較舊的媒體內容不會經常不再檢視，但時，預期的 toobe 可立即存取。</span><span class="sxs-lookup"><span data-stu-id="0c798-133">Older media content not viewed frequently anymore but is expected toobe available immediately when accessed.</span></span>
* <span data-ttu-id="0c798-134">需要 toobe 的大型資料集有效地儲存成本，而供未來處理所收集的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-134">Large data sets that need toobe stored cost effectively while more data is being gathered for future processing.</span></span> <span data-ttu-id="0c798-135">(例如，科學資料、來自製造工廠的原始遙測資料等長期儲存)</span><span class="sxs-lookup"><span data-stu-id="0c798-135">(*e.g.*, long-term storage of scientific data, raw telemetry data from a manufacturing facility)</span></span>
* <span data-ttu-id="0c798-136">即使已處理成最終可用格式，但還是需要保存的原始資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-136">Original (raw) data that must be preserved, even after it has been processed into final usable form.</span></span> <span data-ttu-id="0c798-137">(例如，轉碼成其他格式之後的原始媒體檔案)</span><span class="sxs-lookup"><span data-stu-id="0c798-137">(*e.g.*, Raw media files after transcoding into other formats)</span></span>
* <span data-ttu-id="0c798-138">相容性，而且需要長時間儲存 toobe 且難以曾經存取的封存資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-138">Compliance and archival data that needs toobe stored for a long time and is hardly ever accessed.</span></span> <span data-ttu-id="0c798-139">(例如，保全攝影機錄影畫面、醫療機構的舊 X 光/MRI、金融服務的客服電話錄音和文字記錄)</span><span class="sxs-lookup"><span data-stu-id="0c798-139">(*e.g.*, Security camera footage, old X-Rays/MRIs for healthcare organizations, audio recordings and transcripts of customer calls for financial services)</span></span>

<span data-ttu-id="0c798-140">如需儲存體帳戶的詳細資訊，請參閱 [關於 Azure 儲存體帳戶](storage-create-storage-account.md) 。</span><span class="sxs-lookup"><span data-stu-id="0c798-140">See [About Azure storage accounts](storage-create-storage-account.md) for more information on storage accounts.</span></span>

<span data-ttu-id="0c798-141">應用程式只需要封鎖，或附加 blob 儲存體，我們建議使用 Blob 儲存體帳戶，利用 hello tootake 區分計價模型的階層式儲存。</span><span class="sxs-lookup"><span data-stu-id="0c798-141">For applications requiring only block or append blob storage, we recommend using Blob storage accounts, tootake advantage of hello differentiated pricing model of tiered storage.</span></span> <span data-ttu-id="0c798-142">但是，我們了解這可能不是可能在某些情況下，使用一般用途儲存體帳戶會是 hello 方式 toogo，例如：</span><span class="sxs-lookup"><span data-stu-id="0c798-142">However, we understand this might not be possible under certain circumstances where using general-purpose storage accounts would be hello way toogo, such as:</span></span>

* <span data-ttu-id="0c798-143">您需要 toouse 資料表、 佇列，或檔案，且想您的 blob 儲存在 hello 相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-143">You need toouse tables, queues, or files and want your blobs stored in hello same storage account.</span></span> <span data-ttu-id="0c798-144">請注意，任何技術的優點 toostoring 這些 hello 除了擁有 hello 相同共用金鑰使用相同帳戶中。</span><span class="sxs-lookup"><span data-stu-id="0c798-144">Note that there is no technical advantage toostoring these in hello same account other than having hello same shared keys.</span></span>
* <span data-ttu-id="0c798-145">您仍然需要 toouse hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="0c798-145">You still need toouse hello Classic deployment model.</span></span> <span data-ttu-id="0c798-146">Blob 儲存體帳戶，才可透過 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="0c798-146">Blob storage accounts are only available via hello Azure Resource Manager deployment model.</span></span>
* <span data-ttu-id="0c798-147">您需要 toouse 分頁 blob。</span><span class="sxs-lookup"><span data-stu-id="0c798-147">You need toouse page blobs.</span></span> <span data-ttu-id="0c798-148">Blob 儲存體帳戶不支援分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="0c798-148">Blob storage accounts do not support page blobs.</span></span> <span data-ttu-id="0c798-149">我們通常建議使用區塊 Blob，除非您對分頁 Blob 有特定的需求。</span><span class="sxs-lookup"><span data-stu-id="0c798-149">We generally recommend using block blobs unless you have a specific need for page blobs.</span></span>
* <span data-ttu-id="0c798-150">您使用新版 hello[儲存體服務 REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx)低於 2014年-02-14，或是用戶端程式庫的版本低於 4.x，並無法升級您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c798-150">You use a version of hello [Storage Services REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) that is earlier than 2014-02-14 or a client library with a version lower than 4.x, and cannot upgrade your application.</span></span>

> [!NOTE]
> <span data-ttu-id="0c798-151">目前所有的 Azure 區域都支援 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-151">Blob storage accounts are currently supported in all Azure regions.</span></span>
> 
> 

## <a name="comparison-between-hello-storage-tiers"></a><span data-ttu-id="0c798-152">Hello 儲存層之間的比較</span><span class="sxs-lookup"><span data-stu-id="0c798-152">Comparison between hello storage tiers</span></span>
<span data-ttu-id="0c798-153">hello 下表會反白顯示 hello 比較兩個儲存層 hello:</span><span class="sxs-lookup"><span data-stu-id="0c798-153">hello following table highlights hello comparison between hello two storage tiers:</span></span>

<table border="1" cellspacing="0" cellpadding="0" style="border: 1px solid #000000;">
<col width="250">
<col width="250">
<col width="250">
<tbody>
<tr>
    <td><strong><center></center></strong></td>
    <td><span data-ttu-id="0c798-154"><strong><center>經常性存取儲存層</center></strong></span><span class="sxs-lookup"><span data-stu-id="0c798-154"><strong><center>Hot storage tier</center></strong></span></span></td>
    <td><span data-ttu-id="0c798-155"><strong><center>非經常性存取儲存層</center></strong></span><span class="sxs-lookup"><span data-stu-id="0c798-155"><strong><center>Cool storage tier</center></strong></span></span></td
</tr>
<tr>
    <td><span data-ttu-id="0c798-156"><strong><center>可用性</center></strong></span><span class="sxs-lookup"><span data-stu-id="0c798-156"><strong><center>Availability</center></strong></span></span></td>
    <td><span data-ttu-id="0c798-157"><center>99.9%</center></span><span class="sxs-lookup"><span data-stu-id="0c798-157"><center>99.9%</center></span></span></td>
    <td><span data-ttu-id="0c798-158"><center>99%</center></span><span class="sxs-lookup"><span data-stu-id="0c798-158"><center>99%</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="0c798-159"><strong><center>可用性</span><span class="sxs-lookup"><span data-stu-id="0c798-159"><strong><center>Availability</span></span><br><span data-ttu-id="0c798-160">(RA-GRS 讀取)</center></strong></span><span class="sxs-lookup"><span data-stu-id="0c798-160">(RA-GRS reads)</center></strong></span></span></td>
    <td><span data-ttu-id="0c798-161"><center>99.99%</center></span><span class="sxs-lookup"><span data-stu-id="0c798-161"><center>99.99%</center></span></span></td>
    <td><span data-ttu-id="0c798-162"><center>99.9%</center></span><span class="sxs-lookup"><span data-stu-id="0c798-162"><center>99.9%</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="0c798-163"><strong><center>使用費用</center></strong></span><span class="sxs-lookup"><span data-stu-id="0c798-163"><strong><center>Usage charges</center></strong></span></span></td>
    <td><span data-ttu-id="0c798-164"><center>儲存成本較高</span><span class="sxs-lookup"><span data-stu-id="0c798-164"><center>Higher storage costs</span></span><br><span data-ttu-id="0c798-165">存取和交易成本較低</center></span><span class="sxs-lookup"><span data-stu-id="0c798-165">Lower access and transaction costs</center></span></span></td>
    <td><span data-ttu-id="0c798-166"><center>儲存成本較低</span><span class="sxs-lookup"><span data-stu-id="0c798-166"><center>Lower storage costs</span></span><br><span data-ttu-id="0c798-167">存取和交易成本較高</center></span><span class="sxs-lookup"><span data-stu-id="0c798-167">Higher access and transaction costs</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="0c798-168"><strong><center>最小物件大小<center></strong></span><span class="sxs-lookup"><span data-stu-id="0c798-168"><strong><center>Minimum object size<center></strong></span></span></td>
    <td colspan="2"><span data-ttu-id="0c798-169"><center>N/A</center></span><span class="sxs-lookup"><span data-stu-id="0c798-169"><center>N/A</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="0c798-170"><strong><center>最小儲存持續時間<center></strong></span><span class="sxs-lookup"><span data-stu-id="0c798-170"><strong><center>Minimum storage duration<center></strong></span></span></td>
    <td colspan="2"><span data-ttu-id="0c798-171"><center>N/A</center></span><span class="sxs-lookup"><span data-stu-id="0c798-171"><center>N/A</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="0c798-172"><strong><center>延遲</span><span class="sxs-lookup"><span data-stu-id="0c798-172"><strong><center>Latency</span></span><br><span data-ttu-id="0c798-173">（時間 toofirst 位元組）<center></strong></span><span class="sxs-lookup"><span data-stu-id="0c798-173">(Time toofirst byte)<center></strong></span></span></td>
    <td colspan="2"><span data-ttu-id="0c798-174"><center>毫秒</center></span><span class="sxs-lookup"><span data-stu-id="0c798-174"><center>milliseconds</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="0c798-175"><strong><center>延展性和效能目標<center></strong></span><span class="sxs-lookup"><span data-stu-id="0c798-175"><strong><center>Scalability and performance targets<center></strong></span></span></td>
    <td colspan="2"><span data-ttu-id="0c798-176"><center>與一般用途儲存體帳戶相同</center></span><span class="sxs-lookup"><span data-stu-id="0c798-176"><center>Same as general-purpose storage accounts</center></span></span></td>
</tr>
</tbody>
</table>

> [!NOTE]
> <span data-ttu-id="0c798-177">Blob 儲存體帳戶支援 hello 相同的效能和延展性目標為一般用途儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-177">Blob storage accounts support hello same performance and scalability targets as general-purpose storage accounts.</span></span> <span data-ttu-id="0c798-178">如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md) (英文)。</span><span class="sxs-lookup"><span data-stu-id="0c798-178">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for more information.</span></span>
> 
> 

## <a name="pricing-and-billing"></a><span data-ttu-id="0c798-179">價格和計費</span><span class="sxs-lookup"><span data-stu-id="0c798-179">Pricing and Billing</span></span>
<span data-ttu-id="0c798-180">Blob 儲存體帳戶會將新的定價模型用於根據 hello 儲存層的 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0c798-180">Blob storage accounts use a new pricing model for blob storage based on hello storage tier.</span></span> <span data-ttu-id="0c798-181">當使用 Blob 儲存體帳戶時，適用於 hello 遵循計費考量：</span><span class="sxs-lookup"><span data-stu-id="0c798-181">When using a Blob storage account, hello following billing considerations apply:</span></span>

* <span data-ttu-id="0c798-182">**儲存體成本**： 此外 toohello 儲存的資料量，儲存資料的 hello 成本有所不同 hello 儲存層。</span><span class="sxs-lookup"><span data-stu-id="0c798-182">**Storage costs**: In addition toohello amount of data stored, hello cost of storing data varies depending on hello storage tier.</span></span> <span data-ttu-id="0c798-183">hello 每 gb 的成本會更低，比 hello 熱儲存層的 hello 酷炫的儲存層。</span><span class="sxs-lookup"><span data-stu-id="0c798-183">hello per-gigabyte cost is lower for hello cool storage tier than for hello hot storage tier.</span></span>
* <span data-ttu-id="0c798-184">**資料存取成本**: hello 酷炫的儲存層中的資料，您將支付每 gb 的資料存取需要付費讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="0c798-184">**Data access costs**: For data in hello cool storage tier, you will be charged a per-gigabyte data access charge for reads and writes.</span></span>
* <span data-ttu-id="0c798-185">**交易成本**︰這兩層都有每筆交易的費用。</span><span class="sxs-lookup"><span data-stu-id="0c798-185">**Transaction costs**: There is a per-transaction charge for both tiers.</span></span> <span data-ttu-id="0c798-186">不過，hello 酷炫的儲存層的 hello 每筆交易成本高於的 hello 熱儲存層。</span><span class="sxs-lookup"><span data-stu-id="0c798-186">However, hello per-transaction cost for hello cool storage tier is higher than that for hello hot storage tier.</span></span>
* <span data-ttu-id="0c798-187">**地理複寫資料傳輸成本**： 這只適用於 tooaccounts 異地複寫設定，包括 GRS 和 RA-GRS。</span><span class="sxs-lookup"><span data-stu-id="0c798-187">**Geo-Replication data transfer costs**: This only applies tooaccounts with geo-replication configured, including GRS and RA-GRS.</span></span> <span data-ttu-id="0c798-188">異地複寫資料傳輸會產生每 GB 費用。</span><span class="sxs-lookup"><span data-stu-id="0c798-188">Geo-replication data transfer incurs a per-gigabyte charge.</span></span>
* <span data-ttu-id="0c798-189">**輸出資料傳輸成本**︰輸出資料傳輸 (從 Azure 區域傳出的資料) 會產生每 GB 頻寬使用量費用，與一般用途的儲存體帳戶一致。</span><span class="sxs-lookup"><span data-stu-id="0c798-189">**Outbound data transfer costs**: Outbound data transfers (data that is transferred out of an Azure region) incur billing for bandwidth usage on a per-gigabyte basis, consistent with general-purpose storage accounts.</span></span>
* <span data-ttu-id="0c798-190">**變更 hello 儲存層**： 從 cool toohot 變更 hello 儲存層將會產生費用的相等 tooreading 所有現有的每個轉換的 hello 儲存體帳戶中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-190">**Changing hello storage tier**: Changing hello storage tier from cool toohot will incur a charge equal tooreading all hello data existing in hello storage account for every transition.</span></span> <span data-ttu-id="0c798-191">Hello 相反地，從熱 toocool 變更 hello 儲存層將免費提供的成本。</span><span class="sxs-lookup"><span data-stu-id="0c798-191">On hello other hand, changing hello storage tier from hot toocool will be free of cost.</span></span>

> [!NOTE]
> <span data-ttu-id="0c798-192">在排序 tooallow 使用者 tootry hello 出新的儲存層和驗證功能 post 啟動，hello 費用從 cool toohot 變更 hello 儲存層將會就免除關閉年 6 月 30 2016年之前。</span><span class="sxs-lookup"><span data-stu-id="0c798-192">In order tooallow users tootry out hello new storage tiers and validate functionality post launch, hello charge for changing hello storage tier from cool toohot will be waived off until June 30th 2016.</span></span> <span data-ttu-id="0c798-193">從 7 月 1 日 2016年開始，hello 費用就是從 cool toohot 套用的 tooall 轉換。</span><span class="sxs-lookup"><span data-stu-id="0c798-193">Starting July 1st 2016, hello charge will be applied tooall transitions from cool toohot.</span></span> <span data-ttu-id="0c798-194">如需 hello 計價模型的 Blob 儲存體帳戶的詳細資訊，請參閱[Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)頁面。</span><span class="sxs-lookup"><span data-stu-id="0c798-194">For more details on hello pricing model for Blob storage accounts see, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/) page.</span></span> <span data-ttu-id="0c798-195">如需 hello 傳出資料的詳細資訊請參閱傳輸費用，[資料傳輸定價詳細資料](https://azure.microsoft.com/pricing/details/data-transfers/)頁面。</span><span class="sxs-lookup"><span data-stu-id="0c798-195">For more details on hello outbound data transfer charges see, [Data Transfers Pricing Details](https://azure.microsoft.com/pricing/details/data-transfers/) page.</span></span>
> 
> 

## <a name="quick-start"></a><span data-ttu-id="0c798-196">快速啟動</span><span class="sxs-lookup"><span data-stu-id="0c798-196">Quick Start</span></span>
<span data-ttu-id="0c798-197">在本節中，我們將示範下列案例使用 hello Azure 入口網站的 hello:</span><span class="sxs-lookup"><span data-stu-id="0c798-197">In this section we will demonstrate hello following scenarios using hello Azure portal:</span></span>

* <span data-ttu-id="0c798-198">如何 toocreate Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-198">How toocreate a Blob storage account.</span></span>
* <span data-ttu-id="0c798-199">如何 toomanage Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-199">How toomanage a Blob storage account.</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="0c798-200">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0c798-200">Using hello Azure portal</span></span>
#### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a><span data-ttu-id="0c798-201">建立 Blob 儲存體帳戶使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0c798-201">Create a Blob storage account using hello Azure portal</span></span>
1. <span data-ttu-id="0c798-202">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="0c798-202">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c798-203">在 hello 中樞功能表中，選取 **新增** > **資料 + 儲存體** > **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="0c798-203">On hello Hub menu, select **New** > **Data + Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="0c798-204">輸入儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="0c798-204">Enter a name for your storage account.</span></span>
   
    <span data-ttu-id="0c798-205">此名稱必須是全域唯一的。它會當做 hello URL 的一部分使用 tooaccess hello 物件 hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="0c798-205">This name must be globally unique; it is used as part of hello URL used tooaccess hello objects in hello storage account.</span></span>  
4. <span data-ttu-id="0c798-206">選取**資源管理員**為 hello 部署模型。</span><span class="sxs-lookup"><span data-stu-id="0c798-206">Select **Resource Manager** as hello deployment model.</span></span>
   
    <span data-ttu-id="0c798-207">階層式的儲存只能使用資源管理員的儲存體帳戶。這是建議的新資源部署模型的 hello。</span><span class="sxs-lookup"><span data-stu-id="0c798-207">Tiered storage can only be used with Resource Manager storage accounts; this is hello recommended deployment model for new resources.</span></span> <span data-ttu-id="0c798-208">如需詳細資訊，請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0c798-208">For more information, check out hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>  
5. <span data-ttu-id="0c798-209">在 hello 帳戶類型 下拉式清單中，選取  **Blob 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="0c798-209">In hello Account Kind dropdown list, select **Blob Storage**.</span></span>
   
    <span data-ttu-id="0c798-210">這是您在其中選取 hello 儲存體帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="0c798-210">This is where you select hello type of storage account.</span></span> <span data-ttu-id="0c798-211">階層式的儲存不適用於一般用途的儲存體。您僅供以 hello Blob 儲存體類型的帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-211">Tiered storage is not available in general-purpose storage; it is only available in hello Blob storage type account.</span></span>     
   
    <span data-ttu-id="0c798-212">請注意，當您選取此選項，hello 效能層，會設定 tooStandard。</span><span class="sxs-lookup"><span data-stu-id="0c798-212">Note that when you select this, hello performance tier is set tooStandard.</span></span> <span data-ttu-id="0c798-213">無法使用與 hello 高階效能層階層式的儲存。</span><span class="sxs-lookup"><span data-stu-id="0c798-213">Tiered storage is not available with hello Premium performance tier.</span></span>
6. <span data-ttu-id="0c798-214">選取 hello hello 儲存體帳戶的複寫選項： **LRS**， **GRS**，或**RA-GRS**。</span><span class="sxs-lookup"><span data-stu-id="0c798-214">Select hello replication option for hello storage account: **LRS**, **GRS**, or **RA-GRS**.</span></span> <span data-ttu-id="0c798-215">hello 預設值是**RA-GRS**。</span><span class="sxs-lookup"><span data-stu-id="0c798-215">hello default is **RA-GRS**.</span></span>
   
    <span data-ttu-id="0c798-216">LRS = 本機備援儲存體。GRS = 地理備援儲存體 （2 地區）。RA-GRS 是讀取權限的地理備援儲存體 （2 區域具有讀取存取 toohello 第二個）。</span><span class="sxs-lookup"><span data-stu-id="0c798-216">LRS = locally redundant storage; GRS = geo-redundant storage (2 regions); RA-GRS is read-access geo-redundant storage (2 regions with read access toohello second).</span></span>
   
    <span data-ttu-id="0c798-217">如需 Azure 儲存體複寫選項的詳細資訊，請參閱 [Azure 儲存體複寫](storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="0c798-217">For more details on Azure Storage replication options, check out [Azure Storage replication](storage-redundancy.md).</span></span>
7. <span data-ttu-id="0c798-218">針對您的需求選取 hello 右邊的儲存層： 集 hello**存取層**tooeither **Cool**或**作用**。</span><span class="sxs-lookup"><span data-stu-id="0c798-218">Select hello right storage tier for your needs: Set hello **Access tier** tooeither **Cool** or **Hot**.</span></span> <span data-ttu-id="0c798-219">hello 預設值是**作用**。</span><span class="sxs-lookup"><span data-stu-id="0c798-219">hello default is **Hot**.</span></span>
8. <span data-ttu-id="0c798-220">選取您想在其中 toocreate hello 新儲存體帳戶的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-220">Select hello subscription in which you want toocreate hello new storage account.</span></span>
9. <span data-ttu-id="0c798-221">指定新的資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0c798-221">Specify a new resource group or select an existing resource group.</span></span> <span data-ttu-id="0c798-222">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0c798-222">For more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
10. <span data-ttu-id="0c798-223">選取儲存體帳戶的 hello 地區。</span><span class="sxs-lookup"><span data-stu-id="0c798-223">Select hello region for your storage account.</span></span>
11. <span data-ttu-id="0c798-224">按一下**建立**toocreate hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-224">Click **Create** toocreate hello storage account.</span></span>

#### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a><span data-ttu-id="0c798-225">變更 hello 儲存層的 Blob 儲存體帳戶使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0c798-225">Change hello storage tier of a Blob storage account using hello Azure portal</span></span>
1. <span data-ttu-id="0c798-226">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="0c798-226">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c798-227">toonavigate tooyour 儲存體帳戶，選取所有的資源，然後選取 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-227">toonavigate tooyour storage account, select All Resources, then select your storage account.</span></span>
3. <span data-ttu-id="0c798-228">在 hello 設定刀鋒視窗中，按一下 **組態**tooview 和/或變更 hello 帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="0c798-228">In hello Settings blade, click **Configuration** tooview and/or change hello account configuration.</span></span>
4. <span data-ttu-id="0c798-229">針對您的需求選取 hello 右邊的儲存層： 集 hello**存取層**tooeither **Cool**或**作用**。</span><span class="sxs-lookup"><span data-stu-id="0c798-229">Select hello right storage tier for your needs: Set hello **Access tier** tooeither **Cool** or **Hot**.</span></span>
5. <span data-ttu-id="0c798-230">按一下 儲存在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="0c798-230">Click Save at hello top of hello blade.</span></span>

> [!NOTE]
> <span data-ttu-id="0c798-231">變更 hello 儲存層可能會導致產生額外費用。</span><span class="sxs-lookup"><span data-stu-id="0c798-231">Changing hello storage tier may result in additional charges.</span></span> <span data-ttu-id="0c798-232">請參閱 hello[定價和計費](storage-blob-storage-tiers.md#pricing-and-billing)> 一節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-232">Please see hello [Pricing and Billing](storage-blob-storage-tiers.md#pricing-and-billing) section for more details.</span></span>
> 
> 

## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a><span data-ttu-id="0c798-233">評估和移轉 tooBlob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0c798-233">Evaluating and migrating tooBlob storage accounts</span></span>
<span data-ttu-id="0c798-234">hello 本節的目的是 toohelp 使用者 toomake smooth 轉換 toousing Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-234">hello purpose of this section is toohelp users toomake a smooth transition toousing Blob storage accounts.</span></span> <span data-ttu-id="0c798-235">有兩個使用者案例：</span><span class="sxs-lookup"><span data-stu-id="0c798-235">There are two user scenarios:</span></span>

* <span data-ttu-id="0c798-236">您有現有的一般用途儲存體帳戶，並想 tooevaluate 變更 tooa 與 hello 右邊的儲存層的 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-236">You have an existing general-purpose storage account and want tooevaluate a change tooa Blob storage account with hello right storage tier.</span></span>
* <span data-ttu-id="0c798-237">您已決定 toouse Blob 儲存體帳戶或已經有一個，而且要 tooevaluate 是否應該使用 hello 熱或酷炫的儲存層。</span><span class="sxs-lookup"><span data-stu-id="0c798-237">You have decided toouse a Blob storage account or already have one and want tooevaluate whether you should use hello hot or cool storage tier.</span></span>

<span data-ttu-id="0c798-238">在這兩種情況下，hello 首先會是 tooestimate hello 成本儲存和存取資料的 Blob 儲存體帳戶中儲存和比較針對您目前的成本。</span><span class="sxs-lookup"><span data-stu-id="0c798-238">In both cases, hello first order of business is tooestimate hello cost of storing and accessing your data stored in a Blob storage account and compare that against your current costs.</span></span>

### <a name="evaluating-blob-storage-account-tiers"></a><span data-ttu-id="0c798-239">評估 Blob 儲存體帳戶層</span><span class="sxs-lookup"><span data-stu-id="0c798-239">Evaluating Blob storage account tiers</span></span>
<span data-ttu-id="0c798-240">中的儲存和存取儲存在 Blob 儲存體帳戶中的資料順序 tooestimate hello 成本，您將需要 tooevaluate 您現有的使用模式，或接近您的預期的使用模式。</span><span class="sxs-lookup"><span data-stu-id="0c798-240">In order tooestimate hello cost of storing and accessing data stored in a Blob storage account, you will need tooevaluate your existing usage pattern or approximate your expected usage pattern.</span></span> <span data-ttu-id="0c798-241">一般情況下，您會想 tooknow:</span><span class="sxs-lookup"><span data-stu-id="0c798-241">In general, you will want tooknow:</span></span>

* <span data-ttu-id="0c798-242">您的儲存體使用情況 – 目前儲存多少資料，以及每個月的變化情況為何？</span><span class="sxs-lookup"><span data-stu-id="0c798-242">Your storage consumption - How much data is being stored and how does this change on a monthly basis?</span></span>
* <span data-ttu-id="0c798-243">您儲存體的存取模式-多少資料正被讀取和寫入的 toohello 帳戶 （包括新的資料）？</span><span class="sxs-lookup"><span data-stu-id="0c798-243">Your storage access pattern - How much data is being read from and written toohello account (including new data)?</span></span> <span data-ttu-id="0c798-244">有多少交易用於資料存取，而它們是何種交易？</span><span class="sxs-lookup"><span data-stu-id="0c798-244">How many transactions are used for data access, and what kinds of transactions are they?</span></span>

#### <a name="monitoring-existing-storage-accounts"></a><span data-ttu-id="0c798-245">監視現有的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0c798-245">Monitoring existing storage accounts</span></span>
<span data-ttu-id="0c798-246">toomonitor 現有的儲存體帳戶和收集資料，您可以利用 Azure 儲存體分析的執行記錄，並提供儲存體帳戶的度量資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-246">toomonitor your existing storage accounts and gather this data, you can make use of Azure Storage Analytics which performs logging and provides metrics data for a storage account.</span></span>
<span data-ttu-id="0c798-247">儲存體分析可儲存有關要求 toohello 一般用途儲存體帳戶以及 Blob 儲存體帳戶的 Blob 儲存體服務的彙總的交易統計資料和容量資料的度量。</span><span class="sxs-lookup"><span data-stu-id="0c798-247">Storage Analytics can store metrics that include aggregated transaction statistics and capacity data about requests toohello Blob storage service for both general-purpose storage accounts as well as Blob storage accounts.</span></span>
<span data-ttu-id="0c798-248">此資料會儲存在已知資料表中 hello 相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-248">This data is stored in well-known tables in hello same storage account.</span></span>

<span data-ttu-id="0c798-249">如需詳細資訊，請參閱[關於儲存體分析度量](https://msdn.microsoft.com/library/azure/hh343258.aspx)和[儲存體分析度量資料表結構描述](https://msdn.microsoft.com/library/azure/hh343264.aspx)</span><span class="sxs-lookup"><span data-stu-id="0c798-249">For more details, please see [About Storage Analytics Metrics](https://msdn.microsoft.com/library/azure/hh343258.aspx) and [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="0c798-250">Blob 儲存體帳戶公開 hello 表格服務端點，僅適用於儲存和存取該帳戶的 hello 度量資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-250">Blob storage accounts expose hello table service endpoint only for storing and accessing hello metrics data for that account.</span></span>
> 
> 

<span data-ttu-id="0c798-251">toomonitor hello Blob 儲存體服務的 hello 存放裝置耗用量，您將需要 tooenable hello 容量度量。</span><span class="sxs-lookup"><span data-stu-id="0c798-251">toomonitor hello storage consumption for hello Blob storage service, you will need tooenable hello capacity metrics.</span></span>
<span data-ttu-id="0c798-252">使用此啟用，容量儲存體帳戶之 Blob 服務，針對每日記錄和記錄的資料為資料表的項目寫入 toohello *$MetricsCapacityBlob*資料表內 hello 相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-252">With this enabled, capacity data is recorded daily for a storage account's Blob service, and recorded as a table entry that is written toohello *$MetricsCapacityBlob* table within hello same storage account.</span></span>

<span data-ttu-id="0c798-253">toomonitor hello 資料存取模式的 hello Blob 儲存體服務，您將需要 tooenable hello 每小時交易度量應用程式開發介面層級。</span><span class="sxs-lookup"><span data-stu-id="0c798-253">toomonitor hello data access pattern for hello Blob storage service, you will need tooenable hello hourly transaction metrics at an API level.</span></span>
<span data-ttu-id="0c798-254">與此啟用，每個 API 交易是每小時的彙總資料和記錄資料表項目寫入 toohello 為*$MetricsHourPrimaryTransactionsBlob*資料表內 hello 相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-254">With this enabled, per API transactions are aggregated every hour, and recorded as a table entry that is written toohello *$MetricsHourPrimaryTransactionsBlob* table within hello same storage account.</span></span> <span data-ttu-id="0c798-255">hello *$MetricsHourSecondaryTransactionsBlob*資料表記錄 hello 交易 toohello 次要端點發生 RA-GRS 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-255">hello *$MetricsHourSecondaryTransactionsBlob* table records hello transactions toohello secondary endpoint in case of RA-GRS storage accounts.</span></span>

> [!NOTE]
> <span data-ttu-id="0c798-256">如果您已有一般用途的儲存體帳戶，並在中儲存分頁 blob 和虛擬機器磁碟以及區塊和附加 blob 資料，就不適用此估計程序。</span><span class="sxs-lookup"><span data-stu-id="0c798-256">In case you have a general-purpose storage account in which you have stored page blobs and virtual machine disks alongside block and append blob data, this estimation process is not applicable.</span></span> <span data-ttu-id="0c798-257">這是因為您將無法區別容量的交易度量僅根據 hello 型別之 blob 的區塊及附加 blob 可以是移轉 tooa Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-257">This is because you will have no way of distinguishing capacity and transaction metrics based on hello type of blob for only block and append blobs which can be migrated tooa Blob storage account.</span></span>
> 
> 

<span data-ttu-id="0c798-258">tooget 資料使用和存取模式的良好近似值，我們建議您選擇規則的使用方式，代表 hello 度量的保留期限，並藉此推斷。</span><span class="sxs-lookup"><span data-stu-id="0c798-258">tooget a good approximation of your data consumption and access pattern, we recommend you choose a retention period for hello metrics that is representative of your regular usage, and extrapolate.</span></span>
<span data-ttu-id="0c798-259">其中一個選項是 tooretain hello 度量資料的 7 天和收集 hello 資料進行分析 hello hello 月份結尾的每週。</span><span class="sxs-lookup"><span data-stu-id="0c798-259">One option is tooretain hello metrics data for 7 days and collect hello data every week, for analysis at hello end of hello month.</span></span>
<span data-ttu-id="0c798-260">另一個選項是 hello tooretain hello 度量資料過去 30 天內收集及分析和 hello 資料結尾 hello hello 30 天的期限。</span><span class="sxs-lookup"><span data-stu-id="0c798-260">Another option is tooretain hello metrics data for hello last 30 days and collect and analyze hello data at hello end of hello 30-day period.</span></span>

<span data-ttu-id="0c798-261">如需啟用、收集和檢視度量資料的詳細資訊，請參閱 [啟用 Azure 儲存體度量和檢視度量資料](storage-enable-and-view-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="0c798-261">For details on enabling, collecting and viewing metrics data, please see, [Enabling Azure Storage metrics and viewing metrics data](storage-enable-and-view-metrics.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0c798-262">就如同一般使用者資料，儲存、存取和下載分析資料也需付費。</span><span class="sxs-lookup"><span data-stu-id="0c798-262">Storing, accessing and downloading analytics data is also charged just like regular user data.</span></span>
> 
> 

#### <a name="utilizing-usage-metrics-tooestimate-costs"></a><span data-ttu-id="0c798-263">利用使用度量 tooestimate 成本</span><span class="sxs-lookup"><span data-stu-id="0c798-263">Utilizing usage metrics tooestimate costs</span></span>
##### <a name="storage-costs"></a><span data-ttu-id="0c798-264">儲存成本</span><span class="sxs-lookup"><span data-stu-id="0c798-264">Storage costs</span></span>
<span data-ttu-id="0c798-265">hello hello 容量度量資料表中的最新項目*$MetricsCapacityBlob* hello 資料列索引鍵與*'data'*顯示 hello 供使用者資料的儲存容量。</span><span class="sxs-lookup"><span data-stu-id="0c798-265">hello latest entry in hello capacity metrics table *$MetricsCapacityBlob* with hello row key *'data'* shows hello storage capacity consumed by user data.</span></span>
<span data-ttu-id="0c798-266">hello hello 容量度量資料表中的最新項目*$MetricsCapacityBlob* hello 資料列索引鍵與*'分析'*顯示 hello hello 分析記錄檔所使用的儲存容量。</span><span class="sxs-lookup"><span data-stu-id="0c798-266">hello latest entry in hello capacity metrics table *$MetricsCapacityBlob* with hello row key *'analytics'* shows hello storage capacity consumed by hello analytics logs.</span></span>

<span data-ttu-id="0c798-267">接著可以使用這兩個使用者資料與分析資料記錄 （如果啟用） 此總容量使用 tooestimate hello 成本 hello 儲存體帳戶中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-267">This total capacity consumed by both user data and analytics logs (if enabled) can then be used tooestimate hello cost of storing data in hello storage account.</span></span>
<span data-ttu-id="0c798-268">hello 相同方法也可用來估計儲存體成本區塊，並附加一般用途儲存體帳戶中的 blob。</span><span class="sxs-lookup"><span data-stu-id="0c798-268">hello same method can also be used for estimating storage costs for block and append blobs in general-purpose storage accounts.</span></span>

##### <a name="transaction-costs"></a><span data-ttu-id="0c798-269">交易成本</span><span class="sxs-lookup"><span data-stu-id="0c798-269">Transaction costs</span></span>
<span data-ttu-id="0c798-270">hello 總和*'TotalBillableRequests'*，在 api hello 交易中的所有項目度量表會指出 hello 總該特定 API 的交易數。</span><span class="sxs-lookup"><span data-stu-id="0c798-270">hello sum of *'TotalBillableRequests'*, across all entries for an API in hello transaction metrics table indicates hello total number of transactions for that particular API.</span></span> <span data-ttu-id="0c798-271">*例如*，hello 總數*'GetBlob'*使用 hello 資料列索引鍵的所有項目為可計費的要求總數的 hello 總和可以計算在指定時間的交易*' 使用者資訊。GetBlob'*。</span><span class="sxs-lookup"><span data-stu-id="0c798-271">*e.g.*, hello total number of *'GetBlob'* transactions in a given period can be calculated by hello sum of total billable requests for all entries with hello row key *'user;GetBlob'*.</span></span>

<span data-ttu-id="0c798-272">順序 tooestimate Blob 儲存體帳戶的交易成本，您必須向分成三個群組的 hello 交易 toobreak 因為它們的方式不同價格。</span><span class="sxs-lookup"><span data-stu-id="0c798-272">In order tooestimate transaction costs for Blob storage accounts, you will need toobreak down hello transactions into three groups since they are priced differently.</span></span>

* <span data-ttu-id="0c798-273">寫入 'PutBlob'、'PutBlock'、'PutBlockList'、'AppendBlock'、'ListBlobs'、'ListContainers'、'CreateContainer'、'SnapshotBlob' 和 'CopyBlob' 等交易。</span><span class="sxs-lookup"><span data-stu-id="0c798-273">Write transactions such as *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'*, and *'CopyBlob'*.</span></span>
* <span data-ttu-id="0c798-274">刪除 'DeleteBlob' 和 'DeleteContainer' 等交易。</span><span class="sxs-lookup"><span data-stu-id="0c798-274">Delete transactions such as *'DeleteBlob'* and *'DeleteContainer'*.</span></span>
* <span data-ttu-id="0c798-275">所有其他交易</span><span class="sxs-lookup"><span data-stu-id="0c798-275">All other transactions.</span></span>

<span data-ttu-id="0c798-276">在一般用途儲存體帳戶的順序 tooestimate 交易成本，您需要 tooaggregate 無論 hello 作業/應用程式開發介面的所有交易。</span><span class="sxs-lookup"><span data-stu-id="0c798-276">In order tooestimate transaction costs for general-purpose storage accounts, you need tooaggregate all transactions irrespective of hello operation/API.</span></span>

##### <a name="data-access-and-geo-replication-data-transfer-costs"></a><span data-ttu-id="0c798-277">資料存取和異地複寫資料傳輸費用</span><span class="sxs-lookup"><span data-stu-id="0c798-277">Data access and geo-replication data transfer costs</span></span>
<span data-ttu-id="0c798-278">雖然未提供儲存體分析 hello 資料量讀取和寫入 tooa 儲存體帳戶，它可以來概略估計藉由查看 hello 交易度量資料表。</span><span class="sxs-lookup"><span data-stu-id="0c798-278">While storage analytics does not provide hello amount of data read from and written tooa storage account, it can be roughly estimated by looking at hello transaction metrics table.</span></span>
<span data-ttu-id="0c798-279">hello 總和*'TotalIngress'*資料表在 hello 交易度量 api 的所有項目該特定應用程式開發介面的指出 hello 總量，以位元組為單位的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-279">hello sum of *'TotalIngress'* across all entries for an API in hello transaction metrics table indicates hello total amount of ingress data in bytes for that particular API.</span></span>
<span data-ttu-id="0c798-280">同樣地 hello 總和*'TotalEgress'*指出 hello 的輸出資料，以位元組為單位的總容量。</span><span class="sxs-lookup"><span data-stu-id="0c798-280">Similarly hello sum of *'TotalEgress'* indicates hello total amount of egress data, in bytes.</span></span>

<span data-ttu-id="0c798-281">順序 tooestimate hello 資料存取的成本 Blob 儲存體帳戶，您必須使用 toobreak 向 hello 分成兩個群組的交易。</span><span class="sxs-lookup"><span data-stu-id="0c798-281">In order tooestimate hello data access costs for Blob storage accounts, you will need toobreak down hello transactions into two groups.</span></span>

* <span data-ttu-id="0c798-282">來估計 hello 數量 hello 儲存體帳戶中擷取的資料，請查看 hello 總和*'TotalEgress'*主要 hello *'GetBlob'*和*'Copyblob 應用程式開發'*作業。</span><span class="sxs-lookup"><span data-stu-id="0c798-282">hello amount of data retrieved from hello storage account can be estimated by looking at hello sum of *'TotalEgress'* for primarily hello *'GetBlob'* and *'CopyBlob'* operations.</span></span>
* <span data-ttu-id="0c798-283">您可以藉由查看 hello 總和估計寫入 toohello 儲存體帳戶的資料的 hello 數量*'TotalIngress'*主要 hello *'PutBlob'*， *'PutBlock'*， *'Copyblob 應用程式開發'*和*'AppendBlock'*作業。</span><span class="sxs-lookup"><span data-stu-id="0c798-283">hello amount of data written toohello storage account can be estimated by looking at hello sum of *'TotalIngress'* for primarily hello *'PutBlob'*, *'PutBlock'*, *'CopyBlob'* and *'AppendBlock'* operations.</span></span>

<span data-ttu-id="0c798-284">hello 異地備援 blob 儲存體帳戶也可以透過 hello 估計 hello GRS 或 RA-GRS 儲存體帳戶發生寫入的資料量的計算的資料傳輸的成本。</span><span class="sxs-lookup"><span data-stu-id="0c798-284">hello cost of geo-replication data transfer for Blob storage accounts can also be calculated by using hello estimate for hello amount of data written in case of a GRS or RA-GRS storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="0c798-285">如需計算使用 hello 熱或酷炫的儲存層的 hello 成本更詳細範例，請看看 hello 標題*'什麼是作用和 Cool 存取層，以及如何應該判斷哪一個 toouse' 嗎？*</span><span class="sxs-lookup"><span data-stu-id="0c798-285">For a more detailed example about calculating hello costs for using hello hot or cool storage tier, please take a look at hello FAQ titled *'What are Hot and Cool access tiers and how should I determine which one toouse?'*</span></span> <span data-ttu-id="0c798-286">在 hello [Azure 儲存體定價頁面](https://azure.microsoft.com/pricing/details/storage/)。</span><span class="sxs-lookup"><span data-stu-id="0c798-286">in hello [Azure Storage Pricing Page](https://azure.microsoft.com/pricing/details/storage/).</span></span>
> 
> 

### <a name="migrating-existing-data"></a><span data-ttu-id="0c798-287">移轉現有的資料</span><span class="sxs-lookup"><span data-stu-id="0c798-287">Migrating existing data</span></span>
<span data-ttu-id="0c798-288">Blob 儲存體帳戶專門用於儲存區塊和附加 Blob。</span><span class="sxs-lookup"><span data-stu-id="0c798-288">A Blob storage account is specialized for storing only block and append blobs.</span></span> <span data-ttu-id="0c798-289">現有的一般用途儲存體帳戶、 toostore 資料表、 佇列、 檔案和磁碟，以及 blob，可讓您不能轉換的 tooBlob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-289">Existing general-purpose storage accounts, which allow you toostore tables, queues, files and disks, as well as blobs, cannot be converted tooBlob storage accounts.</span></span> <span data-ttu-id="0c798-290">toouse hello 儲存層，您會需要 toocreate 新 Blob 儲存體帳戶，並將現有的資料移轉到新建立的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-290">toouse hello storage tiers, you will need toocreate new Blob storage accounts and migrate your existing data into hello newly created accounts.</span></span>

<span data-ttu-id="0c798-291">您可以使用下列方法 toomigrate 現有資料至 Blob 儲存體帳戶，從內部部署存放裝置、 協力廠商雲端存放裝置提供者，或從現有的一般用途儲存體帳戶在 Azure 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="0c798-291">You can use hello following methods toomigrate existing data into Blob storage accounts from on-premises storage devices, from third-party cloud storage providers, or from your existing general-purpose storage accounts in Azure:</span></span>

#### <a name="azcopy"></a><span data-ttu-id="0c798-292">AzCopy</span><span class="sxs-lookup"><span data-stu-id="0c798-292">AzCopy</span></span>
<span data-ttu-id="0c798-293">AzCopy 是專為高效能的資料 tooand 複製從 Azure 儲存體設計的 Windows 命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="0c798-293">AzCopy is a Windows command-line utility designed for high-performance copying of data tooand from Azure Storage.</span></span> <span data-ttu-id="0c798-294">您可以使用 從內部部署儲存體裝置 AzCopy toocopy 資料到 Blob 儲存體帳戶從現有的一般用途儲存體帳戶或 tooupload 資料，將 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-294">You can use AzCopy toocopy data into your Blob storage account from your existing general-purpose storage accounts, or tooupload data from your on-premises storage devices into your Blob storage account.</span></span>

<span data-ttu-id="0c798-295">如需詳細資訊，請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="0c798-295">For more details, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

#### <a name="data-movement-library"></a><span data-ttu-id="0c798-296">資料移動程式庫</span><span class="sxs-lookup"><span data-stu-id="0c798-296">Data Movement Library</span></span>
<span data-ttu-id="0c798-297">Azure 儲存體的資料移動.NET 程式庫根據 hello 核心資料移動架構提供 AzCopy。</span><span class="sxs-lookup"><span data-stu-id="0c798-297">Azure Storage data movement library for .NET is based on hello core data movement framework that powers AzCopy.</span></span> <span data-ttu-id="0c798-298">hello 程式庫設計的高效能、 可靠且簡單的資料傳輸作業類似 tooAzCopy。</span><span class="sxs-lookup"><span data-stu-id="0c798-298">hello library is designed for high-performance, reliable and easy data transfer operations similar tooAzCopy.</span></span> <span data-ttu-id="0c798-299">這可讓您的 hello 所提供的功能 AzCopy 應用程式中原本就不需要執行與監視外部的執行個體的 AzCopy toodeal tootake 完整優點。</span><span class="sxs-lookup"><span data-stu-id="0c798-299">This allows you tootake full benefits of hello features provided by AzCopy in your application natively without having toodeal with running and monitoring external instances of AzCopy.</span></span>

<span data-ttu-id="0c798-300">如需詳細資訊，請參閱 [適用於 .Net 的 Azure 儲存體資料移動程式庫](https://github.com/Azure/azure-storage-net-data-movement)</span><span class="sxs-lookup"><span data-stu-id="0c798-300">For more details, see [Azure Storage Data Movement Library for .Net](https://github.com/Azure/azure-storage-net-data-movement)</span></span>

#### <a name="rest-api-or-client-library"></a><span data-ttu-id="0c798-301">REST API 或用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="0c798-301">REST API or Client Library</span></span>
<span data-ttu-id="0c798-302">您可以建立自訂應用程式 toomigrate 資料到 Blob 儲存體帳戶，使用其中一種 hello Azure 用戶端程式庫或 hello Azure 儲存體服務 REST API。</span><span class="sxs-lookup"><span data-stu-id="0c798-302">You can create a custom application toomigrate your data into a Blob storage account using one of hello Azure client libraries or hello Azure storage services REST API.</span></span> <span data-ttu-id="0c798-303">Azure 儲存體針對以下多種語言和平台提供豐富的用戶端程式庫：例如 .NET、Java、C++、Node.JS、PHP、Ruby 和 Python。</span><span class="sxs-lookup"><span data-stu-id="0c798-303">Azure Storage provides rich client libraries for multiple languages and platforms like .NET, Java, C++, Node.JS, PHP, Ruby, and Python.</span></span> <span data-ttu-id="0c798-304">hello 用戶端程式庫提供進階的功能，例如重試邏輯、 記錄和並行上傳。</span><span class="sxs-lookup"><span data-stu-id="0c798-304">hello client libraries offer advanced capabilities such as retry logic, logging, and parallel uploads.</span></span> <span data-ttu-id="0c798-305">您也可以直接對 hello REST API，可以呼叫任何提出 HTTP/HTTPS 要求的語言所開發。</span><span class="sxs-lookup"><span data-stu-id="0c798-305">You can also develop directly against hello REST API, which can be called by any language that makes HTTP/HTTPS requests.</span></span>

<span data-ttu-id="0c798-306">如需詳細資訊，請參閱 [開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="0c798-306">For more details, see [Get Started with Azure Blob storage](storage-dotnet-how-to-use-blobs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0c798-307">使用用戶端加密進行加密的 blob 存放區與 hello blob 儲存的加密相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0c798-307">Blobs encrypted using client-side encryption store encryption-related metadata stored with hello blob.</span></span> <span data-ttu-id="0c798-308">是關鍵的 hello blob 中繼資料，而且特別是 hello 加密相關中繼資料，會保留，應該確保任何複製機制。</span><span class="sxs-lookup"><span data-stu-id="0c798-308">It is absolutely critical that any copy mechanism should ensure that hello blob metadata, and especially hello encryption-related metadata, is preserved.</span></span> <span data-ttu-id="0c798-309">如果您複製 hello blob，如果沒有這個中繼資料，hello blob 內容將無法擷取一次。</span><span class="sxs-lookup"><span data-stu-id="0c798-309">If you copy hello blobs without this metadata, hello blob content will not be retrievable again.</span></span> <span data-ttu-id="0c798-310">如需有關加密相關中繼資料的詳細資訊，請參閱 [Azure 儲存體用戶端加密](storage-client-side-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="0c798-310">For more details regarding encryption-related metadata, see [Azure Storage Client-Side Encryption](storage-client-side-encryption.md).</span></span>
> 
> 

## <a name="faqs"></a><span data-ttu-id="0c798-311">常見問題集</span><span class="sxs-lookup"><span data-stu-id="0c798-311">FAQs</span></span>
1. <span data-ttu-id="0c798-312">**現有的儲存體帳戶是否仍然可用？**</span><span class="sxs-lookup"><span data-stu-id="0c798-312">**Are existing storage accounts still available?**</span></span>
   
    <span data-ttu-id="0c798-313">是，現有的儲存體帳戶仍然可用，且價格或功能不變。</span><span class="sxs-lookup"><span data-stu-id="0c798-313">Yes, existing storage accounts are still available and are unchanged in pricing or functionality.</span></span>  <span data-ttu-id="0c798-314">它們並沒有 hello 能力 toochoose 儲存層，將不會在未來的 hello 擁有階層處理功能。</span><span class="sxs-lookup"><span data-stu-id="0c798-314">They do not have hello ability toochoose a storage tier and will not have tiering capabilities in hello future.</span></span>
2. <span data-ttu-id="0c798-315">**為何和何時應該開始使用 Blob 儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="0c798-315">**Why and when should I start using Blob storage accounts?**</span></span>
   
    <span data-ttu-id="0c798-316">Blob 儲存體帳戶專門用來儲存 blob，並讓我們 toointroduce 新 blob 為中心的功能。</span><span class="sxs-lookup"><span data-stu-id="0c798-316">Blob storage accounts are specialized for storing blobs and allow us toointroduce new blob-centric features.</span></span> <span data-ttu-id="0c798-317">從現在開始，Blob 儲存體帳戶，會根據此帳戶類型會引進 hello 建議的方式將 blob 儲存為未來的功能，例如階層式儲存體階層處理。</span><span class="sxs-lookup"><span data-stu-id="0c798-317">Going forward, Blob storage accounts are hello recommended way for storing blobs, as future capabilities such as hierarchical storage and tiering will be introduced based on this account type.</span></span> <span data-ttu-id="0c798-318">不過，它已啟動 tooyou 當您想要 toomigrate 根據您的業務需求。</span><span class="sxs-lookup"><span data-stu-id="0c798-318">However, it is up tooyou when you would like toomigrate based on your business requirements.</span></span>
3. <span data-ttu-id="0c798-319">**可以將轉換我現有的儲存體帳戶 tooa Blob 儲存體帳戶嗎？**</span><span class="sxs-lookup"><span data-stu-id="0c798-319">**Can I convert my existing storage account tooa Blob storage account?**</span></span>
   
    <span data-ttu-id="0c798-320">否。</span><span class="sxs-lookup"><span data-stu-id="0c798-320">No.</span></span> <span data-ttu-id="0c798-321">Blob 儲存體帳戶是不同類型的儲存體帳戶，您將需要 toocreate 新它與以上所述，將資料移轉。</span><span class="sxs-lookup"><span data-stu-id="0c798-321">Blob storage account is a different kind of storage account and you will need toocreate it new and migrate your data as explained above.</span></span>
4. <span data-ttu-id="0c798-322">**可以儲存物件 hello 中這兩個儲存層中相同的帳戶嗎？**</span><span class="sxs-lookup"><span data-stu-id="0c798-322">**Can I store objects in both storage tiers in hello same account?**</span></span>
   
    <span data-ttu-id="0c798-323">hello *'存取層'*屬性表示 hello 儲存層會在帳戶層級設定，並套用 tooall 物件，該帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="0c798-323">hello *'Access Tier'* attribute which indicates hello storage tier is set at an account level and applies tooall objects in that account.</span></span> <span data-ttu-id="0c798-324">您無法在物件層級設定 hello 存取層的屬性。</span><span class="sxs-lookup"><span data-stu-id="0c798-324">You cannot set hello access tier attribute at an object level.</span></span>
5. <span data-ttu-id="0c798-325">**可以變更 hello 儲存層的 我的 Blob 儲存體帳戶嗎？**</span><span class="sxs-lookup"><span data-stu-id="0c798-325">**Can I change hello storage tier of my Blob storage account?**</span></span>
   
    <span data-ttu-id="0c798-326">是。</span><span class="sxs-lookup"><span data-stu-id="0c798-326">Yes.</span></span> <span data-ttu-id="0c798-327">您將會無法 toochange hello 儲存層所設定的 hello *'存取層'* hello 儲存體帳戶上的屬性。</span><span class="sxs-lookup"><span data-stu-id="0c798-327">You will be able toochange hello storage tier by setting hello *'Access Tier'* attribute on hello storage account.</span></span> <span data-ttu-id="0c798-328">變更 hello 儲存層將會套用 tooall hello 帳戶中所儲存的物件。</span><span class="sxs-lookup"><span data-stu-id="0c798-328">Changing hello storage tier will apply tooall objects stored in hello account.</span></span> <span data-ttu-id="0c798-329">從熱 toocool 變更 hello 儲存層將不會產生任何費用，而從 cool toohot 變更將會產生每次讀取 hello 帳戶中的所有 hello 資料 GB 成本。</span><span class="sxs-lookup"><span data-stu-id="0c798-329">Change hello storage tier from hot toocool will not incur any charges, while changing from cool toohot will incur a per GB cost for reading all hello data in hello account.</span></span>
6. <span data-ttu-id="0c798-330">**頻率可以變更 hello 儲存層的 我的 Blob 儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="0c798-330">**How frequently can I change hello storage tier of my Blob storage account?**</span></span>
   
    <span data-ttu-id="0c798-331">雖然我們不會強制執行限制 hello 儲存層可以變更的頻率，請留意從 cool toohot 變更 hello 儲存層會產生明顯的費用。</span><span class="sxs-lookup"><span data-stu-id="0c798-331">While we do not enforce a limitation on how frequently hello storage tier can be changed, please be aware that changing hello storage tier from cool toohot will incur significant charges.</span></span> <span data-ttu-id="0c798-332">我們不建議您經常變更 hello 儲存層。</span><span class="sxs-lookup"><span data-stu-id="0c798-332">We do not recommend changing hello storage tier frequently.</span></span>
7. <span data-ttu-id="0c798-333">**Hello 酷炫的儲存層中的 hello blob 的行為會有所不同比 hello 的 hello 熱儲存層中？**</span><span class="sxs-lookup"><span data-stu-id="0c798-333">**Will hello blobs in hello cool storage tier behave differently than hello ones in hello hot storage tier?**</span></span>
   
    <span data-ttu-id="0c798-334">Hello 熱儲存層中的 blob 擁有 hello 相同延遲為一般用途儲存體帳戶中的 blob。</span><span class="sxs-lookup"><span data-stu-id="0c798-334">Blobs in hello hot storage tier have hello same latency as blobs in general-purpose storage accounts.</span></span> <span data-ttu-id="0c798-335">Hello 酷炫的儲存層中的 blob 的一般用途儲存體帳戶中有以 blob 形式類似延遲 （以毫秒為單位）。</span><span class="sxs-lookup"><span data-stu-id="0c798-335">Blobs in hello cool storage tier have a similar latency (in milliseconds) as blobs in general-purpose storage accounts.</span></span>
   
    <span data-ttu-id="0c798-336">Hello 酷炫的儲存層中的 blob 會比有較稍低可用性服務等級 (SLA) 儲存在 hello 熱儲存層中的 hello blob。</span><span class="sxs-lookup"><span data-stu-id="0c798-336">Blobs in hello cool storage tier will have a slightly lower availability service level (SLA) than hello blobs stored in hello hot storage tier.</span></span> <span data-ttu-id="0c798-337">如需詳細資訊，請參閱 [儲存體的 SLA](https://azure.microsoft.com/support/legal/sla/storage)。</span><span class="sxs-lookup"><span data-stu-id="0c798-337">For more details, see [SLA for storage](https://azure.microsoft.com/support/legal/sla/storage).</span></span>
8. <span data-ttu-id="0c798-338">**可以將分頁 Blob 和虛擬機器磁碟儲存在 Blob 儲存體帳戶嗎？**</span><span class="sxs-lookup"><span data-stu-id="0c798-338">**Can I store page blobs and virtual machine disks in Blob storage accounts?**</span></span>
   
    <span data-ttu-id="0c798-339">Blob 儲存體帳戶僅支援區塊和附加 Blob，不支援分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="0c798-339">Blob storage accounts support only block and append blobs, and not page blobs.</span></span> <span data-ttu-id="0c798-340">Azure 虛擬機器磁碟都由分頁 blob，因此 Blob 儲存體帳戶不能使用的 toostore 虛擬機器磁碟。</span><span class="sxs-lookup"><span data-stu-id="0c798-340">Azure virtual machine disks are backed by page blobs and as a result Blob storage accounts cannot be used toostore virtual machine disks.</span></span> <span data-ttu-id="0c798-341">不過它是區塊 blob，Blob 儲存體帳戶中的 hello 虛擬機器磁碟的可能 toostore 備份。</span><span class="sxs-lookup"><span data-stu-id="0c798-341">However it is possible toostore backups of hello virtual machine disks as block blobs in a Blob storage account.</span></span>
9. <span data-ttu-id="0c798-342">**我需要 toochange 我現有的應用程式 toouse Blob 儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="0c798-342">**Will I need toochange my existing applications toouse Blob storage accounts?**</span></span>
   
    <span data-ttu-id="0c798-343">對區塊和附加 Blob 而言，Blob 儲存體帳戶與一般用途儲存體帳戶的 API 完全一致。</span><span class="sxs-lookup"><span data-stu-id="0c798-343">Blob storage accounts are 100% API consistent with general-purpose storage accounts for block and append blobs.</span></span> <span data-ttu-id="0c798-344">只要您的應用程式是使用區塊 blob，或附加 blob，而您使用 hello 2014-02-14 版的 hello[儲存體服務 REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx)以上應用程式應該處理。</span><span class="sxs-lookup"><span data-stu-id="0c798-344">As long as your application is using block blobs or append blobs, and you are using hello 2014-02-14 version of hello [Storage Services REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) or greater your application should work.</span></span> <span data-ttu-id="0c798-345">如果您使用較舊版本的 hello 通訊協定，則您必須 tooupdate 您應用程式 toouse hello 新版本，以 toowork 順暢地搭配這兩種類型的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c798-345">If you are using an older version of hello protocol, then you will need tooupdate your application toouse hello new version so as toowork seamlessly with both types of storage accounts.</span></span> <span data-ttu-id="0c798-346">一般情況下，我們一律建議使用 hello 的儲存體帳戶類型不論您使用的最新版本。</span><span class="sxs-lookup"><span data-stu-id="0c798-346">In general, we always recommend using hello latest version regardless of which storage account type you use.</span></span>
10. <span data-ttu-id="0c798-347">**使用者經驗是否會有所改變？**</span><span class="sxs-lookup"><span data-stu-id="0c798-347">**Will there be a change in user experience?**</span></span>
    
    <span data-ttu-id="0c798-348">Blob 儲存體帳戶是用於儲存區塊的非常類似 tooa 一般用途儲存體帳戶和附加 blob，並支援所有的 hello 重要功能的 Azure 儲存體，包括高持久性和可用性、 延展性、 效能和安全性。</span><span class="sxs-lookup"><span data-stu-id="0c798-348">Blob storage accounts are very similar tooa general-purpose storage accounts for storing block and append blobs, and support all hello key features of Azure Storage, including high durability and availability, scalability, performance, and security.</span></span> <span data-ttu-id="0c798-349">Hello 功能和限制特定 tooBlob 儲存體帳戶和其上方的所有項目已提出的儲存層以外其他維持 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="0c798-349">Other than hello features and restrictions specific tooBlob storage accounts and its storage tiers that have been called out above, everything else remains hello same.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c798-350">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c798-350">Next steps</span></span>
### <a name="evaluate-blob-storage-accounts"></a><span data-ttu-id="0c798-351">評估 Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0c798-351">Evaluate Blob storage accounts</span></span>
[<span data-ttu-id="0c798-352">檢查各區域的 Blob 儲存體帳戶可用性</span><span class="sxs-lookup"><span data-stu-id="0c798-352">Check availability of Blob storage accounts by region</span></span>](https://azure.microsoft.com/regions/#services)

[<span data-ttu-id="0c798-353">啟用 Azure 儲存體計量以評估您目前的儲存體帳戶使用量</span><span class="sxs-lookup"><span data-stu-id="0c798-353">Evaluate usage of your current storage accounts by enabling Azure Storage metrics</span></span>](storage-enable-and-view-metrics.md)

[<span data-ttu-id="0c798-354">檢查各區域的 Blob 儲存體價格</span><span class="sxs-lookup"><span data-stu-id="0c798-354">Check Blob storage pricing by region</span></span>](https://azure.microsoft.com/pricing/details/storage/)

[<span data-ttu-id="0c798-355">檢查資料傳輸價格</span><span class="sxs-lookup"><span data-stu-id="0c798-355">Check data transfers pricing</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a><span data-ttu-id="0c798-356">開始使用 Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0c798-356">Start using Blob storage accounts</span></span>
[<span data-ttu-id="0c798-357">開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="0c798-357">Get Started with Azure Blob storage</span></span>](storage-dotnet-how-to-use-blobs.md)

[<span data-ttu-id="0c798-358">從 Azure 儲存體移動資料 tooand</span><span class="sxs-lookup"><span data-stu-id="0c798-358">Moving data tooand from Azure Storage</span></span>](storage-moving-data.md)

[<span data-ttu-id="0c798-359">使用 AzCopy 命令列公用程式的 hello 傳輸資料</span><span class="sxs-lookup"><span data-stu-id="0c798-359">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

[<span data-ttu-id="0c798-360">瀏覽及探索您的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0c798-360">Browse and explore your storage accounts</span></span>](http://storageexplorer.com/)

