---
title: "使用 Azure 網路監看員 IP 流程驗證來驗證流量 - REST | Microsoft Docs"
description: "本文說明如何檢查虛擬機器中的流入或流出流量是被允許或拒絕"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 6d3ce00a7d4f9c0cd57fa8815625a1065b03b5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="7958f-103">使用 Azure 網路監看員的 IP 流程驗證元件來檢查流量是被允許或拒絕</span><span class="sxs-lookup"><span data-stu-id="7958f-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7958f-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7958f-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="7958f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7958f-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="7958f-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7958f-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="7958f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7958f-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="7958f-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="7958f-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="7958f-109">IP 流量驗證是網路監看員的一項功能，可讓您驗證虛擬機器中的流入或流出流量是否被允許。</span><span class="sxs-lookup"><span data-stu-id="7958f-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="7958f-110">可執行傳入或傳出流量的驗證。</span><span class="sxs-lookup"><span data-stu-id="7958f-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="7958f-111">此案例可用於取得虛擬機器的目前狀態，以了解其是否可以和外部資源或後端通訊。</span><span class="sxs-lookup"><span data-stu-id="7958f-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="7958f-112">IP 流量驗證可用來驗證是否已正確設定網路安全性群組 (NSG) 規則，並針對 NSG 規則所封鎖的流量進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="7958f-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="7958f-113">使用 IP 流量驗證的另一個原因是可以確保 NSG 會正確封鎖您想要封鎖的流量。</span><span class="sxs-lookup"><span data-stu-id="7958f-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7958f-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="7958f-114">Before you begin</span></span>

<span data-ttu-id="7958f-115">使用 ARMclient 透過 PowerShell 呼叫 REST API。</span><span class="sxs-lookup"><span data-stu-id="7958f-115">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="7958f-116">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="7958f-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="7958f-117">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="7958f-117">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="7958f-118">案例</span><span class="sxs-lookup"><span data-stu-id="7958f-118">Scenario</span></span>

<span data-ttu-id="7958f-119">此案例使用 IP 流程驗證來確認虛擬機器是否可以透過連接埠 443 與其他機器進行通訊。</span><span class="sxs-lookup"><span data-stu-id="7958f-119">This scenario uses IP flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="7958f-120">如果流量被拒絕，它會傳回拒絕該流量的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="7958f-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="7958f-121">若要深入了解 IP 流程驗證，請瀏覽 [IP 流程驗證概觀 (英文)](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7958f-121">To learn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="7958f-122">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="7958f-122">In this scenario, you:</span></span>

* <span data-ttu-id="7958f-123">擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7958f-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="7958f-124">呼叫 IP 流程驗證</span><span class="sxs-lookup"><span data-stu-id="7958f-124">Call IP flow verify</span></span>
* <span data-ttu-id="7958f-125">驗證結果</span><span class="sxs-lookup"><span data-stu-id="7958f-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="7958f-126">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="7958f-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="7958f-127">擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7958f-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="7958f-128">執行下列指令碼，以傳回虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7958f-128">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="7958f-129">下列程式碼需要變數值︰</span><span class="sxs-lookup"><span data-stu-id="7958f-129">The following code needs values for the variables:</span></span>

* <span data-ttu-id="7958f-130">**subscriptionId** - 要使用的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="7958f-130">**subscriptionId** - The subscription Id to use.</span></span>
* <span data-ttu-id="7958f-131">**resourceGroupName** - 包含虛擬機器的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="7958f-131">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="7958f-132">所需資訊是類型 `Microsoft.Compute/virtualMachines` 下的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7958f-132">The information that is needed is the id under the type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="7958f-133">結果應該會與下列程式碼範例類似：</span><span class="sxs-lookup"><span data-stu-id="7958f-133">The results should be similar to the following code sample:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a><span data-ttu-id="7958f-134">呼叫 IP 流程驗證</span><span class="sxs-lookup"><span data-stu-id="7958f-134">Call IP flow Verify</span></span>

<span data-ttu-id="7958f-135">下列範例會建立要求來驗證指定虛擬機器的流量。</span><span class="sxs-lookup"><span data-stu-id="7958f-135">The following example creates a request to verify the traffic for a specified virtual machine.</span></span> <span data-ttu-id="7958f-136">回應會傳回流量是被允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="7958f-136">The response returns if the traffic is allowed or if the traffic is denied.</span></span> <span data-ttu-id="7958f-137">如果流量被拒絕，它也會傳回封鎖該流量的規則。</span><span class="sxs-lookup"><span data-stu-id="7958f-137">If traffic is denied it also returns what rule blocks the traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="7958f-138">IP 流量驗證需要配置 VM 資源。</span><span class="sxs-lookup"><span data-stu-id="7958f-138">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="7958f-139">指令碼需要虛擬機器的資源識別碼和虛擬機器上網路介面的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="7958f-139">The script requires the resource Id of a virtual machine and of a network interface card on the virtual machine.</span></span> <span data-ttu-id="7958f-140">上述輸出會提供這些值。</span><span class="sxs-lookup"><span data-stu-id="7958f-140">These values are provided by the preceding output.</span></span>

> [!Important]
> <span data-ttu-id="7958f-141">針對所有網路監看員 REST 呼叫，要求 URI 中的資源群組名稱是包含網路監看員執行個體的那一個，而非要對其執行診斷動作的資源。</span><span class="sxs-lookup"><span data-stu-id="7958f-141">For all Network Watcher REST calls the resource group name in the request URI is the one that contains the Network Watcher instance, not the resources you are performing the diagnostic actions on.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-the-results"></a><span data-ttu-id="7958f-142">了解結果</span><span class="sxs-lookup"><span data-stu-id="7958f-142">Understanding the results</span></span>

<span data-ttu-id="7958f-143">您收到的回應會告訴您流量是被允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="7958f-143">The response you get back tells you whether the traffic is allowed or denied.</span></span> <span data-ttu-id="7958f-144">回應看起來就像下列其中一個範例︰</span><span class="sxs-lookup"><span data-stu-id="7958f-144">The response looks like one of the following examples:</span></span>

<span data-ttu-id="7958f-145">**允許**</span><span class="sxs-lookup"><span data-stu-id="7958f-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="7958f-146">**拒絕**</span><span class="sxs-lookup"><span data-stu-id="7958f-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="7958f-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7958f-147">Next steps</span></span>

<span data-ttu-id="7958f-148">如果流量遭到封鎖，但不應如此，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)以深入了解網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="7958f-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to learn more about Network Security Groups.</span></span>












