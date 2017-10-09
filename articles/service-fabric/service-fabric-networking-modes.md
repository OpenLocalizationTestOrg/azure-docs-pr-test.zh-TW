---
title: "網路模式 Azure Service Fabric 容器服務 aaaConfigure |Microsoft 文件"
description: "了解如何 toosetup hello 不同的網路模式，Azure Service Fabric 支援。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 5c5dd4c590c7698a947503cbe8ef66ff7d6b503a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="b7361-103">Service Fabric 容器網路模式</span><span class="sxs-lookup"><span data-stu-id="b7361-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="b7361-104">hello 預設網路模式提供 hello Service Fabric 中容器服務叢集為 hello`nat`網路模式。</span><span class="sxs-lookup"><span data-stu-id="b7361-104">hello default networking mode offered in hello Service Fabric cluster for container services is hello `nat` networking mode.</span></span> <span data-ttu-id="b7361-105">以 hello`nat`網路模式中，有一個以上的容器服務接聽 toohello 相同連接埠會導致部署錯誤。</span><span class="sxs-lookup"><span data-stu-id="b7361-105">With hello `nat` networking mode, having more than one containers service listening toohello same port results in deployment errors.</span></span> <span data-ttu-id="b7361-106">執行數個服務接聽相同的連接埠，Service Fabric 支援的 hello hello`open`網路模式 （5.7 或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="b7361-106">For running several services that listen on hello same port, Service Fabric supports hello `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="b7361-107">以 hello`open`網路模式，每個容器服務取得內部允許多個服務 toolisten toohello 相同的連接埠的動態指派的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b7361-107">With hello `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services toolisten toohello same port.</span></span>   

<span data-ttu-id="b7361-108">因此，靜態端點 hello 服務資訊清單中定義的單一服務類型，與新的服務可能會建立及刪除沒有部署錯誤使用 hello`open`網路模式。</span><span class="sxs-lookup"><span data-stu-id="b7361-108">Thus, with a single service type with a static endpoint defined in hello service manifest, new services may be created and deleted without deployment errors using hello `open` networking mode.</span></span> <span data-ttu-id="b7361-109">同樣地，可以使用相同的 hello`docker-compose.yml`檔案具有靜態連接埠對應建立多個服務。</span><span class="sxs-lookup"><span data-stu-id="b7361-109">Similarly, one can use hello same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="b7361-110">使用動態指派 IP toodiscover 服務的 hello 不建議 hello 的 IP 位址變更自 hello 服務重新啟動或移動 tooanother 節點時。</span><span class="sxs-lookup"><span data-stu-id="b7361-110">Using hello dynamically assigned IP toodiscover services is not advisable since hello IP address changes when hello service restarts or moves tooanother node.</span></span> <span data-ttu-id="b7361-111">只使用 hello **Service Fabric 命名服務**或 hello **DNS 服務**的服務探索。</span><span class="sxs-lookup"><span data-stu-id="b7361-111">Only use hello **Service Fabric Naming Service**  or hello **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="b7361-112">在 Azure 中每個 vNET 僅允許總計 4096 個 IP。</span><span class="sxs-lookup"><span data-stu-id="b7361-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="b7361-113">因此，hello 的 hello 節點數目和 hello 容器服務執行個體數目的總和 (使用`open`網路) 不能超過 4096 vNET 中的。</span><span class="sxs-lookup"><span data-stu-id="b7361-113">Thus, hello sum of hello number of nodes and hello number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="b7361-114">這類適用之高密度的情況下，hello`nat`建議您在網路模式。</span><span class="sxs-lookup"><span data-stu-id="b7361-114">For such high-density scenarios, hello `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="b7361-115">設定開啟網路模式</span><span class="sxs-lookup"><span data-stu-id="b7361-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="b7361-116">啟用 DNS 服務設定 hello Azure Resource Manager 範本和 hello IP 提供者下`fabricSettings`。</span><span class="sxs-lookup"><span data-stu-id="b7361-116">Set up hello Azure Resource Manager template by enabling DNS Service and hello IP Provider under `fabricSettings`.</span></span> 

    ```json
    "fabricSettings": [
                {
                    "name": "DnsService",
                    "parameters": [
                       {
                            "name": "IsEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name": "Hosting",
                    "parameters": [
                      { 
                            "name": "IPProviderEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name":  "Trace/Etw", 
                    "parameters": [
                    {
                            "name": "Level",
                            "value": "5"
                    }
                    ]
                },
                {
                    "name": "Setup",
                    "parameters": [
                    {
                            "name": "ContainerNetworkSetup",
                            "value": "true"
                    }
                    ]
                }
            ],
    ```

