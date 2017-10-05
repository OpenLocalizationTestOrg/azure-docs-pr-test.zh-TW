---
title: "具有 App Service 環境的多層式安全性架構"
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
ms.openlocfilehash: 0fb02c13f99a8f4a46e0142c20da3b152c809b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="e076e-103">實作具有 App Service 環境的多層式安全性架構。</span><span class="sxs-lookup"><span data-stu-id="e076e-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="e076e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e076e-104">Overview</span></span>
<span data-ttu-id="e076e-105">由於 App Service 環境提供部署至虛擬網路的隔離執行階段環境，因此開發人員能夠建立多層式安全性架構，針對每個實體應用程式層提供不同層級的網路存取。</span><span class="sxs-lookup"><span data-stu-id="e076e-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="e076e-106">常見的需求之一，是要隱藏對 API 後端的一般網際網路存取，而只允許由上游 Web 應用程式呼叫 API。</span><span class="sxs-lookup"><span data-stu-id="e076e-106">A common desire is to hide API back-ends from general Internet access, and only allow APIs to be called by upstream web apps.</span></span>  <span data-ttu-id="e076e-107">[網路安全性群組 (NSG)][NetworkSecurityGroups] 可用於包含 App Service 環境的子網路，用以限制對 API 應用程式的公用存取。</span><span class="sxs-lookup"><span data-stu-id="e076e-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments to restrict public access to API applications.</span></span>

<span data-ttu-id="e076e-108">下圖顯示的範例架構，具有部署在 App Service 環境上的 WebAPI 型應用程式。</span><span class="sxs-lookup"><span data-stu-id="e076e-108">The diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="e076e-109">三個不同的 Web 應用程式執行個體部署在三個不同的 App Service 環境上，使後端呼叫相同的 WebAPI 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e076e-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls to the same WebAPI app.</span></span>

![概念性架構][ConceptualArchitecture] 

<span data-ttu-id="e076e-111">綠色加號指出包含 "apiase" 之子網路上的網路安全性群組，允許來自於上游 Web 應用程式的傳入呼叫，及其本身的呼叫。</span><span class="sxs-lookup"><span data-stu-id="e076e-111">The green plus signs indicate that the network security group on the subnet containing "apiase" allows inbound calls from the upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="e076e-112">不過，相同的網路安全群組明確拒絕網際網路對一般輸入流量的存取。</span><span class="sxs-lookup"><span data-stu-id="e076e-112">However the same network security group explicitly denies access to general inbound traffic from the Internet.</span></span> 

<span data-ttu-id="e076e-113">此主題的其餘部分將逐步解說在包含 "apiase" 的子網路上設定網路安全群組所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="e076e-113">The remainder of this topic walks through the steps needed to configure the network security group on the subnet containing "apiase".</span></span>

## <a name="determining-the-network-behavior"></a><span data-ttu-id="e076e-114">判斷網路行為</span><span class="sxs-lookup"><span data-stu-id="e076e-114">Determining the Network Behavior</span></span>
<span data-ttu-id="e076e-115">若要知道需要哪些網路安全性規則，您必須判斷哪些網路用戶端將能夠聯繫包含 API 應用程式的 App Service 服務環境，而哪些用戶端將遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="e076e-115">In order to know what network security rules are needed, you need to determine which network clients will be allowed to reach the App Service Environment containing the API app, and which clients will be blocked.</span></span>

<span data-ttu-id="e076e-116">由於[網路安全性群組 (NSG)][NetworkSecurityGroups] 會套用至子網路，而 App Service 環境部署在子網路中，因此 NSG 中包含的規則將會套用至**所有**在 App Service 環境上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e076e-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied to subnets, and App Service Environments are deployed into subnets, the rules contained in an NSG apply to **all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="e076e-117">舊本文的範例架構而言，一旦將網路安全性群組套用至包含 "apiase" 的子網路後，所有在 "apiase" App Service 環境上執行的應用程式都將受到相同安全性規則集的保護。</span><span class="sxs-lookup"><span data-stu-id="e076e-117">Using the sample architecture for this article, once a network security group is applied to the subnet containing "apiase", all apps running on the "apiase" App Service Environment will be protected by the same set of security rules.</span></span> 

