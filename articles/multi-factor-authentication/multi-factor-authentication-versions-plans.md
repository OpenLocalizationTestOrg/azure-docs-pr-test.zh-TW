---
title: "Azure MFA 版本和耗用量計劃 | Microsoft Docs"
description: "Multi-Factor Authentication 用戶端、不同的方法及可用版本的詳細資訊。 每個耗用量計劃的詳細資料"
keywords: 
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: richagi
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: joflore
ms.openlocfilehash: af86434e1205d67829fc7079d97a37f013c0f2d8
ms.sourcegitcommit: 7d4b3cf1fc9883c945a63270d3af1f86e3bfb22a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="how-to-get-azure-multi-factor-authentication"></a>如何取得 Azure Multi-Factor Authentication

說到保護您的帳戶，雙步驟驗證在整個組織中應該為標準。 這項功能對於資源具有特殊存取權限的系統管理帳戶特別重要。 基於這個理由，Microsoft 為 Office 365 和 Azure 系統管理員免費提供基本雙步驟驗證功能。 如果您想要升級您系統管理員的功能，或擴充雙步驟驗證到其他的使用者，您可以購買 Azure Multi-Factor Authentication。 

本文說明提供給系統管理員之版本和完整 Azure MFA 版本之間的差異。 如果您準備好部署完整的 Azure MFA 供應項目，稍後的章節會涵蓋實作選項和 Microsoft 計算耗用量的方式。


