---
title: "建立非互動式驗證 .NET HDInsight 應用程式 - Azure | Microsoft Docs"
description: "了解如何建立非互動式驗證 .NET HDInsight 應用程式。"
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
ms.openlocfilehash: 7821a9e60e60ff01cff06db2a6f216a260c1c41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="ea4b2-103">建立非互動式驗證 .NET HDInsight 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea4b2-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="ea4b2-104">您可以使用應用程式本身的身分識別 (非互動式) 或使用應用程式的登入使用者的身分識別 (互動式)，執行 .NET Azure HDInsight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under the identity of the signed-in user of the application (interactive).</span></span> <span data-ttu-id="ea4b2-105">如需互動式應用程式的範例，請參閱[連接至 Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight)。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-105">For a sample of the interactive application, see [Connect to Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="ea4b2-106">本文將說明如何建立非互動式驗證 .NET 應用程式，來連接到 Azure 及管理 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-106">This article shows you how to create non-interactive authentication .NET application to connect to Azure and manage HDInsight.</span></span>

<span data-ttu-id="ea4b2-107">從非互動式 .NET 應用程式，您需要︰</span><span class="sxs-lookup"><span data-stu-id="ea4b2-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="ea4b2-108">您的 Azure 訂用帳戶租用戶識別碼 (又稱為目錄識別碼)。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="ea4b2-109">請參閱[取得租用戶識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id)。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="ea4b2-110">Azure Active Directory 應用程式用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-110">The Azure Active Directory application client ID.</span></span> <span data-ttu-id="ea4b2-111">請參閱[建立 Azure Active Directory 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application)以及[取得應用程式識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="ea4b2-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="ea4b2-112">Azure Active Directory 應用程式祕密金鑰。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-112">The Azure Active Directory application secret key.</span></span> <span data-ttu-id="ea4b2-113">請參閱[取得應用程式驗證金鑰](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="ea4b2-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea4b2-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="ea4b2-114">Prerequisites</span></span>
* <span data-ttu-id="ea4b2-115">HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-115">HDInsight cluster.</span></span> <span data-ttu-id="ea4b2-116">請參閱[入門教學課程](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster)。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-to-role"></a><span data-ttu-id="ea4b2-117">將 Azure AD 應用程式指派給角色</span><span class="sxs-lookup"><span data-stu-id="ea4b2-117">Assign Azure AD application to role</span></span>
<span data-ttu-id="ea4b2-118">您必須將應用程式指派給某個 [角色](../active-directory/role-based-access-built-in-roles.md) ，以便授與它執行動作的權限。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-118">You must assign the application to a [role](../active-directory/role-based-access-built-in-roles.md) to grant it permissions for performing actions.</span></span> <span data-ttu-id="ea4b2-119">您可以針對訂用帳戶、資源群組或資源的層級設定範圍。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-119">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="ea4b2-120">較低的範圍層級會繼承較高層級的權限 (舉例來說，為資源群組的讀取者角色新增應用程式，代表該角色可以讀取資源群組及其所包含的任何資源)。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-120">The permissions are inherited to lower levels of scope (for example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains).</span></span> <span data-ttu-id="ea4b2-121">在本教學課程中，您將在資源群組層級設定範圍。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-121">In this tutorial, you will set the scope at the resource group level.</span></span> <span data-ttu-id="ea4b2-122">如需詳細資訊，請參閱[使用角色指派來管理 Azure 訂用帳戶資源的存取權](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="ea4b2-122">For more information, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="ea4b2-123">**將擁有者角色新增至 Azure AD 應用程式**</span><span class="sxs-lookup"><span data-stu-id="ea4b2-123">**To add the Owner role to the Azure AD application**</span></span>

1. <span data-ttu-id="ea4b2-124">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ea4b2-125">按一下左側面板上的 [資源群組] 。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-125">Click **Resource Group** from the left pane.</span></span>
3. <span data-ttu-id="ea4b2-126">按一下資源群組，它包含您稍後在本教學課程中要在其中執行 Hive 查詢的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-126">Click the resource group that contains the HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="ea4b2-127">如果有太多的資源群組，您可以使用篩選器。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-127">If there are too many resource groups, you can use the filter.</span></span>
4. <span data-ttu-id="ea4b2-128">從資源群組功能表中，按一下 [存取控制 (IAM)]。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-128">Click **Access control (IAM)** from the resource group menu.</span></span>
5. <span data-ttu-id="ea4b2-129">從 [使用者] 刀鋒視窗中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-129">Click **Add** from the **Users** blade.</span></span>
6. <span data-ttu-id="ea4b2-130">依照指示以將 [擁有者] 角色新增至您在上一個程序中建立的 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-130">Follow the instruction to add the **Owner** role to the Azure AD application you created in the last procedure.</span></span> <span data-ttu-id="ea4b2-131">當您成功完成此作業時，您會看到 [使用者] 刀鋒視窗中列出的應用程式具有 [擁有者] 角色。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-131">When you complete it successfully, you shall see the application listed in the Users blade with the Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="ea4b2-132">開發 HDInsight 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="ea4b2-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="ea4b2-133">建立 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea4b2-133">Create a C# console application.</span></span>
2. <span data-ttu-id="ea4b2-134">新增以下 Nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="ea4b2-134">Add the following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="ea4b2-135">使用下列程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="ea4b2-135">Use the following code sample:</span></span>

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
                private static string secretKey = "<Enter the Application Secret Key>";
        
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
                    Console.WriteLine("Press Enter to continue");
                    Console.ReadLine();
                }

                /// Get the access token for a service principal and provided key                
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

## <a name="next-steps"></a><span data-ttu-id="ea4b2-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ea4b2-136">Next steps</span></span>
* [<span data-ttu-id="ea4b2-137">使用入口網站建立 Azure Active Directory 應用程式和服務主體</span><span class="sxs-lookup"><span data-stu-id="ea4b2-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="ea4b2-138">使用 Azure Resource Manager 驗證服務主體</span><span class="sxs-lookup"><span data-stu-id="ea4b2-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="ea4b2-139">Azure 角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="ea4b2-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
