---
title: "aaaPrepare Windows VHD tooupload tooAzure |Microsoft 文件"
description: "如何上傳 tooAzure 之前 tooprepare Windows VHD 或 VHDX"
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a>準備 Windows VHD 或 VHDX tooupload tooAzure
您上傳 Windows 虛擬機器 (VM) 從內部部署 tooMicrosoft Azure 之前，您必須準備 hello 虛擬硬碟 （VHD 或 VHDX）。 Azure 支援 hello VHD 檔案格式而且有固定大小的磁碟第 1 代 Vm。 hello 最大允許 hello VHD 為 1023 GB。 您可以將轉換層代 1 的 VM 從 hello VHDX 檔案系統 tooVHD 和 toofixed 大小動態擴充磁碟。 但您無法變更 VM 的世代。 如需詳細資訊，請參閱[應該在 Hyper-V 中建立第 1 代還是第 2 代的 VM](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v) \(英文\)。

Azure vm hello 支援原則的相關資訊，請參閱[Microsoft 伺服器軟體支援的 Microsoft Azure Vm](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)。

> [!Note]
> 本文章中的 hello 指示適用於 toohello 64 位元版本的 Windows Server 2008 R2 或更新版本的 Windows 伺服器作業系統。 如需 Azure 中執行 32 位元版本的作業系統相關資訊，請參閱[在 Azure 虛擬機器中對 32 位元作業系統的支援](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines) \(機器翻譯\)。

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a>轉換 hello 虛擬磁碟 tooVHD 和固定的大小磁碟 
如果您需要 tooconvert 虛擬磁碟 toohello 所需格式 Azure 中，使用本節中的 hello 方法之一。 您執行 hello 虛擬磁碟轉換程序，並確定該 hello Windows VHD hello 本機伺服器運作正常之前，請備份 hello VM。 請解決所有錯誤 hello VM 本身內 tooconvert 再試一次，或將它上傳 tooAzure 之前。

在轉換 hello 磁碟之後，建立會使用轉換的 hello 磁碟的 VM。 啟動和登入 toohello VM toofinish hello VM 準備上傳。

### <a name="convert-disk-using-hyper-v-manager"></a>使用 HYPER-V 管理員轉換磁碟
1. 開啟 HYPER-V 管理員，然後選取 本機電腦上 hello 左邊。 在 hello hello 電腦清單上方的功能表，按一下 **動作** > **編輯磁碟**。
2. 在 hello**尋找虛擬硬碟**畫面上，找出並選取您的虛擬磁碟。
3. 在 hello**選擇動作**畫面上，，然後選取**轉換**和**下一步**。
4. 如果您需要從 VHDX tooconvert，選取**VHD** ，然後按一下**下一步**
5. 如果您需要從動態擴充磁碟 tooconvert，選取**固定大小**，然後按一下**下一步**
6. 找出並選取路徑 toosave hello 新 VHD 的檔案。
7. 按一下 [完成] 。

>[!NOTE]
>這篇文章中的 hello 命令必須以提高權限的 PowerShell 工作階段執行。

