---
title: "管理 Azure 資料目錄中的資料資產 | Microsoft Docs"
description: "本文專門說明如何控制 Azure 資料目錄中已註冊資料資產的可見性和擁有權。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 8b9159b7bc4f7b2dac12d9012c6c903e75a6ac16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="46f04-103">管理 Azure 資料目錄中的資料資產</span><span class="sxs-lookup"><span data-stu-id="46f04-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="46f04-104">簡介</span><span class="sxs-lookup"><span data-stu-id="46f04-104">Introduction</span></span>
<span data-ttu-id="46f04-105">Azure 資料目錄專為資料來源探索功能而設計，讓您能夠輕鬆地探索和了解要執行分析和做出決策所需的資料來源。</span><span class="sxs-lookup"><span data-stu-id="46f04-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand the data sources you need to perform analysis and make decisions.</span></span> <span data-ttu-id="46f04-106">當您和其他使用者都能找到並了解最大範圍的可用資料來源時，這些探索功能就能發揮最大效果。</span><span class="sxs-lookup"><span data-stu-id="46f04-106">These discovery capabilities make the biggest impact when you and other users can find and understand the broadest range of available data sources.</span></span> <span data-ttu-id="46f04-107">考慮到這些要素，資料目錄的預設行為是要讓所有目錄使用者都能看見並找到所有已註冊的資料來源。</span><span class="sxs-lookup"><span data-stu-id="46f04-107">With these elements in mind, the default behavior of Data Catalog is for all registered data sources to be visible to and discoverable by all catalog users.</span></span>

<span data-ttu-id="46f04-108">資料目錄並不會讓您存取資料本身。</span><span class="sxs-lookup"><span data-stu-id="46f04-108">Data Catalog does not give you access to the data itself.</span></span> <span data-ttu-id="46f04-109">資料能否存取是由資料來源的擁有者控制。</span><span class="sxs-lookup"><span data-stu-id="46f04-109">Data access is controlled by the owner of the data source.</span></span> <span data-ttu-id="46f04-110">利用資料目錄，您可以探索資料來源，以及檢視與目錄中註冊的來源相關的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="46f04-110">With Data Catalog, you can discover data sources and view the metadata that's related to the sources that are registered in the catalog.</span></span>

<span data-ttu-id="46f04-111">不過，有時候只有特定使用者或特定群組的成員才能看到資料來源。</span><span class="sxs-lookup"><span data-stu-id="46f04-111">There might be situations, however, where data sources should only be visible to specific users, or to members of specific groups.</span></span> <span data-ttu-id="46f04-112">若是這樣的情況，使用者便可取得目錄中的註冊資料資產的擁有權，然後控制其擁有之資產的可見性。</span><span class="sxs-lookup"><span data-stu-id="46f04-112">In such scenarios, users can take ownership of registered data assets within the catalog and then control the visibility of the assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="46f04-113">本文所描述的功能只適用於標準版 Azure 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="46f04-113">The functionality described in this article is available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="46f04-114">免費版不提供擁有權和限制資料資產可見性的功能。</span><span class="sxs-lookup"><span data-stu-id="46f04-114">The Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="46f04-115">管理資料資產的擁有權</span><span class="sxs-lookup"><span data-stu-id="46f04-115">Manage ownership of data assets</span></span>
<span data-ttu-id="46f04-116">根據預設，資料目錄中註冊的資料資產為無人擁有。</span><span class="sxs-lookup"><span data-stu-id="46f04-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="46f04-117">所有具有目錄存取權的使用者都可以探索及標註這些資產。</span><span class="sxs-lookup"><span data-stu-id="46f04-117">Any user with permission to access the catalog can discover and annotate these assets.</span></span> <span data-ttu-id="46f04-118">使用者可以取得無人擁有之資料資產的擁有權，並接著限制其擁有之資產的可見性。</span><span class="sxs-lookup"><span data-stu-id="46f04-118">Users can take ownership of unowned data assets and then limit the visibility of the assets they own.</span></span>

