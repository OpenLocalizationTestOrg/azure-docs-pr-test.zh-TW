---
title: "aaaAzure DMZ 範例 – 建立簡單的周邊網路與 Nsg |Microsoft 文件"
description: "建置具有網路安全性群組 (NSG) 的 DMZ"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="b9208-103">範例 1 – 使用 NSG 搭配傳統 PowerShell 建立簡單的 DMZ</span><span class="sxs-lookup"><span data-stu-id="b9208-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="b9208-104">[傳回 toohello 安全性界限最佳作法頁面][HOME]</span><span class="sxs-lookup"><span data-stu-id="b9208-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b9208-105">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="b9208-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="b9208-106">傳統 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9208-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="b9208-107">此範例會建立包含四個 Windows 伺服器和網路安全性群組的基本 DMZ。</span><span class="sxs-lookup"><span data-stu-id="b9208-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="b9208-108">這個範例會說明每個相關 PowerShell 命令 tooprovide hello 更深入的了解每個步驟。</span><span class="sxs-lookup"><span data-stu-id="b9208-108">This example describes each of hello relevant PowerShell commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="b9208-109">另外還有流量案例 > 一節 tooprovide 的深入了解逐步如何流量就會繼續進行 hello 層級的防禦 hello 周邊網路。</span><span class="sxs-lookup"><span data-stu-id="b9208-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="b9208-110">最後，在 hello references 區段中是 hello 完整程式碼和指示 toobuild 此環境 tootest 和試驗各種案例。</span><span class="sxs-lookup"><span data-stu-id="b9208-110">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="b9208-111">![具有 NSG 的輸入 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="b9208-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="b9208-112">環境描述</span><span class="sxs-lookup"><span data-stu-id="b9208-112">Environment description</span></span>
<span data-ttu-id="b9208-113">在此範例中的訂用帳戶包含 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="b9208-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="b9208-114">兩個雲端服務：“FrontEnd001” 和 “BackEnd001”</span><span class="sxs-lookup"><span data-stu-id="b9208-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="b9208-115">一個虛擬網路 “CorpNetwork”，包含兩個子網路：“FrontEnd” 和 “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="b9208-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="b9208-116">已套用的 tooboth 子網路的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="b9208-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="b9208-117">一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)</span><span class="sxs-lookup"><span data-stu-id="b9208-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="b9208-118">兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="b9208-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="b9208-119">一個代表 DNS 伺服器的 Windows Server ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="b9208-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="b9208-120">在 hello 參考區段中，沒有建立大多數的 hello 環境在此範例中所述的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b9208-120">In hello references section, there is a PowerShell script that builds most of hello environment described in this example.</span></span> <span data-ttu-id="b9208-121">建置 hello Vm 和虛擬網路，由 hello 範例指令碼，雖然不詳述於本文件說明。</span><span class="sxs-lookup"><span data-stu-id="b9208-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="b9208-122">toobuild hello 環境。</span><span class="sxs-lookup"><span data-stu-id="b9208-122">toobuild hello environment;</span></span>

1. <span data-ttu-id="b9208-123">儲存 hello 網路組態 xml 檔案包含在 hello 參考一節 （名稱、 位置和 IP 位址 toomatch hello 指定案例與更新）</span><span class="sxs-lookup"><span data-stu-id="b9208-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="b9208-124">Hello 指令碼 toomatch hello 環境 hello 指令碼中的更新 hello 使用者變數是 toobe 執行 （訂用帳戶、 服務名稱等等）</span><span class="sxs-lookup"><span data-stu-id="b9208-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="b9208-125">在 PowerShell 中執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="b9208-125">Execute hello script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="b9208-126">表示在 hello PowerShell 指令碼中的 hello 區域必須符合表示 hello 網路組態 xml 檔中的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="b9208-126">hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>
>
>

