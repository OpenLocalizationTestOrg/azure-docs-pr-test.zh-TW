---
title: "DMZ 範例 – 建置 DMZ 以透過防火牆和 NSG 保護應用程式 | Microsoft Docs"
description: "建置具有防火牆和網路安全性群組 (NSG) 的 DMZ"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc0e8a3fa749eb2e6f65ef92c2d3cb404cfc8bc0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="example-2--build-a-dmz-to-protect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="29775-103">範例 2 – 建置 DMZ 以透過防火牆和 NSG 保護應用程式</span><span class="sxs-lookup"><span data-stu-id="29775-103">Example 2 – Build a DMZ to protect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="29775-104">[返回 [安全性界限最佳作法] 頁面][HOME]</span><span class="sxs-lookup"><span data-stu-id="29775-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="29775-105">此範例會建立 DMZ，其內含防火牆、四個 Windows 伺服器和網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="29775-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="29775-106">此範例也會逐步解說每個相關命令，以讓您更加深入地了解每個步驟。</span><span class="sxs-lookup"><span data-stu-id="29775-106">It will also walk through each of the relevant commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="29775-107">另外您還會看到＜流量案例＞一節，本節提供深入的逐步說明，讓您知道流量是如何流經 DMZ 內的各個防禦層。</span><span class="sxs-lookup"><span data-stu-id="29775-107">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="29775-108">最後則有＜參考＞一節，本節提供完整的程式碼和指示，以供您建置此環境來測試和試驗各種案例。</span><span class="sxs-lookup"><span data-stu-id="29775-108">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="29775-109">![輸入 DMZ NVA 與 NSG][1]</span><span class="sxs-lookup"><span data-stu-id="29775-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="29775-110">環境描述</span><span class="sxs-lookup"><span data-stu-id="29775-110">Environment Description</span></span>
<span data-ttu-id="29775-111">此範例中，有一個訂用帳戶包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="29775-111">In this example there is a subscription that contains the following:</span></span>

* <span data-ttu-id="29775-112">兩個雲端服務：“FrontEnd001” 和 “BackEnd001”</span><span class="sxs-lookup"><span data-stu-id="29775-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="29775-113">一個虛擬網路 “CorpNetwork”，包含兩個子網路：“FrontEnd” 和 “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="29775-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="29775-114">套用至這兩個子網路的單一網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="29775-114">A single Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="29775-115">一個網路虛擬應用裝置 (在此範例中為 Barracuda NextGen 防火牆)，且已連線到 Frontend 子網路</span><span class="sxs-lookup"><span data-stu-id="29775-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected to the Frontend subnet</span></span>
* <span data-ttu-id="29775-116">一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)</span><span class="sxs-lookup"><span data-stu-id="29775-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="29775-117">兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="29775-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="29775-118">一個代表 DNS 伺服器的 Windows Server ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="29775-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="29775-119">雖然此範例使用 Barracuda NextGen 防火牆，但還有許多不同的網路虛擬應用裝置能夠用於此範例。</span><span class="sxs-lookup"><span data-stu-id="29775-119">Although this example uses a Barracuda NextGen Firewall, many of the different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="29775-120">在下面的＜參考＞一節中有提供 PowerShell 指令碼，其可建置上述的大部分環境。</span><span class="sxs-lookup"><span data-stu-id="29775-120">In the references section below there is a PowerShell script that will build most of the environment described above.</span></span> <span data-ttu-id="29775-121">至於 VM 和虛擬網路的建置，雖然也是由此範例指令碼來完成，但本文不會詳加敘述。</span><span class="sxs-lookup"><span data-stu-id="29775-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span>

<span data-ttu-id="29775-122">若要建置環境：</span><span class="sxs-lookup"><span data-stu-id="29775-122">To build the environment:</span></span>

1. <span data-ttu-id="29775-123">儲存＜參考＞一節中所包含的網路組態 xml 檔 (更新名稱、位置和 IP 位址以符合給定的案例)</span><span class="sxs-lookup"><span data-stu-id="29775-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="29775-124">更新指令碼中的使用者變數，以符合要用來執行指令碼的環境 (訂用帳戶、服務名稱等)</span><span class="sxs-lookup"><span data-stu-id="29775-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="29775-125">在 PowerShell 中執行指令碼</span><span class="sxs-lookup"><span data-stu-id="29775-125">Execute the script in PowerShell</span></span>

<span data-ttu-id="29775-126">**注意**：PowerShell 指令碼中所指的區域必須符合網路組態 xml 檔中所指的區域。</span><span class="sxs-lookup"><span data-stu-id="29775-126">**Note**: The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>

<span data-ttu-id="29775-127">指令碼順利執行後，即可採取下列指令碼後續步驟：</span><span class="sxs-lookup"><span data-stu-id="29775-127">Once the script runs successfully the following post-script steps may be taken:</span></span>

