---
title: "在 OMS IT 服務管理連接器 aaaITSM 連線 |Microsoft 文件"
description: "連接您 ITSM 產品/服務 IT 服務管理連接器在 OMS toocentrally 監視及管理 hello ITSM 工作項目。"
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a>將 ITSM 產品/服務與 IT 服務管理連接器進行連線 (預覽)
這篇文章提供有關如何資訊 tooconnect 您 ITSM 產品/服務 tooIT Service Management Connector 在 OMS 中，以及集中管理您的工作項目。 如需有關 IT 服務管理連接器的詳細資訊，請參閱[概觀](log-analytics-itsmc-overview.md)。

支援下列產品/服務的 hello:

- [System Center Service Manager](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [ServiceNow](#connect-servicenow-to-it-service-management-connector-in-oms)
- [Provance](#connect-provance-to-it-service-management-connector-in-oms)
- [Cherwell](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a>連接 System Center Service Manager tooIT 在 OMS 中的服務管理連接器

hello 下列各節提供詳細說明如何 tooconnect 您的 System Center Service Manager 產品 toohello 在 OMS 中的 IT 服務管理連接器。

### <a name="prerequisites"></a>必要條件

請確定您有下列必要條件符合 hello:

- 已安裝 IT 服務管理連接器。
詳細資訊︰[設定](log-analytics-itsmc-overview.md#configuration)。
- hello 服務管理員 Web 應用程式 （Web 應用程式） 是部署和設定。 Web 應用程式的相關在[這裡](#create-and-deploy-service-manager-web-app-service)。
- 已建立及設定的混合式連線。 更多資訊：[設定 hello 混合式連線](#configure-the-hybrid-connection)。
- Service Manager 的支援版本：2012 R2 或 2016。
- 使用者角色︰[進階操作員](https://technet.microsoft.com/library/ff461054.aspx)。

### <a name="connection-procedure"></a>連線程序

使用下列程序 tooconnect hello 您的 System Center Service Manager 執行個體 toohello IT 服務管理連接器：

1. 跳過**OMS** >**設定** > **連線來源**。
2. 選取**ITSM 連接器**，然後按一下新增新的連線。

    ![Service Manager ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. 下表，hello 中所述，提供 hello 資訊，然後按一下**儲存**toocreate hello 連線：

> [!NOTE]
> 這些全部都是必要參數。

| **欄位** | **說明** |
| --- | --- |
| **名稱**   | 輸入您想要以 hello IT 服務管理連接器 tooconnect hello System Center Service Manager 執行個體的名稱。  稍後當您設定這個執行個體的工作項目/檢視詳細的記錄分析時，會使用這個名稱。 |
| **選取連線類型**   | 選取 **System Center Service Manager**。 |
| **伺服器 URL**   | 輸入 hello hello 服務管理員 Web 應用程式 URL。 Service Manager Web 應用程式的相關詳細資訊在[這裡](#create-and-deploy-service-manager-web-app-service)。
| **用戶端識別碼**   | 輸入您產生 （使用 hello 自動指令碼） 來驗證 hello Web 應用程式的用戶端識別碼 hello。 Hello 自動化指令碼的詳細資訊[這裡。](log-analytics-itsmc-service-manager-script.md)|
| **用戶端祕密**   | 型別 hello 用戶端密碼，產生此識別碼。   |
| **資料同步範圍**   | 選取您想透過 hello IT 服務管理連接器 toosync 的 hello Service Manager 工作項目。  系統會將這些工作項目匯入 Log Analytics。 **選項︰**事件、變更要求。|
| **同步資料** | 輸入經過天數 hello 資料從 hello 數的字。 **上限**：120 天。 |
| **在 ITSM 解決方案中建立新的設定項目** | 如果您想在 hello ITSM 產品 toocreate hello 設定項目，請選取此選項。 選取時，OMS 將會建立受影響的 hello Ci 支援 ITSM 系統 （如果不存在的 Ci) 是在 hello 的組態項目。 **預設**︰停用。 |

順利連線並同步處理時︰

- 從 Service Manager 選取的工作項目將匯入 OMS **Log Analytics。** 您可以檢視這些 hello 摘要 hello IT 服務管理連接器磚上的工作項目。

- 您可以從 OMS 建立這個 Service Manager 執行個體中的 OMS 警示或記錄搜尋事件。

詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。

### <a name="create-and-deploy-service-manager-web-app-service"></a>建立及部署 Service Manager Web 應用程式服務

tooconnect hello 以 hello OMS 上的 IT 服務管理連接器在內部部署 Service Manager 時，Microsoft 已建立 hello GitHub 上的服務管理員 Web 應用程式。

tooset 設定 hello ITSM Web 應用程式為您的服務管理員，請勿 hello 遵循：

- **部署 hello Web 應用程式**– 部署 hello Web 應用程式、 設定 hello 屬性，以及使用 Azure AD 進行驗證。 您可以部署 hello web 應用程式使用 hello[自動化指令碼](log-analytics-itsmc-service-manager-script.md)Microsoft 已提供您。
- **設定 hello 混合式連接** - [設定此連線](#configure-the-hybrid-connection)、 以手動方式。

#### <a name="deploy-hello-web-app"></a>部署 hello web 應用程式
使用 hello 自動化[指令碼](log-analytics-itsmc-service-manager-script.md)toodeploy hello Web 應用程式、 設定 hello 屬性，以及使用 Azure AD 進行驗證。

藉由提供下列必要的詳細資料的 hello 執行 hello 指令碼：

- Azure 訂用帳戶詳細資料
- 資源群組名稱
- 位置
- Service Manager 伺服器詳細資料 (伺服器名稱、網域、使用者名稱和密碼)
- Web 應用程式的網站名稱前置詞
- 服務匯流排命名空間。

hello 指令碼會建立使用您指定的 hello 名稱 hello Web 應用程式 (以及幾個額外字串 toomake 它唯一)。 它會產生 hello **Web 應用程式 URL**，**用戶端識別碼**和**用戶端密碼**。

Hello 值儲存您使用它們的 IT 服務管理 Connector 建立連線時。

**檢查 hello Web 應用程式安裝**

1. 跳過**Azure 入口網站** > **資源**。
2. 選取 hello Web 應用程式中，按一下**設定** > **應用程式設定**。
3. 確認您提供的 hello 透過 hello 指令碼的應用程式部署的 hello 時間 hello Service Manager 執行個體的 hello 資訊。

### <a name="configure-hello-hybrid-connection"></a>設定 hello 混合式連接

使用下列程序 tooconfigure hello 混合式連接的 hello Service Manager 執行個體連接與 hello IT 服務管理連接器在 OMS 中的 hello。

1. Hello 服務管理員 Web 應用程式中，尋找底下**Azure 資源**。
2. 按一下 [設定] > [網路]。
3. 在 [混合式連線] 下，按一下 [設定混合式連線端點]。

    ![混合式連線網路](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. 在 hello**混合式連線**刀鋒視窗中，按一下 **新增混合式連接**。

    ![混合式連線新增](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. 在 hello**新增混合式連線**刀鋒視窗中，按一下 **建立新的混合式連線**。

    ![新增混合式連線](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. 輸入下列值的 hello:

    - **端點名稱**： 指定 hello 新混合式連接的名稱。
    -  **端點主機**: hello Service Manager 管理伺服器的 FQDN。
    - **端點連接埠**：輸入 5724
    - **服務匯流排命名空間**︰使用現有的或建立一個新的服務匯流排命名空間。
    - **位置**： 選取 hello 位置。
    -  **名稱**： 指定名稱 toohello servicebus，如果您要建立它。

    ![混合式連線值](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. 按一下**確定**tooclose hello**建立混合式連接**刀鋒視窗，然後開始建立 hello 混合式連接。

    Hello 混合式連線建立之後，它會顯示在 [hello] 刀鋒視窗。

7. 建立 hello 混合式連線之後，請選取 hello 連線，然後按一下**新增選取的混合式連接**。

    ![新增混合式連線](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a>設定 hello 接聽程式的安裝程式

使用下列程序 tooconfigure hello hello 混合式連接的接聽程式設定的 hello。

1. 在 hello**混合式連線**刀鋒視窗中，按一下**下載 hello 連線管理員**並將它安裝在 hello System Center Service Manager 執行個體執行所在的電腦上。

    Hello 安裝完成之後，**混合式連接管理員 UI**才可使用選項**啟動**功能表。

2. 按一下 [混合式連線管理員 UI]，系統會提示您輸入 Azure 認證。

3. 使用您的 Azure 認證登入並選取您建立 hello 混合式連接所在的訂用帳戶。

4. 按一下 [儲存] 。

混合式連線已成功連線。

![混合式連線成功](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> 建立 hello 混合式連線之後，請確認，然後瀏覽 hello 測試 hello 連接 Service Manager Web 應用程式部署。 請確定 hello 連接成功之前 tooconnect toohello IT 服務管理連接器在 OMS 中再試一次。

hello 下列影像顯示 hello 成功連接詳細資料：

![混合式連線測試](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a>連接 ServiceNow tooIT 在 OMS 中的服務管理連接器

hello 下列各節提供詳細說明如何 tooconnect 您的 ServiceNow 產品 toohello 在 OMS 中的 IT 服務管理連接器。

### <a name="prerequisites"></a>必要條件

請確定您有下列必要條件符合 hello:

- 已安裝 IT 服務管理連接器。 詳細資訊︰[設定。](log-analytics-itsmc-overview.md#configuration)
- ServiceNow 支援版本 – Fuji、Geneva、Helsinki。

ServiceNow 管理員必須執行 hello 依照它們的 ServiceNow 執行個體：
- 產生用戶端識別碼和 hello ServiceNow 產品的用戶端密碼。 如需有關如何 toogenerate 用戶端識別碼和密碼，請參閱詳細[OAuth 設定](http://wiki.servicenow.com/index.php?title=OAuth_Setup)。
- 安裝 Microsoft OMS 整合 （ServiceNow 的應用程式） 的 hello 使用者應用程式。 [深入了解](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 )。
- 建立整合 hello 使用者安裝應用程式的使用者角色。 有關 toocreate hello 整合使用者角色的方式[這裡](#create-integration-user-role-in-servicenow-app)。


### <a name="connection-procedure"></a>**連線程序**

使用下列程序 toocreate ServiceNow 連接 hello:

1. 跳過**OMS** > **設定** > **連線來源**。
2. 選取**ITSM 連接器**，然後按一下新增新的連線。

    ![ServiceNow 連線](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. 下表，hello 中所述，提供 hello 資訊，然後按一下**儲存**toocreate hello 連線：

> [!NOTE]
> 這些全部都是必要參數。

| **欄位** | **說明** |
| --- | --- |
| **名稱**   | 輸入您想要以 hello IT 服務管理連接器 tooconnect hello ServiceNow 執行個體的名稱。  稍後當您在 OMS 中設定這個 ITSM 的工作項目/檢視詳細的記錄分析時，會使用這個名稱。 |
| **選取連線類型**   | 選取 **ServiceNow**。 |
| **使用者名稱**   | 輸入您在 hello ServiceNow 的應用程式 toosupport hello 連接 toohello IT 服務管理連接器中建立的 hello 整合使用者名稱。 詳細資訊︰[建立 ServiceNow 應用程式使用者角色](#create-integration-user-role-in-servicenow-app)。|
| **密碼**   | 輸入 hello 這個使用者名稱相關聯的密碼。 **請注意**： 使用者名稱和密碼用來產生驗證權杖，並會不會儲存在 hello OMS 服務中。  |
| **伺服器 URL**   | 輸入您想 tooconnect tooIT Service Management Connector hello ServiceNow 執行個體的 hello URL。 |
| **用戶端識別碼**   | 輸入您想 toouse OAuth2 驗證，您先前產生的 hello 用戶端識別碼。  如需產生用戶端識別碼和祕密的資訊：[OAuth 設定](http://wiki.servicenow.com/index.php?title=OAuth_Setup)。 |
| **用戶端祕密**   | 型別 hello 用戶端密碼，產生此識別碼。   |
| **資料同步範圍**   | 選取您想 toosync tooOMS，透過 hello IT 服務管理連接器的 hello ServiceNow 工作項目。  選取的 hello 值會匯入記錄分析。   **選項︰**事件和變更要求。|
| **同步資料** | 輸入經過天數 hello 資料從 hello 數的字。 **上限**：120 天。 |
| **在 ITSM 解決方案中建立新的設定項目** | 如果您想在 hello ITSM 產品 toocreate hello 設定項目，請選取此選項。 選取時，OMS 將會建立受影響的 hello Ci 支援 ITSM 系統 （如果不存在的 Ci) 是在 hello 的組態項目。 **預設**︰停用。 |


順利連線並同步處理時︰

- 從 ServiceNow 連線選取的工作項目將匯入 OMS Log Analytics。  您可以檢視這些 hello 摘要 hello IT 服務管理連接器磚上的工作項目。
- 您可以在這個 ServiceNow 執行個體中建立 OMS 警示或記錄搜尋的事件、警示和活動。  


詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。

### <a name="create-integration-user-role-in-servicenow-app"></a>在 ServiceNow 應用程式中建立整合使用者角色

下列程序的使用者 hello:

1.  請瀏覽 hello [ServiceNow 存放區](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0)並安裝 hello **ServiceNow 與 Microsoft OMS 整合的使用者應用程式**到 ServiceNow 執行個體。
2.  安裝之後，請瀏覽 hello 左導覽列的 hello ServiceNow 執行個體、 搜尋和選取 Microsoft OMS 整合器。  
3.  按一下 [安裝檢查清單]。

    hello 狀態會顯示為**完成**如果 hello 」 使用者角色，但 toobe 建立。

4.  中的 hello 文字方塊，接下來太**建立整合使用者**，輸入可以連接 toohello IT 服務管理連接器在 OMS 中的 hello 使用者 hello 使用者名稱。
5.  輸入對這個使用者而言 hello 密碼，然後按一下**確定**。  

>[!NOTE]

> 您在 OMS 中使用這些認證 toomake hello ServiceNow 連接。

hello 預設角色指派會顯示 hello 新建立的使用者。

預設角色︰
- personalize_choices
- import_transformer
-   x_mioms_microsoft.user
-   itil
-   template_editor
-   view_changer

已成功建立 hello 使用者時，一旦 hello 狀態**檢查安裝檢查清單**移動 tooCompleted，列出 hello hello hello 應用程式建立的使用者角色的詳細資料。

> [!NOTE]

> tooallow 使用者 toocreate**警示**和**事件**從 OMS ServiceNow 中：

> - 確定您擁有 hello 事件管理模組已安裝在您的 ServiceNow 執行個體上。

> - 新增下列角色 toohello 整合使用者的 hello:
>      - evt_mgmt_integration
>      - evt_mgmt_operator  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a>連接 Provance tooIT 在 OMS 中的服務管理連接器

hello 下列各節提供詳細說明如何 tooconnect 您 Provance 產品 toohello 在 OMS 中的 IT 服務管理連接器。

### <a name="prerequisites"></a>必要條件

請確定您有下列必要條件符合 hello:

- 已安裝 IT 服務管理連接器。 詳細資訊︰[設定](log-analytics-itsmc-overview.md#configuration)。
- 應該向 Azure AD 註冊 Provance 應用程式 - 並將用戶端識別碼設為可用。 如需詳細資訊，請參閱[如何 tooconfigure active directory 驗證](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。
- 使用者角色：管理員。

### <a name="connection-procedure"></a>連線程序

使用下列程序 toocreate Provance 連接 hello:

1. 跳過**OMS** > **設定** > **連線來源**。
2. 選取**ITSM 連接器**，然後按一下新增新的連線。  

    ![Provance 連線](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. 下表，hello 中所述，提供 hello 資訊，然後按一下**儲存**toocreate hello 連線。

> [!NOTE]
> 這些全部都是必要參數。

| **欄位** | **說明** |
| --- | --- |
| **名稱**   | 輸入您想要以 hello IT 服務管理連接器 tooconnect hello Provance 執行個體的名稱。  稍後當您在 OMS 中設定這個 ITSM 的工作項目/檢視詳細的記錄分析時，會使用這個名稱。 |
| **選取連線類型**   | 選取 [Provance]。 |
| **使用者名稱**   | 輸入可以連接 toohello IT 服務管理連接器的 hello 使用者名稱。    |
| **密碼**   | 輸入 hello 這個使用者名稱相關聯的密碼。 **注意：**使用者名稱和密碼用來產生驗證權杖，並會不會儲存在 hello OMS 服務內。 _|
| **伺服器 URL**   | 輸入您想 tooconnect tooIT Service Management Connector Provance 執行個體的 hello URL。 |
| **用戶端識別碼**   | 型別 hello 來驗證此連線，您在 Provance 執行個體中產生的用戶端識別碼。  在用戶端識別碼的詳細資訊，請參閱[如何 tooconfigure active directory 驗證](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。 |
| **資料同步範圍**   | 選取您想 toosync tooOMS，透過 hello IT 服務管理連接器的 hello Provance 工作項目。  系統會將這些工作項目匯入 Log Analytics。   **選項︰**事件、變更要求。|
| **同步資料** | 輸入經過天數 hello 資料從 hello 數的字。 **上限**：120 天。 |
| **在 ITSM 解決方案中建立新的設定項目** | 如果您想在 hello ITSM 產品 toocreate hello 設定項目，請選取此選項。 選取時，OMS 將會建立受影響的 hello Ci 支援 ITSM 系統 （如果不存在的 Ci) 是在 hello 的組態項目。 **預設**︰停用。|

順利連線並同步處理時︰

- 從 Provance 連線選取的工作項目將匯入 OMS **Log Analytics**。  您可以檢視這些 hello 摘要 hello IT 服務管理連接器磚上的工作項目。
- 您可以在這個 Provance 執行個體中建立 OMS 警示或記錄搜尋的事件和活動。

詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a>連接 Cherwell tooIT 在 OMS 中的服務管理連接器

hello 下列各節提供詳細說明如何 tooconnect 您 Cherwell 產品 toohello 在 OMS 中的 IT 服務管理連接器。

### <a name="prerequisites"></a>必要條件

請確定您有下列必要條件符合 hello:

- 已安裝 IT 服務管理連接器。 詳細資訊︰[設定](log-analytics-itsmc-overview.md#configuration)。
- 所產生的用戶端識別碼。 詳細資訊︰[產生 Cherwell 的用戶端識別碼](#generate-client-id-for-cherwell)。
- 使用者角色：管理員。

### <a name="connection-procedure"></a>連線程序

使用下列程序 toocreate Cherwell 連接 hello:

1. 跳過**OMS** >  **設定** > **連線來源**。
2. 選取 ITSM 連接器，然後按一下新增新的連線。  

    ![Cherwell 使用者識別碼](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. 下表，hello 中所述，提供 hello 資訊，然後按一下**儲存**toocreate hello 連線。

> [!NOTE]
> 這些全部都是必要參數。

| **欄位** | **說明** |
| --- | --- |
| **名稱**   | 輸入您想 tooconnect toohello IT 服務管理連接器 hello Cherwell 執行個體的名稱。  稍後當您在 OMS 中設定這個 ITSM 的工作項目/檢視詳細的記錄分析時，會使用這個名稱。 |
| **選取連線類型**   | 選取 [Cherwell]。 |
| **使用者名稱**   | 輸入可以連接 toohello IT 服務管理連接器的 hello Cherwell 使用者名稱。 |
| **密碼**   | 輸入 hello 這個使用者名稱相關聯的密碼。 **注意：**使用者名稱和密碼用來產生驗證權杖，並會不會儲存在 hello OMS 服務中。|
| **伺服器 URL**   | 輸入您想 tooconnect tooIT Service Management Connector Cherwell 執行個體的 hello URL。 |
| **用戶端識別碼**   | 型別 hello 來驗證此連線，您在您 Cherwell 的執行個體中產生的用戶端識別碼。   |
| **資料同步範圍**   | 選取您想透過 hello IT 服務管理連接器 toosync 的 hello Cherwell 工作項目。  系統會將這些工作項目匯入 Log Analytics。   **選項︰**事件、變更要求。 |
| **同步資料** | 輸入經過天數 hello 資料從 hello 數的字。 **上限**：120 天。 |
| **在 ITSM 解決方案中建立新的設定項目** | 如果您想在 hello ITSM 產品 toocreate hello 設定項目，請選取此選項。 選取時，OMS 將會建立受影響的 hello Ci 支援 ITSM 系統 （如果不存在的 Ci) 是在 hello 的組態項目。 **預設**︰停用。 |

順利連線並同步處理時︰

- 從這個 Cherwell 連線選取的工作項目將匯入 OMS Log Analytics。 您可以檢視這些 hello 摘要 hello IT 服務管理連接器磚上的工作項目。
- 您可以從 OMS 建立這個 Cherwell 執行個體的事件和活動。 詳細資訊︰建立 OMS 警示的 ITSM工作項目及建立 OMS 記錄的 ITSM 工作項目。

詳細資訊︰[建立 OMS 警示的 ITSM工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)及[建立 OMS 記錄的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)。

### <a name="generate-client-id-for-cherwell"></a>產生 Cherwell 的用戶端識別碼

toogenerate hello cherwell 的用戶端識別碼/金鑰，請使用下列程序的 hello:

1. 登入 tooyour Cherwell 的執行個體為系統管理員。
2. 按一下 [安全性] > [編輯 REST API 用戶端設定]。
3. 選取 [建立新的用戶端] > [用戶端祕密]。

    ![Cherwell 使用者識別碼](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a>後續步驟
 - [建立 OMS 警示的 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [從 OMS 記錄建立 ITSM 工作項目](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [檢視您連線的 Log Analytics](log-analytics-itsmc-overview.md#using-the-solution)
