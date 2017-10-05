---
title: "Azure DMZ 範例 – 建置具有 NSG 的簡單 DMZ | Microsoft Docs"
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
ms.openlocfilehash: ec29e6b250f927a3a4a94ffdf83d6c7c0e325722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="17ca4-103">範例 1 – 使用 NSG 搭配 Azure Resource Manager 範本建立簡單的 DMZ</span><span class="sxs-lookup"><span data-stu-id="17ca4-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="17ca4-104">[返回 [安全性界限最佳作法] 頁面][HOME]</span><span class="sxs-lookup"><span data-stu-id="17ca4-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="17ca4-105">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="17ca4-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="17ca4-106">傳統 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="17ca4-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="17ca4-107">此範例會建立包含四個 Windows 伺服器和網路安全性群組的基本 DMZ。</span><span class="sxs-lookup"><span data-stu-id="17ca4-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="17ca4-108">此範例說明每個相關範本區段，以讓您更加深入地了解每個步驟。</span><span class="sxs-lookup"><span data-stu-id="17ca4-108">This example describes each of the relevant template sections to provide a deeper understanding of each step.</span></span> <span data-ttu-id="17ca4-109">另外您還會看到＜流量案例＞一節，本節提供深入的逐步說明，讓您知道流量是如何流經 DMZ 內的各個防禦層。</span><span class="sxs-lookup"><span data-stu-id="17ca4-109">There is also a Traffic Scenario section to provide an in-depth step-by-step look at how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="17ca4-110">最後則有＜參考＞一節，本節提供完整的範本程式碼和指示，以供您建置此環境來測試和試驗各種案例。</span><span class="sxs-lookup"><span data-stu-id="17ca4-110">Finally, in the references section is the complete template code and instructions to build this environment to test and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="17ca4-111">![具有 NSG 的輸入 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="17ca4-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="17ca4-112">環境描述</span><span class="sxs-lookup"><span data-stu-id="17ca4-112">Environment description</span></span>
<span data-ttu-id="17ca4-113">此範例中，訂用帳戶包含下列資源：</span><span class="sxs-lookup"><span data-stu-id="17ca4-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="17ca4-114">單一資源群組</span><span class="sxs-lookup"><span data-stu-id="17ca4-114">A single resource group</span></span>
* <span data-ttu-id="17ca4-115">含有兩個子網路的虛擬網路；“FrontEnd” 和 “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="17ca4-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="17ca4-116">套用至這兩個子網路的單一網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="17ca4-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="17ca4-117">一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)</span><span class="sxs-lookup"><span data-stu-id="17ca4-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="17ca4-118">兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="17ca4-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="17ca4-119">一個代表 DNS 伺服器的 Windows Server ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="17ca4-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="17ca4-120">與應用程式 web 伺服器相關聯的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="17ca4-120">A public IP address associated with the application web server</span></span>

<span data-ttu-id="17ca4-121">在 [參考] 區段中，有連結至 Azure Resource Manager 範本，可建置這個範例中所述的環境。</span><span class="sxs-lookup"><span data-stu-id="17ca4-121">In the references section, there is a link to an Azure Resource Manager template that builds the environment described in this example.</span></span> <span data-ttu-id="17ca4-122">至於 VM 和虛擬網路的建置，雖然也是由此範例範本來完成，但本文不會詳加敘述。</span><span class="sxs-lookup"><span data-stu-id="17ca4-122">Building the VMs and Virtual Networks, although done by the example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="17ca4-123">**若要建置此環境**(這份文件的參考一節中有詳細指示)。</span><span class="sxs-lookup"><span data-stu-id="17ca4-123">**To build this environment** (detailed instructions are in the references section of this document);</span></span>

