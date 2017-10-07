---
title: "教學課程︰以內部部署 Active Directory 和 Azure Active Directory 設定自動化使用者佈建的 Workday | Microsoft Docs"
description: "深入了解如何 toouse Workday 的 Active Directory 和 Azure Active Directory 身分識別資料來源。"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a>教學課程︰以內部部署 Active Directory 和 Azure Active Directory 設定自動化使用者佈建的 Workday
本教學課程的 hello 目標是 tooshow hello 到 Active Directory 和 Azure Active Directory，必須使用選擇性的回寫的某些屬性 tooWorkday tooperform tooimport 人從 Workday 步驟。 



## <a name="overview"></a>概觀

hello[佈建服務的 Azure Active Directory 使用者](active-directory-saas-app-provisioning.md)hello 與整合[Workday 人力資源應用程式開發介面](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html)中排序 tooprovision 使用者帳戶。 Azure AD 會使用此連接 tooenable hello 遵循使用者佈建工作流程：

* **佈建使用者 tooActive 目錄**-到一或多個 Active Directory 樹系同步處理選取的使用者集合將 Workday 中。 

* **僅限雲端的使用者 tooAzure Active Directory 佈建**-存在於 Active Directory 和 Azure Active Directory 的混合式使用者可以佈建到 hello 後者使用[AAD Connect](connect/active-directory-aadconnect.md)。 不過，僅限雲端的使用者可以直接從 Workday tooAzure Active Directory 使用 hello 佈建服務的 Azure AD 使用者佈建。

* **電子郵件的回寫位址 tooWorkday** -hello Azure AD 使用者佈建服務可以撰寫選取 Azure AD 使用者屬性後的 tooWorkday，例如 hello 電子郵件地址。

### <a name="scenarios-covered"></a>涵蓋的案例

hello Workday 使用者佈建 hello Azure AD 使用者佈建服務所支援的工作流程可讓 hello 下列人力資源和身分識別生命週期管理案例的自動化：

* **雇用的員工**-tooWorkday，加入新的員工時在 Active Directory、 Azure Active Directory 和 Office 365 （選擇性） 將會自動建立使用者帳戶和[支援 Azure AD 的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)，寫入 hello 電子郵件地址 tooWorkday 背面。

* **員工屬性和設定檔更新** - 在 Workday 中更新員工記錄時 (例如姓名、職稱或經理)，系統會在 Active Directory、Azure Active Directory、Office 365 (選擇性) 和 [Azure AD 支援的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)中自動更新其使用者帳戶。

* **員工離職** - 在 Workday 中將員工設定為離職時，系統會在 Active Directory、Azure Active Directory、Office 365 (選擇性) 和 [Azure AD 支援的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)中自動停用其使用者帳戶。

* **重新雇用的員工**-當員工 rehired workday，舊的帳戶可以自動重新啟動或重新佈建 （取決於您的喜好設定） tooActive 目錄、 Azure Active Directory，並選擇性地 Office 365 和[支援 Azure AD 的其他 SaaS 應用程式](active-directory-saas-app-provisioning.md)。


## <a name="planning-your-solution"></a>規劃您的解決方案

開始之前您的 Workday 整合，確認下列和讀取 hello 下列指引的 hello 必要條件 toomatch 您目前的 Active Directory 架構和使用者佈建需求與 hello 方案提供的 Azure Active目錄。

### <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

