---
title: "Azure MFA server aaaUser 入口網站 |Microsoft 文件"
description: "這是描述 tooget 如何開始使用 Azure MFA 和 hello 使用者入口網站的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 06b419fa-3507-4980-96a4-d2e3960e1772
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 0e36644c3d780249fb98d5da654e9d267c63561a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="user-portal-for-hello-azure-multi-factor-authentication-server"></a>Hello Azure Multi-factor Authentication Server 使用者入口網站

hello 使用者入口網站是一個 IIS 網站，允許使用者 tooenroll Azure Multi-factor Authentication (MFA)，並維護自己的帳戶。 使用者可能會變更其電話號碼、 變更 PIN，或選擇 toobypass 他們下一步的登入期間的雙步驟驗證。

使用者登入 toohello 一般的使用者名稱與密碼的使用者入口網站，然後完成兩步驟驗證通話或回答安全性問題 toocomplete 驗證。 如果允許使用者註冊，使用者設定其電話號碼和 PIN hello 第一次登入時 toohello 使用者入口網站中。

使用者入口網站管理員可以設定，並授與權限 tooadd 新的使用者及更新現有使用者。

根據您的環境中，您可以在 hello toodeploy hello 使用者入口網站相同的伺服器以 Azure Multi-factor Authentication Server 或在另一個網際網路對向伺服器上。

