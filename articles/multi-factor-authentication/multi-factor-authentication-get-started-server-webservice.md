---
title: "aaaAzure MFA Server Mobile App Web Service |Microsoft 文件"
description: "hello Microsoft 驗證器應用程式提供額外的頻外驗證選項。  它可讓 hello MFA server toouse 推播通知 toousers。"
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 6c8d6fcc-70f4-4da4-9610-c76d66635b8b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 4175b68fcbf85ec3fd53d8edf4e07306c75a4c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-mobile-app-authentication-with-azure-multi-factor-authentication-server"></a>使用 Azure Multi-Factor Authentication Server 來啟用行動應用程式驗證

hello Microsoft 驗證器應用程式提供額外的頻外驗證選項。 而非自動的撥打電話或 SMS toohello 使用者在登入期間，Azure Multi-factor Authentication 將 hello 使用者的智慧型手機或平板電腦上推入通知 toohello Microsoft Authenticator 應用程式。 hello 使用者只需點選**確認**（或輸入 PIN 並點選 [驗證]） 中 hello 應用程式 toocomplete 其登入。

當手機收訊不可靠時，建議使用行動應用程式進行兩步驟驗證。 如果您使用 hello 應用程式為 OATH 權杖產生器時，不需要任何網路或網際網路連線。

根據您的環境中，您可以在 hello toodeploy hello 行動裝置應用程式 web 服務相同的伺服器以 Azure Multi-factor Authentication Server 或在另一個網際網路對向伺服器上。

## <a name="requirements"></a>需求

toouse hello Microsoft 驗證器應用程式，hello 需要下列憑證以便 hello 應用程式可以順利進行通訊與 Mobile App Web Service:

