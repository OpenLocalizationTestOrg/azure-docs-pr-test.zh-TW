---
title: "aaaAzure AD Connect Health 代理程式安裝 |Microsoft 文件"
description: "這是描述 hello 代理程式安裝 AD FS 和同步處理的 hello Azure AD Connect Health 頁面。"
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9019628ec1d4c477496e08910cfd668ed1933a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a>Azure AD Connect Health 代理程式安裝
這份文件會逐步引導您完成安裝及設定 hello Azure AD Connect Health 代理程式。 您可以下載 hello 代理程式從[這裡](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent)。

## <a name="requirements"></a>需求
下表中的 hello 是使用 Azure AD Connect Health 需求的清單。

| 需求 | 說明 |
| --- | --- |
| Azure AD Premium |Azure AD Connect Health 是 Azure AD Premium 的一個功能，而且需要 Azure AD Premium。 </br></br>如需詳細資訊，請參閱[開始使用 Azure AD Premium](../active-directory-get-started-premium.md) </br>toostart 免費的 30 天試用版，請參閱[開始使用試用版。](https://azure.microsoft.com/trial/get-started-active-directory/) |
| 您必須是全域系統管理員的 Azure AD tooget 開始使用 Azure AD Connect Health |根據預設，只有 hello 全域系統管理員可以安裝和設定 hello 健全狀況代理程式 tooget 啟動，存取 hello 入口網站，和執行 Azure AD Connect Health 內的任何作業。 如需詳細資訊，請參閱[管理您的 Azure AD 目錄](../active-directory-administer.md)。 <br><br> 使用角色型存取控制您可以允許存取 tooAzure AD Connect Health tooother 使用者在組織中。 如需詳細資訊，請參閱[適用於 Azure AD Connect Health 的角色型存取控制](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)。 </br></br>**重要事項：** hello 安裝 hello 代理程式必須是工作或學校帳戶時使用的帳戶。 不能是 Microsoft 帳戶。 如需詳細資訊，請參閱[以組織身分註冊 Azure](../sign-up-organization.md) |
| Azure AD Connect Health 代理程式安裝在每部目標伺服器上 | Azure AD Connect Health 需要 hello 健康狀態代理程式 toobe 安裝並設定目標的伺服器 tooreceive hello 資料，並提供 hello 的監視和分析功能 </br></br>比方說，tooget 資料從您的 AD FS 基礎結構，hello 代理程式必須安裝在 hello AD FS 和 Web 應用程式 Proxy 伺服器上。 同樣地，tooget 資料在您內部部署 AD DS 基礎結構，hello 代理程式必須安裝 hello 網域控制站上。 </br></br> |
| 輸出連線 toohello Azure 服務端點 | 在安裝和執行階段，hello 代理程式需要連接 tooAzure AD Connect Health 服務端點。 如果使用防火牆封鎖輸出連線，請確定下列端點該 hello 加入 toohello 允許清單： </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.servicebus.windows.net - Port: 5671 </li><li>&#42;.adhybridhealth.azure.com/</li><li>https://management.azure.com </li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
|以 IP 位址為基礎的輸出連線 | IP 位址篩選防火牆，請參閱 toohello [Azure IP 範圍](https://www.microsoft.com/en-us/download/details.aspx?id=41653)。|
| 已篩選或停用輸出流量的 SSL 檢查 | 如果沒有 SSL 檢查或終止 hello 網路層級的輸出流量，hello 代理程式註冊步驟或資料上傳作業可能會失敗。 |
| Hello 執行 hello 代理程式的伺服器上的防火牆連接埠。 |hello 代理程式需要下列 toobe 開啟 hello 代理程式 toocommunicate hello Azure AD Health 服務端點一起使用的防火牆連接埠的 hello。</br></br><li>TCP 通訊埠 443</li><li>TCP 通訊埠 5671</li> |
| 允許下列網站，如果已啟用 IE 增強式安全性的 hello |如果已啟用 IE 增強式安全性，然後 hello 下列網站，必須允許 hello 進行 toohave hello 代理程式安裝的伺服器上。</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>hello 信任的 Azure Active Directory 組織的同盟伺服器。 例如︰https://sts.contoso.com</li> |
|停用 FIPS|Azure AD Connect Health 代理程式不支援 FIPS。|

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-fs"></a>安裝 Azure AD Connect Health 代理程式的 AD FS hello
toostart hello 代理程式安裝中，按兩下您下載的 hello.exe 檔案。 在 hello 第一個畫面上，按一下 安裝。

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install1.png)

一旦 hello 安裝完成時，按一下 [立即設定]。

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install2.png)

