---
title: "aaaConfigure hello Azure MFA NPS 擴充功能 |Microsoft 文件"
description: "安裝 hello NPS 擴充功能之後，請使用下列步驟進行進階設定，例如 IP 允許清單和 UPN 取代。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: c3aed077b23c95f874861eb00c8e6dca668329c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-options-for-hello-nps-extension-for-multi-factor-authentication"></a>進階組態選項的 hello NPS 擴充功能的多重要素驗證

hello 網路原則伺服器 (NPS) 延伸模組會延伸到您在內部部署基礎結構的雲端型 Azure Multi-factor Authentication 功能。 本文假設您已擁有 hello 擴充功能安裝，而想的 tooknow toocustomize hello 延伸模組，您需要的方式。 

## <a name="alternate-login-id"></a>替代登入識別碼

因為 hello NPS 擴充連接 tooboth，您的內部部署和雲端目錄，您可能會遇到的問題，您在內部部署使用者主體名稱 (Upn) 不符 hello hello 雲端中的名稱。 toosolve 這個問題，請使用替代登入識別碼。 

內 hello NPS 擴充功能，您可以指定用來取代 hello UPN Azure Multi-factor Authentication Server 的 Active Directory 屬性 toobe。 這可讓您 tooprotect 雙步驟驗證您的內部資源而不需修改內部部署 Upn。 

tooconfigure 替代登入識別碼，跳過`HKLM\SOFTWARE\Microsoft\AzureMfa`和編輯下列登錄值的 hello:

| 名稱 | 類型 | 預設值 | 說明 |
| ---- | ---- | ------------- | ----------- |
| LDAP_ALTERNATE_LOGINID_ATTRIBUTE | 字串 | 空白 | 將指定 hello 屬性名稱的 Active Directory 的 toouse 而不是 hello UPN。 這個屬性用做 hello AlternateLoginId 屬性。 如果此登錄值設定 tooa[有效的 Active Directory 屬性](https://msdn.microsoft.com/library/ms675090.aspx)（適用於例如郵件或 displayName），然後 hello 屬性的值用來取代 hello 使用者的 UPN 來進行驗證。 如果此登錄值是空的或不設定，則會停用 AlternateLoginId 而且 hello 使用者的 UPN 會用於驗證。 |
| LDAP_FORCE_GLOBAL_CATALOG | 布林值 | False | 使用這個旗標 tooforce hello 通用類別目錄的 LDAP 搜尋時查閱 AlternateLoginId。 將網域控制站設定為通用類別目錄中，加入 hello AlternateLoginId 屬性 toohello 通用類別目錄，然後再啟用 此旗標。 <br><br> 如果 LDAP_LOOKUP_FORESTS 設定 （不是空白），**這個旗標會強制執行為 true**，不論 hello hello 登錄設定值。 在此情況下，hello NPS 擴充功能需要 hello 通用類別目錄 toobe 設有 hello AlternateLoginId 屬性，每個樹系。 |
| LDAP_LOOKUP_FORESTS | 字串 | 空白 | 提供樹系 toosearch 以分號分隔的清單。 例如，*contoso.com;foobar.com*。如果設定此登錄值，hello NPS 擴充反覆 hello 順序中所列的人員，並傳回 hello 第一個成功 AlternateLoginId 值搜尋所有 hello 樹系。 如果未設定此登錄值，hello AlternateLoginId 查閱是局部的 toohello 目前網域。|

tootroubleshoot 問題與替代登入識別碼，使用建議的步驟 hello[替代登入識別碼的錯誤](multi-factor-authentication-nps-errors.md#alternate-login-id-errors)。

## <a name="ip-exceptions"></a>IP 例外狀況

如果您需要 toomonitor 伺服器可用性，例如負載平衡器如果確認哪一部伺服器在執行之前傳送工作負載，您不想封鎖的驗證要求這些檢查 toobe。 相反地，建立一份您知道服務帳戶所使用的 IP 位址清單，並停用該清單的 Multi-Factor Authentication 需求。 

tooconfigure IP 白名單，跳過`HKLM\SOFTWARE\Microsoft\AzureMfa`並設定下列登錄值的 hello: 

| 名稱 | 類型 | 預設值 | 說明 |
| ---- | ---- | ------------- | ----------- |
| IP_WHITELIST | 字串 | 空白 | 提供 IP 位址清單 (以分號分隔)。 包括 hello IP 位址的服務要求產生的位置，像是 hello NAS/VPN 伺服器的電腦。 不支援 IP 範圍和子網路。 <br><br> 例如，*10.0.0.1;10.0.0.2;10.0.0.3*。

當要求進入從存在於 hello 白名單 IP 位址時，則會略過雙步驟驗證。 hello IP 白名單是比較的 toohello IP 位址中的 hello 提供*ratNASIPAddress* hello RADIUS 要求的屬性。 如果 RADIUS 要求進入沒有 hello ratNASIPAddress 屬性，則會記錄下列警告 hello:"P_WHITE_LIST_WARNING::IP 白名單忽略因為 NasIpAddress 屬性中的 RADIUS 要求中遺漏來源 IP。 」

## <a name="next-steps"></a>後續步驟

[針對 Azure Multi-factor Authentication 解決 hello NPS 擴充功能中的錯誤訊息](multi-factor-authentication-nps-errors.md)
