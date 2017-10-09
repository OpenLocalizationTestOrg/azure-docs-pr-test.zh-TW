---
title: "aaaDeploy，呼叫，並驗證 web 應用程式開發介面 （& s） REST Api 針對 Azure 邏輯應用程式 |Microsoft 文件"
description: "在工作流程中部署、驗證並呼叫 web API 與 REST API，以便與 Azure Logic Apps 進行系統整合"
keywords: "web API, REST API, 連接器, 工作流程, 系統整合, 驗證"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>部署、呼叫並驗證自訂 API 作為 Logic Apps 的連接器

之後您[建立自訂 Api](./logic-apps-create-api-app.md) ，提供邏輯在動作或觸發程序 toouse 應用程式工作流程，可以呼叫之前，您必須部署您的應用程式開發介面。 雖然 hello 達到最佳體驗效果，您可以從邏輯應用程式呼叫任何 API，新增和[Swagger 中繼資料](http://swagger.io/specification/)描述您的 API 作業和參數。 Swagger 檔案可協助您改善 API 工作，並更輕鬆地整合 Logic Apps。

您可以部署與您 Api [web 應用程式](../app-service-web/app-service-web-overview.md)，但請考慮部署與您 Api [API apps](../app-service-api/app-service-api-apps-why-best-platform.md)，這可讓您的工作更容易當您建置、 裝載，並使用 Api hello 雲端與內部部署。 您不需要 toochange 任何程式碼在您的應用程式開發介面中--只部署 tooan API 應用程式程式碼。 您可以在裝載您 Api [Azure App Service](../app-service/app-service-value-prop-what-is.md)、 平台做為服務 (PaaS) 供應項目，提供一種 hello 最佳、 簡單的方法，和擴充性最高裝載應用程式開發介面。

tooauthenticate 從邏輯應用程式 tooyour Api 的呼叫，您可以設定 Azure Active Directory 中 hello Azure 入口網站，您無需 tooupdate 您的程式碼。 或者，您可以透過您的 API 程式碼要求並強制執行驗證。

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>將您的 API 部署為 web 應用程式或 API 應用程式

您可以從邏輯應用程式呼叫自訂 API 之前，請將做為 web 應用程式或應用程式開發介面應用程式 tooAzure App Service API 部署。 此外，toomake hello 邏輯應用程式的設計工具，供讀取文件 Swagger 設定 hello API 定義屬性並開啟[跨原始資源共用 (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig)的 web 應用程式或應用程式開發介面應用程式。

1. 在 hello Azure 入口網站，選取您的 web 應用程式或應用程式開發介面應用程式。

2. 在 hello 刀鋒視窗中開啟，底下**API**，選擇**API 定義**。 設定 hello **API 定義位置**toohello swagger.json 檔案的 URL。

   通常，hello URL 會出現在這種格式：`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![自訂 api 的連結 tooSwagger 檔案](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. 在 [API] 下，選擇 [CORS]。 設定的 CORS 原則 hello**允許出處**太**'*'** （全部允許）。

   此設定允許來自 Logic App Designer 的要求。

   ![允許從邏輯應用程式的設計工具 tooyour 自訂 API 要求](media/logic-apps-custom-hosted-api/custom-api-cors.png)

如需詳細資訊，請參閱這些文章：

* [新增 ASP.NET web API 的 Swagger 中繼資料](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [部署 ASP.NET web Api tooAzure 應用程式服務](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>從邏輯應用程式工作流程呼叫自訂 API

Hello API 定義屬性和 CORS 設定之後，您的自訂 API 的觸發程序和動作應該可用於 tooinclude 邏輯應用程式工作流程中。 

*  tooview hello 具有 Swagger Url 的網站，您可以瀏覽您的訂用帳戶網站在 hello 邏輯應用程式的設計工具中。

*  tooview 可用的動作，並指向 Swagger 文件中，輸入使用 hello [HTTP + Swagger 動作](../connectors/connectors-native-http-swagger.md)。

*  toocall 任何應用程式開發介面，包括應用程式開發介面不具有或公開 Swagger 文件中，您一律可以建立要求以 hello [HTTP 動作](../connectors/connectors-native-http.md)。

## <a name="authenticate-calls-tooyour-custom-api"></a>驗證呼叫 tooyour 自訂 API

您可以保護以下列方式呼叫 tooyour 自訂 API:

* [變更任何程式碼](#no-code)： 保護您的 API 與[Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md)透過 hello Azure 入口網站，因此您尚未 tooupdate 您的程式碼，或重新部署您的 API。

  > [!NOTE]
  > 根據預設，開啟 hello Azure 入口網站中的 hello Azure AD 驗證不會提供更細緻的授權。 比方說，這項驗證會鎖定 API toojust 特定租用戶、 不 tooa 特定使用者或應用程式。 

* [更新您的 API 程式碼](#update-code)：保護您的 API，方法是透過程式碼強制執行[憑證驗證](#certificate)、[基本驗證](#basic)，或 [Azure AD 驗證](#azure-ad-code)。

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a>驗證呼叫 tooyour 應用程式開發介面，而不需要變更程式碼

以下是 hello，此方法的一般步驟：

1. 將建立兩個 [Azure Active Directory (Azure AD) 應用程式識別](../app-service-api/app-service-api-dotnet-service-principal-auth.md)：一個用於邏輯應用程式，一個用於 Web 應用程式 (或 API 應用程式)。

2. tooauthenticate 呼叫 tooyour 應用程式開發介面，用於 hello hello 認證 （用戶端識別碼和密碼）[服務主體](../app-service-api/app-service-api-dotnet-service-principal-auth.md)，具有相關聯的 hello 邏輯應用程式的 Azure AD 應用程式識別。

3. 包含在邏輯應用程式定義中的 hello 應用程式識別碼。

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>第 1 部分：建立 Azure AD 邏輯應用程式的應用程式識別碼

邏輯應用程式會使用 Azure AD 中針對這個 Azure AD 應用程式識別 tooauthenticate。 您只需要註冊這個身分識別 tooset 一次為您的目錄。 例如，您可以選擇 toouse hello 針對您的邏輯應用程式，相同的識別，即使您可以建立的每個邏輯應用程式的唯一身分識別。 您可以設定在 hello Azure 入口網站，這些身分識別[Azure 傳統入口網站](#app-identity-logic-classic)，或使用[PowerShell](#powershell)。

**在 hello Azure 入口網站中建立 hello 邏輯應用程式的應用程式識別**

1. 在 hello [Azure 入口網站](https://portal.azure.com "https://portal.azure.com")，選擇**Azure Active Directory**。 

2. 確認您在 hello 與 web 應用程式或應用程式開發介面應用程式相同的目錄。

   > [!TIP]
   > tooswitch 目錄中，按一下您的設定檔，然後選取另一個目錄。 或者，選擇 [概觀] > [切換目錄]。

3. Hello 目錄在功能表上，在**管理**，選擇**應用程式註冊** > **新應用程式註冊**。

   > [!TIP]
   > 根據預設，hello 應用程式註冊清單會顯示所有應用程式註冊您的目錄中。 只有您的應用程式註冊下, 一步 toohello 搜尋方塊中，選取 tooview**我的應用程式**。 

   ![建立新的應用程式註冊](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. 指定您的應用程式身分識別名稱，並保留**應用程式類型**設定得**Web 應用程式 / 應用程式開發介面**，提供唯一字串格式的網域為**登入 URL**，選擇**建立**。

   ![提供應用程式識別碼的名稱和登入 URL](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   您現在建立應用程式邏輯的 hello 應用程式識別碼會出現在 hello 應用程式註冊清單。

   ![邏輯應用程式的應用程式識別碼](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. 在 hello 應用程式註冊清單中，選取新的應用程式識別。 複製並儲存 hello**應用程式識別碼**toouse 為 hello 「 用戶端識別碼 」，在第 3 篇應用程式邏輯。

   ![複製並儲存邏輯應用程式的應用程式識別碼](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. 如果看不到您的應用程式識別碼設定，請選擇 [設定] 或 [所有設定]。

7. 在 [API 存取] 下，選擇 [金鑰]。 在 [描述] 下，提供您金鑰的名稱。 在 [到期時間] 下，選取您金鑰的持續時間。

   您要建立 hello 金鑰做為 hello 應用程式識別的 「 密碼 」 或邏輯應用程式密碼。

   ![建立邏輯應用程式身分識別的金鑰](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. 在 hello 工具列上選擇 **儲存**。 在 [值] 下，現在會顯示您的金鑰。 
**請確定 toocopy 和儲存您的金鑰**供稍後使用隱藏 hello 索引鍵，因此當您離開 hello 金鑰刀鋒視窗。

   當您在第 3 篇設定應用程式邏輯時，您指定這個機碼，如 hello 「 密碼 」 或密碼。

   ![複製並儲存金鑰供稍後使用](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**在 hello Azure 傳統入口網站中建立 hello 邏輯應用程式的應用程式識別**

1. 在 hello Azure 傳統入口網站中選擇[ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory)。

2. 選取 hello 您用於 web 應用程式或應用程式開發介面應用程式的相同目錄。

3. 在 hello**應用程式**索引標籤上，選擇**新增**hello hello 頁底端。

4. 為您的應用程式識別碼提供名稱，然後選擇 **[下一步]** \(向右箭號)。

5. 在 [應用程式屬性] 下，提供格式化為**登入 URL** 和**應用程式識別碼 URI** 之網域的唯一字串，然後選擇 [完成] \(勾選記號)。

6. 在 hello**設定**索引標籤上，複製並儲存 hello**用戶端識別碼**如您在第 3 篇的邏輯應用程式 toouse。

7. 在下**金鑰**，開啟 hello**選取持續時間**清單。 選取您金鑰的持續時間。

   您要建立 hello 金鑰做為 hello 應用程式識別的 「 密碼 」 或邏輯應用程式密碼。

8. 在 hello hello 頁面底部，選擇**儲存**。 您可能必須 toowait 幾秒鐘的時間。

9. 在下**金鑰**，請確定 toocopy 儲存 hello 金鑰現在會出現。 

   當您在第 3 篇設定應用程式邏輯時，您指定這個機碼，如 hello 「 密碼 」 或密碼。

如需詳細資訊，了解如何太[設定您應用程式服務應用程式 toouse 的 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。

<a name="powershell"></a>

**在 PowerShell 中建立應用程式邏輯的 hello 應用程式識別**

您可以使用 PowerShell，透過 Azure Resource Manager 來執行這項工作中。 在 PowerShell 中，執行以下命令：

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. 請確定 toocopy hello**租用戶識別碼**(Azure AD 租用戶的 GUID)，hello**應用程式識別碼**，和您所使用的 hello 密碼。

如需詳細資訊，了解如何太[PowerShell tooaccess 資源以建立服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)。

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>第 2 部分：建立 Web 應用程式或 API 應用程式的 Azure AD 應用程式識別碼

如果已部署 web 應用程式或應用程式開發介面應用程式，則可以啟用驗證，並在 hello Azure 入口網站中建立 hello 應用程式識別。 否則，您可以[在您使用 Azure Resource Manager 範本進行部署時開啟驗證](#authen-deploy)。 

**建立 hello 應用程式識別，然後開啟 hello 部署的應用程式的 Azure 入口網站中的驗證**

1. 在 hello [Azure 入口網站](https://portal.azure.com "https://portal.azure.com")、 尋找並選取您的 web 應用程式或應用程式開發介面應用程式。 

2. 在 [設定] 下，選擇 [驗證/授權]。 在 [App Service 驗證] 下，將驗證 [開啟]。 在 [驗證提供者] 下，選擇 [Azure Active Directory]。

   ![開啟驗證](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. 現在建立 Web 應用程式或 API 應用程式的應用程式識別碼，如下所示。 在 hello **Azure Active Directory 設定**刀鋒視窗中，設定**管理模式**太**Express**。 選擇 [建立新的 AD 應用程式]。 為您的應用程式識別碼提供名稱，然後選擇 **[確定]**。 

   ![建立 Web 應用程式或 API 應用程式的應用程式識別碼](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. 在 hello**驗證 / 授權刀鋒視窗**，選擇**儲存**。

現在您必須尋找 hello 用戶端識別碼和租用戶識別碼 hello 與 web 應用程式或應用程式開發介面應用程式相關聯的應用程式識別。 您可以在第 3 部分中使用這些識別碼。 因此繼續執行下列步驟 hello Azure 入口網站或[Azure 傳統入口網站](#find-id-classic)。

**尋找應用程式識別用戶端識別碼和您的 web 應用程式或 hello Azure 入口網站中的應用程式開發介面應用程式的租用戶識別碼**

1. 在 [驗證提供者] 下，選擇 [Azure Active Directory]。 

   ![選擇 [Azure Active Directory]](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. 在 hello **Azure Active Directory 設定**刀鋒視窗中，設定**管理模式**太**進階**。

3. 複製 hello**用戶端識別碼**，並將 GUID 用於儲存在第 3 篇。

   > [!TIP] 
   > 如果**用戶端識別碼**和**簽發者 Url**不會出現，請嘗試重新整理 hello Azure 入口網站，重複步驟 1。

4. 在下**簽發者 Url**、 複製和儲存 just hello GUID 部分 3。 您也可以視需要在您的 web 應用程式或 API 應用程式的部署範本中使用此 GUID。

   此 GUID 是您特定租用戶的 GUID (「租用戶 ID」)，且應該會出現在此 URL：`https://sts.windows.net/{GUID}`

5. 不儲存變更，關閉 hello **Azure Active Directory 設定**刀鋒視窗。

<a name="find-id-classic"></a>

**尋找應用程式識別用戶端識別碼和您的 web 應用程式或 hello Azure 傳統入口網站中的應用程式開發介面應用程式的租用戶識別碼**

1. 在 hello Azure 傳統入口網站中選擇[ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory)。

2.  選取您要用於 web 應用程式或應用程式開發介面應用程式的 hello 目錄。

3. 在 hello**搜尋**，尋找並選取 web 應用程式或應用程式開發介面應用程式的 hello 應用程式識別。

4. 在 hello**設定**索引標籤上，複製 hello**用戶端識別碼**，並儲存在第 3 篇使用 GUID。

5. 取得 hello 用戶端識別碼，在 hello 底部 hello 之後**設定**索引標籤上，選擇**檢視端點**。

6. 複製 hello URL**同盟中繼資料文件**，並瀏覽 toothat URL。

7. 在開啟 hello 中繼資料文件中尋找 hello 根**EntityDescriptor 識別碼**項目，其具有**entityID**這種形式的屬性：`https://sts.windows.net/{GUID}` 

      這個屬性中的 hello GUID 是特定租用戶的 GUID (租用戶 ID)。

8. 複製 hello 租用戶識別碼，並視需要儲存在第 3 部分和 toouse 在您 web 應用程式或應用程式開發介面應用程式的部署範本，使用該識別碼。

如需詳細資訊，請參閱下列主題：

* [Azure App Service 中 API 應用程式的使用者驗證](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Azure App Service 中的驗證與授權](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**在您使用 Azure Resource Manager 範本進行部署時開啟驗證**

您仍然必須從 hello 應用程式識別建立 web 應用程式或不同的應用程式開發介面應用程式的 Azure AD 應用程式身分識別，邏輯應用程式。 toocreate hello 應用程式識別，後續 hello 先前步驟中第 2 部分 hello Azure 入口網站。 您也可以在第 1 部分中的 hello 步驟，但請確定 toouse web 應用程式或應用程式開發介面應用程式的實際`https://{URL}`如**登入 URL**和**應用程式識別碼 URI**。 這些步驟中，您有 toosave 這兩個 hello 用戶端識別碼和您的應用程式部署範本中使用，也部分 3 的租用戶識別碼。

> [!NOTE]
> 當您建立 web 應用程式或應用程式開發介面應用程式的 hello Azure AD 應用程式識別時，您必須使用 hello Azure 入口網站或 Azure 傳統入口網站，而不是 PowerShell。 hello PowerShell 指令程式不會設定所需的 hello 權限 toosign 使用者在網站。

取得 hello 用戶端識別碼和租用戶識別碼之後，將這些識別碼納入 subresource web 應用程式或部署範本中的應用程式開發介面應用程式：

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

tooautomatically 部署空白 web 應用程式和邏輯應用程式與 Azure Active Directory 驗證[檢視 hello 完成範本這裡](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json)，或按一下**部署 tooAzure**這裡：

[![部署 tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a>第 3 部分： 填入邏輯應用程式中的 hello 授權 > 一節

hello 先前的範本已設定好之後，此授權 > 一節，但如果您直接撰寫 hello 邏輯應用程式，您必須包含 hello 完整授權 > 一節。

開啟您的邏輯應用程式定義在程式碼檢視中，移 toohello **HTTP**動作 區段中，尋找 hello**授權**區段，並加入這一行：

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| 元素 | 說明 |
| ------- | ----------- |
| tenant |hello GUID hello Azure AD 租用戶 |
| audience |必要。 您想 tooaccess-hello hello web 應用程式或應用程式開發介面應用程式的應用程式識別用戶端識別碼 hello 目標資源的 hello GUID |
| clientId |hello GUID hello 用戶端要求存取-hello hello 邏輯應用程式的應用程式識別用戶端識別碼 |
| secret |必要。 hello 金鑰或密碼，從 hello hello hello 存取權杖要求的用戶端應用程式識別 |
| 類型 |hello 驗證類型。 ActiveDirectoryOAuth 驗證的 hello 值是`ActiveDirectoryOAuth`。 |

例如：

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a>透過程式碼保護 API 呼叫

<a name="certificate"></a>

#### <a name="certificate-authentication"></a>憑證驗證

toovalidate hello 源自的連入邏輯應用程式 tooyour web 應用程式或應用程式開發介面應用程式，您可以使用用戶端憑證。 深入了解程式碼，tooset[如何 tooconfigure TLS 相互驗證](../app-service-web/app-service-web-configure-tls-mutual-auth.md)。

在 hello**授權**區段中，加入這一行： 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| 元素 | 說明 |
| ------- | ----------- |
| 類型 |必要。 hello 驗證類型。 SSL 用戶端憑證，hello 值必須是`ClientCertificate`。 |
| password |必要。 hello 密碼存取 hello 用戶端憑證 （PFX 檔案） |
| pfx |必要。 Base64 編碼內容的 hello 用戶端憑證 （PFX 檔案） |

<a name="basic"></a>

#### <a name="basic-authentication"></a>基本驗證

toovalidate 源自的連入邏輯應用程式 tooyour web 應用程式或應用程式開發介面應用程式，您可以使用基本驗證，例如使用者名稱和密碼。 基本驗證是常見的模式，和 web 應用程式或應用程式開發介面應用程式，您可以使用任何語言使用 toobuild 在此驗證。

在 hello**授權**區段中，加入這一行：

`{"type": "basic", "username": "username", "password": "password"}`。

| 元素 | 說明 |
| --- | --- |
| 類型 |必要。 hello 驗證類型。 Hello 值必須是基本驗證， `Basic`。 |
| username |必要。 hello 進行驗證的使用者名稱 |
| password |必要。 hello 密碼進行驗證 |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>透過程式碼驗證 Azure Active Directory

根據預設，開啟 hello Azure 入口網站中的 hello Azure AD 驗證不會提供更細緻的授權。 比方說，這項驗證會鎖定 API toojust 特定租用戶、 不 tooa 特定使用者或應用程式。 

toorestrict API 存取 tooyour 邏輯應用程式透過程式碼，擷取已 hello JSON web 權杖 (JWT) 的 hello 標頭。 檢查 hello 呼叫者的身分識別，並拒絕不符合要求。

繼續進行，tooimplement 此驗證您自己的程式碼以及不使用 hello Azure 入口網站中的完全了解如何太[以在 Azure 應用程式中的內部部署 Active Directory 驗證](../app-service-web/web-sites-authentication-authorization.md)。

toocreate 邏輯應用程式的應用程式識別和使用該身分識別 toocall 您的 API，您必須依照 hello 先前的步驟。

## <a name="next-steps"></a>後續步驟

* [使用診斷記錄及警示檢查邏輯應用程式效能](logic-apps-monitor-your-logic-apps.md)