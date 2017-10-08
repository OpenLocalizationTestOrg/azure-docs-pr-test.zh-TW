---
title: "Azure 入口網站中的應用程式的 aaaCreate 識別 |Microsoft 文件"
description: "描述如何 toocreate 新的 Azure Active Directory 應用程式和服務主體可以使用 Azure Resource Manager toomanage hello 角色型存取控制存取 tooresources。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a>使用入口網站 toocreate Azure Active Directory 應用程式和服務主體可存取資源

當您需要 tooaccess 或修改資源的應用程式時，您必須在設定 Azure Active Directory (AD) 應用程式，並指派 hello 所需的權限 tooit。 這個方法很理想 toorunning hello 應用程式，以您自己的認證，因為：

* 您可以指派權限 toohello 不同於您自己的權限的應用程式識別。 一般而言，這些權限會限制的 tooexactly 哪些 hello 應用程式需要 toodo。
* 如果您的責任的變更，您並沒有 toochange hello 應用程式的認證。 
* 執行無人看管的指令碼時，您可以使用憑證 tooautomate 驗證。

本主題說明您如何 tooperform 那些逐步 hello 入口網站。 它著重在 hello 應用程式所在預定的 toorun 只能有一個組織內的單一租用戶應用程式。 您通常會將單一租用戶應用程式用在組織內執行的企業營運系統應用程式。
 
## <a name="required-permissions"></a>所需的權限
toocomplete 本主題中，您必須有足夠的權限 tooregister 的應用程式與 Azure AD 租用戶，並在您 Azure 訂用帳戶中指派 hello 應用程式 tooa 角色。 讓我們確定您擁有 hello 正確的權限 tooperform 那些步驟。

