---
title: "位於防火牆後方 aaaAccess 金鑰保存庫 |Microsoft 文件"
description: "了解如何 tooaccess Azure 金鑰保存庫位於防火牆後方的應用程式"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: ab4bb0c27a41fef878a20dace6cab203df04e579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>在防火牆後存取 Azure 金鑰保存庫
### <a name="q-my-key-vault-client-application-needs-toobe-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-tooenable-access-tooa-key-vault"></a>問： 我的金鑰保存庫用戶端應用程式需要在防火牆後面的 toobe。 哪些連接埠、 主機或 IP 位址應該開啟 tooenable 存取 tooa 金鑰保存庫？
tooaccess 金鑰保存庫，用戶端應用程式金鑰保存庫有 tooaccess 多個端點的各種不同功能：

* 透過 Azure Active Directory (Azure AD) 進行的驗證。
* Azure 金鑰保存庫的管理。 這包括透過 Azure Resource Manager 建立、讀取、更新、刪除和設定存取原則。
* 存取和管理物件 （金鑰和密碼） 本身儲存在金鑰保存庫中，瀏覽 hello 金鑰保存庫特定端點 (例如， [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net))。  

視您的組態和環境而定，會有一些變化。   

## <a name="ports"></a>連接埠
所有流量 tooa 金鑰保存庫的所有三個函式 （驗證、 管理和資料飛機存取） 都會透過 HTTPS： 通訊埠 443。 不過，偶爾會有 CRL 的 HTTP (連接埠 80) 流量。 支援 OCSP 的用戶端不應該觸達 CRL，但可能偶爾會觸達 [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl)。  

## <a name="authentication"></a>驗證
金鑰保存庫用戶端應用程式需要 tooaccess Azure Active Directory 端點進行驗證。 hello 端點是用定 hello Azure AD 租用戶的組態，主體 （使用者主體或服務主體） 和 hello hello 類型輸入的帳戶-例如，Microsoft 帳戶或工作或學校帳戶。  

| 主體類型 | 端點:連接埠 |
| --- | --- |
| 使用 Microsoft 帳戶的使用者<br> (例如， user@hotmail.com) |**全域：**<br> login.microsoftonline.com:443<br><br> **Azure 中國︰**<br> login.chinacloudapi.cn:443<br><br>**Azure 美國政府︰**<br> login-us.microsoftonline.com:443<br><br>**Azure 德國︰**<br> login.microsoftonline.de:443<br><br> 和 <br>login.live.com:443 |
| 使用者或服務主體與 Azure AD 中使用工作或學校帳戶 (例如， user@contoso.com) |**全域：**<br> login.microsoftonline.com:443<br><br> **Azure 中國︰**<br> login.chinacloudapi.cn:443<br><br>**Azure 美國政府︰**<br> login-us.microsoftonline.com:443<br><br>**Azure 德國︰**<br> login.microsoftonline.de:443 |
| 使用者或服務主體使用工作或學校帳戶，再加上 Active Directory Federation Services (AD FS) 或其他同盟的端點 (例如， user@contoso.com) |公司帳戶或學校帳戶的所有端點，加上 AD FS 或其他同盟端點 |

還有其他可能的複雜案例。 請參閱太[Azure Active Directory 驗證流程](/documentation/articles/active-directory-authentication-scenarios/)，[整合應用程式與 Azure Active Directory](/documentation/articles/active-directory-integrating-applications/)，和[Active Directory 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn151124.aspx)如需詳細資訊。  

## <a name="key-vault-management"></a>金鑰保存庫管理
金鑰保存庫管理 （CRUD 並設定存取原則），hello 金鑰保存庫用戶端應用程式需要 tooaccess Azure 資源管理員端點。  

| 作業類型 | 端點:連接埠 |
| --- | --- |
| 透過 Azure Resource Manager 的<br> 金鑰保存庫控制項面作業 |**全域：**<br> management.azure.com:443<br><br> **Azure 中國︰**<br> management.chinacloudapi.cn:443<br><br> **Azure 美國政府︰**<br> management.usgovcloudapi.net:443<br><br> **Azure 德國︰**<br> management.microsoftazure.de:443 |
| Azure Active Directory 圖形 API |**全域：**<br> graph.windows.net:443<br><br> **Azure 中國︰**<br> graph.chinacloudapi.cn:443<br><br> **Azure 美國政府︰**<br> graph.windows.net:443<br><br> **Azure 德國︰**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>金鑰保存庫作業
對於所有金鑰保存庫物件 （金鑰和密碼） 管理與密碼編譯作業，hello 金鑰保存庫用戶端必須 tooaccess hello 金鑰保存庫端點。 hello 端點 DNS 尾碼的金鑰保存庫的 hello 位置而有所不同。 hello 金鑰保存庫端點是否為 hello 格式*保存庫名稱*。*區域特定的 dns 尾碼*、 hello 下表中所述。  

| 作業類型 | 端點:連接埠 |
| --- | --- |
| 包括金鑰的密碼編譯作業在內的作業；建立、讀取、更新和刪除金鑰與密碼；對金鑰保存庫物件 (金鑰或密碼) 設定或取得標籤和其他屬性 |**全域：**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure 中國︰**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure 美國政府︰**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure 德國︰**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>IP 位址範圍
hello 金鑰保存庫服務會使用其他 Azure 資源，例如 PaaS 基礎結構。 如此就不可能 tooprovide 特定 IP 位址範圍，服務端點會有任何特定時間的金鑰保存庫。 如果您的防火牆支援 IP 位址範圍，請參閱 toohello [Microsoft Azure Datacenter IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)文件。 驗證和身分識別 (Azure Active Directory)，您的應用程式必須能夠 tooconnect toohello 端點中所述[驗證和身分識別位址](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)。

## <a name="next-steps"></a>後續步驟
如果您有金鑰保存庫相關的問題，請瀏覽 hello [Azure 金鑰保存庫論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)。

