---
title: "aaaAccess Azure 媒體服務 API 與 Azure Active Directory 驗證 |Microsoft 文件"
description: "深入了解概念及步驟 tootake toouse Azure Active Directory (Azure AD) tooauthenticate 存取 toohello Azure 媒體服務 API。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: bb8f75f39100dc37098260c24ab4a199ef689d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-hello-azure-media-services-api-with-azure-ad-authentication"></a>存取 hello Azure 媒體服務 API 與 Azure AD 驗證
 
hello Azure Media Services API 是 Rest API。 您可以使用它 tooperform 媒體資源的作業使用 REST API，或使用可用的用戶端 Sdk。 Azure 媒體服務提供適用於 Microsoft .NET 的媒體服務用戶端 SDK。 toobe 授權 tooaccess Media Services 資源和 hello Media Services API，您必須先通過驗證。 

媒體服務支援 [Azure Active Directory (Azure AD) 型驗證](../active-directory/active-directory-whatis.md)。 hello Azure 媒體 REST 服務，必須具備 hello 使用者或應用程式可發出 hello REST API 要求的其中一個 hello**參與者**或**擁有者**角色 tooaccess hello 資源。 如需詳細資訊，請參閱[開始 hello Azure 入口網站中的 角色型存取控制使用](../active-directory/role-based-access-control-what-is.md)。  

> [!IMPORTANT]
> 目前，Media Services 支援 hello Azure 存取控制服務驗證模型。 不過，存取控制授權將在 2018 年 6 月 1 日被取代。 我們建議您儘速移轉 toohello Azure AD 驗證模型。

本文件概略 tooaccess hello Media Services API 使用 REST 或.NET 應用程式開發介面的方式。

## <a name="access-control"></a>存取控制

Hello Azure 媒體 REST 要求 toosucceed，hello 呼叫使用者必須 hello 它嘗試 tooaccess Media Services 帳戶的參與者或擁有者角色。  
只有具備 hello 擁有者角色的使用者可以提供媒體資源 （帳戶） 存取 toonew 使用者或應用程式。 hello 參與者角色可以存取 hello 媒體資源。
未經授權的要求會失敗，狀態碼為 401。 如果您看到此錯誤的程式碼，請檢查您的使用者是否具有 hello 參與者或 hello 使用者 Media Services 帳戶指派的擁有者角色。 您可以檢查這個 hello Azure 入口網站中。 搜尋您媒體的帳戶，然後再按一下 [hello**存取控制**] 索引標籤。 

