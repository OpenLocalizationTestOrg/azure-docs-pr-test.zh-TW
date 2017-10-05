---
title: "使用 Azure 網路監看員 IP 流量驗證來驗證流量 - Azure 入口網站 | Microsoft Docs"
description: "本文說明如何檢查虛擬機器中的流入或流出流量是被允許或拒絕"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7db29c186cf6e6f3b40a680ab76f1d2763f806ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="59e21-103">使用 Azure 網路監看員的 IP 流量驗證元件來檢查 VM 中的流入或流出流量是被允許或拒絕</span><span class="sxs-lookup"><span data-stu-id="59e21-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="59e21-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="59e21-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="59e21-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="59e21-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="59e21-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="59e21-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="59e21-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="59e21-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="59e21-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="59e21-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="59e21-109">IP 流量驗證是網路監看員的一項功能，可讓您驗證虛擬機器中的流入或流出流量是否被允許。</span><span class="sxs-lookup"><span data-stu-id="59e21-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="59e21-110">可執行傳入或傳出流量的驗證。</span><span class="sxs-lookup"><span data-stu-id="59e21-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="59e21-111">此案例可用於取得虛擬機器的目前狀態，以了解其是否可以和外部資源或其他資源。</span><span class="sxs-lookup"><span data-stu-id="59e21-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or another resource.</span></span> <span data-ttu-id="59e21-112">IP 流量驗證可用來驗證是否已正確設定網路安全性群組 (NSG) 規則，並針對 NSG 規則所封鎖的流量進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="59e21-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="59e21-113">使用 IP 流量驗證的另一個原因是可以確保 NSG 會正確封鎖您想要封鎖的流量。</span><span class="sxs-lookup"><span data-stu-id="59e21-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="59e21-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="59e21-114">Before you begin</span></span>

<span data-ttu-id="59e21-115">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員，或您擁有現有的網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="59e21-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="59e21-116">此案例也假設已有具有有效虛擬機器的資源群組可供使用。</span><span class="sxs-lookup"><span data-stu-id="59e21-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="59e21-117">案例</span><span class="sxs-lookup"><span data-stu-id="59e21-117">Scenario</span></span>

<span data-ttu-id="59e21-118">此案例使用 IP 流量驗證來驗證虛擬機器是否可以透過連接埠 443 和其他機器通訊。</span><span class="sxs-lookup"><span data-stu-id="59e21-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="59e21-119">如果流量被拒絕，它會傳回拒絕該流量的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="59e21-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="59e21-120">若要深入了解 IP 流量驗證，請造訪 [IP 流量驗證概觀](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="59e21-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="59e21-121">執行 IP 流量驗證</span><span class="sxs-lookup"><span data-stu-id="59e21-121">Run IP flow verify</span></span>

<span data-ttu-id="59e21-122">瀏覽至您的網路監看員，然後按一下 [IP 流量驗證]。</span><span class="sxs-lookup"><span data-stu-id="59e21-122">Navigate to your Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="59e21-123">選取虛擬機器和您想要驗證流量的網路介面。</span><span class="sxs-lookup"><span data-stu-id="59e21-123">Select the virtual machine and network interface you want to verify traffic from.</span></span> <span data-ttu-id="59e21-124">輸入任何其他篩選的資訊，然後按一下 [檢查]。</span><span class="sxs-lookup"><span data-stu-id="59e21-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="59e21-125">一旦您按一下 [檢查]，會檢查根據您提供之準則的流程。</span><span class="sxs-lookup"><span data-stu-id="59e21-125">Once you click **Check**, the flow based on the criteria you provided is checked.</span></span> <span data-ttu-id="59e21-126">結果是**允許存取**或**拒絕存取**。</span><span class="sxs-lookup"><span data-stu-id="59e21-126">The result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="59e21-127">如果存取被拒，會提供封鎖流量的網路安全性群組 (NSG) 和安全性規則。</span><span class="sxs-lookup"><span data-stu-id="59e21-127">If access is denied, the Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="59e21-128">如果拒絕流量是預期的行為，則此規則已成功。</span><span class="sxs-lookup"><span data-stu-id="59e21-128">If the denial of traffic is expected behavior, then the rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="59e21-129">IP 流量驗證需要配置 VM 資源。</span><span class="sxs-lookup"><span data-stu-id="59e21-129">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="59e21-130">您可以從下列映像中看到，允許輸出的 HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="59e21-130">As you can see from the following image, the outbound HTTPS traffic was allowed.</span></span>

![IP 流量驗證概觀][1]

<span data-ttu-id="59e21-132">如下圖所示，流量會變更為輸入，輸入連接埠會變更為 123。</span><span class="sxs-lookup"><span data-stu-id="59e21-132">As seen in the following image, traffic is changed to inbound and the inbound port changed to 123.</span></span> <span data-ttu-id="59e21-133">流量現在會遭拒絕，會提供「拒絕存取」訊息與網路安全性群組以及拒絕流量的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="59e21-133">Traffic is now denied, the message "Access denied" is provided along with the network security group and security rule that deny the traffic.</span></span>

![IP 流量結果][2]

## <a name="next-steps"></a><span data-ttu-id="59e21-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59e21-135">Next steps</span></span>

<span data-ttu-id="59e21-136">如果流量遭到封鎖，但不應如此，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)以追蹤網路安全性群組和所定義的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="59e21-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













