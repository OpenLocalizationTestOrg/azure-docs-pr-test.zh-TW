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
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a>實作具有 App Service 環境的多層式安全性架構。
## <a name="overview"></a>Overview
由於 App Service 環境提供部署至虛擬網路的隔離執行階段環境，因此開發人員能夠建立多層式安全性架構，針對每個實體應用程式層提供不同層級的網路存取。

常見的 desire toohide API 的後端從一般的網際網路存取，並只允許由上游的 web 應用程式呼叫 Api toobe。  [網路安全性群組 (Nsg)] [ NetworkSecurityGroups]可以包含應用程式服務環境 toorestrict 公用存取 tooAPI 應用程式的子網路上使用。

hello 圖顯示在 App Service 環境上部署的基礎 WebAPI 應用程式的範例架構。  三個不同的 web 應用程式部署執行個體，在三個個別應用程式服務環境，讓後端呼叫 toohello 相同 WebAPI 應用程式。

![概念性架構][ConceptualArchitecture] 

hello 綠色加號表示該 hello 網路安全性群組，其中包含 「 apiase"hello 子網路上的允許輸入的電話 hello 從上游的 web 應用程式，以及呼叫其本身。  不過 hello 相同的網路安全性群組明確拒絕存取 toogeneral 輸入從 hello 網際網路的流量。 

hello 本主題其餘部分會包含"apiase"hello 子網路上逐步 hello 步驟所需的 tooconfigure hello 網路安全性群組。

## <a name="determining-hello-network-behavior"></a>判斷 hello 網路的行為
在訂單 tooknow 網路安全性規則所需，您需要的 toodetermine tooreach hello App Service 環境包含 hello API 應用程式，以及哪些用戶端將會封鎖，將允許哪些網路用戶端。

因為[網路安全性群組 (Nsg)] [ NetworkSecurityGroups]套用的 toosubnets，而且應用程式服務環境部署至子網路，NSG 中所含的 hello 規則套用太**所有**App Service 環境上執行的應用程式。  相同設定的安全性規則套用的 toohello 包含"apiase，"hello"apiase"hello 將受保護的 App Service 環境上執行的所有應用程式的子網路的網路安全性群組之後，如本文中，使用 hello 範例架構。 

* **判斷上游的呼叫端的 hello 輸出 IP 位址：** hello IP 位址或位址的 hello 上游的呼叫端是什麼？  這些位址必須 toobe hello NSG 中明確允許必要的可存取。  由於應用程式服務環境之間的呼叫會被視為 「 網際網路 」 呼叫，因此 hello 輸出 IP 位址指派 tooeach 的 hello 三個上游應用程式服務環境的需求 toobe hello NSG hello"apiase 「 子網路中允許的存取。   如需詳細資訊，需判斷 hello 輸出的 IP 位址，如 App Service 環境中執行的應用程式，請參閱 hello[網路架構][ NetworkArchitecture]概觀文件。
* **Hello 後端應用程式開發介面應用程式需要 toocall 本身嗎？**  有時候是容易被忽略，而且難以察覺的點狀況下 hello hello 後端應用程式需要 toocall 本身的地方。  如果在 App Service 環境的後端應用程式開發介面應用程式需要 toocall 本身，這也會處理做為 「 網際網路 」 呼叫。  Hello 範例架構中，這需要允許存取的 hello"apiase"App Service 環境以及 hello 輸出 IP 位址。

## <a name="setting-up-hello-network-security-group"></a>設定 hello 網路安全性群組
一旦 hello 設定的已知輸出的 IP 位址，hello 下一個步驟是 tooconstruct 網路安全性群組。  您可以針對以 Resource Manager 為基礎的虛擬網路以及傳統虛擬網路建立網路安全性群組。  hello 以下範例顯示建立及使用 Powershell 在傳統虛擬網路上設定 NSG。

Hello 範例架構，hello 環境位於美國中南部，以便在該區域中建立空白的 nsg 關聯：

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

先明確允許 hello Azure 的管理基礎結構所述 hello 發行項上加入規則[輸入流量][ InboundTraffic]應用程式服務環境中。

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

接下來，兩個規則會加入 tooallow HTTP 和 HTTPS 呼叫 hello 第一個上游 App Service 環境 (「 fe1ase")。

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

確定並重複的 hello 第二個和第三個上游應用程式服務環境 （「 fe2ase"和"fe3ase"）。

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

最後，授與存取 toohello 輸出 IP 位址的 hello 後端 API 的應用程式服務環境，以便讓它可以在回呼至本身。

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

沒有其他的網路安全性規則需要 toobe 預設設定，因為每個 NSG 具有一組區塊從 hello 網際網路對內的存取的預設規則。

hello hello 網路安全性群組中的規則的完整清單如下所示。  請注意如何 hello 最後一個規則，會反白顯示，會封鎖從已被明確被授與存取以外的所有呼叫端的傳入的存取。

![NSG 組態][NSGConfiguration] 

hello 最後一個步驟是 tooapply hello NSG toohello 子網路，其中包含 hello"apiase"App Service 環境。  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

與 hello NSG 套用 toohello 子網路只 hello 三個上游的應用程式服務環境中，hello App Service 環境包含 hello API 後端允許和 toocall hello"apiase 」 環境中。

## <a name="additional-links-and-information"></a>其他連結和資訊
所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。

關於 [網路安全性群組](../virtual-network/virtual-networks-nsg.md)的資訊。 

了解[輸出 IP 位址][NetworkArchitecture]和 App Service 環境。

App Service 環境所使用的[網路連接埠][InboundTraffic]。

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
