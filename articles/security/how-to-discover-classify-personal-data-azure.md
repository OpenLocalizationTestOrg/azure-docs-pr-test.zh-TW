---
title: "在 Microsoft Azure 中探索、識別並分類個人資料 | Microsoft Docs"
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
ms.openlocfilehash: 6ccb064a9a76e7041d4f365b3997673dc9182e0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a><span data-ttu-id="42bdc-103">在 Microsoft Azure 中探索、識別並分類個人資料</span><span class="sxs-lookup"><span data-stu-id="42bdc-103">Discover, identify, and classify personal data in Microsoft Azure</span></span>

<span data-ttu-id="42bdc-104">本文提供指導方針，說明如何在數個 Azure 工具和服務中探索、識別和分類個人資料，包括使用 Azure 資料目錄、Azure Active Directory、SQL Database、Azure HDInsight 中適用於 Hadoop 叢集的 Power Query、Azure 資訊保護、Azure 搜尋服務，以及適用於 Azure Cosmos DB 的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="42bdc-104">This article provides guidance on how to discover, identify, and classify personal data in several Azure tools and services, including using Azure Data Catalog, Azure Active Directory, SQL Database, Power Query for Hadoop clusters in Azure HDInsight, Azure Information Protection, Azure Search, and SQL queries for Azure Cosmos DB.</span></span>

## <a name="scenario-problem-statement-and-goal"></a><span data-ttu-id="42bdc-105">情節、問題陳述和目標</span><span class="sxs-lookup"><span data-stu-id="42bdc-105">Scenario, problem statement, and goal</span></span>

<span data-ttu-id="42bdc-106">美國的運動公司會收集各種個人和其他資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-106">A U.S.-based sports company collects a variety of personal and other data.</span></span> <span data-ttu-id="42bdc-107">這包括客戶和員工資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-107">This includes customers and employee data.</span></span> <span data-ttu-id="42bdc-108">該公司會將資料保存在多個資料庫中，並將它儲存在其 Azure 環境中的數個不同位置。</span><span class="sxs-lookup"><span data-stu-id="42bdc-108">The company keeps it in multiple databases, and stores it in several different locations in their Azure environment.</span></span> <span data-ttu-id="42bdc-109">除了銷售運動設備之外，它們還會主辦全世界精銳運動事件並管理註冊，包含在 EU 和在某些案例中，它們所收集的客戶資料包含醫療資訊。</span><span class="sxs-lookup"><span data-stu-id="42bdc-109">In addition to selling sports equipment, they also host and manage registration for elite athletic events around the world, including in the EU, and in some cases the customer data they collect includes medical information.</span></span>

<span data-ttu-id="42bdc-110">由於公司每年都會主辦多場國際自行車巡迴賽，並在全球各地都擁有代表團人員，幾個資料集就相當大了。</span><span class="sxs-lookup"><span data-stu-id="42bdc-110">Since the company hosts many international bicycling tours every year and has contingent staff in locations around the globe, a couple of the data sets are quite large.</span></span> <span data-ttu-id="42bdc-111">該公司也有開發人員建置的應用程式，可供客戶與員工使用。</span><span class="sxs-lookup"><span data-stu-id="42bdc-111">The company also has developer-built applications that are used by both customers and employees.</span></span>

<span data-ttu-id="42bdc-112">公司需要解決下列問題：</span><span class="sxs-lookup"><span data-stu-id="42bdc-112">The company wants to address the following problems:</span></span>

- <span data-ttu-id="42bdc-113">必須從公司收集的其他資料中分類/辨別客戶和員工的個人資料，從而確保適當的存取與安全性。</span><span class="sxs-lookup"><span data-stu-id="42bdc-113">Customer and employee personal data must be classified/distinguished from the other data the company collects in order to ensure proper access and security.</span></span>
- <span data-ttu-id="42bdc-114">資料管理需要跨 Azure 環境的不同區域，輕鬆地探索客戶個人資料的位置。</span><span class="sxs-lookup"><span data-stu-id="42bdc-114">The data admin needs to easily discover the location of customer personal data across various areas of the Azure environment.</span></span>
- <span data-ttu-id="42bdc-115">出現在共用文件和電子郵件通訊中的客戶和員工個人資料必須加以標記，才能協助確保它保持安全。</span><span class="sxs-lookup"><span data-stu-id="42bdc-115">Customer and employee personal data that appears in shared documents and email communications must be labeled to help ensure that it’s kept secure.</span></span>
- <span data-ttu-id="42bdc-116">公司的應用程式開發人員需要一個方法，能夠輕鬆地在其 web 和行動裝置應用程式中搜尋客戶和員工的個人資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-116">The company’s app developers need a way to easily search for customer and employee personal data in their web and mobile apps.</span></span>
- <span data-ttu-id="42bdc-117">開發人員也需要查詢其文件資料庫來取得個人資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-117">Developers also need to query their document database for personal data.</span></span>

