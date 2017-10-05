---
title: "使用 Azure 網路監看員 IP 流量驗證來驗證流量 - Azure CLI | Microsoft Docs"
description: "本文說明如何使用 Azure CLI 檢查虛擬機器中的流入或流出流量是被允許或拒絕"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c5fe6c662b3ee2a443904b0f12cbfd495d9bc85e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="6cddc-103">使用 Azure 網路監看員的 IP 流量驗證元件來檢查 VM 中的流入或流出流量是被允許或拒絕</span><span class="sxs-lookup"><span data-stu-id="6cddc-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6cddc-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6cddc-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="6cddc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cddc-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="6cddc-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6cddc-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="6cddc-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6cddc-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="6cddc-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="6cddc-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="6cddc-109">IP 流量驗證是網路監看員的一項功能，可讓您驗證虛擬機器中的流入或流出流量是否被允許。</span><span class="sxs-lookup"><span data-stu-id="6cddc-109">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="6cddc-110">此案例可用於取得虛擬機器的目前狀態，以了解其是否可以和外部資源或後端通訊。</span><span class="sxs-lookup"><span data-stu-id="6cddc-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="6cddc-111">IP 流量驗證可用來驗證是否已正確設定網路安全性群組 (NSG) 規則，並針對 NSG 規則所封鎖的流量進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="6cddc-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="6cddc-112">使用 IP 流量驗證的另一個原因是要確保您想要封鎖的流量會被 NSG 正確封鎖。</span><span class="sxs-lookup"><span data-stu-id="6cddc-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="6cddc-113">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="6cddc-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6cddc-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="6cddc-114">Before you begin</span></span>

<span data-ttu-id="6cddc-115">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員，或您擁有現有的網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="6cddc-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="6cddc-116">此案例也假設已有具有有效虛擬機器的資源群組可供使用。</span><span class="sxs-lookup"><span data-stu-id="6cddc-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="6cddc-117">案例</span><span class="sxs-lookup"><span data-stu-id="6cddc-117">Scenario</span></span>

<span data-ttu-id="6cddc-118">此案例使用 IP 流量驗證來驗證虛擬機器是否可以和已知的 Bing IP 位址通訊。</span><span class="sxs-lookup"><span data-stu-id="6cddc-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="6cddc-119">如果流量被拒絕，它會傳回拒絕該流量的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="6cddc-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="6cddc-120">若要深入了解 IP 流量驗證，請造訪 [IP 流量驗證概觀](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6cddc-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="6cddc-121">取得 VM</span><span class="sxs-lookup"><span data-stu-id="6cddc-121">Get a VM</span></span>

<span data-ttu-id="6cddc-122">IP 流量驗證會測試虛擬機器上的 IP 位址流向遠端目的地的流量，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="6cddc-122">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="6cddc-123">Cmdlet 需要虛擬機器的識別碼。</span><span class="sxs-lookup"><span data-stu-id="6cddc-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="6cddc-124">如果您已經知道要使用的虛擬機器識別碼，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="6cddc-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-the-nics"></a><span data-ttu-id="6cddc-125">取得 NICS</span><span class="sxs-lookup"><span data-stu-id="6cddc-125">Get the NICS</span></span>

<span data-ttu-id="6cddc-126">您需要虛擬機器上 NIC 的 IP 位址，在此範例中，我們會擷取虛擬機器上的 NIC。</span><span class="sxs-lookup"><span data-stu-id="6cddc-126">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="6cddc-127">如果您已經知道您想要在虛擬機器上測試的 IP 位址，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="6cddc-127">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="6cddc-128">執行 IP 流量驗證</span><span class="sxs-lookup"><span data-stu-id="6cddc-128">Run IP flow verify</span></span>

<span data-ttu-id="6cddc-129">既然我們已經擁有了執行 Cmdlet 所需的資訊，我們可以執行 `network watcher ip-flow-verify` Cmdlet 來測試流量。</span><span class="sxs-lookup"><span data-stu-id="6cddc-129">Now that we have the information needed to run the cmdlet, we run the `network watcher ip-flow-verify` cmdlet to test the traffic.</span></span> <span data-ttu-id="6cddc-130">在此範例中，我們會使用第一個 NIC 上的第一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6cddc-130">In this example, we are using the first IP address on the first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> <span data-ttu-id="6cddc-131">IP 流量驗證需要配置 VM 資源以供執行。</span><span class="sxs-lookup"><span data-stu-id="6cddc-131">IP Flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="6cddc-132">檢閱結果</span><span class="sxs-lookup"><span data-stu-id="6cddc-132">Review Results</span></span>

<span data-ttu-id="6cddc-133">`network watcher ip-flow-verify` 執行後會傳回結果，下列範例就是上一個步驟所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="6cddc-133">After running `network watcher ip-flow-verify` the results are returned, the following example is the results returned from the preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="6cddc-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6cddc-134">Next steps</span></span>

<span data-ttu-id="6cddc-135">如果流量遭到封鎖，但不應如此，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)以追蹤網路安全性群組和所定義的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="6cddc-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="6cddc-136">請造訪[使用網路監看員稽核網路安全性群組 (NSG)](network-watcher-nsg-auditing-powershell.md) 以了解如何稽核 NSG 設定。</span><span class="sxs-lookup"><span data-stu-id="6cddc-136">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
