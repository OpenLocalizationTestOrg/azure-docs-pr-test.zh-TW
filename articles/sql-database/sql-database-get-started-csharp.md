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
# <a name="use-c-to-create-a-sql-database-with-the-sql-database-library-for-net"></a>以 SQL Database Library for .NET 使用 C# 建立 SQL 資料庫

了解如何使用 C# 透過 [Microsoft Azure SQL Management Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql) 建立 Azure SQL Database。 本文說明如何使用 SQL 和 C# 建立單一資料庫。 若要建立彈性集區，請參閱 [建立彈性集區](sql-database-elastic-pool-manage-csharp.md)。

Azure SQL Database Management Library for .NET 提供 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 式 API，它會包裝 [Resource Manager 式 SQL Database REST API](https://docs.microsoft.com/rest/api/sql/)。

> [!NOTE]
> SQL Database 的許多新功能只有在使用 [Azure Resource Manager 部署模型](../azure-resource-manager/resource-group-overview.md)時才支援，所以您應該一律使用最新的**適用於 .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet Package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)) 的 Azure SQL Database Management Library**。 支援較舊的[以傳統部署模型為基礎的程式庫](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql)，以提供回溯相容性，因此我們建議您使用較新的以 Resource Manager 為基礎的程式庫。
> 
> 

若要完成這篇文章中的步驟，您需要下列項目︰

* Azure 訂用帳戶。 如果需要 Azure 訂用帳戶，可以先按一下此頁面頂端的 [免費帳戶]  ，然後再回來完成這篇文章。
* Visual Studio。 如需免費的 Visual Studio，請參閱 [Visual Studio 下載](https://www.visualstudio.com/downloads/download-visual-studio-vs) 頁面。

> [!NOTE]
> 本文會建立一個新的空白 SQL Database。 在下列範例中修改 *CreateOrUpdateDatabase(...)* 方法，以複製資料庫、調整資料庫大小、在集區中建立資料庫等等。  
> 

## <a name="create-a-console-app-and-install-the-required-libraries"></a>建立主控台應用程式並安裝必要的程式庫
1. 啟動 Visual Studio。
2. 按一下 [檔案] > [新增] > [專案]。
3. 建立 C# **主控台應用程式** 並將其命名為︰ *SqlDbConsoleApp*

若要使用 C# 建立 SQL Database，請載入必要的管理程式庫 (使用 [封裝管理員主控台](http://docs.nuget.org/Consume/Package-Manager-Console))：

1. 按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。
2. 輸入 `Install-Package Microsoft.Azure.Management.Sql -Pre` 以安裝最新的 [Microsoft Azure SQL 管理程式庫](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)。
3. 輸入 `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` 以安裝 [Microsoft Azure Resource Manager 程式庫](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)。
4. 輸入 `Install-Package Microsoft.Azure.Common.Authentication -Pre` 以安裝 [Microsoft Azure 通用驗證程式庫](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication)。 

> [!NOTE]
> 這篇文章中的範例使用每個 API 要求的同步表單，並且封鎖直到基礎服務上的 REST 呼叫完成。 有可用的非同步方法。
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>建立 SQL Database 伺服器、防火牆規則和 SQL Database - C# 範例
下列範例會建立資源群組、伺服器、防火牆規則和 SQL Database。 請參閱[建立用來存取資源的服務主體](#create-a-service-principal-to-access-resources)以取得 `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` 變數。

以下列內容取代 **Program.cs** 的內容，並以您應用程式的值更新 `{variables}` (請勿包含 `{}`)。

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





## <a name="create-a-service-principal-to-access-resources"></a>建立用來存取資源的服務主體
下列 PowerShell 指令碼會建立 Active Directory (AD) 應用程式以及驗證 C# 應用程式所需的服務主體。 指令碼會輸出先前 C# 範例所需的值。 如需詳細資訊，請參閱 [使用 Azure PowerShell 建立用來存取資源的服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)。

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



## <a name="next-steps"></a>後續步驟
既然您已試用 SQL Database 並以 C# 設定資料庫，您就可以進行下列文章：

* [使用 SQL Server Management Studio 連接到 SQL Database 並執行範例 T-SQL 查詢](sql-database-connect-query-ssms.md)

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
