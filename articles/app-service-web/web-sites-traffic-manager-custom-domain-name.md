---
title: "aaaConfigure web 應用程式中使用流量管理員進行負載平衡的 Azure App Service 中的自訂網域名稱。"
description: "在包含負載平衡的流量管理員的 Azure App Service 中使用 Web 應用程式的自訂網域名稱。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a>在使用流量管理員的 Azure App Service 中設定 Web 應用程式的自訂網域名稱
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

本文提供對 Azure App Service (使用流量管理員進行負載平衡的網站) 使用自訂網域名稱的一般指示。

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>了解 DNS 記錄
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a>將 Web 應用程式設定為標準模式
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>新增自訂網域的 DNS 記錄
> [!NOTE]
> 如果您已購買通過 Azure App Service Web 應用程式網域則略過下列步驟，而且 toohello 最後一個步驟，請參閱[購買 Web 應用程式網域](custom-dns-web-site-buydomains-web-app.md)發行項。
> 
> 

tooassociate 您使用 Azure App Service 中的 web 應用程式的自訂網域，您必須新增新的項目 hello DNS 資料表中的自訂網域使用 hello 網域註冊機構購買您的網域名稱，從所提供的工具。 使用下列步驟 toolocate hello 並使用 hello DNS 工具。

1. 登入 tooyour 帳戶在網域註冊機構，並尋找頁面，以管理 DNS 記錄。 查詢的連結或 hello 網站的區域標示為**網域名稱**， **DNS**，或**名稱伺服器管理**。 通常可以找到 toothis 頁面的連結可檢視您帳戶的資訊，和例如尋找連結**我的網域**。
2. 一旦找到 hello 管理頁面的網域名稱，尋找可讓您 tooedit hello DNS 記錄的連結。 這可能會以 **Zone file****DNS Records** 或 **Advanced** 組態連結的形式列出。
   
   * hello 頁面最有可能已經建立，例如項目產生關聯的一些記錄 '**@**'或'\*' 與 '網域停車' 頁面。 它也可能包含常見子網域 (如 **www**) 的記錄。
   * hello 頁面會提到**CNAME 記錄**，或是提供下拉式清單 tooselect 記錄類型。 它也可能提及其他記錄 (如 **A 記錄**和 **MX 記錄**)。 在部分情況下，會以其他名稱來稱呼 CNAME 記錄，如 **別名記錄**。
   * hello 頁面也可讓您太欄位**對應**從**主機名稱**或**網域名稱**tooanother 網域名稱。
3. 每個註冊機構的 hello 細節有所不同，一般來說您對應*從*自訂網域名稱 (例如**contoso.com**，)*至*hello Traffic Manager 網域名稱 (**contoso.trafficmanager.net**) 所用的 web 應用程式。
   
   > [!NOTE]
   > 或者，如果記錄已在使用，而且需要 toopreemptively 繫結的應用程式 tooit，您可以建立額外的 CNAME 記錄。 例如，繫結 toopreemptively **www.contoso.com** tooyour web 應用程式，建立 CNAME 記錄從**awverify.www**太**contoso.trafficmanager.net**。 然後，您可以加入"www.contoso.com"tooyour Web 應用程式而不需要變更 hello"www"CNAME 記錄。 如需詳細資訊，請參閱[在自訂網域中建立 Web 應用程式的 DNS 記錄][CREATEDNS]。
   > 
   > 
4. 當您完成後，在加入或修改在註冊機構的 DNS 記錄時，儲存 hello 變更。

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a>啟用流量管理員
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 hello [Node.js 開發人員中心](/develop/nodejs/)。

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
