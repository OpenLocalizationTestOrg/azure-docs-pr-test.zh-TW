---
title: "應用程式與 Azure Active Directory aaaManaging |Microsoft 文件"
description: "此文章 hello 的優點與您的內部部署、 雲端 SaaS 應用程式整合 Azure Active Directory。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 0016f8b433e101d8a150bc6d9be3931851578241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-applications-with-azure-active-directory"></a>使用 Azure Active Directory 來管理應用程式
超過 hello 實際工作流程或內容，企業會有兩個的所有應用程式的基本需求：

1. tooincrease 產能應用程式應該簡單 toodiscover 和存取
2. hello 組織 tooenable 安全性和控管，需要控制和監督者可以與實際存取每個應用程式

中的雲端應用程式最適合這可以使用身分識別 toocontrol hello world"*誰是允許 toodo 什麼*"。

在運算術語中：

* *誰*稱為*識別*-hello 管理使用者和群組
* *什麼*稱為*存取管理*– hello 存取 tooprotected 資源管理

這兩個元件統稱為*身分識別和存取管理 (IAM)*，定義由 hello [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam)群組做為"*hello 安全性專業領域，可讓 hello 權限個人 tooaccess hello 正確的資源在 hello 以滑鼠右鍵 hello 右基於時間*"。

好，那麼是什麼 hello 問題嗎？ 如果 IAM *未* 在一個地方使用整合解決方案加以管理：

* 身分識別系統管理員可以建立並分開，更新所有應用程式中的使用者帳戶的 tooindividually 多餘且耗時的活動。
* 使用者擁有 toomemorize 多個認證 tooaccess hello 應用程式需要與 toowork。 如此一來，使用者傾向 toowrite 向他們的密碼，或使用其他密碼管理解決方案造成其他資料安全性風險。
* 備援、 耗費時間的活動減少 hello 的使用者和系統管理員正在增加您的業務營收的商務活動。

因此，通常何者會防止組織採用整合式 IAM 解決方案？

* 最技術解決方案根據需要 toobe 部署，並由其自身應用程式的每個組織的軟體平台。
* 採用雲端應用程式通常會比 IT 組織可以與現有的 IAM 解決方案整合需要更高的費率。
* 安全性和監視工具需要額外的自訂及整合 tooachieve 完整 E2E 案例。

## <a name="azure-active-directory-integrated-with-applications"></a>與應用程式整合的 Azure Active Directory
Azure Active Directory 是 Microsoft 的全方位「身分識別即服務」(IDaaS) 解決方案，它能夠：

