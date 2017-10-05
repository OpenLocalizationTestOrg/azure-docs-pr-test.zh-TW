---
title: "Azure DMZ 範例 – 建置具有 NSG 的簡單 DMZ | Microsoft Docs"
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
ms.openlocfilehash: ed172d552e1e4c9ee27c58abcd7ad2d98df21579
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="84107-103">範例 1 – 使用 NSG 搭配傳統 PowerShell 建立簡單的 DMZ</span><span class="sxs-lookup"><span data-stu-id="84107-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="84107-104">[返回 [安全性界限最佳作法] 頁面][HOME]</span><span class="sxs-lookup"><span data-stu-id="84107-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="84107-105">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="84107-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="84107-106">傳統 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="84107-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="84107-107">此範例會建立包含四個 Windows 伺服器和網路安全性群組的基本 DMZ。</span><span class="sxs-lookup"><span data-stu-id="84107-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="84107-108">此範例說明每個相關 PowerShell 命令，以讓您更加深入地了解每個步驟。</span><span class="sxs-lookup"><span data-stu-id="84107-108">This example describes each of the relevant PowerShell commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="84107-109">另外您還會看到＜流量案例＞一節，本節提供深入的逐步說明，讓您知道流量是如何流經 DMZ 內的各個防禦層。</span><span class="sxs-lookup"><span data-stu-id="84107-109">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="84107-110">最後則有＜參考＞一節，本節提供完整的程式碼和指示，以供您建置此環境來測試和試驗各種案例。</span><span class="sxs-lookup"><span data-stu-id="84107-110">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="84107-111">![具有 NSG 的輸入 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="84107-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="84107-112">環境描述</span><span class="sxs-lookup"><span data-stu-id="84107-112">Environment description</span></span>
<span data-ttu-id="84107-113">此範例中，訂用帳戶包含下列資源：</span><span class="sxs-lookup"><span data-stu-id="84107-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="84107-114">兩個雲端服務：“FrontEnd001” 和 “BackEnd001”</span><span class="sxs-lookup"><span data-stu-id="84107-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="84107-115">一個虛擬網路 “CorpNetwork”，包含兩個子網路：“FrontEnd” 和 “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="84107-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="84107-116">套用至這兩個子網路的單一網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="84107-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="84107-117">一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)</span><span class="sxs-lookup"><span data-stu-id="84107-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="84107-118">兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="84107-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="84107-119">一個代表 DNS 伺服器的 Windows Server ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="84107-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="84107-120">在＜參考＞一節中有提供 PowerShell 指令碼，其可建置本範例中的大部分環境。</span><span class="sxs-lookup"><span data-stu-id="84107-120">In the references section, there is a PowerShell script that builds most of the environment described in this example.</span></span> <span data-ttu-id="84107-121">至於 VM 和虛擬網路的建置，雖然也是由此範例指令碼來完成，但本文不會詳加敘述。</span><span class="sxs-lookup"><span data-stu-id="84107-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="84107-122">建置環境：</span><span class="sxs-lookup"><span data-stu-id="84107-122">To build the environment;</span></span>

1. <span data-ttu-id="84107-123">儲存＜參考＞一節中所包含的網路組態 xml 檔 (更新名稱、位置和 IP 位址以符合給定的案例)</span><span class="sxs-lookup"><span data-stu-id="84107-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="84107-124">更新指令碼中的使用者變數，以符合要用來執行指令碼的環境 (訂用帳戶、服務名稱等)</span><span class="sxs-lookup"><span data-stu-id="84107-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="84107-125">在 PowerShell 中執行指令碼</span><span class="sxs-lookup"><span data-stu-id="84107-125">Execute the script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="84107-126">PowerShell 指令碼中所指的區域必須符合網路組態 xml 檔中所指的區域。</span><span class="sxs-lookup"><span data-stu-id="84107-126">The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>
>
>

