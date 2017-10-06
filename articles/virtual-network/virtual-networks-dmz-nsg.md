---
title: "aaaAzure DMZ 範例 – 建立簡單的周邊網路與 Nsg |Microsoft 文件"
description: "建置具有網路安全性群組 (NSG) 的 DMZ"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="63734-103">範例 1 – 使用 NSG 搭配 Azure Resource Manager 範本建立簡單的 DMZ</span><span class="sxs-lookup"><span data-stu-id="63734-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="63734-104">[傳回 toohello 安全性界限最佳作法頁面][HOME]</span><span class="sxs-lookup"><span data-stu-id="63734-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="63734-105">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="63734-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="63734-106">傳統 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="63734-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="63734-107">此範例會建立包含四個 Windows 伺服器和網路安全性群組的基本 DMZ。</span><span class="sxs-lookup"><span data-stu-id="63734-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="63734-108">這個範例會說明每個 hello 相關的範本區段 tooprovide 更深入的了解每個步驟。</span><span class="sxs-lookup"><span data-stu-id="63734-108">This example describes each of hello relevant template sections tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="63734-109">另外還有流量案例 > 一節 tooprovide 逐步深入流量就會繼續進行的 hello 周邊網路中的 hello 保護層。</span><span class="sxs-lookup"><span data-stu-id="63734-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step look at how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="63734-110">最後，在 hello references 區段中是 hello 完成範本的程式碼和指示 toobuild 此環境 tootest 和試驗各種案例。</span><span class="sxs-lookup"><span data-stu-id="63734-110">Finally, in hello references section is hello complete template code and instructions toobuild this environment tootest and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="63734-111">![具有 NSG 的輸入 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="63734-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="63734-112">環境描述</span><span class="sxs-lookup"><span data-stu-id="63734-112">Environment description</span></span>
<span data-ttu-id="63734-113">在此範例中的訂用帳戶包含 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="63734-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="63734-114">單一資源群組</span><span class="sxs-lookup"><span data-stu-id="63734-114">A single resource group</span></span>
* <span data-ttu-id="63734-115">含有兩個子網路的虛擬網路；“FrontEnd” 和 “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="63734-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="63734-116">已套用的 tooboth 子網路的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="63734-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="63734-117">一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)</span><span class="sxs-lookup"><span data-stu-id="63734-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="63734-118">兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="63734-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="63734-119">一個代表 DNS 伺服器的 Windows Server ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="63734-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="63734-120">Hello 應用程式 web 伺服器相關聯的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="63734-120">A public IP address associated with hello application web server</span></span>

<span data-ttu-id="63734-121">在 hello 參考區段中，沒有連結 tooan Azure Resource Manager 範本建置這個範例中所述的 hello 環境。</span><span class="sxs-lookup"><span data-stu-id="63734-121">In hello references section, there is a link tooan Azure Resource Manager template that builds hello environment described in this example.</span></span> <span data-ttu-id="63734-122">建置 hello Vm 和虛擬網路，由 hello 範例範本，雖然不詳述於本文件說明。</span><span class="sxs-lookup"><span data-stu-id="63734-122">Building hello VMs and Virtual Networks, although done by hello example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="63734-123">**toobuild 此環境**（詳細的指示是在 hello 的這份文件的 references 區段中;）</span><span class="sxs-lookup"><span data-stu-id="63734-123">**toobuild this environment** (detailed instructions are in hello references section of this document);</span></span>

