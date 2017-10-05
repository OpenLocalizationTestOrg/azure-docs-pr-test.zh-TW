---
title: "Blob 的 Azure 非經常性存取儲存體 | Microsoft Docs"
description: "Azure Blob 儲存體的儲存層會根據存取模式，為物件資料提供具成本效益的儲存體。 非經常性存取儲存層已針對不常存取的資料最佳化。"
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
ms.openlocfilehash: 21e7b9c6a063b29a76043154a760fd9131425655
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-blob-storage-hot-and-cool-storage-tiers"></a><span data-ttu-id="c5fdb-104">Azure Blob 儲存體︰經常性存取與非經常性存取儲存層</span><span class="sxs-lookup"><span data-stu-id="c5fdb-104">Azure Blob Storage: Hot and cool storage tiers</span></span>
## <a name="overview"></a><span data-ttu-id="c5fdb-105">概觀</span><span class="sxs-lookup"><span data-stu-id="c5fdb-105">Overview</span></span>
<span data-ttu-id="c5fdb-106">Azure 儲存體會為 Blob 物件儲存體提供兩個儲存層，所以您可根據您的資料使用方式，以最符合成本效益的方式進行儲存。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-106">Azure Storage offers two storage tiers for Blob object storage so that you can store your data most cost-effectively depending on how you use it.</span></span> <span data-ttu-id="c5fdb-107">Azure **經常性存取儲存層** 已最佳化，可用於儲存經常存取的資料。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-107">The Azure **hot storage tier** is optimized for storing data that is accessed frequently.</span></span> <span data-ttu-id="c5fdb-108">Azure **非經常性存取儲存層** 已最佳化，可用於儲存不常存取且長期存留的資料。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-108">The Azure **cool storage tier** is optimized for storing data that is infrequently accessed and long-lived.</span></span> <span data-ttu-id="c5fdb-109">非經常性存取儲存層中的資料可容忍稍微較低的可用性，但仍要求高持久性以及與經常性存取資料類似的存取時間和輸送量特性。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-109">Data in the cool storage tier can tolerate slightly lower availability, but still requires high durability and similar time-to-access and throughput characteristics as hot data.</span></span> <span data-ttu-id="c5fdb-110">對於非經常性存取資料而言，稍微較低的可用性 SLA 和更高的存取成本是可接受的取捨，可讓儲存體成本降低許多。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-110">For cool data a slightly lower availability SLA and higher access costs are acceptable trade-offs for much lower storage costs.</span></span>

<span data-ttu-id="c5fdb-111">現今，儲存在雲端的資料迅速成長。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-111">Today, data stored in the cloud is growing at an exponential pace.</span></span> <span data-ttu-id="c5fdb-112">若要管理您不斷擴充的儲存體需求的成本，根據存取頻率和計劃性保留期來組織您的資料很有幫助。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-112">To manage costs for your expanding storage needs, it's helpful to organize your data based on attributes like frequency-of-access and planned retention period.</span></span> <span data-ttu-id="c5fdb-113">就資料在存留期內的產生、處理和存取方式而言，儲存在雲端的資料可能不同。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-113">Data stored in the cloud can be different in terms of how it is generated, processed, and accessed over its lifetime.</span></span> <span data-ttu-id="c5fdb-114">有些資料在其存留期內會積極地存取及修改。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-114">Some data is actively accessed and modified throughout its lifetime.</span></span> <span data-ttu-id="c5fdb-115">有些資料在其存留期的早期存取頻率很高，但存取頻率隨著資料老化而大幅下滑。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-115">Some data is accessed frequently early in its lifetime, with access dropping drastically as the data ages.</span></span> <span data-ttu-id="c5fdb-116">有些資料在雲端維持閒置，而且儲存後就很少存取。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-116">Some data remains idle in the cloud and is rarely, if ever, accessed once stored.</span></span>

<span data-ttu-id="c5fdb-117">上述每個資料存取案例均受惠於針對特定存取模式最佳化的差異化儲存層。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-117">Each of these data access scenarios described above benefits from a differentiated tier of storage that is optimized for a particular access pattern.</span></span> <span data-ttu-id="c5fdb-118">隨著經常性存取與非經常性存取儲存層的引進，Azure Blob 儲存體現可透過各種價格模式，滿足差異化儲存層的這項需求。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-118">With the introduction of hot and cool storage tiers, Azure Blob storage now addresses this need for differentiated storage tiers with separate pricing models.</span></span>

## <a name="blob-storage-accounts"></a><span data-ttu-id="c5fdb-119">Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c5fdb-119">Blob storage accounts</span></span>
<span data-ttu-id="c5fdb-120">**Blob 儲存體帳戶** 是特殊的儲存體帳戶，可將非結構化資料儲存為 Azure 儲存體中的 Blob (物件)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-120">**Blob storage accounts** are specialized storage accounts for storing your unstructured data as blobs (objects) in Azure Storage.</span></span> <span data-ttu-id="c5fdb-121">使用 Blob 儲存體帳戶，您現在可以在經常性存取和非經常性存取儲存層之間做選擇，以較低的儲存體成本來儲存較不常存取的非經常性存取資料，而以較低的存取成本來儲存較常存取的經常性存取資料。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-121">With Blob storage accounts, you can now choose between hot and cool storage tiers to store your less frequently accessed cool data at a lower storage cost, and store more frequently accessed hot data at a lower access cost.</span></span> <span data-ttu-id="c5fdb-122">Blob 儲存體帳戶類似於現有的一般用途儲存體帳戶，可共用所有強大的持續性、可用性、延展性以及您現今使用的效能功能，包括區塊 Blob 和附加 Blob 的 100% API 一致性。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-122">Blob storage accounts are similar to your existing general-purpose storage accounts and share all the great durability, availability, scalability, and performance features that you use today, including 100% API consistency for block blobs and append blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="c5fdb-123">Blob 儲存體帳戶僅支援區塊和附加 Blob，不支援分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-123">Blob storage accounts support only block and append blobs, and not page blobs.</span></span>
> 
> 