這會啟動 PowerShell 視窗 tooinitiate hello 代理程式登錄程序。 出現提示時，使用具有存取 tooperform 代理程式註冊的 Azure AD 帳戶登入。 根據預設 hello 全域管理員帳戶的存取。

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install3.png)

登入後，PowerShell 將會繼續。 在完成時，您可以關閉 PowerShell 和 hello 設定已完成。

此時，hello 啟動代理程式服務應該是自動允許 hello 代理程式上傳所需的 hello 資料 toohello 雲端服務以安全的方式。

如果您有不符合所有 hello 先決條件 hello 上一節所述，在 hello PowerShell 視窗中會出現警告。 要確定 toocomplete hello[需求](active-directory-aadconnect-health-agent-install.md#requirements)之前安裝 hello 代理程式。 下列螢幕擷取畫面的 hello 是這些錯誤的範例。

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install4.png)

已安裝 tooverify hello 代理程式、 尋找 hello 遵循 hello 伺服器上的服務。 如果您已完成 hello 組態，它們應該已執行。 否則，它們會停止，直到 hello 設定已完成。

* Azure AD Connect Health AD FS 診斷服務
* Azure AD Connect Health AD FS Insights 服務
* Azure AD Connect Health AD FS 監視服務

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>Windows Server 2008 R2 伺服器上的代理程式安裝
適用於 Windows Server 2008 R2 伺服器的步驟：

