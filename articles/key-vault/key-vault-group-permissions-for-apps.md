---
title: "對許多應用程式授與 Azure 金鑰保存庫的存取權限 | Microsoft Docs"
description: "了解如何對許多應用程式授與金鑰保存庫的存取權限"
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
ms.openlocfilehash: f58b633de2e4b5702ff2df9b3722662b09510200
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permission-to-many-applications-to-access-a-key-vault"></a><span data-ttu-id="75b2d-103">對許多應用程式授與金鑰保存庫的存取權限</span><span class="sxs-lookup"><span data-stu-id="75b2d-103">Grant permission to many applications to access a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-to-access-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="75b2d-104">問︰我有許多 (超過 16 個) 應用程式需要存取金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="75b2d-104">Q: I have several (over 16) applications that need to access a key vault.</span></span> <span data-ttu-id="75b2d-105">因為 Key Vault 只允許 16 個存取控制項目，我該如何達成此目的？</span><span class="sxs-lookup"><span data-stu-id="75b2d-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="75b2d-106">Key Vault 存取控制原則只支援 16 個項目。</span><span class="sxs-lookup"><span data-stu-id="75b2d-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="75b2d-107">不過，您可以建立 Azure Active Directory 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="75b2d-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="75b2d-108">將所有相關聯的服務主體新增至這個安全性群組，然後對 Key Vault 授與此安全性群組的存取權。</span><span class="sxs-lookup"><span data-stu-id="75b2d-108">Add all the associated service principals to this security group and then grant access to this security group to Key Vault.</span></span>

<span data-ttu-id="75b2d-109">必要條件如下︰</span><span class="sxs-lookup"><span data-stu-id="75b2d-109">Here are the pre-requisites:</span></span>
* <span data-ttu-id="75b2d-110">[安裝 Azure Active Directory V2 PowerShell 模組](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30)。</span><span class="sxs-lookup"><span data-stu-id="75b2d-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="75b2d-111">[安裝 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="75b2d-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="75b2d-112">若要執行下列命令，您需要在 Azure Active Directory 租用戶中建立/編輯群組的權限。</span><span class="sxs-lookup"><span data-stu-id="75b2d-112">To run the following commands, you need permissions to create/edit groups in the Azure Active Directory tenant.</span></span> <span data-ttu-id="75b2d-113">如果您沒有權限，則可能需要連絡 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="75b2d-113">If you don't have permissions, you may need to contact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="75b2d-114">現在在 PowerShell 中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="75b2d-114">Now run the following commands in PowerShell.</span></span>

```powershell
# Connect to Azure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members to this group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members to this group, in this fashion. 
 
# Set the Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust the permissions as required 
```

<span data-ttu-id="75b2d-115">如果您需要對一組應用程式授與一組不同的權限，請為這些應用程式另外建立一個 Azure Active Directory 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="75b2d-115">If you need to grant a different set of permissions to a group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75b2d-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75b2d-116">Next steps</span></span>

<span data-ttu-id="75b2d-117">深入了解如何[保護您的金鑰保存庫](key-vault-secure-your-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="75b2d-117">Learn more about how to [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
