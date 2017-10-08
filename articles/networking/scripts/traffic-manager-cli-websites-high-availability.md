---
title: "CLI 指令碼範例應用程式的高可用性的路由傳送流量 aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例：路由傳送流量以達到應用程式的高可用性"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>路由傳送流量以達到應用程式的高可用性

這個指令碼會建立一個資源群組、兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。 Hello hello 主要區域中的應用程式無法使用時，traffic Manager 將導向流量 toohello 應用程式與 hello 主要區域中，一個區域及 toohello 次要區域。 在執行之前 hello 指令碼，您必須變更 hello MyWebApp，MyWebAppL1 和 MyWebAppL2 值 toounique 值在整個 Azure。 執行 hello 指令碼之後, 您可以存取與 hello URL mywebapp.trafficmanager.net hello 主要區域中的 hello 應用程式。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a>清除部署 

Hello 指令碼範例執行後，hello 後續命令可以使用的 tooremove hello 資源群組，App Service 應用程式，而且所有相關的資源。

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式、 流量管理員設定檔，hello 和所有相關聯的資源。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | 建立 App Service 方案。 這就像是 Azure Web 應用程式的伺服器陣列。 |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#create) | 建立 Azure web 應用程式內 hello 應用程式服務方案。 |
| [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | 建立 Azure 流量管理員設定檔。 |
| [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | 加入端點 tooan Azure 流量管理員設定檔。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 網路文件](../cli-samples.md)。
