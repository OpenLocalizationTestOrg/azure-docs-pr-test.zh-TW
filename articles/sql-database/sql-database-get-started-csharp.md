---
title: "C#：開始使用 Azure SQL Database | Microsoft Docs"
description: "嘗試用 SQL Database 開發 SQL 和 C# 應用程式，然後使用 SQL Database Library for .NET 以 C# 建立 Azure SQL Database。"
keywords: "試用 sql、sql c#"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: cfff2299-a474-4054-8d99-759af1ae5188
ms.service: sql-database
ms.custom: develop apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: csharp
ms.workload: data-management
ms.date: 10/04/2016
ms.author: sstein
ms.openlocfilehash: c8a2703da1ee3687f8d134e768dd8d31dc4f316b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-c-to-create-a-sql-database-with-the-sql-database-library-for-net"></a><span data-ttu-id="b87b9-104">以 SQL Database Library for .NET 使用 C# 建立 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="b87b9-104">Use C# to create a SQL database with the SQL Database Library for .NET</span></span>

<span data-ttu-id="b87b9-105">了解如何使用 C# 透過 [Microsoft Azure SQL Management Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql) 建立 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="b87b9-105">Learn how to use C# to create an Azure SQL database with the [Microsoft Azure SQL Management Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span> <span data-ttu-id="b87b9-106">本文說明如何使用 SQL 和 C# 建立單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="b87b9-106">This article describes how to create a single database with SQL and C#.</span></span> <span data-ttu-id="b87b9-107">若要建立彈性集區，請參閱 [建立彈性集區](sql-database-elastic-pool-manage-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="b87b9-107">To create elastic pools, see [Create an elastic pool](sql-database-elastic-pool-manage-csharp.md).</span></span>

<span data-ttu-id="b87b9-108">Azure SQL Database Management Library for .NET 提供 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 式 API，它會包裝 [Resource Manager 式 SQL Database REST API](https://docs.microsoft.com/rest/api/sql/)。</span><span class="sxs-lookup"><span data-stu-id="b87b9-108">The Azure SQL Database Management Library for .NET provides an [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-based API that wraps the [Resource Manager-based SQL Database REST API](https://docs.microsoft.com/rest/api/sql/).</span></span>

> [!NOTE]
> <span data-ttu-id="b87b9-109">SQL Database 的許多新功能只有在使用 [Azure Resource Manager 部署模型](../azure-resource-manager/resource-group-overview.md)時才支援，所以您應該一律使用最新的**適用於 .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet Package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)) 的 Azure SQL Database Management Library**。</span><span class="sxs-lookup"><span data-stu-id="b87b9-109">Many new features of SQL Database are only supported when you are using the [Azure Resource Manager deployment model](../azure-resource-manager/resource-group-overview.md), so you should always use the latest **Azure SQL Database Management Library for .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet Package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span></span> <span data-ttu-id="b87b9-110">支援較舊的[以傳統部署模型為基礎的程式庫](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql)，以提供回溯相容性，因此我們建議您使用較新的以 Resource Manager 為基礎的程式庫。</span><span class="sxs-lookup"><span data-stu-id="b87b9-110">The older [classic deployment model based libraries](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) are supported for backward compatibility only, so we recommend you use the newer Resource Manager based libraries.</span></span>
> 
> 

<span data-ttu-id="b87b9-111">若要完成這篇文章中的步驟，您需要下列項目︰</span><span class="sxs-lookup"><span data-stu-id="b87b9-111">To complete the steps in this article, you need the following:</span></span>

* <span data-ttu-id="b87b9-112">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b87b9-112">An Azure subscription.</span></span> <span data-ttu-id="b87b9-113">如果需要 Azure 訂用帳戶，可以先按一下此頁面頂端的 [免費帳戶]  ，然後再回來完成這篇文章。</span><span class="sxs-lookup"><span data-stu-id="b87b9-113">If you need an Azure subscription simply click **FREE ACCOUNT** at the top of this page, and then come back to finish this article.</span></span>
* <span data-ttu-id="b87b9-114">Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b87b9-114">Visual Studio.</span></span> <span data-ttu-id="b87b9-115">如需免費的 Visual Studio，請參閱 [Visual Studio 下載](https://www.visualstudio.com/downloads/download-visual-studio-vs) 頁面。</span><span class="sxs-lookup"><span data-stu-id="b87b9-115">For a free copy of Visual Studio, see the [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) page.</span></span>

