---
title: "aaaGet 開始使用 Azure Active Directory 中授權 |Microsoft 文件"
description: "Azure Active Directory 授權的運作方式 tooget 啟動方式最佳做法"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a>在 Azure Active Directory 中進行自身和使用者的授權

> [!div class="op_single_selector"]
> * [Azure 入口網站指示](active-directory-licensing-get-started-azure-portal.md)
> * [取得 Azure 傳統入口網站的資訊](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) 是 Microsoft 的「身分識別即服務 (IDaaS)」解決方案與平台。 Microsoft 在不同的服務版本中提供 Azure AD：

* Azure Active Directory Free，任何 Microsoft 服務 (例如 Office 365、Dynamics、Microsoft Intune 或 Azure) 均提供此版本。 在此模式中，Azure AD 不會產生任何使用費用。

* Azure AD 付費版本，例如：
  - Enterprise Mobility + Security 
  - Azure AD Premium (P1 和 P2)
  - Azure AD Basic
  - Azure Multi-Factor Authentication

如同許多 Microsoft 線上服務一般，大多數 Azure AD 付費版本都是透過賦予每位使用者權利來提供，就像在 Office 365、Microsoft Intune 和 Azure AD 中一樣。 在這些情況下，購買 hello 服務由一或多個訂用帳戶，每個訂用帳戶包含您租用戶中的某些 prepurchased 的授權。 您可透過下列方式來賦予每位使用者權利：

* 指派授權。 
* 建立 hello 使用者與 hello 產品之間的連結。
* 啟用 hello hello 使用者的服務元件。
* 使用一 hello 預付授權。

