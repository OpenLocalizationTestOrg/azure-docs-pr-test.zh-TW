---
title: "aaaAzure AD 連線的健全狀況版本歷程記錄"
description: "本文件說明 Azure AD Connect Health 和已包含在這些版本中的 hello 版本。"
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 8dd4e998-747b-4c52-b8d3-3900fe77d88f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: a583263e412f5da9af75947f3431de2494042388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-version-release-history"></a>Azure AD Connect Health︰版本發行歷程記錄
hello Azure Active Directory 團隊會定期更新 Azure AD Connect Health 的新特色與功能。 本文列出 hello 版本與已發行的功能。

## <a name="october-2016"></a>2016 年 10 月
**代理程式更新：**

* 適用於 AD FS 的 Azure AD Connect Health 代理程式 \(2.6.408.0 版\)
  1. 改進在驗證要求中偵測用戶端 IP 位址
  2. Bug 修正相關 tooAlerts
* 適用於 AD FS 的 Azure AD Connect Health 代理程式 (2.6.408.0 版)
  1. Bug 修正相關 tooAlerts。
* 隨著 Azure AD Connect 1.1.281.0 版發行的 Azure AD Connect Health Agent for Sync (2.6.353.0 版)
  1. Hello 同步處理錯誤報表提供所需的 hello 資料
  2. Bug 修正相關 tooAlerts

**新的預覽功能：**

* Azure AD Connect 的同步處理錯誤報告

**新功能︰**

* Azure AD Connect Health 的 AD FS 的 IP 位址 欄位是不正確的使用者名稱/密碼的前 50 位使用者有關的 hello 報表中可用。

## <a name="july-2016"></a>2016 年 7 月
**新的預覽功能：**

* [適用於 AD DS 的 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)。

## <a name="january-2016"></a>2016 年 1 月
**代理程式更新：**

* 適用於 AD FS 的 Azure AD Connect Health 代理程式 (2.6.91.1512 版)

**新功能︰**

* [Azure AD Connect Health 代理程式的測試連線工具](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)

## <a name="november-2015"></a>2015 年 11 月
**新功能︰**

* 支援 [角色型存取控制](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)

**新的預覽功能：**

* [適用於同步的 Azure AD Connect Health](active-directory-aadconnect-health-sync.md)。

**已修正的問題：**

* 針對代理程式註冊期間看到的錯誤進行修正。

## <a name="september-2015"></a>2015 年 9 月
**新功能︰**

* AD FS 的錯誤使用者名稱密碼報告
* 支援 tooconfigure Unauthenticated HTTP Proxy
* 在 Server core 上支援 tooconfigure 代理程式
* AD FS 的改進 tooAlerts
* 在適用於 AD FS 的 Azure AD Connect Health 代理程式中改善連線和資料上傳。

**已修正的問題：**

* AD FS 使用量詳細資料錯誤類型的錯誤修正。

## <a name="june-2015"></a>2015 年 6 月
**適用於 AD FS 和 AD FS Proxy 的 Azure AD Connect Health 初始版本。**

**新功能︰**

* 監視 AD FS 與 AD FS Proxy 伺服器時以電子郵件通知發出警示。
* 輕鬆存取 tooAD FS 拓撲和 AD FS 效能計數器中的模式。
* 依應用程式、驗證方法、要求網路位置等分組，顯示 AD FS 伺服器上成功權杖要求的趨勢。
* 依應用程式、錯誤類型等分組，顯示 AD FS 伺服器上失敗要求的趨勢。
* 使用 Azure AD 全域管理員認證更輕鬆部署代理程式。  

## <a name="next-steps"></a>後續步驟
深入了解[監視您內部部署識別基礎結構和同步處理雲端中的服務 hello](active-directory-aadconnect-health.md)。

