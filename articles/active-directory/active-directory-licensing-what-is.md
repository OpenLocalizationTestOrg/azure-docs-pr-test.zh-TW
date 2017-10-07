---
title: "aaaLicense hello Azure 傳統入口網站中的 Azure Active Directory 使用者 |Microsoft 文件"
description: "Microsoft Azure Active Directory 授權的描述、 其運作方式、 tooget 啟動的方式，與最佳做法，包括 Office 365、 Microsoft Intune 和 Azure Active Directory Premium 和 Basic 版本"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d769e8c6-7581-43f5-a3b4-de4b1dca2344
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;H1Hack27Feb2017
ms.openlocfilehash: 4d5f244cbee2ae37a30976f70b5d4f21c3516d90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-hello-azure-classic-portal"></a>什麼 Microsoft Azure Active Directory 授權 hello Azure 傳統入口網站？

> [!div class="op_single_selector"]
> * [取得 Azure 入口網站指示](active-directory-licensing-get-started-azure-portal.md)
> * [Azure 傳統入口網站資訊](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) 是 Microsoft 的「身分識別即服務 (IDaaS)」解決方案與平台。 Azure AD 提供的數字的範圍是從 Azure AD 免費版，這是適用於任何 Microsoft 服務，例如 Office 365、 Dynamics、 Microsoft Intune 與 Azure 功能與技術版本 （Azure AD 不會產生任何耗用量費用在此模式中），tooAzure AD 付費版本，例如 Enterprise Mobility Suite (EMS)、 Azure AD Premium 和 Basic，以及 Azure Multi-factor Authentication (MFA)。 如同許多 Microsoft 線上服務一般，大多數 Azure AD 付費版本都是透過賦予每位使用者權利來提供，就像在 Office 365、Microsoft Intune 和 Azure AD 中一樣。 在這些情況下，購買 hello 服務代表與一或多個訂用帳戶，而每個訂用帳戶包含您租用戶中的預購授權數目。 透過授權指派，建立 hello 使用者與 hello 產品啟用 hello hello 使用者的服務元件之間的連結，可達到每個使用者權利，並使用其中一個 hello 預付授權。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 如何置 tooassign hello Azure AD 系統管理員中的系統管理員角色，請參閱[自己和您的使用者在 Azure AD 中的授權](active-directory-licensing-get-started-azure-portal.md)。

