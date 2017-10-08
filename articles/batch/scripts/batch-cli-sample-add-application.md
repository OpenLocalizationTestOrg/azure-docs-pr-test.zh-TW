---
title: "aaaAzure CLI 指令碼範例的批次中加入的應用程式 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 在 Batch 中加入應用程式"
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
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a>新增應用程式 tooAzure 批次使用 Azure CLI

此指令碼示範如何 tooset 組成應用程式適用於 Azure Batch 集區或工作。 tooset 組成應用程式，封裝可執行檔，以及任何相依性，成.zip 檔。 在此範例中的 hello 可執行 zip 檔稱為 ' 我的應用程式-exe.zip'。

## <a name="prerequisites"></a>必要條件

- 安裝 hello Azure CLI 使用 hello 中提供的 hello 指示[Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)，如果您有不這麼做。
- 建立 Batch 帳戶 (如果您還沒有帳戶的話)。 請參閱[建立 Batch 帳戶以 hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)建立帳戶的範例指令碼。

## <a name="sample-script"></a>範例指令碼

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a>清除應用程式

執行 hello 上面的範例指令碼之後，執行下列命令 tooremove hello 應用程式和所有其上傳應用程式套件。

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a>指令碼說明

應用程式和上傳應用程式套件，此指令碼會使用下列命令 toocreate hello。
Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az batch application create](https://docs.microsoft.com/cli/azure/batch/application#create) | 建立應用程式。  |
| [az batch application set](https://docs.microsoft.com/cli/azure/batch/application#set) | 更新應用程式的屬性。  |
| [az batch application package create](https://docs.microsoft.com/cli/azure/batch/application/package#create) | 將指定的應用程式封裝 toohello 應用程式。  |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他批次 CLI 指令碼範例可以在 hello [Azure 批次 CLI 文件](../batch-cli-samples.md)。