### <a name="company-goals"></a><span data-ttu-id="42bdc-118">公司目標</span><span class="sxs-lookup"><span data-stu-id="42bdc-118">Company goals</span></span>

- <span data-ttu-id="42bdc-119">所有客戶和員工的個人資料必須都已在 Azure 資料目錄中加以標記/標註，以便能夠輕鬆地找到。</span><span class="sxs-lookup"><span data-stu-id="42bdc-119">All customer and employee personal data must be tagged/annotated in Azure Data Catalog so it can be found easily.</span></span> <span data-ttu-id="42bdc-120">在理想情況下，客戶和員工的個人資料會分開標記/標註。</span><span class="sxs-lookup"><span data-stu-id="42bdc-120">Ideally customer and employee personal data are tagged/annotated separately.</span></span>
- <span data-ttu-id="42bdc-121">必須能夠輕鬆地從位於 Azure Active Directory 中的客戶和員工使用者設定檔和工作資訊找到個人資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-121">Personal data from customer and employee user profiles and work information residing in Azure Active Directory must be easily located.</span></span>
- <span data-ttu-id="42bdc-122">必須能夠輕鬆地查詢位在多個 SQL Database 中的個人資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-122">Personal data residing in multiple SQL databases must be easily queried.</span></span> 
- <span data-ttu-id="42bdc-123">某些公司的大型資料集是透過 Azure HDInsight 進行管理，並儲存在 Hadoop 中。</span><span class="sxs-lookup"><span data-stu-id="42bdc-123">Some of the company’s large data sets are managed through Azure HDInsight and stored in Hadoop.</span></span> <span data-ttu-id="42bdc-124">必須將這些資料集匯入 Excel 中，以便可以查詢個人資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-124">They must be imported into Excel so they can be queried for personal data.</span></span>
- <span data-ttu-id="42bdc-125">在文件及電子郵件通訊中共用的個人資料必須加以分類、標記，並使用 Azure 資訊保護來保持安全。</span><span class="sxs-lookup"><span data-stu-id="42bdc-125">Personal data shared in documents and email communications must be classified, labeled, and kept secure with Azure Information Protection.</span></span>
- <span data-ttu-id="42bdc-126">公司的應用程式開發人員必須能夠在他們所建立的應用程式中探索客戶和員工的個人資料，而他們可以使用 Azure 搜尋服務來進行。</span><span class="sxs-lookup"><span data-stu-id="42bdc-126">The company’s app developers must be able to discover customer and employee personal data in the apps they’ve built, which they can do with Azure Search.</span></span>
- <span data-ttu-id="42bdc-127">開發人員必須能夠在其文件資料庫中尋找個人資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-127">Developers must be able to find personal data in their document database.</span></span>

## <a name="azure-active-directory-data-discovery"></a><span data-ttu-id="42bdc-128">Azure Active Directory：資料探索</span><span class="sxs-lookup"><span data-stu-id="42bdc-128">Azure Active Directory: Data discovery</span></span>