<span data-ttu-id="b9208-127">一旦 hello 指令碼執行成功的其他選擇性步驟可能會，hello 參考一節中兩個指令碼 tooset hello web 伺服器和應用程式伺服器與簡單的 web 應用程式 tooallow 測試此周邊網路設定。</span><span class="sxs-lookup"><span data-stu-id="b9208-127">Once hello script runs successfully additional optional steps may be taken, in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="b9208-128">hello 下列各節提供網路安全性群組和其運作方式如這個範例的逐步解說的 hello PowerShell 指令碼的索引鍵行的詳細的的描述。</span><span class="sxs-lookup"><span data-stu-id="b9208-128">hello following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of hello PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="b9208-129">網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="b9208-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="b9208-130">此範例會組建 NSG 群組，然後載入六個規則。</span><span class="sxs-lookup"><span data-stu-id="b9208-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="b9208-131">一般而言，您應該先建立特定的 「 允許 」 規則，然後上次 hello 一般 「 拒絕 」 規則。</span><span class="sxs-lookup"><span data-stu-id="b9208-131">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="b9208-132">指派優先順序的 hello 規定哪些規則會先評估。</span><span class="sxs-lookup"><span data-stu-id="b9208-132">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="b9208-133">一旦流量找到 tooapply tooa 特定規則，則會不評估任何進一步的規則。</span><span class="sxs-lookup"><span data-stu-id="b9208-133">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="b9208-134">NSG 規則可套用在 hello 中輸入或輸出方向 （從 hello 觀點 hello 子網路）。</span><span class="sxs-lookup"><span data-stu-id="b9208-134">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="b9208-135">以宣告方式，下列規則的 hello 正在建置輸入流量：</span><span class="sxs-lookup"><span data-stu-id="b9208-135">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="b9208-136">允許內部 DNS 流量 (連接埠 53)</span><span class="sxs-lookup"><span data-stu-id="b9208-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="b9208-137">允許從 hello 網際網路 tooany VM 的 RDP 流量 （連接埠 3389）</span><span class="sxs-lookup"><span data-stu-id="b9208-137">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="b9208-138">允許從 hello 網際網路 tooweb 伺服器 (IIS01) 的 HTTP 流量 （連接埠 80）</span><span class="sxs-lookup"><span data-stu-id="b9208-138">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="b9208-139">允許從 IIS01 tooAppVM1 任何流量 （所有連接埠）</span><span class="sxs-lookup"><span data-stu-id="b9208-139">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="b9208-140">任何流量 （所有連接埠），從 hello 網際網路 toohello 拒絕整個 VNet （這兩個子網路）</span><span class="sxs-lookup"><span data-stu-id="b9208-140">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="b9208-141">拒絕任何從 hello Frontend 子網路 toohello 後端子網路的流量 （所有連接埠）</span><span class="sxs-lookup"><span data-stu-id="b9208-141">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="b9208-142">與這些規則繫結的 tooeach 子網路中，輸入 hello Internet toohello 網頁伺服器從 HTTP 要求是否兩者的規則 3 （允許） 及 5 （拒絕） 將會套用，但由於規則 3 具有較高的優先順序，只將套用的規則 5 就不會發生。</span><span class="sxs-lookup"><span data-stu-id="b9208-142">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="b9208-143">因此 hello HTTP 要求會允許 toohello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b9208-143">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="b9208-144">如果該相同流量已嘗試 tooreach hello DNS01 伺服器，hello 第一個 tooapply 和 hello 流量就不會允許 toopass toohello 伺服器是規則 5 （拒絕）。</span><span class="sxs-lookup"><span data-stu-id="b9208-144">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="b9208-145">規則 6 (Deny) 會封鎖從交談 toohello 後端的子網路 （除了規則 1 和 4 中允許的流量） hello Frontend 子網路中，如果攻擊者竊取 hello web 上的應用程式 hello 前端，hello 攻擊者就此規則集可保護 hello 後端 」 網路有限存取 toohello 後端 「 受保護 」 (只公開 hello AppVM01 伺服器上的 tooresources) 網路。</span><span class="sxs-lookup"><span data-stu-id="b9208-145">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="b9208-146">沒有預設輸出的規則，可讓流量輸出 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="b9208-146">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="b9208-147">在此範例中，我們會允許輸出流量，並不會修改任何輸出規則。</span><span class="sxs-lookup"><span data-stu-id="b9208-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="b9208-148">toolock 下兩個方向的流量，使用者定義路由是必要項，會在 「 範例 3 」 探索上 hello[安全性界限最佳作法頁面][HOME]。</span><span class="sxs-lookup"><span data-stu-id="b9208-148">toolock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="b9208-149">每個規則中討論更多詳細資料，如下所示 (**注意**: hello 遵循清單開頭，以貨幣符號的任何項目 (例如： $NSGName) 是此文件 hello 參考 > 一節中的 hello 指令碼的使用者定義變數):</span><span class="sxs-lookup"><span data-stu-id="b9208-149">Each rule is discussed in more detail as follows (**Note**: any item in hello following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="b9208-150">第一次網路安全性群組必須建置 toohold hello 規則：</span><span class="sxs-lookup"><span data-stu-id="b9208-150">First a Network Security Group must be built toohold hello rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="b9208-151">在此範例中的 hello 第一個規則可讓 DNS hello 後端子網路上所有的內部網路 toohello DNS 伺服器之間的流量。</span><span class="sxs-lookup"><span data-stu-id="b9208-151">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="b9208-152">hello 規則有一些重要的參數：</span><span class="sxs-lookup"><span data-stu-id="b9208-152">hello rule has some important parameters:</span></span>
   
   * <span data-ttu-id="b9208-153">「類型」表示此規則會生效的傳輸流量方向。</span><span class="sxs-lookup"><span data-stu-id="b9208-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="b9208-154">hello 方向是從 hello 的觀點來看 hello 子網路或虛擬機器 （取決於位置會繫結此 NSG）。</span><span class="sxs-lookup"><span data-stu-id="b9208-154">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="b9208-155">因此如果類型是 「 輸入 」 流量輸入 hello 子網路、 hello 規則將會套用，且離開 hello 子網路的流量不會受到此規則。</span><span class="sxs-lookup"><span data-stu-id="b9208-155">Thus if Type is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="b9208-156">"Priority"設定 hello 順序評估流量。</span><span class="sxs-lookup"><span data-stu-id="b9208-156">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="b9208-157">hello hello 數字 hello 高 hello 優先順序。</span><span class="sxs-lookup"><span data-stu-id="b9208-157">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="b9208-158">當規則適用於特定 tooa 流量時，則會不處理任何進一步的規則。</span><span class="sxs-lookup"><span data-stu-id="b9208-158">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="b9208-159">因此如果優先權 1 的規則允許流量，和優先順序為 2 的規則，拒絕的流量，而且這兩個規則套用 tootraffic 則 hello 流量 someserver.mycompany.com tooflow （因為規則 1 有更高的優先順序花費效果，並套用任何進一步的規則）。</span><span class="sxs-lookup"><span data-stu-id="b9208-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="b9208-160">“Action” 指出受此規則影響的流量是要封鎖或允許。</span><span class="sxs-lookup"><span data-stu-id="b9208-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="b9208-161">此規則可讓您從 hello 網際網路 toohello RDP 連接埠上 hello 的任何伺服器上的 RDP 流量 tooflow 繫結的子網路。</span><span class="sxs-lookup"><span data-stu-id="b9208-161">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> <span data-ttu-id="b9208-162">此規則使用兩種特殊位址前置詞：“VIRTUAL_NETWORK” 和 “INTERNET”。</span><span class="sxs-lookup"><span data-stu-id="b9208-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="b9208-163">這些標記是簡單的方式 tooaddress 較大的類別目錄的位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="b9208-163">These tags are an easy way tooaddress a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="b9208-164">這個規則允許輸入的網際網路流量 toohit hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b9208-164">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="b9208-165">此規則不會變更 hello 路由行為。</span><span class="sxs-lookup"><span data-stu-id="b9208-165">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="b9208-166">hello 規則僅允許針對 IIS01 toopass 的流量。</span><span class="sxs-lookup"><span data-stu-id="b9208-166">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="b9208-167">因此從 hello 網際網路的流量是否有 hello web 伺服器，做為其目的地，此規則會允許它，並停止進一步處理規則。</span><span class="sxs-lookup"><span data-stu-id="b9208-167">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="b9208-168">（在 hello 規則優先順序 140 所有其他傳入的網際網路流量會封鎖）。</span><span class="sxs-lookup"><span data-stu-id="b9208-168">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="b9208-169">如果您只在處理 HTTP 流量，這項規則可以更進一步地限制的 tooonly 允許目的地連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="b9208-169">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="b9208-170">此規則可讓從 hello IIS01 伺服器流量 toopass toohello AppVM01 伺服器，更新規則封鎖所有其他前端 tooBackend 流量。</span><span class="sxs-lookup"><span data-stu-id="b9208-170">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="b9208-171">應加入這項規則，如果 hello 連接埠已知的 tooimprove。</span><span class="sxs-lookup"><span data-stu-id="b9208-171">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="b9208-172">例如，如果 hello IIS 伺服器已達到只有 SQL Server 上 AppVM01，hello 目的地連接埠範圍應該變更"*"（任何） too1433 (hello SQL 連接埠) 進而較小的輸入的攻擊介面上 AppVM01 應該 hello web 應用程式不會受到危害。</span><span class="sxs-lookup"><span data-stu-id="b9208-172">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="b9208-173">此規則會拒絕 hello 網際網路 tooany 網路上的伺服器 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="b9208-173">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="b9208-174">Hello 規則優先順序 110 和 120 hello 效果為 tooallow 只有輸入的網際網路流量 toohello 防火牆和伺服器上的 RDP 連接埠而封鎖所有其他項目。</span><span class="sxs-lookup"><span data-stu-id="b9208-174">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="b9208-175">此規則是 「 保險 」 規則 tooblock 未預期的所有流程。</span><span class="sxs-lookup"><span data-stu-id="b9208-175">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="b9208-176">hello 最終規則，拒絕來自 hello Frontend 子網路 toohello 後端子網路流量。</span><span class="sxs-lookup"><span data-stu-id="b9208-176">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="b9208-177">由於這個規則唯一的輸入的規則，（從後端 toohello 前端 hello) 允許反向的流量。</span><span class="sxs-lookup"><span data-stu-id="b9208-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="b9208-178">流量案例</span><span class="sxs-lookup"><span data-stu-id="b9208-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="b9208-179">(*允許*) 網際網路 tooweb 伺服器</span><span class="sxs-lookup"><span data-stu-id="b9208-179">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="b9208-180">網際網路使用者從 FrontEnd001.CloudApp.Net (網際網路面向雲端服務) 要求 HTTP 頁面</span><span class="sxs-lookup"><span data-stu-id="b9208-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="b9208-181">雲端服務會傳遞流量透過連接埠 80 IIS01 朝上開啟端點 （hello web 伺服器）</span><span class="sxs-lookup"><span data-stu-id="b9208-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="b9208-182">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="b9208-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="b9208-183">NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-183">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="b9208-184">NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-184">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="b9208-185">NSG 規則 3 (網際網路 tooIIS01) 會套用，流量會允許中停止的規則處理</span><span class="sxs-lookup"><span data-stu-id="b9208-185">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="b9208-186">流量叫用內部 IP 位址的 hello web 伺服器 IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="b9208-186">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="b9208-187">IIS01 接聽 web 流量、 收到此要求，並開始處理 hello 要求</span><span class="sxs-lookup"><span data-stu-id="b9208-187">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="b9208-188">IIS01 詢問 hello SQL Server 上 AppVM01 資訊</span><span class="sxs-lookup"><span data-stu-id="b9208-188">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="b9208-189">Frontend 子網路上沒有輸出規則，所以允許流量</span><span class="sxs-lookup"><span data-stu-id="b9208-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="b9208-190">hello 後端子網路會開始處理輸入的規則：</span><span class="sxs-lookup"><span data-stu-id="b9208-190">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="b9208-191">NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-191">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="b9208-192">NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-192">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="b9208-193">NSG 規則 3 (網際網路 tooFirewall) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-193">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="b9208-194">NSG 規則 4 (IIS01 tooAppVM01) 會套用，流量會允許中停止的規則處理</span><span class="sxs-lookup"><span data-stu-id="b9208-194">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="b9208-195">AppVM01 收到 hello SQL 查詢並予以回應</span><span class="sxs-lookup"><span data-stu-id="b9208-195">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="b9208-196">由於 hello 後端子網路上有沒有輸出的規則，允許 hello 回應</span><span class="sxs-lookup"><span data-stu-id="b9208-196">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="b9208-197">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="b9208-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="b9208-198">套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-198">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="b9208-199">hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="b9208-199">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="b9208-200">hello IIS 伺服器收到 hello SQL 回應，並完成 hello HTTP 回應，並將傳送 toohello 要求者</span><span class="sxs-lookup"><span data-stu-id="b9208-200">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
