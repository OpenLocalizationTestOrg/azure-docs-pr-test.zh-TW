---
title: "連線提供者和位置︰Azure ExpressRoute |Microsoft Docs"
description: "本文章提供位置的詳細的概觀，其中提供服務，以及如何 tooconnect tooAzure 區域。 依連線提供者排序。"
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: c878513a-d594-42ad-8b0e-403efd0c4b25
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: kaanan
ms.openlocfilehash: df906ae6ff4e149c9cab4aa46ab78c8dd6aa4366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-partners-and-peering-locations"></a>ExpressRoute 合作夥伴和對等互連位置

> [!div class="op_single_selector"]
> * [依提供者的位置](expressroute-locations.md)
> * [依位置的提供者](expressroute-locations-providers.md)


這篇文章中的 hello 資料表會提供 ExpressRoute 連線提供者、 ExpressRoute 地理涵蓋範圍，支援透過 ExpressRoute 和 ExpressRoute 系統整合業者 (Si) 的 Microsoft 雲端服務的相關資訊。

## <a name="partners"></a>ExpressRoute 連線提供者
所有的 Azure 區域和位置都支援 ExpressRoute。 下列地圖 hello 提供 Azure 區域和 ExpressRoute 位置的清單。 ExpressRoute 位置，請參閱的 toothose Microsoft 對等多個服務提供者的位置。

![位置圖][0]

如果您連接 tooat 至少有一個 ExpressRoute 位置 hello 地緣政治區域內，您將必須存取 tooAzure 服務地緣政治區域內的所有區域。

### <a name="azure-regions-tooexpressroute-locations-within-a-geopolitical-region"></a>Azure 區域 tooExpressRoute 地緣政治區域內的位置。
hello 下表提供的 Azure 區域對應 tooExpressRoute 地緣政治區域內的位置。

| **地緣政治區域** | **Azure 區域** | **ExpressRoute 位置** |
| --- | --- | --- |
| **北美洲** |美國東部、美國西部、美國東部 2、美國西部 2、美國中部、美國中南部、美國中北部、美國中西部、加拿大中部、加拿大東部 |亞特蘭大、芝加哥、達拉斯、丹佛、拉斯維加斯、洛杉磯、邁阿密、紐約、聖安東尼奧、西雅圖、矽谷、華盛頓特區、蒙特婁、魁北克市、多倫多 |
| **南美洲** |巴西南部 |聖保羅 |
| **歐洲** |北歐、西歐、英國西部、英國南部 |阿姆斯特丹、都柏林、倫敦、紐波特 (威爾斯)、巴黎 |
| **亞洲** |東亞、東南亞 |香港特別行政區、新加坡 |
| **日本** |日本西部、日本東部 |大阪、東京 |
| **澳大利亞** |澳洲東南部、澳洲東部 |墨爾本、雪梨 |
| **印度** |印度西部、印度中部、印度南部 |辰內，孟買 |
| **南韓** |韓國中部、韓國南部 |釜山、首爾 |

### <a name="regions-and-geopolitical-boundaries-for-national-clouds"></a>國家雲端的區域和地理政治界限
hello 下表提供有關區域和地緣政治界限的國家 （地區） 的雲端。

| **地緣政治區域** | **Azure 區域** | **ExpressRoute 位置** |
| --- | --- | --- |
| **美國政府雲端** |美國愛荷華州政府、美國維吉尼亞州政府、美國國防部中部、美國國防部東部  |芝加哥、達拉斯、紐約、西雅圖、矽谷、華盛頓特區 |
| **中國** |中國北部、中國東部 |北京、上海 |
| **德國** |德國中部、德國東部 |柏林、法蘭克福 |

Hello 標準 ExpressRoute SKU 上不支援跨地理政治區域連線。 您將需要 tooenable hello ExpressRoute premium 附加元件 toosupport 全域連線能力。 不支援連線 toonational 雲端環境。 如果有需要的話，您可以聯絡您的連線提供者。

## <a name="locations"></a>連線提供者位置

