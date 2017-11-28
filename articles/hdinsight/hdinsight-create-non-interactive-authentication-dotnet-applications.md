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
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="371dd-103">建立非互動式驗證 .NET HDInsight 應用程式</span><span class="sxs-lookup"><span data-stu-id="371dd-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="371dd-104">您可以執行.NET 的 Azure HDInsight 應用程式 （非互動式） 的應用程式自己的身分識別或 hello hello 登入的使用者 （互動式） hello 應用程式的識別之下。</span><span class="sxs-lookup"><span data-stu-id="371dd-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under hello identity of hello signed-in user of hello application (interactive).</span></span> <span data-ttu-id="371dd-105">如需 hello 互動式應用程式的範例，請參閱[連接 tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight)。</span><span class="sxs-lookup"><span data-stu-id="371dd-105">For a sample of hello interactive application, see [Connect tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="371dd-106">本文章將示範如何 toocreate 非互動式驗證.NET 應用程式 tooconnect tooAzure 和管理 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="371dd-106">This article shows you how toocreate non-interactive authentication .NET application tooconnect tooAzure and manage HDInsight.</span></span>

<span data-ttu-id="371dd-107">從非互動式 .NET 應用程式，您需要︰</span><span class="sxs-lookup"><span data-stu-id="371dd-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="371dd-108">您的 Azure 訂用帳戶租用戶識別碼 (又稱為目錄識別碼)。</span><span class="sxs-lookup"><span data-stu-id="371dd-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="371dd-109">請參閱[取得租用戶識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id)。</span><span class="sxs-lookup"><span data-stu-id="371dd-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="371dd-110">hello Azure Active Directory 應用程式用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="371dd-110">hello Azure Active Directory application client ID.</span></span> <span data-ttu-id="371dd-111">請參閱[建立 Azure Active Directory 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)以及[取得應用程式識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="371dd-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="371dd-112">hello Azure Active Directory 應用程式祕密金鑰。</span><span class="sxs-lookup"><span data-stu-id="371dd-112">hello Azure Active Directory application secret key.</span></span> <span data-ttu-id="371dd-113">請參閱[取得應用程式驗證金鑰](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="371dd-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="371dd-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="371dd-114">Prerequisites</span></span>
* <span data-ttu-id="371dd-115">HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="371dd-115">HDInsight cluster.</span></span> <span data-ttu-id="371dd-116">請參閱[入門教學課程](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)。</span><span class="sxs-lookup"><span data-stu-id="371dd-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-toorole"></a><span data-ttu-id="371dd-117">指派 Azure AD 應用程式 toorole</span><span class="sxs-lookup"><span data-stu-id="371dd-117">Assign Azure AD application toorole</span></span>
<span data-ttu-id="371dd-118">您必須指派 hello 應用程式 tooa[角色](../active-directory/role-based-access-built-in-roles.md)toogrant 它執行動作的權限。</span><span class="sxs-lookup"><span data-stu-id="371dd-118">You must assign hello application tooa [role](../active-directory/role-based-access-built-in-roles.md) toogrant it permissions for performing actions.</span></span> <span data-ttu-id="371dd-119">您可以設定 hello 範圍層級 hello hello 訂用帳戶、 資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="371dd-119">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="371dd-120">hello 權限是範圍的繼承的 toolower 層級 （例如，新增資源群組的應用程式 toohello 讀取器角色表示它可以讀取 hello 資源群組及它所包含的任何資源）。</span><span class="sxs-lookup"><span data-stu-id="371dd-120">hello permissions are inherited toolower levels of scope (for example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains).</span></span> <span data-ttu-id="371dd-121">在本教學課程中，您將在 hello 資源群組層級設定 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="371dd-121">In this tutorial, you will set hello scope at hello resource group level.</span></span> <span data-ttu-id="371dd-122">如需詳細資訊，請參閱[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="371dd-122">For more information, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="371dd-123">**tooadd hello 擁有者角色 toohello Azure AD 應用程式**</span><span class="sxs-lookup"><span data-stu-id="371dd-123">**tooadd hello Owner role toohello Azure AD application**</span></span>

1. <span data-ttu-id="371dd-124">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="371dd-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="371dd-125">按一下**資源群組**hello 左窗格中。</span><span class="sxs-lookup"><span data-stu-id="371dd-125">Click **Resource Group** from hello left pane.</span></span>
3. <span data-ttu-id="371dd-126">按一下包含您要執行 Hive 查詢稍後在本教學課程中的 hello HDInsight 叢集的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="371dd-126">Click hello resource group that contains hello HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="371dd-127">如果有太多的資源群組，您可以使用 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="371dd-127">If there are too many resource groups, you can use hello filter.</span></span>
4. <span data-ttu-id="371dd-128">按一下**存取控制 (IAM)**從 hello 資源群組功能表。</span><span class="sxs-lookup"><span data-stu-id="371dd-128">Click **Access control (IAM)** from hello resource group menu.</span></span>
5. <span data-ttu-id="371dd-129">按一下**新增**從 hello**使用者**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="371dd-129">Click **Add** from hello **Users** blade.</span></span>
6. <span data-ttu-id="371dd-130">請遵循 hello 指令 tooadd hello**擁有者**hello 最後一個程序建立角色 toohello Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="371dd-130">Follow hello instruction tooadd hello **Owner** role toohello Azure AD application you created in hello last procedure.</span></span> <span data-ttu-id="371dd-131">當您成功完成它時，您應該會看到 hello hello 與 hello 擁有者角色的使用者 刀鋒視窗中列出的應用程式。</span><span class="sxs-lookup"><span data-stu-id="371dd-131">When you complete it successfully, you shall see hello application listed in hello Users blade with hello Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="371dd-132">開發 HDInsight 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="371dd-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="371dd-133">建立 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="371dd-133">Create a C# console application.</span></span>
2. <span data-ttu-id="371dd-134">將下列 Nuget 套件 hello:</span><span class="sxs-lookup"><span data-stu-id="371dd-134">Add hello following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="371dd-135">使用下列程式碼範例的 hello:</span><span class="sxs-lookup"><span data-stu-id="371dd-135">Use hello following code sample:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="371dd-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="371dd-136">Next steps</span></span>
* [<span data-ttu-id="371dd-137">使用入口網站建立 Azure Active Directory 應用程式和服務主體</span><span class="sxs-lookup"><span data-stu-id="371dd-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="371dd-138">使用 Azure Resource Manager 驗證服務主體</span><span class="sxs-lookup"><span data-stu-id="371dd-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="371dd-139">Azure 角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="371dd-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