1. <span data-ttu-id="29775-128">設定防火牆規則，下面的＜防火牆規則＞一節會有這部分的說明。</span><span class="sxs-lookup"><span data-stu-id="29775-128">Set up the firewall rules, this is covered in the section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="29775-129">(選擇性)＜參考＞一節中有兩個指令碼，其會設定 Web 伺服器和具有簡單 Web 應用程式的應用程式伺服器，以便能使用此 DMZ 組態進行測試。</span><span class="sxs-lookup"><span data-stu-id="29775-129">Optionally in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="29775-130">下一節說明大多數與網路安全性群組相關的指令碼陳述式。</span><span class="sxs-lookup"><span data-stu-id="29775-130">The next section explains most of the scripts statements relative to Network Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="29775-131">網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="29775-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="29775-132">此範例會建置 NSG 群組，然後在其中載入六個規則。</span><span class="sxs-lookup"><span data-stu-id="29775-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="29775-133">一般而言，您應該先建立特定的「允許」規則，最後再建立較一般的「拒絕」規則。</span><span class="sxs-lookup"><span data-stu-id="29775-133">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="29775-134">所指定的優先順序會決定要先評估哪些規則。</span><span class="sxs-lookup"><span data-stu-id="29775-134">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="29775-135">一旦發現流量適用特定規則，就不會再評估後續規則。</span><span class="sxs-lookup"><span data-stu-id="29775-135">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="29775-136">NSG 規則可以套用在輸入或輸出方向 (從子網路的觀點出發)。</span><span class="sxs-lookup"><span data-stu-id="29775-136">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
> 
> 

<span data-ttu-id="29775-137">指令碼會以宣告方式為輸入流量建置下列規則：</span><span class="sxs-lookup"><span data-stu-id="29775-137">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="29775-138">允許內部 DNS 流量 (連接埠 53)</span><span class="sxs-lookup"><span data-stu-id="29775-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="29775-139">允許從網際網路到任何 VM 的 RDP 流量 (連接埠 3389)</span><span class="sxs-lookup"><span data-stu-id="29775-139">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="29775-140">允許從網際網路到 NVA (防火牆) 的 HTTP 流量 (連接埠 80)</span><span class="sxs-lookup"><span data-stu-id="29775-140">HTTP traffic (port 80) from the Internet to the NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="29775-141">允許從 IIS01 到 AppVM1 的任何流量 (所有連接埠)</span><span class="sxs-lookup"><span data-stu-id="29775-141">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="29775-142">拒絕從網際網路到整個 VNet (兩個子網路) 的任何流量 (所有連接埠)</span><span class="sxs-lookup"><span data-stu-id="29775-142">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="29775-143">拒絕從 Frontend 子網路到 Backend 子網路的任何流量 (所有連接埠)</span><span class="sxs-lookup"><span data-stu-id="29775-143">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="29775-144">這些規則繫結至每個子網路後，如果有從網際網路到 Web 伺服器的輸入 HTTP 要求，規則 3 (允許) 和規則 5 (拒絕) 皆適用，但由於規則 3 具有較高的優先順序，所以只會適用規則 3，規則 5 則不會派上用場。</span><span class="sxs-lookup"><span data-stu-id="29775-144">With these rules bound to each subnet, if a HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="29775-145">因此會允許 HTTP 要求送往防火牆。</span><span class="sxs-lookup"><span data-stu-id="29775-145">Thus the HTTP request would be allowed to the firewall.</span></span> <span data-ttu-id="29775-146">如果相同的流量嘗試抵達 DNS01 伺服器，規則 5 (拒絕) 會先適用，因此不會允許流量傳遞給伺服器。</span><span class="sxs-lookup"><span data-stu-id="29775-146">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="29775-147">規則 6 (拒絕) 會阻止 Frontend 子網路與 Backend 子網路交談 (規則 1 和 4 允許的流量除外)，這可在攻擊者入侵 Frontend 上的 Web 應用程式時保護 Backend 網路，攻擊者只能對 Backend 的「受保護」網路進行有限度的存取 (只能存取 AppVM01 伺服器上公開的資源)。</span><span class="sxs-lookup"><span data-stu-id="29775-147">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="29775-148">有一個預設輸出規則可允許流量外流到網際網路。</span><span class="sxs-lookup"><span data-stu-id="29775-148">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="29775-149">在此範例中，我們會允許輸出流量，並不會修改任何輸出規則。</span><span class="sxs-lookup"><span data-stu-id="29775-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="29775-150">如果兩個方向的流量都要鎖定，則需要使用者定義的路由，這個部分是在不同範例中探討，您可以在[主要安全性界限文件][HOME]中找到相關資訊。</span><span class="sxs-lookup"><span data-stu-id="29775-150">To lock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in the [main security boundary document][HOME].</span></span>

