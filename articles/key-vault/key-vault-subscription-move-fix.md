---
title: "aaaChange hello 金鑰保存庫租用戶識別碼之後移動訂用帳戶 |Microsoft 文件"
description: "了解如何為金鑰保存庫的訂用帳戶之後 tooswitch hello 租用戶識別碼移動 tooa 不同的租用戶"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 4d0607208c61c57959439d2d0bd8feade4141fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="e5a7b-103">在訂用帳戶移動之後變更金鑰保存庫租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="e5a7b-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="e5a7b-104">問： 我的訂閱已從租用戶 A tootenant B.移動如何變更我現有的金鑰保存庫 hello 租用戶識別碼和正確的 Acl 設定租用戶 B 中的主體？</span><span class="sxs-lookup"><span data-stu-id="e5a7b-104">Q: My subscription was moved from tenant A tootenant B. How do I change hello tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="e5a7b-105">當您的訂用帳戶中建立新的金鑰保存庫時，它是自動繫結的 toohello 該訂用帳戶預設 Azure Active Directory 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="e5a7b-105">When you create a new key vault in a subscription, it is automatically tied toohello default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="e5a7b-106">所有存取原則項目也都會採用的 toothis 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="e5a7b-106">All access policy entries are also tied toothis tenant ID.</span></span> <span data-ttu-id="e5a7b-107">當您移動您的 Azure 訂用帳戶時從租用戶 B，您現有的金鑰保存庫都無法存取 tootenant hello 租用戶 b toofix 中的主體 （使用者和應用程式） 這個問題，您需要：</span><span class="sxs-lookup"><span data-stu-id="e5a7b-107">When you move your Azure subscription from tenant A tootenant B, your existing key vaults are inaccessible by hello principals (users and applications) in tenant B. toofix this issue, you need to:</span></span>

* <span data-ttu-id="e5a7b-108">變更所有現有金鑰保存庫中此訂用帳戶 tootenant b 相關聯的 hello 租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="e5a7b-108">Change hello tenant ID associated with all existing key vaults in this subscription tootenant B.</span></span>
* <span data-ttu-id="e5a7b-109">移除所有現有的存取原則項目。</span><span class="sxs-lookup"><span data-stu-id="e5a7b-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="e5a7b-110">新增與租用戶 B 相關聯的存取原則項目。</span><span class="sxs-lookup"><span data-stu-id="e5a7b-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="e5a7b-111">例如，如果您在金鑰保存庫 'myvault' 的訂用帳戶已從租用戶 A tootenant B，這裡的移如何 toochange hello 租用戶識別碼，此金鑰保存庫和移除舊的存取原則。</span><span class="sxs-lookup"><span data-stu-id="e5a7b-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A tootenant B, here's how toochange hello tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="e5a7b-112">由於此保存庫已在租用戶的 hello 移動之前，hello 的原始值**$vault。Properties.TenantId**為租用戶 A while **(Get AzureRmContext)。Tenant.TenantId**是租用戶 b。</span><span class="sxs-lookup"><span data-stu-id="e5a7b-112">Because this vault was in tenant A before hello move, hello original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="e5a7b-113">現在您的保存庫與 hello 正確租用戶識別碼相關聯，且會移除舊的存取原則項目，設定新的存取原則的項目[Set-azurermkeyvaultaccesspolicy](https://msdn.microsoft.com/library/mt603625.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e5a7b-113">Now that your vault is associated with hello correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5a7b-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e5a7b-114">Next steps</span></span>
<span data-ttu-id="e5a7b-115">如果您有關於 Azure 金鑰保存庫的問題，請瀏覽 hello [Azure 金鑰保存庫論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)。</span><span class="sxs-lookup"><span data-stu-id="e5a7b-115">If you have questions about Azure Key Vault, visit hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