2. <span data-ttu-id="b7361-117">設定 hello 網路設定檔區段 tooallow toobe hello 叢集的每個節點上設定的多個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b7361-117">Set up hello network profile section tooallow multiple IP addresses toobe configured on each node of hello cluster.</span></span> <span data-ttu-id="b7361-118">hello 下列範例會設定每個節點的五個 IP 位址 （因此您可以有五個接聽 toohello 連接埠，每個節點上的服務執行個體） 的 Windows Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="b7361-118">hello following example sets up five IP addresses per node (thus you can have five service instances listening toohello port on each node) for a Windows Service Fabric cluster.</span></span>

    ```json
    "variables": {
        "nicName": "NIC",
        "vmName": "vm",
        "virtualNetworkName": "VNet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "vmNodeType0Name": "[toLower(concat('NT1', variables('vmName')))]",
        "subnet0Name": "Subnet-0",
        "subnet0Prefix": "10.0.0.0/24",
        "subnet0Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet0Name'))]",
        "lbID0": "[resourceId('Microsoft.Network/loadBalancers',concat('LB','-', parameters('clusterName'),'-',variables('vmNodeType0Name')))]",
        "lbIPConfig0": "[concat(variables('lbID0'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
        "lbPoolID0": "[concat(variables('lbID0'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
        "lbProbeID0": "[concat(variables('lbID0'),'/probes/FabricGatewayProbe')]",
        "lbHttpProbeID0": "[concat(variables('lbID0'),'/probes/FabricHttpGatewayProbe')]",
        "lbNatPoolID0": "[concat(variables('lbID0'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]"
    }
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

    <span data-ttu-id="b7361-119">適用於 Linux 叢集的其他公用 IP 組態會加入 tooallow 的傳出連線。</span><span class="sxs-lookup"><span data-stu-id="b7361-119">For Linux clusters, an additional public IP configuration is added tooallow outbound connectivity.</span></span> <span data-ttu-id="b7361-120">hello 下列程式碼片段會設定每個 Linux 叢集節點的五個 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="b7361-120">hello following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

    ```json
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "publicipaddressconfiguration": {
                              "name": "devpub",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 1)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 2)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 3)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 4)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 5)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

3. <span data-ttu-id="b7361-121">適用於 Windows 叢集僅設定 NSG 規則 hello vnet 的連接埠 UDP/53 開啟以 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="b7361-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for hello vNET with hello following values:</span></span>

   | <span data-ttu-id="b7361-122">優先順序</span><span class="sxs-lookup"><span data-stu-id="b7361-122">Priority</span></span> |    <span data-ttu-id="b7361-123">名稱</span><span class="sxs-lookup"><span data-stu-id="b7361-123">Name</span></span>    |    <span data-ttu-id="b7361-124">來源</span><span class="sxs-lookup"><span data-stu-id="b7361-124">Source</span></span>      |  <span data-ttu-id="b7361-125">目的地</span><span class="sxs-lookup"><span data-stu-id="b7361-125">Destination</span></span>   |   <span data-ttu-id="b7361-126">服務</span><span class="sxs-lookup"><span data-stu-id="b7361-126">Service</span></span>    | <span data-ttu-id="b7361-127">動作</span><span class="sxs-lookup"><span data-stu-id="b7361-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="b7361-128">2000</span><span class="sxs-lookup"><span data-stu-id="b7361-128">2000</span></span> | <span data-ttu-id="b7361-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="b7361-129">Custom_Dns</span></span> | <span data-ttu-id="b7361-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b7361-130">VirtualNetwork</span></span> | <span data-ttu-id="b7361-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b7361-131">VirtualNetwork</span></span> | <span data-ttu-id="b7361-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="b7361-132">DNS (UDP/53)</span></span> | <span data-ttu-id="b7361-133">允許</span><span class="sxs-lookup"><span data-stu-id="b7361-133">Allow</span></span>  |