1. <span data-ttu-id="63734-124">部署 hello Azure 資源管理員範本： [Azure 快速入門範本][Template]</span><span class="sxs-lookup"><span data-stu-id="63734-124">Deploy hello Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="63734-125">安裝在 hello 範例應用程式：[範例應用程式指令碼][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="63734-125">Install hello sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="63734-126">在此情況下，hello IIS 伺服器 tooRDP tooany 後端伺服器作為 「 跳躍方塊 」。</span><span class="sxs-lookup"><span data-stu-id="63734-126">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="63734-127">第一部 RDP toohello IIS 伺服器，然後從 hello IIS 伺服器的 RDP toohello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="63734-127">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span> <span data-ttu-id="63734-128">或者，可以將公用 IP 與每個伺服器 NIC 相關聯以便更容易 RDP。</span><span class="sxs-lookup"><span data-stu-id="63734-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="63734-129">hello 下列各節提供 hello 網路安全性群組和其運作方式如這個範例藉由查核透過金鑰行 hello Azure Resource Manager 範本的詳細的描述。</span><span class="sxs-lookup"><span data-stu-id="63734-129">hello following sections provide a detailed description of hello Network Security Group and how it functions for this example by walking through key lines of hello Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="63734-130">網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="63734-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="63734-131">此範例會組建 NSG 群組，然後載入六個規則。</span><span class="sxs-lookup"><span data-stu-id="63734-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="63734-132">一般而言，您應該先建立特定的 「 允許 」 規則，然後上次 hello 一般 「 拒絕 」 規則。</span><span class="sxs-lookup"><span data-stu-id="63734-132">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="63734-133">指派優先順序的 hello 規定哪些規則會先評估。</span><span class="sxs-lookup"><span data-stu-id="63734-133">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="63734-134">一旦流量找到 tooapply tooa 特定規則，則會不評估任何進一步的規則。</span><span class="sxs-lookup"><span data-stu-id="63734-134">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="63734-135">NSG 規則可套用在 hello 中輸入或輸出方向 （從 hello 觀點 hello 子網路）。</span><span class="sxs-lookup"><span data-stu-id="63734-135">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
>
>

<span data-ttu-id="63734-136">以宣告方式，下列規則的 hello 正在建置輸入流量：</span><span class="sxs-lookup"><span data-stu-id="63734-136">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="63734-137">允許內部 DNS 流量 (連接埠 53)</span><span class="sxs-lookup"><span data-stu-id="63734-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="63734-138">允許從 hello 網際網路 tooany VM 的 RDP 流量 （連接埠 3389）</span><span class="sxs-lookup"><span data-stu-id="63734-138">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="63734-139">允許從 hello 網際網路 tooweb 伺服器 (IIS01) 的 HTTP 流量 （連接埠 80）</span><span class="sxs-lookup"><span data-stu-id="63734-139">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="63734-140">允許從 IIS01 tooAppVM1 任何流量 （所有連接埠）</span><span class="sxs-lookup"><span data-stu-id="63734-140">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="63734-141">任何流量 （所有連接埠），從 hello 網際網路 toohello 拒絕整個 VNet （這兩個子網路）</span><span class="sxs-lookup"><span data-stu-id="63734-141">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="63734-142">拒絕任何從 hello Frontend 子網路 toohello 後端子網路的流量 （所有連接埠）</span><span class="sxs-lookup"><span data-stu-id="63734-142">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="63734-143">與這些規則繫結的 tooeach 子網路中，輸入 hello Internet toohello 網頁伺服器從 HTTP 要求是否兩者的規則 3 （允許） 及 5 （拒絕） 將會套用，但由於規則 3 具有較高的優先順序，只將套用的規則 5 就不會發生。</span><span class="sxs-lookup"><span data-stu-id="63734-143">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="63734-144">因此 hello HTTP 要求會允許 toohello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="63734-144">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="63734-145">如果該相同流量已嘗試 tooreach hello DNS01 伺服器，hello 第一個 tooapply 和 hello 流量就不會允許 toopass toohello 伺服器是規則 5 （拒絕）。</span><span class="sxs-lookup"><span data-stu-id="63734-145">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="63734-146">規則 6 (Deny) 會封鎖從交談 toohello 後端的子網路 （除了規則 1 和 4 中允許的流量） hello Frontend 子網路中，如果攻擊者竊取 hello web 上的應用程式 hello 前端，hello 攻擊者就此規則集可保護 hello 後端 」 網路有限存取 toohello 後端 「 受保護 」 (只公開 hello AppVM01 伺服器上的 tooresources) 網路。</span><span class="sxs-lookup"><span data-stu-id="63734-146">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="63734-147">沒有預設輸出的規則，可讓流量輸出 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="63734-147">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="63734-148">在此範例中，我們會允許輸出流量，並不會修改任何輸出規則。</span><span class="sxs-lookup"><span data-stu-id="63734-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="63734-149">tooapply 安全性原則 tootraffic 雙向，使用者定義路由是必要項，會在 「 範例 3 」 探索上 hello[安全性界限最佳作法頁面][HOME]。</span><span class="sxs-lookup"><span data-stu-id="63734-149">tooapply security policy tootraffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="63734-150">會詳細討論每個規則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="63734-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="63734-151">網路安全性群組資源必須是具現化的 toohold hello 規則：</span><span class="sxs-lookup"><span data-stu-id="63734-151">A Network Security Group resource must be instantiated toohold hello rules:</span></span>

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. <span data-ttu-id="63734-152">在此範例中的 hello 第一個規則可讓 DNS hello 後端子網路上所有的內部網路 toohello DNS 伺服器之間的流量。</span><span class="sxs-lookup"><span data-stu-id="63734-152">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="63734-153">hello 規則有一些重要的參數：</span><span class="sxs-lookup"><span data-stu-id="63734-153">hello rule has some important parameters:</span></span>
  * <span data-ttu-id="63734-154">「 destinationAddressPrefix"-規則可以使用稱為 「 預設標記 」 的位址首碼的特殊類型，這些標記是允許輕鬆 tooaddress 的位址前置詞的較大類別目錄的系統提供的識別項。</span><span class="sxs-lookup"><span data-stu-id="63734-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way tooaddress a larger category of address prefixes.</span></span> <span data-ttu-id="63734-155">此規則會使用 hello 預設標記 「 網際網路 」 toosignify 任何 hello VNet 外部位址。</span><span class="sxs-lookup"><span data-stu-id="63734-155">This rule uses hello Default Tag “Internet” toosignify any address outside of hello VNet.</span></span> <span data-ttu-id="63734-156">其他前置詞標籤為 VirtualNetwork 和 AzureLoadBalancer。</span><span class="sxs-lookup"><span data-stu-id="63734-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="63734-157">「方向」表示此規則會生效的傳輸流量方向。</span><span class="sxs-lookup"><span data-stu-id="63734-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="63734-158">hello 方向是從 hello 的觀點來看 hello 子網路或虛擬機器 （取決於位置會繫結此 NSG）。</span><span class="sxs-lookup"><span data-stu-id="63734-158">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="63734-159">因此如果方向是 「 輸入 」 流量輸入 hello 子網路、 hello 規則將會套用，且離開 hello 子網路的流量不會受到此規則。</span><span class="sxs-lookup"><span data-stu-id="63734-159">Thus if Direction is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="63734-160">"Priority"設定 hello 順序評估流量。</span><span class="sxs-lookup"><span data-stu-id="63734-160">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="63734-161">hello hello 數字 hello 高 hello 優先順序。</span><span class="sxs-lookup"><span data-stu-id="63734-161">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="63734-162">當規則適用於特定 tooa 流量時，則會不處理任何進一步的規則。</span><span class="sxs-lookup"><span data-stu-id="63734-162">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="63734-163">因此如果優先權 1 的規則允許流量，和優先順序為 2 的規則，拒絕的流量，而且這兩個規則套用 tootraffic 則 hello 流量 someserver.mycompany.com tooflow （因為規則 1 有更高的優先順序花費效果，並套用任何進一步的規則）。</span><span class="sxs-lookup"><span data-stu-id="63734-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="63734-164">“Access” 指出受此規則影響的流量是要封鎖 ("Deny") 或允許 ("Allow")。</span><span class="sxs-lookup"><span data-stu-id="63734-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. <span data-ttu-id="63734-165">此規則可讓您從 hello 網際網路 toohello RDP 連接埠上 hello 的任何伺服器上的 RDP 流量 tooflow 繫結的子網路。</span><span class="sxs-lookup"><span data-stu-id="63734-165">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. <span data-ttu-id="63734-166">這個規則允許輸入的網際網路流量 toohit hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="63734-166">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="63734-167">此規則不會變更 hello 路由行為。</span><span class="sxs-lookup"><span data-stu-id="63734-167">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="63734-168">hello 規則僅允許針對 IIS01 toopass 的流量。</span><span class="sxs-lookup"><span data-stu-id="63734-168">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="63734-169">因此從 hello 網際網路的流量是否有 hello web 伺服器，做為其目的地，此規則會允許它，並停止進一步處理規則。</span><span class="sxs-lookup"><span data-stu-id="63734-169">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="63734-170">（在 hello 規則優先順序 140 所有其他傳入的網際網路流量會封鎖）。</span><span class="sxs-lookup"><span data-stu-id="63734-170">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="63734-171">如果您只在處理 HTTP 流量，這項規則可以更進一步地限制的 tooonly 允許目的地連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="63734-171">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. <span data-ttu-id="63734-172">此規則可讓從 hello IIS01 伺服器流量 toopass toohello AppVM01 伺服器，更新規則封鎖所有其他前端 tooBackend 流量。</span><span class="sxs-lookup"><span data-stu-id="63734-172">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="63734-173">應加入這項規則，如果 hello 連接埠已知的 tooimprove。</span><span class="sxs-lookup"><span data-stu-id="63734-173">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="63734-174">例如，如果 hello IIS 伺服器已達到只有 SQL Server 上 AppVM01，hello 目的地連接埠範圍應該變更"*"（任何） too1433 (hello SQL 連接埠) 進而較小的輸入的攻擊介面上 AppVM01 應該 hello web 應用程式不會受到危害。</span><span class="sxs-lookup"><span data-stu-id="63734-174">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. <span data-ttu-id="63734-175">此規則會拒絕 hello 網際網路 tooany 網路上的伺服器 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="63734-175">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="63734-176">Hello 規則優先順序 110 和 120 hello 效果為 tooallow 只有輸入的網際網路流量 toohello 防火牆和伺服器上的 RDP 連接埠而封鎖所有其他項目。</span><span class="sxs-lookup"><span data-stu-id="63734-176">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="63734-177">此規則是 「 保險 」 規則 tooblock 未預期的所有流程。</span><span class="sxs-lookup"><span data-stu-id="63734-177">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. <span data-ttu-id="63734-178">hello 最終規則，拒絕來自 hello Frontend 子網路 toohello 後端子網路流量。</span><span class="sxs-lookup"><span data-stu-id="63734-178">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="63734-179">由於這個規則唯一的輸入的規則，（從後端 toohello 前端 hello) 允許反向的流量。</span><span class="sxs-lookup"><span data-stu-id="63734-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="63734-180">流量案例</span><span class="sxs-lookup"><span data-stu-id="63734-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="63734-181">(*允許*) 網際網路 tooweb 伺服器</span><span class="sxs-lookup"><span data-stu-id="63734-181">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="63734-182">網際網路使用者要求 HTTP 頁面從 hello 與 hello IIS01 NIC 的 NIC 相關聯的 hello 公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="63734-182">An internet user requests an HTTP page from hello public IP address of hello NIC associated with hello IIS01 NIC</span></span>