> [!NOTE]
> <span data-ttu-id="b87b9-116">本文會建立一個新的空白 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="b87b9-116">This article creates a new, blank SQL database.</span></span> <span data-ttu-id="b87b9-117">在下列範例中修改 *CreateOrUpdateDatabase(...)* 方法，以複製資料庫、調整資料庫大小、在集區中建立資料庫等等。</span><span class="sxs-lookup"><span data-stu-id="b87b9-117">Modify the *CreateOrUpdateDatabase(...)* method in the following sample to copy databases, scale databases, create a database in a pool, etc.</span></span>  
> 

## <a name="create-a-console-app-and-install-the-required-libraries"></a><span data-ttu-id="b87b9-118">建立主控台應用程式並安裝必要的程式庫</span><span class="sxs-lookup"><span data-stu-id="b87b9-118">Create a console app and install the required libraries</span></span>
1. <span data-ttu-id="b87b9-119">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b87b9-119">Start Visual Studio.</span></span>
2. <span data-ttu-id="b87b9-120">按一下 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="b87b9-120">Click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="b87b9-121">建立 C# **主控台應用程式** 並將其命名為︰ *SqlDbConsoleApp*</span><span class="sxs-lookup"><span data-stu-id="b87b9-121">Create a C# **Console Application** and name it: *SqlDbConsoleApp*</span></span>

<span data-ttu-id="b87b9-122">若要使用 C# 建立 SQL Database，請載入必要的管理程式庫 (使用 [封裝管理員主控台](http://docs.nuget.org/Consume/Package-Manager-Console))：</span><span class="sxs-lookup"><span data-stu-id="b87b9-122">To create a SQL database with C#, load the required management libraries (using the [package manager console](http://docs.nuget.org/Consume/Package-Manager-Console)):</span></span>

