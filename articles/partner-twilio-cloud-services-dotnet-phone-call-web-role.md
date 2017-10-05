---
title: "如何從 Twilio 撥打電話 (.NET) | Microsoft Docs"
description: "了解如何在 Azure 上使用 Twilio API 服務撥打電話及傳送簡訊。 程式碼範例以 .NET 撰寫。"
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 0899a49cbfda775017dab7fc6d8963bbeb86d74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="68fcc-104">如何在 Azure 上的 Web 角色中使用 Twilio 撥打電話</span><span class="sxs-lookup"><span data-stu-id="68fcc-104">How to make a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="68fcc-105">本指南將說明如何從 Azure 代管的網頁上使用 Twilio 撥打電話。</span><span class="sxs-lookup"><span data-stu-id="68fcc-105">This guide demonstrates how to use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="68fcc-106">產生的應用程式會提示使用者利用指定的號碼和訊息撥打電話，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="68fcc-106">The resulting application prompts the user to make a call with the given number and message, as shown in the following screenshot.</span></span>

![Azure call form using Twilio and ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="68fcc-108"><a name="twilio-prereqs"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="68fcc-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="68fcc-109">您必須執行下列動作才能使用本主題中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="68fcc-109">You will need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="68fcc-110">從 [Twilio 主控台][twilio_console]取得 Twilio 帳戶和驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="68fcc-110">Acquire a Twilio account and authentication token from the [Twilio Console][twilio_console].</span></span> <span data-ttu-id="68fcc-111">若要開始使用 Twilio，請在 [https://www.twilio.com/try-twilio][try_twilio] 上註冊。</span><span class="sxs-lookup"><span data-stu-id="68fcc-111">To get started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="68fcc-112">您可以在 [http://www.twilio.com/pricing][twilio_pricing] 上評估價格。</span><span class="sxs-lookup"><span data-stu-id="68fcc-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="68fcc-113">如需 Twilio 所提供之 API 的相關資訊，請參閱 [http://www.twilio.com/voice/api][twilio_api]。</span><span class="sxs-lookup"><span data-stu-id="68fcc-113">For information about the API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="68fcc-114">將「Twilio .NET 程式庫」新增至您的 Web 角色。</span><span class="sxs-lookup"><span data-stu-id="68fcc-114">Add the *Twilio .NET libary* to your web role.</span></span> <span data-ttu-id="68fcc-115">請參閱本主題稍後的「將 Twilio 程式庫新增至 Web 角色專案」。</span><span class="sxs-lookup"><span data-stu-id="68fcc-115">See **To add the Twilio libraries to your web role project**, later in this topic.</span></span>

<span data-ttu-id="68fcc-116">您應知悉如何[在 Azure 上建立基本 Web 角色][azure_webroles_get_started]。</span><span class="sxs-lookup"><span data-stu-id="68fcc-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="68fcc-117"><a name="howtocreateform"></a>作法：建立用以撥打電話的 Web 表單</span><span class="sxs-lookup"><span data-stu-id="68fcc-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="68fcc-118"><a id="use_nuget"></a>將 Twilio 程式庫新增至 Web 角色專案：</span><span class="sxs-lookup"><span data-stu-id="68fcc-118"><a id="use_nuget"></a>To add the Twilio libraries to your web role project:</span></span>

1. <span data-ttu-id="68fcc-119">在 Visual Studio 中開啟方案。</span><span class="sxs-lookup"><span data-stu-id="68fcc-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="68fcc-120">以滑鼠右鍵按一下 [參考] 。</span><span class="sxs-lookup"><span data-stu-id="68fcc-120">Right-click **References**.</span></span>
3. <span data-ttu-id="68fcc-121">按一下 [管理 NuGet 封裝] 。</span><span class="sxs-lookup"><span data-stu-id="68fcc-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="68fcc-122">按一下 [線上] 。</span><span class="sxs-lookup"><span data-stu-id="68fcc-122">Click **Online**.</span></span>
5. <span data-ttu-id="68fcc-123">在搜尋線上方塊中，輸入 twilio。</span><span class="sxs-lookup"><span data-stu-id="68fcc-123">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="68fcc-124">在 Twilio 套件上按一下 [安裝]  。</span><span class="sxs-lookup"><span data-stu-id="68fcc-124">Click **Install** on the Twilio package.</span></span>

<span data-ttu-id="68fcc-125">下列程式碼將說明如何建立 Web 表單，以擷取撥打電話所需的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="68fcc-125">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="68fcc-126">在此範例中，會建立名為 **TwilioCloud** 的 ASP.NET Web 角色。</span><span class="sxs-lookup"><span data-stu-id="68fcc-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <span data-ttu-id="68fcc-127"><a id="howtocreatecode"></a>作法：建立用以撥打電話的程式碼</span><span class="sxs-lookup"><span data-stu-id="68fcc-127"><a id="howtocreatecode"></a>How to: Create the code to make the call</span></span>
<span data-ttu-id="68fcc-128">下列程式碼會在使用者完成表單時受到呼叫，可用來建立通話訊息及產生通話。</span><span class="sxs-lookup"><span data-stu-id="68fcc-128">The following code, which is called when the user completes the form, creates the call message and generates the call.</span></span> <span data-ttu-id="68fcc-129">在此範例中，程式碼會在表單按鈕的 onclick 事件處理常式中執行。</span><span class="sxs-lookup"><span data-stu-id="68fcc-129">In this example, the code is run in the onclick event handler of the button on the form.</span></span> <span data-ttu-id="68fcc-130">(在下方的程式碼中，請使用您的 Twilio 帳戶和驗證權杖，而不要使用指派給 `accountSID` 和 `authToken` 的預留位置值。)</span><span class="sxs-lookup"><span data-stu-id="68fcc-130">(Use your Twilio account and authentication token instead of the placeholder values assigned to `accountSID` and `authToken` in the code below.)</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // the placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of the Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve the account, used later to retrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve the values entered by the user.
                var to = PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using the Twilio message and the user-entered
                // text. You must replace spaces in the user's text with '%20'
                // to make the text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display the endpoint, API version, and the URL for the message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"The URL is {url}");

                // Place the call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="68fcc-131">通話建立後，會顯示 Twilio 端點、API 版本和通話狀態。</span><span class="sxs-lookup"><span data-stu-id="68fcc-131">The call is made, and the Twilio endpoint, API version, and the call status are displayed.</span></span> <span data-ttu-id="68fcc-132">下列螢幕擷取畫面顯示執行範例的輸出。</span><span class="sxs-lookup"><span data-stu-id="68fcc-132">The following screenshot shows output from a sample run.</span></span>

![Azure call response using Twilio and ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="68fcc-134">如需 TwiML 的相關資訊，請參閱 [http://www.twilio.com/docs/api/twiml][twiml]。</span><span class="sxs-lookup"><span data-stu-id="68fcc-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="68fcc-135">如需 &lt;Say&gt; 和其他 Twilio 動詞的詳細資訊，請參閱 [http://www.twilio.com/docs/api/twiml/say][twilio_say]。</span><span class="sxs-lookup"><span data-stu-id="68fcc-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="68fcc-136"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="68fcc-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="68fcc-137">此程式可說明在 Azure 上的 ASP.NET Web 角色中使用 Twilio 的基本功能。</span><span class="sxs-lookup"><span data-stu-id="68fcc-137">This code was provided to show you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="68fcc-138">在部署至生產環境中的 Azure 之前，您可以新增更多錯誤處理或其他功能。</span><span class="sxs-lookup"><span data-stu-id="68fcc-138">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="68fcc-139">例如：</span><span class="sxs-lookup"><span data-stu-id="68fcc-139">For example:</span></span>

* <span data-ttu-id="68fcc-140">除了使用 Web 表單以外，您也可以使用 Azure Blob 儲存體或 Azure SQL Database 執行個體來儲存電話號碼和通話文字。</span><span class="sxs-lookup"><span data-stu-id="68fcc-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance to store phone numbers and call text.</span></span> <span data-ttu-id="68fcc-141">如需在 Azure 中使用 Blob 的相關資訊，請參閱[如何在 .NET 中使用 Azure Blob 儲存體服務][howto_blob_storage_dotnet]。</span><span class="sxs-lookup"><span data-stu-id="68fcc-141">For information about using Blobs in Azure, see [How to use the Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="68fcc-142">如需使用 SQL Database 的相關資訊，請參閱[如何在 .NET 應用程式中使用 Azure SQL Database][howto_sql_azure_dotnet]。</span><span class="sxs-lookup"><span data-stu-id="68fcc-142">For information about using SQL Database, see [How to use Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="68fcc-143">您可以使用 `RoleEnvironment.getConfigurationSettings`，從部署的組態設定中擷取 Twilio 帳戶 ID 和驗證權杖，而不要在表單中進行值的硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="68fcc-143">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in your form.</span></span> <span data-ttu-id="68fcc-144">如需 `RoleEnvironment` 類別的相關資訊，請參閱 [Microsoft.WindowsAzure.ServiceRuntime 命名空間][azure_runtime_ref_dotnet]。</span><span class="sxs-lookup"><span data-stu-id="68fcc-144">For information about the `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="68fcc-145">閱讀 [https://www.twilio.com/docs/security][twilio_docs_security] 上的 Twilio 安全性指引。</span><span class="sxs-lookup"><span data-stu-id="68fcc-145">Read the Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="68fcc-146">在 [https://www.twilio.com/docs][twilio_docs] 上深入了解 Twilio。</span><span class="sxs-lookup"><span data-stu-id="68fcc-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="68fcc-147"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="68fcc-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="68fcc-148">如何透過 Twilio 來使用 Azure 的語音和簡訊功能</span><span class="sxs-lookup"><span data-stu-id="68fcc-148">How to use Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