* 讓 IAM 做為雲端服務 
* 提供集中式存取管理、單一登入 (SSO) 及報告功能 
* 支援的整合式的存取管理[數千個應用程式](https://azure.microsoft.com/marketplace/active-directory/)在 hello 應用程式庫，包括 Salesforce、 Google Apps、 Box、 Concur、 和多個。 

與 Azure Active Directory，所有應用程式發行您的合作夥伴，且 （商務或取用者） 的客戶有 hello 相同的身分識別和存取管理功能。<br> 這樣做可讓您 toosignificantly 縮減營運成本。

如果您需要 tooimplement 還未列在 hello 應用程式庫的應用程式嗎？ 這是一個位元較費時，比從 hello 應用程式庫的應用程式設定 SSO，而 Azure AD 可讓您使用精靈，可協助您與 hello 組態。

Azure AD 的 hello 值超出 「 僅 」 雲端應用程式。 您也可以透過提供安全的遠端存取，將它與內部部署應用程式搭配使用。 與安全遠端存取，您可以排除 hello hello 需要 Vpn 或其他傳統的遠端存取管理實作。

藉由提供您的應用程式的集中存取管理和單一登入 (SSO)，Azure AD 提供 hello 解決方案 toohello 主要資料安全性和產能的問題。

* 使用者可以存取一次登入，提供更多時間 tooincome 產生或商務作業活動完成的多個應用程式。
* 身分識別的系統管理員可以管理存取 tooapplications 在同一個地方。

hello 權益 hello 使用者並為您的公司是明顯。 讓我們探討身分識別管理員 」 和 「 hello 組織 hello 優點。

## <a name="integrated-application-benefits"></a>整合式應用程式優點
hello SSO 程序有兩個步驟：

* 驗證，驗證 hello 使用者的身分識別的 hello 程序。
* 授權 hello 決策 tooenable 或封鎖存取 tooa 資源的存取原則。

當使用 Azure AD toomanage 應用程式，並啟用 SSO:

* 在 hello 使用者在內部部署 (例如 AD) 或 Azure AD 帳戶進行驗證。
* 上 hello Azure AD 指派和保護原則確保一致的使用者體驗及 tooadd 指派、 位置及 MFA 的條件之任何應用程式，不論其內部的功能，讓您執行授權。

它重要 hello 方式 hello 授權的 toounderstand 職務 hello 目標應用程式會根據 hello 應用程式已與 Azure AD 整合的方式而有所不同。

* **由服務提供者預先整合應用程式** ：如同 Office 365 和 Azure，這些應用程式都是直接在 Azure AD 上建置並仰賴其完整的身分識別和存取管理功能。 存取 toothese 應用程式是透過目錄資訊和語彙基元發行啟用。
* **由 Microsoft 預先整合的應用程式和自訂應用程式** ：這些是依賴內部應用程式目錄並可獨立於 Azure AD 運作的獨立雲端應用程式。 存取 toothese 應用程式會啟用發行應用程式特定的認證對應 tooan 應用程式帳戶。 Hello 應用程式功能，依據 hello 認證可能同盟語彙基元或使用者名稱和先前在 hello 應用程式佈建的帳戶密碼。
* **在內部部署應用程式**透過主要讓存取 tooon 內部部署應用程式的 hello Azure AD application proxy 發行應用程式。 這些應用程式依賴於 Windows Server Active Directory 之類的內部部署目錄中心。 存取 toothese 應用程式會啟用觸發 hello proxy toodeliver hello 應用程式內容 toohello 終端使用者同時接受在內部部署的 hello 登入需求。

例如，如果使用者加入您的組織，您需要 toocreate 帳戶 hello 使用者 hello 主要登入作業的 Azure AD 中。 如果這位使用者需要存取 tooa 受管理應用程式，例如 Salesforce，您也需要 toocreate 帳戶在 Salesforce 中的這個使用者，並連結到 toohello Azure 帳戶 toomake SSO 工作。 當 hello 使用者離開公司時，它是建議 toodelete hello Azure AD 帳戶，而且中的所有對等項目的帳戶 hello IAM hello hello 使用者具有存取權的應用程式存放區。

## <a name="access-detection"></a>存取偵測
現代企業 IT 部門通常不會察覺所有 hello 雲端應用程式所使用的。 Cloud App Discovery 搭配，Azure AD 提供您方案 toodetect 這些應用程式。

## <a name="account-management"></a>帳戶管理
傳統上，管理帳戶在 hello 各種應用程式是手動程序所執行 IT 或支援 hello 組織中個人。 Azure AD 將跨所有服務提供者整合的應用程式和由 Microsoft 預先整合的這些應用程式的帳戶管理完全自動化，可支援自動化使用者佈建或 SAML JIT。

## <a name="automated-user-provisioning"></a>自動的使用者佈建
某些應用程式提供自動化介面用於建立和移除 (或停用) 帳戶。 如果有提供者提供這樣的介面，Azure AD 會加以利用。 這可減少您的營運成本，因為系統管理工作會自動發生，並改善您環境的 hello 安全性，因為它降低 hello 機率未經授權的存取。

## <a name="access-management"></a>存取管理
您可以使用 Azure AD 管理存取 tooapplications 使用個別或規則驅動的指派。 您也可以委派存取管理 toohello 適當的人員在 hello 組織確保 hello 最佳監督和降低技術服務人員 hello 負擔。

## <a name="on-premises-applications"></a>內部應用程式
內建的應用程式 proxy 的 hello 可讓您 toopublish 兩者一致導致您在內部部署的應用程式 tooyour 使用者存取現代化雲端應用程式和 hello 優點的經驗從 Azure AD 監視、 報告和安全性功能.

## <a name="reporting-and-monitoring"></a>報告和監控
Azure AD 提供預先整合的報告和監控功能，可讓您 tooknow 誰可以存取 tooapplications 和當他們實際使用它們。

## <a name="related-capabilities"></a>相關功能
您可以使用 Azure AD 透過更細微的存取原則和預先整合的 MFA 來保護您的應用程式。 有關 Azure MFA 的詳細資訊請參閱的 toolearn [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/)。

## <a name="getting-started"></a>開始使用
tooget 啟動整合應用程式與 Azure AD，看看 hello[整合 Azure Active Directory 與取得的應用程式啟動指南](active-directory-integrating-applications-getting-started.md)。

## <a name="see-also"></a>另請參閱
[Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)

