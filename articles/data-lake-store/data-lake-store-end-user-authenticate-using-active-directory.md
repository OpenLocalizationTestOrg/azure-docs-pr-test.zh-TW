---
title: "使用者驗證︰搭配使用 Azure Active Directory 與 Data Lake Store | Microsoft Docs"
description: "深入了解如何使用 Azure Active Directory 的 Data Lake Store tooachieve 使用者驗證"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a>使用 Azure Active Directory 以 Data Lake Store 進行使用者驗證
> [!div class="op_single_selector"]
> * [服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)
> * [使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store 使用 Azure Active Directory 進行驗證。 如果之前撰寫的應用程式，適用於 Azure 資料湖存放區或 Azure Data Lake Analytics，您必須先決定您希望如何 tooauthenticate 應用程式與 Azure Active Directory (Azure AD)。 hello 兩個主要選項如下：

* 使用者驗證 (本文)
* 服務對服務驗證

這兩個選項會導致以 OAuth 2.0 權杖取得附加的 tooeach 所提出的要求 tooAzure 資料湖存放區或 Azure Data Lake Analytics 所提供的應用程式。

本文說明如何建立 **Azure AD 原生應用程式以進行使用者驗證**。 如需服務對服務驗證的 Azure AD 應用程式組態的指示，請參閱[使用 Azure Active Directory 以 Data Lake Store 進行服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。

## <a name="prerequisites"></a>必要條件
* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

* 您的訂用帳戶識別碼。 您可以從 hello Azure 入口網站來擷取它。 例如，它位於 hello Data Lake Store 帳戶 刀鋒視窗。
  
    ![取得訂用帳戶識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* 您的 Azure AD 網域名稱。 您可以透過暫留在 hello 右上角的 hello Azure 入口網站中的 hello 滑鼠擷取它。 Hello 網域名稱是從 hello 以下螢幕擷取畫面， **contoso.onmicrosoft.com**，和括號中的 hello GUID 是 hello 租用戶識別碼。 
  
    ![取得 AAD 網域](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a>使用者驗證
這是建議的方法，如果您想在 tooyour 應用程式透過 Azure AD 使用者 toolog hello。 您的應用程式將會無法 tooaccess 以 hello Azure 資源相同的存取層級 hello 使用者的登入。 您的使用者將需要 tooprovide 定期為了讓您的應用程式 toomaintain 存取其認證。

擁有 hello 使用者登入的 hello 結果是您的應用程式提供存取權杖和重新整理權杖。 hello 存取權杖取得附加的 tooeach 要求 tooData 湖存放區或資料湖分析，並有效期為一小時的預設值。 可以使用新的存取權杖，以及它無效，向上 tootwo 週，根據預設，如果定期使用的 tooobtain hello 重新整理權杖。 您可以使用兩種不同方法讓使用者登入。

### <a name="using-hello-oauth-20-pop-up"></a>使用 OAuth 2.0 hello 快顯視窗
您的應用程式可以觸發 OAuth 2.0 授權快顯視窗，在哪一個 hello 使用者輸入其認證。 這個快顯視窗也會搭配 hello Azure AD 雙因素驗證 (2FA) 程序，視需要。 

> [!NOTE]
> 不是支援這個方法尚未在 hello Azure AD 驗證程式庫 (ADAL) 的 Python 或 Java。
> 
> 

### <a name="directly-passing-in-user-credentials"></a>直接傳遞使用者認證
您的應用程式可以直接提供使用者認證 tooAzure AD。 這個方法僅適用於有組織識別碼的使用者帳戶；不適用於個人/「Live ID」使用者帳戶 (包括以 @outlook.com 或 @live.com 結尾的帳戶)。此外，這個方法與需要 Azure AD 雙因素驗證 (2FA) 的使用者帳戶不相容。

### <a name="what-do-i-need-toouse-this-approach"></a>採取這種方法需要 toouse？
* Azure AD 網域名稱。 這已經列於本文章的 hello 必要條件。
* Azure AD **原生應用程式**
* Hello Azure AD 的原生應用程式的應用程式識別碼
* Hello Azure AD 的原生應用程式重新導向 URI
* 設定委派權限


## <a name="step-1-create-an-active-directory-native-application"></a>步驟 1：建立 Active Directory 原生應用程式

建立和設定 Azure AD 原生應用程式，以便使用 Azure Active Directory 以 Azure Data Lake Store 進行使用者驗證。 如需指示，請參閱[建立 Azure AD 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md)。

遵循上述連結 hello hello 指示，請確定您選取**原生**應用程式類型，如 hello 以下螢幕擷取畫面所示。

![建立 Web 應用程式](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "建立原生應用程式")

## <a name="step-2-get-application-id-and-redirect-uri"></a>步驟 2：取得應用程式識別碼和重新導向 URI

請參閱[取得 hello 應用程式識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)tooretrieve hello 的應用程式識別碼 （也稱為 hello Azure 傳統入口網站中的 hello 用戶端識別碼） hello Azure AD 的原生應用程式。

tooretrieve hello 重新導向 URI，請遵循下列 hello 步驟。

1. Hello Azure 入口網站，從選取**Azure Active Directory**，按一下 **應用程式註冊**，然後尋找並按一下您剛才建立的 Azure AD hello 原生應用程式。

2. 從 hello**設定**刀鋒視窗中的 hello 應用程式中，按一下**重新導向 Uri**。

    ![取得重新導向 URI](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. 複製顯示 hello 值。


## <a name="step-3-set-permissions"></a>步驟 3：設定權限

1. Hello Azure 入口網站，從選取**Azure Active Directory**，按一下 **應用程式註冊**，然後尋找並按一下您剛才建立的 Azure AD hello 原生應用程式。

2. 從 hello**設定**刀鋒視窗中的 hello 應用程式中，按一下**必要的權限**，然後按一下**新增**。

    ![用戶端識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. 在 hello**加入應用程式開發介面存取**刀鋒視窗中，按一下**選取應用程式開發介面**，按一下**Azure 資料湖**，然後按一下**選取**。

    ![用戶端識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  在 hello**加入應用程式開發介面存取**刀鋒視窗中，按一下 [**選取權限**，選取 hello] 核取方塊 toogive**完整存取 tooData Lake Store**，然後按一下**選取**.

    ![用戶端識別碼](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    按一下 [完成] 。

5. 重複的 hello 最後的兩個步驟 toogrant 權限**Windows Azure 服務管理 API**以及。
   
## <a name="next-steps"></a>後續步驟
在本文中，您建立 Azure AD 的原生應用程式並收集到您需要在您撰寫使用.NET SDK、 Java SDK、 REST API 等用戶端應用程式中的 hello 資訊。您可以現在繼續 toohello 下列文章會討論如何 toouse hello Azure AD web 應用程式 toofirst 向資料湖存放區，然後再執行 hello 存放區上的其他操作。

* [使用 .NET SDK 開始使用 Azure Data Lake Store](data-lake-store-get-started-net-sdk.md)
* [使用 Java SDK 開始使用 Azure Data Lake Store](data-lake-store-get-started-java-sdk.md)
* [使用 REST API 開始使用 Azure Data Lake Store](data-lake-store-get-started-rest-api.md)