* <span data-ttu-id="e076e-118">**判斷上游呼叫端的輸出 IP 位址：**上游呼叫端的 IP 位址為何？</span><span class="sxs-lookup"><span data-stu-id="e076e-118">**Determine the outbound IP address of upstream callers:**  What is the IP address or addresses of the upstream callers?</span></span>  <span data-ttu-id="e076e-119">這些位址在 NSG 中必須明確地允許存取。</span><span class="sxs-lookup"><span data-stu-id="e076e-119">These addresses will need to be explicitly allowed access in the NSG.</span></span>  <span data-ttu-id="e076e-120">由於 App Service 環境之間的呼叫會被視為「網際網路」呼叫，因此這表示指派給這三個上游 App Service 環境的輸出 IP 位址，在 "apiase" 子網路的 NSG 中必須是允許存取的。</span><span class="sxs-lookup"><span data-stu-id="e076e-120">Since calls between App Service Environments are considered "Internet" calls, this means the outbound IP address assigned to each of the three upstream App Service Environments needs to be allowed access in the NSG for the "apiase" subnet.</span></span>   <span data-ttu-id="e076e-121">若想進一步了解如何判斷在 App Service 環境中執行之應用程式的輸出 IP 位址，請參閱[網路架構][NetworkArchitecture]概觀文章。</span><span class="sxs-lookup"><span data-stu-id="e076e-121">For more details on determining the outbound IP address for apps running in an App Service Environment see the [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="e076e-122">**後端 API 應用程式是否需要呼叫本身？**</span><span class="sxs-lookup"><span data-stu-id="e076e-122">**Will the back-end API app need to call itself?**</span></span>  <span data-ttu-id="e076e-123">後端應用程式有時候需要呼叫本身，這是常會被忽略而難以察覺的情況。</span><span class="sxs-lookup"><span data-stu-id="e076e-123">A sometimes overlooked and subtle point is the scenario where the back-end application needs to call itself.</span></span>  <span data-ttu-id="e076e-124">如果 App Service 環境上的後端 API 應用程式需要呼叫本身，我們也會將其視為「網際網路」呼叫。</span><span class="sxs-lookup"><span data-stu-id="e076e-124">If a back-end API application on an App Service Environment needs to call itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="e076e-125">在範例架構中，這必須允許 "apiase" App Service 環境的輸出 IP 位址進行存取。</span><span class="sxs-lookup"><span data-stu-id="e076e-125">In the sample architecture this requires allowing access from the outbound IP address of the "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-the-network-security-group"></a><span data-ttu-id="e076e-126">設定網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="e076e-126">Setting up the Network Security Group</span></span>
<span data-ttu-id="e076e-127">得知輸出 IP 位址集後，下一步是要建構網路安全群組。</span><span class="sxs-lookup"><span data-stu-id="e076e-127">Once the set of outbound IP addresses are known, the next step is to construct a network security group.</span></span>  <span data-ttu-id="e076e-128">您可以針對以 Resource Manager 為基礎的虛擬網路以及傳統虛擬網路建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e076e-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="e076e-129">下列範例說明如何在傳統虛擬網路上使用 Powershell 建立和設定 NSG。</span><span class="sxs-lookup"><span data-stu-id="e076e-129">The examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="e076e-130">在範例架構中，環境位於美國中南部，因此會在該區域中建立空的 NSG：</span><span class="sxs-lookup"><span data-stu-id="e076e-130">For the sample architecture, the environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="e076e-131">首先要為 Azure 管理基礎結構新增明確的允許規則，如 App Service 環境的[輸入流量][InboundTraffic]相關文章所說明。</span><span class="sxs-lookup"><span data-stu-id="e076e-131">First an explicit allow rule is added for the Azure management infrastructure as noted in the article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="e076e-132">接著要新增兩個規則，以允許從第一個上游 App Service 環境 ("fe1ase") 進行 HTTP 和 HTTPS 呼叫。</span><span class="sxs-lookup"><span data-stu-id="e076e-132">Next, two rules are added to allow HTTP and HTTPS calls from the first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access to requests from the first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="e076e-133">為第二個和第三個上游 App Service 環境 ("fe2ase" 和 "fe3ase") 重複相同步驟。</span><span class="sxs-lookup"><span data-stu-id="e076e-133">Rinse and repeat for the second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access to requests from the second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access to requests from the third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="e076e-134">最後，授與後端 API 的 App Service 環境輸出 IP 位址的存取權，使其能夠回呼本身。</span><span class="sxs-lookup"><span data-stu-id="e076e-134">Lastly, grant access to the outbound IP address of the back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on the apiase environment to call back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="e076e-135">無須設定其他網路安全性規則，因為依預設每個 NSG 有一組預設規則會封鎖來自網際網路的輸入存取。</span><span class="sxs-lookup"><span data-stu-id="e076e-135">No other network security rules need to be configured because every NSG has a set of default rules that block inbound access from the Internet by default.</span></span>

<span data-ttu-id="e076e-136">網路安全性群組中的完整規則清單顯示如下。</span><span class="sxs-lookup"><span data-stu-id="e076e-136">The full list of rules in the network security group are shown below.</span></span>  <span data-ttu-id="e076e-137">請留意最後一個規則 (反白顯示) 如何封鎖未被明確授與存取權的所有呼叫端進行的輸入存取。</span><span class="sxs-lookup"><span data-stu-id="e076e-137">Note how the last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![NSG 組態][NSGConfiguration] 

<span data-ttu-id="e076e-139">最後一個步驟是將 NSG 套用至包含 "apiase" App Service 環境的子網路。</span><span class="sxs-lookup"><span data-stu-id="e076e-139">The final step is to apply the NSG to the subnet that contains the "apiase" App Service Environment.</span></span>  

     #Apply the NSG to the backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="e076e-140">NSG 套用至子網路後，將只有三個上游 App Service 環境以及包含 API 後端的 App Service 環境能夠呼叫 "apiase" 環境。</span><span class="sxs-lookup"><span data-stu-id="e076e-140">With the NSG applied to the subnet, only the three upstream App Service Environments, and the App Service Environment containing the API back-end, are allowed to call into the "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="e076e-141">其他連結和資訊</span><span class="sxs-lookup"><span data-stu-id="e076e-141">Additional Links and Information</span></span>
<span data-ttu-id="e076e-142">您可以在 [應用程式服務環境的讀我檔案](../app-service/app-service-app-service-environments-readme.md)中取得 App Service 環境的所有相關文章與做法。</span><span class="sxs-lookup"><span data-stu-id="e076e-142">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="e076e-143">關於 [網路安全性群組](../virtual-network/virtual-networks-nsg.md)的資訊。</span><span class="sxs-lookup"><span data-stu-id="e076e-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="e076e-144">了解[輸出 IP 位址][NetworkArchitecture]和 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="e076e-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="e076e-145">App Service 環境所使用的[網路連接埠][InboundTraffic]。</span><span class="sxs-lookup"><span data-stu-id="e076e-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
