---
title: "aaaNetwork 架構概觀的應用程式服務環境"
description: "App Service 環境網路拓撲的架構概觀。"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 13d03a37-1fe2-4e3e-9d57-46dfb330ba52
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 3cbc86883f5687a9ada35a3ab2f577a450a3fa0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-architecture-overview-of-app-service-environments"></a>App Service 環境的網路架構概觀
## <a name="introduction"></a>簡介
子網路內一定會建立應用程式服務環境[虛擬網路][ virtualnetwork] -App Service 環境中執行的應用程式可以與私用通訊端點位於 hello 相同虛擬網路拓撲。  因為客戶可能會鎖定其虛擬網路基礎結構的部分，就會發生的 App Service 環境的網路通訊流程重要 toounderstand hello 類型。

## <a name="general-network-flow"></a>一般網路流程
當 App Service 環境 (ASE) 針對應用程式使用公開虛擬 IP 位址 (VIP) 時，所有傳入的流量都會到達該公用 VIP。  這包括應用程式的 HTTP 和 HTTPS 流量，以及 FTP 的其他流量、遠端偵錯功能和 Azure 管理作業。  如需完整清單的 hello 特定連接埠 （必要和選擇性） 所提供的 hello 公用 VIP 請參閱 hello 文件[控制輸入的流量][ controllinginboundtraffic] tooan App Service 環境。 

應用程式服務環境也支援執行只有 tooa 虛擬網路內部的位址、 繫結的應用程式，也稱為 tooas ILB （內部負載平衡器） 位址。  ILB 上已啟用應用程式，以及遠端的偵錯呼叫 ASE、 HTTP 與 HTTPS 流量到達 hello ILB 位址。  最常見的 ILB ASE 組態 hello ILB 位址也會到達 FTP/FTPS 流量。  但是 Azure 的管理作業仍會流 tooports 454/455 上的 ILB hello 公用 VIP，啟用 ASE。

hello 圖顯示 hello 應用程式的繫結的 tooa 公用虛擬 IP 位址所在的 App Service 環境的 hello 概觀各種輸入和輸出網路流量。

![一般網路流程][GeneralNetworkFlows]

App Service 環境可以與各種私用客戶端點進行通訊。  例如，應用程式正在執行中的 App Service 環境可以連接 toodatabase 伺服器中的 IaaS 虛擬機器上執行的 hello hello 相同虛擬網路拓撲。

> [!IMPORTANT]
> 查看 hello 網路圖表，從 hello App Service 環境的不同子網路中部署 hello 「 其他計算資源 」。 部署資源在 hello hello ASE 與同一個子網路會封鎖從 ASE toothose 資源 （除了特定的內部 ASE 路由） 的連線。 部署 tooa 不同的子網路改用 (在 hello 相同的 VNET)。 hello App Service 環境就會無法 tooconnect。 不需要任何其他設定。
> 
> 

App Service 環境也會與管理和操作 App Service 環境所需的 SQL 資料庫和 Azure 儲存體資源進行通訊。  部分與通訊的 App Service 環境的 hello Sql 和儲存體資源位於 hello 與 hello App Service 環境，而其他人位於遠端的 Azure 區域中相同的區域。  如此一來，輸出連線 toohello 網際網路時一律需要 App Service 環境 toofunction 正確。 

網路安全性群組的子網路，App Service 環境已部署，因為可以使用的 toocontrol 輸入的流量 toohello 子網路。  如需如何 toocontrol 輸入流量 tooan App Service 環境的詳細資訊，請參閱下列資訊 hello[文章][controllinginboundtraffic]。

如需詳細資訊，如何 tooallow 連出網際網路連線從 App Service 環境，請參閱下列文章使用相關的 hello [Express Route][ExpressRoute]。  hello hello 文章所述的相同方式套用時使用站台對站連線能力，並使用強制通道。

## <a name="outbound-network-addresses"></a>輸出網路位址
App Service 環境進行傳出呼叫，IP 位址時，一律與 hello 傳出呼叫相關聯。  hello 特定 IP 位址，可取決於所呼叫的 hello 端點是否位於 hello 虛擬網路拓撲，內外 hello 虛擬網路拓撲。

如果呼叫 hello 端點**外**hello 虛擬網路拓撲，然後 hello 輸出位址 （也稱為 hello 輸出 NAT 位址），可為 hello App Service 環境的 hello 公用 VIP。  這個位址可以找到屬性刀鋒視窗中的 hello App Service 環境的 hello 入口網站使用者介面中。

