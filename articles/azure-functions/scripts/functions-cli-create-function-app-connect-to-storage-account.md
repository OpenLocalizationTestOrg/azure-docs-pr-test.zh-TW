---
title: "建立連線至 Azure 儲存體的 Azure 函式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立連線至 Azure 儲存體的 Azure 函式"
services: functions
documentationcenter: functions
author: ggailey777
manager: cfowler
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 363a3fd1c80538495658720274840b921baa8675
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/29/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a>將函式應用程式整合到 Azure 儲存體帳戶

此範例指令碼會建立函數應用程式和儲存體帳戶。

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您在本機使用 CLI，請確定您是執行 Azure CLI 2.0 版或更新版本。 若要尋找版本，請執行 `az --version`。 如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。 

## <a name="sample-script"></a>範例指令碼

此範例會建立 Azure 函數應用程式，然後將儲存體連接字串新增至應用程式設定。

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a>清除部署

在執行過指令碼範例之後，請執行下列命令來移除資源群組和所有相關資源：

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令。 下表中的每個命令都會連結至命令特定的文件。

| 命令 | 注意事項 |
|---|---|
| [az login](https://docs.microsoft.com/cli/azure/#login) | 登入 Azure。 |
| [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create) | 指定位置建立資源群組 |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account) | 建立儲存體帳戶 |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#az_functionapp_create) | 建立新的函式應用程式 |
| [az group delete](https://docs.microsoft.com/cli/azure/group#az_group_delete) | 清除 |

## <a name="next-steps"></a>後續步驟

如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以在 [Azure Functions 文件](../functions-cli-samples.md)中找到其他 Azure Functions CLI 指令碼範例。
