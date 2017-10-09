---
title: "C#：開始使用 Azure SQL Database | Microsoft Docs"
description: "SQL Database 開發 SQL 和 C# 應用程式，再使用 C# 使用 hello SQL 資料庫 Library for.NET 建立 Azure SQL Database。"
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
ms.openlocfilehash: e880ebabd53546bea37a13186b0f1a13db35b684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a><span data-ttu-id="13a9f-104">C# toocreate SQL database 使用適用於.NET 的 hello SQL 資料庫程式庫</span><span class="sxs-lookup"><span data-stu-id="13a9f-104">Use C# toocreate a SQL database with hello SQL Database Library for .NET</span></span>

<span data-ttu-id="13a9f-105">了解如何 toouse C# toocreate Azure SQL 資料庫與 hello [Microsoft Azure SQL Management Library for.NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)。</span><span class="sxs-lookup"><span data-stu-id="13a9f-105">Learn how toouse C# toocreate an Azure SQL database with hello [Microsoft Azure SQL Management Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span> <span data-ttu-id="13a9f-106">本文說明如何 toocreate 單一資料庫使用 SQL 和 C#。</span><span class="sxs-lookup"><span data-stu-id="13a9f-106">This article describes how toocreate a single database with SQL and C#.</span></span> <span data-ttu-id="13a9f-107">toocreate 彈性集區，請參閱[建立彈性集區](sql-database-elastic-pool-manage-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="13a9f-107">toocreate elastic pools, see [Create an elastic pool](sql-database-elastic-pool-manage-csharp.md).</span></span>

