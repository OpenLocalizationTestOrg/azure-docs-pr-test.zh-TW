---
title: "驗證與 Azure 網路監看員 IP 流量 aaaverify 流量-PowerShell |Microsoft 文件"
description: "本文說明如何 toocheck 如果從虛擬機器的流量 tooor 允許或拒絕使用 PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="368f2-103">如果允許或拒絕 VM 與 IP 流量 tooor 流量檢查，請確定 Azure 網路監看員的元件</span><span class="sxs-lookup"><span data-stu-id="368f2-103">Check if traffic is allowed or denied tooor from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="368f2-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="368f2-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="368f2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="368f2-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="368f2-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="368f2-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="368f2-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="368f2-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="368f2-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="368f2-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="368f2-109">IP 流量驗證是一項功能可讓您 tooverify 如果允許 tooor 從虛擬機器的流量的網路監看員。</span><span class="sxs-lookup"><span data-stu-id="368f2-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="368f2-110">這個案例中很有用 tooget 的虛擬機器是否可以彼此通訊 tooan 外部資源或後端的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="368f2-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="368f2-111">IP 流量確認是否可使用的 tooverify，是否您的網路安全性群組 (NSG) 規則都已正確設定及疑難排解 NSG 規則而遭到封鎖的流量。</span><span class="sxs-lookup"><span data-stu-id="368f2-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="368f2-112">另一個原因需要使用 IP 流程可讓您確認是否想要封鎖 tooensure 流量正在封鎖正確 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="368f2-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="368f2-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="368f2-113">Before you begin</span></span>

<span data-ttu-id="368f2-114">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員或具有網路監看員的現有執行個體。</span><span class="sxs-lookup"><span data-stu-id="368f2-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="368f2-115">hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="368f2-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="368f2-116">案例</span><span class="sxs-lookup"><span data-stu-id="368f2-116">Scenario</span></span>

<span data-ttu-id="368f2-117">這個案例使用 IP 流量，如果虛擬機器可以彼此 tooa 通訊已知驗證 tooverify Bing IP 位址。</span><span class="sxs-lookup"><span data-stu-id="368f2-117">This scenario uses IP flow verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="368f2-118">如果 hello 流量遭到拒絕，它會傳回 hello 安全性規則，拒絕的流量。</span><span class="sxs-lookup"><span data-stu-id="368f2-118">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="368f2-119">更多關於 IP 流程驗證，請造訪 toolearn [IP 流量確認概觀](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="368f2-119">toolearn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="368f2-120">擷取網路監看員</span><span class="sxs-lookup"><span data-stu-id="368f2-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="368f2-121">hello 第一個步驟是 tooretrieve hello 網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="368f2-121">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="368f2-122">hello`$networkWatcher`變數傳遞 toohello IP 流量驗證指令程式。</span><span class="sxs-lookup"><span data-stu-id="368f2-122">hello `$networkWatcher` variable is passed toohello IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="368f2-123">取得 VM</span><span class="sxs-lookup"><span data-stu-id="368f2-123">Get a VM</span></span>

<span data-ttu-id="368f2-124">IP 流量，請確認測試流量 tooor 從虛擬機器 tooor 從遠端目的地上的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="368f2-124">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="368f2-125">Hello cmdlet 需要虛擬機器的識別碼。</span><span class="sxs-lookup"><span data-stu-id="368f2-125">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="368f2-126">如果您已經知道 hello 虛擬機器 toouse hello 識別碼，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="368f2-126">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a><span data-ttu-id="368f2-127">取得 hello NIC</span><span class="sxs-lookup"><span data-stu-id="368f2-127">Get hello NICS</span></span>

<span data-ttu-id="368f2-128">需要 hello 的 hello 虛擬機器上的 NIC 的 IP 位址，在此範例中我們擷取 hello Nic 的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="368f2-128">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="368f2-129">如果您已經知道 hello IP 位址，您會想 tootest hello 虛擬機器上，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="368f2-129">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="368f2-130">執行 IP 流量驗證</span><span class="sxs-lookup"><span data-stu-id="368f2-130">Run IP flow verify</span></span>

<span data-ttu-id="368f2-131">現在，我們已經 hello 資訊所需 toorun hello 指令程式，我們會執行 hello `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello 流量。</span><span class="sxs-lookup"><span data-stu-id="368f2-131">Now that we have hello information needed toorun hello cmdlet, we run hello `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="368f2-132">在此範例中，我們會使用第一個 IP 位址 hello hello 第一個 NIC 上</span><span class="sxs-lookup"><span data-stu-id="368f2-132">In this example, we are using hello first IP address on hello first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="368f2-133">IP 流量確認需要 hello VM 資源配置 toorun。</span><span class="sxs-lookup"><span data-stu-id="368f2-133">IP flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="368f2-134">檢閱結果</span><span class="sxs-lookup"><span data-stu-id="368f2-134">Review Results</span></span>

<span data-ttu-id="368f2-135">執行之後`Test-AzureRmNetworkWatcherIPFlow`hello 結果、 hello 下列範例是 hello hello 前面步驟所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="368f2-135">After running `Test-AzureRmNetworkWatcherIPFlow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="368f2-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="368f2-136">Next steps</span></span>

<span data-ttu-id="368f2-137">如果正在封鎖流量，不應該看到[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack hello 網路安全性群組和安全性規則所定義的關閉。</span><span class="sxs-lookup"><span data-stu-id="368f2-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













