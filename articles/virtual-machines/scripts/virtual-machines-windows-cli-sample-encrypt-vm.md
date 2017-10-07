---
title: "CLI 指令碼範例-aaaAzure 加密 Windows VM |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 將 Windows VM 加密"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 7a9928467f818cd5358d3d19bff5129d8fa21313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a>如何在 Azure 中將 Windows 虛擬機器加密

此指令碼會建立一個安全的 Azure Key Vault、加密金鑰、Azure Active Directory 服務主體，以及 Window 虛擬機器 (VM)。 然後使用 hello 從金鑰保存庫和服務主體認證的加密金鑰來加密 hello VM。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate hello 資源群組中，Azure 金鑰保存庫、 服務主體，虛擬機器，以及所有相關聯的資源。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | 建立 Azure 金鑰保存庫 toostore 安全資料例如加密金鑰。 |
| [az keyvault key create](https://docs.microsoft.com/cli/azure/keyvault/key#create) | 在 Key Vault 中建立加密金鑰。 |
| [az ad sp create-for-rbac](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | 建立 Azure Active Directory 服務主體 toosecurely 驗證與控制存取 tooencryption 金鑰。 |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | 設定權限在 hello 金鑰保存庫 toogrant hello 服務主體存取 tooencryption 索引鍵。 |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | 建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。 此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。  |
| [az vm encryption enable](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | 可讓 VM 使用 hello 服務主體認證和加密金鑰加密。 |
| [az vm encryption show](https://docs.microsoft.com/cli/azure/vm/encryption#show) | 顯示 hello hello VM 加密程序狀態。 |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Windows VM 文件](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json)。
