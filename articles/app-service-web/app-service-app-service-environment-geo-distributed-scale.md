---
title: "aaaGeo 分散式應用程式服務環境的小數位數"
description: "了解 toohorizontally 調整與流量管理員和應用程式服務環境中使用地理分散的應用程式的規模。"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: c1b05ca8-3703-4d87-a9ae-819d741787fb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: stefsch
ms.openlocfilehash: 9b441f637d8b7f679b3d83240baf99b8ee57e8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="geo-distributed-scale-with-app-service-environments"></a>App Service 環境的異地分散調整
## <a name="overview"></a>概觀
應用程式案例都會需要極高的小數位數可以超過 hello 計算資源容量可用 tooa 單一部署的應用程式。  例如，投票應用程式、體育活動及電視娛樂活動，都屬於需要極高延展性的案例。 水平向外延展應用程式，具有多個應用程式部署在單一區域中，以及跨區域 toohandle 極端負載需求進行，可以滿足大規模需求。

App Service 環境是水平相應放大的理想平台。一旦選取 App Service 環境設定，可支援已知的要求速率，開發人員可以部署其他應用程式服務環境中 「 cookie 裁切器 」 的方式 tooattain 所需的尖峰負載容量。

例如假設 App Service 環境組態上所執行的應用程式已經過測試的 toohandle 20k 每秒要求數 (RPS)。  如果 hello 所需的尖峰負載容量是 100k RPS、 然後可以建立五 （5） 應用程式服務環境以及設定的 tooensure hello 應用程式可以處理 hello 預計的負載上限。

因為客戶通常存取使用自訂 （或虛名） 網域，開發人員需要應用程式的方式 toodistribute 應用程式會透過 hello App Service 環境的執行個體的所有要求。  這是很好的方法 tooaccomplish tooresolve hello 自訂網域使用[Azure 流量管理員設定檔][AzureTrafficManagerProfile]。  hello Traffic Manager 設定檔可在所有的設定的 toopoint hello 個別的應用程式服務環境。  Traffic Manager 將會自動處理在所有應用程式服務環境根據 hello 負載平衡設定 hello Traffic Manager 設定檔中的 hello 分散的客戶。  這個方法適用於無論 hello 應用程式服務環境的所有會部署在單一 Azure 區域中，或是部署到多個 Azure 區域在全球各地。

此外，由於客戶透過 hello 虛名網域存取應用程式，客戶不知道執行應用程式的應用程式服務環境的 hello 數量。  因此，開發人員可以根據觀察到的流量負載，快速且輕鬆地新增和移除 App Service 環境。

hello 下的概念圖描繪在單一區域內的三個應用程式服務環境水平延展的應用程式。

![概念性架構][ConceptualArchitecture] 

hello 本主題剩下的逐步解說設定使用多個應用程式服務環境的 hello 範例應用程式在分散式拓撲所需的 hello 步驟。

## <a name="planning-hello-topology"></a>規劃 hello 拓樸
建立分散式應用程式使用量時之前, 它有助於 toohave 事先少數的片段資訊。

