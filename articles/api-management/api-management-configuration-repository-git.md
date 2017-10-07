---
title: "aaaConfigure 使用 Git-Azure API 管理服務 |Microsoft 文件"
description: "深入了解如何 toosave 並設定您使用 Git 的 API 管理服務組態。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a>如何 toosave 並設定您使用 Git 的 API 管理服務設定
> 
> 

每個 API 管理服務執行個體維護組態資料庫，其中包含 hello 組態與 hello 服務執行個體的中繼資料的相關資訊。 可以變更 toohello 服務執行個體變更 hello 發行者入口網站中的設定、 使用 PowerShell cmdlet 或 REST API 呼叫。 此外 toothese 方法，您也可以管理您的服務執行個體設定使用 Git，請啟用服務管理案例，例如：

* 組態版本 - 下載並儲存不同版本的服務組態
* 大量的組態變更-在本機儲存機制中進行變更 toomultiple 組件的服務組態和整合 hello 變更後 toohello 與單一作業
* 熟悉 Git 工具鏈和工作流程-使用 hello Git 工具，以及您已熟悉的工作流程

hello 下列圖表顯示 hello 不同的方式 tooconfigure 概觀您 API 管理服務執行個體。

![Git 設定][api-management-git-configure]

當您使用 hello 發行者入口網站、 PowerShell cmdlet 或 REST API hello tooyour 服務進行變更時，您要管理服務設定資料庫使用 hello`https://{name}.management.azure-api.net`端點，右邊 hello hello 圖表所示。 hello 左下的方 hello 圖表將說明如何管理您使用 Git 的服務組態和您服務的 Git 儲存機制位於`https://{name}.scm.azure-api.net`。

hello 下列步驟提供管理 API 管理服務執行個體使用 Git 的概觀。

1. 存取服務中的 Git 組態
2. 儲存您服務組態資料庫 tooyour Git 儲存機制
3. 複製 hello Git 儲存機制 tooyour 本機電腦
4. 提取下 tooyour 本機 hello 最新的儲存機制和認可並推送變更後 tooyour 儲存機制
5. 從您的儲存機制的 hello 變更部署至您的服務組態資料庫

本文說明如何 tooenable 和您的服務組態使用 Git toomanage hello Git 儲存機制中的 hello 檔案和資料夾提供的參考。

## <a name="access-git-configuration-in-your-service"></a>存取服務中的 Git 組態
您可以在 hello 右上角的 hello 發行者入口網站中檢視 hello Git 圖示，快速檢視 hello Git 組態狀態。 在此範例中，hello 狀態訊息會指出有未儲存的變更 toohello 儲存機制。 這是因為 hello API 管理服務組態資料庫有尚未儲存 toohello 儲存機制。

![Git 狀態][api-management-git-icon-enable]

tooview 和設定您的 Git 組態設定，您可以按一下 hello Git 圖示，或按一下 hello**安全性**功能表和瀏覽 toohello**設定存放庫** 索引標籤。

![啟用 GIT][api-management-enable-git]

> [!IMPORTANT]
> 屬性會儲存在 hello 儲存機制，並將保留在其歷程記錄，直到您未定義任何機密停用然後重新啟用 Git 權限。 屬性會提供安全的地方 toomanage 常數字串值，所以您不需 toostore，包括密碼，跨所有應用程式開發介面設定和原則，它們直接在您的原則陳述式中。 如需詳細資訊，請參閱[如何在 Azure API 管理原則中的 toouse 屬性](api-management-howto-properties.md)。
> 
> 

啟用或停用使用 hello REST API 的 Git 存取資訊，請參閱[啟用或停用使用 hello REST API 的 Git 存取](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit)。

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a>toosave hello 服務組態 toohello Git 儲存機制
hello 複製 hello 儲存機制之前的第一個步驟是 toosave hello 目前狀態的 hello 服務組態 toohello 儲存機制。 按一下**儲存組態 toorepository**。

![儲存組態][api-management-save-configuration]

Hello 確認畫面上進行任何所需的變更，然後按一下 **確定**toosave。