1. <span data-ttu-id="17ca4-124">將 Azure Resource Manager 範本部署在：[Azure 快速入門範本][Template]</span><span class="sxs-lookup"><span data-stu-id="17ca4-124">Deploy the Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="17ca4-125">將範例應用程式安裝在︰[範例應用程式指令碼][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="17ca4-125">Install the sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="17ca4-126">在這個執行個體中 RDP 至任何後端伺服器，IIS 伺服器會作為「跳躍箱」。</span><span class="sxs-lookup"><span data-stu-id="17ca4-126">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="17ca4-127">首先 RDP 到 IIS 伺服器，然後從 IIS 伺服器 RDP 到後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="17ca4-127">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span> <span data-ttu-id="17ca4-128">或者，可以將公用 IP 與每個伺服器 NIC 相關聯以便更容易 RDP。</span><span class="sxs-lookup"><span data-stu-id="17ca4-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="17ca4-129">下列各節藉由逐步解說 Azure Resource Manager 範本的重要程式行，詳細說明此範例的網路安全性群組和其運作方式。</span><span class="sxs-lookup"><span data-stu-id="17ca4-129">The following sections provide a detailed description of the Network Security Group and how it functions for this example by walking through key lines of the Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="17ca4-130">網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="17ca4-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="17ca4-131">此範例會組建 NSG 群組，然後載入六個規則。</span><span class="sxs-lookup"><span data-stu-id="17ca4-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="17ca4-132">一般而言，您應該先建立特定的「允許」規則，最後再建立較一般的「拒絕」規則。</span><span class="sxs-lookup"><span data-stu-id="17ca4-132">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="17ca4-133">所指定的優先順序會決定要先評估哪些規則。</span><span class="sxs-lookup"><span data-stu-id="17ca4-133">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="17ca4-134">一旦發現流量適用特定規則，就不會再評估後續規則。</span><span class="sxs-lookup"><span data-stu-id="17ca4-134">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="17ca4-135">NSG 規則可以套用在輸入或輸出方向 (從子網路的觀點出發)。</span><span class="sxs-lookup"><span data-stu-id="17ca4-135">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
>
>

<span data-ttu-id="17ca4-136">指令碼會以宣告方式為輸入流量建置下列規則：</span><span class="sxs-lookup"><span data-stu-id="17ca4-136">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="17ca4-137">允許內部 DNS 流量 (連接埠 53)</span><span class="sxs-lookup"><span data-stu-id="17ca4-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="17ca4-138">允許從網際網路到任何 VM 的 RDP 流量 (連接埠 3389)</span><span class="sxs-lookup"><span data-stu-id="17ca4-138">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="17ca4-139">允許從網際網路到 Web 伺服器 (IIS01) 的 HTTP 流量 (連接埠 80)</span><span class="sxs-lookup"><span data-stu-id="17ca4-139">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="17ca4-140">允許從 IIS01 到 AppVM1 的任何流量 (所有連接埠)</span><span class="sxs-lookup"><span data-stu-id="17ca4-140">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="17ca4-141">拒絕從網際網路到整個 VNet (兩個子網路) 的任何流量 (所有連接埠)</span><span class="sxs-lookup"><span data-stu-id="17ca4-141">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="17ca4-142">拒絕從 Frontend 子網路到 Backend 子網路的任何流量 (所有連接埠)</span><span class="sxs-lookup"><span data-stu-id="17ca4-142">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="17ca4-143">這些規則繫結至每個子網路後，如果有從網際網路到 Web 伺服器的輸入 HTTP 要求，規則 3 (允許) 和規則 5 (拒絕) 皆適用，但由於規則 3 具有較高的優先順序，所以只會適用規則 3，規則 5 則不會派上用場。</span><span class="sxs-lookup"><span data-stu-id="17ca4-143">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="17ca4-144">因此會允許 HTTP 要求送往 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="17ca4-144">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="17ca4-145">如果相同的流量嘗試抵達 DNS01 伺服器，規則 5 (拒絕) 會先適用，因此不會允許流量傳遞給伺服器。</span><span class="sxs-lookup"><span data-stu-id="17ca4-145">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="17ca4-146">規則 6 (拒絕) 會阻止 Frontend 子網路與 Backend 子網路交談 (規則 1 和 4 允許的流量除外)，此規則集可在攻擊者入侵 Frontend 上的 Web 應用程式時保護 Backend 網路，攻擊者只能對 Backend 的「受保護」網路進行有限度的存取 (只能存取 AppVM01 伺服器上公開的資源)。</span><span class="sxs-lookup"><span data-stu-id="17ca4-146">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="17ca4-147">有一個預設輸出規則可允許流量外流到網際網路。</span><span class="sxs-lookup"><span data-stu-id="17ca4-147">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="17ca4-148">在此範例中，我們會允許輸出流量，並不會修改任何輸出規則。</span><span class="sxs-lookup"><span data-stu-id="17ca4-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="17ca4-149">如果兩個方向的流量都要套用安全性原則，則需要使用者定義的路由，會在[安全性界限最佳作法頁面][HOME]上的＜範例 3＞中探討。</span><span class="sxs-lookup"><span data-stu-id="17ca4-149">To apply security policy to traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="17ca4-150">會詳細討論每個規則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="17ca4-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="17ca4-151">必須具現化網路安全性群組資源，以保存規則︰</span><span class="sxs-lookup"><span data-stu-id="17ca4-151">A Network Security Group resource must be instantiated to hold the rules:</span></span>

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

2. <span data-ttu-id="17ca4-152">此範例中的第一個規則會允許所有內部網路之間的 DNS 流量流往 Backend 子網路上的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="17ca4-152">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="17ca4-153">此規則有一些重要參數：</span><span class="sxs-lookup"><span data-stu-id="17ca4-153">The rule has some important parameters:</span></span>
  * <span data-ttu-id="17ca4-154">"destinationAddressPrefix" - 規則可以使用稱為「預設標記」的位址首碼特殊類型，這些標記是系統提供的識別項，可使用簡單的方法來解決較大的位址前置詞類別。</span><span class="sxs-lookup"><span data-stu-id="17ca4-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way to address a larger category of address prefixes.</span></span> <span data-ttu-id="17ca4-155">此規則會使用預設標記「網際網路」來表示 VNet 之外的任何位址。</span><span class="sxs-lookup"><span data-stu-id="17ca4-155">This rule uses the Default Tag “Internet” to signify any address outside of the VNet.</span></span> <span data-ttu-id="17ca4-156">其他前置詞標籤為 VirtualNetwork 和 AzureLoadBalancer。</span><span class="sxs-lookup"><span data-stu-id="17ca4-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="17ca4-157">「方向」表示此規則會生效的傳輸流量方向。</span><span class="sxs-lookup"><span data-stu-id="17ca4-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="17ca4-158">方向是來自子網路或虛擬機器的角度 (取決於此 NSG 繫結的位置)。</span><span class="sxs-lookup"><span data-stu-id="17ca4-158">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="17ca4-159">因此，如果 Direction 是 “Inbound” 且流量進入子網路，此規則將會適用，而離開子網路的流量則不受此規則所影響。</span><span class="sxs-lookup"><span data-stu-id="17ca4-159">Thus if Direction is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="17ca4-160">"Priority" 會設定流量的評估順序。</span><span class="sxs-lookup"><span data-stu-id="17ca4-160">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="17ca4-161">編號愈低，優先順序就愈高。</span><span class="sxs-lookup"><span data-stu-id="17ca4-161">The lower the number the higher the priority.</span></span> <span data-ttu-id="17ca4-162">當規則套用至特定流量時，就不會再處理其他規則。</span><span class="sxs-lookup"><span data-stu-id="17ca4-162">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="17ca4-163">因此，如果優先順序為 1 的規則允許流量，優先順序為 2 的規則拒絕流量，而這兩個規則皆適用於流量，則會允許流量流動 (規則 1 有更高的優先順序，所以會生效，並且不會再套用其他規則)。</span><span class="sxs-lookup"><span data-stu-id="17ca4-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="17ca4-164">“Access” 指出受此規則影響的流量是要封鎖 ("Deny") 或允許 ("Allow")。</span><span class="sxs-lookup"><span data-stu-id="17ca4-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

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

3. <span data-ttu-id="17ca4-165">此規則會允許 RDP 流量從網際網路流往繫結子網路上任何伺服器的 RDP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="17ca4-165">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> 

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

4. <span data-ttu-id="17ca4-166">此規則允許輸入網際網路流量抵達 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="17ca4-166">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="17ca4-167">此規則不會變更路由的行為。</span><span class="sxs-lookup"><span data-stu-id="17ca4-167">This rule does not change the routing behavior.</span></span> <span data-ttu-id="17ca4-168">這個規則只會允許指向 IIS01 的流量通過。</span><span class="sxs-lookup"><span data-stu-id="17ca4-168">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="17ca4-169">因此，如果來自網際網路的流量將 Web 伺服器做為其目的地，此規則會允許流量，並停止再處理其他規則。</span><span class="sxs-lookup"><span data-stu-id="17ca4-169">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="17ca4-170">(在優先順序為 140 的規則中，其他所有輸入網際網路流量皆會遭到封鎖)。</span><span class="sxs-lookup"><span data-stu-id="17ca4-170">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="17ca4-171">如果您只要處理 HTTP 流量，則可將此規則進一步限制為只允許目的地連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="17ca4-171">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet to [variables('VM01Name')]",
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

5. <span data-ttu-id="17ca4-172">此規則允許流量從 IIS01 伺服器傳遞到 AppVM01 伺服器，較後面的規則會封鎖其他所有 Frontend 到 Backend 的流量。</span><span class="sxs-lookup"><span data-stu-id="17ca4-172">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="17ca4-173">如果已知連接埠應該加入，可改善此規則。</span><span class="sxs-lookup"><span data-stu-id="17ca4-173">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="17ca4-174">例如，如果 IIS 伺服器只會抵達 AppVM01 上的 SQL Server，且 Web 應用程式曾遭到入侵，則目的地連接埠範圍應該從 “*” (任何) 變更為 1433 (SQL 連接埠)，以縮小 AppVM01 上的輸入攻擊面。</span><span class="sxs-lookup"><span data-stu-id="17ca4-174">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] to [variables('VM02Name')]",
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