4. <span data-ttu-id="b7361-134">指定每個服務的 hello 應用程式資訊清單中的 hello 網路模式`<NetworkConfig NetworkType="open">`。</span><span class="sxs-lookup"><span data-stu-id="b7361-134">Specify hello networking mode in hello app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="b7361-135">hello 模式`open`導致 hello 服務取得專用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b7361-135">hello mode `open` results in hello service getting a dedicated IP address.</span></span> <span data-ttu-id="b7361-136">如果未指定的模式，則預設 toohello 基本`nat`模式。</span><span class="sxs-lookup"><span data-stu-id="b7361-136">If a mode isn't specified, it defaults toohello basic `nat` mode.</span></span> <span data-ttu-id="b7361-137">因此，在下列資訊清單的範例，hello`NodeContainerServicePackage1`和`NodeContainerServicePackage2`可以每個接聽 toohello 相同的連接埠 (這兩個服務都在接聽`Endpoint1`)。</span><span class="sxs-lookup"><span data-stu-id="b7361-137">Thus, in hello following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen toohello same port (both services are listening on `Endpoint1`).</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <ApplicationManifest ApplicationTypeName="NodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Description>Calculator Application</Description>
      <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
        <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
      </Parameters>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage1" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService1.Code" Isolation="hyperv">
           <NetworkConfig NetworkType="open"/>
           <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage2" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService2.Code" Isolation="default">
            <NetworkConfig NetworkType="open"/>
            <PortBinding ContainerPort="8910" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
    </ApplicationManifest>
    ```
<span data-ttu-id="b7361-138">您可以跨 Windows 叢集之應用程式內的服務，混合和比對不同網路模式。</span><span class="sxs-lookup"><span data-stu-id="b7361-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="b7361-139">因此，您可以讓某些服務在 `open` 模式中，以及某些服務在 `nat` 網路模式中。</span><span class="sxs-lookup"><span data-stu-id="b7361-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="b7361-140">當服務設定為`nat`，它會接聽 toomust hello 連接埠是唯一的。</span><span class="sxs-lookup"><span data-stu-id="b7361-140">When a service is configured with `nat`, hello port it is listening toomust be unique.</span></span> <span data-ttu-id="b7361-141">在 Linux 叢集上不支援針對不同服務混合網路模式。</span><span class="sxs-lookup"><span data-stu-id="b7361-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="b7361-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7361-142">Next steps</span></span>
<span data-ttu-id="b7361-143">在本文中，您會了解 Service Fabric 提供的網路模式。</span><span class="sxs-lookup"><span data-stu-id="b7361-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="b7361-144">Service Fabric 應用程式模型</span><span class="sxs-lookup"><span data-stu-id="b7361-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="b7361-145">Service Fabric 服務資訊清單資源</span><span class="sxs-lookup"><span data-stu-id="b7361-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="b7361-146">部署 Windows 容器 tooService 網狀架構上 Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b7361-146">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="b7361-147">部署 Docker 容器 tooService Linux 上的網狀架構</span><span class="sxs-lookup"><span data-stu-id="b7361-147">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