<span data-ttu-id="29775-151">上面討論的 NSG 規則非常類似[範例 1 - 建置具有 NSG 的簡單 DMZ][Example1] 中的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="29775-151">The above discussed NSG rules are very similar to the NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="29775-152">請檢閱該文件中的 NSG 說明，以清楚了解每個 NSG 規則和它的屬性。</span><span class="sxs-lookup"><span data-stu-id="29775-152">Please review the NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="29775-153">防火牆規則</span><span class="sxs-lookup"><span data-stu-id="29775-153">Firewall Rules</span></span>
<span data-ttu-id="29775-154">電腦上必須安裝管理用戶端，才能管理防火牆和建立所需的組態。</span><span class="sxs-lookup"><span data-stu-id="29775-154">A management client will need to be installed on a PC to manage the firewall and create the configurations needed.</span></span> <span data-ttu-id="29775-155">請參閱防火牆 (或其他 NVA) 廠商提供的說明文件，以了解如何管理裝置。</span><span class="sxs-lookup"><span data-stu-id="29775-155">See the documentation from your firewall (or other NVA) vendor on how to manage the device.</span></span> <span data-ttu-id="29775-156">本節剩餘部分將說明如何透過廠商的管理用戶端 (亦即不是使用 Azure 入口網站或 PowerShell) 設定防火牆本身。</span><span class="sxs-lookup"><span data-stu-id="29775-156">The remainder of this section will describe the configuration of the firewall itself, through the vendors management client (i.e. not the Azure portal or PowerShell).</span></span>

<span data-ttu-id="29775-157">適用於下載用戶端和連線到此範例所用 Barracuda 的指示，可以在這裡找到： [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="29775-157">Instructions for client download and connecting to the Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="29775-158">防火牆上必須建立轉送規則。</span><span class="sxs-lookup"><span data-stu-id="29775-158">On the firewall, forwarding rules will need to be created.</span></span> <span data-ttu-id="29775-159">此範例只會將網際網路流量往內路由傳送到防火牆，再傳送到 Web 伺服器，因此只需要一個轉送 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="29775-159">Since this example only routes internet traffic in-bound to the firewall and then to the web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="29775-160">在此範例所使用的 Barracuda NextGen 防火牆上，傳送此流量的這個規則是目的地 NAT 規則 (“Dst NAT”)。</span><span class="sxs-lookup"><span data-stu-id="29775-160">On the Barracuda NextGen Firewall used in this example the rule would be a Destination NAT rule (“Dst NAT”) to pass this traffic.</span></span>

<span data-ttu-id="29775-161">若要建立下列規則 (或驗證現有的預設規則)，請先從 Barracuda NG Admin 用戶端儀表板瀏覽至 [設定] 索引標籤，在 [作業組態] 區段中按一下 [規則集]。</span><span class="sxs-lookup"><span data-stu-id="29775-161">To create the following rule (or verify existing default rules), starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="29775-162">此時會出現「主要規則」方格，顯示此防火牆現有的作用中規則和已停用規則。</span><span class="sxs-lookup"><span data-stu-id="29775-162">A grid called, “Main Rules” will show the existing active and deactivated rules on the firewall.</span></span> <span data-ttu-id="29775-163">此方格右上角有一個小型的綠色 "+" 按鈕，按一下此按鈕即可建立新規則 (注意：您的防火牆可能會遭「鎖定」不準變更，如果您看到標示為 [鎖定] 的按鈕且無法建立或編輯規則，請按一下此按鈕以「解除鎖定」規則集並允許編輯)。</span><span class="sxs-lookup"><span data-stu-id="29775-163">In the upper right corner of this grid is a small, green “+” button, click this to create a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable to create or edit rules, click this button to “unlock” the ruleset and allow editing).</span></span> <span data-ttu-id="29775-164">如果您想要編輯現有規則，請選取該規則，以滑鼠右鍵按一下並選取 [編輯規則]。</span><span class="sxs-lookup"><span data-stu-id="29775-164">If you wish to edit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="29775-165">建立新規則並提供名稱，例如 "WebTraffic"。</span><span class="sxs-lookup"><span data-stu-id="29775-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="29775-166">目的地 NAT 規則圖示看起來像這樣：![目的地 NAT 圖示][2]</span><span class="sxs-lookup"><span data-stu-id="29775-166">The Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="29775-167">規則本身則看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="29775-167">The rule itself would look something like this:</span></span>

