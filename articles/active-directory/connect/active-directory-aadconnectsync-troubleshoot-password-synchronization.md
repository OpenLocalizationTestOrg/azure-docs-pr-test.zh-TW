---
title: "搭配 Azure AD Connect 同步化 aaaTroubleshoot 密碼同步化 |Microsoft 文件"
description: "這篇文章提供有關如何資訊 tootroubleshoot 密碼同步處理問題。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a>針對使用 Azure AD Connect 同步執行的密碼同步處理進行疑難排解
本主題提供如何 tootroubleshoot 發出密碼同步處理步驟。 如果密碼未如預期般同步，可能會影響一部分使用者或所有使用者。 Azure Active directory (Azure AD) 連線版本 1.1.524.0 部署，或更新版本中，目前已診斷的指令程式，您可以使用 tootroubleshoot 密碼同步處理的問題：

* 如果您有問題會在同步處理沒有密碼，請參閱 toohello[沒有密碼會同步處理： 使用 hello 診斷的指令程式來進行疑難排解](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet)> 一節。

* 如果您有個別的物件發生問題，請參閱 toohello[一個物件不會同步處理密碼： 使用 hello 診斷的指令程式來進行疑難排解](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet)> 一節。

舊版的 Azure AD Connect 部署：

* 如果您有問題會在同步處理沒有密碼，請參閱 toohello[沒有密碼會同步處理： 疑難排解步驟的手動](#no-passwords-are-synchronized-manual-troubleshooting-steps)> 一節。

* 如果您有個別的物件發生問題，請參閱 toohello[一個物件不會同步處理密碼： 疑難排解步驟的手動](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps)> 一節。

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>不會將密碼同步處理： 使用 hello 診斷的指令程式來進行疑難排解
您可以使用 hello `Invoke-ADSyncDiagnostics` cmdlet toofigure 出為什麼沒有密碼會同步處理。

> [!NOTE]
> hello `Invoke-ADSyncDiagnostics` cmdlet 是僅適用於 Azure AD Connect 版本 1.1.524.0 或更新版本。

### <a name="run-hello-diagnostics-cmdlet"></a>執行 hello 診斷 cmdlet
會在同步處理不會將密碼 tootroubleshoot 問題：

1. 開啟新的 Windows PowerShell 工作階段，在您 Azure AD Connect 的伺服器上以 hello**系統管理員身分執行**選項。

2. 執行 `Set-ExecutionPolicy RemoteSigned` 或 `Set-ExecutionPolicy Unrestricted`。

3. 執行 `Import-Module ADSyncDiagnostics`。

4. 執行 `Invoke-ADSyncDiagnostics -PasswordSync`。

### <a name="understand-hello-results-of-hello-cmdlet"></a>了解 hello cmdlet 的 hello 結果
hello 診斷 cmdlet 會執行下列檢查 hello:

* 會驗證該 hello Azure AD 租用戶啟用密碼同步處理功能。

* 會驗證該 hello Azure AD Connect 伺服器不是預備模式。

* 針對每個現有的內部部署 Active Directory 連接器 （其對應 tooan 現有 Active Directory 樹系）：

   * 會驗證該 hello 啟用密碼同步處理功能。
   
   * 密碼同步處理活動訊號中的事件 hello 搜尋 Windows 應用程式事件記錄檔。

   * 每個 Active Directory 網域下 hello 在內部部署 Active Directory 連接器：

      * 會驗證該 hello 網域可從 hello Azure AD Connect 的伺服器連線。

      * 驗證 hello hello 在內部部署 Active Directory 連接器所使用的 Active Directory 網域服務 (AD DS) 帳戶具有 hello 正確的使用者名稱、 密碼和密碼同步處理所需的權限。

hello 下列圖表說明單一網域，在內部部署 Active Directory 拓樸的 hello cmdlet 的 hello 的結果：

![密碼同步化的診斷輸出](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

hello 本節其餘部分將說明特定 hello cmdlet 所傳回的結果和對應的問題。

#### <a name="password-synchronization-feature-isnt-enabled"></a>密碼同步化功能未啟用
如果您尚未使用 hello Azure AD Connect 精靈啟用密碼同步處理，會傳回下列錯誤 hello:

![密碼同步化未啟用](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a>Azure AD Connect 伺服器處於預備模式
如果正在預備模式 hello Azure AD Connect 的伺服器，暫時停用密碼同步處理，並 hello 會傳回下列錯誤：

![Azure AD Connect 伺服器處於預備模式](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a>沒有密碼同步化活動訊號事件
每個內部部署 Active Directory 連接器各有自己的密碼同步化通道。 當建立 hello 密碼同步處理通道，而且沒有任何同步處理的密碼變更 toobe 時，活動訊號事件 (EventId 654) 會產生一次每隔 30 分鐘在 hello Windows 應用程式事件記錄檔。 每個內部部署 Active Directory 連接器 hello 指令程式會搜尋 hello 中對應的活動訊號事件過去三小時內。 如果不找到任何活動訊號的事件，hello 會傳回下列錯誤：

![沒有密碼同步化活動訊號事件](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a>AD DS 帳戶沒有正確的權限
如果使用 hello hello AD DS 帳戶內部部署 Active Directory 連接器 toosynchronize 密碼雜湊並沒有 hello 適當的權限，hello 會傳回下列錯誤：

![不正確的認證](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a>不正確的 AD DS 帳戶使用者名稱或密碼
如果 hello AD DS 帳戶由 hello 在內部部署 Active Directory 連接器 toosynchronize 密碼雜湊不正確的使用者名稱或密碼，hello 會傳回下列錯誤：

![不正確的認證](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>一個物件不會同步處理密碼： 使用 hello 診斷的指令程式來進行疑難排解
您可以使用 hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine 為什麼一個物件並未同步處理密碼。

> [!NOTE]
> hello `Invoke-ADSyncDiagnostics` cmdlet 是僅適用於 Azure AD Connect 版本 1.1.524.0 或更新版本。

### <a name="run-hello-diagnostics-cmdlet"></a>執行 hello 診斷 cmdlet
會在同步處理不會將密碼 tootroubleshoot 問題：

1. 開啟新的 Windows PowerShell 工作階段，在您 Azure AD Connect 的伺服器上以 hello**系統管理員身分執行**選項。

2. 執行 `Set-ExecutionPolicy RemoteSigned` 或 `Set-ExecutionPolicy Unrestricted`。

3. 執行 `Import-Module ADSyncDiagnostics`。

4. 執行下列 cmdlet 的 hello:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   例如：
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a>了解 hello cmdlet 的 hello 結果
hello 診斷 cmdlet 會執行下列檢查 hello:

* Hello hello Active Directory 連接器空間、 Metaverse 和 Azure 中的 hello Active Directory 物件狀態會檢查 AD 連接器空間。

* 驗證已啟用密碼同步處理的同步處理規則，並套用 toohello Active Directory 物件。

* 嘗試 tooretrieve 並顯示 hello 的結果 hello 最後嘗試 toosynchronize hello 密碼 hello 物件。

疑難排解密碼同步化單一物件時，hello 下列圖表說明 hello cmdlet 的 hello 結果：

![密碼同步化的診斷輸出 - 單一物件](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

hello 本節其餘部分將說明特定 hello cmdlet 所傳回的結果和對應的問題。

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a>hello Active Directory 物件不是匯出的 tooAzure AD
這在內部部署 Active Directory 帳戶的密碼同步處理失敗，因為在 hello Azure AD 租用戶中沒有對應的物件。 會傳回下列錯誤 hello:

![遺漏 Azure AD 物件](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a>使用者有暫時密碼
目前，Azure AD Connect 不支援與 Azure AD 同步暫時密碼。 密碼會被視為 toobe 暫存如果 hello**在下次登入時變更密碼**hello 在內部部署 Active Directory 使用者上設定選項。 會傳回下列錯誤 hello:

![未匯出暫時密碼](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a>上次嘗試 toosynchronize 密碼的結果，就無法使用
根據預設，Azure AD Connect 儲存 hello 的有效期是七天的密碼同步處理嘗試的結果。 如果沒有可用的 hello 選取 Active Directory 物件的結果，則會傳回下列警告 hello:

![單一物件的診斷輸出 - 沒有密碼同步記錄](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a>未同步任何密碼：手動疑難排解步驟
請遵循這些步驟 toodetermine，不會將密碼同步處理的原因：

1. 中的 hello 連接伺服器[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)嗎？ 處於預備模式的伺服器不會同步處理任何密碼。

2. 執行 hello hello 指令碼[取得的密碼同步處理設定 hello 狀態](#get-the-status-of-password-sync-settings)> 一節。 它可讓您 hello 密碼同步處理組態的概觀。  

    ![來自密碼同步設定的 PowerShell 指令碼輸出](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. 如果 hello 功能未啟用 Azure AD 中，或未啟用 hello 同步通道狀態，執行 hello 連線安裝精靈。 選取 [自訂同步處理選項] 並取消選取密碼同步。這項變更暫時停用 hello 功能。 然後再次執行 hello 精靈並重新啟用密碼同步。執行 hello 指令碼一次 hello 組態的 tooverify 是否正確。

4. 查看有錯誤的 hello 事件記錄檔。 尋找下列事件，則表示問題 hello:
    * 來源：「目錄同步作業」識別碼：0、611、652、655。如果您看到這些事件，即表示有連線問題。 hello 事件記錄檔訊息包含您有問題的所在的樹系資訊。 如需詳細資訊，請參閱[連線問題](#connectivity problem)。

5. 如果您沒有看到任何活動訊號，或任何其他操作都沒有作用，請執行[觸發所有密碼的完整同步](#trigger-a-full-sync-of-all-passwords)。 Hello 指令碼只執行一次。

6. 請參閱 hello[疑難排解不同步處理密碼的一個物件](#one-object-is-not-synchronizing-passwords)> 一節。

### <a name="connectivity-problems"></a>連線問題

您是否能夠與 Azure AD 連線？

沒有 hello 帳戶具有必要的權限 tooread hello 密碼雜湊中的所有網域？ 如果您安裝連接使用 Express 設定時，應該已經正確 hello 權限。 

如果您使用自訂安裝，hello 手動設定權限執行 hello 下列動作：
    
1. hello Active Directory 連接器，開始使用 toofind hello 帳戶**同步處理服務管理員**。 
 
2. 跳過**連接器**，然後搜尋您正在疑難排解的 hello 在內部部署 Active Directory 樹系。 
 
3. 選取 hello 連接器，然後按一下**屬性**。 
 
4. 跳過**連接 tooActive Directory 樹系**。  
    
    ![Active Directory 連接器所使用的帳戶](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    請注意 hello 使用者名稱和 hello hello 帳戶所在的網域。
    
5. 啟動**Active Directory 使用者和電腦**，然後確認您稍早發現的 hello 帳戶具有設定所有的網域樹系中的 hello 根目錄的 hello 後續權限：
    * 複寫目錄變更
    * 複寫目錄變更 (全部)

6. 為 hello 網域控制站連線到 Azure AD connect 嗎？ 如果 hello 連接伺服器無法連線 tooall 網域控制站，設定**只使用慣用的網域控制站**。  
    
    ![Active Directory 連接器所使用的網域控制站](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. 請返回太**同步處理服務管理員**和**設定目錄分割**。 
 
8. 選取您的網域中**選取目錄分割**，選取 hello**只使用慣用的網域控制站**核取方塊，然後**設定**。 

9. 在 [hello] 清單中，輸入 hello 網域控制站連接應該用於密碼同步處理。hello 匯入和匯出也使用相同的清單。 針對您的所有網域執行這些步驟。

10. 如果 hello 指令碼會顯示沒有任何活動訊號，請執行 hello 指令碼[觸發完整同步處理所有密碼](#trigger-a-full-sync-of-all-passwords)。

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a>一個物件未同步密碼：手動疑難排解步驟
您可以輕鬆地疑難排解密碼同步處理的問題，藉由檢閱 hello 物件狀態。

1. 在**Active Directory 使用者和電腦**搜尋 hello 使用者，然後確認該 hello**使用者必須變更密碼，在下次登入時**核取方塊。  

    ![Active Directory 生產力密碼](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    如果選取 [hello] 核取方塊，詢問 hello 使用者 toosign 中的，並變更 hello 密碼。 暫時密碼不會與 Azure AD 同步。

2. 如果在 Active Directory 中 hello 密碼正確無誤，請遵循 hello hello 同步處理引擎中的使用者。 由下列 hello 使用者從內部部署 Active Directory tooAzure AD，您可以看到 hello 物件上是否具描述性的錯誤。

    a. 啟動 hello[同步處理服務管理員](active-directory-aadconnectsync-service-manager-ui.md)。

    b. 按一下 [連接器] 。

    c. 選取 hello **Active Directory 連接器**hello 使用者所在的位置。

    d. 選取 [搜尋連接器空間] 。

    e. 在 hello**範圍**方塊中，選取**DN 或錨點**，然後輸入 hello 完整 DN hello 使用者您正在疑難排解。

    ![在連接器空間中依 DN 搜尋使用者](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    f. 找出您要尋找，然後按一下 hello 使用者**屬性**toosee 所有 hello 屬性。 如果 hello 使用者不是在 hello 搜尋結果，請確認您[篩選規則](active-directory-aadconnectsync-configure-filtering.md)，並確定您執行[套用並驗證變更](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes)的 hello 使用者 tooappear 連線中。

    g. 過去一週中，按一下 toosee hello 密碼同步處理物件的詳細資料 hello hello**記錄**。  

    ![物件記錄詳細資料](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    如果 hello 物件記錄是空的 Azure AD Connect 已從 Active Directory 無法 tooread hello 密碼雜湊。 請繼續進行[連線錯誤](#connectivity-errors)疑難排解。 如果您看到任何其他值比**成功**，toohello 資料表中的，請參閱[密碼同步處理記錄](#password-sync-log)。

    h. 選取 hello**歷程**索引標籤，然後確認該至少一個同步處理規則中 hello **PasswordSync**資料行是**True**。 Hello 預設組態中，在 hello hello 同步處理規則名稱是**中 from AD-User AccountEnabled**。  

    ![使用者的相關歷程資訊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    i. 按一下**Metaverse 物件屬性**toodisplay 的使用者屬性清單。  

    ![Metaverse 資訊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    確認沒有任何 **cloudFiltered** 屬性存在。 請確定 hello 網域屬性 （domainFQDN 和 domainNetBios） 具有 hello 預期的值。

    j. 按一下 hello**連接器** 索引標籤。請確定您看到連接器 tooboth 內部部署 Active Directory 與 Azure AD。

    ![Metaverse 資訊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    k. 選取 hello 資料列代表 Azure AD 中，按一下**屬性**，然後按一下hello**歷程** 索引標籤 hello 連接器空間物件中應該會有輸出規則 hello **PasswordSync**資料行集太**True**。 Hello 預設組態中，在 hello hello 同步處理規則名稱是**出 tooAAD-User Join**。  

    ![連接器空間物件屬性對話方塊](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a>密碼同步記錄
hello 狀態資料行可以有下列值的 hello:

| 狀態 | 說明 |
| --- | --- |
| 成功 |已成功同步處理密碼。 |
| FilteredByTarget |密碼設定得**使用者必須變更密碼，在下次登入時**。 未同步處理密碼。 |
| NoTargetConnection |Hello metaverse 或 hello Azure AD 連接器空間中任何物件。 |
| SourceConnectorNotPresent |Hello 在內部部署 Active Directory 連接器空間中找不到物件。 |
| TargetNotExportedToDirectory |hello Azure AD 連接器空間中的 hello 物件尚未匯出。 |
| MigratedCheckDetailsForMoreInfo |記錄項目建立於組建 1.0.9125.0 之前，並且以其舊版的狀態顯示。 |
| 錯誤 |服務傳回未知的錯誤。 |
| 不明 |嘗試 tooprocess 密碼雜湊的批次時發生錯誤。  |
| MissingAttribute |無法使用 Azure AD Domain Services 所需的特定屬性 (例如，Kerberos 雜湊)。 |
| RetryRequestedByTarget |先前無法使用 Azure AD Domain Services 所需的特定屬性 (例如，Kerberos 雜湊)。 會嘗試 tooresynchronize hello 使用者密碼雜湊。 |

## <a name="scripts-toohelp-troubleshooting"></a>指令碼 toohelp 疑難排解

### <a name="get-hello-status-of-password-sync-settings"></a>取得密碼同步處理設定 hello 狀態
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a>觸發所有密碼的完整同步處理
> [!NOTE]
> 只執行一次這個指令碼。 如果您需要 toorun，它一次以上，其他項目是 hello 問題。 tootroubleshoot hello 問題，請連絡 Microsoft 支援。

您可以使用下列指令碼的 hello 觸發完整同步處理所有密碼：

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a>後續步驟
* [使用 Azure AD Connect 同步處理實作密碼同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)
* [Azure AD Connect 同步：自訂同步處理選項](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
