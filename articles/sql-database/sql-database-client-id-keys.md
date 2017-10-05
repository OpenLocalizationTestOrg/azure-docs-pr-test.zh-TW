---
title: "取得應用程式驗證的值 - Azure SQL Database | Microsoft Docs"
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
ms.openlocfilehash: ec6256e9c5bb0d9c8d15d0f673cea70b3915eb34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-required-values-for-authenticating-an-application-to-access-sql-database-from-code"></a><span data-ttu-id="0890d-103">取得驗證應用程式以從程式碼存取 SQL Database 的所需值</span><span class="sxs-lookup"><span data-stu-id="0890d-103">Get the required values for authenticating an application to access SQL Database from code</span></span>
<span data-ttu-id="0890d-104">若要從程式碼建立和管理 SQL Database，您必須在建立 Azure 資源所使用的訂用帳戶的 Azure Active Directory (AAD) 網域中註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0890d-104">To create and manage SQL Database from code you must register your app in the Azure Active Directory (AAD) domain  in the subscription where your Azure resources have been created.</span></span>

## <a name="create-a-service-principal-to-access-resources-from-an-application"></a><span data-ttu-id="0890d-105">從應用程式建立用來存取資源的服務主體</span><span class="sxs-lookup"><span data-stu-id="0890d-105">Create a service principal to access resources from an application</span></span>
<span data-ttu-id="0890d-106">您必須安裝並執行最新的 [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0890d-106">You need to have the latest [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="0890d-107">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="0890d-107">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="0890d-108">下列 PowerShell 指令碼會建立 Active Directory (AD) 應用程式以及驗證 C# 應用程式所需的服務主體。</span><span class="sxs-lookup"><span data-stu-id="0890d-108">The following PowerShell script creates the Active Directory (AD) application and the service principal that we need to authenticate our C# app.</span></span> <span data-ttu-id="0890d-109">指令碼會輸出先前 C# 範例所需的值。</span><span class="sxs-lookup"><span data-stu-id="0890d-109">The script outputs values we need for the preceding C# sample.</span></span> <span data-ttu-id="0890d-110">如需詳細資訊，請參閱 [使用 Azure PowerShell 建立用來存取資源的服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="0890d-110">For detailed information, see [Use Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

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




## <a name="see-also"></a><span data-ttu-id="0890d-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0890d-111">See also</span></span>
* [<span data-ttu-id="0890d-112">以 C# 建立 SQL Database</span><span class="sxs-lookup"><span data-stu-id="0890d-112">Create a SQL database with C#</span></span>](sql-database-get-started-csharp.md)
* [<span data-ttu-id="0890d-113">使用 Azure Active Directory 驗證連線到 SQL Database</span><span class="sxs-lookup"><span data-stu-id="0890d-113">Connecting to SQL Database By Using Azure Active Directory Authentication</span></span>](sql-database-aad-authentication.md)

