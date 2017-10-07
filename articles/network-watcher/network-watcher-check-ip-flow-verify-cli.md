---
title: "與 Azure 網路監看員 IP 流程驗證-Azure CLI aaaVerify 流量 |Microsoft 文件"
description: "本文說明如何從虛擬機器的流量 tooor 允許或拒絕使用 Azure CLI 如果 toocheck"
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
ms.openlocfilehash: 128a00b4296994551e7e17838a51e6d9de180e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="c8510-103">如果是允許或拒絕流量 tooor 從 IP 流程驗證 VM 的 Azure 網路監看員的元件，請檢查</span><span class="sxs-lookup"><span data-stu-id="c8510-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c8510-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c8510-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="c8510-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8510-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="c8510-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c8510-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="c8510-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c8510-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="c8510-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="c8510-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="c8510-109">IP 流程驗證是一項功能可讓您 tooverify 如果允許 tooor 從虛擬機器的流量的網路監看員。</span><span class="sxs-lookup"><span data-stu-id="c8510-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="c8510-110">這個案例中很有用 tooget 的虛擬機器是否可以彼此通訊 tooan 外部資源或後端的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="c8510-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="c8510-111">IP 流量確認是否可使用的 tooverify，是否您的網路安全性群組 (NSG) 規則都已正確設定及疑難排解 NSG 規則而遭到封鎖的流量。</span><span class="sxs-lookup"><span data-stu-id="c8510-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="c8510-112">另一個原因需要使用 IP 流程可讓您確認是否想要封鎖 tooensure 流量正在封鎖正確 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="c8510-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="c8510-113">本文使用我們的下一個層代 CLI hello 資源管理部署模型，Azure CLI 2.0 中，這是適用於 Windows、 Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="c8510-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="c8510-114">tooperform hello 步驟在本文中，您需要[hello Azure 命令列介面安裝的 Mac、 Linux 及 Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="c8510-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c8510-115">開始之前</span><span class="sxs-lookup"><span data-stu-id="c8510-115">Before you begin</span></span>

<span data-ttu-id="c8510-116">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員或具有網路監看員的現有執行個體。</span><span class="sxs-lookup"><span data-stu-id="c8510-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="c8510-117">hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="c8510-117">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="c8510-118">案例</span><span class="sxs-lookup"><span data-stu-id="c8510-118">Scenario</span></span>

<span data-ttu-id="c8510-119">此案例使用 IP 流程確認 tooverify，如果虛擬機器可以彼此 tooa 通訊已知 Bing IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c8510-119">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="c8510-120">如果 hello 流量遭到拒絕，它會傳回 hello 安全性規則，拒絕的流量。</span><span class="sxs-lookup"><span data-stu-id="c8510-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="c8510-121">toolearn 深入了解 IP 流程驗證，請瀏覽[IP 流程確認概觀](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c8510-121">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="c8510-122">取得 VM</span><span class="sxs-lookup"><span data-stu-id="c8510-122">Get a VM</span></span>

<span data-ttu-id="c8510-123">IP 流量，請確認測試流量 tooor 從虛擬機器 tooor 從遠端目的地上的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c8510-123">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="c8510-124">Hello cmdlet 需要虛擬機器的識別碼。</span><span class="sxs-lookup"><span data-stu-id="c8510-124">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="c8510-125">如果您已經知道 hello 虛擬機器 toouse hello 識別碼，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="c8510-125">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-hello-nics"></a><span data-ttu-id="c8510-126">取得 hello NIC</span><span class="sxs-lookup"><span data-stu-id="c8510-126">Get hello NICS</span></span>

<span data-ttu-id="c8510-127">需要 hello 的 hello 虛擬機器上的 NIC 的 IP 位址，在此範例中我們擷取 hello Nic 的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="c8510-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="c8510-128">如果您已經知道 hello IP 位址，您會想 tootest hello 虛擬機器上，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="c8510-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="c8510-129">執行 IP 流量驗證</span><span class="sxs-lookup"><span data-stu-id="c8510-129">Run IP flow verify</span></span>

<span data-ttu-id="c8510-130">現在，我們已經 hello 資訊所需 toorun hello 指令程式，我們會執行 hello `az network watcher test-ip-flow` cmdlet tootest hello 流量。</span><span class="sxs-lookup"><span data-stu-id="c8510-130">Now that we have hello information needed toorun hello cmdlet, we run hello `az network watcher test-ip-flow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="c8510-131">在此範例中，我們會使用第一個 IP 位址 hello hello 第一個 NIC 上</span><span class="sxs-lookup"><span data-stu-id="c8510-131">In this example, we are using hello first IP address on hello first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="c8510-132">需要 hello VM 資源配置 toorun IP 流程驗證。</span><span class="sxs-lookup"><span data-stu-id="c8510-132">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="c8510-133">檢閱結果</span><span class="sxs-lookup"><span data-stu-id="c8510-133">Review Results</span></span>

<span data-ttu-id="c8510-134">執行之後`az network watcher test-ip-flow`hello 結果、 hello 下列範例是 hello hello 前面步驟所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="c8510-134">After running `az network watcher test-ip-flow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="c8510-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8510-135">Next steps</span></span>

<span data-ttu-id="c8510-136">如果正在封鎖流量，不應該看到[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack hello 網路安全性群組和安全性規則所定義的關閉。</span><span class="sxs-lookup"><span data-stu-id="c8510-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="c8510-137">深入了解 tooaudit NSG 設定造訪[稽核網路安全性群組群組 (NSG) 與網路監看員](network-watcher-nsg-auditing-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="c8510-137">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
