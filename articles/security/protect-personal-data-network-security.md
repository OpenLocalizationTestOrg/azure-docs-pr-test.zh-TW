---
title: "aaaProtect 個人資料與 Azure 網路的安全性功能 |Microsoft 文件"
description: "使用 Azure 網路安全性功能來保護個人資料"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: be112a9408d327ccedf871656afe800fc7f775e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a><span data-ttu-id="7ea8c-103">使用網路安全性功能來保護個人資料：Azure 應用程式閘道和網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="7ea8c-103">Protect personal data with network security features: Azure Application Gateway and Network Security Groups</span></span>

<span data-ttu-id="7ea8c-104">本文章提供資訊和程序，可協助您使用 Azure 應用程式閘道和網路安全性群組 tooprotect 個人資料。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-104">This article provides information and procedures that will help you use Azure Application Gateway and Network Security Groups tooprotect personal data.</span></span>

<span data-ttu-id="7ea8c-105">個人資料的多層式的安全性策略 tooprotect hello 隱私權的重要元素是防禦機制以防止 SQL 資料隱碼或跨網站指令碼，例如通用的弱點可能會惡意探索。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-105">An important element in a multi-layered security strategy tooprotect hello privacy of personal data is a defense against common vulnerability exploits such as SQL injection or cross-site scripting.</span></span> <span data-ttu-id="7ea8c-106">保持超出 Azure 虛擬網路的不必要的網路流量可協助防止潛在的敏感資料和 Microsoft Azure 提供您工具 toohelp 保護資料，避免攻擊者危害。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-106">Keeping unwanted network traffic out of your Azure virtual network helps protect against potential compromise of sensitive data, and Microsoft Azure gives you tools toohelp protect your data against attackers.</span></span>

## <a name="scenario"></a><span data-ttu-id="7ea8c-107">案例</span><span class="sxs-lookup"><span data-stu-id="7ea8c-107">Scenario</span></span>

<span data-ttu-id="7ea8c-108">大型出航公司搬遷後 hello 美國，展開在 hello 地中海、 Adriatic，與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="7ea8c-109">中的努力 furtherance，它取得數個較小海上行位於義大利、 德國、 丹麥和 hello 英國</span><span class="sxs-lookup"><span data-stu-id="7ea8c-109">In furtherance of those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="7ea8c-110">hello 公司使用 Microsoft Azure 雲端 toostore hello 中的公司資料，然後處理和存取這項資料的虛擬機器上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-110">hello company uses Microsoft Azure toostore corporate data in hello cloud and run applications on virtual machines that process and access this data.</span></span> <span data-ttu-id="7ea8c-111">此資料包含其全球客戶群的名稱、地址、電話號碼和信用卡資訊等個人識別資訊。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-111">This data includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="7ea8c-112">它也會包含在所有位置的傳統的人力資源資訊，例如地址、 電話號碼、 稅務識別碼和醫療公司員工的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-112">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="7ea8c-113">hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫，其中包含與目前和過去的客戶的個人資訊 tootrack 關聯性。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="7ea8c-114">從 hello 公司遠端辦公室和位於 hello 世界各地的旅遊代理程式的公司員工存取 hello 網路擁有存取 toosome 公司資源，並使用 web 應用程式裝載於 Azure Vm toointeract 與它。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-114">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources and use web-based applications hosted in Azure VMs toointeract with it.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="7ea8c-115">問題陳述</span><span class="sxs-lookup"><span data-stu-id="7ea8c-115">Problem statement</span></span>

<span data-ttu-id="7ea8c-116">hello 公司必須保護客戶的 hello 隱私權和員工的個人資料，避免攻擊者利用軟體弱點 toorun 惡意程式碼，可能會公開的個人資料儲存或 hello 公司以雲端為基礎的應用程式所使用。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-116">hello company must protect hello privacy of customers’ and employees’ personal data from attackers who exploit software vulnerabilities toorun malicious code that could expose personal data stored or used by hello company’s cloud-based applications.</span></span>

## <a name="company-goal"></a><span data-ttu-id="7ea8c-117">公司目標</span><span class="sxs-lookup"><span data-stu-id="7ea8c-117">Company goal</span></span>

<span data-ttu-id="7ea8c-118">hello 公司的目標 tooensure 未經授權的人員無法存取公司的 Azure 虛擬網路和 hello 應用程式和資料位於那里利用高畫質視訊常見弱點。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-118">hello company’s goal tooensure that unauthorized persons cannot access corporate Azure Virtual Networks and hello applications and data that reside there by exploiting common vulnerabilities.</span></span> 

