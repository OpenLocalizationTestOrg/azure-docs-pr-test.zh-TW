---
title: "aaaMFA 軟體開發套件的自訂應用程式 |Microsoft 文件"
description: "本文章將示範如何 toodownload 並用 hello Azure MFA SDK tooenable 雙步驟驗證，您的自訂應用程式。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a>在自訂應用程式中建置 Multi-Factor Authentication (SDK)

hello Azure Multi-factor Authentication 軟體開發套件 (SDK) 可讓您建置兩步驟驗證直接內建 hello 登入或交易程序的 Azure AD 租用戶中的應用程式。

hello Multi-factor Authentication SDK 適用於 C#、 Visual Basic (.NET)、 Java、 Perl、 PHP 和 Ruby。 hello SDK 提供了雙步驟驗證的精簡型包裝函式。 它包含所需的所有 toowrite 您的程式碼，包括加註的原始程式碼檔案、 範例檔案，以及詳細的 ReadMe 檔案。 每一套 SDK 也包含憑證和私密金鑰的加密是唯一 tooyour Multi-factor Authentication 提供者的交易。 只要您有的提供者，您就可以視需要下載 hello SDK 為多種語言和格式。

hello Api hello Multi-factor Authentication SDK 中的 hello 結構很簡單。 請呼叫 tooan API （例如驗證模式） 的 hello 多因素選項參數與使用者資料 （例如 hello 電話號碼 toocall 或 hello 的 PIN 號碼 toovalidate） 的單一函式。 hello Api 轉譯 hello 函式呼叫 web 服務要求 toohello 雲端型 Azure Multi-factor Authentication 服務。 所有呼叫必須都包含參考 toohello 私用憑證包含在每個 SDK 中。

因為 hello 應用程式開發介面不需要存取 toousers Azure Active Directory 中登錄，您必須提供檔案或資料庫中的使用者資訊。 此外，hello 應用程式開發介面不會提供註冊或使用者管理功能，因此您需要 toobuild 這些應用程式的處理程序。

> [!IMPORTANT]
> toodownload hello SDK，您需要 toocreate Azure Multi-factor Auth 提供者，即使您的 Azure MFA、 AAD Premium 或 EMS 授權數量。 如果您針對此用途建立 Azure Multi-factor Auth 提供者，並已經有授權，請確定 toocreate hello 提供者以 hello**每個已啟用的使用者**模型。 然後，連結 hello 包含 hello Azure MFA、 Azure AD Premium 或 EMS 授權提供者 toohello 目錄。 此組態可確保，您才需要付費如果您有多個唯一的使用者使用 hello SDK 比 hello 您所擁有的授權數目。


## <a name="download-hello-sdk"></a>下載 SDK hello
下載 Azure Multi-factor Authentication SDK hello 需要[Azure 多因素驗證提供者](multi-factor-authentication-get-started-auth-provider.md)。  即使您擁有 Azure MFA、Azure AD Premium 或 Enterprise Mobility Suite 授權，這還是需要完整的 Azure 訂用帳戶。  toodownload hello SDK，瀏覽 toohello Multi-factor Authentication 管理入口網站。 您可能會達到 hello 入口網站管理 hello 直接，Multi-factor Auth 提供者，或按一下 hello **「 Go toohello 入口網站 」** hello MFA 服務設定 頁面上的連結。

### <a name="download-from-hello-azure-classic-portal"></a>從 hello Azure 傳統入口網站下載
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)身為系統管理員。
2. Hello 左側選取**Active Directory**。
3. 在 hello Active Directory 頁面上，在 hello 頂端選取**Multi-factor Auth 提供者**
4. Hello 底部選取**管理**。 新的頁面隨即開啟。
5. 按一下左，請在 hello 下方的 hello **SDK**。
   <center>![下載](./media/multi-factor-authentication-sdk/download.png)</center>
6. 選取 hello 語言，然後按一下一個 hello 相關的下載連結。
7. Hello 下載檔案的儲存。

### <a name="download-from-hello-service-settings"></a>下載從 hello 服務設定
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)身為系統管理員。
2. Hello 左側選取**Active Directory**。
3. 按兩下您的 Azure AD 執行個體。
4. 在 hello 頂端按一下**設定**
5. 在多因素驗證底下選取 **管理服務設定**
   ![下載](./media/multi-factor-authentication-sdk/download2.png)
