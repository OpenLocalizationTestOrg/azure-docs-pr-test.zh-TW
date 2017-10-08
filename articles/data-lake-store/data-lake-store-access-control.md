---
title: "資料湖存放區中的存取控制的 aaaOverview |Microsoft 文件"
description: "了解 Azure Data Lake Store 中的存取控制運作方式"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="333fb-103">Azure Data Lake Store 中的存取控制</span><span class="sxs-lookup"><span data-stu-id="333fb-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="333fb-104">Azure Data Lake Store 實作衍生自 HDFS，又衍生自 hello POSIX 存取控制模型的存取控制模型。</span><span class="sxs-lookup"><span data-stu-id="333fb-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from hello POSIX access control model.</span></span> <span data-ttu-id="333fb-105">本文摘要說明 hello hello 存取控制模型的資料湖存放區的基本概念。</span><span class="sxs-lookup"><span data-stu-id="333fb-105">This article summarizes hello basics of hello access control model for Data Lake Store.</span></span> <span data-ttu-id="333fb-106">toolearn 進一步了解 hello HDFS 存取控制模型，請參閱[HDFS 權限指南](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)。</span><span class="sxs-lookup"><span data-stu-id="333fb-106">toolearn more about hello HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="333fb-107">檔案和資料夾的存取控制清單</span><span class="sxs-lookup"><span data-stu-id="333fb-107">Access control lists on files and folders</span></span>

<span data-ttu-id="333fb-108">存取控制清單 (ACL) 有兩種類型，**存取 ACL** 和**預設 ACL**。</span><span class="sxs-lookup"><span data-stu-id="333fb-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="333fb-109">**存取 Acl**： 這些控制項存取 tooan 物件。</span><span class="sxs-lookup"><span data-stu-id="333fb-109">**Access ACLs**: These control access tooan object.</span></span> <span data-ttu-id="333fb-110">檔案和資料夾均有存取 ACL。</span><span class="sxs-lookup"><span data-stu-id="333fb-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="333fb-111">**預設 Acl**: 「 範本 」 的 Acl 判斷 hello 存取 Acl，該資料夾下建立所有子系項目的資料夾與相關聯。</span><span class="sxs-lookup"><span data-stu-id="333fb-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine hello Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="333fb-112">檔案沒有預設 ACL。</span><span class="sxs-lookup"><span data-stu-id="333fb-112">Files do not have Default ACLs.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="333fb-114">存取 Acl 和預設 Acl 有 hello 相同的結構。</span><span class="sxs-lookup"><span data-stu-id="333fb-114">Both Access ACLs and Default ACLs have hello same structure.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="333fb-116">父代上的變更 hello 預設 ACL 不會影響 hello 存取 ACL 或預設的子項目已存在的 ACL。</span><span class="sxs-lookup"><span data-stu-id="333fb-116">Changing hello Default ACL on a parent does not affect hello Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="333fb-117">使用者和身分識別</span><span class="sxs-lookup"><span data-stu-id="333fb-117">Users and identities</span></span>

<span data-ttu-id="333fb-118">每個檔案和資料夾都有這些身分識別的不同權限︰</span><span class="sxs-lookup"><span data-stu-id="333fb-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="333fb-119">hello 擁有 hello 檔案的使用者</span><span class="sxs-lookup"><span data-stu-id="333fb-119">hello owning user of hello file</span></span>
* <span data-ttu-id="333fb-120">hello 擁有的群組</span><span class="sxs-lookup"><span data-stu-id="333fb-120">hello owning group</span></span>
* <span data-ttu-id="333fb-121">具名使用者</span><span class="sxs-lookup"><span data-stu-id="333fb-121">Named users</span></span>
* <span data-ttu-id="333fb-122">具名群組</span><span class="sxs-lookup"><span data-stu-id="333fb-122">Named groups</span></span>
* <span data-ttu-id="333fb-123">所有其他使用者</span><span class="sxs-lookup"><span data-stu-id="333fb-123">All other users</span></span>

<span data-ttu-id="333fb-124">hello 身分識別的使用者和群組是 Azure Active Directory (Azure AD) 身分識別。</span><span class="sxs-lookup"><span data-stu-id="333fb-124">hello identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="333fb-125">因此除非另有說明 」 中的使用者，"hello 內容的資料湖存放區，可以是表示 Azure AD 使用者或 Azure AD 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="333fb-125">So unless otherwise noted, a "user," in hello context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="333fb-126">權限</span><span class="sxs-lookup"><span data-stu-id="333fb-126">Permissions</span></span>

<span data-ttu-id="333fb-127">hello 物件的權限的檔案系統是**讀取**，**寫入**，和**Execute**，也可以用檔案及資料夾 hello 下表所示：</span><span class="sxs-lookup"><span data-stu-id="333fb-127">hello permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in hello following table:</span></span>