## <a name="solutions"></a><span data-ttu-id="7ea8c-119">解決方案</span><span class="sxs-lookup"><span data-stu-id="7ea8c-119">Solutions</span></span>

<span data-ttu-id="7ea8c-120">Microsoft Azure 提供的安全性機制 toohelp 防止垃圾的流量進入 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-120">Microsoft Azure provides security mechanisms toohelp prevent unwanted traffic from entering Azure Virtual Networks.</span></span> <span data-ttu-id="7ea8c-121">輸入和輸出流量的控制傳統上是由防火牆執行。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-121">Control of inbound and outbound traffic is traditionally performed by firewalls.</span></span> <span data-ttu-id="7ea8c-122">在 Azure 中，您可以使用 hello 應用程式閘道以 hello Web 應用程式防火牆和網路安全性群組 (NSG) 做為簡單的分散式防火牆。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-122">In Azure, you can use hello Application Gateway with hello Web Application Firewall and Network Security Groups (NSG), which act as a simple distributed firewall.</span></span> <span data-ttu-id="7ea8c-123">這些工具讓您 toodetect，而且封鎖不想要的網路流量。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-123">These tools enable you toodetect and block unwanted network traffic.</span></span>

### <a name="application-gatewayweb-application-firewall"></a><span data-ttu-id="7ea8c-124">應用程式閘道/Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="7ea8c-124">Application Gateway/Web Application Firewall</span></span>

<span data-ttu-id="7ea8c-125">hello [Web 應用程式防火牆](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)(WAF) 元件的 hello [Azure 應用程式閘道](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction)保護 web 應用程式，也就是越來越多的常見的已知惡意攻擊的目標弱點。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-125">hello [Web Application Firewall](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) (WAF) component of hello [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) protects web applications, which are increasingly targets of malicious attacks that exploit common known vulnerabilities.</span></span> <span data-ttu-id="7ea8c-126">集中式 WAF 可以防禦 Web 攻擊並簡化安全性管理，而不需要變更任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-126">A centralized WAF both protects against web attacks and simplifies security management without requiring any application changes.</span></span>

<span data-ttu-id="7ea8c-127">Azure WAF 可處理各種攻擊類別，包括 SQL 插入、跨網站指令碼、HTTP 通訊協定違規和異常、Bot、編目程式、掃描程式、常見應用程式錯誤設定、HTTP 阻絕服務，以及其他常見的攻擊，例如命令插入、HTTP 要求、走私、HTTP 回應分割及遠端檔案包含攻擊。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-127">Azure WAF addresses various attack categories including SQL injection, cross site scripting, HTTP protocol violations and anomalies, bots, crawlers, scanners, common application misconfigurations, HTTP Denial of Service, and other common attacks such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attacks.</span></span> 

<span data-ttu-id="7ea8c-128">您可以使用 WAF，建立應用程式閘道，或新增 WAF tooan 現有應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-128">You can create an application gateway with WAF, or add WAF tooan existing application gateway.</span></span> <span data-ttu-id="7ea8c-129">在上述任何情況下，Azure 應用程式閘道都需要有自己的子網路。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-129">In either case, Azure Application Gateway requires its own subnet.</span></span>

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a><span data-ttu-id="7ea8c-130">如何建立具有 WAF 的應用程式閘道？</span><span class="sxs-lookup"><span data-stu-id="7ea8c-130">How do I create an application gateway with WAF?</span></span> 

<span data-ttu-id="7ea8c-131">toocreate WAF 啟用，與新的應用程式閘道 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="7ea8c-131">toocreate a new application gateway with WAF enabled, do hello following:</span></span>

1. <span data-ttu-id="7ea8c-132">Hello 和 toohello Azure 入口網站中的記錄檔**我的最愛**窗格中的 hello 入口網站中，按一下 **新增**</span><span class="sxs-lookup"><span data-stu-id="7ea8c-132">Log in toohello Azure portal and in hello **Favorites** pane of hello portal, click **New**</span></span>

2. <span data-ttu-id="7ea8c-133">在 hello**新增**刀鋒視窗中，按一下 **網路**。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-133">In hello **New** blade, click **Networking**.</span></span>

3. <span data-ttu-id="7ea8c-134">按一下 [應用程式閘道]。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-134">Click **Application Gateway**.</span></span>

4. <span data-ttu-id="7ea8c-135">瀏覽 toohello Azure 入口網站**按一下 新增\>網路\>應用程式閘道。**</span><span class="sxs-lookup"><span data-stu-id="7ea8c-135">Navigate toohello Azure portal, **click New \> Networking \> Application Gateway.**</span></span>

   ![建立應用程式閘道](media/protect-netsec/app-gateway-01.png)

