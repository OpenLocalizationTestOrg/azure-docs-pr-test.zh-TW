---
title: "建立叢集的 Azure Load Balancer 規則"
description: "設定 Azure Load Balancer 來開啟 Azure Service Fabric 叢集的連接埠。"
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: c99c4d9f343ca97fd3cd363fb54feaf5507bb77c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="e25cb-103">開啟 Service Fabric 叢集的連接埠</span><span class="sxs-lookup"><span data-stu-id="e25cb-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="e25cb-104">此負載平衡器會隨 Azure Service Fabric 叢集一起部署，以將流量導向至節點上所執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e25cb-104">The load balancer deployed with your Azure Service Fabric cluster directs traffic to your app running on a node.</span></span> <span data-ttu-id="e25cb-105">如果您變更應用程式以使用不同的連接埠，您必須在 Azure Load Balancer 中公開該連接埠 (或路由不同的連接埠)。</span><span class="sxs-lookup"><span data-stu-id="e25cb-105">If you change your app to use a different port, you must expose that port (or route a different port) in the Azure Load Balancer.</span></span>

<span data-ttu-id="e25cb-106">當您將 Service Fabric 叢集部署至 Azure 時，系統會自動為您建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e25cb-106">When you deployed your service fabric cluster to Azure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="e25cb-107">如果您沒有負載平衡器，請參閱[設定網際網路面向的負載平衡器](..\load-balancer\load-balancer-get-started-internet-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e25cb-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="e25cb-108">設定 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e25cb-108">Configure service fabric</span></span>