* Azure Multi-Factor Authentication Server 6.0 或更新版本
* 將 Mobile App Web 服務安裝在執行 Microsoft® [Internet Information Services (IIS) IIS 7.x 或更新版本](http://www.iis.net/)的網際網路對向 Web 伺服器上
* 安裝、 登錄，並設定 tooAllowed ASP.NET v4.0.30319
* 所需的角色服務包括 ASP.NET 和 IIS 6 Metabase 相容性
* 可透過公用 URL 存取 Mobile App Web 服務
* 已使用 SSL 憑證來保護 Mobile App Web 服務。
* Hello Azure Multi-factor Authentication Web 服務 SDK 安裝在 IIS 7.x 或更高版本上 hello **hello Azure Multi-factor Authentication Server 與相同的伺服器**
* 使用 SSL 憑證保護 hello Azure Multi-factor Authentication Web 服務 SDK。
* 行動裝置應用程式 Web 服務可以透過 SSL 連線 toohello Azure Multi-factor Authentication Web 服務 SDK
* 行動裝置應用程式 Web 服務可以驗證 toohello Azure MFA Web 服務 SDK 使用 hello hello"PhoneFactor Admins"安全性群組的成員將服務帳戶的認證。 此服務帳戶和群組存在於 Active Directory hello Azure Multi-factor Authentication Server 是否已加入網域的伺服器上。 此服務帳戶和群組存在於本機 hello Azure Multi-factor Authentication Server 上如果不是聯結的 tooa 網域。

## <a name="install-hello-mobile-app-web-service"></a>安裝 hello 行動裝置應用程式 web 服務

在安裝之前 hello 行動裝置應用程式 web 服務，請留意下列詳細資料的 hello:

* 您需要屬於 "PhoneFactor Admins" 群組的服務帳戶。 此帳戶可以是的 hello 相同 hello 其中一個用於 hello 使用者入口網站安裝。
* 它是很有幫助 tooopen hello 網際網路對向網頁伺服器上的網頁瀏覽器並瀏覽 toohello hello hello web.config 檔案中所輸入的 Web 服務 SDK URL。 如果 hello 瀏覽器可以順利取得 toohello web 服務，它應該提示您輸入認證。 輸入 hello 使用者名稱和 hello 檔案中出現的相同輸入 hello web.config 檔案的密碼。 確定未出現任何憑證警告或錯誤。
* 如果反向 proxy 或防火牆是場合的 hello Mobile App Web Service 網頁伺服器，且正在執行 SSL 卸載，您可以編輯 hello Mobile App Web Service 的 web.config 檔案，好讓 hello 行動裝置應用程式 Web 服務可以使用 http 而非 https。 從 hello 行動裝置應用程式 toohello 防火牆/反向 proxy 仍然需要 SSL。 新增下列金鑰 toohello hello \<appSettings\> > 一節：

        <add key="SSL_REQUIRED" value="false"/>

### <a name="install-hello-web-service-sdk"></a>安裝 hello web 服務 SDK

在任一案例中，如果 hello Azure Multi-factor Authentication Web 服務 SDK 是**不**hello Azure Multi-factor Authentication (MFA) 伺服器上已安裝，完成 hello 步驟後面。

1. 開啟 hello Multi-factor Authentication Server 主控台。
2. 移 toohello **Web 服務 SDK**選取**安裝 Web 服務 SDK**。
3. 使用 hello 預設值，除非您需要 toochange 完成 hello 安裝它們，因為某些原因。
4. 繫結在 IIS 中的 SSL 憑證 toohello 站台。

如果您有關於 IIS 伺服器上設定 SSL 憑證問題，請參閱 hello 文章[如何 tooSet 上 IIS 的 SSL](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis)。

hello Web 服務 SDK 必須使用 SSL 憑證保護。 自我簽署憑證適用於這項用途。 憑證匯入 hello hello hello hello 使用者入口網站網頁伺服器上的本機電腦帳戶的 「 信任的根憑證授權單位 存放區，以便起始 hello SSL 連線時信任該憑證。

![MFA Server 組態設定 Web 服務 SDK](./media/multi-factor-authentication-get-started-server-webservice/sdk.png)

### <a name="install-hello-service"></a>安裝 hello 服務

1. **在 hello MFA Server**，瀏覽 toohello 安裝路徑。
2. 瀏覽 toohello 資料夾 hello Azure MFA Server 就已安裝的 hello 預設是**C:\Program Files\Azure Multi-factor Authentication**。
3. 找出 hello 安裝檔案**MultiFactorAuthenticationMobileAppWebServiceSetup64**。 如果伺服器 hello**不**網際網路對向，複製 hello 安裝檔案 toohello 網際網路對向伺服器。
4. Hello MFA 伺服器是否**不**網際網路對向交換器 toohello**網際網路對向伺服器**。
5. 執行 hello **MultiFactorAuthenticationMobileAppWebServiceSetup64**身為系統管理員安裝檔案，如有需要，變更 hello 站台和變更 hello 虛擬目錄 tooa 簡短名稱，如果您想要。
6. 分頁裝訂 hello 安裝之後，瀏覽過**C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService** （或根據 hello 虛擬目錄名稱的適當目錄），並編輯 hello Web.Config 檔案。

   * 尋找 hello 金鑰**"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"**並變更**值 =""**太**值 = 「 網域 \ 使用者 」**其中網域 \ 使用者是屬於的服務帳戶「 PhoneFactor 系統管理員 」 群組。
   * 尋找 hello 金鑰**"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"**並變更**值 =""**太**值 ="Password"**密碼所在 hello 服務的 hello 密碼在 hello 前一行中輸入的帳戶。
   * 尋找 hello **pfMobile App Web Service_pfwssdk_PfWsSdk**設定和變更 hello 值從**http://localhost:4898/PfWsSdk.asmx** toohello Web 服務 SDK URL (範例： https://mfa.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx)。
   * 儲存 hello Web.Config 檔案並關閉 [記事本]。

   > [!NOTE]
   > 因為此連線使用 SSL，您必須參考 hello 由 Web 服務 SDK**完整的網域名稱 (FQDN)**和**不是 IP 位址**。 hello SSL 憑證會核發 hello FQDN，而且 hello 用的 URL 必須符合 hello hello 憑證名稱。

7. 如果 hello 網站底下安裝 Mobile App Web Service 已不已繫結使用公開簽署的憑證，hello 伺服器上安裝 hello 憑證、 開啟 IIS 管理員，並繫結 hello 憑證 toohello 網站。
8. 從任何電腦開啟網頁瀏覽器並瀏覽 toohello 安裝 Mobile App Web Service 的 URL (範例： https://mfa.contoso.com/MultiFactorAuthMobileAppWebService)。 確定未出現任何憑證警告或錯誤。

## <a name="configure-hello-mobile-app-settings-in-hello-azure-multi-factor-authentication-server"></a>在 hello Azure Multi-factor Authentication Server 中設定 hello 行動裝置應用程式設定

既然 hello 行動裝置應用程式 web 服務已安裝，您會需要 tooconfigure hello Azure Multi-factor Authentication Server toowork hello 入口網站。

1. 在 hello Multi-factor Authentication Server 主控台的 hello 使用者入口網站 圖示。 如果允許使用者 toocontrol 其驗證方法，請檢查**行動裝置應用程式**hello 設定 索引標籤底下**tooselect 方法可讓使用者**。 未啟用這個功能，使用者會需要的 toocontact 服務台 toocomplete 啟用 hello 行動裝置應用程式。
2. 檢查 hello**允許行動裝置應用程式的使用者 tooactivate**方塊。
3. 檢查 hello**允許使用者註冊**方塊。
4. 按一下 hello**行動裝置應用程式**圖示。
5. 輸入 hello hello 安裝 MultiFactorAuthenticationMobileAppWebServiceSetup64 時所建立的虛擬目錄搭配使用的 URL (範例： https://mfa.contoso.com/MultiFactorAuthMobileAppWebService/) 在 hello 欄位**行動應用程式 Web 服務 URL:**。
6. 填入 hello**帳戶名稱**hello 這個帳戶的行動應用程式中的 hello 公司或組織名稱 toodisplay 欄位。
   ![MFA Server 組態行動裝置應用程式設定](./media/multi-factor-authentication-get-started-server-webservice/mobile.png)

## <a name="next-steps"></a>後續步驟

- [使用 Azure Multi-Factor Authentication 與協力廠商 VPN 的進階案例](multi-factor-authentication-advanced-vpn-configurations.md)。