hello 下表顯示服務提供者的位置。 如果您想 tooview 依位置的可用提供者，請參閱[服務提供者位置](expressroute-locations-providers.md#locations)。


### <a name="production-azure"></a>生產 Azure
| **服務提供者** | **Microsoft Azure** | **Office 365 和 Dynamics 365** | **位置** |
| --- | --- | --- | --- |
| **[AARNet](https://www.aarnet.edu.au/network-and-services/cloud-services-applications/azure-expressroute/)** |支援 |支援 |墨爾本、雪梨 |
| **[Airtel](http://www.airtel.in/business/connexion)** | 支援 | 支援 | 辰內，孟買 |
| **[Aryaka Networks](http://www.aryaka.com/)** |支援 |支援 |阿姆斯特丹、達拉斯、香港、矽谷、新加坡、東京、華盛頓特區 |
| **[Ascenty Data Centers](https://ascenty.com/solucoes/conectividade-e-interconexoes/Microsoft-express-route/)** |敬請期待 |敬請期待 |聖保羅 |
| **[AT&T NetBond](https://www.synaptic.att.com/clouduser/html/productdetail/ATT_NetBond.htm)** |支援 |支援 |阿姆斯特丹、芝加哥、達拉斯、倫敦、矽谷、新加坡、雪梨、東京、多倫多、華盛頓特區 |
| **[Bell Canada](https://business.bell.ca/shop/enterprise/cloud-connect-access-to-cloud-partner-services)** |支援 |支援 |蒙特婁、多倫多 |
| **[British Telecom](http://www.globalservices.bt.com/uk/en/news/bt_to_provide_connectivity_to_microsoft_azure)** |支援 |支援 |阿姆斯特丹、香港、倫敦、矽谷、新加坡、雪梨、東京、華盛頓特區 |
| **[CenturyLink](http://www.centurylink.com/business/enterprise/services/data-network/mpls-vpn.html)** |敬請期待 |敬請期待 |矽谷 |
| **China Telecom Global** |支援 |不支援 |香港 |
| **[Cologix](http://www.cologix.com/solutions/cloud-connect/public-clouds/microsoft-cloud/)** |支援 |支援 |達拉斯、蒙特婁、多倫多 |
| **[Colt](http://www.colt.net/uk/en/news/colt-announces-dedicated-cloud-access-for-microsoft-azure-services-en.htm)** |支援 |支援 |阿姆斯特丹、都柏林、倫敦、巴黎、東京 |
| **Comcast** |支援 |支援 |芝加哥、矽谷、華盛頓特區 |
| **[主控台](https://www.consoleconnect.com/partners/cloudsaas/)**| 支援 | 支援 |矽谷、多倫多 |
| **[CoreSite](http://www.coresite.com/solutions/cloud-services/public-cloud-providers/microsoft-azure-expressroute)** |支援 |支援 |丹佛、洛杉磯、紐約 |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |支援 |支援 |阿姆斯特丹、亞特蘭大、芝加哥、達拉斯、香港、倫敦、洛杉磯、墨爾本、紐約、大阪、巴黎、聖保羅、西雅圖、矽谷、新加坡、雪梨、東京、多倫多、華盛頓特區 |
| **euNetworks** |支援 |支援 |阿姆斯特丹 |
| **GÉANT** |支援 |支援 |阿姆斯特丹 |
| **[Global Cloud Xchange (GCX)] (http://globalcloudxchange.com/cloud-platform/cloud-x-fusion/cloud-x-fusion-for-azure/)** | 支援| 支援 | 辰內 |
| **[InterCloud](https://www.intercloud.com/)** |支援 |支援 |阿姆斯特丹、倫敦、新加坡、華盛頓特區 |
| **[Internet Initiative Japan Inc. - IIJ](http://www.iij.ad.jp/en/news/pressrelease/2015/1216-2.html)** |支援 |支援 |大阪、東京 |
| **Internet Solutions - Cloud Connect** |支援 |支援 |阿姆斯特丹、倫敦 |
| **[Interxion](http://www.interxion.com/why-interxion/colocate-with-the-clouds/Microsoft-Azure/)** |支援 |支援 |阿姆斯特丹、都柏林、倫敦、巴黎 |
| **Jisc** |支援 |支援 |倫敦 |
| **KINX** |支援 |支援 |首爾 |
| **[KPN](http://www.kpn.com/cloudconnect)** | 支援 | 支援 | 阿姆斯特丹 | 
| **[Level 3 Communications](http://your.level3.com/LP=882?WT.tsrc=02192014LP882AzureVanityAzureText)** |支援 |支援 |阿姆斯特丹、芝加哥、達拉斯、拉斯維加斯、倫敦、聖保羅、西雅圖、矽谷、新加坡、華盛頓特區 |
| **LG CNS** |支援 |支援 |釜山、首爾 |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |支援 |支援 |阿姆斯特丹、芝加哥、達拉斯、香港、拉斯維加斯、倫敦、洛杉磯、墨爾本、邁阿密、紐約、魁北克市、聖安東尼奧、西雅圖、矽谷、新加坡、雪梨、多倫多、華盛頓特區 |
| **MTN** |支援 |支援 |倫敦 |
| **[Neutrona Networks](http://www.neutrona.com/index.php/services#cloud-connect)** |支援 |支援 |邁阿密、聖保羅 |
| **[新一代資料](http://www.nextgenerationdata.co.uk/ngd-cloud-gateway/)** |支援 |支援 |Newport(Wales) |
| **NEXTDC** |支援 |支援 |墨爾本、雪梨 |
| **[NTT Communications](http://www.ntt.com/en/services/network/virtual-private-network.html)** |支援 |支援 |倫敦、洛杉磯、大阪、新加坡、東京、華盛頓特區 |
| **[NTT SmartConnect](http://cloud.nttsmc.com/cxc/azure.html)** |支援 |支援 |大阪 |
| **[Orange](http://www.orange-business.com/en/products/business-vpn-galerie)** |支援 |支援 |阿姆斯特丹、香港、倫敦、巴黎、矽谷、新加坡、雪梨、華盛頓特區 |
| **PCCW Global Limited** |支援 |支援 |香港 |
| **Sejong Telecom** |支援 |支援 |首爾 |
| **[SIFY](http://telecom.sify.com/azure-expressroute.html)** |支援 |支援 |辰內 |
| **[SingTel](http://info.singtel.com/about-us/news-releases/singtel-provide-secure-private-access-microsoft-azure-public-cloud)** |支援 |支援 |新加坡 |
| **[Softbank](http://www.softbank.jp/biz/cloud/cloud_access/direct_access_for_az/)** |支援 |支援 |大阪、東京 |
| **[Tata Communications](http://www.tatacommunications.com/lp/izo/azure/azure_index.html)** |支援 |支援 |阿姆斯特丹、辰內、香港、倫敦、孟買、矽谷、新加坡、華盛頓特區 |
| **[TeleCity Group](http://www.telecitygroup.com/investor-centre/news_details.htm?locid=03100500400b00d&xml)** |支援 |支援 |阿姆斯特丹、都柏林、倫敦 |
| **[Telefonica](https://www.business-solutions.telefonica.com/es/enterprise/solutions/efficient-infrastructure/managed-voice-data-connectivity/)** |支援 |支援 |阿姆斯特丹、聖保羅 |
| **[Telehouse - KDDI](http://www.telehouse.net/solutions/cloud-services/cloud-link)** |支援 |支援 |倫敦 |
| **Telenor** |支援 |支援 |阿姆斯特丹、倫敦 |
| **[Telstra Corporation](http://www.telstra.com.au/business-enterprise/network-services/networks/cloud-direct-connect/)** |支援 |支援 |墨爾本、雪梨 |
| **[Telus](http://www.telus.com)** |支援 |支援 |多倫多 |
| **[UOLDIVEO](http://www.uoldiveo.com.br/solucoes/cloud.html#rmcl)** |支援 |支援 |聖保羅 |
| **[Verizon](http://www.verizonenterprise.com/products/networking/secure-cloud-interconnect/)** |支援 |支援 |阿姆斯特丹、芝加哥、達拉斯、香港、倫敦、矽谷、新加坡、雪梨、東京、華盛頓特區 |
| **[Vodafone](http://www.vodafone.com/business/global-enterprise/global-connectivity/vodafone-ip-vpn-cloud-connect)** |支援 |不支援 |倫敦 |
| **[Zayo Group](http://www.zayo.com/solutions/industries/cloud-connectivity/microsoft-expressroute)** |支援 |支援 |阿姆斯特丹、芝加哥、達拉斯+、倫敦+、洛杉磯、紐約、矽谷、多倫多、華盛頓特區 |

 **+** 表示即將推出

### <a name="national-cloud-environment"></a>國家雲端環境

### <a name="us-government-cloud"></a>美國政府雲端
| **服務提供者** | **Microsoft Azure** | **Office 365** | **位置** |
| --- | --- | --- | --- |
| **[AT&T NetBond](https://www.synaptic.att.com/clouduser/html/productdetail/ATT_NetBond.htm)** |支援 |支援 |芝加哥、華盛頓特區 |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |支援 |支援 |芝加哥、達拉斯、紐約、西雅圖、矽谷、華盛頓特區 |
| **[Level 3 Communications](http://your.level3.com/LP=882?WT.tsrc=02192014LP882AzureVanityAzureText)** |支援 |支援 |芝加哥、紐約+、矽谷、華盛頓特區 |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |支援 | 支援 | 芝加哥、達拉斯 |
| **[Verizon](http://news.verizonenterprise.com/2014/04/secure-cloud-interconnect-solutions-enterprise/)** |支援 |支援 |芝加哥、達拉斯、紐約、華盛頓特區 |

### <a name="china"></a>中國
| **服務提供者** | **Microsoft Azure** | **Office 365** | **位置** |
| --- | --- | --- | --- |
| **China Telecom** |支援 |不支援 |北京、上海 |

詳細資訊，請參閱 toolearn[中國 ExpressRoute](http://www.windowsazure.cn/home/features/expressroute/)。

### <a name="germany"></a>德國
| **服務提供者** | **Microsoft Azure** | **Office 365** | **位置** |
| --- | --- | --- | --- |
| **[Colt](http://www.colt.net/uk/en/news/colt-announces-dedicated-cloud-access-for-microsoft-azure-services-en.htm)** |支援 |不支援 |柏林+、法蘭克福 |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |支援 |不支援 |法蘭克福 |
| **[e-shelter](https://www.e-shelter.de/en/microsoft-expressroutetm)** |支援 |不支援 |柏林 |
| **Interxion** |支援 |不支援 |法蘭克福 |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |支援  | 不支援 | 柏林 |
| **T-Systems** |支援 |不支援 |柏林 |

## <a name="connectivity-through-exchange-providers"></a>透過 Exchange 提供者連線

如果上一節中未列出您的連線提供者，您仍然可以建立連線。

* 如果已連線的 hello 上表中的 hello 交換 tooany，連絡您的連線提供者 toosee。 您可以檢查 hello 下列連結 toogather 交換服務提供者所提供服務的詳細資訊。 數個連線提供者都已連接的 tooEthernet 交換。
  * [Cologix](http://www.cologix.com/)
  * [Console](https://www.consoleconnect.com/partners/cloudsaas/)
  * [CoreSite](http://www.coresite.com/)
  * [Equinix Cloud Exchange](http://www.equinix.com/services/interconnection-connectivity/cloud-exchange/)
  * [Interxion](http://www.interxion.com/products/interconnection/cloud-connect/)
  * [Megaport](https://www.megaport.com/services/microsoft-expressroute/)
  * [NextDC](http://www.nextdc.com/)
  * [TeleCity CloudIX](http://www.telecitygroup.com/colocation-services/cloud-ix.htm)
* 具有擴充您的網路 toohello 對等互連位置所選擇的連線提供者。
  * 請確保您的連線提供者以高可用性的方式延伸您的連線，因此不會有單一失敗點。
* 為連線提供者 tooconnect tooMicrosoft 訂購 ExpressRoute 電路 hello 交換。
  * 遵循的步驟[建立 ExpressRoute 電路](expressroute-howto-circuit-classic.md)tooset 連線設定。

## <a name="connectivity-through-additional-service-providers"></a>透過額外服務提供者連線

| **連線提供者** | **Exchange** | **位置** |
| --- | --- | --- |
| **[1CLOUDSTAR](http://www.1cloudstar.com/service/cloudconnect-azure-expressroute/)** |Equinix |新加坡 |
| **[Airgate Technologies, Inc.](http://airgate.ca/cloud-express/)** | Equinix、Cologix | 多倫多、蒙特婁 |
| **[Alaska Communications](http://www.alaskacommunications.com/For-Your-Business/Direct-Cloud-Service)** |Equinix |Seattle |
| **[Altice Business](https://golightpath.com/transport)** |Equinix |紐約、華盛頓特區 |
| **[Arteria Networks Corporation](https://arteria-net.com/business/service/cloud_access/sca/)** |Equinix |東京 |
| **[Bezeq International Ltd.](https://www.bezeqint.net/english)** | euNetworks | 倫敦 |
| **[BroadBand Tower, Inc.](http://www.bbtower.co.jp/product-service/data-center/network/dcconnect-for-azure/)** | Equinix | 東京 |
| **[C3ntro Telecom](http://www.c3ntro.com/data/cloud-conectivity/)** | Equinix、Megaport | 達拉斯 |
| **[Cogeco Peer 1](https://www.cogecopeer1.com/en/)**| Equinix | 蒙特婁、多倫多 |
| **[Cox Business](https://www.cox.com/business/networking/cloud-connectivity.html)** | Equinix | 達拉斯、矽谷、華盛頓特區 | 
| **[Data Foundry](https://www.datafoundry.com/services/cloud-connect)** | Megaport | 達拉斯 |
| **[Epsilon Telecommunications Limited](http://www.epsilontel.com/data-connectivity/cloud-access/)** | Equinix | 倫敦、新加坡、華盛頓特區 |
| **[Eurofiber](https://eurofiber.nl/microsoft-azure/)** | Equinix | 阿姆斯特丹 |
| **[指數 E](http://www.exponential-e.com/services/connectivity-services/cloud-connect-exchange)** | Equinix | 倫敦 |
| **[Fastweb S.p.A](http://www.fastweb.it/grandi-aziende/connessione-voce-e-wifi/scheda-prodotto/rete-privata-virtuale/)** | Equinix | 阿姆斯特丹 |
| **[Gtt Communications Inc](https://www.gtt.net/wp-content/uploads/2017/04/EtherCloud-Data-Sheet.pdf)** |Equinix | 華盛頓 |
| **[HSO](http://www.hso.co.uk/products/cloud-direct)** |Equinix | 倫敦、斯勞 |
| **LGA Telecom** |Equinix |新加坡|
| **[Lightower](http://www.lightower.com/network-solutions/cloud-connect/#microsoft-azure)** |Equinix | 芝加哥、紐約、華盛頓特區 |
| **[Macroview Telecom](http://www.macroview.com/en/scripts/catitem.php?catid=solution&sectionid=expressroute)** |Equinix |香港 |
| **[Macquarie Telecom Group](https://macquariegovernment.com/secure-cloud/secure-cloud-exchange/)** | Megaport | 雪梨 |
| **[Masergy](https://www.masergy.com/solutions/hybrid-networking/cloud-marketplace/microsoft-azure)** | Equinix | 華盛頓 |
| **[NexGen Networks](http://www.nexgen-net.com/nexgen-networks-direct-connect-microsoft-azure-expressroute.html)** | Interxion | 倫敦 |
| **[Nianet](https://nianet.dk/produkter/internet/microsoft-expressroute)** |Telecity | 阿姆斯特丹、法蘭克福 |  
| **[QSC AG](https://www.qsc.de/de/produkte-loesungen/cloud-services-und-it-outsourcing/pure-enterprise-cloud/multi-cloud-management/azure-expressroute/)** |Interxion | 法蘭克福 |  
| **Rogers** | Cologix、Equinix | 蒙特婁、多倫多 |
| **[Tamares Telecom](http://www.tamarestelecom.com/our-services/#Connectivity)** | Telecity | 倫敦 | 
| **[ThinkTel](http://www.thinktel.ca/services/agile-ix-data/expressroute/)** | Equinix | 多倫多 | 
| **[Transtelco](http://www.transtelco.net/tcloud/microsoft)** |Equinix | 達拉斯、洛杉磯 |  
| **[United Information Highway (UIH)](https://www.uih.co.th/en/internet-solution/cloud-direct/uih-cloud-direct-for-microsoft-azure-expressroute)**| Equinix | 新加坡 |
| **[Webair](https://www.webair.com/microsoft-express-route-partnership/)**| Megaport | 紐約 |
| **[Windstream](http://www.windstreambusiness.com/solutions/cloud-services/cloud-and-managed-hosting-services)**| Equinix | 芝加哥、矽谷、華盛頓特區 |
| **Zain** |Equinix |倫敦|
| **[Zertia](http://www.zertia.es/index.php/novedades)**| Level 3 | 馬德里 |
| **[Zirro](https://zirro.com/services/)**| Equinix | 蒙特婁、多倫多 |

## <a name="connectivity-through-datacenter-providers"></a>透過資料中心提供者連線
| **提供者** | **Exchange** |
| --- | --- |
| **[Cyrus One](https://cyrusone.com/enterprise-data-center-services/connectivity-and-interconnection/cloud-connectivity-reaching-amazon-microsoft-google-and-more/microsoft-azure-expressroute/?doing_wp_cron=1498512235.6733090877532958984375)** | Megaport |
| **[Digital Realty](https://www.digitalrealty.com/services/interconnection/service-exchange/)** | Megaport |
| **[EdgeConnex](http://www.edgeconnex.com/services/edge-data-centers-proximity-matters/)** | Megaport |
| **[RagingWire Data Centers](http://www.ragingwire.com/wholesale/wholesale-data-centers-worldwide-nexcenters)** | 主控台 |
| **[T5 Datacenters](http://t5datacenters.com/network-cloud-connect/)** | 主控台 |

## <a name="connectivity-through-national-research-and-education-networks-nren"></a>透過 National Research and Education Networks (NREN) 連線

| **提供者**|
| --- |
| **AARNET**| 
| **DeIC，透過 GÉANT**|
| **GARR，透過 GÉANT**|
| **GÉANT**|
| **HEAnet，透過 GÉANT**|
| **JISC**|
| **RedIRIS，透過 GÉANT**|
| **SINET**|
| **Surfnet，透過 GÉANT**|

* 如果您連線服務提供者未列在此處，請檢查 toosee，如果連接的 tooany hello ExpressRoute 交換夥伴上面所列。

## <a name="expressroute-system-integrators"></a>ExpressRoute 系統整合者
啟用私人連線能力 toofit 您的需求可能會很困難，取決於您網路的 hello 小數位數。 您可以使用與任何一列在下列資料表 tooassist hello hello 系統整合者您上架 tooExpressRoute。

| **系統整合者** | **Continent** |
| --- | --- |
| **[Altogee](http://www.altogee.be/expressroute)** | 歐洲 |
| **[Avanade Inc.](http://www.avanade.com/)** | 亞洲、歐洲、北美洲、南美洲 |
| **[Bright Skies GmbH](http://bskies.io/expressroute)** | 歐洲
| **[Ensyst](http://www.ensyst.com.au)** | 亞洲
| **[Equinix Professional Services](http://www.equinix.com/services/consulting/)** | 北美洲 |
| **[FlexManage](http://www.flexmanage.com/cloud)** | 北美洲 |
| **[Inframon](http://www.inframon.com/partner/microsoft/)** | 歐洲 |
| **[hello 顧問的 IT 團隊](http://itconsult.com.au/microsoft-expressroute)** | 澳大利亞 |
| **[MOQdigital](http://www.moqdigital.com.au/insights/technical/network-connectivity-options-for-azure)** | 澳大利亞 |
| **[MSG Services](https://www.msg-services.de/it-services/managed-services/cloud-outsourcing/)** | 歐洲 (德國) |
| **[Nelite](http://nelite.com/)** | 歐洲 |
| **[New Signature](https://www.newsignature.co.uk/)** | 歐洲 |
| **[OneAs1a](http://www.oneas1a.com/express-connect-any-cloud-ecac)** | 亞洲 |
| **[Orange Networks](https://orange-networks.com/blog/88-azureexpressroute)** | 歐洲 |
| **[Perficient](http://www.perficient.com/Partners/Microsoft/Cloud/Azure-ExpressRoute)** | 北美洲 |
| **[Presidio](http://info.presidio.com/microsoft-azure-expressroute)** | 北美洲 |
| **[sol-tec](http://www.sol-tec.com/Technologies)** | 歐洲 |
| **[Vigilant.IT](https://vigilant.it/expressroute)** | 澳大利亞 |


## <a name="next-steps"></a>後續步驟
* 如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。
* 請確定符合所有必要條件。 請參閱 [ExpressRoute 必要條件](expressroute-prerequisites.md)。

<!--Image References-->
[0]: ./media/expressroute-locations/expressroute-locations-map.png "位置圖"