1. <span data-ttu-id="b87b9-123">按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="b87b9-123">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="b87b9-124">輸入 `Install-Package Microsoft.Azure.Management.Sql -Pre` 以安裝最新的 [Microsoft Azure SQL 管理程式庫](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)。</span><span class="sxs-lookup"><span data-stu-id="b87b9-124">Type `Install-Package Microsoft.Azure.Management.Sql -Pre` to install the latest [Microsoft Azure SQL Management Library](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span>
3. <span data-ttu-id="b87b9-125">輸入 `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` 以安裝 [Microsoft Azure Resource Manager 程式庫](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)。</span><span class="sxs-lookup"><span data-stu-id="b87b9-125">Type `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` to install the [Microsoft Azure Resource Manager Library](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span></span>
4. <span data-ttu-id="b87b9-126">輸入 `Install-Package Microsoft.Azure.Common.Authentication -Pre` 以安裝 [Microsoft Azure 通用驗證程式庫](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication)。</span><span class="sxs-lookup"><span data-stu-id="b87b9-126">Type `Install-Package Microsoft.Azure.Common.Authentication -Pre` to install the [Microsoft Azure Common Authentication Library](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span></span> 

> [!NOTE]
> <span data-ttu-id="b87b9-127">這篇文章中的範例使用每個 API 要求的同步表單，並且封鎖直到基礎服務上的 REST 呼叫完成。</span><span class="sxs-lookup"><span data-stu-id="b87b9-127">The examples in this article use a synchronous form of each API request and block until completion of the REST call on the underlying service.</span></span> <span data-ttu-id="b87b9-128">有可用的非同步方法。</span><span class="sxs-lookup"><span data-stu-id="b87b9-128">There are async methods available.</span></span>
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a><span data-ttu-id="b87b9-129">建立 SQL Database 伺服器、防火牆規則和 SQL Database - C# 範例</span><span class="sxs-lookup"><span data-stu-id="b87b9-129">Create a SQL Database server, firewall rule, and SQL database - C# example</span></span>
<span data-ttu-id="b87b9-130">下列範例會建立資源群組、伺服器、防火牆規則和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="b87b9-130">The following sample creates a resource group, server, firewall rule, and a SQL database.</span></span> <span data-ttu-id="b87b9-131">請參閱[建立用來存取資源的服務主體](#create-a-service-principal-to-access-resources)以取得 `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` 變數。</span><span class="sxs-lookup"><span data-stu-id="b87b9-131">See, [Create a service principal to access resources](#create-a-service-principal-to-access-resources) to get the `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variables.</span></span>

<span data-ttu-id="b87b9-132">以下列內容取代 **Program.cs** 的內容，並以您應用程式的值更新 `{variables}` (請勿包含 `{}`)。</span><span class="sxs-lookup"><span data-stu-id="b87b9-132">Replace the contents of **Program.cs** with the following, and update the `{variables}` with your app values (do not include the `{}`).</span></span>

    using Microsoft.Azure;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Sql;
    using Microsoft.Azure.Management.Sql.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;

    namespace SqlDbConsoleApp
    {
    class Program
       {
        // For details about these four (4) values, see
        // https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal/
        static string _subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _tenantId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationSecret = "{your-password}";

        // Create management clients for the Azure resources your app needs to work with.
        // This app works with Resource Groups, and Azure SQL Database.
        static ResourceManagementClient _resourceMgmtClient;
        static SqlManagementClient _sqlMgmtClient;

        // Authentication token
        static AuthenticationResult _token;

        // Azure resource variables
        static string _resourceGroupName = "{resource-group-name}";
        static string _resourceGrouplocation = "{Azure-region}";

        static string _serverlocation = _resourceGrouplocation;
        static string _serverName = "{server-name}";
        static string _serverAdmin = "{server-admin-login}";
        static string _serverAdminPassword = "{server-admin-password}";

        static string _firewallRuleName = "{firewall-rule-name}";
        static string _startIpAddress = "{0.0.0.0}";
        static string _endIpAddress = "{255.255.255.255}";

        static string _databaseName = "{dbfromcsarticle}";
        static string _databaseEdition = DatabaseEditions.Basic;
        static string _databasePerfLevel = ""; // "S0", "S1", and so on here for other tiers


        static void Main(string[] args)
        {
            // Authenticate:
            _token = GetToken(_tenantId, _applicationId, _applicationSecret);
            Console.WriteLine("Token acquired. Expires on:" + _token.ExpiresOn);

            // Instantiate management clients:
            _resourceMgmtClient = new ResourceManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken));
            _sqlMgmtClient = new SqlManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken)) { SubscriptionId = _subscriptionId };

            Console.WriteLine("Resource group...");
            ResourceGroup rg = CreateOrUpdateResourceGroup(_resourceMgmtClient, _subscriptionId, _resourceGroupName, _resourceGrouplocation);
            Console.WriteLine("Resource group: " + rg.Id);


            Console.WriteLine("Server...");
            Server sgr = CreateOrUpdateServer(_sqlMgmtClient, _resourceGroupName, _serverlocation, _serverName, _serverAdmin, _serverAdminPassword);
            Console.WriteLine("Server: " + sgr.Id);

            Console.WriteLine("Server firewall...");
            FirewallRule fwr = CreateOrUpdateFirewallRule(_sqlMgmtClient, _resourceGroupName, _serverName, _firewallRuleName, _startIpAddress, _endIpAddress);
            Console.WriteLine("Server firewall: " + fwr.Id);

            Console.WriteLine("Database...");
            Database dbr = CreateOrUpdateDatabase(_sqlMgmtClient, _resourceGroupName, _serverName, _databaseName, _databaseEdition, _databasePerfLevel);
            Console.WriteLine("Database: " + dbr.Id);


            Console.WriteLine("Press any key to continue...");
            Console.ReadKey();
        }

        static ResourceGroup CreateOrUpdateResourceGroup(ResourceManagementClient resourceMgmtClient, string subscriptionId, string resourceGroupName, string resourceGroupLocation)
        {
            ResourceGroup resourceGroupParameters = new ResourceGroup()
            {
                Location = resourceGroupLocation,
            };
            resourceMgmtClient.SubscriptionId = subscriptionId;
            ResourceGroup resourceGroupResult = resourceMgmtClient.ResourceGroups.CreateOrUpdate(resourceGroupName, resourceGroupParameters);
            return resourceGroupResult;
        }

        static Server CreateOrUpdateServer(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverLocation, string serverName, string serverAdmin, string serverAdminPassword)
        {
            Server serverParameters = new Server()
            {
                Location = serverLocation,
                AdministratorLogin = serverAdmin,
                AdministratorLoginPassword = serverAdminPassword,
                Version = "12.0"
            };
            Server serverResult = sqlMgmtClient.Servers.CreateOrUpdate(resourceGroupName, serverName, serverParameters);
            return serverResult;
        }

        static FirewallRule CreateOrUpdateFirewallRule(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string firewallRuleName, string startIpAddress, string endIpAddress)
        {
            FirewallRule firewallParameters = new FirewallRule()
            {
                StartIpAddress = startIpAddress,
                EndIpAddress = endIpAddress
            };
            FirewallRule firewallResult = sqlMgmtClient.FirewallRules.CreateOrUpdate(resourceGroupName, serverName, firewallRuleName, firewallParameters);
            return firewallResult;
        }

        static Database CreateOrUpdateDatabase(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string databaseName, string databaseEdition, string databasePerfLevel)
        {
            // Retrieve the server that will host this database
            Server currentServer = sqlMgmtClient.Servers.Get(resourceGroupName, serverName);

            // Create a database: configure create or update parameters and properties explicitly
            Database newDatabaseParameters = new Database()
            {
                Location = currentServer.Location,
                CreateMode = CreateMode.Default,
                Edition = databaseEdition,
                RequestedServiceObjectiveName = databasePerfLevel

            };
            Database dbResponse = sqlMgmtClient.Databases.CreateOrUpdate(resourceGroupName, serverName, databaseName, newDatabaseParameters);
            return dbResponse;
        }



        private static AuthenticationResult GetToken(string tenantId, string applicationId, string applicationSecret)
        {
            AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/" + tenantId);
            _token = authContext.AcquireToken("https://management.core.windows.net/", new ClientCredential(applicationId, applicationSecret));
            return _token;
        }
      }
    }





