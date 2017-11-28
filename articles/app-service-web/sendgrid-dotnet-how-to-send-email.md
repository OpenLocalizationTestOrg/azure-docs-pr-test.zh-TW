---
title: "aaaHow toouse hello SendGrid 電子郵件服務 (.NET) |Microsoft 文件"
description: "深入了解如何在 Azure 上傳送電子郵件以 hello SendGrid 電子郵件服務。 以 C# 和使用 hello.NET API 撰寫的程式碼範例。"
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
ms.openlocfilehash: b3d77bb67898b991c7293e6b9086b263f6bcb755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-with-azure"></a><span data-ttu-id="30def-104">如何使用 Azure 的電子郵件使用 SendGrid tooSend</span><span class="sxs-lookup"><span data-stu-id="30def-104">How tooSend Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="30def-105">概觀</span><span class="sxs-lookup"><span data-stu-id="30def-105">Overview</span></span>
<span data-ttu-id="30def-106">本指南示範如何 tooperform 常見的程式設計工作使用 SendGrid 傳送電子郵件在 Azure 上的服務。</span><span class="sxs-lookup"><span data-stu-id="30def-106">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="30def-107">hello 範例以 C 撰寫\#並且支援.NET 標準 1.3。</span><span class="sxs-lookup"><span data-stu-id="30def-107">hello samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="30def-108">涵蓋的 hello 案例包括建構的電子郵件、 傳送電子郵件、 加入附件，並啟用各種 mail 和追蹤設定。</span><span class="sxs-lookup"><span data-stu-id="30def-108">hello scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="30def-109">如需有關 SendGrid 和傳送電子郵件的詳細資訊，請參閱 hello[後續步驟][ Next steps] > 一節。</span><span class="sxs-lookup"><span data-stu-id="30def-109">For more information on SendGrid and sending email, see hello [Next steps][Next steps] section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="30def-110">什麼是 hello SendGrid 電子郵件服務？</span><span class="sxs-lookup"><span data-stu-id="30def-110">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="30def-111">SendGrid 是 [雲端架構電子郵件服務]，能提供可靠的 [交易式電子郵件傳遞]、擴充性和即時分析，以及有彈性的 API 來輕鬆進行自訂整合。</span><span class="sxs-lookup"><span data-stu-id="30def-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="30def-112">常見的 SendGrid 使用案例包括︰</span><span class="sxs-lookup"><span data-stu-id="30def-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="30def-113">自動將資料傳送回條或採購確認 toocustomers。</span><span class="sxs-lookup"><span data-stu-id="30def-113">Automatically sending receipts or purchase confirmations toocustomers.</span></span>
* <span data-ttu-id="30def-114">管理通訊群組清單，以便將每月傳單和促銷傳送給客戶。</span><span class="sxs-lookup"><span data-stu-id="30def-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="30def-115">收集封鎖的電子郵件和客戶參與情形等項目的即時計量。</span><span class="sxs-lookup"><span data-stu-id="30def-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="30def-116">轉寄客戶查詢。</span><span class="sxs-lookup"><span data-stu-id="30def-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="30def-117">處理內送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="30def-117">Processing incoming emails.</span></span>

