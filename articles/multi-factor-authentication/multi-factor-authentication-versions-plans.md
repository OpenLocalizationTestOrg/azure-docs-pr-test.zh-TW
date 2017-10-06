---
title: "aaaAzure MFA 版本和耗用量計劃 |Microsoft 文件"
description: "Hello multi-factor Authentication 用戶端 hello 不同的方法和可用的版本的相關資訊。 每個耗用量計劃的詳細資料"
keywords: 
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: kgremban
ms.openlocfilehash: 4914747e435531b9f950356d23aa386f3d9585d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-azure-multi-factor-authentication"></a>如何 tooget Azure 多重要素驗證

說 tooprotecting 您的帳戶，雙步驟驗證應該是標準整個組織。 這項功能是有特殊權限存取 tooresources 的系統管理帳戶的特別重要。 基於這個理由，Microsoft 會提供基本的雙步驟驗證功能 tooOffice 365 和 Azure 系統管理員。 如果您想 tooupgrade hello 功能為您的系統管理員，或擴充您的使用者的雙步驟驗證 toohello rest，您可以購買 Azure Multi-factor Authentication。 

本文說明 hello hello 版本提供 tooadministrators 和 hello 完整的 Azure MFA 版本之間的差異，並指定每個中可用的功能。 如果您已準備 toodeploy hello 完成 Azure MFA 供應項目，hello 稍後的章節涵蓋實作選項和 Microsoft 如何計算耗用量。