13. <span data-ttu-id="b9208-201">因為 hello Frontend 子網路上沒有任何輸出規則 hello 回應，而 hello 網際網路使用者會收到要求的 hello 網頁。</span><span class="sxs-lookup"><span data-stu-id="b9208-201">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="b9208-202">(*允許*) RDP toobackend</span><span class="sxs-lookup"><span data-stu-id="b9208-202">(*Allowed*) RDP toobackend</span></span>
1. <span data-ttu-id="b9208-203">網際網路上的伺服器系統管理員要求的 BackEnd001.CloudApp.Net:xxxxx 其中 xxxxx 是 RDP tooAppVM01 hello 隨機指派通訊埠編號上的 RDP 工作階段 tooAppVM01 （hello Azure 入口網站上或透過 PowerShell，可以找到 hello 指派連接埠）</span><span class="sxs-lookup"><span data-stu-id="b9208-203">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="b9208-204">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="b9208-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="b9208-205">NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-205">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="b9208-206">NSG 規則 2 (RDP) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="b9208-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="b9208-207">由於沒有輸出規則，會套用預設規則並允許傳回的流量</span><span class="sxs-lookup"><span data-stu-id="b9208-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="b9208-208">已啟用 RDP 工作階段</span><span class="sxs-lookup"><span data-stu-id="b9208-208">RDP session is enabled</span></span>
5. <span data-ttu-id="b9208-209">AppVM01 會提示您輸入 hello 使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="b9208-209">AppVM01 prompts for hello user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="b9208-210">(允許) DNS 伺服器上的 Web 伺服器 DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="b9208-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="b9208-211">Web 伺服器，IIS01，需要的資料摘要在 www.data.gov，但需要 tooresolve hello 位址。</span><span class="sxs-lookup"><span data-stu-id="b9208-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="b9208-212">hello 的網路組態 hello VNet 清單 DNS01 (10.0.2.4 hello 後端子網路上) 做為主要 DNS 伺服器 hello，IIS01 傳送 hello DNS 要求 tooDNS01</span><span class="sxs-lookup"><span data-stu-id="b9208-212">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="b9208-213">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="b9208-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="b9208-214">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="b9208-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="b9208-215">NSG 規則 1 (DNS) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="b9208-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="b9208-216">DNS 伺服器收到 hello 要求</span><span class="sxs-lookup"><span data-stu-id="b9208-216">DNS server receives hello request</span></span>
6. <span data-ttu-id="b9208-217">DNS 伺服器沒有快取的 hello 位址和要求的根 DNS 伺服器上 hello 網際網路</span><span class="sxs-lookup"><span data-stu-id="b9208-217">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="b9208-218">Backend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="b9208-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="b9208-219">網際網路 DNS 伺服器回應，因為此工作階段已在內部起始，hello 允許回應</span><span class="sxs-lookup"><span data-stu-id="b9208-219">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="b9208-220">DNS 伺服器快取 hello 回應及回應 toohello 初始要求後 tooIIS01</span><span class="sxs-lookup"><span data-stu-id="b9208-220">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="b9208-221">Backend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="b9208-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="b9208-222">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="b9208-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="b9208-223">套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-223">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="b9208-224">hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量</span><span class="sxs-lookup"><span data-stu-id="b9208-224">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="b9208-225">IIS01 DNS01 收到 hello 回應</span><span class="sxs-lookup"><span data-stu-id="b9208-225">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="b9208-226">(允許) Web 伺服器存取 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="b9208-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="b9208-227">IIS01 要求 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="b9208-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="b9208-228">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="b9208-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="b9208-229">hello 後端子網路會開始處理輸入的規則：</span><span class="sxs-lookup"><span data-stu-id="b9208-229">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="b9208-230">NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-230">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="b9208-231">NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-231">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="b9208-232">NSG 規則 3 (網際網路 tooIIS01) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-232">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="b9208-233">NSG 規則 4 (IIS01 tooAppVM01) 會套用，流量會允許中停止的規則處理</span><span class="sxs-lookup"><span data-stu-id="b9208-233">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="b9208-234">AppVM01 收到 hello 要求和回應檔案 （假設已獲授權存取）</span><span class="sxs-lookup"><span data-stu-id="b9208-234">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="b9208-235">由於 hello 後端子網路上有沒有輸出的規則，允許 hello 回應</span><span class="sxs-lookup"><span data-stu-id="b9208-235">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="b9208-236">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="b9208-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="b9208-237">套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="b9208-238">hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="b9208-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="b9208-239">hello IIS 伺服器收到 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="b9208-239">hello IIS server receives hello file</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="b9208-240">(*拒絕*) Web toobackend 伺服器</span><span class="sxs-lookup"><span data-stu-id="b9208-240">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="b9208-241">網際網路使用者嘗試 tooaccess AppVM01 上的檔案，即可透過 hello BackEnd001.CloudApp.Net 服務</span><span class="sxs-lookup"><span data-stu-id="b9208-241">An internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="b9208-242">因為不沒有開啟的檔案共用的任何端點，此流量不會傳送 hello 雲端服務，並不會連線到 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="b9208-242">Since there are no endpoints open for file share, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="b9208-243">如果基於某些原因，hello 端點處於開啟狀態，NSG 規則 5 (網際網路 tooVNet) 會封鎖此流量</span><span class="sxs-lookup"><span data-stu-id="b9208-243">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="b9208-244">(拒絕) DNS 伺服器上的 Web DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="b9208-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="b9208-245">網際網路使用者嘗試註冊的內部 DNS 記錄上 DNS01 hello BackEnd001.CloudApp.Net 服務透過 toolook</span><span class="sxs-lookup"><span data-stu-id="b9208-245">An internet user tries toolook up an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="b9208-246">因為沒有開啟以供 DNS 的端點，此流量不會傳送 hello 雲端服務，並不會連線到 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="b9208-246">Since there are no endpoints open for DNS, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="b9208-247">如果基於某些原因，hello 端點處於開啟狀態，NSG 規則 5 (網際網路 tooVNet) 會封鎖此流量 (注意： 不原因有兩個適用於該規則 1 」 (DNS)、 第一個 hello 來源位址是 hello 網際網路，此規則只適用於 toohello 也為 hello 本機 VNet 來源此規則是允許規則，讓它永遠不會拒絕的流量）</span><span class="sxs-lookup"><span data-stu-id="b9208-247">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="b9208-248">(*拒絕*) Web tooSQL 透過防火牆存取</span><span class="sxs-lookup"><span data-stu-id="b9208-248">(*Denied*) Web tooSQL access through firewall</span></span>
1. <span data-ttu-id="b9208-249">網際網路使用者從 FrontEnd001.CloudApp.Net (網際網路面向雲端服務) 要求 SQL 資料</span><span class="sxs-lookup"><span data-stu-id="b9208-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="b9208-250">因為沒有開啟以供 SQL 的端點，此流量不會傳送 hello 雲端服務，並不會到達 hello 防火牆</span><span class="sxs-lookup"><span data-stu-id="b9208-250">Since there are no endpoints open for SQL, this traffic would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="b9208-251">如果端點處於開啟狀態的因為某些原因，hello Frontend 子網路會開始處理輸入的規則：</span><span class="sxs-lookup"><span data-stu-id="b9208-251">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="b9208-252">NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-252">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="b9208-253">NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="b9208-253">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="b9208-254">NSG 規則 3 (網際網路 tooIIS01) 會套用，流量會允許中停止的規則處理</span><span class="sxs-lookup"><span data-stu-id="b9208-254">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="b9208-255">流量叫用內部 IP 位址的 hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="b9208-255">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="b9208-256">IIS01 未接聽通訊埠 1433，因此沒有回應 toohello 要求</span><span class="sxs-lookup"><span data-stu-id="b9208-256">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="b9208-257">結論</span><span class="sxs-lookup"><span data-stu-id="b9208-257">Conclusion</span></span>
<span data-ttu-id="b9208-258">這個範例是相當簡單且直接正向的方式，隔離 hello 後端的輸入流量子網路。</span><span class="sxs-lookup"><span data-stu-id="b9208-258">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="b9208-259">您可以在[這裡][HOME]找到更多範例和網路安全性界限的概觀。</span><span class="sxs-lookup"><span data-stu-id="b9208-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="b9208-260">參考</span><span class="sxs-lookup"><span data-stu-id="b9208-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="b9208-261">主要的指令碼和網路組態</span><span class="sxs-lookup"><span data-stu-id="b9208-261">Main script and network config</span></span>
<span data-ttu-id="b9208-262">在 PowerShell 指令碼檔案中儲存 hello 完整的指令碼。</span><span class="sxs-lookup"><span data-stu-id="b9208-262">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="b9208-263">Hello 儲存到檔案中的網路設定名為"NetworkConf1.xml。 」</span><span class="sxs-lookup"><span data-stu-id="b9208-263">Save hello Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="b9208-264">修改 hello 使用者定義的變數做為必要且執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b9208-264">Modify hello user-defined variables as needed and run hello script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="b9208-265">完整指令碼</span><span class="sxs-lookup"><span data-stu-id="b9208-265">Full script</span></span>
<span data-ttu-id="b9208-266">此指令碼，會根據 hello 使用者定義的變數。</span><span class="sxs-lookup"><span data-stu-id="b9208-266">This script will, based on hello user-defined variables;</span></span>