<span data-ttu-id="13a9f-108">hello Azure SQL Database 管理.NET 程式庫提供[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-基礎應用程式開發介面中包裝 hello[資源管理員為基礎的 SQL Database REST API](https://docs.microsoft.com/rest/api/sql/)。</span><span class="sxs-lookup"><span data-stu-id="13a9f-108">hello Azure SQL Database Management Library for .NET provides an [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-based API that wraps hello [Resource Manager-based SQL Database REST API](https://docs.microsoft.com/rest/api/sql/).</span></span>

> [!NOTE]
> <span data-ttu-id="13a9f-109">您使用 hello 時，才支援許多新的 SQL Database 功能[Azure Resource Manager 部署模型](../azure-resource-manager/resource-group-overview.md)，因此您一定要使用 hello 最新**Azure SQL Database 管理.NET 程式庫 ([文件](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet 封裝](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**。</span><span class="sxs-lookup"><span data-stu-id="13a9f-109">Many new features of SQL Database are only supported when you are using hello [Azure Resource Manager deployment model](../azure-resource-manager/resource-group-overview.md), so you should always use hello latest **Azure SQL Database Management Library for .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet Package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span></span> <span data-ttu-id="13a9f-110">較舊的 hello[傳統部署模型的基礎程式庫](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql)回溯相容性，因此，建議使用較新版 hello 基礎的資源管理員程式庫支援。</span><span class="sxs-lookup"><span data-stu-id="13a9f-110">hello older [classic deployment model based libraries](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) are supported for backward compatibility only, so we recommend you use hello newer Resource Manager based libraries.</span></span>
> 
> 

<span data-ttu-id="13a9f-111">toocomplete hello 本文中的步驟，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="13a9f-111">toocomplete hello steps in this article, you need hello following:</span></span>

* <span data-ttu-id="13a9f-112">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="13a9f-112">An Azure subscription.</span></span> <span data-ttu-id="13a9f-113">如果您需要 Azure 訂用帳戶，只需按一下**免費帳戶**在 hello 頂端頁面，然後再回來 toofinish 這篇文章。</span><span class="sxs-lookup"><span data-stu-id="13a9f-113">If you need an Azure subscription simply click **FREE ACCOUNT** at hello top of this page, and then come back toofinish this article.</span></span>
* <span data-ttu-id="13a9f-114">Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="13a9f-114">Visual Studio.</span></span> <span data-ttu-id="13a9f-115">一份免費的 Visual Studio，請參閱 hello [Visual Studio 下載](https://www.visualstudio.com/downloads/download-visual-studio-vs)頁面。</span><span class="sxs-lookup"><span data-stu-id="13a9f-115">For a free copy of Visual Studio, see hello [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) page.</span></span>

> [!NOTE]
> <span data-ttu-id="13a9f-116">本文會建立一個新的空白 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="13a9f-116">This article creates a new, blank SQL database.</span></span> <span data-ttu-id="13a9f-117">修改 hello *CreateOrUpdateDatabase(...)*方法 hello 遵循範例 toocopy 資料庫，在資料庫調整規模，請建立資料庫集區等等。</span><span class="sxs-lookup"><span data-stu-id="13a9f-117">Modify hello *CreateOrUpdateDatabase(...)* method in hello following sample toocopy databases, scale databases, create a database in a pool, etc.</span></span>  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a><span data-ttu-id="13a9f-118">建立主控台應用程式並安裝所需的 hello 程式庫</span><span class="sxs-lookup"><span data-stu-id="13a9f-118">Create a console app and install hello required libraries</span></span>
1. <span data-ttu-id="13a9f-119">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="13a9f-119">Start Visual Studio.</span></span>
2. <span data-ttu-id="13a9f-120">按一下 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="13a9f-120">Click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="13a9f-121">建立 C# **主控台應用程式** 並將其命名為︰ *SqlDbConsoleApp*</span><span class="sxs-lookup"><span data-stu-id="13a9f-121">Create a C# **Console Application** and name it: *SqlDbConsoleApp*</span></span>

<span data-ttu-id="13a9f-122">toocreate C# 中，負載 hello 的 SQL 資料庫所需管理程式庫 (使用 hello[封裝管理員主控台](http://docs.nuget.org/Consume/Package-Manager-Console)):</span><span class="sxs-lookup"><span data-stu-id="13a9f-122">toocreate a SQL database with C#, load hello required management libraries (using hello [package manager console](http://docs.nuget.org/Consume/Package-Manager-Console)):</span></span>

1. <span data-ttu-id="13a9f-123">按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="13a9f-123">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="13a9f-124">型別`Install-Package Microsoft.Azure.Management.Sql -Pre`最新 tooinstall hello [Microsoft Azure SQL 管理程式庫](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)。</span><span class="sxs-lookup"><span data-stu-id="13a9f-124">Type `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall hello latest [Microsoft Azure SQL Management Library](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span>
3. <span data-ttu-id="13a9f-125">型別`Install-Package Microsoft.Azure.Management.ResourceManager -Pre`tooinstall hello [Microsoft Azure 資源管理員程式庫](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)。</span><span class="sxs-lookup"><span data-stu-id="13a9f-125">Type `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [Microsoft Azure Resource Manager Library](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span></span>
4. <span data-ttu-id="13a9f-126">型別`Install-Package Microsoft.Azure.Common.Authentication -Pre`tooinstall hello [Microsoft Azure 通用驗證程式庫](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication)。</span><span class="sxs-lookup"><span data-stu-id="13a9f-126">Type `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [Microsoft Azure Common Authentication Library](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span></span> 

> [!NOTE]
> <span data-ttu-id="13a9f-127">hello 這篇文章中的範例使用同步表單的每個 API 要求和區塊直到完成 hello REST 呼叫 hello 基礎服務上。</span><span class="sxs-lookup"><span data-stu-id="13a9f-127">hello examples in this article use a synchronous form of each API request and block until completion of hello REST call on hello underlying service.</span></span> <span data-ttu-id="13a9f-128">有可用的非同步方法。</span><span class="sxs-lookup"><span data-stu-id="13a9f-128">There are async methods available.</span></span>
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a><span data-ttu-id="13a9f-129">建立 SQL Database 伺服器、防火牆規則和 SQL Database - C# 範例</span><span class="sxs-lookup"><span data-stu-id="13a9f-129">Create a SQL Database server, firewall rule, and SQL database - C# example</span></span>
<span data-ttu-id="13a9f-130">hello 下列範例會建立資源群組、 伺服器、 防火牆規則，與 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="13a9f-130">hello following sample creates a resource group, server, firewall rule, and a SQL database.</span></span> <span data-ttu-id="13a9f-131">請參閱，[建立服務主體的 tooaccess 資源](#create-a-service-principal-to-access-resources)tooget hello`_subscriptionId, _tenantId, _applicationId, and _applicationSecret`變數。</span><span class="sxs-lookup"><span data-stu-id="13a9f-131">See, [Create a service principal tooaccess resources](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variables.</span></span>

<span data-ttu-id="13a9f-132">取代 hello 內容**Program.cs** hello 下列項目，與更新 hello`{variables}`以您的應用程式的值 (不包括 hello `{}`)。</span><span class="sxs-lookup"><span data-stu-id="13a9f-132">Replace hello contents of **Program.cs** with hello following, and update hello `{variables}` with your app values (do not include hello `{}`).</span></span>

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

        // Create management clients for hello Azure resources your app needs toowork with.
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


            Console.WriteLine("Press any key toocontinue...");
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
            // Retrieve hello server that will host this database
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





## <a name="create-a-service-principal-tooaccess-resources"></a><span data-ttu-id="13a9f-133">建立服務主體的 tooaccess 資源</span><span class="sxs-lookup"><span data-stu-id="13a9f-133">Create a service principal tooaccess resources</span></span>
<span data-ttu-id="13a9f-134">hello 下列 PowerShell 指令碼會建立 hello Active Directory (AD) 應用程式和 hello 服務主體，我們需要 tooauthenticate 我們 C# 應用程式。</span><span class="sxs-lookup"><span data-stu-id="13a9f-134">hello following PowerShell script creates hello Active Directory (AD) application and hello service principal that we need tooauthenticate our C# app.</span></span> <span data-ttu-id="13a9f-135">hello 指令碼輸出我們需要 hello 前面 C# 範例的值。</span><span class="sxs-lookup"><span data-stu-id="13a9f-135">hello script outputs values we need for hello preceding C# sample.</span></span> <span data-ttu-id="13a9f-136">如需詳細資訊，請參閱[使用 Azure PowerShell toocreate 服務主體 tooaccess 資源](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="13a9f-136">For detailed information, see [Use Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a><span data-ttu-id="13a9f-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13a9f-137">Next steps</span></span>
<span data-ttu-id="13a9f-138">現在，您已嘗試 SQL 資料庫並設定資料庫，以使用 C#，您已準備好進行 hello 下列文章：</span><span class="sxs-lookup"><span data-stu-id="13a9f-138">Now that you've tried SQL Database and set up a database with C#, you're ready for hello following articles:</span></span>

* [<span data-ttu-id="13a9f-139">SQL Server Management Studio 連接 tooSQL 資料庫及執行範例 T-SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="13a9f-139">Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query</span></span>](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a><span data-ttu-id="13a9f-140">其他資源</span><span class="sxs-lookup"><span data-stu-id="13a9f-140">Additional Resources</span></span>
* [<span data-ttu-id="13a9f-141">SQL Database</span><span class="sxs-lookup"><span data-stu-id="13a9f-141">SQL Database</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* [<span data-ttu-id="13a9f-142">資料庫類別</span><span class="sxs-lookup"><span data-stu-id="13a9f-142">Database Class</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

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
