---
title: "Azure Active Directory 中的條件式存取的 aaaBest 作法 |Microsoft 文件"
description: "了解您在設定條件式存取原則時應該知道的事件及應避免的動作。"
services: active-directory
keywords: "條件式存取 tooapps，Azure AD 中，使用條件式存取保護存取 toocompany 資源，條件式存取原則"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a>Azure Active Directory 中條件式存取的最佳做法

此主題提供與您在設定條件式存取原則時應該知道的事件及應避免的動作相關的資訊。 閱讀本主題之前，您應該熟悉 hello 概念和術語 hello 述[Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal.md)

## <a name="what-you-should-know"></a>您應該知道的事情

### <a name="whats-required-toomake-a-policy-work"></a>Toomake 原則工作的必要條件？

當您建立新的原則時，未選取任何使用者、群組、應用程式或存取控制項。

![雲端應用程式](./media/active-directory-conditional-access-best-practices/02.png)


toomake 原則運作，您必須設定下列 hello:


|何事           | 方式                                  | 理由|
|:--            | :--                                  | :-- |
|**雲端應用程式** |您需要 tooselect 一或多個應用程式。  | 條件式存取原則 hello 目標是 tooenable 您 toofine 微調授權的使用者可以存取您的應用程式的方式。|
| **使用者和群組** | 您必須至少一個 tooselect 使用者或群組是授權您選取的 tooaccess hello 雲端應用程式。 | 永遠不會觸發未指派使用者和群組的條件式存取原則。 |
| **存取控制** | 您必須至少一個 tooselect 存取控制。 | 原則處理器需要 tooknow 哪些 toodo 如果符合條件。|


在 新增 toothese 基本需求，在許多情況下，您也應該設定條件。 雖然沒有已設定的條件，也可以運作的原則，條件是 hello 驅動因素，來微調存取 tooyour 應用程式。


![雲端應用程式](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a>如何評估指派？

所有指派邏輯上都會使用 **AND** 運算子。 如果您有多個指派設定，tootrigger 原則，必須滿足所有指派。  

如果您需要 tooconfigure 位置條件適用於 tooall 連線從您的組織網路之外，您可以達成的：

- 包含**所有位置**
- 排除**所有信任的 IP**

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a>如果您擁有 hello Azure 傳統入口網站中的原則和設定的 Azure 入口網站，會發生什麼事？  
這兩項原則會強制執行由 Azure Active Directory 和 hello 使用者只在符合所有需求時，取得存取權。

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a>如果您擁有 hello Intune Silverlight 入口網站中的原則和 hello Azure 入口網站，會發生什麼事？
這兩項原則會強制執行由 Azure Active Directory 和 hello 使用者只在符合所有需求時，取得存取權。

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a>如果我有多個原則設定相同的使用者的 hello，會發生什麼情況？  
每個登入，Azure Active Directory 會評估所有原則，並可確保之前已授與存取權 toohello 使用者符合所有需求。


### <a name="does-conditional-access-work-with-exchange-activesync"></a>條件式存取是否適用於 Exchange ActiveSync？

是，您可以在條件式存取原則中使用 Exchange ActiveSync。


## <a name="what-you-should-avoid-doing"></a>您應該避免做的事

hello 條件式存取架構為您提供絕佳的設定彈性。 不過，很大的彈性也表示您應該仔細檢閱每個組態原則先前 tooreleasing 它 tooavoid 非預期的結果。 在此內容中，您應該特別特別注意 tooassignments 例如會影響完整集**所有使用者 / 群組 / 雲端應用程式**。

在您環境中，您應該避免 hello 的設定：


**針對所有使用者、所有雲端應用程式：**

- **封鎖存取** - 此組態會封鎖您整個組織，這絕對不是一個好方法。

- **需要相容的裝置**-使用者，不要已註冊其裝置的資訊，此原則會封鎖所有存取，包括存取 toohello Intune 入口網站。 如果您是系統管理員沒有已註冊的裝置，這項原則會阻止您從取回 hello Azure 入口網站 toochange hello 原則。

- **需要加入網域**-此原則的封鎖存取具有也 hello 潛在 tooblock 所有使用者存取您組織中如果您沒有加入網域的裝置尚未。


**針對所有使用者、所有雲端應用程式、所有裝置平台：**

- **封鎖存取** - 此組態會封鎖您整個組織，這絕對不是一個好方法。


## <a name="common-scenarios"></a>常見案例

### <a name="requiring-multi-factor-authentication-for-apps"></a>應用程式需要 Multi-Factor Authentication

許多環境中有其他人需要比 hello 較高的保護層級的應用程式。
這種，例如 hello 擁有存取 toosensitive 資料的應用程式。
如果您想 tooadd 另一層保護 toothese 應用程式，您可以設定條件式存取原則，當使用者同時存取這些應用程式要求多重要素驗證。


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>從不受信任的網路存取時需要 Multi-Factor Authentication

此案例中是類似 toohello 前一個案例，因為它會增加多因素驗證的需求。
不過，hello 主要差異是這項需求的 hello 條件。  
當應用程式存取 toosensitve 資料與已 hello 焦點的 hello 前一個案例時，這種情況的 hello 焦點是受信任的位置。  
換句話說，如果使用者從您不信任的網路存取應用程式，您可能需要 Multi-Factor Authentication。


### <a name="only-trusted-devices-can-access-office-365-services"></a>只有受信任的裝置可以存取 Office 365 服務

如果您使用 Intune 在您的環境中，您可以立即開始使用 hello Azure 主控台中的 hello 條件式存取原則介面。

許多 Intune 客戶使用條件式存取 tooensure 只有受信任的裝置才可以存取 Office 365 服務。 這表示，行動裝置向 Intune 註冊並符合相容性原則的需求，Windows 電腦會聯結的 tooan 在內部部署網域。 重要的改進是，您不需要 tooset hello hello Office 365 服務的每個相同的原則。  當您建立新的原則時，設定 hello 雲端應用程式 tooinclude 每個您想使用 tooprotect 使用條件式存取的 hello O365 應用程式。

## <a name="next-steps"></a>後續步驟

如果您想如何 tooconfigure 條件式存取原則，請參閱的 tooknow[開始使用 Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal-get-started.md)。
