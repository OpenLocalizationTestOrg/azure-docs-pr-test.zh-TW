---
title: "Azure CLI 指令碼範例 - 輪替儲存體帳戶存取金鑰 | Microsoft Docs"
description: "建立 Azure 儲存體帳戶，然後擷取並輪替其帳戶存取金鑰。"
services: storage
documentationcenter: na
author: tamram
manager: timlt
editor: tysonn
ms.assetid: 
ms.custom: mvc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: sample
ms.date: 06/22/2017
ms.author: tamram
ms.openlocfilehash: c8c99dd8663eab5b5c1c47d34f110f9dceaace6b
ms.sourcegitcommit: 5a6e943718a8d2bc5babea3cd624c0557ab67bd5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="create-a-storage-account-and-rotate-its-account-access-keys"></a>建立儲存體帳戶並輪替其帳戶存取金鑰

此指令碼會建立 Azure 儲存體帳戶、顯示儲存體帳戶的新存取金鑰，然後更新 (輪替) 該金鑰。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/storage/rotate-storage-account-keys/rotate-storage-account-keys.sh "Rotate storage account keys")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令來移除資源群組、儲存體帳戶和所有相關資源。

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令來建立儲存體帳戶，並擷取和輪替其存取金鑰。 下表中的每個項目都會連結至特定命令的文件。

| 命令 | 注意事項 |
|---|---|
| [az group create](/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az storage account create](/cli/azure/storage/account#create) | 在指定的資源群組中建立 Azure 儲存體帳戶。 |
| [az storage account keys list](/cli/azure/storage/account/keys#list) | 顯示指定帳戶的儲存體帳戶存取金鑰。 |
| [az storage account keys renew](/cli/azure/storage/account/keys#renew) | 重新產生主要或次要的儲存體帳戶存取金鑰。 |

## <a name="next-steps"></a>後續步驟

如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](/cli/azure/overview)。

您可以在[適用於 Azure Blob 儲存體的 Azure CLI 範例](../blobs/storage-samples-blobs-cli.md)中，找到其他儲存體 CLI 指令碼範例。