2. <span data-ttu-id="63734-183">hello 公用 IP 位址傳送流量 toohello 朝向 IIS01 VNet （hello web 伺服器）</span><span class="sxs-lookup"><span data-stu-id="63734-183">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="63734-184">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="63734-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="63734-185">NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="63734-185">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="63734-186">NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="63734-186">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="63734-187">NSG 規則 3 (網際網路 tooIIS01) 會套用，流量會允許中停止的規則處理</span><span class="sxs-lookup"><span data-stu-id="63734-187">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="63734-188">流量叫用內部 IP 位址的 hello web 伺服器 IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="63734-188">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="63734-189">IIS01 接聽 web 流量、 收到此要求，並開始處理 hello 要求</span><span class="sxs-lookup"><span data-stu-id="63734-189">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="63734-190">IIS01 詢問 hello SQL Server 上 AppVM01 資訊</span><span class="sxs-lookup"><span data-stu-id="63734-190">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="63734-191">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="63734-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="63734-192">hello 後端子網路會開始處理輸入的規則：</span><span class="sxs-lookup"><span data-stu-id="63734-192">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="63734-193">NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="63734-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="63734-194">NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="63734-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="63734-195">NSG 規則 3 (網際網路 tooFirewall) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="63734-195">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="63734-196">NSG 規則 4 (IIS01 tooAppVM01) 會套用，流量會允許中停止的規則處理</span><span class="sxs-lookup"><span data-stu-id="63734-196">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="63734-197">AppVM01 收到 hello SQL 查詢並予以回應</span><span class="sxs-lookup"><span data-stu-id="63734-197">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="63734-198">由於 hello 後端子網路上有沒有輸出的規則，允許 hello 回應</span><span class="sxs-lookup"><span data-stu-id="63734-198">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="63734-199">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="63734-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="63734-200">套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="63734-200">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="63734-201">hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="63734-201">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="63734-202">hello IIS 伺服器收到 hello SQL 回應，並完成 hello HTTP 回應，並將傳送 toohello 要求者</span><span class="sxs-lookup"><span data-stu-id="63734-202">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requester</span></span>
13. <span data-ttu-id="63734-203">由於沒有 hello Frontend 子網路上的輸出規則，允許 hello 回應而 hello 網際網路使用者會收到要求的 hello 網頁。</span><span class="sxs-lookup"><span data-stu-id="63734-203">Since there are no outbound rules on hello Frontend subnet, hello response is allowed and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-tooiis-server"></a><span data-ttu-id="63734-204">(*允許*) RDP tooIIS 伺服器</span><span class="sxs-lookup"><span data-stu-id="63734-204">(*Allowed*) RDP tooIIS server</span></span>
1. <span data-ttu-id="63734-205">網際網路上的伺服器系統管理員要求在 hello 與 hello （透過入口網站或 PowerShell hello 可以找到這個公用 IP 位址） IIS01 NIC 的 NIC 相關聯的 hello 公用 IP 位址上的 RDP 工作階段 tooIIS01</span><span class="sxs-lookup"><span data-stu-id="63734-205">A Server Admin on internet requests an RDP session tooIIS01 on hello public IP address of hello NIC associated with hello IIS01 NIC (this public IP address can be found via hello Portal or PowerShell)</span></span>
2. <span data-ttu-id="63734-206">hello 公用 IP 位址傳送流量 toohello 朝向 IIS01 VNet （hello web 伺服器）</span><span class="sxs-lookup"><span data-stu-id="63734-206">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="63734-207">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="63734-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="63734-208">NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="63734-208">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="63734-209">NSG 規則 2 (RDP) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="63734-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="63734-210">由於沒有輸出規則，會套用預設規則並允許傳回的流量</span><span class="sxs-lookup"><span data-stu-id="63734-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="63734-211">已啟用 RDP 工作階段</span><span class="sxs-lookup"><span data-stu-id="63734-211">RDP session is enabled</span></span>
6. <span data-ttu-id="63734-212">IIS01 會提示您輸入 hello 使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="63734-212">IIS01 prompts for hello user name and password</span></span>

