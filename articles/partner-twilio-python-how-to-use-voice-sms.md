---
title: "aaaHow tooUse Twilio 語音和 SMS (Python) |Microsoft 文件"
description: "了解如何 toomake 電話及傳送 SMS 訊息 hello Twilio API 服務在 Azure 上。 程式碼範例以 Python 撰寫。"
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a>如何為語音和簡訊功能以 Python Twilio tooUse
本指南示範如何 tooperform 常見的程式設計工作以 hello Twilio API 服務在 Azure 上。 涵蓋的 hello 案例包括撥電話及傳送短訊息服務 (SMS) 訊息。 如需有關 Twilio 和您的應用程式中使用語音和 SMS 的詳細資訊，請參閱 hello[接下來的步驟](#NextSteps)> 一節。

## <a id="WhatIs"></a>什麼是 Twilio？
Twilio 是及支援的業務通訊的 hello 未來、 啟用開發人員 tooembed 語音 VoIP 及訊息加入應用程式。 這些虛擬化在雲端為基礎、 全域環境中，公開透過 hello Twilio 通訊 API 平台所需的所有基礎結構。 應用程式是簡單 toobuild 及擴充。 享受隨收隨付定價的彈性和雲端可靠性的好處。

**Twilio 語音**可讓您的應用程式 toomake 撥打與接聽電話。
**Twilio SMS**可讓您的應用程式 toosend 及接收文字訊息。
**Twilio 用戶端**可讓您從任何電話、 平板電腦或瀏覽器 toomake VoIP 呼叫，並支援 WebRTC。

## <a id="Pricing"></a>Twilio 定價和特別優惠
Azure 客戶可在升級 Twilio 帳戶時獲得價值 10 元美金的 Twilio 點數[特殊優惠][special_offer]。 此 Twilio 信用額度可以套用的 tooany Twilio 使用量 ($10 信用相等 toosending 多達 1000 SMS 訊息或接收向上 too1000 輸入語音分鐘，視您的電話號碼和訊息或呼叫目的地的 hello 位置而定)。 請兌換此 [Twilio 點數][special_offer]，並開始使用。

Twilio 是隨收隨付的服務。 不需要設定費，隨時都可結清帳戶。 如需詳細資訊，請參閱 [Twilio 價格][twilio_pricing]。

## <a id="Concepts"></a>概念
hello Twilio API 是 rest 式 API，應用程式提供語音和 SMS 功能。 用戶端程式庫有多種語言版本，相關清單請參閱 [Twilio API 程式庫][twilio_libraries]。

Hello Twilio API 的重要層面是 Twilio 動詞和 Twilio 標記語言 (TwiML)。

### <a id="Verbs"></a>Twilio 動詞
hello API 會使用 Twilio 動詞命令。例如，hello **&lt;說&gt;**動詞命令會指示 Twilio tooaudibly 傳遞的訊息上呼叫。

hello 如下的 Twilio 指令動詞的清單。 深入了解 hello 其他動詞命令和功能，透過[Twilio 標記語言的文件][twiml]。

* **&lt;撥號&gt;**： 連接 hello 呼叫端 tooanother 電話。
* **&lt;收集&gt;**： 會收集輸入 hello 電話字鍵台上的數字。
* **&lt;掛斷&gt;**：結束通話。
* **&lt;暫停&gt;**：靜候一段指定的秒數。
* **&lt;播放&gt;**：播放音訊檔案。
* **&lt;佇列&gt;**： 新增 hello tooa 佇列的呼叫端。
* **&lt;記錄&gt;**： 記錄 hello 呼叫端的 hello 語音，並傳回包含 hello 記錄檔的 URL。
* **&lt;重新導向&gt;**： 控制權的通話或 SMS toohello TwiML 於不同的 URL。
* **&lt;拒絕&gt;**： 拒絕傳入的呼叫未使用計費您 tooyour Twilio 數目。
* **&lt;說出&gt;**： 將文字 toospeech 所做的呼叫上。
* **&lt;Sms&gt;**：傳送簡訊。

### <a id="TwiML"></a>TwiML
TwiML 是以 XML 為基礎的指示，就會通知方式的 Twilio hello Twilio 動詞命令為基礎的一組 tooprocess 通話或 SMS。

例如，下列 TwiML hello 將轉換的 hello 文字**Hello World** toospeech。

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

當您的應用程式呼叫 hello Twilio 應用程式開發介面時，其中 hello API 參數會是傳回 hello TwiML 回應 hello URL。 供開發應用程式，您可以使用您的應用程式所使用的 Twilio 提供 Url tooprovide hello TwiML 回應。 您也可以裝載自己 Url tooproduce hello TwiML 回應，和另一個選項是 toouse hello`TwiMLResponse`物件。

如需 Twilio 動詞、屬性和 TwiML 的詳細資訊，請參閱 [TwiML][twiml]。 如需 hello Twilio API 的詳細資訊，請參閱[Twilio API][twilio_api]。

## <a id="CreateAccount"></a>建立 Twilio 帳戶
當您準備好 tooget Twilio 帳戶，請在註冊[再試一次 Twilio][try_twilio]。 您可以先使用免費帳戶，稍後再升級帳戶。

註冊 Twilio 帳戶時，您會收到帳戶 SID 和驗證權杖。 同時會為所需的 toomake Twilio API 呼叫。 tooprevent 未經授權存取 tooyour 帳戶，讓驗證權杖的安全。 您的帳戶 SID 與驗證權杖是否可在 hello [Twilio 主控台][twilio_console]，請在 hello 欄位標示為**帳戶 SID**和**驗證語彙基元**分別。

## <a id="create_app"></a>建立 Python 應用程式
Python 應用程式使用 hello Twilio 服務，且在 Azure 中執行並無不同 hello Twilio 服務會使用任何其他 Python 應用程式。 雖然 Twilio 服務是以 REST 為基礎，並可以數種方式呼叫來自 Python，本文將著重在 toouse Twilio 的服務使用[Twilio 程式庫，從 GitHub python][twilio_python]。 如需使用 Python hello Twilio 程式庫的詳細資訊，請參閱[http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs]。

首先，[安裝新的 Azure Linux VM] [azure_vm_setup] tooact 做為新的 Python web 應用程式的主機。 Hello 虛擬機器開始執行之後，您需要 tooexpose 公用連接埠上的應用程式，如下所述。

### <a name="add-an-incoming-rule"></a>新增傳入規則
  1. 移 toohello [網路安全性群組] [azure_nsg] 頁面。
  2. 選取 hello 網路安全性群組對應與虛擬機器。
  3. 新增**連接埠 80** 的**傳出規則**。 為確定 tooallow 連入來自任何位址。

### <a name="set-hello-dns-name-label"></a>設定 hello DNS 名稱標籤
  1. 移 toohello [hello 公用 IP 地址] [azure_ips] 頁面。
  2. 選取具有您的虛擬機器的公用 IP 該 correspends hello。
  3. 設定 hello **DNS 名稱標籤**在 hello**組態**> 一節。 在此範例中的 hello 情況下它看起來類似下面的*您網域標籤*。 centralus.cloudapp.azure.com

之後，就可以透過 SSH toohello 虛擬機器，您可以安裝 tooconnect hello 您選擇的 Web 架構 (hello 兩個最知名的 Python[酒瓶](http://flask.pocoo.org/)和[Django](https://www.djangoproject.com))。 您可以只要執行 hello 安裝其中任一`pip install`命令。

請注意，我們只在連接埠 80 上設定 hello 虛擬機器 tooallow 流量。 因此請確定 tooconfigure hello 應用程式 toouse 此連接埠。

## <a id="configure_app"></a>設定您的應用程式 tooUse Twilio 文件庫
您可以設定您應用程式 toouse hello Twilio 程式庫的 Python，有兩種：

* 安裝 Python Pip 套件 hello Twilio 程式庫。 它可以安裝以 hello 下列命令：
   
        $ pip install twilio

    -或-

* 從 GitHub 的 python 下載 hello Twilio 程式庫 ([https://github.com/twilio/twilio-python][twilio_python]) 並將它安裝像這樣：

        $ python setup.py install

一旦您的 Python 安裝 hello Twilio 程式庫，您可以再`import`Python 檔案中：

        import twilio

如需詳細資訊，請參閱 [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme]。

## <a id="howto_make_call"></a>作法：撥出電話
下列的 hello 會示範如何呼叫 toomake 傳出。 此程式碼也會使用 Twilio 提供站台 tooreturn hello Twilio 標記語言 (TwiML) 回應。 替換為您的值為 hello **from_number**和**to_number**電話號碼，並確定您已驗證過 hello **from_number**電話號碼為您的 Twilio 帳戶之前執行的 hello 程式碼。

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

如前所述，此程式碼會使用 Twilio 提供站台 tooreturn hello TwiML 回應。 您可以改為使用您自己的站台 tooprovide hello TwiML 回應。如需詳細資訊，請參閱[如何 tooProvide TwiML 回應從您自己網站](#howto_provide_twiml_responses)。

## <a id="howto_send_sms"></a>作法：傳送簡訊
hello 下列範例示範如何 toosend SMS 訊息使用 hello`TwilioRestClient`類別。 hello **from_number**數目由 Twilio 為試用版帳戶 toosend SMS 訊息。 hello **to_number**數目必須在您的 Twilio 帳戶之前驗證執行 hello 程式碼。

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <a id="howto_provide_twiml_responses"></a>作法：從您自己的網站提供 TwiML 回應
當您的應用程式啟動呼叫 toohello Twilio 應用程式開發介面時，會傳送 Twilio，是您要求 tooa URL 必須是 tooreturn TwiML 回應。 上述的 hello 範例會使用 hello Twilio 提供 URL [http://twimlets.com/message][twimlet_message_url]。 (雖然 TwiML 是設計給 Twilio 使用的，但您也可以在瀏覽器中檢視 TwiML。 例如，按一下[http://twimlets.com/message] [ twimlet_message_url] toosee 空`<Response>`項目，另一個範例中，按一下 [ [http://twimlets.com/message?訊息 %5B0 %5 D = Hello %20world] [ twimlet_message_url_hello_world] toosee`<Response>`包含項目`<Say>`項目。)

而不是依賴 hello Twilio 提供 URL，您可以建立您自己會傳回 HTTP 回應的網站。 您可以建立 hello 網站中的任何語言，傳回 XML 回應。本主題假設您將使用 Python toocreate hello TwiML。

hello 下列範例會輸出 TwiML 回應指出**Hello World** hello 呼叫。

使用 Flask：

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

使用 Django：

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

您可以看到從 hello 上述範例中，hello TwiML 回應是只是 XML 文件。 hello Python 的 Twilio 文件庫包含類別，會為您產生 TwiML。 hello 下面範例會產生 hello 相等回應，如上所示，但使用 hello `twiml` hello Python 的 Twilio 文件庫中的模組：

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

如需 TwiML 的詳細資訊，請參閱 [https://www.twilio.com/docs/api/twiml][twiml_reference]。

一旦您設定 tooprovide TwiML 回應的 Python 應用程式，做為 hello hello 應用程式 URL hello URL 傳入 hello`client.calls.create`方法。 例如，如果您有 Web 應用程式名為**MyTwiML**部署的 tooan Azure 託管服務，您可以使用它的 url 為 webhook，hello 下列範例所示：

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <a id="AdditionalServices"></a>如何：使用其他 Twilio 服務
此外 toohello 範例所示，Twilio 提供網頁型應用程式開發介面，您可以使用其他 Twilio 功能 tooleverage 從 Azure 應用程式。 完整的詳細資訊，請參閱 hello [Twilio API 文件][twilio_api]。

## <a id="NextSteps"></a>後續步驟
既然您已經學會 hello hello Twilio 服務基本概念，請依照下列多個這些連結 toolearn:

* [Twilio 安全性方針][twilio_security_guidelines]
* [Twilio 作法指南與範例程式碼][twilio_howtos]
* [Twilio 快速入門教學課程][twilio_quickstarts]
* [GitHub 上的 Twilio][twilio_on_github]
* [Talk tooTwilio 支援][twilio_support]

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
