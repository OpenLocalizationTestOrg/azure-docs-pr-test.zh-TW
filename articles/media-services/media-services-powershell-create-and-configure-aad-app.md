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
# <a name="use-powershell-to-create-an-azure-ad-app-to-use-with-the-azure-media-services-api"></a><span data-ttu-id="6578a-103">使用 PowerShell 建立 Azure AD 應用程式，以搭配 Azure 媒體服務 API 使用</span><span class="sxs-lookup"><span data-stu-id="6578a-103">Use PowerShell to create an Azure AD app to use with the Azure Media Services API</span></span>

<span data-ttu-id="6578a-104">了解如何使用 PowerShell 指令碼建立 Azure Active Directory (Azure AD) 應用程式和服務主體，以存取 Azure 媒體服務資源。</span><span class="sxs-lookup"><span data-stu-id="6578a-104">Learn how to use a PowerShell script to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="6578a-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="6578a-105">Prerequisites</span></span>

- <span data-ttu-id="6578a-106">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6578a-106">An Azure account.</span></span> <span data-ttu-id="6578a-107">如果您沒有帳戶，請先從 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="6578a-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="6578a-108">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="6578a-108">A Media Services account.</span></span> <span data-ttu-id="6578a-109">如需詳細資訊，請參閱[在 Azure 入口網站建立 Azure 媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="6578a-109">For more information, see [Create an Azure Media Services account in the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="6578a-110">Azure PowerShell 0.8.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6578a-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="6578a-111">如需詳細資訊，請參閱[如何使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="6578a-111">For more information, see [How to use Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="6578a-112">Azure Resource Manager Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6578a-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="6578a-113">使用 PowerShell 建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="6578a-113">Create an Azure AD app by using PowerShell</span></span>  

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

<span data-ttu-id="6578a-114">如需詳細資訊，請參閱下列文章。</span><span class="sxs-lookup"><span data-stu-id="6578a-114">For more information, see the following articles:</span></span>

- [<span data-ttu-id="6578a-115">使用 Azure PowerShell 建立用來存取資源的服務主體</span><span class="sxs-lookup"><span data-stu-id="6578a-115">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="6578a-116">使用 Azure PowerShell 管理角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="6578a-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- <span data-ttu-id="6578a-117">[如何使用憑證手動設定精靈應用程式](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="6578a-117">[How to manually configure daemon apps by using certificates](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6578a-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6578a-118">Next steps</span></span>

<span data-ttu-id="6578a-119">開始使用[上傳檔案至您的帳戶](media-services-portal-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="6578a-119">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
