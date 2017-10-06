---
title: "aaaAzure Active Directory 混合式身分識別設計考量-決定身分識別需求 |Microsoft 文件"
description: "識別導致 hello 混合式身分識別設計 toodefine hello 需求的 hello 公司的商務需求。"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: b2f1cad923b0f08ededa0d8f9a4ea8e799956e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a>判斷混合式身分識別解決方案的身分識別需求
hello 設計的混合式身分識別解決方案的第一個步驟是充分利用此解決方案的 hello 商業組織 toodetermine hello 需求。  混合式身分識別 （它支援所有其他雲端方案提供驗證） 支援角色會啟動，且會在解除鎖定使用者新的工作負載的 tooprovide 新的實用功能。  這些工作負載或服務，您會希望 tooadopt 為您的使用者會指定 hello 混合式身分識別設計的 hello 需求。  這些服務和工作負載需要 tooleverage 混合式身分識別這兩個內部部署和 hello 雲端中。  

您需要 toogo 比 hello 商務 toounderstand 的重要層面，什麼是現在的需求，以及哪些 hello 公司計劃 hello 未來。 如果您沒有混合式身分識別設計的 hello 的長期策略 hello 可見性，有可能會是，您的方案將不會擴充在 hello 的商務需求成長及變更。   他圖表所示的混合式身分識別架構和 hello 的工作負載針對使用者正在取消鎖定範例 T。 這只是範例的所有 hello 新的可能性，可以解除鎖定，並使用純色的混合式身分識別的策略來傳遞。 

屬於 hello 混合式身分識別架構的部分元件![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)

## <a name="determine-business-needs"></a>判斷商務需求
每一家公司會有不同需求，即使這些公司屬於 hello 相同的業界 hello 真正的業務需求可能都不同。 您仍然可以利用從 hello 業界的最佳作法，但最終仍是導致 hello 混合式身分識別設計 toodefine hello 需求的 hello 公司的商務需求。 

請確定 tooanswer hello 下列問題 tooidentify 業務需要：

