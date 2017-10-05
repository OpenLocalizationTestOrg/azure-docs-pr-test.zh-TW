---
title: "如何使用 SendGrid 電子郵件服務 (.NET) (.NET) | Microsoft Docs"
description: "了解如何在 Azure 使用 SendGrid 電子郵件服務傳送電子郵件。 程式碼範例是以 C# 撰寫並使用 .NET API。"
services: app-service-web
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: 
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: b3a48b3c838763b022a18e55817ec7455fe94c85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-send-email-using-sendgrid-with-azure"></a><span data-ttu-id="915ae-104">如何在 Azure 上使用 SendGrid 傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="915ae-104">How to Send Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="915ae-105">概觀</span><span class="sxs-lookup"><span data-stu-id="915ae-105">Overview</span></span>
<span data-ttu-id="915ae-106">本指南示範如何在 Azure 上透過 SendGrid 電子郵件服務執行常見程式設計工作。</span><span class="sxs-lookup"><span data-stu-id="915ae-106">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="915ae-107">這些範例均以 C\# 撰寫，且支援 .NET Standard 1.3。</span><span class="sxs-lookup"><span data-stu-id="915ae-107">The samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="915ae-108">涵蓋的案例包括建構電子郵件、傳送電子郵件、新增附件以及啟用各種郵件和追蹤設定。</span><span class="sxs-lookup"><span data-stu-id="915ae-108">The scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="915ae-109">如需有關 SendGrid 及傳送電子郵件的詳細資訊，請參閱[後續步驟][Next steps]一節。</span><span class="sxs-lookup"><span data-stu-id="915ae-109">For more information on SendGrid and sending email, see the [Next steps][Next steps] section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="915ae-110">什麼是 SendGrid 電子郵件服務？</span><span class="sxs-lookup"><span data-stu-id="915ae-110">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="915ae-111">SendGrid 是 [雲端架構電子郵件服務]，能提供可靠的 [交易式電子郵件傳遞]、擴充性和即時分析，以及有彈性的 API 來輕鬆進行自訂整合。</span><span class="sxs-lookup"><span data-stu-id="915ae-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="915ae-112">常見的 SendGrid 使用案例包括︰</span><span class="sxs-lookup"><span data-stu-id="915ae-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="915ae-113">自動將收據或採購確認傳送給客戶。</span><span class="sxs-lookup"><span data-stu-id="915ae-113">Automatically sending receipts or purchase confirmations to customers.</span></span>
* <span data-ttu-id="915ae-114">管理通訊群組清單，以便將每月傳單和促銷傳送給客戶。</span><span class="sxs-lookup"><span data-stu-id="915ae-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="915ae-115">收集封鎖的電子郵件和客戶參與情形等項目的即時計量。</span><span class="sxs-lookup"><span data-stu-id="915ae-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="915ae-116">轉寄客戶查詢。</span><span class="sxs-lookup"><span data-stu-id="915ae-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="915ae-117">處理內送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="915ae-117">Processing incoming emails.</span></span>

