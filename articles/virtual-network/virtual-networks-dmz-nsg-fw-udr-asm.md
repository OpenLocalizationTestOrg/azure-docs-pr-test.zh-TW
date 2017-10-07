---
title: "範例-aaaDMZ 建置 DMZ tooProtect 網路使用防火牆、 UDR，以及 NSG |Microsoft 文件"
description: "建置具有防火牆、使用者定義的路由 (UDR) 和網路安全性群組 (NSG) 的 DMZ"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="7c7a2-103">範例 3 – 建置 DMZ tooProtect 網路使用防火牆、 UDR，以及 NSG</span><span class="sxs-lookup"><span data-stu-id="7c7a2-103">Example 3 – Build a DMZ tooProtect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="7c7a2-104">[傳回 toohello 安全性界限最佳作法頁面][HOME]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="7c7a2-105">此範例會建立 DMZ，其內含防火牆、四個 Windows 伺服器、使用者定義的路由、IP 轉送和網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="7c7a2-106">它也將會逐步每 hello 相關命令 tooprovide 更深入的了解每個步驟。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="7c7a2-107">另外還有流量案例 > 一節 tooprovide 的深入了解逐步如何流量就會繼續進行 hello 層級的防禦 hello 周邊網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="7c7a2-108">最後，在 hello references 區段中是 hello 完整程式碼和指示 toobuild 此環境 tootest 和試驗各種案例。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="7c7a2-109">![具有 NVA、NSG 和 UDR 的雙向 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="7c7a2-110">環境設定</span><span class="sxs-lookup"><span data-stu-id="7c7a2-110">Environment Setup</span></span>
<span data-ttu-id="7c7a2-111">在此範例中沒有包含 hello 下列訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="7c7a2-112">三個雲端服務：“SecSvc001”、“FrontEnd001” 和 “BackEnd001”</span><span class="sxs-lookup"><span data-stu-id="7c7a2-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="7c7a2-113">一個虛擬網路 "CorpNetwork"，包含三個子網路：“SecNet”、“FrontEnd” 和 “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="7c7a2-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="7c7a2-114">網路的虛擬設備，在此範例中，防火牆連接 toohello SecNet 子網路</span><span class="sxs-lookup"><span data-stu-id="7c7a2-114">A network virtual appliance, in this example a firewall, connected toohello SecNet subnet</span></span>
* <span data-ttu-id="7c7a2-115">一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="7c7a2-116">兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="7c7a2-117">一個代表 DNS 伺服器的 Windows Server ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="7c7a2-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="7c7a2-118">在下面 hello references 區段中沒有將建置大部分 hello 環境上面所述的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-118">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="7c7a2-119">建置 hello Vm 和虛擬網路，由 hello 範例指令碼，雖然不詳述於本文件說明。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-119">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="7c7a2-120">toobuild hello 環境：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-120">toobuild hello environment:</span></span>

1. <span data-ttu-id="7c7a2-121">儲存 hello 網路組態 xml 檔案包含在 hello 參考一節 （名稱、 位置和 IP 位址 toomatch hello 指定案例與更新）</span><span class="sxs-lookup"><span data-stu-id="7c7a2-121">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="7c7a2-122">Hello 指令碼 toomatch hello 環境 hello 指令碼中的更新 hello 使用者變數是 toobe 執行 （訂用帳戶、 服務名稱等等）</span><span class="sxs-lookup"><span data-stu-id="7c7a2-122">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="7c7a2-123">在 PowerShell 中執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="7c7a2-123">Execute hello script in PowerShell</span></span>

<span data-ttu-id="7c7a2-124">**請注意**： 表示 hello PowerShell 指令碼中的 hello 區域必須符合表示 hello 網路組態 xml 檔中的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-124">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="7c7a2-125">Hello 指令碼順利執行之後可能會進入 hello 後指令碼的步驟：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-125">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="7c7a2-126">設定 hello 防火牆規則，這會涵蓋 hello 下面的一節中： 防火牆規則的描述。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-126">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="7c7a2-127">（選擇性） 在 hello references 區段中是兩個指令碼 tooset hello web 伺服器和應用程式伺服器，以測試此 DMZ 設定簡單的 web 應用程式 tooallow。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-127">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="7c7a2-128">一旦 hello 指令碼順利執行 hello 防火牆規則需要 toobe 完成，這在 hello 一節中說明： 防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-128">Once hello script runs successfully hello firewall rules will need toobe completed, this is covered in hello section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="7c7a2-129">使用者定義的路由 (UDR)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="7c7a2-130">根據預設，下列系統路由 hello 的定義如下：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-130">By default, hello following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="7c7a2-131">hello VNETLocal 一律為 hello 定義位址首碼的 hello VNet 的該特定的網路 （亦即它將變更從 VNet tooVNet 根據每個特定的 VNet 的定義方式）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-131">hello VNETLocal is always hello defined address prefix(es) of hello VNet for that specific network (ie it will change from VNet tooVNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="7c7a2-132">hello 路由是靜態的而且預設上述剩餘的系統。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-132">hello remaining system routes are static and default as above.</span></span>

<span data-ttu-id="7c7a2-133">與優先順序，路由透過 hello 最長的前置詞比對 (LPM) 方法來處理，因此 hello hello 資料表中最明確的路由會套用 tooa 目的地位址。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-133">As for priority, routes are processed via hello Longest Prefix Match (LPM) method, thus hello most specific route in hello table would apply tooa given destination address.</span></span>

<span data-ttu-id="7c7a2-134">因此，流量 （例如 toohello DNS01 伺服器，10.0.2.4） 給 hello 區域網路 (10.0.0.0/16) 就會路由傳送跨 toohello 10.0.0.0/16 路由到期的 hello VNet tooits 目的地。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-134">Therefore, traffic (for example toohello DNS01 server, 10.0.2.4) intended for hello local network (10.0.0.0/16) would be routed across hello VNet tooits destination due toohello 10.0.0.0/16 route.</span></span> <span data-ttu-id="7c7a2-135">換句話說，如 10.0.2.4，hello 10.0.0.0/16 路由 hello 最明確的路由，即使是 hello 10.0.0.0/8/8 以及 0.0.0.0/0 也會無法套用，但是因為它是以較不特定他們不會影響此流量。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-135">In other words, for 10.0.2.4, hello 10.0.0.0/16 route is hello most specific route, even though hello 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="7c7a2-136">因此 hello 流量 too10.0.2.4 會擁有下一個躍點的 hello 區域 VNet 和直接路由傳送 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-136">Thus hello traffic too10.0.2.4 would have a next hop of hello local VNet and simply route toohello destination.</span></span>

<span data-ttu-id="7c7a2-137">如果流量設計的目的 10.1.1.1 比方說，hello 10.0.0.0/16 路由不會套用，但 hello 10.0.0.0/8 hello 最適合的而此 hello 流量會卸除 （「 黑色書背 」），因為 hello 下一個躍點為 Null。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-137">If traffic was intended for 10.1.1.1 for example, hello 10.0.0.0/16 route wouldn’t apply, but hello 10.0.0.0/8 would be hello most specific, and this hello traffic would be dropped (“black holed”) since hello next hop is Null.</span></span> 

<span data-ttu-id="7c7a2-138">如果 hello 目的地未套用 tooany hello Null 前置詞或 hello VNETLocal 前置詞，則它會遵循 hello 最不特定路由，0.0.0.0/0，並傳送出 toohello 網際網路的 hello 下一個躍點，因此 Azure 的網際網路邊緣外。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-138">If hello destination didn’t apply tooany of hello Null prefixes or hello VNETLocal prefixes, then it would follow hello least specific route, 0.0.0.0/0 and be routed out toohello Internet as hello next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="7c7a2-139">如果在 hello 路由表中有兩個相同的前置詞，hello 如下 hello hello 路由 「 來源 」 屬性為基礎的喜好設定順序：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-139">If there are two identical prefixes in hello route table, hello following is hello order of preference based on hello routes “source” attribute:</span></span>

1. <span data-ttu-id="7c7a2-140">「 VirtualAppliance"= 使用者定義的路由手動新增的 toohello 資料表</span><span class="sxs-lookup"><span data-stu-id="7c7a2-140">"VirtualAppliance" = A User Defined Route manually added toohello table</span></span>
2. <span data-ttu-id="7c7a2-141">"VPNGateway"= 動態路由 (BGP 混合式網路搭配使用時)，加入動態網路通訊協定，這些路由會隨著時間變更為 hello 動態的通訊協定會自動反映變更，所以網路中</span><span class="sxs-lookup"><span data-stu-id="7c7a2-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as hello dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="7c7a2-142">"Default"= hello 系統路由 hello 區域 VNet 和 hello 靜態項目上的 hello 路由表中所示。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-142">“Default” = hello System Routes, hello local VNet and hello static entries as shown in hello route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="7c7a2-143">您現在可以使用 ExpressRoute 與 VPN 閘道 tooforce 輸出使用使用者定義路由 (UDR)，並輸入的跨單位流量 toobe 路由的 tooa 網路的虛擬設備 (NVA)。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways tooforce outbound and inbound cross-premises traffic toobe routed tooa network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-hello-local-routes"></a><span data-ttu-id="7c7a2-144">建立 hello 區域路由</span><span class="sxs-lookup"><span data-stu-id="7c7a2-144">Creating hello local routes</span></span>
<span data-ttu-id="7c7a2-145">在此範例中，需要兩個路由表，分別指派給 hello 前端和 Backend 子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-145">In this example, two routing tables are needed, one each for hello Frontend and Backend subnets.</span></span> <span data-ttu-id="7c7a2-146">每個資料表會載入適當的 hello 指定子網路的靜態路由。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-146">Each table is loaded with static routes appropriate for hello given subnet.</span></span> <span data-ttu-id="7c7a2-147">為了 hello 此範例中，每一個資料表具有三個路由：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-147">For hello purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="7c7a2-148">沒有下個躍點定義 tooallow 本機子網路流量 toobypass hello 防火牆的本機子網路流量</span><span class="sxs-lookup"><span data-stu-id="7c7a2-148">Local subnet traffic with no Next Hop defined tooallow local subnet traffic toobypass hello firewall</span></span>
2. <span data-ttu-id="7c7a2-149">下個躍點定義防火牆為使用虛擬網路流量，這會覆寫，可讓本機 VNet 流量 tooroute 直接 hello 預設規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides hello default rule that allows local VNet traffic tooroute directly</span></span>
3. <span data-ttu-id="7c7a2-150">所有剩餘的流量 (0/0)，與下個躍點定義為 hello 防火牆</span><span class="sxs-lookup"><span data-stu-id="7c7a2-150">All remaining traffic (0/0) with a Next Hop defined as hello firewall</span></span>

<span data-ttu-id="7c7a2-151">一旦建立 hello 路由表是繫結的 tootheir 子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-151">Once hello routing tables are created they are bound tootheir subnets.</span></span> <span data-ttu-id="7c7a2-152">如 hello 前端子網路路由表，一旦建立並繫結 toohello 子網路看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-152">For hello Frontend subnet routing table, once created and bound toohello subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="7c7a2-153">此範例中，針對 hello 下列命令會使用的 toobuild hello 路由表中，新增使用者定義的路由，然後再繫結 hello 路由表 tooa 子網路 (請注意，貨幣符號開頭如下的任何項目 (例如： $BESubnet) 中的 hello 指令碼的使用者定義變數hello 參考本文件一節）：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-153">For this example, hello following commands are used toobuild hello route table, add a user defined route, and then bind hello route table tooa subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="7c7a2-154">必須建立第一個 hello 基底路由表。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-154">First hello base routing table must be created.</span></span> <span data-ttu-id="7c7a2-155">這個程式碼片段會顯示 hello 建立 hello 資料表 hello 後端子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-155">This snippet shows hello creation of hello table for hello Backend subnet.</span></span> <span data-ttu-id="7c7a2-156">Hello 的指令碼中對應的資料表也會建立為 hello Frontend 子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-156">In hello script, a corresponding table is also created for hello Frontend subnet.</span></span>
   
     <span data-ttu-id="7c7a2-157">New-AzureRouteTable -Name $BERouteTableName \`</span><span class="sxs-lookup"><span data-stu-id="7c7a2-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="7c7a2-158">一旦建立 hello 路由表，就可以新增特定的使用者定義的路由。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-158">Once hello route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="7c7a2-159">在這個片段中，會透過 hello 虛擬應用裝置 （$VMIP [0]，變數是在 [hello hello 虛擬設備稍早在 hello 指令碼中建立時指派的 IP 位址使用的 toopass） 路由傳送所有流量 (0.0.0.0/0)。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-159">In this snipped, all traffic (0.0.0.0/0) will be routed through hello virtual appliance (a variable, $VMIP[0], is used toopass in hello IP address assigned when hello virtual appliance was created earlier in hello script).</span></span> <span data-ttu-id="7c7a2-160">在 hello 指令碼對應的規則也會建立 hello 前端資料表中。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-160">In hello script, a corresponding rule is also created in hello Frontend table.</span></span>
   
     <span data-ttu-id="7c7a2-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="7c7a2-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="7c7a2-162">hello 路由項目上方將會覆寫 hello"0.0.0.0/0 」，預設路由但 hello 預設 10.0.0.0/16 規則還是現有的讓流量 hello VNet tooroute 內直接 toohello 目的地和 toohello 網路的虛擬設備。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-162">hello above route entry will override hello default "0.0.0.0/0" route, but hello default 10.0.0.0/16 rule still existing which would allow traffic within hello VNet tooroute directly toohello destination and not toohello Network Virtual Appliance.</span></span> <span data-ttu-id="7c7a2-163">toocorrect 必須新增此行為 hello 遵循規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-163">toocorrect this behavior hello follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="7c7a2-164">此時沒有所做的選擇 toobe。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-164">At this point there is a choice toobe made.</span></span> <span data-ttu-id="7c7a2-165">以上述兩個路由 hello 所有流量會路由都傳送 toohello 防火牆進行評估，甚至在單一子網路內的流量。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-165">With hello above two routes all traffic will route toohello firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="7c7a2-166">這可能需要，不過 tooallow 流量內的子網路 tooroute 本機而不需要涉入 hello 防火牆可以加入第三個、 非常特定的規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-166">This may be desired, however tooallow traffic within a subnet tooroute locally without involvement from hello firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="7c7a2-167">此路由狀態的任何位址 destine 就可以只 hello 本機子網路的路由那里直接 (NextHopType = VNETLocal)。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-167">This route states that any address destine for hello local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="7c7a2-168">最後，與 hello 路由表建立並填入使用者定義的路由，hello 資料表現在必須繫結的 tooa 子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-168">Finally, with hello routing table created and populated with a user defined routes, hello table must now be bound tooa subnet.</span></span> <span data-ttu-id="7c7a2-169">在 hello 指令碼 hello 前端路由表也是繫結的 toohello Frontend 子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-169">In hello script, hello front end route table is also bound toohello Frontend subnet.</span></span> <span data-ttu-id="7c7a2-170">以下是 hello hello 後端子網路的繫結指令碼。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-170">Here is hello binding script for hello back end subnet.</span></span>
   
     <span data-ttu-id="7c7a2-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span><span class="sxs-lookup"><span data-stu-id="7c7a2-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="7c7a2-172">IP 轉送</span><span class="sxs-lookup"><span data-stu-id="7c7a2-172">IP Forwarding</span></span>
<span data-ttu-id="7c7a2-173">附屬功能 tooUDR，是 IP 轉送。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-173">A companion feature tooUDR, is IP Forwarding.</span></span> <span data-ttu-id="7c7a2-174">這是 設定虛擬應用裝置，好讓它 tooreceive 流量未特別定址 toohello 應用裝置，然後轉寄該流量 tooits 最終目的端。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-174">This is a setting on a Virtual Appliance that allows it tooreceive traffic not specifically addressed toohello appliance and then forward that traffic tooits ultimate destination.</span></span>

<span data-ttu-id="7c7a2-175">例如，如果流量從 AppVM01 使得要求 toohello DNS01 伺服器，UDR 會路由此 toohello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-175">As an example, if traffic from AppVM01 makes a request toohello DNS01 server, UDR would route this toohello firewall.</span></span> <span data-ttu-id="7c7a2-176">與 IP 轉送已啟用，將接受 hello 應用裝置 (10.0.0.4) 並再轉寄 tooits 最終目的端 (10.0.2.4) hello hello DNS01 目的地 (10.0.2.4) 流量。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-176">With IP Forwarding enabled, hello traffic for hello DNS01 destination (10.0.2.4) will be accepted by hello appliance (10.0.0.4) and then forwarded tooits ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="7c7a2-177">不含 IP 轉送 hello 防火牆上啟用，流量就不會接受 hello 應用裝置即使 hello 路由表有 hello 防火牆為 hello 下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-177">Without IP Forwarding enabled on hello Firewall, traffic would not be accepted by hello appliance even though hello route table has hello firewall as hello next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7c7a2-178">它是關鍵 tooremember tooenable IP 轉送 」 搭配使用者定義之路由。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-178">It’s critical tooremember tooenable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="7c7a2-179">設定 IP 轉送是單一命令，可在建立 VM 時執行。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="7c7a2-180">Hello 流程，此範例 hello 程式碼片段朝向 hello hello 指令碼的結尾，並與 hello UDR 命令分組：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-180">For hello flow of this example hello code snippet is towards hello end of hello script and grouped with hello UDR commands:</span></span>

1. <span data-ttu-id="7c7a2-181">呼叫 hello VM 執行個體是您的虛擬應用裝置，請在此情況下，hello 防火牆並啟用 IP 轉送 」 (請注意，紅色貨幣符號開頭的任何項目 (例如： $VMName[0]) 是這份文件 hello 參考 > 一節中的 hello 指令碼的使用者定義變數。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-181">Call hello VM instance that is your virtual appliance, hello firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="7c7a2-182">hello 零以括號，[0] 代表 hello 的 Vm，而不需修改 hello 範例指令碼 toowork hello 陣列中的第一個 VM，必須是第一個 VM (VM 0) 的 hello hello 防火牆）：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-182">hello zero in brackets, [0], represents hello first VM in hello array of VMs, for hello example script toowork without modification, hello first VM (VM 0) must be hello firewall):</span></span>
   
     <span data-ttu-id="7c7a2-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span><span class="sxs-lookup"><span data-stu-id="7c7a2-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="7c7a2-184">網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="7c7a2-185">此範例會建置 NSG 群組，然後在其中載入單一規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="7c7a2-186">此群組，就只有 toohello 前端及後端的子網路 (不 hello SecNet) 繫結。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-186">This group is then bound only toohello Frontend and Backend subnets (not hello SecNet).</span></span> <span data-ttu-id="7c7a2-187">以宣告方式建立 hello 下列規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-187">Declaratively hello following rule is being built:</span></span>

1. <span data-ttu-id="7c7a2-188">任何流量 （所有連接埠），從 hello 網際網路 toohello 拒絕整個 VNet （所有的子網路）</span><span class="sxs-lookup"><span data-stu-id="7c7a2-188">Any traffic (all ports) from hello Internet toohello entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="7c7a2-189">雖然此範例使用 NSG，但它的主要目的是做為防止人為設定錯誤的第二道防線。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="7c7a2-190">我們希望 tooblock 所有傳入的流量 hello 網際網路 tooeither hello 前端或後端子網路流量只應該流經 hello SecNet 子網路 toohello 防火牆 （然後如果適當 toohello 前端或後端上子網路）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-190">We want tooblock all inbound traffic from hello internet tooeither hello Frontend or Backend subnets, traffic should only flow through hello SecNet subnet toohello firewall (and then if appropriate on toohello Frontend or Backend subnets).</span></span> <span data-ttu-id="7c7a2-191">此外，以 hello UDR 規則的地方，任何未將它轉換 hello 前端或後端的子網路的流量會被導向出 toohello 防火牆 (感謝您 tooUDR)。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-191">Plus, with hello UDR rules in place, any traffic that did make it into hello Frontend or Backend subnets would be directed out toohello firewall (thanks tooUDR).</span></span> <span data-ttu-id="7c7a2-192">hello 防火牆將會看到這個非對稱式資料流，然後會卸除 hello 輸出流量。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-192">hello firewall would see this as an asymmetric flow and would drop hello outbound traffic.</span></span> <span data-ttu-id="7c7a2-193">因此有三個層級的安全性保護 hello 前端和後端子網路。1) 沒有開啟端點上 hello FrontEnd001 和 BackEnd001 雲端服務，2) Nsg 拒絕流量從 hello 網際網路，3) hello 卸除對稱流量的防火牆。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-193">Thus there are three layers of security protecting hello Frontend and Backend subnets; 1) no open endpoints on hello FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from hello Internet, 3) hello firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="7c7a2-194">在此範例中的 hello 網路安全性群組相關的一個有趣的一點是它包含一個規則，底下所示，也就是 toodeny 網際網路流量 toohello 整個虛擬網路會包括子網路-安全性 hello。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-194">One interesting point regarding hello Network Security Group in this example is that it contains only one rule, shown below, which is toodeny internet traffic toohello entire virtual network which would include hello Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="7c7a2-195">不過，因為 hello NSG 僅繫結 toohello 前端和後端子網路，hello 規則不處理流量的輸入 toohello 安全性子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-195">However, since hello NSG is only bound toohello Frontend and Backend subnets, hello rule isn’t processed on traffic inbound toohello Security subnet.</span></span> <span data-ttu-id="7c7a2-196">如此一來，即使 hello NSG 規則會指出沒有網際網路流量 tooany 位址上 hello VNet，因為 hello NSG 從未繫結 toohello 安全性子網路，將流量 toohello 安全性子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-196">As a result, even though hello NSG rule says no Internet traffic tooany address on hello VNet, because hello NSG was never bound toohello Security subnet, traffic will flow toohello Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="7c7a2-197">防火牆規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-197">Firewall Rules</span></span>
<span data-ttu-id="7c7a2-198">Hello 防火牆上轉送規則需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-198">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="7c7a2-199">因為 hello 防火牆封鎖或轉送所有輸入、 輸出和內部 VNet 流量需要許多的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-199">Since hello firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="7c7a2-200">此外，所有傳入的流量會叫用 hello 安全性服務公用 IP 位址 （在不同的連接埠），toobe 處理 hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-200">Also, all inbound traffic will hit hello Security Service public IP address (on different ports), toobe processed by hello firewall.</span></span> <span data-ttu-id="7c7a2-201">最佳作法是在稍後設定 hello 子網路和防火牆規則 tooavoid 重新作業之前 toodiagram hello 邏輯流程。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-201">A best practice is toodiagram hello logical flows before setting up hello subnets and firewall rules tooavoid rework later.</span></span> <span data-ttu-id="7c7a2-202">hello 圖是此範例中的 hello 防火牆規則的邏輯檢視：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-202">hello following figure is a logical view of hello firewall rules for this example:</span></span>

<span data-ttu-id="7c7a2-203">![Hello 防火牆規則的邏輯檢視][2]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-203">![Logical View of hello Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="7c7a2-204">根據網路虛擬應用裝置中使用的 hello，hello 管理連接埠而異。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-204">Based on hello Network Virtual Appliance used, hello management ports will vary.</span></span> <span data-ttu-id="7c7a2-205">在此範例中，所參考的 Barracuda NextGen 防火牆使用連接埠 22、801 和 807。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="7c7a2-206">請參閱 hello 應用裝置廠商文件 toofind hello 確切使用連接埠正在使用的 hello 裝置的管理。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-206">Please consult hello appliance vendor documentation toofind hello exact ports used for management of hello device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="7c7a2-207">邏輯規則說明</span><span class="sxs-lookup"><span data-stu-id="7c7a2-207">Logical Rule Description</span></span>
<span data-ttu-id="7c7a2-208">Hello 邏輯在圖中，由於 hello 防火牆是 hello 該子，網路上唯一的資源，而且這個圖表會顯示 hello 防火牆規則和如何在邏輯上允許或拒絕流量和不 hello 實際路由的路徑，不會顯示 hello 安全性子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-208">In hello logical diagram above, hello security subnet is not shown since hello firewall is hello only resource on that subnet, and this diagram is showing hello firewall rules and how they logically allow or deny traffic flows and not hello actual routed path.</span></span> <span data-ttu-id="7c7a2-209">此外，hello 外部連接埠為 hello RDP 流量會更高範圍的連接埠 (8014 – 8026) 和已選取的 toosomewhat 對齊 hello 與選取的最後一個 hello 本機 IP 位址更容易閱讀的兩個八位元 （例如本機伺服器位址 10.0.1.4 相關聯外部連接埠 8014），但是無法使用任何更高版本的非衝突連接埠。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-209">Also, hello external ports selected for hello RDP traffic are higher ranged ports (8014 – 8026) and were selected toosomewhat align with hello last two octets of hello local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="7c7a2-210">在此範例中，我們需要 7 種規則，以下說明這些規則類型：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="7c7a2-211">外部規則 (適用於輸入流量)：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="7c7a2-212">防火牆管理規則： 這個應用程式重新導向規則允許流量 toopass toohello 管理連接埠的 hello 網路的虛擬設備。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-212">Firewall Management Rule: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance.</span></span>
  2. <span data-ttu-id="7c7a2-213">RDP 規則 （適用於每個 windows 伺服器）： 這些四項規則 （每個伺服器一個） 將允許的 hello 管理個別的伺服器，透過 RDP。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of hello individual servers via RDP.</span></span> <span data-ttu-id="7c7a2-214">這也可能集結成一個規則視 hello 的 hello 網路正在使用的虛擬應用裝置的功能而定。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-214">This could also be bundled into one rule depending on hello capabilities of hello Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="7c7a2-215">應用程式流量規則： 有兩個應用程式流量規則，先針對 hello 前端 web 流量，hello 和 hello hello 後端流量 （例如 web 伺服器 toodata 層） 的第二個。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-215">Application Traffic Rules: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="7c7a2-216">這些規則的 hello 組態將取決於 hello （您的伺服器放置的位置） 的網路架構及流量 （流動的方向 hello 流量，及使用哪些連接埠）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-216">hello configuration of these rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="7c7a2-217">hello 第一個規則可讓 hello 實際的應用程式流量 tooreach hello 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-217">hello first rule will allow hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="7c7a2-218">Hello 其他規則允許針對安全性、 管理等，而應用程式規則是允許外部使用者或服務 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-218">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="7c7a2-219">針對此範例中，連接埠 80 上沒有單一的 web 伺服器，因此單一防火牆應用程式規則將會重新導向輸入的流量 toohello 外部 IP，toohello web 伺服器的內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span> <span data-ttu-id="7c7a2-220">hello 重新導向流量的工作階段會 NAT 有 toohello 內部伺服器。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-220">hello redirected traffic session would be NAT’d toohello internal server.</span></span>
     * <span data-ttu-id="7c7a2-221">第二個應用程式流量規則的 hello hello 後端規則 tooallow hello Web 伺服器 tootalk toohello AppVM01 伺服器 （但不是 AppVM02），透過任何連接埠。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-221">hello second Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="7c7a2-222">內部規則 (適用於內部 VNet 流量)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="7c7a2-223">輸出 tooInternet 規則： 這項規則將會允許來自任何網路流量 toopass toohello 選取網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-223">Outbound tooInternet Rule: This rule will allow traffic from any network toopass toohello selected networks.</span></span> <span data-ttu-id="7c7a2-224">此規則通常是預設的規則已經 hello 在防火牆上，但是已停用狀態。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-224">This rule is usually a default rule already on hello firewall, but in a disabled state.</span></span> <span data-ttu-id="7c7a2-225">在此範例中，應啟用此規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="7c7a2-226">DNS 規則： 這個規則允許只有 DNS （連接埠 53） 流量 toopass toohello DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-226">DNS Rule: This rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="7c7a2-227">針對會封鎖大部分的流量 hello 前端 toohello 後端從這個環境，此規則特別允許 DNS 來自任何區域子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-227">For this environment most traffic from hello Frontend toohello Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="7c7a2-228">子網路 tooSubnet 規則： 這項規則是的 tooallow hello 後的任何伺服器端 hello 前端子網路上的子網路 tooconnect tooany 伺服器 （但不是 hello 反向）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-228">Subnet tooSubnet Rule: This rule is tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet (but not hello reverse).</span></span>
* <span data-ttu-id="7c7a2-229">（適用於不符合上述 hello 的流量） 的保全規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-229">Fail-safe Rule (for traffic that doesn’t meet any of hello above):</span></span>
  1. <span data-ttu-id="7c7a2-230">拒絕所有流量的規則： 這應該一律 hello 最終規則 （依據優先順序） 且因此如果流量流失敗時 toomatch hello 之前它就會卸除此規則的規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-230">Deny All Traffic Rule: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="7c7a2-231">這是預設規則且通常會啟動，一般來說並不需要修改。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="7c7a2-232">Hello 第二個應用程式流量規則，在任何連接埠允許的簡單的這個範例，在真實案例 hello 最特定的連接埠和位址範圍應使用的 tooreduce hello 受攻擊面，此規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-232">On hello second application traffic rule, any port is allowed for easy of this example, in a real scenario hello most specific port and address ranges should be used tooreduce hello attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="7c7a2-233">所有上述規則 hello 建立之後，請務必將允許或拒絕所需的每個規則 tooensure 流量 tooreview hello 優先順序。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-233">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="7c7a2-234">例如，hello 規則是依優先順序。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-234">For this example, hello rules are in priority order.</span></span> <span data-ttu-id="7c7a2-235">它是簡單 toobe 鎖定 hello 防火牆到期 toomis 排序規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-235">It's easy toobe locked out of hello firewall due toomis-ordered rules.</span></span> <span data-ttu-id="7c7a2-236">基本上，確保 hello 防火牆本身的 hello 管理永遠 hello 絕對最高優先權規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-236">At a minimum, ensure hello management for hello firewall itself is always hello absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="7c7a2-237">規則的必要條件</span><span class="sxs-lookup"><span data-stu-id="7c7a2-237">Rule Prerequisites</span></span>
<span data-ttu-id="7c7a2-238">必要條件 hello 虛擬機器執行 hello 防火牆，其中一個是公用端點。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-238">One prerequisite for hello Virtual Machine running hello firewall are public endpoints.</span></span> <span data-ttu-id="7c7a2-239">Hello 防火牆 tooprocess 流量 hello 適當的公用端點必須為開啟狀態。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-239">For hello firewall tooprocess traffic hello appropriate public endpoints must be open.</span></span> <span data-ttu-id="7c7a2-240">有三種類型的流量，在此範例中。1） 管理的傳輸 toocontrol hello 防火牆和防火牆規則、 2) RDP 流量 toocontrol hello windows 伺服器，以及 3） 應用程式的流量。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-240">There are three types of traffic in this example; 1) Management traffic toocontrol hello firewall and firewall rules, 2) RDP traffic toocontrol hello windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="7c7a2-241">這些邏輯檢視上述的 hello 防火牆規則的下半部是 hello 中 hello 上方的流量類型的三個資料行。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-241">These are hello three columns of traffic types in hello upper half of logical view of hello firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c7a2-242">此索引鍵 takeway 是 tooremember，**所有**流量將通過 hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-242">A key takeway here is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="7c7a2-243">因此 tooremote 桌面 toohello IIS01 伺服器，即使它是在 hello Front End 雲端服務和 hello 前端子網路，tooaccess 此我們需要 tooRDP toohello 防火牆的伺服器連接埠 8014，，然後允許 hello 防火牆 tooroute hello RDP 要求內部toohello IIS01 RDP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-243">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="7c7a2-244">hello Azure 入口網站的 [連線] 按鈕將無法運作，所以沒有直接的 RDP 路徑 tooIIS01 （就可以看到 hello 入口網站）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-244">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="7c7a2-245">這表示所有連線 hello 從網際網路將 toohello 安全性服務和連接埠，例如 secscv001.cloudapp.net:xxxx (參考 hello 上方圖表 hello 對應的外部連接埠和內部 IP 和連接埠)。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-245">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference hello above diagram for hello mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="7c7a2-246">端點可在 VM 建立 hello 時開啟或張貼組建，因為在 hello 範例指令碼中完成，而且此程式碼片段所示 (請注意，以貨幣符號的任何項目開頭 (例如： $VMName[$i]) 是 hello referen 中的 hello 指令碼的使用者定義變數本文件 ce 一節。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-246">An endpoint can be opened either at hello time of VM creation or post build as is done in hello example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="7c7a2-247">hello"$i 」 中，[$i]，代表特定 VM 的 Vm 陣列中的 hello 陣列編號）：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-247">hello “$i” in brackets, [$i], represents hello array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="7c7a2-248">雖然不清楚如下所示金額 toohello 使用變數，但端點是**只**hello 安全性雲端服務上開啟。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-248">Although not clearly shown here due toohello use of variables, but endpoints are **only** opened on hello Security Cloud Service.</span></span> <span data-ttu-id="7c7a2-249">這是處理的所有傳入的流量 tooensure （路由傳送，NAT，卸除） hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-249">This is tooensure that all inbound traffic is handled (routed, NAT'd, dropped) by hello firewall.</span></span>

<span data-ttu-id="7c7a2-250">管理用戶端將會需要 toobe PC toomanage hello 防火牆上安裝，並建立所需的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-250">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="7c7a2-251">Toomanage hello 裝置的方式，請參閱 hello 文件從您的防火牆 （或其他 NVA） 廠商。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-251">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="7c7a2-252">hello 這個區段和 hello 下一步 區段中，防火牆規則建立的其餘部分將說明 hello 透過 hello 廠商管理用戶端 （也就不是 hello Azure 入口網站或 PowerShell） 本身，hello 防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-252">hello remainder of this section and hello next section, Firewall Rules Creation, will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="7c7a2-253">用戶端下載及連接 toohello Barracuda 用在此範例中的指示可在這裡找到： [Barracuda NG 系統管理員](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-253">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="7c7a2-254">一旦登入 hello 防火牆但建立防火牆規則之前，有兩種必要的物件類別，可簡化建立 hello 規則;網路和服務的物件。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-254">Once logged onto hello firewall but before creating firewall rules, there are two prerequisite object classes that can make creating hello rules easier; Network & Service objects.</span></span>

<span data-ttu-id="7c7a2-255">此範例中，三個具名的網路物件應該定義 （一個用於 hello Frontend 子網路和 hello 後端子網路，也 hello hello DNS 伺服器 IP 位址的網路物件）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-255">For this example, three named network objects should be defined (one for hello Frontend subnet and hello Backend subnet, also a network object for hello IP address of hello DNS server).</span></span> <span data-ttu-id="7c7a2-256">toocreate 具名網路。從 hello Barracuda NG 管理用戶端儀表板開始，瀏覽 toohello 設定] 索引標籤、 hello 操作的組態區段中按一下 [規則集，然後在 hello 防火牆物件功能表上，按一下 「 網路 」 然後 hello 編輯網路功能表中按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-256">toocreate a named network; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Networks” under hello Firewall Objects menu, then click New in hello Edit Networks menu.</span></span> <span data-ttu-id="7c7a2-257">hello 網路物件現在可以建立，藉由新增 hello 名稱與 hello 前置詞：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-257">hello network object can now be created, by adding hello name and hello prefix:</span></span>

<span data-ttu-id="7c7a2-258">![建立 FrontEnd 網路物件][3]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="7c7a2-259">這會建立 hello FrontEnd 子網路的具名的網路，應該為 hello 後端的子網路以及建立類似的物件。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-259">This will create a named network for hello FrontEnd subnet, a similar object should be created for hello BackEnd subnet as well.</span></span> <span data-ttu-id="7c7a2-260">現在您可以更輕鬆地在 hello 防火牆規則中依名稱參考 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-260">Now hello subnets can be more easily referenced by name in hello firewall rules.</span></span>

<span data-ttu-id="7c7a2-261">Hello DNS 伺服器物件：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-261">For hello DNS Server Object:</span></span>

<span data-ttu-id="7c7a2-262">![建立 DNS 伺服器物件][4]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="7c7a2-263">DNS 規則 hello 文件中的更新版本中，系統會使用這個單一 IP 位址的參考。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-263">This single IP address reference will be utilized in a DNS rule later in hello document.</span></span>

<span data-ttu-id="7c7a2-264">hello 第二個必要條件物件是服務物件。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-264">hello second prerequisite objects are Services objects.</span></span> <span data-ttu-id="7c7a2-265">這些會代表每部伺服器的 hello RDP 連線通訊埠。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-265">These will represent hello RDP connection ports for each server.</span></span> <span data-ttu-id="7c7a2-266">由於 hello 現有 RDP 服務物件繫結的 toohello 預設 RDP 連接埠，3389，建立新的服務可以 tooallow 流量從 hello 外部連接埠 (8014 8026)。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-266">Since hello existing RDP service object is bound toohello default RDP port, 3389, new Services can be created tooallow traffic from hello external ports (8014-8026).</span></span> <span data-ttu-id="7c7a2-267">新的連接埠也可以加入現有 RDP service toohello，但為了便於示範，可以建立個別規則的每個伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-267">hello new ports could also be added toohello existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="7c7a2-268">toocreate 新 RDP 規則的伺服器。hello Barracuda NG 管理用戶端儀表板，從開始瀏覽 toohello 設定 索引標籤，在 hello 操作設定區段按一下規則集，然後 hello 防火牆物件功能表上，向下捲動服務的 hello 清單底下，按一下 服務，然後選取 hello「 RDP 」 服務。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-268">toocreate a new RDP rule for a server; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Services” under hello Firewall Objects menu, scroll down hello list of services and select hello “RDP” service.</span></span> <span data-ttu-id="7c7a2-269">按一下滑鼠右鍵並選取 [複製]，然後按一下滑鼠右鍵並選取 [貼上]。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="7c7a2-270">現在會有可供編輯的 RDP-Copy1 服務物件。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="7c7a2-271">RDP Copy1 上按一下滑鼠右鍵並選取 [編輯]，hello 編輯服務物件的視窗會隨即快顯如下所示：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-271">Right-click RDP-Copy1 and select Edit, hello Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="7c7a2-272">![預設 RDP 規則的複本][5]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="7c7a2-273">hello 值接著可以編輯的 toorepresent hello 特定伺服器的 RDP 服務。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-273">hello values can then be edited toorepresent hello RDP service for a specific server.</span></span> <span data-ttu-id="7c7a2-274">上述預設 AppVM01 hello RDP 規則應該修改的 tooreflect 新的服務名稱、 描述和外部的 RDP 連接埠用於 hello 圖 8 圖表 (注意： hello RDP 預設值是 3389 toohello 外部連接埠正在使用這個變更 hello 連接埠AppVM01 hello 外部連接埠的 hello 案例中的特定伺服器為 8025） hello 已修改的服務如下所示：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-274">For AppVM01 hello above default RDP rule should be modified tooreflect a new Service Name, Description, and external RDP Port used in hello Figure 8 diagram (Note: hello ports are changed from hello RDP default of 3389 toohello external port being used for this specific server, in hello case of AppVM01 hello external Port is 8025) hello modified service is shown below:</span></span>

<span data-ttu-id="7c7a2-275">![AppVM01 規則][6]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="7c7a2-276">此程序必須重複的 toocreate RDP 服務 hello 剩餘的伺服器。AppVM02、 DNS01 和 IIS01。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-276">This process must be repeated toocreate RDP Services for hello remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="7c7a2-277">這些服務的 hello 建立會讓 hello 規則建立更簡單且更明顯 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-277">hello creation of these Services will make hello Rule creation simpler and more obvious in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="7c7a2-278">Hello 防火牆 RDP 服務不需要有兩個原因。1） 第一個 hello 防火牆 VM 是 Linux 型映像會使用 SSH 連接埠 22 VM 管理，而不是 RDP 和 2） 通訊埠 22，因此 hello 下述 tooallow 管理連線能力的第一個管理規則允許兩個其他管理連接埠。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-278">An RDP service for hello Firewall is not needed for two reasons; 1) first hello firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in hello first management rule described below tooallow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="7c7a2-279">建立防火牆規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-279">Firewall Rules Creation</span></span>
<span data-ttu-id="7c7a2-280">此範例使用三種類型的防火牆規則，它們各有不同的圖示：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="7c7a2-281">hello 應用程式重新導向規則：![應用程式重新導向圖示][7]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-281">hello Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="7c7a2-282">hello 目的地 NAT 規則：![目的地 NAT 圖示][8]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-282">hello Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="7c7a2-283">hello 傳遞規則：![傳遞圖示][9]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-283">hello Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="7c7a2-284">這些規則的詳細資訊可以在 hello Barracuda 網站上找到。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-284">More information on these rules can be found at hello Barracuda web site.</span></span>

<span data-ttu-id="7c7a2-285">toocreate hello 下列規則 （或確認現有的預設規則），從 hello Barracuda NG 管理用戶端儀表板開始，瀏覽 toohello 設定 索引標籤、 在 hello 操作設定 區段按一下 規則集。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-285">toocreate hello following rules (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="7c7a2-286">方格呼叫時，「 主要規則 」 會顯示 hello 現有使用中且已停用此防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-286">A grid called, “Main Rules” will show hello existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="7c7a2-287">Hello 右上角的此方格是很小，綠色"+"按鈕，再按一下這個 toocreate 新的規則 (請注意： 您的防火牆可能 「 鎖定 」 的變更，如果您看到一個按鈕標示 「 鎖定 」，而且您會無法 toocreate 或編輯規則，請按一下此按鈕 「 解除鎖定 」 hello 太規則 set，並允許編輯)。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-287">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello rule set and allow editing).</span></span> <span data-ttu-id="7c7a2-288">如果您想 tooedit 現有的規則，就會選取該規則、 以滑鼠右鍵按一下並選取 編輯規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-288">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="7c7a2-289">一旦您的規則建立和/或修改，它們必須是推入 toohello 防火牆，然後啟動，如果這不是 hello 規則變更不會生效。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-289">Once your rules are created and/or modified, they must be pushed toohello firewall and then activated, if this is not done hello rule changes will not take effect.</span></span> <span data-ttu-id="7c7a2-290">hello 推播和啟動處理程序說明如下 hello 詳細資料的規則描述。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-290">hello push and activation process is described below hello details rule descriptions.</span></span>

<span data-ttu-id="7c7a2-291">每個規則的 hello 細節所需的 toocomplete 此範例中所述，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-291">hello specifics of each rule required toocomplete this example are described as follows:</span></span>

* <span data-ttu-id="7c7a2-292">**防火牆規則管理**： 此應用程式重新導向規則允許流量的 hello 網路虛擬應用裝置，在此範例中 Barracuda NextGen 防火牆 toopass toohello 管理連接埠。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-292">**Firewall Management Rule**: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="7c7a2-293">hello 管理連接埠為 801、 807 和選擇性 22。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-293">hello management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="7c7a2-294">hello 外部和內部連接埠是 hello 相同 （也就是沒有連接埠轉譯）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-294">hello external and internal ports are hello same (i.e. no port translation).</span></span> <span data-ttu-id="7c7a2-295">此 SETUP-MGMT-ACCESS 規則 (在 Barracuda NextGen 防火牆 6.1 版中) 是預設規則，且為預設啟用。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="7c7a2-296">![防火牆管理規則][10]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="7c7a2-297">hello 這個規則中的來源位址空間可以是任何，如果 hello 已知管理 IP 位址範圍時，減少此領域也會減少 hello 攻擊介面 toohello 管理連接埠。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-297">hello source address space in this rule is Any, if hello management IP address ranges are known, reducing this scope would also reduce hello attack surface toohello management ports.</span></span>
> 
> 

* <span data-ttu-id="7c7a2-298">**RDP 規則**： 這些目的地 NAT 規則將允許的 hello 管理個別的伺服器，透過 RDP。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-298">**RDP Rules**:  These Destination NAT rules will allow management of hello individual servers via RDP.</span></span>
  <span data-ttu-id="7c7a2-299">此規則有四個所需的重要欄位 toocreate:</span><span class="sxs-lookup"><span data-stu-id="7c7a2-299">There are four critical fields needed toocreate this rule:</span></span>
  
  1. <span data-ttu-id="7c7a2-300">來源 – tooallow RDP 從任何地方，hello 「 任何 」 用於 hello 來源欄位的參考。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-300">Source – tooallow RDP from anywhere, hello reference “Any” is used in hello Source field.</span></span>
  2. <span data-ttu-id="7c7a2-301">服務 – 使用適當的服務物件建立更早版本，在此情況下"AppVM01 RDP"hello，hello 外部連接埠重新導向 toohello 伺服器本機 IP 位址和 tooport 3386 （hello 預設 RDP 連接埠）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-301">Service – use hello appropriate Service Object created earlier, in this case “AppVM01 RDP”, hello external ports redirect toohello servers local IP address and tooport 3386 (hello default RDP port).</span></span> <span data-ttu-id="7c7a2-302">這個特定的規則是供 RDP 存取 tooAppVM01。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-302">This specific rule is for RDP access tooAppVM01.</span></span>
  3. <span data-ttu-id="7c7a2-303">目的地 – 應 hello *hello 防火牆上的本機連接埠*，[DCHP 1 本機 IP] 或 eth0 如果使用靜態 Ip。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-303">Destination – should be hello *local port on hello firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="7c7a2-304">hello 序數編號 （eth0、 eth1 等） 可能會不同，如果您的網路應用裝置有多個本機介面。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-304">hello ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="7c7a2-305">這是 hello 連接埠 hello 防火牆送出從 （可能為接收埠的 hello hello 相同），是在 hello 目標清單欄位的 hello 實際的路由的目的地。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-305">This is hello port hello firewall is sending out from (may be hello same as hello receiving port), hello actual routed destination is in hello Target List field.</span></span>
  4. <span data-ttu-id="7c7a2-306">重新導向 – 這一節說明虛擬應用裝置 hello tooultimately 而重新導向此流量。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-306">Redirection – this section tells hello virtual appliance where tooultimately redirect this traffic.</span></span> <span data-ttu-id="7c7a2-307">hello 最簡單的重新導向是 tooplace hello IP 和連接埠 （選用） 在 hello 目標清單的欄位。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-307">hello simplest redirection is tooplace hello IP and Port (optional) in hello Target List field.</span></span> <span data-ttu-id="7c7a2-308">如果沒有連接埠是使用的 hello hello 傳入要求上的目的地連接埠將會使用 （亦即未轉譯），如果連接埠指定 hello 連接埠也會是 NAT 會連同 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-308">If no port is used hello destination port on hello inbound request will be used (ie no translation), if a port is designated hello port will also be NAT’d along with hello IP address.</span></span>
     
     <span data-ttu-id="7c7a2-309">![防火牆 RDP 規則][11]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="7c7a2-310">總共四個 RDP 規則需要 toobe 建立：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-310">A total of four RDP rules will need toobe created:</span></span> 
     
     | <span data-ttu-id="7c7a2-311">規則名稱</span><span class="sxs-lookup"><span data-stu-id="7c7a2-311">Rule Name</span></span> | <span data-ttu-id="7c7a2-312">伺服器</span><span class="sxs-lookup"><span data-stu-id="7c7a2-312">Server</span></span> | <span data-ttu-id="7c7a2-313">服務</span><span class="sxs-lookup"><span data-stu-id="7c7a2-313">Service</span></span> | <span data-ttu-id="7c7a2-314">目標清單</span><span class="sxs-lookup"><span data-stu-id="7c7a2-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="7c7a2-315">RDP-to-IIS01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-315">RDP-to-IIS01</span></span> |<span data-ttu-id="7c7a2-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-316">IIS01</span></span> |<span data-ttu-id="7c7a2-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="7c7a2-317">IIS01 RDP</span></span> |<span data-ttu-id="7c7a2-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="7c7a2-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="7c7a2-319">RDP-to-DNS01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-319">RDP-to-DNS01</span></span> |<span data-ttu-id="7c7a2-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-320">DNS01</span></span> |<span data-ttu-id="7c7a2-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="7c7a2-321">DNS01 RDP</span></span> |<span data-ttu-id="7c7a2-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="7c7a2-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="7c7a2-323">RDP-to-AppVM01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="7c7a2-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-324">AppVM01</span></span> |<span data-ttu-id="7c7a2-325">AppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="7c7a2-325">AppVM01 RDP</span></span> |<span data-ttu-id="7c7a2-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="7c7a2-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="7c7a2-327">RDP-to-AppVM02</span><span class="sxs-lookup"><span data-stu-id="7c7a2-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="7c7a2-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="7c7a2-328">AppVM02</span></span> |<span data-ttu-id="7c7a2-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="7c7a2-329">AppVm02 RDP</span></span> |<span data-ttu-id="7c7a2-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="7c7a2-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="7c7a2-331">縮小下 hello 來源 hello 範圍和服務欄位將會減少 hello 受攻擊面。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-331">Narrowing down hello scope of hello Source and Service fields will reduce hello attack surface.</span></span> <span data-ttu-id="7c7a2-332">應該使用，可讓功能 hello 最有限的範圍。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-332">hello most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="7c7a2-333">**應用程式流量規則**： 有兩個應用程式流量規則，先針對 hello 前端 web 流量，hello 和 hello hello 後端流量 （例如 web 伺服器 toodata 層） 的第二個。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-333">**Application Traffic Rules**: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="7c7a2-334">這些規則將取決於 hello （您的伺服器放置的位置） 的網路架構及流量 （流動的方向 hello 流量，及使用哪些連接埠）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-334">These rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="7c7a2-335">先討論是 hello 前端網路流量的規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-335">First discussed is hello front end rule for web traffic:</span></span>
  
    <span data-ttu-id="7c7a2-336">![防火牆 Web 規則][12]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="7c7a2-337">此目的地 NAT 規則可讓 hello 實際的應用程式流量 tooreach hello 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-337">This Destination NAT rule allows hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="7c7a2-338">Hello 其他規則允許針對安全性、 管理等，而應用程式規則是允許外部使用者或服務 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-338">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="7c7a2-339">針對此範例中，連接埠 80 上沒有單一的 web 伺服器，因此 hello 單一防火牆應用程式規則將會重新導向輸入的流量 toohello 外部 IP，toohello web 伺服器的內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-339">For this example, there is a single web server on port 80, thus hello single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span>
  
    <span data-ttu-id="7c7a2-340">**請注意**： 沒有指定在 hello 目標清單的欄位中的通訊埠，因此 hello 輸入連接埠 80 （或 hello 選取服務為 443） 將會使用 hello hello web 伺服器的重新導向。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-340">**Note**: that there is no port assigned in hello Target List field, thus hello inbound port 80 (or 443 for hello Service selected) will be used in hello redirection of hello web server.</span></span> <span data-ttu-id="7c7a2-341">如果 hello web 伺服器正在接聽不同的通訊埠，如連接埠 8080，hello 目標清單的欄位可能是更新的 too10.0.1.4:8080 tooallow 以及 hello 連接埠重新導向。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-341">If hello web server is listening on a different port, for example port 8080, hello Target List field could be updated too10.0.1.4:8080 tooallow for hello Port redirection as well.</span></span>
  
    <span data-ttu-id="7c7a2-342">下一個應用程式流量規則是的 hello hello 透過任何服務的後端規則 tooallow hello Web 伺服器 tootalk toohello AppVM01 伺服器 （但不是 AppVM02）：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-342">hello next Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="7c7a2-343">![防火牆 AppVM01 規則][13]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="7c7a2-344">此階段規則可讓 IIS 上任何伺服器 hello 前端子網路 tooreach hello AppVM01 （IP 位址 10.0.2.5） 上任何連接埠，使用 hello web 應用程式所需的任何通訊協定 tooaccess 資料。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-344">This Pass rule allows any IIS server on hello Frontend subnet tooreach hello AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol tooaccess data needed by hello web application.</span></span>
  
    <span data-ttu-id="7c7a2-345">在這個螢幕擷取畫面 」\<明確目的地\>"hello 目的地欄位 toosignify 10.0.2.5 中做 hello 目的地。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-345">In this screen shot an "\<explicit-dest\>" is used in hello Destination field toosignify 10.0.2.5 as hello destination.</span></span> <span data-ttu-id="7c7a2-346">這可以是明確所示的具名網路物件 （為 「 已完成在 hello hello DNS 伺服器的先決條件）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-346">This could be either explicit as shown or a named Network Object (as was done in hello prerequisites for hello DNS server).</span></span> <span data-ttu-id="7c7a2-347">這是總 toohello hello 防火牆的系統管理員將使用 toowhich 方法。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-347">This is up toohello administrator of hello firewall as toowhich method will be used.</span></span> <span data-ttu-id="7c7a2-348">hello 第一個空白資料列下按兩下 tooadd 10.0.2.5 Explict Desitnation，為\<明確目的地\>快顯的 hello 視窗中輸入 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-348">tooadd 10.0.2.5 as an Explict Desitnation, double-click on hello first blank row under \<explicit-dest\> and enter hello address in hello window that pops up.</span></span>
  
    <span data-ttu-id="7c7a2-349">由於這是內部的流量，以便太設定 hello 連線方法，沒有 NAT 需要此傳遞規則之後，「 否 SNAT"。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-349">With this Pass Rule, no NAT is needed since this is internal traffic, so hello Connection Method can be set too"No SNAT".</span></span>
  
    <span data-ttu-id="7c7a2-350">**請注意**： 如果只會有一個，或是已知特定數目的網頁伺服器、 網路物件資源可能會建立 toobe 更特定 toothose 確切的 IP 位址而不是，此規則中的 hello 來源網路是 hello 前端子網路上的任何資源hello 整個 Frontend 子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-350">**Note**: hello Source network in this rule is any resource on hello FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created toobe more specific toothose exact IP addresses instead of hello entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="7c7a2-351">此規則使用"Any"toomake hello 範例應用程式更容易 toosetup 並用 hello 服務，這也可讓 ICMPv4 (ping) 中的單一規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-351">This rule uses hello service “Any” toomake hello sample application easier toosetup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="7c7a2-352">不過，這不是建議的作法。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="7c7a2-353">hello 連接埠和通訊協定 （「 服務 」） 應該縮小 toohello 最小可能在跨界限可讓應用程式作業 tooreduce hello 受攻擊面。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-353">hello ports and protocols (“Services”) should be narrowed toohello minimum possible that allows application operation tooreduce hello attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="7c7a2-354">雖然此規則會顯示正在使用的明確目的參考，以一致的方法應該用於整個 hello 防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout hello firewall configuration.</span></span> <span data-ttu-id="7c7a2-355">建議您在名為的網路物件的 hello 用於整個更容易閱讀，並可支援性。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-355">It is recommended that hello named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="7c7a2-356">hello 的明確目的地是使用此處的唯一 tooshow 替代參考方法，通常不建議 （特別是針對複雜的組態）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-356">hello explicit-dest is used here only tooshow an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="7c7a2-357">**輸出 tooInternet 規則**： 此傳遞規則以允許從任何來源網路 toopass toohello 選取目的地網路的流量。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-357">**Outbound tooInternet Rule**: This Pass rule will allow traffic from any Source network toopass toohello selected Destination networks.</span></span> <span data-ttu-id="7c7a2-358">此規則是 hello Barracuda NextGen 在防火牆上，通常已經預設規則，但處於停用狀態。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-358">This rule is a default rule usually already on hello Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="7c7a2-359">此規則上按一下滑鼠右鍵，可以存取 hello 啟用 Rule 命令。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-359">Right-clicking on this rule can access hello Activate Rule command.</span></span> <span data-ttu-id="7c7a2-360">如下所示的 hello 規則已修改過的 tooadd hello 兩本機子網路做為參考，此規則的這個文件 toohello 來源屬性 hello 必要條件一節中所建立。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-360">hello rule shown here has been modified tooadd hello two local subnets that were created as references in hello prerequisite section of this document toohello Source attribute of this rule.</span></span>
  
    <span data-ttu-id="7c7a2-361">![防火牆輸出規則][14]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="7c7a2-362">**DNS 規則**： 此傳遞規則允許只有 DNS （連接埠 53） 流量 toopass toohello DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="7c7a2-363">針對會封鎖大部分的流量 hello 前端 toohello 後端從這個環境，此規則特別允許 DNS。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-363">For this environment most traffic from hello FrontEnd toohello BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="7c7a2-364">![防火牆 DNS 規則][15]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="7c7a2-365">**請注意**： 在此畫面次的 hello 連線方法是否包含。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-365">**Note**: In this screen shot hello Connection Method is included.</span></span> <span data-ttu-id="7c7a2-366">此規則為內部 IP toointernal IP 位址流量，因為沒有 NATing 是必要，但是這個 hello 連線方式設定過此階段規則的"No SNAT"。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-366">Because this rule is for internal IP toointernal IP address traffic, no NATing is required, this hello Connection Method is set too“No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="7c7a2-367">**子網路 tooSubnet 規則**： 此傳遞規則是預設規則已啟動，並修改的 tooallow 回 hello 上的任何伺服器端的子網路 tooconnect tooany 伺服器 hello 前端子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-367">**Subnet tooSubnet Rule**: This Pass rule is a default rule that has been activated and modified tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet.</span></span> <span data-ttu-id="7c7a2-368">此規則為內部所有流量以便 hello 連線方式設定 tooNo SNAT。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-368">This rule is all internal traffic so hello Connection Method can be set tooNo SNAT.</span></span>
  
    <span data-ttu-id="7c7a2-369">![防火牆內部 VNet 規則][16]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="7c7a2-370">**請注意**: hello 雙向核取方塊未核取 （也不是簽入大多數規則），這是極大的這項規則，因為它可讓規則 「 單向 」 這，可以從 hello 後端子 toohello 前端網路，起始的連線但不是 hello 反向。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-370">**Note**: hello Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from hello back end subnet toohello front end network, but not hello reverse.</span></span> <span data-ttu-id="7c7a2-371">如果核取該核取方塊，此規則就會啟用雙向流量，從我們的邏輯圖來看並不需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="7c7a2-372">**拒絕所有流量規則**： 應一律為 hello 最終規則 （依據優先順序），因此如果流量流失敗 toomatch 任何上述規則 hello 它就會卸除此規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-372">**Deny All Traffic Rule**: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="7c7a2-373">這是預設規則且通常會啟動，一般來說並不需要修改。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="7c7a2-374">![防火牆拒絕規則][17]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c7a2-375">所有上述規則 hello 建立之後，請務必將允許或拒絕所需的每個規則 tooensure 流量 tooreview hello 優先順序。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-375">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="7c7a2-376">例如，hello 規則是 hello 順序他們應該會顯示 hello 的轉送規則 hello Barracuda 管理用戶端在主要方格中。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-376">For this example, hello rules are in hello order they should appear in hello Main Grid of forwarding rules in hello Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="7c7a2-377">啟用規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-377">Rule Activation</span></span>
<span data-ttu-id="7c7a2-378">Hello 規則集必須是與 hello ruleset 修改 toohello hello 邏輯圖表的規格上, 傳 toohello 防火牆，然後啟動。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-378">With hello ruleset modified toohello specification of hello logic diagram, hello ruleset must be uploaded toohello firewall and then activated.</span></span>

<span data-ttu-id="7c7a2-379">![防火牆規則啟用][18]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="7c7a2-380">在 hello 右上角的 hello 管理用戶端都是叢集的按鈕。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-380">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="7c7a2-381">按一下 hello 傳送變更 按鈕 toosend hello 修改規則 toohello 防火牆，然後按一下 hello 「 啟用 」 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-381">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="7c7a2-382">與 hello 啟用 hello 防火牆規則集的範例環境的這個組建已完成。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-382">With hello activation of hello firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="7c7a2-383">流量案例</span><span class="sxs-lookup"><span data-stu-id="7c7a2-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7c7a2-384">索引鍵 takeway 是 tooremember，**所有**流量將通過 hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-384">A key takeway is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="7c7a2-385">因此 tooremote 桌面 toohello IIS01 伺服器，即使它是在 hello Front End 雲端服務和 hello 前端子網路，tooaccess 此我們需要 tooRDP toohello 防火牆的伺服器連接埠 8014，，然後允許 hello 防火牆 tooroute hello RDP 要求內部toohello IIS01 RDP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-385">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="7c7a2-386">hello Azure 入口網站的 [連線] 按鈕將無法運作，所以沒有直接的 RDP 路徑 tooIIS01 （就可以看到 hello 入口網站）。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-386">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="7c7a2-387">這表示所有連線 hello 從網際網路將 toohello 安全性服務和連接埠，例如 secscv001.cloudapp.net:xxxx。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-387">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="7c7a2-388">針對這些案例，hello 下列防火牆規則應該有：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-388">For these scenarios, hello following firewall rules should be in place:</span></span>

1. <span data-ttu-id="7c7a2-389">防火牆管理</span><span class="sxs-lookup"><span data-stu-id="7c7a2-389">Firewall Management</span></span>
2. <span data-ttu-id="7c7a2-390">RDP tooIIS01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-390">RDP tooIIS01</span></span>
3. <span data-ttu-id="7c7a2-391">RDP tooDNS01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-391">RDP tooDNS01</span></span>
4. <span data-ttu-id="7c7a2-392">RDP tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-392">RDP tooAppVM01</span></span>
5. <span data-ttu-id="7c7a2-393">RDP tooAppVM02</span><span class="sxs-lookup"><span data-stu-id="7c7a2-393">RDP tooAppVM02</span></span>
6. <span data-ttu-id="7c7a2-394">應用程式流量 toohello Web</span><span class="sxs-lookup"><span data-stu-id="7c7a2-394">App Traffic toohello Web</span></span>
7. <span data-ttu-id="7c7a2-395">應用程式流量 tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-395">App Traffic tooAppVM01</span></span>
8. <span data-ttu-id="7c7a2-396">輸出 toohello 網際網路</span><span class="sxs-lookup"><span data-stu-id="7c7a2-396">Outbound toohello Internet</span></span>
9. <span data-ttu-id="7c7a2-397">前端 tooDNS01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-397">Frontend tooDNS01</span></span>
10. <span data-ttu-id="7c7a2-398">內部子網路的流量 （只後端 toofront 結束）</span><span class="sxs-lookup"><span data-stu-id="7c7a2-398">Intra-Subnet Traffic (back end toofront end only)</span></span>
11. <span data-ttu-id="7c7a2-399">全部拒絕</span><span class="sxs-lookup"><span data-stu-id="7c7a2-399">Deny All</span></span>

<span data-ttu-id="7c7a2-400">hello 實際的防火牆規則集最有可能很多其他規則中加入 toothese，比此處所列的 hello，hello 任何給定的防火牆規則也會有不同的優先順序數字。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-400">hello actual firewall ruleset will most likely have many other rules in addition toothese, hello rules on any given firewall will also have different priority numbers than hello ones listed here.</span></span> <span data-ttu-id="7c7a2-401">此清單和相關聯的數字是 tooprovide 只這些 11 個規則和 hello 相對優先權彼此之間的相關性。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-401">This list and associated numbers are tooprovide relevance between just these eleven rules and hello relative priority amongst them.</span></span> <span data-ttu-id="7c7a2-402">換句話說，hello 實際在防火牆上，hello"RDP tooIIS01 」 可能是規則數字 5，但只要它是之下 hello 「 防火牆管理 」 規則，其會與此清單的 hello 意圖對齊 hello"RDP tooDNS01 」 規則。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-402">In other words; on hello actual firewall, hello “RDP tooIIS01” may be rule number 5, but as long as it’s below hello “Firewall Management” rule and above hello “RDP tooDNS01” rule it would align with hello intention of this list.</span></span> <span data-ttu-id="7c7a2-403">hello 清單也有助於 hello 以下案例允許為求簡單明瞭。例如：「FW 規則 9 (DNS)」。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-403">hello list will also aid in hello below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="7c7a2-404">為求簡潔，四個 RDP 規則將會是共同的 hello 稱，"hello RDP 規則"hello 流量案例時 tooRDP 不相關。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-404">Also for brevity, hello four RDP rules will be collectively called, “hello RDP rules” when hello traffic scenario is unrelated tooRDP.</span></span>

<span data-ttu-id="7c7a2-405">也請記得網路安全性群組會就地升級輸入網際網路上的流量 hello 前端和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-405">Also recall that Network Security Groups are in-place for inbound internet traffic on hello Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="7c7a2-406">（允許）網際網路 tooWeb 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c7a2-406">(Allowed) Internet tooWeb Server</span></span>
1. <span data-ttu-id="7c7a2-407">網際網路使用者從 SecSvc001.CloudApp.Net (網際網路面向雲端服務) 要求 HTTP 頁面</span><span class="sxs-lookup"><span data-stu-id="7c7a2-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="7c7a2-408">雲端服務將流量透過開啟連接埠 80 上 10.0.0.4:80 的 toofirewall 介面上的端點</span><span class="sxs-lookup"><span data-stu-id="7c7a2-408">Cloud service passes traffic through open endpoint on port 80 toofirewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="7c7a2-409">指派 tooSecurity 子網路，所以系統 NSG 規則允許流量 toofirewall 沒有 NSG</span><span class="sxs-lookup"><span data-stu-id="7c7a2-409">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="7c7a2-410">流量達到 hello 防火牆 (10.0.1.4) 的內部 IP 位址</span><span class="sxs-lookup"><span data-stu-id="7c7a2-410">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="7c7a2-411">防火牆開始處理規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="7c7a2-412">FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-412">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7c7a2-413">FW 規則 2-5 （RDP 規則） 不套用，請移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7c7a2-414">FW 規則 6 (應用程式： Web) 會套用，允許流量，防火牆 Nat 它 too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it too10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="7c7a2-415">hello Frontend 子網路會開始處理輸入的規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-415">hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7c7a2-416">NSG 規則 1 （封鎖網際網路） 並不適用 (此流量已 NAT 像 hello 防火牆，因此 hello 來源位址現在是 hello 防火牆，它會在 hello 安全性子網路上，看到 hello Frontend 子網路 NSG toobe 「 本機 」 流量，因此允許)，移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Frontend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="7c7a2-417">預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-417">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="7c7a2-418">IIS01 接聽 web 流量、 收到此要求，並開始處理 hello 要求</span><span class="sxs-lookup"><span data-stu-id="7c7a2-418">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
8. <span data-ttu-id="7c7a2-419">IIS01 嘗試後端子網路上的 FTP 工作階段 tooAppVM01 tooinitiates</span><span class="sxs-lookup"><span data-stu-id="7c7a2-419">IIS01 attempts tooinitiates an FTP session tooAppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="7c7a2-420">Frontend 子網路上的 hello UDR 路由可讓 hello 防火牆 hello 下一個躍點</span><span class="sxs-lookup"><span data-stu-id="7c7a2-420">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
10. <span data-ttu-id="7c7a2-421">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="7c7a2-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="7c7a2-422">防火牆開始處理規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="7c7a2-423">FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-423">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7c7a2-424">不適用 FW 規則 2-5 （RDP 規則），移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="7c7a2-425">FW 規則 6 (應用程式： Web) 不會套用，請移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-425">FW Rule 6 (App: Web) doesn’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="7c7a2-426">FW 規則 7 (應用程式： 後端) 會套用，允許流量，防火牆將轉送流量 too10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic too10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="7c7a2-427">hello 後端子網路會開始處理輸入的規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-427">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7c7a2-428">NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-428">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7c7a2-429">預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-429">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="7c7a2-430">AppVM01 收到 hello 要求，並起始 hello 工作階段，而會回應</span><span class="sxs-lookup"><span data-stu-id="7c7a2-430">AppVM01 receives hello request and initiates hello session and responds</span></span>
14. <span data-ttu-id="7c7a2-431">後端子網路上的 hello UDR 路由可讓 hello 防火牆 hello 下一個躍點</span><span class="sxs-lookup"><span data-stu-id="7c7a2-431">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
15. <span data-ttu-id="7c7a2-432">因為允許在後端子網路 hello 回應 hello 沒有輸出 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-432">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
16. <span data-ttu-id="7c7a2-433">因為這傳回流量上建立之工作階段 hello 防火牆傳送 hello 回應後 toohello 網頁伺服器 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-433">Because this is returning traffic on an established session hello firewall passes hello response back toohello web server (IIS01)</span></span>
17. <span data-ttu-id="7c7a2-434">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7c7a2-435">NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-435">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7c7a2-436">預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-436">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="7c7a2-437">hello IIS 伺服器收到 hello 回應、 完成 AppVM01，hello 交易，然後完成 建立 hello HTTP 回應，這個 HTTP 回應會傳送 toohello 要求者</span><span class="sxs-lookup"><span data-stu-id="7c7a2-437">hello IIS server receives hello response, completes hello transaction with AppVM01, and then completes building hello HTTP response, this HTTP response is sent toohello requestor</span></span>
19. <span data-ttu-id="7c7a2-438">由於有允許前端子網路 hello 回應 hello 上的沒有輸出 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-438">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
20. <span data-ttu-id="7c7a2-439">hello HTTP 回應的叫用 hello 防火牆和 NAT 工作階段因為這是建立 hello 回應 tooan 接受 hello 防火牆</span><span class="sxs-lookup"><span data-stu-id="7c7a2-439">hello HTTP response hits hello firewall, and because this is hello response tooan established NAT session is accepted by hello firewall</span></span>
21. <span data-ttu-id="7c7a2-440">hello 防火牆會重新導向 hello 回應後 toohello 網際網路使用者</span><span class="sxs-lookup"><span data-stu-id="7c7a2-440">hello firewall then redirects hello response back toohello Internet User</span></span>
22. <span data-ttu-id="7c7a2-441">由於沒有任何輸出 NSG 規則或 UDR 躍點 hello Frontend 子網路上允許 hello 回應，而 hello 網際網路使用者會收到要求的 hello 網頁。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-441">Since there are no outbound NSG rules or UDR hops on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-internet-rdp-toobackend"></a><span data-ttu-id="7c7a2-442">（允許）網際網路 RDP tooBackend</span><span class="sxs-lookup"><span data-stu-id="7c7a2-442">(Allowed) Internet RDP tooBackend</span></span>
1. <span data-ttu-id="7c7a2-443">網際網路上的伺服器系統管理員要求 RDP 工作階段 tooAppVM01 透過 SecSvc001.CloudApp.Net:8025，8025 所在 hello"RDP tooAppVM01 」 防火牆規則的 hello 指派給使用者的連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="7c7a2-443">Server Admin on internet requests RDP session tooAppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is hello user assigned port number for hello “RDP tooAppVM01” firewall rule</span></span>
2. <span data-ttu-id="7c7a2-444">hello 雲端服務則傳遞 8025 toofirewall 介面連接埠上 10.0.0.4:8025 流量通過 hello 開放式端點</span><span class="sxs-lookup"><span data-stu-id="7c7a2-444">hello cloud service passes traffic through hello open endpoint on port 8025 toofirewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="7c7a2-445">指派 tooSecurity 子網路，所以系統 NSG 規則允許流量 toofirewall 沒有 NSG</span><span class="sxs-lookup"><span data-stu-id="7c7a2-445">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="7c7a2-446">防火牆開始處理規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="7c7a2-447">FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-447">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7c7a2-448">不會套用 FW 規則 2 (RDP IIS)，移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-448">FW Rule 2 (RDP IIS) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7c7a2-449">FW 規則 3 (RDP DNS01) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-449">FW Rule 3 (RDP DNS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="7c7a2-450">FW 規則 4 (RDP AppVM01) 會套用，允許流量，防火牆 Nat 它 too10.0.2.5:3386 （AppVM01 上的 RDP 連接埠）</span><span class="sxs-lookup"><span data-stu-id="7c7a2-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it too10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="7c7a2-451">hello 後端子網路會開始處理輸入的規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-451">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7c7a2-452">NSG 規則 1 （封鎖網際網路） 並不適用 (此流量已 NAT 像 hello 防火牆，因此 hello 來源位址現在是 hello 防火牆，它會在 hello 安全性子網路上，看到 hello 後端子網路 NSG toobe 「 本機 」 流量，因此允許)，移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Backend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="7c7a2-453">預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-453">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="7c7a2-454">AppVM01 正在接聽 RDP 流量並回應</span><span class="sxs-lookup"><span data-stu-id="7c7a2-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="7c7a2-455">由於沒有輸出 NSG 規則，會套用預設規則並允許傳回的流量</span><span class="sxs-lookup"><span data-stu-id="7c7a2-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="7c7a2-456">UDR 路由傳出流量 toohello 防火牆為 hello 下一個躍點</span><span class="sxs-lookup"><span data-stu-id="7c7a2-456">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
9. <span data-ttu-id="7c7a2-457">因為這傳回流量上建立之工作階段 hello 防火牆傳送 hello 回應後 toohello 網際網路使用者</span><span class="sxs-lookup"><span data-stu-id="7c7a2-457">Because this is returning traffic on an established session hello firewall passes hello response back toohello internet user</span></span>
10. <span data-ttu-id="7c7a2-458">已啟用 RDP 工作階段</span><span class="sxs-lookup"><span data-stu-id="7c7a2-458">RDP session is enabled</span></span>
11. <span data-ttu-id="7c7a2-459">AppVM01 會提示輸入使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="7c7a2-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="7c7a2-460">(允許) DNS 伺服器上的 Web 伺服器 DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="7c7a2-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="7c7a2-461">Web 伺服器，IIS01，需要的資料摘要在 www.data.gov，但需要 tooresolve hello 位址。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="7c7a2-462">hello 的網路組態 hello VNet 清單 DNS01 (10.0.2.4 hello 後端子網路上) 做為主要 DNS 伺服器 hello，IIS01 傳送 hello DNS 要求 tooDNS01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-462">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="7c7a2-463">UDR 路由傳出流量 toohello 防火牆為 hello 下一個躍點</span><span class="sxs-lookup"><span data-stu-id="7c7a2-463">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
4. <span data-ttu-id="7c7a2-464">沒有輸出的 NSG 規則是繫結的 toohello Frontend 子網路，允許流量</span><span class="sxs-lookup"><span data-stu-id="7c7a2-464">No outbound NSG rules are bound toohello Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="7c7a2-465">防火牆開始處理規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="7c7a2-466">FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-466">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7c7a2-467">不適用 FW 規則 2-5 （RDP 規則），移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7c7a2-468">不適用 FW 規則 6 和 7 （應用程式的規則），移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-468">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="7c7a2-469">FW 規則 8 (tooInternet) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-469">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="7c7a2-470">FW 規則 9 (DNS) 會套用，允許流量，防火牆將轉送流量 too10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic too10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="7c7a2-471">hello 後端子網路會開始處理輸入的規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-471">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7c7a2-472">NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-472">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7c7a2-473">預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-473">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="7c7a2-474">DNS 伺服器收到 hello 要求</span><span class="sxs-lookup"><span data-stu-id="7c7a2-474">DNS server receives hello request</span></span>
8. <span data-ttu-id="7c7a2-475">DNS 伺服器沒有快取的 hello 位址和要求的根 DNS 伺服器上 hello 網際網路</span><span class="sxs-lookup"><span data-stu-id="7c7a2-475">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
9. <span data-ttu-id="7c7a2-476">UDR 路由傳出流量 toohello 防火牆為 hello 下一個躍點</span><span class="sxs-lookup"><span data-stu-id="7c7a2-476">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
10. <span data-ttu-id="7c7a2-477">Backend 子網路上沒有輸出 NSG 規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="7c7a2-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="7c7a2-478">防火牆開始處理規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="7c7a2-479">FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-479">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7c7a2-480">不適用 FW 規則 2-5 （RDP 規則），移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="7c7a2-481">不適用 FW 規則 6 和 7 （應用程式的規則），移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-481">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="7c7a2-482">FW 規則 8 (tooInternet) 會套用，允許流量，工作階段已 SNAT 推出 tooroot hello 網際網路上的 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c7a2-482">FW Rule 8 (tooInternet) does apply, traffic is allowed, session is SNAT out tooroot DNS server on hello Internet</span></span>
12. <span data-ttu-id="7c7a2-483">網際網路 DNS 伺服器回應，因為此工作階段起始從 hello 防火牆，hello 回應接受 hello 防火牆</span><span class="sxs-lookup"><span data-stu-id="7c7a2-483">Internet DNS server responds, since this session was initiated from hello firewall, hello response is accepted by hello firewall</span></span>
13. <span data-ttu-id="7c7a2-484">因為這是已建立的工作階段，hello 防火牆轉送 hello 回應 toohello 起始伺服器，DNS01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-484">As this is an established session, hello firewall forwards hello response toohello initiating server, DNS01</span></span>
14. <span data-ttu-id="7c7a2-485">hello 後端子網路會開始處理輸入的規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-485">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7c7a2-486">NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-486">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7c7a2-487">預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-487">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="7c7a2-488">hello DNS 伺服器會接收和快取 hello 回應，並再回應 toohello 初始要求後 tooIIS01</span><span class="sxs-lookup"><span data-stu-id="7c7a2-488">hello DNS server receives and caches hello response, and then responds toohello initial request back tooIIS01</span></span>
16. <span data-ttu-id="7c7a2-489">後端子網路上的 hello UDR 路由可讓 hello 防火牆 hello 下一個躍點</span><span class="sxs-lookup"><span data-stu-id="7c7a2-489">hello UDR route on backend subnet makes hello firewall hello next hop</span></span>
17. <span data-ttu-id="7c7a2-490">Hello 後端子網路上不存在任何輸出 NSG 規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="7c7a2-490">No outbound NSG rules exist on hello Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="7c7a2-491">這是建立之工作階段上 hello 防火牆，轉寄 hello 回應 hello 防火牆後 toohello IIS 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c7a2-491">This is an established session on hello firewall, hello response is forwarded by hello firewall back toohello IIS server</span></span>
19. <span data-ttu-id="7c7a2-492">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7c7a2-493">套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-493">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="7c7a2-494">hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量</span><span class="sxs-lookup"><span data-stu-id="7c7a2-494">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
20. <span data-ttu-id="7c7a2-495">IIS01 DNS01 收到 hello 回應</span><span class="sxs-lookup"><span data-stu-id="7c7a2-495">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-backend-server-toofrontend-server"></a><span data-ttu-id="7c7a2-496">（允許）後端伺服器 tooFrontend 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c7a2-496">(Allowed) Backend server tooFrontend server</span></span>
1. <span data-ttu-id="7c7a2-497">系統管理員登入透過 RDP tooAppVM02 要求直接從 hello IIS01 伺服器，透過 windows 檔案總管中的檔案</span><span class="sxs-lookup"><span data-stu-id="7c7a2-497">An administrator logged on tooAppVM02 via RDP requests a file directly from hello IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="7c7a2-498">後端子網路上的 hello UDR 路由可讓 hello 防火牆 hello 下一個躍點</span><span class="sxs-lookup"><span data-stu-id="7c7a2-498">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
3. <span data-ttu-id="7c7a2-499">因為允許在後端子網路 hello 回應 hello 沒有輸出 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-499">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
4. <span data-ttu-id="7c7a2-500">防火牆開始處理規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="7c7a2-501">FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-501">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7c7a2-502">不適用 FW 規則 2-5 （RDP 規則），移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7c7a2-503">不適用 FW 規則 6 和 7 （應用程式的規則），移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-503">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="7c7a2-504">FW 規則 8 (tooInternet) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-504">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="7c7a2-505">不會套用 FW 規則 9 (DNS)，移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-505">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="7c7a2-506">FW 規則 10 （內部子網路） 會套用，允許流量，防火牆會傳遞流量 too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="7c7a2-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic too10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="7c7a2-507">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7c7a2-508">NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-508">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7c7a2-509">預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-509">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="7c7a2-510">假設適當的驗證和授權，IIS01 接受 hello 要求和回應</span><span class="sxs-lookup"><span data-stu-id="7c7a2-510">Assuming proper authentication and authorization, IIS01 accepts hello request and responds</span></span>
7. <span data-ttu-id="7c7a2-511">Frontend 子網路上的 hello UDR 路由可讓 hello 防火牆 hello 下一個躍點</span><span class="sxs-lookup"><span data-stu-id="7c7a2-511">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
8. <span data-ttu-id="7c7a2-512">由於有允許前端子網路 hello 回應 hello 上的沒有輸出 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-512">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
9. <span data-ttu-id="7c7a2-513">因為這是現有的工作階段上 hello 防火牆允許此回應與 hello 防火牆傳回 hello 回應 tooAppVM02</span><span class="sxs-lookup"><span data-stu-id="7c7a2-513">As this is an existing session on hello firewall this response is allowed and hello firewall returns hello response tooAppVM02</span></span>
10. <span data-ttu-id="7c7a2-514">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7c7a2-515">NSG 規則 1 （封鎖網際網路） 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-515">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7c7a2-516">預設 NSG 規則允許 toosubnet 子網路的流量，允許流量，停止處理 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-516">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="7c7a2-517">AppVM02 收到 hello 回應</span><span class="sxs-lookup"><span data-stu-id="7c7a2-517">AppVM02 receives hello response</span></span>

#### <a name="denied-internet-direct-tooweb-server"></a><span data-ttu-id="7c7a2-518">（拒絕）網際網路直接 tooWeb 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c7a2-518">(Denied) Internet direct tooWeb Server</span></span>
1. <span data-ttu-id="7c7a2-519">網際網路的使用者嘗試 tooaccess hello web 伺服器，IIS01，透過 hello FrontEnd001.CloudApp.Net 服務</span><span class="sxs-lookup"><span data-stu-id="7c7a2-519">Internet user tries tooaccess hello web server, IIS01, through hello FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="7c7a2-520">因為沒有開啟以供 HTTP 流量的端點，這就不會通過 hello 雲端服務，並不會連線到 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c7a2-520">Since there are no endpoints open for HTTP traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="7c7a2-521">如果基於某些原因，hello 端點處於開啟狀態，在 hello Frontend 子網路上的 hello NSG （區塊網際網路） 會封鎖此流量</span><span class="sxs-lookup"><span data-stu-id="7c7a2-521">If hello endpoints were open for some reason, hello NSG (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="7c7a2-522">最後，hello 前端子網路 UDR 路由傳送會從 IIS01 toohello 防火牆 hello 下一個躍點，為傳送任何輸出流量，而且 hello 防火牆會認為這是對稱的流量，卸除 hello 輸出回應因此會有至少三個獨立層的防禦之間 hello 網際網路和 IIS01 透過防止未經授權的/不適當的存取其雲端服務。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-522">Finally, hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toobackend-server"></a><span data-ttu-id="7c7a2-523">（拒絕）網際網路 tooBackend 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c7a2-523">(Denied) Internet tooBackend Server</span></span>
1. <span data-ttu-id="7c7a2-524">網際網路的使用者嘗試 tooaccess AppVM01 上的檔案，即可透過 hello BackEnd001.CloudApp.Net 服務</span><span class="sxs-lookup"><span data-stu-id="7c7a2-524">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="7c7a2-525">因為不有開啟的檔案共用的任何端點，這不會傳送 hello 雲端服務，並不會連線到 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c7a2-525">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="7c7a2-526">如果基於某些原因，hello 端點處於開啟狀態，hello NSG （區塊網際網路） 會封鎖此流量</span><span class="sxs-lookup"><span data-stu-id="7c7a2-526">If hello endpoints were open for some reason, hello NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="7c7a2-527">最後，hello UDR 路由就會從 AppVM01 toohello 防火牆 hello 下一個躍點，為傳送任何輸出流量，而且 hello 防火牆會認為這是對稱的流量，卸除 hello 輸出回應因此有防禦機制以之間至少三個獨立的圖層hello 網際網路和 AppVM01，透過其雲端服務，防止未經授權的/不適當的存取。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-527">Finally, hello UDR route would send any outbound traffic from AppVM01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-toobackend-server"></a><span data-ttu-id="7c7a2-528">（拒絕）前端伺服器 tooBackend 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c7a2-528">(Denied) Frontend server tooBackend Server</span></span>
1. <span data-ttu-id="7c7a2-529">假設 IIS01 已遭到洩露，而且正在嘗試伺服器 tooscan hello 後端子網路的惡意程式碼。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-529">Assume IIS01 was compromised and is running malicious code trying tooscan hello Backend subnet servers.</span></span>
2. <span data-ttu-id="7c7a2-530">hello 前端子網路 UDR 路由傳送會傳送任何輸出流量從 IIS01 toohello 防火牆為 hello 下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-530">hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop.</span></span> <span data-ttu-id="7c7a2-531">這不是可改變的 hello 危害 VM。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-531">This is not something that can be altered by hello compromised VM.</span></span>
3. <span data-ttu-id="7c7a2-532">如果 hello 要求 tooAppVM01 或可能無法 hello （因為 tooFW 規則 7 和 9） 的防火牆允許流量的 DNS 查閱 toohello DNS 伺服器 hello 防火牆會處理 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-532">hello firewall would process hello traffic, if hello request was tooAppVM01, or toohello DNS server for DNS lookups that traffic could potentially be allowed by hello firewall (due tooFW Rules 7 and 9).</span></span> <span data-ttu-id="7c7a2-533">所有其他流量則會遭 FW 規則 11 (全部拒絕) 封鎖。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="7c7a2-534">進階威脅偵測是否已啟用 hello 防火牆 （其未涵蓋在本文件中，請參閱進階威脅功能您特定的網路應用裝置 hello 廠商文件），甚至會允許 hello 基本轉送規則的流量在這個討論如果 hello 流量包含已知的簽章或進階的威脅規則的旗標的模式，就無法防止文件。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-534">If advanced threat detection was enabled on hello firewall (which is not covered in this document, see hello vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by hello basic forwarding rules discussed in this document could be prevented if hello traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="7c7a2-535">(拒絕) DNS 伺服器上的網際網路 DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="7c7a2-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="7c7a2-536">網際網路的使用者嘗試 toolookup DNS01 內部 DNS 記錄透過 BackEnd001.CloudApp.Net 服務</span><span class="sxs-lookup"><span data-stu-id="7c7a2-536">Internet user tries toolookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="7c7a2-537">因為沒有開啟以供 DNS 流量的端點，這就不會通過 hello 雲端服務，並不會連線到 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c7a2-537">Since there are no endpoints open for DNS traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="7c7a2-538">如果基於某些原因，hello 端點處於開啟狀態，hello Frontend 子網路上的 hello NSG 規則 （區塊網際網路） 會封鎖此流量</span><span class="sxs-lookup"><span data-stu-id="7c7a2-538">If hello endpoints were open for some reason, hello NSG rule (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="7c7a2-539">最後，hello 後端子網路 UDR 路由傳送會從 DNS01 toohello 防火牆 hello 下一個躍點，為傳送任何輸出流量，而且 hello 防火牆會認為這是對稱的流量，卸除輸出回應因此會有至少三個獨立層的 hello防禦之間 hello 網際網路和 DNS01 透過防止未經授權的/不適當的存取其雲端服務。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-539">Finally, hello Backend subnet UDR route would send any outbound traffic from DNS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toosql-access-through-firewall"></a><span data-ttu-id="7c7a2-540">（拒絕）透過防火牆存取網際網路 tooSQL</span><span class="sxs-lookup"><span data-stu-id="7c7a2-540">(Denied) Internet tooSQL access through Firewall</span></span>
1. <span data-ttu-id="7c7a2-541">網際網路使用者從 SecSvc001.CloudApp.Net (網際網路面向雲端服務) 要求 SQL 資料</span><span class="sxs-lookup"><span data-stu-id="7c7a2-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="7c7a2-542">因為沒有開啟以供 SQL 的端點，這不會傳送 hello 雲端服務，並不會到達 hello 防火牆</span><span class="sxs-lookup"><span data-stu-id="7c7a2-542">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="7c7a2-543">如果基於某些原因，SQL 端點處於開啟狀態，hello 防火牆就會開始處理規則：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-543">If SQL endpoints were open for some reason, hello firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="7c7a2-544">FW 規則 1 (FW Mgmt) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-544">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7c7a2-545">FW 規則 2-5 （RDP 規則） 不套用，請移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7c7a2-546">不適用 FW 規則 6 和 7 （應用程式的規則），移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-546">FW Rule 6 & 7 (Application Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="7c7a2-547">FW 規則 8 (tooInternet) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-547">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="7c7a2-548">不會套用 FW 規則 9 (DNS)，移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-548">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="7c7a2-549">不會套用 FW 規則 10 （內部子網路），移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move toonext rule</span></span>
   7. <span data-ttu-id="7c7a2-550">FW 規則 11 (全部拒絕) 適用，封鎖流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="7c7a2-551">參考</span><span class="sxs-lookup"><span data-stu-id="7c7a2-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="7c7a2-552">主要的指令碼和網路組態</span><span class="sxs-lookup"><span data-stu-id="7c7a2-552">Main Script and Network Config</span></span>
<span data-ttu-id="7c7a2-553">在 PowerShell 指令碼檔案中儲存 hello 完整的指令碼。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-553">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="7c7a2-554">將儲存到檔案中名為"NetworkConf2.xml"hello 網路組態。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-554">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="7c7a2-555">視需要修改 hello 使用者定義的變數。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-555">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="7c7a2-556">執行 hello 指令碼，然後遵循 hello 防火牆規則設定指示上述。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-556">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="7c7a2-557">完整指令碼</span><span class="sxs-lookup"><span data-stu-id="7c7a2-557">Full Script</span></span>
<span data-ttu-id="7c7a2-558">此指令碼，會根據 hello 使用者定義的變數：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-558">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="7c7a2-559">連接 tooan Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7c7a2-559">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="7c7a2-560">建立新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7c7a2-560">Create a new storage account</span></span>
3. <span data-ttu-id="7c7a2-561">建立新的 VNet 和 hello 網路組態檔中所定義的三個子網路</span><span class="sxs-lookup"><span data-stu-id="7c7a2-561">Create a new VNet and three subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="7c7a2-562">建置五部虛擬機器：1 個防火牆和 4 個 Windows Server VM</span><span class="sxs-lookup"><span data-stu-id="7c7a2-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="7c7a2-563">設定 UDR，包括：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="7c7a2-564">建立兩個新的路由表</span><span class="sxs-lookup"><span data-stu-id="7c7a2-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="7c7a2-565">新增路由 toohello 資料表</span><span class="sxs-lookup"><span data-stu-id="7c7a2-565">Add routes toohello tables</span></span>
   3. <span data-ttu-id="7c7a2-566">繫結資料表 tooappropriate 子網路</span><span class="sxs-lookup"><span data-stu-id="7c7a2-566">Bind tables tooappropriate subnets</span></span>
6. <span data-ttu-id="7c7a2-567">啟用 hello NVA 中的 IP 轉送</span><span class="sxs-lookup"><span data-stu-id="7c7a2-567">Enable IP Forwarding on hello NVA</span></span>
7. <span data-ttu-id="7c7a2-568">設定 NSG，包括：</span><span class="sxs-lookup"><span data-stu-id="7c7a2-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="7c7a2-569">建立 NSG</span><span class="sxs-lookup"><span data-stu-id="7c7a2-569">Creating a NSG</span></span>
   2. <span data-ttu-id="7c7a2-570">新增規則</span><span class="sxs-lookup"><span data-stu-id="7c7a2-570">Adding a rule</span></span>
   3. <span data-ttu-id="7c7a2-571">繫結 hello NSG toohello 適當的子網路</span><span class="sxs-lookup"><span data-stu-id="7c7a2-571">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="7c7a2-572">此 PowerShell 指令碼應該在連線到網際網路的電腦或伺服器上本機執行。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c7a2-573">此指令碼在執行時，PowerShell 中可能會跳出警告或其他參考訊息。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="7c7a2-574">只有紅色字體的錯誤訊息才需要擔心。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-574">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

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

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
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

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="7c7a2-575">網路組態檔</span><span class="sxs-lookup"><span data-stu-id="7c7a2-575">Network Config File</span></span>
<span data-ttu-id="7c7a2-576">儲存此 xml 檔，以更新的位置，並新增 hello 連結 toothis 檔案 toohello $NetworkConfigFile 變數上述 hello 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="7c7a2-576">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
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

#### <a name="sample-application-scripts"></a><span data-ttu-id="7c7a2-577">範例應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="7c7a2-577">Sample Application Scripts</span></span>
<span data-ttu-id="7c7a2-578">如果您想 tooinstall 範例應用程式，和其他周邊網路的範例，其中一個已提供在 hello 下列連結：[範例應用程式指令碼][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="7c7a2-578">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "具有 NVA、NSG 和 UDR 的雙向 DMZ"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Hello 防火牆規則的邏輯檢視"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "建立前端網路物件"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "建立 DNS 伺服器物件"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "預設 RDP 規則的複本"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 規則"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "應用程式重新導向圖示"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "目的地 NAT 圖示"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "傳遞圖示"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "防火牆管理規則"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "防火牆 RDP 規則"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "防火牆 Web 規則"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "防火牆 AppVM01 規則"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "防火牆輸出規則"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "防火牆 DNS 規則"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "防火牆內部 VNet 規則"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "防火牆拒絕規則"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "防火牆規則啟用"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
