---
title: "aaaCreate Azure 雲端服務的內部負載平衡器 |Microsoft 文件"
description: "了解 toocreate 內部負載平衡器在 hello 傳統部署模型中使用 PowerShell 的方式"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="fdb02-103">開始為雲端服務建立內部負載平衡器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="fdb02-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fdb02-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdb02-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="fdb02-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fdb02-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="fdb02-106">雲端服務</span><span class="sxs-lookup"><span data-stu-id="fdb02-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="fdb02-107">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="fdb02-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="fdb02-108">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="fdb02-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="fdb02-109">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="fdb02-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="fdb02-110">了解如何太[使用 hello 資源管理員的模型執行這些步驟](load-balancer-get-started-ilb-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="fdb02-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="fdb02-111">設定雲端服務的內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="fdb02-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="fdb02-112">虛擬機器和雲端服務都支援內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="fdb02-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="fdb02-113">只有在 hello 雲端服務內仍可使用區域虛擬網路外的雲端服務中建立的內部負載平衡器端點。</span><span class="sxs-lookup"><span data-stu-id="fdb02-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within hello cloud service.</span></span>

<span data-ttu-id="fdb02-114">hello 內部負載平衡器組態有 toobe hello 以下範例所示，hello 建立 hello hello 雲端服務中的第一次部署期間設定。</span><span class="sxs-lookup"><span data-stu-id="fdb02-114">hello internal load balancer configuration has toobe set during hello creation of hello first deployment in hello cloud service, as shown in hello sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdb02-115">下列必要條件 toorun hello 步驟是 toohave 已經針對 hello 雲端部署建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fdb02-115">A prerequisite toorun hello steps below is toohave a virtual network already created for hello cloud deployment.</span></span> <span data-ttu-id="fdb02-116">您將需要 hello 虛擬網路名稱和子網路名稱 toocreate hello 內部負載平衡。</span><span class="sxs-lookup"><span data-stu-id="fdb02-116">You will need hello virtual network name and subnet name toocreate hello Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="fdb02-117">步驟 1</span><span class="sxs-lookup"><span data-stu-id="fdb02-117">Step 1</span></span>

<span data-ttu-id="fdb02-118">為您的雲端部署，Visual Studio 中開啟 hello 服務組態檔 (.cscfg)，然後加入下列區段 toocreate hello 內部負載平衡 hello 下的最後的 hello"`</Role>`"hello 網路組態項目。</span><span class="sxs-lookup"><span data-stu-id="fdb02-118">Open hello service configuration file (.cscfg) for your cloud deployment in Visual Studio and add hello following section toocreate hello Internal Load Balancing under hello last "`</Role>`" item for hello network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="fdb02-119">讓我們加入 hello 值 hello 網路組態檔 tooshow 的外觀。</span><span class="sxs-lookup"><span data-stu-id="fdb02-119">Let's add hello values for hello network configuration file tooshow how it will look.</span></span> <span data-ttu-id="fdb02-120">在 hello 範例中，假設您建立 VNet 子網路 10.0.0.0/24 test_subnet 和靜態 ip 位址 10.0.0.4 呼叫以呼叫"test_vnet"。</span><span class="sxs-lookup"><span data-stu-id="fdb02-120">In hello example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="fdb02-121">hello 負載平衡器將會命名為 testLB。</span><span class="sxs-lookup"><span data-stu-id="fdb02-121">hello load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="fdb02-122">如需 hello 負載平衡器組態結構描述的詳細資訊，請參閱[新增負載平衡器](https://msdn.microsoft.com/library/azure/dn722411.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fdb02-122">For more information about hello load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="fdb02-123">步驟 2</span><span class="sxs-lookup"><span data-stu-id="fdb02-123">Step 2</span></span>

<span data-ttu-id="fdb02-124">變更 hello 服務定義 (.csdef) 檔案 tooadd 端點 toohello 內部負載平衡。</span><span class="sxs-lookup"><span data-stu-id="fdb02-124">Change hello service definition (.csdef) file tooadd endpoints toohello Internal Load Balancing.</span></span> <span data-ttu-id="fdb02-125">hello 目前建立的角色執行個體時，hello 服務定義檔會加入 hello 角色執行個體 toohello 內部負載平衡。</span><span class="sxs-lookup"><span data-stu-id="fdb02-125">hello moment a role instance is created, hello service definition file will add hello role instances toohello Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="fdb02-126">下列 hello 相同 hello 上述範例中的值，讓我們加入 hello 值 toohello 服務定義檔。</span><span class="sxs-lookup"><span data-stu-id="fdb02-126">Following hello same values from hello example above, let's add hello values toohello service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="fdb02-127">hello 網路流量將負載平衡使用 hello testLB 負載平衡器連入要求，也在連接埠 80 傳送 tooworker 角色執行個體使用通訊埠 80。</span><span class="sxs-lookup"><span data-stu-id="fdb02-127">hello network traffic will be load balanced using hello testLB load balancer using port 80 for incoming requests, sending tooworker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdb02-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fdb02-128">Next steps</span></span>

[<span data-ttu-id="fdb02-129">使用來源 IP 同質性設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="fdb02-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="fdb02-130">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="fdb02-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