<span data-ttu-id="29775-168">![防火牆規則][3]</span><span class="sxs-lookup"><span data-stu-id="29775-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="29775-169">在這邊，任何到達嘗試連線到 HTTP (連接埠 80，若為 HTTPS 則為 443) 的輸入位址，都會被傳送出防火牆的「DHCP1 本機 IP」介面，並重新導向至 IP 位址為 10.0.1.5 的 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="29775-169">Here any inbound address that hits the Firewall trying to reach HTTP (port 80 or 443 for HTTPS) will be sent out the Firewall’s “DHCP1 Local IP” interface and redirected to the Web Server with the IP Address of 10.0.1.5.</span></span> <span data-ttu-id="29775-170">流量是在連接埠 80 上進入，並在連接埠 80 上前往 Web 伺服器，所以不需要變更連接埠。</span><span class="sxs-lookup"><span data-stu-id="29775-170">Since the traffic is coming in on port 80 and going to the web server on port 80 no port change was needed.</span></span> <span data-ttu-id="29775-171">不過，如果我們的 Web 伺服器是在連接埠 8080 上接聽，因此將防火牆上的輸入連接埠 80 轉譯為 Web 伺服器上的輸入連接埠 8080，則 [目標清單] 可以是 [10.0.1.5:8080]。</span><span class="sxs-lookup"><span data-stu-id="29775-171">However, the Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating the inbound port 80 on the firewall to inbound port 8080 on the web server.</span></span>

<span data-ttu-id="29775-172">另外，也應該針對「來自網際網路的目的地規則」表明連線方法，其中「動態 SNAT」是最合適的。</span><span class="sxs-lookup"><span data-stu-id="29775-172">A Connection Method should also be signified, for the Destination Rule from the Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="29775-173">雖然只建立了一個規則，但請務必正確設定其優先順序。</span><span class="sxs-lookup"><span data-stu-id="29775-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="29775-174">如果防火牆上所有規則的方格中，此新規則位於底部 (在「BLOCKALL」規則之下)，它將永遠不會派上用場。</span><span class="sxs-lookup"><span data-stu-id="29775-174">If in the grid of all rules on the firewall this new rule is on the bottom (below the "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="29775-175">請確定針對 Web 流量新建立的規則在 BLOCKALL 規則之上。</span><span class="sxs-lookup"><span data-stu-id="29775-175">Ensure the newly created rule for web traffic is above the BLOCKALL rule.</span></span>

<span data-ttu-id="29775-176">規則一經建立，就必須推送至防火牆並啟用，如果沒有這麼做，規則的變更就不會生效。</span><span class="sxs-lookup"><span data-stu-id="29775-176">Once the rule is created, it must be pushed to the firewall and then activated, if this is not done the rule change will not take effect.</span></span> <span data-ttu-id="29775-177">下一節會說明推送和啟用程序。</span><span class="sxs-lookup"><span data-stu-id="29775-177">The push and activation process is described in the next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="29775-178">啟用規則</span><span class="sxs-lookup"><span data-stu-id="29775-178">Rule Activation</span></span>
<span data-ttu-id="29775-179">修改規則集以新增此規則後，必須將規則集上傳至防火牆並加以啟用。</span><span class="sxs-lookup"><span data-stu-id="29775-179">With the ruleset modified to add this rule, the ruleset must be uploaded to the firewall and activated.</span></span>

<span data-ttu-id="29775-180">![防火牆規則啟用][4]</span><span class="sxs-lookup"><span data-stu-id="29775-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="29775-181">管理用戶端右上角是按鈕叢集。</span><span class="sxs-lookup"><span data-stu-id="29775-181">In the upper right hand corner of the management client are a cluster of buttons.</span></span> <span data-ttu-id="29775-182">按一下 [傳送變更] 按鈕將修改過的規則傳送到防火牆，然後按一下 [啟用] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="29775-182">Click the “Send Changes” button to send the modified rules to the firewall, then click the “Activate” button.</span></span>