<span data-ttu-id="84107-127">指令碼順利執行後，即可採取其他選擇性步驟，＜參考＞一節中有兩個指令碼，其會設定 Web 伺服器和具有簡單 Web 應用程式的應用程式伺服器，以便能使用此 DMZ 組態進行測試。</span><span class="sxs-lookup"><span data-stu-id="84107-127">Once the script runs successfully additional optional steps may be taken, in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="84107-128">下列各節藉由逐步解說 PowerShell 指令碼的重要程式行，詳細說明此範例的網路安全性群組和其運作方式。</span><span class="sxs-lookup"><span data-stu-id="84107-128">The following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of the PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="84107-129">網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="84107-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="84107-130">此範例會組建 NSG 群組，然後載入六個規則。</span><span class="sxs-lookup"><span data-stu-id="84107-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="84107-131">一般而言，您應該先建立特定的「允許」規則，最後再建立較一般的「拒絕」規則。</span><span class="sxs-lookup"><span data-stu-id="84107-131">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="84107-132">所指定的優先順序會決定要先評估哪些規則。</span><span class="sxs-lookup"><span data-stu-id="84107-132">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="84107-133">一旦發現流量適用特定規則，就不會再評估後續規則。</span><span class="sxs-lookup"><span data-stu-id="84107-133">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="84107-134">NSG 規則可以套用在輸入或輸出方向 (從子網路的觀點出發)。</span><span class="sxs-lookup"><span data-stu-id="84107-134">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
> 
> 

<span data-ttu-id="84107-135">指令碼會以宣告方式為輸入流量建置下列規則：</span><span class="sxs-lookup"><span data-stu-id="84107-135">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="84107-136">允許內部 DNS 流量 (連接埠 53)</span><span class="sxs-lookup"><span data-stu-id="84107-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="84107-137">允許從網際網路到任何 VM 的 RDP 流量 (連接埠 3389)</span><span class="sxs-lookup"><span data-stu-id="84107-137">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="84107-138">允許從網際網路到 Web 伺服器 (IIS01) 的 HTTP 流量 (連接埠 80)</span><span class="sxs-lookup"><span data-stu-id="84107-138">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="84107-139">允許從 IIS01 到 AppVM1 的任何流量 (所有連接埠)</span><span class="sxs-lookup"><span data-stu-id="84107-139">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="84107-140">拒絕從網際網路到整個 VNet (兩個子網路) 的任何流量 (所有連接埠)</span><span class="sxs-lookup"><span data-stu-id="84107-140">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="84107-141">拒絕從 Frontend 子網路到 Backend 子網路的任何流量 (所有連接埠)</span><span class="sxs-lookup"><span data-stu-id="84107-141">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="84107-142">這些規則繫結至每個子網路後，如果有從網際網路到 Web 伺服器的輸入 HTTP 要求，規則 3 (允許) 和規則 5 (拒絕) 皆適用，但由於規則 3 具有較高的優先順序，所以只會適用規則 3，規則 5 則不會派上用場。</span><span class="sxs-lookup"><span data-stu-id="84107-142">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="84107-143">因此會允許 HTTP 要求送往 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="84107-143">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="84107-144">如果相同的流量嘗試抵達 DNS01 伺服器，規則 5 (拒絕) 會先適用，因此不會允許流量傳遞給伺服器。</span><span class="sxs-lookup"><span data-stu-id="84107-144">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="84107-145">規則 6 (拒絕) 會阻止 Frontend 子網路與 Backend 子網路交談 (規則 1 和 4 允許的流量除外)，此規則集可在攻擊者入侵 Frontend 上的 Web 應用程式時保護 Backend 網路，攻擊者只能對 Backend 的「受保護」網路進行有限度的存取 (只能存取 AppVM01 伺服器上公開的資源)。</span><span class="sxs-lookup"><span data-stu-id="84107-145">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="84107-146">有一個預設輸出規則可允許流量外流到網際網路。</span><span class="sxs-lookup"><span data-stu-id="84107-146">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="84107-147">在此範例中，我們會允許輸出流量，並不會修改任何輸出規則。</span><span class="sxs-lookup"><span data-stu-id="84107-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="84107-148">如果兩個方向的流量都要鎖定，則需要使用者定義的路由，會在[安全性界限最佳作法頁面][HOME]上的＜範例 3＞中探討。</span><span class="sxs-lookup"><span data-stu-id="84107-148">To lock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="84107-149">以下會更為詳細地討論每個規則 (**注意**：下列清單中以貨幣符號開頭的項目 (例如：$NSGName) 皆為來自本文＜參考＞一節之指令碼的使用者定義變數)：</span><span class="sxs-lookup"><span data-stu-id="84107-149">Each rule is discussed in more detail as follows (**Note**: any item in the following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from the script in the reference section of this document):</span></span>

