---
title: "aaaGet 使用 hello Azure 入口網站來啟動 Azure AD 驗證與 |Microsoft 文件"
description: "了解如何 toouse hello Azure 入口網站 tooaccess Azure Active Directory (Azure AD) 驗證 tooconsume hello Azure 媒體服務 API。"
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
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a>開始使用 Azure AD 驗證使用 hello Azure 入口網站

了解如何 toouse hello Azure 入口網站 tooaccess Azure Active Directory (Azure AD) 驗證 tooaccess hello Azure 媒體服務 API。

## <a name="prerequisites"></a>必要條件

- 一個 Azure 帳戶。 如果您沒有帳戶，請先從 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。 
- 媒體服務帳戶。 如需詳細資訊，請參閱[使用 hello Azure 入口網站建立 Azure Media Services 帳戶](media-services-portal-create-account.md)。
- 請確定您檢閱 hello[存取 Azure 媒體服務應用程式開發介面與 Azure AD 驗證概觀](media-services-use-aad-auth-to-access-ams-api.md)。 

當您使用 Azure AD 驗證搭配 Azure 媒體服務 時，會有兩個驗證選項：

- **使用者驗證**。 驗證使用 hello 應用程式 toointeract 和媒體服務資源的人員。 hello 互動式應用程式應該會先提示 hello 使用者提供認證。 範例是由授權的使用者 toomonitor 編碼工作的主控台應用程式管理或即時資料流。 
- **服務主體驗證**。 驗證服務。 通常使用這種驗證方法的應用程式有執行精靈服務、中介層服務或排程的工作的應用程式：Web 應用程式、函數應用程式、邏輯應用程式、API 或微服務。

> [!IMPORTANT]
> 目前，Media Services 支援 hello Azure 存取控制服務驗證模型。 不過，存取控制授權將在 2018 年 6 月 1 日被取代。 我們建議您儘速移轉 toohello Azure AD 驗證模型。

## <a name="select-hello-authentication-method"></a>選取 hello 驗證方法

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Media Services 帳戶。
2. 選取如何 tooconnect toohello 媒體服務 API。

    ![選取連線方式的頁面](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a>使用者驗證

tooconnect toohello Media Services API 使用 hello 使用者驗證選項，hello 用戶端應用程式需要 toorequest 具有 hello 下列參數的 Azure AD 權杖：  

* Azure AD 租用戶端點
* 媒體服務資源 URI
* 媒體服務 (原生) 應用程式用戶端識別碼 
* 媒體服務 (原生) 應用程式重新導向 URI 
* REST 媒體服務的資源 URI

您可以取得這些參數在 hello hello 值**Media Services API 的使用者驗證**頁面。 

![使用使用者驗證頁面連線](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

如果您使用 Media Services 的 Microsoft.NET SDK hello 連接 toohello Media Services API，hello 必要的值可用 tooyou hello SDK 的一部分。 如需詳細資訊，請參閱[使用 Azure AD 驗證 tooaccess hello 與.NET 的 Azure 媒體服務 API](media-services-dotnet-get-started-with-aad.md)。

如果您未使用 Media Services.NET 用戶端 hello SDK，所以您必須使用先前所討論的 hello 參數，手動建立的 Azure AD 的權杖要求。 如需詳細資訊，請參閱[toouse hello Azure AD 驗證程式庫 tooget 如何 hello Azure AD 權杖](../active-directory/develop/active-directory-authentication-libraries.md)。

## <a name="service-principal-authentication"></a>服務主體驗證

tooconnect toohello Media Services API 使用 hello 服務主體的選項中, 介層應用程式 （web API 或 web 應用程式） 需要 toorequest 具有 hello 下列參數的 Azure AD 權杖：  

* Azure AD 租用戶端點
* 媒體服務資源 URI 
* REST 媒體服務的資源 URI
* Azure AD 應用程式的值： hello**用戶端識別碼**和**用戶端密碼**

您可以取得這些參數在 hello hello 值**連接 tooMedia 服務應用程式開發介面與服務主體**頁面。 使用此頁面 toocreate 新的 Azure AD 應用程式或 tooselect 現有。 選取 hello Azure AD 應用程式之後，您可以取得 hello 用戶端識別碼 （應用程式識別碼），並產生 hello 用戶端密碼 （金鑰） 值。 

![使用服務主體連線的頁面](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

當 hello**服務主體**刀鋒視窗中開啟時，會選取 hello 第一個 Azure AD 應用程式符合下列準則的 hello:

- 它是已註冊的 Azure AD 應用程式。
- 它對 hello 帳戶參與者或 Owner Role-Based 存取控制的權限。

您建立或選取 Azure AD 應用程式之後，您可以建立和複製用戶端密碼 （金鑰） 和 hello 用戶端識別碼 （應用程式識別碼）。 hello 用戶端密碼和用戶端識別碼是在此案例中需要的 tooget hello 存取權杖。

如果您沒有權限 toocreate Azure AD 應用程式網域中，不會顯示 hello Azure AD 應用程式控制項的 hello 刀鋒視窗，並會顯示警告訊息。

如果您使用 Media Services.NET SDK hello 連接 toohello Media Services API，請參閱[使用 Azure AD 驗證 tooaccess hello 與.NET 的 Azure 媒體服務 API](media-services-dotnet-get-started-with-aad.md)。

如果您未使用 Media Services.NET 用戶端 hello SDK，您必須手動建立使用先前所討論的 hello 參數的 Azure AD 權杖要求。 如需詳細資訊，請參閱[toouse hello Azure AD 驗證程式庫 tooget 如何 hello Azure AD 權杖](../active-directory/develop/active-directory-authentication-libraries.md)。

### <a name="get-hello-client-id-and-client-secret"></a>取得 hello 用戶端識別碼和用戶端密碼

您選取現有的 Azure AD 應用程式或選取 hello 選項 toocreate 新之後，會顯示 hello 下列按鈕：

![[Manage permissions] \(管理權限\) 和 [Manage application] \(管理應用程式\) 按鈕](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

tooopen hello Azure AD 應用程式 刀鋒視窗中，按一下**管理應用程式**。 在 hello**管理應用程式**刀鋒視窗中，您可以取得 hello 應用程式的用戶端識別碼 （應用程式識別碼）。 用戶端密碼 （金鑰），選取 toogenerate**金鑰**。

![管理應用程式刀鋒視窗的 [Keys] \(金鑰\) 選項](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a>管理權限和 hello 應用程式

選取 hello Azure AD 應用程式之後，您可以管理 hello 應用程式和權限。 tooset 其他應用程式中，按一下 註冊您的 Azure AD 應用程式 tooaccess**管理權限**。 管理工作，例如變更索引鍵和回覆 Url 或 tooedit hello 應用程式的資訊清單中，按一下**管理應用程式**。

### <a name="edit-hello-apps-settings-or-manifest"></a>編輯 hello 應用程式設定或資訊清單

tooedit hello 應用程式的設定或資訊清單中，按一下**管理應用程式**。

![管理應用程式頁面](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a>後續步驟

開始使用[上傳檔案 tooyour 帳戶](media-services-portal-upload-files.md)。
