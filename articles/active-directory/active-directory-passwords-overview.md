---
title: "aaaAzure AD 自助式密碼重設概觀 |Microsoft 文件"
description: "Azure AD 中的自助式密碼重設可為您的組織做些什麼？"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 0efc291b1eeec0b7ae33ff5a7d9ed38e70c8be6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-self-service-password-reset-for-hello-it-professional"></a>Azure AD 自助式密碼重設 hello IT 專業人員

「 自助 」 是 buzzword 內擲回周圍許多 IT 部門跨 hello world 及不同的意義。 hello 市場是大量湧入 toomanage 內部群組、 密碼或從 hello 雲端或內部部署使用者設定檔可讓您的產品。

Azure Active Directory (Azure AD) 自助式密碼重設 (SSPR) 以容易使用和部署突顯本身的特色。 Azure AD 自助式密碼重設結合了一組功能︰

* 讓使用者 toomanage 他們自己的密碼
  * 從任何裝置
  * 在任何位置
  * 在任何時間
* 符合身為系統管理員的您所定義的原則規定

如果您已準備就緒，即可利用我們的[快速入門指引](active-directory-passwords-getting-started.md)開始使用 Azure AD SSPR，並且快速地讓使用者重設自己的密碼。

## <a name="what-is-possible"></a>可行功用

* **自助式密碼變更**可讓使用者或系統管理員 toochange 其密碼沒有系統管理員的協助
* **自助帳戶解除鎖定**他們自己的帳戶沒有系統管理員的協助可讓終端使用者 toounlock
* **自助式密碼重設**可讓使用者或系統管理員 tooreset 自動不需要系統管理員協助其密碼。 自助式密碼重設需要 Azure AD Premium 或 Basic - [Azure Active Directory 版本](active-directory-editions.md)。
* **系統管理員起始密碼重設**hello 從使用者或其他系統管理員密碼，可讓系統管理員 tooreset [Azure 入口網站](https://docs.microsoft.com/azure/azure-portal-overview)
* **密碼管理活動報告**讓系統管理員得以深入了解其組織內發生的密碼重設和註冊活動- [管理報告](active-directory-passwords-reporting.md)
* **密碼回寫**允許管理從 hello 雲端部署在內部部署密碼，因此所有 hello 都與先前案例可以執行，或是在 hello 代替，都同盟或密碼同步處理使用者。 如果要進行密碼回寫，就必須使用 [Azure AD Premium](active-directory-get-started-premium.md)。

## <a name="why-choose-azure-ad-self-service-password-reset"></a>為何選擇 Azure AD 自助式密碼重設

* **降低成本**，技術服務人員和支援輔助密碼重設通常佔 IT 組織費用的 20%
* **改善使用者體驗**和**降低技術服務人員磁碟區**，提供結束使用者 hello 電源 tooresolve 他們自己的密碼問題一次而不需呼叫服務台或開啟支援要求。
* **發揮行動力**因為使用者可隨時隨地重設密碼。

## <a name="azure-ad-self-service-password-reset-availability"></a>Azure AD 自助式密碼重設可用性

視您的訂用帳戶而定，Azure AD 自助式密碼重設會以 3 個層級提供。

* **Azure AD Free** – 僅限雲端的系統管理員可以重設自己的密碼
* **Azure AD Basic** 或任何**付費 Office 365 訂用帳戶** – 僅限雲端的使用者及僅限雲端的系統管理員可以重設自己的密碼
* **Azure AD Premium** – 任何使用者或系統管理員，包括僅限雲端、同盟或密碼同步使用者可以重設自己的密碼。 在內部部署密碼需要啟用密碼回寫 toobe。

## <a name="azure-ad-self-service-password-reset-a-sum-of-hello-parts"></a>Azure AD 自助式密碼重設的 hello 部分總和

自助式密碼重設 Azure AD 中是由下列元件的 hello 所組成：

* **密碼管理設定入口網站**其中您可以控制您的租用戶透過 hello Azure 入口網站中管理密碼方式的選項
* **密碼重設註冊入口網站**使用者可以在其中自行註冊密碼重設
* **密碼重設入口網站**提供其中使用者可以使用重設其密碼 hello 系統管理員所定義的 hello 挑戰和 hello 解答使用者
* **使用者密碼變更入口網站**，使用者可以在其中藉由輸入舊密碼並提供新密碼，以變更自己的密碼
* **密碼管理報表**其中系統管理員可以檢視和分析密碼活動報告為其租用戶中 hello Azure 入口網站
* **密碼回寫 tooon 內部使用 Azure AD Connect**允許您 tooenable 管理內部部署同盟，或密碼同步處理使用者從 hello 雲端

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a>Azure AD 價格、SLA、更新和藍圖

Hello 遵循頁面上可以找到詳細瞭解這些主題

* [**Azure AD 價格詳細資料**](https://azure.microsoft.com/pricing/details/active-directory/)
* [**Office 365 價格**](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [**Azure 服務等級協定**](https://azure.microsoft.com/support/legal/sla/)
* [**Microsoft Online Services 的服務等級協定**](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [**Azure 更新**](https://azure.microsoft.com/updates/)
* [**Azure 藍圖**](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a>後續步驟

hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊

* [**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理 
* [**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權
* [**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理
* [**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱
* [**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。
* [**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能
* [**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式
* [**常見問題集**](active-directory-passwords-faq.md) - 如何？ 原因為何？ 何事？ 何地？ 何人？ 何時？ -回答您總是想 tooask tooquestions
* [**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR

