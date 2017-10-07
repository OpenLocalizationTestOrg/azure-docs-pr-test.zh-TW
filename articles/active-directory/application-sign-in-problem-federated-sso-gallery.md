---
title: "aaaProblems 登入 tooa 圖庫應用程式設定同盟單一登入 |Microsoft 文件"
description: "您所設定的 SAML 型同盟單一登入與 Azure AD 的登入應用程式時，即 hello 特定錯誤的指引"
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
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a>登入 tooa 圖庫應用程式設定同盟單一登入問題

tootroubleshoot 您的問題，您需要在 Azure AD 做為後續 tooverify hello 應用程式組態：

-   您已依照 hello Azure AD 組件庫的應用程式的所有 hello 組態步驟。

-   hello 識別碼和設定在 AAD 中的回覆 URL 符合它們 hello 應用程式中的預期值

-   您已指派使用者 toohello 應用程式

## <a name="application-not-found-in-directory"></a>在目錄中找不到應用程式

*錯誤 AADSTS70001: Hello 目錄中未找到具有識別碼 'https://contoso.com' 的應用程式*。

**可能的原因**

hello 簽發者屬性會從傳送 hello 應用程式 tooAzure hello SAML 要求中的 AD 與 hello hello 應用程式的 Azure AD 中設定的識別項值不相符。

**解決方案**

請確定它符合 hello Azure AD 中所設定的識別碼值的 hello SAML 要求中的 hello 簽發者屬性：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  跳過**網域和 Url** > 一節。 請確認 hello 值在 hello 相符 hello 值顯示在 hello 錯誤中的 hello 識別碼值的文字方塊中的識別項。

您已在 Azure AD 中更新 hello 識別碼的值，並透過 hello hello SAML 要求中的應用程式將與其相符 hello 的值之後，您應該能夠 toosign toohello 應用程式中。

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a>hello 回覆地址不符 hello 回覆地址為 hello 應用程式設定。

*錯誤 AADSTS50011: hello 的回覆地址 'https://contoso.com' 不符合為 hello 應用程式設定的 hello 回覆位址*

**可能的原因**

hello AssertionConsumerServiceURL hello SAML 要求中的值不符合 hello 回覆 URL 的值或在 Azure AD 中設定的模式。 hello AssertionConsumerServiceURL hello SAML 要求中的值是您在 hello 錯誤中看到的 hello URL。

**解決方案**

請確定它的比對 hello 回覆 URL 值設定在 Azure AD 中的 hello SAML 要求中的 hello AssertionConsumerServiceURL 值。

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  跳過**網域和 Url** > 一節。 驗證或更新 hello 回覆 URL 文字方塊 toomatch hello AssertionConsumerServiceURL hello SAML 要求中的值中的 hello 值。  
    * 如果您沒有看到 hello 回覆 URL 文字方塊中，選取 hello**顯示進階的 URL 設定**核取方塊。

您已在 Azure AD 中更新 hello 回覆 URL 值，以及它有之後符合 hello 值 hello 應用程式以傳送 hello SAML 要求，您應該能夠 toosign toohello 應用程式中。

## <a name="user-not-assigned-a-role"></a>使用者未指派角色

*錯誤 AADSTS50105: hello 登入的使用者 'brian@contoso.com' 未指派 tooa hello 應用程式角色*。

**可能的原因**

hello 使用者未被授與存取 toohello 應用程式在 Azure AD 中。

**解決方案**

tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。

8.  按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。

9.  按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。

10. Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。

11. 將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。 按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。

12. **選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。

13. 當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。

14. **選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。

15. 按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。

一段短時間，您已選取的 hello 使用者是使用這些應用程式 hello hello 方案描述 部分中所述的方法可以 toolaunch。

## <a name="not-a-valid-saml-request"></a>非有效的 SAML 要求

*錯誤 AADSTS75005: hello 要求不是有效的 Saml2 通訊協定訊息。*

**可能的原因**

Azure AD 不支援 SAML 要求 hello 進行單一登入的應用程式所傳送的 hello。 以下為一些常見問題：

-   遺漏 hello SAML 要求中的必要的欄位

-   SAML 要求編碼方法

**解決方案**

1.  擷取 SAML 要求。 請遵循 hello 教學課程[如何 toodebug SAML 型單一登入 tooapplications 在 Azure AD 中](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)toolearn toocapture hello SAML 要求的方式。

2.  請連絡 hello 應用程式廠商及共用：

   -   SAML 要求

   -   [Azure AD 單一登入 SAML 通訊協定需求](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

它們應該先驗證它們的單一登入支援 hello Azure AD SAML 實作。

## <a name="no-resource-in-requiredresourceaccess-list"></a>requiredResourceAccess 清單中沒有資源

*錯誤 AADSTS65005:hello 用戶端應用程式已要求存取 tooresource ' 00000002-0000-0000-c000-000000000000'。此要求失敗，因為 hello 用戶端在其 requiredResourceAccess 清單中未指定此資源*。

**可能的原因**

hello 應用程式物件已損毀。

**解決方式：選項 1**

toosolve hello 問題，請新增 hello Azure AD 組態中的 hello 唯一的識別碼值。 tooadd 識別碼值，請遵循下列 hello 步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您已設定單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表

8.  在 hello**網域和 URL**區段中，檢查 hello**顯示進階的 URL 設定**。

9.  在 hello**識別碼**文字方塊中輸入 hello 應用程式的唯一識別碼。

10. **儲存**hello 組態。


**解決方式：選項 2**

如果選項 1，上方無效，請嘗試移除 hello 目錄中的 hello 應用程式。 接著，新增和重新設定 hello 應用程式，請遵循 hello 執行下列步驟：

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式

7.  按一下**刪除**hello 左上方的 hello 應用程式在**概觀**刀鋒視窗。

8.  重新整理 Azure AD，並從 hello Azure AD 圖庫新增 hello 應用程式。 然後，設定 hello 應用程式

<span id="_Hlk477190176" class="anchor"></span>之後重新設定 hello 應用程式，您應該能夠 toosign toohello 應用程式中。

## <a name="certificate-or-key-not-configured"></a>未設定憑證或金鑰

*錯誤 AADSTS50003︰未設定簽署金鑰。*

**可能的原因**

hello 應用程式物件已損毀，且 Azure AD 無法辨識 hello hello 應用程式設定的憑證。

**解決方案**

toodelete 並建立新的憑證，請依照下列步驟執行 hello:

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

 * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  按一下**建立新憑證**下 hello **SAML 簽章憑證**> 一節。

9.  選取到期日。 然後按一下 [儲存] 。

10. 請檢查**啟用新的憑證**toooverride hello 作用中憑證。 然後，按一下 **儲存**在 hello hello 刀鋒視窗頂端，並接受 tooactivate hello 變換憑證。

11. 在 hello **SAML 簽章憑證**區段中，按一下**移除**tooremove hello**未使用**憑證。

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a>自訂 hello SAML 宣告時的問題傳送 tooan 應用程式

toolearn 如何 toocustomize hello SAML 屬性宣告傳送 tooyour 應用程式，請參閱[宣告 Azure Active Directory 中的對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)如需詳細資訊。

## <a name="next-steps"></a>後續步驟
[如何 toodebug SAML 型單一登入 tooapplications 在 Azure AD 中](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
