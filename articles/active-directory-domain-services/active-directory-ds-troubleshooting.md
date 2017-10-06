---
title: "Azure Active Directory Domain Services：疑難排解指南 | Microsoft Docs"
description: "Azure AD 網域服務的疑難排解指南"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a>Azure AD 網域服務 - 疑難排解指南
這篇文章提供設定或管理 Azure Active Directory (AD) 網域服務時，可能會遇到的問題之疑難排解提示。

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a>您無法為 Azure AD 目錄啟用 Azure AD 網域服務
本節可協助您疑難排解錯誤時嘗試 tooenable 您目錄的 Azure AD 網域服務和失敗或取得切換後 too'Disabled'。

挑選 hello 對應 toohello 您遇到的錯誤訊息的疑難排解步驟。

| **錯誤訊息** | **解決方案** |
| --- |:--- |
| *hello 名稱 contoso100.com 已在此網路上的使用中。指定未使用的名稱。* |[Hello 虛擬網路中的網域名稱衝突](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| *無法在此 Azure AD 租用戶中啟用網域服務。hello 服務沒有足夠的權限 toohello 應用程式呼叫 Azure AD 網域服務同步'。刪除呼叫 'Azure AD 網域服務同步處理' hello 應用程式，然後再次嘗試您的 Azure AD 租用戶的 tooenable 網域服務。* |[沒有足夠的權限 toohello Azure AD 網域服務同步處理應用程式網域服務。](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| *無法在此 Azure AD 租用戶中啟用網域服務。hello Azure AD 租用戶中的應用程式不會不會有 hello 的網域服務所需的權限 tooenable 網域服務。刪除與 hello 應用程式識別碼 d87dcbc6-a371-462e-88e3-28ad15ec4e64 hello 應用程式，然後再次嘗試 tooenable Azure AD 租用戶的網域服務。* |[hello 網域服務應用程式未正確設定您的租用戶中](active-directory-ds-troubleshooting.md#invalid-configuration) |
| *無法在此 Azure AD 租用戶中啟用網域服務。hello Microsoft Azure AD 應用程式已停用 Azure AD 租用戶中。啟用與 hello 應用程式識別碼 00000002-0000-0000-c000-000000000000 hello 應用程式，然後再次嘗試 tooenable Azure AD 租用戶的網域服務。* |[Azure AD 租用戶中的 hello Microsoft Graph 應用程式已停用](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a>網域名稱衝突
**錯誤訊息：**

*hello 名稱 contoso100.com 已在此網路上的使用中。指定未使用的名稱。*

**補救：**

請確定您沒有現有的網域 hello 與該虛擬網路上可用的相同網域名稱。 比方說，假設您擁有 hello 選取的虛擬網路上呼叫 'contoso.com' 已存在的網域。 您嘗試 tooenable hello 與 Azure AD 網域服務受管理網域的更新版本中，該虛擬網路上相同的網域名稱 (也就是 ' contoso.com')。 嘗試 tooenable Azure AD 網域服務時發生失敗。

此失敗是由於 tooname hello 網域名稱，該虛擬網路上的衝突。 在此情況下，您必須使用不同的名稱 tooset 註冊您 Azure AD 網域服務受管理的網域。 或者，可以解除佈建 hello 現有網域，然後繼續 tooenable Azure AD 網域服務。

### <a name="inadequate-permissions"></a>權限不足
**錯誤訊息：**

*無法在此 Azure AD 租用戶中啟用網域服務。hello 服務沒有足夠的權限 toohello 應用程式呼叫 Azure AD 網域服務同步'。刪除呼叫 'Azure AD 網域服務同步處理' hello 應用程式，然後再次嘗試您的 Azure AD 租用戶的 tooenable 網域服務。*

**補救：**

如果您的 Azure AD 目錄中沒有 hello 名稱 'Azure AD 網域服務同步處理' 的應用程式，請檢查 toosee。 如果此應用程式存在，請將它刪除，然後再重新啟用 Azure AD 網域服務。

執行 hello hello 應用程式和 toodelete hello 存在的步驟 toocheck 之後，如果存在 hello 應用程式：

1. 瀏覽 toohello **Azure 傳統入口網站**([https://manage.windowsazure.com](https://manage.windowsazure.com))。
2. 選取 hello **Active Directory** hello 左窗格上的節點。
3. 選取 hello Azure AD 租用戶 （目錄），您想要 tooenable Azure AD 網域服務。
4. 瀏覽 toohello**應用程式**] 索引標籤。
5. 選取 hello**我公司所擁有的應用程式**hello 下拉式清單中的選項。
6. 檢查名為 [Azure AD 網域服務同步處理] 的應用程式。如果 hello 應用程式存在，繼續 toodelete 它。
7. 一旦您刪除 hello 應用程式之後, 再試一次一次 tooenable Azure AD 網域服務。

### <a name="invalid-configuration"></a>無效的組態
**錯誤訊息：**

*無法在此 Azure AD 租用戶中啟用網域服務。hello Azure AD 租用戶中的應用程式不會不會有 hello 的網域服務所需的權限 tooenable 網域服務。刪除與 hello 應用程式識別碼 d87dcbc6-a371-462e-88e3-28ad15ec4e64 hello 應用程式，然後再次嘗試 tooenable Azure AD 租用戶的網域服務。*

**補救：**

如果您的 Azure AD 目錄中的 hello 名稱 'AzureActiveDirectoryDomainControllerServices' （具有 d87dcbc6-a371-462e-88e3-28ad15ec4e64 的應用程式識別碼） 的應用程式，請檢查 toosee。 如果此應用程式，您需要 toodelete 它，然後重新啟用 Azure AD 網域服務。

使用下列 PowerShell 指令碼 toofind hello 應用程式的 hello，並將它刪除。

> [!NOTE]
> 此指令碼會使用 **Azure AD PowerShell 第 2 版** Cmdlet。 如需所有可用的 cmdlet 與 toodownload hello 模組的完整清單，讀取 hello [azure Ad PowerShell 參考文件](https://msdn.microsoft.com/library/azure/mt757189.aspx)。
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a>Microsoft Graph 已停用
**錯誤訊息：**

無法在此 Azure AD 租用戶中啟用網域服務。 hello Microsoft Azure AD 應用程式已停用 Azure AD 租用戶中。 啟用與 hello 應用程式識別碼 00000002-0000-0000-c000-000000000000 hello 應用程式，然後再次嘗試 tooenable Azure AD 租用戶的網域服務。

**補救：**

如果您已停用與 hello 識別項 00000002-0000-0000-c000-000000000000 應用程式，請檢查 toosee。 此應用程式是 hello Microsoft Azure AD 應用程式，並提供 Graph API 存取 tooyour Azure AD 租用戶。 Azure AD 網域服務需要您的 Azure AD 租用戶 tooyour 管理此應用程式啟用 toobe toosynchronize 網域。

tooresolve 這個錯誤，請啟用這個應用程式，然後再次嘗試您的 Azure AD 租用戶的 tooenable 網域服務。

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a>使用者會無法 toosign toohello Azure AD 網域服務受管理的網域中
如果您的 Azure AD 租用戶中的一個或多個使用者無法 toosign toohello 新建立的受管理的網域中，執行下列疑難排解步驟的 hello:

* **使用 UPN 格式登入：**再試一次 toosign 使用 hello UPN 的格式 (例如，'joeuser@contoso.com') 而不是 hello SAMAccountName 格式 ('CONTOSO\joeuser')。 hello SAMAccountName 可能自動產生使用者的 UPN 前置詞太長，或 hello 相同 hello 受管理的網域上的其他使用者的身分。 hello UPN 格式會保證 toobe Azure AD 租用戶內的唯一。

> [!NOTE]
> 我們建議使用 hello UPN 格式 toosign toohello Azure AD 網域服務受管理的網域中。
>
>

* 請確定您有[啟用密碼同步處理](active-directory-ds-getting-started-password-sync.md)根據 hello hello 快速入門指南中所述的步驟。
* **外部帳戶：**確保 hello 受影響的使用者帳戶不是在 hello Azure AD 租用戶中的外部帳戶。 外部帳戶的範例包括 Microsoft 帳戶 (例如 joe@live.com) 或來自外部 Azure AD 目錄的使用者帳戶。 由於 Azure AD 網域服務並沒有這類使用者帳戶的認證，這些使用者無法登入 toohello 受管理的網域。
* **同步處理帳戶：**如果 hello 受影響的使用者帳戶會從內部部署目錄同步處理，請確認：

  * 您已部署或更新 toohello[建議的最新版本的 Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594)。
  * 您已設定 Azure AD Connect 太[執行完整同步處理](active-directory-ds-getting-started-password-sync.md)。
  * 根據您目錄中的 hello 大小，可能需要一些時間，使用者帳戶並認證雜湊 toobe 可在 Azure AD 網域服務。 請確定您等待足夠的時間後再重試 （取決於您的目錄-幾個小時 tooa 天，或兩個大型目錄 hello 大小） 的驗證。
  * 如果之後驗證先前步驟的 hello hello 問題持續發生，請嘗試重新啟動 hello Microsoft Azure AD 同步服務。 同步作業機器，啟動命令提示字元並執行下列命令的 hello:

    1. net stop 'Microsoft Azure AD Sync'
    2. net start 'Microsoft Azure AD Sync'
* **僅限雲端帳戶**： 如果 hello 受影響的使用者帳戶是僅限雲端的使用者帳戶，請確定該 hello 使用者在您啟用 Azure AD 網域服務之後變更其密碼。 這個步驟會導致 hello 認證所需的 Azure AD 網域服務 toobe 產生的雜湊。

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a>不會從受管理的網域中移除從 Azure AD 租用戶移除的使用者
Azure AD 會防止您意外刪除使用者物件。 當您刪除使用者帳戶從 Azure AD 租用戶時，hello 對應使用者物件是移動的 toohello 資源回收筒。 當此刪除操作已同步的 tooyour 受管理的網域時，它會導致 hello 對應使用者帳戶 toobe 標示為已停用。 這項功能可協助您復原，或稍後復原 hello 使用者帳戶。

hello 使用者帳戶會保留在 hello 停用受管理的網域中的狀態，即使您重新建立使用者帳戶與 hello 相同 Azure AD 目錄中的 UPN。 您需要 tooforce tooremove hello 受管理的網域中的使用者帳戶，從 Azure AD 租用戶刪除它。

tooremove hello 的使用者帳戶完全受管理的網域中，永久刪除 hello 使用者從 Azure AD 租用戶。 使用具有 hello hello Remove-msoluser PowerShell cmdlet '-RemoveFromRecycleBin' 選項，如下所述[MSDN 文章](https://msdn.microsoft.com/library/azure/dn194132.aspx)。

## <a name="contact-us"></a>與我們連絡
連絡 hello Azure Active Directory 網域服務的產品小組太[分享意見反應或尋求支援](active-directory-ds-contact-us.md)。
