---
title: "aaaAzure 容器執行個體的多個容器群組 |Azure 文件"
description: "Azure 容器執行個體 - 多容器群組"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 976f578cd2a9bf7f05ab97f24662139bb72062ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-group"></a>部署容器群組

Azure 容器執行個體支援 hello 部署到單一主機使用的多個容器*容器群組*。 在建置應用程式 Sidecar 以便記錄、監視或進行服務需要第二個附加程序的任何其他設定時，這非常有用。 

本文件會逐步解說如何使用 Azure Resource Manager 範本來執行簡單的多容器 Sidecar 設定。

## <a name="configure-hello-template"></a>設定 hello 範本

建立名為`azuredeploy.json`並複製 hello 遵循 json 到其中。 

此範例會定義含有兩個容器和一個公用 IP 位址的容器群組。 hello 的 hello 群組的第一個容器執行網際網路對向應用程式。 hello 第二個容器，hello sidecar 對 HTTP 要求 toohello 主要 web 應用程式透過 hello 群組的本機網路。 

如果確定接收到 200 以外的 HTTP 回應碼，這個 sidecar 範例可能是展開的 tootrigger 警示。 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",    
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
    "resources": [
      {
        "name": "myContainerGroup",
        "type": "Microsoft.ContainerInstance/containerGroups",
        "apiVersion": "2017-08-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
          "containers": [
            {
              "name": "[variables('container1name')]",
              "properties": {
                "image": "[variables('container1image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                },
                "ports": [
                  {
                    "port": 80
                  }
                ]
              }
            },
            {
              "name": "[variables('container2name')]",
              "properties": {
                "image": "[variables('container2image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                }
              }
            }
          ],
          "osType": "Linux",
          "ipAddress": {
            "type": "Public",
            "ports": [
              {
                "protocol": "tcp",
                "port": "80"
              }
            ]
          }
        }
      }
    ],
    "outputs": {
      "containerIPv4Address": {
        "type": "string",
        "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', 'myContainerGroup')).ipAddress.ip]"
      }
    }
  }
```

toouse 私用容器映像登錄中，加入物件 toohello json 文件以 hello 遵循格式。

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a>部署 hello 範本

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

部署以 hello hello 範本[az 群組部署建立](/cli/azure/group/deployment#create)命令。

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

在幾秒內，您就會從 Azure 收到首次的回應。 

## <a name="view-deployment-state"></a>檢視部署狀態

hello 部署，使用 hello tooview hello 狀態`az container show`命令。 這會傳回 hello 佈建應用程式可以存取哪些 hello 透過公用 IP 位址。

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

輸出：

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a>檢視記錄檔   

檢視的容器，使用 hello hello 記錄輸出`az container logs`命令。 hello`--container-name`引數會指定哪些 toopull 記錄檔中的 hello 容器。 在此範例中，指定 hello 第一個容器。 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

輸出：

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

toosee hello 記錄檔中的 hello 端汽車容器、 執行 hello 相同命令指定 hello 第二個容器名稱。

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

輸出：

```bash
Every 3.0s: curl -I http://localhost                                                                                                                       Mon Jul 17 11:27:36 2017

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 1663
Content-Type: text/html; charset=utf-8
Last-Modified: Sun, 16 Jul 2017 02:08:22 GMT
Date: Mon, 17 Jul 2017 18:27:36 GMT
```

如您所見，hello sidecar 定期進行 HTTP 要求 toohello 主要 web 應用程式，透過 hello 群組的本機網路 tooensure 它正在執行。

## <a name="next-steps"></a>後續步驟

本文件涵蓋 hello 部署 Azure 容器執行個體的多個容器所需的步驟。 Azure 容器執行個體遇到結束 tooend，請參閱 hello Azure 容器執行個體教學課程。

> [!div class="nextstepaction"]
> [Azure 容器執行個體教學課程]: ./container-instances-tutorial-prepare-app.md
