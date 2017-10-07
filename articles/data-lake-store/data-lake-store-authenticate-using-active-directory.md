---
title: "服務對服務驗證︰使用 Azure Active Directory 以 Data Lake Store 進行 | Microsoft Docs"
description: "深入了解如何使用 Azure Active Directory 的 Data Lake Store tooachieve 服務對服務驗證"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 2e56237a75f020067b3248a1e1cfaf3c8df1371c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a>使用 Azure Active Directory 以 Data Lake Store 進行服務對服務驗證
> [!div class="op_single_selector"]
> * [服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)
> * [使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store 使用 Azure Active Directory 進行驗證。 如果之前撰寫的應用程式，適用於 Azure 資料湖存放區或 Azure Data Lake Analytics，您必須先決定您希望如何 tooauthenticate 應用程式與 Azure Active Directory (Azure AD)。 hello 兩個主要選項如下：

* 使用者驗證 
* 服務對服務驗證 (本文) 

這兩個選項會導致以 OAuth 2.0 權杖取得附加的 tooeach 所提出的要求 tooAzure 資料湖存放區或 Azure Data Lake Analytics 所提供的應用程式。

本文說明如何建立 **Azure AD Web 應用程式以進行服務對服務驗證**。 如需有關適用於使用者驗證的 Azure AD 應用程式組態的指示，請參閱[使用 Azure Active Directory 以 Data Lake Store 進行使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)。

## <a name="prerequisites"></a>必要條件
* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="step-1-create-an-active-directory-web-application"></a>步驟 1：建立 Active Directory Web 應用程式

建立和設定 Azure AD Web 應用程式，以便使用 Azure Active Directory 以 Azure Data Lake Store 進行服務對服務驗證。 如需指示，請參閱[建立 Azure AD 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md)。

遵循上述連結 hello hello 指示，請確定您選取**Web 應用程式 / 應用程式開發介面**應用程式類型，如 hello 以下螢幕擷取畫面所示。

![建立 Web 應用程式](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "建立 Web 應用程式")

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a>步驟 2：取得應用程式識別碼、驗證金鑰及租用戶識別碼
以程式設計方式登入時，您將在您的應用程式需要 hello 識別碼。 如果 hello 應用程式是在它自己的認證下執行，您也必須驗證金鑰。

* 如需如何 tooretrieve hello 應用程式識別碼和驗證金鑰 （也稱為的 hello 用戶端機密） 應用程式的指示，請參閱[取得應用程式識別碼和驗證金鑰](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)。

* 如需有關如何 tooretrieve hello 租用戶識別碼的指示，請參閱[取得租用戶識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id)。

## <a name="step-3-assign-hello-azure-ad-application-toohello-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a>步驟 3： 指派 hello Azure AD 應用程式 toohello Azure Data Lake Store 帳戶的檔案或資料夾 （僅適用於服務對服務驗證）
1. 登入新 toohello [Azure 入口網站](https://portal.azure.com)並開啟您想以 hello 您稍早建立的 Azure Active Directory 應用程式的 tooassociate hello Azure Data Lake Store 帳戶。
2. 在您的 [資料湖儲存區帳戶] 刀鋒視窗中，按一下 [資料總管] 。
   
    ![在 Data Lake Store 帳戶中建立目錄](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "在 Data Lake Store 帳戶中建立目錄")
3. 在 hello**資料總管**刀鋒視窗中，按一下 hello 檔案或資料夾，您想 tooprovide 存取 toohello Azure AD 應用程式，然後按一下**存取**。 tooconfigure access tooa 檔案，您必須按一下**存取**從 hello**檔案預覽**刀鋒視窗。
   
    ![設定 Data Lake 檔案系統上的 ACL](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "設定 Data Lake 檔案系統上的 ACL")
4. hello**存取**刀鋒視窗會列出 hello 標準權限和自訂存取已指派 toohello 根。 按一下 hello**新增**圖示 tooadd 自訂層級的 Acl。
   
    ![列出標準和自訂存取](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "列出標準和自訂的存取")
5. 按一下 hello**新增**圖示 tooopen hello**加入自訂存取**刀鋒視窗。 在這個刀鋒視窗中，按一下**選取使用者或群組**，然後在**選取使用者或群組**刀鋒視窗中，尋找您稍早建立的 hello Azure Active Directory 應用程式。 如果您有大量從群組 toosearch，使用 hello 文字方塊在 hello 頂端 toofilter hello 群組名稱。 按一下您想 tooadd，然後按一下 hello 群組**選取**。
   
    ![加入群組](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "加入群組")
6. 按一下**選取權限**選取 hello 權限，是否要為一份預設 ACL 將 tooassign hello 權限，存取 ACL，或兩者。 按一下 [確定] 。
   
    ![指派權限 toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "指派權限 toogroup")
   
    如需有關 Data Lake Store 中的權限及預設/存取 ACL 的詳細資訊，請參閱 [Data Lake Store 中的存取控制](data-lake-store-access-control.md)。
7. 在 hello**加入自訂存取**刀鋒視窗中，按一下**確定**。 hello 新加入的群組相關聯的 hello 權限，現在會列在 hello**存取**刀鋒視窗。
   
    ![指派權限 toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "指派權限 toogroup")

## <a name="step-4-get-hello-oauth-20-token-endpoint-only-for-java-based-applications"></a>步驟 4： 取得 hello OAuth 2.0 權杖端點 （僅適用於 Java 為基礎的應用程式）

1. 登入新 toohello [Azure 入口網站](https://portal.azure.com)從 hello 左窗格中按一下 Active Directory。

2. 從 hello 左窗格中，按一下 **應用程式註冊**。

3. 從 hello hello 應用程式註冊刀鋒視窗頂端，按一下 **端點**。

    ![OAuth 權杖端點](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth 權杖端點")

4. 從 [hello] 清單中的端點，複製到 hello OAuth 2.0 權杖端點。

    ![OAuth 權杖端點](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth 權杖端點")   

## <a name="next-steps"></a>後續步驟
在本文中您建立的 Azure AD web 應用程式，並收集您需要在用戶端應用程式中您撰寫使用.NET SDK、 Java SDK 等 hello 資訊。您可以現在繼續 toohello 下列文章會討論如何 toouse hello Azure AD web 應用程式 toofirst 向資料湖存放區，然後再執行 hello 存放區上的其他操作。

* [使用 .NET SDK 開始使用 Azure Data Lake Store](data-lake-store-get-started-net-sdk.md)
* [使用 Java SDK 開始使用 Azure Data Lake Store](data-lake-store-get-started-java-sdk.md)

這篇文章帶您完成 hello 基本步驟所需 tooget 主體註冊並執行您的應用程式的使用者。 您可以查看下列文章 tooget 進一步資訊的 hello:
* [使用 PowerShell toocreate 服務主體](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [使用憑證驗證進行服務主體驗證](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [其他方法 tooauthenticate tooAzure AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


