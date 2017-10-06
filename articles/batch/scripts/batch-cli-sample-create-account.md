---
title: "CLI 指令碼範例-aaaAzure 建立 Batch 帳戶 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立 Batch 帳戶"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a>以 hello Azure CLI 建立 Batch 帳戶

此指令碼會建立 Azure Batch 帳戶，並顯示可以查詢及更新的 hello 帳戶方式的各種屬性。

## <a name="prerequisites"></a>必要條件

安裝 hello Azure CLI 使用 hello 中提供的 hello 指示[Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)，如果您有不這麼做。

## <a name="batch-account-sample-script"></a>Batch 帳戶範例指令碼

當您建立的批次帳戶時，依預設其運算節點會指派內部 hello 批次服務。 配置的運算節點會是主體 tooa 不同的核心配額，可以驗證 hello 帳戶，透過共用金鑰認證或 Azure Active Dirctory 語彙基元。

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>使用使用者訂閱範例指令碼的 Batch 帳戶

您也可以選擇 toohave 批次在您自己的 Azure 訂用帳戶中建立的計算節點。
帳戶配置的計算節點插入您的訂用帳戶必須透過 Azure Active Directory 權杖驗證配置的 hello 計算節點都會計入您的訂用帳戶配額。 toocreate 在此模式中的帳戶，其中一個金鑰保存庫的參考建立時必須指定 hello 帳戶。

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>清除部署

其中一個 hello 上方範例指令碼執行之後，執行下列命令 tooremove hello 的資源群組和所有相關的資源 （包括批次帳戶、 Azure 儲存體帳戶以及 Azure 金鑰保存庫）。

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 批次帳戶和所有相關的資源的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az batch account create](https://docs.microsoft.com/cli/azure/batch/account#create) | 建立 hello Batch 帳戶。  |
| [az batch account set](https://docs.microsoft.com/cli/azure/batch/account#set) | 更新 hello 批次帳戶的屬性。  |
| [az batch account show](https://docs.microsoft.com/cli/azure/batch/account#show) | 指定批次帳戶的 hello 的擷取詳細資料。  |
| [az batch account keys list](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | 擷取 hello 便捷鍵的 hello 指定批次帳戶。  |
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | 驗證指定的 hello 批次帳戶進一步 CLI 互動。  |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | 建立儲存體帳戶。 |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | 建立金鑰保存庫。 |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | 更新 hello 指定的金鑰保存庫的 hello 安全性的原則。 |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他批次 CLI 指令碼範例可以在 hello [Azure 批次 CLI 文件](../batch-cli-samples.md)。
