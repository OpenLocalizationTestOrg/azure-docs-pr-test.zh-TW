---
title: "在 Windows 中的 aaaTroubleshoot Azure 檔案儲存體問題 |Microsoft 文件"
description: "針對 Windows 中的 Azure 檔案儲存體問題進行疑難排解"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: ba0315d1add76a27fec93a9aee3aa99ccb7fa164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a>針對 Windows 中的 Azure 檔案儲存體問題進行疑難排解

本文列出常見的問題，則相關的 tooMicrosoft Azure 檔案儲存體，當您從 Windows 用戶端連接。 文中也會提供這些問題的可能原因和解決方案。 此外 toohello 疑難排解這篇文章中的步驟，您也可以使用[AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5)以確保該 hello Windows 用戶端的環境具有正確的必要條件。 AzFileDiagnostics 會自動偵測大部份的本文中提到的 hello 徵狀以及可協助您環境的 tooget 最佳效能設定。 您也可以找到此資訊在 hello [Azure 檔案共用疑難排解](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares)提供步驟 tooassist 連接/對應/掛接 Azure 檔案共用您的問題。


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a>當您嘗試掛接或取消掛接 Azure 檔案共用時發生錯誤 53、錯誤 67 或錯誤 87

當您嘗試的 toomount 檔案共用從內部部署或不同資料中心時，您可能會收到下列錯誤 hello:

- 發生系統錯誤 53。 找不到 hello 網路路徑。
- 發生系統錯誤 67。 找不到 hello 網路名稱。
- 發生系統錯誤 87。 hello 參數不正確。

### <a name="cause-1-unencrypted-communication-channel"></a>原因 1：通訊通道未加密

基於安全性理由，如果沒有加密 hello 通訊通道，並 hello 連接不嘗試從封鎖 tooAzure 檔案共用的連線 hello hello Azure 檔案共用所在的相同資料中心。 只有當 hello 使用者的用戶端作業系統支援 SMB 加密，提供通訊通道加密。

Windows 8、Windows Server 2012 和更新版本的每個系統交涉都要求包含支援加密的 SMB 3.0。

### <a name="solution-for-cause-1"></a>原因 1 的解決方案

從沒有 hello 下列其中一種用戶端連線：

- 符合 Windows 8 和 Windows Server 2012 或更新版本中的 hello 需求
- 會從 hello 中的虛擬機器連線相同資料中心為 hello hello Azure 檔案共用所使用的 Azure 儲存體帳戶

### <a name="cause-2-port-445-is-blocked"></a>原因 2：連接埠 445 遭到封鎖

如果已封鎖連接埠 445 連出通訊 tooan Azure 檔案儲存體資料中心，會發生系統錯誤 53 或系統錯誤 67。 允許或禁止存取連接埠 445 的 Isp toosee hello 摘要太移[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx)。

toounderstand 是否 hello hello 「 系統錯誤 53 」 訊息的原因，您可以使用 Portqry tooquery hello TCP:445 端點。 如果篩選會顯示 hello TCP:445 端點，則會封鎖 hello TCP 連接埠。 查詢範例如下：

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

如果 TCP 通訊埠 445 遭到封鎖 hello 網路路徑的規則，您會看到下列輸出的 hello:

  `TCP port 445 (microsoft-ds service): FILTERED`

