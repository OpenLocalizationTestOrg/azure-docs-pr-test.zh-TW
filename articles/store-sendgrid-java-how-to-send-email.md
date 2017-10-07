---
title: "aaaHow toouse hello SendGrid 電子郵件服務 (Java) |Microsoft 文件"
description: "深入了解如何在 Azure 上傳送電子郵件以 hello SendGrid 電子郵件服務。 程式碼範例以 Java 撰寫。"
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: cc75c43e-ede9-492b-98c2-9147fcb92c21
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork
ms.openlocfilehash: 542ce0003e94fc8f5551487d5a3cd6f75d27e8cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java"></a>如何 tooSend 電子郵件從 Java 使用 SendGrid
本指南示範如何 tooperform 常見的程式設計工作使用 SendGrid 傳送電子郵件在 Azure 上的服務。 hello 範例是以 Java 撰寫。 hello 涵蓋案例包括**建構電子郵件**，**傳送電子郵件**，**加入附件**，**使用篩選器**，和**更新屬性**。 如需有關 SendGrid 和傳送電子郵件的詳細資訊，請參閱 hello[後續步驟](#next-steps)> 一節。

## <a name="what-is-hello-sendgrid-email-service"></a>什麼是 hello SendGrid 電子郵件服務？
SendGrid 是 [雲端架構電子郵件服務]，能提供可靠的 [交易式電子郵件傳遞]、擴充性和即時分析，以及有彈性的 API 來輕鬆進行自訂整合。 常見的 SendGrid 使用案例包括：

* 自動將資料傳送回條 toocustomers
* 管理通訊群組清單，以便將每月電子傳單和特別優惠傳送給客戶
* 收集封鎖的電子郵件、客戶的回應情形等項目的即時度量
* 產生 toohelp 識別趨勢的報表
* 轉寄客戶查詢
* 透過電子郵件從您的應用程式傳送通知

如需詳細資訊，請參閱 <http://sendgrid.com>。

## <a name="create-a-sendgrid-account"></a>建立 SendGrid 帳戶
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a>如何： 使用 hello javax.mail 程式庫
取得 hello javax.mail 程式庫，例如從<http://www.oracle.com/technetwork/java/javamail> ，匯入您的程式碼。 高階 hello 程序使用 hello javax.mail 文件庫 toosend 電子郵件使用 SMTP 是 toodo hello 下列：

1. 指定 hello SMTP 值，包括即 sendgrid smtp.sendgrid.net hello SMTP 伺服器。

```
        import java.util.Properties;
        import javax.activation.*;
        import javax.mail.*;
        import javax.mail.internet.*;

        public class MyEmailer {
           private static final String SMTP_HOST_NAME = "smtp.sendgrid.net";
           private static final String SMTP_AUTH_USER = "your_sendgrid_username";
           private static final String SMTP_AUTH_PWD = "your_sendgrid_password";

           public static void main(String[] args) throws Exception{
               new MyEmailer().SendMail();
           }

           public void SendMail() throws Exception
           {
              Properties properties = new Properties();
                 properties.put("mail.transport.protocol", "smtp");
                 properties.put("mail.smtp.host", SMTP_HOST_NAME);
                 properties.put("mail.smtp.port", 587);
                 properties.put("mail.smtp.auth", "true");
                 // …
```

1. 擴充 hello *javax.mail.Authenticator*類別，並在您實作*getPasswordAuthentication*方法，傳回您的 SendGrid 使用者名稱和密碼。  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. 透過 *javax.mail.Session* 物件建立經過驗證的電子郵件工作階段。  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. 建立郵件並指派 [收件者]、[寄件者]、[主旨] 和內容值。 這會顯示 hello [How To： 建立電子郵件](#how-to-create-an-email)> 一節。
4. 傳送 hello 訊息透過*javax.mail.Transport*物件。 這會顯示 hello [How To： 傳送電子郵件] [如何： 傳送電子郵件] 區段。

## <a name="how-to-create-an-email"></a>如何：建立電子郵件
hello 下列範例示範如何 toospecify 值一封電子郵件。

    MimeMessage message = new MimeMessage(mailSession);
    Multipart multipart = new MimeMultipart("alternative");
    BodyPart part1 = new MimeBodyPart();
    part1.setText("Hello, Your Contoso order has shipped. Thank you, John");
    BodyPart part2 = new MimeBodyPart();
    part2.setContent(
        "<p>Hello,</p>
        <p>Your Contoso order has <b>shipped</b>.</p>
        <p>Thank you,<br>John</br></p>",
        "text/html");
    multipart.addBodyPart(part1);
    multipart.addBodyPart(part2);
    message.setFrom(new InternetAddress("john@contoso.com"));
    message.addRecipient(Message.RecipientType.TO,
       new InternetAddress("someone@example.com"));
    message.setSubject("Your recent order");
    message.setContent(multipart);

## <a name="how-to-send-an-email"></a>如何：傳送電子郵件
hello 如何遵循顯示 toosend 電子郵件。

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>如何：新增附件
hello 下列程式碼示範您如何 tooadd 附件。

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify hello local file tooattach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses hello local file name as hello attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>如何： 使用篩選 tooenable 頁尾、 追蹤和分析
SendGrid 提供其他電子郵件功能，藉由使用 hello*篩選*。 這些是可以加入 tooan 電子郵件訊息，若要啟用特定的功能，例如啟用點選追蹤、 Google analytics、 追蹤、 訂用帳戶的設定，依此類推。 如需完整的篩選器清單，請參閱[篩選器設定][Filter Settings]。

* hello 下列範例示範如何 tooinsert 頁尾篩選，導致在 hello 電子郵件傳送的 hello 下方出現的 HTML 文字。

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* 另一個篩選器範例就是點擊追蹤。 比方說，電子郵件文字中包含超連結，例如 hello 下列項目，而且您想 tootrack hello 按一下頻率：

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* tooenable hello 按一下追蹤，下列程式碼使用 hello:

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>如何：更新電子郵件屬性
某些電子郵件內容會被覆寫使用**設定*屬性** * 或附加**新增*屬性** *。

例如，toospecify **ReplyTo**位址，請使用下列 hello:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

tooadd **Cc**收件者、 使用 hello 下列：

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>如何：使用其他 SendGrid 服務
SendGrid 提供網頁型應用程式開發介面，您可以從 Azure 應用程式使用 tooleverage 其他 SendGrid 功能。 完整的詳細資訊，請參閱 hello [SendGrid API 文件][SendGrid API documentation]。

## <a name="next-steps"></a>後續步驟
既然您已經學會 hello 的 hello SendGrid 電子郵件服務的基本概念，請遵循這些連結 toolearn 更多。

* 示範如何使用 SendGrid Azure 部署中的範例：[如何在 Azure 的部署中使用 SendGrid 從 Java toosend 電子郵件](store-sendgrid-java-how-to-send-email-example.md)
* SendGrid Java SDK：<https://sendgrid.com/docs/Code_Examples/java.html>
* SendGrid API 文件：<https://sendgrid.com/docs/API_Reference/index.html>
* Azure 客戶的 SendGrid 特別優惠：<https://sendgrid.com/windowsazure.html>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
[雲端架構電子郵件服務]: https://sendgrid.com/email-solutions
[交易式電子郵件傳遞]: https://sendgrid.com/transactional-email
