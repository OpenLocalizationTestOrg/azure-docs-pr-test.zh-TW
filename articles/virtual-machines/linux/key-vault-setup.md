---
title: "設定 Linux VM 的 Azure Key Vault | Microsoft Docs"
description: "如何使用 CLI 2.0 設定要與 Azure Resource Manager 虛擬機器搭配使用的 Key Vault。"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 2cc9b4c978e9a4deb0c8443c4b0f9e301a7cf492
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-key-vault-for-virtual-machines-with-the-azure-cli-20"></a><span data-ttu-id="25ad1-103">如何使用 Azure CLI 2.0 設定虛擬機器的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="25ad1-103">How to set up Key Vault for virtual machines with the Azure CLI 2.0</span></span>

<span data-ttu-id="25ad1-104">在 Azure Resource Manager 堆疊中，密碼/憑證會被塑造成 Key Vault 所提供的資源。</span><span class="sxs-lookup"><span data-stu-id="25ad1-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="25ad1-105">若要深入了解「Azure 金鑰保存庫」，請參閱 [什麼是 Azure 金鑰保存庫？](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="25ad1-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="25ad1-106">為了讓 Key Vault 能與 Azure Resource Manager VM 搭配使用，必須將「金鑰保存庫」上的 *EnabledForDeployment* 屬性設定為 true。</span><span class="sxs-lookup"><span data-stu-id="25ad1-106">In order for Key Vault to be used with Azure Resource Manager VMs, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="25ad1-107">本文說明如何使用 Azure CLI 2.0 設定要與 Azure 虛擬機器 (VM) 搭配使用的 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="25ad1-107">This article shows you how to set up Key Vault for use with Azure virtual machines (VMs) using the Azure CLI 2.0.</span></span> <span data-ttu-id="25ad1-108">您也可以使用 [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="25ad1-108">You can also perform these steps with the [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="25ad1-109">若要執行這些步驟，您需要安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並且使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="25ad1-109">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="25ad1-110">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="25ad1-110">Create a Key Vault</span></span>
<span data-ttu-id="25ad1-111">使用 [az keyvault create](/cli/azure/keyvault#create) 建立金鑰保存庫並指派部署原則。</span><span class="sxs-lookup"><span data-stu-id="25ad1-111">Create a key vault and assign the deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="25ad1-112">下列範例會在 `myResourceGroup` 資源群組中建立名為 `myKeyVault` 的金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="25ad1-112">The following example creates a key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="25ad1-113">更新要與 VM 搭配使用的 Key Vault</span><span class="sxs-lookup"><span data-stu-id="25ad1-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="25ad1-114">使用 [az keyvault update](/cli/azure/keyvault#update) 對現有的金鑰保存庫設定部署原則。</span><span class="sxs-lookup"><span data-stu-id="25ad1-114">Set the deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="25ad1-115">下列範例會更新 `myResourceGroup` 資源群組中名為 `myKeyVault` 的金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="25ad1-115">The following updates the key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="25ad1-116">使用範本來設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="25ad1-116">Use templates to set up Key Vault</span></span>
<span data-ttu-id="25ad1-117">當您使用範本時，您需要針對 Key Vault 資源將 `enabledForDeployment` 屬性設定為 `true`，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="25ad1-117">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource as follows:</span></span>

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="25ad1-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="25ad1-118">Next steps</span></span>
<span data-ttu-id="25ad1-119">如需使用範本來建立 Key Vault 時可以設定的其他選項，請參閱[建立金鑰保存庫](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)。</span><span class="sxs-lookup"><span data-stu-id="25ad1-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
