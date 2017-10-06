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
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a>在訂用帳戶移動之後變更金鑰保存庫租用戶識別碼
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a>問： 我的訂閱已從租用戶 A tootenant B.移動如何變更我現有的金鑰保存庫 hello 租用戶識別碼和正確的 Acl 設定租用戶 B 中的主體？
當您的訂用帳戶中建立新的金鑰保存庫時，它是自動繫結的 toohello 該訂用帳戶預設 Azure Active Directory 租用戶識別碼。 所有存取原則項目也都會採用的 toothis 租用戶識別碼。 當您移動您的 Azure 訂用帳戶時從租用戶 B，您現有的金鑰保存庫都無法存取 tootenant hello 租用戶 b toofix 中的主體 （使用者和應用程式） 這個問題，您需要：

* 變更所有現有金鑰保存庫中此訂用帳戶 tootenant b 相關聯的 hello 租用戶識別碼
* 移除所有現有的存取原則項目。
* 新增與租用戶 B 相關聯的存取原則項目。

例如，如果您在金鑰保存庫 'myvault' 的訂用帳戶已從租用戶 A tootenant B，這裡的移如何 toochange hello 租用戶識別碼，此金鑰保存庫和移除舊的存取原則。

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

由於此保存庫已在租用戶的 hello 移動之前，hello 的原始值**$vault。Properties.TenantId**為租用戶 A while **(Get AzureRmContext)。Tenant.TenantId**是租用戶 b。

現在您的保存庫與 hello 正確租用戶識別碼相關聯，且會移除舊的存取原則項目，設定新的存取原則的項目[Set-azurermkeyvaultaccesspolicy](https://msdn.microsoft.com/library/mt603625.aspx)。

## <a name="next-steps"></a>後續步驟
如果您有關於 Azure 金鑰保存庫的問題，請瀏覽 hello [Azure 金鑰保存庫論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)。

