---
title: "Azure AD Connect：必要條件與硬體 | Microsoft Docs"
description: "本主題說明 hello 先決條件和 Azure AD Connect 的 hello 硬體需求"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 91b88fda-bca6-49a8-898f-8d906a661f07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2ec8b5da9440c92e8f9d6702d5e5e20de952b588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-for-azure-ad-connect"></a>Azure AD Connect 的必要條件
本主題描述 hello 必要條件和 Azure AD Connect 的 hello 硬體需求。

## <a name="before-you-install-azure-ad-connect"></a>安裝 Azure AD Connect 之前
安裝 Azure AD Connect 之前，您需要注意一些事項。

### <a name="azure-ad"></a>Azure AD
* Azure 訂用帳戶或 [Azure 試用版訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)。 此訂用帳戶才需要存取 hello Azure 入口網站，且不會針對使用 Azure AD Connect。 如果您使用 PowerShell 或 Office 365，然後您不需要 Azure 訂用帳戶 toouse Azure AD Connect。 如果您有 Office 365 授權，您可以也使用 hello Office 365 入口網站。 與付費的 Office 365 授權，您也可以取得 hello 到 Azure 入口網站從 hello Office 365 入口網站。
  * 您也可以使用 hello [Azure 入口網站](https://portal.azure.com)。 此入口網站不需要 Azure AD 授權。
* [新增並驗證 hello 網域](../active-directory-domains-add-azure-portal.md)想 toouse 在 Azure AD 中。 比方說，如果您計劃 toouse contoso.com，為您的使用者，則請確定此網域已經過驗證，您不只使用 hello contoso.onmicrosoft.com 預設網域。
* Azure AD 租用戶預設允許 5 萬個物件。 當您驗證您的網域時，hello 限制是增加的 too300k 物件。 如果您需要更多的物件，在 Azure AD 中，您需要更進一步增加支援案例 toohave hello 限制 tooopen。 如果您需要 50 萬個以上的物件，您需要如 Office 365、Azure AD Basic、Azure AD Premium 或 Enterprise Mobility + Security 等授權。

### <a name="prepare-your-on-premises-data"></a>準備您的內部部署資料
* 使用[IdFix](https://support.office.com/article/Install-and-run-the-Office-365-IdFix-tool-f4bd2439-3e41-4169-99f6-3fabdfa326ac) tooidentify 錯誤，例如重複的項目和格式化您的目錄同步處理 tooAzure AD 和 Office 365 之前的問題。
* 檢閱 [您可在 Azure AD 中啟用的選用同步處理功能](active-directory-aadconnectsyncservice-features.md) ，並評估您應該啟用哪些功能。

### <a name="on-premises-active-directory"></a>內部部署 Active Directory
* hello AD 結構描述版本與樹系功能等級必須是 Windows Server 2003 或更新版本。 hello 網域控制站可以執行任何版本，只要符合 「 hello 結構描述和樹系層級的需求。
* 如果您計劃 toouse hello 功能**密碼回寫**，則 hello 網域控制站必須是 （具有最新的預存程序） 的 Windows Server 2008 或更新版本。 如果您的 DC 是 2008 (R2 之前)，則也必須套用 [Hotfix KB2386717](http://support.microsoft.com/kb/2386717)。
* 使用 Azure AD 的 hello 網域控制站必須是可寫入。 它是**不支援**toouse RODC （唯讀網域控制站） 與 Azure AD Connect 不符合任何寫入重新導向。
* 它是**不支援**toouse 內部部署樹系/網域使用 SLDs （單一標籤網域）。
* 它是**不支援**toouse 內部部署樹系/網域使用 「 點 」 (名稱包含句點"。")NetBios 名稱。
* 建議太[啟用 hello Active Directory 資源回收筒](active-directory-aadconnectsync-recycle-bin.md)。

### <a name="azure-ad-connect-server"></a>Azure AD Connect 伺服器
* Azure AD Connect 無法安裝至 Small Business Server 或 Windows Server Essentials。 hello 伺服器必須使用 Windows Server standard 或更高。
* hello Azure AD Connect 的伺服器必須有完整的 GUI 安裝。 它是**不支援**tooinstall 在 server core 上的。
* Azure AD Connect 必須安裝於 Windows Server 2008 或更新版本上。 此伺服器可以是網域控制站或成員伺服器 (使用快速設定時)。 如果您使用自訂設定，hello 伺服器也可以獨立，而且沒有 toobe tooa 聯結的網域。
* 如果您在 Windows Server 2008 或 Windows Server 2008 R2 上安裝 Azure AD Connect，則請確定 tooapply hello 最新的 hotfix，從 Windows Update。 hello 安裝不是能 toostart 與未修補的伺服器。
* 如果您計劃 toouse hello 功能**密碼同步化**，則 hello Azure AD Connect 的伺服器必須是 Windows Server 2008 R2 SP1 或更新版本。
* 如果您計劃 toouse**群組受管理的服務帳戶**，則 hello Azure AD Connect 的伺服器必須是 Windows Server 2012 或更新版本。
* hello Azure AD Connect 的伺服器必須擁有[.NET Framework 4.5.1](#component-prerequisites)或更新版本和[Microsoft PowerShell 3.0](#component-prerequisites)安裝或更新版本。
* hello Azure AD Connect 的伺服器必須沒有 PowerShell 文字記錄的群組原則管理。
* 如果部署 Active Directory Federation Services 時，安裝 AD FS 或 Web 應用程式 Proxy 的 hello 伺服器必須是 Windows Server 2012 R2 或更新版本。 [Windows 遠端管理](#windows-remote-management) ，才能執行遠端安裝。
* 如果部署的是 Active Directory 同盟服務，則您需要 [SSL 憑證](#ssl-certificate-requirements)。
* 如果正在部署 Active Directory Federation Services，則您需要 tooconfigure[名稱解析](#name-resolution-for-federation-servers)。
* 如果您的全域系統管理員啟用 MFA，然後 hello URL **https://secure.aadcdn.microsoftonline-p.com**必須在 hello 信任的網站清單。 您必須提示的 tooadd 之前並未將此站台 toohello 信任的網站清單中的 MFA 挑戰，並提示您時。 您可以使用 Internet Explorer tooadd 它 tooyour 信任的網站。

### <a name="sql-server-used-by-azure-ad-connect"></a>Azure AD Connect 使用的 SQL Server
* Azure AD Connect 需要 SQL Server 資料庫 toostore 識別資料。 預設會安裝 SQL Server 2012 Express LocalDB (SQL Server Express 的精簡版)。 SQL Server Express 有大小限制為 10GB，可讓您 toomanage 約 100,000 物件。 如果您需要 toomanage 更大量的目錄物件，您會需要 toopoint hello 安裝精靈 tooa 不同的 SQL Server 安裝。
* 如果您使用個別的 SQL Server，這些需求適用於：
  * Azure AD Connect 支援從 SQL Server 2008 （具有最新的 Service Pack) tooSQL Server 2016 SP1 的 Microsoft SQL Server 的所有版本。 **不支援** 使用 Microsoft Azure SQL Database 作為資料庫。
  * 您必須使用不區分大小寫的 SQL 定序。 這些定序是在其名稱中使用 \_CI_ 來識別。 它是**不支援**toouse 區分大小寫的定序中，由\_CS_ 其名稱中的。
  * 您在每個 SQL 執行個體中只能有一個同步引擎。 它是**不支援**tooshare SQL 執行個體與 FIM/MIM 同步、 DirSync 或 Azure AD Sync。

### <a name="accounts"></a>帳戶
* 您想使用 toointegrate hello Azure AD 租用戶的 Azure AD 全域管理員帳戶。 此帳戶必須是**學校或組織帳戶**，不能是 **Microsoft 帳戶**。
* 如果您使用快速設定或從 DirSync 升級，則必須具有本機 Active Directory 的企業系統管理員帳戶。
* [Active Directory 中的帳戶](active-directory-aadconnect-accounts-permissions.md)如果您使用 hello 自訂設定安裝路徑。

### <a name="connectivity"></a>連線能力
* hello Azure AD Connect 伺服器需要內部網路和網際網路的 DNS 解析。 hello DNS 伺服器必須能夠 tooresolve 命名 tooyour 內部 Active Directory 和 hello Azure AD 端點。
* 如果您的內部網路上有防火牆，而且需要 tooopen hello Azure AD Connect 的伺服器和網域控制站之間的連接埠，然後查看[Azure AD Connect 的連接埠](active-directory-aadconnect-ports.md)如需詳細資訊。
* 如果您的 proxy 或防火牆限制可存取的 Url，然後 hello 記載於 Url [Office 365 Url 與 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)必須開啟。
  * 如果您使用 hello 德國或 hello Microsoft Azure 政府雲端中的 Microsoft 雲端，則請參閱[Azure AD Connect 同步處理服務執行個體的考量](active-directory-aadconnect-instances.md)url。
* 預設使用 TLS 1.0 toocommunicate 與 Azure AD 為 azure AD Connect。 您可以變更此 tooTLS 1.2 中的 hello 步驟[啟用 TLS 1.2 的 Azure AD Connect](#enable-tls-12-for-azure-ad-connect)。
* 如果您使用輸出 proxy 連接 toohello 網際網路，hello 遵循 hello 中的設定**C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config**檔案必須新增 hello 安裝精靈Azure AD Connect 同步處理 toobe 無法 tooconnect toohello 網際網路和 Azure AD。 此文字必須在 hello hello 檔案最下方輸入。 在此程式碼， &lt;PROXYADRESS&gt;代表 hello 實際 proxy IP 位址或主機名稱。

```
    <system.net>
        <defaultProxy>
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* 如果您的 proxy 伺服器需要驗證，則 hello[服務帳戶](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account)必須定位在 hello 網域，而您必須使用自訂的 hello 設定安裝路徑 toospecify[自訂的服務帳戶](active-directory-aadconnect-get-started-custom.md#install-required-components). 您也需要不同的變更 toomachine.config。在 machine.config 中這項變更，與 hello 安裝精靈，並同步處理引擎回應 tooauthentication 要求 hello proxy 伺服器。 所有安裝精靈 頁面中，但不包括 hello**設定**頁面上，hello 登入使用者的認證會用。 在 hello**設定**結尾 hello hello 安裝精靈，hello 內容的頁面是交換的 toohello[服務帳戶](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account)您所建立。 hello machine.config 區段應如下所示。

```
    <system.net>
        <defaultProxy enabled="true" useDefaultCredentials="true">
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* 當 Azure AD Connect 目錄同步作業的一部分傳送 web 要求 tooAzure AD 時，Azure AD 可能佔用 too5 分鐘 toorespond。 很常見的 proxy 伺服器 toohave 連接閒置逾時設定。 請確定設定至少 6 分鐘以上的 tooat hello 組態。

如需詳細資訊，請參閱 MSDN 有關 hello[預設的 proxy 項目](https://msdn.microsoft.com/library/kd3cf2ex.aspx)。  
如需連線問題的詳細資訊，請參閱[針對連線問題進行疑難排解](active-directory-aadconnect-troubleshoot-connectivity.md)。

### <a name="other"></a>其他
* 選擇性： 測試使用者帳戶 tooverify 同步處理。

## <a name="component-prerequisites"></a>元件的必要條件
### <a name="powershell-and-net-framework"></a>PowerShell 和 .Net Framework
Azure AD Connect 需要 Microsoft PowerShell 和 .NET Framework 4.5.1。 您需要在伺服器上安裝此版本或更新版本。 根據您的 Windows Server 版本，請勿 hello 遵循：

* Windows Server 2012R2
  * 預設會安裝 Microsoft PowerShell。 不需採取任何動作。
  * .NET Framework 4.5.1 和更新版本會透過 Windows Update 提供。 請確定您已安裝最新的更新 tooWindows hello 伺服器 hello 控制台 中。
* Windows Server 2008R2 和 Windows Server 2012
  * hello 最新版本的 Microsoft PowerShell 是用於**Windows Management Framework 4.0**上提供[Microsoft Download Center](http://www.microsoft.com/downloads)。
  * .NET Framework 4.5.1 和更新版本可從 [Microsoft 下載中心](http://www.microsoft.com/downloads)取得。
* Windows Server 2008
  * hello 最新支援的 PowerShell 版本位於**Windows Management Framework 3.0**上提供[Microsoft Download Center](http://www.microsoft.com/downloads)。
  * .NET Framework 4.5.1 和更新版本可從 [Microsoft 下載中心](http://www.microsoft.com/downloads)取得。

### <a name="enable-tls-12-for-azure-ad-connect"></a>啟用 Azure AD Connect 的 TLS 1.2
Azure AD Connect 會依預設使用 TLS 1.0 加密 hello hello 同步作業引擎伺服器與 Azure AD 之間的通訊。 您可以變更此設定預設的.Net 應用程式 toouse TLS 1.2 hello 伺服器上。 您可以在 [Microsoft 資訊安全摘要報告 2960358](https://technet.microsoft.com/security/advisory/2960358) 中找到 TLS 1.2 的相關詳細資訊。

1. TLS 1.2 無法在 Windows Server 2008 上啟用。 您需要 Windows Server 2008R2 或更新版本。 請確定您沒有安裝適用於您作業系統的 hello.Net 4.5.1 hotfix，請參閱[Microsoft 安全性摘要報告 2960358](https://technet.microsoft.com/security/advisory/2960358)。 您的伺服器上可能已經安裝此 Hotfix 或更新版本。
2. 如果您使用 Windows Server 2008R2，請確定已啟用 TLS 1.2。 在 Windows Server 2012 伺服器和更新版本上，TLS 1.2 應該已經啟用。
   ```
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2]
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   ```
3. 適用於所有作業系統，設定此登錄機碼並重新啟動伺服器 hello。
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319
   "SchUseStrongCrypto"=dword:00000001
   ```
4. 如果您也想 tooenable TLS 1.2 hello 同步作業引擎伺服器與遠端的 SQL Server，則請確定您有針對安裝所需的 hello 版本[Microsoft SQL Server 的 TLS 1.2 支援](https://support.microsoft.com/kb/3135244)。

## <a name="prerequisites-for-federation-installation-and-configuration"></a>同盟安裝和組態的必要條件
### <a name="windows-remote-management"></a>Windows 遠端管理
使用 Azure AD Connect toodeploy Active Directory Federation Services 或 hello Web 應用程式 Proxy 時，請檢查這些需求：

* 如果 hello 目標伺服器已加入網域，請確定已啟用 Windows 遠端管理
  * 在提高權限的 PSH 命令視窗中，使用 `Enable-PSRemoting –force`
* 如果 hello 目標伺服器是在非網域聯結 WAP 電腦，則有幾個額外的需求
  * 在目標電腦 （WAP 機器） hello:
    * 請確定 hello winrm (Windows 遠端管理 / Ws-management) 服務正在執行透過 hello 服務 嵌入式管理單元
    * 在提高權限的 PSH 命令視窗中，使用 `Enable-PSRemoting –force`
  * 在 hello 的 hello 精靈正在執行 （如果 hello 目標機器非網域聯結或未受信任的網域） 的電腦：
    * 在提升權限 PSH 命令視窗中，使用 hello 命令`Set-Item WSMan:\localhost\Client\TrustedHosts –Value <DMZServerFQDN> -Force –Concatenate`
    * 在伺服器管理員中：
      * 新增周邊網路 WAP 主機 toomachine 集區 (伺服器管理員-> 管理...-> 新增伺服器使用 DNS 索引標籤)
      * 伺服器管理員的所有伺服器] 索引標籤： 以滑鼠右鍵按一下 WAP 伺服器並選擇 [管理身分...中，輸入 hello WAP 電腦本機 （不是網域） 認證
      * toovalidate 遠端 PSH 連線能力，在 伺服器管理員的所有伺服器 索引都標籤的 hello： 以滑鼠右鍵按一下 WAP 伺服器，然後選擇 Windows PowerShell。 應該會開啟遠端 PSH 工作階段可以建立 tooensure 遠端 PowerShell 工作階段。

### <a name="ssl-certificate-requirements"></a>SSL 憑證需求
* 強烈建議 toouse hello 跨 AD FS 陣列的所有節點和所有的 Web 應用程式 proxy 伺服器相同的 SSL 憑證。
* hello 憑證必須是 X509 憑證。
* 您可以在測試實驗室環境中的同盟伺服器上使用自我簽署的憑證。 不過，針對生產環境中，我們建議您從公用 CA 取得憑證 hello。
  * 如果使用不是公開信任的憑證，請確定每部 Web Application Proxy 伺服器上安裝該 hello 憑證是兩個 hello 本機伺服器上，所有同盟伺服器上受信任
* hello 身分識別的 hello 憑證必須符合 hello federation service 名稱 (例如，sts.contoso.com)。
  * hello 識別是 dnsname 類型的其中一個主體別名 (SAN) 延伸，或如果沒有 SAN 項目，hello 主體名稱指定為一般名稱。  
  * 多個 SAN 項目中可以存在 hello 憑證提供的其中一個符合 hello federation service 名稱。
  * 如果您計劃 toouse 工作地點加入，額外一個 SAN 無須 hello 值**enterpriseregistration。** 後面接著 hello 使用者主體名稱 (UPN) 尾碼，您的組織，例如**enterpriseregistration.contoso.com**。
* 不支援以 CryptoAPI 新一代 (CNG) 金鑰和金鑰儲存體為基礎的憑證。 這表示您必須使用以 CSP (密碼編譯服務提供者) 為基礎的憑證，而不是 KSP (金鑰儲存體提供者)。
* 支援萬用字元憑證。

### <a name="name-resolution-for-federation-servers"></a>同盟伺服器的名稱解析
* AD FS federation service 名稱 (例如，sts.contoso.com) hello 內部網路 （內部 DNS 伺服器） 和 hello 外部網路 (透過網域註冊機構的公用 DNS) 設定 hello 的 DNS 記錄。 Hello 內部網路 DNS 記錄，請確定您使用的記錄和不 CNAME 記錄。 這是必要的 windows 驗證 toowork 正確從您加入網域的電腦。
* 如果您要部署多部 AD FS 伺服器或 Web Application Proxy 伺服器，請確定您已設定您的負載平衡器和 hello AD FS 同盟服務名稱 (例如，sts.contoso.com) 點 toohello hello DNS 記錄負載平衡器。
* 在您的內部網路中使用 Internet Explorer 的瀏覽器應用程式的 windows 整合式的驗證 toowork，請確定該 hello AD FS federation service 名稱 (例如，sts.contoso.com) 會在 IE 中加入 toohello 近端內部網路區域。 這可以控制透過群組原則和部署的 tooall 您加入網域的電腦。

## <a name="azure-ad-connect-supporting-components"></a>Azure AD Connect 支援元件
hello 以下是安裝 Azure AD Connect 的 hello 伺服器安裝 Azure AD Connect 的元件的清單。 此清單適用於基本快速安裝。 如果您選擇不同的 SQL Server toouse hello 上安裝同步處理服務 頁面上，然後 SQL Express LocalDB 未安裝在本機。

* Azure AD Connect Health
* 適用於 IT 專業人員的 Microsoft Online Services 登入小幫手 (已安裝但未與其相依)
* Microsoft SQL Server 2012 命令列公用程式
* Microsoft SQL Server 2012 Express LocalDB
* Microsoft SQL Server 2012 Native Client
* Microsoft Visual C++ 2013 Redistribution Package

## <a name="hardware-requirements-for-azure-ad-connect"></a>Azure AD Connect 的硬體需求
hello 表顯示 hello hello Azure AD Connect 同步作業電腦的最低需求。

| Active Directory 中的物件數目 | CPU | 記憶體 | 硬碟大小 |
| --- | --- | --- | --- |
| 少於 10,000 個 |1.6 GHz |4 GB |70 GB |
| 10,000–50,000 個 |1.6 GHz |4 GB |70 GB |
| 50,000–100,000 個 |1.6 GHz |16 GB |100 GB |
| 100,000 或多個物件所需 hello 完整 SQL Server 版本 | | | |
| 100,000–300,000 個 |1.6 GHz |32 GB |300 GB |
| 300,000–600,000 個 |1.6 GHz |32 GB |450 GB |
| 超過 600,000 個 |1.6 GHz |32 GB |500 GB |

hello 執行 AD FS 電腦的最低需求，或 Web 應用程式伺服器為 hello 下列：

* CPU：雙核心 1.6 GHz 以上
* 記憶體：2 GB 以上
* Azure VM：A2 組態或更高等級

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
