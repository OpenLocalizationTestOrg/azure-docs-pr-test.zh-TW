---
title: "aaaDiscover，辨識，並在 Microsoft Azure 中的個人資料分類 |Microsoft 文件"
description: "深入了解搜尋、分類、探索及識別資料"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a><span data-ttu-id="b3a2f-103">在 Microsoft Azure 中探索、識別並分類個人資料</span><span class="sxs-lookup"><span data-stu-id="b3a2f-103">Discover, identify, and classify personal data in Microsoft Azure</span></span>

<span data-ttu-id="b3a2f-104">本文提供指引 toodiscover，識別、 和分類在數個 Azure 工具和服務，包括使用的 Azure HDInsight，Azure 中的 Hadoop 叢集的 Azure 資料目錄、 Azure Active Directory、 SQL 資料庫、 Power Query 中的個人資料的方式資訊保護，Azure 搜尋中，與 SQL Azure Cosmos DB 查詢。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-104">This article provides guidance on how toodiscover, identify, and classify personal data in several Azure tools and services, including using Azure Data Catalog, Azure Active Directory, SQL Database, Power Query for Hadoop clusters in Azure HDInsight, Azure Information Protection, Azure Search, and SQL queries for Azure Cosmos DB.</span></span>

## <a name="scenario-problem-statement-and-goal"></a><span data-ttu-id="b3a2f-105">情節、問題陳述和目標</span><span class="sxs-lookup"><span data-stu-id="b3a2f-105">Scenario, problem statement, and goal</span></span>

<span data-ttu-id="b3a2f-106">美國的運動公司會收集各種個人和其他資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-106">A U.S.-based sports company collects a variety of personal and other data.</span></span> <span data-ttu-id="b3a2f-107">這包括客戶和員工資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-107">This includes customers and employee data.</span></span> <span data-ttu-id="b3a2f-108">hello 公司保存在多個資料庫，並將它儲存在 Azure 環境中的數個不同位置。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-108">hello company keeps it in multiple databases, and stores it in several different locations in their Azure environment.</span></span> <span data-ttu-id="b3a2f-109">此外 tooselling 運動設備，它們也裝載和管理註冊的 hello world，包括在 hello EU，周圍精銳運動事件並在某些情況下 hello 它們所收集的客戶資料包含醫療資訊。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-109">In addition tooselling sports equipment, they also host and manage registration for elite athletic events around hello world, including in hello EU, and in some cases hello customer data they collect includes medical information.</span></span>

<span data-ttu-id="b3a2f-110">由於 hello 公司裝載許多國際 bicycling tours and techniques 每年，約聘人員中有 hello 全球各地，幾個 hello 資料集就相當大。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-110">Since hello company hosts many international bicycling tours every year and has contingent staff in locations around hello globe, a couple of hello data sets are quite large.</span></span> <span data-ttu-id="b3a2f-111">hello 公司也有可供客戶與員工的開發人員建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-111">hello company also has developer-built applications that are used by both customers and employees.</span></span>

<span data-ttu-id="b3a2f-112">hello 公司希望有 tooaddress hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="b3a2f-112">hello company wants tooaddress hello following problems:</span></span>

- <span data-ttu-id="b3a2f-113">客戶和員工的個人資料必須與 hello 分類/區別其他資料 hello 公司會收集在順序 tooensure 適當的存取和安全性。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-113">Customer and employee personal data must be classified/distinguished from hello other data hello company collects in order tooensure proper access and security.</span></span>
- <span data-ttu-id="b3a2f-114">hello 資料系統管理員必須 tooeasily 探索跨不同區域的 hello Azure 環境的 hello 客戶的個人資料的位置。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-114">hello data admin needs tooeasily discover hello location of customer personal data across various areas of hello Azure environment.</span></span>
- <span data-ttu-id="b3a2f-115">客戶和員工個人資料會出現在共用文件和電子郵件通訊必須標示為 toohelp 確保它保持安全。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-115">Customer and employee personal data that appears in shared documents and email communications must be labeled toohelp ensure that it’s kept secure.</span></span>
- <span data-ttu-id="b3a2f-116">hello 公司的應用程式開發人員需要在 web 和行動裝置應用程式的客戶和員工個人資料的方式 tooeasily 搜尋。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-116">hello company’s app developers need a way tooeasily search for customer and employee personal data in their web and mobile apps.</span></span>
- <span data-ttu-id="b3a2f-117">開發人員也需要 tooquery 其文件資料庫的個人資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-117">Developers also need tooquery their document database for personal data.</span></span>

