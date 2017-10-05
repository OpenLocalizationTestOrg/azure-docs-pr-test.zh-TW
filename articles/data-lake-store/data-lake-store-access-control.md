---
title: "Data Lake Store 中的存取控制概觀 | Microsoft Docs"
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
ms.openlocfilehash: 99fbad770290d280bdec490d988391ad276ce1ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="cfe73-103">Azure Data Lake Store 中的存取控制</span><span class="sxs-lookup"><span data-stu-id="cfe73-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="cfe73-104">Azure Data Lake Store 實作的存取控制模型衍生自 HDFS，而 HDFS 又衍生自 POSIX 存取控制模型。</span><span class="sxs-lookup"><span data-stu-id="cfe73-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from the POSIX access control model.</span></span> <span data-ttu-id="cfe73-105">本文摘要說明 Data Lake Store 存取控制模型的基本概念。</span><span class="sxs-lookup"><span data-stu-id="cfe73-105">This article summarizes the basics of the access control model for Data Lake Store.</span></span> <span data-ttu-id="cfe73-106">若要深入了解 HDFS 存取控制模型，請參閱 [HDFS 權限指南](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)。</span><span class="sxs-lookup"><span data-stu-id="cfe73-106">To learn more about the HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="cfe73-107">檔案和資料夾的存取控制清單</span><span class="sxs-lookup"><span data-stu-id="cfe73-107">Access control lists on files and folders</span></span>

<span data-ttu-id="cfe73-108">存取控制清單 (ACL) 有兩種類型，**存取 ACL** 和**預設 ACL**。</span><span class="sxs-lookup"><span data-stu-id="cfe73-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="cfe73-109">**存取 ACL**：這些控制物件的存取權。</span><span class="sxs-lookup"><span data-stu-id="cfe73-109">**Access ACLs**: These control access to an object.</span></span> <span data-ttu-id="cfe73-110">檔案和資料夾均有存取 ACL。</span><span class="sxs-lookup"><span data-stu-id="cfe73-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="cfe73-111">**預設 ACL**：與資料夾相關聯之 ACL 的「範本」，用以判斷再該資料夾下建立的任何子項目的存取 ACL。</span><span class="sxs-lookup"><span data-stu-id="cfe73-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine the Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="cfe73-112">檔案沒有預設 ACL。</span><span class="sxs-lookup"><span data-stu-id="cfe73-112">Files do not have Default ACLs.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="cfe73-114">存取 ACL 和預設 ACL 有相同的結構。</span><span class="sxs-lookup"><span data-stu-id="cfe73-114">Both Access ACLs and Default ACLs have the same structure.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="cfe73-116">變更父代的預設 ACL 並不會影響現存子項目的存取 ACL 或預設 ACL。</span><span class="sxs-lookup"><span data-stu-id="cfe73-116">Changing the Default ACL on a parent does not affect the Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="cfe73-117">使用者和身分識別</span><span class="sxs-lookup"><span data-stu-id="cfe73-117">Users and identities</span></span>

<span data-ttu-id="cfe73-118">每個檔案和資料夾都有這些身分識別的不同權限︰</span><span class="sxs-lookup"><span data-stu-id="cfe73-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="cfe73-119">檔案的擁有使用者</span><span class="sxs-lookup"><span data-stu-id="cfe73-119">The owning user of the file</span></span>
* <span data-ttu-id="cfe73-120">擁有群組</span><span class="sxs-lookup"><span data-stu-id="cfe73-120">The owning group</span></span>
* <span data-ttu-id="cfe73-121">具名使用者</span><span class="sxs-lookup"><span data-stu-id="cfe73-121">Named users</span></span>
* <span data-ttu-id="cfe73-122">具名群組</span><span class="sxs-lookup"><span data-stu-id="cfe73-122">Named groups</span></span>
* <span data-ttu-id="cfe73-123">所有其他使用者</span><span class="sxs-lookup"><span data-stu-id="cfe73-123">All other users</span></span>

<span data-ttu-id="cfe73-124">使用者和群組的身分識別皆為 Azure Active Directory (Azure AD) 身分識別。</span><span class="sxs-lookup"><span data-stu-id="cfe73-124">The identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="cfe73-125">因此，除非另有註明，否則 Data Lake Store 中的「使用者」可能表示 Azure AD 使用者或 Azure AD 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="cfe73-125">So unless otherwise noted, a "user," in the context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="cfe73-126">權限</span><span class="sxs-lookup"><span data-stu-id="cfe73-126">Permissions</span></span>

<span data-ttu-id="cfe73-127">檔案系統物件的權限為 [讀取]、[寫入] 和 [執行]，這些權限可以用於下表所示的檔案和資料夾：</span><span class="sxs-lookup"><span data-stu-id="cfe73-127">The permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in the following table:</span></span>

