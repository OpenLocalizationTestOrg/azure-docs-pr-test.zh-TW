---
title: "Azure 應用程式使用 Azure CLI aaaCreate 識別 |Microsoft 文件"
description: "描述如何 toouse Azure CLI toocreate Azure Active Directory 應用程式和服務主體授與它存取 tooresources 透過以角色為基礎的存取控制。 它會顯示如何使用密碼或憑證 tooauthenticate 應用程式。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a>使用 Azure CLI toocreate 服務主體 tooaccess 資源

當您擁有的應用程式或需要 tooaccess 資源的指令碼時，您可以設定 hello 應用程式的身分識別，並驗證它自己的認證與 hello 應用程式。 此身分識別就是所謂的服務主體。 這種方法可讓您︰

* 指派權限 toohello 不同於您自己的權限的應用程式識別。 一般而言，這些權限會限制的 tooexactly 哪些 hello 應用程式需要 toodo。
* 使用憑證在執行無人看管的指令碼時進行驗證。

本文章將示範如何 toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset 組成的應用程式 toorun 在它自己的認證和身分識別。 安裝新版的 hello [Azure CLI 1.0](../cli-install-nodejs.md) toomake 確定您的環境符合本文章中的 hello 範例。

## <a name="required-permissions"></a>所需的權限
toocomplete 本主題中，您必須在您的 Azure Active Directory 和 Azure 訂用帳戶擁有足夠的權限。 具體來說，您必須是能夠 toocreate hello Azure Active Directory 中的應用程式，並且將 hello 服務主體 tooa 角色指派。 

