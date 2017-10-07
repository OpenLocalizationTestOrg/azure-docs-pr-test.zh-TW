---
title: "aaaPoint 公司網際網路網域 tooa Traffic Manager 網域名稱 |Microsoft 文件"
description: "本文將協助您點將公司網域名稱 tooa Traffic Manager 網域名稱。"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a>點將公司網際網路網域 tooan Azure Traffic Manager 網域

當您建立流量管理員設定檔時，Azure 會自動為該設定檔指派 DNS 名稱。 toouse 從您的 DNS 區域的名稱建立的 CNAME DNS 記錄，將您的 Traffic Manager 設定檔的 toohello 網域名稱對應。 您可以在 hello 找到 hello Traffic Manager 網域名稱**一般**hello 組態 頁面上的 hello Traffic Manager 設定檔 > 一節。

比方說，toopoint 名稱 www.contoso.com toohello Traffic Manager DNS 名稱 contoso.trafficmanager.net，您會建立下列 DNS 資源記錄的 hello:

    www.contoso.com IN CNAME contoso.trafficmanager.net

所有流量都要求太*www.contoso.com*太導向*contoso.trafficmanager.net*。

> [!IMPORTANT]
> 您無法指向第二層網域，例如*contoso.com*，toohello Traffic Manager 網域。 DNS 通訊協定標準不允許第二層網域名稱的 CNAME 記錄。

## <a name="next-steps"></a>後續步驟

* [流量管理員路由方法](traffic-manager-routing-methods.md)
* [流量管理員 - 停用、啟用或刪除設定檔](disable-enable-or-delete-a-profile.md)
* [流量管理員 - 停用或啟用端點](disable-or-enable-an-endpoint.md)
