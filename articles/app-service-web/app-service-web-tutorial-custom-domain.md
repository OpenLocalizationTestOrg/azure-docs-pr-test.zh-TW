---
title: "aaaMap 現有的自訂 DNS 命名 tooAzure Web 應用程式 |Microsoft 文件"
description: "了解如何 tooadd 現有的自訂 DNS 網域名稱 （虛名網域） tooa web 應用程式、 行動裝置應用程式後端或在 Azure App Service API 應用程式。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a>將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應

[Azure Web Apps](app-service-web-overview.md) 提供可高度擴充、自我修復的 Web 主機服務。 本教學課程會示範如何 toomap 現有的自訂 DNS 命名 tooAzure Web 應用程式。

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 使用 CNAME 記錄來對應子網域 (例如，`www.contoso.com`)
> * 使用 A 記錄來對應根網域 (例如，`contoso.com`)
> * 使用 CNAME 記錄來對應萬用字元網域 (例如，`*.contoso.com`)
> * 使用指令碼來自動對應網域

您可以使用**CNAME 記錄**或**記錄**toomap 自訂的 DNS 名稱 tooApp 服務。 

> [!NOTE]
> 我們建議您對所有自訂 DNS 名稱使用 CNAME，但根網域除外 (例如 `contoso.com`)。

toomigrate 即時網站和其 DNS 網域名稱 tooApp 服務，請參閱[移轉作用中的 DNS 名稱 tooAzure App Service](app-service-custom-domain-name-migrate.md)。

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

* [建立 App Service 應用程式](/azure/app-service/)，或使用您針對另一個教學課程建立的應用程式。
* 購買網域名稱，並確定您的網域提供者 （例如 GoDaddy) 存取 toohello DNS 登錄。

  例如，tooadd DNS 項目`contoso.com`和`www.contoso.com`，您必須是能夠 tooconfigure hello DNS 設定 hello`contoso.com`根網域。

  > [!NOTE]
  > 如果您沒有現有的網域名稱，請考慮[購買網域使用 hello Azure 入口網站](custom-dns-web-site-buydomains-web-app.md)。 

## <a name="prepare-hello-app"></a>準備 hello 應用程式