1. <span data-ttu-id="b9208-267">連接 tooan Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b9208-267">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="b9208-268">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b9208-268">Create a storage account</span></span>
3. <span data-ttu-id="b9208-269">建立 VNet 和 hello 網路組態檔中所定義的兩個子網路</span><span class="sxs-lookup"><span data-stu-id="b9208-269">Create a VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="b9208-270">建立四個 Windows Server VM</span><span class="sxs-lookup"><span data-stu-id="b9208-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="b9208-271">設定 NSG，包括：</span><span class="sxs-lookup"><span data-stu-id="b9208-271">Configure NSG including:</span></span>
   * <span data-ttu-id="b9208-272">建立 NSG</span><span class="sxs-lookup"><span data-stu-id="b9208-272">Creating an NSG</span></span>
   * <span data-ttu-id="b9208-273">在其中填入規則</span><span class="sxs-lookup"><span data-stu-id="b9208-273">Populating it with rules</span></span>
   * <span data-ttu-id="b9208-274">繫結 hello NSG toohello 適當的子網路</span><span class="sxs-lookup"><span data-stu-id="b9208-274">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="b9208-275">此 PowerShell 指令碼應該在連線到網際網路的電腦或伺服器上本機執行。</span><span class="sxs-lookup"><span data-stu-id="b9208-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9208-276">此指令碼在執行時，PowerShell 中可能會跳出警告或其他參考訊息。</span><span class="sxs-lookup"><span data-stu-id="b9208-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="b9208-277">只有紅色字體的錯誤訊息才需要擔心。</span><span class="sxs-lookup"><span data-stu-id="b9208-277">Only error messages in red are cause for concern.</span></span>
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

  BackEnd Service (BackEnd subnet 10.0.2.0/24)
   DNS01      - 10.0.2.4
   AppVM01    - 10.0.2.5
   AppVM02    - 10.0.2.6