* **Hello 應用程式的自訂網域：** hello 客戶將會使用 tooaccess hello 應用程式的自訂網域名稱為何？  Hello 範例應用程式 hello 自訂網域名稱是*www.scalableasedemo.com*
* **Traffic Manager 網域：**網域名稱必須選擇建立時的 toobe [Azure 流量管理員設定檔][AzureTrafficManagerProfile]。  此名稱將會結合 hello *trafficmanager.net*尾碼 tooregister Traffic Manager 所管理的網域項目。  Hello 範例應用程式中，為 hello 名稱選擇*可擴充 ase 示範*。  如此一來 hello Traffic Manager 所管理的完整網域名稱是*可擴充 ase demo.trafficmanager.net*。
* **縮放比例 hello 應用程式使用量的策略：**將 hello 應用程式使用量會分佈在單一區域中的多個應用程式服務環境嗎？  多個區域嗎？  兩種方法混合搭配使用嗎？  hello 決策應該根據預期客戶流量將產生的位置，以及如何以及 hello rest 應用程式的支援後端基礎結構可以調整。  例如，對於 100% 無狀態的應用程式，可以使用每一 Azure 區域多個 App Service 環境的組合，乘以跨多個 Azure 區域部署的 App Service 環境數，來大幅調整應用程式。  透過從 15 + 公用 Azure 地區可用 toochoose，客戶可以真正建置全球大規模應用程式使用量。  Hello 範例應用程式中使用這個發行項，單一 Azure 區域 （美國中南部） 中建立三個應用程式服務環境。
* **Hello 應用程式服務環境的命名慣例：**每個 App Service 環境名稱必須是唯一。  一或兩個應用程式服務環境之外，它是很有幫助 toohave 命名慣例 toohelp 識別每個 App Service 環境。  Hello 範例應用程式使用簡單的命名慣例。  hello hello 三個應用程式服務環境的名稱是*fe1ase*， *fe2ase*，和*fe3ase*。
* **Hello 應用程式的命名慣例：**將部署的 hello 應用程式的多個執行個體，因為每個執行個體部署的 hello 應用程式需要名稱。  應用程式服務環境的一項小已知但很方便功能是相同的應用程式名稱可跨多個應用程式服務環境的 hello。  因為每個應用程式服務環境都有唯一的網域尾碼，開發人員可以選擇 toore 使用 hello 完全相同的應用程式的名稱，每個環境中。  例如，開發人員可以將應用程式命名如下：myapp.foo1.p.azurewebsites.net、myapp.foo2.p.azurewebsites.net、myapp.foo3.p.azurewebsites.net，依此類推。Hello 範例應用程式透過每個應用程式執行個體也都有唯一名稱。  hello 所使用的應用程式執行個體名稱是*webfrontend1*， *webfrontend2*，和*webfrontend3*。

## <a name="setting-up-hello-traffic-manager-profile"></a>Hello Traffic Manager 設定檔設定
一旦應用程式的多個執行個體部署在多個應用程式服務環境，hello 個別的應用程式執行個體可以註冊使用 Traffic Manager。  Hello 範例應用程式流量管理員設定檔所需的*可擴充 ase demo.trafficmanager.net* ，可以路由傳送客戶部署的 hello 遵循 tooany 應用程式執行個體：

* **webfrontend1.fe1ase.p.azurewebsites.net:** hello 範例應用程式上部署的執行個體 hello 第一個 App Service 環境。
* **webfrontend2.fe2ase.p.azurewebsites.net:** hello 範例應用程式上部署的執行個體 hello 第二個 App Service 環境。
* **webfrontend3.fe3ase.p.azurewebsites.net:** hello 範例應用程式上部署的執行個體 hello 第三個的 App Service 環境。

多個 Azure 應用程式服務端點，皆執行於 hello hello 最簡單的方式 tooregister**相同**Azure 區域中，是以 hello Powershell [Azure 資源管理員 Traffic Manager 支援][ARMTrafficManager].  

hello 第一個步驟是 toocreate Azure Traffic Manager 設定檔。  下列程式碼 hello 顯示 hello 設定檔的建立 hello 範例應用程式的方式：

    $profile = New-AzureTrafficManagerProfile –Name scalableasedemo -ResourceGroupName yourRGNameHere -TrafficRoutingMethod Weighted -RelativeDnsName scalable-ase-demo -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"

請注意如何 hello *RelativeDnsName*參數已設定太*可擴充 ase 示範*。  這是如何 hello 網域名稱*可擴充 ase demo.trafficmanager.net*建立並與流量管理員設定檔相關聯。

hello *TrafficRoutingMethod*參數會定義 hello 負載平衡的原則 Traffic Manager 將使用的 toodetermine toospread 客戶如何載入所有 hello 可用的端點。  在此範例 hello*加權*選擇的方法。  這將導致客戶的要求會分散在所有的 hello 與每個端點相關聯的相對加權為基礎的 hello 註冊應用程式端點。 

建立 hello 設定檔，每個應用程式執行個體就會以原生的 Azure 端點加入 toohello 設定檔。  hello 的下列程式碼會擷取參考 tooeach 前端 web 應用程式，並將每個應用程式為透過 hello Traffic Manager 端點*TargetResourceId*參數。

    $webapp1 = Get-AzureRMWebApp -Name webfrontend1
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend1 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp1.Id –EndpointStatus Enabled –Weight 10

    $webapp2 = Get-AzureRMWebApp -Name webfrontend2
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend2 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp2.Id –EndpointStatus Enabled –Weight 10

    $webapp3 = Get-AzureRMWebApp -Name webfrontend3
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend3 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp3.Id –EndpointStatus Enabled –Weight 10

    Set-AzureTrafficManagerProfile –TrafficManagerProfile $profile