>[!NOTE]
><span data-ttu-id="63734-213">在此情況下，hello IIS 伺服器 tooRDP tooany 後端伺服器作為 「 跳躍方塊 」。</span><span class="sxs-lookup"><span data-stu-id="63734-213">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="63734-214">第一部 RDP toohello IIS 伺服器，然後從 hello IIS 伺服器的 RDP toohello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="63734-214">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="63734-215">(允許) DNS 伺服器上的 Web 伺服器 DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="63734-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="63734-216">Web 伺服器，IIS01，需要的資料摘要在 www.data.gov，但需要 tooresolve hello 位址。</span><span class="sxs-lookup"><span data-stu-id="63734-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="63734-217">hello 的網路組態 hello VNet 清單 DNS01 (10.0.2.4 hello 後端子網路上) 做為主要 DNS 伺服器 hello，IIS01 傳送 hello DNS 要求 tooDNS01</span><span class="sxs-lookup"><span data-stu-id="63734-217">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="63734-218">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="63734-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="63734-219">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="63734-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="63734-220">NSG 規則 1 (DNS) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="63734-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="63734-221">DNS 伺服器收到 hello 要求</span><span class="sxs-lookup"><span data-stu-id="63734-221">DNS server receives hello request</span></span>
6. <span data-ttu-id="63734-222">DNS 伺服器沒有快取的 hello 位址和要求的根 DNS 伺服器上 hello 網際網路</span><span class="sxs-lookup"><span data-stu-id="63734-222">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="63734-223">Backend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="63734-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="63734-224">網際網路 DNS 伺服器回應，因為此工作階段已在內部起始，hello 允許回應</span><span class="sxs-lookup"><span data-stu-id="63734-224">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="63734-225">DNS 伺服器快取 hello 回應及回應 toohello 初始要求後 tooIIS01</span><span class="sxs-lookup"><span data-stu-id="63734-225">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="63734-226">Backend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="63734-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="63734-227">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="63734-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="63734-228">套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="63734-228">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="63734-229">hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量</span><span class="sxs-lookup"><span data-stu-id="63734-229">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="63734-230">IIS01 DNS01 收到 hello 回應</span><span class="sxs-lookup"><span data-stu-id="63734-230">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="63734-231">(允許) Web 伺服器存取 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="63734-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="63734-232">IIS01 要求 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="63734-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="63734-233">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="63734-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="63734-234">hello 後端子網路會開始處理輸入的規則：</span><span class="sxs-lookup"><span data-stu-id="63734-234">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="63734-235">NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="63734-235">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="63734-236">NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="63734-236">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="63734-237">NSG 規則 3 (網際網路 tooIIS01) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="63734-237">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="63734-238">NSG 規則 4 (IIS01 tooAppVM01) 會套用，流量會允許中停止的規則處理</span><span class="sxs-lookup"><span data-stu-id="63734-238">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="63734-239">AppVM01 收到 hello 要求和回應檔案 （假設已獲授權存取）</span><span class="sxs-lookup"><span data-stu-id="63734-239">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="63734-240">由於 hello 後端子網路上有沒有輸出的規則，允許 hello 回應</span><span class="sxs-lookup"><span data-stu-id="63734-240">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="63734-241">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="63734-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="63734-242">套用 tooInbound 流量 hello 後端子網路 toohello Frontend 子網路，因此沒有任何 hello NSG 規則適用於沒有 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="63734-242">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="63734-243">hello 允許子網路之間流量的預設系統規則會允許這個流量，因此允許 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="63734-243">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="63734-244">hello IIS 伺服器收到 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="63734-244">hello IIS server receives hello file</span></span>

