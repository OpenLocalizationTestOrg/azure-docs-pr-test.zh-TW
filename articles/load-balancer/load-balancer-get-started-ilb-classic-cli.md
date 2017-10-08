---
title: "aaaCreate 內部負載平衡器-Azure CLI 傳統 |Microsoft 文件"
description: "了解內部負載平衡器使用 toocreate hello Azure CLI hello 傳統部署模型中的方式"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a><span data-ttu-id="b49ca-103">開始建立內部負載平衡器 （傳統） 使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="b49ca-103">Get started creating an internal load balancer (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b49ca-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b49ca-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="b49ca-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b49ca-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="b49ca-106">雲端服務</span><span class="sxs-lookup"><span data-stu-id="b49ca-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="b49ca-107">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="b49ca-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b49ca-108">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b49ca-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="b49ca-109">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="b49ca-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b49ca-110">了解如何太[使用 hello 資源管理員的模型執行這些步驟](load-balancer-get-started-ilb-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="b49ca-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="b49ca-111">toocreate 設定虛擬機器的內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="b49ca-111">toocreate an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="b49ca-112">內部負載平衡器設定和 hello 伺服器，則會傳送其流量 tooit toocreate，您必須執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="b49ca-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you must do hello following:</span></span>

1. <span data-ttu-id="b49ca-113">建立執行個體的內部負載平衡一組負載平衡的 hello 伺服器之間取得平衡的連入流量 toobe 負載 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="b49ca-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="b49ca-114">新增對應 toohello 將接收 hello 連入流量的虛擬機器端點。</span><span class="sxs-lookup"><span data-stu-id="b49ca-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="b49ca-115">設定將用來傳送嗨流量 toobe 負載平衡 toosend 其流量 toohello 虛擬 IP (VIP) 位址 hello 內部負載平衡的執行個體的 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b49ca-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="b49ca-116">使用 CLI 逐步建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="b49ca-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="b49ca-117">本指南也說明如何 toocreate 內部負載平衡器根據上面的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="b49ca-117">This guide shows how toocreate an internal load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="b49ca-118">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="b49ca-118">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="b49ca-119">執行 hello **azure 組態模式**命令 tooswitch tooclassic 模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b49ca-119">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="b49ca-120">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="b49ca-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="b49ca-121">建立端點與負載平衡器集</span><span class="sxs-lookup"><span data-stu-id="b49ca-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="b49ca-122">hello 案例假設 hello 虛擬機器 」 DB1 」 和 「 DB2 「 呼叫 」 mytestcloud 」 的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b49ca-122">hello scenario assumes hello virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="b49ca-123">這些虛擬機器使用稱為我的「testvnet」，且具子網路「subnet-1」的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b49ca-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="b49ca-124">本指南將使用連接埠 1433 做為私用連接埠與本機連接埠，以建立內部負載平衡器集。</span><span class="sxs-lookup"><span data-stu-id="b49ca-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="b49ca-125">這是常見的案例，您擁有 hello 後端使用直接使用的公用 IP 位址不會公開內部負載平衡器 tooguarantee hello 資料庫伺服器上的 SQL 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b49ca-125">This is a common scenario where you have SQL virtual machines on hello back end using an internal load balancer tooguarantee hello database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="b49ca-126">步驟 1</span><span class="sxs-lookup"><span data-stu-id="b49ca-126">Step 1</span></span>

<span data-ttu-id="b49ca-127">使用 `azure network service internal-load-balancer add`建立內部負載平衡器集。</span><span class="sxs-lookup"><span data-stu-id="b49ca-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="b49ca-128">如需詳細資訊，請參閱 `azure service internal-load-balancer --help` 。</span><span class="sxs-lookup"><span data-stu-id="b49ca-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="b49ca-129">您可以查看 hello 內部負載平衡器屬性使用 hello 命令`azure service internal-load-balancer list`*雲端服務名稱*。</span><span class="sxs-lookup"><span data-stu-id="b49ca-129">You can check hello internal load balancer properties using hello command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="b49ca-130">這裡會遵循 hello 輸出的範例：</span><span class="sxs-lookup"><span data-stu-id="b49ca-130">Here follows an example of hello output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="b49ca-131">步驟 2</span><span class="sxs-lookup"><span data-stu-id="b49ca-131">Step 2</span></span>

<span data-ttu-id="b49ca-132">您設定 hello 內部負載平衡器設定，當您將加入 hello 第一個端點。</span><span class="sxs-lookup"><span data-stu-id="b49ca-132">You configure hello internal load balancer set when you add hello first endpoint.</span></span> <span data-ttu-id="b49ca-133">您會將關聯 hello 端點、 虛擬機器和探查連接埠 toohello 內部負載平衡器在此步驟中設定。</span><span class="sxs-lookup"><span data-stu-id="b49ca-133">You will associate hello endpoint, virtual machine and probe port toohello internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="b49ca-134">步驟 3</span><span class="sxs-lookup"><span data-stu-id="b49ca-134">Step 3</span></span>

<span data-ttu-id="b49ca-135">確認 hello 負載平衡器組態使用`azure vm show`*虛擬機器名稱*</span><span class="sxs-lookup"><span data-stu-id="b49ca-135">Verify hello load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="b49ca-136">hello 輸出將會：</span><span class="sxs-lookup"><span data-stu-id="b49ca-136">hello output will be:</span></span>

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="b49ca-137">為虛擬機器建立遠端桌面端點</span><span class="sxs-lookup"><span data-stu-id="b49ca-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="b49ca-138">您可以從公用連接埠 tooa 本機連接埠的特定虛擬機器使用建立遠端桌面端點 tooforward 網路流量`azure vm endpoint create`。</span><span class="sxs-lookup"><span data-stu-id="b49ca-138">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="b49ca-139">從負載平衡器移除虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b49ca-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="b49ca-140">您可以從正在刪除相關聯的 hello 端點來設定內部負載平衡器移除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b49ca-140">You can remove a virtual machine from an internal load balancer set by deleting hello associated endpoint.</span></span> <span data-ttu-id="b49ca-141">一旦移除 hello 端點時，hello 虛擬機器將不會屬於 toohello 負載平衡器不再設定。</span><span class="sxs-lookup"><span data-stu-id="b49ca-141">Once hello endpoint is removed, hello virtual machine won't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="b49ca-142">使用 hello 上述範例中，您可以建立虛擬機器 」 DB1"hello 端點使用將從內部負載平衡器 「 ilbset"hello 命令`azure vm endpoint delete`。</span><span class="sxs-lookup"><span data-stu-id="b49ca-142">Using hello example above, you can remove hello endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="b49ca-143">如需詳細資訊，請參閱 `azure vm endpoint --help` 。</span><span class="sxs-lookup"><span data-stu-id="b49ca-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b49ca-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b49ca-144">Next steps</span></span>

[<span data-ttu-id="b49ca-145">使用來源 IP 同質性設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="b49ca-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b49ca-146">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="b49ca-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