>[!IMPORTANT]
>本文旨在幫助您了解購買 Azure Multi-Factor Authentication 的不同方式。 如需定價和計費的特定詳細資訊，您應一律參考 [Multi-Factor Authentication 定價頁面](https://azure.microsoft.com/pricing/details/multi-factor-authentication/)。

## <a name="available-versions-of-azure-multi-factor-authentication"></a>可用的 Azure Multi-Factor Authentication 版本

下表說明三種 Multi-Factor Authentication 版本之間的差異︰

| 版本 | 描述 |
| --- | --- |
| Multi-Factor Authentication for Office 365 |這個版本專門搭配 Office 365 應用程式運作，並且可從 Office 365 入口網站管理。 系統管理員可以[使用雙步驟驗證來保護 Office 365 資源的安全](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6)。 此版本隨附於 Office 365 訂用帳戶。 |
| 適用於 Azure AD 系統管理員的 Multi-Factor Authentication | Azure AD 租用戶中指派為全域管理員角色的使用者，可以為其 Azure AD 全域系統管理員帳戶啟用雙步驟驗證，而不需要額外收費。|
| Azure Multi-Factor Authentication | 通常稱為「完整」版本，Azure Multi-Factor Authentication 提供最豐富的功能。 它能透過 [Azure 入口網站](https://portal.azure.com)、進階報告及支援一系列內部部署和雲端應用程式來提供其他設定選項。 Azure Multi-Factor Authentication 隨附於 [Azure Active Directory Premium 方案](https://www.microsoft.com/cloud-platform/azure-active-directory-features)和 [Enterprise Mobility + Security 方案](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing)中，並可以在雲端中部署或進行內部部署。 |

## <a name="feature-comparison-of-versions"></a>版本的功能比較
下表提供 Azure Multi-Factor Authentication 各版本中可用的功能清單。

> [!NOTE]
> 此比較表會討論每個 Multi-Factor Authentication 版本中所包含的功能。 如果您擁有完整的 Azure Multi-Factor Authentication 服務，則依您使用的是[雲端中的 MFA 或內部部署 MFA](multi-factor-authentication-get-started.md) 而定，某些功能可能無法使用。


| 功能 | Multi-Factor Authentication for Office 365 | 適用於 Azure AD 系統管理員的 Multi-Factor Authentication | Azure Multi-Factor Authentication |
| --- |:---:|:---:|:---:|
| 透過 MFA 保護 Azure AD 系統管理員帳戶 |● |● (僅限 Azure AD 全域系統管理員帳戶) |● |
| 以行動應用程式做為第二個因素 |● |● |● |
| 以撥打電話做為第二個因素 |● |● |● |
| 以 SMS 做為第二個因素 |● |● |● |
| 用戶端應用程式密碼不支援 MFA |● |● |● |
| 系統管理員控制驗證方法 |● |● |● |
| 透過 MFA 保護非系統管理員帳戶 |● (僅適用於 Office 365 應用程式) | |● |
| PIN 模式 | | |● |
| 詐騙警示 | | |● |
| MFA 報告 | | |● |
| 一次性略過 | | |● |
| 通話的自訂問候語 | | |● |
| 自訂的通話來電者 ID | | |● |
| 信任的 IP | | |● |
| 記住受信任裝置的 MFA |● |● |● |
| MFA SDK | | |● (已過時) | 
| 內部部署應用程式的 MFA | | |● |

## <a name="how-to-get-azure-multi-factor-authentication"></a>如何取得 Azure Multi-Factor Authentication
如果您想要 Azure Multi-Factor Authentication 所提供的完整功能，有數個選項︰

### <a name="option-1---mfa-licenses"></a>選項 1 - MFA 授權

購買 Azure Multi-Factor Authentication 授權，並將其指派給您 Azure Active Directory 中的使用者。 

如果您使用此選項，則僅在需要為一些沒有授權的使用者提供雙步驟驗證時，才建立 Azure Multi-Factor Authentication 提供者。 否則，您可能會被計費兩次。

### <a name="option-2---bundled-licenses-that-include-mfa"></a>選項 2 - 包括 MFA 的配套授權

購買隨附 Azure Multi-Factor Authentication 的授權 (例如 Azure Active Directory Premium 或是 Enterprise Mobility + Security)，並將其指派給您 Azure Active Directory 中的使用者。 

如果您使用此選項，則僅在需要為一些沒有授權的使用者提供雙步驟驗證時，才需建立 Azure Multi-Factor Authentication 提供者。 否則，您可能會被計費兩次。 

### <a name="option-3---mfa-consumption-based-model"></a>選項 3 - MFA 耗用量為基礎的模型

在 Azure 訂用帳戶中建立 Azure Multi-Factor Authentication 提供者。 Azure MFA 提供者都是針對企業合約、Azure 貨幣承諾或信用卡 (如所有其他 Azure 資源) 進行計費的 Azure 資源。 這些提供者只能建立在完整的 Azure 訂用帳戶中，不限於具有 $0 消費限制的 Azure 訂用帳戶。 當您啟用授權時會建立有限的訂用帳戶，像是選項 1 和 2。 

使用 Azure Multi-Factor Authentication 提供者時，有兩種使用量模型可透過您的 Azure 訂用帳戶計費：  

1. **每個啟用的使用者** - 適用於想要為一群定期需要驗證之固定數量員工啟用雙步驟驗證的企業。 每個使用者會根據 Azure AD 租用戶和您 Azure MFA 伺服器中啟用的 MFA 使用者數目計費。 使用者如果在 Azure AD 與 Azure MFA Server 中啟用 MFA，並啟用網域同步處理 (Azure AD Connect)，則我們會計算較大的使用者組。 如果未啟用網域同步處理，則我們會計算在 Azure AD 與 Azure MFA Server 中啟用 MFA 的所有使用者總和。 計費是按比例計費，而每日回報給商務系統。 

  > [!NOTE]
  > 計費範例 1︰今日有 5,000 個使用者啟用 MFA。 MFA 系統會將該數字除以 31，並報告那一天有 161.29 個使用者。 明天多啟用 15 個使用者，則 MFA 系統會報告那一天有 161.77 個使用者。 計費週期結束時，針對您的 Azure 訂用帳戶計費的使用者總數加起來大約為 5,000 個。 
  >
  > 計費範例 2︰您有具有授權的使用者與不具有授權的使用者混合，因此您需要有每個使用者 Azure MFA 提供者來補足差距。 您的租用戶上有 4,500 個 Enterprise Mobility + Security 授權，但 5,000 個使用者啟用 MFA。 Azure 訂用帳戶會對 500 個使用者計費，按比例計費且每日報告為 16.13 個使用者。 

2. **每次驗證** - 適用於想要為大量不定期需要驗證之使用者啟用雙步驟驗證的企業。 計費是根據雙步驟驗證要求數目，不論這些驗證是否成功還是遭到拒絕。 這個計費會以 10 個驗證的組件出現在您的 Azure 使用量聲明中，並每日回報。 

  > [!NOTE]
  > 計費範例 3：今日，Azure MFA 服務收到 3,105 個雙步驟驗證要求。 您的 Azure 訂用帳戶會以 310.5 個驗證組件計費。 

請務必注意，您可以有 Azure MFA 授權，但仍需支付耗用量為基礎的組態。 如果您設定每次驗證 Azure MFA 提供者，需支付每個雙步驟驗證的要求，甚至包括具有授權的使用者。 如果在不連結至 Azure AD 租用戶的網域上設定每個使用者 Azure MFA 提供者，則會以每個啟用的使用者計費，即使您的使用者在 Azure AD 具有授權。 

## <a name="next-steps"></a>後續步驟

- 如需定價詳細資料，請參閱 [Azure MFA 定價](https://azure.microsoft.com/pricing/details/multi-factor-authentication/)。

- 選擇要[在雲端還是內部部署](multi-factor-authentication-get-started.md)部署 Azure MFA
