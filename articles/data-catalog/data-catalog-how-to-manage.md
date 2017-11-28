---
title: "在 Azure 資料目錄中的 aaaManage 資料資產 |Microsoft 文件"
description: "hello 文章重點說明在 Azure 資料目錄中登錄 toocontrol 可見性和資料資產的擁有權的方式。"
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
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="d5af9-103">管理 Azure 資料目錄中的資料資產</span><span class="sxs-lookup"><span data-stu-id="d5af9-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="d5af9-104">簡介</span><span class="sxs-lookup"><span data-stu-id="d5af9-104">Introduction</span></span>
<span data-ttu-id="d5af9-105">Azure 資料目錄是為探索而設計的資料來源，以便您可以輕鬆地找出並了解 hello 資料來源，您需要 tooperform 分析和做出決策。</span><span class="sxs-lookup"><span data-stu-id="d5af9-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand hello data sources you need tooperform analysis and make decisions.</span></span> <span data-ttu-id="d5af9-106">您與其他使用者可以尋找並了解 hello 大範圍的可用資料來源時，這些探索功能會構成 hello 大影響。</span><span class="sxs-lookup"><span data-stu-id="d5af9-106">These discovery capabilities make hello biggest impact when you and other users can find and understand hello broadest range of available data sources.</span></span> <span data-ttu-id="d5af9-107">請注意這些項目時，資料目錄 hello 預設行為是針對所有已註冊的資料來源 toobe 可見 tooand 可探索所有目錄使用者。</span><span class="sxs-lookup"><span data-stu-id="d5af9-107">With these elements in mind, hello default behavior of Data Catalog is for all registered data sources toobe visible tooand discoverable by all catalog users.</span></span>

<span data-ttu-id="d5af9-108">資料目錄不允許您存取 toohello 資料本身。</span><span class="sxs-lookup"><span data-stu-id="d5af9-108">Data Catalog does not give you access toohello data itself.</span></span> <span data-ttu-id="d5af9-109">Hello hello 資料來源的擁有者所控制的資料存取。</span><span class="sxs-lookup"><span data-stu-id="d5af9-109">Data access is controlled by hello owner of hello data source.</span></span> <span data-ttu-id="d5af9-110">以資料目錄，您可以探索資料來源，並檢視相關的 toohello 來源註冊 hello 目錄中的 hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="d5af9-110">With Data Catalog, you can discover data sources and view hello metadata that's related toohello sources that are registered in hello catalog.</span></span>

<span data-ttu-id="d5af9-111">可能的情況下，不過，資料來源只應該儲存可見 toospecific 使用者或特定群組的 toomembers。</span><span class="sxs-lookup"><span data-stu-id="d5af9-111">There might be situations, however, where data sources should only be visible toospecific users, or toomembers of specific groups.</span></span> <span data-ttu-id="d5af9-112">在這種情況下，使用者可以取得 hello 目錄中註冊的資料資產的擁有權，然後控制他們所擁有的 hello 資產 hello 可見性。</span><span class="sxs-lookup"><span data-stu-id="d5af9-112">In such scenarios, users can take ownership of registered data assets within hello catalog and then control hello visibility of hello assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="d5af9-113">本文中所述的 hello 功能是只在 hello 標準版本的 Azure 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="d5af9-113">hello functionality described in this article is available only in hello Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="d5af9-114">hello 免費版本未提供功能的擁有權，以及限制資料資產可見性。</span><span class="sxs-lookup"><span data-stu-id="d5af9-114">hello Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="d5af9-115">管理資料資產的擁有權</span><span class="sxs-lookup"><span data-stu-id="d5af9-115">Manage ownership of data assets</span></span>
<span data-ttu-id="d5af9-116">根據預設，資料目錄中註冊的資料資產為無人擁有。</span><span class="sxs-lookup"><span data-stu-id="d5af9-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="d5af9-117">任何具有權限 tooaccess hello 類別目錄的使用者可以探索，並加上註解這些資產。</span><span class="sxs-lookup"><span data-stu-id="d5af9-117">Any user with permission tooaccess hello catalog can discover and annotate these assets.</span></span> <span data-ttu-id="d5af9-118">使用者可以使用未擁有的資料資產的擁有權，並限制他們自己的 hello 資產 hello 可見性。</span><span class="sxs-lookup"><span data-stu-id="d5af9-118">Users can take ownership of unowned data assets and then limit hello visibility of hello assets they own.</span></span>

