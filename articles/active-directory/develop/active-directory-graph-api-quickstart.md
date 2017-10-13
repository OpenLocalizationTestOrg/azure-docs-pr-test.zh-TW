---
title: "Azure AD Graph API 快速入門 | Microsoft Aure"
description: "Azure Active Directory Graph API 會透過 OData REST API 端點，以程式設計方式存取 Azure AD。 應用程式可以使用 Graph API，來執行有關目錄資料和物件的建立、讀取、更新及刪除 (CRUD) 作業。"
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
ms.openlocfilehash: fad5c315a247673b7a2ad52b4a78b49c567a997a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="quickstart-for-the-azure-ad-graph-api"></a>Azure AD Graph API 的快速入門
Azure Active Directory (AD) Graph API 是透過 OData REST API 端點，以程式設計方式存取 Azure AD。 應用程式可以使用 Graph API，來執行有關目錄資料和物件的建立、讀取、更新及刪除 (CRUD) 作業。 例如，您可以使用圖形 API 來建立新的使用者、檢視或更新使用者的內容、變更使用者的密碼，請檢查以角色為基礎的存取權的群組成員資格停用或刪除使用者。 如需 Graph API 功能和應用程式案例的詳細資訊，請參閱 [Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) 和 [Azure AD Graph API 的先決條件](https://msdn.microsoft.com/library/hh974476.aspx)。 

> [!IMPORTANT]
> 強烈建議您使用 [Microsoft Graph](https://developer.microsoft.com/graph) 取代 Azure AD Graph API 來存取 Azure Active Directory 資源。 我們的開發工作現在是針對 Microsoft Graph，並沒有針對 Azure AD Graph API 規劃的進一步增強功能 。 有極少數的案例可能仍適用 Azure AD Graph API；如需詳細資訊，請參閱 Office 開發人員中心的 [Microsoft Graph 或 Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) 部落格文章。
> 
> 

## <a name="how-to-construct-a-graph-api-url"></a>如何建構 Graph API URL
在 Graph API 中，若要存取您想要對其執行 CRUD 作業的目錄資料和物件 (亦即，資源或實體)，您可使用以「開放式資料 (OData) 通訊協定」為基礎的 URL。 Graph API 中使用的 URL 是由下列四個主要部分所組成：服務根目錄、租用戶識別碼、資源路徑和查詢字串選項： `https://graph.windows.net/{tenant-identifier}/{resource-path}?[query-parameters]`。 在下列 URL 中取得範例： `https://graph.windows.net/contoso.com/groups?api-version=1.6`。

* **服務根目錄**：在 Azure AD Graph API 中，服務根目錄一律為 https://graph.windows.net。
* **租用戶識別碼**：此區段可以是已驗證 (已註冊) 的網域名稱，在上述範例中為 contoso.com。 它也可以是租用戶物件識別碼，或是 “myorganization” 或 “me” 別名。 如需詳細資訊，請參閱 [在 Graph API 中將實體和作業定址](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-operations-overview))。
* **資源路徑**：URL 的這個部分會識別要互動的資源 (使用者、群組、特定的使用者或特定的群組等)。在上述範例中，它是將該資源集定址的頂層「群組」。 您也可以為特定的實體定址，例如，“users/{objectId}” 或 “users/userPrincipalName”。
* **查詢參數**：問號 (?) 可區隔資源路徑區段和查詢參數區段。 在 Graph API 中，所有要求上都需要 “api-version” 查詢參數。 Graph API 也支援下列 OData 查詢選項：**$filter**、**$orderby**、**$expand**、**$top**, 和 **$format**。 目前不支援下列查詢選項：**$count**、**$inlinecount** 和 **$skip**。 如需詳細資訊，請參閱 [Azure AD Graph API 中支援的查詢、篩選和分頁選項](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options)。

## <a name="graph-api-versions"></a>Graph API 版本
您可以在 “api-version” 查詢參數中指定 Graph API 要求的版本。 如果是 1.5 版和更新版本，您可以使用數字版本值；api-version=1.6。 如果是較早的版本，您可以使用遵守 YYYY-MM-DD 格式的日期字串；例如，api-version=2013-11-08。 如果是預覽功能，請使用字串 "beta"；例如，api-version=beta。 如需 Graph API 版本間差異的詳細資訊，請參閱 [Azure AD Graph API 版本設定](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning)。

## <a name="graph-api-metadata"></a>Graph API 中繼資料
若要傳回圖形 API 中繼資料檔案，可在 URL 中的租用戶識別碼之後加入 "$metadata" 區段。例如，下列 URL 會傳回示範公司的中繼資料：`https://graph.windows.net/GraphDir1.OnMicrosoft.com/$metadata?api-version=1.6`。 您可以在 Web 瀏覽器的網址列中輸入這個 URL 來查看中繼資料。 傳回的 CSDL 中繼資料文件會說明實體和複雜類型、其屬性，以及由您要求的 Graph API 版本所公開的函式和動作。 省略 api-version 參數會傳回適用於最新版本的中繼資料。

## <a name="common-queries"></a>常用查詢
[Azure AD Graph API 常用查詢](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#CommonQueries) 會列出可與 Azure AD Graph 搭配使用的常用查詢，包括可用來存取目錄中最上層資源的查詢，以及在目錄中執行作業的查詢。

例如， `https://graph.windows.net/contoso.com/tenantDetails?api-version=1.6` 會傳回目錄 contoso.com 的公司資訊。

或者， `https://graph.windows.net/contoso.com/users?api-version=1.6` 會列出目錄 contoso.com 中的所有使用者物件。

## <a name="using-the-graph-explorer"></a>使用圖表總管
當您建置應用程式時，可以使用適用於 Azure AD Graph API 的圖表總管來查詢目錄資料。

如果您瀏覽至 Graph 總管、登入，然後輸入 `https://graph.windows.net/GraphDir1.OnMicrosoft.com/users?api-version=1.6` 來顯示登入使用者之目錄中的所有使用者，即會看見下列輸出：

![Azure AD Graph API 總管](./media/active-directory-graph-api-quickstart/graph_explorer.png)

**載入 Graph 總管**：若要載入此工具，請瀏覽至 [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/)。 按一下 [登入]，並使用 Azure AD 帳戶認證來登入，以針對您的租用戶執行 Graph 總管。 如果您針對自己的租用戶執行「Graph 總管」，則您或系統管理員就必須在登入期間表示同意。 如果您擁有 Office 365 訂用帳戶，就會自動擁有 Azure AD 租用戶。 事實上，您用來登入 Office 365 的認證就是 Azure AD 帳戶，而您可以將這些認證與圖表總管搭配使用。

**執行查詢**：若要執行查詢，可在要求文字方塊中輸入查詢，然後按一下 [GET] 或 **Enter** 鍵。 結果即會顯示於回應方塊中。 例如，`https://graph.windows.net/myorganization/groups?api-version=1.6` 會列出登入使用者之目錄中的所有群組物件。

請注意，圖表總管具有下列功能與限制：

* 資源集上的自動完成功能。 若要查看此功能，請按一下要求文字方塊 (公司 URL 出現的位置)。 您可以從下拉式清單中選取資源集。
* 支援 "me" 和 "myorganization" 定址別名。 例如，您可以使用 `https://graph.windows.net/me?api-version=1.6` 來傳回登入使用者的使用者物件，或者使用 `https://graph.windows.net/myorganization/users?api-version=1.6` 來傳回目前目錄中的所有使用者。
* 回應標頭區段 對於執行查詢時所發生的問題，此區段有助於進行疑難排解。
* 適用於回應的 JSON 檢視器，並具備展開和摺疊功能。
* 不支援顯示縮圖相片。

## <a name="using-fiddler-to-write-to-the-directory"></a>使用 Fiddler 寫入目錄
基於本快速入門指南的目的，您可以使用「Fiddler Web 偵錯工具」，練習對 Azure AD 目錄執行「寫入」作業。 如需詳細資訊以及安裝 Fiddler 的方式，請參閱 [http://www.telerik.com/fiddler](http://www.telerik.com/fiddler)。

在下列範例中，您將使用「Fiddler Web 偵錯工具」，在 Azure AD 目錄中建立新的安全性群組 ‘MyTestGroup’。

**取得存取權杖**：若要存取 Azure AD Graph，用戶端必須先順利通過 Azure AD 的驗證。 如需詳細資訊，請參閱 [Azure AD 的驗證案例](active-directory-authentication-scenarios.md)。

**撰寫和執行查詢**：請完成下列步驟：

1. 開啟 Fiddler Web 偵錯工具，然後切換到 [編輯器]  索引標籤。
2. 由於您想要建立新的安全性群組，因此，請從下拉式功能表中選取 [Post]  做為 HTTP 方法。 如需有關群組物件的作業與權限詳細資訊，請參閱 [Azure AD Graph REST API 參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)內的[群組](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#GroupEntity)。
3. 在 [Post] 旁邊的欄位中，輸入下列內容做為要求 URL：`https://graph.windows.net/mytenantdomain/groups?api-version=1.6`。
   
   > [!NOTE]
   > 您必須使用自己的 Azure AD目錄網域名稱來取代 mytenantdomain。
   > 
   > 
4. 在 [Post] 下拉式清單正下方的欄位中，輸入下列內容：
   
    ```
   Host: graph.windows.net
   Authorization: Bearer <your access token>
   Content-Type: application/json
   ```
   
   > [!NOTE]
   > 使用 Azure AD 目錄的存取權杖來取代 &lt;您的存取權杖&gt;。
   > 
   > 
5. 在 [要求本文]  欄位中，輸入下列內容：
   
    ```
        {
            "displayName":"MyTestGroup",
            "mailNickname":"MyTestGroup",
            "mailEnabled":"false",
            "securityEnabled": true
        }
   ```
   
    如需建立群組的詳細資訊，請參閱 [建立群組](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#CreateGroup)。

如需 Graph 所公開的 Azure AD 實體和類型詳細資訊，以及可使用 Graph 在其上執行的作業相關資訊，請參閱 [Azure AD Graph REST API 參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)。

## <a name="next-steps"></a>後續步驟
* 深入了解 [Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)
* 深入了解 [Azure AD 圖形 API 權限範圍](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)