如需有關如何 toouse Portqry，請參閱[hello Portqry.exe 命令列公用程式的說明](https://support.microsoft.com/help/310099)。

### <a name="solution-for-cause-2"></a>原因 2 的解決方案

使用您的 IT 部門 tooopen 埠 445 輸出太[Azure IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。

### <a name="cause-3-ntlmv1-is-enabled"></a>原因 3：已啟用 NTLMv1

如果 hello 用戶端上啟用 NTLMv1 通訊不會發生系統錯誤 53 或系統錯誤 87。 Azure 檔案儲存體僅支援 NTLMv2 驗證。 啟用 NTLMv1 會使用戶端變得較不安全。 因此，Azure 檔案儲存體會封鎖通訊。 

toodetermine 是否這是 hello 錯誤的原因 hello，確認下列登錄子機碼的 hello 設定 tooa 值為 3:

**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**

如需詳細資訊，請參閱 hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) TechNet 上的主題。

### <a name="solution-for-cause-3"></a>原因 3 的解決方案

還原 hello **LmCompatibilityLevel**值 3 的下列登錄子機碼的 hello toohello 預設值：

  **HKLM\SYSTEM\CurrentControlSet\Control\Lsa**

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a>錯誤 1816年"沒有足夠的配額是這個命令可用 tooprocess 「 當您複製 tooan Azure 檔案共用

### <a name="cause"></a>原因

當您到達 hello 的並行能用於 hello 檔案共用所掛接的 hello 電腦上檔案的開啟控制代碼的時間上限，就會發生錯誤 1816年。

### <a name="solution"></a>方案

減少 hello 數目同時開啟的控制代碼關閉某些控點，然後再試一次。 如需詳細資訊，請參閱 [Microsoft Azure 儲存體效能與延展性檢查清單](storage-performance-checklist.md)。

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a>複製 tooand 從在 Windows Azure 檔案儲存體的緩慢檔案

當您嘗試 tootransfer 檔案 toohello Azure 檔案服務時，您可能會看到效能變慢。

- 如果您沒有特定的最小 I/O 大小需求，我們建議您使用的是 1 MB，如 hello I/O 大小，以獲得最佳效能。
-   如果您知道 hello 最終大小，您會使用擴充的檔案寫入，且您的軟體沒有相容性問題，當 hello security 的結尾 hello 檔案上包含零，然後設定 hello 檔案大小事先而不是進行每次寫入擴充的寫入。
-   使用 hello 右複製方法：
    -   針對兩個檔案共用之間的所有傳輸，使用 [AzCopy](storage-use-azcopy.md#file-copy)。
    -   在內部部署電腦上的檔案共用之間，使用 [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) \(英文\)。

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a>針對 Windows 8.1 或 Windows Server 2012 R2 的考量

用戶端執行 Windows 8.1 或 Windows Server 2012 R2，請確定該 hello [KB3114025](https://support.microsoft.com/help/3114025)安裝 hotfix。 此 hotfix 可改善建立 hello 效能，並關閉控制代碼。

您可以執行下列指令碼 toocheck 是否已安裝 hello hotfix hello:

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

如果已安裝 hotfix，hello 會顯示下列輸出：

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> 自 2015 年 12 月起，Azure Marketplace 中的 Windows Server 2012 R2 映像預設已安裝 Hotfix KB3114025。

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a>[我的電腦] 中沒有任何含磁碟機代號的資料夾

如果您使用 net 使用對應的 Azure 檔案共用系統管理員身分，hello 共用就會出現 toobe 遺失。

### <a name="cause"></a>原因

根據預設，Windows 檔案總管不會以系統管理員身分執行。 如果您從 系統管理命令提示字元執行 net 使用，您會將 hello 網路磁碟機對應身為系統管理員。 因為對應磁碟機是以使用者為中心，hello 登入的使用者帳戶不會顯示 hello 磁碟機如果它們已掛接於不同的使用者帳戶。

### <a name="solution"></a>方案
從非系統管理員命令列掛接 hello 共用。 或者，您可以依照[本 TechNet 主題](https://technet.microsoft.com/library/ee844140.aspx)tooconfigure hello **EnableLinkedConnections**登錄值。

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a>如果 hello 儲存體帳戶包含正斜線，net use 命令會失敗

### <a name="cause"></a>原因

hello net use 命令會將正斜線 （/） 解譯為命令列選項。 如果您的使用者帳戶名稱開頭是正斜線，hello 磁碟機對應將會失敗。

### <a name="solution"></a>方案

您可以使用其中一個遵循步驟 toowork hello 問題 hello:

- 執行下列 PowerShell 命令的 hello:

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  批次檔中，您可以執行以此方式 hello 命令：

  `Echo new-smbMapping ... | powershell -command –`

- 除非 hello 正斜線 hello 第一個字元，請將雙引號括住 hello 金鑰 toowork 解決這個問題。 如果是，請使用 hello 互動模式，分別輸入您的密碼，或重新產生您的索引鍵 tooget 開頭不是正斜線的索引鍵。

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a>應用程式或服務無法存取掛接的 Azure 檔案儲存體磁碟機

### <a name="cause"></a>原因

磁碟機是按每個使用者掛接。 如果在 hello 裝載 hello 磁碟機的其中一個不同的使用者帳戶下執行應用程式或服務，hello 應用程式不會看到 hello 磁碟機。

### <a name="solution"></a>方案

使用其中一種 hello 下列方案：

-   從 hello 掛接 hello 磁碟機包含 hello 應用程式的相同使用者帳戶。 您可以使用 PsExec 之類的工具。
- 傳入 hello 使用者名稱和密碼參數的 hello net use 命令 hello 儲存體帳戶名稱和金鑰。

請遵循下列指示之後，您可能會收到 hello 時執行 net hello 系統或網路服務帳戶使用，下列錯誤訊息: 「 發生系統錯誤 1312年。 指定的登入工作階段不存在。 可能已被終止。」 如果發生這種情況，請確定傳遞 toonet 使用該 hello 使用者名稱包含網域資訊 (例如:"[儲存體帳戶名稱]。 file.core.windows.net")。

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a>"您要複製不支援加密的檔案 tooa 目的地 」 的錯誤

Hello 網路上複製檔案時，hello 時檔案解密 hello 來源電腦上，以純文字傳送，並重新加密 hello 目的地端。 不過，您可能會看到下列錯誤，當您考慮 toocopy 加密檔案的 hello: 「 您所複製不支援加密的 hello 檔案 tooa 目的地 」。

### <a name="cause"></a>原因
如果您使用加密檔案系統 (EFS)，可能會發生此問題。 BitLocker 加密的檔案可以複製的 tooAzure 檔案存放裝置。 不過，Azure 檔案儲存體不支援 NTFS EFS。

### <a name="workaround"></a>因應措施
toocopy hello 網路上的檔案，您必須先將其解密。 使用其中一種 hello 下列方法：

- 使用 hello**複製 /d**命令。 它可讓加密的 hello toobe 儲存為 hello 目的地端的解密檔案的檔案。
- 設定下列登錄機碼的 hello:
  - 路徑 = HKLM\Software\Policies\Microsoft\Windows\System
  - 數值類型 = DWORD
  - Name = CopyFileAllowDecryptedRemoteDestination
  - Value = 1

請注意該設定 hello 登錄機碼會影響所有的複製作業所 toonetwork 共用。

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決問題。
