---
title: "aaaCreate 叢集中的 Azure 負載平衡器規則"
description: "設定 Azure Service Fabric 叢集的 Azure 負載平衡器 tooopen 連接埠。"
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
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="06e99-103">開啟 Service Fabric 叢集的連接埠</span><span class="sxs-lookup"><span data-stu-id="06e99-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="06e99-104">hello 負載平衡器部署與 Azure Service Fabric 叢集指示流量 tooyour 應用程式的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="06e99-104">hello load balancer deployed with your Azure Service Fabric cluster directs traffic tooyour app running on a node.</span></span> <span data-ttu-id="06e99-105">如果您變更您的應用程式 toouse 不同的通訊埠，您必須公開該通訊埠 （或路由傳送不同的連接埠） 在 hello Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="06e99-105">If you change your app toouse a different port, you must expose that port (or route a different port) in hello Azure Load Balancer.</span></span>

<span data-ttu-id="06e99-106">當您部署您的 service fabric 叢集 tooAzure 時，為您自動建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="06e99-106">When you deployed your service fabric cluster tooAzure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="06e99-107">如果您沒有負載平衡器，請參閱[設定網際網路面向的負載平衡器](..\load-balancer\load-balancer-get-started-internet-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="06e99-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="06e99-108">設定 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="06e99-108">Configure service fabric</span></span>

<span data-ttu-id="06e99-109">Service Fabric 應用程式**ServiceManifest.xml**組態檔定義您的應用程式必須要有 toouse hello 端點。</span><span class="sxs-lookup"><span data-stu-id="06e99-109">Your Service Fabric application **ServiceManifest.xml** config file defines hello endpoints your application expects toouse.</span></span> <span data-ttu-id="06e99-110">Hello 負載平衡器 hello 設定檔已更新的 toodefine 端點之後，必須更新的 tooexpose 該 （或不同） 連接埠。</span><span class="sxs-lookup"><span data-stu-id="06e99-110">After hello config file has been updated toodefine an endpoint, hello load balancer must be updated tooexpose that (or a different) port.</span></span> <span data-ttu-id="06e99-111">如需有關如何 toocreate hello 服務網狀架構端點的詳細資訊，請參閱[安裝端點](service-fabric-service-manifest-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="06e99-111">For more information on how toocreate hello service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="06e99-112">建立負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="06e99-112">Create a load balancer rule</span></span>

<span data-ttu-id="06e99-113">負載平衡器規則面對網際網路的連接埠會開啟，並將轉寄流量 toohello 內部節點的應用程式所使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="06e99-113">A load balancer rule opens up an internet-facing port and forwards traffic toohello internal node's port used by your application.</span></span> <span data-ttu-id="06e99-114">如果您沒有負載平衡器，請參閱[設定網際網路面向的負載平衡器](..\load-balancer\load-balancer-get-started-internet-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="06e99-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="06e99-115">負載平衡器規則，您需要下列資訊 toocollect hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="06e99-115">toocreate a load balancer rule, you need toocollect hello following information:</span></span>

- <span data-ttu-id="06e99-116">負載平衡器名稱。</span><span class="sxs-lookup"><span data-stu-id="06e99-116">Load balancer name.</span></span>
- <span data-ttu-id="06e99-117">資源群組的 hello 負載平衡器和 service fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="06e99-117">Resource group of hello load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="06e99-118">外部連接埠。</span><span class="sxs-lookup"><span data-stu-id="06e99-118">External port.</span></span>
- <span data-ttu-id="06e99-119">內部連接埠。</span><span class="sxs-lookup"><span data-stu-id="06e99-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="06e99-120">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="06e99-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="06e99-121">如果您需要 toodetermine hello hello 負載平衡器名稱，請使用此命令 tooquickly get 所有負載平衡器和相關聯的 hello 資源群組的清單。</span><span class="sxs-lookup"><span data-stu-id="06e99-121">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and hello associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="06e99-122">只需要單一命令 toocreate hello 與負載平衡器規則**Azure CLI**。</span><span class="sxs-lookup"><span data-stu-id="06e99-122">It only takes a single command toocreate a load balancer rule with hello **Azure CLI**.</span></span> <span data-ttu-id="06e99-123">您只需要 tooknow hello 負載平衡器與資源群組 toocreate 新規則的兩個 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="06e99-123">You just need tooknow both hello name of hello load balancer and resource group toocreate a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="06e99-124">hello Azure CLI 命令具有一些 hello 下表所述的參數：</span><span class="sxs-lookup"><span data-stu-id="06e99-124">hello Azure CLI command has a few parameters that are described in hello following table:</span></span>

| <span data-ttu-id="06e99-125">參數</span><span class="sxs-lookup"><span data-stu-id="06e99-125">Parameter</span></span> | <span data-ttu-id="06e99-126">說明</span><span class="sxs-lookup"><span data-stu-id="06e99-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="06e99-127">hello 連接埠 hello service fabric 應用程式正在接聽。</span><span class="sxs-lookup"><span data-stu-id="06e99-127">hello port hello service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="06e99-128">hello 連接埠 hello 負載平衡器會公開的外部連接。</span><span class="sxs-lookup"><span data-stu-id="06e99-128">hello port hello load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="06e99-129">hello hello 名稱負載平衡器 toochange。</span><span class="sxs-lookup"><span data-stu-id="06e99-129">hello name of hello load balancer toochange.</span></span> |
| `-g`       | <span data-ttu-id="06e99-130">hello 具有 hello 負載平衡器和 service fabric 叢集資源群組。</span><span class="sxs-lookup"><span data-stu-id="06e99-130">hello resource group that has both hello load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="06e99-131">hello 選擇 hello 規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="06e99-131">hello chosen name of hello rule.</span></span> |


>[!NOTE]
><span data-ttu-id="06e99-132">如需有關如何 toocreate 負載平衡器以 hello Azure CLI，請參閱[建立負載平衡器以 hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="06e99-132">For more information on how toocreate a load balancer with hello Azure CLI, see [Create a load balancer with hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="06e99-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06e99-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="06e99-134">如果您需要 toodetermine hello hello 負載平衡器名稱，請使用此命令 tooquickly get 所有負載平衡器和相關聯的資源群組的清單。</span><span class="sxs-lookup"><span data-stu-id="06e99-134">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="06e99-135">PowerShell 是比 hello Azure CLI 更為複雜。</span><span class="sxs-lookup"><span data-stu-id="06e99-135">PowerShell is a little more complicated than hello Azure CLI.</span></span> <span data-ttu-id="06e99-136">在概念上，執行下列步驟 toocreate hello 規則。</span><span class="sxs-lookup"><span data-stu-id="06e99-136">Conceptually, do hello following steps toocreate a rule.</span></span>

1. <span data-ttu-id="06e99-137">從 Azure 取得 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="06e99-137">Get hello load balancer from Azure.</span></span>
2. <span data-ttu-id="06e99-138">建立規則。</span><span class="sxs-lookup"><span data-stu-id="06e99-138">Create a rule.</span></span>
3. <span data-ttu-id="06e99-139">新增 hello 規則 toohello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="06e99-139">Add hello rule toohello load balancer.</span></span>
4. <span data-ttu-id="06e99-140">更新 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="06e99-140">Update hello load balancer.</span></span>

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="06e99-141">關於 hello`New-AzureRmLoadBalancerRuleConfig`命令時，hello`-FrontendPort`代表 hello 連接埠 hello 負載平衡器會公開外部連接，和 hello`-BackendPort`代表 hello 連接埠 hello service fabric 應用程式正在接聽。</span><span class="sxs-lookup"><span data-stu-id="06e99-141">Regarding hello `New-AzureRmLoadBalancerRuleConfig` command, hello `-FrontendPort` represents hello port hello load balancer exposes for external connections, and hello `-BackendPort` represents hello port hello service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="06e99-142">如需有關如何 toocreate 負載平衡器使用 PowerShell，請參閱[使用 PowerShell 建立負載平衡器](..\load-balancer\load-balancer-get-started-internet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="06e99-142">For more information on how toocreate a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

