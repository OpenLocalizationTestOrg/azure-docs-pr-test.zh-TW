---
title: "aaaAzure CLI 指令碼範例-將繫結的自訂 SSL 憑證 tooa 函式應用程式 |Microsoft 文件"
description: "Azure CLI 指令碼範例-繫結的自訂 SSL 憑證 tooa 函式應用程式在 Azure 中"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a>繫結的自訂 SSL 憑證 tooa 函式應用程式

這個範例指令碼應用程式服務中建立函數應用程式及其相關資源，然後將自訂網域名稱 tooit 的 hello SSL 憑證繫結。 針對此範例，您需要：

* 存取 tooyour 網域註冊機構的 DNS 設定 頁面。
* 有效。PFX 檔案並將其密碼的 hello SSL 憑證想 tooupload 並繫結。

toobind SSL 憑證，必須建立函式應用程式，App Service 方案中，而不是在耗用量計劃。

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | 建立應用程式服務計劃所需 toobind SSL 憑證。 |
| [az functionapp create]() | 建立函式應用程式。 |
| [az appservice web config hostname add](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | 將對應的自訂網域 toohello 函式應用程式。 |
| [az appservice web config ssl upload](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | 上傳 SSL 憑證 tooa 函式應用程式。 |
| [az appservice web config ssl upload](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | 將繫結上傳的 SSL 憑證 tooa 函式應用程式。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件]()。
