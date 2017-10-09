---
title: "aaaCreate 網際網路對向負載平衡器-Azure CLI 傳統 |Microsoft 文件"
description: "了解如何在模型中使用傳統部署使用網際網路對向負載平衡器 toocreate hello Azure CLI"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a><span data-ttu-id="2bd50-103">開始建立網際網路對向 hello Azure CLI 中的負載平衡器 （傳統）</span><span class="sxs-lookup"><span data-stu-id="2bd50-103">Get started creating an Internet facing load balancer (classic) in hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2bd50-104">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="2bd50-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="2bd50-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bd50-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="2bd50-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2bd50-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="2bd50-107">Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="2bd50-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="2bd50-108">您可以使用 Azure 資源之前，它是 Azure 目前有兩種部署模型的重要 toounderstand: Azure 資源管理員] 和 [傳統。</span><span class="sxs-lookup"><span data-stu-id="2bd50-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="2bd50-109">在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。</span><span class="sxs-lookup"><span data-stu-id="2bd50-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="2bd50-110">您可以按一下上方的這篇文章 hello hello 索引標籤檢視 hello 文件不同的工具。</span><span class="sxs-lookup"><span data-stu-id="2bd50-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="2bd50-111">本文涵蓋 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="2bd50-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="2bd50-112">您也可以[toocreate 網際網路向負載平衡器使用 Azure 資源管理員的如何了解](load-balancer-get-started-internet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="2bd50-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="2bd50-113">使用 CLI 逐步建立網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="2bd50-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="2bd50-114">本指南也說明如何 toocreate 網際網路負載平衡器根據上面的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="2bd50-114">This guide shows how toocreate an Internet load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="2bd50-115">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="2bd50-115">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="2bd50-116">執行 hello **azure 組態模式**命令 tooswitch tooclassic 模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2bd50-116">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="2bd50-117">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="2bd50-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="2bd50-118">建立端點與負載平衡器集</span><span class="sxs-lookup"><span data-stu-id="2bd50-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="2bd50-119">hello 案例假設 hello 虛擬機器 」 web1"和"web2 」 所建立。</span><span class="sxs-lookup"><span data-stu-id="2bd50-119">hello scenario assumes hello virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="2bd50-120">本指南將使用連接埠 80 作為公用連接埠，以及 80 作為本機連接埠，建立負載平衡器集。</span><span class="sxs-lookup"><span data-stu-id="2bd50-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="2bd50-121">探查連接埠也會設定連接埠 80 和具名的 hello 負載平衡器設定 「 lbset"。</span><span class="sxs-lookup"><span data-stu-id="2bd50-121">A probe port is also configured on port 80 and named hello load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="2bd50-122">步驟 1</span><span class="sxs-lookup"><span data-stu-id="2bd50-122">Step 1</span></span>

<span data-ttu-id="2bd50-123">建立 hello 第一個端點和負載平衡器設定使用`azure network vm endpoint create`虛擬機器 」 web1"。</span><span class="sxs-lookup"><span data-stu-id="2bd50-123">Create hello first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="2bd50-124">步驟 2</span><span class="sxs-lookup"><span data-stu-id="2bd50-124">Step 2</span></span>

<span data-ttu-id="2bd50-125">新增第二個虛擬機器 」 web2"toohello 負載平衡器集。</span><span class="sxs-lookup"><span data-stu-id="2bd50-125">Add a second virtual machine "web2" toohello load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="2bd50-126">步驟 3</span><span class="sxs-lookup"><span data-stu-id="2bd50-126">Step 3</span></span>

<span data-ttu-id="2bd50-127">確認 hello 負載平衡器組態使用`azure vm show`。</span><span class="sxs-lookup"><span data-stu-id="2bd50-127">Verify hello load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="2bd50-128">hello 輸出將會：</span><span class="sxs-lookup"><span data-stu-id="2bd50-128">hello output will be:</span></span>

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="2bd50-129">為虛擬機器建立遠端桌面端點</span><span class="sxs-lookup"><span data-stu-id="2bd50-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="2bd50-130">您可以從公用連接埠 tooa 本機連接埠的特定虛擬機器使用建立遠端桌面端點 tooforward 網路流量`azure vm endpoint create`。</span><span class="sxs-lookup"><span data-stu-id="2bd50-130">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="2bd50-131">從負載平衡器移除虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2bd50-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="2bd50-132">您必須從 hello 虛擬機器負載平衡器集 toodelete hello 關聯端點 toohello。</span><span class="sxs-lookup"><span data-stu-id="2bd50-132">You have toodelete hello endpoint associated toohello load balancer set from hello virtual machine.</span></span> <span data-ttu-id="2bd50-133">一旦移除 hello 端點時，hello 虛擬機器不屬於 toohello 負載平衡器不再設定。</span><span class="sxs-lookup"><span data-stu-id="2bd50-133">Once hello endpoint is removed, hello virtual machine doesn't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="2bd50-134">使用 hello 上述範例中，您可以移除虛擬機器 」 web1"建立 hello 端點從負載平衡器使用 hello 命令"lbset" `azure vm endpoint delete`。</span><span class="sxs-lookup"><span data-stu-id="2bd50-134">Using hello example above, you can remove hello endpoint created for virtual machine "web1" from load balancer "lbset" using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="2bd50-135">您可以瀏覽選項 toomanage 端點使用 hello 命令`azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="2bd50-135">You can explore more options toomanage endpoints using hello command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bd50-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2bd50-136">Next steps</span></span>

[<span data-ttu-id="2bd50-137">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="2bd50-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="2bd50-138">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="2bd50-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="2bd50-139">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="2bd50-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