![MFA 使用者入口網站](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> hello 使用者入口網站才可使用 Multi-factor Authentication Server。 如果您使用多重要素驗證 hello 雲端中，請參閱使用者 toohello[安裝您的帳戶進行兩步驟驗證](./end-user/multi-factor-authentication-end-user-first-time.md)或[管理您的設定進行兩步驟驗證](./end-user/multi-factor-authentication-end-user-manage-settings.md)。

## <a name="install-hello-web-service-sdk"></a>安裝 hello web 服務 SDK

在任一案例中，如果 hello Azure Multi-factor Authentication Web 服務 SDK 是**不**hello Azure Multi-factor Authentication (MFA) 伺服器上已安裝，完成 hello 步驟後面。

1. 開啟 hello Multi-factor Authentication Server 主控台。
2. 移 toohello **Web 服務 SDK**選取**安裝 Web 服務 SDK**。
3. 使用 hello 預設值，除非您需要 toochange 完成 hello 安裝它們，因為某些原因。
4. 繫結在 IIS 中的 SSL 憑證 toohello 站台。

如果您有關於 IIS 伺服器上設定 SSL 憑證問題，請參閱 hello 文章[如何 tooSet 上 IIS 的 SSL](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis)。

hello Web 服務 SDK 必須使用 SSL 憑證保護。 自我簽署憑證適用於這項用途。 憑證匯入 hello hello hello hello 使用者入口網站網頁伺服器上的本機電腦帳戶的 「 信任的根憑證授權單位 存放區，以便起始 hello SSL 連線時信任該憑證。

![MFA Server 組態設定 Web 服務 SDK](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-hello-user-portal-on-hello-same-server-as-hello-azure-multi-factor-authentication-server"></a>部署在 hello hello 使用者入口網站相同的 hello Azure Multi-factor Authentication Server 伺服器

hello 下列必要條件是必要的 tooinstall hello 使用者入口網站上 hello**相同伺服器**hello Azure Multi-factor Authentication Server 如下：

* IIS，包括 ASP.NET 及 IIS 6 metabase 相容性 (適用於 IIS 7 或更高版本)
* 具有 hello 電腦及網域，如果有適用的系統管理員權限的帳戶。 hello 帳戶需要權限 toocreate Active Directory 安全性群組。
* 安全 hello 使用者入口網站的 SSL 憑證。
* 使用 SSL 憑證的安全 hello Azure Multi-factor Authentication Web 服務 SDK。

toodeploy hello 使用者入口網站中，依照下列步驟：

1. 開啟 hello Azure Multi-factor Authentication Server 主控台中，按一下 hello**使用者入口網站**圖示 hello 保留功能表，然後按一下 **安裝使用者入口網站**。
2. 使用 hello 預設值，除非您需要 toochange 完成 hello 安裝它們，因為某些原因。
3. 在 IIS 中的 SSL 憑證 toohello 站台繫結

   > [!NOTE]
   > 此 SSL 憑證通常是公開簽署的 SSL 憑證。

4. 從任何電腦開啟網頁瀏覽器並瀏覽 toohello 安裝 hello 使用者入口網站的 URL (範例： https://mfa.contoso.com/MultiFactorAuth)。 確定未出現任何憑證警告或錯誤。

![MFA Server 使用者入口網站安裝](./media/multi-factor-authentication-get-started-portal/install.png)

如果您有關於 IIS 伺服器上設定 SSL 憑證問題，請參閱 hello 文章[如何 tooSet 上 IIS 的 SSL](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis)。

## <a name="deploy-hello-user-portal-on-a-separate-server"></a>部署一部伺服器上的 hello 使用者入口網站

如果正在 Azure Multi-factor Authentication Server 的 hello 伺服器不是網際網路對向，您應該安裝 hello 使用者入口網站上**個別的網際網路對向伺服器**。

如果組織所使用 hello Microsoft Authenticator 應用程式做為其中一個 hello 驗證方法，並在它自己的伺服器上的 toodeploy hello 使用者入口網站，請完成下列需求的 hello:

* 使用 6.0 版或更高版本的 hello Azure Multi-factor Authentication Server。
* 安裝 hello 使用者入口網站上的網際網路對向網頁伺服器執行 Microsoft internet Information Services (IIS) 6.x 或更高版本。
* 當使用 IIS 6.x 時，請確定 ASP.NET 2.0.50727 版已安裝、 登錄，並設定太**允許**。
* 使用 IIS 7.x 或更高版本時，包括基本驗證、ASP.NET 和 IIS 6 Metabase 相容性。
* 安全 hello 使用者入口網站的 SSL 憑證。
* 使用 SSL 憑證的安全 hello Azure Multi-factor Authentication Web 服務 SDK。
* 確定該 hello 使用者入口網站可透過 SSL 連線 toohello Azure Multi-factor Authentication Web 服務 SDK。
* 請確定該 hello 使用者入口網站可以驗證 toohello Azure Multi-factor Authentication Web 服務 SDK 使用 hello"PhoneFactor Admins"安全性群組中的 hello 的服務帳戶的認證。 此服務帳戶和群組應該存在於 Active Directory 如果 hello Azure Multi-factor Authentication Server 在已加入網域的伺服器上執行。 此服務帳戶和群組存在於本機 hello Azure Multi-factor Authentication Server 上如果不是聯結的 tooa 網域。

Hello Azure Multi-factor Authentication Server 以外的伺服器上安裝 hello 使用者入口網站需要 hello 下列步驟：

1. **在 hello MFA Server**，瀏覽 toohello 安裝路徑 (範例： C:\Program files\multi-factor Authentication Server)，並複製 hello 檔案**MultiFactorAuthenticationUserPortalSetup64** tooa 位置您要安裝它的可存取 toohello 網際網路對向伺服器。
2. **Hello 網際網路對向網頁伺服器上**、 系統管理員身分執行 hello MultiFactorAuthenticationUserPortalSetup64 安裝檔案，如有需要，變更 hello 站台和如果您想要變更 hello 虛擬目錄 tooa 簡短名稱。
3. 繫結在 IIS 中的 SSL 憑證 toohello 站台。

   > [!NOTE]
   > 此 SSL 憑證通常是公開簽署的 SSL 憑證。

4. 瀏覽過**C:\inetpub\wwwroot\MultiFactorAuth**
5. 編輯 [記事本] 中的 hello Web.Config 檔案

    * 尋找 hello 金鑰**"USE_WEB_SERVICE_SDK"**並變更**值 ="false"**太**值 ="true"**
    * 尋找 hello 金鑰**"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"**並變更**值 =""**太**值 = 「 網域 \ 使用者 」**其中網域 \ 使用者是屬於的服務帳戶「 PhoneFactor 系統管理員 」 群組。
    * 尋找 hello 金鑰**"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"**並變更**值 =""**太**值 ="Password"**密碼所在 hello 服務的 hello 密碼在 hello 前一行中輸入的帳戶。
    * 找出 hello 值**https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx**及變更此預留位置 URL toohello 我們在步驟 2 中安裝 Web 服務 SDK URL。
    * 儲存 hello Web.Config 檔案並關閉 [記事本]。

6. 從任何電腦開啟網頁瀏覽器並瀏覽 toohello 安裝 hello 使用者入口網站的 URL (範例： https://mfa.contoso.com/MultiFactorAuth)。 確定未出現任何憑證警告或錯誤。

如果您有關於 IIS 伺服器上設定 SSL 憑證問題，請參閱 hello 文章[如何 tooSet 上 IIS 的 SSL](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis)。

## <a name="configure-user-portal-settings-in-hello-azure-multi-factor-authentication-server"></a>在 hello Azure Multi-factor Authentication Server 中設定使用者入口網站設定

現在已安裝該 hello 使用者入口網站，您會需要 tooconfigure hello Azure Multi-factor Authentication Server toowork hello 入口網站。

1. 在 hello Azure Multi-factor Authentication Server 主控台的 hello**使用者入口網站**圖示。 Hello 設定 索引標籤中，輸入 hello URL toohello 使用者入口網站中 hello**使用者入口網站 URL**文字方塊。 如果已啟用電子郵件功能，此 URL 隨附於匯入 hello Azure Multi-factor Authentication Server 時，所傳送 toousers hello 電子郵件。
2. 選擇 hello 設定您想 toouse hello 使用者入口網站中的。 例如，如果允許使用者 toochoose 其驗證方法，請確定所**tooselect 方法可讓使用者**勾選，以及他們可以選擇從 hello 方法。
3. 定義誰應該是系統管理員在 hello**管理員** 索引標籤。您可以建立更細微的系統管理權限，使用 hello 新增/編輯方塊中的 hello 核取方塊和下拉式清單。

選用組態：
- **安全性問題**-定義核准的安全性問題，它們會出現在您的環境和 hello 的語言。
- **通過的工作階段** - 使用 MFA，設定使用者入口網站與表單架構網站的整合。
- **可信任 Ip** -允許使用者 tooskip MFA，從清單中的驗證信任的 Ip 或範圍時。

![MFA Server 使用者入口網站組態](./media/multi-factor-authentication-get-started-portal/config.png)

Azure Multi-factor Authentication server 會提供幾個選項用於 hello 使用者入口網站。 hello 下表提供一份這些選項的說明來進行。

| 使用者入口網站設定 | 說明 |
|:--- |:--- |
| 使用者入口網站 URL | 輸入 hello URL 裝載 hello 入口網站位置。 |
| 主要驗證 | 登入 toohello 入口網站時，請指定驗證 toouse hello 類型。 Windows、Radius 或 LDAP 驗證。 |
| 允許在使用者 toolog | Hello 登入頁面上 hello 使用者入口網站允許使用者 tooenter 使用者名稱和密碼。 如果未選取此選項，hello 方塊呈現灰色。 |
| 允許使用者註冊 | 允許在 Multi-factor Authentication 使用者 tooenroll 加以採用 tooa 安裝畫面提示他們輸入其他資訊，例如電話號碼。 提示輸入備用電話，可讓使用者 toospecify 次要的電話號碼。 提示輸入協力廠商 OATH 權杖，允許使用者 toospecify 協力廠商 OATH 權杖。 |
| 允許使用者 tooinitiate 單次許可 | 允許使用者 tooinitiate 單次許可。 如果使用者設定這個選項，它會影響 hello hello 使用者登入的下一次。 提示輸入許可秒 hello 使用者提供的方塊，讓他們可以變更 hello 預設值是 300 秒。 否則，hello 單次許可只會為 300 秒。 |
| 允許使用者 tooselect 方法 | 允許使用者 toospecify 其主要連絡方法。 此方法可以是通話、簡訊、行動裝置應用程式或 OATH 權杖。 |
| 允許使用者 tooselect 語言 | 允許使用者使用 hello 通話、 簡訊、 行動裝置的應用程式或 OATH 權杖的 toochange hello 語言。 |
| 允許使用者 tooactivate 行動裝置應用程式 | 讓使用者 toogenerate 啟用程式碼 toocomplete hello 行動裝置應用程式啟用程序與 hello 伺服器搭配使用。  您也可以設定的裝置啟用的 hello 數目 hello 應用程式上、 介於 1 到 10 之間。 |
| 使用遞補用的安全性問題 | 允許在雙步驟驗證失敗時使用安全性問題。 您可以指定 hello，必須成功回答安全性問題數目。 |
| 允許使用者 tooassociate 協力廠商 OATH 權杖 | 允許使用者 toospecify 協力廠商 OATH 權杖。 |
| 使用遞補用的 OATH 權杖 | 萬一兩步驟驗證不成功，請允許 hello 使用 OATH 權杖。 您也可以指定以分鐘為單位的 hello 工作階段逾時。 |
| 啟用記錄 | 啟用 hello 使用者入口網站的記錄。 hello 記錄檔位於： C:\Program files\multi-factor Authentication Server\Logs。 |

一旦啟用，而且它們也都會簽署 toohello 使用者入口網站中，這些設定會變成可見 toohello hello 入口網站中的使用者。

![使用者入口網站設定](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>自助式使用者註冊

如果您想要使用者 toosign 並註冊，您必須選取 hello**允許在使用者 toolog**和**允許使用者註冊**hello 設定 索引標籤下的選項。請記住，您所選擇的 hello 設定會影響 hello 使用者登入體驗。

例如，當使用者登入時 hello toohello 使用者入口網站第一次，便會進入 toohello Azure Multi-factor Authentication 使用者設定 頁面。 根據您設定的方式 Azure Multi-factor Authentication，hello 使用者可能會無法 tooselect 其驗證方法。

如果它們選取 hello 語音通話驗證方法，或已預先設定的 toouse 該方法，hello 頁面會提示 hello 使用者 tooenter，其主要電話號碼和延伸模組，如果適用的話。 也可能會允許 tooenter 備用電話號碼。

![註冊主要和備份電話號碼](./media/multi-factor-authentication-get-started-portal/backupphone.png)

如果 hello 使用者需要的 toouse PIN 驗證時，hello 頁面會提示他們 toocreate PIN。 輸入電話號碼和 PIN （如果適用） 之後, hello 使用者按一下 hello**現在呼叫我 tooAuthenticate**  按鈕。 Azure Multi-factor Authentication 會執行通話驗證 toohello 使用者的主要電話號碼。 hello 使用者必須回答 hello 電話輸入 PIN （如果適用） 並按 # toomove 上 toohello hello 自我註冊程序的下一個步驟。

如果 hello 使用者選取 hello 簡訊驗證方法，或是已預先設定的 toouse 該方法，hello 頁面會提示他們的行動電話號碼的 hello 使用者。 如果 hello 使用者需要的 toouse PIN 驗證時，hello 頁面也會提示他們 tooenter PIN。  請輸入其電話號碼和 PIN （如果適用） 之後, hello 使用者按一下 hello**文字現在我 tooAuthenticate**  按鈕。 Azure Multi-factor Authentication 會執行 SMS 驗證 toohello 使用者的行動電話。 hello 使用者會收到 hello 文字訊息，其中之一-單次密碼 (OTP)，然後以該 OTP 加上 PIN （如果適用） 回覆 toohello 訊息。

![使用者入口網站簡訊](./media/multi-factor-authentication-get-started-portal/text.png)

如果 hello 使用者選取 hello 行動裝置應用程式的驗證方法，hello 頁面會提示 hello 使用者 tooinstall hello Microsoft 驗證器應用程式在其裝置上的，並產生啟用代碼。 在安裝之後 hello 應用程式，hello 使用者會按一下 hello 產生啟用代碼 按鈕。

> [!NOTE]
> toouse hello Microsoft 驗證器應用程式，hello 使用者必須啟用其裝置的推播通知。

啟用代碼和 URL，以及一個條碼圖片，接著會顯示 hello 頁面。 如果 hello 使用者需要的 toouse PIN 驗證時，hello 頁面此外提示他們輸入 tooenter PIN。 hello 使用者 hello 啟用代碼和 URL 輸入 hello Microsoft 驗證器應用程式或使用 hello 條碼掃描器 tooscan hello 條碼圖，然後按一下 hello [啟用] 按鈕。

Hello 使用者 hello 啟用完成後，請按一下 hello**立即驗證我** 按鈕。 Azure Multi-factor Authentication 會執行驗證 toohello 使用者的行動裝置應用程式。 hello 使用者必須輸入 PIN （如果適用），並在其行動裝置應用程式 toomove 按 hello [驗證] 按鈕上 toohello hello 自我註冊程序的下一個步驟。

如果 hello 系統管理員已設定 hello Azure Multi-factor Authentication Server toocollect 安全性問題和答案，hello 使用者便會進入 toohello 安全性問題 頁面。 hello 使用者必須選取四個安全性問題，並提供 tootheir 選取問題的答案。

![使用者入口網站安全性問題](./media/multi-factor-authentication-get-started-portal/secq.png)

hello 使用者自助式註冊現已完成和 hello 使用者登入 toohello 使用者入口網站。 使用者可登入 toohello 使用者入口網站中上一步中 hello 未來 toochange 隨時其電話號碼、 Pin、 驗證方法和安全性問題系統管理員可以變更它們的方法。

## <a name="next-steps"></a>後續步驟

- [部署 hello Azure Multi-factor Authentication 伺服器行動應用程式 Web 服務](multi-factor-authentication-get-started-server-webservice.md)
