---
title: "Azure Active Directory 中的 aaaLicense 使用者 |Microsoft 文件"
description: "深入了解如何 toolicense 自己和您在 Azure Active Directory 中的使用者。"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: ae0bc030fa02b79d1dd01ca961b4e96e6b9c470d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-license-users-in-azure-active-directory"></a>快速入門：在 Azure Active Directory 中授權使用者
以授權為基礎的 Azure AD 服務的運作方式，是在您的 Azure 租用戶中啟用 Azure Active Directory (Azure AD) 訂用帳戶。 Hello 訂閱在作用中之後，會由 Azure AD 系統管理員管理服務功能，而且所授權的使用者使用。 當您購買企業行動力 + 安全性、 Azure AD Premium 或 Azure AD Basic，您的租用戶時，會更新與 hello 訂用帳戶，包括其有效期間內，而且預付授權。 您的訂用帳戶資訊，包括 hello 分派或可用授權數目是透過 hello Azure 入口網站下**Azure Active Directory**所開啟的 hello**授權**磚。 hello**授權**刀鋒視窗是也 hello 最佳地方 toomanage 授權指派。

取得訂用帳戶是所有您需要付費功能 tooconfigure，雖然您仍需指派使用者授權的付費 Azure AD 的付費功能。 應存取 Azure AD 付費功能或者透過 Azure AD 付費功能管理的人員，都必須獲得授權。 授權指派是一種使用者與購買的服務 (例如 Azure AD Premium、Basic 或 Enterprise Mobility + Security) 之間的對應。

您可以使用[群組為基礎的授權指派](active-directory-licensing-whatis-azure-portal.md)tooset hello 如下的規則：
* 目錄中的所有使用者都自動取得授權
* Everyone 具有 hello 適當職稱取得授權
* 您可以將委派 hello 組織中的 hello 決策 tooother 管理員 (使用[自助群組](active-directory-accessmanagement-self-service-group-management.md))

> [!TIP]
> 如需授權指派 toogroups 詳細討論，包括進階的案例和 Office 365 授權的情況下，請參閱[指派授權 Azure Active Directory 中的群組成員資格 toousers](active-directory-licensing-group-assignment-azure-portal.md)。

## <a name="assign-licenses-toousers-and-groups"></a>指派授權 toousers 和群組
使用有效的訂用帳戶，應該先指派授權 tooyourself 並重新整理您的瀏覽器 tooensure，您會看到所有包含的 hello 預期功能與您的訂用帳戶。 hello 下一個步驟是 tooassign 授權 toohello 使用者需要存取 toopaid Azure AD 功能。 輕鬆 tooassign 授權是使用者，而非 tooindividuals tooassign 授權 toogroups。 當您指派授權 tooa 群組時，所有群組成員已都獲得授權。 加入或從 hello 群組中移除使用者時，會自動會指派或移除 hello 適當授權。 

> [!NOTE]
> 並非所有位置都可使用某些 Microsoft 服務。 Hello 管理員 tooa 使用者可以指派授權之前，必須指定 hello**使用位置**hello 使用者的屬性。 您可以設定此屬性在**使用者** &gt; **設定檔** &gt; **設定**hello Azure 入口網站中。 當使用群組授權指派，其使用位置未指定任何使用者會繼承 hello hello 目錄位置。

tooassign 授權下**Azure Active Directory** &gt; **授權** &gt; **所有產品**，選取一或多個產品，然後選取**指派**hello 命令列上。

![選取授權 tooassign](media/license-users-groups/select-license-to-assign.png)

您可以使用 hello**使用者和群組**刀鋒視窗 toochoose hello 產品中的多個使用者或群組或 toodisable 服務計劃。 使用上最上層 toosearch hello [搜尋] 方塊，使用者和群組的名稱。

![選取要指派授權的使用者或群組](media/license-users-groups/select-user-for-license-assignment.png)

當您指派授權 tooa 群組時，可能需要一些時間才所有使用者都會都繼承 hello 授權 hello 群組 hello 大小而定。 您可以檢查處理狀態 hello hello**群組**刀鋒視窗中的，在 hello**授權**磚。

![授權指派狀態](media/license-users-groups/license-assignment-status.png)

在 Azure AD 授權指派期間，可能會發生指派錯誤，但在管理 Azure AD 和 Enterprise Mobility + Security 產品時則相對較少發生。 可能發生的指派錯誤僅限於：
- 指派衝突： 在使用者先前已指派與 hello 目前的授權不相容的授權。 在此情況下，hello 新授權指派，需要移除目前 hello。
- 超過可用的授權： hello 分派群組中的使用者數目超過 hello 可用的授權，使用者的指派狀態會反映失敗 tooassign toomissing 授權到期。

### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure AD B2B 共同作業授權

B2B 共同作業可讓您 tooinvite guest 使用者到 Azure AD 租用戶 tooprovide 存取 tooAzure AD 服務和您將提供任何 Azure 資源。  

沒有邀請 B2B 使用者並指派它們 tooan 在 Azure AD 中的應用程式需付費。 針對每個來賓 too10 應用程式設定使用者和 3 的基本報告也是 B2B 共同作業的使用者可以免費。 如果 guest 使用者有任何適當的授權指派 hello 夥伴的 Azure AD 租用戶中，它們將會用您以及授權。

它不是必要，但如果您想 tooprovide 存取 toopaid Azure AD 功能，這些 B2B 來賓使用者必須獲得授權與適當的 Azure AD 授權。 邀請其他租用戶與 Azure AD 的付費授權可以指派 B2B 共同作業的使用者權限受邀 tooan 額外的五個來賓使用者 toohello 租用戶。 如需這方面的案例和資訊，請參閱 [B2B 共同作業授權指引](active-directory-b2b-licensing.md)。

## <a name="view-assigned-licenses"></a>檢視已指派的授權

已指派授權和可用授權的摘要檢視會顯示在 [Azure Active Directory] &gt; [授權] &gt; [所有產品] 下。

![檢視授權摘要](media/license-users-groups/view-license-summary.png)

選取特定產品時，會顯示可用的已指派使用者和群組的詳細清單。 hello**授權使用者**清單會顯示目前耗用一個授權和是否 hello 授權已直接指派 toohello 使用者，或如果它繼承自群組的所有使用者。

![檢視授權詳細資料](media/license-users-groups/view-license-detail.png)

同樣地，hello**授權群組**清單會顯示所有群組已指派給 toowhich 授權。 選取使用者或群組的 tooopen hello**授權**刀鋒視窗中，會顯示所有授權指派給 toothat 物件。

## <a name="remove-a-license"></a>移除授權

tooremove 授權，請移 toohello 使用者或群組，並開啟 hello**授權**磚。 選取 hello 授權，然後按一下 **移除**。

![移除授權](media/license-users-groups/remove-license.png)

無法直接移除繼承自群組的 hello 使用者的授權。 相反地，移除 hello 使用者從他們從中繼承 hello 授權 hello 群組。


## <a name="next-steps"></a>後續步驟
本快速入門中，您學到如何 tooassign 授權 toousers 和 Azure AD 目錄中的群組。 

您可以使用 hello hello Azure 入口網站中的下列 Azure AD 中的連結 tooconfigure 訂用帳戶授權指派。

> [!div class="nextstepaction"]
> [指派 Azure AD 授權](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Overview) 