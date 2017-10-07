---
title: "Azure Active Directory B2C：開發人員的自訂原則使用注意事項 | Microsoft Docs"
description: "開發人員在使用自訂原則來設定和維護 Azure AD B2C 時的注意事項"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a>Azure Active Directory B2C 自訂原則公開預覽版的版本資訊
hello 自訂原則的功能集現在已可供公開預覽版供所有的 Azure Active Directory B2C 下評估 (Azure AD B2C) 客戶。 此功能集為目標的進階身分識別開發人員在建置 hello 最複雜的身分識別解決方案。  

現在，此功能集需要開發人員 tooconfigure hello 身分識別體驗架構透過直接編輯的 XML 檔案。 用這種方式進行設定的效果最好，卻也複雜。 進階身分識別開發人員使用 hello 身分識別體驗架構應該規劃 tooinvest 一些時間完成逐步解說，以及讀取參考文件。 

## <a name="features-included-in-this-public-preview"></a>此公開預覽版包含的功能
Hello hello 公開預覽版中導入了新的功能，開發人員可以執行下列工作的 hello:<br>

* 使用自訂原則來撰寫和上傳自訂驗證使用者旅程。 
   * 逐步將使用者旅程描述為宣告提供者之間的交換。 
   * 定義使用者旅程中的條件式分支。 
* 將啟用 REST API 功能的服務整合到您的自訂驗證使用者旅程。  
* 加入與 hello OpenIDConnect 標準與相容的身分識別提供者同盟。 <br>
* 加入與遵守 toohello SAML 2.0 通訊協定的身分識別提供者同盟。 

## <a name="terms-of-hello-public-preview"></a>Hello 公用預覽中的條款

* 我們建議您僅為了評估目的 toouse hello 新功能。<br>
* 新功能不適合在生產環境中使用。<br>
* 服務等級協定 (Sla) 不會套用 toohello 新功能。 <br>
* 您可以透過標準支援管道來提出支援要求。 <br>
* 正式運作的日期還未確定。<br>
* 我們決定，以及因為任何原因，Microsoft 可以加上旗標和拒絕或限制案例和使用者皆超過 hello 範圍 hello Azure AD B2C 產品教授 tooserve 做為客戶識別和存取管理 (CIAM) 平台。

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a>自訂原則功能集開發人員的責任
手動原則設定會授與較低層級存取 toohello 基礎平台的 Azure AD B2C 加以 hello 建立唯一的、 可完全自訂信任架構。 可能的排列方式，自訂身分識別提供者，信任關係的外部服務，與逐步工作流程整合進階開發人員使用他們的 hello 置於更高的要求。

toofully 權益從 hello 公開預覽，我們建議開發人員的耗用 hello 自訂原則的功能集遵守 toohello 指導方針：
* 熟悉的 hello 識別經驗引擎 hello 設定語言和金鑰/密碼管理。
* 完整掌控案例和自訂整合。
* 有系統地執行案例測試。
* 對至少一個開發和測試環境以及一個生產環境遵循軟體開發和分段進行的最佳做法。
* 隨時掌握有關從 hello 身分識別提供者和服務整合與新的開發。 比方說，追蹤的機密資料中的排程和解除排程變更 toohello 服務的變更。
* 設定使用中的監視和監視的實際執行環境的 hello 回應性。
* 最新的連絡人電子郵件地址，並保持回應 toohello Microsoft live 網站小組電子郵件。
* 建議使用的 toodo 來 hello Microsoft live 網站小組時，請採取及時的動作。 


>[!NOTE]
>這些功能最終可能包含在 Azure AD 內建原則，使其更容易存取 tooall 開發人員。

## <a name="next-steps"></a>後續步驟
[開始使用自訂原則](active-directory-b2c-get-started-custom.md)。