* 具有全域系統管理員存取權的有效 Azure AD Premium P1 訂用帳戶
* 可供測試和整合之用的 Workday 實作租用戶
* 在 Workday toocreate 系統整合使用者的系統管理員權限和基於測試目的請變更 tootest 員工資料
* 使用者佈建 tooActive 目錄，2012年或更新版本執行 Windows 服務已加入網域的伺服器是需要的 toohost hello[在內部部署同步處理代理程式](https://go.microsoft.com/fwlink/?linkid=847801)
* 可在 Active Directory 與 Azure AD 之間同步處理的 [Azure AD Connect](connect/active-directory-aadconnect.md)

> [!NOTE]
> 如果您的 Azure AD 租用戶位於歐洲，請參閱 hello[已知問題](#known-issues)下一節。


### <a name="solution-architecture"></a>方案架構

Azure AD 提供一組豐富的佈建連接器 toohelp 解決佈建和身分識別生命週期管理從 Workday tooActive 目錄中，Azure AD，SaaS 應用程式和更新版本。 哪些功能您將使用，而且設定 hello 方案的方式會根據您的組織環境和需求而有所不同。 第一個步驟中，採用 hello 下列數量的確實存在且已部署在組織中的內的建：

* 您正在使用多少 Active Directory 樹系？
* 您正在使用多少 Active Directory 網域？
* 有多少 Active Directory 組織單位 (OU) 正在使用？
* 有多少 Azure Active Directory 租用戶正在使用？
* 有需要佈建 toobe tooboth Active Directory 與 Azure Active Directory （例如 「 混合 」 使用者） 的使用者嗎？
* 有需要佈建 toobe tooAzure Active Directory，但沒有 Active Directory （例如 「 僅限雲端的 「 使用者） 的使用者嗎？
* 使用者電子郵件地址需要寫回 tooWorkday toobe 嗎？

答案 toothese 問題之後，您可以規劃佈建部署下列 hello 準則工作日。

#### <a name="using-provisioning-connector-apps"></a>使用佈建連接器應用程式

Azure Active Directory 支援適用於 Workday 和大量其他 SaaS 應用程式的預先整合佈建連接器。 

單一的佈建連接器以單一來源系統的 hello API 介面，並協助佈建資料 tooa 單一目標系統。 大部分 Azure AD 支援的佈建連接器為單一來源和目標系統 (例如 Azure AD tooServiceNow)，可能會安裝程式只需加 hello 應用程式有問題從 hello Azure AD app 資源庫 (例如 ServiceNow)。 

在 Azure AD 中佈建連接器執行個體與應用程式執行個體之間具有一對一關聯性：

| 來源系統 | 目標系統 |
| ---------- | ---------- | 
| Azure AD 租用戶 | SaaS 應用程式 |


不過，當使用 Workday 和 Active Directory，會視為的多個來源和目標系統 toobe:

| 來源系統 | 目標系統 | 注意事項 |
| ---------- | ---------- | ---------- |
| Workday | Active Directory 樹系 | 系統會將每個樹系視為相異目標系統 |
| Workday | Azure AD 租用戶 | 根據僅限雲端使用者的要求 |
| Active Directory 樹系 | Azure AD 租用戶 | 目前由 AAD Connect 處理此流程 |
| Azure AD 租用戶 | Workday | 適用於電子郵件地址的回寫 |

toofacilitate 這些多個工作流程 toomultiple 來源和目標系統，Azure AD 提供多個佈建連接器應用程式，您可以從 hello Azure AD app 資源庫加入：

![AAD 應用程式庫](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* **目錄佈建的 workday tooActive** -此應用程式可協助從 Workday tooa 單一 Active Directory 樹系佈建的使用者帳戶。 如果您有多個樹系，您可以從每個 Active Directory 樹系需要以 tooprovision hello Azure AD app 資源庫來新增此應用程式的一個執行個體。

* **Workday tooAzure AD 佈建**-雖然 AAD Connect 是 hello 工具應該使用的 toosynchronize Active Directory 使用者 tooAzure Active Directory，此應用程式可能會使用的 toofacilitate 從 Workday tooa 單一的僅限雲端的使用者佈建Azure Active Directory 租用戶。

* **Workday 的回寫**-此應用程式可協助從 Azure Active Directory tooWorkday 使用者的電子郵件地址的回寫。

> [!TIP]
> hello 規則 」 Workday 」 應用程式用來設定單一登入 Workday 與 Azure Active Directory 之間。 

如何 tooset 安裝及設定這些特殊佈建連接器應用程式 」 是 hello hello 剩餘各節，本教學課程的主題。 哪些應用程式，您可以選擇 tooconfigure 將取決於您的系統上需要 tooprovision，以及多少 Active Directory 樹系與 Azure AD 租用戶不在您的環境中。

![概觀](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a>在 Workday 中設定系統整合使用者
所有 hello Workday 佈建連接器的常見的需求是它們需要認證的 Workday 系統整合帳戶 tooconnect toohello Workday 人力資源應用程式開發介面。 本章節描述 toocreate 系統整合者 Workday 中的帳戶。

> [!NOTE]
> 它是可能 toobypass 此程序，並以 hello 系統整合帳戶改用 Workday 全域管理員帳戶。 這可能會在示範中正常運作，但不建議用於生產環境部署。

### <a name="create-an-integration-system-user"></a>建立整合系統使用者

**toocreate 整合系統使用者：**

1. 使用系統管理員帳戶登入 Workday 租用戶。 在 hello **Workday Workbench**，輸入在 hello 搜尋方塊中，建立使用者，然後按一下**建立整合系統使用者**。 
   
    ![建立使用者](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "建立使用者")
2. 完整的 hello**建立整合系統使用者**藉由提供使用者名稱和密碼為新的整合系統使用者的工作。  
 * 保留 hello**在下次登入時要求新密碼**選項未選取，因為這個使用者會登入以程式設計的方式。 
 * 保留 hello**工作階段逾時分鐘數**其預設值是 0，這可以防止 hello 使用者工作階段提前逾時。 
   
    ![建立整合系統使用者](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "建立整合系統使用者")

### <a name="create-a-security-group"></a>建立安全性群組
您需要 toocreate 受限的整合系統安全性群組，並指派 hello 使用者 tooit。

**toocreate 安全性群組：**

1. 輸入在 hello 搜尋方塊中，建立安全性群組，然後按一下**建立安全性群組**。 
   
    ![建立安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "建立安全性群組")
2. 完整的 hello**建立安全性群組**工作。  
3. 選取整合系統安全性群組 — 未受限從 hello**類型的安全性群組**下拉式清單。
4. 建立安全性群組 toowhich 明確加入成員。 
   
    ![建立安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "建立安全性群組")

### <a name="assign-hello-integration-system-user-toohello-security-group"></a>指派 hello 整合系統使用者 toohello 安全性群組

**tooassign hello 整合系統使用者：**

1. 在 [hello] 搜尋方塊中，輸入編輯安全性群組，然後按一下**編輯安全性群組**。 
   
    ![編輯安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "編輯安全性群組")
2. 搜尋，並依名稱選取 hello 新整合的安全性群組。 
   
    ![編輯安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "編輯安全性群組")
3. 新增 hello 新整合系統使用者 toohello 新安全性群組。 
   
    ![系統安全性群組](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "系統安全性群組")  

### <a name="configure-security-group-options"></a>設定安全性群組選項
在此步驟中，您將授與 toohello 新的安全群組的權限**取得**和**放**hello 下列網域安全性原則所保護的 hello 物件上的作業：

* 外部帳戶佈建
* 人員資料：公用人員報告
* 人員資料：所有職位
* 人員資料：目前人員配置資訊
* 人員資料：人員個人檔案的職稱

**tooconfigure 安全性群組選項：**

1. Hello 搜尋方塊中，輸入網域安全性原則，然後按一下 hello 連結**功能區域的網域安全性原則**。  
   
    ![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "網域安全性原則")  
2. 搜尋系統和選取 hello**系統**功能區域。  按一下 [確定] 。  
   
    ![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "網域安全性原則")  
3. 在 [hello] 清單中的 hello 系統功能區域的安全性原則，依序展開**安全性管理**hello 網域安全性原則並加以選取**外部帳戶佈建**。  
   
    ![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "網域安全性原則")  
4. 按一下**編輯權限**，然後在 hello**編輯權限**對話方塊頁面上，新增 hello 新安全性群組 toohello 安全性群組清單與**取得**和**放**整合權限。 
   
    ![編輯權限](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "編輯權限")  
5. 重複步驟 1 選取的功能區域，tooreturn toohello 螢幕上，再搜尋人員配置，這次選取 hello**人員配置 功能區域**按一下**確定**。
   
    ![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "網域安全性原則")  
6. 在 hello 清單中的 hello 人員配置 功能區域的安全性原則，依序展開**工作者資料： 人員配置**和重複上述步驟 4 的每一種剩餘的安全性原則：

   * 人員資料：公用人員報告
   * 人員資料：所有職位
   * 人員資料：目前人員配置資訊
   * 人員資料：人員個人檔案的職稱
   
7. 重複步驟 1 所選取的功能區域的 tooreturn toohello 螢幕上，這次搜尋**連絡人資訊**選取 hello 人員配置 功能區域，然後按一下**確定**。

8.  在 hello 清單中的 hello 人員配置 功能區域的安全性原則，依序展開**工作者資料： 工作的連絡資訊**，並重複上述步驟 4 hello 安全性原則下：

    * 人員資料：公司電子郵件

    ![網域安全性原則](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "網域安全性原則")  
    
### <a name="activate-security-policy-changes"></a>啟用安全性原則變更

**tooactivate 安全性原則變更：**

1. 輸入啟動 hello 搜尋 方塊中，然後按一下 hello 連結**啟動擱置安全性原則變更**。 
   
    ![啟用](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "啟用") 
2. 啟動擱置安全性原則變更為稽核用途，輸入註解工作，然後按一下開始 hello**確定**。 
   
    ![啟用擱置的安全性](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "啟用擱置的安全性")   
3. Hello 藉由檢查 hello 核取方塊的下一個畫面上的完整 hello 工作**確認**，然後按一下**確定**。 
   
    ![啟用擱置的安全性](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "啟用擱置的安全性")  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a>設定使用者佈建從 Workday tooActive 目錄
請遵循這些指示 tooconfigure 使用者帳戶佈建從 Workday tooeach 您需要佈建的 Active Directory 樹系。

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>第 1 部分： 加入 hello 佈建的連接器應用程式和建立 hello 連接 tooWorkday

**tooconfigure Workday tooActive 目錄佈建：**

1.  跳過<https://portal.azure.com>

2.  在 hello 左的導覽列中，選取  **Azure Active Directory**

3.  依序選取 [企業應用程式] 和 [所有應用程式]。

4.  選取**新增應用程式**，並選取 hello**所有**類別目錄。

5.  搜尋**Workday 佈建 tooActive 目錄**，並從 hello 組件庫中加入該應用程式。

6.  Hello 之後加入的應用程式，而且會顯示 hello 應用程式詳細資料 畫面中，選取**佈建**

7.  變更 hello**佈建****模式**太**自動**

8.  完整的 hello**系統管理員認證**區段，如下所示：

   * **系統管理員使用者名稱**– 附加 hello 租用戶網域名稱輸入 hello hello Workday 的整合系統帳戶，使用者名稱。 **其應該類似於：username@contoso4**

   * **系統管理員密碼 –** Enter hello hello Workday 的整合系統帳戶密碼

   * **租用戶 URL-**輸入您的租用戶 hello URL toohello Workday web 服務端點。 這應該看起來： https://wd3-impl-services1.workday.com/ccx/service/contoso4 其中 contoso4 會取代您正確租用戶的名稱，而 wd3 impl 取代 hello 正確環境字串。

   * **Active Directory 樹系-** hello hello Get ADForest powershell 指令程式所傳回的 「 名稱 」 您的 Active Directory 樹系。 此字串通常類似於：*contoso.com*

   * **Active Directory 容器-**輸入 hello 容器字串，其中包含您的 AD 樹系中的所有使用者。 範例：*OU=Standard Users,OU=Users,DC=contoso,DC=test*

   * **電子郵件通知 –** 輸入您的電子郵件地址，然後勾選 [發生失敗時傳送電子郵件] 核取方塊。

   * 按一下 hello**測試連接** 按鈕。 如果 hello 連接測試成功，按一下 hello**儲存**hello 頂端的按鈕。 如果失敗，請仔細檢查 hello 的 Workday 認證會在 Workday 中有效。 

![Azure 入口網站](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a>第 2 部分：設定屬性對應 

在本節中，您會設定使用者資料從 Workday 流動至 Active Directory 的方式。

1.  在 hello 佈建索引標籤下**對應**，按一下 **同步處理新的 Workday 工作者 tooOnPremises**。

2.  在 hello**來源物件範圍**欄位，您可以選取 在 Workday 中的使用者將應該提供 tooAD，藉由定義一組屬性為基礎的篩選條件的範圍內。 hello 預設範圍為 「 Workday 中的所有使用者 」。 範例篩選：

   * 範例： 範圍 toousers 以背景工作識別碼 2000000 1000000 之間

      * 屬性：WorkerID

      * 運算子：REGEX Match

      * 值：(1[0-9][0-9][0-9][0-9][0-9][0-9])

   * 範例：僅員工和非約聘人員 

      * 屬性：EmployeeID

      * 運算子：IS NOT NULL

3.  在 hello**目標物件動作**欄位，您可以全域篩選允許 toobe Active Directory 上執行哪些動作。 最常見的動作是 [建立] 和 [更新]。

4.  在 [hello**屬性對應**] 區段中，您可以定義如何個別 Workday 對應 tooActive 目錄屬性的屬性。

5. 按一下現有的屬性對應 tooupdate，或是按一下**加入新的對應**底部 hello hello 螢幕 tooadd 新對應。 個別屬性對應支援下列屬性：

      * **對應類型**

         * **直接**– 寫入 hello hello Workday 屬性 toohello AD 具有屬性值，任何變更

         * **常數**-將靜態、 常數字串值寫入至 hello AD 屬性

         * **運算式**– 可讓您 toowrite hello AD 屬性，根據一個或多個新的 Workday 屬性的自訂值。 [如需詳細資訊，請參閱這篇有關運算式的文章](active-directory-saas-writing-expressions-for-attribute-mappings.md)。

      * **來源屬性**-從 Workday hello 使用者屬性。

      * **預設值** – 選用。 如果 hello 來源屬性的值是空的 hello 對應會改為寫入此值。
            此空白 tooleave 最常見的組態。

      * **目標屬性**– Active Directory 中的 hello 使用者屬性。

      * **符合使用此屬性的物件**– 是否應使用此對應 toouniquely 識別 Workday 與 Active Directory 之間的使用者。 這通常是背景工作 ID 欄位上設定，workday，通常會對應至其中一個 Active Directory 中的 hello 員工識別碼屬性。

      * **比對優先順序** – 您可以設定多個比對屬性。 具有多個屬性時，系統會以此欄位定義的順序進行評估。 只要找到相符項目，便不會評估進一步比對屬性。

      * **套用此對應**
       
         * **一律** – 將此對應套用於使用者建立和更新動作

         * **僅限建立期間** - 僅將此對應套用於使用者建立動作

6. toosave 對應時，按一下**儲存**頂端 hello 屬性對應的區段。

![Azure 入口網站](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

**下列為 Workday 與 Active Directory 之間的一些範例屬性對應，以及一些常用運算式**

-   對應 toohello parentDistinguishedName AD 屬性的 hello 運算式可以是使用的 tooprovision 使用者 tooa 特定 OU 根據一個或多個新的 Workday 來源屬性。 此範例會根據使用者在 Workday 中的城市資料，將其置於不同的 OU。

-   對應 toohello userPrincipalName AD 屬性的 hello 運算式建立的 UPN firstName.LastName@contoso.com。其也會取代不合法的特殊字元。

-   [此為有關撰寫運算式的文件](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| WORKDAY 屬性 | ACTIVE DIRECTORY 屬性 |  比對識別碼？ | 建立/更新 |
| ---------- | ---------- | ---------- | ---------- |
|  **WorkerID**  |  EmployeeID | **是** | 僅於建立時寫入 | 
|  **Municipality**   |   l   |     | 建立 + 更新 |
|  **Company**         | company   |     |  建立 + 更新 |
|  **CountryReferenceTwoLetter**      |   co |     |   建立 + 更新 |
| **CountryReferenceTwoLetter**    |  c  |     |         建立 + 更新 |
| **SupervisoryOrganization**  | department  |     |  建立 + 更新 |
|  **PreferredNameData**  |  displayName |     |   建立 + 更新 |
| **EmployeeID**    |  cn    |   |   僅於建立時寫入 |
| **Fax**      | facsimileTelephoneNumber     |     |    建立 + 更新 |
| **名字**   | givenName       |     |    建立 + 更新 |
| **Switch(\[Active\], , "0", "True", "1",)** |  accountDisabled      |     | 建立 + 更新 |
| **Mobile**  |    mobile       |     |       僅於建立時寫入 |
| **EmailAddress**    | mail    |     |     建立 + 更新 |
| **ManagerReference**   | manager  |     |  建立 + 更新 |
| **WorkSpaceReference** | physicalDeliveryOfficeName    |     |  建立 + 更新 |
| **PostalCode**  |   postalCode  |     | 建立 + 更新 |
| **LocalReference** |  preferredLanguage  |     |  建立 + 更新 |
| **Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\|\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)*$)", , "", , )**      |    sAMAccountName            |     |         僅於建立時寫入 |
| **姓氏**   |   sn   |     |  建立 + 更新 |
| **CountryRegionReference** |  st     |     | 建立 + 更新 |
| **AddressLineData**    |  streetAddress  |     |   建立 + 更新 |
| **PrimaryWorkTelephone**  |  telephoneNumber   |     | 僅於建立時寫入 |
| **BusinessTitle**   |  title     |     |  建立 + 更新 |
| **Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**   | userPrincipalName     |     | 建立 + 更新                                                   
| **Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**  | parentDistinguishedName     |     |  建立 + 更新 |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a>第 3 部分： Hello 在內部部署同步處理代理程式設定

在訂單 tooprovision tooActive 目錄在內部，必須 hello desire Active Directory 樹系中網域的伺服器上安裝代理程式。 網域系統管理員 （或企業系統管理員） 完成 hello 程序所需的認證。

**[您可以下載 hello 在內部部署同步處理代理程式在此](https://go.microsoft.com/fwlink/?linkid=847801)**

安裝代理程式之後, 執行以下 tooconfigure hello 代理程式，您的環境的 hello Powershell 命令。

**命令 1**

> cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent

> import-module AADSyncAgent.psd1

**命令 2**

> Add-ADSyncAgentActiveDirectoryConfiguration

* 輸入： 針對 [目錄名稱] 輸入 hello AD 樹系名稱，如同部分輸入\#2
* 輸入：Active Directory 樹系的系統管理員使用者名稱和密碼

**命令 3**

> Add-ADSyncAgentAzureActiveDirectoryConfiguration

* 輸入：Azure AD 租用戶的全域系統管理員使用者名稱和密碼

**命令 4**

> Get-AdSyncAgentProvisioningTasks

* 動作：確認已傳回資料。 此命令會自動探索 Azure AD 租用戶中的 Workday 佈建應用程式。 範例輸出︰

> 名稱：我的 AD 樹系
>
> 已啟用：True
>
> DirectoryName：mydomain.contoso.com
>
> 已認證：False
>
> 識別碼：WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203

**命令 5**

> Start-AdSyncAgentSynchronization -Automatic

**命令 6**

> net stop aadsyncagent

**命令 7**

> net start aadsyncagent

### <a name="part-4-start-hello-service"></a>第 4 部分： 啟動 hello 服務
當組件 1-3 已完成之後時，您可以開始佈建服務 hello Azure 管理入口網站中的 hello。

1.  在 hello**佈建**索引標籤，設定 hello**佈建狀態**至**上**。

2. 按一下 [儲存] 。

3. 這會啟動 hello 初始同步處理，這可能要花費數小時取決於使用者人數會 workday。

4. 個別同步處理的事件，例如哪些使用者會讀出 Workday，以及之後加入或已更新 tooActive 目錄，然後可以在 hello 檢視**稽核記錄檔** 索引標籤。**[請參閱 hello 佈建上 tooread hello 稽核記錄的方式的詳細指示的報告指南](active-directory-saas-provisioning-reporting.md)**

5.  hello hello 代理程式電腦上的 Windows 應用程式記錄檔會顯示透過 hello 代理程式執行的所有作業。

6. 完成之後，其會寫入 [佈建] 索引標籤中的稽核摘要報告內，如下所示。

![Azure 入口網站](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a>設定使用者佈建 tooAzure Active Directory
設定佈建 tooAzure Active Directory 的方式將取決於您佈建的需求，在 hello 表中所述。

| 案例 | 方案 |
| -------- | -------- |
| **使用者需要佈建 toobe tooActive 目錄與 Azure AD** | 使用 **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **使用者需要佈建 toobe tooActive 目錄只** | 使用 **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **使用者需要佈建 toobe tooAzure AD 唯一 （僅限雲端）** | 使用 hello **Workday tooAzure Active Directory 佈建**hello 應用程式庫中的應用程式 |

如需設定 Azure AD Connect 的指示，請參閱 hello [Azure AD Connect 文件](connect/active-directory-aadconnect.md)。

hello 下列各節描述如何設定 Workday 和 Azure AD tooprovision 僅限雲端的使用者之間的連線。

> [!IMPORTANT]
> 如果您需要佈建 toobe tooAzure AD 和不在內部部署 Active Directory 的僅限雲端的使用者，只能後面 hello 的下列程序。

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>第 1 部分： 加入 hello Azure AD 佈建的連接器應用程式和建立 hello 連接 tooWorkday

**tooconfigure Workday tooAzure Active Directory 佈建為僅限雲端的使用者：**

1.  跳過<https://portal.azure.com>。

2.  在 hello 左的導覽列中，選取  **Azure Active Directory**

3.  依序選取 [企業應用程式] 和 [所有應用程式]。

4.  選取**新增應用程式**，然後選取 hello**所有**類別目錄。

5.  搜尋**Workday tooAzure AD 佈建**，並從 hello 組件庫中加入該應用程式。

6.  Hello 之後加入的應用程式，而且會顯示 hello 應用程式詳細資料 畫面中，選取**佈建**

7.  變更 hello**佈建****模式**太**自動**

8.  完整的 hello**系統管理員認證**區段，如下所示：

   * **系統管理員使用者名稱**– 附加 hello 租用戶網域名稱輸入 hello hello Workday 的整合系統帳戶，使用者名稱。 其應該類似於：username@contoso4

   * **系統管理員密碼 –** Enter hello hello Workday 的整合系統帳戶密碼

   * **租用戶 URL-**輸入您的租用戶 hello URL toohello Workday web 服務端點。 這應該看起來： https://wd3-impl-services1.workday.com/ccx/service/contoso4 其中 contoso4 會取代您正確租用戶的名稱，而 wd3 impl 會取代 hello 正確環境字串 （如有必要）。

   * **電子郵件通知 –** 輸入您的電子郵件地址，然後勾選 [發生失敗時傳送電子郵件] 核取方塊。

   * 按一下 hello**測試連接** 按鈕。

   * 如果 hello 連接測試成功，按一下 hello**儲存**hello 頂端的按鈕。 如果失敗，，再次該 hello Workday 的 URL 是 Workday 中的有效認證。


### <a name="part-2-configure-attribute-mappings"></a>第 2 部分：設定屬性對應 

在本節中，您會針對僅限雲端使用者設定使用者資料從 Workday 流動至 Azure Active Directory 的方式。

1.  在 hello 佈建索引標籤下**對應**，按一下 **同步處理的背景工作 tooAzure AD**。

2.   在 hello**來源物件範圍**欄位，您可以選取 Workday 中的使用者將應該提供 tooAzure AD，藉由定義一組屬性為基礎的篩選條件的範圍內。 hello 預設範圍為 「 Workday 中的所有使用者 」。 範例篩選：

   * 範例： 範圍 toousers 以背景工作識別碼 2000000 1000000 之間

      * 屬性：WorkerID

      * 運算子：REGEX Match

      * 值：(1[0-9][0-9][0-9][0-9][0-9][0-9])

   * 範例：僅約聘人員和非正式員工

      * 屬性：ContingentID

      * 運算子：IS NOT NULL

3.  在 hello**目標物件動作**欄位，您可以全域篩選允許 toobe 在 Azure AD 上執行哪些動作。 最常見的動作是 [建立] 和 [更新]。

4.  在 [hello**屬性對應**] 區段中，您可以定義如何個別 Workday 對應 tooActive 目錄屬性的屬性。

5. 按一下現有的屬性對應 tooupdate，或是按一下**加入新的對應**底部 hello hello 螢幕 tooadd 新對應。 個別屬性對應支援下列屬性：

   * **對應類型**

      * **直接**– 寫入 hello hello Workday 屬性 toohello AD 具有屬性值，任何變更

      * **常數**-將靜態、 常數字串值寫入至 hello AD 屬性

      * **運算式**– 可讓您 toowrite hello AD 屬性，根據一個或多個新的 Workday 屬性的自訂值。 [如需詳細資訊，請參閱這篇有關運算式的文章](active-directory-saas-writing-expressions-for-attribute-mappings.md)。

   * **來源屬性**-從 Workday hello 使用者屬性。

   * **預設值** – 選用。 如果 hello 來源屬性的值是空的 hello 對應會改為寫入此值。
            此空白 tooleave 最常見的組態。

   * **目標屬性**– 在 Azure AD 中的 hello 使用者屬性。

   * **符合使用此屬性的物件**– 是否應使用此對應 toouniquely 識別 Workday 與 Azure AD 之間的使用者。 這通常是背景工作 ID 欄位上設定，workday，通常在 Azure AD 中對應至 hello 員工 ID 屬性 （新） 或延伸模組屬性。

   * **比對優先順序** – 您可以設定多個比對屬性。 具有多個屬性時，系統會以此欄位定義的順序進行評估。 只要找到相符項目，便不會評估進一步比對屬性。

   * **套用此對應**

     * **一律** – 將此對應套用於使用者建立和更新動作

     * **僅限建立期間** - 僅將此對應套用於使用者建立動作

6. toosave 對應時，按一下**儲存**頂端 hello 屬性對應的區段。

### <a name="part-3-start-hello-service"></a>第 3 部分： 啟動 hello 服務
當組件 1-2 已經完成時，您可以開始佈建服務的 hello。

1.  在 hello**佈建**索引標籤，設定 hello**佈建狀態**至**上**。

2. 按一下 [儲存] 。

3. 這會啟動 hello 初始同步處理，這可能要花費數小時取決於使用者人數會 workday。

4. 可以檢視個別的同步處理事件，在 hello**稽核記錄檔** 索引標籤。**[請參閱 hello 佈建上 tooread hello 稽核記錄的方式的詳細指示的報告指南](active-directory-saas-provisioning-reporting.md)**

5. 完成之後，其會寫入 [佈建] 索引標籤中的稽核摘要報告內，如下所示。


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a>設定電子郵件地址 tooWorkday 的回寫
從 Azure Active Directory tooWorkday 遵循這些指示 tooconfigure 回寫的使用者電子郵件地址。

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>第 1 部分： 加入 hello 佈建的連接器應用程式和建立 hello 連接 tooWorkday

**tooconfigure Workday tooActive 目錄佈建：**

1.  跳過<https://portal.azure.com>

2.  在 hello 左的導覽列中，選取  **Azure Active Directory**

3.  依序選取 [企業應用程式] 和 [所有應用程式]。

4.  選取**新增應用程式**，然後選取 hello**所有**類別目錄。

5.  搜尋**Workday 回寫**，並從 hello 組件庫中加入該應用程式。

6.  Hello 之後加入的應用程式，而且會顯示 hello 應用程式詳細資料 畫面中，選取**佈建**

7.  變更 hello**佈建****模式**太**自動**

8.  完整的 hello**系統管理員認證**區段，如下所示：

   * **系統管理員使用者名稱**– 附加 hello 租用戶網域名稱輸入 hello hello Workday 的整合系統帳戶，使用者名稱。 其應該類似於：username@contoso4

   * **系統管理員密碼 –** Enter hello hello Workday 的整合系統帳戶密碼

   * **租用戶 URL-**輸入您的租用戶 hello URL toohello Workday web 服務端點。 這應該看起來： https://wd3-impl-services1.workday.com/ccx/service/contoso4 其中 contoso4 會取代您正確租用戶的名稱，而 wd3 impl 會取代 hello 正確環境字串 （如有必要）。

   * **電子郵件通知 –** 輸入您的電子郵件地址，然後勾選 [發生失敗時傳送電子郵件] 核取方塊。

   * 按一下 hello**測試連接** 按鈕。 如果 hello 連接測試成功，按一下 hello**儲存**hello 頂端的按鈕。 如果失敗，，再次該 hello Workday 的 URL 是 Workday 中的有效認證。


### <a name="part-2-configure-attribute-mappings"></a>第 2 部分：設定屬性對應 


在本節中，您會設定使用者資料從 Workday 流動至 Active Directory 的方式。

1.  在 hello 佈建索引標籤下**對應**，按一下 **同步處理 Azure AD 使用者 tooWorkday**。

2.  在 hello**來源物件範圍**欄位，您可以選擇性地篩選將 Azure Active Directory 中的使用者應該擁有電子郵件地址寫回 tooWorkday。 hello 預設範圍為 「 在 Azure AD 中的所有使用者 」。 

3.  在 [hello**屬性對應**] 區段中，您可以定義如何個別 Workday 對應 tooActive 目錄屬性的屬性。 沒有預設的 hello 電子郵件地址的對應。 不過，符合識別碼的 hello 必須更新的 toomatch 使用者在其對應的項目與 workday 的 Azure AD 中。 受歡迎的比對方法 toosynchronize hello Workday 背景工作識別碼或員工識別碼在 Azure AD 中為 tooextensionAttribute1 15，然後在 Workday 在 Azure AD toomatch 使用者使用這個屬性。

4.  您的對應，按一下 toosave**儲存**頂端 hello hello 屬性對應 > 一節。

### <a name="part-3-start-hello-service"></a>第 3 部分： 啟動 hello 服務
當組件 1-2 已經完成時，您可以開始佈建服務的 hello。

1.  在 hello**佈建**索引標籤，設定 hello**佈建狀態**至**上**。

2. 按一下 [儲存] 。

3. 這會啟動 hello 初始同步處理，這可能要花費數小時取決於使用者人數會 workday。

4. 可以檢視個別的同步處理事件，在 hello**稽核記錄檔** 索引標籤。**[請參閱 hello 佈建上 tooread hello 稽核記錄的方式的詳細指示的報告指南](active-directory-saas-provisioning-reporting.md)**

5. 完成之後，其會寫入 [佈建] 索引標籤中的稽核摘要報告內，如下所示。

## <a name="known-issues"></a>已知問題

* **稽核記錄檔在歐洲地區設定中**-因為 hello 本版 technical preview 版本的已知的問題與 hello[稽核記錄檔](active-directory-saas-provisioning-reporting.md)hello Workday 連接器應用程式並未出現在 hello [的Azure入口網站](https://portal.azure.com)如果 hello Azure AD 租用戶位於歐洲的資料中心。 我們即將推出此問題的修正。 請檢查此空間在 hello 附近未來更新一次。 

## <a name="additional-resources"></a>其他資源
* [教學課程：設定 Workday 與 Azure Active Directory 之間的單一登入](active-directory-saas-workday-tutorial.md)
* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>後續步驟

* [瞭解如何 tooreview 記錄並取得上佈建活動報表](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