#### <a name="denied-rdp-toobackend"></a><span data-ttu-id="63734-245">(*拒絕*) RDP toobackend</span><span class="sxs-lookup"><span data-stu-id="63734-245">(*Denied*) RDP toobackend</span></span>
1. <span data-ttu-id="63734-246">網際網路使用者嘗試 tooRDP tooserver AppVM01</span><span class="sxs-lookup"><span data-stu-id="63734-246">An internet user tries tooRDP tooserver AppVM01</span></span>
2. <span data-ttu-id="63734-247">因為沒有與此伺服器的 NIC 相關聯的公用 IP 位址，此流量會永遠不會輸入 hello VNet，並不會連線到 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="63734-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="63734-248">不過，如果因為某些原因已啟用公用 IP 位址，NSG 規則 2 (RDP) 會允許此流量</span><span class="sxs-lookup"><span data-stu-id="63734-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="63734-249">在此情況下，hello IIS 伺服器 tooRDP tooany 後端伺服器作為 「 跳躍方塊 」。</span><span class="sxs-lookup"><span data-stu-id="63734-249">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="63734-250">第一部 RDP toohello IIS 伺服器，然後從 hello IIS 伺服器的 RDP toohello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="63734-250">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="63734-251">(*拒絕*) Web toobackend 伺服器</span><span class="sxs-lookup"><span data-stu-id="63734-251">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="63734-252">網際網路使用者嘗試 tooaccess AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="63734-252">An internet user tries tooaccess a file on AppVM01</span></span>
2. <span data-ttu-id="63734-253">因為沒有與此伺服器的 NIC 相關聯的公用 IP 位址，此流量會永遠不會輸入 hello VNet，並不會連線到 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="63734-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="63734-254">如果基於某些原因，已啟用的公用 IP 位址，NSG 規則 5 (網際網路 tooVNet) 會封鎖此流量</span><span class="sxs-lookup"><span data-stu-id="63734-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="63734-255">(拒絕) DNS 伺服器上的 Web DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="63734-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="63734-256">網際網路使用者嘗試 toolook 上 DNS01 內部 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="63734-256">An internet user tries toolook up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="63734-257">因為沒有與此伺服器的 NIC 相關聯的公用 IP 位址，此流量會永遠不會輸入 hello VNet，並不會連線到 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="63734-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="63734-258">如果基於某些原因，已啟用的公用 IP 位址，NSG 規則 5 (網際網路 tooVNet) 會封鎖此流量 (注意： 因為 hello 要求來源位址不會套用規則 1 」 (DNS) 是 hello 網際網路和規則 1 僅適用於 toohello hello 來源為區域 VNet)</span><span class="sxs-lookup"><span data-stu-id="63734-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because hello requests source address is hello internet and Rule 1 only applies toohello local VNet as hello source)</span></span>

