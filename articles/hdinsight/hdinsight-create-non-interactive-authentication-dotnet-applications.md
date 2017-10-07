---
title: "aaaCreate 非互動式驗證.NET HDInsight applciations-Azure |Microsoft 文件"
description: "深入了解如何 toocreate 非互動式驗證.NET HDInsight 應用程式。"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 8e32430f-6404-498a-9fcd-f20338d964af
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 5367c160b0146e6b855486b95f363e8fe7f1c98f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>建立非互動式驗證 .NET HDInsight 應用程式
您可以執行.NET 的 Azure HDInsight 應用程式 （非互動式） 的應用程式自己的身分識別或 hello hello 登入的使用者 （互動式） hello 應用程式的識別之下。 如需 hello 互動式應用程式的範例，請參閱[連接 tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight)。 本文章將示範如何 toocreate 非互動式驗證.NET 應用程式 tooconnect tooAzure 和管理 HDInsight。

從非互動式 .NET 應用程式，您需要︰

* 您的 Azure 訂用帳戶租用戶識別碼 (又稱為目錄識別碼)。 請參閱[取得租用戶識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id)。
* hello Azure Active Directory 應用程式用戶端識別碼。 請參閱[建立 Azure Active Directory 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)以及[取得應用程式識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)
* hello Azure Active Directory 應用程式祕密金鑰。 請參閱[取得應用程式驗證金鑰](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)

## <a name="prerequisites"></a>必要條件
* HDInsight 叢集。 請參閱[入門教學課程](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)。



## <a name="assign-azure-ad-application-toorole"></a>指派 Azure AD 應用程式 toorole
您必須指派 hello 應用程式 tooa[角色](../active-directory/role-based-access-built-in-roles.md)toogrant 它執行動作的權限。 您可以設定 hello 範圍層級 hello hello 訂用帳戶、 資源群組或資源。 hello 權限是範圍的繼承的 toolower 層級 （例如，新增資源群組的應用程式 toohello 讀取器角色表示它可以讀取 hello 資源群組及它所包含的任何資源）。 在本教學課程中，您將在 hello 資源群組層級設定 hello 範圍。 如需詳細資訊，請參閱[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](../active-directory/role-based-access-control-configure.md)

**tooadd hello 擁有者角色 toohello Azure AD 應用程式**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**資源群組**hello 左窗格中。
3. 按一下包含您要執行 Hive 查詢稍後在本教學課程中的 hello HDInsight 叢集的 hello 資源群組。 如果有太多的資源群組，您可以使用 hello 篩選器。
4. 按一下**存取控制 (IAM)**從 hello 資源群組功能表。
5. 按一下**新增**從 hello**使用者**刀鋒視窗。
6. 請遵循 hello 指令 tooadd hello**擁有者**hello 最後一個程序建立角色 toohello Azure AD 應用程式。 當您成功完成它時，您應該會看到 hello hello 與 hello 擁有者角色的使用者 刀鋒視窗中列出的應用程式。

## <a name="develop-hdinsight-client-application"></a>開發 HDInsight 用戶端應用程式

1. 建立 C# 主控台應用程式。
2. 將下列 Nuget 套件 hello:

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. 使用下列程式碼範例的 hello:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Common.Authentication;
        using Microsoft.Azure.Common.Authentication.Factories;
        using Microsoft.Azure.Common.Authentication.Models;
        using Microsoft.Azure.Management.Resources;
        using Microsoft.Azure.Management.HDInsight;
        
        namespace CreateHDICluster
        {
            internal class Program
            {
                private static HDInsightManagementClient _hdiManagementClient;
        
                private static Guid SubscriptionId = new Guid("<Enter Your Azure Subscription ID>");
                private static string tenantID = "<Enter Your Tenant ID (A.K.A. Directory ID)>";
                private static string applicationID = "<Enter Your Application ID>";
                private static string secretKey = "<Enter hello Application Secret Key>";
        
                private static void Main(string[] args)
                {
                    var key = new SecureString();
                    foreach (char c in secretKey) { key.AppendChar(c); }

                    var tokenCreds = GetTokenCloudCredentials(tenantID, applicationID, key);
                    var subCloudCredentials = GetSubscriptionCloudCredentials(tokenCreds, SubscriptionId);
        
                    var resourceManagementClient = new ResourceManagementClient(subCloudCredentials);
                    resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        
                    _hdiManagementClient = new HDInsightManagementClient(subCloudCredentials);
        
                    var results = _hdiManagementClient.Clusters.List();
                    foreach (var name in results.Clusters)
                    {
                        Console.WriteLine("Cluster Name: " + name.Name);
                        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
                        Console.WriteLine("\t Cluster location: " + name.Location);
                        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
                    }
                    Console.WriteLine("Press Enter toocontinue");
                    Console.ReadLine();
                }

                /// Get hello access token for a service principal and provided key                
                public static TokenCloudCredentials GetTokenCloudCredentials(string tenantId, string clientId, SecureString secretKey)
                {
                    var authFactory = new AuthenticationFactory();
                    var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
                    var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
                    var accessToken =
                        authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
        
                    return new TokenCloudCredentials(accessToken);
                }
        
                public static SubscriptionCloudCredentials GetSubscriptionCloudCredentials(SubscriptionCloudCredentials creds, Guid subId)
                {
                    return new TokenCloudCredentials(subId.ToString(), ((TokenCloudCredentials)creds).Token);
                }
            }
        }

## <a name="next-steps"></a>後續步驟
* [使用入口網站建立 Azure Active Directory 應用程式和服務主體](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [使用 Azure Resource Manager 驗證服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)
