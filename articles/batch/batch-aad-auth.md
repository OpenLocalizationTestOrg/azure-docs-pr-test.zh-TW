---
title: "aaaUse Azure Active Directory tooauthenticate Azure Batch 服務解決方案 |Microsoft 文件"
description: "批次支援 Azure AD 的 hello 批次服務驗證。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a>使用 Active Directory 驗證 Batch 服務解決方案

Azure Batch 支援使用 [Azure Active Directory][aad_about] (Azure AD)進行驗證。 Azure AD 是 Microsoft 的多租用戶雲端型目錄和身分識別管理服務。 Azure 本身會使用 Azure AD tooauthenticate 其客戶、 服務管理員和組織使用者。

搭配 Azure Batch 使用 Azure AD 驗證時，您可以使用下列其中一種方式進行驗證：

- 使用**整合式的驗證**tooauthenticate hello 應用程式互動的使用者。 使用整合式的驗證的應用程式收集使用者的認證，並使用這些認證 tooauthenticate 存取 tooBatch 資源。
- 使用**服務主體**tooauthenticate 無人看管的應用程式。 服務主體定義 hello 原則和應用程式的權限順序 toorepresent hello 應用程式中存取資源，在執行階段時。

toolearn 進一步了解 Azure AD，請參閱 hello [Azure Active Directory 文件](https://docs.microsoft.com/azure/active-directory/)。

## <a name="authentication-and-pool-allocation-mode"></a>驗證和集區配置模式

當您建立 Batch 帳戶時，可以指定應配置為該帳戶所建立之集區的位置。 在 hello 預設批次服務訂用帳戶或使用者訂用帳戶中，您可以選擇 tooallocate 集區。 您的選擇會影響您驗證該帳戶中的存取 tooresources 的方式。

- **Batch 服務訂用帳戶**。 根據預設，Batch 集區會在 Batch 服務訂用帳戶中配置。 如果您選擇此選項時，您可以驗證該帳戶中的存取 tooresources 不論是透過[共用金鑰](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service)或與 Azure AD。
- **使用者訂用帳戶**。 您可以選擇 tooallocate 批次集區，您指定的使用者訂用帳戶中。 如果您選擇此選項，必須向 Azure AD 進行驗證。

## <a name="endpoints-for-authentication"></a>用於驗證的端點

您需要 tooinclude tooauthenticate 批次應用程式與 Azure AD，您的程式碼在某些已知端點。

### <a name="azure-ad-endpoint"></a>Azure AD 端點

基底 hello Azure AD 授權端點：

`https://login.microsoftonline.com/`

tooauthenticate 與 Azure AD，您會使用這個端點以及 hello 租用戶識別碼 （目錄識別碼）。 hello 租用戶識別碼會識別 hello Azure AD 租用戶 toouse 進行驗證。 tooretrieve hello 租用戶識別碼，請遵循所述的 hello 步驟[取得 Azure Active Directory 中的 hello 租用戶識別碼](#get-the-tenant-id-for-your-active-directory):

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> 當您使用服務主體進行驗證時需要 hello 租用戶專用端點。 
> 
> 當您使用整合式的驗證進行驗證，但建議使用 hello 租用戶專用端點。 不過，您也可以使用 hello Azure AD 通用端點。 hello 一般端點提供一般認證未提供特定租用戶時，收集介面。 hello 共同端點`https://login.microsoftonline.com/common`。
>
>

如需 Azure AD 端點的詳細資訊，請參閱 [Azure AD 的驗證案例][aad_auth_scenarios]。

### <a name="batch-resource-endpoint"></a>Batch 資源端點

使用 hello **Azure Batch 資源端點**tooacquire token 來驗證要求 toohello 批次服務：

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a>向租用戶註冊您的應用程式

hello 第一個步驟中使用 Azure AD tooauthenticate 在 Azure AD 租用戶註冊您的應用程式。 註冊您的應用程式可讓您 toocall hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) 從程式碼。 hello ADAL 提供應用程式開發介面使用從您的應用程式的 Azure AD 進行驗證。 不論您計劃 toouse 整合式的驗證或服務主體，註冊您的應用程式是必要。

當您註冊您的應用程式時，您會提供有關您的應用程式 tooAzure AD 資訊。 然後 azure AD 提供應用程式識別碼，搭配 tooassociate 您的應用程式在執行階段的 Azure AD。 toolearn 深入了解 hello 應用程式識別碼，請參閱[應用程式與 Azure Active Directory 中的服務主體物件](../active-directory/develop/active-directory-application-objects.md)。

tooregister 批次應用程式中，遵循 hello 步驟在 hello[來新增應用程式](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application)一節中[整合應用程式與 Azure Active Directory][aad_integrate]。 如果您為原生應用程式註冊您的應用程式，您可以指定任何有效的 URI hello**重新導向 URI**。 不需要 toobe 實際的端點。

您已註冊您的應用程式之後，您會看到 hello 應用程式識別碼：

![向 Azure AD 註冊您的 Batch 應用程式](./media/batch-aad-auth/app-registration-data-plane.png)

如需向 Azure AD 註冊應用程式的詳細資訊，請參閱 [Azure AD 的驗證案例](../active-directory/develop/active-directory-authentication-scenarios.md)。

## <a name="get-hello-tenant-id-for-your-active-directory"></a>取得您的 Active Directory 中的 hello 租用戶識別碼

hello 租用戶識別碼會識別 hello Azure AD 租用戶提供驗證服務 tooyour 應用程式。 tooget hello 租用戶識別碼，請遵循下列步驟：

1. 在 hello Azure 入口網站，選取您的 Active Directory。
2. 按一下 [內容] 。
3. 複製 hello GUID 值提供給 hello 目錄識別碼。 此值也稱為 hello 租用戶識別碼。

![複製 hello 目錄識別碼](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a>使用整合式驗證

tooauthenticate 使用整合式驗證，您需要 toogrant 您應用程式的權限 tooconnect toohello 批次服務 API。 這個步驟可讓您的應用程式 tooauthenticate 呼叫 toohello 批次服務 API 與 Azure AD。

一旦您[註冊您的應用程式](#register-your-application-with-an-azure-ad-tenant)，請遵循下列步驟在 hello Azure 入口網站的 toogrant 它存取 toohello 批次服務：

1. 在 hello 左側導覽窗格中的 hello Azure 入口網站，選擇 **更服務**，按一下**應用程式註冊**。
2. 搜尋 hello hello 清單中的應用程式註冊您應用程式名稱：

    ![搜尋您的應用程式名稱](./media/batch-aad-auth/search-app-registration.png)

3. 開啟 hello**設定**刀鋒視窗，您的應用程式。 在 hello **API 存取**區段中，選取**必要的權限**。
4. 在 [hello**必要的權限**刀鋒視窗中，按一下 hello**新增**] 按鈕。
5. 在步驟 1 中，搜尋 hello 批次 API。 針對每個這些字串的搜尋，直到您找到 hello API:
    1. **MicrosoftAzureBatch**。
    2. **Microsoft Azure Batch**。 較新的 Azure AD 租用戶可以使用這個名稱。
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864**是 hello 識別碼 hello 批次 API。 
6. 一旦您找到 hello 批次 API，請選取它，然後按一下 hello**選取** 按鈕。
6. 在步驟 2 中，選取 hello 核取方塊旁太**存取 Azure 批次服務**按一下 hello**選取** 按鈕。
7. 按一下 hello**完成** 按鈕。

hello**必要的使用權限**刀鋒視窗現在顯示您的 Azure AD 應用程式具有存取 tooboth ADAL 和 hello 批次服務 API。 權限會自動授與 tooADAL 當您第一次使用 Azure AD 註冊您的應用程式。

![授與 API 權限](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a>使用服務主體 

tooauthenticate 執行自動安裝的應用程式，您可以使用服務主體。 您已註冊您的應用程式之後，請遵循下列步驟在 hello Azure 入口網站 tooconfigure 服務主體：

1. 要求應用程式的祕密金鑰。
2. 指派 RBAC 角色 tooyour 應用程式。

### <a name="request-a-secret-key-for-your-application"></a>要求應用程式的祕密金鑰

當您的應用程式進行驗證與服務主體時，會傳送 hello 應用程式識別碼和祕密金鑰 tooAzure AD。 您將需要 toocreate，並從您的程式碼複製 hello 秘密金鑰 toouse。

請遵循這些步驟 hello Azure 入口網站中：

1. 在 hello 左側導覽窗格中的 hello Azure 入口網站，選擇 **更服務**，按一下**應用程式註冊**。
2. 搜尋 hello hello 清單中的應用程式註冊您應用程式的名稱。
3. 顯示 hello**設定**刀鋒視窗。 在 hello **API 存取**區段中，選取**金鑰**。
4. toocreate 金鑰，請輸入 hello 索引鍵的說明。 然後，選取一或二年 hello 索引鍵的持續時間。 
5. 按一下 hello**儲存**按鈕 toocreate，並顯示 hello 鍵。 您必須能夠 tooaccess 複製 hello 索引鍵值 tooa 安全的地方，它一次之後保留 hello 刀鋒視窗。 

    ![建立祕密金鑰](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a>指派 RBAC 角色 tooyour 應用程式

與服務主體 tooauthenticate，您需要 tooassign RBAC 角色 tooyour 應用程式。 請遵循下列步驟：

1. 在 hello Azure 入口網站，瀏覽您的應用程式所使用的 toohello 批次帳戶。
2. 在 hello**設定**刀鋒視窗中的 hello 批次帳戶，請選取**存取控制 (IAM)**。
3. 按一下 hello**新增** 按鈕。 
4. 從 hello**角色**下拉式清單中，選擇其中一個 hello_參與者_或_讀取器_應用程式角色。 如需有關這些角色的詳細資訊，請參閱[開始 hello Azure 入口網站中的 角色型存取控制使用](../active-directory/role-based-access-control-what-is.md)。  
5. 在 hello**選取**欄位中，輸入 hello 應用程式的名稱。 從 [hello] 清單中，選取您的應用程式，然後按一下**儲存**。

您的應用程式現在應該會以您指派的 RBAC 角色，出現在您的存取控制設定中。 

![指派 RBAC 角色 tooyour 應用程式](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a>取得 Azure Active Directory 中的 hello 租用戶識別碼

hello 租用戶識別碼會識別 hello Azure AD 租用戶提供驗證服務 tooyour 應用程式。 tooget hello 租用戶識別碼，請遵循下列步驟：

1. 在 hello Azure 入口網站，選取您的 Active Directory。
2. 按一下 [內容] 。
3. 複製 hello GUID 值提供給 hello 目錄識別碼。 此值也稱為 hello 租用戶識別碼。

![複製 hello 目錄識別碼](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a>程式碼範例

本節中的 hello 程式碼範例顯示如何使用 Azure AD tooauthenticate 整合式驗證，以及與服務主體。 這些程式碼範例會使用.NET 中，但 hello 概念類似於其他語言。

> [!NOTE]
> Azure AD 驗證權杖會在一小時後過期。 使用長時間執行時**BatchClient**物件，我們建議您擷取權杖從 ADAL 上每個要求 tooensure 一定有效的語彙基元。 
>
>
> tooachieve 這在.NET 中，撰寫方法擷取 hello 從 Azure AD 權杖，並傳遞該方法 tooa **BatchTokenCredentials**為委派的物件。 hello 委派方法會呼叫每個要求 toohello 批次服務 tooensure 提供有效的語彙基元。 根據預設，ADAL 會快取權杖，因此只在必要時才會從 Azure AD 擷取新的權杖。 如需關於 Azure AD 中的權杖資訊，請參閱 [Azure AD 的驗證案例][aad_auth_scenarios]。
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a>程式碼範例︰搭配 Batch .NET 使用 Azure AD 整合式驗證

使用整合式驗證從批次.NET 中，參考 hello tooauthenticate [Azure 批次.NET](https://www.nuget.org/packages/Azure.Batch/)封裝和 hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/)封裝。

Hello 如下`using`程式碼中的陳述式：

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

參考 hello Azure AD 端點，在您的程式碼，包括 hello 租用戶識別碼。 tooretrieve hello 租用戶識別碼，請遵循所述的 hello 步驟[取得 Azure Active Directory 中的 hello 租用戶識別碼](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

參考 hello 批次服務資源端點：

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

參考您的 Batch 帳戶：

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

指定您的應用程式的 hello 應用程式識別碼 （用戶端識別碼）。 hello 應用程式識別碼是可從您的應用程式註冊在 hello Azure 入口網站中：

```csharp
private const string ClientId = "<application-id>";
```

也請複製 hello 重新導向 hello 註冊程序期間所指定的 URI。 hello 重新導向 URI 指定在您的程式碼必須符合 hello 重新導向時註冊 hello 應用程式所提供的 URI:

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

從 Azure AD 中撰寫回呼方法 tooacquire hello 驗證語彙基元。 hello **GetAuthenticationTokenAsync**如下所示的回呼方法會呼叫 ADAL tooauthenticate hello 應用程式互動的使用者。 hello **AcquireTokenAsync**方法提供 adal 提示 hello 使用者輸入其認證，然後 hello 應用程式一次進行 hello 使用者提供他們 （除非它已快取的認證）：

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

建構**BatchTokenCredentials**採用 hello 委派做為參數的物件。 使用這些認證 tooopen **BatchClient**物件。 您可以使用該**BatchClient** hello 批次服務針對後續作業的物件：

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a>程式碼範例︰搭配 Batch .NET 使用 Azure AD 服務主體

與服務主體從批次.NET 中，參考 hello tooauthenticate [Azure 批次.NET](https://www.nuget.org/packages/Azure.Batch/)封裝和 hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/)封裝。

Hello 如下`using`程式碼中的陳述式：

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

參考 hello Azure AD 端點，在您的程式碼，包括 hello 租用戶識別碼。 使用服務主體時，您必須提供租用戶特定的端點。 tooretrieve hello 租用戶識別碼，請遵循所述的 hello 步驟[取得 Azure Active Directory 中的 hello 租用戶識別碼](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

參考 hello 批次服務資源端點：  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

參考您的 Batch 帳戶：

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

指定您的應用程式的 hello 應用程式識別碼 （用戶端識別碼）。 hello 應用程式識別碼是可從您的應用程式註冊在 hello Azure 入口網站中：

```csharp
private const string ClientId = "<application-id>";
```

指定您所複製的 hello Azure 入口網站的 hello 祕密金鑰：

```csharp
private const string ClientKey = "<secret-key>";
```

從 Azure AD 中撰寫回呼方法 tooacquire hello 驗證語彙基元。 hello **GetAuthenticationTokenAsync**回呼方法，如下所示呼叫 ADAL 自動驗證：

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

建構**BatchTokenCredentials**採用 hello 委派做為參數的物件。 使用這些認證 tooopen **BatchClient**物件。 然後您可以使用， **BatchClient** hello 批次服務針對後續作業的物件：

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a>後續步驟

toolearn 進一步了解 Azure AD，請參閱 hello [Azure Active Directory 文件](https://docs.microsoft.com/azure/active-directory/)。 深入了解範例來示範如何 toouse ADAL 位於 hello [Azure 程式碼範例](https://azure.microsoft.com/resources/samples/?service=active-directory)程式庫。

toolearn 進一步了解服務主體，請參閱[應用程式與 Azure Active Directory 中的服務主體物件](../active-directory/develop/active-directory-application-objects.md)。 服務主體使用 toocreate hello Azure 入口網站，請參閱[使用入口網站 toocreate Active Directory 應用程式和服務主體可存取資源](../resource-group-create-service-principal-portal.md)。 您也可以使用 PowerShell 或 Azure CLI 來建立服務主體。 

tooauthenticate 批次管理應用程式使用 Azure AD，請參閱[與 Active Directory 驗證批次管理解決方案](batch-aad-auth-management.md)。 

[aad_about]: ../active-directory/active-directory-whatis.md "什麼是 Azure Active Directory？"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD 的驗證案例"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "整合應用程式與 Azure Active Directory"
[azure_portal]: http://portal.azure.com