5. <span data-ttu-id="7ea8c-137">在 hello**基本概念**刀鋒視窗中，輸入下列欄位的 hello hello 值： 名稱、 層 （Standard 或 WAF） SKU 大小 （小、 中或大） 執行個體計數 (提供高可用性 2)、 訂用帳戶資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-137">In hello **Basics** blade that appears, enter hello values for hello following fields: Name, Tier (Standard or WAF), SKU size (Small, Medium, or Large),  Instance count (2 for high availability), Subscription, Resource group, and Location.</span></span>

6. <span data-ttu-id="7ea8c-138">在 hello**設定**刀鋒視窗中出現在下方**虛擬網路**，按一下 **選擇虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-138">In hello **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="7ea8c-139">此步驟會開啟輸入 hello 刀鋒視窗中選擇虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-139">This step opens enter hello Choose virtual network blade.</span></span>

7. <span data-ttu-id="7ea8c-140">按一下**建立新**tooopen hello**建立虛擬網路**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-140">Click **Create new** tooopen hello **Create virtual network** blade.</span></span>

8. <span data-ttu-id="7ea8c-141">輸入下列值的 hello： 名稱、 位址空間、 子網路名稱、 子網路位址範圍。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-141">Enter hello following values: Name, Address space, Subnet name, Subnet address range.</span></span> <span data-ttu-id="7ea8c-142">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-142">Click **OK**.</span></span>

9. <span data-ttu-id="7ea8c-143">在 hello**設定**刀鋒視窗底下**前端 IP 組態**，選擇 hello IP 位址類型。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-143">On hello **Settings** blade under **Frontend IP configuration**, choose hello IP address type.</span></span>

10. <span data-ttu-id="7ea8c-144">依序按一下 [選擇公用 IP 位址] 和 [新建]。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-144">Click **Choose a public IP address,** then **Create new.**</span></span>

11. <span data-ttu-id="7ea8c-145">接受 hello 預設值，然後按一下  **確定。**</span><span class="sxs-lookup"><span data-stu-id="7ea8c-145">Accept hello default value, and click **OK.**</span></span>

12. <span data-ttu-id="7ea8c-146">在 hello**設定**刀鋒視窗底下**接聽程式組態**，選取 HTTP 或 HTTPS 之下 toouse**通訊協定**。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-146">On hello **Settings** blade under **Listener configuration**, select toouse HTTP or HTTPS under **Protocol**.</span></span> <span data-ttu-id="7ea8c-147">toouse HTTPS，需要憑證。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-147">toouse HTTPS, a certificate is required.</span></span>

13. <span data-ttu-id="7ea8c-148">設定 hello WAF 特定的設定：**防火牆狀態**(**啟用**) 和**防火牆模式**(**防止**)。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-148">Configure hello WAF specific settings: **Firewall status** (**Enabled**) and **Firewall mode** (**Prevention**).</span></span> <span data-ttu-id="7ea8c-149">如果您選擇**偵測**做為 hello 模式流量只會記錄。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-149">If you choose **Detection** as hello mode, traffic is only logged.</span></span>

14. <span data-ttu-id="7ea8c-150">檢閱 hello**摘要**頁面上，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-150">Review hello **Summary** page and click **OK**.</span></span> <span data-ttu-id="7ea8c-151">現在 hello 應用程式閘道會排入佇列，並建立。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-151">Now hello application gateway is queued up and created.</span></span>

<span data-ttu-id="7ea8c-152">建立 hello 應用程式閘道後，您可以瀏覽 tooit hello 入口網站中的，並繼續 hello 應用程式閘道的組態。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-152">After hello application gateway has been created, you can navigate tooit in hello portal and continue configuration of hello application gateway.</span></span>

