---
title: "設定 Azure Service Fabric 容器服務的網路模式 | Microsoft Docs"
description: "了解如何設定 Azure Service Fabric 支援的不同網路模式。"
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
ms.openlocfilehash: f792f9604a5d6e62551ed92c1049d6e2b4216417
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="a1a03-103">Service Fabric 容器網路模式</span><span class="sxs-lookup"><span data-stu-id="a1a03-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="a1a03-104">容器服務之 Service Fabric 叢集中提供的預設網路模式是 `nat` 網路模式。</span><span class="sxs-lookup"><span data-stu-id="a1a03-104">The default networking mode offered in the Service Fabric cluster for container services is the `nat` networking mode.</span></span> <span data-ttu-id="a1a03-105">使用 `nat` 網路模式，讓一個以上的容器服務接聽相同連接埠會導致部署錯誤。</span><span class="sxs-lookup"><span data-stu-id="a1a03-105">With the `nat` networking mode, having more than one containers service listening to the same port results in deployment errors.</span></span> <span data-ttu-id="a1a03-106">為了執行在相同通訊埠上接聽的數個服務，Service Fabric 支援 `open` 網路模式 (5.7 版或更高版本)。</span><span class="sxs-lookup"><span data-stu-id="a1a03-106">For running several services that listen on the same port, Service Fabric supports the `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="a1a03-107">使用 `open` 網路模式，每個容器服務會取得動態指派 IP 位址，在內部允許多個服務接聽相同的連接埠。</span><span class="sxs-lookup"><span data-stu-id="a1a03-107">With the `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services to listen to the same port.</span></span>   

<span data-ttu-id="a1a03-108">因此，使用單一服務類型 (具有在服務資訊清單中定義的靜態端點)，就可以使用 `open` 網路模式建立和刪除新的服務，而不會造成部署錯誤。</span><span class="sxs-lookup"><span data-stu-id="a1a03-108">Thus, with a single service type with a static endpoint defined in the service manifest, new services may be created and deleted without deployment errors using the `open` networking mode.</span></span> <span data-ttu-id="a1a03-109">同樣地，可以使用相同 `docker-compose.yml` 檔案 (具有靜態連接埠對應) 來建立多個服務。</span><span class="sxs-lookup"><span data-stu-id="a1a03-109">Similarly, one can use the same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="a1a03-110">不建議使用動態指派 IP 來探索服務，因為當服務重新啟動或移至其他節點時，IP 位址會變更。</span><span class="sxs-lookup"><span data-stu-id="a1a03-110">Using the dynamically assigned IP to discover services is not advisable since the IP address changes when the service restarts or moves to another node.</span></span> <span data-ttu-id="a1a03-111">只使用 **Service Fabric 命名服務**或 **DNS 服務**來進行服務探索。</span><span class="sxs-lookup"><span data-stu-id="a1a03-111">Only use the **Service Fabric Naming Service**  or the **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="a1a03-112">在 Azure 中每個 vNET 僅允許總計 4096 個 IP。</span><span class="sxs-lookup"><span data-stu-id="a1a03-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="a1a03-113">因此，節點數目和容器服務執行個體數目的總和 (使用 `open` 網路) 在 vNET 中不能超過 4096 個。</span><span class="sxs-lookup"><span data-stu-id="a1a03-113">Thus, the sum of the number of nodes and the number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="a1a03-114">對於這類高密度案例，建議使用 `nat` 網路模式。</span><span class="sxs-lookup"><span data-stu-id="a1a03-114">For such high-density scenarios, the `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="a1a03-115">設定開啟網路模式</span><span class="sxs-lookup"><span data-stu-id="a1a03-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="a1a03-116">藉由啟用 `fabricSettings` 下的 DNS 服務和 IP 提供者，設定 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="a1a03-116">Set up the Azure Resource Manager template by enabling DNS Service and the IP Provider under `fabricSettings`.</span></span> 

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

2. <span data-ttu-id="a1a03-117">設定網路設定檔區段，以允許在叢集的每個節點上設定多個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a1a03-117">Set up the network profile section to allow multiple IP addresses to be configured on each node of the cluster.</span></span> <span data-ttu-id="a1a03-118">下列範例會針對 Windows Service Fabric 叢集，在每個節點上設定五個 IP 位址 (因此您可以有五個服務執行個體接聽每個節點上的連接埠)。</span><span class="sxs-lookup"><span data-stu-id="a1a03-118">The following example sets up five IP addresses per node (thus you can have five service instances listening to the port on each node) for a Windows Service Fabric cluster.</span></span>

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

    <span data-ttu-id="a1a03-119">對於 Linux 叢集，會新增額外公用 IP 設定以允許輸出連線。</span><span class="sxs-lookup"><span data-stu-id="a1a03-119">For Linux clusters, an additional public IP configuration is added to allow outbound connectivity.</span></span> <span data-ttu-id="a1a03-120">下列程式碼片段會針對 Linux 叢集的每個節點設定五個 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="a1a03-120">The following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

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

