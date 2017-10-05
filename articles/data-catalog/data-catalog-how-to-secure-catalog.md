---
title: "如何保護對 Azure 資料目錄的存取 | Microsoft Docs"
description: "本文說明如何保護資料目錄及其資料資產。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: 9664a7bc8493b08c8e0797ac6f1b212079829833
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-secure-access-to-data-catalog-and-data-assets"></a><span data-ttu-id="072c8-103">如何保護對資料目錄及資料資產的存取</span><span class="sxs-lookup"><span data-stu-id="072c8-103">How to secure access to data catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="072c8-104">只有在標準版「Azure 資料目錄」中才有提供此功能。</span><span class="sxs-lookup"><span data-stu-id="072c8-104">This feature is available only in the standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="072c8-105">「Azure 資料目錄」可讓您指定誰可以存取資料目錄，以及他們可以對目錄中的中繼資料執行哪些作業 (註冊、標註、取得擁有權)。</span><span class="sxs-lookup"><span data-stu-id="072c8-105">Azure Data Catalog allows you to specify who can access the data catalog and what operations (register, annotate, take ownership) they can perform on metadata in the catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="072c8-106">目錄使用者和權限</span><span class="sxs-lookup"><span data-stu-id="072c8-106">Catalog users and permissions</span></span>
<span data-ttu-id="072c8-107">將資料目錄的存取權授與使用者或群組並設定權限：</span><span class="sxs-lookup"><span data-stu-id="072c8-107">To give a user or a group the access to a data catalog and set permissions:</span></span>

1. <span data-ttu-id="072c8-108">在[您資料目錄的首頁](http://www.azuredatacatalog.com)，按一下工具列上的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="072c8-108">On the [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on the toolbar.</span></span>

    ![資料目錄 - 設定](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="072c8-110">在 [設定] 頁面中，展開 [目錄使用者] 區段。</span><span class="sxs-lookup"><span data-stu-id="072c8-110">In the settings page, expand the **Catalog Users** section.</span></span>
    <span data-ttu-id="072c8-111">![目錄使用者 - 新增](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="072c8-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="072c8-112">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="072c8-112">Click **Add**.</span></span>
4. <span data-ttu-id="072c8-113">在與此目錄關聯的 Azure Active Directory (AAD) 中輸入完整的「使用者名稱」或「安全性群組」的名稱。</span><span class="sxs-lookup"><span data-stu-id="072c8-113">Enter the fully qualified **user name** or name of the **security group** in the Azure Active Directory (AAD) associated with the catalog.</span></span> <span data-ttu-id="072c8-114">如果您要新增多個使用者或群組，請使用逗號 (\`,’) 作為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="072c8-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="072c8-115">![目錄使用者 - 使用者或群組](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="072c8-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="072c8-116">按 **ENTER** 或 **TAB** 來移出文字方塊。</span><span class="sxs-lookup"><span data-stu-id="072c8-116">Press **ENTER** or **TAB** out of the text box.</span></span> 
6.  <span data-ttu-id="072c8-117">確認所有權限 ([標註]、[註冊] 及 [取得擁有權]) 皆已預設指派給這些使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="072c8-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned to these users or groups by default.</span></span> <span data-ttu-id="072c8-118">也就是說，使用者或群組可以[註冊資料資產]( data-catalog-how-to-register.md)、[標註資料資產]( data-catalog-how-to-annotate.md)，以及[取得資料資產的擁有權]( data-catalog-how-to-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="072c8-118">That is, the user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="072c8-119">![目錄使用者 - 預設權限](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="072c8-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="072c8-120">若只想將目錄的讀取存取權授與使用者或群組，請將該使用者或群組的 [標註] 選項取消選取。</span><span class="sxs-lookup"><span data-stu-id="072c8-120">To give a user or group only the read access to the catalog, clear the **annotate** option for that user or group.</span></span> <span data-ttu-id="072c8-121">當您這麼做時，該使用者或群組便無法標註目錄中的資料資產，但可以檢視它們。</span><span class="sxs-lookup"><span data-stu-id="072c8-121">When you do so, the user or group cannot annotate data assets in the catalog but they can view them.</span></span> 
8.  <span data-ttu-id="072c8-122">若要拒絕使用者或群組註冊資料資產，請將該使用者或群組的 [註冊] 選項取消選取。</span><span class="sxs-lookup"><span data-stu-id="072c8-122">To deny a user or group from registering data assets, clear the **register** option for that user or group.</span></span>
9.  <span data-ttu-id="072c8-123">若要拒絕使用者取得資料資產的擁有權，請將該使用者或群組的 [取得擁有權] 選項取消選取。</span><span class="sxs-lookup"><span data-stu-id="072c8-123">To deny a user from taking ownership of a data asset, clear the **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="072c8-124">若要從目錄使用者中刪除某個使用者/群組，請按一下清單底部該使用者/群組的 [x]。</span><span class="sxs-lookup"><span data-stu-id="072c8-124">To delete a user/group from catalog users, click **x** for the user/group at the bottom of the list.</span></span> 
    <span data-ttu-id="072c8-125">![目錄使用者 - 刪除使用者](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="072c8-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="072c8-126">建議您將安全性群組新增到目錄使用者中，而不要直接新增使用者並指派權限。</span><span class="sxs-lookup"><span data-stu-id="072c8-126">We recommend that you add security groups to catalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="072c8-127">然後，將使用者新增到符合其角色及所需目錄存取權的安全性群組中。</span><span class="sxs-lookup"><span data-stu-id="072c8-127">Then, add users to the security groups that match their roles and their required access to the catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="072c8-128">特殊考量</span><span class="sxs-lookup"><span data-stu-id="072c8-128">Special considerations</span></span>

- <span data-ttu-id="072c8-129">指派給安全性群組的權限是附加的。</span><span class="sxs-lookup"><span data-stu-id="072c8-129">The permissions assigned to security groups are additive.</span></span> <span data-ttu-id="072c8-130">假設使用者位於兩個群組中。</span><span class="sxs-lookup"><span data-stu-id="072c8-130">Say, a user is in two groups.</span></span> <span data-ttu-id="072c8-131">一個群組具有標註權限，而另一個群組沒有標註權限。</span><span class="sxs-lookup"><span data-stu-id="072c8-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="072c8-132">那麼，使用者會具有標註權限。</span><span class="sxs-lookup"><span data-stu-id="072c8-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="072c8-133">明確指派給使用者的權限會覆寫指派給使用者所屬群組的權限。</span><span class="sxs-lookup"><span data-stu-id="072c8-133">The permissions assigned explicitly to a user override the permissions assigned to groups to which the user belongs.</span></span> <span data-ttu-id="072c8-134">在上述範例中，假設您已將使用者明確新增到目錄使用者中，而未指派標註權限。</span><span class="sxs-lookup"><span data-stu-id="072c8-134">In the previous example, say, you explicitly added the user to catalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="072c8-135">那麼，儘管該使用者所屬群組具有標註權限，他也無法標註資料資產。</span><span class="sxs-lookup"><span data-stu-id="072c8-135">The user cannot annotate data assets even though the user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="072c8-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="072c8-136">Next steps</span></span>
- [<span data-ttu-id="072c8-137">開始使用 Azure 資料目錄</span><span class="sxs-lookup"><span data-stu-id="072c8-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