|            |    <span data-ttu-id="333fb-128">檔案</span><span class="sxs-lookup"><span data-stu-id="333fb-128">File</span></span>     |   <span data-ttu-id="333fb-129">資料夾</span><span class="sxs-lookup"><span data-stu-id="333fb-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="333fb-130">**讀取 (R)**</span><span class="sxs-lookup"><span data-stu-id="333fb-130">**Read (R)**</span></span> | <span data-ttu-id="333fb-131">可以讀取檔案的 hello 內容</span><span class="sxs-lookup"><span data-stu-id="333fb-131">Can read hello contents of a file</span></span> | <span data-ttu-id="333fb-132">需要**讀取**和**Execute** toolist hello hello 資料夾內容</span><span class="sxs-lookup"><span data-stu-id="333fb-132">Requires **Read** and **Execute** toolist hello contents of hello folder</span></span>|
| <span data-ttu-id="333fb-133">**寫入 (W)**</span><span class="sxs-lookup"><span data-stu-id="333fb-133">**Write (W)**</span></span> | <span data-ttu-id="333fb-134">可以寫入或附加 tooa 檔案</span><span class="sxs-lookup"><span data-stu-id="333fb-134">Can write or append tooa file</span></span> | <span data-ttu-id="333fb-135">需要**寫入**和**Execute** toocreate 資料夾的子系項目</span><span class="sxs-lookup"><span data-stu-id="333fb-135">Requires **Write** and **Execute** toocreate child items in a folder</span></span> |
| <span data-ttu-id="333fb-136">**執行 (X)**</span><span class="sxs-lookup"><span data-stu-id="333fb-136">**Execute (X)**</span></span> | <span data-ttu-id="333fb-137">並不表示 hello 內容資料湖存放區中的任何項目</span><span class="sxs-lookup"><span data-stu-id="333fb-137">Does not mean anything in hello context of Data Lake Store</span></span> | <span data-ttu-id="333fb-138">需要的 tootraverse hello 子資料夾的項目</span><span class="sxs-lookup"><span data-stu-id="333fb-138">Required tootraverse hello child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="333fb-139">權限的簡短形式</span><span class="sxs-lookup"><span data-stu-id="333fb-139">Short forms for permissions</span></span>

<span data-ttu-id="333fb-140">**RWX**是使用的 tooindicate**讀取 + 寫入 + 執行**。</span><span class="sxs-lookup"><span data-stu-id="333fb-140">**RWX** is used tooindicate **Read + Write + Execute**.</span></span> <span data-ttu-id="333fb-141">更緊縮的數字形式存在於其中**讀取 = 4**，**寫入 = 2**，和**Execute = 1**，hello 總和代表 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, hello sum of which represents hello permissions.</span></span> <span data-ttu-id="333fb-142">以下有一些範例。</span><span class="sxs-lookup"><span data-stu-id="333fb-142">Following are some examples.</span></span>

| <span data-ttu-id="333fb-143">數值形式</span><span class="sxs-lookup"><span data-stu-id="333fb-143">Numeric form</span></span> | <span data-ttu-id="333fb-144">簡短形式</span><span class="sxs-lookup"><span data-stu-id="333fb-144">Short form</span></span> |      <span data-ttu-id="333fb-145">意義</span><span class="sxs-lookup"><span data-stu-id="333fb-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="333fb-146">7</span><span class="sxs-lookup"><span data-stu-id="333fb-146">7</span></span>            | <span data-ttu-id="333fb-147">RWX</span><span class="sxs-lookup"><span data-stu-id="333fb-147">RWX</span></span>        | <span data-ttu-id="333fb-148">讀取 + 寫入 + 執行</span><span class="sxs-lookup"><span data-stu-id="333fb-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="333fb-149">5</span><span class="sxs-lookup"><span data-stu-id="333fb-149">5</span></span>            | <span data-ttu-id="333fb-150">R-X</span><span class="sxs-lookup"><span data-stu-id="333fb-150">R-X</span></span>        | <span data-ttu-id="333fb-151">讀取 + 執行</span><span class="sxs-lookup"><span data-stu-id="333fb-151">Read + Execute</span></span>         |
| <span data-ttu-id="333fb-152">4</span><span class="sxs-lookup"><span data-stu-id="333fb-152">4</span></span>            | <span data-ttu-id="333fb-153">R--</span><span class="sxs-lookup"><span data-stu-id="333fb-153">R--</span></span>        | <span data-ttu-id="333fb-154">讀取</span><span class="sxs-lookup"><span data-stu-id="333fb-154">Read</span></span>                   |
| <span data-ttu-id="333fb-155">0</span><span class="sxs-lookup"><span data-stu-id="333fb-155">0</span></span>            | ---        | <span data-ttu-id="333fb-156">沒有權限</span><span class="sxs-lookup"><span data-stu-id="333fb-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="333fb-157">不會繼承權限</span><span class="sxs-lookup"><span data-stu-id="333fb-157">Permissions do not inherit</span></span>

<span data-ttu-id="333fb-158">資料湖存放區所使用的 hello POSIX 樣式模型，在權限的項目會儲存 hello 項目本身上。</span><span class="sxs-lookup"><span data-stu-id="333fb-158">In hello POSIX-style model that's used by Data Lake Store, permissions for an item are stored on hello item itself.</span></span> <span data-ttu-id="333fb-159">換句話說，無法繼承項目的權限，從 hello 父項目。</span><span class="sxs-lookup"><span data-stu-id="333fb-159">In other words, permissions for an item cannot be inherited from hello parent items.</span></span>

## <a name="common-scenarios-related-toopermissions"></a><span data-ttu-id="333fb-160">常見的案例相關的 toopermissions</span><span class="sxs-lookup"><span data-stu-id="333fb-160">Common scenarios related toopermissions</span></span>