#### <a name="denied-sql-access-on-hello-web-server"></a><span data-ttu-id="63734-259">(*拒絕*) hello web 伺服器上的 SQL 存取</span><span class="sxs-lookup"><span data-stu-id="63734-259">(*Denied*) SQL access on hello web server</span></span>
1. <span data-ttu-id="63734-260">網際網路使用者向 IIS01 要求 SQL 資料</span><span class="sxs-lookup"><span data-stu-id="63734-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="63734-261">因為沒有與此伺服器的 NIC 相關聯的公用 IP 位址，此流量會永遠不會輸入 hello VNet，並不會連線到 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="63734-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="63734-262">如果基於某些原因，已啟用的公用 IP 位址，hello Frontend 子網路會開始處理輸入的規則：</span><span class="sxs-lookup"><span data-stu-id="63734-262">If a Public IP address was enabled for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="63734-263">NSG 規則 1 」 (DNS) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="63734-263">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="63734-264">NSG 規則 2 」 (RDP) 不會套用移動 toonext 規則</span><span class="sxs-lookup"><span data-stu-id="63734-264">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="63734-265">NSG 規則 3 (網際網路 tooIIS01) 會套用，流量會允許中停止的規則處理</span><span class="sxs-lookup"><span data-stu-id="63734-265">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="63734-266">流量叫用內部 IP 位址的 hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="63734-266">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="63734-267">IIS01 未接聽通訊埠 1433，因此沒有回應 toohello 要求</span><span class="sxs-lookup"><span data-stu-id="63734-267">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="63734-268">結論</span><span class="sxs-lookup"><span data-stu-id="63734-268">Conclusion</span></span>
<span data-ttu-id="63734-269">這個範例是相當簡單且直接正向的方式，隔離 hello 後端的輸入流量子網路。</span><span class="sxs-lookup"><span data-stu-id="63734-269">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="63734-270">您可以在[這裡][HOME]找到更多範例和網路安全性界限的概觀。</span><span class="sxs-lookup"><span data-stu-id="63734-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="63734-271">參考</span><span class="sxs-lookup"><span data-stu-id="63734-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="63734-272">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="63734-272">Azure Resource Manager template</span></span>
<span data-ttu-id="63734-273">這個範例會使用預先定義的 Azure Resource Manager 範本 Microsoft 維護的 GitHub 儲存機制中，並開啟 toohello 社群。</span><span class="sxs-lookup"><span data-stu-id="63734-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="63734-274">此範本可以直接從 GitHub，部署或下載並修改 toofit 您的需求。</span><span class="sxs-lookup"><span data-stu-id="63734-274">This template can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> 

