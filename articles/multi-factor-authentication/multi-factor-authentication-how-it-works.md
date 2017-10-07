---
title: "aaaAzure Multi-factor Authentication 的運作方式"
description: "Azure Multi-factor Authentication 協助保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。 它藉由要求第二種形式的驗證提供額外的安全性，並透過一系列簡單的驗證選項提供增強式驗證。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a>Azure Multi-Factor Authentication 的作用
hello 的雙步驟驗證的安全性在於其分層方法。 使用多重驗證因素會為攻擊者帶來相當程度的挑戰。 即使攻擊者設法 toolearn hello 使用者的密碼，它是裝置的毫無用處也不用擁有 hello 信任。 

![Proofup](./media/multi-factor-authentication-how-it-works/howitworks.png)

Azure Multi-factor Authentication 協助保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。  它藉由要求第二種形式的驗證提供額外的安全性，並透過一系列簡單的驗證選項提供增強式驗證。


## <a name="methods-available-for-two-step-verification"></a>雙步驟驗證適用的方法
當使用者登入時，額外的驗證傳送 toohello 使用者。  hello 下面是可以用於這個第二個驗證方法的清單。

| 驗證方法 | 說明 |
| --- | --- |
| 撥打電話 |通話時會 tooa 使用者已註冊的電話。 hello 使用者輸入 PIN，如有必要，然後按下 hello # 鍵。 |
| 簡訊 |Tooa 使用者的行動電話，以六位數代碼時，就會傳送簡訊。 hello 使用者 hello 登入頁面上，輸入此代碼。 |
| 行動應用程式通知 |驗證要求會傳送 tooa 使用者的智慧型手機。 hello 使用者輸入 PIN，如有必要，以選取**確認**hello 行動裝置應用程式上。 |
| 行動應用程式驗證碼 |hello 行動裝置應用程式，在使用者的智慧型手機上執行，會顯示驗證碼，以變更每隔 30 秒。 hello 使用者尋找 hello 最新的程式碼，並進入 hello 登入頁面上。 |
| 協力廠商 OATH 權杖 | Azure Multi-factor Authentication Server 可以設定的 tooaccept 協力廠商驗證方法。 |

Azure Multi-Factor Authentication 為雲端與伺服器提供可選取的驗證方法。 您可以選擇可供使用者使用的方法：撥打電話、簡訊、應用程式通知或應用程式驗證碼。 如需詳細資訊，請參閱 [可選取的驗證方法](multi-factor-authentication-whats-next.md#selectable-verification-methods)。

## <a name="next-steps"></a>後續步驟

- 了解不同的 hello[版本和 Azure Multi-factor Authentication 的耗用量方法](multi-factor-authentication-versions-plans.md)

- 選擇是否 toodeploy Azure MFA [hello 雲端或內部部署中](multi-factor-authentication-get-started.md)

- 閱讀[常見問題](multi-factor-authentication-faq.md)的解答