---
title: "aaaAzure Active Directory 混合式身分識別設計考量-判斷內容管理需求 |Microsoft 文件"
description: "深入瞭解如何 toodetermine hello 內容管理您的業務需求。 通常當使用者具有自己的裝置他可能的替代方式相應 toohello 使用應用程式，他也多個的認證。 它是重要的 toodifferentiate 內容使用個人的認證與 hello 使用公司認證所建立的項目所建立。 您的身分識別解決方案應該能夠與雲端服務 tooprovide toointeract 順暢的體驗 toohello 使用者，同時確保其隱私權和增加 hello 防止資料外洩。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a>判斷混合式身分識別解決方案的內容管理需求
了解 hello 內容管理的需求為您的企業可能會直接影響您決定哪一個混合式身分識別解決方案 toouse。 與請 hello 的多個裝置和使用者 toobring hello 功能自己的裝置 ([BYOD](http://aka.ms/byodcg))、 hello 公司必須保護它自己的資料，但它也必須保留使用者的隱私權。 通常當使用者具有自己的裝置他可能的替代方式相應 toohello 使用應用程式，他也多個的認證。 它是重要的 toodifferentiate 內容使用個人的認證與 hello 使用公司認證所建立的項目所建立。 您的身分識別解決方案應該能夠與雲端服務 tooprovide toointeract 順暢的體驗 toohello 使用者，同時確保其隱私權和增加 hello 防止資料外洩。 

身分識別解決方案會利用不同的技術控制項，在訂單 tooprovide 內容管理 hello 圖所示：

![](./media/hybrid-id-design-considerations/securitycontrols.png)

**充分運用身分識別管理系統的安全性控制項**

一般情況下，內容管理需求將會利用您的身分識別管理系統，在下列區域的 hello:

* 隱私權： 識別 hello 使用者擁有的資源，並套用 hello 適當的控制項 toomaintain 完整性。
* 資料分類： 識別 hello 使用者或群組以及根據分類 tooits 存取 tooan 物件層級。 
* 資料外洩防護： 負責保護資料 tooavoid 外洩的安全性控制項需要 toointeract 與 hello 身分識別系統 toovalidate hello 使用者的身分識別。 這對於稽核記錄用途也很重要。

> [!NOTE]
> 如需資料分類的最佳做法與指導方針，請參閱 [雲端整備的資料分類](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) 。
> 
> 

當您規劃混合式身分識別解決方案確定遵循該 hello 問題根據 tooyour 組織的需求：

* 您的公司有安全性控制項中的位置 tooenforce 資料隱私權？
  * 如果是，這些安全性控制項將會無法與 hello 混合式身分識別解決方案，而您會進入 tooadopt toointegrate 嗎？
* 貴公司是否使用資料分類？
  * 如果是，是否 hello 目前解決方案能夠 toointegrate 與 hello 混合式身分識別解決方案，而您會進入 tooadopt？
* 貴公司目前對於資料外洩有任何解決方案嗎？ 
  * 如果是，是否 hello 目前解決方案能夠 toointegrate 與 hello 混合式身分識別解決方案，而您會進入 tooadopt？
* 您的公司是否需要 tooaudit 存取 tooresources？
  * 如果是，是哪種類型的資源？
  * 如果是，需要哪一個資訊層級？
  * 如果是，其中必須位於 hello 稽核記錄？ 在內部部署或 hello 雲端中嗎？
* 您的公司需要 tooencrypt 包含敏感性資料 (SSNs、 信用卡號碼等) 的任何電子郵件嗎？
* 您的公司需要 tooencrypt 所有文件/內容與外部公司夥伴共用嗎？
* 您的公司是否需要 tooenforce 特定種類的電子郵件上的公司原則 （執行所有無回應，不會轉送）？

> [!NOTE]
> 請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。 [定義的資料保護策略](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)將介紹可用 hello 選項以及每個選項的優點/缺點。  回答這些問題之後，您就能選取最適合業務需求的選項。
> 
> 

## <a name="next-steps"></a>後續步驟
[判斷存取控制需求](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a>另請參閱
[設計考量概觀](active-directory-hybrid-identity-design-considerations-overview.md)

