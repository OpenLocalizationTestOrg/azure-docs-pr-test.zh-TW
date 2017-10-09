---
title: "驗證與 Azure 網路監看員 IP 流量 aaaVerify 流量-REST |Microsoft 文件"
description: "本文說明如何 toocheck 如果允許或拒絕流量 tooor 從虛擬機器"
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
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="bd4bf-103">使用 Azure 網路監看員的 IP 流程驗證元件來檢查流量是被允許或拒絕</span><span class="sxs-lookup"><span data-stu-id="bd4bf-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="bd4bf-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bd4bf-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="bd4bf-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd4bf-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="bd4bf-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bd4bf-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="bd4bf-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bd4bf-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="bd4bf-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="bd4bf-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="bd4bf-109">IP 流量驗證是一項功能可讓您 tooverify 如果允許 tooor 從虛擬機器的流量的網路監看員。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="bd4bf-110">hello 驗證可以執行傳入或傳出的流量。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="bd4bf-111">這個案例中很有用 tooget 的虛擬機器是否可以彼此通訊 tooan 外部資源或後端的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="bd4bf-112">IP 流量確認是否可使用的 tooverify，是否您的網路安全性群組 (NSG) 規則都已正確設定及疑難排解 NSG 規則而遭到封鎖的流量。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="bd4bf-113">另一個原因需要使用 IP 流程可讓您確認是否想要封鎖 tooensure 流量正在封鎖正確 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bd4bf-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="bd4bf-114">Before you begin</span></span>

<span data-ttu-id="bd4bf-115">ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-115">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="bd4bf-116">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="bd4bf-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="bd4bf-117">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-117">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="bd4bf-118">案例</span><span class="sxs-lookup"><span data-stu-id="bd4bf-118">Scenario</span></span>

<span data-ttu-id="bd4bf-119">此案例使用 IP 流量確認 tooverify，如果虛擬機器可以彼此 tooanother 機器通訊透過連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-119">This scenario uses IP flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="bd4bf-120">如果 hello 流量遭到拒絕，它會傳回 hello 安全性規則，拒絕的流量。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="bd4bf-121">進一步了解 IP 流量，請確認 toolearn 造訪[IP 流量確認概觀](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bd4bf-121">toolearn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="bd4bf-122">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="bd4bf-122">In this scenario, you:</span></span>

* <span data-ttu-id="bd4bf-123">擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bd4bf-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="bd4bf-124">呼叫 IP 流程驗證</span><span class="sxs-lookup"><span data-stu-id="bd4bf-124">Call IP flow verify</span></span>
* <span data-ttu-id="bd4bf-125">驗證結果</span><span class="sxs-lookup"><span data-stu-id="bd4bf-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="bd4bf-126">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="bd4bf-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="bd4bf-127">擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bd4bf-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="bd4bf-128">執行下列指令碼 tooreturn hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-128">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="bd4bf-129">hello 下列程式碼需要的值為 hello 變數：</span><span class="sxs-lookup"><span data-stu-id="bd4bf-129">hello following code needs values for hello variables:</span></span>

* <span data-ttu-id="bd4bf-130">**subscriptionId** -hello 訂用帳戶 Id toouse。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-130">**subscriptionId** - hello subscription Id toouse.</span></span>
* <span data-ttu-id="bd4bf-131">**resourceGroupName** -hello 包含虛擬機器的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-131">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="bd4bf-132">hello 所需的資訊是 hello 識別碼 hello 類型之下`Microsoft.Compute/virtualMachines`。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-132">hello information that is needed is hello id under hello type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="bd4bf-133">hello 結果應該類似下列程式碼範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="bd4bf-133">hello results should be similar toohello following code sample:</span></span>

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

## <a name="call-ip-flow-verify"></a><span data-ttu-id="bd4bf-134">呼叫 IP 流程驗證</span><span class="sxs-lookup"><span data-stu-id="bd4bf-134">Call IP flow Verify</span></span>

<span data-ttu-id="bd4bf-135">hello 下列範例會建立指定的虛擬機器要求 tooverify hello 流量。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-135">hello following example creates a request tooverify hello traffic for a specified virtual machine.</span></span> <span data-ttu-id="bd4bf-136">如果允許 hello 流量或 hello 流量遭到拒絕，就會傳回 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-136">hello response returns if hello traffic is allowed or if hello traffic is denied.</span></span> <span data-ttu-id="bd4bf-137">如果已拒絕的流量，它也會傳回哪些規則區塊 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-137">If traffic is denied it also returns what rule blocks hello traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="bd4bf-138">IP 流量確認需要 hello VM 資源一配置。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-138">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="bd4bf-139">hello 指令碼需要 hello 資源識別碼和 hello 虛擬機器上的網路介面卡的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-139">hello script requires hello resource Id of a virtual machine and of a network interface card on hello virtual machine.</span></span> <span data-ttu-id="bd4bf-140">Hello，上述輸出會提供這些值。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-140">These values are provided by hello preceding output.</span></span>

> [!Important]
> <span data-ttu-id="bd4bf-141">所有網路監看員 REST 呼叫 hello hello 要求 URI 為 hello 另一個則包含 hello 網路監看員執行個體，不會 hello 您執行的 hello 診斷動作的資源中的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-141">For all Network Watcher REST calls hello resource group name in hello request URI is hello one that contains hello Network Watcher instance, not hello resources you are performing hello diagnostic actions on.</span></span>

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

## <a name="understanding-hello-results"></a><span data-ttu-id="bd4bf-142">了解 hello 結果</span><span class="sxs-lookup"><span data-stu-id="bd4bf-142">Understanding hello results</span></span>

<span data-ttu-id="bd4bf-143">您會回到 hello 回應會告訴您是否允許或拒絕 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-143">hello response you get back tells you whether hello traffic is allowed or denied.</span></span> <span data-ttu-id="bd4bf-144">hello 回應看起來像 hello 遵循範例的其中一個：</span><span class="sxs-lookup"><span data-stu-id="bd4bf-144">hello response looks like one of hello following examples:</span></span>

<span data-ttu-id="bd4bf-145">**允許**</span><span class="sxs-lookup"><span data-stu-id="bd4bf-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="bd4bf-146">**拒絕**</span><span class="sxs-lookup"><span data-stu-id="bd4bf-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="bd4bf-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd4bf-147">Next steps</span></span>

<span data-ttu-id="bd4bf-148">如果正在封鎖流量，不應該看到[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)toolearn 更多關於網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="bd4bf-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn more about Network Security Groups.</span></span>












