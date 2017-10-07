---
title: "aaaHow toosecure 存取 tooAzure 資料目錄 |Microsoft 文件"
description: "本文說明如何 toosecure 資料類別目錄和資料資產。"
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
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a><span data-ttu-id="ec1f7-103">Toosecure 存取 toodata 類別目錄和資料資產的方式</span><span class="sxs-lookup"><span data-stu-id="ec1f7-103">How toosecure access toodata catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ec1f7-104">只在 Azure 資料目錄的 hello standard edition 中使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-104">This feature is available only in hello standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="ec1f7-105">Azure 資料目錄可讓您 toospecify hello 資料目錄，以及可以存取的人員作業 （註冊、 標註，取得擁有權） 可以在 hello 目錄中的中繼資料上執行。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-105">Azure Data Catalog allows you toospecify who can access hello data catalog and what operations (register, annotate, take ownership) they can perform on metadata in hello catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="ec1f7-106">目錄使用者和權限</span><span class="sxs-lookup"><span data-stu-id="ec1f7-106">Catalog users and permissions</span></span>
<span data-ttu-id="ec1f7-107">toogive 使用者或群組 hello 存取 tooa 資料目錄，並設定權限：</span><span class="sxs-lookup"><span data-stu-id="ec1f7-107">toogive a user or a group hello access tooa data catalog and set permissions:</span></span>

1. <span data-ttu-id="ec1f7-108">在 [hello[首頁上的資料目錄](http://www.azuredatacatalog.com)，按一下**設定**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-108">On hello [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on hello toolbar.</span></span>

    ![資料目錄 - 設定](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="ec1f7-110">在 [hello] 設定頁面上，展開 [hello**目錄使用者**> 一節。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-110">In hello settings page, expand hello **Catalog Users** section.</span></span>
    <span data-ttu-id="ec1f7-111">![目錄使用者 - 新增](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="ec1f7-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="ec1f7-112">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-112">Click **Add**.</span></span>
4. <span data-ttu-id="ec1f7-113">輸入完整的 hello**使用者名**或名稱 hello**安全性群組**hello 與 hello 目錄相關聯的 Azure Active Directory (AAD) 中。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-113">Enter hello fully qualified **user name** or name of hello **security group** in hello Azure Active Directory (AAD) associated with hello catalog.</span></span> <span data-ttu-id="ec1f7-114">如果您要新增多個使用者或群組，請使用逗號 (\`,’) 作為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="ec1f7-115">![目錄使用者 - 使用者或群組](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="ec1f7-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="ec1f7-116">按**ENTER**或**] 索引標籤**hello 文字方塊外部。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-116">Press **ENTER** or **TAB** out of hello text box.</span></span> 
6.  <span data-ttu-id="ec1f7-117">確認所有的權限 (**註解**，**註冊**，和**Take Ownership**) 依預設指派 toothese 使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned toothese users or groups by default.</span></span> <span data-ttu-id="ec1f7-118">也就是說，hello 使用者或群組可以[註冊資料資產]( data-catalog-how-to-register.md)，[加上註解的資料資產]( data-catalog-how-to-annotate.md)，和[取得擁有權的資料資產]( data-catalog-how-to-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-118">That is, hello user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="ec1f7-119">![目錄使用者 - 預設權限](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="ec1f7-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="ec1f7-120">使用者或群組的 toogive hello 讀取存取 toohello 類別目錄中，只清除 hello**加上註解**該使用者或群組的選項。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-120">toogive a user or group only hello read access toohello catalog, clear hello **annotate** option for that user or group.</span></span> <span data-ttu-id="ec1f7-121">當您這樣做時，hello 使用者或群組無法標註 hello 目錄中的資料資產，但他們可以檢視它們。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-121">When you do so, hello user or group cannot annotate data assets in hello catalog but they can view them.</span></span> 
8.  <span data-ttu-id="ec1f7-122">toodeny 使用者或群組註冊資料資產清除 hello**註冊**該使用者或群組的選項。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-122">toodeny a user or group from registering data assets, clear hello **register** option for that user or group.</span></span>
9.  <span data-ttu-id="ec1f7-123">使用者從資料資產，清除 hello 的擁有權取得 toodeny**取得擁有權**該使用者或群組的選項。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-123">toodeny a user from taking ownership of a data asset, clear hello **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="ec1f7-124">按一下 [使用者/群組從目錄使用者 toodelete **x** hello 使用者/群組 hello hello 清單底端。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-124">toodelete a user/group from catalog users, click **x** for hello user/group at hello bottom of hello list.</span></span> 
    <span data-ttu-id="ec1f7-125">![目錄使用者 - 刪除使用者](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="ec1f7-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ec1f7-126">我們建議您直接加入安全性群組 toocatalog 使用者，而不是新增使用者並指派權限。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-126">We recommend that you add security groups toocatalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="ec1f7-127">然後，加入使用者 toohello 安全性群組符合其角色和其所需的存取 toohello 類別目錄。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-127">Then, add users toohello security groups that match their roles and their required access toohello catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="ec1f7-128">特殊考量</span><span class="sxs-lookup"><span data-stu-id="ec1f7-128">Special considerations</span></span>

- <span data-ttu-id="ec1f7-129">hello 權限指派給 toosecurity 群組會加總。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-129">hello permissions assigned toosecurity groups are additive.</span></span> <span data-ttu-id="ec1f7-130">假設使用者位於兩個群組中。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-130">Say, a user is in two groups.</span></span> <span data-ttu-id="ec1f7-131">一個群組具有標註權限，而另一個群組沒有標註權限。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="ec1f7-132">那麼，使用者會具有標註權限。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="ec1f7-133">明確指派 tooa 指派的權限 toogroups toowhich hello 使用者所隸屬的使用者覆寫 hello hello 權限。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-133">hello permissions assigned explicitly tooa user override hello permissions assigned toogroups toowhich hello user belongs.</span></span> <span data-ttu-id="ec1f7-134">在 hello 前一個範例中，假設您明確地加入 hello 使用者 toocatalog 使用者和未指派的權限加上註解。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-134">In hello previous example, say, you explicitly added hello user toocatalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="ec1f7-135">hello 使用者無法標註的資料資產，即使 hello 使用者隸屬的群組，沒有加上註解的權限。</span><span class="sxs-lookup"><span data-stu-id="ec1f7-135">hello user cannot annotate data assets even though hello user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec1f7-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec1f7-136">Next steps</span></span>
- [<span data-ttu-id="ec1f7-137">開始使用 Azure 資料目錄</span><span class="sxs-lookup"><span data-stu-id="ec1f7-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

