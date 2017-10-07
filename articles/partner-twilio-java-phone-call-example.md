---
title: "aaaHow tooMake 來電 Twilio (Java) |Microsoft 文件"
description: "了解 toomake 電話如何從網頁上，在 Azure 上的 Java 應用程式中使用 Twilio 呼叫。"
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a>如何在 Java 應用程式在 Azure 上的電話使用 Twilio tooMake
hello 下列範例示範您如何使用 Twilio toomake 呼叫，以從 Azure 中裝載的網頁。 hello 產生應用程式會提示 hello 使用者通話值 hello 下列螢幕擷取畫面所示。

![Azure Call Form Using Twilio and Java][twilio_java]

您將需要 toodo hello 下列 toouse 本主題中的 hello 程式碼：

1. 取得 Twilio 帳戶和驗證權杖。 開始使用 Twilio，tooget 評估在定價[http://www.twilio.com/pricing][twilio_pricing]。 您可以在註冊[https://www.twilio.com/try-twilio][try_twilio]。 Hello Twilio 所提供的 API 的相關資訊，請參閱[http://www.twilio.com/api][twilio_api]。
2. 取得 hello Twilio JAR。 在[https://github.com/twilio/twilio-java][twilio_java_github]，您可以下載 hello GitHub 來源並建立您自己的 JAR，或下載預先建立的 JAR （不論有無相依性）。
   使用預先建置 TwilioJava 3.3.8-與-相依性 JAR hello 寫入 hello 本主題中的程式碼。
3. 新增 hello JAR tooyour Java 建置路徑。
4. 如果您使用 Eclipse toocreate 此 Java 應用程式，包括 hello Twilio JAR 應用程式部署檔案中 (WAR) 使用 Eclipse 的部署組件功能。 如果您未使用 Eclipse toocreate 此 Java 應用程式，請確定 hello Twilio JAR 內含 hello 做為您的 Java 應用程式，並將它們加入 toohello 類別路徑，您的應用程式的 Azure 角色相同。
5. 確定您 cacerts 金鑰存放區包含 hello Equifax 安全憑證授權單位憑證的 MD5 指紋 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello 序列值為 35:DE:F4:CF，hello SHA1 指紋為 D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A)。 這是 hello hello 憑證授權單位 (CA) 憑證[https://api.twilio.com] [ twilio_api_service]服務，當您使用 Twilio Api 時呼叫。 新增此 CA 憑證 tooyour JDK cacert 存放區的相關資訊，請參閱[加入 Java CA 憑證存放區的憑證 toohello][add_ca_cert]。

此外，在 hello 資訊的熟悉度[建立 Hello World 應用程式使用 hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world]，或與其他技術在裝載 Java 應用程式在 Azure 如果您不使用 Eclipse，強烈建議。

## <a name="create-a-web-form-for-making-a-call"></a>建立用以撥打電話的 Web 表單
下列程式碼的 hello 顯示 toocreate web 表單 tooretrieve 進行呼叫的使用者資料的方式。 在此範例中，我們新建立了名為 **TwilioCloud** 的動態 Web 專案，並將 **callform.jsp** 新增為 JSP 檔案。

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toomake-hello-call"></a>建立 hello 程式碼 toomake hello 呼叫
hello 下列程式碼會呼叫 hello 使用者完成 hello callform.jsp 所顯示的表單時，會建立 hello 呼叫訊息並產生 hello 呼叫。 基於此範例中，名為 hello JSP 檔案**makecall.jsp** ，並且加入 toohello **TwilioCloud**專案。 (使用您的 Twilio 帳戶和驗證語彙基元而非 hello 預留位置值太指派**accountSID**和**authToken** hello 的下列程式碼。)

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

此外 toomaking hello 呼叫、 makecall.jsp 顯示 hello Twilio 端點、 應用程式開發介面版本，以及 hello 呼叫狀態。 下列螢幕擷取畫面的 hello 是範例：

![Azure Call Response Using Twilio and Java][twilio_java_response]

## <a name="run-hello-application"></a>執行 hello 應用程式
下列是 hello 高階步驟 toorun 您的應用程式。詳細說明這些步驟可以找到在[建立 Hello World 應用程式使用 hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world]。

1. 匯出您 TwilioCloud WAR toohello Azure **approot**資料夾。 
2. 修改**startup.cmd** toounzip TwilioCloud WAR。
3. 編譯您的應用程式的 hello 計算模擬器。
4. Hello 計算模擬器中啟動您的部署。
5. 開啟瀏覽器，然後執行 **http://localhost:8080/TwilioCloud/callform.jsp**。
6. 在 hello 表單中輸入值，請按一下**進行這個呼叫**，然後查看 makecall.jsp hello 結果。

當您準備好 toodeploy tooAzure，部署 toohello 雲端重新編譯、 部署 tooAzure，以及執行 http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp hello 瀏覽器中的 (您值取代為*your_hosted_name*)。

## <a name="next-steps"></a>後續步驟
此程式碼提供 tooshow 您基本的功能在 Azure 上使用 Twilio 在 Java 中的。 在部署之前 tooAzure 在生產環境中的，您可能想要 tooadd 詳細的錯誤處理或其他功能。 例如：

* 而不是使用網頁表單，也可以使用 Azure 儲存體 blob 或 SQL Database toostore 電話號碼，並呼叫的文字。 使用 java 的 Azure 儲存體 blob 的相關資訊，請參閱[tooUse hello 來自 Java 的 Blob 儲存體服務的方式][howto_blob_storage_java]。 使用 java 的 SQL 資料庫的相關資訊，請參閱[在 Java 中使用 SQL Database][howto_sql_azure_java]。
* 您可以使用**RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio 帳戶識別碼和驗證語彙基元從您的部署組態設定，而不是硬式編碼 makecall.jsp 中的 hello 值。 如需 hello **RoleEnvironment**類別，請參閱[使用 hello Azure 之 JSP 中服務執行階段程式庫][ azure_runtime_jsp]和 hello Azure 服務執行階段封裝文件，網址[http://dl.windowsazure.com/javadoc][azure_javadoc]。
* hello makecall.jsp 程式碼會將 Twilio 提供的 URL，指派[http://twimlets.com/message][twimlet_message_url]，toohello **Url**變數。 此 URL 提供通知以 hello tooproceed 如何呼叫的 Twilio Twilio 標記語言 (TwiML) 回應。 例如，可以包含 hello TwiML 傳回**&lt;說&gt;**正在口語的 toohello 呼叫收件者的文字會產生的指令動詞。 而不是使用 hello Twilio 提供 URL，您可以建置自己服務 toorespond tooTwilio 要求。如需詳細資訊，請參閱[如何 tooUse 語音和簡訊功能，在 Java 中 Twilio][howto_twilio_voice_sms_java]。 可以找到 TwiML 的詳細資訊，在[http://www.twilio.com/docs/api/twiml][twiml]，和其他相關資訊**&lt;說&gt;**和其他 Twilio 動詞命令，請參閱[http://www.twilio.com/docs/api/twiml/say][twilio_say]。
* 讀取 hello Twilio 安全性指導方針，在[https://www.twilio.com/docs/security][twilio_docs_security]。

如需 Twilio 的其他資訊，請參閱 [https://www.twilio.com/docs][twilio_docs]。

## <a name="see-also"></a>另請參閱
* [如何 tooUse Twilio 語音和簡訊功能，在 Java 中][howto_twilio_voice_sms_java]
* [新增憑證 toohello Java CA 憑證存放區][add_ca_cert]

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
