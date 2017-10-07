---
title: "aaaBind 現有的自訂 SSL 憑證 tooAzure Web 應用程式 |Microsoft 文件"
description: "了解 tootoobind，自訂 SSL 憑證 tooyour web 應用程式、 行動裝置應用程式後端或在 Azure App Service API 應用程式。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a>繫結現有自訂 SSL 憑證 tooAzure Web 應用程式

Azure Web Apps 提供可高度擴充、自我修復的 Web 主機服務。 此教學課程會示範如何自訂 SSL toobind 您太購自受信任的憑證授權單位憑證[Azure Web Apps](app-service-web-overview.md)。 當您完成時，您會無法 tooaccess web 應用程式在您的自訂 DNS 網域的 hello HTTPS 端點。

![Web 應用程式與自訂 SSL 憑證](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 升級應用程式的定價層
> * 繫結您自訂的 SSL 憑證 tooApp 服務
> * 為應用程式強制使用 HTTPS
> * 使用指令碼來自動繫結 SSL 憑證

> [!NOTE]
> 如果您需要 tooget 自訂的 SSL 憑證，可以直接取得 hello Azure 入口網站中的其中一個，並將它繫結 tooyour web 應用程式。 請遵循 hello [App Service 憑證教學課程](web-sites-purchase-ssl-web-site.md)。

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

- [建立 App Service 應用程式](/azure/app-service/)
- [對應的自訂 DNS 名稱 tooyour web 應用程式](app-service-web-tutorial-custom-domain.md)
- 取得受信任憑證授權單位所核發的 SSL 憑證

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a>SSL 憑證的需求

toouse App Service 中的憑證，hello 憑證必須符合下列需求的所有 hello:

* 由受信任的憑證授權單位簽署
* 以受密碼保護的 PFX 檔案形式匯出
* 包含長度至少為 2048 位元的私密金鑰
* 包含 hello 憑證鏈結中的所有中繼憑證

> [!NOTE]
> **橢圓曲線密碼編譯 (ECC) 憑證**可搭配 App Service 使用，但不在本文討論範圍內。 使用 hello 確切步驟 toocreate ECC 憑證上的憑證授權單位。

## <a name="prepare-your-web-app"></a>準備您的 Web 應用程式

toobind 自訂 SSL 憑證 tooyour web 應用程式，您[App Service 方案](https://azure.microsoft.com/pricing/details/app-service/)必須在 hello**基本**，**標準**，或**Premium**層。 在此步驟中，您確定，您的 web 應用程式在 hello 支援定價層。

### <a name="log-in-tooazure"></a>登入 tooAzure

開啟 hello [Azure 入口網站](https://portal.azure.com)。

### <a name="navigate-tooyour-web-app"></a>瀏覽 tooyour web 應用程式

從 hello 左窗格中，按一下 **應用程式服務**，然後按一下hello web 應用程式名稱。

![選取 Web 應用程式](./media/app-service-web-tutorial-custom-ssl/select-app.png)

您處於 hello 管理您的 web 應用程式 頁面。  

### <a name="check-hello-pricing-tier"></a>核取 hello 定價層

在 hello 左側瀏覽您的 web 應用程式頁面，捲動 toohello**設定**區段，然後選取**向上擴充 （應用程式服務方案）**。

![相應增加功能表](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

請確定您的 web 應用程式不在 hello toomake**免費**或**共用**層。 系統會以深藍色方塊醒目顯示 Web 應用程式目前的層。

![檢查定價層](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

不支援自訂 SSL hello**免費**或**共用**層。 如果您需要 tooscale 總時，請遵循 hello 下一節中的 hello 步驟。 否則，請關閉 hello**選擇定價層**頁面上，並略過太[上傳和 SSL 憑證繫結](#upload)。

### <a name="scale-up-your-app-service-plan"></a>相應增加您的 App Service 方案

選取其中一個 hello**基本**，**標準**，或**Premium**層。

按一下 [選取] 。

![選擇定價層](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

當您看到下列通知 hello 時，hello 調整規模作業已完成。

![相應增加通知](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a>繫結 SSL 憑證

您已準備好 tooupload SSL 憑證 tooyour web 應用程式。

### <a name="merge-intermediate-certificates"></a>合併中繼憑證

如果您的憑證授權單位可提供您多個憑證 hello 憑證鏈結中，您需要為了 toomerge hello 憑證。 

toodo 這開啟每個憑證所收到的文字編輯器中。 

建立 hello 合併憑證，請呼叫檔案_mergedcertificate.crt_。 在文字編輯器中，將複製到這個檔案的 hello 內容的每個憑證。 憑證的 hello 順序看起來應該像 hello 下列範本：

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a>匯出憑證 tooPFX

使用 hello 私用金鑰來產生憑證要求匯出合併的 SSL 憑證。

如果您是使用 OpenSSL 產生憑證要求，則已建立私密金鑰檔案。 tooexport 您憑證 tooPFX，執行下列命令的 hello。 Hello 預留位置取代_&lt;私用金鑰檔 >_和_&lt;合併憑證檔案 >_。

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

請在出現提示時定義一個匯出密碼。 上傳您 SSL 憑證 tooApp 服務更新版本時，您將使用此密碼。

如果您使用 IIS 或_Certreq.exe_ toogenerate 您的憑證要求、 安裝 hello 憑證 tooyour 本機電腦，然後[匯出 hello 憑證 tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx)。

### <a name="upload-your-ssl-certificate"></a>上傳 SSL 憑證

tooupload SSL 憑證，請按一下**SSL 憑證**hello 左瀏覽 web 應用程式中。

按一下 [上傳憑證]。

在 [PFX 憑證檔案] 中，選取您的 PFX 檔案。 在**憑證密碼**，匯出 hello PFX 檔案時，您所建立的型別 hello 密碼。

按一下 [上傳] 。

![Upload certificate](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

當應用程式服務完成上傳您的憑證時，它會出現在 hello **SSL 憑證**頁面。

![Certificate uploaded](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a>繫結 SSL 憑證

在 hello **SSL 繫結**區段中，按一下**新增繫結**。

在 hello**新增 SSL 繫結**頁面上，使用 hello 下拉式清單 tooselect hello 網域名稱 toosecure 和 hello 憑證 toouse。

> [!NOTE]
> 如果您已上傳您的憑證，但是看 hello 網域名稱在 hello **Hostname**下拉式清單中，請嘗試重新整理 hello 瀏覽器頁面。
>
>

在**SSL 類型**，選取是否 toouse **[伺服器名稱指示 (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** 或以 IP 為主的 SSL。

- **以 SNI 為基礎的 SSL**：可能會新增多個以 SNI 為基礎的 SSL 繫結。 此選項可讓多個 SSL 憑證 toosecure hello 上的多個網域相同的 IP 位址。 大多數現代化的瀏覽器 (包括 Internet Explorer、Chrome、Firefox 和 Opera) 都支援 SNI (可在[伺服器名稱指示](http://wikipedia.org/wiki/Server_Name_Indication)找到更完整的瀏覽器支援資訊)。
- **以 IP 為基礎的 SSL**：可能只會新增一個以 IP 為基礎的 SSL 繫結。 此選項可讓只有一個 SSL 憑證 toosecure 專用的公用 IP 位址。 toosecure 多個網域，您必須保護它們全部透過 hello 相同的 SSL 憑證。 這是以 SSL 繫結的 hello 傳統選項。

按一下 [新增繫結]。

![繫結 SSL 憑證](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

當應用程式服務完成上傳您的憑證時，它會出現在 hello **SSL 繫結**區段。

![憑證繫結 tooweb 應用程式](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a>將 IP SSL 的 A 記錄重新對應

如果您不在您 web 應用程式中使用 IP SSL，請略過太[測試您的自訂網域的 HTTPS](#test)。

根據預設，web 應用程式會使用共用的公用 IP 位址。 當您將以 IP 為基礎的 SSL 與憑證繫結時，App Service 會為 Web 應用程式建立新的專用 IP 位址。

如果您已對應的記錄 tooyour web 應用程式，您的網域登錄以更新這個新的專用 IP 位址。

Web 應用程式的**自訂網域**hello 新的專用 IP 位址更新頁面。 [複製此 IP 位址](app-service-web-tutorial-custom-domain.md#info)，然後[重新對應 hello 記錄](app-service-web-tutorial-custom-domain.md#map-an-a-record)toothis 新的 IP 位址。

<a name="test"></a>

## <a name="test-https"></a>測試 HTTPS

所有已離開 toodo 是 toomake 確定 HTTPS 適合您的自訂網域。 在不同的瀏覽器中瀏覽過`https://<your.custom.domain>`toosee，設定您的 web 應用程式。

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> 如果您的 web 應用程式出現憑證驗證錯誤，您可能使用了自我簽署憑證。
>
> 如果不是 hello 案例，您可能有遺漏的中繼憑證匯出您的憑證 toohello PFX 檔案時。

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a>強制使用 HTTPS

App Service 不會強制使用 HTTPS，因此任何使用者仍可以使用 HTTP 存取您的 Web 應用程式。 web 應用程式的 HTTPS tooenforce 定義重寫規則中 hello _web.config_ web 應用程式的檔案。 應用程式服務會使用這個檔案，不論 hello 語言架構 web 應用程式。

> [!NOTE]
> 有語言特定的要求重新導向。 ASP.NET MVC 可使用 hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)篩選器，而不是在 hello 重寫規則_web.config_。

如果您是 .NET 開發人員，應該很熟悉這個檔案。 它會在您方案的 hello 根目錄。

此外，如果您是使用 PHP、Node.js、Python 或 Java 進行開發，我們有可能會在 App Service 中代表您產生這個檔案。

Tooyour web 應用程式的 FTP 端點連接在 hello 指示[部署您使用 FTP/S 的應用程式服務的應用程式 tooAzure](app-service-deploy-ftp.md)。

此檔案應該位於 _/home/site/wwwroot_。 如果沒有，請建立_web.config_以下列 XML 的 hello 這個資料夾中的檔案：

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

現有_web.config_檔案中，複製 hello 整個`<rule>`項目插入您_web.config_的`configuration/system.webServer/rewrite/rules`項目。 如果有其他`<rule>`中的項目您_web.config_，複製的位置 hello`<rule>`之前 hello 其他項目`<rule>`項目。

每當 hello 使用者提出 HTTP 要求 tooyour web 應用程式時，此規則就會傳回 HTTP 301 （永久重新導向） toohello HTTPS 通訊協定。 例如，它會重新導向從`http://contoso.com`太`https://contoso.com`。

如需有關 hello IIS URL Rewrite 模組的詳細資訊，請參閱 hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite)文件。

## <a name="enforce-https-for-web-apps-on-linux"></a>強制 Linux 上的 Web Apps 使用 HTTPS

Linux 上的 App Service 不會強制使用 HTTPS，因此任何使用者仍可以使用 HTTP 存取您的 Web 應用程式。 web 應用程式的 HTTPS tooenforce 定義重寫規則中 hello _.htaccess_ web 應用程式的檔案。 

Tooyour web 應用程式的 FTP 端點連接在 hello 指示[部署您使用 FTP/S 的應用程式服務的應用程式 tooAzure](app-service-deploy-ftp.md)。

在_/home/site/wwwroot_，建立_.htaccess_檔案以下列程式碼的 hello:

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

每當 hello 使用者提出 HTTP 要求 tooyour web 應用程式時，此規則就會傳回 HTTP 301 （永久重新導向） toohello HTTPS 通訊協定。 例如，它會重新導向從`http://contoso.com`太`https://contoso.com`。

## <a name="automate-with-scripts"></a>使用指令碼進行自動化

您可以自動化的 SSL 繫結的 web 應用程式與指令碼，使用 hello [Azure CLI](/cli/azure/install-azure-cli)或[Azure PowerShell](/powershell/azure/overview)。

### <a name="azure-cli"></a>Azure CLI

hello 下列命令會將匯出的 PFX 檔案上傳，並取得 hello 指紋。

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

hello 下列命令會將使用 hello 指紋 hello 前一個命令從 sni SSL 繫結。

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a>Azure PowerShell

hello 下列命令將匯出的 PFX 檔案上傳並新增 sni SSL 繫結。

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 升級應用程式的定價層
> * 繫結您自訂的 SSL 憑證 tooApp 服務
> * 為應用程式強制使用 HTTPS
> * 使用指令碼來自動繫結 SSL 憑證

如何前進 toohello 下一個教學課程 toolearn toouse Azure 內容傳遞網路。

> [!div class="nextstepaction"]
> [將內容傳遞網路 (CDN) tooan Azure App Service](app-service-web-tutorial-content-delivery-network.md)