<span data-ttu-id="c5fdb-124">Blob 儲存體帳戶會公開 [存取層] 屬性，以便您根據儲存在帳戶中的資料，將儲存層指定為 [經常性存取] 或 [非經常性存取]。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-124">Blob storage accounts expose the **Access Tier** attribute, which allows you to specify the storage tier as **Hot** or **Cool** depending on the data stored in the account.</span></span> <span data-ttu-id="c5fdb-125">如果您的資料使用模式有變動，您也可以隨時在這些儲存層之間切換。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-125">If there is a change in the usage pattern of your data, you can also switch between these storage tiers at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="c5fdb-126">變更儲存層可能會導致額外的費用。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-126">Changing the storage tier may result in additional charges.</span></span> <span data-ttu-id="c5fdb-127">如需詳細資訊，請參閱 [價格和計費](storage-blob-storage-tiers.md#pricing-and-billing) 一節。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-127">Please see the [Pricing and Billing](storage-blob-storage-tiers.md#pricing-and-billing) section for more details.</span></span>
> 
> 

<span data-ttu-id="c5fdb-128">經常性存取儲存層的使用案例範例包括︰</span><span class="sxs-lookup"><span data-stu-id="c5fdb-128">Example usage scenarios for the hot storage tier include:</span></span>

* <span data-ttu-id="c5fdb-129">使用中或預期會經常存取 (讀取和寫入) 的資料。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-129">Data that is in active use or expected to be accessed (read from and written to) frequently.</span></span>
* <span data-ttu-id="c5fdb-130">資料會預備好進行處理且最終移轉至非經常性存取儲存層。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-130">Data that is staged for processing and eventual migration to the cool storage tier.</span></span>

<span data-ttu-id="c5fdb-131">非經常性存取儲存層的使用案例範例包括︰</span><span class="sxs-lookup"><span data-stu-id="c5fdb-131">Example usage scenarios for the cool storage tier include:</span></span>

* <span data-ttu-id="c5fdb-132">備份、封存和災害復原資料集。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-132">Backup, archival and disaster recovery datasets.</span></span>
* <span data-ttu-id="c5fdb-133">不再經常檢視，但存取時應立即可用的較舊媒體內容。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-133">Older media content not viewed frequently anymore but is expected to be available immediately when accessed.</span></span>
* <span data-ttu-id="c5fdb-134">當收集較多資料以供未來處理時，需要以符合成本效益方式預存的大型資料集。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-134">Large data sets that need to be stored cost effectively while more data is being gathered for future processing.</span></span> <span data-ttu-id="c5fdb-135">(例如，科學資料、來自製造工廠的原始遙測資料等長期儲存)</span><span class="sxs-lookup"><span data-stu-id="c5fdb-135">(*e.g.*, long-term storage of scientific data, raw telemetry data from a manufacturing facility)</span></span>
* <span data-ttu-id="c5fdb-136">即使已處理成最終可用格式，但還是需要保存的原始資料。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-136">Original (raw) data that must be preserved, even after it has been processed into final usable form.</span></span> <span data-ttu-id="c5fdb-137">(例如，轉碼成其他格式之後的原始媒體檔案)</span><span class="sxs-lookup"><span data-stu-id="c5fdb-137">(*e.g.*, Raw media files after transcoding into other formats)</span></span>
* <span data-ttu-id="c5fdb-138">需要儲存一段時間且幾乎不曾存取的相容性和封存資料。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-138">Compliance and archival data that needs to be stored for a long time and is hardly ever accessed.</span></span> <span data-ttu-id="c5fdb-139">(例如，保全攝影機錄影畫面、醫療機構的舊 X 光/MRI、金融服務的客服電話錄音和文字記錄)</span><span class="sxs-lookup"><span data-stu-id="c5fdb-139">(*e.g.*, Security camera footage, old X-Rays/MRIs for healthcare organizations, audio recordings and transcripts of customer calls for financial services)</span></span>

<span data-ttu-id="c5fdb-140">如需儲存體帳戶的詳細資訊，請參閱 [關於 Azure 儲存體帳戶](storage-create-storage-account.md) 。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-140">See [About Azure storage accounts](storage-create-storage-account.md) for more information on storage accounts.</span></span>

<span data-ttu-id="c5fdb-141">對於只需要封鎖或附加 Blob 儲存體的應用程式，我們建議使用 Blob 儲存體帳戶，以充分利用分層式儲存的差異化價格模型。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-141">For applications requiring only block or append blob storage, we recommend using Blob storage accounts, to take advantage of the differentiated pricing model of tiered storage.</span></span> <span data-ttu-id="c5fdb-142">但是，我們了解在某些情況下這可能不可行，因為使用一般用途的儲存體帳戶是最好的選擇，例如︰</span><span class="sxs-lookup"><span data-stu-id="c5fdb-142">However, we understand this might not be possible under certain circumstances where using general-purpose storage accounts would be the way to go, such as:</span></span>

* <span data-ttu-id="c5fdb-143">您需要使用資料表、佇列或檔案，並希望 Blob 儲存在相同的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-143">You need to use tables, queues, or files and want your blobs stored in the same storage account.</span></span> <span data-ttu-id="c5fdb-144">請注意，將這些 Blob 儲存在相同的帳戶，而非擁有相同的共用金鑰。並沒有任何技術優勢</span><span class="sxs-lookup"><span data-stu-id="c5fdb-144">Note that there is no technical advantage to storing these in the same account other than having the same shared keys.</span></span>
* <span data-ttu-id="c5fdb-145">您仍然需要使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-145">You still need to use the Classic deployment model.</span></span> <span data-ttu-id="c5fdb-146">僅可透過 Azure Resource Manager 部署模型取得 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-146">Blob storage accounts are only available via the Azure Resource Manager deployment model.</span></span>
* <span data-ttu-id="c5fdb-147">您必須使用分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-147">You need to use page blobs.</span></span> <span data-ttu-id="c5fdb-148">Blob 儲存體帳戶不支援分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-148">Blob storage accounts do not support page blobs.</span></span> <span data-ttu-id="c5fdb-149">我們通常建議使用區塊 Blob，除非您對分頁 Blob 有特定的需求。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-149">We generally recommend using block blobs unless you have a specific need for page blobs.</span></span>
* <span data-ttu-id="c5fdb-150">您使用早於 2014-02-14 的 [儲存體服務 REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) 版本，或版本低於 4.x 的用戶端程式庫，所以無法升級您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-150">You use a version of the [Storage Services REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) that is earlier than 2014-02-14 or a client library with a version lower than 4.x, and cannot upgrade your application.</span></span>

> [!NOTE]
> <span data-ttu-id="c5fdb-151">目前所有的 Azure 區域都支援 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-151">Blob storage accounts are currently supported in all Azure regions.</span></span>
> 
> 

## <a name="comparison-between-the-storage-tiers"></a><span data-ttu-id="c5fdb-152">儲存層之間的比較</span><span class="sxs-lookup"><span data-stu-id="c5fdb-152">Comparison between the storage tiers</span></span>
<span data-ttu-id="c5fdb-153">下表列出兩個儲存層之間的比較：</span><span class="sxs-lookup"><span data-stu-id="c5fdb-153">The following table highlights the comparison between the two storage tiers:</span></span>

<table border="1" cellspacing="0" cellpadding="0" style="border: 1px solid #000000;">
<col width="250">
<col width="250">
<col width="250">
<tbody>
<tr>
    <td><strong><center></center></strong></td>
    <td><span data-ttu-id="c5fdb-154"><strong><center>經常性存取儲存層</center></strong></span><span class="sxs-lookup"><span data-stu-id="c5fdb-154"><strong><center>Hot storage tier</center></strong></span></span></td>
    <td><span data-ttu-id="c5fdb-155"><strong><center>非經常性存取儲存層</center></strong></span><span class="sxs-lookup"><span data-stu-id="c5fdb-155"><strong><center>Cool storage tier</center></strong></span></span></td
</tr>
<tr>
    <td><span data-ttu-id="c5fdb-156"><strong><center>可用性</center></strong></span><span class="sxs-lookup"><span data-stu-id="c5fdb-156"><strong><center>Availability</center></strong></span></span></td>
    <td><span data-ttu-id="c5fdb-157"><center>99.9%</center></span><span class="sxs-lookup"><span data-stu-id="c5fdb-157"><center>99.9%</center></span></span></td>
    <td><span data-ttu-id="c5fdb-158"><center>99%</center></span><span class="sxs-lookup"><span data-stu-id="c5fdb-158"><center>99%</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="c5fdb-159"><strong><center>可用性</span><span class="sxs-lookup"><span data-stu-id="c5fdb-159"><strong><center>Availability</span></span><br><span data-ttu-id="c5fdb-160">(RA-GRS 讀取)</center></strong></span><span class="sxs-lookup"><span data-stu-id="c5fdb-160">(RA-GRS reads)</center></strong></span></span></td>
    <td><span data-ttu-id="c5fdb-161"><center>99.99%</center></span><span class="sxs-lookup"><span data-stu-id="c5fdb-161"><center>99.99%</center></span></span></td>
    <td><span data-ttu-id="c5fdb-162"><center>99.9%</center></span><span class="sxs-lookup"><span data-stu-id="c5fdb-162"><center>99.9%</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="c5fdb-163"><strong><center>使用費用</center></strong></span><span class="sxs-lookup"><span data-stu-id="c5fdb-163"><strong><center>Usage charges</center></strong></span></span></td>
    <td><span data-ttu-id="c5fdb-164"><center>儲存成本較高</span><span class="sxs-lookup"><span data-stu-id="c5fdb-164"><center>Higher storage costs</span></span><br><span data-ttu-id="c5fdb-165">存取和交易成本較低</center></span><span class="sxs-lookup"><span data-stu-id="c5fdb-165">Lower access and transaction costs</center></span></span></td>
    <td><span data-ttu-id="c5fdb-166"><center>儲存成本較低</span><span class="sxs-lookup"><span data-stu-id="c5fdb-166"><center>Lower storage costs</span></span><br><span data-ttu-id="c5fdb-167">存取和交易成本較高</center></span><span class="sxs-lookup"><span data-stu-id="c5fdb-167">Higher access and transaction costs</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="c5fdb-168"><strong><center>最小物件大小<center></strong></span><span class="sxs-lookup"><span data-stu-id="c5fdb-168"><strong><center>Minimum object size<center></strong></span></span></td>
    <td colspan="2"><span data-ttu-id="c5fdb-169"><center>N/A</center></span><span class="sxs-lookup"><span data-stu-id="c5fdb-169"><center>N/A</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="c5fdb-170"><strong><center>最小儲存持續時間<center></strong></span><span class="sxs-lookup"><span data-stu-id="c5fdb-170"><strong><center>Minimum storage duration<center></strong></span></span></td>
    <td colspan="2"><span data-ttu-id="c5fdb-171"><center>N/A</center></span><span class="sxs-lookup"><span data-stu-id="c5fdb-171"><center>N/A</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="c5fdb-172"><strong><center>延遲</span><span class="sxs-lookup"><span data-stu-id="c5fdb-172"><strong><center>Latency</span></span><br><span data-ttu-id="c5fdb-173">(距第一位元組時間)<center></strong></span><span class="sxs-lookup"><span data-stu-id="c5fdb-173">(Time to first byte)<center></strong></span></span></td>
    <td colspan="2"><span data-ttu-id="c5fdb-174"><center>毫秒</center></span><span class="sxs-lookup"><span data-stu-id="c5fdb-174"><center>milliseconds</center></span></span></td>
</tr>
<tr>
    <td><span data-ttu-id="c5fdb-175"><strong><center>延展性和效能目標<center></strong></span><span class="sxs-lookup"><span data-stu-id="c5fdb-175"><strong><center>Scalability and performance targets<center></strong></span></span></td>
    <td colspan="2"><span data-ttu-id="c5fdb-176"><center>與一般用途儲存體帳戶相同</center></span><span class="sxs-lookup"><span data-stu-id="c5fdb-176"><center>Same as general-purpose storage accounts</center></span></span></td>
</tr>
</tbody>
</table>

> [!NOTE]
> <span data-ttu-id="c5fdb-177">Blob 儲存體帳戶支援與一般用途儲存體帳戶相同的效能和延展性目標。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-177">Blob storage accounts support the same performance and scalability targets as general-purpose storage accounts.</span></span> <span data-ttu-id="c5fdb-178">如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md) (英文)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-178">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for more information.</span></span>
> 
> 

## <a name="pricing-and-billing"></a><span data-ttu-id="c5fdb-179">價格和計費</span><span class="sxs-lookup"><span data-stu-id="c5fdb-179">Pricing and Billing</span></span>
<span data-ttu-id="c5fdb-180">Blob 儲存體帳戶會對以儲存層基礎的 Blob 儲存體使用新的價格模型。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-180">Blob storage accounts use a new pricing model for blob storage based on the storage tier.</span></span> <span data-ttu-id="c5fdb-181">使用 Blob 儲存體帳戶時，需考量下列計費資訊：</span><span class="sxs-lookup"><span data-stu-id="c5fdb-181">When using a Blob storage account, the following billing considerations apply:</span></span>

* <span data-ttu-id="c5fdb-182">**儲存體成本**︰除了儲存的資料量以外，儲存資料的成本會因儲存層而異。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-182">**Storage costs**: In addition to the amount of data stored, the cost of storing data varies depending on the storage tier.</span></span> <span data-ttu-id="c5fdb-183">非經常性存取儲存層的每 GB 成本低於經常性存取儲存層的每 GB 成本低。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-183">The per-gigabyte cost is lower for the cool storage tier than for the hot storage tier.</span></span>
* <span data-ttu-id="c5fdb-184">**資料存取成本**︰對於非經常性存取儲存層中的資料，您將支付讀取和寫入的每 GB 資料存取費用。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-184">**Data access costs**: For data in the cool storage tier, you will be charged a per-gigabyte data access charge for reads and writes.</span></span>
* <span data-ttu-id="c5fdb-185">**交易成本**︰這兩層都有每筆交易的費用。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-185">**Transaction costs**: There is a per-transaction charge for both tiers.</span></span> <span data-ttu-id="c5fdb-186">不過，非經常性存取儲存層的每筆交易成本高於經常性存取儲存層的每筆交易成本。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-186">However, the per-transaction cost for the cool storage tier is higher than that for the hot storage tier.</span></span>
* <span data-ttu-id="c5fdb-187">**異地複寫資料傳輸成本**︰這只適用於已設定異地複寫的帳戶，包括 GRS 和 RA-GRS。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-187">**Geo-Replication data transfer costs**: This only applies to accounts with geo-replication configured, including GRS and RA-GRS.</span></span> <span data-ttu-id="c5fdb-188">異地複寫資料傳輸會產生每 GB 費用。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-188">Geo-replication data transfer incurs a per-gigabyte charge.</span></span>
* <span data-ttu-id="c5fdb-189">**輸出資料傳輸成本**︰輸出資料傳輸 (從 Azure 區域傳出的資料) 會產生每 GB 頻寬使用量費用，與一般用途的儲存體帳戶一致。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-189">**Outbound data transfer costs**: Outbound data transfers (data that is transferred out of an Azure region) incur billing for bandwidth usage on a per-gigabyte basis, consistent with general-purpose storage accounts.</span></span>
* <span data-ttu-id="c5fdb-190">**變更儲存層**︰將儲存層從非經常性存取變更為經常性存取時，每次轉換會產生等於讀取儲存體帳戶中所有資料的費用。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-190">**Changing the storage tier**: Changing the storage tier from cool to hot will incur a charge equal to reading all the data existing in the storage account for every transition.</span></span> <span data-ttu-id="c5fdb-191">相反地，將儲存層從經常存取變更為不常存取是免費的。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-191">On the other hand, changing the storage tier from hot to cool will be free of cost.</span></span>

> [!NOTE]
> <span data-ttu-id="c5fdb-192">為了讓使用者試用新的儲存層並驗證啟動後的功能，在 2016 年 6 月 30 日之前，將免除將儲存層從不常存取變更為經常存取的費用。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-192">In order to allow users to try out the new storage tiers and validate functionality post launch, the charge for changing the storage tier from cool to hot will be waived off until June 30th 2016.</span></span> <span data-ttu-id="c5fdb-193">從 2016 年 7 月 1 日起，費用將適用於從不常存取到經常存取的所有轉換。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-193">Starting July 1st 2016, the charge will be applied to all transitions from cool to hot.</span></span> <span data-ttu-id="c5fdb-194">如需 Blob 儲存體帳戶的價格模型詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/) 頁面。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-194">For more details on the pricing model for Blob storage accounts see, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/) page.</span></span> <span data-ttu-id="c5fdb-195">如需輸出資料傳輸費用的詳細資訊，請參閱 [資料傳輸價格詳細資料](https://azure.microsoft.com/pricing/details/data-transfers/) 頁面。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-195">For more details on the outbound data transfer charges see, [Data Transfers Pricing Details](https://azure.microsoft.com/pricing/details/data-transfers/) page.</span></span>
> 
> 

## <a name="quick-start"></a><span data-ttu-id="c5fdb-196">快速啟動</span><span class="sxs-lookup"><span data-stu-id="c5fdb-196">Quick Start</span></span>
<span data-ttu-id="c5fdb-197">在這一節中，我們將使用 Azure 入口網站示範下列案例︰</span><span class="sxs-lookup"><span data-stu-id="c5fdb-197">In this section we will demonstrate the following scenarios using the Azure portal:</span></span>

* <span data-ttu-id="c5fdb-198">如何建立 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-198">How to create a Blob storage account.</span></span>
* <span data-ttu-id="c5fdb-199">如何管理 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-199">How to manage a Blob storage account.</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="c5fdb-200">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c5fdb-200">Using the Azure portal</span></span>
#### <a name="create-a-blob-storage-account-using-the-azure-portal"></a><span data-ttu-id="c5fdb-201">使用 Azure 入口網站建立 Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c5fdb-201">Create a Blob storage account using the Azure portal</span></span>
1. <span data-ttu-id="c5fdb-202">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-202">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c5fdb-203">在 [中樞] 功能表上，選取 [新增] > [資料+儲存體] > [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-203">On the Hub menu, select **New** > **Data + Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="c5fdb-204">輸入儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-204">Enter a name for your storage account.</span></span>
   
    <span data-ttu-id="c5fdb-205">此名稱必須是全域唯一的；它會做為用來存取儲存體帳戶中物件之 URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-205">This name must be globally unique; it is used as part of the URL used to access the objects in the storage account.</span></span>  
4. <span data-ttu-id="c5fdb-206">選取 [Resource Manager]  做為部署模型。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-206">Select **Resource Manager** as the deployment model.</span></span>
   
    <span data-ttu-id="c5fdb-207">分層式儲存體僅適用於 Resource Manager 儲存體帳戶；這是新資源的建議部署模型。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-207">Tiered storage can only be used with Resource Manager storage accounts; this is the recommended deployment model for new resources.</span></span> <span data-ttu-id="c5fdb-208">如需詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-208">For more information, check out the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>  
5. <span data-ttu-id="c5fdb-209">在 [帳戶類型] 下拉式清單中，選取 [Blob 儲存體] 。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-209">In the Account Kind dropdown list, select **Blob Storage**.</span></span>
   
    <span data-ttu-id="c5fdb-210">這是您用來選取儲存體帳戶類型的地方。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-210">This is where you select the type of storage account.</span></span> <span data-ttu-id="c5fdb-211">分層式儲存體不適用於一般用途的儲存體；它僅適用於 Blob 儲存體類型帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-211">Tiered storage is not available in general-purpose storage; it is only available in the Blob storage type account.</span></span>     
   
    <span data-ttu-id="c5fdb-212">請注意，當您選取此選項，效能層會設定為「標準」。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-212">Note that when you select this, the performance tier is set to Standard.</span></span> <span data-ttu-id="c5fdb-213">分層式儲存體不適用於進階效能層。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-213">Tiered storage is not available with the Premium performance tier.</span></span>
6. <span data-ttu-id="c5fdb-214">選取儲存體帳戶的複寫選項︰[LRS]、[GRS] 或 [RA-GRS]。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-214">Select the replication option for the storage account: **LRS**, **GRS**, or **RA-GRS**.</span></span> <span data-ttu-id="c5fdb-215">預設值是 [RA-GRS] 。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-215">The default is **RA-GRS**.</span></span>
   
    <span data-ttu-id="c5fdb-216">LRS = 本地備援儲存體；GRS = 異地備援儲存體 (2 個區域)；RA-GRS 是讀取權限異地備援儲存體 (2 個區域，具有第二個區域的讀取權限)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-216">LRS = locally redundant storage; GRS = geo-redundant storage (2 regions); RA-GRS is read-access geo-redundant storage (2 regions with read access to the second).</span></span>
   
    <span data-ttu-id="c5fdb-217">如需 Azure 儲存體複寫選項的詳細資訊，請參閱 [Azure 儲存體複寫](storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-217">For more details on Azure Storage replication options, check out [Azure Storage replication](storage-redundancy.md).</span></span>
7. <span data-ttu-id="c5fdb-218">針對您的需求選取正確的儲存層︰將 [存取層] 設定為 [非經常性存取] 或 [經常性存取]。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-218">Select the right storage tier for your needs: Set the **Access tier** to either **Cool** or **Hot**.</span></span> <span data-ttu-id="c5fdb-219">預設值為 [經常存取] 。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-219">The default is **Hot**.</span></span>
8. <span data-ttu-id="c5fdb-220">選取您要在其中建立新儲存體帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-220">Select the subscription in which you want to create the new storage account.</span></span>
9. <span data-ttu-id="c5fdb-221">指定新的資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-221">Specify a new resource group or select an existing resource group.</span></span> <span data-ttu-id="c5fdb-222">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-222">For more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
10. <span data-ttu-id="c5fdb-223">選取儲存體帳戶的區域。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-223">Select the region for your storage account.</span></span>
11. <span data-ttu-id="c5fdb-224">按一下 [建立]  建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-224">Click **Create** to create the storage account.</span></span>

#### <a name="change-the-storage-tier-of-a-blob-storage-account-using-the-azure-portal"></a><span data-ttu-id="c5fdb-225">使用 Azure 入口網站變更 Blob 儲存體帳戶的儲存層</span><span class="sxs-lookup"><span data-stu-id="c5fdb-225">Change the storage tier of a Blob storage account using the Azure portal</span></span>
1. <span data-ttu-id="c5fdb-226">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-226">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c5fdb-227">瀏覽至儲存體帳戶、選取 [所有資源]，然後選取您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-227">To navigate to your storage account, select All Resources, then select your storage account.</span></span>
3. <span data-ttu-id="c5fdb-228">在 [設定] 刀鋒視窗中按一下 [組態]  ，以檢視和/或變更帳戶組態。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-228">In the Settings blade, click **Configuration** to view and/or change the account configuration.</span></span>
4. <span data-ttu-id="c5fdb-229">針對您的需求選取正確的儲存層︰將 [存取層] 設定為 [非經常性存取] 或 [經常性存取]。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-229">Select the right storage tier for your needs: Set the **Access tier** to either **Cool** or **Hot**.</span></span>
5. <span data-ttu-id="c5fdb-230">按一下刀鋒視窗頂端的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-230">Click Save at the top of the blade.</span></span>

> [!NOTE]
> <span data-ttu-id="c5fdb-231">變更儲存層可能會導致額外的費用。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-231">Changing the storage tier may result in additional charges.</span></span> <span data-ttu-id="c5fdb-232">如需詳細資訊，請參閱 [價格和計費](storage-blob-storage-tiers.md#pricing-and-billing) 一節。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-232">Please see the [Pricing and Billing](storage-blob-storage-tiers.md#pricing-and-billing) section for more details.</span></span>
> 
> 

## <a name="evaluating-and-migrating-to-blob-storage-accounts"></a><span data-ttu-id="c5fdb-233">評估及移轉至 Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c5fdb-233">Evaluating and migrating to Blob storage accounts</span></span>
<span data-ttu-id="c5fdb-234">這一節的目的是要協助使用者順利地轉換成使用 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-234">The purpose of this section is to help users to make a smooth transition to using Blob storage accounts.</span></span> <span data-ttu-id="c5fdb-235">有兩個使用者案例：</span><span class="sxs-lookup"><span data-stu-id="c5fdb-235">There are two user scenarios:</span></span>

* <span data-ttu-id="c5fdb-236">您有現有的一般用途儲存體帳戶，而且想要評估變更成具有正確儲存層的 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-236">You have an existing general-purpose storage account and want to evaluate a change to a Blob storage account with the right storage tier.</span></span>
* <span data-ttu-id="c5fdb-237">您已決定使用 Blob 儲存體帳戶，或已有一個帳戶並想要評估您應該使用經常性存取還是非經常性存取儲存層。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-237">You have decided to use a Blob storage account or already have one and want to evaluate whether you should use the hot or cool storage tier.</span></span>

<span data-ttu-id="c5fdb-238">在這兩種情況下，第一要務是估計儲存和存取在 Blob 儲存體帳戶中所儲存資料的成本，並與您目前的成本進行比較。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-238">In both cases, the first order of business is to estimate the cost of storing and accessing your data stored in a Blob storage account and compare that against your current costs.</span></span>

### <a name="evaluating-blob-storage-account-tiers"></a><span data-ttu-id="c5fdb-239">評估 Blob 儲存體帳戶層</span><span class="sxs-lookup"><span data-stu-id="c5fdb-239">Evaluating Blob storage account tiers</span></span>
<span data-ttu-id="c5fdb-240">若要估計儲存和存取在 Blob 儲存體帳戶中所儲存資料的成本，必須評估您現有的使用模式或接近您預期的使用模式。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-240">In order to estimate the cost of storing and accessing data stored in a Blob storage account, you will need to evaluate your existing usage pattern or approximate your expected usage pattern.</span></span> <span data-ttu-id="c5fdb-241">一般而言，您會想要知道︰</span><span class="sxs-lookup"><span data-stu-id="c5fdb-241">In general, you will want to know:</span></span>

* <span data-ttu-id="c5fdb-242">您的儲存體使用情況 – 目前儲存多少資料，以及每個月的變化情況為何？</span><span class="sxs-lookup"><span data-stu-id="c5fdb-242">Your storage consumption - How much data is being stored and how does this change on a monthly basis?</span></span>
* <span data-ttu-id="c5fdb-243">您的儲存體存取模式 – 有多少資料正從帳戶讀取和寫入其中 (包括新資料)？</span><span class="sxs-lookup"><span data-stu-id="c5fdb-243">Your storage access pattern - How much data is being read from and written to the account (including new data)?</span></span> <span data-ttu-id="c5fdb-244">有多少交易用於資料存取，而它們是何種交易？</span><span class="sxs-lookup"><span data-stu-id="c5fdb-244">How many transactions are used for data access, and what kinds of transactions are they?</span></span>

#### <a name="monitoring-existing-storage-accounts"></a><span data-ttu-id="c5fdb-245">監視現有的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c5fdb-245">Monitoring existing storage accounts</span></span>
<span data-ttu-id="c5fdb-246">若要監視現有的儲存體帳戶並收集此資料，您可以利用 Azure 儲存體分析來執行記錄及提供儲存體帳戶的度量資料。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-246">To monitor your existing storage accounts and gather this data, you can make use of Azure Storage Analytics which performs logging and provides metrics data for a storage account.</span></span>
<span data-ttu-id="c5fdb-247">儲存體分析可以針對一般用途儲存體帳戶和 Blob 儲存體帳戶，儲存包含與 Blob 儲存體服務要求相關之彙總交易統計資料和容量資料的度量。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-247">Storage Analytics can store metrics that include aggregated transaction statistics and capacity data about requests to the Blob storage service for both general-purpose storage accounts as well as Blob storage accounts.</span></span>
<span data-ttu-id="c5fdb-248">此資料會儲存在相同儲存體帳戶的已知資料表中。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-248">This data is stored in well-known tables in the same storage account.</span></span>

<span data-ttu-id="c5fdb-249">如需詳細資訊，請參閱[關於儲存體分析度量](https://msdn.microsoft.com/library/azure/hh343258.aspx)和[儲存體分析度量資料表結構描述](https://msdn.microsoft.com/library/azure/hh343264.aspx)</span><span class="sxs-lookup"><span data-stu-id="c5fdb-249">For more details, please see [About Storage Analytics Metrics](https://msdn.microsoft.com/library/azure/hh343258.aspx) and [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="c5fdb-250">Blob 儲存體帳戶會公開僅適用於儲存和存取該帳戶度量資料的表格服務端點。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-250">Blob storage accounts expose the table service endpoint only for storing and accessing the metrics data for that account.</span></span>
> 
> 

<span data-ttu-id="c5fdb-251">若要監視 Blob 儲存體服務的儲存體使用情況，您必須啟用容量度量。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-251">To monitor the storage consumption for the Blob storage service, you will need to enable the capacity metrics.</span></span>
<span data-ttu-id="c5fdb-252">啟用此度量後，系統會每日記錄儲存體帳戶的 Blob 服務容量資料，而該資料會以資料表項目形式記錄並寫入至相同儲存體帳戶內的 $MetricsCapacityBlob  資料表。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-252">With this enabled, capacity data is recorded daily for a storage account's Blob service, and recorded as a table entry that is written to the *$MetricsCapacityBlob* table within the same storage account.</span></span>

<span data-ttu-id="c5fdb-253">若要監視 Blob 儲存體服務的資料存取模式，您必須在 API 層級啟用每小時交易度量。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-253">To monitor the data access pattern for the Blob storage service, you will need to enable the hourly transaction metrics at an API level.</span></span>
<span data-ttu-id="c5fdb-254">啟用此度量後，系統會每小時彙總每筆 API 交易，而該資料會以資料表項目形式記錄並寫入至相同儲存體帳戶內的 $MetricsHourPrimaryTransactionsBlob  資料表。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-254">With this enabled, per API transactions are aggregated every hour, and recorded as a table entry that is written to the *$MetricsHourPrimaryTransactionsBlob* table within the same storage account.</span></span> <span data-ttu-id="c5fdb-255">如果是 RA-GRS 儲存體帳戶，$MetricsHourSecondaryTransactionsBlob  資料表會將交易記錄至次要端點。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-255">The *$MetricsHourSecondaryTransactionsBlob* table records the transactions to the secondary endpoint in case of RA-GRS storage accounts.</span></span>

> [!NOTE]
> <span data-ttu-id="c5fdb-256">如果您已有一般用途的儲存體帳戶，並在中儲存分頁 blob 和虛擬機器磁碟以及區塊和附加 blob 資料，就不適用此估計程序。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-256">In case you have a general-purpose storage account in which you have stored page blobs and virtual machine disks alongside block and append blob data, this estimation process is not applicable.</span></span> <span data-ttu-id="c5fdb-257">這是因為您無法只根據針對可移轉至 Blob 儲存體帳戶之區塊和附加 blob 的 blob 類型，區分容量和交易度量。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-257">This is because you will have no way of distinguishing capacity and transaction metrics based on the type of blob for only block and append blobs which can be migrated to a Blob storage account.</span></span>
> 
> 

<span data-ttu-id="c5fdb-258">若要取得資料使用和存取模式的適當近似值，建議您針對代表一般使用情況的度量選擇保留期，並進行推斷。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-258">To get a good approximation of your data consumption and access pattern, we recommend you choose a retention period for the metrics that is representative of your regular usage, and extrapolate.</span></span>
<span data-ttu-id="c5fdb-259">其中一個選項是保留度量資料 7 天並每週收集資料，以便月底進行分析。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-259">One option is to retain the metrics data for 7 days and collect the data every week, for analysis at the end of the month.</span></span>
<span data-ttu-id="c5fdb-260">另一個選項是保留最近 30 天的度量資料，並在 30 天期間的結尾收集和分析資料。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-260">Another option is to retain the metrics data for the last 30 days and collect and analyze the data at the end of the 30-day period.</span></span>

<span data-ttu-id="c5fdb-261">如需啟用、收集和檢視度量資料的詳細資訊，請參閱 [啟用 Azure 儲存體度量和檢視度量資料](storage-enable-and-view-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-261">For details on enabling, collecting and viewing metrics data, please see, [Enabling Azure Storage metrics and viewing metrics data](storage-enable-and-view-metrics.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c5fdb-262">就如同一般使用者資料，儲存、存取和下載分析資料也需付費。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-262">Storing, accessing and downloading analytics data is also charged just like regular user data.</span></span>
> 
> 

#### <a name="utilizing-usage-metrics-to-estimate-costs"></a><span data-ttu-id="c5fdb-263">利用使用度量來估計成本</span><span class="sxs-lookup"><span data-stu-id="c5fdb-263">Utilizing usage metrics to estimate costs</span></span>
##### <a name="storage-costs"></a><span data-ttu-id="c5fdb-264">儲存成本</span><span class="sxs-lookup"><span data-stu-id="c5fdb-264">Storage costs</span></span>
<span data-ttu-id="c5fdb-265">容量度量資料表 $MetricsCapacityBlob 中具有資料列索引鍵 'data' 的最新項目會顯示使用者資料所耗用的儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-265">The latest entry in the capacity metrics table *$MetricsCapacityBlob* with the row key *'data'* shows the storage capacity consumed by user data.</span></span>
<span data-ttu-id="c5fdb-266">容量度量資料表 $MetricsCapacityBlob 中具有資料列索引鍵 'analytics' 的最新項目會顯示分析記錄檔所耗用的儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-266">The latest entry in the capacity metrics table *$MetricsCapacityBlob* with the row key *'analytics'* shows the storage capacity consumed by the analytics logs.</span></span>

<span data-ttu-id="c5fdb-267">使用者資料和分析記錄檔 (若已啟用) 所耗用的總容量便可用來估計在儲存體帳戶中儲存資料的成本。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-267">This total capacity consumed by both user data and analytics logs (if enabled) can then be used to estimate the cost of storing data in the storage account.</span></span>
<span data-ttu-id="c5fdb-268">相同的方法也可用來估計一般用途儲存體帳戶中區塊和附加 blob 的儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-268">The same method can also be used for estimating storage costs for block and append blobs in general-purpose storage accounts.</span></span>

##### <a name="transaction-costs"></a><span data-ttu-id="c5fdb-269">交易成本</span><span class="sxs-lookup"><span data-stu-id="c5fdb-269">Transaction costs</span></span>
<span data-ttu-id="c5fdb-270">交易度量資料表中 API 的所有項目的 'TotalBillableRequests' 總和，會指出該特定 API 的交易總數。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-270">The sum of *'TotalBillableRequests'*, across all entries for an API in the transaction metrics table indicates the total number of transactions for that particular API.</span></span> <span data-ttu-id="c5fdb-271">例如，在給定期間的 'GetBlob' 交易總數計算方式為將所有包含 'user;GetBlob'列索引鍵的可計費要求總數進行加總。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-271">*e.g.*, the total number of *'GetBlob'* transactions in a given period can be calculated by the sum of total billable requests for all entries with the row key *'user;GetBlob'*.</span></span>

<span data-ttu-id="c5fdb-272">若要估計 Blob 儲存體帳戶的交易成本，您必須將交易細分成三個群組，因為它們的定價方式不同。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-272">In order to estimate transaction costs for Blob storage accounts, you will need to break down the transactions into three groups since they are priced differently.</span></span>

* <span data-ttu-id="c5fdb-273">寫入 'PutBlob'、'PutBlock'、'PutBlockList'、'AppendBlock'、'ListBlobs'、'ListContainers'、'CreateContainer'、'SnapshotBlob' 和 'CopyBlob' 等交易。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-273">Write transactions such as *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'*, and *'CopyBlob'*.</span></span>
* <span data-ttu-id="c5fdb-274">刪除 'DeleteBlob' 和 'DeleteContainer' 等交易。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-274">Delete transactions such as *'DeleteBlob'* and *'DeleteContainer'*.</span></span>
* <span data-ttu-id="c5fdb-275">所有其他交易</span><span class="sxs-lookup"><span data-stu-id="c5fdb-275">All other transactions.</span></span>

<span data-ttu-id="c5fdb-276">若要估計一般用途儲存體帳戶的交易成本，不論作業/API 為何，您必須彙總所有的交易。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-276">In order to estimate transaction costs for general-purpose storage accounts, you need to aggregate all transactions irrespective of the operation/API.</span></span>

##### <a name="data-access-and-geo-replication-data-transfer-costs"></a><span data-ttu-id="c5fdb-277">資料存取和異地複寫資料傳輸費用</span><span class="sxs-lookup"><span data-stu-id="c5fdb-277">Data access and geo-replication data transfer costs</span></span>
<span data-ttu-id="c5fdb-278">雖然儲存體分析不會提供讀取自和寫入至儲存體帳戶的資料量，但可藉由查看交易度量資料表大致估算。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-278">While storage analytics does not provide the amount of data read from and written to a storage account, it can be roughly estimated by looking at the transaction metrics table.</span></span>
<span data-ttu-id="c5fdb-279">交易度量資料表中 API 的所有項目的 'TotalIngress'  總和，會指出該特定 API 的輸入資料總量 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-279">The sum of *'TotalIngress'* across all entries for an API in the transaction metrics table indicates the total amount of ingress data in bytes for that particular API.</span></span>
<span data-ttu-id="c5fdb-280">同樣地，'TotalEgress'  的總和會指出輸出資料總數 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-280">Similarly the sum of *'TotalEgress'* indicates the total amount of egress data, in bytes.</span></span>

<span data-ttu-id="c5fdb-281">若要估計 Blob 儲存體帳戶的資料存取成本，您必須將交易細分成兩個群組。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-281">In order to estimate the data access costs for Blob storage accounts, you will need to break down the transactions into two groups.</span></span>

* <span data-ttu-id="c5fdb-282">查看主要 'GetBlob' 和 'CopyBlob' 作業的 'TotalEgress' 總和，可以估計從儲存體帳戶擷取的資料量。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-282">The amount of data retrieved from the storage account can be estimated by looking at the sum of *'TotalEgress'* for primarily the *'GetBlob'* and *'CopyBlob'* operations.</span></span>
* <span data-ttu-id="c5fdb-283">查看主要 'PutBlob'、'PutBlock'、'CopyBlob' 和 'AppendBlock' 作業的 'TotalIngress' 總和，可以估計寫入至儲存體帳戶的資料量。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-283">The amount of data written to the storage account can be estimated by looking at the sum of *'TotalIngress'* for primarily the *'PutBlob'*, *'PutBlock'*, *'CopyBlob'* and *'AppendBlock'* operations.</span></span>

<span data-ttu-id="c5fdb-284">如果是 GRS 或 RA-GRS 儲存體帳戶，使用寫入的資料量估計值，也可以計算 Blob 儲存體帳戶的異地複寫資料傳輸成本。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-284">The cost of geo-replication data transfer for Blob storage accounts can also be calculated by using the estimate for the amount of data written in case of a GRS or RA-GRS storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="c5fdb-285">關於計算使用經常性存取或非經常性存取儲存層的成本，如需更詳細的範例，請查看標題為「經常性存取或非經常性存取層是什麼，以及如何判斷要使用哪一個？」的常見問題。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-285">For a more detailed example about calculating the costs for using the hot or cool storage tier, please take a look at the FAQ titled *'What are Hot and Cool access tiers and how should I determine which one to use?'*</span></span> <span data-ttu-id="c5fdb-286">於 [Azure 儲存體定價頁面](https://azure.microsoft.com/pricing/details/storage/)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-286">in the [Azure Storage Pricing Page](https://azure.microsoft.com/pricing/details/storage/).</span></span>
> 
> 

### <a name="migrating-existing-data"></a><span data-ttu-id="c5fdb-287">移轉現有的資料</span><span class="sxs-lookup"><span data-stu-id="c5fdb-287">Migrating existing data</span></span>
<span data-ttu-id="c5fdb-288">Blob 儲存體帳戶專門用於儲存區塊和附加 Blob。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-288">A Blob storage account is specialized for storing only block and append blobs.</span></span> <span data-ttu-id="c5fdb-289">現有的一般用途儲存體帳戶 (允許您儲存資料表、佇列、檔案、磁碟以及 Blob) 無法轉換為 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-289">Existing general-purpose storage accounts, which allow you to store tables, queues, files and disks, as well as blobs, cannot be converted to Blob storage accounts.</span></span> <span data-ttu-id="c5fdb-290">若要使用儲存層，您必須建立新的 Blob 儲存體帳戶，並將現有的資料移轉至新建立的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-290">To use the storage tiers, you will need to create new Blob storage accounts and migrate your existing data into the newly created accounts.</span></span>

<span data-ttu-id="c5fdb-291">您可以使用下列方法，將現有的資料從內部部署儲存體裝置、第三方雲端儲存體提供者，或 Azure 中現有的一般用途儲存體帳戶移轉至 Blob 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="c5fdb-291">You can use the following methods to migrate existing data into Blob storage accounts from on-premises storage devices, from third-party cloud storage providers, or from your existing general-purpose storage accounts in Azure:</span></span>

#### <a name="azcopy"></a><span data-ttu-id="c5fdb-292">AzCopy</span><span class="sxs-lookup"><span data-stu-id="c5fdb-292">AzCopy</span></span>
<span data-ttu-id="c5fdb-293">AzCopy 為 Windows 命令列公用程式，可以極高效能將資料複製到 Azure 儲存體，以及從 Azure 儲存體複製資料。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-293">AzCopy is a Windows command-line utility designed for high-performance copying of data to and from Azure Storage.</span></span> <span data-ttu-id="c5fdb-294">您可以使用 AzCopy 將資料從現有一般用途的儲存體帳戶複製到 Blob 儲存體帳戶中，或將資料從內部部署儲存體裝置上傳至 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-294">You can use AzCopy to copy data into your Blob storage account from your existing general-purpose storage accounts, or to upload data from your on-premises storage devices into your Blob storage account.</span></span>

<span data-ttu-id="c5fdb-295">如需詳細資訊，請參閱 [使用 AzCopy 命令列公用程式傳輸資料](storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-295">For more details, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

#### <a name="data-movement-library"></a><span data-ttu-id="c5fdb-296">資料移動程式庫</span><span class="sxs-lookup"><span data-stu-id="c5fdb-296">Data Movement Library</span></span>
<span data-ttu-id="c5fdb-297">適用於 .NET 的 Azure 儲存體資料移動程式庫是以支援 AzCopy 的核心資料移動架構為基礎。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-297">Azure Storage data movement library for .NET is based on the core data movement framework that powers AzCopy.</span></span> <span data-ttu-id="c5fdb-298">此程式庫是針對類似於 AzCopy 的高效能、可靠且簡單的資料傳輸作業而設計的。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-298">The library is designed for high-performance, reliable and easy data transfer operations similar to AzCopy.</span></span> <span data-ttu-id="c5fdb-299">這可讓您充分受惠於 AzCopy 在您的應用程式中以原生方式提供的功能，而無需處理 AzCopy 外部執行個體的執行和監視。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-299">This allows you to take full benefits of the features provided by AzCopy in your application natively without having to deal with running and monitoring external instances of AzCopy.</span></span>

<span data-ttu-id="c5fdb-300">如需詳細資訊，請參閱 [適用於 .Net 的 Azure 儲存體資料移動程式庫](https://github.com/Azure/azure-storage-net-data-movement)</span><span class="sxs-lookup"><span data-stu-id="c5fdb-300">For more details, see [Azure Storage Data Movement Library for .Net](https://github.com/Azure/azure-storage-net-data-movement)</span></span>

#### <a name="rest-api-or-client-library"></a><span data-ttu-id="c5fdb-301">REST API 或用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="c5fdb-301">REST API or Client Library</span></span>
<span data-ttu-id="c5fdb-302">您可以建立自訂應用程式，以使用其中一個 Azure 用戶端程式庫或 Azure 儲存體服務 REST API，將您的資料移轉至 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-302">You can create a custom application to migrate your data into a Blob storage account using one of the Azure client libraries or the Azure storage services REST API.</span></span> <span data-ttu-id="c5fdb-303">Azure 儲存體針對以下多種語言和平台提供豐富的用戶端程式庫：例如 .NET、Java、C++、Node.JS、PHP、Ruby 和 Python。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-303">Azure Storage provides rich client libraries for multiple languages and platforms like .NET, Java, C++, Node.JS, PHP, Ruby, and Python.</span></span> <span data-ttu-id="c5fdb-304">這些用戶端程式庫提供多種進階功能，例如大重試邏輯、記錄與並行上傳等等。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-304">The client libraries offer advanced capabilities such as retry logic, logging, and parallel uploads.</span></span> <span data-ttu-id="c5fdb-305">您也可以直接透過 REST API 開發，它可以透過提出 HTTP/HTTPS 要求的任何語言進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-305">You can also develop directly against the REST API, which can be called by any language that makes HTTP/HTTPS requests.</span></span>

<span data-ttu-id="c5fdb-306">如需詳細資訊，請參閱 [開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-306">For more details, see [Get Started with Azure Blob storage](storage-dotnet-how-to-use-blobs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c5fdb-307">使用用戶端加密來加密的 Blob 會儲存利用 Blob 儲存的加密相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-307">Blobs encrypted using client-side encryption store encryption-related metadata stored with the blob.</span></span> <span data-ttu-id="c5fdb-308">任何複製機制絕對要能夠確保保留 Blob 中繼資料 (尤其是加密相關中繼資料)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-308">It is absolutely critical that any copy mechanism should ensure that the blob metadata, and especially the encryption-related metadata, is preserved.</span></span> <span data-ttu-id="c5fdb-309">如果您複製不含此中繼資料的 Blob，Blob 內容將無法再次擷取。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-309">If you copy the blobs without this metadata, the blob content will not be retrievable again.</span></span> <span data-ttu-id="c5fdb-310">如需有關加密相關中繼資料的詳細資訊，請參閱 [Azure 儲存體用戶端加密](storage-client-side-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-310">For more details regarding encryption-related metadata, see [Azure Storage Client-Side Encryption](storage-client-side-encryption.md).</span></span>
> 
> 

## <a name="faqs"></a><span data-ttu-id="c5fdb-311">常見問題集</span><span class="sxs-lookup"><span data-stu-id="c5fdb-311">FAQs</span></span>
1. <span data-ttu-id="c5fdb-312">**現有的儲存體帳戶是否仍然可用？**</span><span class="sxs-lookup"><span data-stu-id="c5fdb-312">**Are existing storage accounts still available?**</span></span>
   
    <span data-ttu-id="c5fdb-313">是，現有的儲存體帳戶仍然可用，且價格或功能不變。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-313">Yes, existing storage accounts are still available and are unchanged in pricing or functionality.</span></span>  <span data-ttu-id="c5fdb-314">它們並沒有選擇儲存層的能力，所以未來不會有分層功能。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-314">They do not have the ability to choose a storage tier and will not have tiering capabilities in the future.</span></span>
2. <span data-ttu-id="c5fdb-315">**為何和何時應該開始使用 Blob 儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="c5fdb-315">**Why and when should I start using Blob storage accounts?**</span></span>
   
    <span data-ttu-id="c5fdb-316">Blob 儲存體帳戶專門用於儲存 Blob，可讓我們引進以 Blob 為中心的新功能。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-316">Blob storage accounts are specialized for storing blobs and allow us to introduce new blob-centric features.</span></span> <span data-ttu-id="c5fdb-317">從現在開始，Blob 儲存體帳戶是儲存 Blob 的建議方式，因為將會根據此帳戶類型引進未來的功能，例如階層式儲存體和分層功能。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-317">Going forward, Blob storage accounts are the recommended way for storing blobs, as future capabilities such as hierarchical storage and tiering will be introduced based on this account type.</span></span> <span data-ttu-id="c5fdb-318">不過，您可以根據您的業務需求決定何時移轉。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-318">However, it is up to you when you would like to migrate based on your business requirements.</span></span>
3. <span data-ttu-id="c5fdb-319">**是否可以將現有的儲存體帳戶轉換成 Blob 儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="c5fdb-319">**Can I convert my existing storage account to a Blob storage account?**</span></span>
   
    <span data-ttu-id="c5fdb-320">否。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-320">No.</span></span> <span data-ttu-id="c5fdb-321">Blob 儲存體帳戶是不同種類的儲存體帳戶，您必須建立新的並如上所述移轉您的資料。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-321">Blob storage account is a different kind of storage account and you will need to create it new and migrate your data as explained above.</span></span>
4. <span data-ttu-id="c5fdb-322">**可以在相同帳戶中的這兩個儲存層中儲存物件嗎？**</span><span class="sxs-lookup"><span data-stu-id="c5fdb-322">**Can I store objects in both storage tiers in the same account?**</span></span>
   
    <span data-ttu-id="c5fdb-323">[存取層]  屬性指定儲存層會設定於帳戶層級並套用至該帳戶中的所有物件。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-323">The *'Access Tier'* attribute which indicates the storage tier is set at an account level and applies to all objects in that account.</span></span> <span data-ttu-id="c5fdb-324">您無法在物件層級設定存取層屬性。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-324">You cannot set the access tier attribute at an object level.</span></span>
5. <span data-ttu-id="c5fdb-325">**是否可以在 Blob 儲存體帳戶上變更儲存層？**</span><span class="sxs-lookup"><span data-stu-id="c5fdb-325">**Can I change the storage tier of my Blob storage account?**</span></span>
   
    <span data-ttu-id="c5fdb-326">是。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-326">Yes.</span></span> <span data-ttu-id="c5fdb-327">在儲存體帳戶上設定 [存取層]  屬性，就能夠變更儲存層。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-327">You will be able to change the storage tier by setting the *'Access Tier'* attribute on the storage account.</span></span> <span data-ttu-id="c5fdb-328">變更儲存層將會套用到帳戶中儲存的所有物件。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-328">Changing the storage tier will apply to all objects stored in the account.</span></span> <span data-ttu-id="c5fdb-329">將儲存層從經常存取變更為不常存取並不會產生任何費用，而從不常存取變更為經常存取則會產生用於讀取帳戶中所有資料的每 GB 成本。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-329">Change the storage tier from hot to cool will not incur any charges, while changing from cool to hot will incur a per GB cost for reading all the data in the account.</span></span>
6. <span data-ttu-id="c5fdb-330">**可以變更 Blob 儲存體帳戶的儲存層的頻率為何？**</span><span class="sxs-lookup"><span data-stu-id="c5fdb-330">**How frequently can I change the storage tier of my Blob storage account?**</span></span>
   
    <span data-ttu-id="c5fdb-331">雖然我們不會強制執行可以變更儲存層的頻率限制，但請留意，將儲存層從不常存取變更為經常存取將產生明顯的費用。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-331">While we do not enforce a limitation on how frequently the storage tier can be changed, please be aware that changing the storage tier from cool to hot will incur significant charges.</span></span> <span data-ttu-id="c5fdb-332">我們不建議您經常變更儲存層。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-332">We do not recommend changing the storage tier frequently.</span></span>
7. <span data-ttu-id="c5fdb-333">**非經常性存取儲存層中的 Blob 與經常性存取儲存層中的 Blob 的行為會有所不同嗎？**</span><span class="sxs-lookup"><span data-stu-id="c5fdb-333">**Will the blobs in the cool storage tier behave differently than the ones in the hot storage tier?**</span></span>
   
    <span data-ttu-id="c5fdb-334">經常性存取儲存層中的 Blob 與一般用途儲存體帳戶中的 Blob 有相同的延遲。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-334">Blobs in the hot storage tier have the same latency as blobs in general-purpose storage accounts.</span></span> <span data-ttu-id="c5fdb-335">非經常性存取儲存層中的 Blob 與一般用途儲存體帳戶中的 Blob 有類似的延遲 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-335">Blobs in the cool storage tier have a similar latency (in milliseconds) as blobs in general-purpose storage accounts.</span></span>
   
    <span data-ttu-id="c5fdb-336">相較於經常性存取儲存層中儲存的 Blob，非經常性存取儲存層中的 Blob 有稍微較低的可用性服務等級 (SLA)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-336">Blobs in the cool storage tier will have a slightly lower availability service level (SLA) than the blobs stored in the hot storage tier.</span></span> <span data-ttu-id="c5fdb-337">如需詳細資訊，請參閱 [儲存體的 SLA](https://azure.microsoft.com/support/legal/sla/storage)。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-337">For more details, see [SLA for storage](https://azure.microsoft.com/support/legal/sla/storage).</span></span>
8. <span data-ttu-id="c5fdb-338">**可以將分頁 Blob 和虛擬機器磁碟儲存在 Blob 儲存體帳戶嗎？**</span><span class="sxs-lookup"><span data-stu-id="c5fdb-338">**Can I store page blobs and virtual machine disks in Blob storage accounts?**</span></span>
   
    <span data-ttu-id="c5fdb-339">Blob 儲存體帳戶僅支援區塊和附加 Blob，不支援分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-339">Blob storage accounts support only block and append blobs, and not page blobs.</span></span> <span data-ttu-id="c5fdb-340">Azure 虛擬機器磁碟是由分頁 Blob 支援，因此 Blob 儲存體帳戶無法用來儲存虛擬機器磁碟。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-340">Azure virtual machine disks are backed by page blobs and as a result Blob storage accounts cannot be used to store virtual machine disks.</span></span> <span data-ttu-id="c5fdb-341">不過，可以將虛擬機器磁碟的備份儲存為 Blob 儲存體帳戶中的區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-341">However it is possible to store backups of the virtual machine disks as block blobs in a Blob storage account.</span></span>
9. <span data-ttu-id="c5fdb-342">**是否需要將現有的應用程式變更成使用 Blob 儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="c5fdb-342">**Will I need to change my existing applications to use Blob storage accounts?**</span></span>
   
    <span data-ttu-id="c5fdb-343">對區塊和附加 Blob 而言，Blob 儲存體帳戶與一般用途儲存體帳戶的 API 完全一致。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-343">Blob storage accounts are 100% API consistent with general-purpose storage accounts for block and append blobs.</span></span> <span data-ttu-id="c5fdb-344">只要您的應用程式使用區塊 Blob 或附加 Blob，而且您使用 2014-02-14 版或更高版本的[儲存體服務 REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx)，您的應用程式就應該能運作。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-344">As long as your application is using block blobs or append blobs, and you are using the 2014-02-14 version of the [Storage Services REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) or greater your application should work.</span></span> <span data-ttu-id="c5fdb-345">如果您使用舊版的通訊協定，則必須將應用程式更新成使用新的版本，才能完美地搭配這兩種類型的儲存體帳戶運作。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-345">If you are using an older version of the protocol, then you will need to update your application to use the new version so as to work seamlessly with both types of storage accounts.</span></span> <span data-ttu-id="c5fdb-346">一般而言，不論您使用哪個儲存體帳戶類型，我們都會建議使用最新版本。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-346">In general, we always recommend using the latest version regardless of which storage account type you use.</span></span>
10. <span data-ttu-id="c5fdb-347">**使用者經驗是否會有所改變？**</span><span class="sxs-lookup"><span data-stu-id="c5fdb-347">**Will there be a change in user experience?**</span></span>
    
    <span data-ttu-id="c5fdb-348">儲存區塊和附加 Blob 時，Blob 儲存體帳戶非常類似於一般用途的儲存體帳戶，並支援 Azure 儲存體的所有重要功能，包括高持久性和可用性、延展性、效能和安全性。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-348">Blob storage accounts are very similar to a general-purpose storage accounts for storing block and append blobs, and support all the key features of Azure Storage, including high durability and availability, scalability, performance, and security.</span></span> <span data-ttu-id="c5fdb-349">除了 Blob 儲存體帳戶特有的功能和限制及其上面所列的儲存層以外，其他一切均維持不變。</span><span class="sxs-lookup"><span data-stu-id="c5fdb-349">Other than the features and restrictions specific to Blob storage accounts and its storage tiers that have been called out above, everything else remains the same.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5fdb-350">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5fdb-350">Next steps</span></span>
### <a name="evaluate-blob-storage-accounts"></a><span data-ttu-id="c5fdb-351">評估 Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c5fdb-351">Evaluate Blob storage accounts</span></span>
[<span data-ttu-id="c5fdb-352">檢查各區域的 Blob 儲存體帳戶可用性</span><span class="sxs-lookup"><span data-stu-id="c5fdb-352">Check availability of Blob storage accounts by region</span></span>](https://azure.microsoft.com/regions/#services)

[<span data-ttu-id="c5fdb-353">啟用 Azure 儲存體計量以評估您目前的儲存體帳戶使用量</span><span class="sxs-lookup"><span data-stu-id="c5fdb-353">Evaluate usage of your current storage accounts by enabling Azure Storage metrics</span></span>](storage-enable-and-view-metrics.md)

[<span data-ttu-id="c5fdb-354">檢查各區域的 Blob 儲存體價格</span><span class="sxs-lookup"><span data-stu-id="c5fdb-354">Check Blob storage pricing by region</span></span>](https://azure.microsoft.com/pricing/details/storage/)

[<span data-ttu-id="c5fdb-355">檢查資料傳輸價格</span><span class="sxs-lookup"><span data-stu-id="c5fdb-355">Check data transfers pricing</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a><span data-ttu-id="c5fdb-356">開始使用 Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c5fdb-356">Start using Blob storage accounts</span></span>
[<span data-ttu-id="c5fdb-357">開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="c5fdb-357">Get Started with Azure Blob storage</span></span>](storage-dotnet-how-to-use-blobs.md)

[<span data-ttu-id="c5fdb-358">從 Azure 儲存體來回移動資料</span><span class="sxs-lookup"><span data-stu-id="c5fdb-358">Moving data to and from Azure Storage</span></span>](storage-moving-data.md)

[<span data-ttu-id="c5fdb-359">使用 AzCopy 命令列公用程式傳輸資料</span><span class="sxs-lookup"><span data-stu-id="c5fdb-359">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

[<span data-ttu-id="c5fdb-360">瀏覽及探索您的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c5fdb-360">Browse and explore your storage accounts</span></span>](http://storageexplorer.com/)