6. <span data-ttu-id="17ca4-175">此規則會拒絕從網際網路到網路上任何伺服器的流量。</span><span class="sxs-lookup"><span data-stu-id="17ca4-175">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="17ca4-176">利用優先順序為 110 和 120 的規則，效果將可只允許輸入網際網路流量流往防火牆以及伺服器上的 RDP 連接埠，除此之外的其他流量則予以封鎖。</span><span class="sxs-lookup"><span data-stu-id="17ca4-176">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="17ca4-177">此規則是「保險」規則，可封鎖所有未預期的流程。</span><span class="sxs-lookup"><span data-stu-id="17ca4-177">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate the [variables('VNetName')] VNet from the Internet",
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

7. <span data-ttu-id="17ca4-178">最後一個規則會拒絕從 Frontend 子網路到 Backend 子網路的流量。</span><span class="sxs-lookup"><span data-stu-id="17ca4-178">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="17ca4-179">此規則是僅限輸入的規則，所以允許反向流量 (從 Backend 到 Frontend)。</span><span class="sxs-lookup"><span data-stu-id="17ca4-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate the [variables('Subnet1Name')] subnet from the [variables('Subnet2Name')] subnet",
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

## <a name="traffic-scenarios"></a><span data-ttu-id="17ca4-180">流量案例</span><span class="sxs-lookup"><span data-stu-id="17ca4-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="17ca4-181">(允許) 網際網路到 Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="17ca4-181">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="17ca4-182">網際網路使用者向 IIS01 NIC 相關聯的 NIC 公用 IP 位址要求 HTTP 頁面</span><span class="sxs-lookup"><span data-stu-id="17ca4-182">An internet user requests an HTTP page from the public IP address of the NIC associated with the IIS01 NIC</span></span>
2. <span data-ttu-id="17ca4-183">公用 IP 位址會將對 VNet 的流量傳遞至 IIS01 (web 伺服器)</span><span class="sxs-lookup"><span data-stu-id="17ca4-183">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="17ca4-184">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="17ca4-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="17ca4-185">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-185">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="17ca4-186">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-186">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="17ca4-187">NSG 規則 3 (網際網路到 IIS01) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-187">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="17ca4-188">流量抵達 Web 伺服器 IIS01 的內部 IP 位址 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="17ca4-188">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="17ca4-189">IIS01 正在接聽 Web 流量，接收此要求並開始處理要求</span><span class="sxs-lookup"><span data-stu-id="17ca4-189">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="17ca4-190">IIS01 向 AppVM01 上的 SQL Server 要求資訊</span><span class="sxs-lookup"><span data-stu-id="17ca4-190">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="17ca4-191">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="17ca4-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="17ca4-192">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="17ca4-192">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="17ca4-193">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="17ca4-194">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="17ca4-195">NSG 規則 3 (網際網路到防火牆) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-195">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="17ca4-196">NSG 規則 4 (IIS01 到 AppVM01) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-196">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="17ca4-197">AppVM01 接收 SQL 查詢並回應</span><span class="sxs-lookup"><span data-stu-id="17ca4-197">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="17ca4-198">Backend 子網路上沒有輸出規則，所以允許回應</span><span class="sxs-lookup"><span data-stu-id="17ca4-198">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="17ca4-199">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="17ca4-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="17ca4-200">Backend 子網路到 Frontend 子網路的輸入流量沒有適用的 NSG 規則，因此不會套用任何 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-200">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="17ca4-201">允許子網路間流量的預設系統規則會允許此流量，因此允許流量。</span><span class="sxs-lookup"><span data-stu-id="17ca4-201">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="17ca4-202">IIS 伺服器會接收 SQL 回應、完成 HTTP 回應並傳送給要求者</span><span class="sxs-lookup"><span data-stu-id="17ca4-202">The IIS server receives the SQL response and completes the HTTP response and sends to the requester</span></span>
13. <span data-ttu-id="17ca4-203">Frontend 子網路上沒有輸出規則，所以允許回應，網際網路使用者會收到要求的網頁。</span><span class="sxs-lookup"><span data-stu-id="17ca4-203">Since there are no outbound rules on the Frontend subnet, the response is allowed and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-iis-server"></a><span data-ttu-id="17ca4-204">(允許) RDP 到 IIS 伺服器</span><span class="sxs-lookup"><span data-stu-id="17ca4-204">(*Allowed*) RDP to IIS server</span></span>
1. <span data-ttu-id="17ca4-205">網際網路上的伺服器系統管理員會要求 RDP 工作階段至與 IIS01 NIC 相關聯的 NIC 之公用 IP 位址上的 IIS01 (可以透過入口網站或 PowerShell 找到這個公用 IP 位址)</span><span class="sxs-lookup"><span data-stu-id="17ca4-205">A Server Admin on internet requests an RDP session to IIS01 on the public IP address of the NIC associated with the IIS01 NIC (this public IP address can be found via the Portal or PowerShell)</span></span>
2. <span data-ttu-id="17ca4-206">公用 IP 位址會將對 VNet 的流量傳遞至 IIS01 (web 伺服器)</span><span class="sxs-lookup"><span data-stu-id="17ca4-206">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="17ca4-207">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="17ca4-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="17ca4-208">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-208">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="17ca4-209">NSG 規則 2 (RDP) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="17ca4-210">由於沒有輸出規則，會套用預設規則並允許傳回的流量</span><span class="sxs-lookup"><span data-stu-id="17ca4-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="17ca4-211">已啟用 RDP 工作階段</span><span class="sxs-lookup"><span data-stu-id="17ca4-211">RDP session is enabled</span></span>
6. <span data-ttu-id="17ca4-212">IIS01 會提示輸入使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="17ca4-212">IIS01 prompts for the user name and password</span></span>

