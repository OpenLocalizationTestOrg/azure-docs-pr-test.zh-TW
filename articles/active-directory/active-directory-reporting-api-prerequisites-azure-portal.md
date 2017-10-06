---
title: "aaaPrerequisites tooaccess hello Azure AD 報告 API |Microsoft 文件"
description: "深入了解 hello 必要條件 tooaccess hello Azure AD 報告 API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>必要條件 tooaccess hello Azure AD 報告 API

hello [Azure AD 報告 Api](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview)提供您透過一組以 REST 為基礎的 Api 以程式設計方式存取 toohello 資料。 您可以從各種程式設計語言和工具呼叫這些 API。

報告應用程式開發介面使用的 hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize 存取 toohello web Api。 

tooget 透過 hello API 存取 toohello 報告資料，您需要 toohave hello 遵循指派角色的其中一個：

- 安全性讀取者
- 安全性系統管理員
- 全域管理員


tooprepare 報告 API 您存取 toohello，您必須：

1. 註冊應用程式 
2. 授與權限 
3. 收集組態設定 

如有相關疑問、問題或意見，請[提出支援票證](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)。

## <a name="register-an-azure-active-directory-application"></a>註冊 Azure Active Directory 應用程式

即使您要存取 hello 報告 API 使用指令碼，您會需要 tooregister 應用程式。 這可讓您**應用程式識別碼**，這是必要的授權呼叫它可讓您的程式碼 tooreceive 語彙基元。

tooconfigure 目錄 tooaccess hello Azure AD 報告 API，您必須登入 toohello hello 的成員也是 Azure 系統管理員帳戶的 Azure 入口網站**全域管理員**Azure AD 租用戶中的目錄角色.

> [!IMPORTANT]
> 使用像這樣的"admin"權限認證下執行的應用程式可能非常強大，因此請在確定 tookeep hello 應用程式的識別碼/密碼認證的安全性。
> 


**tooregister Azure Active Directory 應用程式：**

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. 在 [hello **Azure Active Directory**刀鋒視窗中，按一下 [**應用程式註冊**。

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. 在 [hello**應用程式註冊**刀鋒視窗中，在 hello 頂端的 hello 工具列中按一下**新應用程式註冊**。

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. 在 [hello**建立**刀鋒視窗中，執行下列步驟的 hello:

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    a. 在 [hello**名稱**文字方塊中，輸入`Reporting API application`。

    b. 對於 [應用程式類型]，選取 [Web 應用程式/API]。

    c. 在 [hello**登入 URL**文字方塊中，輸入`https://localhost`。

    d. 按一下 [建立] 。 


## <a name="grant-permissions"></a>授與權限 

這個步驟中的 hello 目標應用程式是 toogrant**讀取目錄資料**權限 toohello **Windows Azure Active Directory**應用程式開發介面。

![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**toogrant 您應用程式的權限 toouse hello API:**

1. 在 [hello**應用程式註冊**刀鋒視窗中的，在 hello 應用程式清單中，按一下**Reporting API 的應用程式**。

2. 在 [hello **Reporting API 的應用程式**刀鋒視窗中，在 hello 頂端的 hello 工具列中按一下**設定**。 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. 在 [hello**設定**刀鋒視窗中，按一下 [**必要的權限**。 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. 在 [hello**必要的權限**刀鋒視窗中的，在 hello **API**清單中，按一下**Windows Azure Active Directory**。 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. 在 [hello**啟用存取**刀鋒視窗中，選取**讀取目錄資料**。 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. 在 hello hello 上方的工具列中按一下**儲存**。

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a>收集組態設定 
這個區段會顯示如何 tooget hello 您目錄中的下列設定：

* 網域名稱
* 用戶端識別碼
* 用戶端密碼

設定呼叫 toohello 報告 API 時，您會需要這些值。 

### <a name="get-your-domain-name"></a>取得您的網域名稱

**tooget 您的網域名稱：**

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. 在 [hello **Azure Active Directory**刀鋒視窗中，按一下 [**網域名稱**。

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. 複製 hello 網域清單中的網域名稱。


### <a name="get-your-applications-client-id"></a>取得應用程式的用戶端識別碼

**tooget 應用程式的用戶端識別碼：**

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. 在 [hello**應用程式註冊**刀鋒視窗中的，在 hello 應用程式清單中，按一下**Reporting API 的應用程式**。

3. 在 [hello **Reporting API 的應用程式**刀鋒視窗中的，在 hello**應用程式識別碼**，按一下 [**按一下 toocopy**。

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>取得應用程式的用戶端祕密
tooget 應用程式的用戶端秘密，toocreate 新的金鑰，儲存其值在儲存 hello 新的金鑰，因為它不可能 tooretrieve 時這個值稍後再。

**tooget 應用程式的用戶端密碼：**

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. 在 [hello**應用程式註冊**刀鋒視窗中的，在 hello 應用程式清單中，按一下**Reporting API 的應用程式**。


3. 在 [hello **Reporting API 的應用程式**刀鋒視窗中，在 hello 頂端的 hello 工具列中按一下**設定**。 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. 在 [hello**設定**刀鋒視窗中的，在 hello **APIR 存取**區段中，按一下**金鑰**。 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. 在 [hello**金鑰**刀鋒視窗中，執行下列步驟的 hello:

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    a. 在 [hello**描述**文字方塊中，輸入`Reporting API`。

    b. 選取 [2 年後] 來作為 [到期]。

    c. 按一下 [儲存] 。

    d. 複製 hello 索引鍵的值。


## <a name="next-steps"></a>後續步驟
* 您像 tooaccess hello hello Azure AD 的資料會報告 API 以程式設計的方式？ 簽出[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)。
* 如果您想要深入了解 Azure Active Directory 報告 toofind，請參閱 hello [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。  

