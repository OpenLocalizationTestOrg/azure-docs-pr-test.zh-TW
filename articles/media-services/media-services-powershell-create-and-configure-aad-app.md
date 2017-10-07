---
title: "aaaUse PowerShell toocreate Azure AD 應用程式 tooaccess hello Azure Media Services API |Microsoft 文件"
description: "深入了解如何 toouse PowerShell toocreate Azure Active Directory (Azure AD) 應用程式並將它設定 tooaccess hello Azure 媒體服務 API。"
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
ms.openlocfilehash: 1a8b4a53ad10b559f6ee4242b95c5bd15ee8e903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a>使用 PowerShell toocreate Azure AD 應用程式 toouse 以 hello Azure 媒體服務 API

了解如何 toouse PowerShell 指令碼 toocreate Azure Active Directory (Azure AD) 應用程式和服務主體 tooaccess Azure Media Services 資源。  

## <a name="prerequisites"></a>必要條件

- 一個 Azure 帳戶。 如果您沒有帳戶，請先從 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。 
- 媒體服務帳戶。 如需詳細資訊，請參閱[hello Azure 入口網站中建立 Azure Media Services 帳戶](media-services-portal-create-account.md)。
- Azure PowerShell 0.8.8 版或更新版本。 如需詳細資訊，請參閱[如何 toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)。
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
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

如需詳細資訊，請參閱下列文章 hello:

- [使用 Azure PowerShell toocreate 服務主體 tooaccess 資源](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [使用 Azure PowerShell 管理角色型存取控制](../active-directory/role-based-access-control-manage-access-powershell.md)
- [Toomanually 藉由使用憑證所設定的精靈應用程式](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>後續步驟

開始使用[上傳檔案 tooyour 帳戶](media-services-portal-upload-files.md)。