![建立應用程式閘道](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-tooan-existing-application"></a><span data-ttu-id="7ea8c-154">如何新增 WAF tooan 現有的應用程式？</span><span class="sxs-lookup"><span data-stu-id="7ea8c-154">How do I add WAF tooan existing application?</span></span>

<span data-ttu-id="7ea8c-155">tooupdate 現有的應用程式閘道 toosupport WAF 防止模式中 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="7ea8c-155">tooupdate an existing application gateway toosupport WAF in prevention mode, do hello following:</span></span>

1. <span data-ttu-id="7ea8c-156">在 [hello Azure 入口網站中**我的最愛**] 窗格中，按一下**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-156">In hello Azure portal **Favorites** pane, click **All resources**.</span></span>

2. <span data-ttu-id="7ea8c-157">按一下 hello hello 中的現有應用程式閘道**所有資源**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-157">Click hello existing Application Gateway in hello **All resources** blade.</span></span> 
>[!NOTE]
<span data-ttu-id="7ea8c-158">注意： 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入 hello 名稱 hello 篩選器中依名稱...</span><span class="sxs-lookup"><span data-stu-id="7ea8c-158">Note: If hello subscription you selected already has several resources in it, you can enter hello name in hello Filter by name…</span></span> <span data-ttu-id="7ea8c-159">方塊 tooeasily 存取 hello DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-159">box tooeasily access hello DNS zone.</span></span>
3. <span data-ttu-id="7ea8c-160">按一下**Web 應用程式防火牆**更新 hello 應用程式閘道的設定：**升級 tooWAF 層**（核取）**防火牆狀態**（啟用）， **防火牆模式**（防止）。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-160">Click **Web application firewall** and update hello application gateway settings: **Upgrade tooWAF Tier** (checked), **Firewall status** (enabled),     **Firewall mode** (Prevention).</span></span> <span data-ttu-id="7ea8c-161">您也需要 tooconfigure hello 規則集，並設定已停用的規則。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-161">You also need tooconfigure hello rule set, and configure disabled rules.</span></span>

<span data-ttu-id="7ea8c-162">如需詳細資訊 toocreate WAF 與新的應用程式閘道以及 tooadd WAF tooan 現有應用程式的閘道，請參閱[建立 web 應用程式防火牆使用 hello 入口網站應用程式閘道。](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)</span><span class="sxs-lookup"><span data-stu-id="7ea8c-162">For more detailed information on how toocreate a new application gateway with WAF and how tooadd WAF tooan existing application gateway, see [Create an application gateway with web application firewall by using hello portal.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)</span></span>

### <a name="network-security-groups"></a><span data-ttu-id="7ea8c-163">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="7ea8c-163">Network Security Groups</span></span>

<span data-ttu-id="7ea8c-164">A[網路安全性群組](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)(NSG) 包含一份可允許或拒絕網路流量 tooresources 太連線安全性規則[Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network/)(VNet)。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-164">A [network security group](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) contains a list of security rules that allow or deny network traffic tooresources connected too[Azure Virtual Networks](https://docs.microsoft.com/azure/virtual-network/) (VNet).</span></span> <span data-ttu-id="7ea8c-165">Nsg 可以是相關聯的 toosubnets 或個別 Vm。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-165">NSGs can be associated toosubnets or individual VMs.</span></span> <span data-ttu-id="7ea8c-166">當 NSG 相關聯的 tooa 子網路，hello 規則適用於 tooall 資源連線的 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-166">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> <span data-ttu-id="7ea8c-167">流量可以進一步限制也關聯 NSG tooa VM 或 nic。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-167">Traffic can further be restricted by also associating an NSG tooa VM or NIC.</span></span>

<span data-ttu-id="7ea8c-168">NSG 包含四個屬性：名稱、地區、資源群組和規則。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-168">NSGs contain four properties: Name, Region, Resource group, and Rules.</span></span>
>[!Note]
<span data-ttu-id="7ea8c-169">雖然 NSG 存在於資源群組中，可能很關聯的 tooresources 在資源群組中，只要 hello 資源屬於 hello 與 hello NSG 的相同 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-169">Although an NSG exists in a resource group, it can be associated tooresources in any resource group, as long as hello resource is part of hello same Azure region as hello NSG.</span></span>

<span data-ttu-id="7ea8c-170">NSG 規則包含 9 個屬性：名稱、通訊協定 (TCP、UDP 或 \*，其中包括 ICMP 以及 UDP 和 TCP)、來源連接埠範圍、目的地連接埠範圍、來源位址前置詞、目的地位址前置詞、方向 (輸入或輸出)、優先順序 (介於 100 與 4096 之間) 和存取類型 (允許或拒絕)。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-170">NSG rules contain nine properties: Name, Protocol (TCP, UDP, or \*, which includes ICMP as well as UDP and TCP), Source port range, Destination port range, Source address prefix, Destination address prefix, Direction (inbound or outbound), Priority (between 100 and 4096) and Access type (allow or deny).</span></span> <span data-ttu-id="7ea8c-171">所有的 Nsg 包含一組可刪除，或您所建立的 hello 規則覆寫預設規則。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-171">All NSGs contain a set of default rules that can be deleted, or overridden by hello rules you create.</span></span>

#### <a name="how-do-i-implement-nsgs"></a><span data-ttu-id="7ea8c-172">如何實作 NSG？</span><span class="sxs-lookup"><span data-stu-id="7ea8c-172">How do I implement NSGs?</span></span>

<span data-ttu-id="7ea8c-173">實作 Nsg 需要計劃，並有幾個設計考量，您需要 tootake 納入考量。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-173">Implementing NSGs requires planning, and there are several design considerations you need tootake into account.</span></span> <span data-ttu-id="7ea8c-174">其中包括每個訂用帳戶和每個 NSG; 規則 Nsg hello 數目的限制VNet 和子網路設計，特殊的規則、 ICMP 流量，具有子網路、 負載平衡器，以及更多層的隔離。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-174">These include limits on hello number of NSGs per subscription and rules per NSG; VNet and subnet design, special rules, ICMP traffic, isolation of tiers with subnets, load balancers, and more.</span></span>

<span data-ttu-id="7ea8c-175">如需規劃及實作 NSG 的詳細指引以及範例部署案例，請參閱[使用網路安全性群組來篩選網路流量](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-175">For more guidance in planning and implementing NSGs, and a sample deployment scenario, see [Filter network traffic with network security groups.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)</span></span>

#### <a name="how-do-i-create-rules-in-an-nsg"></a><span data-ttu-id="7ea8c-176">如何在 NSG 中建立規則？</span><span class="sxs-lookup"><span data-stu-id="7ea8c-176">How do I create rules in an NSG?</span></span>

<span data-ttu-id="7ea8c-177">toocreate 輸入現有 NSG 中的規則，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="7ea8c-177">toocreate inbound rules in an existing NSG, do hello following:</span></span>

1. <span data-ttu-id="7ea8c-178">依序按一下 [瀏覽] 和 [網路安全性群組]。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-178">Click **Browse**, and then **Network security groups**.</span></span>

2. <span data-ttu-id="7ea8c-179">在 hello Nsg 清單中按一下**NSG 前端**，然後**輸入安全性規則。**</span><span class="sxs-lookup"><span data-stu-id="7ea8c-179">In hello list of NSGs, click **NSG-FrontEnd**, and then **Inbound security rules.**</span></span>

3. <span data-ttu-id="7ea8c-180">在 hello 清單中的連入的安全性規則，按一下 **新增。**</span><span class="sxs-lookup"><span data-stu-id="7ea8c-180">In hello list of Inbound security rules, click **Add.**</span></span>

4. <span data-ttu-id="7ea8c-181">在 hello 下列欄位中輸入 hello 值： 名稱、 優先順序、 來源、 通訊協定、 來源範圍，目的地，目的地連接埠範圍和動作。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-181">Enter hello values in hello following fields: Name, Priority, Source, Protocol, Source range, Destination, Destination port range, and Action.</span></span>

<span data-ttu-id="7ea8c-182">幾秒之後，hello 新規則會出現在 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="7ea8c-182">hello new rule will appear in hello NSG after a few seconds.</span></span>

![網路安全性規則](media/protect-netsec/inbound-security.png)

<span data-ttu-id="7ea8c-184">如需 toocreate Nsg 中的子網路，如何建立規則，並與前端和後端的子網路，將 NSG 關聯的詳細指示，請參閱[建立使用 hello Azure 入口網站的網路安全性群組。](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)</span><span class="sxs-lookup"><span data-stu-id="7ea8c-184">For more instructions on how toocreate NSGs in subnets, create rules, and associate an NSG with a front-end and back-end subnet, see [Create network security groups using hello Azure portal.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ea8c-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ea8c-185">Next steps</span></span>

[<span data-ttu-id="7ea8c-186">Azure 網路安全性</span><span class="sxs-lookup"><span data-stu-id="7ea8c-186">Azure Network Security</span></span>](https://azure.microsoft.com/blog/azure-network-security/)

[<span data-ttu-id="7ea8c-187">Azure 網路安全性最佳做法</span><span class="sxs-lookup"><span data-stu-id="7ea8c-187">Azure Network Security Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[<span data-ttu-id="7ea8c-188">取得網路安全性群組的相關資訊</span><span class="sxs-lookup"><span data-stu-id="7ea8c-188">Get information about a network security group</span></span>](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[<span data-ttu-id="7ea8c-189">Web 應用程式防火牆 (WAF)</span><span class="sxs-lookup"><span data-stu-id="7ea8c-189">Web application firewall (WAF)</span></span>](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
