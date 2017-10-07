---
title: "aaaAzure Active Directory 混合式身分識別設計考量的概觀 |Microsoft 文件"
description: "混合式身分識別設計考量指南的概觀和內容對應"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 100509c4-0b83-4207-90c8-549ba8372cf7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 10aacb04c90abd100eb56d7c44d590946b052f18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations"></a>Azure Active Directory 混合式身分識別設計考量
取用者為基礎的裝置是種 hello 公司世界中，並以雲端為基礎的軟體做為服務 (SaaS) 應用程式是簡易 tooadopt。 因此，要持續掌控使用者在內部資料中心與雲端平台間的應用程式存取，是很不容易的。  

Microsoft 的身分識別解決方案跨越內部部署和雲端架構的功能，建立單一使用者識別進行驗證和授權 tooall 資源，不論位置為何。 我們稱之為混合式身分識別。 有不同的設計與使用 Microsoft 解決方案的混合式身分識別的設定選項，而且在某些情況下可能很難 toodetermine 哪些組合最符合您組織的 hello 需求。 

此混合式身分識別設計考量指南將協助您 toounderstand toodesign 混合式身分識別解決方案最適合 hello 的商務和技術為您的組織需要的方式。  本指南詳細說明一系列步驟和工作，您可以依照 toohelp 您設計符合組織的獨特需求的混合式身分識別解決方案。 Hello 步驟和工作，hello 指南將在 hello 相關技術和功能選項可用 tooorganizations toomeet 功能與服務品質 （例如可用性、 延展性、 效能、 管理及安全性）層級的需求。 

具體來說，hello 混合式身分識別設計考量指南的目標是 tooanswer hello 下列問題： 

* 問題該怎麼我需要 tooask 並回答 toodrive 的混合式身分識別特定設計技術或問題領域最符合我的需求？
* 哪些系列活動應該完成 toodesign hello 技術或問題領域的混合式身分識別解決方案？ 
* 混合式身分識別技術和組態選項是否可用 toohelp 我滿足我的需求？ 什麼是 hello 之間的利弊得失這些選項，讓我可以選取企業 hello 最佳選項？

## <a name="who-is-this-guide-intended-for"></a>本指南的適用對象為何？
 負責為中型或大型組織設計混合式身分識別解決方案的 CIO、CITO、首席身分識別架構設計人員、企業架構設計人員和 IT 架構設計人員。

## <a name="how-can-this-guide-help-you"></a>本指南對您有何幫助？
您可以使用此指南 toounderstand toodesign 無法 toointegrate 雲端的混合式身分識別解決方案以使用您目前的身分識別管理系統的基礎內部部署身分識別解決方案。 

hello 下列圖形顯示的範例，可讓 IT 系統管理員 toomanage toointegrate 其目前 Windows Server Active Directory 方案位於內部部署與 Microsoft Azure Active Directory tooenable 使用者 toouse 單一混合式身分識別解決方案登入 (SSO) 位於 hello 雲端和內部部署的應用程式。

![](./media/hybrid-id-design-considerations/hybridID-example.png)

以上圖中的 hello 是運用雲端的混合式身分識別解決方案的範例服務 toointegrate tooprovide 順序中的內部部署功能，單一體驗 toohello 終端使用者驗證程序和 toofacilitate IT 管理這些資源。 雖然這可能是很常見的案例，每個組織的混合式身分識別設計是可能 toobe 不同 hello 範例因為 toodifferent 需求中圖 1 所述。 

本指南提供一系列步驟和工作，您可以依照 toodesign 符合貴組織的獨特需求的混合式身分識別解決方案。 整個 hello 下列步驟和工作、 hello 指南顯示 hello 相關技術和功能 選項為您的組織的可用 tooyou toomeet 功能和服務品質等級需求。

**假設**：您有 Windows Server、Active Directory 網域服務與 Azure Active Directory 的相關經驗。 在本文件中，我們假設您想要了解這些解決方案本身或在整合式解決方案中如何滿足您的商務需求。

## <a name="design-considerations-overview"></a>設計考量概觀
本文件提供一組步驟和工作，您可以依照 toodesign 最符合您需求的混合式身分識別解決方案。 hello 步驟會呈現在排序順序相同。 您在稍後步驟中學習的設計考量可能需要您 toochange 您所做的決定在先前步驟中，不過，由於 tooconflicting 設計選擇。 每個嘗試 tooalert 您 toopotential 設計衝突 hello 文件。 

Hello 設計最符合您的需求逐一執行多次，必要 tooincorporate hello 步驟之後，才會獲得所有 hello 文件中的 hello 考量。 

| 混合式身分識別階段 | 主題清單 |
| --- | --- |
| 判斷身分識別需求 |[判斷商務需求](active-directory-hybrid-identity-design-considerations-business-needs.md)<br> [判斷目錄同步處理需求](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)<br> [判斷多重要素驗證需求](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)<br> [定義混合式身分識別採用策略](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md) |
| 透過增強式身分識別解決方案規劃更高的資料安全性 |[判斷資料保護需求](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md) <br> [判斷內容管理需求](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)<br> [判斷存取控制需求](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)<br> [判斷事件因應需求](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) <br> [定義資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) |
| 規劃混合式身分識別生命週期 |[判斷混合式身分識別管理工作](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) <br> [同步處理管理](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)<br> [判斷混合式身分識別管理採用策略](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md) |

## <a name="download-this-guide"></a>下載此指南
您可以從 hello 下載 hello 混合式身分識別設計考量指南的 pdf 版本[Technet 資源庫](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288)。 

