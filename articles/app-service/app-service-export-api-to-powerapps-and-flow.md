---
title: "aaaExporting Azure 託管應用程式開發介面 tooPowerApps 和 Microsoft Flow |Microsoft 文件"
description: "在應用程式服務 tooPowerApps 和 Microsoft Flow 裝載 tooexpose 應用程式開發介面的方式的概觀"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/20/2017
ms.author: mahender
ms.openlocfilehash: 285b6efa3af5b0feac1ee2f617c0dc56dc3fd198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-an-azure-hosted-api-toopowerapps-and-microsoft-flow"></a>匯出 Azure 託管應用程式開發介面 tooPowerApps 和 Microsoft Flow

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>為 PowerApps 和 Microsoft Flow 建立自訂連接器

[PowerApps](https://powerapps.com)是用於建立和使用自訂商務應用程式，tooyour 資料連接，以及跨平台運作的服務。 [Microsoft Flow](https://flow.microsoft.com)可讓您輕鬆 tooautomate 工作流程且喜愛的應用程式與服務之間的商務程序。 PowerApps 與 Microsoft Flow 隨附各種內建連接器 toodata 來源，例如 Office 365、 Dynamics 365、 Salesforce 等等。 不過，使用者也需要 toobe 無法 tooleverage 資料來源和正在其組織建立的應用程式開發介面。

同樣地，開發人員想 tooexpose 其廣泛 hello 內組織可能會想 toomake 其應用程式開發介面使用 tooPowerApps 和 Microsoft Flow 使用者更多的 Api。 本主題將告訴您如何 tooexpose 應用程式開發介面建置 Azure 應用程式服務或 Azure 函式 tooPowerApps 與 Microsoft Flow。 [Azure App Service](https://azure.microsoft.com/services/app-service/)是可讓開發人員 tooquickly 和輕鬆地建置企業級 web、 行動裝置，以及 API 應用程式的平台做為服務供應項目。 [Azure 函數](https://azure.microsoft.com/services/functions/)是以事件為基礎的無伺服器計算的解決方案，可讓您可以回應您的系統與隨標尺 tooother 部分 tooquickly 撰寫程式碼。

toolearn 進一步了解這些服務，請參閱：
- [PowerApps 引導式學習](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) 
- [Microsoft Flow 引導式學習](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [什麼是 App Service？](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [什麼是 Azure Functions？](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>共用 API 定義

應用程式開發介面通常使用描述[OpenAPI 文件](https://www.openapis.org/)（有時稱為 tooas"Swagger 」 文件）。 這包含所有的 hello 哪些作業，以及如何 hello 資料應該結構化資訊。 PowerApps 和 Microsoft Flow 可以為任何 OpenAPI 2.0 文件建立自訂連接器。 一旦建立自訂連接器，它可以用於完全 hello 相同的方式，做為其中一個 hello 內建的連接器，而且可以快速整合到應用程式。

Azure App Service 和 Azure Functions 有[內建支援](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata)，可供建立、裝載及管理 OpenAPI 文件。 在順序 toocreate web、 行動裝置的自訂連接器，應用程式開發介面或函式應用程式，PowerApps 和流程需要 toobe 指定 hello 定義的複本。

> [!NOTE]
> 因為正在使用 hello API 定義的複本，PowerApps 與 Microsoft Flow 不會立即知道更新或重大變更 toohello 應用程式。 如果 hello API 的新版本可供使用，這些步驟應重複 hello 新版本。 

tooprovide PowerApps 與 Microsoft Flow hello 裝載應用程式開發介面定義您的應用程式，請遵循下列步驟：

1. 開啟 hello [Azure 入口網站](https://portal.azure.com)並瀏覽 tooyour 應用程式服務或 Azure 函式的應用程式。

    如果使用 Azure 應用程式服務，請選取**API 定義**hello 設定值清單。 
    
    如果使用 Azure Functions，請選取您的函數應用程式，然後依序選擇 [平台功能]、[API 定義]。 您也可以選擇 tooopen hello **API 定義 （預覽）**改為索引標籤。

2. 如果已提供 API 定義，則您會看到**匯出 tooPowerApps + Microsoft Flow**  按鈕。 按一下此按鈕 toobegin hello 匯出程序。

3. 選取 hello**匯出模式**。 這會決定您需要 toofollow toocreate 連接器 hello 步驟。 App Service 提供兩種選項，供您將 API 定義提供給 PowerApps 和 Microsoft Flow：

    **Express**可讓您建立 hello 自訂連接器從內 hello Azure 入口網站。 它需要該 hello 目前登入的使用者具有使用權限 toocreate 連接器 hello 目標環境中。 這是建議的方法，如果滿足該需求，可以 hello。 如果使用此模式，請遵循 hello [Express 匯出](#express)下列指示。

    **手動**可讓您將匯出的 hello 可匯入使用 hello PowerApps 或 Microsoft Flow 入口網站的應用程式開發介面定義的複本。 這是建議的方法如果 hello Azure 使用者和權限 toocreate 連接器 hello 使用者不同的人或 hello 連接器必須在另一個租用戶中建立的 toobe hello。 如果使用此模式，請遵循 hello[手動匯出和匯入](#manual)下列指示。

<a name="express"></a>
## <a name="express-export"></a>快速匯出

在本節中，您將建立新的自訂連接器從 hello Azure 入口網站中。 您必須登入 hello 租用戶 toowhich 想 tooexport，而且您必須擁有權限 toocreate 自訂連接器 hello 目標環境中。

1. 選取您想在其中要 toocreate hello 連接器 hello 環境。 然後提供您的自訂連接器名稱。

2. 如果您的 API 定義包含任何安全性定義，則會在步驟 2 中叫出這些定義。 必要時，提供 hello 安全性組態詳細資料所需 toogrant 使用者存取 tooyour API。 如需詳細資訊，請參閱下面的[驗證](#auth)。 

3. 按一下**確定**toocreate 您自訂的連接器。


<a name="manual"></a>
## <a name="manual-export-and-import"></a>手動匯出和匯入

在訂單 toocreate 自訂連接器的 web、 行動、 應用程式開發介面或函式應用程式，將需要兩個步驟：

1. [從應用程式服務或 Azure 函式擷取 hello 應用程式開發介面定義](#export)
2. [匯入 PowerApps 與 Microsoft Flow hello API 定義](#import)

很可能在這兩個步驟將需要 toobe 由組織內的個別人員執行，因為指定的使用者可能沒有權限 tooperform 這兩個動作。 在此情況下，具有參與者存取 toohello 應用程式服務或 Azure 函式的應用程式的開發人員需要 tooobtain hello 應用程式開發介面定義 （單一 JSON 檔案） 或連結 tooit。 它們必須 tooprovide 該定義 tooa PowerApps 或 Microsoft Flow 擁有者。 該擁有者可以使用 hello 中繼資料 toocreate hello 自訂連接器。

<a name="export"></a>
### <a name="retrieving-hello-api-definition-from-app-service-or-azure-functions"></a>從應用程式服務或 Azure 函式擷取 hello 應用程式開發介面定義

在本節中，您會匯出您的應用程式服務 api，稍後在 hello PowerApps 或 Microsoft Flow 入口網站中使用的 toobe hello API 定義。

1. 您可以選擇 tooeither**下載 hello API 定義**或**取得連結**。 無論您的選擇，hello 下一節中會提供 hello 結果。 選取其中一個選項，並遵循 hello 指示。
 
2. 如果您的 API 定義包含任何安全性定義，則會在步驟 2 中叫出這些定義。 在匯入期間，PowerApps 和 Microsoft Flow 會偵測這些定義並提示輸入安全性資訊。 收集 hello 認證相關的 tooeach 定義以供使用 hello 下一節。 如需詳細資訊，請參閱下面的[驗證](#auth)。 

<a name="import"></a>
### <a name="importing-hello-api-definition-into-powerapps-and-microsoft-flow"></a>匯入 PowerApps 與 Microsoft Flow hello API 定義

在本節中，您將建立自訂連接器 PowerApps 與 Microsoft Flow 使用稍早取得的 hello 應用程式開發介面定義中。 自訂連接器 hello 兩個服務，因此您只需要一次 tooimport hello 定義之間共用。 如需有關自訂連接器的詳細資訊，請參閱[在 PowerApps 中註冊及使用自訂連接器]和[在 Microsoft Flow 中註冊及使用自訂連接器]。

1. 開啟 hello [Powerapps web 入口網站](https://web.powerapps.com)或 hello [Microsoft Flow web 入口網站](https://flow.microsoft.com/)，並登入。 

2. 按一下 hello**設定**hello 右上方的 hello 頁面，然後選取按鈕 （hello 齒輪圖示）**自訂連接器**。 

3. 按一下 [建立自訂連接器]。

4. 在 hello**一般**索引標籤上，為您的 API 提供的名稱，然後上傳 hello OpenAPI 定義或貼上 hello 中繼資料 URL 中。 按一下 [繼續]。

4. 在 hello**安全性**索引標籤上，如果您是提示的 tooprovide 驗證詳細資料，輸入 hello hello 上一節中所取得的值。 如果沒有，請繼續執行 toohello 下一個步驟。

5. 在 hello**定義**索引標籤上，所有 OpenAPI 檔案中定義的 hello 作業將都會自動擴展。 如果定義了所有所需的作業，您可以移 toohello 下一個步驟。 如果沒有，您可以在此新增與修改作業。

6. 按一下 [建立連接器]。 如果您想 tootest API 呼叫，請移 toohello 下一個步驟。

7. 在 hello**測試**索引標籤上，建立連接、 選取作業 tootest，然後輸入 hello 作業所需的任何資料。

8. 按一下 [測試作業]。


<a name="auth"></a>
## <a name="authentication"></a>驗證

PowerApps 與 Microsoft Flow 原生支援可使用的 toolog 中您自訂的連接器的使用者身分識別提供者的集合。 如果您的 API 需要驗證，請確保它會依照您 OpenAPI 文件中的_安全性定義_擷取。 在匯出期間，您必須允許 PowerApps Microsoft Flow tooperform 登入動作的 tooprovide 組態值。

此章節將涵蓋支援的 hello express 流程 hello 驗證類型： API 金鑰、 Azure Active Directory 和一般的 OAuth 2.0。 提供者和每個需要 hello 認證的完整清單，請參閱[在 PowerApps 中註冊及使用自訂連接器]和[在 Microsoft Flow 中註冊及使用自訂連接器]。

### <a name="api-key"></a>API 金鑰
使用此安全性配置時，您的連接器的 hello 使用者將無法提示的 tooprovide hello 索引鍵，在建立連線時。 您可以提供 API 金鑰名稱 toohelp 他們知道需要哪些金鑰。 對於 Azure 函式，這通常會是 hello 主機金鑰，涵蓋 hello 函式應用程式中的幾個函式的其中之一。

### <a name="azure-active-directory"></a>Azure Active Directory
當設定需要 AAD 登入的自訂連接器，兩個 AAD 應用程式註冊所需： 一個 toomodel hello 後端 API 和 PowerApps 與流程中的一個 toomodel hello 連接器。

您的 API 應該是設定的 toowork 與 hello 第一次註冊，而且這會已經注意如果您使用 hello[應用程式服務驗證/授權](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)功能。

您將需要建立 hello hello 連接器的第二個註冊 toomanually 使用 hello 步驟涵蓋[加入 AAD 應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application)。 hello 註冊需要 toohave 委派存取 tooyour API 和回覆 URL `https://msmanaged-na.consent.azure-apim.net/redirect`。 請參閱[本例](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/)如需詳細資訊，以取代您的 API hello Azure 資源管理員。

下列組態值的 hello 是必要的：
- **用戶端識別碼**-hello 您連接器的 AAD 註冊用戶端識別碼
- **用戶端密碼**-hello 的 AAD 註冊您的連接器的用戶端密碼
- **登入 URL** -hello AAD 基底 URL。 在公用 Azure 中，這通常是 `https://login.windows.net`。
- **租用戶識別碼**-hello hello 租用戶 toobe hello 登入使用的識別碼。 這應該是 「 通用 」，或 hello hello 租用戶中的 hello 建立連接器識別碼。
- **資源 URL** -hello 您 API 後端的 AAD 註冊的資源 URL

> [!IMPORTANT]
> 如果其他的個人要匯入 hello API 定義 PowerApps 與 Microsoft Flow 當做 hello 手動流程的一部分，您將需要 tooprovide 其與 hello 用戶端識別碼和用戶端密碼**的 hello el registro del conector**，以及為您的 API hello 資源 URL。 確定這些密碼都已受到安全地管理。 **不會共用 hello 的 hello API 本身的安全性認證。**

### <a name="generic-oauth-20"></a>Generic OAuth 2.0
hello 泛型的 OAuth 2.0 支援可讓您 toointegrate 任何 OAuth 2.0 提供者。 這可以讓您 toobring 原生不支援的任何自訂提供者。

下列組態值的 hello 是必要的：
- **用戶端識別碼**-hello OAuth 2.0 用戶端識別碼
- **用戶端密碼**-hello OAuth 2.0 用戶端密碼
- **授權 URL** -hello OAuth 2.0 授權 URL
- **語彙基元 URL** -hello OAuth 2.0 權杖 URL
- **重新整理 URL** -hello OAuth 2.0 重新整理 URL



[在 PowerApps 中註冊及使用自訂連接器]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[在 Microsoft Flow 中註冊及使用自訂連接器]: https://flow.microsoft.com/documentation/register-custom-api/