<span data-ttu-id="29775-183">在啟用防火牆規則集後，這個範例環境的建置便已完成。</span><span class="sxs-lookup"><span data-stu-id="29775-183">With the activation of the firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="29775-184">(選擇性) 您可以執行＜參考＞一節中的後續建置指令碼，將應用程式新增至此環境來測試下方的流量案例。</span><span class="sxs-lookup"><span data-stu-id="29775-184">Optionally, the post build scripts in the References section can be run to add an application to this environment to test the below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29775-185">請務必了解您不會直接到達 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="29775-185">It is critical to realize that you will not hit the web server directly.</span></span> <span data-ttu-id="29775-186">當瀏覽器從 FrontEnd001.CloudApp.Net 要求 HTTP 頁面時，HTTP 端點 (連接埠 80) 會將此流量傳遞至防火牆而非 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="29775-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, the HTTP endpoint (port 80) passes this traffic to the firewall not the web server.</span></span> <span data-ttu-id="29775-187">然後，防火牆會根據上面建立的規則，將該要求 NAT 處理到 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="29775-187">The firewall then, according to the rule created above, NATs that request to the Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="29775-188">流量案例</span><span class="sxs-lookup"><span data-stu-id="29775-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-to-web-server-through-firewall"></a><span data-ttu-id="29775-189">(允許) 透過防火牆從 Web 到 Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="29775-189">(Allowed) Web to Web Server through Firewall</span></span>
1. <span data-ttu-id="29775-190">網際網路使用者從 FrontEnd001.CloudApp.Net (網際網路面向雲端服務) 要求 HTTP 頁面</span><span class="sxs-lookup"><span data-stu-id="29775-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="29775-191">雲端服務透過連接埠 80 上的開放端點將流量傳遞至 10.0.1.4:80 上的防火牆本機介面</span><span class="sxs-lookup"><span data-stu-id="29775-191">Cloud service passes traffic through open endpoint on port 80 to firewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="29775-192">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="29775-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="29775-193">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="29775-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="29775-194">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="29775-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="29775-195">NSG 規則 3 (網際網路到防火牆) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="29775-195">NSG Rule 3 (Internet to Firewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="29775-196">流量抵達防火牆的內部 IP 位址 (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="29775-196">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="29775-197">防火牆轉送規則會認為此流量是連接埠 80 流量，將它重新導向至 Web 伺服器 IIS01</span><span class="sxs-lookup"><span data-stu-id="29775-197">Firewall forwarding rule see this is port 80 traffic, redirects it to the web server IIS01</span></span>
6. <span data-ttu-id="29775-198">IIS01 正在接聽 Web 流量，接收此要求並開始處理要求</span><span class="sxs-lookup"><span data-stu-id="29775-198">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
7. <span data-ttu-id="29775-199">IIS01 向 AppVM01 上的 SQL Server 要求資訊</span><span class="sxs-lookup"><span data-stu-id="29775-199">IIS01 asks the SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="29775-200">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="29775-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="29775-201">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="29775-201">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="29775-202">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="29775-202">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="29775-203">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="29775-203">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="29775-204">NSG 規則 3 (網際網路到防火牆) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="29775-204">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="29775-205">NSG 規則 4 (IIS01 到 AppVM01) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="29775-205">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="29775-206">AppVM01 接收 SQL 查詢並回應</span><span class="sxs-lookup"><span data-stu-id="29775-206">AppVM01 receives the SQL Query and responds</span></span>
11. <span data-ttu-id="29775-207">Backend 子網路上沒有輸出規則，所以允許回應</span><span class="sxs-lookup"><span data-stu-id="29775-207">Since there are no outbound rules on the Backend subnet the response is allowed</span></span>
12. <span data-ttu-id="29775-208">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="29775-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="29775-209">Backend 子網路到 Frontend 子網路的輸入流量沒有適用的 NSG 規則，因此不會套用任何 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="29775-209">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="29775-210">允許子網路間流量的預設系統規則會允許此流量，因此允許流量。</span><span class="sxs-lookup"><span data-stu-id="29775-210">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
13. <span data-ttu-id="29775-211">IIS 伺服器接收 SQL 回應、完成 HTTP 回應並傳送給要求者</span><span class="sxs-lookup"><span data-stu-id="29775-211">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span></span>
14. <span data-ttu-id="29775-212">這是來自防火牆的 NAT 工作階段，所以回應目的地 (一開始) 是針對防火牆</span><span class="sxs-lookup"><span data-stu-id="29775-212">Since this is a NAT session from the firewall, the response destination (initially) is for the Firewall</span></span>
15. <span data-ttu-id="29775-213">防火牆接收來自 Web 伺服器的回應，並往回轉送給網際網路使用者</span><span class="sxs-lookup"><span data-stu-id="29775-213">The firewall receives the response from the Web Server and forwards back to the Internet User</span></span>
16. <span data-ttu-id="29775-214">Frontend 子網路上沒有輸出規則，所以允許回應，網際網路使用者會收到要求的網頁。</span><span class="sxs-lookup"><span data-stu-id="29775-214">Since there are no outbound rules on the Frontend subnet the response is allowed, and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-backend"></a><span data-ttu-id="29775-215">(允許) RDP 到 Backend</span><span class="sxs-lookup"><span data-stu-id="29775-215">(Allowed) RDP to Backend</span></span>
1. <span data-ttu-id="29775-216">網際網路上的伺服器管理員在 BackEnd001.CloudApp.Net:xxxxx 上要求 AppVM01 的 RDP 工作階段，其中 xxxxx 是 RDP 到 AppVM01 的隨機指派連接埠號碼 (在 Azure 入口網站上或透過 PowerShell，即可找到指派的連接埠)</span><span class="sxs-lookup"><span data-stu-id="29775-216">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="29775-217">防火牆只在 FrontEnd001.CloudApp.Net 位址上接聽，因此不會與此流量有關聯</span><span class="sxs-lookup"><span data-stu-id="29775-217">Since the Firewall is only listening on the FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="29775-218">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="29775-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="29775-219">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="29775-219">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="29775-220">NSG 規則 2 (RDP) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="29775-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="29775-221">由於沒有輸出規則，會套用預設規則並允許傳回的流量</span><span class="sxs-lookup"><span data-stu-id="29775-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="29775-222">已啟用 RDP 工作階段</span><span class="sxs-lookup"><span data-stu-id="29775-222">RDP session is enabled</span></span>
6. <span data-ttu-id="29775-223">AppVM01 會提示輸入使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="29775-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="29775-224">(允許) DNS 伺服器上的 Web 伺服器 DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="29775-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="29775-225">Web 伺服器 IIS01 需要 www.data.gov 的資料摘要，但需要解析位址。</span><span class="sxs-lookup"><span data-stu-id="29775-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="29775-226">VNet 的網路組態將 DNS01 (Backend 子網路上的 10.0.2.4) 列為主要 DNS 伺服器，IIS01 將 DNS 要求傳送至 DNS01</span><span class="sxs-lookup"><span data-stu-id="29775-226">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="29775-227">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="29775-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="29775-228">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="29775-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="29775-229">NSG 規則 1 (DNS) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="29775-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="29775-230">DNS 伺服器收到要求</span><span class="sxs-lookup"><span data-stu-id="29775-230">DNS server receives the request</span></span>
6. <span data-ttu-id="29775-231">DNS 伺服器沒有快取的位址，並要求網際網路上的根 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="29775-231">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="29775-232">Backend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="29775-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="29775-233">網際網路 DNS 伺服器回應，因為此工作階段是從內部起始，所以允許回應</span><span class="sxs-lookup"><span data-stu-id="29775-233">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="29775-234">DNS 伺服器快取回應，然後將初始要求回應到 IIS01</span><span class="sxs-lookup"><span data-stu-id="29775-234">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="29775-235">Backend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="29775-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="29775-236">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="29775-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="29775-237">Backend 子網路到 Frontend 子網路的輸入流量沒有適用的 NSG 規則，因此不會套用任何 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="29775-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="29775-238">允許子網路間流量的預設系統規則會允許此流量，因此允許流量</span><span class="sxs-lookup"><span data-stu-id="29775-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="29775-239">IIS01 從 DNS01 接收回應</span><span class="sxs-lookup"><span data-stu-id="29775-239">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="29775-240">(允許) Web 伺服器存取 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="29775-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="29775-241">IIS01 要求 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="29775-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="29775-242">Frontend 子網路上沒有輸出規則，允許流量</span><span class="sxs-lookup"><span data-stu-id="29775-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="29775-243">Backend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="29775-243">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="29775-244">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="29775-244">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="29775-245">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="29775-245">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="29775-246">NSG 規則 3 (網際網路到防火牆) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="29775-246">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="29775-247">NSG 規則 4 (IIS01 到 AppVM01) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="29775-247">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="29775-248">AppVM01 接收要求並以檔案回應 (假設已獲得存取授權)</span><span class="sxs-lookup"><span data-stu-id="29775-248">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="29775-249">Backend 子網路上沒有輸出規則，所以允許回應</span><span class="sxs-lookup"><span data-stu-id="29775-249">Since there are no outbound rules on the Backend subnet the response is allowed</span></span>
6. <span data-ttu-id="29775-250">Frontend 子網路開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="29775-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="29775-251">Backend 子網路到 Frontend 子網路的輸入流量沒有適用的 NSG 規則，因此不會套用任何 NSG 規則</span><span class="sxs-lookup"><span data-stu-id="29775-251">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
   2. <span data-ttu-id="29775-252">允許子網路間流量的預設系統規則會允許此流量，因此允許流量。</span><span class="sxs-lookup"><span data-stu-id="29775-252">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="29775-253">IIS 伺服器接收檔案</span><span class="sxs-lookup"><span data-stu-id="29775-253">The IIS server receives the file</span></span>

#### <a name="denied-web-direct-to-web-server"></a><span data-ttu-id="29775-254">(拒絕) Web 直接到 Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="29775-254">(Denied) Web direct to Web Server</span></span>
<span data-ttu-id="29775-255">Web 伺服器、IIS01 和防火牆都在相同的雲端服務中，因此共用相同的公開 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="29775-255">Since the Web Server, IIS01, and the Firewall are in the same Cloud Service they share the same public facing IP address.</span></span> <span data-ttu-id="29775-256">因此，HTTP 流量皆會導向至防火牆。</span><span class="sxs-lookup"><span data-stu-id="29775-256">Thus any HTTP traffic would be directed to the firewall.</span></span> <span data-ttu-id="29775-257">雖然可成功服務要求，但要求不能直接前往 Web 伺服器，依設計它會先傳遞通過防火牆。</span><span class="sxs-lookup"><span data-stu-id="29775-257">While the request would be successfully served, it cannot go directly to the Web Server, it passed, as designed, through the Firewall first.</span></span> <span data-ttu-id="29775-258">請參閱本節第一個案例中的流量。</span><span class="sxs-lookup"><span data-stu-id="29775-258">See the first Scenario in this section for the traffic flow.</span></span>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="29775-259">(拒絕) Web 到 Backend 伺服器</span><span class="sxs-lookup"><span data-stu-id="29775-259">(Denied) Web to Backend Server</span></span>
1. <span data-ttu-id="29775-260">網際網路使用者嘗試透過 BackEnd001.CloudApp.Net 服務存取 AppVM01 上的檔案</span><span class="sxs-lookup"><span data-stu-id="29775-260">Internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="29775-261">因為沒有用於檔案共用的開放端點，此流量不會通過雲端服務到達伺服器</span><span class="sxs-lookup"><span data-stu-id="29775-261">Since there are no endpoints open for file share, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="29775-262">如果基於某些原因而開放端點，NSG 規則 5 (網際網路到 VNet) 會封鎖此流量</span><span class="sxs-lookup"><span data-stu-id="29775-262">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="29775-263">(拒絕) DNS 伺服器上的 Web DNS 查閱</span><span class="sxs-lookup"><span data-stu-id="29775-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="29775-264">網際網路使用者嘗試透過 BackEnd001.CloudApp.Net 服務查閱 DNS01 上的內部 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="29775-264">Internet user tries to lookup an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="29775-265">因為沒有用於 DNS 的開放端點，此流量不會通過雲端服務到達伺服器</span><span class="sxs-lookup"><span data-stu-id="29775-265">Since there are no endpoints open for DNS, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="29775-266">如果基於某些原因而開放端點，NSG 規則 5 (網際網路到 VNet) 會封鎖此流量 (注意：有兩個原因導致規則 1 (DNS) 不適用，首先，來源位址是網際網路，此規則只適用於以本機 VNet 做為來源，再者，這是允許規則，所以它永遠不會拒絕流量)</span><span class="sxs-lookup"><span data-stu-id="29775-266">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-to-sql-access-through-firewall"></a><span data-ttu-id="29775-267">(拒絕) Web 透過防火牆對 SQL 進行存取</span><span class="sxs-lookup"><span data-stu-id="29775-267">(Denied) Web to SQL access through Firewall</span></span>
1. <span data-ttu-id="29775-268">網際網路使用者從 FrontEnd001.CloudApp.Net (網際網路面向雲端服務) 要求 SQL 資料</span><span class="sxs-lookup"><span data-stu-id="29775-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="29775-269">因為沒有用於 SQL 的開放端點，此流量不會通過雲端服務到達防火牆</span><span class="sxs-lookup"><span data-stu-id="29775-269">Since there are no endpoints open for SQL, this would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="29775-270">如果基於某些原因而開放端點，Frontend 子網路會開始處理輸入規則：</span><span class="sxs-lookup"><span data-stu-id="29775-270">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="29775-271">NSG 規則 1 (DNS) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="29775-271">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="29775-272">NSG 規則 2 (RDP) 不適用，移至下一個規則</span><span class="sxs-lookup"><span data-stu-id="29775-272">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="29775-273">NSG 規則 3 (網際網路到防火牆) 適用，允許流量，停止處理規則</span><span class="sxs-lookup"><span data-stu-id="29775-273">NSG Rule 2 (Internet to Firewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="29775-274">流量抵達防火牆的內部 IP 位址 (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="29775-274">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="29775-275">防火牆沒有 SQL 的轉送規則，因此捨棄流量</span><span class="sxs-lookup"><span data-stu-id="29775-275">Firewall has no forwarding rules for SQL and drops the traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="29775-276">結論</span><span class="sxs-lookup"><span data-stu-id="29775-276">Conclusion</span></span>
<span data-ttu-id="29775-277">這種使用防火牆保護應用程式並隔離後端子網路與輸入流量的方式相當直接簡單。</span><span class="sxs-lookup"><span data-stu-id="29775-277">This is a relatively straight forward way of protecting your application with a firewall and isolating the back end subnet from inbound traffic.</span></span>

<span data-ttu-id="29775-278">您可以在[這裡][HOME]找到更多範例和網路安全性界限的概觀。</span><span class="sxs-lookup"><span data-stu-id="29775-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="29775-279">參考</span><span class="sxs-lookup"><span data-stu-id="29775-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="29775-280">主要的指令碼和網路組態</span><span class="sxs-lookup"><span data-stu-id="29775-280">Main Script and Network Config</span></span>
<span data-ttu-id="29775-281">將完整指令碼儲存在 PowerShell 指令碼檔案中。</span><span class="sxs-lookup"><span data-stu-id="29775-281">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="29775-282">將網路組態儲存到名為 “NetworkConf2.xml” 的檔案。</span><span class="sxs-lookup"><span data-stu-id="29775-282">Save the Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="29775-283">視需要修改使用者定義的變數。</span><span class="sxs-lookup"><span data-stu-id="29775-283">Modify the user defined variables as needed.</span></span> <span data-ttu-id="29775-284">執行指令碼，然後依照上面的防火牆規則設定指示進行。</span><span class="sxs-lookup"><span data-stu-id="29775-284">Run the script, then follow the Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="29775-285">完整指令碼</span><span class="sxs-lookup"><span data-stu-id="29775-285">Full Script</span></span>
<span data-ttu-id="29775-286">根據使用者定義的變數，此指令碼會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="29775-286">This script will, based on the user defined variables:</span></span>

1. <span data-ttu-id="29775-287">連線到 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="29775-287">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="29775-288">建立新的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="29775-288">Create a new storage account</span></span>
3. <span data-ttu-id="29775-289">依網路組態檔中的定義建立新的 VNet 和兩個子網路</span><span class="sxs-lookup"><span data-stu-id="29775-289">Create a new VNet and two subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="29775-290">建置 4 個 Windows Server VM</span><span class="sxs-lookup"><span data-stu-id="29775-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="29775-291">設定 NSG，包括：</span><span class="sxs-lookup"><span data-stu-id="29775-291">Configure NSG including:</span></span>
   * <span data-ttu-id="29775-292">建立 NSG</span><span class="sxs-lookup"><span data-stu-id="29775-292">Creating a NSG</span></span>
   * <span data-ttu-id="29775-293">在其中填入規則</span><span class="sxs-lookup"><span data-stu-id="29775-293">Populating it with rules</span></span>
   * <span data-ttu-id="29775-294">將 NSG 繫結至適當的子網路</span><span class="sxs-lookup"><span data-stu-id="29775-294">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="29775-295">此 PowerShell 指令碼應該在連線到網際網路的電腦或伺服器上本機執行。</span><span class="sxs-lookup"><span data-stu-id="29775-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29775-296">此指令碼在執行時，PowerShell 中可能會跳出警告或其他參考訊息。</span><span class="sxs-lookup"><span data-stu-id="29775-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="29775-297">只有紅色字體的錯誤訊息才需要擔心。</span><span class="sxs-lookup"><span data-stu-id="29775-297">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on the FrontEnd Subnet (plus the NVA on the FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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

    # User Defined Global Variables
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
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: To ensure proper NSG Rule creation later in this script:
        #       - The Web Server must be VM 1
        #       - The AppVM1 Server must be VM 2
        #       - The DNS server must be VM 4
        #
        #       Otherwise the NSG rules in the last section of this
        #       script will need to be changed to match the modified
        #       VM array numbers ($i) so the NSG Rule IP addresses
        #       are aligned to the associated VM IP addresses.

        # VM 0 - The Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - The Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - The First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - The Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - The DNS Server
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
    Else { Write-Host "The network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation varible is correct and the netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see the above messages for more information." -ForegroundColor Red
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
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all the EndPoints we'll need once we're up and running
                # Note: Web traffic goes through the firewall, so we'll need to set up a HTTP endpoint.
                #       Also, the firewall will be redirecting web traffic to a new IP and Port in a
                #       forwarding rule, so the HTTP endpoint here will have the same public and local
                #       port and the firewall will do the NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when the appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

      # Build the NSG
        Write-Host "Building the NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) to $($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on the IIS Server)
      # Install Backend resource (Run Post-Build Script on the AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="29775-298">網路組態檔</span><span class="sxs-lookup"><span data-stu-id="29775-298">Network Config File</span></span>
<span data-ttu-id="29775-299">以更新的位置儲存此 xml 檔案，並將此檔案的連結加入到上述指令碼中的 $NetworkConfigFile 變數。</span><span class="sxs-lookup"><span data-stu-id="29775-299">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="29775-300">範例應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="29775-300">Sample Application Scripts</span></span>
<span data-ttu-id="29775-301">如果您想要為此範例和其他 DMZ 範例安裝範例應用程式，下列連結中有提供一個：[範例應用程式指令碼][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="29775-301">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
<span data-ttu-id="29775-302">[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "具有 NSG 的輸入 DMZ"</span><span class="sxs-lookup"><span data-stu-id="29775-302">[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Inbound DMZ with NSG"</span></span>
<span data-ttu-id="29775-303">[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "目的地 NAT 圖示"</span><span class="sxs-lookup"><span data-stu-id="29775-303">[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Destination NAT Icon"</span></span>
<span data-ttu-id="29775-304">[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "防火牆規則"</span><span class="sxs-lookup"><span data-stu-id="29775-304">[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Firewall Rule"</span></span>
<span data-ttu-id="29775-305">[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "防火牆規則啟用"</span><span class="sxs-lookup"><span data-stu-id="29775-305">[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Firewall Rule Activation"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
