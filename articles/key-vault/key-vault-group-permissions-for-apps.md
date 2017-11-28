---
title: "aaaGrant 權限 toomany 應用程式 tooaccess Azure key vault |Microsoft 文件"
description: "了解 toogrant 權限 toomany 應用程式 tooaccess 金鑰的保存庫"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 785d4e40-fb7b-485a-8cbc-d9c8c87708e6
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: ambapat
ms.openlocfilehash: 5258149f939856f91b3848fc50399e58e5894f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a><span data-ttu-id="13e79-103">授與權限 toomany 應用程式 tooaccess 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="13e79-103">Grant permission toomany applications tooaccess a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="13e79-104">問： 我有數個 （超過 16 個） 需要 tooaccess 金鑰保存庫的應用程式。</span><span class="sxs-lookup"><span data-stu-id="13e79-104">Q: I have several (over 16) applications that need tooaccess a key vault.</span></span> <span data-ttu-id="13e79-105">因為 Key Vault 只允許 16 個存取控制項目，我該如何達成此目的？</span><span class="sxs-lookup"><span data-stu-id="13e79-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="13e79-106">Key Vault 存取控制原則只支援 16 個項目。</span><span class="sxs-lookup"><span data-stu-id="13e79-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="13e79-107">不過，您可以建立 Azure Active Directory 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="13e79-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="13e79-108">加入所有 hello 建立關聯的服務主體 toothis 安全性群組，然後授與存取 toothis 安全性群組 tooKey 保存庫。</span><span class="sxs-lookup"><span data-stu-id="13e79-108">Add all hello associated service principals toothis security group and then grant access toothis security group tooKey Vault.</span></span>

<span data-ttu-id="13e79-109">以下是 hello 先決條件：</span><span class="sxs-lookup"><span data-stu-id="13e79-109">Here are hello pre-requisites:</span></span>
* <span data-ttu-id="13e79-110">[安裝 Azure Active Directory V2 PowerShell 模組](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30)。</span><span class="sxs-lookup"><span data-stu-id="13e79-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="13e79-111">[安裝 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="13e79-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="13e79-112">toorun hello 下列命令，您需要在 hello Azure Active Directory 租用戶中的權限 toocreate/編輯群組。</span><span class="sxs-lookup"><span data-stu-id="13e79-112">toorun hello following commands, you need permissions toocreate/edit groups in hello Azure Active Directory tenant.</span></span> <span data-ttu-id="13e79-113">如果您沒有權限，您可能需要 toocontact 您的 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="13e79-113">If you don't have permissions, you may need toocontact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="13e79-114">現在，執行下列命令在 PowerShell 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="13e79-114">Now run hello following commands in PowerShell.</span></span>

```powershell
# Connect tooAzure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members toothis group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members toothis group, in this fashion. 
 
# Set hello Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust hello permissions as required 
```

<span data-ttu-id="13e79-115">如果您需要 toogrant 一組不同的應用程式的權限 tooa 群組，建立個別 Azure Active Directory 安全性群組之類的應用程式。</span><span class="sxs-lookup"><span data-stu-id="13e79-115">If you need toogrant a different set of permissions tooa group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13e79-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13e79-116">Next steps</span></span>

<span data-ttu-id="13e79-117">深入了解如何太[安全金鑰保存庫](key-vault-secure-your-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="13e79-117">Learn more about how too[Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
