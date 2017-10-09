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
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a>C# toocreate SQL database 使用適用於.NET 的 hello SQL 資料庫程式庫

了解如何 toouse C# toocreate Azure SQL 資料庫與 hello [Microsoft Azure SQL Management Library for.NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)。 本文說明如何 toocreate 單一資料庫使用 SQL 和 C#。 toocreate 彈性集區，請參閱[建立彈性集區](sql-database-elastic-pool-manage-csharp.md)。

hello Azure SQL Database 管理.NET 程式庫提供[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-基礎應用程式開發介面中包裝 hello[資源管理員為基礎的 SQL Database REST API](https://docs.microsoft.com/rest/api/sql/)。

> [!NOTE]
> 您使用 hello 時，才支援許多新的 SQL Database 功能[Azure Resource Manager 部署模型](../azure-resource-manager/resource-group-overview.md)，因此您一定要使用 hello 最新**Azure SQL Database 管理.NET 程式庫 ([文件](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet 封裝](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**。 較舊的 hello[傳統部署模型的基礎程式庫](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql)回溯相容性，因此，建議使用較新版 hello 基礎的資源管理員程式庫支援。
> 
> 

toocomplete hello 本文中的步驟，您需要下列 hello:

* Azure 訂用帳戶。 如果您需要 Azure 訂用帳戶，只需按一下**免費帳戶**在 hello 頂端頁面，然後再回來 toofinish 這篇文章。
* Visual Studio。 一份免費的 Visual Studio，請參閱 hello [Visual Studio 下載](https://www.visualstudio.com/downloads/download-visual-studio-vs)頁面。

> [!NOTE]
> 本文會建立一個新的空白 SQL Database。 修改 hello *CreateOrUpdateDatabase(...)*方法 hello 遵循範例 toocopy 資料庫，在資料庫調整規模，請建立資料庫集區等等。  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a>建立主控台應用程式並安裝所需的 hello 程式庫
1. 啟動 Visual Studio。
2. 按一下 [檔案] > [新增] > [專案]。
3. 建立 C# **主控台應用程式** 並將其命名為︰ *SqlDbConsoleApp*

toocreate C# 中，負載 hello 的 SQL 資料庫所需管理程式庫 (使用 hello[封裝管理員主控台](http://docs.nuget.org/Consume/Package-Manager-Console)):

1. 按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。
2. 型別`Install-Package Microsoft.Azure.Management.Sql -Pre`最新 tooinstall hello [Microsoft Azure SQL 管理程式庫](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)。
3. 型別`Install-Package Microsoft.Azure.Management.ResourceManager -Pre`tooinstall hello [Microsoft Azure 資源管理員程式庫](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)。
4. 型別`Install-Package Microsoft.Azure.Common.Authentication -Pre`tooinstall hello [Microsoft Azure 通用驗證程式庫](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication)。 

> [!NOTE]
> hello 這篇文章中的範例使用同步表單的每個 API 要求和區塊直到完成 hello REST 呼叫 hello 基礎服務上。 有可用的非同步方法。
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>建立 SQL Database 伺服器、防火牆規則和 SQL Database - C# 範例
hello 下列範例會建立資源群組、 伺服器、 防火牆規則，與 SQL 資料庫。 請參閱，[建立服務主體的 tooaccess 資源](#create-a-service-principal-to-access-resources)tooget hello`_subscriptionId, _tenantId, _applicationId, and _applicationSecret`變數。

取代 hello 內容**Program.cs** hello 下列項目，與更新 hello`{variables}`以您的應用程式的值 (不包括 hello `{}`)。

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





## <a name="create-a-service-principal-tooaccess-resources"></a>建立服務主體的 tooaccess 資源
hello 下列 PowerShell 指令碼會建立 hello Active Directory (AD) 應用程式和 hello 服務主體，我們需要 tooauthenticate 我們 C# 應用程式。 hello 指令碼輸出我們需要 hello 前面 C# 範例的值。 如需詳細資訊，請參閱[使用 Azure PowerShell toocreate 服務主體 tooaccess 資源](../azure-resource-manager/resource-group-authenticate-service-principal.md)。

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



## <a name="next-steps"></a>後續步驟
現在，您已嘗試 SQL 資料庫並設定資料庫，以使用 C#，您已準備好進行 hello 下列文章：

* [SQL Server Management Studio 連接 tooSQL 資料庫及執行範例 T-SQL 查詢](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a>其他資源
* [SQL Database](https://azure.microsoft.com/documentation/services/sql-database/)
* [資料庫類別](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

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