<span data-ttu-id="63734-275">hello 主要範本位於 hello 檔中名為"azuredeploy.json。 」</span><span class="sxs-lookup"><span data-stu-id="63734-275">hello main template is in hello file named "azuredeploy.json."</span></span> <span data-ttu-id="63734-276">此範本可以透過 PowerShell 或 CLI 送 （與 hello 相關聯的 「 azuredeploy.parameters.json 」 檔案） toodeploy 此範本。</span><span class="sxs-lookup"><span data-stu-id="63734-276">This template can be submitted via PowerShell or CLI (with hello associated "azuredeploy.parameters.json" file) toodeploy this template.</span></span> <span data-ttu-id="63734-277">我找到 hello 最簡單的方式是 toouse hello hello README.md 頁面，在 GitHub 上的 「 部署 tooAzure 」 按鈕。</span><span class="sxs-lookup"><span data-stu-id="63734-277">I find hello easiest way is toouse hello "Deploy tooAzure" button on hello README.md page at GitHub.</span></span>

<span data-ttu-id="63734-278">toodeploy hello 範本，從 GitHub 和 hello Azure 入口網站建置這個範例，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="63734-278">toodeploy hello template that builds this example from GitHub and hello Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="63734-279">從瀏覽器中，瀏覽 toohello[範本][Template]</span><span class="sxs-lookup"><span data-stu-id="63734-279">From a browser, navigate toohello [Template][Template]</span></span>
2. <span data-ttu-id="63734-280">按一下 hello 」 部署 tooAzure 」 按鈕 （或 hello"視覺化 」 按鈕 toosee 此範本的圖形表示法）</span><span class="sxs-lookup"><span data-stu-id="63734-280">Click hello "Deploy tooAzure" button (or hello "Visualize" button toosee a graphical representation of this template)</span></span>
3. <span data-ttu-id="63734-281">在 hello 參數刀鋒視窗中，輸入 hello 儲存體帳戶、 使用者名稱和密碼，然後按一下  **確定**</span><span class="sxs-lookup"><span data-stu-id="63734-281">Enter hello Storage Account, User Name, and Password in hello Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="63734-282">建立此部署的資源群組 (您可以使用現有的資源群組，但建議您建立新的以獲得最佳結果)</span><span class="sxs-lookup"><span data-stu-id="63734-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="63734-283">如有必要，變更 hello 訂用帳戶和位置設定您的 VNet。</span><span class="sxs-lookup"><span data-stu-id="63734-283">If necessary, change hello Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="63734-284">按一下**檢查 法律條款**，閱讀 hello 條款，然後按一下**購買**tooagree。</span><span class="sxs-lookup"><span data-stu-id="63734-284">Click **Review legal terms**, read hello terms, and click **Purchase** tooagree.</span></span>
8. <span data-ttu-id="63734-285">按一下**建立**toobegin hello 部署此範本。</span><span class="sxs-lookup"><span data-stu-id="63734-285">Click **Create** toobegin hello deployment of this template.</span></span>
9. <span data-ttu-id="63734-286">一旦 hello 部署順利完成時，瀏覽的 toohello 內設定此部署 toosee hello 資源建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="63734-286">Once hello deployment finishes successfully, navigate toohello Resource Group created for this deployment toosee hello resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="63734-287">此範本可讓 RDP toohello IIS01 僅限伺服器 (尋找 hello IIS01 公用 IP 上 hello 入口網站)。</span><span class="sxs-lookup"><span data-stu-id="63734-287">This template enables RDP toohello IIS01 server only (find hello Public IP for IIS01 on hello Portal).</span></span> <span data-ttu-id="63734-288">在此情況下，hello IIS 伺服器 tooRDP tooany 後端伺服器作為 「 跳躍方塊 」。</span><span class="sxs-lookup"><span data-stu-id="63734-288">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="63734-289">第一部 RDP toohello IIS 伺服器，然後從 hello IIS 伺服器的 RDP toohello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="63734-289">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

