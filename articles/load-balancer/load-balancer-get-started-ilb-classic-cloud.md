---
title: "建立 Azure 雲端服務的內部負載平衡器 | Microsoft Docs"
description: "了解如何在傳統部署模型中使用 PowerShell 建立內部負載平衡器"
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
ms.openlocfilehash: 8dbc951416d577fa7f534c2eab1605c6bee61fce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="c1519-103">開始為雲端服務建立內部負載平衡器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="c1519-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1519-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1519-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="c1519-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c1519-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="c1519-106">雲端服務</span><span class="sxs-lookup"><span data-stu-id="c1519-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="c1519-107">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="c1519-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c1519-108">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="c1519-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="c1519-109">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="c1519-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c1519-110">了解如何[使用 Resource Manager 模型執行這些步驟](load-balancer-get-started-ilb-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="c1519-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="c1519-111">設定雲端服務的內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c1519-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="c1519-112">虛擬機器和雲端服務都支援內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c1519-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="c1519-113">在區域虛擬網路外的雲端服務中建立的內部負載平衡器端點，將只能在雲端服務內存取。</span><span class="sxs-lookup"><span data-stu-id="c1519-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within the cloud service.</span></span>

<span data-ttu-id="c1519-114">內部負載平衡器組態必須在於雲端服務中建立第一個部署的期間進行設定，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="c1519-114">The internal load balancer configuration has to be set during the creation of the first deployment in the cloud service, as shown in the sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1519-115">執行下列步驟的必要條件是已經為雲端部署建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c1519-115">A prerequisite to run the steps below is to have a virtual network already created for the cloud deployment.</span></span> <span data-ttu-id="c1519-116">您需要虛擬網路名稱和子網路名才能建立內部負載平衡。</span><span class="sxs-lookup"><span data-stu-id="c1519-116">You will need the virtual network name and subnet name to create the Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="c1519-117">步驟 1</span><span class="sxs-lookup"><span data-stu-id="c1519-117">Step 1</span></span>

<span data-ttu-id="c1519-118">在 Visual Studio 中開啟雲端部署的服務組態檔 (.cscfg) 並新增下列區段，以在網路組態的最後一個 "`</Role>`" 項目下建立內部負載平衡。</span><span class="sxs-lookup"><span data-stu-id="c1519-118">Open the service configuration file (.cscfg) for your cloud deployment in Visual Studio and add the following section to create the Internal Load Balancing under the last "`</Role>`" item for the network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of the load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="c1519-119">讓我們新增網路組態檔的值，以顯示看起來如何。</span><span class="sxs-lookup"><span data-stu-id="c1519-119">Let's add the values for the network configuration file to show how it will look.</span></span> <span data-ttu-id="c1519-120">在此範例中，假設您利用稱為 test_subnet 的子網路 10.0.0.0/24 和靜態 IP 10.0.0.4 建立稱為 "test_vnet" 的 VNet。</span><span class="sxs-lookup"><span data-stu-id="c1519-120">In the example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="c1519-121">負載平衡器將會命名為 testLB。</span><span class="sxs-lookup"><span data-stu-id="c1519-121">The load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="c1519-122">如需關於負載平衡器結構描述的詳細資訊，請參閱 [新增負載平衡器](https://msdn.microsoft.com/library/azure/dn722411.aspx)</span><span class="sxs-lookup"><span data-stu-id="c1519-122">For more information about the load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="c1519-123">步驟 2</span><span class="sxs-lookup"><span data-stu-id="c1519-123">Step 2</span></span>

<span data-ttu-id="c1519-124">變更服務定義 (.csdef) 檔案，以將端點新增至內部負載平衡。</span><span class="sxs-lookup"><span data-stu-id="c1519-124">Change the service definition (.csdef) file to add endpoints to the Internal Load Balancing.</span></span> <span data-ttu-id="c1519-125">建立角色執行個體時，服務定義檔會將角色執行個體新增至內部負載平衡。</span><span class="sxs-lookup"><span data-stu-id="c1519-125">The moment a role instance is created, the service definition file will add the role instances to the Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="c1519-126">遵循與上述範例相同的值，讓我們將值新增至服務定義檔。</span><span class="sxs-lookup"><span data-stu-id="c1519-126">Following the same values from the example above, let's add the values to the service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="c1519-127">網路流量會使用 testLB 負載平衡器進行負載平衡，使用連接埠 80 進行連入要求，也在連接埠 80 上傳送背景工作角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="c1519-127">The network traffic will be load balanced using the testLB load balancer using port 80 for incoming requests, sending to worker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1519-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c1519-128">Next steps</span></span>

[<span data-ttu-id="c1519-129">使用來源 IP 同質性設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="c1519-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c1519-130">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="c1519-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

