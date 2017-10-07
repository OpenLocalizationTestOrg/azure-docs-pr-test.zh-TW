---
title: "aaaHow toomake 通話從 Twilio (.NET) |Microsoft 文件"
description: "了解如何 toomake 電話及傳送 SMS 訊息 hello Twilio API 服務在 Azure 上。 程式碼範例以 .NET 撰寫。"
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
ms.openlocfilehash: 857d89961c563a51fef944f4a72828036af79b43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a>如何 toomake 電話呼叫在 Azure 上的 web 角色中使用 Twilio
本指南示範如何 toouse Twilio toomake 從網頁呼叫裝載在 Azure 中。 hello 產生應用程式會提示 hello 使用者 toomake 呼叫以指定數字與訊息、 hello hello 下列螢幕擷取畫面所示。

![Azure call form using Twilio and ASP.NET][twilio_dotnet_basic_form]

## <a name="twilio-prereqs"></a>必要條件
您將需要 toodo hello 下列 toouse 本主題中的 hello 程式碼：

1. 取得 Twilio 帳戶和驗證權杖從 hello [Twilio 主控台][twilio_console]。 tooget 啟動與 Twilio，符號在[https://www.twilio.com/try-twilio][try_twilio]。 您可以在 [http://www.twilio.com/pricing][twilio_pricing] 上評估價格。 Hello Twilio 所提供的 API 的相關資訊，請參閱[http://www.twilio.com/voice/api][twilio_api]。
2. 新增 hello *Twilio.NET 程式庫*tooyour web 角色。 請參閱**tooadd hello Twilio 文件庫 tooyour web 角色專案**稍後在本主題中。

您應知悉如何[在 Azure 上建立基本 Web 角色][azure_webroles_get_started]。

## <a name="howtocreateform"></a>作法：建立用以撥打電話的 Web 表單
<a id="use_nuget"></a>tooadd hello Twilio 文件庫 tooyour web 角色專案：

1. 在 Visual Studio 中開啟方案。
2. 以滑鼠右鍵按一下 [參考] 。
3. 按一下 [管理 NuGet 封裝] 。
4. 按一下 [線上] 。
5. 在 hello 搜尋線上方塊中，輸入*twilio*。
6. 按一下**安裝**hello Twilio 封裝上。

下列程式碼的 hello 顯示 toocreate web 表單 tooretrieve 進行呼叫的使用者資料的方式。 在此範例中，會建立名為 **TwilioCloud** 的 ASP.NET Web 角色。

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

## <a id="howtocreatecode"></a>如何： 建立 hello 程式碼 toomake hello 呼叫
hello 下列程式碼會呼叫 hello 使用者完成 hello 表單時，會建立 hello 呼叫訊息並產生 hello 呼叫。 在此範例中，hello 程式碼會執行 hello onclick 按鈕事件處理常式 hello hello 表單上。 (使用您的 Twilio 帳戶和驗證語彙基元而非 hello 預留位置值太指派`accountSID`和`authToken`hello 的下列程式碼。)

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
            // hello placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of hello Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve hello account, used later tooretrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve hello values entered by hello user.
                var too= PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using hello Twilio message and hello user-entered
                // text. You must replace spaces in hello user's text with '%20'
                // toomake hello text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display hello endpoint, API version, and hello URL for hello message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"hello URL is {url}");

                // Place hello call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

hello 呼叫，並會顯示 hello Twilio 端點、 應用程式開發介面版本和 hello 呼叫狀態。 hello 的範例，執行下列螢幕擷取畫面顯示輸出。

![Azure call response using Twilio and ASP.NET][twilio_dotnet_basic_form_output]

如需 TwiML 的相關資訊，請參閱 [http://www.twilio.com/docs/api/twiml][twiml]。 如需 &lt;Say&gt; 和其他 Twilio 動詞的詳細資訊，請參閱 [http://www.twilio.com/docs/api/twiml/say][twilio_say]。

## <a id="nextsteps"></a>接續步驟
此程式碼提供 tooshow 您基本的功能使用 Twilio 中 ASP.NET web 角色在 Azure 上。 在部署之前 tooAzure 在生產環境中的，您可能想要 tooadd 詳細的錯誤處理或其他功能。 例如：

* 而不是使用網頁表單，您無法使用 Azure Blob 儲存體或 Azure SQL Database 執行個體 toostore 電話號碼，並呼叫的文字。 如需使用 Blob 在 Azure 中的資訊，請參閱[toouse hello.net 的 Azure Blob 儲存體服務的方式][howto_blob_storage_dotnet]。 如需使用 SQL Database 的資訊，請參閱[toouse Azure SQL 資料庫中的.NET 應用程式][howto_sql_azure_dotnet]。
* 您可以使用`RoleEnvironment.getConfigurationSettings`tooretrieve hello Twilio 帳戶識別碼和驗證語彙基元從您的部署組態設定，而不是硬式編碼您的表單中的 hello 值。 如需 hello`RoleEnvironment`類別，請參閱[Microsoft.WindowsAzure.ServiceRuntime 命名空間][azure_runtime_ref_dotnet]。
* 讀取 hello Twilio 安全性指導方針，在[https://www.twilio.com/docs/security][twilio_docs_security]。
* 在 [https://www.twilio.com/docs][twilio_docs] 上深入了解 Twilio。

## <a name="seealso"></a>另請參閱
* [如何從 Azure 的語音和簡訊功能 toouse Twilio](twilio-dotnet-how-to-use-for-voice-sms.md)

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