|            |    <span data-ttu-id="cfe73-128">檔案</span><span class="sxs-lookup"><span data-stu-id="cfe73-128">File</span></span>     |   <span data-ttu-id="cfe73-129">資料夾</span><span class="sxs-lookup"><span data-stu-id="cfe73-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="cfe73-130">**讀取 (R)**</span><span class="sxs-lookup"><span data-stu-id="cfe73-130">**Read (R)**</span></span> | <span data-ttu-id="cfe73-131">可以讀取檔案的內容</span><span class="sxs-lookup"><span data-stu-id="cfe73-131">Can read the contents of a file</span></span> | <span data-ttu-id="cfe73-132">需要 [讀取] 和 [執行] 才能列出資料夾內容</span><span class="sxs-lookup"><span data-stu-id="cfe73-132">Requires **Read** and **Execute** to list the contents of the folder</span></span>|
| <span data-ttu-id="cfe73-133">**寫入 (W)**</span><span class="sxs-lookup"><span data-stu-id="cfe73-133">**Write (W)**</span></span> | <span data-ttu-id="cfe73-134">可寫入或附加至檔案</span><span class="sxs-lookup"><span data-stu-id="cfe73-134">Can write or append to a file</span></span> | <span data-ttu-id="cfe73-135">需要 [寫入] 和 [執行] 才能在資料夾中建立子項目</span><span class="sxs-lookup"><span data-stu-id="cfe73-135">Requires **Write** and **Execute** to create child items in a folder</span></span> |
| <span data-ttu-id="cfe73-136">**執行 (X)**</span><span class="sxs-lookup"><span data-stu-id="cfe73-136">**Execute (X)**</span></span> | <span data-ttu-id="cfe73-137">不表示 Data Lake Store 的內容中的任何項目</span><span class="sxs-lookup"><span data-stu-id="cfe73-137">Does not mean anything in the context of Data Lake Store</span></span> | <span data-ttu-id="cfe73-138">需要周遊資料夾的子項目</span><span class="sxs-lookup"><span data-stu-id="cfe73-138">Required to traverse the child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="cfe73-139">權限的簡短形式</span><span class="sxs-lookup"><span data-stu-id="cfe73-139">Short forms for permissions</span></span>

<span data-ttu-id="cfe73-140">**RWX** 用來表示 [讀取 + 寫入 + 執行]。</span><span class="sxs-lookup"><span data-stu-id="cfe73-140">**RWX** is used to indicate **Read + Write + Execute**.</span></span> <span data-ttu-id="cfe73-141">有更壓縮的數字形式存在，其中 [讀取 = 4]、[寫入 = 2] 和 [執行 = 1]，其總和代表各種權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, the sum of which represents the permissions.</span></span> <span data-ttu-id="cfe73-142">以下有一些範例。</span><span class="sxs-lookup"><span data-stu-id="cfe73-142">Following are some examples.</span></span>

| <span data-ttu-id="cfe73-143">數值形式</span><span class="sxs-lookup"><span data-stu-id="cfe73-143">Numeric form</span></span> | <span data-ttu-id="cfe73-144">簡短形式</span><span class="sxs-lookup"><span data-stu-id="cfe73-144">Short form</span></span> |      <span data-ttu-id="cfe73-145">意義</span><span class="sxs-lookup"><span data-stu-id="cfe73-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="cfe73-146">7</span><span class="sxs-lookup"><span data-stu-id="cfe73-146">7</span></span>            | <span data-ttu-id="cfe73-147">RWX</span><span class="sxs-lookup"><span data-stu-id="cfe73-147">RWX</span></span>        | <span data-ttu-id="cfe73-148">讀取 + 寫入 + 執行</span><span class="sxs-lookup"><span data-stu-id="cfe73-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="cfe73-149">5</span><span class="sxs-lookup"><span data-stu-id="cfe73-149">5</span></span>            | <span data-ttu-id="cfe73-150">R-X</span><span class="sxs-lookup"><span data-stu-id="cfe73-150">R-X</span></span>        | <span data-ttu-id="cfe73-151">讀取 + 執行</span><span class="sxs-lookup"><span data-stu-id="cfe73-151">Read + Execute</span></span>         |
| <span data-ttu-id="cfe73-152">4</span><span class="sxs-lookup"><span data-stu-id="cfe73-152">4</span></span>            | <span data-ttu-id="cfe73-153">R--</span><span class="sxs-lookup"><span data-stu-id="cfe73-153">R--</span></span>        | <span data-ttu-id="cfe73-154">讀取</span><span class="sxs-lookup"><span data-stu-id="cfe73-154">Read</span></span>                   |
| <span data-ttu-id="cfe73-155">0</span><span class="sxs-lookup"><span data-stu-id="cfe73-155">0</span></span>            | ---        | <span data-ttu-id="cfe73-156">沒有權限</span><span class="sxs-lookup"><span data-stu-id="cfe73-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="cfe73-157">不會繼承權限</span><span class="sxs-lookup"><span data-stu-id="cfe73-157">Permissions do not inherit</span></span>

<span data-ttu-id="cfe73-158">在 Data Lake Store 所使用的 POSIX 樣式模型中，項目的權限會儲存在項目本身。</span><span class="sxs-lookup"><span data-stu-id="cfe73-158">In the POSIX-style model that's used by Data Lake Store, permissions for an item are stored on the item itself.</span></span> <span data-ttu-id="cfe73-159">換句話說，無法從父項目繼承項目的權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-159">In other words, permissions for an item cannot be inherited from the parent items.</span></span>

## <a name="common-scenarios-related-to-permissions"></a><span data-ttu-id="cfe73-160">權限相關的常見案例</span><span class="sxs-lookup"><span data-stu-id="cfe73-160">Common scenarios related to permissions</span></span>

