---
title: "使用 PowerShell 建立 Azure AD 應用程式，以存取 Azure 媒體服務 API | Microsoft Docs"
description: "了解如何使用 PowerShell 建立 Azure Active Directory (Azure AD) 應用程式，並設定它以存取 Azure 媒體服務 API。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: eea0f3a03dd77ce56484f32b192299bd97c05300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-create-an-azure-ad-app-to-use-with-the-azure-media-services-api"></a>使用 PowerShell 建立 Azure AD 應用程式，以搭配 Azure 媒體服務 API 使用

了解如何使用 PowerShell 指令碼建立 Azure Active Directory (Azure AD) 應用程式和服務主體，以存取 Azure 媒體服務資源。  

## <a name="prerequisites"></a>必要條件

- 一個 Azure 帳戶。 如果您沒有帳戶，請先從 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。 
- 媒體服務帳戶。 如需詳細資訊，請參閱[在 Azure 入口網站建立 Azure 媒體服務帳戶](media-services-portal-create-account.md)。
- Azure PowerShell 0.8.8 版或更新版本。 如需詳細資訊，請參閱[如何使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview) \(英文\)。
- Azure Resource Manager Cmdlet。  

## <a name="create-an-azure-ad-app-by-using-powershell"></a>使用 PowerShell 建立 Azure AD 應用程式  

```powershell
Login-AzureRmAccount
Import-Module AzureRM.Resources
Set-AzureRmContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds to allow the service principal application to become active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

如需詳細資訊，請參閱下列文章。

- [使用 Azure PowerShell 建立用來存取資源的服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [使用 Azure PowerShell 管理角色型存取控制](../active-directory/role-based-access-control-manage-access-powershell.md)
- [如何使用憑證手動設定精靈應用程式](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad) \(英文\)

## <a name="next-steps"></a>後續步驟

開始使用[上傳檔案至您的帳戶](media-services-portal-upload-files.md)。
