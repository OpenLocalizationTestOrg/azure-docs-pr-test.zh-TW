---
title: "在訂用帳戶移動之後變更金鑰保存庫租用戶識別碼 | Microsoft Docs"
description: "了解如何在訂用帳戶移到不同租用戶之後，切換金鑰保存庫的租用戶識別碼"
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
ms.openlocfilehash: 2f007dd4f877b48003cddcefa5f4321049853361
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="19d78-103">在訂用帳戶移動之後變更金鑰保存庫租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="19d78-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-to-tenant-b-how-do-i-change-the-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="19d78-104">問︰我的訂用帳戶已從租用戶 A 移到租用戶 B。如何變更現有金鑰保存庫的租用戶識別碼並且為租用戶 B 中的主體設定正確的 ACL？</span><span class="sxs-lookup"><span data-stu-id="19d78-104">Q: My subscription was moved from tenant A to tenant B. How do I change the tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="19d78-105">當您在訂用帳戶中建立新的金鑰保存庫時，它會自動繫結到該訂用帳戶的預設 Azure Active Directory 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="19d78-105">When you create a new key vault in a subscription, it is automatically tied to the default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="19d78-106">所有存取原則項目也會繫結到此租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="19d78-106">All access policy entries are also tied to this tenant ID.</span></span> <span data-ttu-id="19d78-107">當您將 Azure 訂用帳戶從租用戶 A 移到租用戶 B 時，租用戶 B 中的主體 (使用者和應用程式) 無法存取現有的金鑰保存庫。若要修正這個問題，您需要：</span><span class="sxs-lookup"><span data-stu-id="19d78-107">When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. To fix this issue, you need to:</span></span>

* <span data-ttu-id="19d78-108">將此訂用帳戶中與所有現有金鑰保存庫相關聯的租用戶識別碼變更為租用戶 B。</span><span class="sxs-lookup"><span data-stu-id="19d78-108">Change the tenant ID associated with all existing key vaults in this subscription to tenant B.</span></span>
* <span data-ttu-id="19d78-109">移除所有現有的存取原則項目。</span><span class="sxs-lookup"><span data-stu-id="19d78-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="19d78-110">新增與租用戶 B 相關聯的存取原則項目。</span><span class="sxs-lookup"><span data-stu-id="19d78-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="19d78-111">例如，如果您在已從租用戶 A 移到租用戶 B 的訂用帳戶中有金鑰保存庫 'myvault'，以下就是您變更此金鑰保存庫的租用戶識別碼及移除舊存取原則的方式。</span><span class="sxs-lookup"><span data-stu-id="19d78-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A to tenant B, here's how to change the tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="19d78-112">由於此保存庫在移動前位於租用戶 A 中，所以 **$vault.Properties.TenantId** 的原始值是租用戶 A，而 **(Get-AzureRmContext).Tenant.TenantId** 則是租用戶 B。</span><span class="sxs-lookup"><span data-stu-id="19d78-112">Because this vault was in tenant A before the move, the original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="19d78-113">現在，您的保存庫已與正確的租用戶識別碼相關聯，而且移除了舊的存取原則項目，請使用 [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx)來設定新的存取原則項目。</span><span class="sxs-lookup"><span data-stu-id="19d78-113">Now that your vault is associated with the correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="19d78-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="19d78-114">Next steps</span></span>
<span data-ttu-id="19d78-115">如果您有關於 Azure 金鑰保存庫的問題，請造訪 [Azure 金鑰保存庫論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)。</span><span class="sxs-lookup"><span data-stu-id="19d78-115">If you have questions about Azure Key Vault, visit the [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

