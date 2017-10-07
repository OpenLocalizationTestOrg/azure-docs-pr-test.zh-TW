---
title: "需在 Azure MFA 的兩步驟驗證 aaaLearn |Microsoft 文件"
description: "什麼是 Azure multi-factor Authentication，為什麼要使用 MFA，hello multi-factor Authentication 用戶端以及 hello 不同的方法和版本的詳細資訊。 "
keywords: "簡介 tooMFA，mfa 概觀、 何謂 mfa"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a>什麼是 Azure Multi-Factor Authentication？
雙步驟驗證是驗證的需要一個以上的驗證方法，並將重要的第二層安全性 toouser 登入和交易方法。 其運作方式是要求任何兩個或多個下列驗證方法的 hello:

* 您知道的某些資訊 (通常是密碼)
* 您擁有的某些東西 (不容易輕易複製的信任裝置，例如電話)
* 您身上的某些特徵 (生物識別技術)

<center>![使用者名稱和密碼](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![憑證](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![智慧型手機](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![智慧卡](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![虛擬智慧卡](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![使用者名稱和密碼](./media/multi-factor-authentication/cert.png)</center>

Azure Multi-Factor Authentication (MFA) 是 Microsoft 的雙步驟驗證解決方案。 Azure MFA 有助於保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。 它可以透過一些驗證方法 (包括電話、文字訊息，或行動應用程式驗證) 來提供強大的驗證功能。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a>為何使用 Azure Multi-Factor Authentication？
與以前比較起來，現今人們連線網路的時間越來越長。 智慧型手機、 平板電腦、 膝上型電腦和電腦的人有如何將 tooconnect 並隨時保持連線的幾個不同選項。 人們可以從任何地方存取他們的帳戶與應用程式，這表示他們可以完成更多工作並為客戶提供更好的服務。

Azure Multi-factor Authentication 是簡單 toouse，可擴充、 可靠的解決方案，以及提供驗證第二種方法讓您的使用者永遠會受到保護。

| ![輕鬆 tooUse](./media/multi-factor-authentication/simple.png) | ![可調整](./media/multi-factor-authentication/scalable.png) | ![永遠受到保護](./media/multi-factor-authentication/protected.png) | ![可靠](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| **輕鬆 toouse** |**可調整** |**永遠受到保護** |**可靠** |

* **輕鬆 tooUse** -Azure Multi-factor Authentication 是簡單 tooset 註冊和使用。 hello 額外的保護，隨附於 Azure Multi-factor Authentication Server 可讓使用者 toomanage 自己的裝置。 最棒的是，在許多情況下，只需簡單按幾下滑鼠即可進行設定。
* **可擴充**-Azure Multi-factor Authentication 使用 hello 雲端的 hello 電源，並整合與您內部部署 AD 和自訂應用程式。 這項保護甚至會擴充 tooyour 高容量的關鍵任務的案例。
* **永遠會受到保護**-Azure Multi-factor Authentication 提供使用 hello 最高的業界標準的強式驗證。
* **可靠** - 我們保證 Azure Multi-Factor Authentication 的可用性可達到 99.9%。 hello 服務會被視為無法使用時無法 tooreceive 或處理序的 hello 雙步驟驗證的驗證要求。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a>後續步驟

- 深入了解 [Azure Multi-Factor Authentication 的作用](multi-factor-authentication-how-it-works.md)

- 了解不同的 hello[版本和 Azure Multi-factor Authentication 的耗用量方法](multi-factor-authentication-versions-plans.md)
