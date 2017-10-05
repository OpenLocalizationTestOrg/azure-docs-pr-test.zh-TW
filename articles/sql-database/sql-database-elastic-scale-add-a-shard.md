---
title: "使用彈性資料庫工具加入分區 | Microsoft Docs"
description: "如何使用 Elastic Scale API 將新的分區新增至分區集。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6a91ea2251ea3b748faba5c97765bfded9c00234
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="d57be-103">使用彈性資料庫工具加入分區</span><span class="sxs-lookup"><span data-stu-id="d57be-103">Adding a shard using Elastic Database tools</span></span>
## <a name="to-add-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="d57be-104">為新的範圍或索引鍵加入分區</span><span class="sxs-lookup"><span data-stu-id="d57be-104">To add a shard for a new range or key</span></span>
<span data-ttu-id="d57be-105">對於已經存在的分區對應，應用程式通常只需要加入新的分區，以處理預期來自新的索引鍵或索引鍵範圍的資料。</span><span class="sxs-lookup"><span data-stu-id="d57be-105">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="d57be-106">例如，以租用戶識別碼分區化的應用程式，可能需要為新的租用戶佈建新的分區，或者，每月分區化的資料可能需要在每個新月份開始之前佈建新的分區。</span><span class="sxs-lookup"><span data-stu-id="d57be-106">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="d57be-107">如果索引鍵值的新範圍尚不屬於現有的對應，則新增分區並將新的索引鍵或範圍與該分區產生關聯就非常簡單。</span><span class="sxs-lookup"><span data-stu-id="d57be-107">If the new range of key values is not already part of an existing mapping, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-to-an-existing-shard-map"></a><span data-ttu-id="d57be-108">範例：將分區及其範圍加入至現有的分區對應</span><span class="sxs-lookup"><span data-stu-id="d57be-108">Example:  adding a shard and its range to an existing shard map</span></span>
<span data-ttu-id="d57be-109">這個範例會使用 [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx)、[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)、[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) 方法，並建立 [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="d57be-109">This sample uses the [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) the [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of the [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="d57be-110">在下列範例中，已建立名為 **sample_shard_2** 的資料庫及其中的所有必要結構描述物件，以保存範圍 [300, 400)。</span><span class="sxs-lookup"><span data-stu-id="d57be-110">In the sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created to hold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create the mapping and associate it with the new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="d57be-111">或者，您也可以使用 Powershell 建立新的分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="d57be-111">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="d57be-112">範例請見 [這裡](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。</span><span class="sxs-lookup"><span data-stu-id="d57be-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="to-add-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="d57be-113">為現有範圍的空白部分加入分區</span><span class="sxs-lookup"><span data-stu-id="d57be-113">To add a shard for an empty part of an existing range</span></span>
<span data-ttu-id="d57be-114">在某些情況下，您可能已將某個範圍對應至分區，並在其某些部分填入資料，但現在您想讓後續的資料導向至不同的分區。</span><span class="sxs-lookup"><span data-stu-id="d57be-114">In some circumstances, you may have already mapped a range to a shard and partially filled it with data, but you now want upcoming data to be directed to a different shard.</span></span> <span data-ttu-id="d57be-115">例如，假設您依日期範圍分區，並且已配置 50 天給某個分區，但在第 24 天，您想要將後續資料分配到不同的分區。</span><span class="sxs-lookup"><span data-stu-id="d57be-115">For example, you shard by day range and have already allocated 50 days to a shard, but on day 24, you want future data to land in a different shard.</span></span> <span data-ttu-id="d57be-116">彈性資料庫 [分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md) 可以執行這項作業，但如果不需要移動資料 (例如，尚不存在日期範圍 [25, 50) 的資料，亦即第 25 天 (含) 到第 50 天 (不含)，您可以直接使用分區對應管理 API 完全執行此作業。</span><span class="sxs-lookup"><span data-stu-id="d57be-116">The elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for the range of days [25, 50), i.e., day 25 inclusive to 50 exclusive, does not yet exist) you can perform this entirely using the Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-the-empty-portion-to-a-newly-added-shard"></a><span data-ttu-id="d57be-117">範例：分割範圍並將空白部分指派給新增的分區</span><span class="sxs-lookup"><span data-stu-id="d57be-117">Example: splitting a range and assigning the empty portion to a newly-added shard</span></span>
<span data-ttu-id="d57be-118">已建立名為 "sample_shard_2" 的資料庫，及其中所有必要的結構描述物件。</span><span class="sxs-lookup"><span data-stu-id="d57be-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split the Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) to different shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline to a different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="d57be-119">**重要**：只有在您確定更新對應的範圍是空白時，才可使用這項技術。</span><span class="sxs-lookup"><span data-stu-id="d57be-119">**Important**:  Use this technique only if you are certain that the range for the updated mapping is empty.</span></span>  <span data-ttu-id="d57be-120">上述方法並不會檢查要移動的資料範圍，因此您最好在程式碼中納入檢查。</span><span class="sxs-lookup"><span data-stu-id="d57be-120">The methods above do not check data for the range being moved, so it is best to include checks in your code.</span></span>  <span data-ttu-id="d57be-121">如果資料列存在於要移動的範圍中，則實際的資料分佈將不會符合更新的分區對應。</span><span class="sxs-lookup"><span data-stu-id="d57be-121">If rows exist in the range being moved, the actual data distribution will not match the updated shard map.</span></span> <span data-ttu-id="d57be-122">在這些情況下，請改用 [分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md) 執行作業。</span><span class="sxs-lookup"><span data-stu-id="d57be-122">Use the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) to perform the operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

