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
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="7a613-103">如何從 Java 在 Azure 部署中的 電子郵件使用 SendGrid tooSend</span><span class="sxs-lookup"><span data-stu-id="7a613-103">How tooSend Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="7a613-104">hello 下列範例示範您如何使用 SendGrid toosend 電子郵件，從 Azure 中裝載的網頁。</span><span class="sxs-lookup"><span data-stu-id="7a613-104">hello following example shows you how you can use SendGrid toosend emails from a web page hosted in Azure.</span></span> <span data-ttu-id="7a613-105">hello 產生應用程式會提示 hello 使用者的電子郵件值 hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="7a613-105">hello resulting application will prompt hello user for email values, as shown in hello following screen shot.</span></span>

![Email form][emailform]

<span data-ttu-id="7a613-107">所產生電子郵件的 hello 看起來類似 toohello 下列螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="7a613-107">hello resulting email will look similar toohello following screen shot.</span></span>

![Email message][emailsent]

<span data-ttu-id="7a613-109">您將需要 toodo hello 下列 toouse 本主題中的 hello 程式碼：</span><span class="sxs-lookup"><span data-stu-id="7a613-109">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="7a613-110">取得 hello javax.mail （每瓶)，例如從<http://www.oracle.com/technetwork/java/javamail/index.html>。</span><span class="sxs-lookup"><span data-stu-id="7a613-110">Obtain hello javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="7a613-111">新增 hello （每瓶) tooyour Java 建置路徑。</span><span class="sxs-lookup"><span data-stu-id="7a613-111">Add hello JARs tooyour Java build path.</span></span>
3. <span data-ttu-id="7a613-112">如果您使用 Eclipse toocreate 此 Java 應用程式，您可以在應用程式部署檔 (WAR) 使用 Eclipse 的部署組件功能包含 hello SendGrid 程式庫。</span><span class="sxs-lookup"><span data-stu-id="7a613-112">If you are using Eclipse toocreate this Java application, you can include hello SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="7a613-113">如果您未使用 Eclipse toocreate 此 Java 應用程式，請確定 hello 程式庫內含 hello 做為您的 Java 應用程式，並將它們加入 toohello 類別路徑，您的應用程式的 Azure 角色相同。</span><span class="sxs-lookup"><span data-stu-id="7a613-113">If you are not using Eclipse toocreate this Java application, ensure hello libraries are included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>