<span data-ttu-id="333fb-161">以下是一些常見的案例 toohelp 您了解哪些權限需要 tooperform Data Lake Store 帳戶上的特定作業。</span><span class="sxs-lookup"><span data-stu-id="333fb-161">Following are some common scenarios toohelp you understand which permissions are needed tooperform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-tooread-a-file"></a><span data-ttu-id="333fb-162">需要 tooread 檔案權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-162">Permissions needed tooread a file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="333fb-164">Hello 檔案 toobe 讀取，如 hello 呼叫端需要**讀取**權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-164">For hello file toobe read, hello caller needs **Read** permissions.</span></span>
* <span data-ttu-id="333fb-165">針對所有 hello hello 資料夾結構中包含 hello 檔案的資料夾，hello 呼叫端需要**Execute**權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-165">For all hello folders in hello folder structure that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-tooappend-tooa-file"></a><span data-ttu-id="333fb-166">需要 tooappend tooa 檔案權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-166">Permissions needed tooappend tooa file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="333fb-168">Hello 檔案 toobe 附加到，如 hello 呼叫端需要**寫入**權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-168">For hello file toobe appended to, hello caller needs **Write** permissions.</span></span>
* <span data-ttu-id="333fb-169">針對所有 hello 包含 hello 檔案的資料夾，hello 呼叫端需要**Execute**權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-169">For all hello folders that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-toodelete-a-file"></a><span data-ttu-id="333fb-170">需要 toodelete 檔案權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-170">Permissions needed toodelete a file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="333fb-172">Hello 父資料夾，hello 呼叫端需要**寫入 + 執行**權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-172">For hello parent folder, hello caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="333fb-173">針對所有 hello hello 檔案的路徑中的其他資料夾，hello 呼叫端需要**Execute**權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-173">For all hello other folders in hello file’s path, hello caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="333fb-174">撰寫 hello 檔案的權限不需要的 toodelete 它只要 hello 先前的兩個條件都成立。</span><span class="sxs-lookup"><span data-stu-id="333fb-174">Write permissions on hello file are not required toodelete it as long as hello previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a><span data-ttu-id="333fb-175">需要 tooenumerate 資料夾權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-175">Permissions needed tooenumerate a folder</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="333fb-177">Hello 資料夾 tooenumerate，如 hello 呼叫端需要**讀取 + Execute**權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-177">For hello folder tooenumerate, hello caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="333fb-178">針對所有 hello 上階資料夾，hello 呼叫端需要**Execute**權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-178">For all hello ancestor folders, hello caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-hello-azure-portal"></a><span data-ttu-id="333fb-179">在 hello Azure 入口網站中的檢視權限</span><span class="sxs-lookup"><span data-stu-id="333fb-179">Viewing permissions in hello Azure portal</span></span>

<span data-ttu-id="333fb-180">從 hello**資料總管**刀鋒視窗中的 hello Data Lake Store 帳戶按一下**存取**toosee hello Acl 的檔案或資料夾。</span><span class="sxs-lookup"><span data-stu-id="333fb-180">From hello **Data Explorer** blade of hello Data Lake Store account, click **Access** toosee hello ACLs for a file or a folder.</span></span> <span data-ttu-id="333fb-181">按一下**存取**toosee hello Acl hello**目錄**下 hello 資料夾**mydatastore**帳戶。</span><span class="sxs-lookup"><span data-stu-id="333fb-181">Click **Access** toosee hello ACLs for hello **catalog** folder under hello **mydatastore** account.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="333fb-183">在這個刀鋒視窗中，hello 頂部區段會顯示 hello 具備權限，您的概觀。</span><span class="sxs-lookup"><span data-stu-id="333fb-183">On this blade, hello top section shows an overview of hello permissions that you have.</span></span> <span data-ttu-id="333fb-184">（在 hello 螢幕擷取畫面，hello 使用者是 Bob）。接下來，會顯示 hello 存取權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-184">(In hello screenshot, hello user is Bob.) Following that, hello access permissions are shown.</span></span> <span data-ttu-id="333fb-185">在這之後，從 hello**存取**刀鋒視窗中，按一下 **簡單檢視**toosee hello 較簡單的檢視。</span><span class="sxs-lookup"><span data-stu-id="333fb-185">After that, from hello **Access** blade, click **Simple View** toosee hello simpler view.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="333fb-187">按一下**進階檢視**toosee hello 更進階的檢視，其中會顯示 hello 概念的預設 Acl、 遮罩和超級使用者。</span><span class="sxs-lookup"><span data-stu-id="333fb-187">Click **Advanced View** toosee hello more advanced view, where hello concepts of Default ACLs, mask, and super-user are shown.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a><span data-ttu-id="333fb-189">hello 超級使用者</span><span class="sxs-lookup"><span data-stu-id="333fb-189">hello super-user</span></span>

<span data-ttu-id="333fb-190">超級使用者具有 hello 大部分的權限的所有 hello 使用者 hello 資料湖存放區中。</span><span class="sxs-lookup"><span data-stu-id="333fb-190">A super-user has hello most rights of all hello users in hello Data Lake Store.</span></span> <span data-ttu-id="333fb-191">超級使用者：</span><span class="sxs-lookup"><span data-stu-id="333fb-191">A super-user:</span></span>

* <span data-ttu-id="333fb-192">也有 RWX 權限**所有**檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="333fb-192">Has RWX Permissions too**all** files and folders.</span></span>
* <span data-ttu-id="333fb-193">可以變更任何檔案或資料夾的 「 hello 」 權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-193">Can change hello permissions on any file or folder.</span></span>
* <span data-ttu-id="333fb-194">可以變更 hello 擁有使用者或擁有的任何檔案或資料夾的群組。</span><span class="sxs-lookup"><span data-stu-id="333fb-194">Can change hello owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="333fb-195">在 Azure 中，Data Lake Store 帳戶具有數個 Azure 角色，包括︰</span><span class="sxs-lookup"><span data-stu-id="333fb-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="333fb-196">擁有者</span><span class="sxs-lookup"><span data-stu-id="333fb-196">Owners</span></span>
* <span data-ttu-id="333fb-197">參與者</span><span class="sxs-lookup"><span data-stu-id="333fb-197">Contributors</span></span>
* <span data-ttu-id="333fb-198">讀取者</span><span class="sxs-lookup"><span data-stu-id="333fb-198">Readers</span></span>

