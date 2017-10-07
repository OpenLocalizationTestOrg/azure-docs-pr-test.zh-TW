---
title: "aaaPrerequisites tooaccess hello Azure AD 報告 API。 | Microsoft Docs"
description: "深入了解 hello 必要條件 tooaccess hello Azure AD 報告 API"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>必要條件 tooaccess hello Azure AD 報告 API
hello [Azure AD 報告 Api](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview)提供您透過一組以 REST 為基礎的 Api 以程式設計方式存取 toohello 資料。 您可以從各種程式設計語言和工具呼叫這些 API。

報告應用程式開發介面使用的 hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize 存取 toohello web Api。 

tooprepare 報告 API 您存取 toohello，您必須：

1. 在 Azure AD 租用戶中建立應用程式 
2. 授與 hello 應用程式適當的權限 tooaccess hello Azure AD 資料
3. 從您的目錄蒐集組態設定

如有相關疑問、問題或意見，請連絡 [AAD 報告協助](mailto:aadreportinghelp@microsoft.com)。

## <a name="create-an-azure-ad-application"></a>建立 Azure AD 應用程式
tooconfigure 目錄 tooaccess hello Azure AD 報告 API，您必須登入 toohello 也是 Azure AD 租用戶中的 hello 全域管理員目錄角色成員的 Azure 訂用帳戶系統管理員帳戶的 Azure 傳統入口網站。

> [!IMPORTANT]
> 使用像這樣的"admin"權限認證下執行的應用程式可能非常強大，因此請在確定 tookeep hello 應用程式的識別碼/密碼認證的安全性。
> 
> 

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. 從 hello **active directory**清單中，選取您的目錄。
3. 在 hello 最上層顯示 hello 功能表上，按一下**應用程式**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Hello 下方列上，按一下**新增**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/03.png) 
5. 在 [hello**怎麼辦想 toodo？** ] 對話方塊中，按一下**加入我組織正在開發的應用程式**。 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/04.png) 
6. 在 [hello**告訴我們您的應用程式**] 對話方塊中，執行下列步驟的 hello: 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. 在 hello**名稱**文字方塊中，輸入名稱 (例如： 報告 API 應用程式)。
   
    b. 選取 [Web 應用程式和/或 Web API]。
   
    c. 按一下 [下一步] 。
7. 在 [hello**應用程式屬性**] 對話方塊中，執行下列步驟的 hello: 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. 在 hello**登入 URL**文字方塊中，輸入`https://localhost`。
   
    b. 在 hello**應用程式識別碼 URI**文字方塊中，輸入```https://localhost/ReportingApiApp```。
   
    c. 按一下頁面底部的 [新增] 。

## <a name="grant-your-application-permission-toouse-hello-api"></a>授與您的應用程式的權限 toouse hello 應用程式開發介面
1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. 從 hello **active directory**清單中，選取您的目錄。
3. 在 hello 最上層顯示 hello 功能表上，按一下**應用程式**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png)
4. 在 hello 應用程式清單中，選取您新建立的應用程式。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/07.png)
5. 在 hello 最上層顯示 hello 功能表上，按一下**設定**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/08.png)
6. 在 hello**權限 tooother 應用程式** 區段下的 hello **Azure Active Directory**資源按一下 hello**應用程式權限**下拉式清單，然後選取**讀取目錄資料**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/09.png)
7. Hello 下方列上，按一下**儲存**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>從您的目錄蒐集組態設定
這個區段會顯示如何 tooget hello 您目錄中的下列設定：

* 網域名稱
* 用戶端識別碼
* 用戶端密碼

設定呼叫 toohello 報告 API 時，您會需要這些值。 

### <a name="get-your-domain-name"></a>取得您的網域名稱
1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. 從 hello **active directory**清單中，選取您的目錄。
3. 在 hello 最上層顯示 hello 功能表上，按一下**網域**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/11.png) 
4. 在 hello**網域名稱**資料行中，複製您的網域名稱。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a>取得 hello 應用程式的用戶端識別碼
1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. 從 hello **active directory**清單中，選取您的目錄。
3. 在 hello 最上層顯示 hello 功能表上，按一下**應用程式**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png) 
4. 在 hello 應用程式清單中，選取您新建立的應用程式。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/07.png)
5. 在 hello 最上層顯示 hello 功能表上，按一下**設定**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/08.png)
6. 複製您的 [用戶端識別碼] 。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a>取得 hello 應用程式的用戶端密碼
tooget 應用程式的用戶端秘密，toocreate 新的金鑰，儲存其值在儲存 hello 新的金鑰，因為它不可能 tooretrieve 時這個值稍後再。

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. 從 hello **active directory**清單中，選取您的目錄。
3. 在 hello 最上層顯示 hello 功能表上，按一下**應用程式**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png) 
4. 在 hello 應用程式清單中，選取您新建立的應用程式。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/07.png)
5. 在 hello 最上層顯示 hello 功能表上，按一下**設定**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/08.png)
6. 在 hello**金鑰**區段中，執行下列步驟的 hello: 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. 從 hello 持續時間] 清單中，選取 [持續時間
   
    b. Hello 下方列上，按一下**儲存**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. 複製 hello 索引鍵的值。

## <a name="next-steps"></a>後續步驟
* 您像 tooaccess hello hello Azure AD 的資料會報告 API 以程式設計的方式？ 簽出[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)。
* 如果您想要深入了解 Azure Active Directory 報告 toofind，請參閱 hello [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。  

