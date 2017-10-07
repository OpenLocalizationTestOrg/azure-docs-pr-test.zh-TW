---
title: "aaaGet 開始使用 Azure Active Directory 識別身分保護，Microsoft Graph |Microsoft 文件"
description: "提供簡介 tooquery Microsoft Graph 從 Azure Active Directory 的風險事件和相關聯的資訊清單。"
services: active-directory
keywords: "azure active directory identity protection, 風險事件, 弱點, 安全性原則, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a>開始使用 Azure Active Directory Identity Protection 和 Microsoft Graph
Microsoft Graph 是 Microsoft 統一的 API 端點的 hello 與家庭的 hello [Azure Active Directory 識別身分保護](active-directory-identityprotection.md)應用程式開發介面。 hello 第一個應用程式開發介面， **identityRiskEvents**，可讓您 tooquery Microsoft Graph 清單的[風險事件](active-directory-identityprotection-risk-events-types.md)和相關聯的資訊。 本文可協助您開始查詢此 API。 深入了解簡介、 完整的文件，與存取 toohello 圖表總管，請參閱 hello [Microsoft Graph 網站](https://graph.microsoft.io/)。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。

有三個步驟 tooaccessing 識別身分保護資料，Microsoft Graph 透過：

1. 新增應用程式與用戶端密碼。 
2. 使用此密碼和其他一些資訊 tooauthenticate tooMicrosoft 圖形中，您在何處接收驗證 token 片段。 
3. 使用這個語彙基元 toomake 要求 toohello API 端點，並回到識別身分保護資料。

開始之前，您需要下列項目：

* 系統管理員權限 toocreate hello 應用程式在 Azure AD 中
* 您的租用戶網域 (例如 contoso.onmicrosoft.com) hello 名稱

## <a name="add-an-application-with-a-client-secret"></a>新增應用程式與用戶端密碼
1. [登入](https://manage.windowsazure.com)tooyour 身為系統管理員的 Azure 傳統入口網站。 
2. 在 hello 左側瀏覽窗格中，按一下  **Active Directory**。 
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
4. 在 hello 最上層顯示 hello 功能表上，按一下**應用程式**。
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. 按一下**新增**hello hello 頁底端。
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. 在 [hello**您該怎麼想 toodo** ] 對話方塊中，按一下**加入我組織正在開發的應用程式**。
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. 在 [hello**告訴我們您的應用程式**] 對話方塊中，執行下列步驟的 hello:
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    a. 在 hello**名稱**文字方塊中，輸入您的應用程式的名稱 (例如： AADIP 風險事件 API 應用程式)。
   
    b. 在 [類型]，選取 [Web 應用程式和/或 Web API]。
   
    c. 按一下 [下一步] 。
8. 在 [hello**應用程式屬性**] 對話方塊中，執行下列步驟的 hello:
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    a. 在 hello**登入 URL**文字方塊中，輸入`http://localhost`。
   
    b. 在 hello**應用程式識別碼 URI**文字方塊中，輸入`http://localhost`。
   
    c. 按一下頁面底部的 [新增] 。

現在您可以設定您的應用程式了。

![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a>授與您的應用程式的權限 toouse hello 應用程式開發介面
1. 在您的應用程式頁面上，hello hello 上方的功能表中按一下**設定**。 
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. 在 hello**權限 tooother 應用程式**區段中，按一下**新增應用程式**。
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. 在 [hello**權限 tooother 應用程式**] 對話方塊中，執行下列步驟的 hello:
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    a. 選取 [Microsoft Graph]。
   
    b. 按一下頁面底部的 [新增] 。
4. 按一下 [應用程式權限: 0]，然後選取 [讀取所有身分識別風險事件資訊]。
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. 按一下**儲存**hello hello 頁底端。
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a>取得存取金鑰
1. 在您的應用程式 頁面的 hello**金鑰**區段中，選取持續時間為 1 年。
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. 按一下**儲存**hello hello 頁底端。
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. 在 hello 金鑰 > 一節，複製 hello 您新建立的金鑰值並貼到安全的位置。
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > 如果遺失此機碼，您將有 tooreturn toothis 區段，並建立新的金鑰。 請勿將此金鑰告知他人︰任何人只要擁有此金鑰就可以存取您的資料。
   > 
   > 
4. 在 hello**屬性**區段，複製 hello**用戶端識別碼**，然後將它貼到安全的位置。 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a>驗證 tooMicrosoft 圖形和查詢 hello 識別風險事件 API
到目前為止，您應該已擁有︰

* 複製上述的 hello 用戶端識別碼
* 複製上述的 hello 金鑰
* hello 租用戶的網域名稱

tooauthenticate，傳送 post 要求太`https://login.microsoft.com`以 hello 遵循 hello 主體中的參數：

* grant_type: “**client_credentials**”
* resource: “**https://graph.microsoft.com**”
* client_id: <your client ID>
* client_secret: <your key>

> [!NOTE]
> 您需要 tooprovide 值 hello **client_id**和 hello **client_secret**參數。
> 
> 

如果成功，這會傳回驗證權杖。  
toocall hello 應用程式開發介面，建立 hello 參數後面的標頭：

    `Authorization`=”<token_type> <access_token>"


驗證時，您可以在 hello 傳回權杖中找到 hello 語彙基元類型及存取語彙基元。

以下列 API URL 要求 toohello 中傳送此標頭：`https://graph.microsoft.com/beta/identityRiskEvents`

hello 回應，如果成功，風險的事件所識別的集合與相關聯的 hello OData JSON 格式，但可以剖析和處理可視中的資料。

以下是驗證和呼叫 hello 應用程式開發介面使用 Powershell 的範例程式碼。  
您只需要加入用戶端識別碼、金鑰和租用戶網域。

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a>後續步驟
恭喜，您剛建立的第一個呼叫 tooMicrosoft 圖形 ！  
現在您可以查詢識別風險事件，並使用 hello 資料，不過您看到符合。

深入了解 Microsoft Graph toolearn 及 toobuild 應用程式使用方式 hello Graph API，請參閱 hello[文件](https://graph.microsoft.io/docs)及其他更多在 hello [Microsoft Graph 網站](https://graph.microsoft.io/)。 此外，也請確定 toobookmark hello [Azure AD Identity Protection 應用程式開發介面](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)hello 識別保護 Api 可在圖表中的所有列出的頁面。 當我們新增識別身分保護透過 API 使用的新方式 toowork，您會在該頁面上看到它們。

## <a name="additional-resources"></a>其他資源
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)
* [Azure Active Directory Identity Protection 偵測到的風險事件類型](active-directory-identityprotection-risk-events-types.md)
* [Microsoft Graph](https://graph.microsoft.io/)
* [Microsoft Graph 概觀](https://graph.microsoft.io/docs)
* [Azure AD Identity Protection 服務根目錄](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

