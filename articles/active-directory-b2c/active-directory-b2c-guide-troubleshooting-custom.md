---
title: "Azure Active Directory B2C：針對自訂原則進行疑難排解 | Microsoft Docs"
description: "了解方法 toosolving 錯誤時使用的 Azure Active Directory 中的自訂原則。"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: b9e1b46df1ddb29cdb90953e4a0d6f1dd085441f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a>針對 Azure AD B2C 自訂原則和身分識別體驗架構進行疑難排解

如果您使用 Azure Active Directory B2C (Azure AD B2C) 的自訂原則，您可能會遇到設定 hello 身分識別遇到架構原則語言 XML 格式的挑戰。  學習 toowrite 自訂原則可以如同學習新的語言。 在本文中，我們將說明可協助您快速找出並解決問題的工具和提示。 

> [!NOTE]
> 本文著重在針對 Azure AD B2C 自訂原則設定進行疑難排解。 它不能處理 hello 信賴憑證者的合作對象應用程式或其身分識別文件庫。

## <a name="xml-editing"></a>XML 編輯

hello 最常見的錯誤，在將自訂原則設定不正確格式化 XML。 良好的 XML 編輯器幾乎不可或缺。 良好的 XML 編輯器會顯示 XML 原貌、為內容加上色彩、預先填入常用字詞、保持編製 XML 元素的索引，而且可以根據結構描述進行驗證。 以下是我們最喜愛的兩個 XML 編輯器：

* [Visual Studio Code](https://code.visualstudio.com/)
* [Notepad++](https://notepad-plus-plus.org/)

在您上傳 XML 檔案之前，XML 結構描述驗證會識別錯誤。 在 hello 根資料夾中的 hello 入門套件，取得 TrustFrameworkPolicy_0.3.0.0.xsd hello XML 結構描述定義。 如需詳細資訊，請在 hello 文件的 XML 編輯器中，請尋找*XML 工具*和*XML 驗證*。

您可能會發現檢閱 XML 規則很有幫助。 Azure AD B2C 會拒絕它所偵測到的任何 XML 格式錯誤。 格式錯誤的 XML 有時可能會產生令人誤解的錯誤訊息。

## <a name="upload-policies-and-policy-validation"></a>上傳原則和原則驗證

 XML 檔案上傳驗證是自動執行。 大部分的錯誤會造成 hello 上載 toofail。 驗證包含您要上傳的 hello 原則檔案。 它也包含 hello 鏈結的 hello 上傳檔案太參照的檔案 (hello 信賴憑證者的合作對象原則檔、 hello 擴充功能檔案與 hello 基底檔案)。 
 
 常見的驗證錯誤 hello 如下。

錯誤程式碼片段︰`... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`
* hello ClaimType 值可能拼錯，或者不存在於 hello 結構描述。
* ClaimType 值必須定義至少一個 hello hello 原則中的檔案。 
    例如：` <ClaimType Id="socialIdpUserId">`
* 如果 ClaimType 定義在 hello 延伸模組檔案中，但它也會用於 TechnicalProfile 值 hello 基底檔案中上, 傳 hello 基底檔案會導致錯誤。

錯誤程式碼片段︰`...makes a reference tooa ClaimsTransformation with id...`
* 針對 hello 錯誤可能是 hello 相同 hello ClaimType 錯誤與 hello 原因。

錯誤程式碼片段︰`Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`
* 請檢查該 hello hello 中的 TenantId 值 **\<TrustFrameworkPolicy\>** 和 **\<BasePolicy\>** 項目符合目標 Azure AD B2C租用戶。  

## <a name="troubleshoot-hello-runtime"></a>疑難排解 hello 執行階段

* 使用`Run Now`和`https://jwt.io`tootest 您獨立於您的 web 或行動應用程式的原則。 此網站的作用就像信賴憑證者應用程式。 它會顯示 hello JSON Web Token (JWT) 所產生的 Azure AD B2C 原則 hello 內容。 toocreate 測試應用程式在識別經驗 Framework 中，使用 hello 下列值：
    * 名稱︰TestApp
    * Web 應用程式/Web API：無
    * 原生用戶端︰否

* tootrace hello 之間交換訊息的用戶端瀏覽器及 Azure AD B2C 使用[Fiddler](http://www.telerik.com/fiddler)。 它可協助您了解使用者旅程圖在協調流程步驟中的何處失敗。

* 在**開發模式**，使用**Application Insights** tootrace hello 活動的身分識別體驗架構的使用者之旅。 在**開發模式**，您可以觀察 hello 交換 hello 身分識別體驗架構之間的宣告和 hello 各種宣告提供者所定義的技術的設定檔，例如身分識別提供者，應用程式開發介面為基礎的服務，hello Azure AD B2C 使用者目錄中及其他服務，例如 Azure 多 Multi-factor-authentication。  

## <a name="recommended-practices"></a>建議的做法

**為您的情節保留多個版本。將它們和您的應用程式一起放在一個專案中。** hello 基底、 延伸與信賴憑證者的合作對象檔案會直接相互依存性。 將它們儲存成一個群組。 當新功能加入 tooyour 原則時，保留不同工作版本。 階段自己的工作版本檔案系統與 hello 與他們互動的應用程式程式碼。  您的應用程式可能會在一個租用戶中叫用許多不同的信賴憑證者原則。 它們可能會變成預期從您的 Azure AD B2C 原則的 hello 宣告而定。

**使用已知的使用者旅程圖來開發和測試技術設定檔。** 使用已測試的入門套件原則 tooset 設定您的技術檔。 將它們併入您自己的使用者旅程圖之前，先個別進行測試。

**使用已測試的技術設定檔來開發和測試使用者旅程圖。** 以累加方式變更使用者之旅 hello 協調流程的步驟。 漸進地建置您想要的情節。

## <a name="next-steps"></a>後續步驟

* 在 GitHub 中下載 hello [active-directory-b2c-custom-policy-starterpack] (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip).zip 檔案。