### <a name="company-goals"></a><span data-ttu-id="b3a2f-118">公司目標</span><span class="sxs-lookup"><span data-stu-id="b3a2f-118">Company goals</span></span>

- <span data-ttu-id="b3a2f-119">所有客戶和員工的個人資料必須都已在 Azure 資料目錄中加以標記/標註，以便能夠輕鬆地找到。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-119">All customer and employee personal data must be tagged/annotated in Azure Data Catalog so it can be found easily.</span></span> <span data-ttu-id="b3a2f-120">在理想情況下，客戶和員工的個人資料會分開標記/標註。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-120">Ideally customer and employee personal data are tagged/annotated separately.</span></span>
- <span data-ttu-id="b3a2f-121">必須能夠輕鬆地從位於 Azure Active Directory 中的客戶和員工使用者設定檔和工作資訊找到個人資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-121">Personal data from customer and employee user profiles and work information residing in Azure Active Directory must be easily located.</span></span>
- <span data-ttu-id="b3a2f-122">必須能夠輕鬆地查詢位在多個 SQL Database 中的個人資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-122">Personal data residing in multiple SQL databases must be easily queried.</span></span> 
- <span data-ttu-id="b3a2f-123">某些 hello 公司的大型資料集是透過 Azure HDInsight 並儲存在 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-123">Some of hello company’s large data sets are managed through Azure HDInsight and stored in Hadoop.</span></span> <span data-ttu-id="b3a2f-124">必須將這些資料集匯入 Excel 中，以便可以查詢個人資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-124">They must be imported into Excel so they can be queried for personal data.</span></span>
- <span data-ttu-id="b3a2f-125">在文件及電子郵件通訊中共用的個人資料必須加以分類、標記，並使用 Azure 資訊保護來保持安全。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-125">Personal data shared in documents and email communications must be classified, labeled, and kept secure with Azure Information Protection.</span></span>
- <span data-ttu-id="b3a2f-126">hello 公司的應用程式開發人員必須要能夠 toodiscover 客戶和員工個人資料 hello 的應用程式建立了它們，它們可以使用 Azure 搜尋作業中。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-126">hello company’s app developers must be able toodiscover customer and employee personal data in hello apps they’ve built, which they can do with Azure Search.</span></span>
- <span data-ttu-id="b3a2f-127">開發人員必須要能夠 toofind 其文件資料庫中的個人資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-127">Developers must be able toofind personal data in their document database.</span></span>

## <a name="azure-active-directory-data-discovery"></a><span data-ttu-id="b3a2f-128">Azure Active Directory：資料探索</span><span class="sxs-lookup"><span data-stu-id="b3a2f-128">Azure Active Directory: Data discovery</span></span>

<span data-ttu-id="b3a2f-129">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 是 Microsoft 的雲端式、多租用戶目錄和身分識別管理服務。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-129">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span> <span data-ttu-id="b3a2f-130">客戶和員工的使用者設定檔和包含個人資料中的使用者工作資訊，可以找出您[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) 環境使用 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-130">You can locate customer and employee user profiles and user work information that contain personal data in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="b3a2f-131">如果您想 toofind 或變更特定使用者的個人資料，這會特別有用。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-131">This is particularly helpful if you want toofind or change personal data for a specific user.</span></span> <span data-ttu-id="b3a2f-132">您也可以新增或變更使用者設定檔及工作資訊。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-132">You can also add or change user profile and work information.</span></span> <span data-ttu-id="b3a2f-133">您必須使用屬於 hello 目錄全域管理員帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-133">You must sign in with an account that’s a global admin for hello directory.</span></span>

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a><span data-ttu-id="b3a2f-134">如何找出或檢視使用者設定檔和工作資訊？</span><span class="sxs-lookup"><span data-stu-id="b3a2f-134">How do I locate or view user profile and work information?</span></span>