## <a name="create-a-service-principal-to-access-resources"></a><span data-ttu-id="b87b9-133">建立用來存取資源的服務主體</span><span class="sxs-lookup"><span data-stu-id="b87b9-133">Create a service principal to access resources</span></span>
<span data-ttu-id="b87b9-134">下列 PowerShell 指令碼會建立 Active Directory (AD) 應用程式以及驗證 C# 應用程式所需的服務主體。</span><span class="sxs-lookup"><span data-stu-id="b87b9-134">The following PowerShell script creates the Active Directory (AD) application and the service principal that we need to authenticate our C# app.</span></span> <span data-ttu-id="b87b9-135">指令碼會輸出先前 C# 範例所需的值。</span><span class="sxs-lookup"><span data-stu-id="b87b9-135">The script outputs values we need for the preceding C# sample.</span></span> <span data-ttu-id="b87b9-136">如需詳細資訊，請參閱 [使用 Azure PowerShell 建立用來存取資源的服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="b87b9-136">For detailed information, see [Use Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in to Azure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set to the subscription you want to work with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is the display name for your app, must be unique in your directory.
    # $uri does not need to be a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for the app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # To avoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun the following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output the values we need for our C# application to successfully authenticate

    Write-Output "Copy these values into the C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a><span data-ttu-id="b87b9-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b87b9-137">Next steps</span></span>
<span data-ttu-id="b87b9-138">既然您已試用 SQL Database 並以 C# 設定資料庫，您就可以進行下列文章：</span><span class="sxs-lookup"><span data-stu-id="b87b9-138">Now that you've tried SQL Database and set up a database with C#, you're ready for the following articles:</span></span>

* [<span data-ttu-id="b87b9-139">使用 SQL Server Management Studio 連接到 SQL Database 並執行範例 T-SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="b87b9-139">Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query</span></span>](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a><span data-ttu-id="b87b9-140">其他資源</span><span class="sxs-lookup"><span data-stu-id="b87b9-140">Additional Resources</span></span>
* [<span data-ttu-id="b87b9-141">SQL Database</span><span class="sxs-lookup"><span data-stu-id="b87b9-141">SQL Database</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* [<span data-ttu-id="b87b9-142">資料庫類別</span><span class="sxs-lookup"><span data-stu-id="b87b9-142">Database Class</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

<!--Image references-->
[1]: ./media/sql-database-get-started-csharp/aad.png
[2]: ./media/sql-database-get-started-csharp/permissions.png
[3]: ./media/sql-database-get-started-csharp/getdomain.png
[4]: ./media/sql-database-get-started-csharp/aad2.png
[5]: ./media/sql-database-get-started-csharp/aad-applications.png
[6]: ./media/sql-database-get-started-csharp/add.png
[7]: ./media/sql-database-get-started-csharp/add-application.png
[8]: ./media/sql-database-get-started-csharp/add-application2.png
[9]: ./media/sql-database-get-started-csharp/clientid.png