>[!NOTE]
><span data-ttu-id="17ca4-213">在這個執行個體中 RDP 至任何後端伺服器，IIS 伺服器會作為「跳躍箱」。</span><span class="sxs-lookup"><span data-stu-id="17ca4-213">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="17ca4-214">首先 RDP 到 IIS 伺服器，然後從 IIS 伺服器 RDP 到後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="17ca4-214">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="17ca4-215">(允許) DNS 伺服器上的 Web 伺服器 DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="17ca4-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="17ca4-216">Web 伺服器 IIS01 需要 www.data.gov 的資料摘要，但需要解析位址。</span><span class="sxs-lookup"><span data-stu-id="17ca4-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="17ca4-217">VNet 的網路組態將 DNS01 (Backend 子網路上的 10.0.2.4) 列為主要 DNS 伺服器，IIS01 將 DNS 要求傳送至 DNS01</span><span class="sxs-lookup"><span data-stu-id="17ca4-217">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="17ca4-218">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="17ca4-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="17ca4-219">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="17ca4-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="17ca4-220">NSG 規則 1 (DNS) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="17ca4-221">DNS 伺服器收到要求</span><span class="sxs-lookup"><span data-stu-id="17ca4-221">DNS server receives the request</span></span>
6. <span data-ttu-id="17ca4-222">DNS 伺服器沒有快取的位址，並要求網際網路上的根 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="17ca4-222">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="17ca4-223">Backend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="17ca4-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="17ca4-224">網際網路 DNS 伺服器回應，因為此工作階段是從內部起始，所以允許回應</span><span class="sxs-lookup"><span data-stu-id="17ca4-224">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="17ca4-225">DNS 伺服器快取回應，然後將初始要求回應到 IIS01</span><span class="sxs-lookup"><span data-stu-id="17ca4-225">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="17ca4-226">Backend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="17ca4-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="17ca4-227">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="17ca4-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="17ca4-228">Backend 子網路到 Frontend 子網路的輸入流量沒有適用的 NSG 規則，因此不會套用任何 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-228">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="17ca4-229">允許子網路間流量的預設系統規則會允許此流量，因此允許流量</span><span class="sxs-lookup"><span data-stu-id="17ca4-229">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="17ca4-230">IIS01 從 DNS01 接收回應</span><span class="sxs-lookup"><span data-stu-id="17ca4-230">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="17ca4-231">(允許) Web 伺服器存取 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="17ca4-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="17ca4-232">IIS01 要求 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="17ca4-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="17ca4-233">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="17ca4-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="17ca4-234">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="17ca4-234">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="17ca4-235">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-235">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="17ca4-236">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-236">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="17ca4-237">NSG 規則 3 (網際網路到 IIS01) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-237">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="17ca4-238">NSG 規則 4 (IIS01 到 AppVM01) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-238">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="17ca4-239">AppVM01 接收要求並以檔案回應 (假設已獲得存取授權)</span><span class="sxs-lookup"><span data-stu-id="17ca4-239">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="17ca4-240">Backend 子網路上沒有輸出規則，所以允許回應</span><span class="sxs-lookup"><span data-stu-id="17ca4-240">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="17ca4-241">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="17ca4-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="17ca4-242">Backend 子網路到 Frontend 子網路的輸入流量沒有適用的 NSG 規則，因此不會套用任何 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-242">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="17ca4-243">允許子網路間流量的預設系統規則會允許此流量，因此允許流量。</span><span class="sxs-lookup"><span data-stu-id="17ca4-243">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="17ca4-244">IIS 伺服器接收檔案</span><span class="sxs-lookup"><span data-stu-id="17ca4-244">The IIS server receives the file</span></span>