1. 確定該 hello 伺服器正在執行 Service Pack 1 或更高版本。
2. 關閉 IE ESC 以安裝代理程式：
3. 每一個 hello 預先安裝 hello AD Health 代理程式的伺服器上安裝 Windows PowerShell 4.0。 tooinstall Windows PowerShell 4.0:
   * 安裝[Microsoft.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779)使用 hello 遵循連結 toodownload hello 離線安裝程式。
   * 安裝 PowerShell ISE (從 Windows 功能)
   * 安裝 hello [Windows Management Framework 4.0。](https://www.microsoft.com/download/details.aspx?id=40855)
   * 安裝 Internet Explorer 第 10 版或更高版本 hello 伺服器上。 （需要 hello 健全狀況服務 tooauthenticate，使用您的 Azure 系統管理員認證）。
4. 如需有關如何在 Windows Server 2008 R2 上安裝 Windows PowerShell 4.0 的詳細資訊，請參閱 hello wiki 文章[這裡](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx)。

### <a name="enable-auditing-for-ad-fs"></a>啟用 AD FS 的稽核
> [!NOTE]
> 本節僅適用於 tooAD FS 伺服器。 您沒有 toofollow hello Web 應用程式 Proxy 伺服器上的這些步驟。
>

為了讓 hello 流量分析功能 toogather 並分析資料，hello Azure AD Connect Health 代理程式需要 hello hello AD FS 稽核記錄檔中的資訊。 預設不會啟用這些記錄檔。 使用下列程序 tooenable AD FS 稽核的 hello 和 toolocate hello AD FS 稽核記錄檔，在 AD FS 伺服器上。

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2008-r2"></a>Windows Server 2008 R2 上的 AD FS 的稽核 tooenable
1. 按一下**啟動**，點太**程式**，點太**系統管理工具**，然後按一下**本機安全性原則**。
2. 瀏覽 toohello**安全性 \ 使用者權限管理**資料夾，然後按兩下 產生安全性稽核。
3. 在 hello**本機安全性設定**索引標籤上，確認已列出 hello AD FS 2.0 服務帳戶。 如果不存在，請按一下**新增使用者或群組**並將它加入 toohello 清單，然後按一下**確定**。
4. tooenable 稽核，使用提高的權限開啟命令提示字元並執行下列命令的 hello:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. 關閉 [本機安全性原則]，然後開啟 hello 管理嵌入式管理單元。 按一下 [管理] 嵌入式管理單元 tooopen hello**啟動**，點太**程式**，點太**系統管理工具**，然後按一下AD FS 2.0 管理。
6. Hello 動作] 窗格中按一下 [編輯同盟服務內容。
7. 在 [hello **Federation Service 屬性**對話方塊方塊中，按一下 hello**事件**] 索引標籤。
8. 選取 hello**成功稽核**和**失敗稽核**核取方塊。
9. 按一下 [確定] 。

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>Windows Server 2012 R2 上的 AD FS 的稽核 tooenable
1. 開啟**本機安全性原則**開啟**伺服器管理員**hello 開始 畫面或桌面上 hello hello 工作列中的 伺服器管理員，然後按一下 **工具/本機安全性原則**.
2. 瀏覽 toohello**安全性本機原則 \ 使用者權限指派**資料夾，然後再按兩下**產生安全性稽核**。
3. 在 hello**本機安全性設定**索引標籤上，確認已列出 hello AD FS 服務帳戶。 如果不存在，請按一下**新增使用者或群組**並將它加入 toohello 清單，然後按一下**確定**。
4. tooenable 稽核，以提高的權限開啟命令提示字元並執行下列命令的 hello: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```。
5. 關閉**本機安全性原則**，然後開啟 hello **AD FS 管理**嵌入式管理單元 （在 伺服器管理員 中，按一下工具，然後選取 AD FS 管理）。
6. 在 hello 動作 窗格中，按一下 **編輯 Federation Service 屬性**。
7. 在 hello Federation Service 屬性 對話方塊中，按一下 hello**事件** 索引標籤。
8. 選取 hello**成功稽核與失敗稽核**核取方塊，然後按一下**確定**。

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2016"></a>Windows Server 2016 上的 AD FS 的稽核 tooenable
1. 開啟**本機安全性原則**開啟**伺服器管理員**hello 開始 畫面或桌面上 hello hello 工作列中的 伺服器管理員，然後按一下 **工具/本機安全性原則**.
2. 瀏覽 toohello**安全性本機原則 \ 使用者權限指派**資料夾，然後再按兩下**產生安全性稽核**。
3. 在 hello**本機安全性設定**索引標籤上，確認已列出 hello AD FS 服務帳戶。 如果不存在，請按一下**新增使用者或群組**然後新增 hello AD FS 服務帳戶 toohello 清單，然後再按一下**確定**。
4. tooenable 稽核，使用提高的權限開啟命令提示字元並執行下列命令的 hello:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. 關閉**本機安全性原則**，然後開啟 hello **AD FS 管理**嵌入式管理單元 （在 伺服器管理員 中，按一下工具，然後選取 AD FS 管理）。
6. 在 hello 動作 窗格中，按一下 **編輯 Federation Service 屬性**。
7. 在 hello Federation Service 屬性 對話方塊中，按一下 hello**事件** 索引標籤。
8. 選取 hello**成功稽核與失敗稽核**核取方塊，然後按一下**確定**。 預設會啟用此功能。
9. 開啟 PowerShell 視窗，然後執行下列命令的 hello: ```Set-AdfsProperties -AuditLevel Verbose```。

請注意，預設會啟用「基本」稽核層級。 深入了解 hello [Windows Server 2016 中的 AD FS 稽核增強功能](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)


#### <a name="toolocate-hello-ad-fs-audit-logs"></a>toolocate hello AD FS 稽核記錄檔
1. 開啟 [事件檢視器] 。
2. 移 tooWindows 記錄檔，然後選取**安全性**。
3. 在 hello 右邊，按一下 **篩選目前的記錄**。
4. 在 [事件來源] 下，選取 [AD FS 稽核] 。

![AD FS 稽核記錄](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> 群組原則可以停用 AD FS 稽核。 如果已停用 AD FS 稽核，則無法使用有關登入活動的使用量分析。 確定您沒有可停用 AD FS 稽核的群組原則。
>


## <a name="installing-hello-azure-ad-connect-health-agent-for-sync"></a>安裝 hello Azure AD Connect Health 代理程式進行同步
hello Azure AD Connect Health 代理程式同步處理會自動安裝在 Azure AD Connect hello 最新組建。 toouse Azure AD Connect 同步處理，您需要 toodownload hello 最新版的 Azure AD Connect 並安裝它。 您可以下載最新版本的 hello[這裡](http://www.microsoft.com/download/details.aspx?id=47594)。

已安裝 tooverify hello 代理程式、 尋找 hello 遵循 hello 伺服器上的服務。 如果您已完成 hello 組態，它們應該已執行。 否則，它們會停止，直到 hello 設定已完成。

* Azure AD Connect Health Sync Insights 服務
* Azure AD Connect Health Sync Monitoring 服務

![驗證適用於同步處理的 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> 請記住，使用 Azure AD Connect Health 需要 Azure AD Premium。 如果您沒有 Azure AD Premium，您便無法 toocomplete hello Azure 入口網站中的 hello 組態。 如需詳細資訊，請參閱 hello[需求 頁面](active-directory-aadconnect-health-agent-install.md#requirements)。
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>手動 Azure AD Connect Health for Sync 註冊
如果 hello Azure AD Connect Health 進行同步處理代理程式註冊失敗之後成功安裝 Azure AD Connect，您可以使用下列 PowerShell 命令 toomanually 註冊 hello 代理程式的 hello。

> [!IMPORTANT]
> 使用以下 PowerShell 命令，才需要之後安裝 Azure AD Connect 如果 hello 代理程式註冊失敗。
>
>

hello 下列 PowerShell 命令需要只 hello 健全狀況代理程式註冊失敗時即使成功安裝及設定 Azure AD connect。 hello Azure AD Connect Health 服務都啟動之後 hello 代理程式已順利註冊。

您可以手動註冊 hello Azure AD Connect Health 代理程式，使用下列 PowerShell 命令的 hello 的同步處理：

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

hello 命令會使用下列參數：

* AttributeFiltering: $true （預設）-如果 Azure AD Connect 不同步 hello 預設屬性集，而且已自訂的 toouse 已篩選的屬性集。 否則為 $false。
* StagingMode: $false （預設）-如果 hello Azure AD Connect 的伺服器不在執行模式中，$true hello 伺服器是否設定 toobe 中預備模式。

當系統提示您輸入驗證您應該使用 hello 相同的全域管理員帳戶 (例如admin@domain.onmicrosoft.com) 用來設定 Azure AD Connect。

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-ds"></a>安裝 Azure AD Connect Health 代理程式用於 AD DS hello
toostart hello 代理程式安裝中，按兩下您下載的 hello.exe 檔案。 在 hello 第一個畫面上，按一下 安裝。

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

一旦 hello 安裝完成時，按一下 [立即設定]。

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

命令提示字元隨即啟動，然後再啟動可執行 PowerShell that executes Register-AzureADConnectHealthADDSAgent 的特定 PowerShell。 當提示的 toosign 中 tooAzure，請繼續並登入。

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

登入後，PowerShell 將會繼續。 在完成時，您可以關閉 PowerShell 和 hello 設定已完成。

此時，hello 服務應該自動允許 hello 代理程式 toomonitor 啟動，並收集資料。 如果您有不符合所有 hello 先決條件 hello 上一節所述，在 hello PowerShell 視窗中會出現警告。 要確定 toocomplete hello[需求](active-directory-aadconnect-health-agent-install.md#requirements)之前安裝 hello 代理程式。 下列螢幕擷取畫面的 hello 是這些錯誤的範例。

![驗證適用於 AD DS 的 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

已安裝 tooverify hello 代理程式、 尋找 hello 遵循 hello 網域控制站上的服務。

* Azure AD Connect Health AD DS Insights 服務
* Azure AD Connect Health AD DS 監視服務

如果您已完成 hello 組態時，應該已經在執行這些服務。 否則，它們會停止，直到 hello 設定已完成。

![驗證 Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a>使用 PowerShell 進行代理程式註冊
安裝之後 hello 適當的代理程式的 setup.exe，您可以執行使用下列 PowerShell 命令，視 hello 角色而定的 hello hello 代理程式註冊步驟。 開啟 PowerShell 視窗，然後執行 hello 適當的命令：

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

這些命令會接受"Credential"參數 toocomplete hello 註冊為非互動方式或 Server Core 電腦上。
* hello 認證可以傳遞做為參數的 PowerShell 變數中擷取。
* 您可以提供任何 Azure AD 身分識別，其中擁有存取 tooregister hello 代理程式，而且沒有啟用 MFA。
* 預設全域系統管理員可以存取 tooperform 代理程式註冊。 您也可以讓其他特殊權限的身分識別 tooperform 小於此步驟。 深入了解[角色型存取控制](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)。

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-toouse-http-proxy"></a>設定 Azure AD Connect Health 代理程式 toouse HTTP Proxy
您可以設定 Azure AD Connect Health 代理程式 toowork 透過 HTTP Proxy。

> [!NOTE]
> * 不支援使用"Netsh WinHttp set ProxyServerAddress"，因為 hello 代理程式使用 System.Net toomake web 要求，而不是 Microsoft Windows HTTP 服務。
> * hello 設定的 Http Proxy 位址不使用的 toopass 透過加密的 Https 訊息。
> * 不支援已驗證的 Proxy (使用 HTTPBasic)。
>
>

### <a name="change-health-agent-proxy-configuration"></a>變更健康情況代理程式 Proxy 組態
您有下列選項 tooconfigure Azure AD Connect Health 代理程式 toouse HTTP Proxy 的 hello。

> [!NOTE]
> 所有的 Azure AD Connect Health 代理程式服務必須重新啟動，為了讓 hello proxy 設定 toobe 更新。 執行下列命令的 hello:<br>
> Restart-Service AdHealth*
>
>

#### <a name="import-existing-proxy-settings"></a>匯入現有的 Proxy 設定
##### <a name="import-from-internet-explorer"></a>從 Internet Explorer 匯入
可以匯入 Internet Explorer HTTP proxy 設定，toobe 由 hello Azure AD Connect Health 代理程式。 每個執行 hello 健康情況代理程式的 hello 伺服器上執行下列 PowerShell 命令的 hello:

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>從 WinHTTP 匯入
WinHTTP proxy 設定可匯入，toobe 由 hello Azure AD Connect Health 代理程式。 每個執行 hello 健康情況代理程式的 hello 伺服器上執行下列 PowerShell 命令的 hello:

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>以手動方式指定 Proxy 位址
您可以在每部執行 hello 健康情況代理程式，藉由執行下列 PowerShell 命令的 hello hello 伺服器上手動指定 proxy 伺服器：

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

範例：*Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress myproxyserver: 443*

* 「位址」可以是可解析的 DNS 伺服器名稱或 IPv4 位址
* 「連接埠」可以省略。 如果省略，則會選擇 443 做為預設連接埠。

#### <a name="clear-existing-proxy-configuration"></a>清除現有的 Proxy 設定
您可以藉由執行下列命令的 hello 清除 hello 現有的 proxy 設定：

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>讀取目前的 Proxy 設定
您可以藉由執行下列命令的 hello 閱讀 hello 目前設定的 proxy 設定：

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-tooazure-ad-connect-health-service"></a>測試連線 tooAzure AD Connect Health 服務
有可能的問題可能會發生與 hello Azure AD Connect Health 服務 toolose 連線導致 hello Azure AD Connect Health 代理程式。 這些包括網路問題、權限問題或各種其他原因。

如果 hello 代理程式無法 toosend 資料 toohello Azure AD Connect Health 服務的時間超過兩小時，其中會顯示以 hello 遵循 hello 入口網站中的警示: 「 健全狀況服務的資料不是向上 toodate。 」 您可以確認受影響的 hello Azure AD Connect Health 代理程式是否能 tooupload 資料 toohello Azure AD Connect Health 服務藉由執行下列 PowerShell 命令的 hello:

    Test-AzureADConnectHealthConnectivity -Role ADFS

hello 角色參數目前只接受下列值的 hello:

* ADFS
* Sync
* ADDS

您可以在 hello 命令 tooview 使用 hello-ShowResults 旗標的詳細記錄檔。 下列範例使用 hello:

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> toouse hello 連線工具，您必須第一個完成的 hello 代理程式註冊。 如果您不能 toocomplete hello 代理程式註冊，請確定您已符合所有 hello[需求](active-directory-aadconnect-health-agent-install.md#requirements)有關 Azure AD Connect Health。 這項連線測試預設是在代理程式註冊期間執行。
>
>

## <a name="related-links"></a>相關連結
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health 操作](active-directory-aadconnect-health-operations.md)
* [在 AD FS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)
* [使用 Azure AD Connect Health 進行同步處理](active-directory-aadconnect-health-sync.md)
* [在 AD DS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health 常見問題集](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 版本歷程記錄](active-directory-aadconnect-health-version-history.md)