<span data-ttu-id="915ae-118">如需詳細資訊，請造訪 [https://sendgrid.com](https://sendgrid.com) 或 SendGrid 的 [C# 程式庫][sendgrid-csharp] GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="915ae-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="915ae-119">建立 SendGrid 帳戶</span><span class="sxs-lookup"><span data-stu-id="915ae-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-net-class-library"></a><span data-ttu-id="915ae-120">參考 SendGrid .NET 類別庫</span><span class="sxs-lookup"><span data-stu-id="915ae-120">Reference the SendGrid .NET Class Library</span></span>
<span data-ttu-id="915ae-121">[SendGrid NuGet 封裝](https://www.nuget.org/packages/Sendgrid) 是取得 SendGrid API 及透過所有相依性設定應用程式的最簡單方式。</span><span class="sxs-lookup"><span data-stu-id="915ae-121">The [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is the easiest way to get the SendGrid API and to configure your application with all dependencies.</span></span> <span data-ttu-id="915ae-122">NuGet 是 Microsoft Visual Studio 2015 和更新版本隨附的 Visual Studio 擴充，能輕鬆地安裝及更新程式庫和工具。</span><span class="sxs-lookup"><span data-stu-id="915ae-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy to install and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="915ae-123">如果您是執行 Visual Studio 2015 之前的 Visual Studio 版本，若要安裝 NuGet，請造訪 [http://www.nuget.org](http://www.nuget.org)，然後按一下 **安裝 NuGet** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="915ae-123">To install NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click the **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="915ae-124">若要在應用程式中安裝 SendGrid NuGet 封裝，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="915ae-124">To install the SendGrid NuGet package in your application, do the following:</span></span>

1. <span data-ttu-id="915ae-125">按一下 [新增專案]，然後選取 [範本]。</span><span class="sxs-lookup"><span data-stu-id="915ae-125">Click on **New Project** and select a **Template**.</span></span>

   ![建立新專案][create-new-project]
2. <span data-ttu-id="915ae-127">在 [方案總管] 中，以滑鼠右鍵按一下 [參考]，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="915ae-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![SendGrid NuGet 封裝][SendGrid-NuGet-package]
3. <span data-ttu-id="915ae-129">搜尋 **SendGrid**，然後選取結果清單中的 [SendGrid] 項目。</span><span class="sxs-lookup"><span data-stu-id="915ae-129">Search for **SendGrid** and select the **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="915ae-130">從版本下拉式清單中選取 Nuget 套件的最新穩定版本，以搭配本文示範的物件模型和 API 共同使用。</span><span class="sxs-lookup"><span data-stu-id="915ae-130">Select the latest stable version of the Nuget package from the version dropdown to be able to work with the object model and APIs demonstrated in this article.</span></span>

   ![SendGrid 套件][sendgrid-package]
5. <span data-ttu-id="915ae-132">按一下 [安裝]  完成安裝，然後關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="915ae-132">Click **Install** to complete the installation, and then close this dialog.</span></span>

<span data-ttu-id="915ae-133">SendGrid 的 .NET 類別庫稱為 **SendGrid**。</span><span class="sxs-lookup"><span data-stu-id="915ae-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="915ae-134">其中包含下列命名空間：</span><span class="sxs-lookup"><span data-stu-id="915ae-134">It contains the following namespaces:</span></span>

* <span data-ttu-id="915ae-135">**SendGrid** 用以與 SendGrid 的 API 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="915ae-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="915ae-136">**SendGrid.Helpers.Mail** 讓協助程式方法可以輕鬆建立 SendGridMessage 物件，以指定如何傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="915ae-136">**SendGrid.Helpers.Mail** for helper methods to easily create SendGridMessage objects that specify how to send emails.</span></span>

<span data-ttu-id="915ae-137">將下列程式碼命名空間宣告，新增至您想要在其中以程式設計方式存取 SendGrid 電子郵件服務之任何 C# 檔案內的頂端。</span><span class="sxs-lookup"><span data-stu-id="915ae-137">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access the SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="915ae-138">如何：建立電子郵件</span><span class="sxs-lookup"><span data-stu-id="915ae-138">How to: Create an Email</span></span>
<span data-ttu-id="915ae-139">使用 **SendGridMessage** 物件來建立電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="915ae-139">Use the **SendGridMessage** object to create an email message.</span></span> <span data-ttu-id="915ae-140">建立訊息物件後，即可設定屬性和方法，包括電子郵件寄件者、電子郵件收件者以及電子郵件的主旨和本文。</span><span class="sxs-lookup"><span data-stu-id="915ae-140">Once the message object is created, you can set properties and methods, including the email sender, the email recipient, and the subject and body of the email.</span></span>

<span data-ttu-id="915ae-141">下列範例示範如何建立完全填入的電子郵件物件：</span><span class="sxs-lookup"><span data-stu-id="915ae-141">The following example demonstrates how to create a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing the SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="915ae-142">如需 **SendGrid** 類型支援的所有屬性和方法的詳細資訊，請參閱 GitHub 上的 [sendgrid-csharp][sendgrid-csharp]。</span><span class="sxs-lookup"><span data-stu-id="915ae-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="915ae-143">如何：傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="915ae-143">How to: Send an Email</span></span>
<span data-ttu-id="915ae-144">建立電子郵件訊息之後，您可以使用 SendGrid 的 API 進行傳送。</span><span class="sxs-lookup"><span data-stu-id="915ae-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="915ae-145">或者，您也可以使用 [.NET 的內建程式庫][NET-library]。</span><span class="sxs-lookup"><span data-stu-id="915ae-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="915ae-146">傳送電子郵件需要您提供 SendGrid API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="915ae-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="915ae-147">如需有關如何設定 API 金鑰的詳細資訊，請參閱 SendGrid 的 API 金鑰[文件][documentation]。</span><span class="sxs-lookup"><span data-stu-id="915ae-147">If you need details about how to configure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="915ae-148">您可以透過 Azure 入口網站儲存這些認證，只要按一下 [應用程式設定]，並在 [應用程式設定] 下新增金鑰/值組。</span><span class="sxs-lookup"><span data-stu-id="915ae-148">You may store these credentials via your Azure Portal by clicking Application settings and adding the key/value pairs under App settings.</span></span>

 ![Azure 應用程式設定][azure_app_settings]

 <span data-ttu-id="915ae-150">然後，您可以使用下列方式進行存取：</span><span class="sxs-lookup"><span data-stu-id="915ae-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="915ae-151">下列範例顯示如何使用 Web API 傳送郵件。</span><span class="sxs-lookup"><span data-stu-id="915ae-151">The following examples show how to send a message using the Web API.</span></span>

    using System;
    using System.Threading.Tasks;
    using SendGrid;
    using SendGrid.Helpers.Mail;

    namespace Example
    {
        internal class Example
        {
            private static void Main()
            {
                Execute().Wait();
            }

            static async Task Execute()
            {
                var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
                var client = new SendGridClient(apiKey);
                var msg = new SendGridMessage()
                {
                    From = new EmailAddress("test@example.com", "DX Team"),
                    Subject = "Hello World from the SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="915ae-152">如何：新增附件</span><span class="sxs-lookup"><span data-stu-id="915ae-152">How to: Add an attachment</span></span>
<span data-ttu-id="915ae-153">呼叫 **AddAttachment** 方法並最小指定您要附加的檔案名稱和 Base64 編碼內容，即可將附件新增至訊息。</span><span class="sxs-lookup"><span data-stu-id="915ae-153">Attachments can be added to a message by calling the **AddAttachment** method and minimally specifying the file name and Base64 encoded content you want to attach.</span></span> <span data-ttu-id="915ae-154">您可以對想要附加的每個檔案呼叫一次此方法，或是使用 **AddAttachments** 方法，即可包含多個附件。</span><span class="sxs-lookup"><span data-stu-id="915ae-154">You can include multiple attachments by calling this method once for each file you wish to attach or by using the **AddAttachments** method.</span></span> <span data-ttu-id="915ae-155">下列範例示範如何將附件新增至郵件：</span><span class="sxs-lookup"><span data-stu-id="915ae-155">The following example demonstrates adding an attachment to a message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="915ae-156">如何：使用郵件設定來啟用頁尾、追蹤和分析</span><span class="sxs-lookup"><span data-stu-id="915ae-156">How to: Use mail settings to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="915ae-157">透過使用郵件設定和追蹤設定，SendGrid 提供了其他電子郵件功能。</span><span class="sxs-lookup"><span data-stu-id="915ae-157">SendGrid provides additional email functionality through the use of mail settings and tracking settings.</span></span> <span data-ttu-id="915ae-158">這些設定可新增至電子郵件訊息以啟用特定功能，例如點選追蹤、Google 分析、訂用帳戶追蹤等等。</span><span class="sxs-lookup"><span data-stu-id="915ae-158">These settings can be added to an email message to enable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="915ae-159">如需應用程式的完整清單，請參閱[設定文件][settings-documentation]。</span><span class="sxs-lookup"><span data-stu-id="915ae-159">For a full list of apps, see the [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="915ae-160">使用與 **SendGridMessage** 類別一起實作的方法，即可將應用程式套用至 **SendGrid** 電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="915ae-160">Apps can be applied to **SendGrid** email messages using methods implemented as part of the **SendGridMessage** class.</span></span> <span data-ttu-id="915ae-161">下列範例示範頁尾和點選追蹤篩選器：</span><span class="sxs-lookup"><span data-stu-id="915ae-161">The following examples demonstrate the footer and click tracking filters:</span></span>

<span data-ttu-id="915ae-162">下列範例示範頁尾和點選追蹤篩選器：</span><span class="sxs-lookup"><span data-stu-id="915ae-162">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="915ae-163">頁尾設定</span><span class="sxs-lookup"><span data-stu-id="915ae-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="915ae-164">點選追蹤</span><span class="sxs-lookup"><span data-stu-id="915ae-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="915ae-165">如何：使用其他 SendGrid 服務</span><span class="sxs-lookup"><span data-stu-id="915ae-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="915ae-166">SendGrid 提供多個 API 與 Webhook，可供您在 Azure 應用程式中運用其他功能。</span><span class="sxs-lookup"><span data-stu-id="915ae-166">SendGrid offers several APIs and webhooks that you can use to leverage additional functionality within your Azure application.</span></span> <span data-ttu-id="915ae-167">如需詳細資訊，請參閱 [SendGrid API 參考][SendGrid API documentation]。</span><span class="sxs-lookup"><span data-stu-id="915ae-167">For more details, see the [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="915ae-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="915ae-168">Next steps</span></span>
<span data-ttu-id="915ae-169">了解 SendGrid 電子郵件服務的基本概念後，請參考下列連結以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="915ae-169">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="915ae-170">SendGrid C\# 程式庫儲存機制：[sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="915ae-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="915ae-171">SendGrid API 文件︰<https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="915ae-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is the SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference the SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters to Enable Footers, Tracking, and Analytics]: #usefilters
[How to: Use Additional SendGrid Services]: #useservices

[create-new-project]: ./media/sendgrid-dotnet-how-to-send-email/new-project.png
[SendGrid-NuGet-package]: ./media/sendgrid-dotnet-how-to-send-email/reference.png
[sendgrid-package]: ./media/sendgrid-dotnet-how-to-send-email/sendgrid-package.png
[azure_app_settings]: ./media/sendgrid-dotnet-how-to-send-email/azure-app-settings.png
[sendgrid-csharp]: https://github.com/sendgrid/sendgrid-csharp
[SMTP vs. Web API]: https://sendgrid.com/docs/Integrate/index.html
[App Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/api_v3.html
[NET-library]: https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html#-Using-NETs-Builtin-SMTP-Library
[documentation]: https://sendgrid.com/docs/Classroom/Send/api_keys.html
[settings-documentation]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html

<span data-ttu-id="915ae-172">[雲端架構電子郵件服務]: https://sendgrid.com/solutions</span><span class="sxs-lookup"><span data-stu-id="915ae-172">[cloud-based email service]: https://sendgrid.com/solutions</span></span>
<span data-ttu-id="915ae-173">[交易式電子郵件傳遞]: https://sendgrid.com/use-cases/transactional-email</span><span class="sxs-lookup"><span data-stu-id="915ae-173">[transactional email delivery]: https://sendgrid.com/use-cases/transactional-email</span></span>

