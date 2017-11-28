---
title: "設定 Azure Active Directory 驗證 - SQL | Microsoft Docs"
description: "了解如何使用 Azure Active Directory 驗證連接到 SQL Database 與 SQL 資料倉儲。"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: 61a52813769891aa63373437e9300d4f8f47fab2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a><span data-ttu-id="ae669-103">使用 SQL Database 或 SQL 資料倉儲設定和管理 Azure Active Directory 驗證</span><span class="sxs-lookup"><span data-stu-id="ae669-103">Configure and manage Azure Active Directory authentication with SQL Database or SQL Data Warehouse</span></span>

<span data-ttu-id="ae669-104">本文說明如何建立和填入 Azure AD，以及搭配 Azure SQL Database 和 SQL 資料倉儲使用 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="ae669-104">This article shows you how to create and populate Azure AD, and then use Azure AD with Azure SQL Database and SQL Data Warehouse.</span></span> <span data-ttu-id="ae669-105">如需概觀，請參閱 [Azure Active Directory 驗證](sql-database-aad-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="ae669-105">For an overview, see [Azure Active Directory Authentication](sql-database-aad-authentication.md).</span></span>

>  [!NOTE]  
>  <span data-ttu-id="ae669-106">使用 Azure Active Directory 帳戶不支援連線到 Azure VM 上執行的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="ae669-106">Connecting to SQL Server running on an Azure VM is not supported using an Azure Active Directory account.</span></span> <span data-ttu-id="ae669-107">請改用 Active Directory 網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae669-107">Use a domain Active Directory account instead.</span></span>

## <a name="create-and-populate-an-azure-ad"></a><span data-ttu-id="ae669-108">建立和填入 Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae669-108">Create and populate an Azure AD</span></span>
<span data-ttu-id="ae669-109">建立 Azure AD 並利用使用者和群組填入。</span><span class="sxs-lookup"><span data-stu-id="ae669-109">Create an Azure AD and populate it with users and groups.</span></span> <span data-ttu-id="ae669-110">Azure AD 可以是初始網域 Azure AD 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="ae669-110">Azure AD can be the initial domain Azure AD managed domain.</span></span> <span data-ttu-id="ae669-111">Azure AD 也可以是與 Azure AD 同盟的內部部署 Active Directory 網域服務。</span><span class="sxs-lookup"><span data-stu-id="ae669-111">Azure AD can also be an on-premises Active Directory Domain Services that is federated with the Azure AD.</span></span>

<span data-ttu-id="ae669-112">如需詳細資訊，請參閱[整合內部部署身分識別與 Azure Active Directory](../active-directory/active-directory-aadconnect.md)、[將您自己的網域名稱新增至 Azure AD](../active-directory/active-directory-add-domain.md)、[Microsoft Azure 現在支援與 Windows Server Active Directory 同盟](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)、[管理您的 Azure AD 目錄](https://msdn.microsoft.com/library/azure/hh967611.aspx)、[使用 Windows PowerShell 管理 Azure AD](/powershell/azure/overview?view=azureadps-2.0) 和[混合式身分識別所需的連接埠和通訊協定](../active-directory/active-directory-aadconnect-ports.md)。</span><span class="sxs-lookup"><span data-stu-id="ae669-112">For more information, see [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name to Azure AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Manage Azure AD using Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), and [Hybrid Identity Required Ports and Protocols](../active-directory/active-directory-aadconnect-ports.md).</span></span>

## <a name="optional-associate-or-change-the-active-directory-that-is-currently-associated-with-your-azure-subscription"></a><span data-ttu-id="ae669-113">選用：和目前與您的 Azure 訂用帳戶相關聯的 active directory 產生關聯並加以變更</span><span class="sxs-lookup"><span data-stu-id="ae669-113">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
<span data-ttu-id="ae669-114">若要將您的資料庫與貴組織的 Azure AD 目錄產生關聯，請讓目錄成為裝載資料庫之 Azure 訂用帳戶信任的目錄。</span><span class="sxs-lookup"><span data-stu-id="ae669-114">To associate your database with the Azure AD directory for your organization, make the directory a trusted directory for the Azure subscription hosting the database.</span></span> <span data-ttu-id="ae669-115">如需詳細資訊，請參閱 [Azure 訂用帳戶如何與 Azure AD 產生關聯](https://msdn.microsoft.com/library/azure/dn629581.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ae669-115">For more information, see [How Azure subscriptions are associated with Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx).</span></span>

<span data-ttu-id="ae669-116">**其他資訊：** 每個 Azure 訂用帳戶都會與 Azure AD 執行個體有信任關係。</span><span class="sxs-lookup"><span data-stu-id="ae669-116">**Additional information:** Every Azure subscription has a trust relationship with an Azure AD instance.</span></span> <span data-ttu-id="ae669-117">這表示它信任該目錄來驗證使用者、服務和裝置。</span><span class="sxs-lookup"><span data-stu-id="ae669-117">This means that it trusts that directory to authenticate users, services, and devices.</span></span> <span data-ttu-id="ae669-118">多個訂用帳戶可以信任相同的目錄，但是一個訂用帳戶只能信任一個目錄。</span><span class="sxs-lookup"><span data-stu-id="ae669-118">Multiple subscriptions can trust the same directory, but a subscription trusts only one directory.</span></span> <span data-ttu-id="ae669-119">您可以在 [設定]  索引標籤下的 [https://manage.windowsazure.com/](https://manage.windowsazure.com/)看到訂用帳戶所信任的目錄。</span><span class="sxs-lookup"><span data-stu-id="ae669-119">You can see which directory is trusted by your subscription under the **Settings** tab at [https://manage.windowsazure.com/](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="ae669-120">這個訂用帳戶與目錄之間存在的信任關係不同於訂用帳戶與所有其他 Azure 資源 (網站、資料庫等) 之間的關係，後者比較像是訂用帳戶的子資源。</span><span class="sxs-lookup"><span data-stu-id="ae669-120">This trust relationship that a subscription has with a directory is unlike the relationship that a subscription has with all other resources in Azure (websites, databases, and so on), which are more like child resources of a subscription.</span></span> <span data-ttu-id="ae669-121">如果訂用帳戶已過期，則也會停止存取與該訂用帳戶相關聯的其他資源。</span><span class="sxs-lookup"><span data-stu-id="ae669-121">If a subscription expires, then access to those other resources associated with the subscription also stops.</span></span> <span data-ttu-id="ae669-122">但目錄會保留在 Azure 中，而且您可以將其他訂用帳戶與該目錄產生關聯，並繼續管理目錄使用者。</span><span class="sxs-lookup"><span data-stu-id="ae669-122">But the directory remains in Azure, and you can associate another subscription with that directory and continue to manage the directory users.</span></span> <span data-ttu-id="ae669-123">如需有關資源的詳細資訊，請參閱 [了解 Azure 中的資源存取](https://msdn.microsoft.com/library/azure/dn584083.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ae669-123">For more information about resources, see [Understanding resource access in Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).</span></span>

<span data-ttu-id="ae669-124">下列程序會示範如何變更特定訂用帳戶的相關聯目錄。</span><span class="sxs-lookup"><span data-stu-id="ae669-124">The following procedures show you how to change the associated directory for a given subscription.</span></span>
1. <span data-ttu-id="ae669-125">使用 Azure 訂用帳戶管理員連接到您的 [Azure 傳統入口網站](https://manage.windowsazure.com/) 。</span><span class="sxs-lookup"><span data-stu-id="ae669-125">Connect to your [Azure Classic Portal](https://manage.windowsazure.com/) by using an Azure subscription administrator.</span></span>
2. <span data-ttu-id="ae669-126">在左邊的橫幅中，選取 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="ae669-126">On the left banner, select **SETTINGS**.</span></span>
3. <span data-ttu-id="ae669-127">您的訂用帳戶會出現在 [設定] 畫面中。</span><span class="sxs-lookup"><span data-stu-id="ae669-127">Your subscriptions appear in the settings screen.</span></span> <span data-ttu-id="ae669-128">如果未出現所需的訂用帳戶，請按一下頂端的 [訂用帳戶]，拉下 [依目錄篩選] 方塊並選取包含您訂用帳戶的目錄，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="ae669-128">If the desired subscription does not appear, click **Subscriptions** at the top, drop down the **FILTER BY DIRECTORY** box and select the directory that contains your subscriptions, and then click **APPLY**.</span></span>
   
    ![select subscription][4]
4. <span data-ttu-id="ae669-130">在 [設定] 區域中，按一下您的訂用帳戶，然後按一下頁面底部的 [編輯目錄]。</span><span class="sxs-lookup"><span data-stu-id="ae669-130">In the **settings** area, click your subscription, and then click  **EDIT DIRECTORY** at the bottom of the page.</span></span>
   
    ![ad-settings-portal][5]
5. <span data-ttu-id="ae669-132">在 [編輯目錄]  方塊中，選取與您的 SQL Server 或 SQL 資料倉儲相關聯的 Azure Active Directory，然後按一下箭號進行下一步。</span><span class="sxs-lookup"><span data-stu-id="ae669-132">In the **EDIT DIRECTORY** box, select the Azure Active Directory that is associated with your SQL Server or SQL Data Warehouse, and then click the arrow for next.</span></span>
   
    ![edit-directory-select][6]
6. <span data-ttu-id="ae669-134">在 [確認目錄對應] 對話方塊中，確認「**將移除所有的共同管理員**」。</span><span class="sxs-lookup"><span data-stu-id="ae669-134">In the **CONFIRM** directory Mapping dialog box, confirm that "**All co-administrators will be removed.**"</span></span>
   
    ![edit-directory-confirm][7]
7. <span data-ttu-id="ae669-136">按一下核取記號重新載入入口網站。</span><span class="sxs-lookup"><span data-stu-id="ae669-136">Click the check to reload the portal.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ae669-137">當您變更目錄時，所有共同管理員、Azure AD 使用者和群組以及以目錄為基礎之資源使用者的存取權都會被移除，他們將不再有此訂用帳戶或其資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="ae669-137">When you change the directory, access to all co-administrators, Azure AD users and groups, and directory-backed resource users are removed and they no longer have access to this subscription or its resources.</span></span> <span data-ttu-id="ae669-138">只有具備服務管理員身分的您能夠根據新的目錄設定主體的存取權。</span><span class="sxs-lookup"><span data-stu-id="ae669-138">Only you, as a service administrator, can configure access for principals based on the new directory.</span></span> <span data-ttu-id="ae669-139">這項變更可能需要相當長的時間才會傳播到所有資源。</span><span class="sxs-lookup"><span data-stu-id="ae669-139">This change might take a substantial amount of time to propagate to all resources.</span></span> <span data-ttu-id="ae669-140">變更目錄也會變更 SQL Database 和「SQL 資料倉儲」的 Azure AD 系統管理員，並且不允許任何現有 Azure AD 使用者進行資料庫存取。</span><span class="sxs-lookup"><span data-stu-id="ae669-140">Changing the directory, also changes the Azure AD administrator for SQL Database and SQL Data Warehouse and disallow database access for any existing Azure AD users.</span></span> <span data-ttu-id="ae669-141">必須重設 Azure AD 系統管理員 (如下所述) 且必須建立新的 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="ae669-141">The Azure AD admin must be reset (as described below) and new Azure AD users must be created.</span></span>
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a><span data-ttu-id="ae669-142">建立 Azure SQL 伺服器的 Azure AD 系統管理員</span><span class="sxs-lookup"><span data-stu-id="ae669-142">Create an Azure AD administrator for Azure SQL server</span></span>
<span data-ttu-id="ae669-143">每個 Azure SQL 伺服器 (裝載 SQL Database 或「SQL 資料倉儲」) 一開始都只有一個伺服器系統管理員帳戶，也就是整個 Azure SQL 伺服器的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ae669-143">Each Azure SQL server (which hosts a SQL Database or SQL Data Warehouse) starts with a single server administrator account that is the administrator of the entire Azure SQL server.</span></span> <span data-ttu-id="ae669-144">第二個 SQL Server 系統管理員必須建立，也就是 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae669-144">A second SQL Server administrator must be created, that is an Azure AD account.</span></span> <span data-ttu-id="ae669-145">這個主體會在 master 資料庫中建立為自主資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="ae669-145">This principal is created as a contained database user in the master database.</span></span> <span data-ttu-id="ae669-146">身為系統管理員，伺服器系統管理員帳戶是每個使用者資料庫中的 **db_owner** 角色成員，並且會進入每個使用者資料庫做為 **dbo** 使用者。</span><span class="sxs-lookup"><span data-stu-id="ae669-146">As administrators, the server administrator accounts are members of the **db_owner** role in every user database, and enter each user database as the **dbo** user.</span></span> <span data-ttu-id="ae669-147">如需有關伺服器管理員帳戶的詳細資訊，請參閱[管理 Azure SQL Database 的資料庫和登入](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="ae669-147">For more information about the server administrator accounts, see [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md).</span></span>

<span data-ttu-id="ae669-148">將 Azure Active Directory 與異地複寫搭配使用時，必須為主要和次要伺服器設定 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ae669-148">When using Azure Active Directory with geo-replication, the Azure Active Directory administrator must be configured for both the primary and the secondary servers.</span></span> <span data-ttu-id="ae669-149">如果伺服器沒有 Azure Active Directory 系統管理員，則 Azure Active Directory 登入和使用者將會收到「無法連線至伺服器」錯誤。</span><span class="sxs-lookup"><span data-stu-id="ae669-149">If a server does not have an Azure Active Directory administrator, then Azure Active Directory logins and users receive a "Cannot connect" to server error.</span></span>

> [!NOTE]
> <span data-ttu-id="ae669-150">使用者如果不是以 Azure AD 帳戶 (包括 Azure SQL 伺服器系統管理員帳戶) 為基礎，就無法建立以 Azure AD 為基礎的使用者，因為他們不具備向 Azure AD 驗證建議之資料庫使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="ae669-150">Users that are not based on an Azure AD account (including the Azure SQL server administrator account), cannot create Azure AD-based users, because they do not have permission to validate proposed database users with the Azure AD.</span></span>
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a><span data-ttu-id="ae669-151">佈建 Azure SQL 伺服器的 Azure Active Directory 系統管理員</span><span class="sxs-lookup"><span data-stu-id="ae669-151">Provision an Azure Active Directory administrator for your Azure SQL server</span></span>

<span data-ttu-id="ae669-152">下列兩個程序會示範如何在 Azure 入口網站以及使用 PowerShell，佈建 Azure SQL 伺服器的 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ae669-152">The following two procedures show you how to provision an Azure Active Directory administrator for your Azure SQL server in the Azure portal and by using PowerShell.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="ae669-153">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ae669-153">Azure portal</span></span>
1. <span data-ttu-id="ae669-154">在 [Azure 入口網站](https://portal.azure.com/)的右上角，按一下您的連線以拉下可能的 Active Directory 清單。</span><span class="sxs-lookup"><span data-stu-id="ae669-154">In the [Azure portal](https://portal.azure.com/), in the upper-right corner, click your connection to drop down a list of possible Active Directories.</span></span> <span data-ttu-id="ae669-155">選擇正確的 Active Directory 做為預設 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="ae669-155">Choose the correct Active Directory as the default Azure AD.</span></span> <span data-ttu-id="ae669-156">此步驟利用 Azure SQL 伺服器連結與 Active Directory 相關聯的訂用帳戶，確定 Azure AD 和 SQL Server 使用相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae669-156">This step links the subscription association with Active Directory with Azure SQL server making sure that the same subscription is used for both Azure AD and SQL Server.</span></span> <span data-ttu-id="ae669-157">(Azure SQL 伺服器可以裝載 Azure SQL Database 或 Azure SQL 資料倉儲。)</span><span class="sxs-lookup"><span data-stu-id="ae669-157">(The Azure SQL server can be hosting either Azure SQL Database or Azure SQL Data Warehouse.)</span></span>   
    <span data-ttu-id="ae669-158">![choose-ad][8]</span><span class="sxs-lookup"><span data-stu-id="ae669-158">![choose-ad][8]</span></span>   
    
2. <span data-ttu-id="ae669-159">在左邊的橫幅中，選取 [SQL Server]，並選取您的 **SQL Server**，然後在 [SQL Server] 刀鋒視窗中按一下 [Active Directory 系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="ae669-159">In the left banner select **SQL servers**, select your **SQL server**, and then in the **SQL Server** blade, click **Active Directory admin**.</span></span>   
3. <span data-ttu-id="ae669-160">在 [Active Directory 系統管理員] 刀鋒視窗中，按一下 [設定系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="ae669-160">In the **Active Directory admin** blade, click **Set admin**.</span></span>   
    <span data-ttu-id="ae669-161">![選取 Active Directory](./media/sql-database-aad-authentication/select-active-directory.png)</span><span class="sxs-lookup"><span data-stu-id="ae669-161">![select active directory](./media/sql-database-aad-authentication/select-active-directory.png)</span></span>  
    
4. <span data-ttu-id="ae669-162">在 [新增系統管理員] 刀鋒視窗中，搜尋使用者，選取使用者或群組成為系統管理員，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="ae669-162">In the **Add admin** blade, search for a user, select the user or group to be an administrator, and then click **Select**.</span></span> <span data-ttu-id="ae669-163">([Active Directory 系統管理員] 刀鋒視窗會顯示您 Active Directory 的所有成員與群組。</span><span class="sxs-lookup"><span data-stu-id="ae669-163">(The Active Directory admin blade shows all members and groups of your Active Directory.</span></span> <span data-ttu-id="ae669-164">呈現灰色的使用者或群組無法選取，因為他們不受支援成為 Azure AD 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ae669-164">Users or groups that are grayed out cannot be selected because they are not supported as Azure AD administrators.</span></span> <span data-ttu-id="ae669-165">(請在[利用 SQL Database 或 SQL 資料倉儲使用 Azure Active Directory 驗證來驗證](sql-database-aad-authentication.md)的＜Azure AD 功能和限制＞節中參閱支援的系統管理員清單。)以角色為基礎的存取控制 (RBAC) 只會套用至入口網站，並且不會傳播至 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="ae669-165">(See the list of supported admins in the **Azure AD Features and Limitations** section of [Use Azure Active Directory Authentication for authentication with SQL Database or SQL Data Warehouse](sql-database-aad-authentication.md).) Role-based access control (RBAC) applies only to the portal and is not propagated to SQL Server.</span></span>   
    <span data-ttu-id="ae669-166">![選取系統管理員](./media/sql-database-aad-authentication/select-admin.png)</span><span class="sxs-lookup"><span data-stu-id="ae669-166">![select admin](./media/sql-database-aad-authentication/select-admin.png)</span></span>  
    
5. <span data-ttu-id="ae669-167">在 [Active Directory 系統管理員] 刀鋒視窗頂端，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ae669-167">At the top of the **Active Directory admin** blade, click **SAVE**.</span></span>   
    <span data-ttu-id="ae669-168">![儲存系統管理員](./media/sql-database-aad-authentication/save-admin.png)</span><span class="sxs-lookup"><span data-stu-id="ae669-168">![save admin](./media/sql-database-aad-authentication/save-admin.png)</span></span>   

<span data-ttu-id="ae669-169">變更系統管理員的程序可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="ae669-169">The process of changing the administrator may take several minutes.</span></span> <span data-ttu-id="ae669-170">接著，新的系統管理員就會出現在 [Active Directory 系統管理員]  方塊中。</span><span class="sxs-lookup"><span data-stu-id="ae669-170">Then the new administrator appears in the **Active Directory admin** box.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ae669-171">設定 Azure AD 系統管理員時，新的系統管理員名稱 (使用者或群組) 不可以已經存在於虛擬主要資料庫中作為 SQL Server 驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="ae669-171">When setting up the Azure AD admin, the new admin name (user or group) cannot already be present in the virtual master database as a SQL Server authentication user.</span></span> <span data-ttu-id="ae669-172">如果存在，Azure AD 系統管理員設定將會失敗；其中會復原其建立並指出這樣的系統管理員 (名稱) 已經存在。</span><span class="sxs-lookup"><span data-stu-id="ae669-172">If present, the Azure AD admin setup will fail; rolling back its creation and indicating that such an admin (name) already exists.</span></span> <span data-ttu-id="ae669-173">由於這類 SQL Server 驗證使用者並非 Azure AD 的成員，因此使用 Azure AD 驗證來連線到伺服器的一切努力都會失敗。</span><span class="sxs-lookup"><span data-stu-id="ae669-173">Since such a SQL Server authentication user is not part of the Azure AD, any effort to connect to the server using Azure AD authentication fails.</span></span>
   > 


<span data-ttu-id="ae669-174">若要稍後移除系統管理員，請在 [Active Directory 系統管理員] 刀鋒視窗頂端，按一下 [移除系統管理員]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ae669-174">To later remove an Admin, at the top of the **Active Directory admin** blade, click **Remove admin**, and then click **Save**.</span></span>

### <a name="powershell"></a><span data-ttu-id="ae669-175">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae669-175">PowerShell</span></span>
<span data-ttu-id="ae669-176">若要執行 PowerShell Cmdlet，Azure PowerShell 必須已安裝且正在執行中。</span><span class="sxs-lookup"><span data-stu-id="ae669-176">To run PowerShell cmdlets, you need to have Azure PowerShell installed and running.</span></span> <span data-ttu-id="ae669-177">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ae669-177">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="ae669-178">若要佈建 Azure AD 系統管理員，請執行下列 Azure PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="ae669-178">To provision an Azure AD admin, execute the following Azure PowerShell commands:</span></span>

* <span data-ttu-id="ae669-179">Add-AzureRmAccount</span><span class="sxs-lookup"><span data-stu-id="ae669-179">Add-AzureRmAccount</span></span>
* <span data-ttu-id="ae669-180">Select-AzureRmSubscription</span><span class="sxs-lookup"><span data-stu-id="ae669-180">Select-AzureRmSubscription</span></span>

<span data-ttu-id="ae669-181">用來佈建和管理 Azure AD 系統管理員的 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="ae669-181">Cmdlets used to provision and manage Azure AD admin:</span></span>

| <span data-ttu-id="ae669-182">Cmdlet 名稱</span><span class="sxs-lookup"><span data-stu-id="ae669-182">Cmdlet name</span></span> | <span data-ttu-id="ae669-183">說明</span><span class="sxs-lookup"><span data-stu-id="ae669-183">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="ae669-184">Set-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="ae669-184">Set-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="ae669-185">佈建 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員 (必須來自目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae669-185">Provisions an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ae669-186">)</span><span class="sxs-lookup"><span data-stu-id="ae669-186">(Must be from the current subscription.)</span></span> |
| [<span data-ttu-id="ae669-187">Remove-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="ae669-187">Remove-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="ae669-188">移除 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ae669-188">Removes an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> |
| [<span data-ttu-id="ae669-189">Get-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="ae669-189">Get-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="ae669-190">傳回目前為 Azure SQL 伺服器或 Azure SQL 資料倉儲設定的 Azure Active Directory 系統管理員的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ae669-190">Returns information about an Azure Active Directory administrator currently configured for the Azure SQL server or Azure SQL Data Warehouse.</span></span> |

<span data-ttu-id="ae669-191">使用 PowerShell 命令 get-help 來查看這當中每個命令的詳細資料，例如 ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``。</span><span class="sxs-lookup"><span data-stu-id="ae669-191">Use PowerShell command get-help to see more details for each of these commands, for example ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.</span></span>

<span data-ttu-id="ae669-192">下列指令碼會在名為 **Group-23** 的資源群組中，為 **demo_server** 伺服器佈建名為 **DBA_Group** (物件識別碼 `40b79501-b343-44ed-9ce7-da4c8cc7353f`) 的 Azure AD 系統管理員群組：</span><span class="sxs-lookup"><span data-stu-id="ae669-192">The following script provisions an Azure AD administrator group named **DBA_Group** (object id `40b79501-b343-44ed-9ce7-da4c8cc7353f`) for the **demo_server** server in a resource group named **Group-23**:</span></span>

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

<span data-ttu-id="ae669-193">**DisplayName** 輸入參數可接受 Azure AD 顯示名稱或「使用者主體名稱」。</span><span class="sxs-lookup"><span data-stu-id="ae669-193">The **DisplayName** input parameter accepts either the Azure AD display name or the User Principal Name.</span></span> <span data-ttu-id="ae669-194">例如 ``DisplayName="John Smith"`` 和 ``DisplayName="johns@contoso.com"``。</span><span class="sxs-lookup"><span data-stu-id="ae669-194">For example, ``DisplayName="John Smith"`` and ``DisplayName="johns@contoso.com"``.</span></span> <span data-ttu-id="ae669-195">Azure AD 群組只支援 Azure AD 顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="ae669-195">For Azure AD groups only the Azure AD display name is supported.</span></span>

> [!NOTE]
> <span data-ttu-id="ae669-196">Azure PowerShell 命令 ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` 不會阻止您為不支援的使用者佈建 Azure AD 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ae669-196">The Azure PowerShell  command ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` does not prevent you from provisioning Azure AD admins for unsupported users.</span></span> <span data-ttu-id="ae669-197">您可以佈建不支援的使用者，但是該使用者無法連線到資料庫。</span><span class="sxs-lookup"><span data-stu-id="ae669-197">An unsupported user can be provisioned, but can not connect to a database.</span></span> 
> 

<span data-ttu-id="ae669-198">下列範例使用選用的 **ObjectID**：</span><span class="sxs-lookup"><span data-stu-id="ae669-198">The following example uses the optional **ObjectID**:</span></span>

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> <span data-ttu-id="ae669-199">當 **DisplayName** 並非唯一時，就需要 Azure AD **ObjectID**。</span><span class="sxs-lookup"><span data-stu-id="ae669-199">The Azure AD **ObjectID** is required when the **DisplayName** is not unique.</span></span> <span data-ttu-id="ae669-200">若要擷取 **ObjectID** 和 **DisplayName** 的值，請使用 Azure 傳統入口網站的 [Active Directory] 區段，然後檢視使用者或群組的屬性。</span><span class="sxs-lookup"><span data-stu-id="ae669-200">To retrieve the **ObjectID** and **DisplayName** values, use the Active Directory section of Azure Classic Portal, and view the properties of a user or group.</span></span>
> 

<span data-ttu-id="ae669-201">下列範例會傳回 Azure SQL 伺服器的目前 Azure AD 系統管理員的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="ae669-201">The following example returns information about the current Azure AD admin for Azure SQL server:</span></span>

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

<span data-ttu-id="ae669-202">下列範例會移除 Azure AD 系統管理員：</span><span class="sxs-lookup"><span data-stu-id="ae669-202">The following example removes an Azure AD administrator:</span></span>

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

<span data-ttu-id="ae669-203">您也可以使用 REST API 來佈建 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ae669-203">You can also provision an Azure Active Directory Administrator by using the REST APIs.</span></span> <span data-ttu-id="ae669-204">如需詳細資訊，請參閱 [Azure SQL Database 之 Azure SQL Database 作業的 Service Management REST API 參考和作業](https://msdn.microsoft.com/library/azure/dn505719.aspx)</span><span class="sxs-lookup"><span data-stu-id="ae669-204">For more information, see [Service Management REST API Reference and Operations for Azure SQL Databases Operations for Azure SQL Databases](https://msdn.microsoft.com/library/azure/dn505719.aspx)</span></span>

### <a name="cli"></a><span data-ttu-id="ae669-205">CLI</span><span class="sxs-lookup"><span data-stu-id="ae669-205">CLI</span></span>  
<span data-ttu-id="ae669-206">您也可以呼叫下列 CLI 命令來佈建 Azure AD 系統管理員：</span><span class="sxs-lookup"><span data-stu-id="ae669-206">You can also provision an Azure AD admin by calling the following CLI commands:</span></span>
| <span data-ttu-id="ae669-207">命令</span><span class="sxs-lookup"><span data-stu-id="ae669-207">Command</span></span> | <span data-ttu-id="ae669-208">說明</span><span class="sxs-lookup"><span data-stu-id="ae669-208">Description</span></span> |
| --- | --- |
|[<span data-ttu-id="ae669-209">az sql server ad-admin create</span><span class="sxs-lookup"><span data-stu-id="ae669-209">az sql server ad-admin create</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |<span data-ttu-id="ae669-210">佈建 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員 (必須來自目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae669-210">Provisions an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ae669-211">)</span><span class="sxs-lookup"><span data-stu-id="ae669-211">(Must be from the current subscription.)</span></span> |
|[<span data-ttu-id="ae669-212">az sql server ad-admin delete</span><span class="sxs-lookup"><span data-stu-id="ae669-212">az sql server ad-admin delete</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |<span data-ttu-id="ae669-213">移除 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ae669-213">Removes an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> |
|[<span data-ttu-id="ae669-214">az sql server ad-admin list</span><span class="sxs-lookup"><span data-stu-id="ae669-214">az sql server ad-admin list</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |<span data-ttu-id="ae669-215">傳回目前為 Azure SQL 伺服器或 Azure SQL 資料倉儲設定的 Azure Active Directory 系統管理員的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ae669-215">Returns information about an Azure Active Directory administrator currently configured for the Azure SQL server or Azure SQL Data Warehouse.</span></span> |
|[<span data-ttu-id="ae669-216">az sql server ad-admin update</span><span class="sxs-lookup"><span data-stu-id="ae669-216">az sql server ad-admin update</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |<span data-ttu-id="ae669-217">更新 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ae669-217">Updates the Active Directory administrator for an Azure SQL server or Azure SQL Data Warehouse.</span></span> |

<span data-ttu-id="ae669-218">如需 CLI 命令的詳細資訊，請參閱 [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server)。</span><span class="sxs-lookup"><span data-stu-id="ae669-218">For more information about CLI commands, see [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server).</span></span>  


## <a name="configure-your-client-computers"></a><span data-ttu-id="ae669-219">設定用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="ae669-219">Configure your client computers</span></span>
<span data-ttu-id="ae669-220">在您的應用程式或使用者使用 Azure AD 身分識別連接到 Azure SQL Database 或 Azure SQL 資料倉儲的所有用戶端電腦上，您必須安裝下列軟體：</span><span class="sxs-lookup"><span data-stu-id="ae669-220">On all client machines, from which your applications or users connect to Azure SQL Database or Azure SQL Data Warehouse using Azure AD identities, you must install the following software:</span></span>

* <span data-ttu-id="ae669-221">從 [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx)安裝 .NET Framework 4.6 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ae669-221">.NET Framework 4.6 or later from [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span></span>
* <span data-ttu-id="ae669-222">從下載中心的**Microsoft Active Directory Authentication Library for Microsoft SQL Server**，可以下載多種語言 (x86 和 amd64) 的 Azure Active Directory Authentication Library for SQL Server ( [ADALSQL.DLL](http://www.microsoft.com/download/details.aspx?id=48742))。</span><span class="sxs-lookup"><span data-stu-id="ae669-222">Azure Active Directory Authentication Library for SQL Server (**ADALSQL.DLL**) is available in multiple languages (both x86 and amd64) from the download center at [Microsoft Active Directory Authentication Library for Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).</span></span>

<span data-ttu-id="ae669-223">您可以符合這些需求，方法如下︰</span><span class="sxs-lookup"><span data-stu-id="ae669-223">You can meet these requirements by:</span></span>

* <span data-ttu-id="ae669-224">安裝 [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 或 [SQL Server Data Tools for Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) 皆可符合 .NET Framework 4.6 需求。</span><span class="sxs-lookup"><span data-stu-id="ae669-224">Installing either [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) or [SQL Server Data Tools for Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) meets the .NET Framework 4.6 requirement.</span></span>
* <span data-ttu-id="ae669-225">SSMS 安裝 x86 版 **ADALSQL.DLL**。</span><span class="sxs-lookup"><span data-stu-id="ae669-225">SSMS installs the x86 version of **ADALSQL.DLL**.</span></span>
* <span data-ttu-id="ae669-226">SSDT 會安裝 amd64 版的 **ADALSQL.DLL**。</span><span class="sxs-lookup"><span data-stu-id="ae669-226">SSDT installs the amd64 version of **ADALSQL.DLL**.</span></span>
* <span data-ttu-id="ae669-227">來自 [Visual Studio 下載](https://www.visualstudio.com/downloads/download-visual-studio-vs) 的最新 Visual Studio 符合 .NET Framework 4.6 需求，但不會安裝必要的 amd64 版 **ADALSQL.DLL**。</span><span class="sxs-lookup"><span data-stu-id="ae669-227">The latest Visual Studio from [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) meets the .NET Framework 4.6 requirement, but does not install the required amd64 version of **ADALSQL.DLL**.</span></span>

## <a name="create-contained-database-users-in-your-database-mapped-to-azure-ad-identities"></a><span data-ttu-id="ae669-228">在對應至 Azure AD 身分識別的資料庫中建立自主資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="ae669-228">Create contained database users in your database mapped to Azure AD identities</span></span>

<span data-ttu-id="ae669-229">Azure Active Directory 驗證需要建立資料庫使用者做為自主資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="ae669-229">Azure Active Directory authentication requires database users to be created as contained database users.</span></span> <span data-ttu-id="ae669-230">以 Azure AD 身分識別為基礎的自主資料庫使用者係指在 master 資料庫中沒有登入身分的資料庫使用者，並且此使用者會對應至 Azure AD 目錄中與資料庫關聯的身分識別。</span><span class="sxs-lookup"><span data-stu-id="ae669-230">A contained database user based on an Azure AD identity, is a database user that does not have a login in the master database, and which maps to an identity in the Azure AD directory that is associated with the database.</span></span> <span data-ttu-id="ae669-231">Azure AD 身分識別可以是個別的使用者帳戶或群組。</span><span class="sxs-lookup"><span data-stu-id="ae669-231">The Azure AD identity can be either an individual user account or a group.</span></span> <span data-ttu-id="ae669-232">如需有關自主資料庫使用者的詳細資訊，請參閱 [自主資料庫使用者 - 使資料庫可攜](https://msdn.microsoft.com/library/ff929188.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ae669-232">For more information about contained database users, see [Contained Database Users- Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ae669-233">您無法使用入口網站來建立資料庫使用者 (系統管理員除外)。</span><span class="sxs-lookup"><span data-stu-id="ae669-233">Database users (with the exception of administrators) cannot be created using portal.</span></span> <span data-ttu-id="ae669-234">RBAC 角色不會傳播至 SQL Server、SQL Database 或「SQL 資料倉儲」。</span><span class="sxs-lookup"><span data-stu-id="ae669-234">RBAC roles are not propagated to SQL Server, SQL Database, or SQL Data Warehouse.</span></span> <span data-ttu-id="ae669-235">Azure RBAC 角色可用來管理 Azure 資源，並不會套用到資料庫權限。</span><span class="sxs-lookup"><span data-stu-id="ae669-235">Azure RBAC roles are used for managing Azure Resources, and do not apply to database permissions.</span></span> <span data-ttu-id="ae669-236">例如，「SQL Server 參與者」  角色不會授與可連線到 SQL Database 或「SQL 資料倉儲」的存取權。</span><span class="sxs-lookup"><span data-stu-id="ae669-236">For example, the **SQL Server Contributor** role does not grant access to connect to the SQL Database or SQL Data Warehouse.</span></span> <span data-ttu-id="ae669-237">存取權限必須使用 Transact-SQL 陳述式直接在資料庫中授與。</span><span class="sxs-lookup"><span data-stu-id="ae669-237">The access permission must be granted directly in the database using Transact-SQL statements.</span></span>
>

<span data-ttu-id="ae669-238">若要建立以 Azure AD 為基礎的自主資料庫使用者 (而非擁有資料庫的伺服器系統管理員)，請以至少具有 **ALTER ANY USER** 權限的使用者身分，使用 Azure AD 身分識別來連線到資料庫。</span><span class="sxs-lookup"><span data-stu-id="ae669-238">To create an Azure AD-based contained database user (other than the server administrator that owns the database), connect to the database with an Azure AD identity, as a user with at least the **ALTER ANY USER** permission.</span></span> <span data-ttu-id="ae669-239">然後使用下列的 Transact-SQL 語法：</span><span class="sxs-lookup"><span data-stu-id="ae669-239">Then use the following Transact-SQL syntax:</span></span>

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="ae669-240">Azure_AD_principal_name 可以是 Azure AD 使用者的使用者主體名稱或 Azure AD 群組的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="ae669-240">*Azure_AD_principal_name* can be the user principal name of an Azure AD user or the display name for an Azure AD group.</span></span>

<span data-ttu-id="ae669-241">**範例：** 建立代表 Azure AD 同盟或受管理網域使用者的自主資料庫使用者：</span><span class="sxs-lookup"><span data-stu-id="ae669-241">**Examples:** To create a contained database user representing an Azure AD federated or managed domain user:</span></span>
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="ae669-242">若要建立代表 Azure AD 或同盟網域群組的自主資料庫使用者，請輸入安全性群組的顯示名稱：</span><span class="sxs-lookup"><span data-stu-id="ae669-242">To create a contained database user representing an Azure AD or federated domain group, provide the display name of a security group:</span></span>
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="ae669-243">若要建立代表使用 Azure AD 權杖進行連線之應用程式的自主資料庫使用者︰</span><span class="sxs-lookup"><span data-stu-id="ae669-243">To create a contained database user representing an application that connects using an Azure AD token:</span></span>

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  <span data-ttu-id="ae669-244">您無法從 Azure Active Directory 直接建立使用者，除了與您的 Azure 訂用帳戶相關聯的 Azure Active Directory 以外。</span><span class="sxs-lookup"><span data-stu-id="ae669-244">You cannot directly create a user from an Azure Active Directory other than the Azure Active Directory that is associated with your Azure subscription.</span></span> <span data-ttu-id="ae669-245">不過，在相關聯 Active Directory (稱為外部使用者) 中匯入之使用者的其他 Active Directory 成員可以新增至租用戶 Active Directory 中的 Active Directory 群組。</span><span class="sxs-lookup"><span data-stu-id="ae669-245">However, members of other Active Directories that are imported users in the associated Active Directory (known as external users) can be added to an Active Directory group in the tenant Active Directory.</span></span> <span data-ttu-id="ae669-246">藉由建立該 AD 群組的自主資料庫使用者，來自外部 Active Directory 的使用者可以存取 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ae669-246">By creating a contained database user for that AD group, the users from the external Active Directory can gain access to SQL Database.</span></span>   

<span data-ttu-id="ae669-247">如需有關根據 Azure Active Directory 身分識別建立自主資料庫使用者的詳細資訊，請參閱 [CREATE USER (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ae669-247">For more information about creating contained database users based on Azure Active Directory identities, see [CREATE USER (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ae669-248">移除 Azure SQL 伺服器的 Azure Active Directory 系統管理員可防止任何 Azure AD 驗證使用者連線到伺服器。</span><span class="sxs-lookup"><span data-stu-id="ae669-248">Removing the Azure Active Directory administrator for Azure SQL server prevents any Azure AD authentication user from connecting to the server.</span></span> <span data-ttu-id="ae669-249">必要時，SQL Database 系統管理員可以手動刪除無法使用的 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="ae669-249">If necessary, unusable Azure AD users can be dropped manually by a SQL Database administrator.</span></span>   

>  [!NOTE]
>  <span data-ttu-id="ae669-250">如果您收到**連線逾時過期**，您可能需要將 `TransparentNetworkIPResolution` 連接字串的參數設定為 false。</span><span class="sxs-lookup"><span data-stu-id="ae669-250">If you receive a **Connection Timeout Expired**, you may need to set the `TransparentNetworkIPResolution` parameter of the connection string to false.</span></span> <span data-ttu-id="ae669-251">如需詳細資訊，請參閱 [.NET Framework 4.6.1 的連線逾時問題 - TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/)。</span><span class="sxs-lookup"><span data-stu-id="ae669-251">For more information, see [Connection timeout issue with .NET Framework 4.6.1 - TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/).</span></span>   

   
<span data-ttu-id="ae669-252">當您建立資料庫使用者時，該使用者會獲得 **CONNECT** 權限，而可以用 **PUBLIC** 角色的成員身分連線到該資料庫。</span><span class="sxs-lookup"><span data-stu-id="ae669-252">When you create a database user, that user receives the **CONNECT** permission and can connect to that database as a member of the **PUBLIC** role.</span></span> <span data-ttu-id="ae669-253">一開始提供給使用者的權限僅限於已授與 **PUBLIC** 角色的任何權限，或已授與其所屬任何 Windows 群組的任何權限。</span><span class="sxs-lookup"><span data-stu-id="ae669-253">Initially the only permissions available to the user are any permissions granted to the **PUBLIC** role, or any permissions granted to any Windows groups that they are a member of.</span></span> <span data-ttu-id="ae669-254">一旦您佈建以 Azure AD 為基礎的自主資料庫使用者，您可以使用您授與權限給任何其他類型使用者的相同方式，授與該使用者額外的權限。</span><span class="sxs-lookup"><span data-stu-id="ae669-254">Once you provision an Azure AD-based contained database user, you can grant the user additional permissions, the same way as you grant permission to any other type of user.</span></span> <span data-ttu-id="ae669-255">通常會授與權限給資料庫角色並新增使用者至角色。</span><span class="sxs-lookup"><span data-stu-id="ae669-255">Typically grant permissions to database roles, and add users to roles.</span></span> <span data-ttu-id="ae669-256">如需詳細資訊，請參閱 [Database Engine 權限基本概念](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ae669-256">For more information, see [Database Engine Permission Basics](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx).</span></span> <span data-ttu-id="ae669-257">如需有關特殊 SQL Database 角色的詳細資訊，請參閱 [管理 Azure SQL Database 的資料庫和登入](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="ae669-257">For more information about special SQL Database roles, see [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="ae669-258">匯入至管理網域的同盟網域使用者必須使用受管理的網域身分識別。</span><span class="sxs-lookup"><span data-stu-id="ae669-258">A federated domain user that is imported into a manage domain, must use the managed domain identity.</span></span>

> [!NOTE]
> <span data-ttu-id="ae669-259">Azure AD 使用者會在資料庫中繼資料中標示為類型 E (EXTERNAL_USER)，而群組則標示為類型 X (EXTERNAL_GROUPS)。</span><span class="sxs-lookup"><span data-stu-id="ae669-259">Azure AD users are marked in the database metadata with type E (EXTERNAL_USER) and for groups with type X (EXTERNAL_GROUPS).</span></span> <span data-ttu-id="ae669-260">如需詳細資訊，請參閱 [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ae669-260">For more information, see [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span> 
>

## <a name="connect-to-the-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a><span data-ttu-id="ae669-261">使用 SSMS 或 SSDT 連線至使用者資料庫或資料倉儲</span><span class="sxs-lookup"><span data-stu-id="ae669-261">Connect to the user database or data warehouse by using SSMS or SSDT</span></span>  
<span data-ttu-id="ae669-262">若要確認 Azure AD 系統管理員已正確設定，請使用 Azure AD 系統管理員帳戶連接到 **master** 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ae669-262">To confirm the Azure AD administrator is properly set up, connect to the **master** database using the Azure AD administrator account.</span></span>
<span data-ttu-id="ae669-263">若要佈建以 Azure AD 為基礎的自主資料庫使用者 (而非擁有資料庫的伺服器系統管理員)，請利用有權存取資料庫的 Azure AD 身分識別連線到資料庫。</span><span class="sxs-lookup"><span data-stu-id="ae669-263">To provision an Azure AD-based contained database user (other than the server administrator that owns the database), connect to the database with an Azure AD identity that has access to the database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae669-264">Visual Studio 2015 中的 [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 和 [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) 提供 Azure Active Directory 驗證支援。</span><span class="sxs-lookup"><span data-stu-id="ae669-264">Support for Azure Active Directory authentication is available with [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) in Visual Studio 2015.</span></span> <span data-ttu-id="ae669-265">SSMS 的 2016 年 8 月版本也支援 Active Directory 通用驗證，讓系統管理員能夠使用電話、簡訊、含有 PIN 的智慧卡或行動應用程式通知來要求 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="ae669-265">The August 2016 release of SSMS also includes support for Active Directory Universal Authentication, which allows administrators to require Multi-Factor Authentication using a phone call, text message, smart cards with pin, or mobile app notification.</span></span>
 
## <a name="using-an-azure-ad-identity-to-connect-using-ssms-or-ssdt"></a><span data-ttu-id="ae669-266">使用 Azure AD 身分識別以使用 SSMS 或 SSDT 進行連線</span><span class="sxs-lookup"><span data-stu-id="ae669-266">Using an Azure AD identity to connect using SSMS or SSDT</span></span>  

<span data-ttu-id="ae669-267">下列程序會示範如何使用 SQL Server Management Studio 或 SQL Server 資料庫工具的 Azure AD 身分連接到 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ae669-267">The following procedures show you how to connect to a SQL database with an Azure AD identity using SQL Server Management Studio or SQL Server Database Tools.</span></span>

### <a name="active-directory-integrated-authentication"></a><span data-ttu-id="ae669-268">Active Directory 整合驗證</span><span class="sxs-lookup"><span data-stu-id="ae669-268">Active Directory integrated authentication</span></span>

<span data-ttu-id="ae669-269">如果您已使用 Azure Active Directory 認證從同盟網域登入 Windows，請使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="ae669-269">Use this method if you are logged in to Windows using your Azure Active Directory credentials from a federated domain.</span></span>

1. <span data-ttu-id="ae669-270">啟動 Management Studio 或 Data Tools，並在 [連線到伺服器] \(或 [連線到 Database Engine]) 對話方塊的 [驗證] 方塊中，選取 [Active Directory - 整合式]。</span><span class="sxs-lookup"><span data-stu-id="ae669-270">Start Management Studio or Data Tools and in the **Connect to Server** (or **Connect to Database Engine**) dialog box, in the **Authentication** box, select **Active Directory - Integrated**.</span></span> <span data-ttu-id="ae669-271">不需要密碼或沒有密碼可輸入，因為現有的認證將會在連接時出現。</span><span class="sxs-lookup"><span data-stu-id="ae669-271">No password is needed or can be entered because your existing credentials will be presented for the connection.</span></span>   

    ![選取 AD 整合式驗證][11]
2. <span data-ttu-id="ae669-273">按一下 [選項] 按鈕，然後在 [連接屬性] 頁面的 [連接到資料庫] 方塊中，輸入您想要連線的使用者資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="ae669-273">Click the **Options** button, and on the **Connection Properties** page, in the **Connect to database** box, type the name of the user database you want to connect to.</span></span> <span data-ttu-id="ae669-274">([AD 網域名稱或租用戶 ID] 選項僅對 [通用驗證搭配 MFA 連線] 選項提供支援，否則會呈現灰色。)</span><span class="sxs-lookup"><span data-stu-id="ae669-274">(The **AD domain name or tenant ID**” option is only supported for **Universal with MFA connection** options, otherwise it is greyed out.)</span></span>  

    ![選取資料庫名稱][13]

## <a name="active-directory-password-authentication"></a><span data-ttu-id="ae669-276">Active Directory 密碼驗證</span><span class="sxs-lookup"><span data-stu-id="ae669-276">Active Directory password authentication</span></span>

<span data-ttu-id="ae669-277">使用 Azure AD 受管理網域連接到 Azure AD 主體名稱時，請使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="ae669-277">Use this method when connecting with an Azure AD principal name using the Azure AD managed domain.</span></span> <span data-ttu-id="ae669-278">您也可以將其用於沒有網域存取權的同盟帳戶，例如在遠端運作時。</span><span class="sxs-lookup"><span data-stu-id="ae669-278">You can also use it for federated account without access to the domain, for example when working remotely.</span></span>

<span data-ttu-id="ae669-279">如果您使用認證從未與 Azure 建立同盟的網域登入 Windows，或在使用 Azure AD 驗證時使用以初始或用戶端網域為基礎的 Azure AD，請使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="ae669-279">Use this method if you are logged in to Windows using credentials from a domain that is not federated with Azure, or when using Azure AD authentication using Azure AD based on the initial or the client domain.</span></span>

1. <span data-ttu-id="ae669-280">啟動 Management Studio 或 Data Tools，並在 [連線到伺服器] \(或 [連線到 Database Engine]) 對話方塊的 [驗證] 方塊中，選取 [Active Directory - 密碼]。</span><span class="sxs-lookup"><span data-stu-id="ae669-280">Start Management Studio or Data Tools and in the **Connect to Server** (or **Connect to Database Engine**) dialog box, in the **Authentication** box, select **Active Directory - Password**.</span></span>
2. <span data-ttu-id="ae669-281">在 [使用者名稱] 方塊中，以 **username@domain.com** 格式輸入您的 Azure Active Directory 使用者名稱。這必須是來自 Azure Active Directory 的帳戶或來自與 Azure Active Directory 建立同盟之網域的帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae669-281">In the **User name** box, type your Azure Active Directory user name in the format **username@domain.com**. This must be an account from the Azure Active Directory or an account from a domain federate with the Azure Active Directory.</span></span>
3. <span data-ttu-id="ae669-282">在 [密碼]  方塊中，輸入您的 Azure Active Directory 帳戶或同盟網域帳戶的使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="ae669-282">In the **Password** box, type your user password for the Azure Active Directory account or federated domain account.</span></span>

    ![選取 AD 密碼驗證][12]
4. <span data-ttu-id="ae669-284">按一下 [選項] 按鈕，然後在 [連接屬性] 頁面的 [連接到資料庫] 方塊中，輸入您想要連線的使用者資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="ae669-284">Click the **Options** button, and on the **Connection Properties** page, in the **Connect to database** box, type the name of the user database you want to connect to.</span></span> <span data-ttu-id="ae669-285">(請參閱上一個選項中的圖形。)</span><span class="sxs-lookup"><span data-stu-id="ae669-285">(See the graphic in the previous option.)</span></span>

## <a name="using-an-azure-ad-identity-to-connect-from-a-client-application"></a><span data-ttu-id="ae669-286">從用戶端應用程式使用 Azure AD 身分識別來連接</span><span class="sxs-lookup"><span data-stu-id="ae669-286">Using an Azure AD identity to connect from a client application</span></span>

<span data-ttu-id="ae669-287">下列程序示範如何從用戶端應用程式使用 Azure AD 身分識別連接到 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ae669-287">The following procedures show you how to connect to a SQL database with an Azure AD identity from a client application.</span></span>

###  <a name="active-directory-integrated-authentication"></a><span data-ttu-id="ae669-288">Active Directory 整合驗證</span><span class="sxs-lookup"><span data-stu-id="ae669-288">Active Directory integrated authentication</span></span>

<span data-ttu-id="ae669-289">若要使用整合式 Windows 驗證，您網域的 Active Directory 必須與 Azure Active Directory 建立同盟關係。</span><span class="sxs-lookup"><span data-stu-id="ae669-289">To use integrated Windows authentication, your domain’s Active Directory must be federated with Azure Active Directory.</span></span> <span data-ttu-id="ae669-290">連接到資料庫的用戶端應用程式 (或服務) 必須以使用者的網域認證在已加入網域的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="ae669-290">Your client application (or a service) connecting to the database must be running on a domain-joined machine under a user’s domain credentials.</span></span>

<span data-ttu-id="ae669-291">若要使用整合式驗證以及 Azure AD 身分識別連接至資料庫，資料庫連接字串中的驗證關鍵字必須設定為 Active Directory 整合式。</span><span class="sxs-lookup"><span data-stu-id="ae669-291">To connect to a database using integrated authentication and an Azure AD identity, the Authentication keyword in the database connection string must be set to Active Directory Integrated.</span></span> <span data-ttu-id="ae669-292">下列 C# 程式碼範例會使用 ADO.NET。</span><span class="sxs-lookup"><span data-stu-id="ae669-292">The following C# code sample uses ADO .NET.</span></span>

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

<span data-ttu-id="ae669-293">不支援使用連接字串關鍵字 ``Integrated Security=True`` 來連接到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ae669-293">The connection string keyword ``Integrated Security=True`` is not supported for connecting to Azure SQL Database.</span></span> <span data-ttu-id="ae669-294">建立 ODBC 連接時，您必須移除空格，並將「驗證」設為 'ActiveDirectoryIntegrated'。</span><span class="sxs-lookup"><span data-stu-id="ae669-294">When making an ODBC connection, you will need to remove spaces and set Authentication to 'ActiveDirectoryIntegrated'.</span></span>

### <a name="active-directory-password-authentication"></a><span data-ttu-id="ae669-295">Active Directory 密碼驗證</span><span class="sxs-lookup"><span data-stu-id="ae669-295">Active Directory password authentication</span></span>

<span data-ttu-id="ae669-296">若要使用整合式驗證和 Azure AD 身分識別來連接到資料庫，Authentication 關鍵字就必須設定為 Active Directory Password。</span><span class="sxs-lookup"><span data-stu-id="ae669-296">To connect to a database using integrated authentication and an Azure AD identity, the Authentication keyword must be set to Active Directory Password.</span></span> <span data-ttu-id="ae669-297">連接字串必須包含使用者識別碼 (UID) 及密碼 (PWD) 關鍵字和值。</span><span class="sxs-lookup"><span data-stu-id="ae669-297">The connection string must contain User ID/UID and Password/PWD keywords and values.</span></span> <span data-ttu-id="ae669-298">下列 C# 程式碼範例會使用 ADO.NET。</span><span class="sxs-lookup"><span data-stu-id="ae669-298">The following C# code sample uses ADO .NET.</span></span>

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

<span data-ttu-id="ae669-299">深入了解使用 [Azure AD 驗證 GitHub 示範](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth)上所提供之示範程式碼範例的 Azure AD 驗證方法。</span><span class="sxs-lookup"><span data-stu-id="ae669-299">Learn more about Azure AD authentication methods using the demo code samples available at [Azure AD Authentication GitHub Demo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).</span></span>

## <a name="azure-ad-token"></a><span data-ttu-id="ae669-300">Azure AD 權杖</span><span class="sxs-lookup"><span data-stu-id="ae669-300">Azure AD token</span></span>
<span data-ttu-id="ae669-301">這種驗證方法可以從 Azure Active Directory (AAD) 取得權杖，讓中介層服務連接到 Azure SQL Database 或 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="ae669-301">This authentication method allows middle-tier services to connect to Azure SQL Database or Azure SQL Data Warehouse by obtaining a token from Azure Active Directory (AAD).</span></span> <span data-ttu-id="ae669-302">這可容許包含憑證型驗證的複雜案例。</span><span class="sxs-lookup"><span data-stu-id="ae669-302">It enables sophisticated scenarios including certificate-based authentication.</span></span> <span data-ttu-id="ae669-303">您必須完成四個基本步驟，才能使用 Azure AD 權杖驗證︰</span><span class="sxs-lookup"><span data-stu-id="ae669-303">You must complete four basic steps to use Azure AD token authentication:</span></span>

1. <span data-ttu-id="ae669-304">向 Azure Active Directory 註冊您的應用程式，並取得程式碼的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="ae669-304">Register your application with Azure Active Directory and get the client id for your code.</span></span> 
2. <span data-ttu-id="ae669-305">建立代表應用程式的資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="ae669-305">Create a database user representing the application.</span></span> <span data-ttu-id="ae669-306">(稍早在步驟 6 中已完成)。</span><span class="sxs-lookup"><span data-stu-id="ae669-306">(Completed earlier in step 6.)</span></span>
3. <span data-ttu-id="ae669-307">在執行應用程式的用戶端電腦上建立憑證。</span><span class="sxs-lookup"><span data-stu-id="ae669-307">Create a certificate on the client computer runs the application.</span></span>
4. <span data-ttu-id="ae669-308">將憑證加入應用程式當做索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ae669-308">Add the certificate as a key for your application.</span></span>

<span data-ttu-id="ae669-309">範例連接字串︰</span><span class="sxs-lookup"><span data-stu-id="ae669-309">Sample connection string:</span></span>

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

<span data-ttu-id="ae669-310">如需詳細資訊，請參閱 [SQL Server 安全性部落格](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)。</span><span class="sxs-lookup"><span data-stu-id="ae669-310">For more information, see [SQL Server Security Blog](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).</span></span>

### <a name="sqlcmd"></a><span data-ttu-id="ae669-311">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="ae669-311">sqlcmd</span></span>

<span data-ttu-id="ae669-312">下列陳述式中使用 sqlcmd 13.1 進行連線，從 [下載中心](http://go.microsoft.com/fwlink/?LinkID=825643)即可取得此版本。</span><span class="sxs-lookup"><span data-stu-id="ae669-312">The following statements, connect using version 13.1 of sqlcmd, which is available from the [Download Center](http://go.microsoft.com/fwlink/?LinkID=825643).</span></span>

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a><span data-ttu-id="ae669-313">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae669-313">Next steps</span></span>
- <span data-ttu-id="ae669-314">如需 SQL Database 中存取權和控制權的概觀，請參閱 [SQL Database 的存取權和控制權](sql-database-control-access.md)。</span><span class="sxs-lookup"><span data-stu-id="ae669-314">For an overview of access and control in SQL Database, see [SQL Database access and control](sql-database-control-access.md).</span></span>
- <span data-ttu-id="ae669-315">如需 SQL Database 中登入、使用者和資料庫角色的概觀，請參閱[登入、使用者和資料庫角色](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="ae669-315">For an overview of logins, users, and database roles in SQL Database, see [Logins, users, and database roles](sql-database-manage-logins.md).</span></span>
- <span data-ttu-id="ae669-316">如需資料庫主體的詳細資訊，請參閱[主體](https://msdn.microsoft.com/library/ms181127.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ae669-316">For more information about database principals, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span></span>
- <span data-ttu-id="ae669-317">如需資料庫角色的詳細資訊，請參閱[資料庫角色](https://msdn.microsoft.com/library/ms189121.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ae669-317">For more information about database roles, see [Database roles](https://msdn.microsoft.com/library/ms189121.aspx).</span></span>
- <span data-ttu-id="ae669-318">如需 SQL Database 中防火牆規則的詳細資訊，請參閱 [SQL Database 防火牆規則](sql-database-firewall-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ae669-318">For more information about firewall rules in SQL Database, see [SQL Database firewall rules](sql-database-firewall-configure.md).</span></span>

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png