1. <span data-ttu-id="84107-150">首先必須建置網路安全性群組來保存規則：</span><span class="sxs-lookup"><span data-stu-id="84107-150">First a Network Security Group must be built to hold the rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="84107-151">此範例中的第一個規則會允許所有內部網路之間的 DNS 流量流往 Backend 子網路上的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="84107-151">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="84107-152">此規則有一些重要參數：</span><span class="sxs-lookup"><span data-stu-id="84107-152">The rule has some important parameters:</span></span>
   
   * <span data-ttu-id="84107-153">「類型」表示此規則會生效的傳輸流量方向。</span><span class="sxs-lookup"><span data-stu-id="84107-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="84107-154">方向是來自子網路或虛擬機器的角度 (取決於此 NSG 繫結的位置)。</span><span class="sxs-lookup"><span data-stu-id="84107-154">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="84107-155">因此，如果 Type 是 “Inbound” 且流量進入子網路，此規則將會適用，而離開子網路的流量則不受此規則所影響。</span><span class="sxs-lookup"><span data-stu-id="84107-155">Thus if Type is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="84107-156">"Priority" 會設定流量的評估順序。</span><span class="sxs-lookup"><span data-stu-id="84107-156">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="84107-157">編號愈低，優先順序就愈高。</span><span class="sxs-lookup"><span data-stu-id="84107-157">The lower the number the higher the priority.</span></span> <span data-ttu-id="84107-158">當規則套用至特定流量時，就不會再處理其他規則。</span><span class="sxs-lookup"><span data-stu-id="84107-158">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="84107-159">因此，如果優先順序為 1 的規則允許流量，優先順序為 2 的規則拒絕流量，而這兩個規則皆適用於流量，則會允許流量流動 (規則 1 有更高的優先順序，所以會生效，並且不會再套用其他規則)。</span><span class="sxs-lookup"><span data-stu-id="84107-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="84107-160">“Action” 指出受此規則影響的流量是要封鎖或允許。</span><span class="sxs-lookup"><span data-stu-id="84107-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="84107-161">此規則會允許 RDP 流量從網際網路流往繫結子網路上任何伺服器的 RDP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="84107-161">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> <span data-ttu-id="84107-162">此規則使用兩種特殊位址前置詞：“VIRTUAL_NETWORK” 和 “INTERNET”。</span><span class="sxs-lookup"><span data-stu-id="84107-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="84107-163">這些標記可輕易處理較大類別的位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="84107-163">These tags are an easy way to address a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="84107-164">此規則允許輸入網際網路流量抵達 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="84107-164">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="84107-165">此規則不會變更路由的行為。</span><span class="sxs-lookup"><span data-stu-id="84107-165">This rule does not change the routing behavior.</span></span> <span data-ttu-id="84107-166">這個規則只會允許指向 IIS01 的流量通過。</span><span class="sxs-lookup"><span data-stu-id="84107-166">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="84107-167">因此，如果來自網際網路的流量將 Web 伺服器做為其目的地，此規則會允許流量，並停止再處理其他規則。</span><span class="sxs-lookup"><span data-stu-id="84107-167">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="84107-168">(在優先順序為 140 的規則中，其他所有輸入網際網路流量皆會遭到封鎖)。</span><span class="sxs-lookup"><span data-stu-id="84107-168">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="84107-169">如果您只要處理 HTTP 流量，則可將此規則進一步限制為只允許目的地連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="84107-169">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet to $VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="84107-170">此規則允許流量從 IIS01 伺服器傳遞到 AppVM01 伺服器，較後面的規則會封鎖其他所有 Frontend 到 Backend 的流量。</span><span class="sxs-lookup"><span data-stu-id="84107-170">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="84107-171">如果已知連接埠應該加入，可改善此規則。</span><span class="sxs-lookup"><span data-stu-id="84107-171">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="84107-172">例如，如果 IIS 伺服器只會抵達 AppVM01 上的 SQL Server，且 Web 應用程式曾遭到入侵，則目的地連接埠範圍應該從 “*” (任何) 變更為 1433 (SQL 連接埠)，以縮小 AppVM01 上的輸入攻擊面。</span><span class="sxs-lookup"><span data-stu-id="84107-172">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] to $VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="84107-173">此規則會拒絕從網際網路到網路上任何伺服器的流量。</span><span class="sxs-lookup"><span data-stu-id="84107-173">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="84107-174">利用優先順序為 110 和 120 的規則，效果將可只允許輸入網際網路流量流往防火牆以及伺服器上的 RDP 連接埠，除此之外的其他流量則予以封鎖。</span><span class="sxs-lookup"><span data-stu-id="84107-174">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="84107-175">此規則是「保險」規則，可封鎖所有未預期的流程。</span><span class="sxs-lookup"><span data-stu-id="84107-175">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $VNetName VNet from the Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="84107-176">最後一個規則會拒絕從 Frontend 子網路到 Backend 子網路的流量。</span><span class="sxs-lookup"><span data-stu-id="84107-176">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="84107-177">此規則是僅限輸入的規則，所以允許反向流量 (從 Backend 到 Frontend)。</span><span class="sxs-lookup"><span data-stu-id="84107-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="84107-178">流量案例</span><span class="sxs-lookup"><span data-stu-id="84107-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="84107-179">(允許) 網際網路到 Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="84107-179">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="84107-180">網際網路使用者從 FrontEnd001.CloudApp.Net (網際網路面向雲端服務) 要求 HTTP 頁面</span><span class="sxs-lookup"><span data-stu-id="84107-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="84107-181">雲端服務透過連接埠 80 上的開放端點將流量傳遞至 IIS01 (Web 伺服器)</span><span class="sxs-lookup"><span data-stu-id="84107-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="84107-182">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="84107-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="84107-183">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="84107-183">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="84107-184">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="84107-184">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="84107-185">NSG 規則 3 (網際網路到 IIS01) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="84107-185">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="84107-186">流量抵達 Web 伺服器 IIS01 的內部 IP 位址 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="84107-186">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="84107-187">IIS01 正在接聽 Web 流量，接收此要求並開始處理要求</span><span class="sxs-lookup"><span data-stu-id="84107-187">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="84107-188">IIS01 向 AppVM01 上的 SQL Server 要求資訊</span><span class="sxs-lookup"><span data-stu-id="84107-188">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="84107-189">Frontend 子網路上沒有輸出規則，所以允許流量</span><span class="sxs-lookup"><span data-stu-id="84107-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="84107-190">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="84107-190">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="84107-191">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="84107-191">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="84107-192">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="84107-192">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="84107-193">NSG 規則 3 (網際網路到防火牆) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="84107-193">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="84107-194">NSG 規則 4 (IIS01 到 AppVM01) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="84107-194">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="84107-195">AppVM01 接收 SQL 查詢並回應</span><span class="sxs-lookup"><span data-stu-id="84107-195">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="84107-196">Backend 子網路上沒有輸出規則，所以允許回應</span><span class="sxs-lookup"><span data-stu-id="84107-196">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="84107-197">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="84107-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="84107-198">Backend 子網路到 Frontend 子網路的輸入流量沒有適用的 NSG 規則，因此不會套用任何 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="84107-198">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="84107-199">允許子網路間流量的預設系統規則會允許此流量，因此允許流量。</span><span class="sxs-lookup"><span data-stu-id="84107-199">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="84107-200">IIS 伺服器接收 SQL 回應、完成 HTTP 回應並傳送給要求者</span><span class="sxs-lookup"><span data-stu-id="84107-200">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span></span>
