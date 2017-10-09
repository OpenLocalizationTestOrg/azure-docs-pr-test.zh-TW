---
title: "跨單位 Azure 連線的 VPN 裝置 aaaAbout |Microsoft 文件"
description: "本文討論 S2S VPN 閘道跨單位連接的 VPN 裝置和 IPsec 參數。 Tooconfiguration 指示和範例，會提供連結。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: ba449333-2716-4b7f-9889-ecc521e4d616
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: yushwang;cherylmc
ms.openlocfilehash: 8b84afbf93d807342ecd56ab369d5909a13343e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>關於 VPN 裝置和站對站 VPN 閘道連線的 IPsec/IKE 參數

VPN 裝置是必要的 tooconfigure 站台對站 (S2S) 跨單位 VPN 連線使用的 VPN 閘道。 站台對站連線可使用的 toocreate 混合式解決方案，或者每當您想要安全的連線在內部部署網路與您的虛擬網路之間。 本文提供已驗證的 VPN 裝置清單和 VPN 閘道的 IPsec/IKE 參數清單。

> [!IMPORTANT]
> 如果您遇到您在內部部署 VPN 裝置和 VPN 閘道之間的連線問題，請參閱太[已知裝置相容性問題](#known)。
>
>

### <a name="items-toonote-when-viewing-hello-tables"></a>項目 toonote 檢視 hello 資料表時：

* Azure VPN 閘道的名稱已經變更。 只有 hello 名稱已變更。 功能未變更。
  * 靜態路由 = 原則式
  * 動態路由 = 路由式
* 除非另有說明，是 hello 相同，高效能的分散式 VPN 閘道和 RouteBased VPN 閘道的規格。 例如，驗證的 hello 與 RouteBased VPN 閘道相容的 VPN 裝置也是與 hello HighPerformance VPN 閘道相容。

## <a name="devicetable"></a>已經驗證的 VPN 裝置及裝置設定指南

> [!NOTE]
> 設定站對站連線時，您的 VPN 裝置需要公開的 IPv4 IP 位址。
>

我們已與裝置廠商合作驗證一組標準 VPN 裝置。 所有 hello 下列清單中的 hello 裝置系列中的 hello 裝置應該使用 VPN 閘道。 請參閱[有關 VPN 閘道設定](vpn-gateway-about-vpn-gateway-settings.md#vpntype)toounderstand hello VPN 輸入 hello VPN 閘道的解決方案，您想要 tooconfigure 使用 （PolicyBased 或 RouteBased）。

toohelp 設定 VPN 裝置，請參閱對應 tooappropriate 裝置家族的 toohello 連結。 提供 hello 連結 tooconfiguration 指示以最佳方式為基礎。 如需 VPN 裝置的支援，請連絡裝置製造商。

|**廠商**          |**裝置系列**     |**作業系統最低版本** |**原則式設定指示** |**路由式設定指示** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |不相容  |[設定指南](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |AR 系列 VPN 路由器 |2.9.2                  |敬請期待     |不相容  |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall F-series |原則式︰5.4.3<br>路由式︰6.2.0 |[設定指南](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[設定指南](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall X-series |Barracuda Firewall 6.5 |[設定指南](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |不相容 |
| Brocade            |Vyatta 5400 vRouter   |Virtual Router 6.6R3 GA|[設定指南](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |不相容 |
| Check Point |Security Gateway |R77.30 |[設定指南](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[設定指南](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco              |ASA       |8.3 |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |不相容 |
| Cisco |ASR |原則式：IOS 15.1<br>路由式：IOS 15.2 |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |原則式：IOS 15.0<br>路由式*：IOS 15.1 |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[設定範例*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX、SDX、VPX |10.1 和更新版本 |[設定指南](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |不相容 |
| F5 |BIG-IP 系列 |12.0 |[設定指南](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[設定指南](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.4.2 |  |[設定指南](http://cookbook.fortinet.com/ipsec-vpn-microsoft-azure-54) |
| Internet Initiative Japan (IIJ) |SEIL 系列 |SEIL/X 4.60<br>SEIL/B1 4.60<br>SEIL/x86 3.20 |[設定指南](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |不相容 |
| Juniper |SRX |原則式：JunOS 10.2<br>路由式：JunOS 11.4 |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |J 系列 |原則式：JunOS 10.4r9<br>路由式：JunOS 11.4 |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[設定範例](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |路由及遠端存取服務 |Windows Server 2012 |不相容 |[設定範例](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| 開啟系統 AG |任務控制安全性閘道 |N/A |[設定指南](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |不相容 |
| Openswan |Openswan |2.6.32 |(敬請期待) |不相容 |
| Palo Alto Networks |所有執行 PAN-OS 的裝置 |PAN-OS<br>原則式：6.1.5 或更新版本<br>路由式：7.1.4 |[設定指南](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[設定指南](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWall |TZ 系列、NSA 系列<br>SuperMassive 系列<br>E-Class NSA 系列 |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |[SonicOS 6.2 設定指南](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[SonicOS 5.9 設定指南](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |[SonicOS 6.2 設定指南](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[SonicOS 5.9 設定指南](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |
| WatchGuard |全部 |Fireware XTM<br> 原則式：v11.11.x<br>路由式：v11.12.x |[設定指南](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[設定指南](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

(*) ISR 7200 系列路由器僅支援原則式 VPN。

## <a name="additionaldevices"></a>未經驗證的 VPN 裝置

如果您沒有看到 hello 驗證的 VPN 裝置表格中列出您的裝置，您的裝置仍可能使用站對站連線。 如需額外支援和設定指示，請連絡裝置製造商。

## <a name="editing"></a>編輯裝置組態範本

下載提供 hello VPN 裝置組態的範例後，您需要 tooreplace hello 的某些值 tooreflect 環境的 hello 設定。

### <a name="tooedit-a-sample"></a>tooedit 範例：

1. 使用 「 記事本 」 開啟 hello 範例。
2. 搜尋和取代所有 <*文字*> 有關 tooyour 環境的 hello 值字串。 要確定 tooinclude < 和 >。 指定的名稱，當您選取的 hello 名稱應該是唯一的。 如果命令無法運作，請參閱裝置製造商文件。

| **範本中的文字** | **變更為** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |您為此物件選擇的名稱。 例如：myOnPremisesNetwork |
| &lt;RP_AzureNetwork&gt; |您為此物件選擇的名稱。 例如：myAzureNetwork |
| &lt;RP_AccessList&gt; |您為此物件選擇的名稱。 例如：myAzureAccessList |
| &lt;RP_IPSecTransformSet&gt; |您為此物件選擇的名稱。 例如：myIPSecTransformSet |
| &lt;RP_IPSecCryptoMap&gt; |您為此物件選擇的名稱。 例如：myIPSecCryptoMap |
| &lt;SP_AzureNetworkIpRange&gt; |指定範圍。 例如：192.168.0.0 |
| &lt;SP_AzureNetworkSubnetMask&gt; |指定子網路遮罩。 例如：255.255.0.0 |
| &lt;SP_OnPremisesNetworkIpRange&gt; |指定內部部署範圍。 例如：10.2.1.0 |
| &lt;SP_OnPremisesNetworkSubnetMask&gt; |指定內部部署子網路遮罩。 例如：255.255.255.0 |
| &lt;SP_AzureGatewayIpAddress&gt; |此資訊的特定 tooyour 虛擬網路且其位於 hello 管理入口網站為**閘道 IP 位址**。 |
| &lt;SP_PresharedKey&gt; |這項資訊是特定 tooyour 虛擬網路，且位於 hello 管理入口網站作為管理金鑰。 |

## <a name="ipsec"></a>IPsec/IKE 參數

> [!NOTE]
> 雖然 hello 下表中列出的 hello 值會受到 hello VPN 閘道，目前那里就不會為您 toospecify 或選取特定的演算法或參數組合從 hello VPN 閘道。 您必須指定從 hello 在內部部署 VPN 裝置的任何條件約束。 此外，您必須將 **MSS** 固定在 **1350**。
> 
>

在下表的 hello:

* SA = 安全性關聯
* IKE 階段 1 也稱為「主要模式」
* IKE 階段 2 也稱為「快速模式」

### <a name="ike-phase-1-main-mode-parameters"></a>IKE 階段 1 (主要模式) 參數

| **屬性**          |**原則式**    | **路由式**    |
| ---                   | ---               | ---               |
| IKE 版本           |IKEv1              |IKEv2              |
| Diffie-Hellman 群組  |群組 2 (1024 位元) |群組 2 (1024 位元) |
| 驗證方法 |預先共用金鑰     |預先共用金鑰     |
| 加密與雜湊演算法 |1.AES256、SHA256<br>2.AES256、SHA1<br>3.AES128、SHA1<br>4. 3DES、SHA1 |1.AES256、SHA1<br>2.AES256、SHA256<br>3.AES128、SHA1<br>4.AES128、SHA256<br>5. 3DES、SHA1<br>6. 3DES、SHA256 |
| SA 存留期           |28,800 秒     |28,800 秒     |

### <a name="ike-phase-2-quick-mode-parameters"></a>IKE 階段 2 (快速模式) 參數

| **屬性**                  |**原則式**| **路由式**                              |
| ---                           | ---           | ---                                         |
| IKE 版本                   |IKEv1          |IKEv2                                        |
| 加密與雜湊演算法 |1.AES256、SHA256<br>2.AES256、SHA1<br>3.AES128、SHA1<br>4. 3DES、SHA1 |[RouteBased QM SA 提供項目](#RouteBasedOffers) |
| SA 存留期 (時間)            |3,600 秒  |27,000 秒                                |
| SA 存留期 (位元組)           |102,400,000 KB | -                                           |
| 完整轉寄密碼 (PFS) |否             |[RouteBased QM SA 提供項目](#RouteBasedOffers) |
| 停用的對等偵測 (DPD)     |不支援  |支援                                    |


### <a name ="RouteBasedOffers"></a>RouteBased VPN IPsec 安全性關聯 (IKE 快速模式 SA) 提供項目

hello 下表列出 IPsec SA （IKE 快速模式） 提供。 提供項目是列出的 hello 順序喜好設定的呈現或接受該 hello 供應項目。

#### <a name="azure-gateway-as-initiator"></a>Azure 閘道器為啟動者

|-  |**加密**|**驗證**|**PFS 群組**|
|---| ---          |---               |---          |
| 1 |GCM AES256    |GCM (AES256)      |None         |
| 2 |AES256        |SHA1              |None         |
| 3 |3DES          |SHA1              |None         |
| 4 |AES256        |SHA256            |None         |
| 5 |AES128        |SHA1              |None         |
| 6 |3DES          |SHA256            |None         |

#### <a name="azure-gateway-as-responder"></a>Azure 閘道器為回應者

|-  |**加密**|**驗證**|**PFS 群組**|
|---| ---          | ---              |---          |
| 1 |GCM AES256    |GCM (AES256)      |None         |
| 2 |AES256        |SHA1              |None         |
| 3 |3DES          |SHA1              |None         |
| 4 |AES256        |SHA256            |None         |
| 5 |AES128        |SHA1              |None         |
| 6 |3DES          |SHA256            |None         |
| 7 |DES           |SHA1              |None         |
| 8 |AES256        |SHA1              |1            |
| 9 |AES256        |SHA1              |2            |
| 10|AES256        |SHA1              |14           |
| 11|AES128        |SHA1              |1            |
| 12|AES128        |SHA1              |2            |
| 13|AES128        |SHA1              |14           |
| 14|3DES          |SHA1              |1            |
| 15|3DES          |SHA1              |2            |
| 16|3DES          |SHA256            |2            |
| 17|AES256        |SHA256            |1            |
| 18|AES256        |SHA256            |2            |
| 19|AES256        |SHA256            |14           |
| 20|AES256        |SHA1              |24           |
| 21|AES256        |SHA256            |24           |
| 22|AES128        |SHA256            |None         |
| 23|AES128        |SHA256            |1            |
| 24|AES128        |SHA256            |2            |
| 25|AES128        |SHA256            |14           |
| 26|3DES          |SHA1              |14           |

* 您可以使用路由式和高效能 VPN 閘道指定 IPsec ESP NULL 加密。 Null 根據的加密不會提供保護 toodata 在傳輸中和應該只用於時最大輸送量和最小延遲是必要。 用戶端可以選擇 toouse 這在 VNet 對 VNet 通訊案例中，或加密在 hello 方案中其他位置套用時。
* 透過 hello 網際網路的跨單位連線，使用加密與雜湊演算法上方 tooensure 安全性的重要通訊 hello 表格列出使用 hello 預設 Azure VPN 閘道設定。

## <a name="known"></a>已知的裝置相容性問題

> [!IMPORTANT]
> 這些是 hello 協力廠商 VPN 裝置與 Azure VPN 閘道之間的相容性問題。 hello Azure 小組會積極地與 hello 廠商 tooaddress hello 此處列出的問題。 一旦 hello 問題獲得解決，此頁面將會更新與 hello 最新的資訊。 請定期回來查看。
>
>

### <a name="feb-16-2017"></a>2017 年 2 月 16 日

**Palo Alto 網路裝置版本先前 too7.1.4** Azure 路由式 vpn： 如果您使用與 PAN-OS 版本先前 too7.1.4 Palo Alto 網路的 VPN 裝置，且發生連線問題 tooAzure 路由式 VPN 閘道，執行下列步驟的 hello:

1. 請檢查 Palo Alto 網路裝置 hello 韌體版本。 如果超過 7.1.4 PAN-OS 版本，升級 too7.1.4。
2. 在 hello Palo Alto 網路裝置，請變更 hello 階段 2 SA （或快速模式 SA） 存留期 too28 800 秒 （8 小時） 時連線 toohello Azure VPN 閘道。
3. 如果您仍然遇到連線問題，請從 hello Azure 入口網站開啟支援要求。
