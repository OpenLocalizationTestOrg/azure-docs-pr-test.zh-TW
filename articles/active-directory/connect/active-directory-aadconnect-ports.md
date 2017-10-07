---
title: "混合式身分識別所需的連接埠和通訊協定 - Azure | Microsoft Docs"
description: "此頁面是必要的 toobe 開啟以供 Azure AD Connect 的連接埠的技術參考頁面"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: de97b225-ae06-4afc-b2ef-a72a3643255b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 9c62b74b45e7f266e3a55baa2db07a9ff1c9c6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-required-ports-and-protocols"></a>混合式身分識別所需的連接埠和通訊協定
下列文件的 hello 是 hello 所需的連接埠和通訊協定實作混合式身分識別解決方案上的技術參考。 使用下列圖例 hello 和 toohello 對應資料表，請參閱。

![何謂 Azure AD Connect](./media/active-directory-aadconnect-ports/required3.png)

## <a name="table-1---azure-ad-connect-and-on-premises-ad"></a>表 1 - Azure AD Connect 和內部部署 AD
下表說明 hello 連接埠和 hello Azure AD Connect 的伺服器之間通訊所需的通訊協定，並在內部部署 AD。

| 通訊協定 | 連接埠 | 說明 |
| --- | --- | --- |
| DNS |53 (TCP/UDP) |Hello 目的地樹系上的 DNS 查閱。 |
| Kerberos |88 (TCP/UDP) |Kerberos 驗證 toohello AD 樹系。 |
| MS-RPC |135 (TCP/UDP) |Hello hello Azure AD Connect 精靈時，它會繫結 toohello AD 樹系中，初始設定期間，密碼同步處理期間使用。 |
| LDAP |389 (TCP/UDP) |用於從 AD 匯入資料。 資料會使用「Kerberos 簽章及密封」加密。 |
| RPC | 445 (TCP/UDP) |使用無縫式 SSO toocreate hello AD 樹系中的電腦帳戶。 |
| LDAP/SSL |636 (TCP/UDP) |用於從 AD 匯入資料。 簽署及加密 hello 資料傳輸。 只有使用 SSL 時才會使用。 |
| RPC |49152- 65535 (隨機高 RPC 連接埠)(TCP/UDP) |密碼同步化和 hello 時它會繫結 toohello AD 樹系中，Azure AD connect 的初始設定期間，會使用它。 如需詳細資訊，請參閱 [KB929851](https://support.microsoft.com/kb/929851)、[KB832017](https://support.microsoft.com/kb/832017) 和 [KB224196](https://support.microsoft.com/kb/224196)。 |

## <a name="table-2---azure-ad-connect-and-azure-ad"></a>表 2 - Azure AD Connect 和 Azure AD
下表描述 hello 連接埠和通訊協定所需的 hello Azure AD Connect 的伺服器與 Azure AD 之間的通訊。

| 通訊協定 | 連接埠 | 說明 |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |使用 toodownload （憑證撤銷清單） 的 Crl tooverify SSL 憑證。 |
| HTTPS |443(TCP/UDP) |使用 Azure AD 與 toosynchronize。 |

如需清單的 Url 和 IP 位址，您需要 tooopen 在防火牆中，請參閱[Office 365 Url 與 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)。

## <a name="table-3---azure-ad-connect-and-ad-fs-federation-serverswap"></a>表 3 - Azure AD Connect 和 AD FS 同盟伺服器/WAP
下表描述 hello 連接埠和通訊協定所需的 hello Azure AD Connect 的伺服器和 AD FS 同盟/WAP 伺服器之間通訊。  

| 通訊協定 | 連接埠 | 說明 |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |使用 toodownload （憑證撤銷清單） 的 Crl tooverify SSL 憑證。 |
| HTTPS |443(TCP/UDP) |使用 Azure AD 與 toosynchronize。 |
| WinRM |5985 |WinRM 接聽程式 |

## <a name="table-4---wap-and-federation-servers"></a>表 4 - WAP 和同盟伺服器
下表描述 hello 連接埠和通訊協定所需的 hello 同盟伺服器和 WAP 伺服器之間通訊。

| 通訊協定 | 連接埠 | 說明 |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |用於進行驗證。 |

## <a name="table-5---wap-and-users"></a>表 5 - WAP 和使用者
下表描述 hello 連接埠和通訊協定所需的使用者與 hello WAP 伺服器之間的通訊。

| 通訊協定 | 連接埠 | 說明 |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |用於裝置驗證。 |
| TCP |49443 (TCP) |用於憑證驗證。 |

## <a name="table-6a--6b---pass-through-authentication-with-single-sign-on-sso-and-password-hash-sync-with-single-sign-on-sso"></a>表 6a 和 6b - 傳遞驗證搭配單一登入 (SSO) 與密碼雜湊同步處理搭配單一登入 (SSO)
hello 下表描述 hello 連接埠和通訊協定所需的 hello Azure AD Connect 與 Azure AD 之間的通訊。

### <a name="table-6a---pass-through-authentication-with-sso"></a>表 6a - 傳遞驗證搭配 SSO
|通訊協定|連接埠號碼|說明
| --- | --- | ---
|HTTP|80|為安全性驗證 (例如 SSL) 啟用輸出 HTTP 流量。 也需要 hello 連接器的自動更新功能 toofunction 正確。
|HTTPS|443| 啟用作業，例如啟用和停用的 hello 功能、 註冊連接器、 下載連接器更新和處理所有使用者登入要求的輸出 HTTPS 流量。

此外，Azure AD Connect 必須 toobe 無法 toomake 直接 IP 連線 toohello [Azure 資料中心 IP 範圍](https://www.microsoft.com/en-us/download/details.aspx?id=41653)。

### <a name="table-6b---password-hash-sync-with-sso"></a>表 6b - 密碼雜湊同步處理搭配 SSO

|通訊協定|連接埠號碼|說明
| --- | --- | ---
|HTTPS|443| 啟用 SSO 註冊 （只有需要 hello SSO 註冊程序）。

此外，Azure AD Connect 必須 toobe 無法 toomake 直接 IP 連線 toohello [Azure 資料中心 IP 範圍](https://www.microsoft.com/en-us/download/details.aspx?id=41653)。 同樣地，這是只有所需的 hello SSO 註冊程序。

## <a name="table-7a--7b---azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>表 7a 和 7b - 適用於 (AD FS/Sync) 和 Azure AD 的 Azure AD Connect Health 代理程式
hello 下列表格說明 hello 端點、 連接埠，以及 Azure AD Connect Health 代理程式與 Azure AD 之間的通訊所需的通訊協定

### <a name="table-7a---ports-and-protocols-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>表 7a - 適用於 (AD FS/Sync) 和 Azure AD 的 Azure AD Connect Health 代理程式的連接埠和通訊協定
下表描述 hello 下列輸出連接埠和通訊協定所需的 hello Azure AD Connect Health 代理程式與 Azure AD 之間的通訊。  

| 通訊協定 | 連接埠 | 說明 |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |輸出 |
| Azure 服務匯流排 |5671 (TCP/UDP) |輸出 |

### <a name="7b---endpoints-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>7b - 適用於 (AD FS/Sync) 和 Azure AD 之 Azure AD Connect Health 代理程式的端點
如需端點的清單，請參閱[hello hello Azure AD Connect Health 代理程式的需求 > 一節](../connect-health/active-directory-aadconnect-health-agent-install.md#requirements)。

