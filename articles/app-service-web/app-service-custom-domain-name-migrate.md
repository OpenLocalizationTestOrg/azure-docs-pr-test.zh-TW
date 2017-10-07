---
title: "aaaMigrate 作用中的 DNS 名稱 tooAzure 應用程式服務 |Microsoft 文件"
description: "了解如何自訂的 DNS 網域名稱已指派 tooa toomigrate 即時網站 tooAzure 應用程式服務不需任何停機。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a>移轉作用中的 DNS 名稱 tooAzure 應用程式服務

本文將告訴您如何 toomigrate 作用中的 DNS 名稱太[Azure App Service](../app-service/app-service-value-prop-what-is.md)完全不需要停機。

當您移轉即時網站和其 DNS 網域名稱 tooApp 服務時，該 DNS 名稱已提供服務的即時流量。 您可以事先繫結使用 DNS 名稱 tooyour hello App Service 應用程式，在 hello 移轉期間避免 DNS 解析中的停機時間。

如果您不擔心 DNS 解析中的停機時間，請參閱[對應現有自訂 DNS 名稱 tooAzure Web 應用程式](app-service-web-tutorial-custom-domain.md)。

## <a name="prerequisites"></a>必要條件

toocomplete 此使用方法：

- [確定您的 App Service 應用程式不是位於免費層](app-service-web-tutorial-custom-domain.md#checkpricing)。

## <a name="bind-hello-domain-name-preemptively"></a>事先繫結 hello 網域名稱

當事先繫結的自訂網域時，您完成這兩個變更 DNS 記錄之前的 hello 下列：

- 確認網域擁有權
- 啟用您的應用程式的 hello 網域名稱

當您最後會從舊網站 toohello hello App Service 應用程式移轉您自訂的 DNS 名稱時，DNS 解析中會有任何停機時間。

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a>建立網域驗證記錄

tooverify 網域擁有權，新增 TXT 記錄。 從對應的 hello TXT 記錄_awverify。&lt;子網域 >_ too_&lt;應用程式名稱 >。 azurewebsites.net_。 

hello TXT 記錄，您需要取決於 hello 想 toomigrate 的 DNS 記錄。 如需範例，請參閱下表中的 hello (`@`通常代表 hello 根網域):  

| DNS 記錄範例 | TXT 主機 | TXT 值 |
| - | - | - |
| @ (根網域) | _awverify_ | _&lt;應用程式名稱>.azurewebsites.net_ |
| www (子網域) | _awverify.www_ | _&lt;應用程式名稱>.azurewebsites.net_ |
| \* (萬用字元) | _awverify.\*_ | _&lt;應用程式名稱>.azurewebsites.net_ |

在您 DNS 記錄 頁面中，記下 hello 記錄類型的 hello 想 toomigrate 的 DNS 名稱。 App Service 支援 CNAME 與 A 記錄之間的對應。

### <a name="enable-hello-domain-for-your-app"></a>啟用您的應用程式的 hello 網域

在 hello [Azure 入口網站](https://portal.azure.com)，在 hello hello 應用程式頁面的左導覽列中選取**自訂網域**。 

![[自訂網域] 功能表](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

在 [hello**自訂網域**頁面上，選取 hello  **+** 圖示下一步] 太**新增主機名稱**。

![新增主機名稱](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

型別 hello 完整的網域名稱新增 hello TXT 記錄，例如`www.contoso.com`。 萬用字元網域 (像是\*。 contoso.com)，您可以使用任何符合 hello 萬用字元網域的 DNS 名稱。 

選取 [驗證]。

hello**新增 hostname**按鈕就會啟用。 

請確定**主機名稱記錄類型**設定您想要 toomigrate toohello DNS 記錄類型。

選取 [新增主機名稱]。

![新增 DNS 名稱 toohello 應用程式](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

它可能需要一些時間 hello 反映在 hello 應用程式的新主機名稱 toobe**自訂網域**頁面。 請嘗試重新整理 hello 瀏覽器 tooupdate hello 資料。

![CNAME 記錄已新增](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

您的 DNS 名稱現已在您的 Azure 應用程式中啟用。 

## <a name="remap-hello-active-dns-name"></a>重新對應 hello 作用中的 DNS 名稱

hello 事左的 toodo 會重新對應您使用中的 DNS 記錄 toopoint tooApp 服務。 右現在，它仍然指向 tooyour 舊的站台。

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a>複製 hello 應用程式的 IP 位址 （只記錄）

如果您重新對應的是 CNAME 記錄，請略過本節。 

tooremap A 記錄，您需要 hello App Service 應用程式的外部 IP 位址，如下所示 hello**自訂網域**頁面。

關閉 hello**新增 hostname**頁面中的選取**X** hello 右上角。 

在 hello**自訂網域**頁面上，複製 hello 應用程式的 IP 位址。

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a>更新 hello DNS 記錄

在 hello 網域提供者的 DNS 記錄頁面上，選取 hello DNS 記錄 tooremap。

Hello`contoso.com`根網域的範例中，重新對應 hello A 或 CNAME 記錄，例如 hello 下表中的 hello 範例： 

| FQDN 範例 | 記錄類型 | Host | 值 |
| - | - | - | - |
| contoso.com (根網域) | A | `@` | 從 IP 位址[複製 hello 應用程式的 IP 位址](#info) |
| www.contoso.com (子網域) | CNAME | `www` | _&lt;應用程式名稱>.azurewebsites.net_ |
| \*.contoso.com (萬用字元) | CNAME | _\*_ | _&lt;應用程式名稱>.azurewebsites.net_ |

儲存您的設定。

DNS 查詢應該只有在 DNS 傳播會發生之後，立即解決 tooyour App Service 應用程式會啟動。

## <a name="next-steps"></a>後續步驟

了解如何 toobind 自訂 SSL 憑證 tooApp 服務。

> [!div class="nextstepaction"]
> [繫結現有自訂 SSL 憑證 tooAzure Web 應用程式](app-service-web-tutorial-custom-ssl.md)