3. <span data-ttu-id="a1a03-121">僅適用於 Windows 叢集，使用下列值設定 NSG 規則，以開啟 vNET 的連接埠 UDP/53：</span><span class="sxs-lookup"><span data-stu-id="a1a03-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for the vNET with the following values:</span></span>

   | <span data-ttu-id="a1a03-122">優先順序</span><span class="sxs-lookup"><span data-stu-id="a1a03-122">Priority</span></span> |    <span data-ttu-id="a1a03-123">名稱</span><span class="sxs-lookup"><span data-stu-id="a1a03-123">Name</span></span>    |    <span data-ttu-id="a1a03-124">來源</span><span class="sxs-lookup"><span data-stu-id="a1a03-124">Source</span></span>      |  <span data-ttu-id="a1a03-125">目的地</span><span class="sxs-lookup"><span data-stu-id="a1a03-125">Destination</span></span>   |   <span data-ttu-id="a1a03-126">服務</span><span class="sxs-lookup"><span data-stu-id="a1a03-126">Service</span></span>    | <span data-ttu-id="a1a03-127">動作</span><span class="sxs-lookup"><span data-stu-id="a1a03-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="a1a03-128">2000</span><span class="sxs-lookup"><span data-stu-id="a1a03-128">2000</span></span> | <span data-ttu-id="a1a03-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="a1a03-129">Custom_Dns</span></span> | <span data-ttu-id="a1a03-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="a1a03-130">VirtualNetwork</span></span> | <span data-ttu-id="a1a03-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="a1a03-131">VirtualNetwork</span></span> | <span data-ttu-id="a1a03-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="a1a03-132">DNS (UDP/53)</span></span> | <span data-ttu-id="a1a03-133">允許</span><span class="sxs-lookup"><span data-stu-id="a1a03-133">Allow</span></span>  |


4. <span data-ttu-id="a1a03-134">在應用程式資訊清單中為每個服務指定網路模式 `<NetworkConfig NetworkType="open">`。</span><span class="sxs-lookup"><span data-stu-id="a1a03-134">Specify the networking mode in the app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="a1a03-135">模式 `open` 會導致服務取得專用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a1a03-135">The mode `open` results in the service getting a dedicated IP address.</span></span> <span data-ttu-id="a1a03-136">如果未指定模式，則會預設為基本 `nat` 模式。</span><span class="sxs-lookup"><span data-stu-id="a1a03-136">If a mode isn't specified, it defaults to the basic `nat` mode.</span></span> <span data-ttu-id="a1a03-137">因此，在下列資訊清單範例中，`NodeContainerServicePackage1` 和 `NodeContainerServicePackage2` 可以分別接聽相同通訊埠 (這兩個服務都會在 `Endpoint1` 上接聽)。</span><span class="sxs-lookup"><span data-stu-id="a1a03-137">Thus, in the following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen to the same port (both services are listening on `Endpoint1`).</span></span>

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
<span data-ttu-id="a1a03-138">您可以跨 Windows 叢集之應用程式內的服務，混合和比對不同網路模式。</span><span class="sxs-lookup"><span data-stu-id="a1a03-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="a1a03-139">因此，您可以讓某些服務在 `open` 模式中，以及某些服務在 `nat` 網路模式中。</span><span class="sxs-lookup"><span data-stu-id="a1a03-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="a1a03-140">當使用 `nat` 設定服務時，接聽的連接埠必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="a1a03-140">When a service is configured with `nat`, the port it is listening to must be unique.</span></span> <span data-ttu-id="a1a03-141">在 Linux 叢集上不支援針對不同服務混合網路模式。</span><span class="sxs-lookup"><span data-stu-id="a1a03-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="a1a03-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1a03-142">Next steps</span></span>
<span data-ttu-id="a1a03-143">在本文中，您會了解 Service Fabric 提供的網路模式。</span><span class="sxs-lookup"><span data-stu-id="a1a03-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="a1a03-144">Service Fabric 應用程式模型</span><span class="sxs-lookup"><span data-stu-id="a1a03-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="a1a03-145">Service Fabric 服務資訊清單資源</span><span class="sxs-lookup"><span data-stu-id="a1a03-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="a1a03-146">將 Windows 容器部署至 Windows Server 2016 上的 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a1a03-146">Deploy a Windows container to Service Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="a1a03-147">將 Docker 容器部署至 Linux 上的 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a1a03-147">Deploy a Docker container to Service Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