#>

# Fixed Variables
    $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
    $VMName = @()
    $ServiceName = @()
    $VMFamily = @()
    $img = @()
    $size = @()
    $SubnetName = @()
    $VMIP = @()

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
        Return}
    Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
          New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

  # Update Subscription Pointer tooNew Storage Account
    Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="b9208-278">網路組態檔</span><span class="sxs-lookup"><span data-stu-id="b9208-278">Network config file</span></span>
<span data-ttu-id="b9208-279">與更新的位置儲存此 xml 檔並加入 hello 連結 toothis 檔案 toohello $NetworkConfigFile 變數 hello 上述指令碼中。</span><span class="sxs-lookup"><span data-stu-id="b9208-279">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello preceding script.</span></span>

```XML
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="DNS01" IPAddress="10.0.2.4" />
        <DnsServer name="Level3" IPAddress="209.244.0.3" />
      </DnsServers>
    </Dns>
    <VirtualNetworkSites>
      <VirtualNetworkSite name="CorpNetwork" Location="Central US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="FrontEnd">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="BackEnd">
            <AddressPrefix>10.0.2.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
        <DnsServersRef>
          <DnsServerRef name="DNS01" />
          <DnsServerRef name="Level3" />
        </DnsServersRef>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

#### <a name="sample-application-scripts"></a><span data-ttu-id="b9208-280">範例應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="b9208-280">Sample application scripts</span></span>
<span data-ttu-id="b9208-281">如果您想 tooinstall 範例應用程式，和其他周邊網路的範例，其中一個已提供在 hello 下列連結：[範例應用程式指令碼][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="b9208-281">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9208-282">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9208-282">Next steps</span></span>
* <span data-ttu-id="b9208-283">更新並儲存 XML 檔案</span><span class="sxs-lookup"><span data-stu-id="b9208-283">Update and save XML file</span></span>
* <span data-ttu-id="b9208-284">執行 hello PowerShell 指令碼 toobuild hello 環境</span><span class="sxs-lookup"><span data-stu-id="b9208-284">Run hello PowerShell script toobuild hello environment</span></span>
* <span data-ttu-id="b9208-285">安裝 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b9208-285">Install hello sample application</span></span>
* <span data-ttu-id="b9208-286">測試流經此 DMZ 的不同流量</span><span class="sxs-lookup"><span data-stu-id="b9208-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "具有 NSG 的輸入 DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