<span data-ttu-id="7a613-114">您也必須擁有您的 SendGrid 使用者名稱和密碼、 toobe 無法 toosend hello 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="7a613-114">You must also have your own SendGrid username and password, toobe able toosend hello email.</span></span> <span data-ttu-id="7a613-115">tooget 入門 SendGrid，請參閱[如何 toosend 電子郵件使用 SendGrid 從 Java](store-sendgrid-java-how-to-send-email.md)。</span><span class="sxs-lookup"><span data-stu-id="7a613-115">tooget started with SendGrid, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="7a613-116">此外，在 hello 資訊的熟悉度[在 Eclipse 中建立 Azure 的 Hello World 應用程式](http://msdn.microsoft.com/library/windowsazure/hh690944)，或與其他技術在裝載 Java 應用程式在 Azure 中的，如果您不想要使用 Eclipse，強烈建議您。</span><span class="sxs-lookup"><span data-stu-id="7a613-116">Additionally, familiarity with hello information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="7a613-117">建立用以傳送電子郵件的 Web 表單</span><span class="sxs-lookup"><span data-stu-id="7a613-117">Create a web form for sending email</span></span>
<span data-ttu-id="7a613-118">下列程式碼的 hello 顯示 toocreate web 表單 tooretrieve 傳送電子郵件的使用者資料的方式。</span><span class="sxs-lookup"><span data-stu-id="7a613-118">hello following code shows how toocreate a web form tooretrieve user data for sending email.</span></span> <span data-ttu-id="7a613-119">基於此內容的詳細資訊，名為 hello JSP 檔案**emailform.jsp**。</span><span class="sxs-lookup"><span data-stu-id="7a613-119">For purposes of this content, hello JSP file is named **emailform.jsp**.</span></span>

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

## <a name="create-hello-code-toosend-hello-email"></a><span data-ttu-id="7a613-120">建立 hello 程式碼 toosend hello 電子郵件</span><span class="sxs-lookup"><span data-stu-id="7a613-120">Create hello code toosend hello email</span></span>
<span data-ttu-id="7a613-121">hello 下列程式碼，當您完成在 emailform.jsp hello 表單呼叫時，建立 hello 電子郵件訊息，並傳送。</span><span class="sxs-lookup"><span data-stu-id="7a613-121">hello following code, which is called when you complete hello form in emailform.jsp, creates hello email message and sends it.</span></span> <span data-ttu-id="7a613-122">基於此內容的詳細資訊，名為 hello JSP 檔案**sendemail.jsp**。</span><span class="sxs-lookup"><span data-stu-id="7a613-122">For purposes of this content, hello JSP file is named **sendemail.jsp**.</span></span>

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

<span data-ttu-id="7a613-123">此外 toosending hello 電子郵件、 emailform.jsp 提供結果 hello 使用者;下列螢幕擷取畫面的 hello 是範例：</span><span class="sxs-lookup"><span data-stu-id="7a613-123">In addition toosending hello email, emailform.jsp provides a result for hello user; an example is hello following screen shot:</span></span>

![Send mail result][emailresult]

## <a name="next-steps"></a><span data-ttu-id="7a613-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a613-125">Next steps</span></span>
<span data-ttu-id="7a613-126">部署您的應用程式 toohello 計算模擬器並在執行 emailform.jsp 瀏覽器中，請在 hello 表單中輸入值，請按一下**傳送這封電子郵件**，然後就會看到 sendemail.jsp 中的結果。</span><span class="sxs-lookup"><span data-stu-id="7a613-126">Deploy your application toohello compute emulator and within a browser run emailform.jsp, enter values in hello form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="7a613-127">此程式碼提供 tooshow 您如何在 Azure 上的 Java SendGrid toouse。</span><span class="sxs-lookup"><span data-stu-id="7a613-127">This code was provided tooshow you how toouse SendGrid in Java on Azure.</span></span> <span data-ttu-id="7a613-128">在部署之前 tooAzure 在生產環境中的，您可能想要 tooadd 詳細的錯誤處理或其他功能。</span><span class="sxs-lookup"><span data-stu-id="7a613-128">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="7a613-129">例如：</span><span class="sxs-lookup"><span data-stu-id="7a613-129">For example:</span></span> 

* <span data-ttu-id="7a613-130">您可以使用 Azure 儲存體 blob 或 SQL Database toostore 電子郵件地址和電子郵件訊息，而不是使用網頁表單。</span><span class="sxs-lookup"><span data-stu-id="7a613-130">You could use Azure storage blobs or SQL Database toostore email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="7a613-131">使用 java 的 Azure 儲存體 blob 的相關資訊，請參閱[tooUse hello 來自 Java 的 Blob 儲存體服務的方式](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/)。</span><span class="sxs-lookup"><span data-stu-id="7a613-131">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="7a613-132">如需在 Java 中使用 SQL Database 的相關資訊，請參閱 [在 Java 中使用 SQL Database](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/)。</span><span class="sxs-lookup"><span data-stu-id="7a613-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="7a613-133">您可以使用`RoleEnvironment.getConfigurationSettings`tooretrieve hello SendGrid 使用者名稱和密碼從您的部署組態設定，而不是使用 hello web 表單 tooretrieve 這些值。</span><span class="sxs-lookup"><span data-stu-id="7a613-133">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username and password from your deployment's configuration settings, instead of using hello web form tooretrieve those values.</span></span> <span data-ttu-id="7a613-134">如需 hello`RoleEnvironment`類別，請參閱[使用 hello Azure 之 JSP 中服務執行階段程式庫](http://msdn.microsoft.com/library/windowsazure/hh690948)和 hello Azure 服務執行階段封裝文件，網址<http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="7a613-134">For information about hello `RoleEnvironment` class, see [Using hello Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and hello Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="7a613-135">如需使用 SendGrid java 的詳細資訊，請參閱[如何 toosend 電子郵件使用 SendGrid 從 Java](store-sendgrid-java-how-to-send-email.md)。</span><span class="sxs-lookup"><span data-stu-id="7a613-135">For more information about using SendGrid in Java, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
