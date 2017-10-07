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
# <a name="get-hello-required-values-for-authenticating-an-application-tooaccess-sql-database-from-code"></a>取得所需的 hello 值來驗證程式碼從應用程式 tooaccess SQL 資料庫
toocreate 及從程式碼，您必須註冊您的應用程式在 hello Azure Active Directory (AAD) 網域 hello 訂用帳戶中，已建立您的 Azure 資源管理 SQL Database。

## <a name="create-a-service-principal-tooaccess-resources-from-an-application"></a>從應用程式建立服務主體的 tooaccess 資源
您需要最新 toohave hello [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx)安裝且正在執行。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。

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




## <a name="see-also"></a>另請參閱
* [以 C# 建立 SQL Database](sql-database-get-started-csharp.md)
* [連接 tooSQL 資料庫使用 Azure Active Directory 驗證](sql-database-aad-authentication.md)