<span data-ttu-id="e25cb-109">您的 Service Fabric 應用程式 **ServiceManifest.xml** 設定檔會定義應用程式預期使用的端點。</span><span class="sxs-lookup"><span data-stu-id="e25cb-109">Your Service Fabric application **ServiceManifest.xml** config file defines the endpoints your application expects to use.</span></span> <span data-ttu-id="e25cb-110">在更新設定檔以定義端點之後，必須更新負載平衡器以公開該連接埠 (或不同的連接埠)。</span><span class="sxs-lookup"><span data-stu-id="e25cb-110">After the config file has been updated to define an endpoint, the load balancer must be updated to expose that (or a different) port.</span></span> <span data-ttu-id="e25cb-111">如需如何建立 Service Fabric 端點的詳細資訊，請參閱[設定端點](service-fabric-service-manifest-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="e25cb-111">For more information on how to create the service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="e25cb-112">建立負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="e25cb-112">Create a load balancer rule</span></span>

<span data-ttu-id="e25cb-113">負載平衡器規則會開啟網際網路面向的連接埠，並將流量轉送至您的應用程式所使用的內部節點連接埠。</span><span class="sxs-lookup"><span data-stu-id="e25cb-113">A load balancer rule opens up an internet-facing port and forwards traffic to the internal node's port used by your application.</span></span> <span data-ttu-id="e25cb-114">如果您沒有負載平衡器，請參閱[設定網際網路面向的負載平衡器](..\load-balancer\load-balancer-get-started-internet-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e25cb-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="e25cb-115">若要建立負載平衡器規則，您需要收集下列資訊：</span><span class="sxs-lookup"><span data-stu-id="e25cb-115">To create a load balancer rule, you need to collect the following information:</span></span>

- <span data-ttu-id="e25cb-116">負載平衡器名稱。</span><span class="sxs-lookup"><span data-stu-id="e25cb-116">Load balancer name.</span></span>
- <span data-ttu-id="e25cb-117">負載平衡器和 Service Fabric 叢集的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e25cb-117">Resource group of the load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="e25cb-118">外部連接埠。</span><span class="sxs-lookup"><span data-stu-id="e25cb-118">External port.</span></span>
- <span data-ttu-id="e25cb-119">內部連接埠。</span><span class="sxs-lookup"><span data-stu-id="e25cb-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="e25cb-120">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e25cb-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="e25cb-121">如果您需要決定負載平衡器的名稱，請使用此命令，以便快速取得一份所有負載平衡器和相關聯資源群組的清單。</span><span class="sxs-lookup"><span data-stu-id="e25cb-121">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and the associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="e25cb-122">使用 **Azure CLI**，只要一個命令就能建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="e25cb-122">It only takes a single command to create a load balancer rule with the **Azure CLI**.</span></span> <span data-ttu-id="e25cb-123">您只需要知道建立新規則之負載平衡器和資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="e25cb-123">You just need to know both the name of the load balancer and resource group to create a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="e25cb-124">Azure CLI 命令有幾個參數，如下表所述：</span><span class="sxs-lookup"><span data-stu-id="e25cb-124">The Azure CLI command has a few parameters that are described in the following table:</span></span>

| <span data-ttu-id="e25cb-125">參數</span><span class="sxs-lookup"><span data-stu-id="e25cb-125">Parameter</span></span> | <span data-ttu-id="e25cb-126">說明</span><span class="sxs-lookup"><span data-stu-id="e25cb-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="e25cb-127">Service Fabric 應用程式正在接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e25cb-127">The port the service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="e25cb-128">負載平衡器公開給外部連線的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e25cb-128">The port the load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="e25cb-129">所要變更的負載平衡器名稱。</span><span class="sxs-lookup"><span data-stu-id="e25cb-129">The name of the load balancer to change.</span></span> |
| `-g`       | <span data-ttu-id="e25cb-130">包含負載平衡器和 Service Fabric 叢集的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e25cb-130">The resource group that has both the load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="e25cb-131">所選擇的規則名稱。</span><span class="sxs-lookup"><span data-stu-id="e25cb-131">The chosen name of the rule.</span></span> |


>[!NOTE]
><span data-ttu-id="e25cb-132">如需如何使用 Azure CLI 建立負載平衡器的詳細資訊，請參閱[使用 Azure CLI 建立負載平衡器](..\load-balancer\load-balancer-get-started-internet-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="e25cb-132">For more information on how to create a load balancer with the Azure CLI, see [Create a load balancer with the Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="e25cb-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e25cb-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="e25cb-134">如果您需要決定負載平衡器的名稱，請使用此命令，以便快速取得一份所有負載平衡器和相關聯資源群組的清單。</span><span class="sxs-lookup"><span data-stu-id="e25cb-134">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="e25cb-135">PowerShell 比 Azure CLI 稍微複雜一點。</span><span class="sxs-lookup"><span data-stu-id="e25cb-135">PowerShell is a little more complicated than the Azure CLI.</span></span> <span data-ttu-id="e25cb-136">在概念上，執行下列步驟來建立規則。</span><span class="sxs-lookup"><span data-stu-id="e25cb-136">Conceptually, do the following steps to create a rule.</span></span>

1. <span data-ttu-id="e25cb-137">從 Azure 取得負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e25cb-137">Get the load balancer from Azure.</span></span>
2. <span data-ttu-id="e25cb-138">建立規則。</span><span class="sxs-lookup"><span data-stu-id="e25cb-138">Create a rule.</span></span>
3. <span data-ttu-id="e25cb-139">將規則新增至負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e25cb-139">Add the rule to the load balancer.</span></span>
4. <span data-ttu-id="e25cb-140">更新負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e25cb-140">Update the load balancer.</span></span>

```powershell
# Get the load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create the rule based on information from the load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add the rule to the load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update the load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="e25cb-141">至於 `New-AzureRmLoadBalancerRuleConfig` 命令，`-FrontendPort` 代表負載平衡器公開給外部連線的連接埠，而 `-BackendPort` 代表 Service Fabric 應用程式正在接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e25cb-141">Regarding the `New-AzureRmLoadBalancerRuleConfig` command, the `-FrontendPort` represents the port the load balancer exposes for external connections, and the `-BackendPort` represents the port the service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="e25cb-142">如需如何使用 PowerShell 建立負載平衡器的詳細資訊，請參閱[使用 PowerShell 建立負載平衡器](..\load-balancer\load-balancer-get-started-internet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="e25cb-142">For more information on how to create a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

