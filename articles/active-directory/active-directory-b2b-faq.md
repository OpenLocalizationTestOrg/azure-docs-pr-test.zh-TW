---
title: "aaaAzure Active Directory B2B 共同作業常見問題集 |Microsoft 文件"
description: "取得 Azure Active Directory B2B 共同作業相關常見問題的解答 toofrequently。"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 4412bbc65274ff01782db81dfcc8818a6362ea7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>Azure Active Directory B2B 共同作業常見問題集

這些常見問題集 (Faq) 有關 Azure Active Directory (Azure AD) 的企業對企業 (B2B) 共同作業會定期更新的 tooinclude 新主題。

### <a name="is-azure-ad-b2b-collaboration-available-in-hello-azure-classic-portal"></a>位於 Azure AD B2B 共同作業 hello Azure 傳統入口網站？
否。 Azure AD B2B 共同作業功能都只 hello [Azure 入口網站](https://portal.azure.com)在 hello[存取面板](https://myapps.microsoft.com/)。 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>我們是否可以自訂登入頁面，讓我們的 B2B 共同作業來賓使用者感到更直覺式？
當然！ 請參閱我們[有關這項功能的部落格文章](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/)。 如需有關如何 toocustomize 您組織的登入頁面上，請參閱[新增公司品牌 toosign 中的和存取面板頁面](active-directory-add-company-branding.md)。

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>B2B 共同作業的使用者可以存取 SharePoint Online 和 OneDrive 嗎？
是。 不過，在 SharePoint Online 中現有的 guest 使用者，使用 hello 人員選擇器的 hello 能力 toosearch 是**關閉**預設。 在現有的 guest 使用者的 hello 選項 toosearch tooturn 設定**ShowPeoplePickerSuggestionsForGuestUsers**太**上**。 您可以在 hello 租用戶層級，或在 hello 網站集合層級開啟此設定。 您可以使用 hello 組 SPOTenant 和集 SPOSite cmdlet 來變更此設定。 使用這些 cmdlet，成員可以在 hello 目錄中搜尋所有現有的來賓使用者。 Hello 租用戶範圍中的變更不會影響已佈建的 SharePoint Online 網站。

### <a name="is-hello-csv-upload-feature-still-supported"></a>為的 hello CSV 上傳功能仍然受到支援？
是。 如需使用 hello.csv 檔案上傳功能的詳細資訊，請參閱[這個 PowerShell 範例](active-directory-b2b-code-samples.md)。

### <a name="how-can-i-customize-my-invitation-emails"></a>如何自訂我的邀請電子郵件？
您可以使用來自訂幾乎所有項目 hello 邀請者程序 hello [B2B 邀請 Api](active-directory-b2b-api.md)。

### <a name="can-an-invited-external-user-leave-hello-organization-after-being-invited"></a>受邀的外部使用者可以保留之後受邀的 hello 組織嗎？
hello 邀請組織系統管理員可以從他們的目錄中，刪除 B2B 共同作業 guest 使用者，但 hello guest 使用者不能讓 hello 邀請組織目錄本身。 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>來賓使用者是否可以重設其多重要素驗證方法？
是。 Guest 使用者可以重設的相同方式的一般使用者執行其多重要素驗證方法 hello。

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>哪個組織負責多重要素驗證授權？
hello 邀請組織執行多因素驗證。 hello 邀請組織必須確定 hello 組織有足夠的授權 B2B 使用者正在使用多因素驗證。

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>如果夥伴組織已設定多重要素驗證呢？ 我們可以信任其多重要素驗證，而不要使用我們自己的多重要素驗證嗎？
這樣，則您可以選取特定夥伴 tooexclude （hello 邀請組織） 的多因素驗證，這項功能已規劃未來的版本。

### <a name="how-can-i-use-delayed-invitations"></a>我如何使用延遲的邀請？
組織可能會想 tooadd B2B 共同作業的使用者佈建 tooapplications 如有需要，然後傳送邀請。 您可以使用 hello B2B 共同作業邀請 API toocustomize hello 登入工作流程。

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>我是否可以將來賓使用者設為受限的管理員？
當然。 如需詳細資訊，請參閱[新增來賓使用者 tooa 角色](active-directory-users-assign-role-azure-portal.md)。

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-tooaccess-hello-azure-portal"></a>Azure AD B2B 共同作業是否允許 B2B 使用者 tooaccess hello Azure 入口網站？
除非使用者獲指派 hello 有限的系統管理員或全域管理員角色，B2B 共同作業的使用者不需要存取 toohello Azure 入口網站。 不過，B2B 共同作業指派的使用者 hello 有限的系統管理員或全域管理員角色可以存取 hello 入口網站。 此外，如果未指派其中一個系統管理員角色的 guest 使用者存取 hello 入口網站，hello 使用者可能無法 tooaccess 的某些部分 hello 體驗。 hello 來賓使用者角色具有 hello 目錄中的某些權限。

### <a name="can-i-block-access-toohello-azure-portal-for-guest-users"></a>我可以封鎖存取 toohello guest 使用者的 Azure 入口網站嗎？
可以！ 當您設定此原則時，是小心 tooavoid 意外封鎖存取 toomembers 和系統管理員 」。
tooblock guest 使用者的存取 toohello [Azure 入口網站](https://portal.azure.com)，在 [hello Windows Azure 傳統部署模型 API 中使用條件式存取原則：
1. 修改 hello**所有使用者**分組，讓它只包含成員。
  ![修改 hello 群組螢幕擷取畫面](media/active-directory-b2b-faq/modify-all-users-group.png)
2. 建立包含來賓使用者的動態群組。
  ![建立群組螢幕擷取畫面](media/active-directory-b2b-faq/group-with-guest-users.png)
3. 設定條件式存取原則 tooblock guest 使用者存取 hello 入口網站中所示 hello 下列視訊：
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>Azure AD B2B 共同作業是否支援多重要素驗證和取用者電子郵件帳戶？
是。 Azure AD B2B 共同作業支援多重要素驗證和取用者電子郵件帳戶。

### <a name="do-you-plan-toosupport-password-reset-for-azure-ad-b2b-collaboration-users"></a>您是否計劃 toosupport 使用者密碼重設 Azure AD B2B 共同作業？
是。 以下是 hello 邀請來自夥伴組織的 B2B 使用者的自助式密碼重設 (SSPR) 的重要詳細資料：
 
* SSPR 只會發生在 hello 的 hello B2B 使用者的身分識別租用戶。
* 如果 hello 識別租用戶是 Microsoft 帳戶，則會使用 hello SSPR 機制的 Microsoft 帳戶。
* 如果 hello 識別租用戶會在 just-in-time (JIT) 或 「 病毒式"租用戶，會傳送密碼重設電子郵件。
* 為其他租用戶 hello 標準 SSPR 程序會遵循 B2B 使用者。 例如 member SSPR B2B 中的使用者，hello 內容 hello 資源的租用戶會遭到封鎖。 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>在 Just-In-Time (JIT) 或「病毒式」租用戶中，以工作或學校電子郵件地址接受邀請，但沒有既存 Azure AD 帳戶的來賓使用者，可以使用密碼重設嗎？
是。 可讓使用者 tooreset 密碼 hello JIT 租用戶中可以傳送密碼重設郵件。

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>Microsoft Dynamics CRM 是否提供 Azure AD B2B 共同作業的線上支援？
目前，Microsoft Dynamics CRM 不提供 Azure AD B2B 共同作業的線上支援。 不過，我們計劃 toosupport 這在未來的 hello。

### <a name="what-is-hello-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>新建立的 B2B 共同作業使用者的初始密碼 hello 存留期為何？
Azure AD 有一組固定的字元、 密碼強度和同樣適 tooall Azure AD 雲端使用者帳戶的帳戶鎖定需求。 雲端使用者帳戶是不與其他身分識別提供者聯盟的帳戶，例如 
* Microsoft 帳戶
* Facebook
* Active Directory Federation Services
* 其他雲端租用戶 (適用於 B2B 共同作業)

針對同盟帳戶密碼原則必須倚賴套用 hello 內部租用戶和 hello 使用者的 Microsoft 帳戶設定中的 hello 原則。

### <a name="an-organization-might-want-toohave-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-hello-presence-of-hello-identity-provider-claim-hello-correct-model-toouse"></a>組織可能會想 toohave 不同體驗的租用戶使用者和 guest 使用者其應用程式。 有適用於此案例的標準指引嗎？ 是 hello 身分識別提供者宣告 hello 正確的模型 toouse hello 存在嗎？
 Guest 使用者可以使用任何身分識別提供者 tooauthenticate。 如需詳細資訊，請參閱 [B2B 共同作業使用者的屬性](active-directory-b2b-user-properties.md)。 使用 hello **UserType**屬性 toodetermine 使用者經驗。 hello **UserType**宣告目前未包含在 hello 語彙基元。 應用程式應使用 hello Graph API tooquery hello 目錄 hello 使用者及 tooget hello UserType。

### <a name="where-can-i-find-a-b2b-collaboration-community-tooshare-solutions-and-toosubmit-ideas"></a>可以在哪裡找到 B2B 共同作業社群 tooshare 解決方案和 toosubmit 想法？
我們會持續不斷地聽取 tooyour 意見反應，tooimprove B2B 共同作業。 我們邀請您 tooshare 您的使用者案例，最佳作法，以及您對 Azure AD B2B 共同作業的喜歡。 聯結 hello hello 討論[Microsoft 技術社群](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b)。
 
我們也邀請您 toosubmit 您的想法和未來的功能投票[B2B 共同作業想法](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas)。

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-hello-user-is-just-ready-toogo-or-does-hello-user-always-have-tooclick-through-toohello-redemption-url"></a>我們可以傳送的邀請自動贖回票證，因此，hello 使用者是 [只"準備 toogo"嗎？ 或者 hello 使用者永遠有 tooclick 透過 toohello 兌換 URL？
Hello 邀請組織內也是成員的 hello 夥伴組織中的使用者所傳送的邀請不需要由 hello B2B 使用者贖回。

我們建議您邀請 hello 夥伴組織 toojoin hello 邀請組織從一位使用者。 [Hello 資源組織中新增此使用者 toohello 來賓邀請者角色](active-directory-b2b-add-guest-to-role.md)。 此使用者可以邀請 hello 夥伴組織中的其他使用者使用 hello 登入 UI，PowerShell 指令碼，或應用程式開發介面。 然後，B2B 共同作業的使用者從該組織不需要的 tooredeem 其邀請。

### <a name="how-does-b2b-collaboration-work-when-hello-invited-partner-is-using-federation-tooadd-their-own-on-premises-authentication"></a>B2B 共同作業的運作方式時受邀的 hello 夥伴使用同盟 tooadd 他們自己的內部部署驗證？
如果 hello 夥伴具有同盟的 Azure AD 租用戶 toohello 內部驗證基礎結構，在內部部署單一登入 (SSO) 會自動在達成。 如果 hello 夥伴沒有 Azure AD 租用戶，Azure AD 帳戶會建立新的使用者。 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>我以為 Azure AD B2B 不接受 gmail.com 和 outlook.com 電子郵件地址，而 B2C 用於這些類型的帳戶？
我們會移除 B2B 和商務層公司 (B2C) 共同作業方面的身分識別支援的 hello 差異。 使用 hello 身分識別不充分的理由 toochoose b2b 或使用 B2C 之間。 如需有關選擇協同作業選項的資訊，請參閱[比較 Azure Active Directory 的 B2B 共同作業和 B2C](active-directory-b2b-compare-b2c.md)。

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>哪些應用程式和服務支援 Azure B2B 來賓使用者？
Azure AD 整合的所有應用程式都支援 Azure B2B 來賓使用者。 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>如果我們的合作夥伴沒有多重要素驗證，我們是否可以對 B2B 來賓使用者強制使用多重要素驗證？
是。 如需詳細資訊，請參閱 [B2B 共同作業使用者的條件式存取](active-directory-b2b-mfa-instructions.md)。

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>在 SharePoint 中，您可以針對外部使用者定義「允許」或「拒絕」清單。 這在 Azure 中辦得到嗎？
是。 Azure AD B2B 共同作業支援允許清單和拒絕清單。 

### <a name="what-licenses-do-we-need-toouse-azure-ad-b2b"></a>授權做什麼我們需要 Azure AD B2B toouse 嗎？
如資訊什麼授權您的組織需要 toouse Azure AD B2B，請參閱 <<c0> [ 授權指引的 Azure Active Directory B2B 共同作業](active-directory-b2b-licensing.md)。

### <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure AD 管理員如何新增 B2B 共同作業使用者？](active-directory-b2b-admin-add-users.md)
* [資訊工作者如何新增 B2B 共同作業使用者？](active-directory-b2b-iw-add-users.md)
* [hello hello B2B 共同作業邀請電子郵件項目](active-directory-b2b-invitation-email.md)
* [B2B 共同作業邀請兌換](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 共同作業授權](active-directory-b2b-licensing.md)
* [針對 Azure AD B2B 共同作業進行疑難排解](active-directory-b2b-troubleshooting.md)
* [Azure AD B2B 共同作業 API 和自訂](active-directory-b2b-api.md)
* [適用於 B2B 共同作業使用者的多重要素驗證](active-directory-b2b-mfa-instructions.md)
* [在沒有邀請的情況下新增 B2B 共同作業使用者](active-directory-b2b-add-user-without-invite.md)
* [Azure AD 中應用程式管理的文章索引](active-directory-apps-index.md)