[立即試用 Azure AD Premium。](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

如需 Azure AD 服務功能的一般概觀，請參閱[什麼是 Azure AD？](active-directory-whatis.md)。 如需詳細資訊，請參閱[服務等級協定頁面](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/)。

> [!NOTE]
> Azure 隨用隨付訂用帳戶啟用 Azure 資源的建立，並再將它們對應 tooyour 付款方法。 沒有任何與 hello 訂用帳戶相關聯的授權計數。 當您授與 Azure 資源上的使用者權限 toooperate 對應 toohello 訂用帳戶時，它們與 hello 訂用帳戶相關聯而且可以管理訂用帳戶的資源。

## <a name="how-does-azure-active-directory-licensing-work"></a>Azure Active Directory 授權的運作方式為何？

以授權為基礎的 Azure AD 服務可透過在 Azure AD 服務租用戶中啟用訂用帳戶來開始運作。 Hello 訂閱在作用中之後，會由 Azure AD 系統管理員管理 hello 服務功能，而且所授權的使用者使用。

### <a name="manage-subscription-information"></a>管理訂用帳戶資訊

當您購買企業行動力 + 安全性、 Azure AD Premium 或 Azure AD Basic，您的租用戶時，會更新與 hello 訂用帳戶，包括其有效期間內，而且預付授權。 您的訂用帳戶資訊，包括 hello 分派或可用授權數目是透過 Azure 入口網站 hello： 下**Azure Active Directory**，開啟 hello**授權**磚 hello特定的目錄。 hello**授權**刀鋒視窗是也 hello 最佳地方 toomanage 授權指派。

每個訂用帳戶都包含一或多個服務方案，例如 Azure AD、Multi-Factor Authentication、Intune、Exchange Online 或 SharePoint Online。  Azure AD 授權的管理「不」需要進行服務方案等級的管理。 與 office 365 的不同，因為它會仰賴此進階的組態模式 toomanage 存取 tooincluded 服務。 Azure AD 會依賴服務中組態 tooenable 功能，並管理個別的權限。

> [!IMPORTANT]
> Azure AD Premium、 Azure AD Basic 和企業行動力 + 安全性訂用帳戶會佈建的局部的 tootheir 目錄租用戶。 訂用帳戶無法目錄或其他目錄中的使用的 tooentitle 使用者之間分割。 您可以在不同目錄之間移動訂用帳戶，但需要提交支援票證，或者，您也可以先取消再重新購買，來直接購買訂用帳戶。
>
> 當 Azure AD 或 Enterprise Mobility + Security 採購自大量授權的訂閱，並啟用當 hello 協議包含其他 Microsoft Online services (例如，Office 365) 時，會自動發生。 

### <a name="assign-licenses"></a>指派授權

取得訂用帳戶是所有您需要付費功能 tooconfigure，雖然您仍然必須將授權發佈的 Azure AD 的付費功能 toousers。 任何使用者都應該具有存取 tooor 透過 Azure AD 的付費功能管理人員必須指派授權。 授權指派是一種使用者與購買的服務 (例如 Azure AD Premium、Basic 或 Enterprise Mobility + Security) 之間的對應。


您可以透過下列方式來管理目錄中應該擁有授權的使用者： 

* 指派授權在 hello toogroups [Azure 入口網站](active-directory-licensing-whatis-azure-portal.md)。
* 指派授權直接 toousers 透過 hello 入口網站、 PowerShell 或應用程式開發介面。 

您指派授權 tooa 群組時，所有群組成員已都獲得授權。 如果新增或從 hello 群組中移除使用者，hello 適當授權指派，或移除。 群組指派可以利用任何群組管理列印可用 tooyou，而且與以群組為基礎的指派 tooapplications 一致。

您可以使用[群組為基礎的授權指派](active-directory-licensing-whatis-azure-portal.md)tooset hello 如下的規則：
* 目錄中的所有使用者都自動取得授權
* Everyone 具有 hello 適當職稱取得授權
* 您可以將委派 hello 組織中的 hello 決策 tooother 管理員 (使用[自助群組](active-directory-accessmanagement-self-service-group-management.md))

如需授權指派 toogroups 詳細討論，包括進階的案例和 Office 365 授權的情況下，請參閱[指派授權 Azure Active Directory 中的群組成員資格 toousers](active-directory-licensing-group-assignment-azure-portal.md)。

## <a name="get-started-with-azure-ad-licensing"></a>開始使用 Azure AD 授權

Azure AD 很容易就能開始使用。 在註冊 [Azure 免費試用](https://azure.microsoft.com/offers/ms-azr-0044p/)的過程中，您就可以建立您的目錄。

hello 下列最佳作法可協助確保您的租用戶會對齊您可能會耗用其他 Microsoft 服務與您的目標 hello 服務：

- 如果您已經在使用任何 Microsoft hello 組織服務，您已經有 Azure AD 租用戶。 有用的 toouse hello 相同租用戶的其他服務，以便核心身分識別管理，包括佈建和混合式單一登入 (SSO)，可以在 hello 服務間使用它。 搭配單一登入，您的使用者從 hello 豐富功能獲益跨 hello 服務。 因此，如果您決定 toobuy 您公司的 Azure AD 的付費服務，我們建議您使用相同的一次租用戶的 hello。

- 我們建議您在 hello Azure 入口網站中使用新的租用戶，如果您計劃：
  - 對一組不同的使用者 (例如夥伴或客戶) 使用 Azure AD。
  - 在與生產服務隔離的環境中評估 Azure AD 服務。
  - 為服務設置沙箱環境。

  使用您的帳戶建立 hello 新目錄全域系統管理員權限與外部使用者的身分。 當您登入 toohello 與此帳戶的 Azure 入口網站時，您可以看到此租用戶，並存取所有系統管理工作。

> [!NOTE]
> Azure AD 支援「來賓使用者」，也就是 Azure AD 租用戶中的使用者帳戶，這些帳戶是透過 Microsoft 帳戶或另一個租用戶中的 Azure AD 身分識別所建立。 hello Office 365 系統管理入口網站目前不支援這些使用者。 Microsoft 帳戶與 Guest 使用者，則無法無法 tooaccess hello Office 365 系統管理入口網站，從其他 Azure AD 租用戶的來賓使用者會被忽略。 在 hello 後者的情況下，只有 hello 使用者的本機帳戶，請在 hello Azure AD 或 hello 使用者最初建立所在，Office 365 租用戶存取。

### <a name="select-one-or-more-license-trials"></a>選取一或多個授權試用版

您可以在 [Azure Active Directory] &gt; [快速啟動] 下啟用 Azure AD Premium 或 Enterprise Mobility + Security 試用版訂用帳戶。

![選取授權試用版](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

試用版授權位於 hello**授權**刀鋒視窗。

### <a name="assign-licenses-toousers-and-groups"></a>指派授權 toousers 和群組

Hello 訂閱為作用狀態後，您應該指派授權 tooyourself。 然後重新整理 hello 瀏覽器 tooensure 看到 hello 的所有功能。 hello 下一個步驟是 tooassign 授權 toohello 使用者需要存取 toopaid Azure AD 功能。 中所述[指派授權](#assign-licenses)、 tooassign 授權是代表 hello tooidentify hello 群組想要的對象與指派 hello 授權 tooit 的簡單方式。 如此一來，使用者加入或移除從 hello 群組在其生命週期會指派，或分別移除 hello 授權。

> [!NOTE]
> 並非所有位置都可使用某些 Microsoft 服務。 Hello 管理員 tooa 使用者可以指派授權之前，必須指定 hello**使用位置**hello 使用者的屬性。 您可以設定此屬性在**使用者** &gt; **設定檔** &gt; **設定**hello Azure 入口網站中。 當使用群組授權指派，其使用位置未指定任何使用者會繼承 hello hello 目錄位置。

tooassign 授權下**Azure Active Directory** &gt; **授權** &gt; **所有產品**，選取一或多個產品，然後選取**指派**hello 命令列上。

![選取授權 tooassign](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

您可以使用 hello**使用者和群組**刀鋒視窗 toochoose hello 產品中的多個使用者或群組或 toodisable 服務計劃。 使用上最上層 toosearch hello [搜尋] 方塊，使用者和群組的名稱。

![選取要指派授權的使用者或群組](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

您指派授權 tooa 群組時，可能需要一些時間才所有使用者都會都繼承 hello 授權，而是根據 hello hello 群組中的使用者數目。 您可以檢查處理狀態 hello hello**群組**刀鋒視窗中的，在 hello**授權**磚。

![授權指派狀態](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

在 Azure AD 授權指派期間，可能會發生指派錯誤，但在管理 Azure AD 和 Enterprise Mobility + Security 產品時則相對較少發生。 可能發生的指派錯誤僅限於：
- 指派衝突： 在使用者先前已指派與 hello 目前的授權不相容的授權。 在此情況下，hello 新授權指派，需要移除目前 hello。
- 超過可用的授權： hello 分派群組中的使用者數目超過 hello 可用的授權，使用者的指派狀態會反映失敗 tooassign toomissing 授權到期。

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure AD B2B 共同作業授權

B2B 共同作業可讓您 tooinvite guest 使用者到 Azure AD 租用戶 tooprovide 存取 tooAzure AD 服務和您將提供任何 Azure 資源。  

沒有邀請 B2B 使用者並指派它們 tooan 在 Azure AD 中的應用程式需付費。 針對每個來賓 too10 應用程式設定使用者和 3 的基本報告也是 B2B 共同作業的使用者可以免費。 如果 guest 使用者有任何適當的授權指派 hello 夥伴的 Azure AD 租用戶中，它們將會用您以及授權。

它不是必要，但如果您想 tooprovide 存取 toopaid Azure AD 功能，這些 B2B 來賓使用者必須獲得授權與適當的 Azure AD 授權。 邀請其他租用戶與 Azure AD 的付費授權可以指派 B2B 共同作業的使用者權限受邀 tooan 額外的五個來賓使用者 toohello 租用戶。 如需這方面的案例和資訊，請參閱 [B2B 共同作業授權指引](active-directory-b2b-licensing.md)。

### <a name="view-assigned-licenses"></a>檢視已指派的授權

已指派授權和可用授權的摘要檢視會顯示在 [Azure Active Directory] &gt; [授權] &gt; [所有產品] 下。

![檢視授權摘要](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

選取特定產品時，會顯示可用的已指派使用者和群組的詳細清單。 hello**授權使用者**清單會顯示目前耗用一個授權和是否 hello 授權已直接指派 toohello 使用者，或如果它繼承自群組的所有使用者。

![檢視授權詳細資料](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

同樣地，hello**授權群組**清單會顯示所有群組已指派給 toowhich 授權。 選取使用者或群組的 tooopen hello**授權**刀鋒視窗中，會顯示所有授權指派給 toothat 物件。

### <a name="remove-a-license"></a>移除授權

tooremove 授權，請移 toohello 使用者或群組，並開啟 hello**授權**磚。 選取 hello 授權，然後按一下 **移除**。

![移除授權](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

無法直接移除繼承自群組的 hello 使用者的授權。 相反地，移除 hello 使用者從他們從中繼承 hello 授權 hello 群組。

### <a name="extend-trials"></a>延長試用期

客戶試用延伸模組都會提供為自助式註冊透過 hello Office 365 入口網站。 客戶的系統管理員可以移 toohello Office 入口網站 （取決於 hello Office 入口網站的權限的存取），選取 hello Azure AD Premium 試用版。 按一下 hello**試用期延長**連結啟動 hello 延伸模組程序。 您必須輸入信用卡，但不會被收費。

![在 hello Azure 入口網站中的試用期延長](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>後續步驟

深入了解 toolearn 進階案例的授權管理群組，透過讀取 hello 文章[指派授權 tooa 群組](active-directory-licensing-group-assignment-azure-portal.md)。

以下是有關 tooconfigure 並使用其他 Azure AD 的付費功能：

* [自助式密碼重設](active-directory-manage-passwords.md)
* [自助式群組管理](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [直接購買 Azure AD Premium 授權](http://aka.ms/buyaadp)