toomap 自訂 DNS 名稱 tooa web 應用程式，hello web 應用程式的[App Service 方案](https://azure.microsoft.com/pricing/details/app-service/)必須付費的層 (**共用**，**基本**，**標準**，或**進階**)。 在此步驟中，您確定該 hello App Service 應用程式是在 hello 支援定價層。

### <a name="sign-in-tooazure"></a>登入 tooAzure

開啟 hello [Azure 入口網站](https://portal.azure.com)並以您的 Azure 帳戶登入。

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>瀏覽 toohello hello Azure 入口網站中的應用程式

從 hello 左窗格中，選取**應用程式服務**，然後選取 hello hello 應用程式名稱。

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/select-app.png)

您會看到 hello hello App Service 應用程式管理頁面。  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a>核取 hello 定價層

在 hello 左瀏覽的 hello 應用程式頁面，捲動 toohello**設定**區段，然後選取**向上擴充 （應用程式服務方案）**。

![相應增加功能表](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

hello 應用程式目前的階層會以藍色框線反白顯示。 請確定該 hello 應用程式不在 hello toomake**免費**層。 不支援自訂 DNS hello**免費**層。 

![檢查定價層](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

如果 hello App Service 方案不**免費**，請關閉 hello**選擇定價層**頁面上，並略過太[CNAME 記錄對應](#cname)。

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a>向上擴充 hello App Service 方案

選取任何 hello 非可用層 (**共用**，**基本**，**標準**，或**Premium**)。 

按一下 [選取] 。

![檢查定價層](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

當您看到下列通知 hello 時，hello 調整規模作業已完成。

![擴充作業確認](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a>對應 CNAME 記錄

您可以在 hello 教學課程範例中，加入 hello 的 CNAME 記錄`www`子網域 (例如， `www.contoso.com`)。

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>建立 hello CNAME 記錄

新增子網域 toohello 應用程式的預設主機名稱的 CNAME 記錄 toomap (`<app_name>.azurewebsites.net`)。

Hello`www.contoso.com`網域範例中，新增 CNAME 記錄對應 hello 名稱`www`太`<app_name>.azurewebsites.net`。

您新增 hello CNAME 之後，hello DNS 記錄 頁面看起來像下列範例中的 hello 中：

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a>啟用在 Azure 中的 hello CNAME 記錄對應

在 hello 處於 hello Azure 入口網站的導覽 hello 應用程式頁面，選取 **自訂網域**。 

![[自訂網域] 功能表](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

在 hello**自訂網域**頁面 hello 應用程式，加入 hello 完整自訂的 DNS 名稱 (`www.contoso.com`) toohello 清單。

選取 hello  **+** 圖示下一步太**新增 hostname**。

![新增主機名稱](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

型別 hello 完整的網域名稱加入 CNAME 記錄，例如`www.contoso.com`。 

選取 [驗證]。

hello**新增 hostname**按鈕就會啟用。 

請確定**主機名稱記錄類型**設定得**（www.example.com 或任何子網域） 的 CNAME**。

選取 [新增主機名稱]。

![新增 DNS 名稱 toohello 應用程式](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

它可能需要一些時間 hello 反映在 hello 應用程式的新主機名稱 toobe**自訂網域**頁面。 請嘗試重新整理 hello 瀏覽器 tooupdate hello 資料。

![CNAME 記錄已新增](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

如果您錯過步驟或打錯字了某處更早版本，請參閱在 hello hello 頁面底部的驗證錯誤。

![驗證錯誤](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a>對應 A 記錄

您可以在 hello 教學課程範例中，加入 hello 根網域的 A 記錄 (例如， `contoso.com`)。 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a>複製 hello 應用程式的 IP 位址

toomap A 記錄，您需要 hello 應用程式的外部 IP 位址。 您可以在 hello 應用程式中找到這個 IP 位址**自訂網域**hello Azure 入口網站中的頁面。

在 hello 處於 hello Azure 入口網站的導覽 hello 應用程式頁面，選取 **自訂網域**。 

![[自訂網域] 功能表](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

在 hello**自訂網域**頁面上，複製 hello 應用程式的 IP 位址。

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a>建立 hello A 記錄

toomap A 記錄 tooan 應用程式，應用程式服務需要**兩個**DNS 記錄：

- **A** toomap toohello 應用程式的 IP 位址記錄下來。
- A **TXT**記錄 toomap toohello 應用程式的預設主機名稱`<app_name>.azurewebsites.net`。 應用程式服務會使用此記錄只有在設定時，tooverify 您擁有 hello 自訂網域。 驗證您的自訂網域並且在 App Service 中設定之後，您就可以刪除此 TXT 記錄。 

Hello`contoso.com`網域範例中，建立根據下表 toohello hello A 和 TXT 記錄 (`@`通常代表 hello 根網域)。 

| 記錄類型 | Host | 值 |
| - | - | - |
| A | `@` | 從 IP 位址[複製 hello 應用程式的 IP 位址](#info) |
| TXT | `@` | `<app_name>.azurewebsites.net` |

當您加入 hello 記錄時，hello DNS 記錄 頁面看起來像 hello 下列範例中：

![[DNS 記錄] 頁面](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a>啟用 hello 記錄中的對應 hello 應用程式

在 hello 應用程式**自訂網域**在 hello Azure 入口網站頁面上，新增 hello 完整自訂的 DNS 名稱 (例如， `contoso.com`) toohello 清單。

選取 hello  **+** 圖示下一步太**新增 hostname**。

![新增主機名稱](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

型別 hello 完整的網域名稱設定 hello A 記錄，例如`contoso.com`。

選取 [驗證]。

hello**新增 hostname**按鈕就會啟用。 

請確定**主機名稱記錄類型**設定得**記錄 (example.com)**。

選取 [新增主機名稱]。

![新增 DNS 名稱 toohello 應用程式](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

它可能需要一些時間 hello 反映在 hello 應用程式的新主機名稱 toobe**自訂網域**頁面。 請嘗試重新整理 hello 瀏覽器 tooupdate hello 資料。

![A 記錄已新增](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

如果您錯過步驟或打錯字了某處更早版本，請參閱在 hello hello 頁面底部的驗證錯誤。

![驗證錯誤](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a>對應萬用字元網域

在 hello 教學課程範例中，您將對應[萬用字元 DNS 名稱](https://en.wikipedia.org/wiki/Wildcard_DNS_record)(例如， `*.contoso.com`) toohello App Service 應用程式藉由新增一筆 CNAME 記錄。 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>建立 hello CNAME 記錄

新增萬用字元名稱 toohello 應用程式的預設主機名稱的 CNAME 記錄 toomap (`<app_name>.azurewebsites.net`)。

Hello`*.contoso.com`網域範例 hello CNAME 記錄會對應 hello 名稱`*`太`<app_name>.azurewebsites.net`。

當加入 hello CNAME 時，hello DNS 記錄 頁面看起來像 hello 下列範例中：

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a>啟用 hello 應用程式中的 hello CNAME 記錄對應

您現在可以新增任何符合 hello 萬用字元名稱 toohello 應用程式的子網域 (例如，`sub1.contoso.com`和`sub2.contoso.com`符合`*.contoso.com`)。 

在 hello 處於 hello Azure 入口網站的導覽 hello 應用程式頁面，選取 **自訂網域**。 

![[自訂網域] 功能表](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

選取 hello  **+** 圖示下一步太**新增 hostname**。

![新增主機名稱](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

輸入符合 hello 萬用字元網域的完整的網域名稱 (例如， `sub1.contoso.com`)，然後選取**驗證**。

hello**新增 hostname**按鈕就會啟用。 

請確定**主機名稱記錄類型**設定得**（www.example.com 或任何子網域） 的 CNAME 記錄**。

選取 [新增主機名稱]。

![新增 DNS 名稱 toohello 應用程式](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

它可能需要一些時間 hello 反映在 hello 應用程式的新主機名稱 toobe**自訂網域**頁面。 請嘗試重新整理 hello 瀏覽器 tooupdate hello 資料。

選取 hello  **+** 圖示再次 tooadd 與 hello 萬用字元網域相符的另一個主機名稱。 例如，新增 `sub2.contoso.com`。

![CNAME 記錄已新增](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a>在瀏覽器中測試

瀏覽 toohello 您先前設定的 DNS 名稱 (例如， `contoso.com`， `www.contoso.com`， `sub1.contoso.com`，和`sub2.contoso.com`)。

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a>使用指令碼進行自動化

您可以自動化的指令碼，自訂網域管理使用 hello [Azure CLI](/cli/azure/install-azure-cli)或[Azure PowerShell](/powershell/azure/overview)。 

### <a name="azure-cli"></a>Azure CLI 

hello，下列命令會將已設定自訂 DNS 名稱 tooan App Service 應用程式。 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

如需詳細資訊，請參閱[對應自訂網域 tooa web 應用程式](scripts/app-service-cli-configure-custom-domain.md)。 

### <a name="azure-powershell"></a>Azure PowerShell 

hello，下列命令會將已設定自訂 DNS 名稱 tooan App Service 應用程式。 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

如需詳細資訊，請參閱[指派自訂網域 tooa web 應用程式](scripts/app-service-powershell-configure-custom-domain.md)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 使用 CNAME 記錄來對應子網域
> * 使用 A 記錄來對應根網域
> * 使用 CNAME 記錄來對應萬用字元網域
> * 使用指令碼來自動對應網域

前進 toohello 下一個教學課程 toolearn toobind 自訂 SSL 憑證 tooa web 應用程式的方式。

> [!div class="nextstepaction"]
> [繫結現有自訂 SSL 憑證 tooAzure Web 應用程式](app-service-web-tutorial-custom-ssl.md)