[立即試用 Azure AD Premium。](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Azure AD 管理入口網站是 hello Azure 傳統入口網站的一部分。 雖然使用 Azure AD 不需要購買任何 Azure，但是存取此入口網站需要有效的 Azure 訂用帳戶或 [Azure 試用版訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)。
>
>

如需 Azure AD 服務功能的一般概觀，請參閱 [什麼是 Azure AD](active-directory-whatis.md)。
[深入了解 Azure AD 服務等級](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Azure 隨付訂用帳戶不相同： 也表示您的目錄，而這些訂用帳戶啟用 Azure 資源的建立，並將它們對應 tooyour 付款方法。 在此情況下沒有任何與 hello 訂用帳戶相關聯的授權計數。 與 hello 訂用帳戶，hello 使用者存取 toomanaging 訂用帳戶資源，使用者的關聯，來授與它們對應的 Azure 資源 toohello 訂用帳戶的權限 toooperate 達成。
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Azure AD 授權如何運作？
以授權為基礎 (以權利為基礎) 的 Azure AD 服務的運作方式，是在您的 Azure AD 目錄/服務租用戶中啟用訂用帳戶。 Hello 訂用帳戶項目作用之後就可以由目錄/服務系統管理員管理和使用授權的使用者 hello 服務功能。

當您購買或啟用 Enterprise Mobility Suite、 Azure AD Premium 或 Azure AD Basic，您的目錄會更新與 hello 訂用帳戶，包括其有效期間內，而且預付授權。 您的訂用帳戶資訊，包括狀態、 下一個開發週期事件，以及 hello 分派或可用授權數目是透過 hello hello hello 特定目錄的授權 索引標籤下的 Azure 傳統入口網站。 這也是 toobest 位置 toomanage 授權指派。

每個訂用帳戶包含一或多個服務方案之後，每個對應 hello 加入 hello 服務類型，功能層級例如，在 Azure AD，Azure MFA、 Microsoft Intune、 Exchange Online 或 SharePoint Online。 Azure AD 授權管理「不」需要服務方案等級管理。 這是從 Office 365 依賴此進階的組態模式 toomanage 存取 tooincluded 服務不同。 在服務組態中，tooenable 功能依賴 azure AD，並管理個別的權限。

一般情況下，Azure AD 訂用帳戶資訊是透過 hello Azure 傳統入口網站，hello hello 特定目錄的授權 索引標籤下的方式管理。 Azure AD 訂用帳戶，但 hello 的例外是 Azure AD Premium，不要顯示 hello Office 入口網站中。

> [!IMPORTANT]
> Azure AD Premium 和 Basic，以及 Enterprise Mobility Suite 訂閱，會佈建的局部的 tootheir 目錄租用戶。 訂用帳戶無法目錄或其他目錄中的使用的 tooentitle 使用者之間分割。 目錄之間移動訂用帳戶可以，但需要提交支援票證或取消和重新的直接購買 hello 案例中，購買。
>
> 當您購買 Azure AD 或 Enterprise Mobility Suite，透過大量授權的訂用帳戶啟用動作會自動發生時 hello 協議包含其他 Microsoft Online services，例如 Office 365。
>
>

付費型 Azure AD 功能範圍 hello 廣度的 hello 目錄。 範例包括：

* 群組為基礎的指派 tooapplications hello 特定應用程式管理 下啟用。
* 進階和自助式群組管理功能都可在 hello 目錄組態或 hello 特定群組中。
* 進階安全性報告位於 hello 報表 索引標籤
* 雲端應用程式探索會在顯示 hello Azure 入口網站，在 身分識別。

### <a name="assigning-licenses"></a>指派授權
取得訂用帳戶是所有您需要 tooconfigure 付費功能，使用 Azure AD 的付費功能需要散發授權 toohello 恰當的人員。 一般情況下，任何使用者都應該具有存取 tooor 透過 Azure AD 的付費功能管理人員也必須指派授權。 授權指派是一種使用者與購買的服務 (例如 Azure AD Premium、Basic 或 Enterprise Mobility Suite) 之間的對應。

管理您的目錄中哪些使用者應該擁有授權很簡單。 它可以藉由指派 tooa 群組 toocreate 指派規則，透過 Azure AD 管理入口網站 hello 或直接透過入口網站、 PowerShell 或應用程式開發介面 toohello 右個人指派授權，來完成。 指派授權 tooa 群組時，所有群組成員將會都指派授權給使用者。 如果使用者加入或移除從 hello 群組將其指派或移除 hello 適當授權。 群組指派可以利用任何群組管理可用 tooyou，與以群組為基礎的指派 tooapplications 保持一致。 使用這個方法，您可以設定規則，使您的目錄中的所有使用者會自動指派都給、 確保與 hello 適當職稱的每個人都已將授權或甚至委派 hello 組織中的 hello 決策 tooother 管理員。

使用以群組為基礎的授權指派，缺少使用位置的任何使用者將會在指派期間繼承 hello 目錄位置。 Hello 管理員可以變更此位置在任何時間。 在其中 hello 自動指派失敗的情況下 tooerror，hello 使用者資訊底下的授權類型會反映該狀態。

## <a name="getting-started-with-azure-ad-licensing"></a>開始使用 Azure AD 授權
開始使用 Azure AD 會簡單。您一律可以建立您的註冊 tooa 免費的 Azure 試用版一部分的目錄。 [深入了解以組織身分註冊](sign-up-organization.md)。 hello 下列可協助您確認您的目錄，與其他 Microsoft 服務，您可能會耗用或 tooconsume 和您的目標取得 hello 服務計劃最佳對齊。

以下是幾種最佳作法︰

* 如果您已經在使用任何 Microsoft 的組織服務，您就已經有 Azure AD 目錄。 在此情況下，您應該繼續 toouse hello 的其他服務，相同的目錄，以便核心身分識別管理，包括佈建和混合式 SSO，可以利用跨 hello 服務。 您的使用者將會擁有單一登入體驗和將受益跨 hello 服務的更豐富的功能。 如此一來，如果您決定 toobuy Azure AD 的付費服務，您的工作人員，我們建議您使用這 hello 相同的目錄 toodo。
* 如果您計劃 toouse Azure AD 中獲得一組不同的使用者 （合作夥伴、 客戶和等等），或如果您希望 tooevaluate Azure AD 服務，而且想要 toodo，隔離您的實際執行服務，或如果您要尋找 toosetup 沙箱環境您的服務，我們建議您先建立新的目錄，透過 hello Azure Azure 傳統入口網站。 [深入了解建立新 hello Azure 傳統入口網站中的 Azure AD 目錄](active-directory-licensing-directory-independence.md)。 將會建立 hello 新目錄，以防止外部使用者與全域系統管理員權限的身分與您的帳戶。 當您登入 toohello Azure 傳統入口網站，此帳戶，您將會是能 toosee 這個目錄並且存取所有目錄管理工作。 我們建議您建立本機帳戶具有適當權限 toomanage 其他 Microsoft 服務 （即透過 hello Azure 傳統入口網站無法存取）。 [深入了解在 Azure AD 中建立使用者帳戶](active-directory-create-users.md)。

> [!NOTE]
> Azure AD 支援「外部使用者」，這是在 Azure AD 執行個體中，使用 Microsoft 帳戶 (MSA) 或另一個目錄中的 Azure AD 身分識別所建立的使用者帳戶。 我們忙碌時擴充到所有的 Microsoft 的組織的服務，這項功能目前這些帳戶中不支援某些 hello 服務體驗。例如，hello Office 365 系統管理入口網站目前不支援這些使用者。 如此一來，具有 Microsoft 帳戶的外部使用者將無法能 tooaccess hello Office 365 系統管理入口網站，而其他 Azure AD 目錄中的外部使用者將會被忽略。 在 hello 後者的情況下，只有 hello 使用者的本機帳戶、 hello Azure AD 或 Office 365 directory hello 使用者最初建立所在，是透過下列方式存取。
>
>

如之前所述，Azure AD 有不同的付費版本。 這些版本在其購買可用性有些微的差異：

| 產品 | EA/VL | 開啟 | CSP | MPN 使用權利 | 直接購買 | 試用版 |
| --- | --- | --- | --- | --- | --- | --- |
| Enterprise Mobility Suite |X |X |X |X | |X |
| Azure AD Premium |X |X |X | |X |X |
| Azure AD Basic |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>選取一或多個授權試用版
 在所有情況下，您可以選取您想 hello 授權 索引標籤，您的目錄中的 hello 特定試用啟用 Azure AD Premium 或 Enterprise Mobility Suite 試用訂用帳戶。 任何一個試用版都包含 100 個授權的 30 天訂用帳戶。

![Azure Active Directory 試用版授權方案](./media/active-directory-licensing-what-is/trial_plans.png)

![Enterprise Mobility Suite 試用版授權方案](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![啟用的試用版授權方案](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>指派授權
一旦 hello 訂閱為作用中，您應該指派授權 tooyourself，並重新整理 hello 瀏覽器 tooensure，您會看到所有的功能。 hello 下一個步驟是 tooassign 授權 toohello 使用者將需要 tooaccess 或包含在付費型 Azure AD 的功能。 如我們上面所述在 指派授權，"hello 最佳方式 toodo 這是 tooidentify hello 群組代表 hello 預期對象並將它指派 toohello 授權。如此一來，使用者都加入或移除從 hello 群組在其生命週期將會被指派 tooor 移除了 hello 授權。

tooassign 授權 tooa 群組或個別使用者，選取 hello 授權方案，tooassign 然後按一下 **指派**hello 命令列上。

![啟用的試用版授權方案](./media/active-directory-licensing-what-is/assign_licenses.png)

一旦在 hello 分派對話方塊 hello 選取的方案中，您可以選取使用者，並將它們加入 toohello**指派**hello 右邊資料行。 您可以透過 hello 使用者清單頁面上，或搜尋特定人員使用 hello 尋找玻璃上 hello 右上角的 hello 使用者方格。 tooassign 群組中，選取 「 群組 」，從 hello**顯示**功能表，然後按一下 hello 核取按鈕會顯示 hello 右 toorefresh hello 分派。

![指派授權 toogroups](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

您現在可以搜尋或透過群組頁面上，並將其新增 toohello**指派**hello 中的資料行相同的方式。 您可以在單一作業中使用這些 tooassign 使用者和群組的組合。 toocomplete hello 指派程序中，按一下 hello 在 hello 右下 hello 頁面右下角的核取按鈕。

![授權指派進度訊息](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

當指派的群組時，其成員會繼承 hello 授權 30 分鐘內，但通常是在 1-2 分鐘內。

在 Azure AD 授權指派期間，可能會發生指派錯誤，但通常很少見。 可能發生的指派錯誤僅限於：

* 指派衝突-當使用者先前已指派與 hello 目前的授權不相容的授權。 在此情況下，指派 hello 新的授權將會需要移除 hello 前一個。
* 超過可用的授權-hello 分派群組中的使用者數目超過可用的授權時 hello 使用者的指派狀態會反映失敗 tooassign toomissing 授權到期。

### <a name="view-assigned-licenses"></a>檢視已指派的授權
指派的授權，包括使用、 已指派和下一個訂用帳戶的生命週期事件的摘要檢視會顯示在 [hello**授權**] 索引標籤。

![指派授權的檢視 hello 數目](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

瀏覽到授權方案時，會看見已指派的使用者和群組的詳細清單，其中包括指派狀態和路徑 (直接或繼承自一或多個群組)。

![詳細顯示授權方案中已指派的授權](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

移除授權就和指派授權一樣簡單。 如果 hello 使用者直接指派或指派的群組，您可以移除 hello 授權，方法是選取 hello 授權類型，選取**移除**、 新增 hello 使用者或群組 toohello 移除清單中，並確認 hello 動作。 或者，您可以在其中開啟授權類型、 選取 hello 特定使用者或群組，並點選**移除**hello 命令列上。 tooend 使用者繼承授權的群組，只要 hello 使用者從群組中移除 hello。

### <a name="extending-trials"></a>延長試用期
客戶試用延伸模組都會提供自助式透過 hello Office 365 入口網站。 客戶的系統管理員可以瀏覽 toohello [Office 入口網站](https://portal.office.com/#Billing)（取決於 hello Office 入口網站的權限的存取），選取您的 Azure AD Premium 試用版。 按一下 hello**試用期延長**連結，並遵循 hello 指示。 您將需要 tooenter 信用卡，但不是會被收費。

![擴充 hello Office 入口網站中的授權試用版](./media/active-directory-licensing-what-is/extend_license_trial.png)

客戶也可以提交支援要求來要求延長試用期。 客戶的系統管理員可以瀏覽 toohello Office 365 入口網站[支援頁面](http://aka.ms/extendAADtrial)（取決於 hello Office 支援網頁的權限的存取權）。 在此頁面上的 [功能] 下方選取 [訂用帳戶和試用版]，以及在 [徵兆] 下方選取 [試用版問題]。 最後，在 hello 情況下輸入資訊

![使用支援要求延長授權試用期](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>後續步驟
現在，您可能會是準備 tooconfigure，並且使用以 Azure AD Premium 功能。

* [自助式密碼重設](active-directory-manage-passwords.md)
* [自助式群組管理](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect 健康情況](active-directory-aadconnect-health.md)
* [群組指派 tooapplications](active-directory-manage-groups.md)
* [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [直接購買 Azure AD Premium 授權](http://aka.ms/buyaadp)