6. 在 hello 服務設定 頁面上，在 hello 囉 」 畫面底部按一下**Go toohello 入口網站**。 新的頁面隨即開啟。
   ![下載](./media/multi-factor-authentication-sdk/download3a.png)
7. 按一下左，請在 hello 下方的 hello **SDK**。
8. 選取 hello 語言，然後按一下一個 hello 相關的下載連結。
9. Hello 下載檔案的儲存。

## <a name="whats-in-hello-sdk"></a>功能的 hello SDK
hello SDK 包含下列項目 hello:

* **讀我檔案**。 說明如何 toouse hello 新的或現有的應用程式中的多因素驗證應用程式開發介面。
* **原始程式檔**，用於 Multi-Factor Authentication
* **用戶端憑證**toocommunicate 使用 hello Multi-factor Authentication 服務
* **私用金鑰**hello 憑證
* **呼叫結果。** 呼叫結果碼的清單。 tooopen 此檔案，請使用文字格式，例如 WordPad 應用程式使用。 使用 hello 呼叫結果碼 tootest，並進行疑難排解的多因素驗證應用程式中的 hello 實作。 它們不是驗證狀態碼。
* **範例。** Multi-Factor Authentication 基本工作實作的範例程式碼。

> [!WARNING]
> hello 用戶端憑證是特別為您產生的唯一私密憑證。 請勿分享或遺失此檔案。 是金鑰 tooensuring hello 與 hello Multi-factor Authentication 服務通訊的安全性。

## <a name="code-sample"></a>程式碼範例
這個程式碼範例會示範如何在 Azure Multi-factor Authentication SDK tooadd 標準模式語音 hello toouse hello 應用程式開發介面呼叫驗證 tooyour 應用程式。 標準模式是 hello 使用者回應 tooby 按 hello # 鍵將電話通話。

這個範例會使用基本的 ASP.NET 應用程式中的 hello C#.NET 2.0 Multi-factor Authentication SDK 與 C# 伺服器端邏輯，但 hello 流程類似其他語言中。 因為 hello SDK 包含來源檔案，不是可執行檔，您可以建置 hello 檔案和參考它們或直接在您的應用程式中包含它們。

> [!NOTE]
> 當實作多因素驗證時，使用 hello 其他方法 （通話或簡訊） 重音或第三驗證 toosupplement 為您的主要驗證方法 （使用者名稱和密碼）。 這些方法並非設計為主要驗證方法。

### <a name="code-sample-overview"></a>程式碼範例概觀
這個簡單的 web 示範應用程式的範例程式碼會使用 # 金鑰回應 tooverify hello 使用者的驗證電話通話。 此通話因素在 Multi-Factor Authentication 中稱為標準模式。

hello 用戶端程式碼不包含任何 Multi-factor Authentication 特定元素。 由於 hello 額外驗證因素與 hello 主要驗證無關，所以您可以將它們而不必變更 hello 現有登入介面。 hello Multi-factor SDK 中的 hello 應用程式開發介面可讓您自訂 hello 使用者經驗，但是您可能不需要 toochange 任何項目完全。

hello 伺服器端程式碼會加入在步驟 2 中的標準模式驗證。 它會建立具有所需的標準模式驗證的 hello 參數 PfAuthParams 物件： 使用者名稱、 電話號碼和模式，及 hello 路徑 toohello 用戶端憑證 (CertFilePath)，每個呼叫所需要的。 PfAuthParams 中的所有參數的示範，請參閱 hello SDK 中的 hello 範例檔案。

接下來，hello 程式碼會傳遞 hello PfAuthParams 物件 toohello pf_authenticate() 函式。 hello 傳回值會指出 hello 成功或失敗的 hello 驗證。 out 參數、 callStatus 和 errorID hello、 包含其他通話結果資訊。 hello 通話結果碼會記錄在 hello SDK 中的 hello 通話結果檔案。

只需要幾行就能撰寫這個最小實作。 不過，在實際執行的程式碼中，將會包含更複雜的錯誤處理、其他資料庫程式碼和強化的使用者經驗。

### <a name="web-client-code"></a>Web 用戶端程式碼
hello 以下是示範頁面的 web 用戶端程式碼。

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a>伺服器端程式碼
在下列伺服器端程式碼的 hello，會多因素驗證設定，並在步驟 2 中執行。 標準模式 (MODE_STANDARD) 是電話 toowhich hello 使用者回應 hello # 鍵。

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
