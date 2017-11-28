---
title: "建立網際網路對向負載平衡器 - Azure CLI 傳統 | Microsoft Docs"
description: "了解如何使用 Azure CLI 在傳統部署模型中建立網際網路面向的負載平衡器"
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
ms.openlocfilehash: da3a908f17ff5c6d3923549a884ecc0a13cb8e9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-cli"></a><span data-ttu-id="7d601-103">開始在 Azure CLI 中建立網際網路面向的負載平衡器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="7d601-103">Get started creating an Internet facing load balancer (classic) in the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d601-104">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="7d601-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="7d601-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d601-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="7d601-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7d601-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="7d601-107">Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="7d601-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="7d601-108">使用 Azure 資源之前，請務必了解 Azure 目前有 Azure Resource Manager 和「傳統」兩種部署模型。</span><span class="sxs-lookup"><span data-stu-id="7d601-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="7d601-109">在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。</span><span class="sxs-lookup"><span data-stu-id="7d601-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="7d601-110">您可以按一下本文頂端的索引標籤，檢視不同工具的文件。</span><span class="sxs-lookup"><span data-stu-id="7d601-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="7d601-111">本文涵蓋之內容包括傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="7d601-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="7d601-112">您也可以 [了解如何使用 Azure 資源管理員建立網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="7d601-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="7d601-113">使用 CLI 逐步建立網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7d601-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="7d601-114">本指南根據上述案例說明如何建立網際網路面向的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="7d601-114">This guide shows how to create an Internet load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="7d601-115">如果您從未使用過 Azure CLI，請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md) ，並依照指示進行，直到選取您的 Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7d601-115">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="7d601-116">執行 **azure config mode** 命令，以切換為傳統模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="7d601-116">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="7d601-117">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="7d601-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="7d601-118">建立端點與負載平衡器集</span><span class="sxs-lookup"><span data-stu-id="7d601-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="7d601-119">此案例假設虛擬機器 "web1" 和 "web2" 已經建立。</span><span class="sxs-lookup"><span data-stu-id="7d601-119">The scenario assumes the virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="7d601-120">本指南將使用連接埠 80 作為公用連接埠，以及 80 作為本機連接埠，建立負載平衡器集。</span><span class="sxs-lookup"><span data-stu-id="7d601-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="7d601-121">探查連接埠也設定在連接埠 80 上，並將負載平衡器集稱為 "lbset"</span><span class="sxs-lookup"><span data-stu-id="7d601-121">A probe port is also configured on port 80 and named the load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="7d601-122">步驟 1</span><span class="sxs-lookup"><span data-stu-id="7d601-122">Step 1</span></span>

<span data-ttu-id="7d601-123">針對虛擬機器 "web1" 使用 `azure network vm endpoint create` 建立第一個端點和負載平衡器集</span><span class="sxs-lookup"><span data-stu-id="7d601-123">Create the first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="7d601-124">步驟 2</span><span class="sxs-lookup"><span data-stu-id="7d601-124">Step 2</span></span>

<span data-ttu-id="7d601-125">將第二個虛擬機器 "web2" 新增到負載平衡器集。</span><span class="sxs-lookup"><span data-stu-id="7d601-125">Add a second virtual machine "web2" to the load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="7d601-126">步驟 3</span><span class="sxs-lookup"><span data-stu-id="7d601-126">Step 3</span></span>

<span data-ttu-id="7d601-127">使用 `azure vm show` 確認負載平衡器設定</span><span class="sxs-lookup"><span data-stu-id="7d601-127">Verify the load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="7d601-128">輸出將是：</span><span class="sxs-lookup"><span data-stu-id="7d601-128">The output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="7d601-129">為虛擬機器建立遠端桌面端點</span><span class="sxs-lookup"><span data-stu-id="7d601-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="7d601-130">您可以使用 `azure vm endpoint create`建立遠端桌面端點，針對特定的虛擬機器將網路流量從公用連接埠轉送至本機連接埠。</span><span class="sxs-lookup"><span data-stu-id="7d601-130">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="7d601-131">從負載平衡器移除虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7d601-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="7d601-132">您必須從虛擬機器刪除與負載平衡器集相關聯的端點。</span><span class="sxs-lookup"><span data-stu-id="7d601-132">You have to delete the endpoint associated to the load balancer set from the virtual machine.</span></span> <span data-ttu-id="7d601-133">一旦移除端點，虛擬機器就不再屬於負載平衡器集。</span><span class="sxs-lookup"><span data-stu-id="7d601-133">Once the endpoint is removed, the virtual machine doesn't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="7d601-134">使用上述的範例，您可以使用命令 `azure vm endpoint delete` 從負載平衡器 "lbset" 移除針對虛擬機器 "web1" 所建立的端點。</span><span class="sxs-lookup"><span data-stu-id="7d601-134">Using the example above, you can remove the endpoint created for virtual machine "web1" from load balancer "lbset" using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="7d601-135">您可以使用命令 `azure vm endpoint --help` 探索更多管理端點的選項</span><span class="sxs-lookup"><span data-stu-id="7d601-135">You can explore more options to manage endpoints using the command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d601-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d601-136">Next steps</span></span>

[<span data-ttu-id="7d601-137">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7d601-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="7d601-138">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="7d601-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="7d601-139">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="7d601-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
