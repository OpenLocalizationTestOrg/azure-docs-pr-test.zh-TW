---
title: "aaaHow tooUse Twilio 語音和 SMS (Java) |Microsoft 文件"
description: "了解如何 toomake 電話及傳送 SMS 訊息 hello Twilio API 服務在 Azure 上。 程式碼範例以 Java 撰寫。"
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a>如何 tooUse Twilio 語音和簡訊功能，在 Java 中
本指南示範如何 tooperform 常見的程式設計工作以 hello Twilio API 服務在 Azure 上。 涵蓋的 hello 案例包括撥電話及傳送短訊息服務 (SMS) 訊息。 如需有關 Twilio 和您的應用程式中使用語音和 SMS 的詳細資訊，請參閱 hello[接下來的步驟](#NextSteps)> 一節。

## <a id="WhatIs"></a>什麼是 Twilio？
Twilio 是電話語音 web 服務 API，可讓您使用現有的 web 語言和技術 toobuild 語音和 SMS 應用程式。 Twilio 算是協力廠商服務 (並非 Azure 功能，也並非 Microsoft 產品)。

**Twilio 語音**可讓您的應用程式 toomake 撥打與接聽電話。 **Twilio SMS**可讓您的應用程式 toomake 和接收 SMS 訊息。 **Twilio 用戶端**tooenable 語音通訊使用現有的網際網路連線，包括行動裝置的連線，可讓您的應用程式。

## <a id="Pricing"></a>Twilio 定價和特別優惠
[Twilio 定價][twilio_pricing] (英文) 提供 Twilio 的定價資訊。 Azure 客戶可獲得[特殊優惠][special_offer]：免費 1000 則文字簡訊或接聽 1000 分鐘電話。 註冊這 toosign 提供或取得詳細資訊，請瀏覽[http://ahoy.twilio.com/azure][special_offer]。

## <a id="Concepts"></a>概念
hello Twilio API 是 rest 式 API，應用程式提供語音和 SMS 功能。 用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。

Hello Twilio API 的重要層面是 Twilio 動詞和 Twilio 標記語言 (TwiML)。

### <a id="Verbs"></a>Twilio 動詞
hello API 會使用 Twilio 動詞命令。例如，hello **&lt;說&gt;**動詞命令會指示 Twilio tooaudibly 傳遞的訊息上呼叫。

hello 如下的 Twilio 指令動詞的清單。

* **&lt;撥號&gt;**： 連接 hello 呼叫端 tooanother 電話。
* **&lt;收集&gt;**： 會收集輸入 hello 電話字鍵台上的數字。
* **&lt;掛斷&gt;**：結束通話。
* **&lt;播放&gt;**：播放音訊檔案。
* **&lt;佇列&gt;**： 新增 hello tooa 佇列的呼叫端。
* **&lt;暫停&gt;**：靜候一段指定的秒數。
* **&lt;記錄&gt;**： 記錄 hello 呼叫者的語音，並傳回包含 hello 記錄檔的 URL。
* **&lt;重新導向&gt;**： 控制權的通話或 SMS toohello TwiML 於不同的 URL。
* **&lt;拒絕&gt;**： 拒絕傳入的呼叫未使用計費您 tooyour Twilio 數目。
* **&lt;說出&gt;**： 將文字 toospeech 所做的呼叫上。
* **&lt;Sms&gt;**：傳送簡訊。

### <a id="TwiML"></a>TwiML
TwiML 是以 XML 為基礎的指示，就會通知方式的 Twilio hello Twilio 動詞命令為基礎的一組 tooprocess 通話或 SMS。

例如，下列 TwiML hello 將轉換的 hello 文字**Hello World ！** toospeech。

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

當您的應用程式呼叫 hello Twilio 應用程式開發介面時，其中 hello API 參數會是傳回 hello TwiML 回應 hello URL。 供開發應用程式，您可以使用您的應用程式所使用的 Twilio 提供 Url tooprovide hello TwiML 回應。 您也可以裝載自己 Url tooproduce hello TwiML 回應，和另一個選項是 toouse hello **TwiMLResponse**物件。

如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。 如需 hello Twilio API 的詳細資訊，請參閱[Twilio API][twilio_api]。

## <a id="CreateAccount"></a>建立 Twilio 帳戶
當你準備好 tooget Twilio 帳戶時，請在註冊[再試一次 Twilio][try_twilio]。 您可以先使用免費帳戶，稍後再升級帳戶。

註冊 Twilio 帳戶時，您會收到帳戶識別碼和驗證權杖。 同時會為所需的 toomake Twilio API 呼叫。 tooprevent 未經授權存取 tooyour 帳戶，讓驗證權杖的安全。 您的帳戶識別碼和驗證權杖皆可檢視在 hello [Twilio 主控台][twilio_console]，請在 hello 欄位標示為**帳戶 SID**和**驗證語彙基元**分別。

## <a id="create_app"></a>建立 Java 應用程式
1. 取得 hello Twilio JAR，並將它加入的 tooyour Java 建置路徑與 WAR 部署組件。 在[https://github.com/twilio/twilio-java][twilio_java]，您可以下載 hello GitHub 來源並建立您自己的 JAR，或下載預先建立的 JAR （不論有無相依性）。
2. 請確定您的 JDK **cacerts**金鑰存放區包含 hello Equifax 安全憑證授權單位憑證的 MD5 指紋 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 （hello 序號為 35:DE:F4:CF 和 hello SHA1指紋是 D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A)。 這是 hello hello 憑證授權單位 (CA) 憑證[https://api.twilio.com] [ twilio_api_service]服務，當您使用 Twilio Api 時呼叫。 如需確保您的 JDK **cacerts**金鑰存放區包含 hello 正確的 CA 憑證，請參閱[新增憑證 toohello Java CA 憑證存放區][add_ca_cert]。

使用 Java hello Twilio 用戶端程式庫的詳細的指示位於[如何 tooMake 在 Java 應用程式在 Azure 上的電話使用 Twilio][howto_phonecall_java]。

## <a id="configure_app"></a>設定您的應用程式 tooUse Twilio 文件庫
在您的程式碼中，您可以加入**匯入**在 hello hello Twilio 封裝，或您類別的原始程式檔最上方的陳述式要 toouse 應用程式中的。

對於 Java 原始程式檔：

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

對於 Java 伺服器頁面 (JSP) 原始程式檔：

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
根據哪些 Twilio 封裝或類別中，您想 toouse，您**匯入**陳述式可能會不同。

## <a id="howto_make_call"></a>作法：撥出電話
hello 下列範例示範如何 toomake 傳出呼叫使用 hello**呼叫**類別。 此程式碼也會使用 Twilio 提供站台 tooreturn hello Twilio 標記語言 (TwiML) 回應。 替換為您的值為 hello**從**和**至**電話號碼，並確保您確認 hello**從**電話號碼您 Twilio 帳戶先前 toorunning hello 撰寫程式碼。

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

如需有關 hello 參數傳入 toohello **Call.creator**方法，請參閱[http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls]。

如前所述，此程式碼會使用 Twilio 提供站台 tooreturn hello TwiML 回應。 您可以改為使用您自己的站台 tooprovide hello TwiML 回應。如需詳細資訊，請參閱[如何在 Java 應用程式在 Azure 上 TwiML 回應 tooProvide](#howto_provide_twiml_responses)。

## <a id="howto_send_sms"></a>作法：傳送簡訊
hello 下列範例示範如何 toosend SMS 訊息使用 hello**訊息**類別。 hello**從**號**4155992671**，為試用版帳戶 toosend SMS 訊息由 Twilio 中提供。 hello**至**數目必須驗證您 Twilio 帳戶先前 toorunning hello 撰寫程式碼。

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

如需有關 hello 參數傳入 toohello **Message.creator**方法，請參閱[http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms]。

## <a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應
當您的應用程式會起始呼叫 toohello Twilio 應用程式開發介面，例如透過 hello **CallCreator.create**方法，Twilio 會傳送要求 tooa URL 所預期的 tooreturn TwiML 回應。 上述的 hello 範例會使用 hello Twilio 提供 URL [http://twimlets.com/message][twimlet_message_url]。 （雖然 TwiML 設計為使用 Web 服務，您可以檢視 hello TwiML 瀏覽器中。 例如，按一下[http://twimlets.com/message] [ twimlet_message_url] toosee 空**&lt;回應&gt;**項目，做為另一個範例中，按一下 [ [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee **&lt;回應&gt;**包含項目**&lt;說&gt;** 項目。)

而不是依賴 hello Twilio 提供 URL，您可以建立您自己會傳回 HTTP 回應的 URL 站台。 您可以建立 hello 網站中的任何語言，會傳回 HTTP 回應。本主題假設您要主控 JSP 頁面中的 hello URL。

hello 遵循 JSP 頁面結果以指出 TwiML 回應**Hello World ！** 在 hello 呼叫。

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

遵循 JSP 頁面結果，以顯示一些文字，TwiML 回應 hello 具有數個暫停，而且隻字 hello Twilio API 版本與 hello Azure 角色名稱的資訊。

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

hello **Microsoft.authorization**參數可用於 Twilio 提出要求 （不是 SMS 要求）。 toosee hello 可用的要求參數 Twilio 語音和 SMS 要求，請參閱<https://www.twilio.com/docs/api/twiml/twilio_request>和<https://www.twilio.com/docs/api/twiml/sms/twilio_request>分別。 hello **RoleName**環境變數可做為 Azure 部署的一部分。 (如果您想 tooadd 自訂的環境變數，它們無法從挑選**System.getenv**，請參閱 hello 環境變數[其他角色的組態設定][misc_role_config_settings].)

一旦您的 JSP 頁面設定 tooprovide TwiML 回應，做為 hello hello JSP 網頁 URL hello URL 傳入 hello **Call.creator**方法。 比方說，如果您的 Web 應用程式名為 MyTwiML 部署 tooan Azure 託管服務，和 hello 頁面名稱的 hello JSP mytwiml.jsp，可以傳遞 hello URL 太**Call.creator** hello 下列所示：

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

以 TwiML 回應的另一個選項是透過 hello **VoiceResponse**類別，其可於 hello **com.twilio.twiml**封裝。

如需有關在 Azure 的 Java 中使用 Twilio 的詳細資訊，請參閱[如何 tooMake 在 Java 應用程式在 Azure 上的電話使用 Twilio][howto_phonecall_java]。

## <a id="AdditionalServices"></a>如何：使用其他 Twilio 服務
此外 toohello 範例所示，Twilio 提供網頁型應用程式開發介面，您可以使用其他 Twilio 功能 tooleverage 從 Azure 應用程式。 完整的詳細資訊，請參閱 hello [Twilio API 文件][twilio_api_documentation]。

## <a id="NextSteps"></a>後續步驟
既然您已經學會 hello hello Twilio 服務基本概念，請依照下列多個這些連結 toolearn:

* [Twilio 安全性方針][twilio_security_guidelines]
* [Twilio 作法與範例程式碼][twilio_howtos]
* [Twilio 快速入門教學課程][twilio_quickstarts]
* [GitHub 上的 Twilio][twilio_on_github]
* [Talk tooTwilio 支援][twilio_support]

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
