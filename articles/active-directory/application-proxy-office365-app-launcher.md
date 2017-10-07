---
title: "aaaSet 自訂的首頁上，使用 Azure AD Application Proxy 發行應用程式 |Microsoft 文件"
description: "涵蓋有關 Azure AD 應用程式 Proxy 連接器 hello 基本概念"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>使用 Azure AD 應用程式 Proxy 為發佈的應用程式設定自訂首頁

本文將討論如何 tooconfigure 應用程式 toodirect 使用者 tooa 自訂的首頁。 當您發行應用程式 Proxy 的應用程式時，設定內部 URL，但有時候，可能會不 hello 頁面，您的使用者應該會看到第一次。 設定自訂的首頁，讓您的使用者會從 Azure Active Directory 存取面板 hello 或 hello Office 365 應用程式啟動器存取 hello 應用程式時，請移 toohello 右頁。

當使用者啟動 hello 應用程式時，系統正在指示由預設 toohello 根網域 URL hello 發行的應用程式。 hello 登陸頁面通常設定為 hello 首頁 URL。 當您想要應用程式使用者 tooland hello 應用程式內的特定頁面上，請使用 hello Azure AD PowerShell 模組 toodefine 自訂的首頁 Url。 

例如：
- 您的公司網路內部使用者前往太*https://ExpenseApp/login/login.aspx* toosign 中的並存取您的應用程式。
- 因為您有其他資產，如同應用程式 Proxy 需要 tooaccess 在 hello hello 資料夾結構的高層級的影像，您發行 hello 應用程式與*https://ExpenseApp*為 hello 內部 URL。
- hello 的預設外部 URL 是*https://ExpenseApp-contoso.msappproxy.net*，而不需要您的使用者 toohello 登頁面中。  
- 設定*https://ExpenseApp-contoso.msappproxy.net/login/login.aspx*為 hello 首頁 URL toogive 使用者順暢的體驗。 

>[!NOTE]
>當您授與使用者存取 toopublished 應用程式時，hello 應用程式會顯示在 hello [Azure AD 存取面板](active-directory-saas-access-panel-introduction.md)和 hello [Office 365 應用程式啟動器](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher)。

## <a name="before-you-start"></a>開始之前

設定 hello 首頁 URL 之前，請注意下列需求的 hello:

* 請確定您指定的 hello 路徑是子網域的 hello 根網域的 URL 路徑。

  如果 hello 根網域的 URL，例如 https://apps.contoso.com/app1/，您所設定的 hello 首頁 URL 開頭必須 https://apps.contoso.com/app1/。

* 如果您變更 toohello 發佈應用程式時，hello 變更可能會重設 hello hello 首頁 URL 值。 當您更新在未來的 hello hello 應用程式時，您應該重新檢查，然後必要時，更新 hello 首頁 URL。

## <a name="change-hello-home-page-in-hello-azure-portal"></a>變更 hello Azure 入口網站中的 hello 首頁

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。
2. 瀏覽過**Azure Active Directory** > **應用程式註冊**和從 hello 清單中選擇您的應用程式。 
3. 選取**屬性**hello 設定。
4. 更新 hello**首頁 URL**欄位與新的路徑。 

   ![提供新的首頁 URL](./media/application-proxy-office365-app-launcher/homepage.png)

5. 選取 [儲存]。

## <a name="change-hello-home-page-with-powershell"></a>使用 PowerShell 變更 hello 首頁

### <a name="install-hello-azure-ad-powershell-module"></a>安裝 hello Azure AD PowerShell 模組

您使用 PowerShell 來定義自訂的首頁 URL 之前，先安裝 hello Azure AD PowerShell 模組。 您可以從 hello 下載 hello 封裝[PowerShell 資源庫](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131)，它會使用 hello Graph API 端點。 

tooinstall hello 封裝，請遵循下列步驟：

1. 開啟標準的 PowerShell 視窗，並執行下列命令的 hello:

    ```
     Install-Module -Name AzureAD
    ```
    如果您以非系統管理員執行 hello 命令，請使用 hello`-scope currentuser`選項。
2. Hello 安裝期間選取**Y** tooinstall 兩從 Nuget.org 的封裝。兩個套件都是必要套件。 

### <a name="find-hello-objectid-of-hello-app"></a>Hello ObjectID hello 應用程式中尋找

取得 hello ObjectID hello 應用程式，，然後搜尋 hello 應用程式的首頁。

1. 開啟 PowerShell 並匯入 hello Azure AD 模組。

    ```
    Import-Module AzureAD
    ```

2. 以登入 toohello Azure AD 模組 hello 租用戶系統管理員。

    ```
    Connect-AzureAD
    ```
3. 尋找 hello 應用程式依據首頁 URL。 您可以在 hello 入口網站中找到 hello URL 太移**Azure Active Directory** > **企業應用程式** > **所有應用程式**。 這個範例會使用 sharepoint-iddemo。

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. 您應該取得結果，其會類似 toohello 一個如下所示。 複製 hello ObjectID GUID toouse hello 下一節。

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a>更新 hello 首頁 URL

在 hello 為步驟 1 所用的同一個 PowerShell 模組中執行下列步驟的 hello:

1. 確認您擁有 hello 更正應用程式，並取代*8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4*以 hello hello 前面步驟中複製的 ObjectID。

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 現在您已確認 hello 應用程式，您已準備好 tooupdate hello 首頁上，，如下所示。

2. 建立空白的應用程式物件 toohold 想 toomake hello 變更。 這個變數會保存您想 tooupdate hello 值。 此步驟不會建立任何項目。

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. 設定 hello 首頁 URL toohello 您想要的值。 hello 值必須是子網域 hello 已發行應用程式的路徑。 例如，如果您變更 hello 首頁 URL 從*https://sharepoint-iddemo.msappproxy.net/*太*https://sharepoint-iddemo.msappproxy.net/hybrid/*，應用程式的使用者而直接前往 toohello 自訂首頁。

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. 請使用 hello GUID (ObjectID) 中複製 hello 更新 」 步驟 1： 尋找 hello hello 應用程式的 ObjectID。 」

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. tooconfirm hello 變更已成功，重新啟動 hello 應用程式。

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>您讓 toohello 應用程式的任何變更可能會重設 hello 首頁 URL。 如果您的首頁 URL 重設，請重複步驟 2。

## <a name="next-steps"></a>後續步驟

- [啟用與 Azure AD Application Proxy 的遠端存取 tooSharePoint](application-proxy-enable-remote-access-sharepoint.md)
- [在 hello Azure 入口網站中啟用應用程式 Proxy](active-directory-application-proxy-enable.md)