### <a name="check-azure-active-directory-permissions"></a>檢查 Azure Active Directory 權限
1. 登入 tooyour Azure 帳戶透過 hello [Azure 入口網站](https://portal.azure.com)。
2. 選取 **Azure Active Directory**。

     ![選取 Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. 在 Azure Active Directory 中，選取 [使用者設定]。

     ![選取使用者設定](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. 檢查 hello**應用程式註冊**設定。 如果設定太**是**，非系統管理使用者可以註冊 AD 應用程式。 這個設定表示 hello Azure AD 租用戶中的任何使用者可以註冊應用程式。 您可以繼續在太[檢查 Azure 訂用帳戶的權限](#check-azure-subscription-permissions)。

     ![檢視應用程式註冊](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. 如果設定太 hello 應用程式登錄設定**否**，只有系統管理員使用者可以註冊的應用程式。 您的帳戶是否 hello Azure AD 租用戶系統管理員，您會需要 toocheck。 從 [快速工作] 中，選取 [概觀] 和 [尋找使用者]。

     ![尋找使用者](./media/resource-group-create-service-principal-portal/find-user.png)
6. 搜尋您的帳戶，找到時選取它。

     ![搜尋使用者](./media/resource-group-create-service-principal-portal/show-user.png)
7. 對於您的帳戶，選取 [目錄角色]。 

     ![目錄角色](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. 在 Azure AD 中檢視您指派的目錄角色。 如果您的帳戶指派 toohello 使用者角色，但 hello 應用程式登錄設定 （從先前步驟的 hello) 有限的 tooadmin 使用者，請要求系統管理員 tooeither 指派您 tooan 系統管理員角色或 tooenable 使用者 tooregister 應用程式。

     ![檢視角色](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a>檢查 Azure 訂用帳戶權限
您 Azure 訂用帳戶，您的帳戶必須具有`Microsoft.Authorization/*/Write`存取 tooassign AD 應用程式 tooa 角色。 這個動作透過 hello 授與[擁有者](../active-directory/role-based-access-built-in-roles.md#owner)角色或[使用者存取系統管理員](../active-directory/role-based-access-built-in-roles.md#user-access-administrator)角色。 如果您的帳戶指派 toohello**參與者**角色，您沒有足夠的權限。 嘗試 tooassign hello 服務主體 tooa 角色時，您會收到錯誤。 

toocheck 您訂用帳戶的權限：

1. 如果您不已查看您的 Azure AD 帳戶 hello 先前步驟中，選取**Azure Active Directory** hello 左窗格中。

2. 找到您的 Azure AD 帳戶。 從 [快速工作] 中，選取 [概觀] 和 [尋找使用者]。

     ![尋找使用者](./media/resource-group-create-service-principal-portal/find-user.png)
2. 搜尋您的帳戶，找到時選取它。

     ![搜尋使用者](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. 選取 [Azure 資源]。

     ![選取資源](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. 檢視指派的角色，並判斷是否有足夠的權限 tooassign AD 應用程式 tooa 角色。 如果沒有，請詢問您的訂用帳戶管理員 tooadd 您 tooUser 存取 」 系統管理員角色。 在下列映像的 hello，hello 使用者是指派的 toohello 擁有者角色的兩個訂閱，這表示該使用者具有足夠的權限。 

     ![顯示權限](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a>建立 Azure Active Directory 應用程式
1. 登入 tooyour Azure 帳戶透過 hello [Azure 入口網站](https://portal.azure.com)。
2. 選取 **Azure Active Directory**。

     ![選取 Azure Active Directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. 選取 [應用程式註冊]。   

     ![select app registrations](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. 選取 [新增] 。

     ![新增應用程式](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. Hello 應用程式提供名稱和 URL。 選取  **Web 應用程式 / 應用程式開發介面**或**原生**想 toocreate hello 種應用程式。 設定後 hello 值，請選取**建立**。

     ![名稱應用程式](./media/resource-group-create-service-principal-portal/create-app.png)

您已建立好應用程式。

## <a name="get-application-id-and-authentication-key"></a>取得應用程式識別碼和驗證金鑰
以程式設計方式登入時，您會需要您的應用程式和驗證金鑰的 hello 識別碼。 tooget 那些值，使用 hello 下列步驟：

1. 在 Azure Active Directory 中，從 [應用程式註冊]選取您的應用程式。

     ![選取應用程式](./media/resource-group-create-service-principal-portal/select-app.png)
2. 複製 hello**應用程式識別碼**並將它儲存在應用程式程式碼中。 hello hello 中的應用程式[範例應用程式](#sample-applications)區段，請參閱 toothis hello 用戶端識別碼值。

     ![用戶端識別碼](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. toogenerate 需有驗證金鑰，選取**金鑰**。

     ![選取金鑰](./media/resource-group-create-service-principal-portal/select-keys.png)
4. 提供 hello 金鑰和 hello 金鑰的持續時間的描述。 完成時，選取 [儲存]。

     ![儲存金鑰](./media/resource-group-create-service-principal-portal/save-key.png)

     在儲存之後 hello 索引鍵，會顯示 hello hello 機碼值。 因為您不能 tooretrieve hello 金鑰之後，請複製此值。 您提供 hello 機碼值中的 hello 應用程式識別碼 toolog hello 應用程式。 儲存您的應用程式可以擷取 hello 機碼值。

     ![儲存的金鑰](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a>取得租用戶識別碼
以程式設計方式登入時，您需要 toopass hello 租用戶識別碼與驗證要求。 

1. tooget hello 租用戶識別碼，選取**屬性**Azure AD 租用戶。 

     ![選取 Azure AD 屬性](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. 複製 hello**目錄識別碼**。 這個值是您的租用戶識別碼。

     ![租用戶識別碼](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a>指派應用程式 toorole
您的訂用帳戶中的 tooaccess 資源，您必須指派 hello 應用程式 tooa 角色。 決定哪些角色代表 hello hello 應用程式的正確權限。 toolearn 有關 hello 可用的角色，請參閱[RBAC： 內建的角色](../active-directory/role-based-access-built-in-roles.md)。

您可以設定 hello 範圍層級 hello hello 訂用帳戶、 資源群組或資源。 權限是繼承的 toolower 範圍層級。 例如，新增資源群組的應用程式 toohello 讀取器角色表示它可以讀取 hello 資源群組和它所包含的任何資源。

1. 瀏覽 toohello 想 tooassign hello 應用程式的範圍層級。 例如，tooassign hello 訂用帳戶範圍，角色選取**訂閱**。 您可以改為選取資源群組或資源。

     ![select subscription](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. 選取 hello 特定訂用帳戶 （資源群組或資源） tooassign hello 應用程式。

     ![選取要指派的訂用帳戶](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. 選取 [存取控制 (IAM)]。

     ![選取存取](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. 選取 [新增] 。

     ![選取 [新增]](./media/resource-group-create-service-principal-portal/select-add.png)
6. 選取您想 tooassign toohello 應用程式的 hello 角色。 hello 下列影像顯示 hello**讀取器**角色。

     ![選取角色](./media/resource-group-create-service-principal-portal/select-role.png)

8. 搜尋並選取您的應用程式。

     ![搜尋應用程式](./media/resource-group-create-service-principal-portal/search-app.png)
9. 選取**確定**toofinish 指派 hello 角色。 您會看到您 hello 清單中指派該範圍的 tooa 角色之使用者的應用程式。

## <a name="log-in-as-hello-application"></a>Hello 應用程式身分登入

您的應用程式現在已設定在 Azure Active Directory 中。 您必須有識別碼和金鑰 toouse hello 應用程式以登入。 hello 應用程式會指派 tooa 角色，讓它可以執行特定動作。 如需透過不同平台的 hello 應用程式以登入資訊，請參閱：

* [PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [Azure CLI](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [REST](/rest/api/#create-the-request)
* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a>後續步驟
* tooset 多租用戶應用程式，請參閱[以 hello Azure 資源管理員 API 的開發人員指南 tooauthorization](resource-manager-api-authentication.md)。
* toolearn 有關指定安全性原則，請參閱[Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。  
* 如需可授與或拒絕 toousers 可用動作的清單，請參閱[Azure 資源管理員資源提供者作業](../active-directory/role-based-access-control-resource-provider-operations.md)。