### <a name="convert-disk-by-using-powershell"></a>使用 PowerShell 轉換磁碟
您可以將虛擬磁碟轉換使用 hello [CONVERT-VHD](http://technet.microsoft.com/library/hh848454.aspx) Windows PowerShell 命令。 當您啟動 PowerShell 時，選取 [以系統管理員身分執行]。 

hello 下列範例命令會將轉換從 VHDX tooVHD 及動態擴充磁碟 toofixed 大小：

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
此命令中取代 hello 值"-路徑"hello 路徑 toohello 虛擬硬碟，您想要 tooconvert 和 hello 值為"-DestinationPath"hello 新路徑和名稱 hello 轉換磁碟。

### <a name="convert-from-vmware-vmdk-disk-format"></a>從 VMware VMDK 磁碟格式進行轉換
如果您的 Windows VM 映像在 hello [VMDK 檔案格式](https://en.wikipedia.org/wiki/VMDK)，會將其轉換 tooa VHD 使用 hello [Microsoft VM 轉換器](https://www.microsoft.com/download/details.aspx?id=42497)。 如需詳細資訊，請參閱 hello 部落格文章[如何 tooConvert VMware VMDK tooHyper V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx)。

## <a name="set-windows-configurations-for-azure"></a>設定適用於 Azure 的 Windows 設定

在 hello 您計劃的 VM 上 tooupload tooAzure，執行所有的命令在 hello 下列步驟從[提升權限的命令提示字元視窗](https://technet.microsoft.com/library/cc947813.aspx):

1. 移除任何持續性的靜態路由，在 hello 路由表：
   
   * tooview hello 路由表執行`route print`hello 的命令提示字元。
   * 檢查 hello**持續性路由**區段。 如果持續性的路由，請使用[路由刪除](https://technet.microsoft.com/library/cc739598.apx)tooremove 它。
2. 移除 hello WinHTTP proxy:
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. 設定得 hello 磁碟 SAN 原則[Onlineall](https://technet.microsoft.com/library/gg252636.aspx)。 
   
    ```PowerShell
    diskpart 
    ```
    在 hello 開啟命令提示字元視窗中，輸入下列命令的 hello:

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. 設定適用於 Windows 的國際標準時間 (UTC) 時間和太 hello hello (w32time) 的 Windows 時間服務的啟動類型**自動**:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. 設定 hello 電源設定檔 toohello**高效能**:

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a>檢查 hello Windows 服務
請確定每個 hello 下列 Windows 服務已設定 toohello **Windows 預設值**。 這些是必須設定 toomake 確定該 hello VM 已連線的服務的 hello 最小的數字。 tooreset hello 啟動設定，請執行下列命令的 hello:
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a>更新遠端桌面登錄設定
請確定該 hello 下列設定已正確設定遠端桌面連線：

>[!Note] 
>您可能會收到錯誤訊息，當您執行 hello **Set-itemproperty-路徑 ' HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal 服務-名稱&lt;物件名稱&gt;&lt;值&gt;**在這些步驟。 hello 錯誤訊息可以放心忽略。 這表示只有該 hello 網域不會將推送透過群組原則物件，該組態。
>
>

1. 遠端桌面通訊協定 (RDP) 已啟用：
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. hello RDP 連接埠已正確設定時 （預設連接埠 3389）：
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    當您部署 VM 時，則會針對連接埠 3389 建立 hello 預設規則。 如果您想 toochange hello 連接埠號碼，可在動作 hello VM 部署在 Azure 中。

3. hello 接聽項接聽中的每個網路介面：
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. 設定 hello hello RDP 連線的網路層級驗證模式：
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. 設定 hello 持續作用值：
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. 重新連線：
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. 限制並行連線數目 hello:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. 如果有任何自我簽署的憑證繫結 toohello RDP 接聽程式，請將它們移除：
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    這是 toomake 確定當您部署的 hello VM 可以連接您在 hello 開頭。 您也可以檢閱這在稍後階段之後視需要在 Azure 中部署 VM 的 hello。

9. 如果 hello VM 是網域的一部分，請檢查所有 hello 下列設定 toomake 確定 hello 先前的設定不會還原。 您必須核取的 hello 原則包括 hello 下列：
    
    - RDP 已啟用：

         電腦設定\原則\Windows 設定\系統管理範本\元件\遠端桌面服務\遠端桌面工作階段主機\連線：
         
         **允許使用者 tooconnect 從遠端使用遠端桌面**

    - NLA 群組原則：

        設定\系統管理範本\元件\遠端桌面服務\遠端桌面工作階段主機\安全性： 
        
        **透過使用網路層級驗證以要求對遠端連線進行使用者驗證**
    
    - Keep Alive 設定：

        電腦設定\原則\Windows 設定\系統管理範本\Windows 元件\遠端桌面服務\遠端桌面工作階段主機\連線： 
        
        **設定 Keep-Alive 連線間隔**

    - 重新連線設定：

        電腦設定\原則\Windows 設定\系統管理範本\Windows 元件\遠端桌面服務\遠端桌面工作階段主機\連線： 
        
        **自動重新連線**

    - Hello 的數目限制設定連線：

        電腦設定\原則\Windows 設定\系統管理範本\Windows 元件\遠端桌面服務\遠端桌面工作階段主機\連線： 
        
        **限制連線數目**

## <a name="configure-windows-firewall-rules"></a>設定 Windows 防火牆規則
1. 開啟 Windows 防火牆 （網域、 標準和公用） 的 hello 三個設定檔：

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. 執行下列命令在 PowerShell tooallow WinRM 透過 hello 三個防火牆設定檔 （網域、 私人和公用） 中的 hello 和啟用 PowerShell 遠端服務的 hello:
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. 啟用下列防火牆規則 tooallow hello RDP 流量 hello 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. 啟用 hello 檔案和印表機共用規則 hello VM 可以回應 hello 虛擬網路內的 tooa ping 命令：

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. 如果 hello VM 是網域的一部分，請檢查下列設定 toomake 確定 hello 先前的設定不會還原 hello。 您必須核取的 hello AD 原則包括 hello 下列：

    - 啟用 hello Windows 防火牆設定檔

        電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\網域設定檔\Windows 防火牆: **保護所有網路連線**

       電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\標準設定檔\Windows 防火牆: **保護所有網路連線**

    - 啟用 RDP 

        電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\網域設定檔\Windows 防火牆: **允許輸入的遠端桌面例外**

        電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\標準設定檔\Windows 防火牆: **允許輸入的遠端桌面例外**

    - 啟用 ICMP-V4

        電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\網域設定檔\Windows 防火牆: **允許 ICMP 例外**

        電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\標準設定檔\Windows 防火牆: **允許 ICMP 例外**

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a>確認 VM 處於狀況良好、安全且可使用 RDP 存取 
1. 確定 hello 磁碟 toomake 是狀況良好且維持一致，在 hello 下次 VM 重新啟動執行檢查磁碟作業：

    ```PowerShell
    Chkdsk /f
    ```
    請確定 hello 報告會顯示清除且狀況良好的磁碟。

2. 設定 hello 開機設定資料 (BCD) 設定。 

    > [!Note]
    > 請確定您是在提升權限的 CMD 視窗上執行這些命令，而**不是**在 PowerShell 上：
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. 請確認該 hello Windows 管理 Instrumentations 存放庫是一致。 tooperform 下列命令，執行的 hello:

    ```PowerShell
    winmgmt /verifyrepository
    ```
    如果 hello 儲存機制已損毀，請參閱[WMI： 資料庫損毀，或不](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not)。

4. 請確定任何應用程式不使用 hello 連接埠 3389。 Hello RDP 服務在 Azure 中使用此連接埠。 您可以執行**netstat anob** toosee 使用的通訊埠是在 hello VM:

    ```PowerShell
    netstat -anob
    ```

5. 如果您想 tooupload Windows VHD hello 網域控制站，然後執行下列步驟：

    A. 請遵循[這些額外的步驟](https://support.microsoft.com/kb/2904015)tooprepare hello 磁碟。

    B. 請確定您知道 hello DSRM 密碼，如果您有 DSRM toostart hello VM 在某個時間點。 您可能會想 toorefer toothis 連結 tooset hello [DSRM 密碼](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx)。

6. 請確定 hello 內建系統管理員帳戶和密碼已知 tooyou。 您可能想 tooreset hello 目前本機系統管理員密碼，並確定您可以透過 RDP 連線 hello tooWindows 中使用此帳戶 toosign。 此存取權限是由 hello 「 允許登入遠端桌面服務透過 「 群組原則物件所控制。 您可以在 hello 本機群組原則編輯器中檢視此物件下：

    電腦設定\Windows 設定\安全性設定\本機原則\使用者權限指派

7. 請檢查下列 AD hello 原則 toomake 確定您不會封鎖您的 RDP 存取透過 RDP 或從 hello 網路：

    - 電腦設定 \windows 設定 \ 安全性設定 \ 原則 \ 使用者權限 Assignment\Deny 存取 toothis 電腦從 hello 網路

    - 電腦設定\Windows 設定\安全性設定\本機原則\使用者權限指派\拒絕從遠端桌面服務登入


8. 確定 Windows 是仍狀況良好的重新啟動 hello VM toomake 可以達到使用 hello RDP 連接。 此時，您可能想在您本機 HYPER-V toomake 確定 hello VM 正在啟動完全 toocreate VM，然後測試是否可以連線的 RDP。

9. 移除任何額外的傳輸驅動程式介面篩選，例如分析 TCP 封包的軟體或額外的防火牆。 您也可以檢閱這在稍後階段之後視需要在 Azure 中部署 VM 的 hello。

10. 解除安裝任何其他第三方軟體及相關的 toophysical 元件或其他虛擬化技術的驅動程式。

### <a name="install-windows-updates"></a>安裝 Windows 更新
hello 的理想組態太**有在最新 hello hello 機器 hello 修補程式等級**。 如果不可行，請確定已安裝下列更新該 hello:

|                       |                   |           |                                       最低檔案版本 x64       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| 元件               | Binary            | Windows 7 & Windows Server 2008 R2 | Windows 8 & Windows Server 2012             | Windows 8.1 & Windows Server 2012 R2 | Windows 10 & Windows Server 2016 RS1 | Windows 10 RS2             |
| 儲存體                 | disk.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17638 / 6.2.9200.21757 - KB3137061 | 6.3.9600.18203 - KB3137061           | -                                    | -                          |
|                         | storport.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17188 / 6.2.9200.21306 - KB3018489 | 6.3.9600.18573 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.332             |
|                         | ntfs.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17623 / 6.2.9200.21743 - KB3121255 | 6.3.9600.18654 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.447             |
|                         | Iologmsg.dll      | 6.1.7601.23403 - KB3125574         | 6.2.9200.16384 - KB2995387                  | -                                    | -                                    | -                          |
|                         | Classpnp.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17061 / 6.2.9200.21180 - KB2995387 | 6.3.9600.18334 - KB3172614           | 10.0.14393.953 - KB4022715           | -                          |
|                         | Volsnap.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17047 / 6.2.9200.21165 - KB2975331 | 6.3.9600.18265 - KB3145384           | -                                    | 10.0.15063.0               |
|                         | partmgr.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.16681 - KB2877114                  | 6.3.9600.17401 - KB3000850           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | volmgr.sys        |                                    |                                             |                                      |                                      | 10.0.15063.0               |
|                         | Volmgrx.sys       | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | 10.0.15063.0               |
|                         | Msiscsi.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.21006 - KB2955163                  | 6.3.9600.18624 - KB4022726           | 10.0.14393.1066 - KB4022715          | 10.0.15063.447             |
|                         | Msdsm.sys         | 6.1.7601.23403 - KB3125574         | 6.2.9200.21474 - KB3046101                  | 6.3.9600.18592 - KB4022726           | -                                    | -                          |
|                         | Mpio.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.21190 - KB3046101                  | 6.3.9600.18616 - KB4022726           | 10.0.14393.1198 - KB4022715          | -                          |
|                         | Fveapi.dll        | 6.1.7601.23311 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.18294 - KB3172614           | 10.0.14393.576 - KB4022715           | -                          |
|                         | Fveapibase.dll    | 6.1.7601.23403 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.17415 - KB3172614           | 10.0.14393.206 - KB4022715           | -                          |
| 網路                 | netvsc.sys        | -                                  | -                                           | -                                    | 10.0.14393.1198 - KB4022715          | 10.0.15063.250 - KB4020001 |
|                         | mrxsmb10.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.22108 - KB4022724                  | 6.3.9600.18603 - KB4022726           | 10.0.14393.479 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb20.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.21548 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb.sys        | 6.1.7601.23816 - KB4022722         | 6.2.9200.22074 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | tcpip.sys         | 6.1.7601.23761 - KB4022722         | 6.2.9200.22070 - KB4022724                  | 6.3.9600.18478 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.447             |
|                         | http.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17285 - KB3042553                  | 6.3.9600.18574 - KB4022726           | 10.0.14393.251 - KB4022715           | 10.0.15063.483             |
|                         | vmswitch.sys      | 6.1.7601.23727 - KB4022719         | 6.2.9200.22117 - KB4022724                  | 6.3.9600.18654 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.138             |
| 核心                    | ntoskrnl.exe      | 6.1.7601.23807 - KB4022719         | 6.2.9200.22170 - KB4022718                  | 6.3.9600.18696 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.483             |
| 遠端桌面服務問題 | rdpcorets.dll     | 6.2.9200.21506 - KB4022719         | 6.2.9200.22104 - KB4022724                  | 6.3.9600.18619 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.0               |
|                         | termsrv.dll       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17048 - KB2973501                  | 6.3.9600.17415 - KB3000850           | 10.0.14393.0 - KB4022715             | 10.0.15063.0               |
|                         | termdd.sys        | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | win32k.sys        | 6.1.7601.23807 - KB4022719         | 6.2.9200.22168 - KB4022718                  | 6.3.9600.18698 - KB4022726           | 10.0.14393.594 - KB4022715           | -                          |
|                         | rdpdd.dll         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | rdpwd.sys         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
| 安全性                | 到期 tooWannaCrypt | KB4012212                          | KB4012213                                   | KB4012213                            | KB4012606                            | KB4012606                  |
|                         |                   |                                    | KB4012216                                   |                                      | KB4013198                            | KB4013198                  |
|                         |                   | KB4012215                          | KB4012214                                   | KB4012216                            | KB4013429                            | KB4013429                  |
|                         |                   |                                    | KB4012217                                   |                                      | KB4013429                            | KB4013429                  |
       
### 當 toouse sysprep<a id="step23"></a>    

Sysprep 是您可能會遇到將會重設 hello 安裝 hello 系統也會提供 「 全新 hello 體驗 」 移除所有的個人資料，以及重設數個元件的 windows 安裝程序。 您通常這樣如果您想 toocreate 範本，您可以用來部署數個其他的 Vm，有特定的設定。 這稱為**一般化映像**。

相反地，若要唯一 toocreate 其中一個 VM 從一個磁碟，您不需要 toouse sysprep。 在此情況下，您就可以建立從什麼 VM 就所謂的 hello**特製化映像**。

如需有關如何 toocreate 將 VM 從專用的磁碟，請參閱：

- [從特殊化磁碟建立 VM](create-vm-specialized.md)
- [從特殊化 VHD 磁碟建立 VM](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

如果您想 toocreate 一般化映像，您會需要 toorun sysprep。 如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。 

並非 Windows 電腦上安裝的每個角色或應用程式都支援這個一般化。 之前在將您執行此程序，請參閱下列文章 toomake 確定 toohello 該電腦的該 hello 角色支援 sysprep。 如需詳細資訊，請參閱[伺服器角色的 Sysprep 支援](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) \(英文\)。

### <a name="steps-toogeneralize-a-vhd"></a>步驟 toogeneralize VHD

>[!NOTE]
> 您當做下列步驟中所指定的 hello 執行 sysprep.exe 之後，關閉 hello VM，並請勿開啟它回直到您從它建立映像在 Azure 中。

1. 登入 toohello Windows VM。
2. 以系統管理員身分執行**命令提示字元**。 
3. 若要變更 hello 目錄： **%windir%\system32\sysprep**，然後執行**sysprep.exe**。
3. 在 hello**系統準備工具**對話方塊中，選取**進入系統的全新體驗 (OOBE)**，並確定該 hello**一般化**選取核取方塊。

    ![系統準備工具](media/prepare-for-upload-vhd-image/syspre.png)
4. 在 [關機選項] 中選取 [關機]。
5. 按一下 [確定] 。
6. Sysprep 完成時，關閉 hello VM。 請勿使用**重新啟動**tooshut hello VM 關閉。
7. Hello VHD 已準備好 toobe 上傳。 如需有關如何 toocreate 將 VM 從一般化磁碟，請參閱[一般化的 VHD 上傳，並在 Azure 中使用新的 Vm toocreate](sa-upload-generalized.md)。


## <a name="complete-recommended-configurations"></a>完成建議的設定
下列設定的 hello 不會影響上傳 VHD。 不過，我們強烈建議您設定它們。

* 安裝 hello [Azure Vm 代理程式](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 然後您可以啟用 VM 擴充功能。 hello VM 延伸模組實作大部分的 hello 重要功能，您可能會想 toouse 要與您的 Vm，例如，重設密碼、 設定 RDP，等等。 如需詳細資訊，請參閱：

    - [VM 代理程式與擴充功能 - 第 1 部分](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/) \(英文\)
    - [VM 代理程式與擴充功能 - 第 2 部分](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) \(英文\)
* hello 傾印記錄檔可以是 Windows 損毀問題的疑難排解很有幫助。 啟用 hello 傾印記錄檔收集：
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    如果您收到本文章中步驟的任何 hello 程序期間所發生的任何錯誤，這表示相同的 hello 登錄機碼已存在。 在此情況下，使用 hello 改用下列命令：

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  Hello VM 在 Azure 中建立之後，我們建議您將 hello 分頁檔放在 hello 「 暫存磁碟機 」 磁碟區 tooimprove 效能。 您可以如下方式設定這部分：

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
如果沒有任何資料磁碟附加的 toohello VM，hello 暫存磁碟機磁碟區的磁碟機代號通常是 「 D." 這項指定可能是根據 hello 數目可用的磁碟機和 hello 進行設定，而不同。

## <a name="next-steps"></a>後續步驟
* [上傳 Windows VM 映像 tooAzure 資源管理員部署](upload-generalized-managed.md)

