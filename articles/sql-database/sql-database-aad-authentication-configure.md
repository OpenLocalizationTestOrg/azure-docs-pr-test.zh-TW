---
title: "aaaConfigure Azure Active Directory 驗證 SQL |Microsoft 文件"
description: "深入了解如何 tooconnect tooSQL 資料庫和使用 Azure Active Directory 驗證的 SQL 資料倉儲。"
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
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a><span data-ttu-id="ddd41-103">使用 SQL Database 或 SQL 資料倉儲設定和管理 Azure Active Directory 驗證</span><span class="sxs-lookup"><span data-stu-id="ddd41-103">Configure and manage Azure Active Directory authentication with SQL Database or SQL Data Warehouse</span></span>

<span data-ttu-id="ddd41-104">本文章將示範如何 toocreate 並填入 Azure AD，然後搭配使用 Azure AD 與 Azure SQL Database 和 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="ddd41-104">This article shows you how toocreate and populate Azure AD, and then use Azure AD with Azure SQL Database and SQL Data Warehouse.</span></span> <span data-ttu-id="ddd41-105">如需概觀，請參閱 [Azure Active Directory 驗證](sql-database-aad-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-105">For an overview, see [Azure Active Directory Authentication](sql-database-aad-authentication.md).</span></span>

>  [!NOTE]  
>  <span data-ttu-id="ddd41-106">連接的 tooSQL Azure VM 上執行的伺服器不支援使用 Azure Active Directory 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddd41-106">Connecting tooSQL Server running on an Azure VM is not supported using an Azure Active Directory account.</span></span> <span data-ttu-id="ddd41-107">請改用 Active Directory 網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddd41-107">Use a domain Active Directory account instead.</span></span>

## <a name="create-and-populate-an-azure-ad"></a><span data-ttu-id="ddd41-108">建立和填入 Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddd41-108">Create and populate an Azure AD</span></span>
<span data-ttu-id="ddd41-109">建立 Azure AD 並利用使用者和群組填入。</span><span class="sxs-lookup"><span data-stu-id="ddd41-109">Create an Azure AD and populate it with users and groups.</span></span> <span data-ttu-id="ddd41-110">Azure AD 可 hello 初始網域 Azure AD 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="ddd41-110">Azure AD can be hello initial domain Azure AD managed domain.</span></span> <span data-ttu-id="ddd41-111">Azure AD 也可以在內部部署 Active Directory 網域服務，與 hello Azure AD 同盟。</span><span class="sxs-lookup"><span data-stu-id="ddd41-111">Azure AD can also be an on-premises Active Directory Domain Services that is federated with hello Azure AD.</span></span>

<span data-ttu-id="ddd41-112">如需詳細資訊，請參閱[整合內部部署身分識別與 Azure Active Directory](../active-directory/active-directory-aadconnect.md)，[加入您自己的網域名稱 tooAzure AD](../active-directory/active-directory-add-domain.md)， [Microsoft Azure 現在支援與同盟Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)，[管理 Azure AD 目錄](https://msdn.microsoft.com/library/azure/hh967611.aspx)，[使用 Windows PowerShell 管理 Azure AD](/powershell/azure/overview?view=azureadps-2.0)，和[混合式身分識別必要的連接埠和通訊協定](../active-directory/active-directory-aadconnect-ports.md)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-112">For more information, see [Integrating your on-premises identities with Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Add your own domain name tooAzure AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure now supports federation with Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Administering your Azure AD directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Manage Azure AD using Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), and [Hybrid Identity Required Ports and Protocols](../active-directory/active-directory-aadconnect-ports.md).</span></span>

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a><span data-ttu-id="ddd41-113">選擇性： 建立關聯，或變更 hello 目前與 Azure 訂用帳戶相關聯的 active directory</span><span class="sxs-lookup"><span data-stu-id="ddd41-113">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
<span data-ttu-id="ddd41-114">tooassociate hello Azure AD 目錄，以您的組織，您的資料庫建立 hello 目錄 hello Azure 訂用帳戶裝載 hello 資料庫的受信任的目錄。</span><span class="sxs-lookup"><span data-stu-id="ddd41-114">tooassociate your database with hello Azure AD directory for your organization, make hello directory a trusted directory for hello Azure subscription hosting hello database.</span></span> <span data-ttu-id="ddd41-115">如需詳細資訊，請參閱 [Azure 訂用帳戶如何與 Azure AD 產生關聯](https://msdn.microsoft.com/library/azure/dn629581.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-115">For more information, see [How Azure subscriptions are associated with Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx).</span></span>

<span data-ttu-id="ddd41-116">**其他資訊：** 每個 Azure 訂用帳戶都會與 Azure AD 執行個體有信任關係。</span><span class="sxs-lookup"><span data-stu-id="ddd41-116">**Additional information:** Every Azure subscription has a trust relationship with an Azure AD instance.</span></span> <span data-ttu-id="ddd41-117">這表示其信任該目錄 tooauthenticate 使用者、 服務和裝置。</span><span class="sxs-lookup"><span data-stu-id="ddd41-117">This means that it trusts that directory tooauthenticate users, services, and devices.</span></span> <span data-ttu-id="ddd41-118">多個訂閱可以信任 hello 相同的目錄，但訂閱只能信任一個目錄。</span><span class="sxs-lookup"><span data-stu-id="ddd41-118">Multiple subscriptions can trust hello same directory, but a subscription trusts only one directory.</span></span> <span data-ttu-id="ddd41-119">您可以看到所信任的目錄，由您的訂閱下 hello**設定**在索引標籤上[https://manage.windowsazure.com/](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-119">You can see which directory is trusted by your subscription under hello **Settings** tab at [https://manage.windowsazure.com/](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="ddd41-120">此訂用帳戶具有與目錄的信任關係是不同的訂用帳戶已與其他 Azure 中所有資源 （網站、 資料庫等等），後者比較像是訂閱的子資源的 hello 關係。</span><span class="sxs-lookup"><span data-stu-id="ddd41-120">This trust relationship that a subscription has with a directory is unlike hello relationship that a subscription has with all other resources in Azure (websites, databases, and so on), which are more like child resources of a subscription.</span></span> <span data-ttu-id="ddd41-121">如果訂用帳戶已過期，則存取 toothose hello 訂用帳戶相關聯的其他資源也會停止。</span><span class="sxs-lookup"><span data-stu-id="ddd41-121">If a subscription expires, then access toothose other resources associated with hello subscription also stops.</span></span> <span data-ttu-id="ddd41-122">但是 hello 目錄會留在 Azure 中，而且您可以將其他訂用帳戶與該目錄產生關聯，並繼續 toomanage hello 目錄使用者。</span><span class="sxs-lookup"><span data-stu-id="ddd41-122">But hello directory remains in Azure, and you can associate another subscription with that directory and continue toomanage hello directory users.</span></span> <span data-ttu-id="ddd41-123">如需有關資源的詳細資訊，請參閱 [了解 Azure 中的資源存取](https://msdn.microsoft.com/library/azure/dn584083.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-123">For more information about resources, see [Understanding resource access in Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).</span></span>

<span data-ttu-id="ddd41-124">hello 下列程序示範如何 toochange hello 產生指定的訂用帳戶目錄的關聯。</span><span class="sxs-lookup"><span data-stu-id="ddd41-124">hello following procedures show you how toochange hello associated directory for a given subscription.</span></span>
1. <span data-ttu-id="ddd41-125">連接 tooyour [Azure 傳統入口網站](https://manage.windowsazure.com/)利用 Azure 訂用帳戶系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ddd41-125">Connect tooyour [Azure Classic Portal](https://manage.windowsazure.com/) by using an Azure subscription administrator.</span></span>
2. <span data-ttu-id="ddd41-126">在 hello 左邊的橫幅中，選取 **設定**。</span><span class="sxs-lookup"><span data-stu-id="ddd41-126">On hello left banner, select **SETTINGS**.</span></span>
3. <span data-ttu-id="ddd41-127">訂用帳戶會出現在 hello 設定畫面中。</span><span class="sxs-lookup"><span data-stu-id="ddd41-127">Your subscriptions appear in hello settings screen.</span></span> <span data-ttu-id="ddd41-128">如果 hello 需要訂用帳戶不會出現，請按一下**訂閱**hello 頂端下拉 hello**依目錄篩選**方塊並選取包含您的訂閱 hello 目錄，然後按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="ddd41-128">If hello desired subscription does not appear, click **Subscriptions** at hello top, drop down hello **FILTER BY DIRECTORY** box and select hello directory that contains your subscriptions, and then click **APPLY**.</span></span>
   
    ![select subscription][4]
4. <span data-ttu-id="ddd41-130">在 hello**設定**區域中，按一下您的訂閱，然後再按一下**編輯目錄**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="ddd41-130">In hello **settings** area, click your subscription, and then click  **EDIT DIRECTORY** at hello bottom of hello page.</span></span>
   
    ![ad-settings-portal][5]
5. <span data-ttu-id="ddd41-132">在 hello**編輯目錄**，選取 hello 與您的 SQL Server 或 SQL 資料倉儲、 相關聯的 Azure Active Directory，然後按一下下一步 hello 箭號。</span><span class="sxs-lookup"><span data-stu-id="ddd41-132">In hello **EDIT DIRECTORY** box, select hello Azure Active Directory that is associated with your SQL Server or SQL Data Warehouse, and then click hello arrow for next.</span></span>
   
    ![edit-directory-select][6]
6. <span data-ttu-id="ddd41-134">在 [hello**確認**目錄對應] 對話方塊中，確認"**將會移除所有的共同管理員。**"</span><span class="sxs-lookup"><span data-stu-id="ddd41-134">In hello **CONFIRM** directory Mapping dialog box, confirm that "**All co-administrators will be removed.**"</span></span>
   
    ![edit-directory-confirm][7]
7. <span data-ttu-id="ddd41-136">按一下 hello 核取 tooreload hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ddd41-136">Click hello check tooreload hello portal.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ddd41-137">當變更 hello 目錄、 存取 tooall 共同管理員，Azure AD 使用者和群組，並移除目錄為基礎的資源使用者，而且不再有存取 toothis 訂用帳戶或其資源。</span><span class="sxs-lookup"><span data-stu-id="ddd41-137">When you change hello directory, access tooall co-administrators, Azure AD users and groups, and directory-backed resource users are removed and they no longer have access toothis subscription or its resources.</span></span> <span data-ttu-id="ddd41-138">只有您，做為服務管理員，可以設定存取主體根據 hello 新目錄。</span><span class="sxs-lookup"><span data-stu-id="ddd41-138">Only you, as a service administrator, can configure access for principals based on hello new directory.</span></span> <span data-ttu-id="ddd41-139">這項變更可能需要相當長的時間 toopropagate tooall 資源。</span><span class="sxs-lookup"><span data-stu-id="ddd41-139">This change might take a substantial amount of time toopropagate tooall resources.</span></span> <span data-ttu-id="ddd41-140">變更 hello 目錄，也變更 SQL Database 和 SQL 資料倉儲 hello Azure AD 系統管理員，而不允許任何現有的 Azure AD 使用者的資料庫存取權。</span><span class="sxs-lookup"><span data-stu-id="ddd41-140">Changing hello directory, also changes hello Azure AD administrator for SQL Database and SQL Data Warehouse and disallow database access for any existing Azure AD users.</span></span> <span data-ttu-id="ddd41-141">hello Azure AD 系統管理員必須重設 （如下所述），且新的 Azure AD 使用者必須先建立。</span><span class="sxs-lookup"><span data-stu-id="ddd41-141">hello Azure AD admin must be reset (as described below) and new Azure AD users must be created.</span></span>
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a><span data-ttu-id="ddd41-142">建立 Azure SQL 伺服器的 Azure AD 系統管理員</span><span class="sxs-lookup"><span data-stu-id="ddd41-142">Create an Azure AD administrator for Azure SQL server</span></span>
<span data-ttu-id="ddd41-143">每個 SQL Azure 伺服器 （裝載 SQL Database 或 SQL 資料倉儲） 開頭為 hello hello 整個 Azure SQL server 系統管理員的單一伺服器系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddd41-143">Each Azure SQL server (which hosts a SQL Database or SQL Data Warehouse) starts with a single server administrator account that is hello administrator of hello entire Azure SQL server.</span></span> <span data-ttu-id="ddd41-144">第二個 SQL Server 系統管理員必須建立，也就是 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddd41-144">A second SQL Server administrator must be created, that is an Azure AD account.</span></span> <span data-ttu-id="ddd41-145">這個主體的自主的資料庫使用者身分建立 hello master 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="ddd41-145">This principal is created as a contained database user in hello master database.</span></span> <span data-ttu-id="ddd41-146">做為系統管理員，hello server 系統管理員帳戶屬於 hello **db_owner**角色中的每個使用者資料庫，然後輸入 hello 為每個使用者資料庫**dbo**使用者。</span><span class="sxs-lookup"><span data-stu-id="ddd41-146">As administrators, hello server administrator accounts are members of hello **db_owner** role in every user database, and enter each user database as hello **dbo** user.</span></span> <span data-ttu-id="ddd41-147">如需 hello server 系統管理員帳戶的詳細資訊，請參閱[管理資料庫和 Azure SQL Database 中的登入](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-147">For more information about hello server administrator accounts, see [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md).</span></span>

<span data-ttu-id="ddd41-148">當使用異地備援的 Azure Active Directory，hello Azure Active Directory 系統管理員必須設定主要 hello 和 hello 次要伺服器。</span><span class="sxs-lookup"><span data-stu-id="ddd41-148">When using Azure Active Directory with geo-replication, hello Azure Active Directory administrator must be configured for both hello primary and hello secondary servers.</span></span> <span data-ttu-id="ddd41-149">如果伺服器不需要 Azure Active Directory 系統管理員，然後登入 Azure Active Directory 和使用者會收到 「 無法連接 」 tooserver 錯誤。</span><span class="sxs-lookup"><span data-stu-id="ddd41-149">If a server does not have an Azure Active Directory administrator, then Azure Active Directory logins and users receive a "Cannot connect" tooserver error.</span></span>

> [!NOTE]
> <span data-ttu-id="ddd41-150">在 Azure AD 帳戶的內容 （包括 hello Azure SQL server 系統管理員帳戶），根據的使用者無法建立 Azure AD 為基礎的使用者，因為他們沒有權限 toovalidate 提議 hello Azure AD 與資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="ddd41-150">Users that are not based on an Azure AD account (including hello Azure SQL server administrator account), cannot create Azure AD-based users, because they do not have permission toovalidate proposed database users with hello Azure AD.</span></span>
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a><span data-ttu-id="ddd41-151">佈建 Azure SQL 伺服器的 Azure Active Directory 系統管理員</span><span class="sxs-lookup"><span data-stu-id="ddd41-151">Provision an Azure Active Directory administrator for your Azure SQL server</span></span>

<span data-ttu-id="ddd41-152">hello 下列兩個程序顯示如何 tooprovision hello Azure 入口網站中，也可以使用 PowerShell 您 Azure SQL server 的 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ddd41-152">hello following two procedures show you how tooprovision an Azure Active Directory administrator for your Azure SQL server in hello Azure portal and by using PowerShell.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="ddd41-153">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ddd41-153">Azure portal</span></span>
1. <span data-ttu-id="ddd41-154">在 hello [Azure 入口網站](https://portal.azure.com/)、 在 hello 右上角、 按一下 下一份可能的 Active Directory 您連接 toodrop。</span><span class="sxs-lookup"><span data-stu-id="ddd41-154">In hello [Azure portal](https://portal.azure.com/), in hello upper-right corner, click your connection toodrop down a list of possible Active Directories.</span></span> <span data-ttu-id="ddd41-155">選擇 hello 更正為 hello 預設 Azure AD 的 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="ddd41-155">Choose hello correct Active Directory as hello default Azure AD.</span></span> <span data-ttu-id="ddd41-156">此步驟的連結 hello 訂用帳戶關聯與 Active Directory 與 Azure SQL server 並確認的 hello 相同訂用帳戶同時用於 Azure AD 和 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="ddd41-156">This step links hello subscription association with Active Directory with Azure SQL server making sure that hello same subscription is used for both Azure AD and SQL Server.</span></span> <span data-ttu-id="ddd41-157">（hello Azure SQL 伺服器可以裝載 Azure SQL Database 或 Azure SQL 資料倉儲。）</span><span class="sxs-lookup"><span data-stu-id="ddd41-157">(hello Azure SQL server can be hosting either Azure SQL Database or Azure SQL Data Warehouse.)</span></span>   
    <span data-ttu-id="ddd41-158">![choose-ad][8]</span><span class="sxs-lookup"><span data-stu-id="ddd41-158">![choose-ad][8]</span></span>   
    
2. <span data-ttu-id="ddd41-159">在 hello 保持橫幅選取**SQL 伺服器**，選取您**SQL server**，然後在 hello **SQL Server**刀鋒視窗中，按一下**Active Directory 系統管理員**.</span><span class="sxs-lookup"><span data-stu-id="ddd41-159">In hello left banner select **SQL servers**, select your **SQL server**, and then in hello **SQL Server** blade, click **Active Directory admin**.</span></span>   
3. <span data-ttu-id="ddd41-160">在 hello **Active Directory 系統管理員**刀鋒視窗中，按一下 **設定系統管理員**。</span><span class="sxs-lookup"><span data-stu-id="ddd41-160">In hello **Active Directory admin** blade, click **Set admin**.</span></span>   
    <span data-ttu-id="ddd41-161">![選取 Active Directory](./media/sql-database-aad-authentication/select-active-directory.png)</span><span class="sxs-lookup"><span data-stu-id="ddd41-161">![select active directory](./media/sql-database-aad-authentication/select-active-directory.png)</span></span>  
    
4. <span data-ttu-id="ddd41-162">在 hello**新增系統管理員**刀鋒視窗中，搜尋使用者、 選取 hello 使用者或群組 toobe 為系統管理員，然後**選取**。</span><span class="sxs-lookup"><span data-stu-id="ddd41-162">In hello **Add admin** blade, search for a user, select hello user or group toobe an administrator, and then click **Select**.</span></span> <span data-ttu-id="ddd41-163">（hello Active Directory 管理刀鋒視窗會顯示所有成員與 Active directory 群組。</span><span class="sxs-lookup"><span data-stu-id="ddd41-163">(hello Active Directory admin blade shows all members and groups of your Active Directory.</span></span> <span data-ttu-id="ddd41-164">呈現灰色的使用者或群組無法選取，因為他們不受支援成為 Azure AD 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ddd41-164">Users or groups that are grayed out cannot be selected because they are not supported as Azure AD administrators.</span></span> <span data-ttu-id="ddd41-165">(請參閱支援的系統管理員在 hello hello 清單**Azure AD 的功能和限制**區段[使用 Azure Active Directory 驗證的驗證的 SQL 資料庫或 SQL 資料倉儲](sql-database-aad-authentication.md)。)角色型存取控制 (RBAC) 適用於僅 toohello 入口網站，而且不傳播的 tooSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ddd41-165">(See hello list of supported admins in hello **Azure AD Features and Limitations** section of [Use Azure Active Directory Authentication for authentication with SQL Database or SQL Data Warehouse](sql-database-aad-authentication.md).) Role-based access control (RBAC) applies only toohello portal and is not propagated tooSQL Server.</span></span>   
    <span data-ttu-id="ddd41-166">![選取系統管理員](./media/sql-database-aad-authentication/select-admin.png)</span><span class="sxs-lookup"><span data-stu-id="ddd41-166">![select admin](./media/sql-database-aad-authentication/select-admin.png)</span></span>  
    
5. <span data-ttu-id="ddd41-167">頂端的 hello hello **Active Directory 系統管理員**刀鋒視窗中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="ddd41-167">At hello top of hello **Active Directory admin** blade, click **SAVE**.</span></span>   
    <span data-ttu-id="ddd41-168">![儲存系統管理員](./media/sql-database-aad-authentication/save-admin.png)</span><span class="sxs-lookup"><span data-stu-id="ddd41-168">![save admin](./media/sql-database-aad-authentication/save-admin.png)</span></span>   

<span data-ttu-id="ddd41-169">變更 hello 系統管理員的 hello 程序可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="ddd41-169">hello process of changing hello administrator may take several minutes.</span></span> <span data-ttu-id="ddd41-170">然後 hello 新系統管理員會出現在 hello **Active Directory 系統管理員**方塊。</span><span class="sxs-lookup"><span data-stu-id="ddd41-170">Then hello new administrator appears in hello **Active Directory admin** box.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ddd41-171">設定 hello Azure AD 系統管理員，請 hello 新系統管理員的名稱 （使用者或群組） 不能出現在 hello 虛擬 master 資料庫的 SQL Server 驗證使用者身分。</span><span class="sxs-lookup"><span data-stu-id="ddd41-171">When setting up hello Azure AD admin, hello new admin name (user or group) cannot already be present in hello virtual master database as a SQL Server authentication user.</span></span> <span data-ttu-id="ddd41-172">如果有的話，hello Azure AD 系統管理員安裝程式將會失敗;復原其建立，並指出該這類的系統管理員 （名稱） 已經存在。</span><span class="sxs-lookup"><span data-stu-id="ddd41-172">If present, hello Azure AD admin setup will fail; rolling back its creation and indicating that such an admin (name) already exists.</span></span> <span data-ttu-id="ddd41-173">因為這類的 SQL Server 驗證使用者不是 hello Azure AD 的一部分，任何使用 Azure AD 驗證的投入時間 tooconnect toohello 伺服器將會失敗。</span><span class="sxs-lookup"><span data-stu-id="ddd41-173">Since such a SQL Server authentication user is not part of hello Azure AD, any effort tooconnect toohello server using Azure AD authentication fails.</span></span>
   > 


<span data-ttu-id="ddd41-174">toolater 移除系統管理員，在 hello hello 頂端**Active Directory 系統管理員**刀鋒視窗中，按一下 **移除系統管理員**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="ddd41-174">toolater remove an Admin, at hello top of hello **Active Directory admin** blade, click **Remove admin**, and then click **Save**.</span></span>

### <a name="powershell"></a><span data-ttu-id="ddd41-175">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddd41-175">PowerShell</span></span>
<span data-ttu-id="ddd41-176">toorun PowerShell cmdlet，您需要 toohave 安裝並執行 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ddd41-176">toorun PowerShell cmdlets, you need toohave Azure PowerShell installed and running.</span></span> <span data-ttu-id="ddd41-177">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-177">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="ddd41-178">tooprovision 為 Azure AD 系統管理員，請執行下列 Azure PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ddd41-178">tooprovision an Azure AD admin, execute hello following Azure PowerShell commands:</span></span>

* <span data-ttu-id="ddd41-179">Add-AzureRmAccount</span><span class="sxs-lookup"><span data-stu-id="ddd41-179">Add-AzureRmAccount</span></span>
* <span data-ttu-id="ddd41-180">Select-AzureRmSubscription</span><span class="sxs-lookup"><span data-stu-id="ddd41-180">Select-AzureRmSubscription</span></span>

<span data-ttu-id="ddd41-181">Cmdlet 使用 tooprovision 和管理 Azure AD 系統管理員：</span><span class="sxs-lookup"><span data-stu-id="ddd41-181">Cmdlets used tooprovision and manage Azure AD admin:</span></span>

| <span data-ttu-id="ddd41-182">Cmdlet 名稱</span><span class="sxs-lookup"><span data-stu-id="ddd41-182">Cmdlet name</span></span> | <span data-ttu-id="ddd41-183">說明</span><span class="sxs-lookup"><span data-stu-id="ddd41-183">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="ddd41-184">Set-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="ddd41-184">Set-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="ddd41-185">佈建 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員 (必須來自目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddd41-185">Provisions an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ddd41-186">（必須是從 hello 目前訂用帳戶）。</span><span class="sxs-lookup"><span data-stu-id="ddd41-186">(Must be from hello current subscription.)</span></span> |
| [<span data-ttu-id="ddd41-187">Remove-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="ddd41-187">Remove-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="ddd41-188">移除 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ddd41-188">Removes an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> |
| [<span data-ttu-id="ddd41-189">Get-AzureRmSqlServerActiveDirectoryAdministrator</span><span class="sxs-lookup"><span data-stu-id="ddd41-189">Get-AzureRmSqlServerActiveDirectoryAdministrator</span></span>](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |<span data-ttu-id="ddd41-190">傳回目前為 hello Azure SQL server 或 Azure SQL 資料倉儲設定 Azure Active Directory 系統管理員的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ddd41-190">Returns information about an Azure Active Directory administrator currently configured for hello Azure SQL server or Azure SQL Data Warehouse.</span></span> |

<span data-ttu-id="ddd41-191">使用的 PowerShell 命令取得說明 toosee 更詳細說明每個這些命令，例如``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``。</span><span class="sxs-lookup"><span data-stu-id="ddd41-191">Use PowerShell command get-help toosee more details for each of these commands, for example ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.</span></span>

<span data-ttu-id="ddd41-192">hello 下列指令碼會佈建 Azure AD 系統管理員群組命名為**DBA_Group** (物件識別碼`40b79501-b343-44ed-9ce7-da4c8cc7353f`) hello **demo_server**名為資源群組中的伺服器**群組-23**:</span><span class="sxs-lookup"><span data-stu-id="ddd41-192">hello following script provisions an Azure AD administrator group named **DBA_Group** (object id `40b79501-b343-44ed-9ce7-da4c8cc7353f`) for hello **demo_server** server in a resource group named **Group-23**:</span></span>

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

<span data-ttu-id="ddd41-193">hello **DisplayName**輸入的參數接受 hello Azure AD 的顯示名稱或 hello 使用者主體名稱。</span><span class="sxs-lookup"><span data-stu-id="ddd41-193">hello **DisplayName** input parameter accepts either hello Azure AD display name or hello User Principal Name.</span></span> <span data-ttu-id="ddd41-194">例如 ``DisplayName="John Smith"`` 和 ``DisplayName="johns@contoso.com"``。</span><span class="sxs-lookup"><span data-stu-id="ddd41-194">For example, ``DisplayName="John Smith"`` and ``DisplayName="johns@contoso.com"``.</span></span> <span data-ttu-id="ddd41-195">Azure AD 群組只有 hello Azure AD 支援的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="ddd41-195">For Azure AD groups only hello Azure AD display name is supported.</span></span>

> [!NOTE]
> <span data-ttu-id="ddd41-196">hello Azure PowerShell 命令，```Set-AzureRmSqlServerActiveDirectoryAdministrator```不會阻止您佈建 Azure AD 系統管理員不支援的使用者。</span><span class="sxs-lookup"><span data-stu-id="ddd41-196">hello Azure PowerShell  command ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` does not prevent you from provisioning Azure AD admins for unsupported users.</span></span> <span data-ttu-id="ddd41-197">不支援的使用者可以佈建，但無法連接 tooa 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ddd41-197">An unsupported user can be provisioned, but can not connect tooa database.</span></span> 
> 

<span data-ttu-id="ddd41-198">hello 下列範例會使用選擇性的 hello **ObjectID**:</span><span class="sxs-lookup"><span data-stu-id="ddd41-198">hello following example uses hello optional **ObjectID**:</span></span>

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> <span data-ttu-id="ddd41-199">hello Azure AD **ObjectID**時需要 hello **DisplayName**不是唯一的。</span><span class="sxs-lookup"><span data-stu-id="ddd41-199">hello Azure AD **ObjectID** is required when hello **DisplayName** is not unique.</span></span> <span data-ttu-id="ddd41-200">tooretrieve hello **ObjectID**和**DisplayName**值使用 hello Active Directory 區段的 Azure 傳統入口網站，以及檢視 hello 內容的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="ddd41-200">tooretrieve hello **ObjectID** and **DisplayName** values, use hello Active Directory section of Azure Classic Portal, and view hello properties of a user or group.</span></span>
> 

<span data-ttu-id="ddd41-201">下列範例中的 hello 傳回 Azure SQL server 的 hello 目前的 Azure AD 系統管理員的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="ddd41-201">hello following example returns information about hello current Azure AD admin for Azure SQL server:</span></span>

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

<span data-ttu-id="ddd41-202">下列範例中的 hello 移除 Azure AD 系統管理員：</span><span class="sxs-lookup"><span data-stu-id="ddd41-202">hello following example removes an Azure AD administrator:</span></span>

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

<span data-ttu-id="ddd41-203">您也可以使用 hello REST Api 來佈建 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ddd41-203">You can also provision an Azure Active Directory Administrator by using hello REST APIs.</span></span> <span data-ttu-id="ddd41-204">如需詳細資訊，請參閱 [Azure SQL Database 之 Azure SQL Database 作業的 Service Management REST API 參考和作業](https://msdn.microsoft.com/library/azure/dn505719.aspx)</span><span class="sxs-lookup"><span data-stu-id="ddd41-204">For more information, see [Service Management REST API Reference and Operations for Azure SQL Databases Operations for Azure SQL Databases](https://msdn.microsoft.com/library/azure/dn505719.aspx)</span></span>

### <a name="cli"></a><span data-ttu-id="ddd41-205">CLI</span><span class="sxs-lookup"><span data-stu-id="ddd41-205">CLI</span></span>  
<span data-ttu-id="ddd41-206">您也可以使用下列 CLI 命令的呼叫 hello 來佈建 Azure AD 系統管理員：</span><span class="sxs-lookup"><span data-stu-id="ddd41-206">You can also provision an Azure AD admin by calling hello following CLI commands:</span></span>
| <span data-ttu-id="ddd41-207">命令</span><span class="sxs-lookup"><span data-stu-id="ddd41-207">Command</span></span> | <span data-ttu-id="ddd41-208">說明</span><span class="sxs-lookup"><span data-stu-id="ddd41-208">Description</span></span> |
| --- | --- |
|[<span data-ttu-id="ddd41-209">az sql server ad-admin create</span><span class="sxs-lookup"><span data-stu-id="ddd41-209">az sql server ad-admin create</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |<span data-ttu-id="ddd41-210">佈建 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員 (必須來自目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddd41-210">Provisions an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ddd41-211">（必須是從 hello 目前訂用帳戶）。</span><span class="sxs-lookup"><span data-stu-id="ddd41-211">(Must be from hello current subscription.)</span></span> |
|[<span data-ttu-id="ddd41-212">az sql server ad-admin delete</span><span class="sxs-lookup"><span data-stu-id="ddd41-212">az sql server ad-admin delete</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |<span data-ttu-id="ddd41-213">移除 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ddd41-213">Removes an Azure Active Directory administrator for Azure SQL server or Azure SQL Data Warehouse.</span></span> |
|[<span data-ttu-id="ddd41-214">az sql server ad-admin list</span><span class="sxs-lookup"><span data-stu-id="ddd41-214">az sql server ad-admin list</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |<span data-ttu-id="ddd41-215">傳回目前為 hello Azure SQL server 或 Azure SQL 資料倉儲設定 Azure Active Directory 系統管理員的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ddd41-215">Returns information about an Azure Active Directory administrator currently configured for hello Azure SQL server or Azure SQL Data Warehouse.</span></span> |
|[<span data-ttu-id="ddd41-216">az sql server ad-admin update</span><span class="sxs-lookup"><span data-stu-id="ddd41-216">az sql server ad-admin update</span></span>](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |<span data-ttu-id="ddd41-217">更新 Azure SQL server 或 Azure SQL 資料倉儲的 hello Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ddd41-217">Updates hello Active Directory administrator for an Azure SQL server or Azure SQL Data Warehouse.</span></span> |

<span data-ttu-id="ddd41-218">如需 CLI 命令的詳細資訊，請參閱 [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-218">For more information about CLI commands, see [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server).</span></span>  


## <a name="configure-your-client-computers"></a><span data-ttu-id="ddd41-219">設定用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="ddd41-219">Configure your client computers</span></span>
<span data-ttu-id="ddd41-220">所有的用戶端電腦從您的應用程式或使用者連接 tooAzure SQL Database 或 Azure SQL 資料倉儲使用 Azure AD 身分識別，您必須安裝下列軟體的 hello:</span><span class="sxs-lookup"><span data-stu-id="ddd41-220">On all client machines, from which your applications or users connect tooAzure SQL Database or Azure SQL Data Warehouse using Azure AD identities, you must install hello following software:</span></span>

* <span data-ttu-id="ddd41-221">從 [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx)安裝 .NET Framework 4.6 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ddd41-221">.NET Framework 4.6 or later from [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span></span>
* <span data-ttu-id="ddd41-222">SQL Server 的 azure Active Directory 驗證程式庫 (**ADALSQL。DLL**) 提供多個語言版本 （x86 和 amd64） 從 hello 下載中心[Microsoft Active Directory Authentication Library for Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-222">Azure Active Directory Authentication Library for SQL Server (**ADALSQL.DLL**) is available in multiple languages (both x86 and amd64) from hello download center at [Microsoft Active Directory Authentication Library for Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).</span></span>

<span data-ttu-id="ddd41-223">您可以符合這些需求，方法如下︰</span><span class="sxs-lookup"><span data-stu-id="ddd41-223">You can meet these requirements by:</span></span>

* <span data-ttu-id="ddd41-224">安裝  [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)或[for Visual Studio 2015 的 SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)符合 hello.NET Framework 4.6 需求。</span><span class="sxs-lookup"><span data-stu-id="ddd41-224">Installing either [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) or [SQL Server Data Tools for Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) meets hello .NET Framework 4.6 requirement.</span></span>
* <span data-ttu-id="ddd41-225">SSMS 會安裝 hello x86 版本**ADALSQL。DLL**。</span><span class="sxs-lookup"><span data-stu-id="ddd41-225">SSMS installs hello x86 version of **ADALSQL.DLL**.</span></span>
* <span data-ttu-id="ddd41-226">SSDT 安裝 hello amd64 版**ADALSQL。DLL**。</span><span class="sxs-lookup"><span data-stu-id="ddd41-226">SSDT installs hello amd64 version of **ADALSQL.DLL**.</span></span>
* <span data-ttu-id="ddd41-227">hello 最新的 Visual Studio，從[Visual Studio 下載](https://www.visualstudio.com/downloads/download-visual-studio-vs)符合 hello.NET Framework 4.6 需求，但不會安裝必要的 amd64 版本 hello **ADALSQL。DLL**。</span><span class="sxs-lookup"><span data-stu-id="ddd41-227">hello latest Visual Studio from [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) meets hello .NET Framework 4.6 requirement, but does not install hello required amd64 version of **ADALSQL.DLL**.</span></span>

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a><span data-ttu-id="ddd41-228">在對應資料庫 tooAzure AD 身分識別建立自主的資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="ddd41-228">Create contained database users in your database mapped tooAzure AD identities</span></span>

<span data-ttu-id="ddd41-229">Azure Active Directory 驗證需要資料庫使用者 toobe 建立為自主的資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="ddd41-229">Azure Active Directory authentication requires database users toobe created as contained database users.</span></span> <span data-ttu-id="ddd41-230">Azure AD 身分識別為基礎之自主的資料庫使用者是資料庫使用者，並沒有登入 hello master 資料庫中，而對應 tooan 識別在 hello 與 hello 資料庫相關聯的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="ddd41-230">A contained database user based on an Azure AD identity, is a database user that does not have a login in hello master database, and which maps tooan identity in hello Azure AD directory that is associated with hello database.</span></span> <span data-ttu-id="ddd41-231">hello Azure AD 身分識別可以是個別的使用者帳戶或群組。</span><span class="sxs-lookup"><span data-stu-id="ddd41-231">hello Azure AD identity can be either an individual user account or a group.</span></span> <span data-ttu-id="ddd41-232">如需有關自主資料庫使用者的詳細資訊，請參閱 [自主資料庫使用者 - 使資料庫可攜](https://msdn.microsoft.com/library/ff929188.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-232">For more information about contained database users, see [Contained Database Users- Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ddd41-233">無法使用入口網站來建立資料庫使用者 （與 hello 例外狀況的系統管理員）。</span><span class="sxs-lookup"><span data-stu-id="ddd41-233">Database users (with hello exception of administrators) cannot be created using portal.</span></span> <span data-ttu-id="ddd41-234">RBAC 角色不是傳播的 tooSQL 伺服器、 SQL 資料庫或 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="ddd41-234">RBAC roles are not propagated tooSQL Server, SQL Database, or SQL Data Warehouse.</span></span> <span data-ttu-id="ddd41-235">Azure RBAC 角色用來管理 Azure 資源，並不會套用 toodatabase 權限。</span><span class="sxs-lookup"><span data-stu-id="ddd41-235">Azure RBAC roles are used for managing Azure Resources, and do not apply toodatabase permissions.</span></span> <span data-ttu-id="ddd41-236">例如，hello **SQL Server 參與者**角色不授與存取 tooconnect toohello SQL Database 或 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="ddd41-236">For example, hello **SQL Server Contributor** role does not grant access tooconnect toohello SQL Database or SQL Data Warehouse.</span></span> <span data-ttu-id="ddd41-237">必須授與 hello 存取權限，直接在 hello 資料庫中使用 TRANSACT-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="ddd41-237">hello access permission must be granted directly in hello database using Transact-SQL statements.</span></span>
>

<span data-ttu-id="ddd41-238">Azure AD 架構自主資料庫使用者 （非 hello 伺服器系統管理員擁有 hello 資料庫），以具有使用者以 Azure AD 識別身分，連接 toohello 資料庫 toocreate 至少 hello **ALTER ANY USER**權限。</span><span class="sxs-lookup"><span data-stu-id="ddd41-238">toocreate an Azure AD-based contained database user (other than hello server administrator that owns hello database), connect toohello database with an Azure AD identity, as a user with at least hello **ALTER ANY USER** permission.</span></span> <span data-ttu-id="ddd41-239">接著，使用下列 TRANSACT-SQL 語法的 hello:</span><span class="sxs-lookup"><span data-stu-id="ddd41-239">Then use hello following Transact-SQL syntax:</span></span>

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="ddd41-240">*Azure_AD_principal_name*可以是 hello Azure AD 群組的 Azure AD 使用者或 hello 的顯示名稱的使用者主體名稱。</span><span class="sxs-lookup"><span data-stu-id="ddd41-240">*Azure_AD_principal_name* can be hello user principal name of an Azure AD user or hello display name for an Azure AD group.</span></span>

<span data-ttu-id="ddd41-241">**範例：** toocreate 自主的資料庫使用者代表 Azure AD 同盟或受管理網域使用者：</span><span class="sxs-lookup"><span data-stu-id="ddd41-241">**Examples:** toocreate a contained database user representing an Azure AD federated or managed domain user:</span></span>
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="ddd41-242">toocreate 自主的資料庫使用者代表 Azure AD 或同盟網域群組，提供 hello 顯示名稱的安全性群組：</span><span class="sxs-lookup"><span data-stu-id="ddd41-242">toocreate a contained database user representing an Azure AD or federated domain group, provide hello display name of a security group:</span></span>
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

<span data-ttu-id="ddd41-243">toocreate 代表連線使用 Azure AD 權杖的應用程式之自主的資料庫使用者：</span><span class="sxs-lookup"><span data-stu-id="ddd41-243">toocreate a contained database user representing an application that connects using an Azure AD token:</span></span>

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  <span data-ttu-id="ddd41-244">您無法直接從 Azure Active Directory 以外 hello 與您 Azure 訂用帳戶相關聯的 Azure Active Directory 中建立使用者。</span><span class="sxs-lookup"><span data-stu-id="ddd41-244">You cannot directly create a user from an Azure Active Directory other than hello Azure Active Directory that is associated with your Azure subscription.</span></span> <span data-ttu-id="ddd41-245">不過，會匯入的使用者在 hello 其他 Active Directory 的成員相關聯 Active Directory （稱為外部使用者） 可以在 hello 租用戶 Active Directory 中新增 tooan Active Directory 群組。</span><span class="sxs-lookup"><span data-stu-id="ddd41-245">However, members of other Active Directories that are imported users in hello associated Active Directory (known as external users) can be added tooan Active Directory group in hello tenant Active Directory.</span></span> <span data-ttu-id="ddd41-246">藉由建立該 AD 群組的自主的資料庫使用者，hello 使用者從 hello 外部的 Active Directory 可以獲得存取 tooSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ddd41-246">By creating a contained database user for that AD group, hello users from hello external Active Directory can gain access tooSQL Database.</span></span>   

<span data-ttu-id="ddd41-247">如需有關根據 Azure Active Directory 身分識別建立自主資料庫使用者的詳細資訊，請參閱 [CREATE USER (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-247">For more information about creating contained database users based on Azure Active Directory identities, see [CREATE USER (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ddd41-248">移除 Azure SQL server 的 hello Azure Active Directory 系統管理員可防止任何 Azure AD 驗證使用者 toohello 伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="ddd41-248">Removing hello Azure Active Directory administrator for Azure SQL server prevents any Azure AD authentication user from connecting toohello server.</span></span> <span data-ttu-id="ddd41-249">必要時，SQL Database 系統管理員可以手動刪除無法使用的 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="ddd41-249">If necessary, unusable Azure AD users can be dropped manually by a SQL Database administrator.</span></span>   

>  [!NOTE]
>  <span data-ttu-id="ddd41-250">如果您收到**連接逾時過期**，您可能需要 tooset hello `TransparentNetworkIPResolution` hello 連接字串 toofalse 參數。</span><span class="sxs-lookup"><span data-stu-id="ddd41-250">If you receive a **Connection Timeout Expired**, you may need tooset hello `TransparentNetworkIPResolution` parameter of hello connection string toofalse.</span></span> <span data-ttu-id="ddd41-251">如需詳細資訊，請參閱 [.NET Framework 4.6.1 的連線逾時問題 - TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-251">For more information, see [Connection timeout issue with .NET Framework 4.6.1 - TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/).</span></span>   

   
<span data-ttu-id="ddd41-252">當您建立資料庫使用者時，該使用者會收到 hello**連接**權限，而且可以連線 toothat 資料庫 hello 的成員身分**公用**角色。</span><span class="sxs-lookup"><span data-stu-id="ddd41-252">When you create a database user, that user receives hello **CONNECT** permission and can connect toothat database as a member of hello **PUBLIC** role.</span></span> <span data-ttu-id="ddd41-253">一開始 hello 只有權限可用 toohello 使用者，都授與的任何權限 toohello**公用**角色或任何權限授與 tooany Windows 群組，它們的成員。</span><span class="sxs-lookup"><span data-stu-id="ddd41-253">Initially hello only permissions available toohello user are any permissions granted toohello **PUBLIC** role, or any permissions granted tooany Windows groups that they are a member of.</span></span> <span data-ttu-id="ddd41-254">一旦您佈建 Azure AD 為基礎包含資料庫的使用者，您可以授與 hello 使用者額外權限、 hello 相同方式與您授與權限 tooany 其他類型的使用者。</span><span class="sxs-lookup"><span data-stu-id="ddd41-254">Once you provision an Azure AD-based contained database user, you can grant hello user additional permissions, hello same way as you grant permission tooany other type of user.</span></span> <span data-ttu-id="ddd41-255">通常 toodatabase 角色授與權限，並加入使用者 tooroles。</span><span class="sxs-lookup"><span data-stu-id="ddd41-255">Typically grant permissions toodatabase roles, and add users tooroles.</span></span> <span data-ttu-id="ddd41-256">如需詳細資訊，請參閱 [Database Engine 權限基本概念](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-256">For more information, see [Database Engine Permission Basics](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx).</span></span> <span data-ttu-id="ddd41-257">如需有關特殊 SQL Database 角色的詳細資訊，請參閱 [管理 Azure SQL Database 的資料庫和登入](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-257">For more information about special SQL Database roles, see [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="ddd41-258">匯入管理網域的同盟的網域使用者必須使用受管理的 hello 網域身分識別。</span><span class="sxs-lookup"><span data-stu-id="ddd41-258">A federated domain user that is imported into a manage domain, must use hello managed domain identity.</span></span>

> [!NOTE]
> <span data-ttu-id="ddd41-259">Azure AD 使用者標示 hello 資料庫中繼資料中具有類型為 E (EXTERNAL_USER) 和群組類型 X (EXTERNAL_GROUPS)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-259">Azure AD users are marked in hello database metadata with type E (EXTERNAL_USER) and for groups with type X (EXTERNAL_GROUPS).</span></span> <span data-ttu-id="ddd41-260">如需詳細資訊，請參閱 [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-260">For more information, see [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span> 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a><span data-ttu-id="ddd41-261">使用 SSMS 或 SSDT 連線 toohello 使用者資料庫或資料倉儲</span><span class="sxs-lookup"><span data-stu-id="ddd41-261">Connect toohello user database or data warehouse by using SSMS or SSDT</span></span>  
<span data-ttu-id="ddd41-262">tooconfirm hello Azure AD 管理員已正確設定，請連接 toohello**主要**使用 hello Azure AD 系統管理員帳戶的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ddd41-262">tooconfirm hello Azure AD administrator is properly set up, connect toohello **master** database using hello Azure AD administrator account.</span></span>
<span data-ttu-id="ddd41-263">tooprovision Azure AD 架構自主資料庫使用者 （非 hello 伺服器系統管理員擁有 hello 資料庫），會以 Azure AD 識別身分具有存取 toohello 資料庫連接 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ddd41-263">tooprovision an Azure AD-based contained database user (other than hello server administrator that owns hello database), connect toohello database with an Azure AD identity that has access toohello database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddd41-264">Visual Studio 2015 中的 [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 和 [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) 提供 Azure Active Directory 驗證支援。</span><span class="sxs-lookup"><span data-stu-id="ddd41-264">Support for Azure Active Directory authentication is available with [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) in Visual Studio 2015.</span></span> <span data-ttu-id="ddd41-265">hello SSMS 2016 年 8 月版本也支援 Active Directory 通用驗證，可讓系統管理員 toorequire Multi-factor Authentication 通話、 簡訊、 智慧卡使用 pin 或行動裝置應用程式通知。</span><span class="sxs-lookup"><span data-stu-id="ddd41-265">hello August 2016 release of SSMS also includes support for Active Directory Universal Authentication, which allows administrators toorequire Multi-Factor Authentication using a phone call, text message, smart cards with pin, or mobile app notification.</span></span>
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a><span data-ttu-id="ddd41-266">使用 Azure AD 身分識別 tooconnect 使用 SSMS 或 SSDT</span><span class="sxs-lookup"><span data-stu-id="ddd41-266">Using an Azure AD identity tooconnect using SSMS or SSDT</span></span>  

<span data-ttu-id="ddd41-267">下列程序的 hello 會告訴您如何 tooconnect tooa SQL 資料庫以使用 SQL Server Management Studio 或 SQL Server 資料庫工具的 Azure AD 識別身分。</span><span class="sxs-lookup"><span data-stu-id="ddd41-267">hello following procedures show you how tooconnect tooa SQL database with an Azure AD identity using SQL Server Management Studio or SQL Server Database Tools.</span></span>

### <a name="active-directory-integrated-authentication"></a><span data-ttu-id="ddd41-268">Active Directory 整合驗證</span><span class="sxs-lookup"><span data-stu-id="ddd41-268">Active Directory integrated authentication</span></span>

<span data-ttu-id="ddd41-269">如果您登入 tooWindows 同盟的網域從使用 Azure Active Directory 認證，請使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="ddd41-269">Use this method if you are logged in tooWindows using your Azure Active Directory credentials from a federated domain.</span></span>

1. <span data-ttu-id="ddd41-270">啟動 Management Studio 或 Data Tools 和 hello**連接 tooServer** (或**連接 tooDatabase 引擎**) 對話方塊中的，在 hello**驗證**方塊中，選取**Active Directory-整合**。</span><span class="sxs-lookup"><span data-stu-id="ddd41-270">Start Management Studio or Data Tools and in hello **Connect tooServer** (or **Connect tooDatabase Engine**) dialog box, in hello **Authentication** box, select **Active Directory - Integrated**.</span></span> <span data-ttu-id="ddd41-271">需要或由於您現有的認證將會顯示 hello 連線可以輸入任何密碼。</span><span class="sxs-lookup"><span data-stu-id="ddd41-271">No password is needed or can be entered because your existing credentials will be presented for hello connection.</span></span>   

    ![選取 AD 整合式驗證][11]
2. <span data-ttu-id="ddd41-273">按一下 hello**選項** 按鈕，在 hello**連接屬性** 頁面的 hello**連接 toodatabase**  方塊中，輸入 hello 名稱要 tooconnect hello 使用者資料庫的。</span><span class="sxs-lookup"><span data-stu-id="ddd41-273">Click hello **Options** button, and on hello **Connection Properties** page, in hello **Connect toodatabase** box, type hello name of hello user database you want tooconnect to.</span></span> <span data-ttu-id="ddd41-274">(hello **AD 網域名稱或租用戶識別碼**」 選項，才支援**通用 MFA 連線**選項，否則它會呈現灰色。)</span><span class="sxs-lookup"><span data-stu-id="ddd41-274">(hello **AD domain name or tenant ID**” option is only supported for **Universal with MFA connection** options, otherwise it is greyed out.)</span></span>  

    ![選取 hello 資料庫名稱][13]

## <a name="active-directory-password-authentication"></a><span data-ttu-id="ddd41-276">Active Directory 密碼驗證</span><span class="sxs-lookup"><span data-stu-id="ddd41-276">Active Directory password authentication</span></span>

<span data-ttu-id="ddd41-277">使用 Azure AD 主體名稱使用 hello Azure AD 連接受管理的網域時，請使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="ddd41-277">Use this method when connecting with an Azure AD principal name using hello Azure AD managed domain.</span></span> <span data-ttu-id="ddd41-278">您也可以使用同盟帳戶沒有存取 toohello 網域，例如當遠端工作。</span><span class="sxs-lookup"><span data-stu-id="ddd41-278">You can also use it for federated account without access toohello domain, for example when working remotely.</span></span>

<span data-ttu-id="ddd41-279">如果您登入 tooWindows 之網域不同盟與 Azure 中，使用認證，或者使用 Azure AD 驗證使用 Azure AD 根據初始 hello 或 hello 用戶端網域，請使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="ddd41-279">Use this method if you are logged in tooWindows using credentials from a domain that is not federated with Azure, or when using Azure AD authentication using Azure AD based on hello initial or hello client domain.</span></span>

1. <span data-ttu-id="ddd41-280">啟動 Management Studio 或 Data Tools 和 hello**連接 tooServer** (或**連接 tooDatabase 引擎**) 對話方塊中的，在 hello**驗證**方塊中，選取**Active Directory-密碼**。</span><span class="sxs-lookup"><span data-stu-id="ddd41-280">Start Management Studio or Data Tools and in hello **Connect tooServer** (or **Connect tooDatabase Engine**) dialog box, in hello **Authentication** box, select **Active Directory - Password**.</span></span>
2. <span data-ttu-id="ddd41-281">在 hello**使用者名**方塊中，輸入您的 Azure Active Directory 使用者名稱格式為 hello  **username@domain.com** 。這必須是從 hello Azure Active Directory 的帳戶，或與 hello Azure Active Directory 同盟的網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddd41-281">In hello **User name** box, type your Azure Active Directory user name in hello format **username@domain.com**. This must be an account from hello Azure Active Directory or an account from a domain federate with hello Azure Active Directory.</span></span>
3. <span data-ttu-id="ddd41-282">在 hello**密碼**方塊中，鍵入 hello Azure Active Directory 帳戶的使用者密碼或同盟網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddd41-282">In hello **Password** box, type your user password for hello Azure Active Directory account or federated domain account.</span></span>

    ![選取 AD 密碼驗證][12]
4. <span data-ttu-id="ddd41-284">按一下 hello**選項** 按鈕，在 hello**連接屬性** 頁面的 hello**連接 toodatabase**  方塊中，輸入 hello 名稱要 tooconnect hello 使用者資料庫的。</span><span class="sxs-lookup"><span data-stu-id="ddd41-284">Click hello **Options** button, and on hello **Connection Properties** page, in hello **Connect toodatabase** box, type hello name of hello user database you want tooconnect to.</span></span> <span data-ttu-id="ddd41-285">（請參閱 hello 圖形在 hello 先前選項）。</span><span class="sxs-lookup"><span data-stu-id="ddd41-285">(See hello graphic in hello previous option.)</span></span>

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a><span data-ttu-id="ddd41-286">使用 Azure AD 身分識別 tooconnect，從用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="ddd41-286">Using an Azure AD identity tooconnect from a client application</span></span>

<span data-ttu-id="ddd41-287">下列程序的 hello 會告訴您如何 tooconnect tooa SQL 資料庫與 Azure AD 身分識別從用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddd41-287">hello following procedures show you how tooconnect tooa SQL database with an Azure AD identity from a client application.</span></span>

###  <a name="active-directory-integrated-authentication"></a><span data-ttu-id="ddd41-288">Active Directory 整合驗證</span><span class="sxs-lookup"><span data-stu-id="ddd41-288">Active Directory integrated authentication</span></span>

<span data-ttu-id="ddd41-289">toouse 整合式 Windows 驗證，您網域的 Active Directory，必須與 Azure Active Directory 建立同盟。</span><span class="sxs-lookup"><span data-stu-id="ddd41-289">toouse integrated Windows authentication, your domain’s Active Directory must be federated with Azure Active Directory.</span></span> <span data-ttu-id="ddd41-290">用戶端應用程式 （或服務） 連接 toohello 資料庫必須在網域使用者的認證已加入網域的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="ddd41-290">Your client application (or a service) connecting toohello database must be running on a domain-joined machine under a user’s domain credentials.</span></span>

<span data-ttu-id="ddd41-291">tooconnect tooa 資料庫使用整合式驗證和 Azure AD 身分識別，hello 資料庫連接字串中的 hello 驗證關鍵字必須設 tooActive 目錄整合。</span><span class="sxs-lookup"><span data-stu-id="ddd41-291">tooconnect tooa database using integrated authentication and an Azure AD identity, hello Authentication keyword in hello database connection string must be set tooActive Directory Integrated.</span></span> <span data-ttu-id="ddd41-292">hello 下列 C# 程式碼範例會使用 ADO.NET。</span><span class="sxs-lookup"><span data-stu-id="ddd41-292">hello following C# code sample uses ADO .NET.</span></span>

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

<span data-ttu-id="ddd41-293">hello 連接字串關鍵字``Integrated Security=True``連接 tooAzure SQL Database 不支援。</span><span class="sxs-lookup"><span data-stu-id="ddd41-293">hello connection string keyword ``Integrated Security=True`` is not supported for connecting tooAzure SQL Database.</span></span> <span data-ttu-id="ddd41-294">建立 ODBC 連接時，您將會需要 tooremove 空間，並設定驗證 too'ActiveDirectoryIntegrated'。</span><span class="sxs-lookup"><span data-stu-id="ddd41-294">When making an ODBC connection, you will need tooremove spaces and set Authentication too'ActiveDirectoryIntegrated'.</span></span>

### <a name="active-directory-password-authentication"></a><span data-ttu-id="ddd41-295">Active Directory 密碼驗證</span><span class="sxs-lookup"><span data-stu-id="ddd41-295">Active Directory password authentication</span></span>

<span data-ttu-id="ddd41-296">tooconnect tooa 資料庫使用整合式驗證和 Azure AD 身分識別，hello 驗證關鍵字必須設 tooActive 目錄密碼。</span><span class="sxs-lookup"><span data-stu-id="ddd41-296">tooconnect tooa database using integrated authentication and an Azure AD identity, hello Authentication keyword must be set tooActive Directory Password.</span></span> <span data-ttu-id="ddd41-297">hello 連接字串必須包含使用者識別碼/UID 和 PWD 密碼/關鍵字的值。</span><span class="sxs-lookup"><span data-stu-id="ddd41-297">hello connection string must contain User ID/UID and Password/PWD keywords and values.</span></span> <span data-ttu-id="ddd41-298">hello 下列 C# 程式碼範例會使用 ADO.NET。</span><span class="sxs-lookup"><span data-stu-id="ddd41-298">hello following C# code sample uses ADO .NET.</span></span>

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

<span data-ttu-id="ddd41-299">深入了解 Azure AD 的驗證方法使用 hello 示範程式碼範例，可從[Azure AD 驗證 GitHub 示範](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-299">Learn more about Azure AD authentication methods using hello demo code samples available at [Azure AD Authentication GitHub Demo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).</span></span>

## <a name="azure-ad-token"></a><span data-ttu-id="ddd41-300">Azure AD 權杖</span><span class="sxs-lookup"><span data-stu-id="ddd41-300">Azure AD token</span></span>
<span data-ttu-id="ddd41-301">這種驗證方法允許從 Azure Active Directory (AAD) 取得 token 中介層服務 tooconnect tooAzure SQL Database 或 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="ddd41-301">This authentication method allows middle-tier services tooconnect tooAzure SQL Database or Azure SQL Data Warehouse by obtaining a token from Azure Active Directory (AAD).</span></span> <span data-ttu-id="ddd41-302">這可容許包含憑證型驗證的複雜案例。</span><span class="sxs-lookup"><span data-stu-id="ddd41-302">It enables sophisticated scenarios including certificate-based authentication.</span></span> <span data-ttu-id="ddd41-303">您必須完成四個基本步驟 toouse Azure AD 權杖驗證：</span><span class="sxs-lookup"><span data-stu-id="ddd41-303">You must complete four basic steps toouse Azure AD token authentication:</span></span>

1. <span data-ttu-id="ddd41-304">向 Azure Active Directory 註冊應用程式，並取得您的程式碼中的 hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="ddd41-304">Register your application with Azure Active Directory and get hello client id for your code.</span></span> 
2. <span data-ttu-id="ddd41-305">建立資料庫使用者代表 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddd41-305">Create a database user representing hello application.</span></span> <span data-ttu-id="ddd41-306">(稍早在步驟 6 中已完成)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-306">(Completed earlier in step 6.)</span></span>
3. <span data-ttu-id="ddd41-307">在 hello 的用戶端電腦執行 hello 應用程式建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="ddd41-307">Create a certificate on hello client computer runs hello application.</span></span>
4. <span data-ttu-id="ddd41-308">新增 hello 憑證做為您的應用程式的金鑰。</span><span class="sxs-lookup"><span data-stu-id="ddd41-308">Add hello certificate as a key for your application.</span></span>

<span data-ttu-id="ddd41-309">範例連接字串︰</span><span class="sxs-lookup"><span data-stu-id="ddd41-309">Sample connection string:</span></span>

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

<span data-ttu-id="ddd41-310">如需詳細資訊，請參閱 [SQL Server 安全性部落格](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-310">For more information, see [SQL Server Security Blog](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).</span></span>

### <a name="sqlcmd"></a><span data-ttu-id="ddd41-311">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="ddd41-311">sqlcmd</span></span>

<span data-ttu-id="ddd41-312">hello 的陳述式之後，連接使用 sqlcmd，可從 hello 13.1 新版[下載中心](http://go.microsoft.com/fwlink/?LinkID=825643)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-312">hello following statements, connect using version 13.1 of sqlcmd, which is available from hello [Download Center](http://go.microsoft.com/fwlink/?LinkID=825643).</span></span>

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a><span data-ttu-id="ddd41-313">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ddd41-313">Next steps</span></span>
- <span data-ttu-id="ddd41-314">如需 SQL Database 中存取權和控制權的概觀，請參閱 [SQL Database 的存取權和控制權](sql-database-control-access.md)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-314">For an overview of access and control in SQL Database, see [SQL Database access and control](sql-database-control-access.md).</span></span>
- <span data-ttu-id="ddd41-315">如需 SQL Database 中登入、使用者和資料庫角色的概觀，請參閱[登入、使用者和資料庫角色](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-315">For an overview of logins, users, and database roles in SQL Database, see [Logins, users, and database roles](sql-database-manage-logins.md).</span></span>
- <span data-ttu-id="ddd41-316">如需資料庫主體的詳細資訊，請參閱[主體](https://msdn.microsoft.com/library/ms181127.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-316">For more information about database principals, see [Principals](https://msdn.microsoft.com/library/ms181127.aspx).</span></span>
- <span data-ttu-id="ddd41-317">如需資料庫角色的詳細資訊，請參閱[資料庫角色](https://msdn.microsoft.com/library/ms189121.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-317">For more information about database roles, see [Database roles](https://msdn.microsoft.com/library/ms189121.aspx).</span></span>
- <span data-ttu-id="ddd41-318">如需 SQL Database 中防火牆規則的詳細資訊，請參閱 [SQL Database 防火牆規則](sql-database-firewall-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ddd41-318">For more information about firewall rules in SQL Database, see [SQL Database firewall rules](sql-database-firewall-configure.md).</span></span>

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

