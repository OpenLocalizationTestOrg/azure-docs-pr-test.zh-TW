---
title: "適用於 Linux Vm 的 Azure 金鑰保存庫註冊 aaaSet |Microsoft 文件"
description: "如何搭配使用 Azure 資源管理員虛擬機器使用金鑰保存庫註冊 tooset hello CLI 2.0。"
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
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a><span data-ttu-id="69937-103">設定金鑰保存庫使用的虛擬機器的 tooset hello Azure CLI 2.0 的方式</span><span class="sxs-lookup"><span data-stu-id="69937-103">How tooset up Key Vault for virtual machines with hello Azure CLI 2.0</span></span>

<span data-ttu-id="69937-104">Hello Azure Resource Manager 堆疊中的密碼/憑證會模型化為金鑰保存庫所提供的資源。</span><span class="sxs-lookup"><span data-stu-id="69937-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="69937-105">toolearn 進一步了解 Azure 金鑰保存庫，請參閱[何謂 Azure Key Vault？](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="69937-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="69937-106">若要讓 Azure 資源管理員 Vm 搭配使用的金鑰保存庫 toobe，hello *EnabledForDeployment* tootrue 必須設定金鑰保存庫上的屬性。</span><span class="sxs-lookup"><span data-stu-id="69937-106">In order for Key Vault toobe used with Azure Resource Manager VMs, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="69937-107">本文章將示範如何搭配使用 Azure 虛擬機器 (Vm) 使用金鑰保存庫註冊 tooset hello Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="69937-107">This article shows you how tooset up Key Vault for use with Azure virtual machines (VMs) using hello Azure CLI 2.0.</span></span> <span data-ttu-id="69937-108">您也可以執行下列步驟以 hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="69937-108">You can also perform these steps with hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="69937-109">tooperform 這些步驟，您需要 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="69937-109">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="69937-110">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="69937-110">Create a Key Vault</span></span>
<span data-ttu-id="69937-111">建立金鑰保存庫並指派 hello 部署原則與[az keyvault 建立](/cli/azure/keyvault#create)。</span><span class="sxs-lookup"><span data-stu-id="69937-111">Create a key vault and assign hello deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="69937-112">hello 下列範例會建立名為金鑰保存庫`myKeyVault`在 hello`myResourceGroup`資源群組：</span><span class="sxs-lookup"><span data-stu-id="69937-112">hello following example creates a key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="69937-113">更新要與 VM 搭配使用的 Key Vault</span><span class="sxs-lookup"><span data-stu-id="69937-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="69937-114">使用現有的金鑰保存庫上設定 hello 部署原則[az keyvault 更新](/cli/azure/keyvault#update)。</span><span class="sxs-lookup"><span data-stu-id="69937-114">Set hello deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="69937-115">hello 下列更新 hello 名為金鑰保存庫`myKeyVault`在 hello`myResourceGroup`資源群組：</span><span class="sxs-lookup"><span data-stu-id="69937-115">hello following updates hello key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="69937-116">使用金鑰保存庫註冊的範本 tooset</span><span class="sxs-lookup"><span data-stu-id="69937-116">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="69937-117">當您使用範本時，您需要 tooset hello`enabledForDeployment`屬性太`true`hello 金鑰保存庫資源，如下所示：</span><span class="sxs-lookup"><span data-stu-id="69937-117">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource as follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="69937-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69937-118">Next steps</span></span>
<span data-ttu-id="69937-119">如需使用範本來建立 Key Vault 時可以設定的其他選項，請參閱[建立金鑰保存庫](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)。</span><span class="sxs-lookup"><span data-stu-id="69937-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
