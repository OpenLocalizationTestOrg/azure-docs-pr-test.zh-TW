---
title: "aaaAzure Active Directory 混合式身分識別設計考量-判斷混合式身分識別生命週期採用策略 |Microsoft 文件"
description: "有助於定義 hello 混合式身分識別管理工作，根據可用的每個生命週期階段 toohello 選項。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 420b6046-bd9b-4fce-83b0-72625878ae71
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 86ec0a9896f069bc93e49e06006954848f8e4d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-hybrid-identity-lifecycle-adoption-strategy"></a>判斷混合式身分識別生命週期採用策略
在這個工作中，您將定義 hello 身分識別管理策略的混合式身分識別方案 toomeet hello 商務需求所定義的[判斷混合式身分識別管理工作](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)。

toodefine hello 混合式身分識別管理工作，根據 toohello 稍早在此步驟中所呈現的端對端的身分識別生命週期，您將會有 tooconsider hello 選項針對每個生命週期階段。

## <a name="access-management-and-provisioning"></a>存取管理和佈建
良好的帳戶存取管理解決方案，您的組織可以追蹤精確 hello 組織內存取 toowhat 資訊。

存取控制是集中式、單點佈建系統的一項重要功能。 存取控制除了保護機密資訊，還能找出未經授權或不再需要的現有帳戶。 toocontrol 過時帳戶 hello hello，使用者擁有 hello 帳戶的授權資訊與佈建系統連結一起帳戶資訊。 Hello 資料庫和人力資源的目錄中，通常會維護授權的使用者身分識別資訊。

複雜的 IT 組織中的帳戶包括數百個定義 hello 授權參數，以及您佈建的系統來控制這些詳細資料。 新的使用者可以識別的 hello hello 授權來源從您提供的資料。 hello 存取要求核准功能起始 hello 處理程序核准 （或拒絕） 加以佈建的資源。