1. <span data-ttu-id="b3a2f-135">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-135">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="b3a2f-136">選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-136">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![如何找出使用者設定檔和工作資訊](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. <span data-ttu-id="b3a2f-138">在 hello**使用者和群組**刀鋒視窗中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-138">On hello **Users and groups** blade, select **Users**.</span></span>

  ![開啟使用者和群組](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. <span data-ttu-id="b3a2f-140">在 [hello**使用者和群組的使用者**刀鋒視窗中，從 [hello] 清單中，選取使用者，然後用 hello 選使用者的 hello] 刀鋒視窗，選取**設定檔**tooview 可能包含個人資料的使用者設定檔資訊.</span><span class="sxs-lookup"><span data-stu-id="b3a2f-140">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview user profile information that might contain personal data.</span></span>

  ![選取使用者](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. <span data-ttu-id="b3a2f-142">如果您需要 tooadd 或變更使用者設定檔資訊時，您可以這樣做，然後 hello 命令列中，選取 **儲存。**</span><span class="sxs-lookup"><span data-stu-id="b3a2f-142">If you need tooadd or change user profile information, you can do so, and then, in hello command bar, select **Save.**</span></span>
6. <span data-ttu-id="b3a2f-143">在 hello 選使用者的 hello 刀鋒視窗，選取 **工作資訊**tooview 使用者工作的資訊可能包含個人資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-143">On hello blade for hello selected user, select **Work Info** tooview user work information that may contain personal data.</span></span>

 ![檢視工作資訊](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. <span data-ttu-id="b3a2f-145">如果您需要 tooadd 或變更使用者的工作資訊時，您可以這樣做，然後 hello 命令列中，選取 **儲存。**</span><span class="sxs-lookup"><span data-stu-id="b3a2f-145">If you need tooadd or change user work information, you can do so, and then, in hello command bar, select **Save.**</span></span>

## <a name="azure-sql-database-data-discovery"></a><span data-ttu-id="b3a2f-146">Azure SQL Database：資料探索</span><span class="sxs-lookup"><span data-stu-id="b3a2f-146">Azure SQL Database: Data discovery</span></span>

<span data-ttu-id="b3a2f-147">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 是雲端資料庫，可協助開發人員建置及維護應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-147">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span> <span data-ttu-id="b3a2f-148">您可以使用標準 SQL 查詢在 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 中找到個人資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-148">Personal data can be found in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries.</span></span> <span data-ttu-id="b3a2f-149">Azure SQL 彈性查詢 （預覽） 可讓使用者 tooperform 跨資料庫查詢。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-149">Azure SQL elastic query (preview) enables users tooperform cross-database queries.</span></span>

<span data-ttu-id="b3a2f-150">詳細[SQL database](../sql-database/sql-database-technical-overview.md)教學課程會說明許多層面使用 SQL 資料庫，包括如何 toobuild 一個以及 toorun 資料查詢。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-150">A detailed [SQL database](../sql-database/sql-database-technical-overview.md) tutorial explains many aspects of using a SQL database, including how toobuild one and how toorun data queries.</span></span> <span data-ttu-id="b3a2f-151">hello 以下是可用 hello 連結 toospecific 章節的教學課程中的 hello 資訊的摘要。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-151">hello following is a summary of hello information available in hello tutorial with links toospecific sections.</span></span>

### <a name="how-do-i-build-a-sql-database"></a><span data-ttu-id="b3a2f-152">如何建置 SQL Database？</span><span class="sxs-lookup"><span data-stu-id="b3a2f-152">How do I build a SQL database?</span></span>

<span data-ttu-id="b3a2f-153">有三種方式 toodo 它：</span><span class="sxs-lookup"><span data-stu-id="b3a2f-153">There are three ways toodo it:</span></span>

- <span data-ttu-id="b3a2f-154">Azure SQL database 可由 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-154">An Azure SQL database can be created in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="b3a2f-155">在 hello 教學課程中，您將使用一組特定的資源群組和邏輯伺服器內的運算和存放裝置資源。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-155">In hello tutorial, you’ll use a specific set of compute and storage resources within a resource group and logical server.</span></span> <span data-ttu-id="b3a2f-156">您會使用名為 AdventureWorks 的虛構公司之範例資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-156">You’ll use sample data from a fictitious company called AdventureWorks.</span></span> <span data-ttu-id="b3a2f-157">您還會建立伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-157">You’ll also create a server-level firewall rule.</span></span> <span data-ttu-id="b3a2f-158">toolearn 如何 toodo 這個，請瀏覽 hello [hello Azure 入口網站中建立 Azure SQL database](../sql-database/sql-database-get-started-portal.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-158">toolearn how toodo this, visit hello [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md) tutorial.</span></span>

  ![建立 Azure SQL Database](media/how-to-discover-classify-personal-data-azure/create-database.png)
- <span data-ttu-id="b3a2f-160">SQL database 也可以建立在 hello [Azure 雲端殼層](https://azure.microsoft.com/features/cloud-shell/)CLI，瀏覽器為基礎的命令列工具。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-160">A SQL database can also be created in hello [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) CLI, a browser-based command-line tool.</span></span> <span data-ttu-id="b3a2f-161">hello 工具使用 hello Azure 入口網站中，可以直接從該處執行。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-161">hello tool is available in hello Azure portal and can be run directly from there.</span></span> <span data-ttu-id="b3a2f-162">本教學課程中，在您啟動 hello 工具、 定義指令碼變數建立資源群組和邏輯伺服器，並設定伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-162">In this tutorial, you launch hello tool, define script variables, create a resource group and logical server, and configure a server firewall rule.</span></span> <span data-ttu-id="b3a2f-163">然後使用範例資料建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-163">Then you create a database with sample data.</span></span> <span data-ttu-id="b3a2f-164">toolearn 如何 toocreate 資料庫如此一來，請瀏覽 hello[建立單一的 Azure SQL database，使用 Azure CLI hello](../sql-database/sql-database-get-started-cli.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-164">toolearn how toocreate your database this way, visit hello [Create a single Azure SQL database using hello Azure CLI](../sql-database/sql-database-get-started-cli.md) tutorial.</span></span>

  ![CLI 教學課程](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
<span data-ttu-id="b3a2f-166">Linux 系統管理員和開發人員通常都是使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-166">Azure CLI is commonly used by Linux admins and developers.</span></span> <span data-ttu-id="b3a2f-167">某些使用者認為它比 PowerShell (這是您的第三個選項) 更簡單且更直覺。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-167">Some users find it easier and more intuitive than PowerShell, which is your third option.</span></span>

- <span data-ttu-id="b3a2f-168">最後，您可以建立 SQL 資料庫使用 PowerShell，也就是命令/指令碼使用的工具 toocreate 及管理 Azure 及其他資源。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-168">Finally, you can create a SQL database using PowerShell, which is a command line/script tool used toocreate and manage Azure and other resources.</span></span> <span data-ttu-id="b3a2f-169">本教學課程中，在您啟動 hello 工具、 定義指令碼變數建立資源群組和邏輯伺服器，並設定伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-169">In this tutorial, you launch hello tool, define script variables, create a resource group and logical server, and configure a server firewall rule.</span></span> <span data-ttu-id="b3a2f-170">然後使用範例資料建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-170">Then you’ll create a database with sample data.</span></span>

<span data-ttu-id="b3a2f-171">hello 教學課程需要 hello Azure PowerShell 模組版本 4.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-171">hello tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="b3a2f-172">執行 Get-module-ListAvailable AzureRM toofind 您的版本。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-172">Run  Get-Module -ListAvailable AzureRM toofind your version.</span></span> <span data-ttu-id="b3a2f-173">如果您需要 tooinstall 或升級，請參閱安裝 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-173">If you need tooinstall or upgrade, see Install Azure PowerShell module.</span></span>

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

<span data-ttu-id="b3a2f-174">toolearn 如何 toocreate 資料庫如此一來，請瀏覽 hello[建立單一的 Azure SQL database，使用 Powershell](../sql-database/sql-database-get-started-powershell.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-174">toolearn how toocreate your database this way, visit hello [Create a single Azure SQL database using Powershell](../sql-database/sql-database-get-started-powershell.md) tutorial.</span></span>

>[!Note]
<span data-ttu-id="b3a2f-175">Windows 系統管理員通常 toouse PowerShell 中，但其中部分偏好 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-175">Windows admins tend toouse PowerShell, but some of them prefer Azure CLI.</span></span>

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a><span data-ttu-id="b3a2f-176">我該如何搜尋 hello Azure 入口網站中的 SQL database 中的個人資料？ * *</span><span class="sxs-lookup"><span data-stu-id="b3a2f-176">How do I search for personal data in SQL database in hello Azure portal?**</span></span>

<span data-ttu-id="b3a2f-177">您可以使用內部 hello Azure 入口網站 toosearch hello 內建查詢編輯器 」 工具的個人資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-177">You can use hello built-in query editor tool inside hello Azure portal toosearch for personal data.</span></span> <span data-ttu-id="b3a2f-178">將登入使用您的 SQL server 系統管理員登入和密碼，toohello 工具，並接著輸入查詢。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-178">You’ll log in toohello tool using your SQL server admin login and password, and then enter a query.</span></span>

  ![搜尋使用 hello 入口網站的 sql](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

<span data-ttu-id="b3a2f-180">Hello 教學課程的步驟 5 hello 查詢編輯器 窗格中顯示的範例查詢，但它不會著重於個人或機密資訊 （它也會結合兩個資料表的資料，並建立 hello 來源資料行的別名 hello 資料集中所傳回）。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-180">Step 5 of hello tutorial shows an example query in hello query editor pane, but it  doesn’t focus on personal or sensitive information(it also combines data from two tables and creates aliases for hello source column in hello data set being returned).</span></span> <span data-ttu-id="b3a2f-181">hello 下列螢幕擷取畫面顯示 hello 查詢從步驟 5 和 hello 傳回的結果窗格：</span><span class="sxs-lookup"><span data-stu-id="b3a2f-181">hello following screenshot shows hello query from Step 5 as well as hello results pane that’s returned:</span></span>

  ![查詢編輯器](media/how-to-discover-classify-personal-data-azure/query-editor.png)

<span data-ttu-id="b3a2f-183">如果您的資料庫稱為 MyTable，個人資訊的範例查詢可能就會包括名稱、社會安全號碼和識別碼，且會看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="b3a2f-183">If your database was called MyTable, a sample query for personal information might include name, Social Security number and ID number and would look like this:</span></span>

<span data-ttu-id="b3a2f-184">「選取名稱、社會安全號碼、MyTable 的識別碼」</span><span class="sxs-lookup"><span data-stu-id="b3a2f-184">“SELECT Name, SSN, ID number FROM MyTable”</span></span>

<span data-ttu-id="b3a2f-185">您會執行 hello 查詢，並接著看到 hello 導致 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-185">You’d run hello query and then see hello results in hello **Results** pane.</span></span>

<span data-ttu-id="b3a2f-186">如需有關如何 tooquery SQL 資料庫 hello Azure 入口網站中的詳細資訊，請瀏覽 hello[查詢 hello SQL database](../sql-database/sql-database-get-started-portal.md) hello 教學課程 > 一節。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-186">For more information on how tooquery a SQL database in hello Azure portal, visit hello [Query hello SQL database](../sql-database/sql-database-get-started-portal.md) section of hello tutorial.</span></span>

### <a name="how-do-i-search-for-data-across-multiple-databases"></a><span data-ttu-id="b3a2f-187">如何跨多個資料庫搜尋資料？</span><span class="sxs-lookup"><span data-stu-id="b3a2f-187">How do I search for data across multiple databases?</span></span>

<span data-ttu-id="b3a2f-188">SQL 彈性查詢 （預覽） 可讓您 tooperform 跨資料庫和多個資料庫查詢，並傳回單一結果。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-188">SQL elastic query (preview) enables you tooperform cross-database and multiple database queries and return a single result.</span></span> <span data-ttu-id="b3a2f-189">hello[教學課程概觀](../sql-database/sql-database-elastic-query-overview.md)包含案例詳細的描述，並說明 hello 差異垂直和水平的資料庫分割。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-189">hello [tutorial overview](../sql-database/sql-database-elastic-query-overview.md) includes a detailed description of scenarios and explains hello difference between vertical and horizontal database partitioning.</span></span> <span data-ttu-id="b3a2f-190">水平資料分割稱為「分區化」。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-190">Horizontal partitioning is called “sharding.”</span></span>

  ![垂直資料分割](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![水平資料分割](media/how-to-discover-classify-personal-data-azure/horizontal.png)

<span data-ttu-id="b3a2f-193">tooget 啟動，請瀏覽 hello [Azure SQL Database 彈性的查詢概觀 （預覽）](../sql-database/sql-database-elastic-query-overview.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-193">tooget started, visit hello [Azure SQL Database elastic query overview (preview)](../sql-database/sql-database-elastic-query-overview.md) page.</span></span>

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a><span data-ttu-id="b3a2f-194">Power Query (適用於匯入 Azure HDInsight Hadoop 叢集)：大型資料集的資料探索</span><span class="sxs-lookup"><span data-stu-id="b3a2f-194">Power Query (for importing Azure HDInsight Hadoop clusters): data discovery for large data sets</span></span>

<span data-ttu-id="b3a2f-195">Hadoop 是開放原始碼 Apache 儲存體和大型資料集的處理服務，會在 Hadoop 叢集中進行分析並加以儲存。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-195">Hadoop is an open source Apache storage and processing service for large data sets, which are analyzed and stored in Hadoop clusters.</span></span> <span data-ttu-id="b3a2f-196">[Azure HDInsight](https://azure.microsoft.com/services/hdinsight/)可讓在 Azure 中的使用者 toowork 的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-196">[Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) allows users toowork with Hadoop clusters in Azure.</span></span> <span data-ttu-id="b3a2f-197">Power Query 是 Excel 增益集，除此之外，還可協助使用者從不同的來源探索資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-197">Power Query is an Excel add-in that, among other things, helps users discover data from different sources.</span></span>

<span data-ttu-id="b3a2f-198">在 Azure HDInsight Hadoop 叢集相關聯的個人資料可以匯入的 tooExcel 有了 Power Query。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-198">Personal data associated with Hadoop clusters in Azure HDInsight can be imported tooExcel with Power Query.</span></span> <span data-ttu-id="b3a2f-199">一旦 hello 資料位於 Excel 內，您就可以使用查詢 tooidentify 它。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-199">Once hello data is in Excel you can use a query tooidentify it.</span></span>

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a><span data-ttu-id="b3a2f-200">如何使用 Excel 的 Power Query tooimport Hadoop 叢集在 Azure HDInsight 到 Excel？</span><span class="sxs-lookup"><span data-stu-id="b3a2f-200">How do I use Excel Power Query tooimport Hadoop clusters in Azure HDInsight into Excel?</span></span>

<span data-ttu-id="b3a2f-201">HDInsight 教學課程將引導您完成這整個程序。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-201">An HDInsight tutorial will walk you through this entire process.</span></span> <span data-ttu-id="b3a2f-202">它說明必要條件，並包含連結 tooa[開始使用 Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-202">It explains prerequisites, and includes a link tooa [Get started with Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) tutorial.</span></span> <span data-ttu-id="b3a2f-203">指示涵蓋 Excel 2016 2013年和 2010年 （步驟都稍有不同 Excel hello 較舊版本）。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-203">Instructions cover Excel 2016 as well as 2013 and 2010 (steps are slightly different for hello older versions of Excel).</span></span> <span data-ttu-id="b3a2f-204">如果您沒有 hello Excel Power Query 增益集，hello 教學課程將告訴您如何 tooget 它。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-204">If you don’t have hello Excel Power Query add-in, hello tutorial shows you how tooget it.</span></span> <span data-ttu-id="b3a2f-205">您會在 Excel 中啟動 hello 教學課程，而且必須的 toohave 與叢集相關聯的 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-205">You’ll start hello tutorial in Excel and will need toohave an Azure Blob storage account associated with your cluster.</span></span>

  ![在 Excel 中的查詢](media/how-to-discover-classify-personal-data-azure/excel.png)

<span data-ttu-id="b3a2f-207">toolearn 如何 toodo 這個，請瀏覽 hello[使用 Power Query 連接的 Excel tooHadoop](../hdinsight/hdinsight-connect-excel-power-query.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-207">toolearn how toodo this, visit hello [Connect Excel tooHadoop by using Power Query](../hdinsight/hdinsight-connect-excel-power-query.md) tutorial.</span></span>

<span data-ttu-id="b3a2f-208">來源：[使用 Power Query 連接 Excel tooHadoop](../hdinsight/hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="b3a2f-208">Source: [Connect Excel tooHadoop by using Power Query](../hdinsight/hdinsight-connect-excel-power-query.md)</span></span>

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a><span data-ttu-id="b3a2f-209">Azure 資訊保護：文件和電子郵件的個人資料分類</span><span class="sxs-lookup"><span data-stu-id="b3a2f-209">Azure Information Protection: personal data classification for documents and email</span></span>

<span data-ttu-id="b3a2f-210">[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection)可協助 Azure 客戶套用標籤 tooclassify 及保護內部或外部共用的文件與電子郵件通訊。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-210">[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) can help Azure customers apply labels tooclassify and protect internally or externally shared documents and email communications.</span></span> <span data-ttu-id="b3a2f-211">這些項目有些可能會包含客戶或員工的個人資訊。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-211">Some of these items may contain customer or employee personal information.</span></span> <span data-ttu-id="b3a2f-212">系統管理員或使用者可以自動或手動方式定義規則和條件。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-212">Rules and conditions can be defined automatically or manually, by administrators or by users.</span></span> <span data-ttu-id="b3a2f-213">例如，如果使用者儲存文件，其中包含信用卡資訊，請他或她會看到由 hello 管理員設定的標籤建議。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-213">For example, if a user is saving a document that includes credit card information, he or she would see a label recommendation that was configured by hello administrator.</span></span>

### <a name="how-do-i-try-it"></a><span data-ttu-id="b3a2f-214">如何嘗試？</span><span class="sxs-lookup"><span data-stu-id="b3a2f-214">How do I try it?</span></span>

<span data-ttu-id="b3a2f-215">如果您想要 Azure Information Protection 再試一次 toosee toogive，如果它可能是適合您的組織，請瀏覽 hello[快速入門教學課程](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial)。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-215">If you’d like toogive Azure Information Protection a try toosee if it might be a fit for your organization, visit hello [Quickstart tutorial](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial).</span></span> <span data-ttu-id="b3a2f-216">它會引導您執行五個基本步驟，從安裝 tooconfiguring 原則 tooseeing 分類、 標記和動作中的共用 — 和花費時間不超過一小時。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-216">It walks you through five basic steps—from installation tooconfiguring policy tooseeing classification, labeling, and sharing in action—and should take less than a half hour.</span></span>

### <a name="how-do-i-deploy-it"></a><span data-ttu-id="b3a2f-217">如何進行部署？</span><span class="sxs-lookup"><span data-stu-id="b3a2f-217">How do I deploy it?</span></span>

<span data-ttu-id="b3a2f-218">如果您想為您的組織要 toodeploy Azure Information Protection，請瀏覽 hello[分類、 標記和保護的部署藍圖](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap)。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-218">If you’d like toodeploy Azure Information Protection for your organization, visit hello [deployment roadmap for classification, labeling, and protection](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).</span></span>

### <a name="is-there-anything-else-i-should-know"></a><span data-ttu-id="b3a2f-219">還有其他須知事項嗎？</span><span class="sxs-lookup"><span data-stu-id="b3a2f-219">Is there anything else I should know?</span></span>

<span data-ttu-id="b3a2f-220">如互補的資訊可協助您思考如何 tooset 它，請瀏覽 hello[就緒、 設定、 保護 ！](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)</span><span class="sxs-lookup"><span data-stu-id="b3a2f-220">For complementary information that will help you think through how tooset it up, visit hello [Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)</span></span>
<span data-ttu-id="b3a2f-221">部落格文章。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-221">blog post.</span></span> <span data-ttu-id="b3a2f-222">並核取 hello 了更多如需有關 Azure Information Protection 下面所列的連結。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-222">And check hello Learn more links listed below for more on Azure Information Protection.</span></span>

## <a name="azure-search-data-discovery-for-developer-apps"></a><span data-ttu-id="b3a2f-223">Azure 搜尋服務：開發人員應用程式的資料探索</span><span class="sxs-lookup"><span data-stu-id="b3a2f-223">Azure Search: data discovery for developer apps</span></span>

<span data-ttu-id="b3a2f-224">[Azure 搜尋服務](https://azure.microsoft.com/services/search/)是開發人員的雲端搜尋解決方案，可為您的應用程式提供豐富的資料搜尋體驗。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-224">[Azure Search](https://azure.microsoft.com/services/search/) is a cloud search solution for developers, and provides a rich data search experience for your applications.</span></span> <span data-ttu-id="b3a2f-225">Azure 搜尋可讓您 toolocate 資料到使用者定義的索引，源自 Azure Cosmo DB、 Azure SQL Database、 Azure Blob 儲存體、 Azure 資料表儲存體或自訂客戶 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-225">Azure Search allows you toolocate data across user-defined indexes, sourced from Azure Cosmo DB, Azure SQL Database, Azure Blob Storage, Azure Table storage, or custom customer JSON data.</span></span> <span data-ttu-id="b3a2f-226">您也可以建構的個人資料類型或 hello 的特定人員的個人資料使用 hello Azure 搜尋 REST API toosearch Lucene 查詢。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-226">You can also structure Lucene queries using hello Azure Search REST API toosearch for personal data types or hello personal data of specific individuals.</span></span> <span data-ttu-id="b3a2f-227">功能包括全文檢索搜尋、簡單查詢語法及 Lucene 查詢語法。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-227">Features include full text search, simple query syntax, and Lucene query syntax.</span></span> 

## <a name="how-do-i-use-sql-tooquery-data"></a><span data-ttu-id="b3a2f-228">如何使用 SQL tooquery 資料？</span><span class="sxs-lookup"><span data-stu-id="b3a2f-228">How do I use SQL tooquery data?</span></span>

<span data-ttu-id="b3a2f-229">toobegin 與 hello 基本概念，請瀏覽 hello [Azure CosmosD DB： 如何使用 SQL tooquery](../cosmos-db/tutorial-query-documentdb.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-229">toobegin with hello basics, visit hello [Azure CosmosD DB: How tooquery using SQL](../cosmos-db/tutorial-query-documentdb.md) tutorial.</span></span> <span data-ttu-id="b3a2f-230">hello 教學課程提供範例文件和兩個範例 SQL 查詢和結果。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-230">hello tutorial provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="b3a2f-231">如需有關建置 SQL 查詢的詳細指引，請瀏覽 [Azure Cosmos DB 文件 DB API 的 SQL 查詢。](../cosmos-db/documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="b3a2f-231">For more in-depth guidance on building SQL queries, visit [SQL queries for Azure Cosmos DB Document DB API.](../cosmos-db/documentdb-sql-query.md)</span></span>

<span data-ttu-id="b3a2f-232">如果您使用新 tooAzure Cosmos DB，就像 toolearn 方式 toocreate 資料庫中，新增集合，以及加入資料，請瀏覽 hello [Azure Cosmos DB： 建置 DocumentDB API 的 web 應用程式](../cosmos-db/create-documentdb-dotnet.md)快速入門教學課程。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-232">If you’re new tooAzure Cosmos DB and would like toolearn how toocreate a database, add a collection, and add data, visit hello [Azure Cosmos DB: Build a DocumentDB API web app](../cosmos-db/create-documentdb-dotnet.md) Quickstart tutorial.</span></span> <span data-ttu-id="b3a2f-233">如果您想要 toodo 這.NET、 Java 或 Python，例如以外的語言只要選擇您慣用的語言後您 toohello 站台。</span><span class="sxs-lookup"><span data-stu-id="b3a2f-233">If you’d like toodo this in a language other than .NET, such as Java or Python, just choose your preferred language once you get toohello site.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3a2f-234">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3a2f-234">Next steps</span></span>

[<span data-ttu-id="b3a2f-235">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="b3a2f-235">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50)

[<span data-ttu-id="b3a2f-236">什麼是 SQL Database？</span><span class="sxs-lookup"><span data-stu-id="b3a2f-236">What is SQL Database?</span></span>](../sql-database/sql-database-technical-overview.md)

<span data-ttu-id="b3a2f-237">[Azure 入口網站中可用的 SQL Database 查詢編輯器] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)</span><span class="sxs-lookup"><span data-stu-id="b3a2f-237">[SQL Database Query Editor available in Azure portal] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)</span></span>

[<span data-ttu-id="b3a2f-238">什麼是 Azure 資訊保護？</span><span class="sxs-lookup"><span data-stu-id="b3a2f-238">What is Azure Information Protection?</span></span>](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[<span data-ttu-id="b3a2f-239">什麼是 Azure Rights Management？</span><span class="sxs-lookup"><span data-stu-id="b3a2f-239">What is Azure Rights Management?</span></span>](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[<span data-ttu-id="b3a2f-240">Azure 資訊保護：就緒、設定、保護！</span><span class="sxs-lookup"><span data-stu-id="b3a2f-240">Azure Information Protection: Ready, set, protect!</span></span>](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
