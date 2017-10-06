---
title: "aaaSign 入活動報表中的錯誤碼 hello Azure Active Directory 入口網站 |Microsoft 文件"
description: "登入活動報告錯誤碼參考。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: a0ca5b706bfeb0c7ce669712468a083a394712b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-report-error-codes-in-hello-azure-active-directory-portal"></a>登入活動報表中的錯誤碼 hello Azure Active Directory 入口網站

Hello hello 使用者登入報表所提供的資訊，您可以找到解答 tooquestions，例如：

- 誰已使用 Azure Active Directory 登入？
- 已登入哪些應用程式？
- 哪些登入失敗，原因為何？

此主題列出 hello 錯誤代碼和 hello 相關的說明。 

## <a name="how-can-i-display-failed-sign-ins"></a>如何顯示失敗的登入？ 

第一個項目點 tooall 登入活動資料**[登入](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**在 hello**活動**區段**Azure Active**。


![登入活動](./media/active-directory-reporting-activity-sign-ins-errors/61.png "登入活動")


在登入報告中，您可以選取 [失敗] 作為 [登入狀態]，以顯示所有失敗的登入。


![登入活動](./media/active-directory-reporting-activity-sign-ins-errors/06.png "登入活動")

按一下即可顯示 hello 清單中的項目，開啟 hello**活動詳細資料： 登入**刀鋒視窗。 這個檢視可提供您所有 Azure Active Directory 追蹤有關登入，包括 hello hello 詳細資料**登入錯誤碼**和**失敗原因**。

![登入活動](./media/active-directory-reporting-activity-sign-ins-errors/05.png "登入活動")


做為替代 toousing hello Azure 入口網站 tooaccess hello 登入資料，您也可以使用 hello[報告 API](active-directory-reporting-api-getting-started-azure-portal.md)。


hello 下列章節提供您的所有可能的錯誤和 hello 的完整概觀與相關說明。 

## <a name="error-codes"></a>錯誤碼

| 錯誤| 說明 |
| --- | --- |
| 50001| 名為 Y 的 hello 租用戶中找不到名為 X hello 服務主體。這種情況 hello 應用程式尚未安裝的 hello hello 租用戶系統管理員。 或資源主體 hello 目錄中找不到或無效|
| 50008| SAML 判斷提示已遺失或 hello 權杖中的設定不正確。|
| 50011| hello 回覆地址遺漏、 設定不正確或不符合設定的 hello 應用程式的回覆位址。|
| 50053| 帳戶已鎖定，因為嘗試太多次使用不正確的使用者識別碼或密碼中 toosign 的使用者。|
| 50054| 使用舊密碼進行驗證。|
| 50055| 無效的密碼，或輸入的密碼過期。|
| 50057| 使用者帳戶已停用。|
| 50058| 提供給租用戶中未找到或使用者的認證或無訊息的登入要求已傳送但沒有使用者登入或服務是無法 tooauthenticate hello 使用者之間不找到使用者的身分識別的任何資訊。|
| 50074| 強式驗證 (第二個因素) 是必要的|
| 50079| 使用者需要 tooenroll 第二因素驗證|
| 50126| 使用者名稱、密碼無效，或內部部署使用者名稱或密碼無效。|
| 50131| 使用於各種條件式存取錯誤。 例如不正確的 Windows 裝置狀態時，它會要求封鎖，因為 toosuspicious 活動、 存取原則和安全性原則決策。|
| 50133| 工作階段到期 tooexpiration 或最近變更的密碼無效。|
| 50144| 使用者的 Active Directory 密碼已到期。|
| 65001| X 的應用程式沒有權限 tooaccess 應用程式 Y 或 hello 權限已被撤銷。 或 hello 使用者或系統管理員不同意 toouse hello 應用程式識別碼 x 傳送此使用者與資源的互動式授權要求。 Hello 使用者或系統管理員不同意 toouse hello 應用程式識別碼 x 傳送授權要求 tooyour 租用戶系統管理員 tooact 具有代表 hello 應用程式或者： 資源的 Y: Z。|
| 65005| hello 應用程式所需資源存取清單未包含 hello 資源可探索的應用程式或 hello 用戶端應用程式已要求存取 tooresource 其中並未指定於其所需的資源存取清單或 Graph 服務傳回不正確要求或找不到資源。|
| 70001| 名為 Y 的 hello 租用戶中找不到名為 X hello 應用程式。這可以發生如果 hello 應用程式尚未安裝的 hello hello 租用戶或已獲得同意的 tooby 的系統管理員 hello 租用戶中的任何使用者。 您可能會傳送驗證要求 toohello 錯誤租用戶。|
| 80001| 沒有可用的驗證代理程式。|
| 80002| 驗證代理程式的密碼驗證要求已逾時。|
| 80003| 驗證代理程式收到的回應無效。|
| 80004| 登入要求中使用的使用者主體名稱 (UPN) 不正確。|
| 80005| 驗證代理程式：發生錯誤。|
| 80007| 驗證代理程式無法 tooconnect tooActive 目錄。|
| 80010| 驗證代理程式無法 toodecrypt 密碼。|
| 81001| 使用者的 Kerberos 票證太大。|
| 81002| 無法 toovalidate 使用者的 Kerberos 票證。|
| 81003| 無法 toovalidate 使用者的 Kerberos 票證。|
| 81004| Kerberos 驗證嘗試失敗。|
| 81008| 無法 toovalidate 使用者的 Kerberos 票證。|
| 81009| 無法 toovalidate 使用者的 Kerberos 票證。|
| 81010| 無縫式 SSO 失敗，因為 hello 使用者的 Kerberos 票證已過期或無效。|
| 81011| 無法 toofind hello 使用者的 Kerberos 票證中的資訊為基礎的使用者物件。|
| 81012| 嘗試 toosign tooAzure AD 中的 hello 使用者所登入 hello 裝置 hello 使用者不同。|
| 81013| 無法 toofind hello 使用者的 Kerberos 票證中的資訊為基礎的使用者物件。|
| 90014| 預期的欄位不存在於 hello 認證時，在各種情況下使用。|
| 90093| 傳回錯誤碼禁止 hello 要求的圖形。|



## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 hello[登入活動報表 hello Azure Active Directory 入口網站中的](active-directory-reporting-activity-sign-ins.md)。

