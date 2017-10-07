---
title: aaastore-sendgrid-java-how-to-send-email-example
description: "如何在 Azure 部署中使用 SendGrid 從 Java toosend 電子郵件"
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: af096a73-6985-4350-92e4-ce1722c8d72f
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: vibhork;dominic.may@sendgrid.com;elmer.thomas@sendgrid.com
ms.openlocfilehash: 51fde1fc71467f8252532b30d2f87856ec25067b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a>如何從 Java 在 Azure 部署中的 電子郵件使用 SendGrid tooSend
hello 下列範例示範您如何使用 SendGrid toosend 電子郵件，從 Azure 中裝載的網頁。 hello 產生應用程式會提示 hello 使用者的電子郵件值 hello 下列螢幕擷取畫面所示。

![Email form][emailform]

所產生電子郵件的 hello 看起來類似 toohello 下列螢幕擷取畫面。

![Email message][emailsent]

您將需要 toodo hello 下列 toouse 本主題中的 hello 程式碼：

1. 取得 hello javax.mail （每瓶)，例如從<http://www.oracle.com/technetwork/java/javamail/index.html>。
2. 新增 hello （每瓶) tooyour Java 建置路徑。
3. 如果您使用 Eclipse toocreate 此 Java 應用程式，您可以在應用程式部署檔 (WAR) 使用 Eclipse 的部署組件功能包含 hello SendGrid 程式庫。 如果您未使用 Eclipse toocreate 此 Java 應用程式，請確定 hello 程式庫內含 hello 做為您的 Java 應用程式，並將它們加入 toohello 類別路徑，您的應用程式的 Azure 角色相同。

您也必須擁有您的 SendGrid 使用者名稱和密碼、 toobe 無法 toosend hello 電子郵件。 tooget 入門 SendGrid，請參閱[如何 toosend 電子郵件使用 SendGrid 從 Java](store-sendgrid-java-how-to-send-email.md)。

此外，在 hello 資訊的熟悉度[在 Eclipse 中建立 Azure 的 Hello World 應用程式](http://msdn.microsoft.com/library/windowsazure/hh690944)，或與其他技術在裝載 Java 應用程式在 Azure 中的，如果您不想要使用 Eclipse，強烈建議您。

## <a name="create-a-web-form-for-sending-email"></a>建立用以傳送電子郵件的 Web 表單
下列程式碼的 hello 顯示 toocreate web 表單 tooretrieve 傳送電子郵件的使用者資料的方式。 基於此內容的詳細資訊，名為 hello JSP 檔案**emailform.jsp**。

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Send this email</b>.</p>
     <br/>
      <form action="sendemail.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="emailTo">
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="emailFrom">
           </td>
         </tr>
         <tr>
           <td>Subject:</td>
           <td><input type="text" size=100 name="emailSubject" value="My email subject">
           </td>
         </tr>
         <tr>
           <td>Text:</td>
           <td><input type="text" size=400 name="emailText" value="Hello,<p>This is my message.</p>Thank you." />
           </td>
         </tr>
         <tr>
           <td>SendGrid user name:</td>
           <td><input type="text" name="sendGridUser">
           </td>
         </tr>
         <tr>
           <td>SendGrid password:</td>
           <td><input type="password" name="sendGridPassword">
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Send this email">
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toosend-hello-email"></a>建立 hello 程式碼 toosend hello 電子郵件
hello 下列程式碼，當您完成在 emailform.jsp hello 表單呼叫時，建立 hello 電子郵件訊息，並傳送。 基於此內容的詳細資訊，名為 hello JSP 檔案**sendemail.jsp**。

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" import="javax.activation.*, javax.mail.*, javax.mail.internet.*, java.util.Date, java.util.Properties" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email processing happens here</title>
    </head>
    <body>
        <b>This is my send mail page.</b><p/>
     <%

     final String sendGridUser = request.getParameter("sendGridUser");
     final String sendGridPassword = request.getParameter("sendGridPassword");

     class SMTPAuthenticator extends Authenticator
     {
       public PasswordAuthentication getPasswordAuthentication()
       {
            String username = sendGridUser;
            String password = sendGridPassword;

            return new PasswordAuthentication(username, password);   
       }
     }
     try
     {

         // hello SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display hello email fields entered by hello user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create hello authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create hello mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information toostdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create hello message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify hello email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment hello following if you want tooadd a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment hello following if you want tooenable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect hello transport object.
         transport.connect();
         // Send hello message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close hello connection.
         transport.close();

        out.println("<p>Email processing completed.</p>");

     }
     catch (Exception e)
     {
         out.println("<p>Exception encountered: " + 
                            e.getMessage()     +
                            "</p>");   
     }
    %>

    </body>
    </html>

此外 toosending hello 電子郵件、 emailform.jsp 提供結果 hello 使用者;下列螢幕擷取畫面的 hello 是範例：

![Send mail result][emailresult]

## <a name="next-steps"></a>後續步驟
部署您的應用程式 toohello 計算模擬器並在執行 emailform.jsp 瀏覽器中，請在 hello 表單中輸入值，請按一下**傳送這封電子郵件**，然後就會看到 sendemail.jsp 中的結果。

此程式碼提供 tooshow 您如何在 Azure 上的 Java SendGrid toouse。 在部署之前 tooAzure 在生產環境中的，您可能想要 tooadd 詳細的錯誤處理或其他功能。 例如： 

* 您可以使用 Azure 儲存體 blob 或 SQL Database toostore 電子郵件地址和電子郵件訊息，而不是使用網頁表單。 使用 java 的 Azure 儲存體 blob 的相關資訊，請參閱[tooUse hello 來自 Java 的 Blob 儲存體服務的方式](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/)。 如需在 Java 中使用 SQL Database 的相關資訊，請參閱 [在 Java 中使用 SQL Database](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/)。
* 您可以使用`RoleEnvironment.getConfigurationSettings`tooretrieve hello SendGrid 使用者名稱和密碼從您的部署組態設定，而不是使用 hello web 表單 tooretrieve 這些值。 如需 hello`RoleEnvironment`類別，請參閱[使用 hello Azure 之 JSP 中服務執行階段程式庫](http://msdn.microsoft.com/library/windowsazure/hh690948)和 hello Azure 服務執行階段封裝文件，網址<http://dl.windowsazure.com/javadoc>.
* 如需使用 SendGrid java 的詳細資訊，請參閱[如何 toosend 電子郵件使用 SendGrid 從 Java](store-sendgrid-java-how-to-send-email.md)。

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