![儲存組態][api-management-save-configuration-confirm]

在幾分鐘之後會儲存 hello 組態，並且會顯示 hello 儲存機制 hello 組態狀態，包括 hello 日期和時間 hello 最後一項組態變更，而且 hello 之間 hello 服務組態和 hello 上次同步處理儲存機制。

![組態狀態][api-management-configuration-status]

一旦 toohello 儲存機制時，會儲存 hello 組態，可以被複製。

如需執行這項作業使用 hello REST API 的資訊，請參閱[認可組態快照集使用 REST API hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot)。

## <a name="tooclone-hello-repository-tooyour-local-machine"></a>tooclone hello 儲存機制 tooyour 本機電腦
tooclone 儲存機制，您需要 hello URL tooyour 儲存機制、 使用者名稱和密碼。 hello 使用者名稱和 URL 會顯示 hello hello 頂端附近**設定存放庫** 索引標籤。

![git 複製][api-management-configuration-git-clone]

在 hello hello 底端會產生 hello 密碼**設定存放庫** 索引標籤。

![產生密碼][api-management-generate-password]

toogenerate 密碼，必須先確定該 hello**到期**是設定 toohello 預期到期日和時間，然後按一下**產生語彙基元**。

![密碼][api-management-password]

> [!IMPORTANT]
> 記下此密碼。 一旦您離開此頁面 hello 密碼不會再次顯示。
> 
> 

