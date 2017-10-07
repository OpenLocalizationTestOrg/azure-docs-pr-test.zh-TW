---
title: "aaaHow tooget AppSource 通過 Azure Active Directory |Microsoft 文件"
description: "上如何 tooget AppSource 應用程式通過 Azure Active Directory 的詳細資料。"
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a>如何為 Azure Active Directory 的 tooget AppSource 認證
[Microsoft AppSource](https://appsource.microsoft.com/)是目的地商務使用者 toodiscover，再試一次，以及管理 SaaS 應用程式的特定業務 （獨立 SaaS 和附加元件 tooexisting Microsoft SaaS 產品）。

toolist 獨立 AppSource 的 SaaS 應用程式，您的應用程式必須接受單一登入來自任何的公司或組織有 Azure Active Directory 的工作帳戶。 hello 登入程序必須使用 hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md)或[OAuth 2.0](./active-directory-protocols-oauth-code.md)通訊協定。 AppSource 認證不接受 SAML 整合。

## <a name="guides-and-code-samples"></a>指南與程式碼範例
如果您想 toolearn 關於如何 toointegrate 使用 Open ID 的 Azure Active Directory 的應用程式連接時，依照我們的指南和程式碼範例在 hello [Azure Active Directory 開發人員手冊 》](./active-directory-developers-guide.md#get-started "快速入門適用於開發人員的 azure AD")。

## <a name="multi-tenant-applications"></a>多租用戶應用程式

此應用程式接受來自具備 Azure Active Directory 之公司或組織的使用者的單一登入，不需要稱為*多租用戶應用程式*的個別執行個體、設定或部署。 AppSource 建議應用程式中實作多租用戶 tooenable hello*單鍵*免費的試用經驗。

在訂單 tooenable 多租用戶應用程式：
- 設定`Multi-Tenanted`屬性太`Yes`上您的應用程式登錄資訊中 hello [Azure 入口網站](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)(根據預設，在 hello Azure 入口網站中建立的應用程式設定為*單一租用戶*)
- 更新您的程式碼 toosend 要求 toohello '`common`' 端點 (更新 hello 端點從*https://login.microsoftonline.com/ {yourtenant}*太*https://login.microsoftonline.com/common*)
- 對於某些平台，像 ASP.NET，您也需要 tooupdate 程式碼 tooaccept 多個簽發者

如需多租用戶的詳細資訊，請參閱：[如何在任何 Azure Active Directory (AD) 使用者使用 toosign hello 多租用戶應用程式模式](./active-directory-devhowto-multi-tenant-overview.md)。

### <a name="single-tenant-applications"></a>單一租用戶應用程式
此應用程式僅接受來自定義之 Azure Active Directory 執行個體 (稱為*單一租用戶應用程式*) 的使用者登入。 外部使用者 （包括來自其他組織中，工作或學校帳戶或個人帳戶） 登入 tooa 單一租用戶應用程式之後，加入每個使用者為*guest 帳戶*toohello Azure Active Directory 執行個體hello 應用程式註冊。 您可以將使用者新增為來賓帳戶 tooan Azure Active Directory 透過 hello [ *Azure AD B2B 共同作業*](../active-directory-b2b-what-is-azure-ad-b2b.md)位，且可完成[以程式設計方式控制程式](../active-directory-b2b-code-samples.md)。 當您將使用者新增為來賓帳戶 tooan Azure Active Directory 時，邀請電子郵件傳送 toohello，具有使用者 tooaccept hello 邀請 hello 邀請電子郵件中的 hello 連結上按一下。 邀請傳送 tooan 額外的使用者，同時也是 hello 夥伴組織的成員邀請組織中是不必要的 tooaccept 中的邀請 toosign。

單一租用戶應用程式可以啟用 hello*與我連絡*體驗，但如果您想 tooenable hello 單鍵 / 免費的試用經驗 AppSource 建議時，啟用您的應用程式上的多租用戶改為。


## <a name="appsource-trial-experiences"></a>AppSource 試用體驗

### <a name="free-trial-customer-led-trial-experience"></a>免費試用 (以客戶為導向的試用體驗) 
hello*客戶導致試用*AppSource 建議，因為提供的單鍵存取 tooyour 應用程式的 hello 體驗。 這項體驗看起來如下圖：<br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li>使用者會在 AppSource 網站中尋找您的應用程式</li><li>選取 [免費試用] 選項</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li>AppSource 重新導向使用者 tooa URL 在您的網站</li><li>您的網站啟動 hello<i>單一登入</i>自動 （在頁面載入） 處理序</li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li>使用者已重新導向的 tooMicrosoft 登入頁面</li><li>使用者提供認證 toosign 中</li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li>使用者同意您的應用程式</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>登入完成，而且使用者為重新導向後 tooyour 網站</li><li>使用者啟動 hello 免費試用版</li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a>與我連絡 (以合作夥伴為導向的試用體驗)
hello*夥伴的試用經驗*可用時手動 」 或 「 長期作業需要 toohappen tooprovision hello 使用者 / 公司： 例如，您的應用程式需要 tooprovision 虛擬機器資料庫執行個體，或花太多時間 toocomplete 的作業。 在此情況下之後使用者選取 hello,*要求試用*按鈕，然後填寫表單，AppSource 傳送 hello 使用者的連絡資訊。 在收到這項資訊，然後佈建 hello 環境並傳送 hello 指示 toohello 使用者如何 tooaccess hello 的試用經驗：<br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li>使用者會在 AppSource 網站中尋找您的應用程式</li><li>選取 [與我連絡] 選項</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li>將連絡人資訊填入表單</li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td>您會收到使用者資訊</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td>設定環境</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td>連絡使用者試用資訊</td>
        </tr>
        </table><br/><br/>
        <ul><li>您收到使用者資訊並設定試用執行個體</li><li>您傳送嗨超連結 tooaccess toohello 應用程式的使用者</li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li>使用者存取您的應用程式和單一登入程序完成 hello</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li>使用者同意您的應用程式</li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>登入完成，而且使用者為重新導向後 tooyour 網站</li><li>使用者啟動 hello 免費試用版</li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a>詳細資訊
如需 hello AppSource 試用體驗的詳細資訊，請參閱[這段影片](https://aka.ms/trialexperienceforwebapps)。 
 
## <a name="next-steps"></a>後續步驟

- 如需建立支援 Azure Active Directory 登入之應用程式的詳細資訊，請參閱 [Azure AD 的驗證案例](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) 

- 如需有關如何 toolist SaaS 應用程式中 AppSource，請查看詳細[AppSource 合作夥伴資訊](https://appsource.microsoft.com/partners)


## <a name="get-support"></a>取得支援
Azure Active Directory 整合，我們使用[堆疊溢位](http://stackoverflow.com/questions/tagged/azure-active-directory)與 hello 社群 tooprovide 支援。 

我們強烈建議您先詢問您的問題的堆疊溢位，並瀏覽現有問題 toosee，如果其他人已提出您的問題之前。 請確定您的問題或意見已標記為 `[azure-active-directory]`。

使用下列註解區段 tooprovide 意見反應的 hello，並協助我們改善並圖形內容。

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->