---
title: "aaaLayered 與應用程式服務環境的安全性架構"
description: "實作具有 App Service 環境的多層式安全性架構。"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="5b9d9-103">實作具有 App Service 環境的多層式安全性架構。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="5b9d9-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5b9d9-104">Overview</span></span>
<span data-ttu-id="5b9d9-105">由於 App Service 環境提供部署至虛擬網路的隔離執行階段環境，因此開發人員能夠建立多層式安全性架構，針對每個實體應用程式層提供不同層級的網路存取。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="5b9d9-106">常見的 desire toohide API 的後端從一般的網際網路存取，並只允許由上游的 web 應用程式呼叫 Api toobe。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-106">A common desire is toohide API back-ends from general Internet access, and only allow APIs toobe called by upstream web apps.</span></span>  <span data-ttu-id="5b9d9-107">[網路安全性群組 (Nsg)] [ NetworkSecurityGroups]可以包含應用程式服務環境 toorestrict 公用存取 tooAPI 應用程式的子網路上使用。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments toorestrict public access tooAPI applications.</span></span>

<span data-ttu-id="5b9d9-108">hello 圖顯示在 App Service 環境上部署的基礎 WebAPI 應用程式的範例架構。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-108">hello diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="5b9d9-109">三個不同的 web 應用程式部署執行個體，在三個個別應用程式服務環境，讓後端呼叫 toohello 相同 WebAPI 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls toohello same WebAPI app.</span></span>

![概念性架構][ConceptualArchitecture] 

<span data-ttu-id="5b9d9-111">hello 綠色加號表示該 hello 網路安全性群組，其中包含 「 apiase"hello 子網路上的允許輸入的電話 hello 從上游的 web 應用程式，以及呼叫其本身。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-111">hello green plus signs indicate that hello network security group on hello subnet containing "apiase" allows inbound calls from hello upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="5b9d9-112">不過 hello 相同的網路安全性群組明確拒絕存取 toogeneral 輸入從 hello 網際網路的流量。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-112">However hello same network security group explicitly denies access toogeneral inbound traffic from hello Internet.</span></span> 

<span data-ttu-id="5b9d9-113">hello 本主題其餘部分會包含"apiase"hello 子網路上逐步 hello 步驟所需的 tooconfigure hello 網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-113">hello remainder of this topic walks through hello steps needed tooconfigure hello network security group on hello subnet containing "apiase".</span></span>

## <a name="determining-hello-network-behavior"></a><span data-ttu-id="5b9d9-114">判斷 hello 網路的行為</span><span class="sxs-lookup"><span data-stu-id="5b9d9-114">Determining hello Network Behavior</span></span>
<span data-ttu-id="5b9d9-115">在訂單 tooknow 網路安全性規則所需，您需要的 toodetermine tooreach hello App Service 環境包含 hello API 應用程式，以及哪些用戶端將會封鎖，將允許哪些網路用戶端。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-115">In order tooknow what network security rules are needed, you need toodetermine which network clients will be allowed tooreach hello App Service Environment containing hello API app, and which clients will be blocked.</span></span>

<span data-ttu-id="5b9d9-116">因為[網路安全性群組 (Nsg)] [ NetworkSecurityGroups]套用的 toosubnets，而且應用程式服務環境部署至子網路，NSG 中所含的 hello 規則套用太**所有**App Service 環境上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied toosubnets, and App Service Environments are deployed into subnets, hello rules contained in an NSG apply too**all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="5b9d9-117">相同設定的安全性規則套用的 toohello 包含"apiase，"hello"apiase"hello 將受保護的 App Service 環境上執行的所有應用程式的子網路的網路安全性群組之後，如本文中，使用 hello 範例架構。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-117">Using hello sample architecture for this article, once a network security group is applied toohello subnet containing "apiase", all apps running on hello "apiase" App Service Environment will be protected by hello same set of security rules.</span></span> 

* <span data-ttu-id="5b9d9-118">**判斷上游的呼叫端的 hello 輸出 IP 位址：** hello IP 位址或位址的 hello 上游的呼叫端是什麼？</span><span class="sxs-lookup"><span data-stu-id="5b9d9-118">**Determine hello outbound IP address of upstream callers:**  What is hello IP address or addresses of hello upstream callers?</span></span>  <span data-ttu-id="5b9d9-119">這些位址必須 toobe hello NSG 中明確允許必要的可存取。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-119">These addresses will need toobe explicitly allowed access in hello NSG.</span></span>  <span data-ttu-id="5b9d9-120">由於應用程式服務環境之間的呼叫會被視為 「 網際網路 」 呼叫，因此 hello 輸出 IP 位址指派 tooeach 的 hello 三個上游應用程式服務環境的需求 toobe hello NSG hello"apiase 「 子網路中允許的存取。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-120">Since calls between App Service Environments are considered "Internet" calls, this means hello outbound IP address assigned tooeach of hello three upstream App Service Environments needs toobe allowed access in hello NSG for hello "apiase" subnet.</span></span>   <span data-ttu-id="5b9d9-121">如需詳細資訊，需判斷 hello 輸出的 IP 位址，如 App Service 環境中執行的應用程式，請參閱 hello[網路架構][ NetworkArchitecture]概觀文件。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-121">For more details on determining hello outbound IP address for apps running in an App Service Environment see hello [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="5b9d9-122">**Hello 後端應用程式開發介面應用程式需要 toocall 本身嗎？**</span><span class="sxs-lookup"><span data-stu-id="5b9d9-122">**Will hello back-end API app need toocall itself?**</span></span>  <span data-ttu-id="5b9d9-123">有時候是容易被忽略，而且難以察覺的點狀況下 hello hello 後端應用程式需要 toocall 本身的地方。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-123">A sometimes overlooked and subtle point is hello scenario where hello back-end application needs toocall itself.</span></span>  <span data-ttu-id="5b9d9-124">如果在 App Service 環境的後端應用程式開發介面應用程式需要 toocall 本身，這也會處理做為 「 網際網路 」 呼叫。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-124">If a back-end API application on an App Service Environment needs toocall itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="5b9d9-125">Hello 範例架構中，這需要允許存取的 hello"apiase"App Service 環境以及 hello 輸出 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-125">In hello sample architecture this requires allowing access from hello outbound IP address of hello "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-hello-network-security-group"></a><span data-ttu-id="5b9d9-126">設定 hello 網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="5b9d9-126">Setting up hello Network Security Group</span></span>
<span data-ttu-id="5b9d9-127">一旦 hello 設定的已知輸出的 IP 位址，hello 下一個步驟是 tooconstruct 網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-127">Once hello set of outbound IP addresses are known, hello next step is tooconstruct a network security group.</span></span>  <span data-ttu-id="5b9d9-128">您可以針對以 Resource Manager 為基礎的虛擬網路以及傳統虛擬網路建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="5b9d9-129">hello 以下範例顯示建立及使用 Powershell 在傳統虛擬網路上設定 NSG。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-129">hello examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="5b9d9-130">Hello 範例架構，hello 環境位於美國中南部，以便在該區域中建立空白的 nsg 關聯：</span><span class="sxs-lookup"><span data-stu-id="5b9d9-130">For hello sample architecture, hello environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="5b9d9-131">先明確允許 hello Azure 的管理基礎結構所述 hello 發行項上加入規則[輸入流量][ InboundTraffic]應用程式服務環境中。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-131">First an explicit allow rule is added for hello Azure management infrastructure as noted in hello article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="5b9d9-132">接下來，兩個規則會加入 tooallow HTTP 和 HTTPS 呼叫 hello 第一個上游 App Service 環境 (「 fe1ase")。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-132">Next, two rules are added tooallow HTTP and HTTPS calls from hello first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="5b9d9-133">確定並重複的 hello 第二個和第三個上游應用程式服務環境 （「 fe2ase"和"fe3ase"）。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-133">Rinse and repeat for hello second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="5b9d9-134">最後，授與存取 toohello 輸出 IP 位址的 hello 後端 API 的應用程式服務環境，以便讓它可以在回呼至本身。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-134">Lastly, grant access toohello outbound IP address of hello back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="5b9d9-135">沒有其他的網路安全性規則需要 toobe 預設設定，因為每個 NSG 具有一組區塊從 hello 網際網路對內的存取的預設規則。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-135">No other network security rules need toobe configured because every NSG has a set of default rules that block inbound access from hello Internet by default.</span></span>

<span data-ttu-id="5b9d9-136">hello hello 網路安全性群組中的規則的完整清單如下所示。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-136">hello full list of rules in hello network security group are shown below.</span></span>  <span data-ttu-id="5b9d9-137">請注意如何 hello 最後一個規則，會反白顯示，會封鎖從已被明確被授與存取以外的所有呼叫端的傳入的存取。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-137">Note how hello last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![NSG 組態][NSGConfiguration] 

<span data-ttu-id="5b9d9-139">hello 最後一個步驟是 tooapply hello NSG toohello 子網路，其中包含 hello"apiase"App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-139">hello final step is tooapply hello NSG toohello subnet that contains hello "apiase" App Service Environment.</span></span>  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="5b9d9-140">與 hello NSG 套用 toohello 子網路只 hello 三個上游的應用程式服務環境中，hello App Service 環境包含 hello API 後端允許和 toocall hello"apiase 」 環境中。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-140">With hello NSG applied toohello subnet, only hello three upstream App Service Environments, and hello App Service Environment containing hello API back-end, are allowed toocall into hello "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="5b9d9-141">其他連結和資訊</span><span class="sxs-lookup"><span data-stu-id="5b9d9-141">Additional Links and Information</span></span>
<span data-ttu-id="5b9d9-142">所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-142">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="5b9d9-143">關於 [網路安全性群組](../virtual-network/virtual-networks-nsg.md)的資訊。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="5b9d9-144">了解[輸出 IP 位址][NetworkArchitecture]和 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="5b9d9-145">App Service 環境所使用的[網路連接埠][InboundTraffic]。</span><span class="sxs-lookup"><span data-stu-id="5b9d9-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