* 您的公司正在尋找 toocut IT 作業成本？
* 您的公司正在尋找 toosecure 雲端資產 （[基礎結構中的 [SaaS 應用程式）？
* 為您的公司正在尋找 toomodernize 您的 IT 嗎？
  * 是您的使用者更多行動裝置版和嚴苛 IT toocreate 例外狀況成您 DMZ tooallow 不同類型的流量 tooaccess 不同的資源嗎？
  * 您的公司是否有舊版的應用程式需要發行 toobe toothese 現代使用者不容易 toorewrite？
  * 您的公司需要 tooaccomplish 所有這些工作並使其在 hello 控制相同的時間？
* 是您的公司尋找 toosecure 使用者的身分識別，並使新的工具，可利用 Microsoft Azure 安全性專業知識在內部部署的 hello 專業知識，就能降低風險？
* 嘗試移除 hello tooget 貴公司可怕的 「 外部 」 的帳戶，在內部部署及是將它們移 toohello 它們的位置不再休眠的潛在威脅，在內部部署環境內的雲端？

## <a name="analyze-on-premises-identity-infrastructure"></a>分析內部部署身分識別基礎結構
既然您已了解有關您公司的商務需求時，您需要 tooevaluate 您在內部部署身分識別基礎結構。 這項評估是重要的定義 hello 技術需求 toointegrate 目前身分識別解決方案 toohello 雲端身分識別管理系統。 請確定 tooanswer hello 下列問題：

* 您的公司在內部部署中使用何種驗證和授權解決方案？ 
* 您的公司目前有任何內部部署同步處理服務嗎？
* 您的貴公司是否使用任何協力廠商身分識別提供者 (IdP)？

您也需要 toobe 知道您的公司可能會有的 hello 雲端服務。 執行評定 toounderstand hello 目前與整合 SaaS，您的環境中的 IaaS 或 PaaS 模型是非常重要。 請確定 tooanswer hello 遵循這項評估期間的問題：

* 貴公司是否與任何雲端服務提供者整合？
* 如果是，請問使用了哪些服務？
* 這項整合目前已投入使用，或只是一項試驗？

> [!NOTE]
> 如果您不要讓具有正確對應的所有應用程式和雲端服務，您可以使用 hello Cloud App Discovery 工具。 這項工具可讓您的 IT 部門深入了解組織的所有商業和取用者雲端應用程式。 它較容易曾經 toodiscover 陰影 IT 組織中包括使用模式與任何使用者存取您的雲端應用程式的詳細資訊。 請參閱 tooget 啟動[Cloud app discovery](active-directory-cloudappdiscovery-whatis.md)。
> 
> 

## <a name="evaluate-identity-integration-requirements"></a>評估身分識別整合需求
接下來，您需要 tooevaluate hello 身分識別整合需求。 這項評估是使用者驗證的方式、 hello 的組織存在 hello 雲端中所呈現的樣子，hello 組織可讓授權的方式和哪些 hello 使用者體驗是進行 toobe 的重要 toodefine hello 技術需求。 請確定 tooanswer hello 下列問題：

* 您的組織是否會使用同盟和 (或) 標準驗證？
* 同盟是必要條件嗎？  因為 hello 下列內容：
  * Kerberos 型 SSO
  * 您的公司有使用 SAML 或類似同盟功能的內部部署應用程式 (內建或協力廠商)。
  * 透過智慧卡的 MFA。 RSA SecurID 等等。
  * 用戶端存取規則解決 hello 回答以下問題：
    1. 我可以封鎖所有外部存取 tooOffice 365 根據 hello hello 用戶端的 IP 位址嗎？
    2. 我可以封鎖所有外部存取 tooOffice 365、 Exchange ActiveSync 以外嗎？
    3. 我可以封鎖所有外部存取 tooOffice 365，除了瀏覽器型應用程式 （OWA、 SPO） 嗎
    4. 可以封鎖所有外部存取 tooOffice 365 指定之 AD 群組的成員嗎
* 安全性/稽核考量
* 對同盟驗證既有的投資
* 名稱將我們的組織使用我們 hello 雲端中的網域？
* Hello 的組織是否有自訂網域？
  1. 該網域是否為公用的？可透過 DNS 輕易驗證嗎？
  2. 如果不是，要再擁有公用網域，可以在 AD 中是使用的 tooregister 替代的 UPN 嗎？
* Hello 使用者識別碼都是一致的雲端表示法中使用？ 
* Hello 組織有需要與雲端服務整合的應用程式嗎？
* Hello 組織是否有多個網域，並將它們都會使用標準或同盟驗證？

## <a name="evaluate-applications-that-run-in-your-environment"></a>評估在您的環境中執行的應用程式
既然您已了解有關在內部和雲端基礎結構，您需要在這些環境中執行的 tooevaluate hello 應用程式。 這項評估是重要 toodefine hello 技術需求 toointegrate 這些應用程式 toohello 雲端身分識別管理系統。 請確定 tooanswer hello 下列問題：

* 我們的應用程式將在何處運作？
* 使用者會存取內部部署應用程式嗎？  在 [hello 雲端？ 或是兩者都有？
* 是否有計畫 tootake hello 現有應用程式工作負載，並將它們移 toohello 雲端？
* 有計劃將位於內部或在 hello 雲端的 toodevelop 新應用程式會使用雲端驗證嗎？

## <a name="evaluate-user-requirements"></a>評估使用者需求
您也可以 tooevaluate hello 使用者需求。 這項評估是在需要加入及協助使用者，因為這些轉換 toohello 雲端的重要 toodefine hello 步驟。 請確定 tooanswer hello 下列問題：

* 使用者會存取應用程式內部部署嗎？
* 使用者將用來存取 hello 雲端中的應用程式嗎？
* 如何執行使用者通常登入 tootheir 內部部署環境嗎？
* 如何將雲端使用者登入 toohello？

> [!NOTE]
> 請確定每個答案 tootake 附註，並了解 hello 回應 hello 背後的基本原理。 [判斷事件回應需求](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)將介紹可用選項 hello 和專業人員/優缺點的每個選項。  回答這些問題之後，您就能選取最適合業務需求的選項。
> 
> 

## <a name="next-steps"></a>後續步驟
[判斷目錄同步處理需求](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a>另請參閱
[設計考量概觀](active-directory-hybrid-identity-design-considerations-overview.md)

