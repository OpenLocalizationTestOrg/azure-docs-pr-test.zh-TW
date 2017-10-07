---
title: "aaaUpgrade tooAzure AD 應用程式 Proxy |Microsoft 文件"
description: "如果您是從 Microsoft Forefront 或 Unified Access Gateway 升級，選擇哪一個 Proxy 解決方案最適合。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a>比較遠端存取解決方案

Azure Active Directory 應用程式 Proxy 是 Microsoft 提供的兩個遠端存取解決方案其中之一。 其他 hello 是 Web 應用程式 Proxy，hello 在內部部署版本。 這兩種解決方案取代 Microsoft 提供的舊版產品：Microsoft Forefront Threat Management Gateway (TMG) 和 Unified Access Gateway (UAG)。 使用此發行項 toounderstand 這些四個解決方案比較 tooeach 其他的方式。 您仍在使用 hello 取代 TMG 或 UAG 解決方案，請使用這個發行項 toohelp 計劃您的移轉 tooone 的 hello 應用程式 Proxy。 


## <a name="feature-comparison"></a>功能比較

使用此資料表 toounderstand Threat Management Gateway (TMG)、 統一存取閘道 (UAG)、 Web 應用程式 Proxy (WAP) 和 Azure AD 應用程式 Proxy (AP) 比較 tooeach 其他。

| 功能 | TMG | UAG | WAP | AP |
| ------- | --- | --- | --- | --- |
| 憑證驗證 | 是 | 是 | - | - |
| 選擇性地發佈瀏覽器應用程式 | 是 | 是 | 是 | 是 |
| 預先驗證和單一登入 | 是 | 是 | 是 | 是 | 
| 第 2 層/第 3 層防火牆 | 是 | 是 | - | - |
| 轉接 Proxy 功能 | 是 | - | - | - |
| VPN 功能 | 是 | 是 | - | - |
| 豐富通訊協定支援 | - | 是 | 是，如果是透過 HTTP 執行 | 是，如果是透過 HTTP 或透過遠端桌面閘道執行 |
| 作為 ADFS Proxy 伺服器 | - | 是 | 是 | - |
| 應用程式存取的單一入口網站 | - | 是 | - | 是 |
| 回應內文連結轉譯 | 是 | 是 | - | 是 | 
| 使用標頭進行驗證 | - | 是 | - | 是，使用 PingAccess | 
| 雲端級別安全性 | - | - | - | 是 | 
| 條件式存取 | - | 是 | - | 是 |
| Hello 非軍事區域 (DMZ) 中沒有任何元件 | - | - | - | 是 |
| 沒有輸入連線 | - | - | - | 是 |

大部分情況下，我們建議 Azure AD 應用程式，做為 hello 現代解決方案。 Web 應用程式 Proxy 只建議用在需要 AD FS Proxy 伺服器的情節中，而且您無法使用 Azure Active Directory 中的自訂網域。 

Azure AD 應用程式 Proxy 提供唯一優勢在於，當比較 toosimilar 產品，包括：

- 擴充 Azure AD tooon 內部部署資源
   - 雲端級別安全性和保護
   - 條件式存取和多因素驗證等功能是簡單 tooenable
- 在 hello 非軍事區域中沒有 componenet
- 沒有所需的輸入連線
- 一個存取面板，您的使用者可以前往 toofor 所有其應用程式，包括 O365、 Azure AD 整合的 SaaS 應用程式，而您內部部署 web 應用程式。 


## <a name="next-steps"></a>後續步驟

- [使用 Azure AD 應用程式 tooprovide 安全遠端存取 tooon 內部部署應用程式](active-directory-application-proxy-get-started.md)
- [從 Forefront TMG 和 UAG tooApplication Proxy 轉換](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/)。
