---
title: "在 Azure Active Directory aaaAssigning 系統管理員角色 |Microsoft 文件"
description: "系統管理員角色可以使用的 toocreate 或編輯使用者、 指派管理角色、 重設使用者密碼、 管理使用者授權或管理的網域。 指派系統管理員角色的使用者具有 hello 跨組織已訂閱的所有雲端服務 toowhich 相同的權限。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7fc27e8e-b55f-4194-9b8f-2e95705fb731
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.reviewer: Vince.Smith
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: b96350c7264e6ad3620272e015ed9756b512dc4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assigning-administrator-roles-in-azure-active-directory"></a>在 Azure Active Directory 中指派系統管理員角色
> [!div class="op_single_selector"]
> * [Azure 入口網站]()
> * [Azure 傳統入口網站](active-directory-assign-admin-roles.md)
>
>

使用 Azure Active Directory (Azure AD) toodesignate 不同系統管理員針對不同的函式。 這些系統管理員可以存取 hello Azure 入口網站或 Azure 傳統入口網站中，並根據其角色選取的功能，將會無法 toocreate 或編輯使用者、 指派系統管理角色 tooothers、 重設使用者密碼、 管理使用者授權和管理網域，以及其他項目。 指派系統管理員角色的使用者將會在所有您組織已訂閱，無論是否指派 hello 角色在 hello Office 365 入口網站，或在 hello Azure 傳統入口網站，或使用 hello 雲端服務 toowhich hello 相同的權限適用於 Microsoft PowerShell hello Azure AD 模組。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 如何置 tooassign hello Azure AD 系統管理員中的系統管理員角色，請參閱[指派 Azure Active Directory 中的系統管理員角色](active-directory-assign-admin-roles-azure-portal.md)。


下列系統管理員角色的 hello 可用：

* **計費管理員**：進行採購、管理訂用帳戶、管理支援票證，以及監控服務健全狀況。

* **相容性管理員**： 具有此角色的使用者具有在 hello Office 365 安全性與相容性中心 Exchange 系統管理中心內的管理權限。 如需詳細資訊，請參閱[關於 Office 365 管理員角色](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)。

* **條件式存取 」 系統管理員**： 與此角色的使用者有 hello 能力 toomanage Azure Active Directory 條件式存取設定。

* **CRM 服務系統管理員**： 與此角色內 Microsoft CRM Online 的全域權限中的 hello 服務時，hello 能力 toomanage 以及支援票證以及監控服務健康狀況。 如需詳細資訊，請參閱 [關於 Office 365 管理員角色](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)。

* **裝置系統管理員**： 具有此角色的使用者會變成相關聯結的 tooAzure Active Directory 的所有 Windows 10 裝置上的本機電腦系統管理員。 在 Azure Active Directory 中沒有 hello 能力 toomanage 裝置物件。

* **目錄讀取器**： 這是傳統的角色，是不支援 hello 分派 toobe tooapplications[同意架構](active-directory-integrating-applications.md)。 它不應該指派 tooany 使用者。

* **目錄同步作業帳戶**：請勿使用。 此角色會自動指派 toohello Azure AD Connect 服務，和非預期或支援任何其他用途。

* **目錄的寫入器**： 這是傳統的角色，是不支援 hello 分派 toobe tooapplications[同意架構](active-directory-integrating-applications.md)。 它不應該指派 tooany 使用者。

* **Exchange 服務系統管理員**： 具有此角色的使用者全域中有權限 Microsoft Exchange Online，當 hello 服務存在。 如需詳細資訊，請參閱 [關於 Office 365 管理員角色](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)。