>[!IMPORTANT]
>這篇文章的目的在於 toobe 您了解指南 toohelp hello 不同的方式 toobuy Azure 多重要素驗證。 如需定價和計費的特定詳細資訊，您應該一律參考 toohello[定價頁面的 Multi-factor Authentication](https://azure.microsoft.com/pricing/details/multi-factor-authentication/)。

## <a name="available-versions-of-azure-multi-factor-authentication"></a>可用的 Azure Multi-Factor Authentication 版本

hello 下表說明 hello 多重要素驗證的三個版本之間的差異：

| 版本 | 說明 |
| --- | --- |
| Multi-Factor Authentication for Office 365 |這個版本專門搭配 Office 365 應用程式，並管理從 hello Office 365 入口網站。 系統管理員可以[使用雙步驟驗證來保護 Office 365 資源的安全](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6)。 此版本隨附於 Office 365 訂用帳戶。 |
| 適用於 Azure 系統管理員的 Multi-Factor Authentication | Azure 租用戶的全域系統管理員可以為其全域系統管理員帳戶啟用雙步驟驗證，而不需要額外收費。|
| Azure Multi-Factor Authentication | 通常參考的 tooas hello 「 完整 」 版本，Azure Multi-factor Authentication 提供 hello 豐富的功能。 它會提供額外的設定選項，透過 hello [Azure 傳統入口網站](https://manage.windowsazure.com)、 進階報告，以及支援廣泛的內部部署和雲端應用程式。 Azure Multi-factor Authentication 已納入 Azure Active Directory Premium （P1 和 P2 計劃） 和 Enterprise Mobility + Security （E3 和 E5 計劃），而且可以是部署可能[hello 雲端或內部](multi-factor-authentication-get-started.md)。 |

## <a name="feature-comparison-of-versions"></a>版本的功能比較
hello 下表提供可用在 hello hello 功能的清單各種版本的 Azure Multi-factor Authentication。

> [!NOTE]
> 如此比較表討論 hello 功能屬於的每個版本的 Multi-factor Authentication。 如果您擁有 hello 完整的 Azure Multi-factor Authentication 服務，某些功能可能無法使用取決於您是否使用[hello 雲端中的 MFA 或 MFA 內部](multi-factor-authentication-get-started.md)。


| 功能 | Multi-Factor Authentication for Office 365 | 適用於 Azure 系統管理員的 Multi-Factor Authentication | Azure Multi-Factor Authentication |
| --- |:---:|:---:|:---:|
| 透過 MFA 保護系統管理員帳戶 |● |● (僅限全域系統管理員帳戶) |● |
| 以行動應用程式做為第二個因素 |● |● |● |
| 以撥打電話做為第二個因素 |● |● |● |
| 以 SMS 做為第二個因素 |● |● |● |
| 用戶端應用程式密碼不支援 MFA |● |● |● |
| 系統管理員控制驗證方法 |● |● |● |
| PIN 模式 | | |● |
| 詐騙警示 | | |● |
| MFA 報告 | | |● |
| 一次性略過 | | |● |
| 通話的自訂問候語 | | |● |
| 自訂的通話來電者 ID | | |● |
| 信任的 IP | | |● |
| 記住受信任裝置的 MFA |● |● |● |
| MFA SDK | | |● (需要 Multi-Factor Auth Provider 和完整的 Azure 訂用帳戶) |
| 內部部署應用程式的 MFA | | |● |

## <a name="how-tooget-azure-multi-factor-authentication"></a>如何 tooget Azure 多重要素驗證
如果您想要提供 Azure Multi-factor Authentication 的 hello 完整功能，有幾個選項：

### <a name="option-1---mfa-licenses"></a>選項 1 - MFA 授權

購買 Azure Multi-factor Authentication Server 的授權，並將它們指派 tooyour Azure Active Directory 中的使用者。 

如果您使用此選項時，您應該先建立 Azure Multi-factor Authentication 提供者，只有在沒有授權的某些使用者，也必須 tooprovide 雙步驟驗證。 否則，您可能會被計費兩次。

### <a name="option-2---bundled-licenses-that-include-mfa"></a>選項 2 - 包括 MFA 的配套授權

購買授權，包括 Azure Multi-factor Authentication，例如 Azure Active Directory Premium （P1 或 P2） 或 Enterprise Mobility + Security （E3 或 E5），並將它們指派 tooyour Azure Active Directory 中的使用者。 

如果您使用此選項時，您應該先建立 Azure Multi-factor Authentication 提供者，只有在沒有授權的某些使用者，也必須 tooprovide 雙步驟驗證。 否則，您可能會被計費兩次。 

### <a name="option-3---mfa-consumption-based-model"></a>選項 3 - MFA 耗用量為基礎的模型

在 Azure 訂用帳戶中建立 Azure Multi-Factor Authentication 提供者。 Azure MFA 提供者都是針對企業合約、Azure 貨幣承諾或信用卡 (如所有其他 Azure 資源) 進行計費的 Azure 資源。 這些提供者只能建立在完整的 Azure 訂用帳戶中，不限於具有 $0 消費限制的 Azure 訂用帳戶。 當您啟用授權時會建立有限的訂用帳戶，像是選項 1 和 2。 

使用 Azure Multi-Factor Authentication 提供者時，有兩種使用量模型可透過您的 Azure 訂用帳戶計費：  

1. **每個使用者**： 適用於想要定期需要驗證的員工固定數目的 tooenable 雙步驟驗證的企業。 每個使用者計費根據 hello Azure AD 租用戶和/或您的 Azure MFA Server 中啟用 MFA 的使用者數目而定。 使用者是否已啟用 MFA 的兩個 Azure ad 和 Azure MFA Server，而且已啟用網域同步處理 (Azure AD Connect)，則我們計數 hello 大的一組使用者。 如果未啟用網域同步處理，則我們計數 hello 總和的所有使用者在 Azure AD 中啟用 MFA 和 Azure MFA Server。 計費是按比例和報告 toohello 商務系統。 

  > [!NOTE]
  > 計費範例 1︰今日有 5,000 個使用者啟用 MFA。 hello MFA 系統該數目除以 31，以及報表 161.29 使用者針對該日。 明天啟用 15 的更多使用者，因此 hello MFA 系統會針對該日報告 161.77 使用者。 Hello hello 帳單週期結束的使用者對您的 Azure 訂用帳戶計費 hello 總數加總 tooaround 5000。 
  >
  > 計費範例 2： 您必須擁有授權的使用者和沒有，使用者的混合讓您有每位使用者 Azure MFA 提供者 toomake 向上 hello 差異。 您的租用戶上有 4,500 個 Enterprise Mobility + Security 授權，但 5,000 個使用者啟用 MFA。 Azure 訂用帳戶會對 500 個使用者計費，按比例計費且每日報告為 16.13 個使用者。 

2. **每次驗證**-如需偶爾需要驗證的使用者一大群 tooenable 雙步驟驗證的企業。 計費根據 hello hello Azure MFA 雲端服務，無論這些驗證成功或拒絕所接收到的兩步驟驗證要求的數目。 這個計費出現在您的 Azure 使用量陳述式，在組件中的 10 的驗證，每天會報告的 toohello 商務系統。 

  > [!NOTE]
  > 計費範例 3: hello Azure MFA 服務今天收到 3,105 雙步驟驗證要求。 您的 Azure 訂用帳戶會以 310.5 個驗證組件計費。 

很重要的 toonote，您可以有 Azure MFA 的授權，但仍取得支付耗用量為基礎的設定。 如果您設定每次驗證 Azure MFA 提供者，需支付每個雙步驟驗證的要求，甚至包括具有授權的使用者。 如果您不是連結的 tooyour Azure AD 租用戶網域上設定每位使用者的 Azure MFA 提供者，您需要付費每位啟用使用者即使您的使用者具備 Azure AD 授權。 

## <a name="next-steps"></a>後續步驟

- 如需定價詳細資料，請參閱 [Azure MFA 定價](https://azure.microsoft.com/pricing/details/multi-factor-authentication/)。

- 選擇是否 toodeploy Azure MFA [hello 雲端或內部部署中](multi-factor-authentication-get-started.md)
