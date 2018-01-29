---
title: "Azure AD Connect Health 版本歷程記錄"
description: "本文件說明 Azure AD Connect Health 的版本和已包含在這些版本中的功能。"
services: active-directory
documentationcenter: 
author: karavar
manager: mtillman
editor: curtand
ms.assetid: 8dd4e998-747b-4c52-b8d3-3900fe77d88f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: b43eb5e78b70f38226e3e8cb53d1530d348c7c20
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="azure-ad-connect-health-version-release-history"></a>Azure AD Connect Health︰版本發行歷程記錄
Azure Active Directory 團隊會定期以新的特性和功能更新 Azure AD Connect Health。 本文列出已發行的版本和功能。

## <a name="december-2017"></a>2017 年 12 月
**代理程式更新：**

*   適用於 AD DS 的 Azure AD Connect Health 代理程式 (3.0.145.0 版)
  1. 代理程式可用性改善 
  2. 已新增新的代理程式疑難排解命令
  3. Bug 修正和一般改善
*   適用於 AD FS 的 Azure AD Connect Health 代理程式 (3.0.145.0 版)
  1. 已新增新的代理程式疑難排解命令
  2. 代理程式可用性改善 
  3. Bug 修正和一般改善
  
## <a name="october-2017"></a>2017 年 10 月
**代理程式更新：**

 * 隨著 Azure AD Connect 1.1.649.0 版發行的 Azure AD Connect Health Agent for Sync (3.0.129.0 版)
<br></br> 已修正 Azure AD Connect 與 Azure AD Connect Health Agent for Sync 之間的版本相容性問題。此問題會影響要執行 Azure AD Connect 就地升級到 1.1.647.0 版，但目前擁有的是健康情況代理程式 3.0.127.0 版的客戶。 升級之後，健康情況代理程式就不會再將有關 Azure AD Connect 同步處理服務的健康情況資料傳送至 Azure AD 健康情況服務。 透過此修正，就會在 Azure AD Connect 就地升級期間安裝健康情況代理程式 3.0.129.0 版。 健康情況代理程式 3.0.129.0 版與 Azure AD Connect 1.1.649.0 版 沒有相容性問題。

## <a name="july-2017"></a>2017 年 7 月
**代理程式更新：**

*   適用於 AD DS 的 Azure AD Connect Health 代理程式 (3.0.68.0 版)
  1. Bug 修正和一般改善
  2. Sovereign 雲端支援
*   適用於 AD FS 的 Azure AD Connect Health 代理程式 (3.0.68.0 版)
  1. Bug 修正和一般改善
  2. Sovereign 雲端支援
* 隨著 Azure AD Connect 1.1.614.0 版發行的 Azure AD Connect Health Agent for Sync (3.0.68.0 版)
1. Microsoft Azure Government Cloud 和 Microsoft Cloud Germany 的支援

## <a name="april-2017"></a>2017 年 4 月      
**代理程式更新：**

*   適用於 AD FS 的 Azure AD Connect Health 代理程式 (3.0.12.0 版)
  1. Bug 修正和一般改善
*   適用於 AD DS 的 Azure AD Connect Health 代理程式 (3.0.12.0 版)
  1. 效能計數器上傳改善
  2. Bug 修正和一般改善

## <a name="october-2016"></a>2016 年 10 月
**代理程式更新：**

* 適用於 AD FS 的 Azure AD Connect Health 代理程式 \(2.6.408.0 版\)
1. 改進在驗證要求中偵測用戶端 IP 位址
2. 與警示相關的錯誤修正
* 適用於 AD FS 的 Azure AD Connect Health 代理程式 (2.6.408.0 版)
1. 與警示相關的錯誤修正。
* 隨著 Azure AD Connect 1.1.281.0 版發行的 Azure AD Connect Health Agent for Sync (2.6.353.0 版)
1. 提供同步處理錯誤報告所需的資料
2. 與警示相關的錯誤修正

**新的預覽功能：**

* Azure AD Connect 的同步處理錯誤報告

**新功能︰**

* 適用於 AD FS 的 Azure AD Connect Health - IP 位址欄位可用於報告中大約前 50 位使用者名稱/密碼不正確的使用者。

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
* 支援設定未經驗證的 HTTP Proxy
* 支援在伺服器核心上設定代理程式
* 改善 AD FS 的警示
* 在適用於 AD FS 的 Azure AD Connect Health 代理程式中改善連線和資料上傳。

**已修正的問題：**

* AD FS 使用量詳細資料錯誤類型的錯誤修正。

## <a name="june-2015"></a>2015 年 6 月
**適用於 AD FS 和 AD FS Proxy 的 Azure AD Connect Health 初始版本。**

**新功能︰**

* 監視 AD FS 與 AD FS Proxy 伺服器時以電子郵件通知發出警示。
* 在 AD FS 效能計數器中輕鬆存取 AD FS 拓撲和模式。
* 依應用程式、驗證方法、要求網路位置等分組，顯示 AD FS 伺服器上成功權杖要求的趨勢。
* 依應用程式、錯誤類型等分組，顯示 AD FS 伺服器上失敗要求的趨勢。
* 使用 Azure AD 全域管理員認證更輕鬆部署代理程式。  

## <a name="next-steps"></a>後續步驟
深入了解 [在雲端中監視內部部署身分識別基礎結構和同步處理服務](active-directory-aadconnect-health.md)。

