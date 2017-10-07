---
title: " 在 Azure Site Recovery 中管理組態伺服器 | Microsoft Doc"
description: "本文說明如何 tooset 和管理組態伺服器。"
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a>管理組態伺服器

設定伺服器將充當 hello 站台復原服務與您在內部部署基礎結構之間的協調者。 本文說明如何設定、 設定和管理 hello 組態伺服器。

## <a name="prerequisites"></a>必要條件
hello 下面是 hello 最低硬體、 軟體和組態伺服器的網路所需設定 tooset。

> [!NOTE]
> [容量規劃](site-recovery-capacity-planner.md)是您部署與設定的組態伺服器 hello 該套件的重要步驟 tooensure 負載需求。 深入了解[組態伺服器的大小需求](#sizing-requirements-for-a-configuration-server)。

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a>下載 hello 組態伺服器軟體
1. 登入 toohello Azure 入口網站，並瀏覽 tooyour 復原服務保存庫。
2. 瀏覽過**Site Recovery 基礎結構** > **設定伺服器**（底下的 VMware & 實體機器)。

  ![新增伺服器頁面](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. 按一下 hello **+ 伺服器** 按鈕。
4. 在 hello**新增伺服器**頁面上，按一下 hello 下載按鈕 toodownload hello 登錄機碼。 您需要此金鑰期間 hello 組態伺服器安裝 tooregister 它與 Azure Site Recovery 服務。
5. 按一下 hello**下載 hello Microsoft Azure Site Recovery 統一的安裝**連結 toodownload hello 最新版本的 hello 組態伺服器。

  ![下載頁面](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  可以直接從下載最新版本的組態伺服器 hello [Microsoft Download Center 下載頁面](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>從 GUI 安裝和註冊組態伺服器
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>使用命令列安裝和註冊組態伺服器

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a>範例用法
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a>組態伺服器安裝程式命令列引數。
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a>建立 MySql 認證檔案
MySQLCredsFilePath 參數使用檔案做為輸入。 建立使用下列格式，並將它傳遞做為輸入 MySQLCredsFilePath 參數 hello hello 檔案。
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>建立 Proxy 設定組態檔案
ProxySettingsFilePath 參數使用檔案做為輸入。 建立使用下列格式，並將它傳遞做為輸入 ProxySettingsFilePath 參數 hello hello 檔案。

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>修改組態伺服器的 Proxy 設定
1. 登入 tooyour 組態伺服器。
2. 啟動 hello cspsconfigtool.exe 上使用 hello 快顯程式。
3. 按一下 hello**保存庫註冊** 索引標籤。
4. 從 hello 入口網站下載新的保存庫註冊檔，並提供它當做輸入的 toohello 工具。

  ![註冊組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. 提供 hello 新 Proxy 伺服器詳細資料，並按一下 hello**註冊** 按鈕。
6. 開啟系統管理 PowerShell 命令視窗。
7. 執行下列命令的 hello
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  如果您有向外延展處理伺服器附加 toothis 組態伺服器，您需要[hello 向外延展程序的所有伺服器上，請修正 hello proxy 設定](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server)部署中。

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a>重新註冊組態伺服器 hello 與相同的復原服務保存庫
  1. 登入 tooyour 組態伺服器。
  2. 啟動 hello cspsconfigtool.exe 使用 hello 捷徑在桌面上。
  3. 按一下 hello**保存庫註冊** 索引標籤。
  4. 從 hello 入口網站下載新的登錄檔案，並提供它當做輸入的 toohello 工具。
        ![註冊組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. 提供 hello Proxy 伺服器詳細資料，並按一下 hello**註冊** 按鈕。  
  6. 開啟系統管理 PowerShell 命令視窗。
  7. 執行下列命令的 hello

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  如果您有向外延展處理伺服器附加 toothis 組態伺服器，您需要[重新註冊所有 hello 向外延展處理伺服器](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server)部署中。

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>向不同的復原服務保存庫註冊組態伺服器。
1. 登入 tooyour 組態伺服器。
2. 系統管理員命令提示字元中，從執行 hello 命令

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. 啟動 hello cspsconfigtool.exe 上使用 hello 快顯程式。
4. 按一下 hello**保存庫註冊** 索引標籤。
5. 從 hello 入口網站下載新的登錄檔案，並提供它當做輸入的 toohello 工具。

    ![註冊組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. 提供 hello Proxy 伺服器詳細資料，並按一下 hello**註冊** 按鈕。  
7. 開啟系統管理 PowerShell 命令視窗。
8. 執行下列命令的 hello
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>解除委任組態伺服器
在開始解除委任設定伺服器之前，請確定 hello 下列。
1. 停用保護此組態伺服器下的所有虛擬機器。
2. 取消關聯從 hello 組態伺服器的所有複寫原則。
3. 刪除所有相關聯的 toohello 組態伺服器的 Vcenter 伺服器 /vsphere 主機。

### <a name="delete-hello-configuration-server-from-azure-portal"></a>從 Azure 入口網站刪除 hello 組態伺服器
1. 在 Azure 入口網站，瀏覽過**Site Recovery 基礎結構** > **設定伺服器**功能表 hello 保存庫。
2. 按一下您想 toodecommission 組態伺服器 hello。
3. 在 hello 組態伺服器的詳細資料頁面上，按一下 hello 刪除 按鈕。

  ![刪除組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. 按一下**是**tooconfirm hello hello 伺服器刪除。

  >[!WARNING]
  如果您有任何虛擬機器、 複寫原則或 vCenter 伺服器 /vsphere 主機與這個組態伺服器相關聯，您無法刪除 hello 伺服器。 您嘗試 toodelete hello 保存庫之前，請刪除這些實體。

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a>解除安裝 hello 組態伺服器軟體和其相依性
  > [!TIP]
  如果您計劃 tooreuse hello 與 Azure Site Recovery 的組態伺服器一次，然後您可以略過 toostep 4 直接

1. 系統管理員身分登入 toohello 組態伺服器。
2. 開啟 [控制台] > [程式] > [解除安裝程式]
3. 解除安裝 hello 下列順序中的 hello 程式：
  * Microsoft Azure 復原服務代理程式
  * Microsoft Azure Site Recovery Mobility Service/主要目標伺服器
  * Microsoft Azure Site Recovery Provider
  * Microsoft Azure Site Recovery 組態伺服器/處理序伺服器
  * Microsoft Azure Site Recovery 組態伺服器相依性
  * MySQL Server 5.5
4. 執行下列命令從 hello 和系統管理員命令提示字元。
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>更新組態伺服器安全通訊端層 (SSL) 憑證
設定伺服器 hello 可以協調 hello 活動 hello 行動服務處理序伺服器的內建網頁伺服器與主要目標伺服器連接 toohello 組態伺服器。 hello 組態伺服器的網頁伺服器會使用 SSL 憑證 tooauthenticate 其用戶端。 此憑證有三年後的到期，而且可以使用下列方法 hello 隨時更新：

> [!WARNING]
只有在 9.4.XXXX.X 或更新版本上才會履行憑證到期日。 升級所有 hello Azure Site Recovery 元件 （組態伺服器、 處理序伺服器、 主要目標伺服器、 行動服務） 開始 hello 更新憑證的工作流程之前。

1. 在 hello Azure 入口網站中，瀏覽 tooyour 保存庫 > Site Recovery 基礎結構 > 組態伺服器。
2. 按一下您需要 toorenew hello 組態伺服器 hello 的 SSL 憑證。
3. 在 hello 設定伺服器健全狀況，您可以看到 hello hello SSL 憑證的到期日。
4. 依序按一下 hello 更新 hello 憑證**更新憑證**動作 hello 下列影像所示：

  ![刪除組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>安全通訊端層憑證到期警告

> [!NOTE]
hello 2016 年之前所發生的所有安裝的 SSL 憑證的有效設定 tooone 年。 您已開始看到 hello Azure 入口網站中顯示的憑證到期通知。

1. 如果 hello 組態伺服器的 SSL 憑證將會在 hello tooexpire 接下來的兩個月，hello 服務會啟動通知的使用者經由 hello Azure 入口網站 （& s） （您需要訂閱 toobe tooAzure Site Recovery 通知） 的電子郵件。 您會開始在 hello 保存庫資源 頁面上看到通知橫幅。

  ![憑證通知](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. 按一下 hello 憑證到期日的 hello 橫幅 tooget 其他詳細資料。

  ![憑證詳細資料](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  如果您不是看到 [立即更新] 按鈕，而是 [立即升級] 按鈕， 這表示您的環境中尚未升級的 too9.4.xxxx.x 或更高版本的部分元件。

## <a name="sizing-requirements-for-a-configuration-server"></a>組態伺服器的大小需求

| **CPU** | **記憶體** | **快取磁碟大小** | **資料變更率** | **受保護的機器** |
| --- | --- | --- | --- | --- |
| 8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz) |16 GB |300 GB |500 GB 或更少 |複寫少於 100 部電腦。 |
| 12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz) |18 GB |600 GB |500 GB too1 TB |複寫 100-150 部機器。 |
| 16 個 vCPU (2 個插槽 * 8 核心 @ 2.5GHz) |32 GB |1 TB |1 TB too2 TB |複寫 150-200 部機器。 |

  >[!TIP]
  如果您每日的資料變換量超過 2 TB，或您計劃 tooreplicate 200 個以上的虛擬機器，則建議 toodeploy 額外的處理序伺服器 tooload 平衡 hello 複寫流量。 深入了解如何 toodeploy 向外延展處理序伺服器。


## <a name="common-issues"></a>常見問題
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
