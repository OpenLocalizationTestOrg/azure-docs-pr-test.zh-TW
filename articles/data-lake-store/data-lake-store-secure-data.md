---
title: "保護儲存在 Azure Data Lake Store 中的資料 | Microsoft Docs"
description: "了解如何使用群組和存取控制清單來保護 Azure 資料湖儲存區中的資料"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ca35e65f-3986-4f1b-bf93-9af6066bb716
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 345896880b0acfb28607926205b053cb7a332d27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="securing-data-stored-in-azure-data-lake-store"></a><span data-ttu-id="e370c-103">保護儲存在 Azure 資料湖儲存區中的資料</span><span class="sxs-lookup"><span data-stu-id="e370c-103">Securing data stored in Azure Data Lake Store</span></span>
<span data-ttu-id="e370c-104">保護儲存在 Azure 資料湖儲存區中的資料，其方法有三步驟。</span><span class="sxs-lookup"><span data-stu-id="e370c-104">Securing data in Azure Data Lake Store is a three-step approach.</span></span>

1. <span data-ttu-id="e370c-105">首先，在 Azure Active Directory (AAD) 中建立安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e370c-105">Start by creating security groups in Azure Active Directory (AAD).</span></span> <span data-ttu-id="e370c-106">這些安全性群組是用在 Azure 入口網站中實作角色型存取控制 (RBAC)。</span><span class="sxs-lookup"><span data-stu-id="e370c-106">These security groups are used to implement role-based access control (RBAC) in Azure Portal.</span></span> <span data-ttu-id="e370c-107">如需詳細資訊，請參閱 [Microsoft Azure 中的角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="e370c-107">For more information see [Role-based Access Control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>
2. <span data-ttu-id="e370c-108">指派 AAD 安全性群組給 Azure 資料湖儲存區帳戶。</span><span class="sxs-lookup"><span data-stu-id="e370c-108">Assign the AAD security groups to the Azure Data Lake Store account.</span></span> <span data-ttu-id="e370c-109">這會控制從入口網站至資料湖儲存區帳戶，以及從入口網站或 API 至管理作業的存取。</span><span class="sxs-lookup"><span data-stu-id="e370c-109">This controls access to the Data Lake Store account from the portal and management operations from the portal or APIs.</span></span>
3. <span data-ttu-id="e370c-110">指派 AAD 安全性群組做為資料湖儲存區檔案系統上的存取控制清單 (ACL)。</span><span class="sxs-lookup"><span data-stu-id="e370c-110">Assign the AAD security groups as access control lists (ACLs) on the Data Lake Store file system.</span></span>
4. <span data-ttu-id="e370c-111">此外，您也可以針對可以存取 Data Lake Store 中資料的用戶端設定 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="e370c-111">Additionally, you can also set an IP address range for clients that can access the data in Data Lake Store.</span></span>