<span data-ttu-id="30def-118">如需詳細資訊，請造訪 [https://sendgrid.com](https://sendgrid.com) 或 SendGrid 的 [C# 程式庫][sendgrid-csharp] GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="30def-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="30def-119">建立 SendGrid 帳戶</span><span class="sxs-lookup"><span data-stu-id="30def-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a><span data-ttu-id="30def-120">參考 hello SendGrid.NET 類別庫</span><span class="sxs-lookup"><span data-stu-id="30def-120">Reference hello SendGrid .NET Class Library</span></span>
<span data-ttu-id="30def-121">hello [SendGrid NuGet 套件](https://www.nuget.org/packages/Sendgrid)是最簡單方式 tooget hello hello SendGrid API 和 tooconfigure 所有相依性的應用程式。</span><span class="sxs-lookup"><span data-stu-id="30def-121">hello [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is hello easiest way tooget hello SendGrid API and tooconfigure your application with all dependencies.</span></span> <span data-ttu-id="30def-122">NuGet 是 Visual Studio 擴充功能包含 Microsoft Visual Studio 2015 或更新版本，可輕鬆 tooinstall 和更新的程式庫和工具。</span><span class="sxs-lookup"><span data-stu-id="30def-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy tooinstall and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="30def-123">tooinstall NuGet 如果您正在 Visual Studio 的版本早於 Visual Studio 2015，請瀏覽[http://www.nuget.org](http://www.nuget.org)，然後按一下 hello**安裝 NuGet**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="30def-123">tooinstall NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click hello **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="30def-124">tooinstall hello SendGrid NuGet 封裝，應用程式中 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="30def-124">tooinstall hello SendGrid NuGet package in your application, do hello following:</span></span>

1. <span data-ttu-id="30def-125">按一下 [新增專案]，然後選取 [範本]。</span><span class="sxs-lookup"><span data-stu-id="30def-125">Click on **New Project** and select a **Template**.</span></span>

   ![建立新專案][create-new-project]
2. <span data-ttu-id="30def-127">在 [方案總管] 中，以滑鼠右鍵按一下 [參考]，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="30def-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![SendGrid NuGet 封裝][SendGrid-NuGet-package]
3. <span data-ttu-id="30def-129">搜尋**SendGrid**和選取 hello **SendGrid**結果清單中的項目。</span><span class="sxs-lookup"><span data-stu-id="30def-129">Search for **SendGrid** and select hello **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="30def-130">選取從 hello 版本下拉式清單中 toobe 無法 toowork hello 物件模型與應用程式開發介面，在本文中示範的 hello 最新穩定版本 hello Nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="30def-130">Select hello latest stable version of hello Nuget package from hello version dropdown toobe able toowork with hello object model and APIs demonstrated in this article.</span></span>

   ![SendGrid 套件][sendgrid-package]
5. <span data-ttu-id="30def-132">按一下**安裝**toocomplete hello 安裝，並關閉此對話方塊。</span><span class="sxs-lookup"><span data-stu-id="30def-132">Click **Install** toocomplete hello installation, and then close this dialog.</span></span>

<span data-ttu-id="30def-133">SendGrid 的 .NET 類別庫稱為 **SendGrid**。</span><span class="sxs-lookup"><span data-stu-id="30def-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="30def-134">它包含下列命名空間的 hello:</span><span class="sxs-lookup"><span data-stu-id="30def-134">It contains hello following namespaces:</span></span>

* <span data-ttu-id="30def-135">**SendGrid** 用以與 SendGrid 的 API 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="30def-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="30def-136">**SendGrid.Helpers.Mail**協助程式方法 tooeasily 建立 SendGridMessage 物件，以指定 toosend 的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="30def-136">**SendGrid.Helpers.Mail** for helper methods tooeasily create SendGridMessage objects that specify how toosend emails.</span></span>

<span data-ttu-id="30def-137">新增下列程式碼命名空間宣告 toohello 上您想要在其中任何 C# 檔案 tooprogrammatically 存取 hello SendGrid 電子郵件服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="30def-137">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access hello SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="30def-138">如何：建立電子郵件</span><span class="sxs-lookup"><span data-stu-id="30def-138">How to: Create an Email</span></span>
<span data-ttu-id="30def-139">使用 hello **SendGridMessage**物件 toocreate 電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="30def-139">Use hello **SendGridMessage** object toocreate an email message.</span></span> <span data-ttu-id="30def-140">Hello 訊息物件建立之後，您可以設定屬性和方法，包括 hello 電子郵件寄件者、 hello 電子郵件收件者和 hello 主旨和本文 hello 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="30def-140">Once hello message object is created, you can set properties and methods, including hello email sender, hello email recipient, and hello subject and body of hello email.</span></span>

<span data-ttu-id="30def-141">hello 下列範例會示範如何 toocreate 完整擴展的電子郵件物件：</span><span class="sxs-lookup"><span data-stu-id="30def-141">hello following example demonstrates how toocreate a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing hello SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="30def-142">如需 **SendGrid** 類型支援的所有屬性和方法的詳細資訊，請參閱 GitHub 上的 [sendgrid-csharp][sendgrid-csharp]。</span><span class="sxs-lookup"><span data-stu-id="30def-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="30def-143">如何：傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="30def-143">How to: Send an Email</span></span>
<span data-ttu-id="30def-144">建立電子郵件訊息之後，您可以使用 SendGrid 的 API 進行傳送。</span><span class="sxs-lookup"><span data-stu-id="30def-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="30def-145">或者，您也可以使用 [.NET 的內建程式庫][NET-library]。</span><span class="sxs-lookup"><span data-stu-id="30def-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="30def-146">傳送電子郵件需要您提供 SendGrid API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="30def-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="30def-147">如果您需要詳細瞭解 tooconfigure API 金鑰，請瀏覽 SendGrid 的 API 金鑰[文件][documentation]。</span><span class="sxs-lookup"><span data-stu-id="30def-147">If you need details about how tooconfigure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="30def-148">您可能會儲存這些認證，透過 Azure 入口網站的 應用程式設定和 應用程式設定的新增 hello 索引鍵/值組。</span><span class="sxs-lookup"><span data-stu-id="30def-148">You may store these credentials via your Azure Portal by clicking Application settings and adding hello key/value pairs under App settings.</span></span>

 ![Azure 應用程式設定][azure_app_settings]

 <span data-ttu-id="30def-150">然後，您可以使用下列方式進行存取：</span><span class="sxs-lookup"><span data-stu-id="30def-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="30def-151">hello 遵循範例顯示如何使用 toosend hello Web API。</span><span class="sxs-lookup"><span data-stu-id="30def-151">hello following examples show how toosend a message using hello Web API.</span></span>

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
                    Subject = "Hello World from hello SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="30def-152">如何：新增附件</span><span class="sxs-lookup"><span data-stu-id="30def-152">How to: Add an attachment</span></span>
<span data-ttu-id="30def-153">附件可以加入 tooa 訊息呼叫 hello **AddAttachment**方法並使用最低限度指定 hello 檔案名稱和 Base64 編碼內容想 tooattach。</span><span class="sxs-lookup"><span data-stu-id="30def-153">Attachments can be added tooa message by calling hello **AddAttachment** method and minimally specifying hello file name and Base64 encoded content you want tooattach.</span></span> <span data-ttu-id="30def-154">您可以包含多個附件，藉由呼叫這個方法，一旦您想在每個檔案 tooattach 或使用 hello **AddAttachments**方法。</span><span class="sxs-lookup"><span data-stu-id="30def-154">You can include multiple attachments by calling this method once for each file you wish tooattach or by using hello **AddAttachments** method.</span></span> <span data-ttu-id="30def-155">hello 下列範例示範如何將附件 tooa 訊息：</span><span class="sxs-lookup"><span data-stu-id="30def-155">hello following example demonstrates adding an attachment tooa message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="30def-156">如何： 使用郵件設定 tooenable 頁尾、 追蹤和分析</span><span class="sxs-lookup"><span data-stu-id="30def-156">How to: Use mail settings tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="30def-157">SendGrid 提供其他電子郵件功能，透過 hello 使用郵件設定和追蹤設定。</span><span class="sxs-lookup"><span data-stu-id="30def-157">SendGrid provides additional email functionality through hello use of mail settings and tracking settings.</span></span> <span data-ttu-id="30def-158">這些設定可以加入 tooan 電子郵件訊息 tooenable 特定功能，例如點選追蹤、 Google analytics、 追蹤、 訂用帳戶和等等。</span><span class="sxs-lookup"><span data-stu-id="30def-158">These settings can be added tooan email message tooenable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="30def-159">如需完整的應用程式清單，請參閱 hello[設定文件集][settings-documentation]。</span><span class="sxs-lookup"><span data-stu-id="30def-159">For a full list of apps, see hello [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="30def-160">應用程式都可以套用太**SendGrid**電子郵件訊息的方式實作的 hello 一部分**SendGridMessage**類別。</span><span class="sxs-lookup"><span data-stu-id="30def-160">Apps can be applied too**SendGrid** email messages using methods implemented as part of hello **SendGridMessage** class.</span></span> <span data-ttu-id="30def-161">hello 下列範例示範 hello 頁尾，並按一下 追蹤篩選器：</span><span class="sxs-lookup"><span data-stu-id="30def-161">hello following examples demonstrate hello footer and click tracking filters:</span></span>

<span data-ttu-id="30def-162">hello 下列範例示範 hello 頁尾，並按一下 追蹤篩選器：</span><span class="sxs-lookup"><span data-stu-id="30def-162">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="30def-163">頁尾設定</span><span class="sxs-lookup"><span data-stu-id="30def-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="30def-164">點選追蹤</span><span class="sxs-lookup"><span data-stu-id="30def-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="30def-165">如何：使用其他 SendGrid 服務</span><span class="sxs-lookup"><span data-stu-id="30def-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="30def-166">SendGrid 提供數個應用程式開發介面和 webhook 您可以在 Azure 應用程式內使用 tooleverage 額外的功能。</span><span class="sxs-lookup"><span data-stu-id="30def-166">SendGrid offers several APIs and webhooks that you can use tooleverage additional functionality within your Azure application.</span></span> <span data-ttu-id="30def-167">如需詳細資訊，請參閱 hello [SendGrid API 參考][SendGrid API documentation]。</span><span class="sxs-lookup"><span data-stu-id="30def-167">For more details, see hello [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="30def-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30def-168">Next steps</span></span>
<span data-ttu-id="30def-169">既然您已經學會 hello 的 hello SendGrid 電子郵件服務的基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="30def-169">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="30def-170">SendGrid C\# 程式庫儲存機制：[sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="30def-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="30def-171">SendGrid API 文件︰<https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="30def-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is hello SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference hello SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters tooEnable Footers, Tracking, and Analytics]: #usefilters
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

[雲端架構電子郵件服務]: https://sendgrid.com/solutions
[交易式電子郵件傳遞]: https://sendgrid.com/use-cases/transactional-email