hello 最簡單方式 toocheck 您的帳戶是否有足夠的權限是透過 hello 入口網站。 請參閱[在入口網站中檢查必要的權限](resource-group-create-service-principal-portal.md#required-permissions)。

現在，任何繼續 tooa 區段[密碼](#create-service-principal-with-password)或[憑證](#create-service-principal-with-certificate)驗證。

## <a name="create-service-principal-with-password"></a>使用密碼建立服務主體
在本節中，您要執行 hello 步驟 toocreate hello 與密碼，AD 應用程式，並指派 hello 讀取器角色 toohello 服務主體。

1. 登入 tooyour 帳戶。
   
   ```azurecli
   azure login
   ```
2. toocreate 一個應用程式的身分識別提供 hello hello 應用程式名稱及密碼，hello 下列命令所示：
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   會傳回 hello 新的服務主體。 授與權限時，就需要物件識別碼 hello。 中的記錄時，就需要 hello guid 與 hello 服務主要名稱一起列出。 此 guid 為 hello 與 hello 應用程式識別碼相同的值。Hello 範例應用程式中，這個值會為參考的 tooas hello `Client ID`。 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. 授與 hello 服務主體權限您訂用帳戶。 在此範例中，您可以將 hello 服務主體 toohello 讀取器角色，授與權限 tooread hello 訂用帳戶中的所有資源。 若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。 Hello objectid 參數，提供您建立 hello 應用程式時使用的物件識別碼 hello。 然後再執行此命令，您必須等候一段時間的 hello 新服務主體 toopropagate 整個 Azure Active Directory。 當您手動執行這些命令時，通常工作與工作之間經過的時間已足夠。 在指令碼中，您應該加入步驟 toosleep hello 命令之間 (例如`sleep 15`)。 如果您看到主體的錯誤指出 hello 不存在於 hello 目錄，請重新執行 hello 命令。
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
就這麼簡單！ 您的 AD 應用程式和服務主體已設定好。 hello 下一步 區段會顯示以 hello toolog 透過 Azure CLI 的認證。 如果您想 toouse hello 認證在應用程式程式碼中，您不需要 toocontinue 與這個主題。 您可以跳 toohello[範例應用程式](#sample-applications)登入您的應用程式識別碼和密碼的範例。 

### <a name="provide-credentials-through-azure-cli"></a>透過 Azure CLI 提供認證
現在，您必須在 toolog 為 hello tooperform 應用程式的作業。

1. 每當您登入做為服務主體時，您需要 tooprovide hello 租用戶識別碼 hello 目錄的 AD 應用程式。 租用戶是 Azure Active Directory 的執行個體。 tooretrieve hello 您目前已驗證的訂閱，使用的租用戶識別碼：
   
   ```azurecli
   azure account show
   ```
   
   它會傳回：
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     如果您需要 tooget hello 租用戶識別碼的其他訂用帳戶，請使用下列命令的 hello:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. 如果您需要 tooretrieve hello 用戶端識別碼 toouse 登入，請使用：
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     記錄的 hello 值 toouse 是 hello hello 服務主體名稱中所列的 guid。
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. Hello 服務主體的身分登入。
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    系統提示您輸入 hello 密碼。 提供建立 hello AD 應用程式時，您所指定的 hello 密碼。
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

您現在會為您建立的 hello 服務主體的 hello 服務主體進行驗證。

或者，您可以叫用中的 hello 命令列 toolog 從 REST 作業。 從 hello 驗證回應，您可以擷取 hello 存取權杖用於其他作業。 藉由叫用 REST 作業擷取 hello 存取權杖的範例，請參閱[產生存取權杖](resource-manager-rest-api.md#generating-an-access-token)。

## <a name="create-service-principal-with-certificate"></a>使用憑證建立服務主體
在本節中，您可以執行 hello 步驟：

* 建立自我簽署憑證
* hello 憑證與 hello 服務主體建立 hello AD 應用程式
* 指派 hello 讀取器角色 toohello 服務主體

toocomplete 這些步驟，您必須擁有[OpenSSL](http://www.openssl.org/)安裝。

1. 建立自我簽署憑證。
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. 上述步驟建立兩個檔案-privkey.pem 和 cert.pem hello。 將 hello 公用和私用金鑰結合成單一檔案。

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. 開啟 hello **examplecert.pem**檔案，並尋找 hello 個之間字元的長串**---BEGIN CERTIFICATE---**和**---憑證結尾---**。 將複製 hello 憑證資料。 建立 hello 服務主體時，您可以傳遞做為參數的資料。

4. 登入 tooyour 帳戶。

   ```azurecli
   azure login
   ```
5. toocreate hello 服務主體，會提供 hello 名稱 hello 應用程式和 hello 憑證資料，hello 下列命令所示：
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   會傳回 hello 新的服務主體。 授與權限時，就需要物件識別碼 hello。 中的記錄時，就需要 hello guid 與 hello 服務主要名稱一起列出。 此 guid 為 hello 與 hello 應用程式識別碼相同的值。Hello 範例應用程式中，這個值會為參考的 tooas hello 用戶端識別碼。 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. 授與 hello 服務主體權限您訂用帳戶。 在此範例中，您可以將 hello 服務主體 toohello 讀取器角色，授與權限 tooread hello 訂用帳戶中的所有資源。 若為其他角色，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。 Hello objectid 參數，提供您建立 hello 應用程式時使用的物件識別碼 hello。 然後再執行此命令，您必須等候一段時間的 hello 新服務主體 toopropagate 整個 Azure Active Directory。 當您手動執行這些命令時，通常工作與工作之間經過的時間已足夠。 在指令碼中，您應該加入步驟 toosleep hello 命令之間 (例如`sleep 15`)。 如果您看到主體的錯誤指出 hello 不存在於 hello 目錄，請重新執行 hello 命令。
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a>透過自動化的 Azure CLI 指令碼提供憑證
現在，您必須在 toolog 為 hello tooperform 應用程式的作業。

1. 每當您登入做為服務主體時，您需要 tooprovide hello 租用戶識別碼 hello 目錄的 AD 應用程式。 租用戶是 Azure Active Directory 的執行個體。 tooretrieve hello 您目前已驗證的訂閱，使用的租用戶識別碼：
   
   ```azurecli
   azure account show
   ```
   
   它會傳回：
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   如果您需要 tooget hello 租用戶識別碼的其他訂用帳戶，請使用下列命令的 hello:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. tooretrieve hello 憑證指紋和移除不必要的字元，請使用：
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   這會傳回指紋值，類似：
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. 如果您需要 tooretrieve hello 用戶端識別碼 toouse 登入，請使用：
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   記錄的 hello 值 toouse 是 hello hello 服務主體名稱中所列的 guid。
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. Hello 服務主體的身分登入。
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

您現在會做為 hello hello 您建立的 Azure Active Directory 應用程式之主體的服務進行驗證。

## <a name="change-credentials"></a>管理認證

AD 應用程式，因為安全性洩露或認證過期的 toochange hello 認證使用`azure ad app set`。

toochange 密碼，請使用：

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

toochange 憑證的值，請使用：

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a>偵錯

您可能會遇到下列錯誤，建立服務主體時的 hello:

* **「 Authentication_Unauthorized"**或**」 沒有訂用帳戶中找到 hello 內容。 」** -您會看到這個錯誤，當您的帳戶未具備 hello[必要的權限](#required-permissions)hello Azure Active Directory tooregister 應用程式上。 通常，只有 Azure Active Directory 中的管理使用者可以註冊應用程式，且您的帳戶不是系統管理員時，就會看到此錯誤。請要求系統管理員 tooeither 指派您 tooan 系統管理員角色或 tooenable 使用者 tooregister 應用程式。

* 您的帳戶**」 沒有授權 tooperform 動作 'Microsoft.Authorization/roleAssignments/write' 對範圍 ' / 訂用帳戶 / {guid}'。 」** -當您的帳戶未具備足夠的權限 tooassign 角色 tooan 身分識別，您會看到此錯誤。 詢問您的訂用帳戶管理員 tooadd 您 tooUser 存取 」 系統管理員角色。

## <a name="sample-applications"></a>範例應用程式
如需透過不同平台的 hello 應用程式以登入資訊，請參閱：

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>後續步驟
* 如需整合到 Azure 的應用程式管理資源的詳細步驟，請參閱[以 hello Azure 資源管理員 API 的開發人員指南 tooauthorization](resource-manager-api-authentication.md)。
* tooget 需使用憑證和 Azure CLI，請參閱[憑證型驗證的 Azure 服務主體使用 Linux 命令列從](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx)。 
* 如需可授與或拒絕 toousers 可用動作的清單，請參閱[Azure 資源管理員資源提供者作業](../active-directory/role-based-access-control-resource-provider-operations.md)。
