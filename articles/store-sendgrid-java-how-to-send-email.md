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
# <a name="how-toosend-email-using-sendgrid-from-java"></a><span data-ttu-id="b7901-104">如何 tooSend 電子郵件從 Java 使用 SendGrid</span><span class="sxs-lookup"><span data-stu-id="b7901-104">How tooSend Email Using SendGrid from Java</span></span>
<span data-ttu-id="b7901-105">本指南示範如何 tooperform 常見的程式設計工作使用 SendGrid 傳送電子郵件在 Azure 上的服務。</span><span class="sxs-lookup"><span data-stu-id="b7901-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="b7901-106">hello 範例是以 Java 撰寫。</span><span class="sxs-lookup"><span data-stu-id="b7901-106">hello samples are written in Java.</span></span> <span data-ttu-id="b7901-107">hello 涵蓋案例包括**建構電子郵件**，**傳送電子郵件**，**加入附件**，**使用篩選器**，和**更新屬性**。</span><span class="sxs-lookup"><span data-stu-id="b7901-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="b7901-108">如需有關 SendGrid 和傳送電子郵件的詳細資訊，請參閱 hello[後續步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="b7901-108">For more information on SendGrid and sending email, see hello [Next steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="b7901-109">什麼是 hello SendGrid 電子郵件服務？</span><span class="sxs-lookup"><span data-stu-id="b7901-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="b7901-110">SendGrid 是 [雲端架構電子郵件服務]，能提供可靠的 [交易式電子郵件傳遞]、擴充性和即時分析，以及有彈性的 API 來輕鬆進行自訂整合。</span><span class="sxs-lookup"><span data-stu-id="b7901-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="b7901-111">常見的 SendGrid 使用案例包括：</span><span class="sxs-lookup"><span data-stu-id="b7901-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="b7901-112">自動將資料傳送回條 toocustomers</span><span class="sxs-lookup"><span data-stu-id="b7901-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="b7901-113">管理通訊群組清單，以便將每月電子傳單和特別優惠傳送給客戶</span><span class="sxs-lookup"><span data-stu-id="b7901-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="b7901-114">收集封鎖的電子郵件、客戶的回應情形等項目的即時度量</span><span class="sxs-lookup"><span data-stu-id="b7901-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="b7901-115">產生 toohelp 識別趨勢的報表</span><span class="sxs-lookup"><span data-stu-id="b7901-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="b7901-116">轉寄客戶查詢</span><span class="sxs-lookup"><span data-stu-id="b7901-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="b7901-117">透過電子郵件從您的應用程式傳送通知</span><span class="sxs-lookup"><span data-stu-id="b7901-117">Email notifications from your application</span></span>

<span data-ttu-id="b7901-118">如需詳細資訊，請參閱 <http://sendgrid.com>。</span><span class="sxs-lookup"><span data-stu-id="b7901-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="b7901-119">建立 SendGrid 帳戶</span><span class="sxs-lookup"><span data-stu-id="b7901-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a><span data-ttu-id="b7901-120">如何： 使用 hello javax.mail 程式庫</span><span class="sxs-lookup"><span data-stu-id="b7901-120">How to: Use hello javax.mail libraries</span></span>
<span data-ttu-id="b7901-121">取得 hello javax.mail 程式庫，例如從<http://www.oracle.com/technetwork/java/javamail> ，匯入您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b7901-121">Obtain hello javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="b7901-122">高階 hello 程序使用 hello javax.mail 文件庫 toosend 電子郵件使用 SMTP 是 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="b7901-122">At a high-level, hello process for using hello javax.mail library toosend email using SMTP is toodo hello following:</span></span>

1. <span data-ttu-id="b7901-123">指定 hello SMTP 值，包括即 sendgrid smtp.sendgrid.net hello SMTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b7901-123">Specify hello SMTP values, including hello SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

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

1. <span data-ttu-id="b7901-124">擴充 hello *javax.mail.Authenticator*類別，並在您實作*getPasswordAuthentication*方法，傳回您的 SendGrid 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b7901-124">Extend hello *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="b7901-125">透過 *javax.mail.Session* 物件建立經過驗證的電子郵件工作階段。</span><span class="sxs-lookup"><span data-stu-id="b7901-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="b7901-126">建立郵件並指派 [收件者]、[寄件者]、[主旨] 和內容值。</span><span class="sxs-lookup"><span data-stu-id="b7901-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="b7901-127">這會顯示 hello [How To： 建立電子郵件](#how-to-create-an-email)> 一節。</span><span class="sxs-lookup"><span data-stu-id="b7901-127">This is shown in hello [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="b7901-128">傳送 hello 訊息透過*javax.mail.Transport*物件。</span><span class="sxs-lookup"><span data-stu-id="b7901-128">Send hello message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="b7901-129">這會顯示 hello [How To： 傳送電子郵件] [如何： 傳送電子郵件] 區段。</span><span class="sxs-lookup"><span data-stu-id="b7901-129">This is shown in hello [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="b7901-130">如何：建立電子郵件</span><span class="sxs-lookup"><span data-stu-id="b7901-130">How to: Create an email</span></span>
<span data-ttu-id="b7901-131">hello 下列範例示範如何 toospecify 值一封電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b7901-131">hello following shows how toospecify values for an email.</span></span>

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

## <a name="how-to-send-an-email"></a><span data-ttu-id="b7901-132">如何：傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="b7901-132">How to: Send an email</span></span>
<span data-ttu-id="b7901-133">hello 如何遵循顯示 toosend 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b7901-133">hello following shows how toosend an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="b7901-134">如何：新增附件</span><span class="sxs-lookup"><span data-stu-id="b7901-134">How to: Add an attachment</span></span>
<span data-ttu-id="b7901-135">hello 下列程式碼示範您如何 tooadd 附件。</span><span class="sxs-lookup"><span data-stu-id="b7901-135">hello following code shows you how tooadd an attachment.</span></span>

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="b7901-136">如何： 使用篩選 tooenable 頁尾、 追蹤和分析</span><span class="sxs-lookup"><span data-stu-id="b7901-136">How to: Use filters tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="b7901-137">SendGrid 提供其他電子郵件功能，藉由使用 hello*篩選*。</span><span class="sxs-lookup"><span data-stu-id="b7901-137">SendGrid provides additional email functionality through hello use of *filters*.</span></span> <span data-ttu-id="b7901-138">這些是可以加入 tooan 電子郵件訊息，若要啟用特定的功能，例如啟用點選追蹤、 Google analytics、 追蹤、 訂用帳戶的設定，依此類推。</span><span class="sxs-lookup"><span data-stu-id="b7901-138">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="b7901-139">如需完整的篩選器清單，請參閱[篩選器設定][Filter Settings]。</span><span class="sxs-lookup"><span data-stu-id="b7901-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="b7901-140">hello 下列範例示範如何 tooinsert 頁尾篩選，導致在 hello 電子郵件傳送的 hello 下方出現的 HTML 文字。</span><span class="sxs-lookup"><span data-stu-id="b7901-140">hello following shows how tooinsert a footer filter that results in HTML text appearing at hello bottom of hello email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="b7901-141">另一個篩選器範例就是點擊追蹤。</span><span class="sxs-lookup"><span data-stu-id="b7901-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="b7901-142">比方說，電子郵件文字中包含超連結，例如 hello 下列項目，而且您想 tootrack hello 按一下頻率：</span><span class="sxs-lookup"><span data-stu-id="b7901-142">Let’s say that your email text contains a hyperlink, such as hello following, and you want tootrack hello click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="b7901-143">tooenable hello 按一下追蹤，下列程式碼使用 hello:</span><span class="sxs-lookup"><span data-stu-id="b7901-143">tooenable hello click tracking, use hello following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="b7901-144">如何：更新電子郵件屬性</span><span class="sxs-lookup"><span data-stu-id="b7901-144">How to: Update email properties</span></span>
<span data-ttu-id="b7901-145">某些電子郵件內容會被覆寫使用**設定*屬性** * 或附加**新增*屬性** *。</span><span class="sxs-lookup"><span data-stu-id="b7901-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="b7901-146">例如，toospecify **ReplyTo**位址，請使用下列 hello:</span><span class="sxs-lookup"><span data-stu-id="b7901-146">For example, toospecify **ReplyTo** addresses, use hello following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="b7901-147">tooadd **Cc**收件者、 使用 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="b7901-147">tooadd a **Cc** recipient, use hello following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="b7901-148">如何：使用其他 SendGrid 服務</span><span class="sxs-lookup"><span data-stu-id="b7901-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="b7901-149">SendGrid 提供網頁型應用程式開發介面，您可以從 Azure 應用程式使用 tooleverage 其他 SendGrid 功能。</span><span class="sxs-lookup"><span data-stu-id="b7901-149">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="b7901-150">完整的詳細資訊，請參閱 hello [SendGrid API 文件][SendGrid API documentation]。</span><span class="sxs-lookup"><span data-stu-id="b7901-150">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7901-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7901-151">Next steps</span></span>
<span data-ttu-id="b7901-152">既然您已經學會 hello 的 hello SendGrid 電子郵件服務的基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="b7901-152">Now that you’ve learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="b7901-153">示範如何使用 SendGrid Azure 部署中的範例：[如何在 Azure 的部署中使用 SendGrid 從 Java toosend 電子郵件](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="b7901-153">Sample that demonstrates using SendGrid in an Azure deployment: [How toosend email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="b7901-154">SendGrid Java SDK：<https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="b7901-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="b7901-155">SendGrid API 文件：<https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="b7901-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="b7901-156">Azure 客戶的 SendGrid 特別優惠：<https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="b7901-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

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