13. <span data-ttu-id="84107-201">Frontend 子網路上沒有輸出規則，所以允許回應，網際網路使用者會收到要求的網頁。</span><span class="sxs-lookup"><span data-stu-id="84107-201">Since there are no outbound rules on the Frontend subnet the response is allowed, and the internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-backend"></a><span data-ttu-id="84107-202">(允許) RDP 到 Backend</span><span class="sxs-lookup"><span data-stu-id="84107-202">(*Allowed*) RDP to backend</span></span>
1. <span data-ttu-id="84107-203">網際網路上的伺服器管理員在 BackEnd001.CloudApp.Net:xxxxx 上要求 AppVM01 的 RDP 工作階段，其中 xxxxx 是 RDP 到 AppVM01 的隨機指派連接埠號碼 (在 Azure 入口網站上或透過 PowerShell，即可找到指派的連接埠)</span><span class="sxs-lookup"><span data-stu-id="84107-203">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="84107-204">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="84107-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="84107-205">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="84107-205">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="84107-206">NSG 規則 2 (RDP) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="84107-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="84107-207">由於沒有輸出規則，會套用預設規則並允許傳回的流量</span><span class="sxs-lookup"><span data-stu-id="84107-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="84107-208">已啟用 RDP 工作階段</span><span class="sxs-lookup"><span data-stu-id="84107-208">RDP session is enabled</span></span>
5. <span data-ttu-id="84107-209">AppVM01 會提示輸入使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="84107-209">AppVM01 prompts for the user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="84107-210">(允許) DNS 伺服器上的 Web 伺服器 DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="84107-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="84107-211">Web 伺服器 IIS01 需要 www.data.gov 的資料摘要，但需要解析位址。</span><span class="sxs-lookup"><span data-stu-id="84107-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="84107-212">VNet 的網路組態將 DNS01 (Backend 子網路上的 10.0.2.4) 列為主要 DNS 伺服器，IIS01 將 DNS 要求傳送至 DNS01</span><span class="sxs-lookup"><span data-stu-id="84107-212">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="84107-213">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="84107-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="84107-214">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="84107-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="84107-215">NSG 規則 1 (DNS) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="84107-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="84107-216">DNS 伺服器收到要求</span><span class="sxs-lookup"><span data-stu-id="84107-216">DNS server receives the request</span></span>
6. <span data-ttu-id="84107-217">DNS 伺服器沒有快取的位址，並要求網際網路上的根 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="84107-217">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="84107-218">Backend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="84107-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="84107-219">網際網路 DNS 伺服器回應，因為此工作階段是從內部起始，所以允許回應</span><span class="sxs-lookup"><span data-stu-id="84107-219">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="84107-220">DNS 伺服器快取回應，然後將初始要求回應到 IIS01</span><span class="sxs-lookup"><span data-stu-id="84107-220">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="84107-221">Backend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="84107-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="84107-222">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="84107-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="84107-223">Backend 子網路到 Frontend 子網路的輸入流量沒有適用的 NSG 規則，因此不會套用任何 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="84107-223">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="84107-224">允許子網路間流量的預設系統規則會允許此流量，因此允許流量</span><span class="sxs-lookup"><span data-stu-id="84107-224">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="84107-225">IIS01 從 DNS01 接收回應</span><span class="sxs-lookup"><span data-stu-id="84107-225">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="84107-226">(允許) Web 伺服器存取 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="84107-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="84107-227">IIS01 要求 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="84107-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="84107-228">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="84107-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="84107-229">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="84107-229">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="84107-230">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="84107-230">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="84107-231">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="84107-231">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="84107-232">NSG 規則 3 (網際網路到 IIS01) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="84107-232">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="84107-233">NSG 規則 4 (IIS01 到 AppVM01) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="84107-233">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="84107-234">AppVM01 接收要求並以檔案回應 (假設已獲得存取授權)</span><span class="sxs-lookup"><span data-stu-id="84107-234">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="84107-235">Backend 子網路上沒有輸出規則，所以允許回應</span><span class="sxs-lookup"><span data-stu-id="84107-235">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="84107-236">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="84107-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="84107-237">Backend 子網路到 Frontend 子網路的輸入流量沒有適用的 NSG 規則，因此不會套用任何 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="84107-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
   2. <span data-ttu-id="84107-238">允許子網路間流量的預設系統規則會允許此流量，因此允許流量。</span><span class="sxs-lookup"><span data-stu-id="84107-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="84107-239">IIS 伺服器接收檔案</span><span class="sxs-lookup"><span data-stu-id="84107-239">The IIS server receives the file</span></span>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="84107-240">(拒絕) Web 到 Backend 伺服器</span><span class="sxs-lookup"><span data-stu-id="84107-240">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="84107-241">網際網路使用者嘗試透過 BackEnd001.CloudApp.Net 服務存取 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="84107-241">An internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="84107-242">因為沒有用於檔案共用的開放端點，此流量不會通過雲端服務到達伺服器</span><span class="sxs-lookup"><span data-stu-id="84107-242">Since there are no endpoints open for file share, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="84107-243">如果基於某些原因而開放端點，NSG 規則 5 (網際網路到 VNet) 會封鎖此流量</span><span class="sxs-lookup"><span data-stu-id="84107-243">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="84107-244">(拒絕) DNS 伺服器上的 Web DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="84107-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="84107-245">網際網路使用者嘗試透過 BackEnd001.CloudApp.Net 服務查閱 DNS01 上的內部 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="84107-245">An internet user tries to look up an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="84107-246">因為沒有用於 DNS 的開放端點，此流量不會通過雲端服務到達伺服器</span><span class="sxs-lookup"><span data-stu-id="84107-246">Since there are no endpoints open for DNS, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="84107-247">如果基於某些原因而開放端點，NSG 規則 5 (網際網路到 VNet) 會封鎖此流量 (注意：有兩個原因導致規則 1 (DNS) 不適用，首先，來源位址是網際網路，此規則只適用於以本機 VNet 做為來源，再者，此規則是允許規則，所以它永遠不會拒絕流量)</span><span class="sxs-lookup"><span data-stu-id="84107-247">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-to-sql-access-through-firewall"></a><span data-ttu-id="84107-248">(拒絕) Web 透過防火牆對 SQL 進行存取</span><span class="sxs-lookup"><span data-stu-id="84107-248">(*Denied*) Web to SQL access through firewall</span></span>
