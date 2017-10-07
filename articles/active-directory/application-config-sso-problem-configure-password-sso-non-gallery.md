---
title: "設定密碼單一登入非組件庫的應用程式的 aaaProblem |Microsoft 文件"
description: "在 hello Azure AD 應用程式庫中設定密碼單一登入的未列出的自訂非組件庫應用程式時，了解 hello 一般問題的人臉"
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a>為不在資源庫內的應用程式設定密碼單一登入時遇到的問題

本文協助您 toounderstand hello 一般問題的人臉設定時**密碼單一登入**與非組件庫的應用程式。

## <a name="how-toocapture-sign-in-fields-for-an-application"></a>Toocapture 登入欄位如何為應用程式

只有具備 HTML 功能的登入頁面支援登入欄位擷取，而**非標準的登入頁面並不支援**，例如，使用快閃記憶體或其他不具備 HTML 功能技術的頁面。

有兩種方式可讓您用來擷取自訂應用程式的登入欄位：

-   自動登入欄位擷取

-   手動登入欄位擷取

**自動登入欄位擷取**適用於大部分 HTML 啟用登入頁面，如果他們使用**已知 DIV 識別碼 hello 使用者名稱和密碼輸入**欄位。 hello 這個運作的方式是透過抓取 hello HTML hello 頁面 toofind DIV 識別碼符合特定準則的上，然後儲存此應用程式的中繼資料，因此我們可以稍後重新執行密碼 tooit。

**手動登入欄位擷取**可用在 hello 應用程式的 hello 案例**供應商並未標示**hello 輸入用來登入的欄位。 手動登入欄位擷取也可用在 hello 情況下，如果 hello**廠商呈現多個欄位**無法自動偵測。 Azure AD 可以儲存資料所多少個欄位上 hello 登入頁面上，只要您告訴我們，這些欄位位於 hello 頁面。

一般情況下，**如果自動登入欄位擷取無法運作，我們建議嘗試 hello 手動選項。**

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a>Tooautomatically 如何擷取登入應用程式的欄位

tooconfigure**密碼型單一登入**應用程式使用**自動登入欄位擷取**，依照下列步驟執行 hello:

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

  * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  選取 hello 模式**密碼式登入。**

9.  輸入 hello**登入 URL**。 這是讓使用者輸入其使用者名稱和密碼 toosign 中的以 hello URL。 **確認 hello 登入欄位是否顯示在您提供的 hello URL**。

10. 按一下 hello**儲存** 按鈕。

11. 一旦您這樣做，我們會自動將消除該 URL 的使用者名稱和密碼輸入方塊，並且可讓您 toouse Azure AD toosecurely 傳輸密碼 toothat 應用程式使用 hello 存取面板瀏覽器延伸模組。

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a>Toomanually 如何擷取登入應用程式的欄位

