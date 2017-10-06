---
title: "自訂︰Azure AD SSPR | Microsoft Docs"
description: "Azure AD 自助式密碼重設的自訂選項"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4762fffef040f9b409355f9ee0e8cc593e3eea0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a>自訂 Azure AD 的自助式密碼重設功能

IT 專業人員尋找 toodeploy 自助式密碼重設可以自訂 hello 經驗 toomatch 他們的使用者。

## <a name="customize-hello-contact-your-administrator-link"></a>自訂 hello，請連絡您的系統管理員連結

即使 SSPR 不是啟用的使用者仍 「 連絡您的系統管理員 」 連結 hello 密碼重設入口網站。  按一下此連結以電子郵件傳送您的系統管理員請求協助變更 hello 使用者的密碼。 這封電子郵件會傳送 toohello 遵循 hello 順序中的收件者：

1. 如果 hello**密碼管理員**角色指派，請與此角色的系統管理員通知
2. 如果沒有密碼管理員指派，然後系統管理員以 hello**使用者系統管理員**角色會收到通知
3. 如果任一 hello 先前兩個角色指派，然後**全域管理員**會收到通知

在所有情況下，最多 100 位收件者會收到通知。

深入了解 hello 不同的系統管理員角色，以及如何加以查看的 tooassign hello 文件 toofind[指派 Azure Active Directory 中的系統管理員角色](active-directory-assign-admin-roles.md)

### <a name="disable-contact-your-administrator-emails"></a>停用「連絡您的系統管理員」電子郵件

如果您的組織不想收到有關密碼的通知的系統管理員重設要求，hello 下列組態可啟用

* 對所有使用者啟用自助式密碼重設。 此選項位於 [密碼重設] > [屬性] 下。
    * 如果您不想使用者 tooreset 自己的密碼，您可以為範圍存取 tooan 空群組**我們不建議您使用這個選項**。
* 自訂 hello 服務台連結 tooprovide web URL 或 mailto： 使用者可以使用 tooget 協助的位址。 此選項位於 [密碼重設] > [自訂] > [自訂的技術服務人員電子郵件或 URL] 下。

## <a name="customize-adfs-sign-in-page-for-sspr"></a>為 SSPR 自訂 ADFS 登入頁面

ADFS 系統管理員可以新增連結 tootheir 登入頁面在 hello 文章中找到的 hello 指引[新增登入頁面描述](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description)。

使用接在 ADFS 伺服器的 hello 命令加上允許使用者 tooenter hello 自助式密碼重設工作流程的直接連結 toohello ADFS 登入頁面。

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a>自訂 hello 登入及存取面板的外觀及操作

當您的使用者存取 hello 登入頁面時，您可以自訂 hello 標誌出現 hello 登入頁面影像 toofit 以及公司商標。

這些圖形會顯示在下列情況下的 hello:

* 使用者輸入其使用者名稱之後
* 使用者存取自訂的 url
    * 由傳送嗨"whr"參數 toohello 密碼重設頁面上，像是 「 https://login.microsoftonline.com/?whr=contoso.com"
    * 由傳送嗨"username"參數 toohello 重設密碼] 頁面上，例如"https://login.microsoftonline.com/?username=admin@contoso.com"

### <a name="graphics-details"></a>圖形的詳細資料

hello 下列設定 toochange hello 視覺特性 hello 登入頁面可讓您和您可以找到**Azure Active Directory**，**公司商標**，**編輯公司商標**

* 登入頁面影像應該是 PNG 或 JPG 檔案 1420x1200 像素，不能大於 500KB。 我們建議 toobe 約 200 KB 為了獲得最佳結果。
* 登入頁面背景色彩時高延遲的連接上使用，而且必須以 hello RGB 十六進位格式。
* 橫幅影像應該是 PNG 或 JPG 檔案 60x280 像素，不能大於 10 KB。
* 正方形標誌 (一般和深色佈景主題) PNG 或 JPG 240x240 (可調整大小)，不能大於 10 KB。

### <a name="sign-in-text-options"></a>登入文字選項

hello 下列設定可讓您 tooadd 文字 toohello 登入頁面相關 tooyour 組織。 您可以在 [Azure Active Directory]、[公司商標]、[編輯公司商標] 下找到這些設定

* **使用者名稱提示**取代 hello 範例文字someone@example.com一些較適合您的使用者，使用時，建議使用 toobe 左的預設支援的內部和外部使用者
* [登入頁面文字] 的長度最多 256 個字元。 任何位置，連線，且在 hello Windows 10 上體驗 Azure AD Join，此文字會出現您的使用者登入。 使用此文字作為給使用者的使用條款、指示和提示。 **任何人都可以看到您的登入頁面，請勿在此處提供任何機密資訊。**

### <a name="keep-me-signed-in-disabled"></a>已停用 [讓我保持登入]

hello 選項 「 讓我保持登入已停用 」 可讓使用者 tooremain 關閉並重新開啟其瀏覽器視窗時，登入。 這個選項不會影響工作階段存留期。 您可以在 [Azure Active Directory] > [公司商標] > [編輯公司商標] 下找到此設定。

SharePoint Online 和 Office 2010 的某些功能會有相依性的使用者可以 toocheck 此方塊。 如果您隱藏此選項時，使用者可能會收到其他非預期的登入提示。

### <a name="directory-name"></a>目錄名稱

您可以變更下的 hello name 屬性**Azure Active Directory > 屬性**tooshow 易記的組織名稱出現在 hello 入口網站，且自動化的通訊。 這個選項是最明顯 hello hello 表單，請依照下列中的自動化電子郵件格式

* 「Microsoft 代表 CONTOSO 示範」電子郵件中的易記名稱
* 「CONTOSO 示範帳戶電子郵件驗證碼」電子郵件的主旨列

## <a name="next-steps"></a>後續步驟

hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊

* [**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理 
* [**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權
* [**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理
* [**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱
* [**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則
* [**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何使用您的內部部署目錄
* [**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能
* [**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式
* [**常見問題集**](active-directory-passwords-faq.md) - 如何？ 原因為何？ 何事？ 何地？ 何人？ 何時？ -回答您總是想 tooask tooquestions
* [**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR

