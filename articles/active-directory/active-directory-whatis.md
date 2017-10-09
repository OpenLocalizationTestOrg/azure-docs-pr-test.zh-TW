---
title: "aaaWhat 是 Azure Active Directory？"
description: "使用 Azure Active Directory tooextend hello 到您現有內部部署身分識別雲端或開發 Azure AD 整合的應用程式。"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.assetid: 498820c4-9ebe-42be-bda2-ecf38cc514ca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.custom: it-pro
ms.openlocfilehash: b470d7d8f0e733fe9363bd46ed2c2d143d5b3982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-active-directory"></a>什麼是 Azure Active Directory？
Azure Active Directory (Azure AD) 是 Microsoft 的多租用戶雲端型目錄和身分識別管理服務。 Azure AD 結合核心目錄服務及進階身分識別管理和應用程式存取管理。 Azure AD 也提供豐富、 以標準為基礎的平台，可讓開發人員 toodeliver 存取控制 tootheir 應用程式，根據集中化的原則和規則。 

IT 系統管理員，Azure AD 提供價格合理且簡單 toouse 方案 toogive 員工和商業協力廠商單一登入 (SSO) 存取太[數千個 SaaS 應用程式的雲端](active-directory-saas-tutorial-list.md)例如 Office365、 Salesforce.com、 DropBox 和Concur。

應用程式開發人員，Azure AD 可讓您專注於建置它快速、 簡單 toointegrate 世界類別身分識別管理解決方案的應用程式使用組織數百萬 hello world。

Azure AD 也包含一組完整的身分識別管理功能，包括多重要素驗證、裝置註冊、自助式密碼管理、自助式群組管理、特殊權限的帳戶管理、角色型存取控制、應用程式使用量監視、豐富的稽核，以及安全性監視和警示。 這些功能可以協助保護雲端型應用程式的安全、簡化 IT 程序、降低成本，以及協助確保達到公司的規範目標。

此外，與剛[四個點擊](./connect/active-directory-aadconnect-get-started-express.md)，Azure AD 可與現有的 Windows Server Active Directory 整合，讓組織 hello 能力 tooleverage 其現有內部部署身分識別的投資效用發揮 toomanage 存取toocloud 架構的 SaaS 應用程式。

如果您是 Office365、Azure 或 Dynamics CRM Online 的客戶，您可能不知道您已經在使用 Azure AD。 每個 Office365、Azure 和 Dynamics CRM 租用戶實際上都已經是 Azure AD 租用戶。 每當您想要開始使用 Azure AD 的其他雲端應用程式的租用戶 toomanage 存取 toothousands 整合 ！

![Azure AD Connect 堆疊](./media/active-directory-whatis/Azure_Active_Directory.png)

## <a name="how-reliable-is-azure-ad"></a>Azure AD 有多可靠？
Azure AD 的 hello 多租用戶、 地理分散、 高可用性設計表示，您可以依賴它的最重要的商務需求。 用盡 28 資料中心 hello 世界各地具有自動容錯移轉，您必須在 hello 舒適的了解 Azure AD 是非常可靠，而且，即使資料中心停機時，您的目錄資料的複本中至少兩個多地域分散資料置中並且可供立即存取。

如需詳細資料，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。

## <a name="choose-an-edition"></a>選擇版本
所有 Microsoft Online 商務服務都依賴 Azure Active Directory (Azure AD) 來進行登入和其他身分識別需求。 如果您訂閱 tooany （例如，Office 365 或 Microsoft Azure） 的 Microsoft Online 的商務服務，您會取得具有存取 tooall hello 可用功能的 Azure AD。 使用 hello Azure Active Directory Free 版時，您可以管理使用者和群組、 與內部部署目錄同步處理、 跨 Azure、 Office 365 和無數熱門 SaaS 應用程式，例如 Salesforce、 Workday、 Concur、 DocuSign，取得單一登入Google Apps、 Box、 ServiceNow、 Dropbox 和更多。 

tooenhance Azure Active Directory，您可以新增使用 hello Azure Active Directory Basic、 Premium P1 和 Premium P2 edition 的付費的功能。 付費版本的 Azure Active Directory 是建立在您現有的免費目錄上，提供的企業級功能跨越自助、增強的監視、安全性報告、Multi-Factor Authentication (MFA) 及您的行動工作力的安全存取。

> [!NOTE]
> Hello 定價選項，這些版本，請參閱[Azure Active Directory 定價](https://azure.microsoft.com/pricing/details/active-directory/)。 目前在中國不支援 Premium P1、Premium P2 及 Azure Active Directory Basic。 請與我們連絡在 hello Azure Active Directory 論壇，如需詳細資訊。
>

* **Azure Active Directory Basic** - 針對具有雲端優先需求的任務背景工作角色設計，此版本提供以雲端為中心的應用程式存取和自助身分識別管理解決方案。 Azure Active directory Basic 版的 hello，取得提升產能包括和成本減少群組為基礎的存取管理，自助式密碼重設雲端應用程式和 Azure Active Directory 應用程式 Proxy (toopublish 等的功能在內部部署 web 應用程式使用 Azure Active Directory），所有受 99.9%執行時間的企業級 SLA。
* **Azure Active Directory Premium P1** -設計具有多個要求 (demand) 的 tooempower 組織身分識別和存取管理需求，Azure Active Directory Premium edition 將豐富功能的企業級身分識別管理功能和啟用混合式使用者 tooseamlessly 存取內部部署和雲端功能。 此版本包含所需的所有資訊工作者和混合式環境中的身分識別管理員跨應用程式存取、 自助服務身分識別和存取管理 (IAM)、 識別身分保護和 hello 雲端中的安全性。 它支援進階管理和委派資源，例如：動態群組和自助群組管理。 它包含 Microsoft Identity Manager (一項內部部署及身分識別和存取管理套件)，並提供可為您的內部部署使用者啟用自助密碼重設之類解決方案的雲端回寫功能。
* **Azure Active Directory Premium P2** -進階保護的所有使用者和系統管理員所設計，此新的供應項目包括所有 hello 功能在 Azure AD Premium P1，以及我們新的識別身分保護和特殊權限的身分識別管理。 Azure Active Directory 識別身分保護會利用數十億個訊號 tooprovide 風險型條件式存取 tooyour 應用程式和重要的公司資料。 我們也可協助您管理及保護權限的帳戶與 Azure Active Directory Privileged Identity Management，讓您可以探索、 限制和監視系統管理員和其存取 tooresources，並提供在 just-in-time 存取時所需。  

> [!NOTE]
> 許多 Azure Active Directory 功能是透過「隨用隨付」版本提供：
>
> * Active Directory B2C 是消費者導向應用程式的 hello 身分識別和存取管理解決方案。 如需詳細資料，請參閱： [Azure Active Directory B2C](https://azure.microsoft.com/documentation/services/active-directory-b2c/)
> * Azure Multi-Factor Authentication 可透過每一使用者或每一驗證提供者方式使用。 如需詳細資訊，請參閱 [什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)
>

## <a name="how-can-i-get-started"></a>如何開始使用？

**如果您是 IT 管理員：**

* [立即試用！](https://azure.microsoft.com/trial/get-started-active-directory/) - 您可以立即註冊免費的 30 天試用版，並使用此連結在 5 分鐘內部署第一個雲端解決方案

* 閱讀[開始使用 Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) 以取得獲得 Azure AD 租用戶並快速執行的秘訣和訣竅

**如果您是開發人員：**
 
* 請查看我們[開發人員手冊](active-directory-developers-guide.md)tooAzure Active Directory

* [開始使用試用版](https://azure.microsoft.com/trial/get-started-active-directory/) – 立即註冊免費 30 天的試用版，並開始整合您的應用程式與 Azure AD

## <a name="next-steps"></a>後續步驟
[深入了解 Azure 身分識別和存取管理的 hello 基本概念](https://docs.microsoft.com/azure/active-directory/identity-fundamentals)
