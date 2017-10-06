---
title: "在應用程式的頁面上，在登入後 aaaError |Microsoft 文件"
description: "如何使用 Azure AD 的 tooresolve 問題時登入 hello 應用程式本身會發出錯誤"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a>登入後應用程式頁面的錯誤

在此案例中，Azure AD 已簽署 hello 使用者，但是 hello 應用程式會顯示不允許 hello 使用者 toosuccessfully 完成 hello 登流程中發生錯誤。 在此案例中，hello 應用程式不接受 hello 回應問題由 Azure AD。

有可能的原因為何 hello 應用程式不接受來自 Azure AD 的 hello 回應。 如果 hello 應用程式中的 hello 錯誤是不明確，足以 tooknow 遺漏了什麼 hello 回應，然後：

-   如果 hello 應用程式 hello Azure AD 的組件庫，請確認您已依照 hello 文件中的所有 hello 步驟[如何 toodebug SAML 型單一登入 tooapplications Azure Active Directory 中](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)。

-   使用這類工具[Fiddler](http://www.telerik.com/fiddler) toocapture SAML 要求，SAML 回應和 SAML 語彙基元。

-   缺少哪些資訊與 hello 應用程式廠商 tooknow 共用 hello SAML 回應。

## <a name="missing-attributes-in-hello-saml-response"></a>Hello SAML 回應中遺漏屬性

tooadd Azure AD hello 回應 hello Azure AD 組態 toobe 中的屬性，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

   * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  按一下**檢視及編輯所有其他使用者屬性下**hello**使用者屬性**區段 tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。

   tooadd 屬性：

   * 按一下 [新增屬性]。 輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。

   * 按一下 [儲存]。 您會看到 hello hello 資料表中的新屬性。

9.  儲存 hello 組態。

下一次 hello 使用者登入時 toohello 應用程式，Azure AD 傳送 hello SAML 回應 hello 新屬性。

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a>hello 應用程式預期不同的使用者識別碼值或格式

hello 登入 toohello 應用程式失敗，因為 SAML 回應 hello 遺失屬性，例如角色或因為 hello 應用程式預期不同格式的 hello EntityID 屬性。

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a>將屬性加入 hello Azure AD 應用程式組態中：

toochange hello 使用者識別碼的值，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

   * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  在 [hello**使用者屬性**，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。

## <a name="change-entityid-user-identifier-format"></a>變更 EntityID (使用者識別碼) 格式

如果 hello 應用程式預期 hello EntityID 屬性的另一種格式。 然後，您必須能夠 tooselect hello EntityID （使用者識別碼） 格式，Azure AD 會傳送 toohello 應用程式以 hello 回應使用者驗證之後。

Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。 如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 下一節 NameIDPolicy。

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a>hello 應用程式預期 hello SAML 回應不同的簽章方法

Azure Active Directory 進行數位簽署 hello SAML 權杖中的哪些部分 toochange。 請遵循下列步驟執行 hello:

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  按一下**顯示進階憑證簽署設定**下 hello **SAML 簽章憑證**> 一節。

9.  選取適當的 hello**簽署選項**hello 應用程式所需要：

  * 簽署 SAML 回應

  * 簽署 SAML 回應及判斷提示

  * 簽署 SAML 判斷提示

下一次 hello 使用者登入時 toohello 應用程式，Azure AD 登 hello 選取 hello SAML 回應的一部分。

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a>hello 應用程式必須要有簽章演算法 toobe sha-1 hello

根據預設，Azure AD 簽署 hello SAML 權杖使用 hello 大部分的安全性演算法。 不建議變更 hello 登演算法 tooSHA-1，除非需要 hello 應用程式。

toochange hello 簽章演算法，請依照下列步驟執行 hello:

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

   * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  按一下**顯示進階憑證簽署設定**下 hello **SAML 簽章憑證**> 一節。

9.  選取在 hello sha-1**簽署演算法**。

下一次 hello 使用者登入，toohello 應用程式中的，Azure AD 登 hello 使用 sha-1 演算法的 SAML 權杖。

## <a name="next-steps"></a>後續步驟
[如何 toodebug SAML 型單一登入 tooapplications Azure Active Directory 中](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
