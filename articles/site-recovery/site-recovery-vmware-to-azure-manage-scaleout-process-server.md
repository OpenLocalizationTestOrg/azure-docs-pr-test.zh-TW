---
title: " 在 Azure Site Recovery 中管理相應放大處理序伺服器 | Microsoft Doc"
description: "本文說明如何 tooset 及管理 Azure Site Recovery 中的向外延展處理序伺服器。"
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a>管理相應放大處理序伺服器

向外延展處理序伺服器做為協調器 hello 站台復原服務與您在內部部署基礎結構之間資料傳輸。 本文說明如何設定、配置及管理相應放大處理序伺服器。

## <a name="prerequisites"></a>必要條件
hello 下面是 hello 建議的硬體、 軟體和網路所需設定 tooset 向上擴充處理序伺服器。

> [!NOTE]
> [容量規劃](site-recovery-capacity-planner.md)是您部署與設定向外延展處理序伺服器 hello 該套件的重要步驟 tooensure 負載需求。 請在[相應放大處理序伺服器的調整特性](#sizing-requirements-for-a-configuration-server)中閱讀更多資訊。

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a>下載 hello 向外延展處理序伺服器軟體
1. 登入 toohello Azure 入口網站，並瀏覽 tooyour 復原服務保存庫。
2. 瀏覽過**Site Recovery 基礎結構** > **設定伺服器**（底下的 VMware & 實體機器)。
3. 清單中選取您設定伺服器 toodrill 到 hello 組態伺服器的詳細資料頁面。
4. 按一下 hello **+ 處理序伺服器** 按鈕。
5. 在 hello**加入處理序伺服器**頁面上，選取**向外延展部署處理序伺服器在內部**選項從 hello**選擇您希望 toodeploy 處理序伺服器**下拉式清單中。

  ![新增伺服器頁面](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. 按一下 hello**下載 hello Microsoft Azure Site Recovery 統一的安裝**連結 toodownload hello 最新版本的 hello 向外延展處理序伺服器安裝。

  > [!WARNING]
  hello 向外延展處理伺服器的版本應該相等 tooor 小於 hello 組態伺服器版本，在您的環境中執行。 簡單的方式 tooensure 版本相容性層級是 toouse hello 相同，您最近使用過 tooinstall/更新組態伺服器的安裝程式位元。

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a>從 GUI 安裝並註冊相應放大處理序伺服器
如果您有 tooscale 出您的部署超過 200 的來源機器，或總每日變換率超過 2 TB，您會需要額外的處理序伺服器 toohandle hello 流量磁碟區。

檢查 hello[大小處理序伺服器的建議](#size-recommendations-for-the-process-server)，然後遵循這些指示 tooset，hello 的處理序伺服器。 設定好 hello 伺服器之後，您將移轉來源機器 toouse 它。

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a>使用命令列安裝並註冊相應放大處理序伺服器

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a>範例用法
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a>相應放大處理序伺服器安裝程式命令列引數。
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a>建立 Proxy 設定組態檔案
ProxySettingsFilePath 參數使用檔案做為輸入。 使用下列格式，並將它傳遞做為輸入 ProxySettingsFilePath 參數 hello 建立檔案。
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a>修改相應放大處理序伺服器的 Proxy 設定
1. 登入您的相應放大處理序伺服器。
2. 開啟系統管理 PowerShell 命令視窗。
3. 執行下列命令的 hello
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. 下一步瀏覽 toohello 目錄**%PROGRAMDATA%\ASR\Agent**和 hello 執行下列命令
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a>重新註冊相應放大處理序伺服器
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* 接下來，開啟系統管理命令提示字元。
* 瀏覽 toohello 目錄**%PROGRAMDATA%\ASR\Agent**執行 hello 命令

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a>升級相應放大處理序伺服器
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a>將相應放大處理序伺服器解除委任
1. 請確定：
  - 組態伺服器的連線狀態會顯示成**Connected** hello Azure 入口網站中
  - 使用 hello 組態伺服器仍然可以 toocommunicate 為處理序伺服器。
2. 系統管理員身分登入 toohello 處理序伺服器
3. 開啟 [控制台] > [程式] > [解除安裝程式]
4. Hello 順序指定下列中的 hello 程式解除安裝：
  * Microsoft Azure Site Recovery 設定伺服器/處理序伺服器
  * Microsoft Azure Site Recovery 設定伺服器相依性
  * Microsoft Azure 復原服務代理程式

可能需要向上 too15 分鐘 hello 處理序伺服器刪除 tooreflect hello Azure 入口網站中。

  > [!NOTE]
  Hello 處理序伺服器是否以 hello 組態伺服器無法 toocommunicate (入口網站中的連接狀態為 Disconnected，) 則需要 toofollow hello 下列步驟 toopurge 它從 hello 組態伺服器。

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a>從設定伺服器中將已中斷連線的相應放大處理序伺服器取消註冊

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a>相應放大處理序伺服器的調整大小需求

| **額外處理序伺服器** | **快取磁碟大小** | **資料變更率** | **受保護的機器** |
| --- | --- | --- | --- |
|4 個 vCPU (2 個通訊端 * 雙核心 @ 2.5 GHz)，8 GB 記憶體 |300 GB |250 GB 或更少 |複寫 85 部或更少的機器。 |
|8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，12 GB 記憶體 |600 GB |250 GB too1 TB |複寫 85-150 部機器。 |
|12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，24 GB 記憶體 |1 TB |1 TB too2 TB |複寫 150-225 部機器。 |
