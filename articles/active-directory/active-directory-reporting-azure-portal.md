---
title: "aaaAzure Active Directory 報告 |Microsoft 文件"
description: "提供 Azure Active Directory 報告的一般概觀。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a>Azure Active Directory 報告

透過 Azure Active Directory 報告，您可以深入了解環境的運作情況。  
提供的 hello 資料可讓您：

- 判斷使用者如何利用您的應用程式和服務
- 偵測潛在的風險會影響您環境的 hello 健全狀況
- 針對會阻止使用者完成其工作的問題進行疑難排解  

hello 報告的架構會依賴兩個主要功能：

- 安全性報告
- 活動報告

![報告](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a>安全性報告

Azure Active Directory 中的 hello 安全性報表可協助您 tooprotect 貴組織的身分識別。  
Azure Active Directory 中有兩種安全性報告：

- **使用者加上旗標的風險**-從 hello[使用者加上旗標的風險安全性報告](active-directory-reporting-security-user-at-risk.md)，取得可能已受到危害的使用者帳戶的概觀。

- **高風險的登入**-以 hello[危險的登入安全性報告](active-directory-reporting-security-risky-sign-ins.md)，您會取得指標登入嘗試可能會向其他人要求執行不 hello 合法的使用者帳戶的擁有者。 

**Azure AD 授權您需要 tooaccess 安全性報表嗎？**  
所有 Azure Active Directory 版本都可提供標幟為有風險的使用者和有風險的登入報告。  
不過，報表資料粒度層級 hello hello 版本而異： 

- 在 [hello **Azure Active Directory Free 和 Basic 版本**，您已取得的加上旗標的風險和風險的登入的使用者清單。 

- hello **Azure Active Directory Premium 1**版本擴充這個模型也啟用 tooexamine hello 已偵測到每個報表的風險事件的基礎部分。 

- hello **Azure Active Directory Premium 2**版本會提供您以 hello 最詳盡 hello 基礎風險事件的相關資訊，而且它也可讓您自動回應 tooconfigured tooconfigure 安全性原則風險層級。


## <a name="activity-reports"></a>活動報告

Azure Active Directory 中有兩種活動報告：

- **稽核記錄檔**-hello[稽核記錄活動報告](active-directory-reporting-activity-audit-logs.md)您提供的每個租用戶中已執行的工作存取 toohello 歷程記錄。

- **登入**-以 hello[登入活動報表](active-directory-reporting-activity-sign-ins.md)，您可以判斷，具有執行 hello 工作 hello 稽核記錄報告所報告的人員。



hello**稽核記錄報告**為您提供系統活動記錄的相容性。
在其他的之間 hello 會提供資料可讓您 tooaddress 常見案例如：

- 我的租用戶中的某人收到存取 tooan admin 群組。 誰提供存取權給他們？ 

- 我想 tooknow hello 登入特定的應用程式的使用者清單自我最近 onboarded hello 應用程式，而且想 tooknow 也執行

- 我想要 tooknow 多少密碼重設發生在我的租用戶


**Azure AD 授權需要 tooaccess hello 稽核記錄報告？**  
hello 稽核記錄檔報表是可供您擁有授權的功能。 如果您有特定功能的授權，您也可以存取 toohello 稽核記錄檔的資訊。

如需詳細資訊，請參閱**比較正式推出的功能的 hello Free、 Basic 和 Premium edition**中[Azure Active Directory 功能](https://www.microsoft.com/cloud-platform/azure-active-directory-features)。   



hello**登入活動報表**啟用 tootoofind 回答 tooquestions 例如：

- Hello 登入使用者的模式是什麼？
- 一週內有多少使用者登入？
- 這些登入的 hello 狀態為何？


**Azure AD 授權嗎需要 tooaccess hello 登入活動報表嗎？**  
tooaccess hello 登入活動報表，您的租用戶必須有與其相關聯的 Azure AD Premium 授權。


## <a name="programmatic-access"></a>以程式設計方式存取

加法 toohello 使用者介面、 Azure Active Directory 報告也會提供您與[以程式設計方式存取](active-directory-reporting-api-getting-started-azure-portal.md)toohello 報告資料。 這些報告的 hello 資料可以是很有幫助 tooyour 應用程式，例如 SIEM 系統、 稽核和商業智慧工具。 hello Azure AD 報告 Api 提供以程式設計方式存取 toohello 資料透過一組 REST 架構應用程式開發介面。 您可以從各種程式設計語言和工具呼叫這些 API。 


## <a name="next-steps"></a>後續步驟

如果您想深入了解 hello tooknow Azure Active Directory 中的各種報表類型，請參閱：

- [標幟有風險的使用者報告](active-directory-reporting-security-user-at-risk.md)
- [有風險的登入報告](active-directory-reporting-security-risky-sign-ins.md)
- [稽核記錄報告](active-directory-reporting-activity-audit-logs.md)
- [登入記錄報告](active-directory-reporting-activity-sign-ins.md)

如果您想深入了解存取報表資料使用 hello reporting API 的 hello hello tooknow，請參閱： 

- [開始使用 hello Azure Active Directory 報告 API](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png