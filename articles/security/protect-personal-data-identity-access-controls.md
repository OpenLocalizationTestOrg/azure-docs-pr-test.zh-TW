---
title: "aaaProtect 個人資料與 Azure 身分識別和存取控制項 |Microsoft 文件"
description: "使用 Azure 身分識別和存取控制項 toohelp 保護您的個人資料"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a>Azure Active Directory 和 Multi-factor Authentication：使用身分識別和存取控制來保護個人資料

本文章提供資訊和程序，您可以使用 tooprotect 個人資料使用 Azure Active Directory 和多重要素驗證的安全性功能和服務。

## <a name="scenario"></a>案例

大型出航公司搬遷後 hello 美國，展開在 hello 地中海、 Adriatic，與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。 toosupport 努力，它所取得數個較小的出航行位於義大利，德國、 丹麥和 hello 英國 

hello 公司使用 Microsoft Azure toostore 公司資料 hello 雲端中。 其中包含其全球客戶群的名稱、地址、電話號碼和信用卡資訊等個人識別資訊。 它也會包含在所有位置的傳統的人力資源資訊，例如地址、 電話號碼、 稅務識別碼和醫療公司員工的相關資訊。 hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫，其中包含與目前和過去的客戶的個人資訊 tootrack 關聯性。

位於 hello 世界各地的公司員工存取 hello 網路從 hello 公司遠端辦公室和旅行代理程式已存取 toosome 公司資源。

## <a name="problem-statement"></a>問題陳述

hello 公司必須保護客戶的和員工的個人資料 hello 隱私權的搜尋 toouse 盜用身分 toogain 存取的攻擊者。 它們也必須確定合法使用者將資料限制為只有使用者需要 toodo 該存取 toopersonal 他們的工作。

## <a name="company-goal"></a>公司目標

hello 公司的目標是 tooensure 存取 toopersonal 資料會受到嚴格控制。 請務必識別身分的使用者存取 toopersonal 資料受到強式驗證。 [最小權限] 的原則，讓合法使用者擁有唯一的存取，以及沒有更多的 hello 層級，必須強制執行 (https://en.wikipedia.org/wiki/Principle_of_least_privilege)。

## <a name="solutions"></a>解決方案

Microsoft Azure 提供身分識別和存取管理工具 toohelp 公司控制著具有存取 tooresources 包含個人資料。

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) 管理身分識別，並控制存取 tooAzure，以及其他內部部署其他雲端資源、 資料和應用程式。 [Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)協助 Azure 系統管理員 toominimize hello 許多人都有存取 toocertain 資訊，例如個人資料。 它可讓他們 toodiscover、 限制，並監視特殊權限的身分識別及存取 tooresources 和 tooassign 暫時性的 Just-In-Time (JIT) 系統管理權限 tooeligible 使用者。 它也可供深入了解具有 AAD 系統管理員權限的人員。

在使用 AAD PIM hello 活動包括：

- 為您的目錄啟用 Privileged Identity Management

- 使用 Privileged Identity Management 系統管理儀表板 toosee 重要資訊一目了然

- 新增或移除永久或符合資格的系統管理員 tooeach 角色來管理 hello 特殊權限身分識別 （系統管理員）

- 設定 hello 角色啟用

- 啟用角色

- 檢閱角色活動

#### <a name="how-do-i-enable-aad-pim"></a>如何啟用 ADD PIM？

為您的目錄中，使用 PIM toostart 不要遵循 hello:

1. 登入 toohello Azure 入口網站為您的目錄的全域管理員。

2. 如果您的組織具有多個目錄，選取您的使用者名稱 hello 右上角的 hello Azure 入口網站。 選取您將在其中使用 Azure AD Privileged Identity Management hello 目錄。

3. 選取**更多服務**並用 hello**篩選**文字方塊 toosearch 的 Azure AD Privileged Identity Management。

4. 請檢查**Pin toodashboard** ，然後按一下**建立**。 hello Privileged Identity Management 的應用程式會開啟。

一旦設定 Azure AD Privileged Identity Management 之後，每當您開啟 hello 應用程式時看到 hello 瀏覽 刀鋒視窗。

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

如需開始使用 AAD PIM 的詳細資訊和指示，請參閱[開始使用 Azure AD Privileged Identity Management](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)。

### <a name="azure-role-based-access-control"></a>Azure 角色型存取控制

[Azure 角色型存取控制](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)(RBAC) 可協助管理存取 tooAzure 資源啟用 hello 授與的存取權限 hello 使用者指派角色的 Azure 系統管理員。 您可以隔離小組內的責任，並授與僅 hello 數量存取 toousers、 群組和應用程式，它們必須 tooperform 他們的工作。

可以授與以角色為基礎的存取權 toousers 使用 hello Azure 入口網站、 Azure 命令列工具或 Azure 管理 Api。