#### <a name="denied-rdp-to-backend"></a><span data-ttu-id="17ca4-245">(拒絕) RDP 到 Backend</span><span class="sxs-lookup"><span data-stu-id="17ca4-245">(*Denied*) RDP to backend</span></span>
1. <span data-ttu-id="17ca4-246">網際網路使用者嘗試 RDP 伺服器 AppVM01</span><span class="sxs-lookup"><span data-stu-id="17ca4-246">An internet user tries to RDP to server AppVM01</span></span>
2. <span data-ttu-id="17ca4-247">沒有與此伺服器 NIC 相關聯的公用 IP 位址，因此這個流量永遠不會輸入 VNet，而且不會連線到伺服器</span><span class="sxs-lookup"><span data-stu-id="17ca4-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="17ca4-248">不過，如果因為某些原因已啟用公用 IP 位址，NSG 規則 2 (RDP) 會允許此流量</span><span class="sxs-lookup"><span data-stu-id="17ca4-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="17ca4-249">在這個執行個體中 RDP 至任何後端伺服器，IIS 伺服器會作為「跳躍箱」。</span><span class="sxs-lookup"><span data-stu-id="17ca4-249">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="17ca4-250">首先 RDP 到 IIS 伺服器，然後從 IIS 伺服器 RDP 到後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="17ca4-250">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="17ca4-251">(拒絕) Web 到 Backend 伺服器</span><span class="sxs-lookup"><span data-stu-id="17ca4-251">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="17ca4-252">網際網路使用者嘗試存取 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="17ca4-252">An internet user tries to access a file on AppVM01</span></span>
2. <span data-ttu-id="17ca4-253">沒有與此伺服器 NIC 相關聯的公用 IP 位址，因此這個流量永遠不會輸入 VNet，而且不會連線到伺服器</span><span class="sxs-lookup"><span data-stu-id="17ca4-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="17ca4-254">如果因為某些原因已啟用公用 IP 位址，NSG 規則 5 (網際網路到 VNet) 會封鎖此流量</span><span class="sxs-lookup"><span data-stu-id="17ca4-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="17ca4-255">(拒絕) DNS 伺服器上的 Web DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="17ca4-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="17ca4-256">網際網路使用者嘗試查閱 DNS01 上的內部 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="17ca4-256">An internet user tries to look up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="17ca4-257">沒有與此伺服器 NIC 相關聯的公用 IP 位址，因此這個流量永遠不會輸入 VNet，而且不會連線到伺服器</span><span class="sxs-lookup"><span data-stu-id="17ca4-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="17ca4-258">如果因為某些原因已啟用公用 IP 位址，NSG 規則 5 (網際網路到 VNet) 會封鎖此流量 (請注意︰因為要求來源位址是網際網路且規則 1 僅適用於做為來源的本機 VNet，因此不會套用規則 1 (DNS))</span><span class="sxs-lookup"><span data-stu-id="17ca4-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because the requests source address is the internet and Rule 1 only applies to the local VNet as the source)</span></span>