![輸出 IP 位址][OutboundIPAddress]

此位址也可以判斷只能在 hello App Service 環境中，建立應用程式，然後執行有公開 VIP 的 ASEs *nslookup* hello 應用程式的位址。 hello 結果的 IP 位址是 hello 公用 VIP，以及 hello App Service 環境的輸出 NAT 位址。

如果呼叫 hello 端點**內**hello 虛擬網路拓撲，hello 輸出位址的 hello 呼叫應用程式會執行 hello 應用程式的 hello 個別計算資源 hello 內部 IP 位址。  但是沒有任何虛擬網路內部 IP 位址 tooapps 持續性對應。  應用程式可以移動到不同的計算資源和 hello App Service 環境中的可執行的運算資源集區可以因為 tooscaling 作業變更。

但是，由於 App Service 環境永遠位於子網路內，都保證執行應用程式的計算資源 hello 內部 IP 位址將一定會在 hello CIDR hello 子網路範圍內。  如此一來，當使用更細緻的 Acl 或多個網路安全性群組 toosecure 存取 tooother hello 虛擬網路內的端點，hello 包含 hello App Service 環境的需求 toobe 授與存取權的子網路範圍。

hello 下圖顯示這些概念的更多詳細資料：

![輸出網路位址][OutboundNetworkAddresses]

在上方圖表 hello:

* 由於 hello App Service 環境的 hello 公開 VIP 是 192.23.1.2，，是 hello 輸出的 IP 位址太進行呼叫時，使用 「 網際網路 」 端點。
* hello hello 包含子網路，App Service 環境的 hello CIDR 範圍是 10.0.1.0/26。  其他端點內 hello 相同虛擬網路基礎結構會看到 從應用程式呼叫某處源自於此位址範圍內。

## <a name="calls-between-app-service-environments"></a>App Service 環境之間的呼叫
如果您部署多個應用程式服務環境，可能會發生更複雜的案例在 hello 相同虛擬網路，並進行傳出呼叫從一個 App Service 環境 tooanother App Service 環境。  這些跨 App Service 環境的呼叫也會被視為「網際網路」呼叫。

hello 下列圖表顯示多層式架構與應用程式的範例上一個 App Service 環境 （例如：「 前端 」 web 應用程式) （例如內部後端應用程式開發介面應用程式不適合 toobe 從 hello 網際網路存取） 的第二個應用程式服務環境上呼叫應用程式。 

![App Service 環境之間的呼叫][CallsBetweenAppServiceEnvironments] 

在 hello hello App Service 環境 」 ASE 一個"上述範例會有 192.23.1.2 輸出 IP 位址。  如果在此 App Service 環境上執行的應用程式可讓執行在第二個應用程式服務環境中 ("ASE Two") 位於相同虛擬網路，hello hello 輸出的輸出呼叫 tooan 應用程式會視為呼叫做為 「 網際網路 」 呼叫。  如此一來到達 hello hello 網路流量第二個 App Service 環境將會顯示為來自 192.23.1.2 (也就是 hello 子網路位址範圍的 hello 第一個 App Service 環境)。

即使不同的應用程式服務環境之間的呼叫視為 「 網際網路 」 呼叫，當兩個應用程式服務環境位於相同 Azure 地區 hello 網路流量會保留在 hello 地區的 Azure 網路，而且不會實際傳送的 hello透過 hello 公用網際網路。  如此一來，您可以使用網路安全性群組的 hello hello 子網路上第二個應用程式服務環境 tooonly 允許從進行傳入的呼叫 hello 第一個應用程式服務環境中 （其輸出的 IP 位址是 192.23.1.2），以確保 hello 之間的通訊安全App Service 環境。

## <a name="additional-links-and-information"></a>其他連結和資訊
所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。

詳細資料輸入應用程式服務環境所使用的連接埠會使用網路安全性群組 toocontrol 輸入的流量[這裡][controllinginboundtraffic]。

使用使用者定義的路由 toogrant 傳出網際網路存取 tooApp 服務環境的詳細資訊可在此[文章][ExpressRoute]。 

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[controllinginboundtraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[ExpressRoute]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/

<!-- IMAGES -->
[GeneralNetworkFlows]: ./media/app-service-app-service-environment-network-architecture-overview/NetworkOverview-1.png
[OutboundIPAddress]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundIPAddress-1.png
[OutboundNetworkAddresses]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundNetworkAddresses-1.png
[CallsBetweenAppServiceEnvironments]: ./media/app-service-app-service-environment-network-architecture-overview/CallsBetweenEnvironments-1.png

