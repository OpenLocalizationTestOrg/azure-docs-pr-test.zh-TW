---
title: "Azure AD Connect 同步： 如何 toomanage hello Azure AD 服務帳戶 |Microsoft 文件"
description: "本主題將說明如何 toorestore hello Azure AD 服務帳戶。"
services: active-directory
keywords: "如何 tooreset hello 密碼 AADSTS70002、 AADSTS50054，hello Azure AD Connect 同步處理連接器服務帳戶"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a>Azure AD Connect 同步： 如何 toomanage hello Azure AD 服務帳戶
hello hello Azure AD 連接器所使用的服務帳戶應該 toobe 服務可用。 如果您需要 tooreset 其認證，本主題是供您。 例如，如果錯誤重設 hello 密碼 hello 服務帳戶使用 PowerShell，在具有全域管理員。

## <a name="reset-hello-credentials"></a>重設 hello 認證
如果 hello hello Azure AD 連接器上定義的服務帳戶無法聯繫 tooauthentication 問題原因的 Azure AD，hello 密碼可以重設。

1. 登入 toohello Azure AD Connect 同步處理伺服器，並啟動 PowerShell。
2. 執行 `Add-ADSyncAADServiceAccount`。  
   ![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)
3. 提供 Azure AD 全域管理員認證。

此 cmdlet 會重設 hello hello 服務帳戶的密碼，並在 Azure AD 和 hello 同步處理引擎中更新它。

## <a name="known-issues-these-steps-can-solve"></a>這些步驟可以解決的已知問題
本節是一份 hello Azure AD 服務帳戶上重設認證已修正客戶所報告的錯誤。

- - -
事件 6900  
hello 伺服器處理密碼變更通知時發生未預期的錯誤：  
AADSTS70002︰驗證認證時發生錯誤。 AADSTS50054︰使用舊密碼進行驗證。

- - -
事件 659  
擷取密碼原則同步處理設定時發生錯誤。 Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException：  
AADSTS70002︰驗證認證時發生錯誤。 AADSTS50054︰使用舊密碼進行驗證。

## <a name="next-steps"></a>後續步驟
**概觀主題**

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