#### <a name="denied-sql-access-on-the-web-server"></a><span data-ttu-id="17ca4-259">(拒絕) 網頁伺服器上的 SQL 存取</span><span class="sxs-lookup"><span data-stu-id="17ca4-259">(*Denied*) SQL access on the web server</span></span>
1. <span data-ttu-id="17ca4-260">網際網路使用者向 IIS01 要求 SQL 資料</span><span class="sxs-lookup"><span data-stu-id="17ca4-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="17ca4-261">沒有與此伺服器 NIC 相關聯的公用 IP 位址，因此這個流量永遠不會輸入 VNet，而且不會連線到伺服器</span><span class="sxs-lookup"><span data-stu-id="17ca4-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="17ca4-262">如果基於某些原因而啟用公用 IP 位址，Frontend 子網路會開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="17ca4-262">If a Public IP address was enabled for some reason, the Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="17ca4-263">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-263">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="17ca4-264">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-264">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="17ca4-265">NSG 規則 3 (網際網路到 IIS01) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="17ca4-265">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="17ca4-266">流量抵達 IIS01 的內部 IP 位址 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="17ca4-266">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="17ca4-267">IIS01 未接聽連接埠 1433，所以要求沒有回應</span><span class="sxs-lookup"><span data-stu-id="17ca4-267">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="17ca4-268">結論</span><span class="sxs-lookup"><span data-stu-id="17ca4-268">Conclusion</span></span>
<span data-ttu-id="17ca4-269">這個範例隔離後端子網路與輸入流量的方式相當直接簡單。</span><span class="sxs-lookup"><span data-stu-id="17ca4-269">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="17ca4-270">您可以在[這裡][HOME]找到更多範例和網路安全性界限的概觀。</span><span class="sxs-lookup"><span data-stu-id="17ca4-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="17ca4-271">參考</span><span class="sxs-lookup"><span data-stu-id="17ca4-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="17ca4-272">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="17ca4-272">Azure Resource Manager template</span></span>
<span data-ttu-id="17ca4-273">此範例使用預先定義的 Azure Resource Manager 範本 (範本位於由 Microsoft 維護且開放社群使用的 GitHub 存放庫中)。</span><span class="sxs-lookup"><span data-stu-id="17ca4-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="17ca4-274">這個範本可以直接從 GitHub 部署，或下載並修改以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="17ca4-274">This template can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> 