* **全域管理員 / 公司系統管理員**： 使用者與此角色有存取 tooall 系統管理功能在 Azure Active Directory 中，以及服務該同盟 tooAzure 像 Exchange Online、 SharePoint Online 的 Active Directory 和線上商務用 Skype。 hello Azure Active Directory 租用戶註冊的 hello 人員會變成全域管理員。 只有全域管理員才能指派其他系統管理員角色。 您的公司可以有多位全域管理員。 全域系統管理員可以重設 hello 任何使用者，以及所有其他的系統管理員的密碼。

  > [!NOTE]
  > 在 Microsoft Graph API、Azure AD Graph API 及 Azure AD PowerShell 中，是將此角色識別為「公司系統管理員」。 它是 「 全域系統管理員 」 中 hello [Azure 入口網站](https://portal.azure.com)。
  >
  >

* **來賓邀請者**: hello"的成員可以邀請 」 使用者設定為 tooNo 時，此角色中的使用者可以管理 Azure Active Directory B2B 來賓使用者的邀請。 在 B2B 共同作業的詳細資訊[有關 hello Azure AD B2B 共同作業預覽](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)。 這不包含任何其他權限。

* **Intune 服務系統管理員**： 具有此角色的使用者全域中有權限 Microsoft Intune Online，當 hello 服務存在。 此外，這個角色包含 hello 能力 toomanage 使用者和裝置在順序 tooassociate 原則中，以及建立和管理群組。

* **信箱管理員**︰此角色僅用來當作 RIM Blackberry 裝置的 Exchange Online 電子郵件支援的一部分。 如果您的組織不使用 RIM Blackberry 裝置上的 Exchange Online 電子郵件，請勿使用此角色。

* **合作夥伴第 1 層支援**︰請勿使用。 此角色已被取代，將會從 Azure AD 中 hello 未來移除。 此角色僅供少數 Microsoft 轉售合作夥伴使用，不適用於一般用途。

* **合作夥伴第 2 層支援**︰請勿使用。 此角色已被取代，將會從 Azure AD 中 hello 未來移除。 此角色僅供少數 Microsoft 轉售合作夥伴使用，不適用於一般用途。

* **密碼管理員 / 技術支援中心管理員**：具有此角色的使用者可以重設密碼、管理服務要求，以及監視服務健全狀況。 密碼管理員可以僅重設使用者和其他密碼管理員的密碼。

  > [!NOTE]
  > 在 Microsoft Graph API、Azure AD Graph API 和 Azure AD PowerShell 中，會將此角色識別為「技術支援中心管理員」。 「 密碼系統管理員 」 處於 hello [Azure 入口網站](https://portal.azure.com/)。
  >
  >
  
* **Power BI 服務系統管理員**： 與此角色的使用者擁有 Microsoft Power BI 中的全域權限、 hello 服務時，hello 能力 toomanage 以及支援票證以及監控服務健康狀況。 如需詳細資訊，請參閱 [關於 Office 365 管理員角色](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d?ui=en-US&rs=en-001&ad=US)。

* **特殊權限角色管理員**：具備此角色的使用者可以管理 Azure Active Directory 中，以及 Azure AD Privileged Identity Management 內的角色指派。 此外，這個角色允許各個層面的 Privileged Identity Management 管理。

* **安全性系統管理員**： 具有此角色的使用者具有所有 hello 唯讀權限的 hello 安全性讀取者角色，再加上 hello 能力 toomanage 組態與安全性相關的服務： Active Directory 識別身分保護 Azure、 Azure資訊保護、 Privileged 的 Identity Management 和 Office 365 [安全性和規範中心。 Office 365 權限的詳細資訊將會位於[hello Office 365 安全性與相容性中心中的權限](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1)。

* **安全性讀取器**： 具有此角色的使用者全域唯讀存取權，包括 Azure Active Directory 識別身分保護、 Privileged Identity Management 中的所有資訊，以及 hello 能力 tooread Azure Active Directory 登入報表和稽核記錄檔。 hello 角色也會授與 Office 365 安全性與相容性中心中的唯讀權限。 Office 365 權限的詳細資訊將會位於[hello Office 365 安全性與相容性中心中的權限](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1)。

* **服務支援系統管理員**： 使用者與此角色都可以開啟支援要求與 Microsoft Azure 和 Office 365 服務，並檢視 hello hello Azure 入口網站中的服務儀表板和訊息置中與 Office 365 系統管理入口網站。 如需詳細資訊，請參閱 [關於 Office 365 管理員角色](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)。

* **SharePoint 服務系統管理員**： 與此角色的使用者擁有 Microsoft SharePoint Online 內的全域使用權限、 hello 服務時，hello 能力 toomanage 以及支援票證以及監控服務健康狀況。 如需詳細資訊，請參閱 [關於 Office 365 管理員角色](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)。

* **商務用 Skype / Lync 服務系統管理員**： 與此角色的使用者有 Microsoft 商務用 Skype 內的全域權限時 hello 服務已存在，以及管理 Azure Active Directory 中的 Skype 特定使用者屬性。 此外，這個角色授與 hello 能力 toomanage 支援票證和監視服務健全狀況。 如需詳細資訊，請參閱 [關於 Office 365 管理員角色](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)。

  > [!NOTE]
  > 在 Microsoft Graph API、Azure AD Graph API 和 Azure AD PowerShell 中，會將此角色識別為「Lync 服務管理員」。 「 Skype 的商務服務系統管理員 」 處於 hello [Azure 入口網站](https://portal.azure.com/)。
  >
  >

* **使用者帳戶管理員**︰具有此角色的使用者可以建立及管理使用者和群組的所有層面。 此外，這個角色包含 hello 能力 toomanage 支援票證，以及監視服務健全狀況。 適用某些限制。 例如，此角色不允許刪除全域管理員，且在允許變更非系統管理員的密碼時，它不允許變更全域管理員或其他特殊權限系統管理員的密碼。

## <a name="administrator-permissions"></a>系統管理員權限

### <a name="billing-administrator"></a>計費管理員

| 可以執行 | 無法執行 |
| --- | --- |
|<p>檢視公司與使用者資訊</p><p>建立 Office 支援票證</p><p>執行 Office 產品的計費和購買作業</p> |<p>重設使用者密碼</p><p>建立和管理使用者檢視</p><p>建立、編輯和刪除使用者與群組，以及管理使用者授權</p><p>管理網域</p><p>管理公司資訊</p><p>委派系統管理角色 tooothers</p><p>使用目錄同步作業</p><p>檢視稽核記錄檔</p>|

### <a name="conditional-access-administrator"></a>條件式存取系統管理員
| 可以執行 | 無法執行 |
| --- | --- |
|<p>檢視公司與使用者資訊</p><p>管理條件式存取設定</p> |<p>重設使用者密碼</p><p>建立和管理使用者檢視</p><p>建立、編輯和刪除使用者與群組，以及管理使用者授權</p><p>管理網域</p><p>管理公司資訊</p><p>委派系統管理角色 tooothers</p><p>使用目錄同步作業</p><p>檢視稽核記錄檔</p>|

### <a name="global-administrator"></a>全域管理員
| 可以執行 | 無法執行 |
| --- | --- |
|<p>檢視公司與使用者資訊</p><p>建立 Office 支援票證</p><p>執行 Office 產品的計費和購買作業</p><p>重設使用者密碼</p><p>重設其他系統管理員的密碼</p><p>建立和管理使用者檢視</p><p>建立、編輯和刪除使用者與群組，以及管理使用者授權</p><p>管理網域</p><p>管理公司資訊</p><p>委派系統管理角色 tooothers</p><p>使用目錄同步作業</p><p>啟用或停用多重要素驗證</p><p>檢視稽核記錄檔</p> |<p>N/A</p>|

### <a name="password-administrator"></a>密碼管理員
| 可以執行 | 無法執行 |
| --- | --- |
| <p>檢視公司與使用者資訊</p><p>建立 Office 支援票證</p><p>重設使用者密碼</p> <p>重設其他系統管理員的密碼</p>|<p>執行 Office 產品的計費和購買作業</p><p>建立和管理使用者檢視</p><p>建立、編輯和刪除使用者與群組，以及管理使用者授權</p><p>管理網域</p><p>管理公司資訊</p><p>委派系統管理角色 tooothers</p><p>使用目錄同步作業</p><p>檢視報告</p>|

### <a name="service-administrator"></a>服務管理員
| 可以執行 | 無法執行 |
| --- | --- |
| <p>檢視公司與使用者資訊</p><p>建立 Office 支援票證</p> |<p>重設使用者密碼</p><p>執行 Office 產品的計費和購買作業</p><p>建立和管理使用者檢視</p><p>建立、編輯和刪除使用者與群組，以及管理使用者授權</p><p>管理網域</p><p>管理公司資訊</p><p>委派系統管理角色 tooothers</p><p>使用目錄同步作業</p><p>檢視稽核記錄檔</p> |

### <a name="user-administrator"></a>使用者管理員
| 可以執行 | 無法執行 |
| --- | --- |
| <p>檢視公司與使用者資訊</p><p>建立 Office 支援票證</p><p>重設使用者密碼，但有限制。</p><p>重設其他系統管理員的密碼</p><p>重設其他使用者的密碼</p><p>建立和管理使用者檢視</p><p>建立、編輯和刪除使用者與群組，以及管理使用者授權，但有限制。 他無法刪除全域管理員或建立其他管理員。</p> |<p>執行 Office 產品的計費和購買作業</p><p>管理網域</p><p>管理公司資訊</p><p>委派系統管理角色 tooothers</p><p>使用目錄同步作業</p><p>啟用或停用多重要素驗證</p><p>檢視稽核記錄檔</p> |

### <a name="security-reader"></a>安全性讀取者
| 在 | 可以執行 |
| --- | --- |
| 身分識別防護中心 |讀取安全性功能的所有安全性報告和設定資訊<ul><li>反垃圾郵件<li>加密<li>資料外洩防護<li>反惡意程式碼<li>進階威脅防護<li>防網路釣魚<li>郵件流程規則 |
| Privileged Identity Management |<p>具有唯讀存取 tooall 資訊顯示在 Azure AD PIM： 安全性原則和 Azure AD 角色指派的報表，檢閱，並在 hello 未來會讀取存取 toopolicy 資料和案例除了 Azure AD 角色指派的報表。<p>**無法**註冊 Azure AD PIM 或進行任何變更 tooit。 PIM 的入口網站或透過 PowerShell，此角色中的使用者可以啟用其他角色 （例如，全域管理員或特殊權限的角色管理員），如果 hello 使用者是他們的候選項目。 |
| <p>監視 Office 365 服務健康狀況</p><p>Office 365 安全性與法規遵循中心</p> |<ul><li>讀取和管理警示<li>讀取安全性原則<li>讀取威脅情報、執行 Cloud App Discovery，以及在搜尋和調查時執行隔離<li>讀取所有報告 |

### <a name="security-administrator"></a>安全性系統管理員
| 在 | 可以執行 |
| --- | --- |
| 身分識別防護中心 |<ul><li>所有的 hello 安全性讀取者角色的權限。<li>此外，hello 能力 tooperform 除了重設密碼的所有 IPC 作業。 |
| Privileged Identity Management |<ul><li>所有的 hello 安全性讀取者角色的權限。<li>**無法**管理 Azure AD 角色成員資格或設定。 |
| <p>監視 Office 365 服務健康狀況</p><p>Office 365 安全性與法規遵循中心 |<ul><li>所有的 hello 安全性讀取者角色的權限。<li>可以設定 hello 進階威脅防護功能 （惡意程式碼和病毒保護、 惡意 URL 組態、 URL 追蹤等） 中的所有設定。 |

## <a name="details-about-hello-global-administrator-role"></a>Hello 全域管理員角色的相關詳細資料
hello 全域系統管理員具有存取 tooall 系統管理功能。 根據預設，hello 註冊人員的 Azure 訂用帳戶會指派 hello hello 目錄的全域管理員角色。 只有全域管理員才能指派其他系統管理員角色。

### <a name="tooadd-a-colleague-as-a-global-administrator"></a>tooadd 同事身為全域管理員

1. 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)hello 租用戶目錄的全域管理員的帳戶。

   ![開啟 Azure AD 系統管理中心](./media/active-directory-assign-admin-roles/active-directory-admin-center.png)

2. 選取 [使用者和群組] &gt; [所有使用者]

3. 尋找您想 toodesignate 全域系統管理員身分，開啟該使用者的 hello 刀鋒視窗的 hello 使用者。

4. 在 [hello 使用者刀鋒視窗中，選取 [**目錄角色**。
 
5. 在 [hello 目錄角色刀鋒視窗中，選取 [hello**全域管理員**角色，並儲存。

## <a name="assign-or-remove-administrator-roles"></a>指派或移除系統管理員角色
如何 tooassign 系統管理角色 tooa 使用者在 Azure Active Directory 中，請參閱的 toolearn [tooadministrator 角色在 Azure Active Directory 中的指派給使用者](active-directory-users-assign-role-azure-portal.md)。

## <a name="deprecated-roles"></a>已被取代的角色

不應該使用下列角色的 hello。 它們已被取代，將會從 Azure AD 中 hello 未來移除。

* AdHoc 授權管理員
* 傳送電子郵件給經過驗證的使用者建立者
* 加入裝置
* 裝置管理員
* 裝置使用者
* 加入工作場所裝置

## <a name="next-steps"></a>後續步驟
* toolearn 深入了解如何 toochange 管理員 Azure 訂用帳戶，請參閱[如何 tooadd 或變更的 Azure 系統管理員角色](../billing-add-change-azure-subscription-administrator.md)
* toolearn 深入了解如何控制資源存取 Microsoft Azure 中，請參閱[了解 Azure 中的資源存取](active-directory-understanding-resource-access.md)
* 如需有關 Azure Active Directory 與 tooyour Azure 訂用帳戶的關聯方式的詳細資訊，請參閱[都與 Azure Active Directory 相關聯 Azure 訂用帳戶](active-directory-how-subscriptions-associated-directory.md)
* [管理使用者](active-directory-create-users.md)
* [管理密碼](active-directory-manage-passwords.md)
* [管理群組](active-directory-manage-groups.md)