請注意一個呼叫太*新增 AzureTrafficManagerEndpointConfig*每個個別的應用程式執行個體。  hello *TargetResourceId*參數在每個 Powershell 命令參考其中一個 hello 三個已部署的應用程式執行個體。  hello Traffic Manager 設定檔會將負載分散在 hello 設定檔中註冊的所有三個端點。

所有的三個端點使用的 hello hello 相同的值 (10) hello*加權*參數。  這會使流量管理員將客戶要求較平均地分散在所有的三個應用程式執行個體間。 

## <a name="pointing-hello-apps-custom-domain-at-hello-traffic-manager-domain"></a>指在 hello Traffic Manager 網域 hello 應用程式的自訂網域
hello 所需的最後一個步驟是 toopoint hello 自訂網域的 hello 應用程式在 hello Traffic Manager 網域。  這表示 hello 範例應用程式指向*www.scalableasedemo.com*在*可擴充 ase demo.trafficmanager.net*。  此步驟需要 toobe 已完成，但 hello 網域註冊機構管理 hello 自訂網域。  

CNAME 記錄需求 toobe 使用您的註冊機構的網域管理工具，在 hello Traffic Manager 網域建立的點 hello 自訂網域。  hello 圖示範此 CNAME 組態看起來像：

![自訂網域的 CNAME][CNAMEforCustomDomain] 

雖然未涵蓋在本主題中，請記住每個個別的應用程式執行個體必須已向它註冊以及 toohave hello 自訂網域。  否則要求可讓 tooan 應用程式執行個體，並 hello 應用程式沒有 hello hello 應用程式註冊的自訂網域，如果 hello 要求將會失敗。  

在此範例 hello 自訂網域是*www.scalableasedemo.com*，且每個應用程式執行個體具有 hello 與它相關聯的自訂網域。

![自訂網域][CustomDomain] 

向 Azure App Service 應用程式註冊自訂網域的概述，請參閱下列文章 hello[註冊自訂網域][RegisterCustomDomain]。

## <a name="trying-out-hello-distributed-topology"></a>試用 hello 分散式拓撲
hello hello Traffic Manager 和 DNS 設定最終結果是，要求*www.scalableasedemo.com*將通過 hello 下列順序：

1. 瀏覽器或裝置執行 *www.scalableasedemo.com*
2. hello hello 網域註冊機構的 CNAME 項目會導致 hello DNS 查閱重新導向 toobe tooAzure Traffic Manager。
3. 針對提出 DNS 查閱*可擴充 ase demo.trafficmanager.net* hello Azure Traffic Manager DNS 伺服器的其中之一。
4. 根據 hello 負載平衡原則 (hello *TrafficRoutingMethod*建立 hello Traffic Manager 設定檔時，請使用稍早的參數)，Traffic Manager 就會選取其中一個 hello 設定端點，並且傳回 hello 的 FQDN端點 toohello 瀏覽器或裝置。
5. 由於 hello hello 端點的 FQDN 是 hello 的 App Service 環境上執行的應用程式執行個體的 Url，hello 瀏覽器或裝置會要求 Microsoft Azure DNS 伺服器 tooresolve hello FQDN tooan IP 位址。 
6. hello 瀏覽器或裝置將會傳送 hello HTTP/S 要求 toohello IP 位址。  
7. hello 要求會抵達其中一個 hello 部 hello 應用程式服務環境上執行的應用程式執行個體。

hello 主控台圖會顯示 hello 範例應用程式的自訂網域已成功解析 tooan 應用程式執行個體上 hello 三個範例應用程式服務環境的其中一個執行的 DNS 查閱 (在此情況下 hello hello 三個應用程式服務環境的第二個):

![DNS 查閱][DNSLookup] 

## <a name="additional-links-and-information"></a>其他連結和資訊
所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。

文件上 hello Powershell [Azure 資源管理員 Traffic Manager 支援][ARMTrafficManager]。  

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[AzureTrafficManagerProfile]: ../traffic-manager/traffic-manager-manage-profiles.md
[ARMTrafficManager]: ../traffic-manager/traffic-manager-powershell-arm.md
[RegisterCustomDomain]: app-service-web-tutorial-custom-domain.md


<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-geo-distributed-scale/ConceptualArchitecture-1.png
[CNAMEforCustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CNAMECustomDomain-1.png
[DNSLookup]:  ./media/app-service-app-service-environment-geo-distributed-scale/DNSLookup-1.png
[CustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CustomDomain-1.png 