<span data-ttu-id="17ca4-275">主要範本位於名為 "azuredeploy.json" 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="17ca4-275">The main template is in the file named "azuredeploy.json."</span></span> <span data-ttu-id="17ca4-276">此範本可以透過 PowerShell 或 CLI (具有相關聯的 "azuredeploy.parameters.json" 檔案) 提交來部署此範本。</span><span class="sxs-lookup"><span data-stu-id="17ca4-276">This template can be submitted via PowerShell or CLI (with the associated "azuredeploy.parameters.json" file) to deploy this template.</span></span> <span data-ttu-id="17ca4-277">我發現最簡單的方式是在 GitHub 使用 README.md 頁面上的 [部署至 Azure] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="17ca4-277">I find the easiest way is to use the "Deploy to Azure" button on the README.md page at GitHub.</span></span>

<span data-ttu-id="17ca4-278">若要部署從 GitHub 和 Azure 入口網站建立此範例的範本，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="17ca4-278">To deploy the template that builds this example from GitHub and the Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="17ca4-279">從瀏覽器，瀏覽至[範本][Template]</span><span class="sxs-lookup"><span data-stu-id="17ca4-279">From a browser, navigate to the [Template][Template]</span></span>
2. <span data-ttu-id="17ca4-280">按一下 [部署至 Azure] 按鈕 (或 [視覺化] 按鈕以查看這個範本的圖形表示法)</span><span class="sxs-lookup"><span data-stu-id="17ca4-280">Click the "Deploy to Azure" button (or the "Visualize" button to see a graphical representation of this template)</span></span>
3. <span data-ttu-id="17ca4-281">在 [參數] 刀鋒視窗中，輸入儲存體帳戶、使用者名稱和密碼，然後按一下 [確定]</span><span class="sxs-lookup"><span data-stu-id="17ca4-281">Enter the Storage Account, User Name, and Password in the Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="17ca4-282">建立此部署的資源群組 (您可以使用現有的資源群組，但建議您建立新的以獲得最佳結果)</span><span class="sxs-lookup"><span data-stu-id="17ca4-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="17ca4-283">如有必要，變更 VNet 的訂用帳戶和位置設定。</span><span class="sxs-lookup"><span data-stu-id="17ca4-283">If necessary, change the Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="17ca4-284">按一下 [檢閱法律條款] 並閱讀條款，然後按一下 [購買] 表示同意條款。</span><span class="sxs-lookup"><span data-stu-id="17ca4-284">Click **Review legal terms**, read the terms, and click **Purchase** to agree.</span></span>
8. <span data-ttu-id="17ca4-285">按一下 [建立] 開始部署此範本。</span><span class="sxs-lookup"><span data-stu-id="17ca4-285">Click **Create** to begin the deployment of this template.</span></span>
9. <span data-ttu-id="17ca4-286">部署成功完成後，瀏覽至針對此部署建立的資源群組，以查看內部設定的資源。</span><span class="sxs-lookup"><span data-stu-id="17ca4-286">Once the deployment finishes successfully, navigate to the Resource Group created for this deployment to see the resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="17ca4-287">此範本僅對 IIS01 伺服器啟用 RDP (在入口網站上尋找 IIS01 的公用 IP)。</span><span class="sxs-lookup"><span data-stu-id="17ca4-287">This template enables RDP to the IIS01 server only (find the Public IP for IIS01 on the Portal).</span></span> <span data-ttu-id="17ca4-288">在這個執行個體中 RDP 至任何後端伺服器，IIS 伺服器會作為「跳躍箱」。</span><span class="sxs-lookup"><span data-stu-id="17ca4-288">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="17ca4-289">首先 RDP 到 IIS 伺服器，然後從 IIS 伺服器 RDP 到後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="17ca4-289">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