如需有關 Azure rbac 進行基本概念的詳細資訊，請參閱[開始使用 hello Azure 入口網站中的 角色型存取控制。](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a>如何使用 PowerShell 管理 Azure RBAC？

您可以使用 PowerShell cmdlet toomanage Azure rbac 進行，包括下列管理工作的 hello:

- 列出角色

- 查看誰具有存取權

- 授與存取權

- 移除存取

- 建立自訂角色

- 取得資源提供者的動作

- 修改自訂角色

- 刪除自訂角色

- 列出自訂角色

如需有關如何 toomanage Azure RBAC 使用 PowerShell，請參閱指示[使用 Azure PowerShell 管理角色為基礎的存取](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell)。

### <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication

[Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) 是協助保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求的兩步驟驗證解決方案。 它可以透過一些驗證方法 (包括電話、文字訊息，或行動應用程式驗證) 來提供強大的驗證功能。

toodeploy MFA hello Azure 雲端中的，您需要 toofirst 啟用它，然後再開啟雙步驟驗證的使用者。

#### <a name="how-do-i-enable-azure-toouse-mfa"></a>如何啟用 Azure toouse MFA？

如果您的使用者包括 Azure Multi-factor Authentication Server 的授權，並沒有您需要 Azure MFA 上的 toodo tooturn。 如果沒有，您需要在您的目錄中的 toocreate Multi-factor Auth 提供者。 toodo，請遵循下列步驟：

1. 選取**Active Directory** hello Azure 傳統入口網站 （登入為系統管理員） 中。

2. 選取 [Multi-Factor Authentication Provider]。

3. 選取 [新增]，然後在 [應用程式服務] 之下，選取 [Multi-Factor Auth Provider]。

4. 選取 [快速建立]。

5. 填寫 hello 名稱 欄位中，選取 （每次驗證或每個啟用的使用者） 的使用方式模型。

6. 指定哪些 hello MFA 提供者所關聯的目錄。

7. 按一下 hello**建立** 按鈕。

![](media/protect-personal-data-identity-access-controls/quick-create.png)

如需有關的詳細指示 toomanage 您 Multi-factor Auth 提供者，請參閱[開始使用 Azure Multi-factor Auth 提供者。](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a>如何對使用者開啟雙步驟驗證？

您可以強制執行雙步驟驗證的所有登入，或您在特定條件時，才可以建立條件式存取原則 toorequire 雙步驟驗證。

Azure MFA 啟用藉由變更使用者的狀態是 hello 要求雙步驟驗證的傳統方式。 您所啟用的所有 hello 使用者都會都將每次登入時 hello 相同需求 tooperform 雙步驟驗證。 啟用使用者的效力會凌駕任何可能影響該使用者的條件式存取原則。

使用條件式存取原則來啟用 Azure MFA 是用來要求使用雙步驟驗證的更彈性方法。 您可以建立適用於 toogroups 與個別使用者的條件式存取原則。 您可以對高風險群組施加比低風險群組更多的限制，或者，也可以只針對高風險雲端應用程式要求雙步驟驗證，至於低風險的雲端應用程式則略過雙步驟驗證。 不過，條件式存取是 Azure Active Directory 的付費功能。

tooenable MFA 藉由變更使用者狀態，請勿 hello 遵循：

1. Toohello Azure 入口網站管理員身分登入。
2. 跳過**Azure Active Directory\>使用者和群組\>所有使用者**。
3. 選取 [多重要素驗證]。
4. 您為 Azure MFA 想 tooenable 尋找 hello 使用者。 您可能需要 toochange hello hello 頂端的檢視。
5. 請檢查 hello 方塊下一步 toohello 使用者的名稱。
6. 在 hello 右下快速步驟，選擇**啟用**。

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. 確認您的選擇會開啟 hello 快顯視窗中。  針對已啟用 MFA 的使用者將會詢問 tooregister hello 下一次登入。

條件式存取原則，tooenable Azure MFA 進行 hello 遵循：

1. Toohello Azure 入口網站管理員身分登入。

2. 跳過**Azure Active Directory\>條件式存取**。

3. 選取 [新增原則]。

4. 在 [指派] 底下選取 [使用者和群組]。 使用 hello **Include**和**排除**toospecify hello 原則將管理哪些使用者和群組的索引標籤。

5. 在 [指派] 底下選取 [雲端應用程式]。 選擇太**包含所有雲端應用程式**。
6.  在 [存取控制] 底下選取 [授與]。 選擇 [需要多重要素驗證]。
7.  開啟**啟用原則**太**上**，然後選取 **儲存**。

如需如何設定詐騙警示 tooconfigure Azure MFA 設定 tooset 建立單次許可時，使用自訂語音訊息、 設定快取、 指定受信任的 Ip、 建立應用程式密碼、 啟用記住裝置信任的使用者，並選取 MFA驗證方法，請參閱[設定 Azure Multi-factor Authentication 設定。](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)

## <a name="next-steps"></a>後續步驟

- [保護 Azure AD 中的特殊權限存取](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [與 Azure Multi-Factor Authentication 相關的常見問題](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [角色型存取控制疑難排解](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
