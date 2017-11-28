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
# <a name="deploy-a-container-group"></a><span data-ttu-id="35183-103">部署容器群組</span><span class="sxs-lookup"><span data-stu-id="35183-103">Deploy a container group</span></span>

<span data-ttu-id="35183-104">Azure 容器執行個體支援 hello 部署到單一主機使用的多個容器*容器群組*。</span><span class="sxs-lookup"><span data-stu-id="35183-104">Azure Container Instances support hello deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="35183-105">在建置應用程式 Sidecar 以便記錄、監視或進行服務需要第二個附加程序的任何其他設定時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="35183-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="35183-106">本文件會逐步解說如何使用 Azure Resource Manager 範本來執行簡單的多容器 Sidecar 設定。</span><span class="sxs-lookup"><span data-stu-id="35183-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-hello-template"></a><span data-ttu-id="35183-107">設定 hello 範本</span><span class="sxs-lookup"><span data-stu-id="35183-107">Configure hello template</span></span>

<span data-ttu-id="35183-108">建立名為`azuredeploy.json`並複製 hello 遵循 json 到其中。</span><span class="sxs-lookup"><span data-stu-id="35183-108">Create a file named `azuredeploy.json` and copy hello following json into it.</span></span> 

<span data-ttu-id="35183-109">此範例會定義含有兩個容器和一個公用 IP 位址的容器群組。</span><span class="sxs-lookup"><span data-stu-id="35183-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="35183-110">hello 的 hello 群組的第一個容器執行網際網路對向應用程式。</span><span class="sxs-lookup"><span data-stu-id="35183-110">hello first container of hello group runs an internet facing application.</span></span> <span data-ttu-id="35183-111">hello 第二個容器，hello sidecar 對 HTTP 要求 toohello 主要 web 應用程式透過 hello 群組的本機網路。</span><span class="sxs-lookup"><span data-stu-id="35183-111">hello second container, hello sidecar, makes an HTTP request toohello main web application via hello group's local network.</span></span> 

<span data-ttu-id="35183-112">如果確定接收到 200 以外的 HTTP 回應碼，這個 sidecar 範例可能是展開的 tootrigger 警示。</span><span class="sxs-lookup"><span data-stu-id="35183-112">This sidecar example could be expanded tootrigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

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

<span data-ttu-id="35183-113">toouse 私用容器映像登錄中，加入物件 toohello json 文件以 hello 遵循格式。</span><span class="sxs-lookup"><span data-stu-id="35183-113">toouse a private container image registry, add an object toohello json document with hello following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a><span data-ttu-id="35183-114">部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="35183-114">Deploy hello template</span></span>

<span data-ttu-id="35183-115">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="35183-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="35183-116">部署以 hello hello 範本[az 群組部署建立](/cli/azure/group/deployment#create)命令。</span><span class="sxs-lookup"><span data-stu-id="35183-116">Deploy hello template with hello [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="35183-117">在幾秒內，您就會從 Azure 收到首次的回應。</span><span class="sxs-lookup"><span data-stu-id="35183-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="35183-118">檢視部署狀態</span><span class="sxs-lookup"><span data-stu-id="35183-118">View deployment state</span></span>

<span data-ttu-id="35183-119">hello 部署，使用 hello tooview hello 狀態`az container show`命令。</span><span class="sxs-lookup"><span data-stu-id="35183-119">tooview hello state of hello deployment, use hello `az container show` command.</span></span> <span data-ttu-id="35183-120">這會傳回 hello 佈建應用程式可以存取哪些 hello 透過公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="35183-120">This returns hello provisioned public IP address over which hello application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="35183-121">輸出：</span><span class="sxs-lookup"><span data-stu-id="35183-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="35183-122">檢視記錄檔</span><span class="sxs-lookup"><span data-stu-id="35183-122">View logs</span></span>   

<span data-ttu-id="35183-123">檢視的容器，使用 hello hello 記錄輸出`az container logs`命令。</span><span class="sxs-lookup"><span data-stu-id="35183-123">View hello log output of a container using hello `az container logs` command.</span></span> <span data-ttu-id="35183-124">hello`--container-name`引數會指定哪些 toopull 記錄檔中的 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="35183-124">hello `--container-name` argument specifies hello container from which toopull logs.</span></span> <span data-ttu-id="35183-125">在此範例中，指定 hello 第一個容器。</span><span class="sxs-lookup"><span data-stu-id="35183-125">In this example, hello first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="35183-126">輸出：</span><span class="sxs-lookup"><span data-stu-id="35183-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="35183-127">toosee hello 記錄檔中的 hello 端汽車容器、 執行 hello 相同命令指定 hello 第二個容器名稱。</span><span class="sxs-lookup"><span data-stu-id="35183-127">toosee hello logs for hello side-car container, run hello same command specifying hello second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="35183-128">輸出：</span><span class="sxs-lookup"><span data-stu-id="35183-128">Output:</span></span>

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

<span data-ttu-id="35183-129">如您所見，hello sidecar 定期進行 HTTP 要求 toohello 主要 web 應用程式，透過 hello 群組的本機網路 tooensure 它正在執行。</span><span class="sxs-lookup"><span data-stu-id="35183-129">As you can see, hello sidecar is periodically making an HTTP request toohello main web application via hello group's local network tooensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35183-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35183-130">Next steps</span></span>

<span data-ttu-id="35183-131">本文件涵蓋 hello 部署 Azure 容器執行個體的多個容器所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="35183-131">This document covered hello steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="35183-132">Azure 容器執行個體遇到結束 tooend，請參閱 hello Azure 容器執行個體教學課程。</span><span class="sxs-lookup"><span data-stu-id="35183-132">For an end tooend Azure Container Instances experience, see hello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="35183-133">[Azure 容器執行個體教學課程]: ./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="35183-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>