| 生命週期管理階段 | 內部部署 | 雲端 | 混合式 |
| --- | --- | --- | --- |
| 帳戶管理和佈建 |藉由使用 hello Active Directory® 網域服務 (AD DS) 伺服器角色，您可以建立可擴充、 安全且容易管理的基礎結構，為使用者與資源管理，並提供目錄的應用程式，例如 Microsoft® Exchange Server 的支援。 <br><br> [您可以透過身分識別管理員在 AD DS 中佈建群組](https://technet.microsoft.com/library/ff686261.aspx) <br>[ 您可以在 AD DS 中佈建使用者](https://technet.microsoft.com/library/ff686263.aspx) <br><br> 基於安全理由，系統管理員可以使用存取控制 toomanage 使用者存取 tooshared 資源。 存取控制在 hello 物件層級所設定的存取權限，tooobjects 的不同層級中管理在 Active Directory 中，例如完全控制、 寫入、 讀取、 或沒有存取權。 Active Directory 中的存取控制定義不同的使用者如何使用 Active Directory 物件。 根據預設，Active Directory 中的物件權限設定 toohello 最安全的設定。 |您有 toocreate 將存取 Microsoft 雲端服務的每個使用者帳戶。 您也可以變更使用者帳戶，或在已不需要時將它們刪除。 根據預設，使用者沒有系統管理員權限，但是您可以選擇性地指派給他們。 如需詳細資訊，請參閱 [在 Azure AD 中管理使用者](active-directory-create-users.md)。 <br><br> Azure Active directory，其中一個 hello 主要功能是 hello 能力 toomanage 存取 tooresources。 這些資源可以是 hello 目錄中，如同透過角色在 hello 目錄或外部 toohello 目錄，例如 SaaS 應用程式、 Azure services 和 SharePoint 網站或內部部署資源的權限 toomanage 物件 hello 案例的一部分資源。 <br><br> 在 hello 中心的 Azure Active Directory 的存取管理解決方案是 hello 安全性群組。 hello 資源擁有者 （或 hello hello 目錄管理員） 可以指派群組 tooprovide 特定存取權限 toohello 資源他們所擁有。 hello 群組成員的 hello 提供 hello 存取和 hello 資源擁有者可以將委派的其他 – 例如部門經理或技術支援系統管理員群組 toosomeone hello 右 toomanage hello 成員清單<br> <br> Azure AD 主題中的 hello 管理群組會提供有關管理透過群組的存取權的詳細資訊。 |將 Active Directory 身分識別擴充至透過同步和同盟 hello 雲端 |

## <a name="role-based-access-control"></a>角色型存取控制
角色型存取控制 (RBAC) 會使用角色並佈建原則 tooevaluate、 測試和強制執行您的商務程序和規則來授與存取 toousers。 索引鍵的系統管理員建立的佈建原則，並指派使用者 tooroles 和所定義的這些角色的權利 tooresources 集。 RBAC 擴充 hello 身分識別管理解決方案 toouse 軟體式程序，並減少 hello 佈建程序中的使用者手動互動。
Azure AD RBAC 啟用 hello 公司 toorestrict hello 數量他擁有存取 tooAzure 管理入口網站後，可以執行個別的作業。 藉由使用 RBAC toocontrol 存取 toohello 入口網站，使用下列存取管理的 hello 的 IT 系統管理員 ca 委派存取方法：

* **群組為基礎的角色指派**： 可以從本機 Active Directory 指派存取 tooAzure AD 群組可以同步處理。 這可讓您 tooleverage hello 現有的投資，您的組織所做的工具和程序來管理群組。 您也可以使用 Azure AD Premium hello 委派的群組管理功能。
* **利用內建的 Azure 中的角色**： 您可以使用三個角色-使用者和群組具有權限 toodo 只有 hello 工作所需 toodo 工作的擁有者、 參與者和讀取器，tooensure。
* **細微的存取權 tooresources**： 您可以指派角色 toousers 和特定的訂用帳戶、 資源群組或個別的 Azure 資源，例如網站或資料庫群組。 如此一來，您可以確保使用者具有存取 tooall hello 資源所需，就不需要 toomanage 沒有存取 tooresources。

## <a name="provisioning-and-other-customization-options"></a>佈建和其他自訂選項
您的小組可以使用商務計劃和需求 toodecide 多少 toocustomize hello 身分識別解決方案。 例如，大型企業可能需要根據時間表制定分段式推展計劃，以開發工作流程和自訂配接器，漸增地佈建跨地理位置廣泛使用的應用程式。 另一個自訂計劃可能會提供佈建測試成功後的整個組織內的兩個或多個應用程式 toobe。 您可以自訂使用者應用程式互動，並佈建資源的程序可能會變更的 tooaccommodate 自動化佈建。

您可以取消佈建 tooremove 服務或元件。 例如，取消佈建帳戶，表示 hello 帳戶會刪除從資源。

要求和以角色為基礎的方法，可同時支援 Azure ad，結合了 hello 的佈建資源的混合模型。 員工或受管理的系統的子集，企業可能會想使用以角色為基礎的指派 tooautomate 存取。 企業也可以透過要求型的模型，處理其他所有存取要求或例外狀況。 有些企業剛開始會採用手動指派，然後逐漸演化成混合式模型，目標是在未來達到完全角色型的部署。

其他公司可能會發現它並不實用的商業原因 tooachieve 完成角色佈建和目標的混合式方法需要目標。 還是其他公司可能滿意只以要求為基礎的佈建，並不想 tooinvest 額外 toodefine 和管理以角色為基礎、 自動化佈建原則。

## <a name="license-management"></a>授權管理
Azure AD 中的群組為基礎的授權管理可讓系統管理員指派使用者 tooa 安全性群組和 Azure AD 自動會將授權指派 tooall hello hello 群組成員。 如果隨後加入，或從 hello 群組中移除使用者，授權會自動指派或移除依適當情況。

您可以使用您從內部部署 AD 同步處理或在 Azure AD 中管理的群組。 這搭配 Azure AD premium 自助群組管理您可以輕鬆地委派授權指派 toohello 適當決策者。 發生授權衝突和遺失位置資料等問題時，保證會自動解決。

## <a name="self-regulating-user-administration"></a>自我控管使用者管理
當您的組織啟動 tooprovision 資源跨所有的內部組織時，您會實作 hello 自我控管使用者管理功能。 您可以跨組織界限來了解 hello 優點和佈建使用者的優點。 在此環境中，使用者狀態的變更會跨組織界限和地理位置，自動反映在存取權限上。 您可以降低佈建的成本並簡化 hello 存取及核准程序。 hello 實作實現 hello 完整可能會在您的組織中實作的端對端存取管理角色型存取控制。 您可以透過自動化程序來控管使用者佈建，以降低管理成本。 針對大量使用者的情況，您可以自動強制執行安全性原則，簡化並集中化使用者生命週期管理和資源佈建，以改善安全性。

> [!NOTE]
> 如需詳細資訊，請參閱「設定 Azure AD 實現自助式應用程式存取管理」
> 
> 

以授權為基礎 (以權利為基礎) 的 Azure AD 服務的運作方式，是在您的 Azure AD 目錄/服務租用戶中啟用訂用帳戶。 Hello 訂用帳戶項目作用之後就可以由目錄/服務系統管理員管理和使用授權的使用者 hello 服務功能。 如需詳細資訊，請參閱「Azure AD 授權如何運作？
」 與其他協力廠商提供者整合

Azure Active Directory 提供單一登入，並增強應用程式存取安全性 toothousands SaaS 應用程式和內部部署 web 應用程式。 支援的 SaaS 應用程式的 Azure Active Directory 應用程式庫的詳細清單，請參閱 Azure Active Directory 同盟相容性清單： 可能是使用的 tooimplement 協力廠商身分識別提供者單一登入

## <a name="define-synchronization-management"></a>定義同步處理管理
將內部部署目錄與 Azure AD 整合可提供通用身分識別供存取雲端和內部部署資源，進而讓您的使用者更具生產力。 這項整合的使用者和組織可利用的 hello 下列：

* 組織可以跨內部部署或雲端式服務，利用 Windows Server Active Directory，然後連線到 Active Directory tooAzure 提供常見的混合式身分識別的使用者。
* 系統管理員可以根據應用程式資源、裝置和使用者身分識別、網路位置及多因素驗證，提供條件式存取。
* 使用者可以利用 Azure AD tooOffice 365、 Intune、 SaaS 應用程式和協力廠商應用程式中的帳戶透過其通用識別身分。
* 開發人員可以建置運用 hello 常見的身分識別模型，應用程式整合到 Active Directory 內部部署或 Azure 的應用程式，以雲端為基礎的應用程式

hello 圖有一個身分識別同步處理程序的高層級檢視的範例。

![](./media/hybrid-id-design-considerations/identitysync.png)

身分識別同步處理程序

檢閱下列資料表 toocompare hello 同步處理選項的 hello:

| 同步處理管理選項 | 優點 | 缺點 |
| --- | --- | --- |
| 同步型 (透過 DirSync 或 AADConnect) |從內部部署和雲端同步處理的使用者和群組  <br>  **原則控制**： 帳戶原則可以透過 Active Directory，可提供 hello 管理員 hello 能力 toomanage 密碼原則、 工作站、 限制、 鎖定控制，以及詳細資訊，而不需要額外的 tooperform 設定hello 雲端中的工作。  <br>  **存取控制**： 可以限制存取 toohello 雲端服務，使 hello 服務可以透過 hello 企業環境中，透過線上伺服器或兩者來存取。 <br>  減少支援通話： 如果使用者有較少的密碼 tooremember，它們是比較不可能 tooforget 它們。 <br>  安全性： 使用者身分識別和資訊會受到保護，因為所有 hello 伺服器和單一登入中，使用服務主要及控制內部部署。 <br>  支援強力驗證： 您可以使用增強式驗證 （也稱為雙因素驗證） 與 hello 雲端服務。 不過，如果使用增強式驗證，則必須使用單一登入。 | |
| 同盟型 (透過 AD FS) |由 Security Token Service (STS) 啟用。 當您使用 Microsoft 雲端服務設定的 STS tooprovide 單一登入存取時，您將建立您的內部部署 STS 與 Azure AD 租用戶中所指定的 hello 同盟的網域之間的同盟的信任。 <br> 可讓使用者 toouse hello 相同設定的認證 tooobtain 存取 toomultiple 資源 <br>使用者沒有 toomaintain 多組認證。 您尚未，hello 使用者會擁有 tooprovide 其認證 tooeach 一個 hello 參與資源。，B2B 和 B2C 支援的案例。 |需要專業人員來部署及維護專用的內部部署 AD FS 伺服器。 如果您規劃 toouse AD FS STS，有 hello 使用增強式驗證的限制。 如需詳細資訊，請參閱 [設定 AD FS 2.0 的進階選項](http://go.microsoft.com/fwlink/?linkid=235649)。 |

> [!NOTE]
> 如需詳細資訊，請參閱 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
> 
> 

## <a name="see-also"></a>另請參閱
[設計考量概觀](active-directory-hybrid-identity-design-considerations-overview.md)