<span data-ttu-id="333fb-199">所有人 hello**擁有者**Data Lake Store 帳戶的角色會自動超級使用者該帳戶。</span><span class="sxs-lookup"><span data-stu-id="333fb-199">Everyone in hello **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="333fb-200">詳細資訊，請參閱 toolearn[角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="333fb-200">toolearn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="333fb-201">如果您想 toocreate 超級使用者權限的自訂角色型存取控制 (RBAC) 角色，它會需要下列權限的 toohave hello:</span><span class="sxs-lookup"><span data-stu-id="333fb-201">If you want toocreate a custom role-based-access control (RBAC) role that has super-user permissions, it needs toohave hello following permissions:</span></span>
- <span data-ttu-id="333fb-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="333fb-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="333fb-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="333fb-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="hello-owning-user"></a><span data-ttu-id="333fb-204">hello 擁有使用者</span><span class="sxs-lookup"><span data-stu-id="333fb-204">hello owning user</span></span>

<span data-ttu-id="333fb-205">建立 hello 項目 hello 使用者會自動為 hello 擁有 hello 項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="333fb-205">hello user who created hello item is automatically hello owning user of hello item.</span></span> <span data-ttu-id="333fb-206">擁有使用者可以︰</span><span class="sxs-lookup"><span data-stu-id="333fb-206">An owning user can:</span></span>

* <span data-ttu-id="333fb-207">變更 hello 檔案擁有者權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-207">Change hello permissions of a file that is owned.</span></span>
* <span data-ttu-id="333fb-208">變更 hello 只要 hello 擁有使用者也是 hello 目標群組的成員擁有的擁有的檔案群組。</span><span class="sxs-lookup"><span data-stu-id="333fb-208">Change hello owning group of a file that is owned, as long as hello owning user is also a member of hello target group.</span></span>

> [!NOTE]
> <span data-ttu-id="333fb-209">擁有使用者的 hello*無法*變更 hello 擁有另一個擁有檔案的使用者。</span><span class="sxs-lookup"><span data-stu-id="333fb-209">hello owning user *cannot* change hello owning user of another owned file.</span></span> <span data-ttu-id="333fb-210">只有超級使用者可以變更 hello 擁有檔案或資料夾的使用者。</span><span class="sxs-lookup"><span data-stu-id="333fb-210">Only super-users can change hello owning user of a file or folder.</span></span>
>
>

## <a name="hello-owning-group"></a><span data-ttu-id="333fb-211">hello 擁有的群組</span><span class="sxs-lookup"><span data-stu-id="333fb-211">hello owning group</span></span>

<span data-ttu-id="333fb-212">Hello POSIX Acl，在每個使用者都與 「 主要群組 」。</span><span class="sxs-lookup"><span data-stu-id="333fb-212">In hello POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="333fb-213">例如，使用者"alice"可能屬於 toohello"finance"群組。</span><span class="sxs-lookup"><span data-stu-id="333fb-213">For example, user "alice" might belong toohello "finance" group.</span></span> <span data-ttu-id="333fb-214">Alice 也可能屬於 toomultiple 群組，但有一個群組一律指定做為其主要群組。</span><span class="sxs-lookup"><span data-stu-id="333fb-214">Alice might also belong toomultiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="333fb-215">在 POSIX，Alice 建立檔案，當 hello 擁有該檔案群組的設定 tooher 主要群組，在此情況下為"finance"。</span><span class="sxs-lookup"><span data-stu-id="333fb-215">In POSIX, when Alice creates a file, hello owning group of that file is set tooher primary group, which in this case is "finance."</span></span>

<span data-ttu-id="333fb-216">建立新的檔案系統項目時，資料湖存放區會指派值 toohello 擁有群組。</span><span class="sxs-lookup"><span data-stu-id="333fb-216">When a new filesystem item is created, Data Lake Store assigns a value toohello owning group.</span></span>

* <span data-ttu-id="333fb-217">**案例 1**: hello 根資料夾"/"。</span><span class="sxs-lookup"><span data-stu-id="333fb-217">**Case 1**: hello root folder "/".</span></span> <span data-ttu-id="333fb-218">建立 Data Lake Store 帳戶時，會建立這個資料夾。</span><span class="sxs-lookup"><span data-stu-id="333fb-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="333fb-219">在此情況下，擁有 hello 的群組設定建立 hello 帳戶 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="333fb-219">In this case, hello owning group is set toohello user who created hello account.</span></span>
* <span data-ttu-id="333fb-220">**案例 2** （每個其他情況下）： hello 擁有的群組建立新的項目時，會複製從 hello 父資料夾。</span><span class="sxs-lookup"><span data-stu-id="333fb-220">**Case 2** (Every other case): When a new item is created, hello owning group is copied from hello parent folder.</span></span>

<span data-ttu-id="333fb-221">可以變更 hello 擁有的群組：</span><span class="sxs-lookup"><span data-stu-id="333fb-221">hello owning group can be changed by:</span></span>
* <span data-ttu-id="333fb-222">任何超級使用者。</span><span class="sxs-lookup"><span data-stu-id="333fb-222">Any super-users.</span></span>
* <span data-ttu-id="333fb-223">如果 hello 擁有使用者也是 hello 目標群組的成員擁有的使用者，hello。</span><span class="sxs-lookup"><span data-stu-id="333fb-223">hello owning user, if hello owning user is also a member of hello target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="333fb-224">存取檢查演算法</span><span class="sxs-lookup"><span data-stu-id="333fb-224">Access check algorithm</span></span>

<span data-ttu-id="333fb-225">下列圖例的 hello 代表 hello Data Lake Store 帳戶的存取檢查演算法。</span><span class="sxs-lookup"><span data-stu-id="333fb-225">hello following illustration represents hello access check algorithm for Data Lake Store accounts.</span></span>

![Data Lake Store ACL 演算法](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a><span data-ttu-id="333fb-227">hello 遮罩及 「 有效權限 」</span><span class="sxs-lookup"><span data-stu-id="333fb-227">hello mask and "effective permissions"</span></span>

<span data-ttu-id="333fb-228">hello**遮罩**是 RWX 值都會使用的 toolimit 存取**具名使用者**，hello**擁有群組**，和**具名群組**時執行 hello 存取檢查演算法。</span><span class="sxs-lookup"><span data-stu-id="333fb-228">hello **mask** is an RWX value that is used toolimit access for **named users**, hello **owning group**, and **named groups** when you're performing hello access check algorithm.</span></span> <span data-ttu-id="333fb-229">以下是 hello 的 hello 遮罩的重要概念。</span><span class="sxs-lookup"><span data-stu-id="333fb-229">Here are hello key concepts for hello mask.</span></span>

* <span data-ttu-id="333fb-230">hello 遮罩會建立 「 有效權限。 」</span><span class="sxs-lookup"><span data-stu-id="333fb-230">hello mask creates "effective permissions."</span></span> <span data-ttu-id="333fb-231">也就是會修改 hello 權限的存取檢查 hello 次。</span><span class="sxs-lookup"><span data-stu-id="333fb-231">That is, it modifies hello permissions at hello time of access check.</span></span>
* <span data-ttu-id="333fb-232">hello 遮罩可以直接編輯 hello 檔案擁有者和任何超級使用者。</span><span class="sxs-lookup"><span data-stu-id="333fb-232">hello mask can be directly edited by hello file owner and any super-users.</span></span>
* <span data-ttu-id="333fb-233">hello 遮罩可以移除權限 toocreate hello 有效權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-233">hello mask can remove permissions toocreate hello effective permission.</span></span> <span data-ttu-id="333fb-234">hello 遮罩*無法*新增權限 toohello 有效權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-234">hello mask *cannot* add permissions toohello effective permission.</span></span>

<span data-ttu-id="333fb-235">讓我們看看一些範例。</span><span class="sxs-lookup"><span data-stu-id="333fb-235">Let's look at some examples.</span></span> <span data-ttu-id="333fb-236">在下列範例的 hello，hello 遮罩設定太**RWX**，這表示該 hello 遮罩，不會移除任何權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-236">In hello following example, hello mask is set too**RWX**, which means that hello mask does not remove any permissions.</span></span> <span data-ttu-id="333fb-237">hello hello 具名使用者擁有的群組，和名為群組的有效權限不會改變 hello 存取檢查期間。</span><span class="sxs-lookup"><span data-stu-id="333fb-237">hello effective permissions for hello named user, owning group, and named group are not altered during hello access check.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="333fb-239">在下列範例的 hello，hello 遮罩設定太**R-X**。</span><span class="sxs-lookup"><span data-stu-id="333fb-239">In hello following example, hello mask is set too**R-X**.</span></span> <span data-ttu-id="333fb-240">這表示它**關閉 hello 寫入權限**如**具名使用者**，**擁有群組**，和**具名群組**時存取的 hello請檢查。</span><span class="sxs-lookup"><span data-stu-id="333fb-240">This means that it **turns off hello Write permissions** for **named user**, **owning group**, and **named group** at hello time of access check.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="333fb-242">如需參考，以下是檔案或資料夾的 hello 遮罩 hello Azure 入口網站中出現的位置。</span><span class="sxs-lookup"><span data-stu-id="333fb-242">For reference, here is where hello mask for a file or folder appears in hello Azure portal.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="333fb-244">新的 Data Lake Store 帳戶、 hello 存取 ACL 的 hello 遮罩和預設 ACL 的 hello 根資料夾 （"/"） 會預設 tooRWX。</span><span class="sxs-lookup"><span data-stu-id="333fb-244">For a new Data Lake Store account, hello mask for hello Access ACL and Default ACL of hello root folder ("/") defaults tooRWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="333fb-245">新檔案和資料夾的權限</span><span class="sxs-lookup"><span data-stu-id="333fb-245">Permissions on new files and folders</span></span>

<span data-ttu-id="333fb-246">建立新的檔案或資料夾時在現有的資料夾下，判斷 hello hello 父資料夾上的預設 ACL:</span><span class="sxs-lookup"><span data-stu-id="333fb-246">When a new file or folder is created under an existing folder, hello Default ACL on hello parent folder determines:</span></span>

- <span data-ttu-id="333fb-247">子資料夾的預設 ACL 與存取 ACL。</span><span class="sxs-lookup"><span data-stu-id="333fb-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="333fb-248">子檔案的存取 ACL (檔案沒有預設 ACL)。</span><span class="sxs-lookup"><span data-stu-id="333fb-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="hello-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="333fb-249">hello 存取子檔案或資料夾的 ACL</span><span class="sxs-lookup"><span data-stu-id="333fb-249">hello Access ACL of a child file or folder</span></span>

<span data-ttu-id="333fb-250">建立子檔案或資料夾時，父代 hello 預設 ACL 複製 hello hello 子檔案或資料夾的存取 ACL。</span><span class="sxs-lookup"><span data-stu-id="333fb-250">When a child file or folder is created, hello parent's Default ACL is copied as hello Access ACL of hello child file or folder.</span></span> <span data-ttu-id="333fb-251">此外，如果**其他**使用者在 hello 父預設 ACL 有 RWX 權限，就會移除從 hello 子系項目的存取 ACL。</span><span class="sxs-lookup"><span data-stu-id="333fb-251">Also, if **other** user has RWX permissions in hello parent's default ACL, it is removed from hello child item's Access ACL.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="333fb-253">在大部分情況下，hello 先前的資訊會是所有您需要有關如何判斷子系項目的存取 ACL tooknow。</span><span class="sxs-lookup"><span data-stu-id="333fb-253">In most scenarios, hello previous information is all you need tooknow about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="333fb-254">不過，如果您很熟悉與 POSIX 系統和想 toounderstand 深入了解如何達成這項轉換，請參閱 hello 節[Umask 的角色中建立新的檔案及資料夾的 hello 存取 ACL](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders)本文稍後。</span><span class="sxs-lookup"><span data-stu-id="333fb-254">However, if you are familiar with POSIX systems and want toounderstand in-depth how this transformation is achieved, see hello section [Umask’s role in creating hello Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="333fb-255">子資料夾的預設 ACL</span><span class="sxs-lookup"><span data-stu-id="333fb-255">A child folder's Default ACL</span></span>

<span data-ttu-id="333fb-256">父資料夾下建立子資料夾時，hello 父資料夾的預設 ACL 會透過複製，因為是 toohello 子資料夾的預設 ACL。</span><span class="sxs-lookup"><span data-stu-id="333fb-256">When a child folder is created under a parent folder, hello parent folder's Default ACL is copied over as is toohello child folder's Default ACL.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="333fb-258">可供了解 Data Lake Store 中 ACL 的進階主題</span><span class="sxs-lookup"><span data-stu-id="333fb-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="333fb-259">以下是一些您了解如何判斷 Acl 的 Data Lake Store 檔案或資料夾的進階的主題 toohelp。</span><span class="sxs-lookup"><span data-stu-id="333fb-259">Following are some advanced topics toohelp you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a><span data-ttu-id="333fb-260">建立新的檔案及資料夾的 hello 存取 ACL Umask 的角色</span><span class="sxs-lookup"><span data-stu-id="333fb-260">Umask’s role in creating hello Access ACL for new files and folders</span></span>

<span data-ttu-id="333fb-261">在 POSIX 相容的系統中，hello 一般概念是該 umask hello 父資料夾的已使用 tootransform hello 權限 9 位元值**擁有使用者**，**擁有群組**，和**其他**hello 存取新的子檔案或資料夾的 ACL 上。</span><span class="sxs-lookup"><span data-stu-id="333fb-261">In a POSIX-compliant system, hello general concept is that umask is a 9-bit value on hello parent folder that's used tootransform hello permission for **owning user**, **owning group**, and **other** on hello Access ACL of a new child file or folder.</span></span> <span data-ttu-id="333fb-262">umask hello 位元會識別哪一個位元 tooturn 關閉 hello 子系項目的存取 ACL 中。</span><span class="sxs-lookup"><span data-stu-id="333fb-262">hello bits of a umask identify which bits tooturn off in hello child item’s Access ACL.</span></span> <span data-ttu-id="333fb-263">因此，它都會使用 tooselectively 防止 hello 傳播的權限**擁有使用者**，**擁有群組**，和**其他**。</span><span class="sxs-lookup"><span data-stu-id="333fb-263">Thus it is used tooselectively prevent hello propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="333fb-264">Hello umask 在 HDFS 系統中，通常是由系統管理員所控制的 sitewide 組態選項。</span><span class="sxs-lookup"><span data-stu-id="333fb-264">In an HDFS system, hello umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="333fb-265">Data Lake Store 會使用無法變更的 **全帳戶 umask** 。</span><span class="sxs-lookup"><span data-stu-id="333fb-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="333fb-266">下列表格顯示 hello hello 取消遮罩的資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="333fb-266">hello following table shows hello unmask for Data Lake Store.</span></span>

| <span data-ttu-id="333fb-267">使用者群組</span><span class="sxs-lookup"><span data-stu-id="333fb-267">User group</span></span>  | <span data-ttu-id="333fb-268">設定</span><span class="sxs-lookup"><span data-stu-id="333fb-268">Setting</span></span> | <span data-ttu-id="333fb-269">對新的子項目的存取 ACL 的影響</span><span class="sxs-lookup"><span data-stu-id="333fb-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="333fb-270">擁有使用者</span><span class="sxs-lookup"><span data-stu-id="333fb-270">Owning user</span></span> | ---     | <span data-ttu-id="333fb-271">沒有影響</span><span class="sxs-lookup"><span data-stu-id="333fb-271">No effect</span></span>                             |
| <span data-ttu-id="333fb-272">擁有群組</span><span class="sxs-lookup"><span data-stu-id="333fb-272">Owning group</span></span>| ---     | <span data-ttu-id="333fb-273">沒有影響</span><span class="sxs-lookup"><span data-stu-id="333fb-273">No effect</span></span>                             |
| <span data-ttu-id="333fb-274">其他</span><span class="sxs-lookup"><span data-stu-id="333fb-274">Other</span></span>       | <span data-ttu-id="333fb-275">RWX</span><span class="sxs-lookup"><span data-stu-id="333fb-275">RWX</span></span>     | <span data-ttu-id="333fb-276">移除讀取 + 寫入 + 執行</span><span class="sxs-lookup"><span data-stu-id="333fb-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="333fb-277">hello 下列圖例顯示此 umask 作用中。</span><span class="sxs-lookup"><span data-stu-id="333fb-277">hello following illustration shows this umask in action.</span></span> <span data-ttu-id="333fb-278">hello 效果是 tooremove**讀取 + 寫入 + 執行**如**其他**使用者。</span><span class="sxs-lookup"><span data-stu-id="333fb-278">hello net effect is tooremove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="333fb-279">因為 hello umask 未指定的位元**擁有使用者**和**擁有群組**，不會轉換這些權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-279">Because hello umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a><span data-ttu-id="333fb-281">hello 自黏便箋的位元</span><span class="sxs-lookup"><span data-stu-id="333fb-281">hello sticky bit</span></span>

<span data-ttu-id="333fb-282">hello 自黏便箋的位元為 POSIX filesystem 更進階的功能。</span><span class="sxs-lookup"><span data-stu-id="333fb-282">hello sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="333fb-283">在 hello 內容中的資料湖存放區，不太需要該 hello 自黏便箋的位元。</span><span class="sxs-lookup"><span data-stu-id="333fb-283">In hello context of Data Lake Store, it is unlikely that hello sticky bit will be needed.</span></span>

<span data-ttu-id="333fb-284">hello 下表顯示 hello 自黏便箋的位元資料湖存放區中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="333fb-284">hello following table shows how hello sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="333fb-285">使用者群組</span><span class="sxs-lookup"><span data-stu-id="333fb-285">User group</span></span>         | <span data-ttu-id="333fb-286">檔案</span><span class="sxs-lookup"><span data-stu-id="333fb-286">File</span></span>    | <span data-ttu-id="333fb-287">資料夾</span><span class="sxs-lookup"><span data-stu-id="333fb-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="333fb-288">黏性位元 **OFF**</span><span class="sxs-lookup"><span data-stu-id="333fb-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="333fb-289">沒有影響</span><span class="sxs-lookup"><span data-stu-id="333fb-289">No effect</span></span>   | <span data-ttu-id="333fb-290">沒有影響。</span><span class="sxs-lookup"><span data-stu-id="333fb-290">No effect.</span></span>           |
| <span data-ttu-id="333fb-291">黏性位元 **ON**</span><span class="sxs-lookup"><span data-stu-id="333fb-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="333fb-292">沒有影響</span><span class="sxs-lookup"><span data-stu-id="333fb-292">No effect</span></span>   | <span data-ttu-id="333fb-293">防止以外的任何人**超級使用者**和 hello**擁有使用者**項目的刪除或重新命名該子項目。</span><span class="sxs-lookup"><span data-stu-id="333fb-293">Prevents anyone except **super-users** and hello **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="333fb-294">hello 自黏便箋的位元不會顯示 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="333fb-294">hello sticky bit is not shown in hello Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="333fb-295">Data Lake Store 中 ACL 的相關常見問題</span><span class="sxs-lookup"><span data-stu-id="333fb-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="333fb-296">以下是有關 Data Lake Store 中 ACL 的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="333fb-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-tooenable-support-for-acls"></a><span data-ttu-id="333fb-297">是否有 Acl tooenable 支援？</span><span class="sxs-lookup"><span data-stu-id="333fb-297">Do I have tooenable support for ACLs?</span></span>

<span data-ttu-id="333fb-298">否。</span><span class="sxs-lookup"><span data-stu-id="333fb-298">No.</span></span> <span data-ttu-id="333fb-299">Data Lake Store 帳戶一律會啟用透過 ACL 的存取控制。</span><span class="sxs-lookup"><span data-stu-id="333fb-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="333fb-300">需要的 toorecursively 刪除的資料夾和其內容的權限？</span><span class="sxs-lookup"><span data-stu-id="333fb-300">Which permissions are required toorecursively delete a folder and its contents?</span></span>

* <span data-ttu-id="333fb-301">hello 父資料夾必須要有**寫入 + 執行**權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-301">hello parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="333fb-302">hello 資料夾 toobe 刪除，而且每個資料夾內，需要**讀取 + 寫入 + 執行**權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-302">hello folder toobe deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="333fb-303">您不需要寫入權限 toodelete 檔案資料夾中。</span><span class="sxs-lookup"><span data-stu-id="333fb-303">You do not need Write permissions toodelete files in folders.</span></span> <span data-ttu-id="333fb-304">此外，hello 根資料夾"/"可以**從未**被刪除。</span><span class="sxs-lookup"><span data-stu-id="333fb-304">Also, hello root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a><span data-ttu-id="333fb-305">Hello 的檔案或資料夾的擁有者是誰？</span><span class="sxs-lookup"><span data-stu-id="333fb-305">Who is hello owner of a file or folder?</span></span>

<span data-ttu-id="333fb-306">hello 的檔案或資料夾的建立者變成 hello 擁有者。</span><span class="sxs-lookup"><span data-stu-id="333fb-306">hello creator of a file or folder becomes hello owner.</span></span>

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="333fb-307">哪些群組是設定為 hello 擁有的檔案或資料夾，在建立群組？</span><span class="sxs-lookup"><span data-stu-id="333fb-307">Which group is set as hello owning group of a file or folder at creation?</span></span>

<span data-ttu-id="333fb-308">從擁有 hello 父資料夾下的 hello 新檔案或資料夾建立群組的 hello 複製 hello 擁有的群組。</span><span class="sxs-lookup"><span data-stu-id="333fb-308">hello owning group is copied from hello owning group of hello parent folder under which hello new file or folder is created.</span></span>

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="333fb-309">我是 hello 擁有檔案的使用者，但沒有需要的 hello RWX 權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-309">I am hello owning user of a file but I don’t have hello RWX permissions I need.</span></span> <span data-ttu-id="333fb-310">該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="333fb-310">What do I do?</span></span>

<span data-ttu-id="333fb-311">hello 擁有使用者可以變更 hello 權限的 hello 檔案 toogive 本身所需的任何 RWX 權限。</span><span class="sxs-lookup"><span data-stu-id="333fb-311">hello owning user can change hello permissions of hello file toogive themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="333fb-312">當我查看 Acl hello Azure 入口網站中，我看到使用者名稱，但透過應用程式開發介面，看 Guid，為什麼？</span><span class="sxs-lookup"><span data-stu-id="333fb-312">When I look at ACLs in hello Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="333fb-313">Hello Acl 中的項目會儲存為對應 toousers 在 Azure AD 中的 Guid。</span><span class="sxs-lookup"><span data-stu-id="333fb-313">Entries in hello ACLs are stored as GUIDs that correspond toousers in Azure AD.</span></span> <span data-ttu-id="333fb-314">hello Api 傳回 hello Guid 原狀。</span><span class="sxs-lookup"><span data-stu-id="333fb-314">hello APIs return hello GUIDs as is.</span></span> <span data-ttu-id="333fb-315">hello Azure 入口網站嘗試 toomake Acl 更容易 toouse 所轉譯的 hello Guid 為盡可能的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="333fb-315">hello Azure portal tries toomake ACLs easier toouse by translating hello GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a><span data-ttu-id="333fb-316">為何有時候會看到 hello Acl 中的 Guid 當我使用 hello Azure 入口網站？</span><span class="sxs-lookup"><span data-stu-id="333fb-316">Why do I sometimes see GUIDs in hello ACLs when I'm using hello Azure portal?</span></span>

<span data-ttu-id="333fb-317">當 hello 使用者不在 Azure AD 中不再存在時，會顯示 GUID。</span><span class="sxs-lookup"><span data-stu-id="333fb-317">A GUID is shown when hello user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="333fb-318">這通常是因為當 hello 使用者已離開 hello 公司，或已從 Azure AD 中刪除其帳戶。</span><span class="sxs-lookup"><span data-stu-id="333fb-318">Usually this happens when hello user has left hello company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="333fb-319">Data Lake Store 是否支援 ACL 的繼承？</span><span class="sxs-lookup"><span data-stu-id="333fb-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="333fb-320">否。</span><span class="sxs-lookup"><span data-stu-id="333fb-320">No.</span></span>

### <a name="what-is-hello-difference-between-mask-and-umask"></a><span data-ttu-id="333fb-321">Hello 遮罩與 umask 之間的差異為何？</span><span class="sxs-lookup"><span data-stu-id="333fb-321">What is hello difference between mask and umask?</span></span>

| <span data-ttu-id="333fb-322">遮罩</span><span class="sxs-lookup"><span data-stu-id="333fb-322">mask</span></span> | <span data-ttu-id="333fb-323">umask</span><span class="sxs-lookup"><span data-stu-id="333fb-323">umask</span></span>|
|------|------|
| <span data-ttu-id="333fb-324">hello**遮罩**屬性上可用的每個檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="333fb-324">hello **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="333fb-325">hello **umask**是 hello Data Lake Store 帳戶的屬性。</span><span class="sxs-lookup"><span data-stu-id="333fb-325">hello **umask** is a property of hello Data Lake Store account.</span></span> <span data-ttu-id="333fb-326">因此會有只有單一 umask hello 資料湖存放區中。</span><span class="sxs-lookup"><span data-stu-id="333fb-326">So there is only a single umask in hello Data Lake Store.</span></span>    |
| <span data-ttu-id="333fb-327">可以更改 hello 擁有使用者或擁有的檔案或超級使用者的群組上的檔案或資料夾的 hello 遮罩屬性。</span><span class="sxs-lookup"><span data-stu-id="333fb-327">hello mask property on a file or folder can be altered by hello owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="333fb-328">hello umask 屬性無法修改任何使用者，即使超級使用者。</span><span class="sxs-lookup"><span data-stu-id="333fb-328">hello umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="333fb-329">這是不能變更的常數值。</span><span class="sxs-lookup"><span data-stu-id="333fb-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="333fb-330">hello 遮罩屬性會使用於 hello 存取檢查演算法在執行階段 toodetermine 使用者是否具有 hello 右 tooperform 檔案或資料夾中的作業。</span><span class="sxs-lookup"><span data-stu-id="333fb-330">hello mask property is used during hello access check algorithm at runtime toodetermine whether a user has hello right tooperform on operation on a file or folder.</span></span> <span data-ttu-id="333fb-331">hello 遮罩的 hello 角色時的存取檢查 hello 是 toocreate 「 有效權限 」。</span><span class="sxs-lookup"><span data-stu-id="333fb-331">hello role of hello mask is toocreate "effective permissions" at hello time of access check.</span></span> | <span data-ttu-id="333fb-332">hello umask 不在所有使用存取檢查期間。</span><span class="sxs-lookup"><span data-stu-id="333fb-332">hello umask is not used during access check at all.</span></span> <span data-ttu-id="333fb-333">hello umask 為使用的 toodetermine hello 存取 ACL 的新子資料夾的項目。</span><span class="sxs-lookup"><span data-stu-id="333fb-333">hello umask is used toodetermine hello Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="333fb-334">hello 遮罩是 hello 時間的存取檢查會在套用 toonamed 使用者，具名的群組和擁有使用者的 3 位元 RWX 值。</span><span class="sxs-lookup"><span data-stu-id="333fb-334">hello mask is a 3-bit RWX value that applies toonamed user, named group, and owning user at hello time of access check.</span></span>| <span data-ttu-id="333fb-335">hello umask 是 9 位元值，適用於擁有擁有 群組中，使用者 toohello 和**其他**新子系。</span><span class="sxs-lookup"><span data-stu-id="333fb-335">hello umask is a 9-bit value that applies toohello owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="333fb-336">何處可以進一步了解 POSIX 存取控制模型？</span><span class="sxs-lookup"><span data-stu-id="333fb-336">Where can I learn more about POSIX access control model?</span></span>

* [<span data-ttu-id="333fb-337">Linux 上的 POSIX 存取控制清單</span><span class="sxs-lookup"><span data-stu-id="333fb-337">POSIX Access Control Lists on Linux</span></span>](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [<span data-ttu-id="333fb-338">HDFS 權限指南</span><span class="sxs-lookup"><span data-stu-id="333fb-338">HDFS permission guide</span></span>](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [<span data-ttu-id="333fb-339">POSIX 常見問題集</span><span class="sxs-lookup"><span data-stu-id="333fb-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="333fb-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="333fb-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="333fb-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="333fb-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="333fb-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="333fb-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="333fb-343">Ubuntu 上的 POSIX ACL</span><span class="sxs-lookup"><span data-stu-id="333fb-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* [<span data-ttu-id="333fb-344">Linux 上使用存取控制清單的 ACL</span><span class="sxs-lookup"><span data-stu-id="333fb-344">ACL using access control lists on Linux</span></span>](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a><span data-ttu-id="333fb-345">另請參閱</span><span class="sxs-lookup"><span data-stu-id="333fb-345">See also</span></span>

* [<span data-ttu-id="333fb-346">Azure Data Lake Store 概觀</span><span class="sxs-lookup"><span data-stu-id="333fb-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
