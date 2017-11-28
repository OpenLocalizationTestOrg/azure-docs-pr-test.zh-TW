---
title: "驗證與 Azure 網路監看員 IP 流量 aaaVerify 流量-Azure 入口網站 |Microsoft 文件"
description: "本文說明如何 toocheck 如果允許或拒絕流量 tooor 從虛擬機器"
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
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="75a96-103">如果是允許或拒絕流量 tooor 從 IP 流程驗證 VM 的 Azure 網路監看員的元件，請檢查</span><span class="sxs-lookup"><span data-stu-id="75a96-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="75a96-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="75a96-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="75a96-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="75a96-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="75a96-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="75a96-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="75a96-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="75a96-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="75a96-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="75a96-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="75a96-109">IP 流量驗證是一項功能可讓您 tooverify 如果允許 tooor 從虛擬機器的流量的網路監看員。</span><span class="sxs-lookup"><span data-stu-id="75a96-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="75a96-110">hello 驗證可以執行傳入或傳出的流量。</span><span class="sxs-lookup"><span data-stu-id="75a96-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="75a96-111">這個案例中很有用 tooget 的虛擬機器是否可以彼此通訊 tooan 外部資源或其他資源的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="75a96-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or another resource.</span></span> <span data-ttu-id="75a96-112">IP 流量確認是否可使用的 tooverify，是否您的網路安全性群組 (NSG) 規則都已正確設定及疑難排解 NSG 規則而遭到封鎖的流量。</span><span class="sxs-lookup"><span data-stu-id="75a96-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="75a96-113">另一個原因需要使用 IP 流程可讓您確認是否想要封鎖 tooensure 流量正在封鎖正確 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="75a96-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="75a96-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="75a96-114">Before you begin</span></span>

<span data-ttu-id="75a96-115">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員或具有網路監看員的現有執行個體。</span><span class="sxs-lookup"><span data-stu-id="75a96-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="75a96-116">hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="75a96-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="75a96-117">案例</span><span class="sxs-lookup"><span data-stu-id="75a96-117">Scenario</span></span>

<span data-ttu-id="75a96-118">此案例使用 IP 流程確認 tooverify，如果虛擬機器可以彼此 tooanother 機器通訊透過連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="75a96-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="75a96-119">如果 hello 流量遭到拒絕，它會傳回 hello 安全性規則，拒絕的流量。</span><span class="sxs-lookup"><span data-stu-id="75a96-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="75a96-120">toolearn 深入了解 IP 流程驗證，請瀏覽[IP 流程確認概觀](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="75a96-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="75a96-121">執行 IP 流量驗證</span><span class="sxs-lookup"><span data-stu-id="75a96-121">Run IP flow verify</span></span>

<span data-ttu-id="75a96-122">瀏覽 tooyour 網路監看員，並按一下**IP 流量確認**。</span><span class="sxs-lookup"><span data-stu-id="75a96-122">Navigate tooyour Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="75a96-123">選取 hello 虛擬機器和網路介面您想要從 tooverify 流量。</span><span class="sxs-lookup"><span data-stu-id="75a96-123">Select hello virtual machine and network interface you want tooverify traffic from.</span></span> <span data-ttu-id="75a96-124">輸入任何其他篩選的資訊，然後按一下 [檢查]。</span><span class="sxs-lookup"><span data-stu-id="75a96-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="75a96-125">一旦您按一下**檢查**，會檢查您所提供的 hello 準則為基礎的 hello 流程。</span><span class="sxs-lookup"><span data-stu-id="75a96-125">Once you click **Check**, hello flow based on hello criteria you provided is checked.</span></span> <span data-ttu-id="75a96-126">hello 結果是**允許存取**或**拒絕存取**。</span><span class="sxs-lookup"><span data-stu-id="75a96-126">hello result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="75a96-127">如果存取被拒，hello 網路安全性群組 (NSG)，並提供封鎖流量的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="75a96-127">If access is denied, hello Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="75a96-128">Hello 拒絕的流量是預期的行為，然後 hello 規則成功。</span><span class="sxs-lookup"><span data-stu-id="75a96-128">If hello denial of traffic is expected behavior, then hello rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="75a96-129">IP 流量確認需要 hello VM 資源一配置。</span><span class="sxs-lookup"><span data-stu-id="75a96-129">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="75a96-130">您可以從下列映像的 hello 看到，已允許 hello 輸出的 HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="75a96-130">As you can see from hello following image, hello outbound HTTPS traffic was allowed.</span></span>

![IP 流量驗證概觀][1]

<span data-ttu-id="75a96-132">Hello 下列影像所示，變更流量 tooinbound 和 hello 輸入連接埠變更 too123。</span><span class="sxs-lookup"><span data-stu-id="75a96-132">As seen in hello following image, traffic is changed tooinbound and hello inbound port changed too123.</span></span> <span data-ttu-id="75a96-133">現在拒絕的流量，以及 hello 網路安全性群組和安全性規則，拒絕 hello 流量提供 hello 訊息 「 拒絕存取 」。</span><span class="sxs-lookup"><span data-stu-id="75a96-133">Traffic is now denied, hello message "Access denied" is provided along with hello network security group and security rule that deny hello traffic.</span></span>

![IP 流量結果][2]

## <a name="next-steps"></a><span data-ttu-id="75a96-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75a96-135">Next steps</span></span>

<span data-ttu-id="75a96-136">如果正在封鎖流量，不應該看到[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack hello 網路安全性群組和安全性規則所定義的關閉。</span><span class="sxs-lookup"><span data-stu-id="75a96-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