<span data-ttu-id="cfe73-161">以下是一些常見的案例，可協助您了解在 Data Lake Store 帳戶上執行某些作業所需的權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-161">Following are some common scenarios to help you understand which permissions are needed to perform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-to-read-a-file"></a><span data-ttu-id="cfe73-162">讀取檔案所需的權限</span><span class="sxs-lookup"><span data-stu-id="cfe73-162">Permissions needed to read a file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="cfe73-164">對於要讀取的檔案，呼叫端需要 [讀取] 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-164">For the file to be read, the caller needs **Read** permissions.</span></span>
* <span data-ttu-id="cfe73-165">對於資料夾結構中內含檔案的所有資料夾，呼叫端需要 [執行] 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-165">For all the folders in the folder structure that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-append-to-a-file"></a><span data-ttu-id="cfe73-166">附加至檔案所需的權限</span><span class="sxs-lookup"><span data-stu-id="cfe73-166">Permissions needed to append to a file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="cfe73-168">對於要附加的檔案，呼叫端需要 [寫入] 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-168">For the file to be appended to, the caller needs **Write** permissions.</span></span>
* <span data-ttu-id="cfe73-169">對於內含檔案的所有資料夾，呼叫端需要 [執行] 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-169">For all the folders that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-delete-a-file"></a><span data-ttu-id="cfe73-170">刪除檔案所需的權限</span><span class="sxs-lookup"><span data-stu-id="cfe73-170">Permissions needed to delete a file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="cfe73-172">對於父資料夾，呼叫端需要 [寫入 + 執行] 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-172">For the parent folder, the caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="cfe73-173">對於檔案路徑中的所有其他資料夾，呼叫端需要 [執行] 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-173">For all the other folders in the file’s path, the caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="cfe73-174">只要前面的兩個條件成立，刪除檔案時就不需要其寫入權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-174">Write permissions on the file are not required to delete it as long as the previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-to-enumerate-a-folder"></a><span data-ttu-id="cfe73-175">列舉資料夾所需的權限</span><span class="sxs-lookup"><span data-stu-id="cfe73-175">Permissions needed to enumerate a folder</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="cfe73-177">對於要列舉的資料夾，呼叫端需要 [讀取 + 執行] 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-177">For the folder to enumerate, the caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="cfe73-178">對於所有上階資料夾，呼叫端需要 [執行] 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-178">For all the ancestor folders, the caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-the-azure-portal"></a><span data-ttu-id="cfe73-179">在 Azure 入口網站中檢視權限</span><span class="sxs-lookup"><span data-stu-id="cfe73-179">Viewing permissions in the Azure portal</span></span>

<span data-ttu-id="cfe73-180">從 Data Lake Store 帳戶的 [資料總管] 刀鋒視窗，按一下 [存取] 以查看檔案或資料夾的 ACL。</span><span class="sxs-lookup"><span data-stu-id="cfe73-180">From the **Data Explorer** blade of the Data Lake Store account, click **Access** to see the ACLs for a file or a folder.</span></span> <span data-ttu-id="cfe73-181">按一下 [存取] 以查看 **mydatastore** 帳戶之下的**目錄**資料夾。</span><span class="sxs-lookup"><span data-stu-id="cfe73-181">Click **Access** to see the ACLs for the **catalog** folder under the **mydatastore** account.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="cfe73-183">在此刀鋒視窗中，最上方的區段會顯示您擁有之權限的概觀。</span><span class="sxs-lookup"><span data-stu-id="cfe73-183">On this blade, the top section shows an overview of the permissions that you have.</span></span> <span data-ttu-id="cfe73-184">(在螢幕擷取畫面中，使用者是 Bob)。存取權限會顯示於其下。</span><span class="sxs-lookup"><span data-stu-id="cfe73-184">(In the screenshot, the user is Bob.) Following that, the access permissions are shown.</span></span> <span data-ttu-id="cfe73-185">接下來，從 [存取] 刀鋒視窗，按一下 [簡單檢視] 可查看更簡單的檢視。</span><span class="sxs-lookup"><span data-stu-id="cfe73-185">After that, from the **Access** blade, click **Simple View** to see the simpler view.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="cfe73-187">按一下 [進階檢視] 以查看更進階的檢視，其中顯示預設 ACL、遮罩和超級使用者的概念。</span><span class="sxs-lookup"><span data-stu-id="cfe73-187">Click **Advanced View** to see the more advanced view, where the concepts of Default ACLs, mask, and super-user are shown.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="the-super-user"></a><span data-ttu-id="cfe73-189">超級使用者</span><span class="sxs-lookup"><span data-stu-id="cfe73-189">The super-user</span></span>

<span data-ttu-id="cfe73-190">超級使用者具有 Data Lake Store 中所有使用者的大多數權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-190">A super-user has the most rights of all the users in the Data Lake Store.</span></span> <span data-ttu-id="cfe73-191">超級使用者：</span><span class="sxs-lookup"><span data-stu-id="cfe73-191">A super-user:</span></span>

* <span data-ttu-id="cfe73-192">具有**所有**檔案和資料夾的 RWX 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-192">Has RWX Permissions to **all** files and folders.</span></span>
* <span data-ttu-id="cfe73-193">可以變更任何檔案或資料夾的權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-193">Can change the permissions on any file or folder.</span></span>
* <span data-ttu-id="cfe73-194">可以變更任何檔案或資料夾的擁有使用者或擁有群組。</span><span class="sxs-lookup"><span data-stu-id="cfe73-194">Can change the owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="cfe73-195">在 Azure 中，Data Lake Store 帳戶具有數個 Azure 角色，包括︰</span><span class="sxs-lookup"><span data-stu-id="cfe73-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="cfe73-196">擁有者</span><span class="sxs-lookup"><span data-stu-id="cfe73-196">Owners</span></span>
* <span data-ttu-id="cfe73-197">參與者</span><span class="sxs-lookup"><span data-stu-id="cfe73-197">Contributors</span></span>
* <span data-ttu-id="cfe73-198">讀取者</span><span class="sxs-lookup"><span data-stu-id="cfe73-198">Readers</span></span>