下列範例使用 hello Git Bash hello 工具[Git for Windows](http://www.git-scm.com/downloads)但您可以使用任何您已熟悉的 Git 工具。

在 hello 所要的資料夾中開啟您的 Git 工具，並執行下列命令 tooclone hello git 儲存機制 tooyour 本機電腦，請使用 hello 命令 hello 發行者入口網站所提供的 hello。

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Hello 使用者名稱和密碼提示時提供。

如果您收到任何錯誤，請嘗試修改您`git clone`命令 tooinclude hello 使用者名稱和密碼，hello 下列範例所示。

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

如果這會提供錯誤，請再試一次 URL 編碼 hello 命令 hello 密碼部分。 一個快速方式 toodo 這是 tooopen Visual Studio 中，而且問題 hello 下列命令在 hello**即時運算視窗**。 tooopen hello**即時運算視窗**、 Visual Studio 中開啟任何方案或專案 （或建立新的空白的主控台應用程式），然後選擇  **Windows**，**即時運算**從hello**偵錯**功能表。

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

使用 hello 編碼密碼，以及使用者名稱和儲存機制位置 tooconstruct hello git 命令。

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

一旦複製 hello 儲存機制是您可以檢視，並在您的本機檔案系統中使用它。 如需詳細資訊，請參閱 [本機 Git 儲存機制的檔案和資料夾結構參考](#file-and-folder-structure-reference-of-local-git-repository)。

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a>tooupdate 本機儲存機制與 hello 最新的服務執行個體組態
如果您在 hello 發行者入口網站或使用 hello REST API 中進行變更 tooyour API 管理服務執行個體，您必須先儲存這些變更 toohello 儲存機制之前您可以使用 hello 最新的變更來更新本機儲存機制。 toodo 此，依序按一下**儲存組態 toorepository**上 hello**設定存放庫**hello 發行者入口網站，在索引標籤，然後發出下列命令在本機儲存機制中的 hello。

```
git pull
```

執行前`git pull`確認您的本機儲存機制是 hello 資料夾中。 如果您剛完成 hello`git clone`命令時，則您必須變更 hello 目錄 tooyour 儲存機制，藉由執行 hello 下列類似的命令。

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a>從本機儲存機制 toohello 伺服器儲存機制的 toopush 變更
toopush 變更從本機儲存機制 toohello 伺服器儲存機制，您必須認可您的變更，然後將其推送 toohello 伺服器儲存機制。 toocommit 您的變更，開啟您的 Git 命令工具，本機儲存機制，與下列命令的問題 hello 的交換器 toohello 目錄。

```
git add --all
git commit -m "Description of your changes"
```

toopush hello 的所有認可 toohello 伺服器上執行下列命令 hello。

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a>toodeploy 任何服務組態變更 toohello API 管理服務執行個體
一旦您的本機變更認可並推送 toohello 伺服器儲存機制，您可以將它們部署 tooyour API 管理服務執行個體。

![部署][api-management-configuration-deploy]

如需執行這項作業使用 hello REST API 的資訊，請參閱[部署 Git 變更 tooconfiguration 資料庫使用 REST API hello](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration)。

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>本機 Git 儲存機制的檔案和資料夾結構參考
hello hello 本機 git 儲存機制中檔案和資料夾包含 hello 關於 hello 服務執行個體的組態資訊。

| Item | 說明 |
| --- | --- |
| 根 api 管理資料夾 |包含最上層 hello 服務執行個體組態 |
| apis 資料夾 |包含 hello 服務執行個體中的 hello 應用程式開發介面的 hello 組態 |
| 群組資料夾 |Hello 服務執行個體中包含 hello hello 群組組態 |
| 原則資料夾 |Hello 服務執行個體中包含 hello 原則 |
| portalStyles 資料夾 |Hello 服務執行個體中包含 hello hello 開發人員入口網站的自訂項目組態 |
| 產品資料夾 |Hello 服務執行個體中包含 hello hello 產品的組態 |
| 範本資料夾 |Hello 服務執行個體中包含 hello hello 電子郵件範本的組態 |

每個資料夾可以包含一或多個檔案，在某些情況下可以包含一或多個資料夾，例如每個 API、產品或群組的資料夾。 每個資料夾中的 hello 檔案特有的 hello hello 資料夾名稱所描述的實體類型。

| 檔案類型 | 目的 |
| --- | --- |
| json |Hello 個別實體的組態資訊 |
| html |通常顯示 hello 開發人員入口網站中的 hello 實體有關的說明。 |
| xml |Policy statements |
| css |開發人員入口網站自訂的樣式表 |

這些檔案可以建立、 刪除、 編輯和管理您的本機檔案系統和 hello 變更部署後 toohello 您 API 管理服務執行個體。

> [!NOTE]
> hello 下列實體不會包含在 hello Git 儲存機制中，無法使用 Git 進行設定。
> 
> * 使用者
> * 訂用帳戶
> * 屬性
> * 樣式以外的開發人員入口網站實體
> 
> 

### <a name="root-api-management-folder"></a>根 api 管理資料夾
hello 根`api-management`資料夾包含`configuration.json`檔案，其中包含最上層 hello hello 遵循格式中的服務執行個體的相關資訊。

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

hello 前四個設定 (`RegistrationEnabled`， `UserRegistrationTerms`， `UserRegistrationTermsEnabled`，和`UserRegistrationTermsConsentRequired`) 對應 toohello 遵循 hello 設定**識別** 索引標籤中 hello**安全性**> 一節。

| 身分識別設定 | 太對應|
| --- | --- |
| RegistrationEnabled |**匿名使用者 toosign 頁面上將重新導向**核取方塊 |
| UserRegistrationTerms | 文字方塊 |
| UserRegistrationTermsEnabled | 核取方塊 |
| UserRegistrationTermsConsentRequired | 核取方塊 |

![身分識別設定][api-management-identity-settings]

hello 接下來四個設定 (`DelegationEnabled`， `DelegationUrl`， `DelegatedSubscriptionEnabled`，和`DelegationValidationKey`) 對應 toohello 遵循 hello 設定**委派** 索引標籤中 hello**安全性**> 一節。

| 委派設定 | 太對應|
| --- | --- |
| DelegationEnabled |[委派登入和註冊] 核取方塊 |
| DelegationUrl | 文字方塊 |
| DelegatedSubscriptionEnabled | 核取方塊 |
| DelegationValidationKey | 文字方塊 |

![委派設定][api-management-delegation-settings]

hello 最終設定， `$ref-policy`，對應 toohello hello 服務執行個體的全域原則陳述式檔案。

### <a name="apis-folder"></a>apis 資料夾
hello`apis`資料夾的每個應用程式開發介面包含一個資料夾，其中包含下列項目 hello hello 服務執行個體中。

* `apis\<api name>\configuration.json`-這是 hello API 的 hello 組態，而且包含 hello 後端服務 URL 和 hello 作業的相關資訊。 這是 hello 相同的資訊將會傳回，如果您 toocall[取得特定 API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI)與`export=true`中`application/json`格式。
* `apis\<api name>\api.description.html`-這是 hello hello API 描述和對應 toohello`description`屬性 hello [API 實體](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties)。
* `apis\<api name>\operations\`-此資料夾包含`<operation name>.description.html`toohello 作業 hello API 中的對應的檔案。 每個檔案包含單一作業中 hello API，其對應 toohello hello 描述`description`屬性 hello[作業實體](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties)hello REST API 中。

### <a name="groups-folder"></a>群組資料夾
hello`groups`資料夾包含 hello 服務執行個體中定義的每個群組的資料夾。

* `groups\<group name>\configuration.json`-這是 hello hello 群組組態。 這是 hello 相同的資訊將會傳回，如果您 toocall hello[取得特定群組](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup)作業。
* `groups\<group name>\description.html`-這是 hello hello 群組描述和對應 toohello`description`屬性 hello[群組實體](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties)。

### <a name="policies-folder"></a>原則資料夾
hello`policies`資料夾包含您的服務執行個體的 hello 原則陳述式。

* `policies\global.xml` - 包含在您服務執行個體的全域範圍中定義的原則。
* `policies\apis\<api name>\` - 如果您在 API 範圍中定義了任何原則，它們就會包含在此資料夾中。
* `policies\apis\<api name>\<operation name>\`資料夾-如果您有在作業範圍內定義的任何原則，它們包含在這個資料夾中`<operation name>.xml`對應 toohello 原則陳述式，每個作業的檔案。
* `policies\products\`-如果您有任何定義於產品範圍的原則，它們包含在這個資料夾中，其中包含`<product name>.xml`對應 toohello 每項產品的原則陳述式的檔案。

### <a name="portalstyles-folder"></a>portalStyles 資料夾
hello`portalStyles`資料夾包含用於開發人員入口網站的自訂 hello 服務執行個體的組態與樣式表。

* `portalStyles\configuration.json`-包含 hello hello hello 開發人員入口網站所使用的樣式表名稱
* `portalStyles\<style name>.css`-每個`<style name>.css`檔案包含樣式 hello 開發人員入口網站 (`Preview.css`和`Production.css`依預設)。

### <a name="products-folder"></a>產品資料夾
hello`products`資料夾都包含資料夾，以定義 hello 服務執行個體中每個產品。

* `products\<product name>\configuration.json`-這是 hello hello 之產品的組態。 這是 hello 相同的資訊將會傳回，如果您 toocall hello[取得特定產品](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct)作業。
* `products\<product name>\product.description.html`-這是 hello hello 產品描述及對應 toohello`description`屬性 hello [product 實體](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product)hello REST API 中。

### <a name="templates"></a>範本
hello`templates`資料夾包含組態的 hello[電子郵件範本](api-management-howto-configure-notifications.md)hello 服務執行個體。

* `<template name>\configuration.json`-這是 hello hello 電子郵件範本的設定。
* `<template name>\body.html`-這是 hello 主體 hello 電子郵件範本。

## <a name="next-steps"></a>後續步驟
如需其他方式 toomanage 您服務執行個體，請參閱：

* 管理服務執行個體使用下列 PowerShell 指令程式的 hello
  * [服務部署 PowerShell Cmdlet 參考](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [服務管理 PowerShell Cmdlet 參考](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* 管理您的服務執行個體在 hello 發行者入口網站
  * [管理第一個 API](api-management-get-started.md)
* 管理服務執行個體使用 hello REST API
  * [API 管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a>觀看影片概觀
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