<span data-ttu-id="17ca4-290">若要移除此部署，請刪除資源群組，也會刪除所有子資源。</span><span class="sxs-lookup"><span data-stu-id="17ca4-290">To remove this deployment, delete the Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="17ca4-291">範例應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="17ca4-291">Sample application scripts</span></span>
<span data-ttu-id="17ca4-292">一旦範本順利執行後，您可以設定 Web 伺服器和具有簡單 Web 應用程式的應用程式伺服器，以便能使用此 DMZ 組態進行測試。</span><span class="sxs-lookup"><span data-stu-id="17ca4-292">Once the template runs successfully, you can set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span> <span data-ttu-id="17ca4-293">如需為此範例和其他 DMZ 範例安裝範例應用程式，下列連結中有提供一個：[範例應用程式指令碼][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="17ca4-293">To install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="17ca4-294">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17ca4-294">Next steps</span></span>

* <span data-ttu-id="17ca4-295">部署此範例</span><span class="sxs-lookup"><span data-stu-id="17ca4-295">Deploy this example</span></span>
* <span data-ttu-id="17ca4-296">建置範例應用程式</span><span class="sxs-lookup"><span data-stu-id="17ca4-296">Build the sample application</span></span>
* <span data-ttu-id="17ca4-297">測試流經此 DMZ 的不同流量</span><span class="sxs-lookup"><span data-stu-id="17ca4-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
<span data-ttu-id="17ca4-298">[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "具有 NSG 的輸入 DMZ"</span><span class="sxs-lookup"><span data-stu-id="17ca4-298">[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Inbound DMZ with NSG"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md