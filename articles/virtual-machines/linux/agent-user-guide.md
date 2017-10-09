---
title: "aaaAzure Linux VM 代理程式概觀 |Microsoft 文件"
description: "深入了解如何 tooinstall 及設定 Linux 代理程式 (waagent) toomanage Azure 網狀架構控制器的虛擬機器的互動。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a>了解與使用 hello Azure Linux 代理程式
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>簡介
hello Microsoft Azure Linux 代理程式 (waagent) 管理 Linux 和 FreeBSD 佈建、 和 VM 與 hello Azure 網狀架構控制器之間的互動。 它提供下列功能適用於 Linux 和 FreeBSD IaaS 部署的 hello:

> [!NOTE]
> 請參閱 hello Azure Linux 代理程式[讀我檔案](https://github.com/Azure/WALinuxAgent/blob/master/README.md)如需詳細資訊。
> 
> 

* **映像佈建**
  
  * 建立使用者帳戶
  * 設定 SSH 驗證類型
  * 部署 SSH 公開金鑰和金鑰組
  * 設定 hello 主機名稱
  * 發行 hello 主機名稱 toohello 平台 DNS
  * 報告 SSH 主機金鑰指紋 toohello 平台
  * 資源磁碟管理
  * 格式化及裝載 hello 資源磁碟
  * 設定交換空間
* **網路功能**
  
  * 管理路由 tooimprove 相容性與平台 DHCP 伺服器
  * 可確保 hello 穩定性的 hello 網路介面名稱
* **核心**
  
  * 設定虛擬 NUMA (核心 < 2.6.37 時停用)
  * 取用 /dev/random 的 Hyper-V Entropy
  * 設定 hello 根裝置 （這可能是遠端） 的 SCSI 逾時
* **診斷**
  
  * 主控台重新導向 toohello 序列連接埠
* **SCVMM 部署**
  
  * 偵測到與 System Center Virtual Machine Manager 2012 R2 環境中執行時 bootstraps hello 適用於 Linux 的 VMM 代理程式
* **VM 延伸模組**
  
  * 插入至 Linux VM (IaaS) tooenable 軟體和設定自動化，由 Microsoft 和協力廠商所撰寫的元件
  * VM 延伸模組參考實作，網址為 [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>通訊
透過兩個通道，就會發生 hello 從 hello 平台 toohello 代理程式的資訊流程：

* 在 IaaS 部署中，開機時連接的 DVD。 此 DVD 包含 OVF 相容的組態檔，其中包含實際 SSH 金鑰組 hello 以外的所有佈建資訊。
* TCP 端點會公開 REST API 用 tooobtain 部署和拓撲設定。

## <a name="requirements"></a>需求
hello 下列系統都已測試過與已知 toowork 以 hello Azure Linux 代理程式：

> [!NOTE]
> 這份清單可能會有所不同 hello 官方份支援的系統上 hello Microsoft Azure 平台，如下所述： [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3+
* Red Hat Enterprise Linux 6.7+
* Debian 7.0+
* Ubuntu 12.04+
* openSUSE 12.3+
* SLES 11 SP3+
* Oracle Linux 6.4+

其他支援的系統：

* FreeBSD 10+ (Azure Linux 代理程式 v2.0.10+)

hello Linux 代理程式取決於某些系統中的封裝順序 toofunction 正確：

* Python 2.6+
* OpenSSL 1.0+
* OpenSSH 5.3+
* 檔案系統公用程式：sfdisk、fdisk、mkfs、parted
* 密碼工具：chpasswd、sudo
* 文字處理工具：sed、grep
* 網路工具：ip-route
* 掛接 UDF 檔案系統的核心支援。

## <a name="installation"></a>安裝
從您的發佈封裝儲存機制使用 RPM 或 DEB 套件的安裝是慣用的 hello 方法安裝和升級 hello Azure Linux 代理程式。 所有的 hello[背書發佈提供者](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)整合其映像和儲存機制中的 hello Azure Linux 代理程式套件。

請參閱 toohello 文件以 hello [Azure Linux 代理程式在 GitHub 上的儲存機制](https://github.com/Azure/WALinuxAgent)進階的安裝選項，例如安裝從來源或 toocustom 位置或前置詞。

## <a name="command-line-options"></a>命令列選項
### <a name="flags"></a>旗標
* verbose：提高指定命令的詳細程度
* force：略過某些命令的互動式確認

### <a name="commands"></a>命令
* 說明： 列出支援的 hello 命令和旗標。
* 取消佈建： 嘗試 tooclean hello 系統，並使其適用於重新佈建。 這項作業會刪除下列 hello:
  
  * 所有 SSH 主機金鑰 （如果 Provisioning.RegenerateSshHostKeyPair 'y' hello 組態檔中）
  * /etc/resolv.conf 中的名稱伺服器設定
  * 從 /etc/shadow （如果 Provisioning.DeleteRootPassword 'y' hello 組態檔中的） 的根密碼
  * 快取的 DHCP 用戶端租用
  * 重設主機名稱 toolocalhost.localdomain

> [!WARNING]
> 取消佈建不保證該 hello 映像時，所有的機密資訊的清除，而且適用於轉散發。
> 
> 

* 取消佈建 + 使用者： 執行下方-取消佈建 （如上） 的所有內容也會刪除 hello （取自 /var/lib/waagent） 最後一個佈建的使用者帳戶和相關聯的資料。 此參數是為了取消佈建 Azure 上先前佈建的映像檔，以便擷取並重複使用。
* 版本： 顯示 hello waagent 版本
* serialconsole： 設定幼蟲 toomark ttyS0 (hello 第一個序列連接埠) 為 hello 啟動主控台。 這樣可以確保核心開機記錄會傳送 toothe 序列通訊埠供偵錯。
* 精靈： hello 平台服務精靈 toomanage 互動以執行 waagent。 這個引數是指定的 toowaagent hello waagent 初始化指令碼中。
* 開始︰以背景處理序方式執行 waagent

## <a name="configuration"></a>組態
組態檔 (/ etc/waagent.conf) 控制項 hello waagent 的動作。 範例組態檔如下所示：

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

下面將詳細說明各種組態選項的 hello。 組態選項可分成三種：布林、字串或整數。 hello 布林組態選項可以指定為"y"或"n"。 hello"None"可用於某些字串類型組態項目有詳細說明下列特殊關鍵字。

**Provisioning.Enabled：**  
型別︰布林值  
預設：y

這可讓 hello 使用者 tooenable 或停用 hello 佈建在 hello 代理程式的功能。 有效值為 "y" 或 "n"。 佈建已停用，SSH hello 映像中的主控件與使用者金鑰會保留，且會忽略 hello Azure 佈建應用程式開發介面中指定的任何設定。

> [!NOTE]
> hello`Provisioning.Enabled`太"n"用於佈建雲端 init Ubuntu 雲端映像上的參數預設值。
> 
> 

**Provisioning.DeleteRootPassword：**  
型別︰布林值  
預設：n

如果設定，在 hello /etc/hosts 陰影檔案中的 hello 根密碼會清除期間 hello 佈建程序。

**Provisioning.RegenerateSshHostKeyPair：**  
型別︰布林值  
預設：y

如果設定，所有 SSH 主機金鑰組 （ecdsa、 dsa 和 rsa） 刪除期間 hello 從 /etc/ssh/佈建程序。 還會產生單一全新的金鑰組。

hello hello 全新的金鑰組的加密類型為可設定由 hello Provisioning.SshHostKeyPairType 項目。 請注意某些會重新建立任何遺失的加密類型的 SSH 金鑰組 hello SSH 服務精靈重新啟動 （例如，在重新開機） 時。

**Provisioning.SshHostKeyPairType：**  
類型：字串  
預設：rsa

這可以設定 tooan 加密演算法支援的型別 hello hello 虛擬機器上的 SSH 服務精靈。 hello 通常支援值為"rsa"、"dsa"和"ecdsa"。 請注意，Windows 的 "putty.exe" 不支援 "ecdsa"。 因此，如果您要 toouse putty.exe Windows tooconnect tooa Linux 部署，請使用"rsa"或"dsa"。

**Provisioning.MonitorHostName：**  
型別︰布林值  
預設：y

如果設定，waagent 會監視 hello Linux 虛擬機器的主機名稱變更 （hello"hostname"命令所傳回），並自動更新 hello hello 影像 tooreflect hello 變更中的網路設定。 順序 toopush hello 名稱中變更 toohello DNS 伺服器、 網路功能會以 hello 虛擬機器重新啟動。 這會導致網際網路連線短暫中斷。

**Provisioning.DecodeCustomData**  
型別︰布林值  
預設：n

如果設定，waagent 會從 CustomData 將 Base64 解碼。

**Provisioning.ExecuteCustomData**  
型別︰布林值  
預設：n

如果設定，waagent 將在佈建之後執行 CustomData。

**Provisioning.PasswordCryptId**  
型別︰字串  
預設︰6

產生密碼雜湊時由 crypt 使用的演算法。  
 1 - MD5  
 2a - Blowfish  
 5-SHA-256  
 6 - SHA-512  

**Provisioning.PasswordCryptSaltLength**  
型別︰字串  
預設值︰10

產生密碼雜湊時使用的隨機 salt 長度。

**ResourceDisk.Format：**  
型別︰布林值  
預設：y

如果設定，hello hello 平台所提供的資源磁碟會格式化並掛接 waagent"ResourceDisk.Filesystem 」 中的 hello 使用者所要求的 hello filesystem 類型是否"ntfs"以外的任何項目。 Linux (83) 類型的單一分割區可供 hello 磁碟上。 請注意，如果可順利掛接此磁碟分割，則不會格式化。

**ResourceDisk.Filesystem：**  
類型：字串  
預設：ext4

這會指定 hello hello 資源磁碟的檔案系統類型。 支援的值隨 Linux 散發套件而不同。 如果 X，然後 mkfs hello 字串。X 應會出現在 hello Linux 映像上。 SLES 11 映像檔通常會使用 'ext3'。 在此，FreeBSD 映像檔應該是使用 'ufs2'。

**ResourceDisk.MountPoint：**  
類型：字串  
預設值：/mnt/resource 

這會指定 hello 掛載 hello 資源磁碟時的路徑。 請注意該 hello 資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。

**ResourceDisk.MountOptions**  
類型：字串  
預設值︰無

指定磁碟掛接選項傳遞 toobe toohello 掛接-o 命令。 這是以逗號分隔的值清單，例如： 'nodev,nosuid'。 如需詳細資訊，請參閱 Mount(8)。

**ResourceDisk.EnableSwap：**  
型別︰布林值  
預設：n

如果設定，成為分頁檔 (/ 交換檔) hello 資源的磁碟上建立和加入 toohello 系統交換空間。

**ResourceDisk.SwapSizeMB：**  
型別︰整數  
預設值：0

hello 的 hello 分頁檔，以 mb 為單位的大小。

**Logs.Verbose：**  
型別︰布林值  
預設：n

如果設定，則記錄詳細程度會提高。 Waagent 記錄 too/var/log/waagent.log，並可運用 hello 系統 logrotate 功能 toorotate 記錄檔。

**OS.EnableRDMA**  
型別︰布林值  
預設：n

如果設定，hello 代理程式會嘗試 tooinstall，然後載入符合 hello 韌體版本的 hello hello 基礎硬體上的 RDMA 核心驅動程式。

**OS.RootDeviceScsiTimeout：**  
型別︰整數  
預設值︰300

這會以秒為單位 hello OS 磁碟和資料磁碟機上設定 hello SCSI 逾時。 如果沒有設定，hello 系統會使用預設值。

**OS.OpensslPath：**  
類型：字串  
預設值︰無

這可以是使用的 toospecify hello openssl 二進位 toouse 密碼編譯作業的替代路徑。

**HttpProxy.Host, HttpProxy.Port**  
類型：字串  
預設值︰無

如果設定，hello 代理程式將使用此 proxy 伺服器 tooaccess hello 網際網路。 

## <a name="ubuntu-cloud-images"></a>Ubuntu 雲端映像
請注意，利用 Ubuntu 雲端映像[雲端 init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform 許多組態工作，否則會由管理 hello Azure Linux 代理程式。  請注意下列差異 hello:

* **Provisioning.Enabled**太"n"使用佈建工作的雲端 init tooperform Ubuntu 雲端映像上的預設值。
* 下列組態參數的 hello 有不會影響使用雲端 init toomanage hello 資源磁碟和交換空間的 Ubuntu 雲端映像：
  
  * **ResourceDisk.Format**
  * **ResourceDisk.Filesystem**
  * **ResourceDisk.MountPoint**
  * **ResourceDisk.EnableSwap**
  * **ResourceDisk.SwapSizeMB**
* 請參閱下列資源 tooconfigure hello 資源磁碟掛接點的 hello 和佈建期間交換 Ubuntu 雲端映像上的空間：
  
  * [Ubuntu Wiki：設定交換資料分割](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [將自訂資料插入 Azure 虛擬機器](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

