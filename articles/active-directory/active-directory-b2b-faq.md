---
title: "Azure Active Directory B2B 共同作業常見問題集 | Microsoft Docs"
description: "取得 Azure Active Directory B2B 共同作業常見問題集的解答"
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
ms.openlocfilehash: bfedbbf8b26e1b129584a6a644e64a15635f5723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>Azure Active Directory B2B 共同作業常見問題集

這些有關 Azure Active Directory (Azure AD) 企業對企業 (B2B) 共同作業的常見問題集 (FAQ) 會定期更新來包含新的主題。

### <a name="is-azure-ad-b2b-collaboration-available-in-the-azure-classic-portal"></a>Azure 傳統入口網站中是否可以使用 Azure AD B2B 共同作業？
否。 只有在 [Azure 入口網站](https://portal.azure.com)和[存取面板](https://myapps.microsoft.com/)中才可以使用 Azure AD B2B 共同作業功能。 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>我們是否可以自訂登入頁面，讓我們的 B2B 共同作業來賓使用者感到更直覺式？
當然！ 請參閱我們[有關這項功能的部落格文章](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/)。 如需有關如何自訂組織登入頁面的詳細資訊，請參閱[將公司商標新增至登入和存取面板頁面](active-directory-add-company-branding.md)。

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>B2B 共同作業的使用者可以存取 SharePoint Online 和 OneDrive 嗎？
是。 不過，在 SharePoint Online 中使用人員選擇器搜尋現有來賓使用者的功能，預設為**關閉**。 若要開啟搜尋現有來賓使用者的選項，請將 **ShowPeoplePickerSuggestionsForGuestUsers** 設定為 **On**。 您可以在租用戶等級或網站集合等級開啟這項設定。 您可以使用 Set-SPOTenant 和 Set-SPOSite Cmdlet 變更此設定。 透過這些 Cmdlet，成員可以搜尋目錄中所有現有的來賓使用者。 租用戶範圍中的變更不會影響已佈建的 SharePoint Online 網站。

### <a name="is-the-csv-upload-feature-still-supported"></a>是否仍支援 CSV 上傳功能？
是。 如需有關使用 .csv 檔案上傳功能的詳細資訊，請參閱[這個 PowerShell 範例](active-directory-b2b-code-samples.md)。

### <a name="how-can-i-customize-my-invitation-emails"></a>如何自訂我的邀請電子郵件？
您可以使用 [B2B 邀請 API](active-directory-b2b-api.md) 自訂關於邀請者程序的幾乎一切事項。

### <a name="can-an-invited-external-user-leave-the-organization-after-being-invited"></a>受邀的外部使用者是否可以在受邀之後離開組織？
邀請組織的系統管理員，可從他們的目錄中刪除 B2B 共同作業來賓使用者，但來賓使用者不能自行離開邀請的組織目錄。 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>來賓使用者是否可以重設其多重要素驗證方法？
是。 來賓使用者集可以重設其多重要素驗證方法，作法與一般使用者一樣。

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>哪個組織負責多重要素驗證授權？
邀請方組織執行多重要素驗證。 邀請方組織必須確定組織有足夠的授權給使用多重要素驗證的 B2B 使用者。

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>如果夥伴組織已設定多重要素驗證呢？ 我們可以信任其多重要素驗證，而不要使用我們自己的多重要素驗證嗎？
此功能是為未來的版本預備，屆時您將能夠選取特定協力廠商，從您的 (邀請方組織的) 多重要素驗證中排除。

### <a name="how-can-i-use-delayed-invitations"></a>我如何使用延遲的邀請？
組織可能想要新增 B2B 共同作業使用者，依需要將他們佈建至應用程式，然後送出邀請。 您可以使用 B2B 共同作業邀請 API 自訂登入工作流程。

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>我是否可以將來賓使用者設為受限的管理員？
當然。 如需詳細資訊，請參閱[將來賓使用者新增至角色](active-directory-users-assign-role-azure-portal.md)。

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-to-access-the-azure-portal"></a>Azure AD B2B 共同作業是否允許 B2B 使用者存取 Azure 入口網站？
除非使用者獲指派受限的管理員或全域管理員角色，B2B 共同作業使用者不需要存取 Azure 入口網站。 不過，獲指派受限的管理員或全域管理員角色的 B2B 共同作業使用者可以存取入口網站。 此外，如果未獲指派其中一個管理員角色的來賓使用者存取入口網站，使用者可能可以存取特定部份的體驗。 來賓使用者角色在目錄中具有某些權限。

### <a name="can-i-block-access-to-the-azure-portal-for-guest-users"></a>我可以封鎖來賓使用者存取 Azure 入口網站嗎？
可以！ 當您設定此原則時，請小心避免不慎封鎖成員和管理員的存取權。
若要封鎖來賓使用者的 [Azure 入口網站](https://portal.azure.com)存取權，請在 Windows Azure 傳統部署模型 API 中使用條件式存取原則︰
1. 將**所有使用者**群組修改為只包含成員。
  ![修改群組螢幕擷取畫面](media/active-directory-b2b-faq/modify-all-users-group.png)
2. 建立包含來賓使用者的動態群組。
  ![建立群組螢幕擷取畫面](media/active-directory-b2b-faq/group-with-guest-users.png)
3. 設定條件式存取原則以防止來賓使用者存取入口網站，如下列影片中所示：
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>Azure AD B2B 共同作業是否支援多重要素驗證和取用者電子郵件帳戶？
是。 Azure AD B2B 共同作業支援多重要素驗證和取用者電子郵件帳戶。

### <a name="do-you-plan-to-support-password-reset-for-azure-ad-b2b-collaboration-users"></a>您是否打算支援 Azure AD B2B 共同作業使用者的密碼重設？
是。 以下是受到夥伴組織邀請之 B2B 使用者自助式密碼重設 (SSPR) 的重要詳細資料：
 
* SSPR 只會在 B2B 使用者的身分識別租用戶中發生。
* 如果身分識別租用戶是 Microsoft 帳戶，就會使用 Microsoft 帳戶 SSPR 機制。
* 如果身分識別租用戶是及時 (JIT) 或病毒式租用戶，則會傳送密碼重設電子郵件。
* 如果是其他租用戶，則會對 B2B 使用者採用標準 SSPR 程序。 就像 B2B 使用者的成員 SSPR，在資源方面也會封鎖租用。 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>在 Just-In-Time (JIT) 或「病毒式」租用戶中，以工作或學校電子郵件地址接受邀請，但沒有既存 Azure AD 帳戶的來賓使用者，可以使用密碼重設嗎？
是。 會傳送密碼重設郵件，讓使用者重設其 JIT 租用密碼。

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>Microsoft Dynamics CRM 是否提供 Azure AD B2B 共同作業的線上支援？
目前，Microsoft Dynamics CRM 不提供 Azure AD B2B 共同作業的線上支援。 不過，我們計劃在未來支援此功能。

### <a name="what-is-the-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>什麼是新建立的 B2B 共同作業使用者之初始密碼存留期？
Azure AD 有一組固定的字元、密碼強度，以及帳戶鎖定需求，可同樣適用於所有 Azure AD 雲端使用者帳戶。 雲端使用者帳戶是不與其他身分識別提供者聯盟的帳戶，例如 
* Microsoft 帳戶
* Facebook
* Active Directory Federation Services
* 其他雲端租用戶 (適用於 B2B 共同作業)

針對同盟帳戶，密碼原則取決於內部部署租用中套用的原則，以及使用者的 Microsoft 帳戶設定。

### <a name="an-organization-might-want-to-have-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-the-presence-of-the-identity-provider-claim-the-correct-model-to-use"></a>組織可能想要在其應用程式中讓租用戶使用者和來賓使用者有不同的體驗。 有適用於此案例的標準指引嗎？ 識別提供者宣告的存在是否為應使用的正確模型？
 來賓使用者可以使用任何識別提供者進行驗證。 如需詳細資訊，請參閱 [B2B 共同作業使用者的屬性](active-directory-b2b-user-properties.md)。 使用 **UserType** 屬性來決定使用者體驗。 權杖中目前不包含 **UserType** 宣告。 應用程式應該使用圖形 API 來查詢目錄中的使用者及取得 UserType。

### <a name="where-can-i-find-a-b2b-collaboration-community-to-share-solutions-and-to-submit-ideas"></a>哪裡可以找到 B2B 共同作業社群，以分享解決方案和提交構想？
我們會時常聆聽您對改進 B2B 共同作業的意見反應。 我們邀請您分享您的使用者案例、最佳做法，以及您喜歡 Azure AD B2B 共同作業的什麼功能。 請前往 [Microsoft 技術社群](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b)參與討論。
 
我們也邀請您前往 [B2B 共同作業構想](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas)提交您的構想和票選未來的功能。

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-the-user-is-just-ready-to-go-or-does-the-user-always-have-to-click-through-to-the-redemption-url"></a>我們是否可以傳送自動兌換的邀請，讓使用者「隨時出發」？ 還是使用者一定要按一下才能前往兌換 URL？
如果是由邀請方組織中的使用者傳送邀請，而此使用者也是夥伴組織的成員，B2B 使用者就不需要兌換該邀請。

建議您從夥伴組織中邀請一位使用者加入邀請方組織。 [將這個使用者新增至資源組織中的來賓邀請者角色](active-directory-b2b-add-guest-to-role.md)。 這位使用者可以使用登入 UI、PowerShell 指令碼或 API，邀請夥伴組織中的其他使用者。 然後，來自該組織的 B2B 共同作業使用者就不需要兌換他們的邀請。

### <a name="how-does-b2b-collaboration-work-when-the-invited-partner-is-using-federation-to-add-their-own-on-premises-authentication"></a>當受邀的合作夥伴使用同盟來新增自己的內部部署驗證時，B2B 共同作業如何運作？
如果合作夥伴具有與內部部署驗證基礎結構同盟的 Azure AD 租用戶，就會自動達成內部部署單一登入 (SSO)。 如果合作夥伴沒有 Azure AD 租用戶，則系統會為新的使用者建立 Azure AD 帳戶。 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>我以為 Azure AD B2B 不接受 gmail.com 和 outlook.com 電子郵件地址，而 B2C 用於這些類型的帳戶？
在支援哪些身分識別這方面，我們正在消除 B2B 和商務對公司 (B2C) 共同作業之間的差異。 使用的身分識別並不是選擇使用 B2B 或 B2C 時的一個好理由。 如需有關選擇協同作業選項的資訊，請參閱[比較 Azure Active Directory 的 B2B 共同作業和 B2C](active-directory-b2b-compare-b2c.md)。

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>哪些應用程式和服務支援 Azure B2B 來賓使用者？
Azure AD 整合的所有應用程式都支援 Azure B2B 來賓使用者。 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>如果我們的合作夥伴沒有多重要素驗證，我們是否可以對 B2B 來賓使用者強制使用多重要素驗證？
是。 如需詳細資訊，請參閱 [B2B 共同作業使用者的條件式存取](active-directory-b2b-mfa-instructions.md)。

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>在 SharePoint 中，您可以針對外部使用者定義「允許」或「拒絕」清單。 這在 Azure 中辦得到嗎？
是。 Azure AD B2B 共同作業支援允許清單和拒絕清單。 

### <a name="what-licenses-do-we-need-to-use-azure-ad-b2b"></a>我們需要哪些使用權才能使用 Azure AD B2B？
如需您的組織需要哪些授權才能使用 Azure AD B2B 的相關資訊，請參閱 [Azure Active Directory B2B 共同作業授權指引](active-directory-b2b-licensing.md)。

### <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure AD 管理員如何新增 B2B 共同作業使用者？](active-directory-b2b-admin-add-users.md)
* [資訊工作者如何新增 B2B 共同作業使用者？](active-directory-b2b-iw-add-users.md)
* [B2B 共同作業邀請電子郵件的元素](active-directory-b2b-invitation-email.md)
* [B2B 共同作業邀請兌換](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 共同作業授權](active-directory-b2b-licensing.md)
* [針對 Azure AD B2B 共同作業進行疑難排解](active-directory-b2b-troubleshooting.md)
* [Azure AD B2B 共同作業 API 和自訂](active-directory-b2b-api.md)
* [適用於 B2B 共同作業使用者的多重要素驗證](active-directory-b2b-mfa-instructions.md)
* [在沒有邀請的情況下新增 B2B 共同作業使用者](active-directory-b2b-add-user-without-invite.md)
* [Azure AD 中應用程式管理的文章索引](active-directory-apps-index.md)
