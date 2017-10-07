---
title: "aaaQuickstart hello Azure AD Graph API |Microsoft 文件"
description: "hello Azure Active Directory Graph API 提供以程式設計方式存取 tooAzure AD 透過 OData REST API 端點。 應用程式可以使用 hello Graph API tooperform 建立、 讀取、 更新和刪除 (CRUD) 作業目錄資料和物件。"
services: active-directory
documentationcenter: n/a
author: viv-liu
manager: mbaldwin
editor: 
tags: 
ms.assetid: 9dc268a9-32e8-402c-a43f-02b183c295c5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: b4d3c57f06d212b1d095578f19bb86c932dbcc33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-hello-azure-ad-graph-api"></a>Hello Azure AD Graph API 的快速入門
hello Azure Active Directory (AD) Graph API 提供以程式設計方式存取 tooAzure AD 透過 OData REST API 端點。 應用程式可以使用 hello Graph API tooperform 建立、 讀取、 更新和刪除 (CRUD) 作業目錄資料和物件。 比方說，您可以使用 hello Graph API toocreate 新的使用者，檢視或更新使用者的屬性，變更使用者的密碼，檢查的角色為基礎的存取、 停用或刪除 hello 使用者的群組成員資格。 如需有關 hello Graph API 功能和應用程式案例的詳細資訊，請參閱[Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)和[Azure AD Graph API 必要條件](https://msdn.microsoft.com/library/hh974476.aspx)。 

> [!IMPORTANT]
> 我們強烈建議您改用[Microsoft Graph](https://developer.microsoft.com/graph)而不是 Azure AD Graph API tooaccess Azure Active Directory 資源。 我們的開發工作現在是針對 Microsoft Graph，並沒有針對 Azure AD Graph API 規劃的進一步增強功能 。 有極少數的情況下，Azure AD Graph API 仍可能適合;如需詳細資訊，請參閱 hello [Microsoft Graph 或 hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) hello Office 開發人員中心中的部落格文章。
> 
> 

## <a name="how-tooconstruct-a-graph-api-url"></a>如何 tooconstruct Graph API URL
在 Graph API、 tooaccess 目錄資料和物件 （亦即，資源或實體） 針對您想要 tooperform CRUD 作業，您可以使用 hello 開放式資料 (OData) 通訊協定為基礎的 Url。 hello Graph API 中使用的 Url 包含四個主要部分： 服務根目錄、 租用戶識別碼、 資源路徑和查詢字串選項： `https://graph.windows.net/{tenant-identifier}/{resource-path}?[query-parameters]`。 採取的下列 URL 的 hello hello 範例： `https://graph.windows.net/contoso.com/groups?api-version=1.6`。

* **服務根目錄**: Azure AD Graph Api 中 hello 服務根目錄一定是 https://graph.windows.net。
* **租用戶識別碼**： 這個區段可驗證 （登錄） 的網域名稱，在上述範例中，hello contoso.com。它也可以是租用戶物件識別碼或 hello"myorganization"me"別名。 如需詳細資訊，請參閱[定址實體與 hello Graph API 中的作業](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-operations-overview))。
* **資源路徑**: URL 的這一節會識別 hello 資源 toobe 互動 （使用者、 群組、 特定的使用者，或特定群組等）在 hello 上述範例中，是 hello 上方層級 「 群組 」 tooaddress 該資源集。 您也可以為特定的實體定址，例如，“users/{objectId}” 或 “users/userPrincipalName”。
* **查詢參數**： 問號 （？） 分隔 hello 資源路徑區段與 hello 查詢參數 > 一節。 hello Graph API 中的所有要求均都需要 hello"api-version"查詢參數。 hello Graph API 也支援下列 OData 查詢選項的 hello: **$filter**， **$orderby**， **$expand**， **$top**，和**$format**。 目前不支援下列查詢選項的 hello: **$count**， **$inlinecount**，和**$skip**。 如需詳細資訊，請參閱 [Azure AD Graph API 中支援的查詢、篩選和分頁選項](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options)。

## <a name="graph-api-versions"></a>Graph API 版本
Hello"api-version"查詢參數中指定 Graph API 要求的 hello 版本。 如果是 1.5 版和更新版本，您可以使用數字版本值；api-version=1.6。 舊版本中，您使用的日期字串符合 toohello 格式 YYYY MM DD;例如，api-version = 2013年-11-08。 如需預覽功能，使用 hello 字串"beta";例如，api-version = beta。 如需 Graph API 版本間差異的詳細資訊，請參閱 [Azure AD Graph API 版本設定](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning)。

## <a name="graph-api-metadata"></a>Graph API 中繼資料
tooreturn hello Graph API 中繼資料檔案，加入 hello"$metadata 」 區段之後 hello 租用戶識別碼 hello URL。 例如，在 hello 下列 URL 傳回中繼資料的示範公司： `https://graph.windows.net/GraphDir1.OnMicrosoft.com/$metadata?api-version=1.6`。 您可以在 web 瀏覽器 toosee hello 中繼資料 hello 網址列中輸入此 URL。 hello 傳回的 CSDL 中繼資料文件描述 hello 實體和複雜型別、 其屬性和 hello 函式和 hello 版本，您所要求的 Graph api 所公開的動作。 省略 hello api-version 參數傳回 hello 最新版本的中繼資料。

## <a name="common-queries"></a>常用查詢
[Azure AD Graph API 常用查詢](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#CommonQueries)列出可以搭配 hello Azure AD Graph，包括查詢，可以使用的 tooaccess 在您的目錄和查詢 tooperform 操作中您目錄中的最上層資源的常用查詢。

例如， `https://graph.windows.net/contoso.com/tenantDetails?api-version=1.6` 會傳回目錄 contoso.com 的公司資訊。

或`https://graph.windows.net/contoso.com/users?api-version=1.6`列出 hello 目錄 contoso.com 中的所有使用者物件。

## <a name="using-hello-graph-explorer"></a>使用 hello 圖表總管
當您建立您的應用程式，您可以使用圖表總管 hello hello Azure AD Graph API tooquery hello 目錄資料。

hello 以下是 hello 輸出，您會看到 是否您選擇了 toonavigate toohello 圖表總管、 登入，並輸入`https://graph.windows.net/GraphDir1.OnMicrosoft.com/users?api-version=1.6`toodisplay 所有 hello 中的使用者 hello 登入使用者的目錄：

![Azure AD Graph API 總管](./media/active-directory-graph-api-quickstart/graph_explorer.png)

**負載 hello 圖表總管**: tooload hello 工具，請瀏覽過[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/)。 按一下**登入**和登入與您 Azure AD 帳戶認證 toorun hello 圖表總管，針對您的租用戶。 如果您對自己的租用戶執行圖表總管，您或您的系統管理員請登入期間需要 tooconsent。 如果您擁有 Office 365 訂用帳戶，就會自動擁有 Azure AD 租用戶。 hello 認證 toosign 用於 tooOffice 365，事實上，Azure AD 帳戶，而且您可以使用這些認證與圖表總管。

**執行查詢**: toorun 查詢中，輸入您的查詢中的 hello 要求文字方塊中按一下 **取得**或按一下 hello**輸入**索引鍵。 hello 結果會顯示 hello 回應方塊中。 例如，`https://graph.windows.net/myorganization/groups?api-version=1.6`列出 hello 登入使用者的目錄中的所有群組物件。

請注意 hello 遵循 hello 圖表總管的功能和限制：

* 資源集上的自動完成功能。 toosee 這項功能，請按一下 hello 要求的文字方塊 （hello 公司 URL 出現的位置）。 您可以選取設定 hello 下拉式清單中的資源。
* 支援 hello"me"和"myorganization"定址別名。 例如，您可以使用`https://graph.windows.net/me?api-version=1.6`tooreturn hello 使用者物件的 hello 登入的使用者或`https://graph.windows.net/myorganization/users?api-version=1.6`tooreturn hello 目前目錄中的所有使用者。
* 回應標頭區段 此區段可以用 toohelp 執行查詢時所發生的問題進行疑難排解。
* 展開和摺疊功能的 hello 回應 JSON 檢視器。
* 不支援顯示縮圖相片。

## <a name="using-fiddler-toowrite-toohello-directory"></a>使用 Fiddler toowrite toohello 目錄
基於 hello 本快速入門指南，您可以使用 hello Fiddler Web Debugger toopractice 執行寫入作業，針對您的 Azure AD 目錄。 如需詳細資訊和 tooinstall Fiddler，請參閱[http://www.telerik.com/fiddler](http://www.telerik.com/fiddler)。

在 hello 面範例中，您可以使用 Fiddler Web Debugger toocreate 新的安全性群組 'MyTestGroup' Azure AD 目錄中。

**取得存取權杖**: tooaccess Azure AD Graph，用戶端是需要的 toosuccessfully 驗證 tooAzure AD 第一次。 如需詳細資訊，請參閱 [Azure AD 的驗證案例](active-directory-authentication-scenarios.md)。

**撰寫和執行查詢**： 完整 hello 下列步驟：

1. 開啟 Fiddler Web Debugger 並切換 toohello**編輯器** 索引標籤。
2. 由於您希望 toocreate 新的安全性群組，選取**Post**為 hello hello 下拉功能表中的 HTTP 方法。 群組物件上作業和權限的相關資訊，請參閱[群組](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#GroupEntity)內 hello [Azure AD Graph REST API 參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)。
3. Hello 欄位中接下來太**Post**，hello 要求 URL 中 hello 下列輸入： `https://graph.windows.net/mytenantdomain/groups?api-version=1.6`。
   
   > [!NOTE]
   > 您必須將 mytenantdomain 換 hello 的 Azure AD 目錄的網域名稱成。
   > 
   > 
4. 在正下方的 Post 下拉式 hello 欄位中，輸入 hello 下列：
   
    ```
   Host: graph.windows.net
   Authorization: Bearer <your access token>
   Content-Type: application/json
   ```
   
   > [!NOTE]
   > 替代程式&lt;存取權杖&gt;與 hello Azure AD 目錄的存取權杖。
   > 
   > 
5. 在 hello**要求本文**欄位中，輸入 hello 下列：
   
    ```
        {
            "displayName":"MyTestGroup",
            "mailNickname":"MyTestGroup",
            "mailEnabled":"false",
            "securityEnabled": true
        }
   ```
   
    如需建立群組的詳細資訊，請參閱 [建立群組](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#CreateGroup)。

如需有關 Azure AD 實體和 Graph 所公開的型別和 hello 作業可以使用 Graph 執行於其上的相關資訊，請參閱[Azure AD Graph REST API 參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)。

## <a name="next-steps"></a>後續步驟
* 深入了解 hello [Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)
* 深入了解 [Azure AD 圖形 API 權限範圍](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)

