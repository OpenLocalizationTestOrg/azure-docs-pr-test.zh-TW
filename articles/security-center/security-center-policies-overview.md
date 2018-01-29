---
title: "Azure 資訊安全中心安全性原則簡介 | Microsoft Docs"
description: "了解 Azure 資訊安全中心安全性原則和主要功能。"
services: security-center
documentationcenter: na
author: YuriDio
manager: MBaldwin
editor: 
ms.assetid: f24b1e4a-cc36-4542-b21e-041453cdfcd8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/13/2017
ms.author: yurid
ms.openlocfilehash: 7a4d056fa71f211dea5e7be649c39034eabc9395
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="security-policies-overview"></a>安全性原則概觀
本文提供資訊安全中心的安全性原則概觀。

## <a name="what-are-security-policies"></a>什麼是安全性原則？
安全性原則會定義工作負載的所需設定，並且協助確保符合公司或法規安全性需求。 在資訊安全中心，您可以為 Azure 訂用帳戶定義原則，並按照工作負載的類型或資料的機密性訂定這些原則。 例如，對於使用個人識別資訊等規範資料的應用程式，其需要的安全性層級可能比工作負載還高。 

資訊安全中心原則包含下列元件：

- **資料收集**：決定代理程式佈建和[資料收集](https://docs.microsoft.com/azure/security-center/security-center-enable-data-collection)設定。
- **安全性原則**：決定何者控制資訊安全中心監視和建議。 您可以編輯資訊安全中心的[安全性原則](https://docs.microsoft.com/azure/security-center/security-center-policies)。 您也可以使用 [Azure 原則](security-center-azure-policy.md) (在有限預覽中) 建立新的定義、定義額外的原則，並在管理群組指派原則。
- **電子郵件通知**：決定安全性連絡人和[電子郵件通知](https://docs.microsoft.com/azure/security-center/security-center-provide-security-contact-details)設定。
- **定價層**：定義免費或標準[選取項目](https://docs.microsoft.com/azure/security-center/security-center-pricing)。 您選擇的一層將決定範圍中的資源可用的資訊安全中心功能。 您可以指定一層用於訂閱、資源群組和工作區。 


## <a name="who-can-edit-security-policies"></a>誰可以編輯安全性原則？
資訊安全中心會使用角色型存取控制 (RBAC)，以提供可在 Azure 中指派給使用者、群組與服務的內建角色。 使用者開啟資訊安全中心時，只能看到與自己能夠存取之資源相關的資訊。 這表示會為使用者指派資源所屬訂用帳戶或資源群組的擁有者、參與者或讀取者角色。 除了這些角色，有兩個特定的資訊安全中心角色：

- **安全性讀取者**：擁有資訊安全中心的檢視權限 (包括建議、警示、原則和健康情況)，但無法進行變更。
- **安全性管理員**：擁有與安全性讀取者相同的檢視權限，但可以更新安全性原則，並解除建議和警示。


## <a name="next-steps"></a>後續步驟
在本文中，您已了解 Azure 資訊安全中心安全性原則的相關資訊。 若要深入了解「Azure 資訊安全中心」，請參閱下列文章：

* [在 Azure 資訊安全中心設定安全性原則](security-center-policies.md)：了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md)：了解資訊安全中心建議如何協助保護您的 Azure 資源。
* [Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md)：了解如何監視 Azure 資源的健全狀況。
* [管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md)：了解如何管理與回應安全性警示。
* [使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md)：了解如何監視合作夥伴解決方案的健全狀況。
- [Azure 資訊安全中心資料安全性](security-center-data-security.md)：了解資訊安全中心如何管理和保護資料。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)：取得使用服務常見問題的解答。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)：取得最新的 Azure 安全性新聞和資訊。