1. <span data-ttu-id="84107-249">網際網路使用者從 FrontEnd001.CloudApp.Net (網際網路面向雲端服務) 要求 SQL 資料</span><span class="sxs-lookup"><span data-stu-id="84107-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="84107-250">因為沒有用於 SQL 的開放端點，此流量不會通過雲端服務到達防火牆</span><span class="sxs-lookup"><span data-stu-id="84107-250">Since there are no endpoints open for SQL, this traffic would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="84107-251">如果基於某些原因而開放端點，Frontend 子網路會開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="84107-251">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="84107-252">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="84107-252">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="84107-253">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="84107-253">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="84107-254">NSG 規則 3 (網際網路到 IIS01) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="84107-254">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="84107-255">流量抵達 IIS01 的內部 IP 位址 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="84107-255">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="84107-256">IIS01 未接聽連接埠 1433，所以要求沒有回應</span><span class="sxs-lookup"><span data-stu-id="84107-256">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="84107-257">結論</span><span class="sxs-lookup"><span data-stu-id="84107-257">Conclusion</span></span>
<span data-ttu-id="84107-258">這個範例隔離後端子網路與輸入流量的方式相當直接簡單。</span><span class="sxs-lookup"><span data-stu-id="84107-258">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="84107-259">您可以在[這裡][HOME]找到更多範例和網路安全性界限的概觀。</span><span class="sxs-lookup"><span data-stu-id="84107-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="84107-260">參考</span><span class="sxs-lookup"><span data-stu-id="84107-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="84107-261">主要的指令碼和網路組態</span><span class="sxs-lookup"><span data-stu-id="84107-261">Main script and network config</span></span>
<span data-ttu-id="84107-262">將完整指令碼儲存在 PowerShell 指令碼檔案中。</span><span class="sxs-lookup"><span data-stu-id="84107-262">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="84107-263">將網路組態儲存到名為 “NetworkConf1.xml” 的檔案。</span><span class="sxs-lookup"><span data-stu-id="84107-263">Save the Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="84107-264">視需要修改使用者定義的變數並執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="84107-264">Modify the user-defined variables as needed and run the script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="84107-265">完整指令碼</span><span class="sxs-lookup"><span data-stu-id="84107-265">Full script</span></span>
<span data-ttu-id="84107-266">根據使用者定義的變數，此指令碼會執行下列動作；</span><span class="sxs-lookup"><span data-stu-id="84107-266">This script will, based on the user-defined variables;</span></span>