![[Access control] \(存取控制\) 索引標籤](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a>驗證類型 
 
當您使用 Azure AD 驗證搭配 Azure 媒體服務 時，會有兩個驗證選項：

- **使用者驗證**。 驗證使用 hello 應用程式 toointeract 和媒體服務資源的人員。 hello 互動式應用程式應該會先提示 hello hello 使用者提供認證的使用者。 範例是由授權的使用者 toomonitor 編碼工作的主控台應用程式管理或即時資料流。 
- **服務主體驗證**。 驗證服務。 通常使用這種驗證方法的應用程式有執行精靈服務、中介層服務或排程的工作的應用程式。 例如，Web 應用程式、函數應用程式、邏輯應用程式、API 或微服務。

### <a name="user-authentication"></a>使用者驗證 

管理或監視原生應用程式之應用程式應該使用 hello 使用者驗證方法： 行動裝置應用程式、 Windows 應用程式和主控台應用程式。 您想與其中一個 hello 下列案例中的 hello 服務人為互動時，這種解決方案非常有用：

- 編碼工作的監控儀表板。
- 即時串流的監控儀表板。
- Media Services 帳戶中的桌面或行動使用者 tooadminister 資源的管理應用程式。

> [!NOTE]
> 這種驗證方法不應用於消費者對向應用程式。 

原生應用程式必須先取得 Azure ad 存取權杖，然後再使用它，當您進行 HTTP 要求 toohello 媒體服務 REST API。 新增 hello 存取語彙基元 toohello 要求標頭。 

hello 下列圖表顯示一般的互動式應用程式的驗證流程： 

![原生應用程式圖](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

在之前圖表 hello，hello 數字代表 hello 資料流程的 hello 要求依時間先後順序。

> [!NOTE]
> 當您使用 hello 使用者驗證方法時，所有的應用程式共用 hello 相同 （預設值） 的原生應用程式用戶端識別碼和原生應用程式重新導向 URI。 

1. 提示使用者輸入認證。
2. 以下列參數的 hello 要求 Azure AD 存取權杖：  

    * Azure AD 租用戶端點。

        hello 租用戶資訊可以擷取從 hello Azure 入口網站。 Hello 右上角中，將游標放在 hello hello 登入的使用者名稱。
    * 媒體服務資源 URI。 

        這個 URI 是 hello 相同 hello 中的媒體服務帳戶相同的 Azure 環境 (例如，https://rest.media.azure.net)。

    * 媒體服務 (原生) 應用程式用戶端識別碼。
    * 媒體服務 (原生) 應用程式重新導向 URI。
    * REST 媒體服務的資源 URI。
        
        hello URI 表示 hello REST API 端點 (例如，https://test03.restv2.westus.media.azure.net/api/)。

    tooget 值，這些參數，請參閱[使用 hello Azure 入口網站 tooaccess Azure AD 驗證設定](media-services-portal-get-started-with-aad.md)使用 hello 使用者驗證 選項。

3. hello Azure AD 存取權杖會傳送 toohello 用戶端。
4. hello 用戶端傳送 hello Azure AD 存取權杖的要求的 toohello Azure 媒體 REST API。
5. hello 用戶端 hello 資料從取回 Media Services。

如需如何使用 Media Services.NET 用戶端 hello SDK toouse Azure AD 驗證 toocommunicate 與其他要求資訊，請參閱[使用 Azure AD 驗證 tooaccess hello 與.NET 的 Media Services API](media-services-dotnet-get-started-with-aad.md)。 

如果您未使用 Media Services.NET 用戶端 hello SDK，您必須手動建立的 Azure AD 存取權杖要求，使用步驟 2 中所述的 hello 參數。 如需詳細資訊，請參閱[toouse hello Azure AD 驗證程式庫 tooget 如何 hello Azure AD 權杖](../active-directory/develop/active-directory-authentication-libraries.md)。

### <a name="service-principal-authentication"></a>服務主體驗證

通常使用這種驗證方法的應用程式有執行中介層服務和排程的工作的應用程式：Web 應用程式、函數應用程式、邏輯應用程式、API 和微服務。 此驗證方法也會是適用於互動式應用程式，您可能會想 toouse 服務帳戶 toomanage 資源項目。

當您使用 hello 服務主體的驗證方法 toobuild 取用者案例時，驗證通常會處理在 hello 中介層 （透過某些應用程式開發介面），並不是直接在行動或桌面應用程式中。 

toouse 這個方法建立的 Azure AD 應用程式和服務主體在它自己的租用戶中。 建立 hello 應用程式之後，授與 hello 應用程式參與者或擁有者角色存取 toohello Media Services 帳戶。 您可以在 hello Azure 入口網站中使用 Azure CLI 或 PowerShell 指令碼。 您也可以使用現有的 Azure AD 應用程式。 您可以註冊及管理您的 Azure AD 應用程式和服務主體[hello Azure 入口網站中](media-services-portal-get-started-with-aad.md)。 您也可以使用 [Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) 或 [PowerShell](media-services-powershell-create-and-configure-aad-app.md) 執行此動作。 

![中介層應用程式](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

建立您的 Azure AD 應用程式之後，您會取得 hello 下列設定的值。 您需要這些值以進行驗證：

- 用戶端識別碼 
- 用戶端密碼 

在上述圖 hello，hello 數字代表 hello 流程依時間先後順序中的 hello 要求：
    
1. 中介層應用程式 （web API 或 web 應用程式） 會要求具有下列參數的 hello Azure AD 存取權杖：  

    * Azure AD 租用戶端點。

        hello 租用戶資訊可以擷取從 hello Azure 入口網站。 Hello 右上角中，將游標放在 hello hello 登入的使用者名稱。
    * 媒體服務資源 URI。 

        這個 URI 是 hello 相同位於 hello 的 Media Services 帳戶相同的 Azure 環境 (例如，https://rest.media.azure.net)。

    * REST 媒體服務的資源 URI。

        hello URI 表示 hello REST API 端點 (例如，https://test03.restv2.westus.media.azure.net/api/)。

    * Azure AD 應用程式的值： hello 用戶端識別碼和用戶端密碼。
    
    tooget 值，這些參數，請參閱[使用 hello Azure 入口網站 tooaccess Azure AD 驗證設定](media-services-portal-get-started-with-aad.md)使用 hello 服務主體的驗證選項。

2. hello Azure AD 存取權杖會傳送 toohello 中介層。
4. hello 中介層會傳送 hello Azure AD 權杖的要求 toohello Azure 媒體 REST API。
5. hello 中介層回取得 Media Services hello 資料。

如需有關如何使用 Media Services.NET 用戶端 hello SDK toouse Azure AD 驗證 toocommunicate 與其他要求的詳細資訊，請參閱[使用 Azure AD 驗證 tooaccess 與.NET 的 Azure 媒體服務 API](media-services-dotnet-get-started-with-aad.md)。 

如果您未使用 Media Services.NET 用戶端 hello SDK，您必須手動建立的 Azure AD 的權杖要求，使用步驟 1 中所述的參數。 如需詳細資訊，請參閱[toouse hello Azure AD 驗證程式庫 tooget 如何 hello Azure AD 權杖](../active-directory/develop/active-directory-authentication-libraries.md)。

## <a name="troubleshooting"></a>疑難排解

例外狀況:"hello 遠端伺服器傳回錯誤: (401) 未授權。 」

解決方案： Hello 媒體服務 REST 要求 toosucceed，hello 呼叫使用者必須 hello 它嘗試 tooaccess Media Services 帳戶中的參與者或擁有者角色。 如需詳細資訊，請參閱 hello[存取控制](media-services-use-aad-auth-to-access-ams-api.md#access-control)> 一節。

## <a name="resources"></a>資源

下列文件的 hello 是 Azure AD 驗證概念的概觀： 

- [Azure AD 的驗證案例](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [在 Azure AD 新增、更新或移除應用程式](../active-directory/develop/active-directory-integrating-applications.md)
- [使用 PowerShell 設定及 管理角色型存取控制](../active-directory/role-based-access-control-manage-access-powershell.md)

## <a name="next-steps"></a>後續步驟

* 使用 Azure 入口網站 hello 太[存取 Azure AD 驗證 tooconsume Azure Media Services API](media-services-portal-get-started-with-aad.md)。
* 使用 Azure AD 驗證太[存取 Azure Media Services API 的.NET](media-services-dotnet-get-started-with-aad.md)。