<span data-ttu-id="e370c-112">本文提供有關如何使用 Azure 入口網站執行上述工作的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="e370c-112">This article provides instructions on how to use the Azure portal to perform the above tasks.</span></span> <span data-ttu-id="e370c-113">如需 Data Lake Store 如何在帳戶和資料層級實作安全性的深入資訊，請參閱 [Azure Data Lake Store 安全性](data-lake-store-security-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e370c-113">For in-depth information on how Data Lake Store implements security at the account and data level, see [Security in Azure Data Lake Store](data-lake-store-security-overview.md).</span></span> <span data-ttu-id="e370c-114">如需 ACL 如何在 Azure Data Lake Store 中實作的深入資訊，請參閱 [Data Lake Store 中的存取控制的概觀](data-lake-store-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="e370c-114">For deep-dive information on how ACLs are implemented in Azure Data Lake Store, see [Overview of Access Control in Data Lake Store](data-lake-store-access-control.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e370c-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="e370c-115">Prerequisites</span></span>
<span data-ttu-id="e370c-116">開始進行本教學課程之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="e370c-116">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="e370c-117">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="e370c-117">**An Azure subscription**.</span></span> <span data-ttu-id="e370c-118">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e370c-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e370c-119">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="e370c-119">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="e370c-120">如需有關如何建立帳戶的詳細指示，請參閱 [開始使用 Azure 資料湖儲存區](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e370c-120">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="create-security-groups-in-azure-active-directory"></a><span data-ttu-id="e370c-121">在 Azure Active Directory 中建立安全性群組</span><span class="sxs-lookup"><span data-stu-id="e370c-121">Create security groups in Azure Active Directory</span></span>
<span data-ttu-id="e370c-122">如需有關如何建立 AAD 安全性群組及如何新增使用者至群組的詳細指示，請參閱 [管理 Azure Active Directory 中的安全性群組](../active-directory/active-directory-accessmanagement-manage-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="e370c-122">For instructions on how to create AAD security groups and how to add users to the group, see [Managing security groups in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="e370c-123">您可以將使用者及其他群組新增至使用 Azure 入口網站的 Azure AD 的群組中。</span><span class="sxs-lookup"><span data-stu-id="e370c-123">You can add both users and other groups to a group in Azure AD using the Azure portal.</span></span> <span data-ttu-id="e370c-124">不過，若要將服務主體新增至群組，請使用 [Azure AD PowerShell 模組](../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md)。</span><span class="sxs-lookup"><span data-stu-id="e370c-124">However, in order to add a service principal to a group, please use [Azure AD’s PowerShell module](../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).</span></span>
> 
> ```powershell
> # Get the desired group and service principal and identify the correct object IDs
> Get-AzureADGroup -SearchString "<group name>"
> Get-AzureADServicePrincipal -SearchString "<SPI name>"
> 
> # Add the service principal to the group
> Add-AzureADGroupMember -ObjectId <Group object ID> -RefObjectId <SPI object ID>
> ```
 
## <a name="assign-users-or-security-groups-to-azure-data-lake-store-accounts"></a><span data-ttu-id="e370c-125">指派使用者或安全性群組給 Azure 資料湖儲存區帳戶</span><span class="sxs-lookup"><span data-stu-id="e370c-125">Assign users or security groups to Azure Data Lake Store accounts</span></span>
<span data-ttu-id="e370c-126">當您指派使用者或安全性群組給 Azure 資料湖儲存區帳戶時，您可使用 Azure 入口網站和 Azure 資源管理員 API 來控制該帳戶的管理作業存取。</span><span class="sxs-lookup"><span data-stu-id="e370c-126">When you assign users or security groups to Azure Data Lake Store accounts, you control access to the management operations on the account using the Azure portal and Azure Resource Manager APIs.</span></span> 

1. <span data-ttu-id="e370c-127">開啟 Azure 資料湖儲存區帳戶。</span><span class="sxs-lookup"><span data-stu-id="e370c-127">Open an Azure Data Lake Store account.</span></span> <span data-ttu-id="e370c-128">從左側窗格依序按一下 [瀏覽]、[Data Lake Store]，然後從 [Data Lake Store] 刀鋒視窗中，按一下您要指派使用者或安全性群組的目標帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="e370c-128">From the left pane, click **Browse**, click **Data Lake Store**, and then from the Data Lake Store blade, click the account name to which you want to assign a user or security group.</span></span>

2. <span data-ttu-id="e370c-129">在 Data Lake Store 帳戶設定刀鋒視窗中，按一下 [存取控制 (IAM)]。</span><span class="sxs-lookup"><span data-stu-id="e370c-129">In your Data Lake Store account settings blade, click **Access Control (IAM)**.</span></span> <span data-ttu-id="e370c-130">依預設，刀鋒視窗會將 [訂用帳戶管理員] 群組列為擁有者。</span><span class="sxs-lookup"><span data-stu-id="e370c-130">The blade by default lists **Subscription admins** group as an owner.</span></span>
   
    <span data-ttu-id="e370c-131">![指派安全性群組給 Azure Data Lake Store 帳戶](./media/data-lake-store-secure-data/adl.select.user.icon.png "指派安全性群組給 Azure Data Lake Store 帳戶")</span><span class="sxs-lookup"><span data-stu-id="e370c-131">![Assign security group to Azure Data Lake Store account](./media/data-lake-store-secure-data/adl.select.user.icon.png "Assign security group to Azure Data Lake Store account")</span></span>

    <span data-ttu-id="e370c-132">有兩種方式可新增群組並指派相關的角色。</span><span class="sxs-lookup"><span data-stu-id="e370c-132">There are two ways to add a group and assign relevant roles.</span></span>
   
    * <span data-ttu-id="e370c-133">新增使用者/群組至帳戶，然後指派角色，或</span><span class="sxs-lookup"><span data-stu-id="e370c-133">Add a user/group to the account and then assign a role, or</span></span>
    * <span data-ttu-id="e370c-134">新增角色，然後指派使用者/群組給角色。</span><span class="sxs-lookup"><span data-stu-id="e370c-134">Add a role and then assign users/groups to role.</span></span>
     
    <span data-ttu-id="e370c-135">在本節中，我們將探討第一個方法，也就是新增群組，然後指派角色。</span><span class="sxs-lookup"><span data-stu-id="e370c-135">In this section, we look at the first approach, adding a group and then assigning roles.</span></span> <span data-ttu-id="e370c-136">您可以執行類似的步驟先選取角色，然後指派群組給該角色。</span><span class="sxs-lookup"><span data-stu-id="e370c-136">You can perform similar steps to first select a role and then assign groups to that role.</span></span>
4. <span data-ttu-id="e370c-137">在 [使用者] 刀鋒視窗中，按一下 [新增] 以開啟 [新增存取] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e370c-137">In the **Users** blade, click **Add** to open the **Add access** blade.</span></span> <span data-ttu-id="e370c-138">在 [新增存取] 刀鋒視窗中，按一下 [選取角色]，然後選取使用者/群組的角色。</span><span class="sxs-lookup"><span data-stu-id="e370c-138">In the **Add access** blade, click **Select a role**, and then select a role for the user/group.</span></span>
   
    <span data-ttu-id="e370c-139">![新增使用者的角色](./media/data-lake-store-secure-data/adl.add.user.1.png "新增使用者的角色")</span><span class="sxs-lookup"><span data-stu-id="e370c-139">![Add a role for the user](./media/data-lake-store-secure-data/adl.add.user.1.png "Add a role for the user")</span></span>
   
    <span data-ttu-id="e370c-140">[擁有者] 和 [參與者] 角色會提供 Data Lake 帳戶上各種不同管理功能的存取。</span><span class="sxs-lookup"><span data-stu-id="e370c-140">The **Owner** and **Contributor** role provide access to a variety of administration functions on the data lake account.</span></span> <span data-ttu-id="e370c-141">針對與資料湖資料互動的使用者，您可以將它們新增至 [讀取器]**** 角色。</span><span class="sxs-lookup"><span data-stu-id="e370c-141">For users who will interact with data in the data lake, you can add them to the **Reader **role.</span></span> <span data-ttu-id="e370c-142">這些角色的範圍僅限於與 Azure 資料湖儲存區帳戶相關的管理作業。</span><span class="sxs-lookup"><span data-stu-id="e370c-142">The scope of these roles is limited to the management operations related to the Azure Data Lake Store account.</span></span>
   
    <span data-ttu-id="e370c-143">針對資料作業，個別的檔案系統權限會定義使用者的使用範圍。</span><span class="sxs-lookup"><span data-stu-id="e370c-143">For data operations individual file system permissions define what the users can do.</span></span> <span data-ttu-id="e370c-144">因此，擁有 [讀取器] 角色的使用者僅可檢視與帳戶相關的管理設定，但是可依指派給該使用者的檔案系統權限來讀取和寫入資料。</span><span class="sxs-lookup"><span data-stu-id="e370c-144">Therefore, a user having a Reader role can only view administrative settings associated with the account but can potentially read and write data based on file system permissions assigned to them.</span></span> <span data-ttu-id="e370c-145">有關資料湖儲存區檔案系統權限的相關資訊都在 [將安全性群組以 ACL 型式指派給 Azure 資料湖儲存區檔案系統](#filepermissions)。</span><span class="sxs-lookup"><span data-stu-id="e370c-145">Data Lake Store file system permissions are described at [Assign security group as ACLs to the Azure Data Lake Store file system](#filepermissions).</span></span>
5. <span data-ttu-id="e370c-146">在 [新增存取] 刀鋒視窗中，按一下 [新增使用者] 以開啟 [新增使用者] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e370c-146">In the **Add access** blade, click **Add users** to open the **Add users** blade.</span></span> <span data-ttu-id="e370c-147">在此刀鋒視窗中，搜尋您稍早在 Azure Active Directory 中建立的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e370c-147">In this blade, look for the security group you created earlier in Azure Active Directory.</span></span> <span data-ttu-id="e370c-148">若您需要搜尋大量的群組，請使用頂端的文字方塊來篩選群組名稱。</span><span class="sxs-lookup"><span data-stu-id="e370c-148">If you have a lot of groups to search from, use the text box at the top to filter on the group name.</span></span> <span data-ttu-id="e370c-149">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="e370c-149">Click **Select**.</span></span>
   
    <span data-ttu-id="e370c-150">![新增安全性群組](./media/data-lake-store-secure-data/adl.add.user.2.png "新增安全性群組")</span><span class="sxs-lookup"><span data-stu-id="e370c-150">![Add a security group](./media/data-lake-store-secure-data/adl.add.user.2.png "Add a security group")</span></span>
   
    <span data-ttu-id="e370c-151">若要新增未列出的群組/使用者，您可使用 [邀請]  圖示並指定使用者/群組的電子郵件位址來邀請。</span><span class="sxs-lookup"><span data-stu-id="e370c-151">If you want to add a group/user that is not listed, you can invite them by using the **Invite** icon and specifying the e-mail address for the user/group.</span></span>
6. <span data-ttu-id="e370c-152">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e370c-152">Click **OK**.</span></span> <span data-ttu-id="e370c-153">您會看見新增的安全性群組，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e370c-153">You should see the security group added as shown below.</span></span>
   
    <span data-ttu-id="e370c-154">![已新增的安全性群組](./media/data-lake-store-secure-data/adl.add.user.3.png "已新增的安全性群組")</span><span class="sxs-lookup"><span data-stu-id="e370c-154">![Security group added](./media/data-lake-store-secure-data/adl.add.user.3.png "Security group added")</span></span>

7. <span data-ttu-id="e370c-155">您的使用者/安全性群組現在可以存取 Azure 資料湖儲存區帳戶。</span><span class="sxs-lookup"><span data-stu-id="e370c-155">Your user/security group now has access to the Azure Data Lake Store account.</span></span> <span data-ttu-id="e370c-156">若要將存取權授與特定使用者，您可以將他們新增至安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e370c-156">If you want to provide access to specific users, you can add them to the security group.</span></span> <span data-ttu-id="e370c-157">同樣地，若要撤銷使用者的存取權，您可以將他們從安全性群組中移除。</span><span class="sxs-lookup"><span data-stu-id="e370c-157">Similarly, if you want to revoke access for a user, you can remove them from the security group.</span></span> <span data-ttu-id="e370c-158">您也可以將多個安全性群組指派給一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="e370c-158">You can also assign multiple security groups to an account.</span></span> 

## <span data-ttu-id="e370c-159"><a name="filepermissions"></a>將使用者或安全性群組以 ACL 型式指派給 Azure 資料湖儲存區檔案系統</span><span class="sxs-lookup"><span data-stu-id="e370c-159"><a name="filepermissions"></a>Assign users or security group as ACLs to the Azure Data Lake Store file system</span></span>
<span data-ttu-id="e370c-160">藉由指派使用者/安全性群組給 Azure 資料湖檔案系統，您可以針對儲存在 Azure 資料湖儲存區中的資料設定存取控制。</span><span class="sxs-lookup"><span data-stu-id="e370c-160">By assigning user/security groups to the Azure Data Lake file system, you set access control on the data stored in Azure Data Lake Store.</span></span>

1. <span data-ttu-id="e370c-161">在您的 [資料湖儲存區帳戶] 刀鋒視窗中，按一下 [資料總管] 。</span><span class="sxs-lookup"><span data-stu-id="e370c-161">In your Data Lake Store account blade, click **Data Explorer**.</span></span>
   
    <span data-ttu-id="e370c-162">![在 Data Lake Store 帳戶中建立目錄](./media/data-lake-store-secure-data/adl.start.data.explorer.png "在 Data Lake Store 帳戶中建立目錄")</span><span class="sxs-lookup"><span data-stu-id="e370c-162">![Create directories in Data Lake Store account](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Create directories in Data Lake account")</span></span>
2. <span data-ttu-id="e370c-163">在 [資料總管] 刀鋒視窗中，按一下您要將設定 ACL 的檔案或資料夾，然後按一下 [存取]。</span><span class="sxs-lookup"><span data-stu-id="e370c-163">In the **Data Explorer** blade, click the file or folder for which you want to configure the ACL, and then click **Access**.</span></span> <span data-ttu-id="e370c-164">若要指派 ACL 至檔案，您必須從 [檔案預覽] 刀鋒視窗按一下 [存取]。</span><span class="sxs-lookup"><span data-stu-id="e370c-164">To assign ACL to a file, you must click **Access** from the **File Preview** blade.</span></span>
   
    <span data-ttu-id="e370c-165">![設定 Data Lake 檔案系統上的 ACL](./media/data-lake-store-secure-data/adl.acl.1.png "設定 Data Lake 檔案系統上的 ACL")</span><span class="sxs-lookup"><span data-stu-id="e370c-165">![Set ACLs on Data Lake file system](./media/data-lake-store-secure-data/adl.acl.1.png "Set ACLs on Data Lake file system")</span></span>
3. <span data-ttu-id="e370c-166">[存取]  刀鋒視窗會列出已指派至根的標準存取和自訂存取。</span><span class="sxs-lookup"><span data-stu-id="e370c-166">The **Access** blade lists the standard access and custom access already assigned to the root.</span></span> <span data-ttu-id="e370c-167">按一下 [新增]  圖示以新增自訂層級的 ACL。</span><span class="sxs-lookup"><span data-stu-id="e370c-167">Click the **Add** icon to add custom-level ACLs.</span></span>
   
    <span data-ttu-id="e370c-168">![列出標準和自訂存取](./media/data-lake-store-secure-data/adl.acl.2.png "列出標準和自訂的存取")</span><span class="sxs-lookup"><span data-stu-id="e370c-168">![List standard and custom access](./media/data-lake-store-secure-data/adl.acl.2.png "List standard and custom access")</span></span>
   
   * <span data-ttu-id="e370c-169">**標準存取** 為 UNIX 樣式存取，可讓您指定讀取、寫入、執行 (rwx) 三種不同的使用者類別：擁有者、群組和其他。</span><span class="sxs-lookup"><span data-stu-id="e370c-169">**Standard access** is the UNIX-style access, where you specify read, write, execute (rwx) to three distinct user classes: owner, group, and others.</span></span>
   * <span data-ttu-id="e370c-170">**自訂存取** 會對應至 POSIX ACL，讓您除了設定檔案擁有者或群組的權限外，還可以設定特定命名的使用者或群組的權限。</span><span class="sxs-lookup"><span data-stu-id="e370c-170">**Custom access** corresponds to the POSIX ACLs that enables you to set permissions for specific named users or groups, and not only the file's owner or group.</span></span> 
     
     <span data-ttu-id="e370c-171">如需詳細資訊，請參閱 [HDFS ACLs](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists)。</span><span class="sxs-lookup"><span data-stu-id="e370c-171">For more information, see [HDFS ACLs](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists).</span></span> <span data-ttu-id="e370c-172">如需 ACL 如何在 Data Lake Store 中實作的詳細資訊，請參閱 [Data Lake Store 中的存取控制](data-lake-store-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="e370c-172">For more information on how ACLs are implemented in Data Lake Store, see [Access Control in Data Lake Store](data-lake-store-access-control.md).</span></span>
4. <span data-ttu-id="e370c-173">按一下 [新增] 圖示，以開啟 [新增自訂存取] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e370c-173">Click the **Add** icon to open the **Add Custom Access** blade.</span></span> <span data-ttu-id="e370c-174">在此刀鋒視窗中，按一下 [選取使用者或群組]，然後在 [選取使用者或群組] 刀鋒視窗中，搜尋您稍早在 Azure Active Directory 中建立的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e370c-174">In this blade, click **Select User or Group**, and then in **Select User or Group** blade, look for the security group you created earlier in Azure Active Directory.</span></span> <span data-ttu-id="e370c-175">若您需要搜尋大量的群組，請使用頂端的文字方塊來篩選群組名稱。</span><span class="sxs-lookup"><span data-stu-id="e370c-175">If you have a lot of groups to search from, use the text box at the top to filter on the group name.</span></span> <span data-ttu-id="e370c-176">按一下您要新增的群組，然後按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="e370c-176">Click the group you want to add and then click **Select**.</span></span>
   
    <span data-ttu-id="e370c-177">![加入群組](./media/data-lake-store-secure-data/adl.acl.3.png "加入群組")</span><span class="sxs-lookup"><span data-stu-id="e370c-177">![Add a group](./media/data-lake-store-secure-data/adl.acl.3.png "Add a group")</span></span>
5. <span data-ttu-id="e370c-178">按一下 [選取權限]，選取權限及權限的指派方式 (例如預設 ACL、存取 ACL 或兩者並用)。</span><span class="sxs-lookup"><span data-stu-id="e370c-178">Click **Select Permissions**, select the permissions and whether you want to assign the permissions as a default ACL, access ACL, or both.</span></span> <span data-ttu-id="e370c-179">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e370c-179">Click **OK**.</span></span>
   
    <span data-ttu-id="e370c-180">![將權限指派至群組](./media/data-lake-store-secure-data/adl.acl.4.png "將權限指派至群組")</span><span class="sxs-lookup"><span data-stu-id="e370c-180">![Assign permissions to group](./media/data-lake-store-secure-data/adl.acl.4.png "Assign permissions to group")</span></span>
   
    <span data-ttu-id="e370c-181">如需有關 Data Lake Store 中的權限及預設/存取 ACL 的詳細資訊，請參閱 [Data Lake Store 中的存取控制](data-lake-store-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="e370c-181">For more information about permissions in Data Lake Store, and Default/Access ACLs, see [Access Control in Data Lake Store](data-lake-store-access-control.md).</span></span>
6. <span data-ttu-id="e370c-182">在 [新增自訂存取] 刀鋒視窗中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e370c-182">In the **Add Custom Access** blade, click **OK**.</span></span> <span data-ttu-id="e370c-183">具有相關權限的新增群組現在會列在 [存取]  刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="e370c-183">The newly added group, with the associated permissions, will now be listed in the **Access** blade.</span></span>
   
    <span data-ttu-id="e370c-184">![將權限指派至群組](./media/data-lake-store-secure-data/adl.acl.5.png "將權限指派至群組")</span><span class="sxs-lookup"><span data-stu-id="e370c-184">![Assign permissions to group](./media/data-lake-store-secure-data/adl.acl.5.png "Assign permissions to group")</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="e370c-185">在目前的版本中，[自訂存取] 下方只能有 9 個項目。</span><span class="sxs-lookup"><span data-stu-id="e370c-185">In the current release, you can only have 9 entries under **Custom Access**.</span></span> <span data-ttu-id="e370c-186">如要新增超過 9 位使用者，您必須建立安全性群組、新增使用者至安全性群組，並新增存取權限給該資料湖儲存區帳戶的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e370c-186">If you want to add more than 9 users, you should create security groups, add users to security groups, add provide access to those security groups for the Data Lake Store account.</span></span>
   > 
   > 
7. <span data-ttu-id="e370c-187">如有需要，您也可以在新增群組之後修改存取權限。</span><span class="sxs-lookup"><span data-stu-id="e370c-187">If required, you can also modify the access permissions after you have added the group.</span></span> <span data-ttu-id="e370c-188">根據您是否要移除或指派該權限給安全性群組，選擇清除或選取每個權限類型的核取方塊 (讀取、寫入、執行)。</span><span class="sxs-lookup"><span data-stu-id="e370c-188">Clear or select the check box for each permission type (Read, Write, Execute) based on whether you want to remove or assign that permission to the security group.</span></span> <span data-ttu-id="e370c-189">按一下 [儲存] 儲存變更，或按一下 [捨棄] 復原變更。</span><span class="sxs-lookup"><span data-stu-id="e370c-189">Click **Save** to save the changes, or **Discard** to undo the changes.</span></span>

## <a name="set-ip-address-range-for-data-access"></a><span data-ttu-id="e370c-190">設定資料存取的 IP 位址範圍</span><span class="sxs-lookup"><span data-stu-id="e370c-190">Set IP address range for data access</span></span>
<span data-ttu-id="e370c-191">Azure Data Lake Store 可讓您進一步在網路層級鎖定資料存放區的存取。</span><span class="sxs-lookup"><span data-stu-id="e370c-191">Azure Data Lake Store enables you to further lock down access to your data store at network level.</span></span> <span data-ttu-id="e370c-192">您可以啟用防火牆、指定 IP 位址或為受信任的用戶端定義 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="e370c-192">You can enable firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="e370c-193">一旦啟用，只有具有定義範圍內 IP 位址的用戶端可以連線到存放區。</span><span class="sxs-lookup"><span data-stu-id="e370c-193">Once enabled, only clients that have the IP addresses within defined range can connect to the store.</span></span>

<span data-ttu-id="e370c-194">![防火牆設定和 IP 存取](./media/data-lake-store-secure-data/firewall-ip-access.png "防火牆設定和 IP 位址")</span><span class="sxs-lookup"><span data-stu-id="e370c-194">![Firewall settings and IP access](./media/data-lake-store-secure-data/firewall-ip-access.png "Firewall settings and IP address")</span></span>

## <a name="remove-security-groups-for-an-azure-data-lake-store-account"></a><span data-ttu-id="e370c-195">移除 Azure 資料湖儲存區帳戶的安全性群組</span><span class="sxs-lookup"><span data-stu-id="e370c-195">Remove security groups for an Azure Data Lake Store account</span></span>
<span data-ttu-id="e370c-196">當您從 Azure 資料湖儲存區帳戶移除安全性群組時，僅會變更使用 Azure 入口網站和 Azure 資源管理員 API 的帳戶上，其管理作業的存取。</span><span class="sxs-lookup"><span data-stu-id="e370c-196">When you remove security groups from Azure Data Lake Store accounts, you are only changing access to the management operations on the account using the Azure Portal and Azure Resource Manager APIs.</span></span>

1. <span data-ttu-id="e370c-197">在您的 [Data Lake Store 帳戶] 刀鋒視窗中，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="e370c-197">In your Data Lake Store account blade, click **Settings**.</span></span> <span data-ttu-id="e370c-198">從 [設定] 刀鋒視窗中，按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="e370c-198">From the **Settings** blade, click **Users**.</span></span>
   
    <span data-ttu-id="e370c-199">![指派安全性群組給 Azure Data Lake 帳戶](./media/data-lake-store-secure-data/adl.select.user.icon.png "指派安全性群組給 Azure Data Lake 帳戶")</span><span class="sxs-lookup"><span data-stu-id="e370c-199">![Assign security group to Azure Data Lake account](./media/data-lake-store-secure-data/adl.select.user.icon.png "Assign security group to Azure Data Lake account")</span></span>
2. <span data-ttu-id="e370c-200">在 [使用者]  刀鋒視窗中，按一下您要移除的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e370c-200">In the **Users** blade click the security group you want to remove.</span></span>
   
    <span data-ttu-id="e370c-201">![要移除的安全性群組](./media/data-lake-store-secure-data/adl.add.user.3.png "要移除的安全性群組")</span><span class="sxs-lookup"><span data-stu-id="e370c-201">![Security group to remove](./media/data-lake-store-secure-data/adl.add.user.3.png "Security group to remove")</span></span>
3. <span data-ttu-id="e370c-202">在安全性群組的刀鋒視窗中，按一下 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="e370c-202">In the blade for the security group, click **Remove**.</span></span>
   
    <span data-ttu-id="e370c-203">![已移除的安全性群組](./media/data-lake-store-secure-data/adl.remove.group.png "已移除的安全性群組")</span><span class="sxs-lookup"><span data-stu-id="e370c-203">![Security group removed](./media/data-lake-store-secure-data/adl.remove.group.png "Security group removed")</span></span>

## <a name="remove-security-group-acls-from-azure-data-lake-store-file-system"></a><span data-ttu-id="e370c-204">從 Azure 資料湖儲存區檔案系統移除安全性群組 ACL</span><span class="sxs-lookup"><span data-stu-id="e370c-204">Remove security group ACLs from Azure Data Lake Store file system</span></span>
<span data-ttu-id="e370c-205">當您從 Azure 資料湖儲存區檔案系統中移除安全性群組 ACL 時，會變更資料湖儲存區資料的存取。</span><span class="sxs-lookup"><span data-stu-id="e370c-205">When you remove security groups ACLs from Azure Data Lake Store file system, you change access to the data in the Data Lake Store.</span></span>

1. <span data-ttu-id="e370c-206">在您的 [資料湖儲存區帳戶] 刀鋒視窗中，按一下 [資料總管] 。</span><span class="sxs-lookup"><span data-stu-id="e370c-206">In your Data Lake Store account blade, click **Data Explorer**.</span></span>
   
    <span data-ttu-id="e370c-207">![在 Data Lake 帳戶中建立目錄](./media/data-lake-store-secure-data/adl.start.data.explorer.png "在 Data Lake 帳戶中建立目錄")</span><span class="sxs-lookup"><span data-stu-id="e370c-207">![Create directories in Data Lake account](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Create directories in Data Lake account")</span></span>
2. <span data-ttu-id="e370c-208">在 [資料總管] 刀鋒視窗中，按一下您要將移除 ACL 的檔案或資料夾，然後在您的帳戶刀鋒視窗中按一下 [存取] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e370c-208">In the **Data Explorer** blade, click the file or folder for which you want to remove the ACL, and then in your account blade, click the **Access** icon.</span></span> <span data-ttu-id="e370c-209">若要移除檔案的 ACL，您必須從 [檔案預覽] 刀鋒視窗按一下 [存取]。</span><span class="sxs-lookup"><span data-stu-id="e370c-209">To remove ACL for a file, you must click **Access** from the **File Preview** blade.</span></span>
   
    <span data-ttu-id="e370c-210">![設定 Data Lake 檔案系統上的 ACL](./media/data-lake-store-secure-data/adl.acl.1.png "設定 Data Lake 檔案系統上的 ACL")</span><span class="sxs-lookup"><span data-stu-id="e370c-210">![Set ACLs on Data Lake file system](./media/data-lake-store-secure-data/adl.acl.1.png "Set ACLs on Data Lake file system")</span></span>
3. <span data-ttu-id="e370c-211">從 [存取] 刀鋒視窗中的 [自訂存取] 區段，按一下您要移除的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e370c-211">In the **Access** blade, from the **Custom Access** section, click the security group you want to remove.</span></span> <span data-ttu-id="e370c-212">在 [自訂存取] 刀鋒視窗中，按一下 [移除]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e370c-212">In the **Custom Access** blade, click **Remove** and then click **OK**.</span></span>
   
    <span data-ttu-id="e370c-213">![將權限指派至群組](./media/data-lake-store-secure-data/adl.remove.acl.png "將權限指派至群組")</span><span class="sxs-lookup"><span data-stu-id="e370c-213">![Assign permissions to group](./media/data-lake-store-secure-data/adl.remove.acl.png "Assign permissions to group")</span></span>

## <a name="see-also"></a><span data-ttu-id="e370c-214">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e370c-214">See also</span></span>
* [<span data-ttu-id="e370c-215">Azure Data Lake Store 概觀</span><span class="sxs-lookup"><span data-stu-id="e370c-215">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="e370c-216">將資料從 Azure 儲存體 Blob 複製到資料湖存放區</span><span class="sxs-lookup"><span data-stu-id="e370c-216">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="e370c-217">搭配資料湖存放區使用 Azure 資料湖分析</span><span class="sxs-lookup"><span data-stu-id="e370c-217">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="e370c-218">搭配資料湖存放區使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e370c-218">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="e370c-219">使用 PowerShell 開始使用資料湖存放區</span><span class="sxs-lookup"><span data-stu-id="e370c-219">Get Started with Data Lake Store using PowerShell</span></span>](data-lake-store-get-started-powershell.md)
* [<span data-ttu-id="e370c-220">使用 .NET SDK 開始使用資料湖存放區</span><span class="sxs-lookup"><span data-stu-id="e370c-220">Get Started with Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="e370c-221">存取 Data Lake Store 的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="e370c-221">Access diagnostic logs for Data Lake Store</span></span>](data-lake-store-diagnostic-logs.md)