<span data-ttu-id="46f04-119">當資料目錄中的資料資產有擁有者時，只有獲得擁有者授權的使用者可以探索資產並檢視其中繼資料，而且只有擁有者可以從目錄中刪除資產。</span><span class="sxs-lookup"><span data-stu-id="46f04-119">When a data asset in Data Catalog is owned, only users who are authorized by the owners can discover the asset and view its metadata, and only the owners can delete the asset from the catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="46f04-120">資料目錄中的擁有權只會影響目錄中儲存的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="46f04-120">Ownership in Data Catalog affects only the metadata that's stored in the catalog.</span></span> <span data-ttu-id="46f04-121">擁有權不會授與任何關於基礎資料來源的權限。</span><span class="sxs-lookup"><span data-stu-id="46f04-121">Ownership does not confer any permissions on the underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="46f04-122">取得擁有權</span><span class="sxs-lookup"><span data-stu-id="46f04-122">Take ownership</span></span>
<span data-ttu-id="46f04-123">使用者只要在資料目錄入口網站中選取 [取得擁有權] 選項，就能取得資料資產的擁有權。</span><span class="sxs-lookup"><span data-stu-id="46f04-123">Users can take ownership of data assets by selecting the **Take Ownership** option in the Data Catalog portal.</span></span> <span data-ttu-id="46f04-124">取得無人擁有之資料資產的擁有權無需任何特殊權限。</span><span class="sxs-lookup"><span data-stu-id="46f04-124">No special permissions are required to take ownership of an unowned data asset.</span></span> <span data-ttu-id="46f04-125">所有使用者都能取得無人擁有之資料資產的擁有權。</span><span class="sxs-lookup"><span data-stu-id="46f04-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="46f04-126">新增擁有者和共同擁有者</span><span class="sxs-lookup"><span data-stu-id="46f04-126">Add owners and co-owners</span></span>
<span data-ttu-id="46f04-127">如果資料資產已被人擁有，其他使用者就無法簡單地取得擁有權。</span><span class="sxs-lookup"><span data-stu-id="46f04-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="46f04-128">必須由現有擁有者將他們新增為共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="46f04-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="46f04-129">任何擁有者都能將其他使用者或安全性群組新增為共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="46f04-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="46f04-130">已有擁有者的資料資產最好至少有兩個人擔任擁有者。</span><span class="sxs-lookup"><span data-stu-id="46f04-130">It is a best practice to have at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="46f04-131">移除擁有者</span><span class="sxs-lookup"><span data-stu-id="46f04-131">Remove owners</span></span>
<span data-ttu-id="46f04-132">資產擁有者既然能新增共同擁有者，當然也能移除共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="46f04-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="46f04-133">移除自己之擁有者身分的資產擁有者無法再管理資產。</span><span class="sxs-lookup"><span data-stu-id="46f04-133">An asset owner who removes him or herself as an owner can no longer manage the asset.</span></span> <span data-ttu-id="46f04-134">如果資產擁有者移除自己的擁有者身分，而且已無其他共同擁有者，則資產會回復為無人擁有狀態。</span><span class="sxs-lookup"><span data-stu-id="46f04-134">If the asset owner removes him or herself as an owner and there are no other co-owners, the asset reverts to an unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="46f04-135">控制可見性</span><span class="sxs-lookup"><span data-stu-id="46f04-135">Control visibility</span></span>
<span data-ttu-id="46f04-136">資料資產擁有者可以控制其擁有之資料資產的可見性。</span><span class="sxs-lookup"><span data-stu-id="46f04-136">Data-asset owners can control the visibility of the data assets they own.</span></span> <span data-ttu-id="46f04-137">若要以預設值限制可見性，讓所有資料目錄使用者都能探索及檢視資料資產，資產擁有者可以將資產屬性中的可見性設定從 [所有人] 切換為 [擁有者與這些使用者]。</span><span class="sxs-lookup"><span data-stu-id="46f04-137">To restrict visibility as the default, where all Data Catalog users can discover and view the data asset, the asset owner can toggle the visibility setting from **Everyone** to **Owners & These Users** in the properties for the asset.</span></span> <span data-ttu-id="46f04-138">接著，擁有者便可以新增特定使用者和安全性群組。</span><span class="sxs-lookup"><span data-stu-id="46f04-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="46f04-139">請盡可能將資產的擁有權和可見性權限指派給安全性群組而非個別使用者。</span><span class="sxs-lookup"><span data-stu-id="46f04-139">Whenever possible, asset ownership and visibility permissions should be assigned to security groups and not to individual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="46f04-140">目錄管理員</span><span class="sxs-lookup"><span data-stu-id="46f04-140">Catalog administrators</span></span>
<span data-ttu-id="46f04-141">資料目錄管理員都是目錄中所有資產的隱含共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="46f04-141">Data Catalog administrators are implicitly co-owners of all assets in the catalog.</span></span> <span data-ttu-id="46f04-142">資產擁有者無法移除管理員的可見性，而且管理員可以管理目錄中所有資料資產的擁有權和可見性。</span><span class="sxs-lookup"><span data-stu-id="46f04-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in the catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="46f04-143">摘要</span><span class="sxs-lookup"><span data-stu-id="46f04-143">Summary</span></span>
<span data-ttu-id="46f04-144">資料目錄用於中繼資料和資料資產探索的群眾外包模型可讓所有目錄使用者參與和探索。</span><span class="sxs-lookup"><span data-stu-id="46f04-144">The Data Catalog crowdsourcing model to metadata and data asset discovery allows all catalog users to contribute and discover.</span></span> <span data-ttu-id="46f04-145">標準版的資料目錄專為擁有權和管理而設計，可限制特定資料資產的可見性與使用。</span><span class="sxs-lookup"><span data-stu-id="46f04-145">The Standard Edition of Data Catalog is designed for ownership and management to limit the visibility and use of specific data assets.</span></span>
