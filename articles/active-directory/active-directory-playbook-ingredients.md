---
title: "Active Directory PoC 腳本食材 aaaAzure |Microsoft 文件"
description: "探索並快速實作身分識別和存取管理案例"
services: active-directory
keywords: "azure active directory, 腳本, 概念證明, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a>Azure Active Directory 概念證明腳本組成要素 

## <a name="theme"></a>佈景主題
Azure AD 提供身分識別和存取解決方案，跨 hello 企業中的多個區域。 我們分類 hello 下列區域中的 hello 案例： 

* [許多應用程式、一個身分識別](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [增加您的安全性](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [使用自助式縮放比例](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

這定義佈景主題 tooframe hello PoC 有助於 toofocus hello 努力建立業務目標與共鳴，有時候是概念證明 hello 第一個位置中的 hello 感興趣的 hello 觸發程序。 

## <a name="environment"></a>Environment

它是您將在其中傳送 hello PoC hello 環境的重要 toodetermine hello 詳細資料。 在理想情況下可以建置它之後 hello PoC 完成。 hello 目標環境很重要，而且您應該找到 hello 之間進行它為實際盡可能與條件約束或額外的考量 hello 成本的正確平衡。 hello PoCs 一般環境是：
* **生產環境：** hello 案例會實作即時環境中和已部署 Microsoft 雲端服務 （生產 AD、 Office 365、 Azure AD 租用戶/SSO 解決方案）。 
* **使用者接受度測試 (UAT)/開發環境︰**您擁有測試基礎結構 (平行 AD，並可能有 Azure AD 租用戶/SSO 解決方案) 與類似生產環境的測試資料。 一般而言，hello 測試環境是跨多個專案共用 hello 企業中。

本指南中的大部分案例皆具有附加特質。 如此一來，他們可以部署在 hello 生產租用戶中而不會影響 hello PoC 外的使用者。 在整份文件中，我們會指出哪些案例會對整個租用戶造成影響。 在這些情況下，您可能想 tooconsider 非生產環境。 


## <a name="target-users"></a>目標使用者

它是使用者將要執行 hello 案例，尤其是當 hello 環境時，生產或測試重要 toodetermine hello 目標組。 hello PoC 的目標使用者類別如下：
* **試驗使用者：** hello 環境，將它們用於其天 tooday hello 帳戶搭配使用 hello 方案中的實際使用者的工作函式
* **測試使用者：**測試 hello 環境中建立的帳戶 

本指南中的大部分案例均可供試驗使用者進行練習。 在整份文件中，我們會視需要指出目標使用者的考量事項。


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]