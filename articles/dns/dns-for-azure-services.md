---
title: "與其他 Azure 服務的 Azure DNS aaaUsing |Microsoft 文件"
description: "了解 toouse Azure DNS tooresolve 其他 Azure 服務的名稱"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure dns
ms.assetid: e9b5eb94-7984-4640-9930-564bb9e82b78
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 09/21/2016
ms.author: gwallace
ms.openlocfilehash: 791f93d6aff2c638c08518e9f1e8ab89ac8de3f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-dns-works-with-other-azure-services"></a>Azure DNS 如何與其他 Azure 服務搭配運作

Azure DNS 是一種託管的 DNS 管理與名稱解析服務。 這可讓您 toocreate 公用 DNS 名稱 hello 其他應用程式和您在 Azure 中部署的服務。 在您的自訂網域中建立一項 Azure 服務的名稱很簡單，只將記錄新增到服務的 hello 正確的型別。

* 動態配置的 IP 位址，您必須建立 DNS CNAME 記錄 Azure 建立該對應 toohello DNS 名稱為您的服務。 DNS 標準會防止您 hello 區域的 apex 使用 CNAME 記錄。
* 以靜態方式配置的 IP 位址，您可以建立使用任何名稱，DNS A 記錄包括*naked 網域*在 hello 區域的 apex 名稱。

hello 下列資料表外框 hello 支援可用於各種 Azure 服務的記錄類型。 如您在表中所見，Azure DNS 只支援網際網路面向網路資源的 DNS 記錄。 Azure DNS 無法用於內部私人位址的名稱解析。

| Azure 服務 | 網路介面 | 說明 |
| --- | --- | --- |
| 應用程式閘道 |[前端公用 IP](dns-custom-domain.md#public-ip-address) |您可以建立 DNS A 或 CNAME 記錄。 |
| 負載平衡器 |[前端公用 IP](dns-custom-domain.md#public-ip-address)  |您可以建立 DNS A 或 CNAME 記錄。 負載平衡器可以有動態指派的 IPv6 公用 IP 位址。 因此，您必須建立用於 IPv6 位址的 CNAME 記錄。 |
| 流量管理員 |公開名稱 |您只能建立 CNAME，將對應指派 tooyour Traffic Manager 設定檔的 toohello trafficmanager.net 名稱。 如需詳細資訊，請參閱 [流量管理員的運作方式](../traffic-manager/traffic-manager-overview.md#traffic-manager-example)。 |
| 服務雲端 |[公用 IP](dns-custom-domain.md#public-ip-address) |若使用靜態配置的 IP 位址，您可以建立 DNS A 記錄。 動態配置的 IP 位址，您必須建立一筆 CNAME 記錄對應 toohello *.cloudapp.net*名稱。 此規則會套用 tooVMs hello 傳統入口網站中建立，因為它們做為雲端服務部署。 如需詳細資訊，請參閱 [在 雲端服務中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。 |
| App Service | [外部 IP](dns-custom-domain.md#app-service-web-apps) |若使用外部 IP 位址，您可以建立 DNS A 記錄。 否則，您必須建立對應 toohello.azurewebsites.net 名稱的 CNAME 記錄。 如需詳細資訊，請參閱[對應自訂網域名稱 tooan Azure 應用程式](../app-service-web/web-sites-custom-domain-name.md) |
| Resource Manager VM |[公用 IP](dns-custom-domain.md#public-ip-address) |Resource Manager VM 可以有公用 IP 位址。 帶有公用 IP 位址的 VM 也可能擺在負載平衡器後。 您可以建立 hello 公用位址的 DNS A 或 CNAME 記錄。 Hello 負載平衡器上的使用的 toobypass hello VIP 時，可以將這個自訂的名稱。 |
| 傳統 VM |[公用 IP](dns-custom-domain.md#public-ip-address) |使用 PowerShell 或 CLI 建立的傳統 VM 可設定為使用動態或靜態 (保留) 的虛擬位址。 您可以分別建立 DNS CNAME 或 A 記錄。 |