<span data-ttu-id="42bdc-129">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 是 Microsoft 的雲端式、多租用戶目錄和身分識別管理服務。</span><span class="sxs-lookup"><span data-stu-id="42bdc-129">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span> <span data-ttu-id="42bdc-130">您可以使用 [Azure 入口網站](https://portal.azure.com/)來找出客戶和員工的使用者設定檔，以及包含 [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) 環境中個人資料的使用者工作資訊。</span><span class="sxs-lookup"><span data-stu-id="42bdc-130">You can locate customer and employee user profiles and user work information that contain personal data in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="42bdc-131">如果您需要尋找或變更特定使用者的個人資料，這對您會特別有用。</span><span class="sxs-lookup"><span data-stu-id="42bdc-131">This is particularly helpful if you want to find or change personal data for a specific user.</span></span> <span data-ttu-id="42bdc-132">您也可以新增或變更使用者設定檔及工作資訊。</span><span class="sxs-lookup"><span data-stu-id="42bdc-132">You can also add or change user profile and work information.</span></span> <span data-ttu-id="42bdc-133">您必須使用具備目錄全域管理員身分的帳戶來登入。</span><span class="sxs-lookup"><span data-stu-id="42bdc-133">You must sign in with an account that’s a global admin for the directory.</span></span>

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a><span data-ttu-id="42bdc-134">如何找出或檢視使用者設定檔和工作資訊？</span><span class="sxs-lookup"><span data-stu-id="42bdc-134">How do I locate or view user profile and work information?</span></span>

1. <span data-ttu-id="42bdc-135">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="42bdc-135">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="42bdc-136">選取 [更多服務]，在文字方塊中輸入「使用者和群組」，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="42bdc-136">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![如何找出使用者設定檔和工作資訊](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. <span data-ttu-id="42bdc-138">在 [使用者和群組] 刀鋒視窗上，選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="42bdc-138">On the **Users and groups** blade, select **Users**.</span></span>

  ![開啟使用者和群組](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. <span data-ttu-id="42bdc-140">在 [使用者和群組 - 使用者] 刀鋒視窗中，從清單選取使用者，然後在選取的使用者之刀鋒視窗上，選取 [設定檔] 以檢視可能包含個人資料的使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="42bdc-140">On the **Users and groups - Users** blade, select a user from the list, and then, on the blade for the selected user, select **Profile** to view user profile information that might contain personal data.</span></span>

  ![選取使用者](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. <span data-ttu-id="42bdc-142">如果您要新增或變更使用者設定檔資訊，可以這麼做，然後在命令列中選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="42bdc-142">If you need to add or change user profile information, you can do so, and then, in the command bar, select **Save.**</span></span>
6. <span data-ttu-id="42bdc-143">在選取的使用者之刀鋒視窗上，選取 [工作資訊] 來檢視可能包含個人資料的使用者工作資訊。</span><span class="sxs-lookup"><span data-stu-id="42bdc-143">On the blade for the selected user, select **Work Info** to view user work information that may contain personal data.</span></span>

 ![檢視工作資訊](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. <span data-ttu-id="42bdc-145">如果您要新增或變更使用者工作資訊，可以這麼做，然後在命令列中選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="42bdc-145">If you need to add or change user work information, you can do so, and then, in the command bar, select **Save.**</span></span>

## <a name="azure-sql-database-data-discovery"></a><span data-ttu-id="42bdc-146">Azure SQL Database：資料探索</span><span class="sxs-lookup"><span data-stu-id="42bdc-146">Azure SQL Database: Data discovery</span></span>

<span data-ttu-id="42bdc-147">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 是雲端資料庫，可協助開發人員建置及維護應用程式。</span><span class="sxs-lookup"><span data-stu-id="42bdc-147">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span> <span data-ttu-id="42bdc-148">您可以使用標準 SQL 查詢在 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 中找到個人資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-148">Personal data can be found in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries.</span></span> <span data-ttu-id="42bdc-149">Azure SQL 彈性查詢 (預覽) 可讓使用者執行跨資料庫查詢。</span><span class="sxs-lookup"><span data-stu-id="42bdc-149">Azure SQL elastic query (preview) enables users to perform cross-database queries.</span></span>

<span data-ttu-id="42bdc-150">[SQL Database](../sql-database/sql-database-technical-overview.md) 的詳細教學課程會說明多個使用 SQL 資料庫的層面，包括如何建置 SQL Database 以及如何執行資料查詢。</span><span class="sxs-lookup"><span data-stu-id="42bdc-150">A detailed [SQL database](../sql-database/sql-database-technical-overview.md) tutorial explains many aspects of using a SQL database, including how to build one and how to run data queries.</span></span> <span data-ttu-id="42bdc-151">以下摘要是教學課程中的可用資訊，以及特定章節的連結。</span><span class="sxs-lookup"><span data-stu-id="42bdc-151">The following is a summary of the information available in the tutorial with links to specific sections.</span></span>

### <a name="how-do-i-build-a-sql-database"></a><span data-ttu-id="42bdc-152">如何建置 SQL Database？</span><span class="sxs-lookup"><span data-stu-id="42bdc-152">How do I build a SQL database?</span></span>

<span data-ttu-id="42bdc-153">有三種方式可以完成：</span><span class="sxs-lookup"><span data-stu-id="42bdc-153">There are three ways to do it:</span></span>

- <span data-ttu-id="42bdc-154">您可以在 [Azure 入口網站](https://portal.azure.com/)中建立 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="42bdc-154">An Azure SQL database can be created in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="42bdc-155">在本教學課程中，您將使用資源群組和邏輯伺服器內的一組特定運算及儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="42bdc-155">In the tutorial, you’ll use a specific set of compute and storage resources within a resource group and logical server.</span></span> <span data-ttu-id="42bdc-156">您會使用名為 AdventureWorks 的虛構公司之範例資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-156">You’ll use sample data from a fictitious company called AdventureWorks.</span></span> <span data-ttu-id="42bdc-157">您還會建立伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="42bdc-157">You’ll also create a server-level firewall rule.</span></span> <span data-ttu-id="42bdc-158">若要了解如何執行這項操作，請造訪[在 Azure 入口網站中建立 Azure SQL Database](../sql-database/sql-database-get-started-portal.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="42bdc-158">To learn how to do this, visit the [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md) tutorial.</span></span>

  ![建立 Azure SQL Database](media/how-to-discover-classify-personal-data-azure/create-database.png)
- <span data-ttu-id="42bdc-160">您也可以在 [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) CLI 中建立 SQL Database，這是以瀏覽器為基礎的命令列工具。</span><span class="sxs-lookup"><span data-stu-id="42bdc-160">A SQL database can also be created in the [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) CLI, a browser-based command-line tool.</span></span> <span data-ttu-id="42bdc-161">此工具可在 Azure 入口網站中使用，且可以直接從該處執行。</span><span class="sxs-lookup"><span data-stu-id="42bdc-161">The tool is available in the Azure portal and can be run directly from there.</span></span> <span data-ttu-id="42bdc-162">在本教學課程中，您要啟動工具、定義指令碼變數、建立資源群組和邏輯伺服器，並設定伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="42bdc-162">In this tutorial, you launch the tool, define script variables, create a resource group and logical server, and configure a server firewall rule.</span></span> <span data-ttu-id="42bdc-163">然後使用範例資料建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="42bdc-163">Then you create a database with sample data.</span></span> <span data-ttu-id="42bdc-164">若要了解如何以這種方式建立您的資料庫，請造訪[使用 Azure CLI 建立單一 Azure SQL Database](../sql-database/sql-database-get-started-cli.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="42bdc-164">To learn how to create your database this way, visit the [Create a single Azure SQL database using the Azure CLI](../sql-database/sql-database-get-started-cli.md) tutorial.</span></span>

  ![CLI 教學課程](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
<span data-ttu-id="42bdc-166">Linux 系統管理員和開發人員通常都是使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="42bdc-166">Azure CLI is commonly used by Linux admins and developers.</span></span> <span data-ttu-id="42bdc-167">某些使用者認為它比 PowerShell (這是您的第三個選項) 更簡單且更直覺。</span><span class="sxs-lookup"><span data-stu-id="42bdc-167">Some users find it easier and more intuitive than PowerShell, which is your third option.</span></span>

- <span data-ttu-id="42bdc-168">最後，您可以使用 PowerShell 來建立 SQL Database，它是用來建立及管理 Azure 和其他資源的命令列/指令碼工具。</span><span class="sxs-lookup"><span data-stu-id="42bdc-168">Finally, you can create a SQL database using PowerShell, which is a command line/script tool used to create and manage Azure and other resources.</span></span> <span data-ttu-id="42bdc-169">在本教學課程中，您要啟動工具、定義指令碼變數、建立資源群組和邏輯伺服器，並設定伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="42bdc-169">In this tutorial, you launch the tool, define script variables, create a resource group and logical server, and configure a server firewall rule.</span></span> <span data-ttu-id="42bdc-170">然後使用範例資料建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="42bdc-170">Then you’ll create a database with sample data.</span></span>

<span data-ttu-id="42bdc-171">本教學課程需要 Azure PowerShell 模組 4.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="42bdc-171">The tutorial requires the Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="42bdc-172">執行 Get-Module -ListAvailable AzureRM 來尋找您的版本。</span><span class="sxs-lookup"><span data-stu-id="42bdc-172">Run  Get-Module -ListAvailable AzureRM to find your version.</span></span> <span data-ttu-id="42bdc-173">如果您需要安裝或升級，請參閱安裝 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="42bdc-173">If you need to install or upgrade, see Install Azure PowerShell module.</span></span>

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

<span data-ttu-id="42bdc-174">若要了解如何以這種方式建立您的資料庫，請造訪[使用 PowerShell 建立單一 Azure SQL Database](../sql-database/sql-database-get-started-powershell.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="42bdc-174">To learn how to create your database this way, visit the [Create a single Azure SQL database using Powershell](../sql-database/sql-database-get-started-powershell.md) tutorial.</span></span>

>[!Note]
<span data-ttu-id="42bdc-175">Windows 系統管理員通常會使用 PowerShell，但有些則偏好使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="42bdc-175">Windows admins tend to use PowerShell, but some of them prefer Azure CLI.</span></span>

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-the-azure-portal"></a><span data-ttu-id="42bdc-176">如何在 Azure 入口網站中搜尋 SQL Database 中的個人資料？**</span><span class="sxs-lookup"><span data-stu-id="42bdc-176">How do I search for personal data in SQL database in the Azure portal?**</span></span>

<span data-ttu-id="42bdc-177">您可以使用 Azure 入口網站內部的內建查詢編輯器工具來搜尋個人資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-177">You can use the built-in query editor tool inside the Azure portal to search for personal data.</span></span> <span data-ttu-id="42bdc-178">您要使用 SQL Server 系統管理員登入和密碼來登入工具，然後輸入查詢。</span><span class="sxs-lookup"><span data-stu-id="42bdc-178">You’ll log in to the tool using your SQL server admin login and password, and then enter a query.</span></span>

  ![使用入口網站搜尋 SQL](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

<span data-ttu-id="42bdc-180">本教學課程的步驟 5 會在查詢編輯器窗格中顯示一個範例查詢，但它不會著重於個人或機密資訊 (它還會結合來自兩個資料表的資料，並在傳回的資料集中建立來源資料行的別名)。</span><span class="sxs-lookup"><span data-stu-id="42bdc-180">Step 5 of the tutorial shows an example query in the query editor pane, but it  doesn’t focus on personal or sensitive information(it also combines data from two tables and creates aliases for the source column in the data set being returned).</span></span> <span data-ttu-id="42bdc-181">下列螢幕擷取畫面會顯示步驟 5 的查詢，以及傳回的結果窗格：</span><span class="sxs-lookup"><span data-stu-id="42bdc-181">The following screenshot shows the query from Step 5 as well as the results pane that’s returned:</span></span>

  ![查詢編輯器](media/how-to-discover-classify-personal-data-azure/query-editor.png)

<span data-ttu-id="42bdc-183">如果您的資料庫稱為 MyTable，個人資訊的範例查詢可能就會包括名稱、社會安全號碼和識別碼，且會看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="42bdc-183">If your database was called MyTable, a sample query for personal information might include name, Social Security number and ID number and would look like this:</span></span>

<span data-ttu-id="42bdc-184">「選取名稱、社會安全號碼、MyTable 的識別碼」</span><span class="sxs-lookup"><span data-stu-id="42bdc-184">“SELECT Name, SSN, ID number FROM MyTable”</span></span>

<span data-ttu-id="42bdc-185">您要執行查詢，然後在 [結果] 窗格中查看查詢結果。</span><span class="sxs-lookup"><span data-stu-id="42bdc-185">You’d run the query and then see the results in the **Results** pane.</span></span>

<span data-ttu-id="42bdc-186">如需有關在 Azure 入口網站中如何查詢 SQL Database 的詳細資訊，請瀏覽教學課程的[查詢 SQL Database](../sql-database/sql-database-get-started-portal.md) 一節。</span><span class="sxs-lookup"><span data-stu-id="42bdc-186">For more information on how to query a SQL database in the Azure portal, visit the [Query the SQL database](../sql-database/sql-database-get-started-portal.md) section of the tutorial.</span></span>

### <a name="how-do-i-search-for-data-across-multiple-databases"></a><span data-ttu-id="42bdc-187">如何跨多個資料庫搜尋資料？</span><span class="sxs-lookup"><span data-stu-id="42bdc-187">How do I search for data across multiple databases?</span></span>

<span data-ttu-id="42bdc-188">SQL 彈性查詢 (預覽) 可讓您執行跨資料庫和多個資料庫的查詢，並傳回單一結果。</span><span class="sxs-lookup"><span data-stu-id="42bdc-188">SQL elastic query (preview) enables you to perform cross-database and multiple database queries and return a single result.</span></span> <span data-ttu-id="42bdc-189">[教學課程概觀](../sql-database/sql-database-elastic-query-overview.md)包含情節的詳細描述，並說明垂直和水平資料庫資料分割之間的差異。</span><span class="sxs-lookup"><span data-stu-id="42bdc-189">The [tutorial overview](../sql-database/sql-database-elastic-query-overview.md) includes a detailed description of scenarios and explains the difference between vertical and horizontal database partitioning.</span></span> <span data-ttu-id="42bdc-190">水平資料分割稱為「分區化」。</span><span class="sxs-lookup"><span data-stu-id="42bdc-190">Horizontal partitioning is called “sharding.”</span></span>

  ![垂直資料分割](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![水平資料分割](media/how-to-discover-classify-personal-data-azure/horizontal.png)

<span data-ttu-id="42bdc-193">若要開始使用，請造訪 [Azure SQL Database 彈性查詢概觀 (預覽)](../sql-database/sql-database-elastic-query-overview.md) 頁面。</span><span class="sxs-lookup"><span data-stu-id="42bdc-193">To get started, visit the [Azure SQL Database elastic query overview (preview)](../sql-database/sql-database-elastic-query-overview.md) page.</span></span>

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a><span data-ttu-id="42bdc-194">Power Query (適用於匯入 Azure HDInsight Hadoop 叢集)：大型資料集的資料探索</span><span class="sxs-lookup"><span data-stu-id="42bdc-194">Power Query (for importing Azure HDInsight Hadoop clusters): data discovery for large data sets</span></span>

<span data-ttu-id="42bdc-195">Hadoop 是開放原始碼 Apache 儲存體和大型資料集的處理服務，會在 Hadoop 叢集中進行分析並加以儲存。</span><span class="sxs-lookup"><span data-stu-id="42bdc-195">Hadoop is an open source Apache storage and processing service for large data sets, which are analyzed and stored in Hadoop clusters.</span></span> <span data-ttu-id="42bdc-196">[Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) 可讓使用者在 Azure 中使用 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="42bdc-196">[Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) allows users to work with Hadoop clusters in Azure.</span></span> <span data-ttu-id="42bdc-197">Power Query 是 Excel 增益集，除此之外，還可協助使用者從不同的來源探索資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-197">Power Query is an Excel add-in that, among other things, helps users discover data from different sources.</span></span>

<span data-ttu-id="42bdc-198">與 Azure HDInsight 中的 Hadoop 叢集相關聯之個人資料，都可以使用 Power Query 匯入 Excel 中。</span><span class="sxs-lookup"><span data-stu-id="42bdc-198">Personal data associated with Hadoop clusters in Azure HDInsight can be imported to Excel with Power Query.</span></span> <span data-ttu-id="42bdc-199">一旦資料在 Excel 中，您就可以使用查詢來識別它。</span><span class="sxs-lookup"><span data-stu-id="42bdc-199">Once the data is in Excel you can use a query to identify it.</span></span>

#### <a name="how-do-i-use-excel-power-query-to-import-hadoop-clusters-in-azure-hdinsight-into-excel"></a><span data-ttu-id="42bdc-200">如何使用 Excel Power Query 將 Azure HDInsight 中的 Hadoop 叢集匯入 Excel 中？</span><span class="sxs-lookup"><span data-stu-id="42bdc-200">How do I use Excel Power Query to import Hadoop clusters in Azure HDInsight into Excel?</span></span>

<span data-ttu-id="42bdc-201">HDInsight 教學課程將引導您完成這整個程序。</span><span class="sxs-lookup"><span data-stu-id="42bdc-201">An HDInsight tutorial will walk you through this entire process.</span></span> <span data-ttu-id="42bdc-202">它會說明必要條件，並包含[開始使用 Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) 教學課程的連結。</span><span class="sxs-lookup"><span data-stu-id="42bdc-202">It explains prerequisites, and includes a link to a [Get started with Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) tutorial.</span></span> <span data-ttu-id="42bdc-203">指示涵蓋 Excel 2016 以及 2013 和 2010 (舊版本 Excel 的步驟會稍有不同)。</span><span class="sxs-lookup"><span data-stu-id="42bdc-203">Instructions cover Excel 2016 as well as 2013 and 2010 (steps are slightly different for the older versions of Excel).</span></span> <span data-ttu-id="42bdc-204">如果您沒有 Excel Power Query 增益集，本教學課程會告訴您如何完成設定。</span><span class="sxs-lookup"><span data-stu-id="42bdc-204">If you don’t have the Excel Power Query add-in, the tutorial shows you how to get it.</span></span> <span data-ttu-id="42bdc-205">您會在 Excel 中開始教學課程，且必須具有與您叢集相關聯的 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="42bdc-205">You’ll start the tutorial in Excel and will need to have an Azure Blob storage account associated with your cluster.</span></span>

  ![在 Excel 中的查詢](media/how-to-discover-classify-personal-data-azure/excel.png)

<span data-ttu-id="42bdc-207">若要了解如何執行這項操作，請造訪[使用 Power Query 將 Excel 連線到 Hadoop](../hdinsight/hdinsight-connect-excel-power-query.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="42bdc-207">To learn how to do this, visit the [Connect Excel to Hadoop by using Power Query](../hdinsight/hdinsight-connect-excel-power-query.md) tutorial.</span></span>

<span data-ttu-id="42bdc-208">來源：[使用 Power Query 將 Excel 連線到 Hadoop](../hdinsight/hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="42bdc-208">Source: [Connect Excel to Hadoop by using Power Query](../hdinsight/hdinsight-connect-excel-power-query.md)</span></span>

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a><span data-ttu-id="42bdc-209">Azure 資訊保護：文件和電子郵件的個人資料分類</span><span class="sxs-lookup"><span data-stu-id="42bdc-209">Azure Information Protection: personal data classification for documents and email</span></span>

<span data-ttu-id="42bdc-210">[Azure 資訊保護](https://www.microsoft.com/cloud-platform/azure-information-protection)可以協助 Azure 客戶套用標籤，將內部或外部共用的文件與電子郵件通訊加以分類及保護。</span><span class="sxs-lookup"><span data-stu-id="42bdc-210">[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) can help Azure customers apply labels to classify and protect internally or externally shared documents and email communications.</span></span> <span data-ttu-id="42bdc-211">這些項目有些可能會包含客戶或員工的個人資訊。</span><span class="sxs-lookup"><span data-stu-id="42bdc-211">Some of these items may contain customer or employee personal information.</span></span> <span data-ttu-id="42bdc-212">系統管理員或使用者可以自動或手動方式定義規則和條件。</span><span class="sxs-lookup"><span data-stu-id="42bdc-212">Rules and conditions can be defined automatically or manually, by administrators or by users.</span></span> <span data-ttu-id="42bdc-213">例如，如果使用者所要儲存的文件包含信用卡資訊，就會看到系統管理員已設定的標籤建議。</span><span class="sxs-lookup"><span data-stu-id="42bdc-213">For example, if a user is saving a document that includes credit card information, he or she would see a label recommendation that was configured by the administrator.</span></span>

### <a name="how-do-i-try-it"></a><span data-ttu-id="42bdc-214">如何嘗試？</span><span class="sxs-lookup"><span data-stu-id="42bdc-214">How do I try it?</span></span>

<span data-ttu-id="42bdc-215">如果您需要讓 Azure 資訊保護嘗試查看它是否適合貴組織，請瀏覽[快速入門教學課程](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial)。</span><span class="sxs-lookup"><span data-stu-id="42bdc-215">If you’d like to give Azure Information Protection a try to see if it might be a fit for your organization, visit the [Quickstart tutorial](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial).</span></span> <span data-ttu-id="42bdc-216">會引導您執行五個基本步驟 — 從安裝到設定原則、查看動作中的分類、標籤和共用 — 且花費時間不超過一小時。</span><span class="sxs-lookup"><span data-stu-id="42bdc-216">It walks you through five basic steps—from installation to configuring policy to seeing classification, labeling, and sharing in action—and should take less than a half hour.</span></span>

### <a name="how-do-i-deploy-it"></a><span data-ttu-id="42bdc-217">如何進行部署？</span><span class="sxs-lookup"><span data-stu-id="42bdc-217">How do I deploy it?</span></span>

<span data-ttu-id="42bdc-218">如果您需要為貴組織部署 Azure 資訊保護，請瀏覽[分類、標籤和保護的部署藍圖](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap)。</span><span class="sxs-lookup"><span data-stu-id="42bdc-218">If you’d like to deploy Azure Information Protection for your organization, visit the [deployment roadmap for classification, labeling, and protection](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).</span></span>

### <a name="is-there-anything-else-i-should-know"></a><span data-ttu-id="42bdc-219">還有其他須知事項嗎？</span><span class="sxs-lookup"><span data-stu-id="42bdc-219">Is there anything else I should know?</span></span>

<span data-ttu-id="42bdc-220">如需能協助您思考設定方式的補充資訊，請造訪[就緒、設定、保護！](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)</span><span class="sxs-lookup"><span data-stu-id="42bdc-220">For complementary information that will help you think through how to set it up, visit the [Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)</span></span>
<span data-ttu-id="42bdc-221">部落格文章。</span><span class="sxs-lookup"><span data-stu-id="42bdc-221">blog post.</span></span> <span data-ttu-id="42bdc-222">如需有關 Azure 資訊保護的詳細資訊，請檢查下列的深入了解連結。</span><span class="sxs-lookup"><span data-stu-id="42bdc-222">And check the Learn more links listed below for more on Azure Information Protection.</span></span>

## <a name="azure-search-data-discovery-for-developer-apps"></a><span data-ttu-id="42bdc-223">Azure 搜尋服務：開發人員應用程式的資料探索</span><span class="sxs-lookup"><span data-stu-id="42bdc-223">Azure Search: data discovery for developer apps</span></span>

<span data-ttu-id="42bdc-224">[Azure 搜尋服務](https://azure.microsoft.com/services/search/)是開發人員的雲端搜尋解決方案，可為您的應用程式提供豐富的資料搜尋體驗。</span><span class="sxs-lookup"><span data-stu-id="42bdc-224">[Azure Search](https://azure.microsoft.com/services/search/) is a cloud search solution for developers, and provides a rich data search experience for your applications.</span></span> <span data-ttu-id="42bdc-225">Azure 搜尋服務可讓您在使用者定義的索引中找出資料、源自 Azure Cosmo DB、Azure SQL Database、Azure Blob 儲存體、Azure 資料表儲存體或自訂客戶 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-225">Azure Search allows you to locate data across user-defined indexes, sourced from Azure Cosmo DB, Azure SQL Database, Azure Blob Storage, Azure Table storage, or custom customer JSON data.</span></span> <span data-ttu-id="42bdc-226">您也可以使用 Azure 搜尋服務 REST API 來建構 Lucene 查詢，從而搜尋個人資料類型或特定人員的個人資料。</span><span class="sxs-lookup"><span data-stu-id="42bdc-226">You can also structure Lucene queries using the Azure Search REST API to search for personal data types or the personal data of specific individuals.</span></span> <span data-ttu-id="42bdc-227">功能包括全文檢索搜尋、簡單查詢語法及 Lucene 查詢語法。</span><span class="sxs-lookup"><span data-stu-id="42bdc-227">Features include full text search, simple query syntax, and Lucene query syntax.</span></span> 

## <a name="how-do-i-use-sql-to-query-data"></a><span data-ttu-id="42bdc-228">如何使用 SQL 來查詢資料？</span><span class="sxs-lookup"><span data-stu-id="42bdc-228">How do I use SQL to query data?</span></span>

<span data-ttu-id="42bdc-229">若要開始進行基本概念，請瀏覽 [Azure CosmosD DB：如何使用 SQL 查詢](../cosmos-db/tutorial-query-documentdb.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="42bdc-229">To begin with the basics, visit the [Azure CosmosD DB: How to query using SQL](../cosmos-db/tutorial-query-documentdb.md) tutorial.</span></span> <span data-ttu-id="42bdc-230">本教學課程提供一個範例文件及兩個範例 SQL 查詢和結果。</span><span class="sxs-lookup"><span data-stu-id="42bdc-230">The tutorial provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="42bdc-231">如需有關建置 SQL 查詢的詳細指引，請瀏覽 [Azure Cosmos DB 文件 DB API 的 SQL 查詢。](../cosmos-db/documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="42bdc-231">For more in-depth guidance on building SQL queries, visit [SQL queries for Azure Cosmos DB Document DB API.](../cosmos-db/documentdb-sql-query.md)</span></span>

<span data-ttu-id="42bdc-232">如果您還不熟悉 Azure Cosmos DB 且需要了解如何建立資料庫、新增集合及新增資料，請瀏覽 [Azure Cosmos DB：建置 DocumentDB API 的 web 應用程式](../cosmos-db/create-documentdb-dotnet.md)快速入門教學課程。</span><span class="sxs-lookup"><span data-stu-id="42bdc-232">If you’re new to Azure Cosmos DB and would like to learn how to create a database, add a collection, and add data, visit the [Azure Cosmos DB: Build a DocumentDB API web app](../cosmos-db/create-documentdb-dotnet.md) Quickstart tutorial.</span></span> <span data-ttu-id="42bdc-233">如果您需要使用 .NET 以外的語言 (例如 JAVA 或 Python) 來執行這項操作，在您進入站台後，只要選擇您慣用的語言即可。</span><span class="sxs-lookup"><span data-stu-id="42bdc-233">If you’d like to do this in a language other than .NET, such as Java or Python, just choose your preferred language once you get to the site.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42bdc-234">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42bdc-234">Next steps</span></span>

[<span data-ttu-id="42bdc-235">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="42bdc-235">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50)

[<span data-ttu-id="42bdc-236">什麼是 SQL Database？</span><span class="sxs-lookup"><span data-stu-id="42bdc-236">What is SQL Database?</span></span>](../sql-database/sql-database-technical-overview.md)

<span data-ttu-id="42bdc-237">[Azure 入口網站中可用的 SQL Database 查詢編輯器] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)</span><span class="sxs-lookup"><span data-stu-id="42bdc-237">[SQL Database Query Editor available in Azure portal] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)</span></span>

[<span data-ttu-id="42bdc-238">什麼是 Azure 資訊保護？</span><span class="sxs-lookup"><span data-stu-id="42bdc-238">What is Azure Information Protection?</span></span>](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[<span data-ttu-id="42bdc-239">什麼是 Azure Rights Management？</span><span class="sxs-lookup"><span data-stu-id="42bdc-239">What is Azure Rights Management?</span></span>](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[<span data-ttu-id="42bdc-240">Azure 資訊保護：就緒、設定、保護！</span><span class="sxs-lookup"><span data-stu-id="42bdc-240">Azure Information Protection: Ready, set, protect!</span></span>](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
