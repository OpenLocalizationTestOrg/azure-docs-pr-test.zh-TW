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
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a>設定金鑰保存庫使用的虛擬機器的 tooset hello Azure CLI 2.0 的方式

Hello Azure Resource Manager 堆疊中的密碼/憑證會模型化為金鑰保存庫所提供的資源。 toolearn 進一步了解 Azure 金鑰保存庫，請參閱[何謂 Azure Key Vault？](../../key-vault/key-vault-whatis.md) 若要讓 Azure 資源管理員 Vm 搭配使用的金鑰保存庫 toobe，hello *EnabledForDeployment* tootrue 必須設定金鑰保存庫上的屬性。 本文章將示範如何搭配使用 Azure 虛擬機器 (Vm) 使用金鑰保存庫註冊 tooset hello Azure CLI 2.0。 您也可以執行下列步驟以 hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

tooperform 這些步驟，您需要 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。

## <a name="create-a-key-vault"></a>建立金鑰保存庫
建立金鑰保存庫並指派 hello 部署原則與[az keyvault 建立](/cli/azure/keyvault#create)。 hello 下列範例會建立名為金鑰保存庫`myKeyVault`在 hello`myResourceGroup`資源群組：

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a>更新要與 VM 搭配使用的 Key Vault
使用現有的金鑰保存庫上設定 hello 部署原則[az keyvault 更新](/cli/azure/keyvault#update)。 hello 下列更新 hello 名為金鑰保存庫`myKeyVault`在 hello`myResourceGroup`資源群組：

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a>使用金鑰保存庫註冊的範本 tooset
當您使用範本時，您需要 tooset hello`enabledForDeployment`屬性太`true`hello 金鑰保存庫資源，如下所示：

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

## <a name="next-steps"></a>後續步驟
如需使用範本來建立 Key Vault 時可以設定的其他選項，請參閱[建立金鑰保存庫](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)。