<span data-ttu-id="cfe73-199">具備 Data Lake Store 帳戶的 [擁有者]  角色的每個人都會自動成為該帳戶的超級使用者。</span><span class="sxs-lookup"><span data-stu-id="cfe73-199">Everyone in the **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="cfe73-200">若要深入了解，請參閱[角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="cfe73-200">To learn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="cfe73-201">如果您想要建立自訂的角色型存取控制 (RBAC) 角色並讓它具有超級使用者權限，它必須擁有下列權限︰</span><span class="sxs-lookup"><span data-stu-id="cfe73-201">If you want to create a custom role-based-access control (RBAC) role that has super-user permissions, it needs to have the following permissions:</span></span>
- <span data-ttu-id="cfe73-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="cfe73-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="cfe73-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="cfe73-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="the-owning-user"></a><span data-ttu-id="cfe73-204">擁有使用者</span><span class="sxs-lookup"><span data-stu-id="cfe73-204">The owning user</span></span>

<span data-ttu-id="cfe73-205">建立項目的使用者會自動成為項目的擁有使用者。</span><span class="sxs-lookup"><span data-stu-id="cfe73-205">The user who created the item is automatically the owning user of the item.</span></span> <span data-ttu-id="cfe73-206">擁有使用者可以︰</span><span class="sxs-lookup"><span data-stu-id="cfe73-206">An owning user can:</span></span>

* <span data-ttu-id="cfe73-207">變更所擁有檔案的權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-207">Change the permissions of a file that is owned.</span></span>
* <span data-ttu-id="cfe73-208">只要擁有使用者也是目標群組的成員，請變更所擁有檔案的擁有群組。</span><span class="sxs-lookup"><span data-stu-id="cfe73-208">Change the owning group of a file that is owned, as long as the owning user is also a member of the target group.</span></span>

> [!NOTE]
> <span data-ttu-id="cfe73-209">擁有使用者*無法*變更另一個所擁有檔案的擁有使用者。</span><span class="sxs-lookup"><span data-stu-id="cfe73-209">The owning user *cannot* change the owning user of another owned file.</span></span> <span data-ttu-id="cfe73-210">只有超級使用者可以變更檔案或資料夾的擁有使用者。</span><span class="sxs-lookup"><span data-stu-id="cfe73-210">Only super-users can change the owning user of a file or folder.</span></span>
>
>

## <a name="the-owning-group"></a><span data-ttu-id="cfe73-211">擁有群組</span><span class="sxs-lookup"><span data-stu-id="cfe73-211">The owning group</span></span>

<span data-ttu-id="cfe73-212">在 POSIX ACL 中，每個使用者都與「主要群組」相關聯。</span><span class="sxs-lookup"><span data-stu-id="cfe73-212">In the POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="cfe73-213">例如，使用者 "alice" 可能屬於 "finance" 群組。</span><span class="sxs-lookup"><span data-stu-id="cfe73-213">For example, user "alice" might belong to the "finance" group.</span></span> <span data-ttu-id="cfe73-214">Alice 也可能屬於多個群組，但一定有一個群組指定為其主要群組。</span><span class="sxs-lookup"><span data-stu-id="cfe73-214">Alice might also belong to multiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="cfe73-215">在 POSIX 中，當 Alice 會建立檔案時，該檔案的擁有群組會設定為她的主要群組，在此案例中為 "finance"。</span><span class="sxs-lookup"><span data-stu-id="cfe73-215">In POSIX, when Alice creates a file, the owning group of that file is set to her primary group, which in this case is "finance."</span></span>

<span data-ttu-id="cfe73-216">建立新的檔案系統項目時，Data Lake Store 會指派值給擁有群組。</span><span class="sxs-lookup"><span data-stu-id="cfe73-216">When a new filesystem item is created, Data Lake Store assigns a value to the owning group.</span></span>

* <span data-ttu-id="cfe73-217">**案例 1**：根資料夾 "/"。</span><span class="sxs-lookup"><span data-stu-id="cfe73-217">**Case 1**: The root folder "/".</span></span> <span data-ttu-id="cfe73-218">建立 Data Lake Store 帳戶時，會建立這個資料夾。</span><span class="sxs-lookup"><span data-stu-id="cfe73-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="cfe73-219">在此情況下，擁有群組會設定為建立帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="cfe73-219">In this case, the owning group is set to the user who created the account.</span></span>
* <span data-ttu-id="cfe73-220">**案例 2** (其他所有案例)：建立新項目時，會從父資料夾複製擁有群組。</span><span class="sxs-lookup"><span data-stu-id="cfe73-220">**Case 2** (Every other case): When a new item is created, the owning group is copied from the parent folder.</span></span>

<span data-ttu-id="cfe73-221">可以變更擁有群組的對象︰</span><span class="sxs-lookup"><span data-stu-id="cfe73-221">The owning group can be changed by:</span></span>
* <span data-ttu-id="cfe73-222">任何超級使用者。</span><span class="sxs-lookup"><span data-stu-id="cfe73-222">Any super-users.</span></span>
* <span data-ttu-id="cfe73-223">擁有使用者，如果擁有使用者也是目標群組的成員。</span><span class="sxs-lookup"><span data-stu-id="cfe73-223">The owning user, if the owning user is also a member of the target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="cfe73-224">存取檢查演算法</span><span class="sxs-lookup"><span data-stu-id="cfe73-224">Access check algorithm</span></span>

<span data-ttu-id="cfe73-225">下圖代表 Data Lake Store 帳戶的存取檢查演算法。</span><span class="sxs-lookup"><span data-stu-id="cfe73-225">The following illustration represents the access check algorithm for Data Lake Store accounts.</span></span>

![Data Lake Store ACL 演算法](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="the-mask-and-effective-permissions"></a><span data-ttu-id="cfe73-227">遮罩和「有效權限」</span><span class="sxs-lookup"><span data-stu-id="cfe73-227">The mask and "effective permissions"</span></span>

<span data-ttu-id="cfe73-228">**遮罩**是一個 RWX 值，在執行存取檢查演算法時，用來限制**具名使用者**、**擁有群組**和**具名群組**的存取權。</span><span class="sxs-lookup"><span data-stu-id="cfe73-228">The **mask** is an RWX value that is used to limit access for **named users**, the **owning group**, and **named groups** when you're performing the access check algorithm.</span></span> <span data-ttu-id="cfe73-229">以下是遮罩的重要概念。</span><span class="sxs-lookup"><span data-stu-id="cfe73-229">Here are the key concepts for the mask.</span></span>

* <span data-ttu-id="cfe73-230">遮罩可建立「有效權限」。</span><span class="sxs-lookup"><span data-stu-id="cfe73-230">The mask creates "effective permissions."</span></span> <span data-ttu-id="cfe73-231">也就是，它會在存取檢查時修改權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-231">That is, it modifies the permissions at the time of access check.</span></span>
* <span data-ttu-id="cfe73-232">檔案擁有者和任何超級使用者都可以直接編輯遮罩。</span><span class="sxs-lookup"><span data-stu-id="cfe73-232">The mask can be directly edited by the file owner and any super-users.</span></span>
* <span data-ttu-id="cfe73-233">遮罩能夠移除權限，以建立有效的權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-233">The mask can remove permissions to create the effective permission.</span></span> <span data-ttu-id="cfe73-234">遮罩*無法*將權限新增至有效的權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-234">The mask *cannot* add permissions to the effective permission.</span></span>

<span data-ttu-id="cfe73-235">讓我們看看一些範例。</span><span class="sxs-lookup"><span data-stu-id="cfe73-235">Let's look at some examples.</span></span> <span data-ttu-id="cfe73-236">在下列範例中，遮罩已設定為 **RWX**，這表示遮罩不會移除任何權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-236">In the following example, the mask is set to **RWX**, which means that the mask does not remove any permissions.</span></span> <span data-ttu-id="cfe73-237">在存取檢查期間，不會改變具名使用者、擁有群組和具名群組的有效權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-237">The effective permissions for the named user, owning group, and named group are not altered during the access check.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="cfe73-239">在下列範例中，遮罩已設定為 **R-X**。</span><span class="sxs-lookup"><span data-stu-id="cfe73-239">In the following example, the mask is set to **R-X**.</span></span> <span data-ttu-id="cfe73-240">這表示它會在進行存取檢查時**關閉下列各項的寫入權限**：**具名使用者**、**擁有群組**和**具名群組**。</span><span class="sxs-lookup"><span data-stu-id="cfe73-240">This means that it **turns off the Write permissions** for **named user**, **owning group**, and **named group** at the time of access check.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="cfe73-242">以下是檔案或資料夾的遮罩出現在 Azure 入口網站中的位置，可供參考。</span><span class="sxs-lookup"><span data-stu-id="cfe73-242">For reference, here is where the mask for a file or folder appears in the Azure portal.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="cfe73-244">對於新的 Data Lake Store 帳戶，根資料夾 ("/") 的存取 ACL 和預設 ACL 的遮罩會預設為 RWX。</span><span class="sxs-lookup"><span data-stu-id="cfe73-244">For a new Data Lake Store account, the mask for the Access ACL and Default ACL of the root folder ("/") defaults to RWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="cfe73-245">新檔案和資料夾的權限</span><span class="sxs-lookup"><span data-stu-id="cfe73-245">Permissions on new files and folders</span></span>

<span data-ttu-id="cfe73-246">在現有資料夾之下建立新檔案或資料夾時，父資料夾的預設 ACL 可決定︰</span><span class="sxs-lookup"><span data-stu-id="cfe73-246">When a new file or folder is created under an existing folder, the Default ACL on the parent folder determines:</span></span>

- <span data-ttu-id="cfe73-247">子資料夾的預設 ACL 與存取 ACL。</span><span class="sxs-lookup"><span data-stu-id="cfe73-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="cfe73-248">子檔案的存取 ACL (檔案沒有預設 ACL)。</span><span class="sxs-lookup"><span data-stu-id="cfe73-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="the-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="cfe73-249">子檔案或資料夾的存取 ACL</span><span class="sxs-lookup"><span data-stu-id="cfe73-249">The Access ACL of a child file or folder</span></span>

<span data-ttu-id="cfe73-250">建立子檔案或資料夾時，父項的預設 ACL 會複製成為子檔案或資料夾的存取 ACL。</span><span class="sxs-lookup"><span data-stu-id="cfe73-250">When a child file or folder is created, the parent's Default ACL is copied as the Access ACL of the child file or folder.</span></span> <span data-ttu-id="cfe73-251">此外，如果**其他**使用者具有父項的預設 ACL 的 RWX 權限，則會從子項目的存取 ACL 中將它移除。</span><span class="sxs-lookup"><span data-stu-id="cfe73-251">Also, if **other** user has RWX permissions in the parent's default ACL, it is removed from the child item's Access ACL.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="cfe73-253">在大部分情況下，您只需要上述資訊，即可了解如何決定子項目的存取 ACL。</span><span class="sxs-lookup"><span data-stu-id="cfe73-253">In most scenarios, the previous information is all you need to know about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="cfe73-254">不過，如果您很熟悉 POSIX 系統，而且想要深入了解如何達成此轉換，請參閱本文後面的 [為新檔案和資料夾建立存取 ACL 時的 Umask 角色](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) 一節。</span><span class="sxs-lookup"><span data-stu-id="cfe73-254">However, if you are familiar with POSIX systems and want to understand in-depth how this transformation is achieved, see the section [Umask’s role in creating the Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="cfe73-255">子資料夾的預設 ACL</span><span class="sxs-lookup"><span data-stu-id="cfe73-255">A child folder's Default ACL</span></span>

<span data-ttu-id="cfe73-256">在父資料夾下建立子資料夾時，父資料夾的預設 ACL 會依照原狀複製到子資料夾的預設 ACL。</span><span class="sxs-lookup"><span data-stu-id="cfe73-256">When a child folder is created under a parent folder, the parent folder's Default ACL is copied over as is to the child folder's Default ACL.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="cfe73-258">可供了解 Data Lake Store 中 ACL 的進階主題</span><span class="sxs-lookup"><span data-stu-id="cfe73-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="cfe73-259">以下幾個進階主題可協助您了解如何決定 Data Lake Store 檔案或資料夾的 ACL。</span><span class="sxs-lookup"><span data-stu-id="cfe73-259">Following are some advanced topics to help you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-the-access-acl-for-new-files-and-folders"></a><span data-ttu-id="cfe73-260">為新檔案和資料夾建立存取 ACL 時的 Umask 角色</span><span class="sxs-lookup"><span data-stu-id="cfe73-260">Umask’s role in creating the Access ACL for new files and folders</span></span>

<span data-ttu-id="cfe73-261">在 POSIX 相容系統中，一般概念是 umask 是父資料夾上的一個 9 位元值，用來轉換**擁有使用者**、**擁有群組**和**其他**使用者對於新的子檔案或資料夾之存取 ACL 的權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-261">In a POSIX-compliant system, the general concept is that umask is a 9-bit value on the parent folder that's used to transform the permission for **owning user**, **owning group**, and **other** on the Access ACL of a new child file or folder.</span></span> <span data-ttu-id="cfe73-262">Umask 的位元可識別在子項目的存取 ACL 中所要關閉的位元。</span><span class="sxs-lookup"><span data-stu-id="cfe73-262">The bits of a umask identify which bits to turn off in the child item’s Access ACL.</span></span> <span data-ttu-id="cfe73-263">因此可用來選擇性地防止**擁有使用者**、**擁有群組**和**其他使用者**的權限傳播。</span><span class="sxs-lookup"><span data-stu-id="cfe73-263">Thus it is used to selectively prevent the propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="cfe73-264">在 HDFS 系統中，umask 通常是由系統管理員所控制的全網站組態選項。</span><span class="sxs-lookup"><span data-stu-id="cfe73-264">In an HDFS system, the umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="cfe73-265">Data Lake Store 會使用無法變更的 **全帳戶 umask** 。</span><span class="sxs-lookup"><span data-stu-id="cfe73-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="cfe73-266">下表顯示 Data Lake Store 的 unmask。</span><span class="sxs-lookup"><span data-stu-id="cfe73-266">The following table shows the unmask for Data Lake Store.</span></span>

| <span data-ttu-id="cfe73-267">使用者群組</span><span class="sxs-lookup"><span data-stu-id="cfe73-267">User group</span></span>  | <span data-ttu-id="cfe73-268">設定</span><span class="sxs-lookup"><span data-stu-id="cfe73-268">Setting</span></span> | <span data-ttu-id="cfe73-269">對新的子項目的存取 ACL 的影響</span><span class="sxs-lookup"><span data-stu-id="cfe73-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="cfe73-270">擁有使用者</span><span class="sxs-lookup"><span data-stu-id="cfe73-270">Owning user</span></span> | ---     | <span data-ttu-id="cfe73-271">沒有影響</span><span class="sxs-lookup"><span data-stu-id="cfe73-271">No effect</span></span>                             |
| <span data-ttu-id="cfe73-272">擁有群組</span><span class="sxs-lookup"><span data-stu-id="cfe73-272">Owning group</span></span>| ---     | <span data-ttu-id="cfe73-273">沒有影響</span><span class="sxs-lookup"><span data-stu-id="cfe73-273">No effect</span></span>                             |
| <span data-ttu-id="cfe73-274">其他</span><span class="sxs-lookup"><span data-stu-id="cfe73-274">Other</span></span>       | <span data-ttu-id="cfe73-275">RWX</span><span class="sxs-lookup"><span data-stu-id="cfe73-275">RWX</span></span>     | <span data-ttu-id="cfe73-276">移除讀取 + 寫入 + 執行</span><span class="sxs-lookup"><span data-stu-id="cfe73-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="cfe73-277">下圖顯示此 umask 作用中。</span><span class="sxs-lookup"><span data-stu-id="cfe73-277">The following illustration shows this umask in action.</span></span> <span data-ttu-id="cfe73-278">實質效果是移除**其他**使用者的 [讀取 + 寫入 + 執行]。</span><span class="sxs-lookup"><span data-stu-id="cfe73-278">The net effect is to remove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="cfe73-279">由於 umask 未指定**擁有使用者**和**擁有群組**的位元，因此不會轉換這些權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-279">Because the umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="the-sticky-bit"></a><span data-ttu-id="cfe73-281">黏性位元</span><span class="sxs-lookup"><span data-stu-id="cfe73-281">The sticky bit</span></span>

<span data-ttu-id="cfe73-282">黏性位元是 POSIX 檔案系統的更進階功能。</span><span class="sxs-lookup"><span data-stu-id="cfe73-282">The sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="cfe73-283">在 Data Lake Store 的內容中，不太可能需要黏性位元。</span><span class="sxs-lookup"><span data-stu-id="cfe73-283">In the context of Data Lake Store, it is unlikely that the sticky bit will be needed.</span></span>

<span data-ttu-id="cfe73-284">下表顯示黏性位元在 Data Lake Store 中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="cfe73-284">The following table shows how the sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="cfe73-285">使用者群組</span><span class="sxs-lookup"><span data-stu-id="cfe73-285">User group</span></span>         | <span data-ttu-id="cfe73-286">檔案</span><span class="sxs-lookup"><span data-stu-id="cfe73-286">File</span></span>    | <span data-ttu-id="cfe73-287">資料夾</span><span class="sxs-lookup"><span data-stu-id="cfe73-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="cfe73-288">黏性位元 **OFF**</span><span class="sxs-lookup"><span data-stu-id="cfe73-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="cfe73-289">沒有影響</span><span class="sxs-lookup"><span data-stu-id="cfe73-289">No effect</span></span>   | <span data-ttu-id="cfe73-290">沒有影響。</span><span class="sxs-lookup"><span data-stu-id="cfe73-290">No effect.</span></span>           |
| <span data-ttu-id="cfe73-291">黏性位元 **ON**</span><span class="sxs-lookup"><span data-stu-id="cfe73-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="cfe73-292">沒有影響</span><span class="sxs-lookup"><span data-stu-id="cfe73-292">No effect</span></span>   | <span data-ttu-id="cfe73-293">防止任何人 (子項目的**超級使用者**和**擁有使用者**除外) 刪除或重新命名該子項目。</span><span class="sxs-lookup"><span data-stu-id="cfe73-293">Prevents anyone except **super-users** and the **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="cfe73-294">黏性位元不會顯示在 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="cfe73-294">The sticky bit is not shown in the Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="cfe73-295">Data Lake Store 中 ACL 的相關常見問題</span><span class="sxs-lookup"><span data-stu-id="cfe73-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="cfe73-296">以下是有關 Data Lake Store 中 ACL 的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="cfe73-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-to-enable-support-for-acls"></a><span data-ttu-id="cfe73-297">我必須啟用 ACL 的支援嗎？</span><span class="sxs-lookup"><span data-stu-id="cfe73-297">Do I have to enable support for ACLs?</span></span>

<span data-ttu-id="cfe73-298">否。</span><span class="sxs-lookup"><span data-stu-id="cfe73-298">No.</span></span> <span data-ttu-id="cfe73-299">Data Lake Store 帳戶一律會啟用透過 ACL 的存取控制。</span><span class="sxs-lookup"><span data-stu-id="cfe73-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-to-recursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="cfe73-300">若要以遞迴方式刪除資料夾與其內容，需要哪些權限？</span><span class="sxs-lookup"><span data-stu-id="cfe73-300">Which permissions are required to recursively delete a folder and its contents?</span></span>

* <span data-ttu-id="cfe73-301">父資料夾必須具有 [寫入 + 執行] 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-301">The parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="cfe73-302">要刪除的資料夾及其中的每個資料夾，都需要 [讀取 + 寫入 + 執行] 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-302">The folder to be deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="cfe73-303">您不需要寫入權限即可刪除資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="cfe73-303">You do not need Write permissions to delete files in folders.</span></span> <span data-ttu-id="cfe73-304">此外，**決不**會刪除根資料夾 "/"。</span><span class="sxs-lookup"><span data-stu-id="cfe73-304">Also, the root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-the-owner-of-a-file-or-folder"></a><span data-ttu-id="cfe73-305">誰是檔案或資料夾的擁有者？</span><span class="sxs-lookup"><span data-stu-id="cfe73-305">Who is the owner of a file or folder?</span></span>

<span data-ttu-id="cfe73-306">檔案或資料夾的建立者會成為擁有者。</span><span class="sxs-lookup"><span data-stu-id="cfe73-306">The creator of a file or folder becomes the owner.</span></span>

### <a name="which-group-is-set-as-the-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="cfe73-307">在建立檔案或資料夾時，會將哪個群組設定為擁有群組？</span><span class="sxs-lookup"><span data-stu-id="cfe73-307">Which group is set as the owning group of a file or folder at creation?</span></span>

<span data-ttu-id="cfe73-308">擁有群組是從新檔案或資料夾建立所在父資料夾的擁有群組複製而來。</span><span class="sxs-lookup"><span data-stu-id="cfe73-308">The owning group is copied from the owning group of the parent folder under which the new file or folder is created.</span></span>

### <a name="i-am-the-owning-user-of-a-file-but-i-dont-have-the-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="cfe73-309">我是檔案的擁有使用者，但沒有我需要的 RWX 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-309">I am the owning user of a file but I don’t have the RWX permissions I need.</span></span> <span data-ttu-id="cfe73-310">該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="cfe73-310">What do I do?</span></span>

<span data-ttu-id="cfe73-311">擁有使用者可以變更檔案的權限，以取得本身所需的任何 RWX 權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-311">The owning user can change the permissions of the file to give themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-the-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="cfe73-312">當我在 Azure 入口網站中查看 ACL 時，我可看到使用者名稱，但透過 API 卻看到 GUID，為什麼會這樣？</span><span class="sxs-lookup"><span data-stu-id="cfe73-312">When I look at ACLs in the Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="cfe73-313">ACL 中的項目會儲存為對應於 Azure AD 中使用者的 GUID。</span><span class="sxs-lookup"><span data-stu-id="cfe73-313">Entries in the ACLs are stored as GUIDs that correspond to users in Azure AD.</span></span> <span data-ttu-id="cfe73-314">API 會依現狀傳回 GUID。</span><span class="sxs-lookup"><span data-stu-id="cfe73-314">The APIs return the GUIDs as is.</span></span> <span data-ttu-id="cfe73-315">Azure 入口網站會儘可能將 GUID 轉譯成好記的名稱，試圖讓 ACL 更容易使用。</span><span class="sxs-lookup"><span data-stu-id="cfe73-315">The Azure portal tries to make ACLs easier to use by translating the GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-the-acls-when-im-using-the-azure-portal"></a><span data-ttu-id="cfe73-316">當我使用 Azure 入口網站時，為什麼有時候會在 ACL 中看到 GUID？</span><span class="sxs-lookup"><span data-stu-id="cfe73-316">Why do I sometimes see GUIDs in the ACLs when I'm using the Azure portal?</span></span>

<span data-ttu-id="cfe73-317">當使用者已不存在於 Azure AD 時，將會顯示 GUID。</span><span class="sxs-lookup"><span data-stu-id="cfe73-317">A GUID is shown when the user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="cfe73-318">當使用者已離開公司，或已在 Azure AD 中刪除其帳戶時，通常會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="cfe73-318">Usually this happens when the user has left the company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="cfe73-319">Data Lake Store 是否支援 ACL 的繼承？</span><span class="sxs-lookup"><span data-stu-id="cfe73-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="cfe73-320">否。</span><span class="sxs-lookup"><span data-stu-id="cfe73-320">No.</span></span>

### <a name="what-is-the-difference-between-mask-and-umask"></a><span data-ttu-id="cfe73-321">遮罩與 umask 之間的差異為何？</span><span class="sxs-lookup"><span data-stu-id="cfe73-321">What is the difference between mask and umask?</span></span>

| <span data-ttu-id="cfe73-322">遮罩</span><span class="sxs-lookup"><span data-stu-id="cfe73-322">mask</span></span> | <span data-ttu-id="cfe73-323">umask</span><span class="sxs-lookup"><span data-stu-id="cfe73-323">umask</span></span>|
|------|------|
| <span data-ttu-id="cfe73-324">**遮罩** 屬性適用於每個檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="cfe73-324">The **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="cfe73-325">**umask** 是 Data Lake Store 帳戶的屬性。</span><span class="sxs-lookup"><span data-stu-id="cfe73-325">The **umask** is a property of the Data Lake Store account.</span></span> <span data-ttu-id="cfe73-326">因此，Data Lake Store 中只有一個 umask。</span><span class="sxs-lookup"><span data-stu-id="cfe73-326">So there is only a single umask in the Data Lake Store.</span></span>    |
| <span data-ttu-id="cfe73-327">檔案的擁有使用者或擁有群組或超級使用者都可以改變檔案或資料夾的遮罩屬性。</span><span class="sxs-lookup"><span data-stu-id="cfe73-327">The mask property on a file or folder can be altered by the owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="cfe73-328">任何使用者 (甚至是超級使用者) 都不能修改 umask 屬性。</span><span class="sxs-lookup"><span data-stu-id="cfe73-328">The umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="cfe73-329">這是不能變更的常數值。</span><span class="sxs-lookup"><span data-stu-id="cfe73-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="cfe73-330">在存取檢查演算法的執行階段，會使用遮罩屬性來判斷使用者是否具有在檔案或資料夾上執行作業的權限。</span><span class="sxs-lookup"><span data-stu-id="cfe73-330">The mask property is used during the access check algorithm at runtime to determine whether a user has the right to perform on operation on a file or folder.</span></span> <span data-ttu-id="cfe73-331">遮罩的角色就是在存取檢查時建立「有效權限」。</span><span class="sxs-lookup"><span data-stu-id="cfe73-331">The role of the mask is to create "effective permissions" at the time of access check.</span></span> | <span data-ttu-id="cfe73-332">存取檢查期間完全不會使用 umask。</span><span class="sxs-lookup"><span data-stu-id="cfe73-332">The umask is not used during access check at all.</span></span> <span data-ttu-id="cfe73-333">Umask 用來決定資料夾的新子項目的存取 ACL。</span><span class="sxs-lookup"><span data-stu-id="cfe73-333">The umask is used to determine the Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="cfe73-334">遮罩是一個 3 位元的 RWX 值，在存取檢查時會套用至具名使用者、具名群組及擁有使用者。</span><span class="sxs-lookup"><span data-stu-id="cfe73-334">The mask is a 3-bit RWX value that applies to named user, named group, and owning user at the time of access check.</span></span>| <span data-ttu-id="cfe73-335">Umask 是一個 9 位元值，會套用至新子系的擁有使用者、擁有群組及**其他使用者**。</span><span class="sxs-lookup"><span data-stu-id="cfe73-335">The umask is a 9-bit value that applies to the owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="cfe73-336">何處可以進一步了解 POSIX 存取控制模型？</span><span class="sxs-lookup"><span data-stu-id="cfe73-336">Where can I learn more about POSIX access control model?</span></span>

* [<span data-ttu-id="cfe73-337">Linux 上的 POSIX 存取控制清單</span><span class="sxs-lookup"><span data-stu-id="cfe73-337">POSIX Access Control Lists on Linux</span></span>](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [<span data-ttu-id="cfe73-338">HDFS 權限指南</span><span class="sxs-lookup"><span data-stu-id="cfe73-338">HDFS permission guide</span></span>](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [<span data-ttu-id="cfe73-339">POSIX 常見問題集</span><span class="sxs-lookup"><span data-stu-id="cfe73-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="cfe73-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="cfe73-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="cfe73-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="cfe73-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="cfe73-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="cfe73-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="cfe73-343">Ubuntu 上的 POSIX ACL</span><span class="sxs-lookup"><span data-stu-id="cfe73-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* [<span data-ttu-id="cfe73-344">Linux 上使用存取控制清單的 ACL</span><span class="sxs-lookup"><span data-stu-id="cfe73-344">ACL using access control lists on Linux</span></span>](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a><span data-ttu-id="cfe73-345">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cfe73-345">See also</span></span>

* [<span data-ttu-id="cfe73-346">Azure Data Lake Store 概觀</span><span class="sxs-lookup"><span data-stu-id="cfe73-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
