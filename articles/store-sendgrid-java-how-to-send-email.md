---
title: "如何使用 SendGrid 電子郵件服務 (Java) | Microsoft Docs"
description: "了解如何在 Azure 使用 SendGrid 電子郵件服務傳送電子郵件。 程式碼範例以 Java 撰寫。"
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
ms.openlocfilehash: 85a0e302626ca14ac039ee6f662f372ddbeb62c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java"></a><span data-ttu-id="04552-104">如何使用 SendGrid 透過 Java 傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="04552-104">How to Send Email Using SendGrid from Java</span></span>
<span data-ttu-id="04552-105">本指南示範如何在 Azure 上透過 SendGrid 電子郵件服務執行常見程式設計工作。</span><span class="sxs-lookup"><span data-stu-id="04552-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="04552-106">相關範例是以 Java 撰寫的。</span><span class="sxs-lookup"><span data-stu-id="04552-106">The samples are written in Java.</span></span> <span data-ttu-id="04552-107">涵蓋的案例包括**建構電子郵件**、**傳送電子郵件**、**新增附件**、**使用篩選器**及**更新屬性**。</span><span class="sxs-lookup"><span data-stu-id="04552-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="04552-108">如需有關 SendGrid 及傳送電子郵件的詳細資訊，請參閱[後續步驟](#next-steps)一節。</span><span class="sxs-lookup"><span data-stu-id="04552-108">For more information on SendGrid and sending email, see the [Next steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="04552-109">什麼是 SendGrid 電子郵件服務？</span><span class="sxs-lookup"><span data-stu-id="04552-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="04552-110">SendGrid 是 [雲端架構電子郵件服務]，能提供可靠的 [交易式電子郵件傳遞]、擴充性和即時分析，以及有彈性的 API 來輕鬆進行自訂整合。</span><span class="sxs-lookup"><span data-stu-id="04552-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="04552-111">常見的 SendGrid 使用案例包括：</span><span class="sxs-lookup"><span data-stu-id="04552-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="04552-112">自動傳送回條給客戶</span><span class="sxs-lookup"><span data-stu-id="04552-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="04552-113">管理通訊群組清單，以便將每月電子傳單和特別優惠傳送給客戶</span><span class="sxs-lookup"><span data-stu-id="04552-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="04552-114">收集封鎖的電子郵件、客戶的回應情形等項目的即時度量</span><span class="sxs-lookup"><span data-stu-id="04552-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="04552-115">產生報表，協助找出趨勢</span><span class="sxs-lookup"><span data-stu-id="04552-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="04552-116">轉寄客戶查詢</span><span class="sxs-lookup"><span data-stu-id="04552-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="04552-117">透過電子郵件從您的應用程式傳送通知</span><span class="sxs-lookup"><span data-stu-id="04552-117">Email notifications from your application</span></span>

<span data-ttu-id="04552-118">如需詳細資訊，請參閱 <http://sendgrid.com>。</span><span class="sxs-lookup"><span data-stu-id="04552-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="04552-119">建立 SendGrid 帳戶</span><span class="sxs-lookup"><span data-stu-id="04552-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-the-javaxmail-libraries"></a><span data-ttu-id="04552-120">如何：使用 javax.mail 程式庫</span><span class="sxs-lookup"><span data-stu-id="04552-120">How to: Use the javax.mail libraries</span></span>
<span data-ttu-id="04552-121">取得 javax.mail 程式庫，例如從 <http://www.oracle.com/technetwork/java/javamail> 並將其匯入您的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="04552-121">Obtain the javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="04552-122">使用 javax.mail 程式庫來傳送採用 SMTP 之電子郵件的高層級程序就是執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="04552-122">At a high-level, the process for using the javax.mail library to send email using SMTP is to do the following:</span></span>

1. <span data-ttu-id="04552-123">指定 SMTP 值 (包括 SMTP 伺服器)，對 SendGrid 而言是 smtp.sendgrid.net。</span><span class="sxs-lookup"><span data-stu-id="04552-123">Specify the SMTP values, including the SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

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

1. <span data-ttu-id="04552-124">擴充 *javax.mail.Authenticator* 類別，以及在 *getPasswordAuthentication* 方法的實作中，傳回您的 SendGrid 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="04552-124">Extend the *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="04552-125">透過 *javax.mail.Session* 物件建立經過驗證的電子郵件工作階段。</span><span class="sxs-lookup"><span data-stu-id="04552-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="04552-126">建立郵件並指派 [收件者]、[寄件者]、[主旨] 和內容值。</span><span class="sxs-lookup"><span data-stu-id="04552-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="04552-127">這顯示在[如何：建立電子郵件](#how-to-create-an-email)一節中。</span><span class="sxs-lookup"><span data-stu-id="04552-127">This is shown in the [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="04552-128">透過 *javax.mail.Transport* 物件傳送郵件。</span><span class="sxs-lookup"><span data-stu-id="04552-128">Send the message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="04552-129">這顯示在 [如何：傳送電子郵件][如何：傳送電子郵件] 一節中。</span><span class="sxs-lookup"><span data-stu-id="04552-129">This is shown in the [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="04552-130">如何：建立電子郵件</span><span class="sxs-lookup"><span data-stu-id="04552-130">How to: Create an email</span></span>
<span data-ttu-id="04552-131">下列程式碼顯示如何指定電子郵件的值。</span><span class="sxs-lookup"><span data-stu-id="04552-131">The following shows how to specify values for an email.</span></span>

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

## <a name="how-to-send-an-email"></a><span data-ttu-id="04552-132">如何：傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="04552-132">How to: Send an email</span></span>
<span data-ttu-id="04552-133">下列程式碼顯示如何傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="04552-133">The following shows how to send an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect the transport object.
    transport.connect();
    // Send the message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close the connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="04552-134">如何：新增附件</span><span class="sxs-lookup"><span data-stu-id="04552-134">How to: Add an attachment</span></span>
<span data-ttu-id="04552-135">下列程式碼顯示如何新增附件。</span><span class="sxs-lookup"><span data-stu-id="04552-135">The following code shows you how to add an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify the local file to attach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses the local file name as the attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="04552-136">如何：使用篩選器來啟用頁尾、追蹤和分析</span><span class="sxs-lookup"><span data-stu-id="04552-136">How to: Use filters to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="04552-137">SendGrid 運用「篩選器」提供其他電子郵件功能。</span><span class="sxs-lookup"><span data-stu-id="04552-137">SendGrid provides additional email functionality through the use of *filters*.</span></span> <span data-ttu-id="04552-138">這些設定可新增到電子郵件以啟用特定功能，例如啟用點擊追蹤、Google 分析、訂閱追蹤等。</span><span class="sxs-lookup"><span data-stu-id="04552-138">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="04552-139">如需完整的篩選器清單，請參閱[篩選器設定][Filter Settings]。</span><span class="sxs-lookup"><span data-stu-id="04552-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="04552-140">下列程式碼顯示如何插入頁尾篩選器，以使 HTML 文字出現在傳送之電子郵件的底部。</span><span class="sxs-lookup"><span data-stu-id="04552-140">The following shows how to insert a footer filter that results in HTML text appearing at the bottom of the email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="04552-141">另一個篩選器範例就是點擊追蹤。</span><span class="sxs-lookup"><span data-stu-id="04552-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="04552-142">假設您的電子郵件文字包含超連結 (如下所示)，而您想要追蹤點擊率：</span><span class="sxs-lookup"><span data-stu-id="04552-142">Let’s say that your email text contains a hyperlink, such as the following, and you want to track the click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is the body of the message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="04552-143">若要啟用點擊追蹤，請使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="04552-143">To enable the click tracking, use the following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="04552-144">如何：更新電子郵件屬性</span><span class="sxs-lookup"><span data-stu-id="04552-144">How to: Update email properties</span></span>
<span data-ttu-id="04552-145">某些電子郵件內容會被覆寫使用**設定*屬性** * 或附加**新增*屬性** *。</span><span class="sxs-lookup"><span data-stu-id="04552-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="04552-146">例如，若要指定 **ReplyTo** 地址，請使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="04552-146">For example, to specify **ReplyTo** addresses, use the following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="04552-147">若要增加 [副本] 收件者，請使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="04552-147">To add a **Cc** recipient, use the following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="04552-148">如何：使用其他 SendGrid 服務</span><span class="sxs-lookup"><span data-stu-id="04552-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="04552-149">SendGrid 提供的網頁式 API 可供從 Azure 應用程式運用其他 SendGrid 功能。</span><span class="sxs-lookup"><span data-stu-id="04552-149">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="04552-150">如需完整詳細資料，請參閱 [SendGrid API 文件][SendGrid API documentation]。</span><span class="sxs-lookup"><span data-stu-id="04552-150">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="04552-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04552-151">Next steps</span></span>
<span data-ttu-id="04552-152">了解 SendGrid 電子郵件服務的基本概念後，請參考下列連結以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="04552-152">Now that you’ve learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="04552-153">示範在 Azure 部署中使用 SendGrid 的範例：[如何在 Azure 部署中使用 SendGrid 透過 Java 傳送電子郵件](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="04552-153">Sample that demonstrates using SendGrid in an Azure deployment: [How to send email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="04552-154">SendGrid Java SDK：<https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="04552-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="04552-155">SendGrid API 文件：<https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="04552-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="04552-156">Azure 客戶的 SendGrid 特別優惠：<https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="04552-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
<span data-ttu-id="04552-157">[雲端架構電子郵件服務]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="04552-157">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="04552-158">[交易式電子郵件傳遞]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="04552-158">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