<span data-ttu-id="63734-290">tooremove 此部署，刪除 hello 資源群組和所有子資源也將一併刪除。</span><span class="sxs-lookup"><span data-stu-id="63734-290">tooremove this deployment, delete hello Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="63734-291">範例應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="63734-291">Sample application scripts</span></span>
<span data-ttu-id="63734-292">一旦 hello 範本順利執行，您可以設定 hello web 伺服器和應用程式伺服器與簡單的 web 應用程式 tooallow 測試此周邊網路設定。</span><span class="sxs-lookup"><span data-stu-id="63734-292">Once hello template runs successfully, you can set up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span> <span data-ttu-id="63734-293">tooinstall 這個及其他 DMZ 範例的範例應用程式，其中提供了在 hello 下列連結：[範例應用程式指令碼][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="63734-293">tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="63734-294">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63734-294">Next steps</span></span>

* <span data-ttu-id="63734-295">部署此範例</span><span class="sxs-lookup"><span data-stu-id="63734-295">Deploy this example</span></span>
* <span data-ttu-id="63734-296">建置 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="63734-296">Build hello sample application</span></span>
* <span data-ttu-id="63734-297">測試流經此 DMZ 的不同流量</span><span class="sxs-lookup"><span data-stu-id="63734-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "具有 NSG 的輸入 DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md