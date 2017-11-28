---
title: "應用程式驗證-Azure SQL Database 的 aaaGet 值 |Microsoft 文件"
description: "建立服務主體以從程式碼存取 SQL Database。"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
tags: 
ms.assetid: b43e43bb-6660-49e6-b069-abde97eb5770
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: b57dc075ec9e679da9f2f5fa53e02312539cdf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-required-values-for-authenticating-an-application-tooaccess-sql-database-from-code"></a><span data-ttu-id="574b1-103">取得所需的 hello 值來驗證程式碼從應用程式 tooaccess SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="574b1-103">Get hello required values for authenticating an application tooaccess SQL Database from code</span></span>
<span data-ttu-id="574b1-104">toocreate 及從程式碼，您必須註冊您的應用程式在 hello Azure Active Directory (AAD) 網域 hello 訂用帳戶中，已建立您的 Azure 資源管理 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="574b1-104">toocreate and manage SQL Database from code you must register your app in hello Azure Active Directory (AAD) domain  in hello subscription where your Azure resources have been created.</span></span>

## <a name="create-a-service-principal-tooaccess-resources-from-an-application"></a><span data-ttu-id="574b1-105">從應用程式建立服務主體的 tooaccess 資源</span><span class="sxs-lookup"><span data-stu-id="574b1-105">Create a service principal tooaccess resources from an application</span></span>
<span data-ttu-id="574b1-106">您需要最新 toohave hello [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx)安裝且正在執行。</span><span class="sxs-lookup"><span data-stu-id="574b1-106">You need toohave hello latest [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="574b1-107">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="574b1-107">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="574b1-108">hello 下列 PowerShell 指令碼會建立 hello Active Directory (AD) 應用程式和 hello 服務主體，我們需要 tooauthenticate 我們 C# 應用程式。</span><span class="sxs-lookup"><span data-stu-id="574b1-108">hello following PowerShell script creates hello Active Directory (AD) application and hello service principal that we need tooauthenticate our C# app.</span></span> <span data-ttu-id="574b1-109">hello 指令碼輸出我們需要 hello 前面 C# 範例的值。</span><span class="sxs-lookup"><span data-stu-id="574b1-109">hello script outputs values we need for hello preceding C# sample.</span></span> <span data-ttu-id="574b1-110">如需詳細資訊，請參閱[使用 Azure PowerShell toocreate 服務主體 tooaccess 資源](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="574b1-110">For detailed information, see [Use Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

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




## <a name="see-also"></a><span data-ttu-id="574b1-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="574b1-111">See also</span></span>
* [<span data-ttu-id="574b1-112">以 C# 建立 SQL Database</span><span class="sxs-lookup"><span data-stu-id="574b1-112">Create a SQL database with C#</span></span>](sql-database-get-started-csharp.md)
* [<span data-ttu-id="574b1-113">連接 tooSQL 資料庫使用 Azure Active Directory 驗證</span><span class="sxs-lookup"><span data-stu-id="574b1-113">Connecting tooSQL Database By Using Azure Active Directory Authentication</span></span>](sql-database-aad-authentication.md)