<span data-ttu-id="d5af9-119">擁有資料目錄中的資料資產，使用者已獲授權由 hello 擁有者可以找出 hello 資產，並檢視它的中繼資料，並只有 hello 擁有者可以刪除 hello 資產從 hello 類別目錄。</span><span class="sxs-lookup"><span data-stu-id="d5af9-119">When a data asset in Data Catalog is owned, only users who are authorized by hello owners can discover hello asset and view its metadata, and only hello owners can delete hello asset from hello catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="d5af9-120">在資料目錄中的擁有權會影響儲存在 hello 類別目錄 hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="d5af9-120">Ownership in Data Catalog affects only hello metadata that's stored in hello catalog.</span></span> <span data-ttu-id="d5af9-121">擁有權不會授與 hello 基礎資料來源的任何權限。</span><span class="sxs-lookup"><span data-stu-id="d5af9-121">Ownership does not confer any permissions on hello underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="d5af9-122">取得擁有權</span><span class="sxs-lookup"><span data-stu-id="d5af9-122">Take ownership</span></span>
<span data-ttu-id="d5af9-123">使用者可以取得的資料資產的擁有權，藉由選取 hello **Take Ownership** hello 資料目錄入口網站中的選項。</span><span class="sxs-lookup"><span data-stu-id="d5af9-123">Users can take ownership of data assets by selecting hello **Take Ownership** option in hello Data Catalog portal.</span></span> <span data-ttu-id="d5af9-124">任何特殊權限不是未擁有的資料資產的必要的 tootake 擁有權。</span><span class="sxs-lookup"><span data-stu-id="d5af9-124">No special permissions are required tootake ownership of an unowned data asset.</span></span> <span data-ttu-id="d5af9-125">所有使用者都能取得無人擁有之資料資產的擁有權。</span><span class="sxs-lookup"><span data-stu-id="d5af9-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="d5af9-126">新增擁有者和共同擁有者</span><span class="sxs-lookup"><span data-stu-id="d5af9-126">Add owners and co-owners</span></span>
<span data-ttu-id="d5af9-127">如果資料資產已被人擁有，其他使用者就無法簡單地取得擁有權。</span><span class="sxs-lookup"><span data-stu-id="d5af9-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="d5af9-128">必須由現有擁有者將他們新增為共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="d5af9-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="d5af9-129">任何擁有者都能將其他使用者或安全性群組新增為共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="d5af9-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="d5af9-130">它是最佳的作法 toohave 至少兩個人員為擁有者的任何擁有資料資產。</span><span class="sxs-lookup"><span data-stu-id="d5af9-130">It is a best practice toohave at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="d5af9-131">移除擁有者</span><span class="sxs-lookup"><span data-stu-id="d5af9-131">Remove owners</span></span>
<span data-ttu-id="d5af9-132">資產擁有者既然能新增共同擁有者，當然也能移除共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="d5af9-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="d5af9-133">資產擁有者移除本身做為擁有者就無法再管理 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="d5af9-133">An asset owner who removes him or herself as an owner can no longer manage hello asset.</span></span> <span data-ttu-id="d5af9-134">如果 hello 資產擁有者移除本身做為擁有者，而且沒有其他共同擁有者，hello 資產會還原 tooan 未擁有狀態。</span><span class="sxs-lookup"><span data-stu-id="d5af9-134">If hello asset owner removes him or herself as an owner and there are no other co-owners, hello asset reverts tooan unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="d5af9-135">控制可見性</span><span class="sxs-lookup"><span data-stu-id="d5af9-135">Control visibility</span></span>
<span data-ttu-id="d5af9-136">資料資產擁有者可以控制他們所擁有的 hello 資料資產的 hello 可見性。</span><span class="sxs-lookup"><span data-stu-id="d5af9-136">Data-asset owners can control hello visibility of hello data assets they own.</span></span> <span data-ttu-id="d5af9-137">hello 預設 toorestrict 可見性，其中所有的資料目錄使用者可以探索和檢視 hello 資料資產 hello 資產擁有者可以切換 hello 可見性設定從**Everyone**太**擁有者與這些使用者** hello hello 資產的內容中。</span><span class="sxs-lookup"><span data-stu-id="d5af9-137">toorestrict visibility as hello default, where all Data Catalog users can discover and view hello data asset, hello asset owner can toggle hello visibility setting from **Everyone** too**Owners & These Users** in hello properties for hello asset.</span></span> <span data-ttu-id="d5af9-138">接著，擁有者便可以新增特定使用者和安全性群組。</span><span class="sxs-lookup"><span data-stu-id="d5af9-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="d5af9-139">您應該盡可能 toosecurity 群組和不 tooindividual 使用者應該指派資產的擁有權和可見性的權限。</span><span class="sxs-lookup"><span data-stu-id="d5af9-139">Whenever possible, asset ownership and visibility permissions should be assigned toosecurity groups and not tooindividual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="d5af9-140">目錄管理員</span><span class="sxs-lookup"><span data-stu-id="d5af9-140">Catalog administrators</span></span>
<span data-ttu-id="d5af9-141">資料目錄管理員是隱含的 hello 目錄中的所有資產的共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="d5af9-141">Data Catalog administrators are implicitly co-owners of all assets in hello catalog.</span></span> <span data-ttu-id="d5af9-142">資產擁有者無法移除系統管理員的可見性，而系統管理員可以管理擁有權和 hello 目錄中的所有資料資產的可見度。</span><span class="sxs-lookup"><span data-stu-id="d5af9-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in hello catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="d5af9-143">摘要</span><span class="sxs-lookup"><span data-stu-id="d5af9-143">Summary</span></span>
<span data-ttu-id="d5af9-144">hello 資料目錄 crowdsourcing 模型 toometadata 和資料資產探索可讓所有目錄使用者 toocontribute 及探索。</span><span class="sxs-lookup"><span data-stu-id="d5af9-144">hello Data Catalog crowdsourcing model toometadata and data asset discovery allows all catalog users toocontribute and discover.</span></span> <span data-ttu-id="d5af9-145">hello 標準版本的資料類別目錄被針對擁有權和管理 toolimit hello 可見性與使用特定的資料資產。</span><span class="sxs-lookup"><span data-stu-id="d5af9-145">hello Standard Edition of Data Catalog is designed for ownership and management toolimit hello visibility and use of specific data assets.</span></span>