1. <span data-ttu-id="84107-267">連線到 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="84107-267">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="84107-268">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="84107-268">Create a storage account</span></span>
3. <span data-ttu-id="84107-269">依網路組態檔中的定義建立 VNet 和兩個子網路</span><span class="sxs-lookup"><span data-stu-id="84107-269">Create a VNet and two subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="84107-270">建立四個 Windows Server VM</span><span class="sxs-lookup"><span data-stu-id="84107-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="84107-271">設定 NSG，包括：</span><span class="sxs-lookup"><span data-stu-id="84107-271">Configure NSG including:</span></span>
   * <span data-ttu-id="84107-272">建立 NSG</span><span class="sxs-lookup"><span data-stu-id="84107-272">Creating an NSG</span></span>
   * <span data-ttu-id="84107-273">在其中填入規則</span><span class="sxs-lookup"><span data-stu-id="84107-273">Populating it with rules</span></span>
   * <span data-ttu-id="84107-274">將 NSG 繫結至適當的子網路</span><span class="sxs-lookup"><span data-stu-id="84107-274">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="84107-275">此 PowerShell 指令碼應該在連線到網際網路的電腦或伺服器上本機執行。</span><span class="sxs-lookup"><span data-stu-id="84107-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84107-276">此指令碼在執行時，PowerShell 中可能會跳出警告或其他參考訊息。</span><span class="sxs-lookup"><span data-stu-id="84107-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="84107-277">只有紅色字體的錯誤訊息才需要擔心。</span><span class="sxs-lookup"><span data-stu-id="84107-277">Only error messages in red are cause for concern.</span></span>
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
   - One server on the FrontEnd Subnet
   - Three Servers on the BackEnd Subnet
   - Network Security Groups to allow/deny traffic patterns as declared

  Before running script, ensure the network configuration file is created in
  the directory referenced by $NetworkConfigFile variable (or update the
  variable to reflect the path and file name of the config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  the appropriate layer(s) of protection. This script serves as an example of some
  of the techniques that can be used, but should not be used for all scenarios. You
  are responsible to assess your security needs and the appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

  BackEnd Service (BackEnd subnet 10.0.2.0/24)
   DNS01      - 10.0.2.4
   AppVM01    - 10.0.2.5
   AppVM02    - 10.0.2.6

#>

# Fixed Variables
    $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password to be used for all VMs"
    $VMName = @()
    $ServiceName = @()
    $VMFamily = @()
    $img = @()
    $size = @()
    $SubnetName = @()
    $VMIP = @()

# User-Defined Global Variables
  # These should be changes to reflect your subscription and services
  # Invalid options will fail in the validation section

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
    # Note: To ensure proper NSG Rule creation later in this script:
    #       - The Web Server must be VM 0
    #       - The AppVM1 Server must be VM 1
    #       - The DNS server must be VM 3
    #
    #       Otherwise the NSG rules in the last section of this
    #       script will need to be changed to match the modified
    #       VM array numbers ($i) so the NSG Rule IP addresses
    #       are aligned to the associated VM IP addresses.

    # VM 0 - The Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - The First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - The Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - The DNS Server
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

  # Update Subscription Pointer to New Storage Account
    Write-Host "Updating Subscription Pointer to New Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation variable is correct and the network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see the above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

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
    Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

  # Build the NSG
    Write-Host "Building the NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) to $($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign the NSG to the Subnets
        Write-Host "Binding the NSG to both subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on the IIS Server)
  # Install Backend resource (Run Post-Build Script on the AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="84107-278">網路組態檔</span><span class="sxs-lookup"><span data-stu-id="84107-278">Network config file</span></span>
<span data-ttu-id="84107-279">以更新的位置儲存此 xml 檔案，並將此檔案的連結新增到先前指令碼中的 $NetworkConfigFile 變數。</span><span class="sxs-lookup"><span data-stu-id="84107-279">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the preceding script.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="84107-280">範例應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="84107-280">Sample application scripts</span></span>
<span data-ttu-id="84107-281">如果您想要為此範例和其他 DMZ 範例安裝範例應用程式，下列連結中有提供一個：[範例應用程式指令碼][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="84107-281">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="84107-282">後續步驟</span><span class="sxs-lookup"><span data-stu-id="84107-282">Next steps</span></span>
* <span data-ttu-id="84107-283">更新並儲存 XML 檔案</span><span class="sxs-lookup"><span data-stu-id="84107-283">Update and save XML file</span></span>
* <span data-ttu-id="84107-284">執行 PowerShell 指令碼來建置環境</span><span class="sxs-lookup"><span data-stu-id="84107-284">Run the PowerShell script to build the environment</span></span>
* <span data-ttu-id="84107-285">安裝範例應用程式</span><span class="sxs-lookup"><span data-stu-id="84107-285">Install the sample application</span></span>
* <span data-ttu-id="84107-286">測試流經此 DMZ 的不同流量</span><span class="sxs-lookup"><span data-stu-id="84107-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
<span data-ttu-id="84107-287">[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "具有 NSG 的輸入 DMZ"</span><span class="sxs-lookup"><span data-stu-id="84107-287">[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Inbound DMZ with NSG"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

