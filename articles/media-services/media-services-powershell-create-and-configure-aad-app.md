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
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a><span data-ttu-id="079f9-103">使用 PowerShell toocreate Azure AD 應用程式 toouse 以 hello Azure 媒體服務 API</span><span class="sxs-lookup"><span data-stu-id="079f9-103">Use PowerShell toocreate an Azure AD app toouse with hello Azure Media Services API</span></span>

<span data-ttu-id="079f9-104">了解如何 toouse PowerShell 指令碼 toocreate Azure Active Directory (Azure AD) 應用程式和服務主體 tooaccess Azure Media Services 資源。</span><span class="sxs-lookup"><span data-stu-id="079f9-104">Learn how toouse a PowerShell script toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="079f9-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="079f9-105">Prerequisites</span></span>

- <span data-ttu-id="079f9-106">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="079f9-106">An Azure account.</span></span> <span data-ttu-id="079f9-107">如果您沒有帳戶，請先從 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="079f9-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="079f9-108">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="079f9-108">A Media Services account.</span></span> <span data-ttu-id="079f9-109">如需詳細資訊，請參閱[hello Azure 入口網站中建立 Azure Media Services 帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="079f9-109">For more information, see [Create an Azure Media Services account in hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="079f9-110">Azure PowerShell 0.8.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="079f9-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="079f9-111">如需詳細資訊，請參閱[如何 toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="079f9-111">For more information, see [How toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="079f9-112">Azure Resource Manager Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="079f9-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="079f9-113">使用 PowerShell 建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="079f9-113">Create an Azure AD app by using PowerShell</span></span>  

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

<span data-ttu-id="079f9-114">如需詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="079f9-114">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="079f9-115">使用 Azure PowerShell toocreate 服務主體 tooaccess 資源</span><span class="sxs-lookup"><span data-stu-id="079f9-115">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="079f9-116">使用 Azure PowerShell 管理角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="079f9-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="079f9-117">Toomanually 藉由使用憑證所設定的精靈應用程式</span><span class="sxs-lookup"><span data-stu-id="079f9-117">How toomanually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="079f9-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="079f9-118">Next steps</span></span>

<span data-ttu-id="079f9-119">開始使用[上傳檔案 tooyour 帳戶](media-services-portal-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="079f9-119">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
