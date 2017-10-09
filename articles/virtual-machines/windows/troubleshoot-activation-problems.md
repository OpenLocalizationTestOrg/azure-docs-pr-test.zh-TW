---
title: "在 Azure 中的 aaaTroubleshoot Windows 虛擬機器啟用問題 |Microsoft 文件"
description: "提供 hello 疑難排解在 Azure 中修正 Windows 虛擬機器啟用問題的步驟"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a>針對 Azure Windows 虛擬機器啟用問題進行疑難排解

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

如果您無法啟用 Azure Windows 虛擬機器 (VM)，建立從自訂映像時，您可以使用此文件 tootroubleshoot hello 問題中提供的 hello 資訊。 

## <a name="symptom"></a>徵狀

當您嘗試 tooactivate Azure Windows VM 時，您會收到錯誤訊息類似下列範例中的 hello:

**錯誤： 無法啟動該 hello 電腦回報 0xC004F074 hello 軟體 LicensingService。無法聯繫金鑰管理服務 (KMS)。請 hello 應用程式事件記錄檔，如需詳細資訊，參閱。**

## <a name="cause"></a>原因
一般而言，Azure VM 啟用問題發生原因 hello Windows VM 並未設定使用 hello 適當的 KMS 用戶端安裝識別碼，或是 hello Windows VM 有連線問題 toohello Azure KMS 服務 （kms.core.windows.net、 連接埠 1668年）。 

## <a name="solution"></a>方案

>[!NOTE]
>如果您使用站對站 VPN，而且強制通道，請參閱[使用 Azure 自訂路由 tooenable KMS 啟用強制通道](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx)。 
>
>如果您使用 ExpressRoute，您有已發佈的預設路由，請參閱[Azure VM 可能會透過 ExpressRoute 失敗 tooactivate](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx)。

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a>步驟 1 設定 hello 適當的 KMS 用戶端安裝識別碼 （適用於 Windows Server 2016 和 Windows Server 2012 R2）

Hello 從 Windows Server 2016 或 Windows Server 2012 R2 的自訂映像建立的 VM，您必須設定 hello 適當的 KMS 用戶端安裝識別碼 hello VM。

TooWindows 2012 或 Windows 2008 R2，則不適用此步驟。 它會使用 hello 自動化虛擬機器啟用 (AVMA) 功能，才支援 Windows Server 2016 和 Windows Server 2012 R2。

1. 在提升權限的命令提示字元執行 **slmgr.vbs /dlv**。 檢查 hello hello 輸出中的描述值，然後決定是否已建立從零售 （零售通路） 或磁碟區 (VOLUME_KMSCLIENT) 授權媒體：
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. 如果**slmgr.vbs /dlv**顯示零售通路，執行下列命令 tooset hello hello [KMS 用戶端安裝識別碼](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396)hello 版本的 Windows Server 正在使用，而且強制它 tooretry 啟用： 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    比方說，Windows Server 2016 資料中心，您可以執行下列命令的 hello:

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a>步驟 2 確認 hello 連線之間 hello VM 和 Azure KMS 服務

1. 下載並解壓縮 hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) hello VM，不會啟動的工具 tooa 本機資料夾。 

2. 移 tooStart 搜尋 Windows PowerShell、 Windows PowerShell 中，以滑鼠右鍵按一下，然後選取 以系統管理員身分執行。

3. 請確定該 vm 的 hello 設定 toouse hello 正確的 Azure KMS 伺服器。 toodo 這點，執行下列命令：
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    hello 命令應該會傳回： 金鑰管理服務的電腦名稱設定 tookms.core.windows.net:1688 成功。

4. 使用 Psping 您有連線能力 toohello KMS 伺服器驗證。 切換 toohello hello Pstools.zip 下載、 解壓縮的資料夾，然後執行 hello 下列：
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  在 hello 輸出 hello 倒數第二行，請確定您看到： 傳送 = 4，已接收 = 4，遺失 = 0 （0%遺失）。

  如果遺失大於 0 （零），hello VM 並沒有連線 toohello KMS 的伺服器。 在此情況下，如果 hello VM 虛擬網路中，且具有自訂指定的 DNS 伺服器，您必須確定該 DNS 伺服器是可以 tooresolve kms.core.windows.net。 或者，變更解決 kms.core.windows.net hello DNS 伺服器 tooone。

  請注意，如果您從虛擬網路中移除所有 DNS 伺服器，VM 將會使用 Azure 的內部 DNS 服務。 此服務可以解析 kms.core.windows.net。
  
也請確認尚未設定 hello 客體防火牆會封鎖啟用嘗試的方式。

5. 驗證成功的連線 tookms.core.windows.net 之後，執行下列命令，該高權限的 Windows PowerShell 提示字元的 hello。 此命令會多次嘗試啟用。

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

成功的啟用會傳回類似 hello 下列資訊：

**正在啟用 Windows(R) Server Datacenter 版本 (12345678-1234-1234-1234-12345678) … 產品已成功啟用。**

## <a name="faq"></a>常見問題集 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a>我可以建立 Windows Server 2016 hello Azure marketplace。 需要啟動 Windows Server 2016 hello tooconfigure KMS 金鑰嗎？ 
 
否。 在 Azure Marketplace 中的 hello 影像的 hello 適當的 KMS 用戶端安裝識別碼已經設定。 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a>沒有 Windows 啟動工作 hello 相同方式不論如果 hello VM 或不使用 Azure 混合式使用權益 （集線器）？ 
 
是。 
 
### <a name="what-happens-if-windows-activation-period-expires"></a>如果 Windows 啟用期間已到期，會發生什麼情況？ 
 
當 hello 寬限期已過期，仍然未啟用 Windows，Windows Server 2008 R2 和更新版本的 Windows 會顯示啟動相關的其他通知。 hello 桌面底色圖案維持黑色，以及安全性和重大更新，但不是選擇性的更新，將會安裝 Windows Update。 請參閱 hello 通知區段底部 hello hello[授權條件](http://technet.microsoft.com/en-us/library/ff793403.aspx)頁面。   

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。