toomanually 擷取登入欄位，您必須先安裝 hello 存取面板瀏覽器延伸模組和**inPrivate、 incognito，或私用模式中不在執行。** tooinstall hello 瀏覽器延伸模組，後續的 hello 步驟在 hello [tooinstall hello 存取面板瀏覽器延伸模組的方式](#i-cannot-manually-detect-sign-in-fields-for-my-application)> 一節。

tooconfigure**密碼型單一登入**應用程式使用**手動登入欄位擷取**，依照下列步驟執行 hello:

1.  開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**

2.  開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。

3.  在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。

4.  按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。

5.  按一下**所有應用程式**tooview 所有應用程式的清單。

   * 如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**

6.  選取您想 tooconfigure 單一登入的 hello 應用程式。

7.  一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。

8.  選取 hello 模式**密碼式登入。**

9.  輸入 hello**登入 URL**。 這是讓使用者輸入其使用者名稱和密碼 toosign 中的以 hello URL。 **確認 hello 登入欄位是否顯示在您提供的 hello URL**。

10. 按一下 hello**儲存** 按鈕。

11. 一旦您這樣做，我們會自動將消除該 URL 的使用者名稱和密碼輸入方塊，並且可讓您 toouse Azure AD toosecurely 傳輸密碼 toothat 應用程式使用 hello 存取面板瀏覽器延伸模組。 您可以在 hello 失敗的情況下，**異動 hello 登入模式 toouse 手動登入欄位擷取**繼續 toostep 12。

12. 按一下 [設定 &lt;appname&gt; 密碼單一登入設定]。

13. 選取 hello**手動偵測登入欄位**組態選項。

14. 按一下 [確定] 。

15. 按一下 [儲存] 。

16. 依照畫面指示 toouse hello 存取面板中的 hello。

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a>我看到「在該 URL 找不到任何登入欄位」的錯誤

當自動偵測登入欄位失敗時，您就會看到此錯誤。 此問題，請嘗試手動登入欄位偵測所遵循的 hello 步驟 hello tooresolve [toomanually 如何擷取應用程式的登入欄位](#how-to-manually-capture-sign-in-fields-for-an-application)> 一節。

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a>我看到 「 無法 toosave 單一登入設定 」 錯誤

在某些罕見的情況下，更新 hello 單一登入組態可能會失敗。 tooresolve 這重試儲存 hello 單一登入組態一次。

如果此問題持續 toofail 一致的方式，提交支援案例，並提供 hello 蒐集在 hello[如何 toosee hello 詳細資料的入口網站的通知](#i-cannot-manually-detect-sign-in-fields-for-my-application)和[tooget 如何藉由傳送通知的詳細資料 tooa 協助支援工程師](#how-to-get-help-by-sending-notification-details-to-a-support-engineer)區段。

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a>我無法手動偵測應用程式的登入欄位

手動偵測為不使用時，您可能會看到 hello 行為的部分包括：

-   hello 手動擷取程序 toowork，但未正確擷取 hello 欄位

-   hello 右側欄位未取得反白顯示執行 hello 擷取程序時

-   hello 擷取程序接受我 toohello 應用程式的登入頁面如預期般，但會發生任何事

-   手動擷取出現 toowork，但我的使用者瀏覽 toohello hello 存取面板應用程式時，不會發生 SSO。

如果您遇到任何問題，請檢查下列 hello:

-   確定您已擁有 hello hello 存取面板瀏覽器延伸模組最新版本**安裝**和**啟用**hello 中的 hello 步驟[tooinstall 如何 hello 存取面板瀏覽器延伸模組](#how-to-install-the-access-panel-browser-extension)> 一節。

-   請確定您未在您的瀏覽器中時嘗試 hello 擷取處理序**incognito、 inPrivate，或私用模式**。 hello 存取面板延伸模組不支援這些模式中。

-   請確定您的使用者沒有 toosign toohello hello 存取面板時在應用程式**incognito、 inPrivate，或私用模式**。 hello 存取面板延伸模組不支援這些模式中。

-   再試一次 hello 手動擷取程序，確保 hello 紅色標記透過 hello 正確的欄位。

-   Hello 手動擷取程序看起來 toohang，則不會執行 hello 登入頁面上的任何項目 （情況 3 以上），hello 手動擷取處理序再試一次。 但是，此時間之後完成 hello 程序，請按 hello **F12**按鈕 tooopen 瀏覽器的開發人員主控台。 一次，開啟 hello**主控台**和型別**window.location="&lt;輸入設定 hello 應用程式時，您指定的 url 中的 hello 登&gt;"** ，然後按**輸入**。 此強制頁面重新導向的結束 hello 擷取程序，並儲存已擷取的 hello 欄位。

如果這其中沒有任何一種方式適合您，我們很樂意提供協助。 Hello 詳細資料，來嘗試什麼方法，以及所蒐集 hello 中的 hello 資訊提交支援案例[如何 toosee hello 詳細資料的入口網站的通知](#i-cannot-manually-detect-sign-in-fields-for-my-application)和[tooget 如何協助 tooa 支援傳送通知的詳細資料工程](#how-to-get-help-by-sending-notification-details-to-a-support-engineer)區段 （如果適用）。

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>如何 tooinstall hello 存取面板瀏覽器延伸模組

tooinstall hello 存取面板瀏覽器延伸模組，請遵循下列 hello 步驟：

1.  開啟 hello[存取面板](https://myapps.microsoft.com)其中一種支援的 hello 瀏覽器和登入為**使用者**Azure AD 中。

2.  按一下**password SSO 應用程式**hello 存取面板中。

3.  在 hello 提示詢問 tooinstall hello 軟體，選取 **立即安裝**。

4.  根據您的瀏覽器就導向的 toohello 下載連結。 **新增**hello 延伸 tooyour 瀏覽器。

5.  如果您的瀏覽器要求，請選取 tooeither**啟用**或**允許**hello 延伸模組。

6.  安裝之後，**重新啟動**瀏覽器工作階段。

7.  到 hello 存取面板登入，請參閱 < 是否您可以**啟動**password SSO 應用程式。

您可能也 hello 從下載擴充功能的 Chrome 和 Firefox hello 以下的直接連結：

-   [Chrome 存取面板延伸模組](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Firefox 存取面板延伸模組](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>如何 toosee hello 詳細資料的入口網站的通知

您可以依照以下 hello 步驟看到 hello 詳細資料的任何入口網站的通知：

1.  按一下 hello**通知**hello Azure 入口網站的 hello 右上角的圖示 （hello 鈴聲）

2.  選取中的任何通知**錯誤**狀態 （紅色 （！） 的 下一步 toothem 與那些）。

  >!NOTE] 您無法按一下處於**成功**或**進行中**狀態的通知。
  >
  >

3.  這個開啟 hello**通知的詳細資料**刀鋒視窗。

4.  使用此資訊自行 toounderstand 更多有關 hello 問題詳細資料。

5.  如果您仍需要協助，您也可以與您的問題共用與支援工程師或 hello 產品群組 tooget 說明這項資訊。

6.  按一下 hello**複製****圖示**方 hello toohello**複製錯誤**所有文字方塊 toocopy 都 hello 通知詳細資料 tooshare 與支援或產品的群組工程師。

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>藉由傳送通知的詳細資料 tooa 支援工程師 tooget 的說明

它是非常重要，共用**所有 hello 下面所列的詳細資料**支援工程師，如果您需要協助，以便它們可以協助您快速。 您可以輕鬆**擷取螢幕畫面，**或按一下 hello**複製錯誤圖示**，找到 toohello 右邊 hello**複製錯誤**文字方塊。

## <a name="notification-details-explained"></a>說明通知詳細資料

hello 以下說明更每一項 hello 通知項目表示，以及每個提供範例。

### <a name="essential-notification-items"></a>必要通知項目

-   **標題**– hello hello 通知的描述性標題

    -   範例 - **應用程式 Proxy 設定**

-   **描述**– hello 所發生的 hello 運算結果的描述

    -   範例 - **輸入的內部 URL 正由另一個應用程式使用中**

-   **通知識別碼**– hello 的 hello 通知的唯一識別碼

    -   範例 - **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **用戶端要求 Id** – 您的瀏覽器所做的 hello 特定要求識別碼

    -   範例 - **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **時間戳記 UTC** – hello 期間 hello 通知發生，以 UTC 時間戳記

    -   範例 - **2017-03-23T19:50:43.7583681Z**

-   **內部交易識別碼**– hello 我們可能佔用 toolook hello 錯誤，我們系統中的內部識別碼

    -   範例 - **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – 執行 hello 作業的 hello 使用者

    -   範例 - **tperkins@f128.info**

-   **租用戶識別碼**– hello 唯一 hello 租用戶識別碼 hello 使用者執行 hello 作業人員是的成員

    -   範例 - **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **使用者物件識別碼**– hello 執行 hello 作業的 hello 使用者的唯一識別碼

    -   範例 - **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>詳細通知項目

-   **顯示名稱**– **（可以是空的）** hello 錯誤的更詳細的顯示名稱

    -   範例 *- **應用程式 Proxy 設定**

-   **狀態**– hello hello 通知的特定狀態

    -   範例 *- **失敗**

-   **物件識別碼**– **（可以是空的）** hello 的 hello 針對已執行作業的物件識別碼

    -   範例 - **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **詳細資料**– hello 的詳細描述所發生的 hello 運算結果

    -   範例 - **內部 url 'http://bing.com/' 無效，因為已在使用中**

-   **複製錯誤**– 按一下 hello**複製圖示**方 hello toohello**複製錯誤**所有文字方塊 toocopy 都 hello 與支援或產品的群組工程師通知詳細資料 tooshare

    -   範例 - ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>後續步驟
[提供單一登入 tooyour 應用程式與應用程式 Proxy](active-directory-application-proxy-sso-using-kcd.md)

