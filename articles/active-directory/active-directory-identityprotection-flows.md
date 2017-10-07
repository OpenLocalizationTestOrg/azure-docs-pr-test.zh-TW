---
title: "aaaSign 中的體驗與 Azure AD Identity Protection |Microsoft 文件"
description: "識別身分保護已降低或補救使用者或原則時需要多重要素驗證時，請提供 hello 使用者經驗的概觀。"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, 管理應用程式, 安全性, 風險, 風險層級, 弱點, 安全性原則"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a>使用 Azure AD Identity Protection 時的登入體驗
透過 Azure Active Directory Identity Protection，您可以：

* 需要 multi-factor authentication 使用者 tooregister
* 處理高風險的登入和遭到入侵的使用者

因為只要直接登入藉由提供使用者名稱和密碼不是可能再 hello 回應 hello 系統 toothese 問題上使用者的登入體驗有影響。 使用者安全地送回商務的必要的 tooget 不額外的步驟。

本主題會針對可能發生的所有案例，為您提供使用者的登入體驗概觀。

**Multi-Factor Authentication**

* Multi-Factor Authentication 註冊

**有風險的登入**

* 有風險的登入復原
* 已封鎖有風險的登入
* 在有風險的登入期間註冊 Multi-Factor Authentication

**有風險的使用者**

* 遭到入侵的帳戶復原
* 已封鎖遭到入侵的帳戶

## <a name="multi-factor-authentication-registration"></a>Multi-Factor Authentication 註冊
hello 最佳的使用者體驗，同時 hello 遭盜用的帳戶復原流程和 hello 危險的登入流程、 hello 使用者可以自行復原時。 使用者所註冊的多重要素驗證，如果他們已經有可以使用的 toopass 安全性挑戰其帳戶相關聯的電話號碼。 沒有說明服務台或系統管理員介入是需要的 toorecover 從帳戶遭到入侵。 因此，強烈建議您 tooget 您的使用者註冊 multi-factor authentication。 

系統管理員可以：

* 設定原則，需要進行額外安全性驗證的使用者 tooset 註冊他們的帳戶。 
* 允許略過多重要素驗證登錄向上 too30 天，如果他們想 toogive 使用者註冊之前請先在寬限期。

**hello 多重要素驗證註冊具有三個步驟：**

1. 在 hello 第一個步驟中，hello 使用者會收到 multi-factor authentication hello 需求 tooset hello 帳戶的相關通知。 
   
    ![補救](./media/active-directory-identityprotection-flows/140.png "補救")
2. tooset 註冊多重要素驗證，您需要 toolet hello 系統知道您想 toobe 連絡。
   
    ![補救](./media/active-directory-identityprotection-flows/141.png "補救")
3. hello 系統提交挑戰 tooyou，而且您需要 toorespond。
   
    ![補救](./media/active-directory-identityprotection-flows/142.png "補救")

## <a name="risky-sign-in-recovery"></a>有風險的登入復原
系統管理員已設定的原則，登入的風險時嘗試 toosign 中, 會通知 hello 受影響的使用者。 

**hello 風險登入流程有兩個步驟：** 

1. hello 使用者異常偵測其登入，例如從新的位置、 裝置或應用程式登入的相關通知。 
   
    ![補救](./media/active-directory-identityprotection-flows/120.png "補救")
2. hello 使用者所解決的安全性挑戰是必要的 tooprove 其身分識別。 如果 hello 使用者已註冊的多重要素驗證它們需要 tooround 路線安全性程式碼 tootheir 電話號碼。 由於這是僅有風險的登入並遭盜用的帳戶，hello 使用者不需要 toochange hello 密碼，此流程中。 
   
    ![補救](./media/active-directory-identityprotection-flows/121.png "補救")

## <a name="risky-sign-in-blocked"></a>已封鎖有風險的登入
系統管理員也可以選擇 tooset 時登入根據 hello 風險層級的登入風險原則 tooblock 使用者。 解除封鎖 tooget，使用者必須連絡系統管理員或技術服務人員，或嘗試從熟悉的位置或裝置登入。 藉由解決 Multi-Factor Authentication 自行復原，不是此種情況的適用選項。

![補救](./media/active-directory-identityprotection-flows/200.png "補救")

## <a name="compromised-account-recovery"></a>遭到入侵的帳戶復原
符合 hello 使用者的使用者設定使用者風險安全性原則之後，請風險 hello 原則中指定的層級 (而因此假設危害) 之前他們可以登入，必須經過 hello 使用者洩露復原流程。 

**hello 使用者洩露復原流程有三個步驟：**

1. hello 使用者會收到通知，他們的帳戶安全性有風險，因為可疑活動或外洩的認證。
   
    ![補救](./media/active-directory-identityprotection-flows/101.png "補救")
2. hello 使用者所解決的安全性挑戰是必要的 tooprove 其身分識別。 如果 hello 使用者已註冊的多重要素驗證它們可以自行復原而遭到危害。 他們必須 tooround 路線安全性程式碼 tootheir 電話號碼。 
   
   ![補救](./media/active-directory-identityprotection-flows/110.png "補救")
3. 最後，hello 使用者是強制的 toochange 他們的密碼，因為有其他人可能沒有存取 tootheir 帳戶。 
   這項體驗的螢幕擷取畫面如下。
   
   ![補救](./media/active-directory-identityprotection-flows/111.png "補救")

## <a name="compromised-account-blocked"></a>已封鎖遭到入侵的帳戶
tooget 解除封鎖使用者的風險安全性原則所封鎖的使用者，hello 使用者必須連絡管理員或服務台。 藉由解決 Multi-Factor Authentication 自行復原，不是此種情況的適用選項。

![補救](./media/active-directory-identityprotection-flows/104.png "補救")

## <a name="reset-password"></a>重設密碼
如果遭到入侵的使用者已遭封鎖而無法登入，系統管理員可以為其產生暫時密碼。 hello 使用者就能 toochange 密碼在下次登入。

![補救](./media/active-directory-identityprotection-flows/160.png "補救")

## <a name="see-also"></a>另請參閱
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md) 

