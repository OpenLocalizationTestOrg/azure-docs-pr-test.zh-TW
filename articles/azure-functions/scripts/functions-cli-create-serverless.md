---
title: "aaaAzure CLI 指令碼範例-建立無伺服器執行的函式應用程式 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立無伺服器也可執行的函式應用程式"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a>建立無伺服器也可執行的函式應用程式

此範例指令碼會建立 Azure 函式應用程式，這是您的函式容器。 hello 函式建立應用程式使用 hello[耗用量計劃](../functions-scale.md#consumption-plan)，這很適合使用事件驅動的無伺服器工作負載。

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="sample-script"></a>範例指令碼

此指令碼會建立 Azure 函式應用程式使用 hello[耗用量計劃](../functions-scale.md#consumption-plan)。

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>指令碼說明

Hello 資料表連結 toocommand 特定文件中的每個命令。 此指令碼會使用下列命令的 hello:

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az storage account create](/cli/azure/storage/account#create) | 建立 Azure 儲存體帳戶。 |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#create) | 建立 Azure 函式。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他 Azure 函式 CLI 指令碼範例可以在 hello [Azure 函式文件](../functions-cli-samples.md)。
