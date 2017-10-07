---
title: "aaaMonitoring Linux VM 的 VM 延伸模組與 |Microsoft 文件"
description: "了解如何 toouse hello Linux 診斷延伸模組 toomonitor hello 效能和診斷資料，在 Azure 中 Linux 虛擬機器。"
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a>使用 hello Linux 診斷延伸模組 toomonitor hello 效能和診斷資料的 Linux VM

本文件說明 2.3 版 hello Linux 診斷延伸模組。

> [!IMPORTANT]
> 此版本已被取代，且可能會在 2018 年 6 月 30 日之後取消發佈。 3.0 版已取代該版本。 如需詳細資訊，請參閱 hello [3.0 版的 hello Linux 診斷延伸模組的文件](../diagnostic-extension.md)。

## <a name="introduction"></a>簡介

(**注意**: hello Linux 診斷延伸模組是開放上[GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic)其中第一次發行 hello hello 擴充功能上最新的資訊。 您可能會想 toocheck hello [GitHub 頁面](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic)第一次。)

hello Linux 診斷延伸模組可協助使用者監視 hello Microsoft Azure 執行的 Linux Vm。 它有下列功能的 hello:

* 會收集和上傳 hello Linux VM toohello 使用者的儲存體資料表，包括診斷及 syslog 資訊中的 hello 系統效能資訊。
* 可讓使用者 toocustomize hello 資料度量資訊會收集和上傳。
* 可讓使用者 tooupload 指定的記錄檔 tooa 指定之儲存體資料表。

在目前版本 2.3 hello，hello 資料包括：

* 所有 Linux Rsyslog 記錄檔，包括系統、安全性及應用程式記錄檔。
* 所有的系統資料上所指定[hello System Center 跨平台解決方案網站](https://scx.codeplex.com/wikipage?title=xplatproviders)。
* 使用者指定的記錄檔。

這項擴充功能的運作方式與傳統的 hello 和資源管理員部署模型。

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a>新版的 hello 擴充功能和已被取代的舊版本

hello hello 延伸模組的最新版本是**2.3**，和**會取代任何舊版本 （2.0、 2.1 和 2.2），而且未發行的本年度 (2017) 結束**。 如果您停用自動次要版本升級安裝 hello Linux 診斷延伸模組，強烈建議您解除安裝 hello 擴充功能，並重新安裝已啟用自動的次要版本升級。 在傳統 (ASM) Vm，您可以達到這個目的藉由指定 '2.*' hello 版本，如果您要安裝 hello 延伸模組，透過 Azure XPLAT CLI 或 Powershell。 在 ARM Vm 上您可以達到這包括 '"autoUpgradeMinorVersion": true' hello VM 部署範本中。 此外，hello 延伸模組的任何新的安裝應有 hello 自動次要版本升級已開啟選項。

## <a name="enable-hello-extension"></a>啟用 hello 擴充功能

您可以啟用此延伸模組使用 hello [Azure 入口網站](https://portal.azure.com/#)，Azure PowerShell 或 Azure CLI 指令碼。

tooview 並設定 hello 系統的效能資料直接從 hello Azure 入口網站，請遵循[hello Azure 部落格上的這些步驟](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/)。

本文著重在如何 tooenable 和使用 Azure CLI 命令設定 hello 延伸模組。 這可讓您直接從 hello 儲存體資料表的 tooread 並檢視 hello 資料。

請注意，此處所述的 hello 組態方法不適用於 hello Azure 入口網站。 tooview 和設定 hello 系統和效能資料，直接從 hello Azure 入口網站中，必須透過 hello 入口網站啟用 hello 延伸模組。

## <a name="prerequisites"></a>必要條件

* **Azure Linux Agent 2.0.6 版或更新版本**。

  請注意，大部分的 Azure VM Linux 資源庫映像包含版本 2.0.6 或更新版本。 您可以執行**WAAgent-版本**tooconfirm hello VM 所安裝的版本。 如果 hello VM 執行早於 2.0.6 版本，您可以依照[這些指示在 GitHub 上的](https://github.com/Azure/WALinuxAgent "指示")tooupdate 它。
* **Azure CLI**。 請遵循[本指南中的有關安裝 CLI](../../../cli-install-nodejs.md) tooset hello Azure CLI 環境，您的電腦上。 安裝 Azure CLI 之後，您可以使用 hello **azure**命令從命令列介面 （Bash、 終端機或命令提示字元） tooaccess hello Azure CLI 命令。 例如：

  * 執行 **azure vm extension set --help** 取得詳細的說明資訊。
  * 執行**azure 登入**toosign tooAzure 中的。
  * 執行**azure vm 清單**toolist 所有 hello 您尚未在 Azure 的虛擬機器。
* 儲存體帳戶 toostore hello 資料。 您必須是先前所建立的儲存體帳戶名稱和存取金鑰 tooupload hello 資料 tooyour 存放裝置。

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a>使用 hello Azure CLI 命令 tooenable hello Linux 診斷延伸模組

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a>案例 1. 啟用 hello 與 hello 預設資料集的延伸模組

在版本 2.3 或更新版本中，將收集的 hello 預設資料包括：

* 所有 Rsyslog 資訊 (包括系統、安全性及應用程式記錄檔)。  
* 一組核心基礎系統資料。 請注意 hello 完整資料集，會說明 hello [System Center 跨平台解決方案網站](https://scx.codeplex.com/wikipage?title=xplatproviders)。
  如果您想 tooenable 額外的資料，繼續在案例 2 和 3 中的 hello 執行步驟。

步驟 1. 建立名為 privateconfig.json 的檔案以 hello 下列內容：

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

步驟 2. 執行 **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**。

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a>案例 2. 自訂 hello 效能監視度量

本章節描述如何 toocustomize hello 效能和診斷資料的資料表。

步驟 1. 建立名為 privateconfig.json 的檔案，以案例 1 所述的 hello 內容的檔案。 同時也建立名為 PublicConfig.json 的檔案。 指定您想要 toocollect hello 特定資料。

所有支援的提供者和變數，參考 hello [System Center 跨平台解決方案網站](https://scx.codeplex.com/wikipage?title=xplatproviders)。 您可以擁有多個查詢，並將其儲存在多個資料表中，藉由附加多個查詢 toohello 指令碼。

根據預設，永遠都會收集 hello Rsyslog 資料。

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


步驟 2. 執行 **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**。

### <a name="scenario-3-upload-your-own-log-files"></a>案例 3. 上傳您自己的記錄檔

本章節描述如何 toocollect 和上傳的特定記錄檔檔案 tooyour 儲存體帳戶。 您需要 toospecify 這兩個 hello 路徑 tooyour 記錄檔案和 hello 名稱 hello 資料表所在 toostore 您的記錄檔。 您可以加入多個檔案/資料表項目 toohello 指令碼，以建立多個記錄檔。

步驟 1. 建立名為 privateconfig.json 的檔案，以案例 1 所述的 hello 內容的檔案。 然後建立名為 PublicConfig.json hello 下列的其他檔案內容：

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

步驟 2. 執行 `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`。

請注意，這項設定在擴充功能版本先前 too2.3 hello，所有的記錄寫入太`/var/log/mysql.err`太可能會重複`/var/log/syslog`(或`/var/log/messages`根據 hello Linux distro) 以及。 如果您想要 tooavoid 記錄此複本，您可以排除記錄`local6`記錄 rsyslog 組態中的功能。 它相依於 hello Linux distro 中，但在 Ubuntu 14.04 系統上，hello 檔案 toomodify`/etc/rsyslog.d/50-default.conf`而且您可以取代 hello 列`*.*;auth,authpriv.none -/var/log/syslog`太`*.*;auth,authpriv,local6.none -/var/log/syslog`。 已修正此問題在 hello 最新 hotfix 版本的 2.3 (2.3.9007)，因此如果您擁有 hello 擴充功能版本 2.3，應該不會發生此問題。 如果仍有即使之後重新啟動您的 VM，請與我們連絡，並協助我們進行疑難排解，hello 最新的 hotfix 版本不會自動安裝。

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a>案例 4. 停止收集任何記錄檔的 hello 延伸模組

本章節描述 toostop hello 延伸模組，從收集的記錄檔。 即使使用本次將仍會啟動並執行 hello 監視代理程式處理序的附註。 如果您想要 toostop hello 完全監視代理程式處理序，您可以藉由停用 hello 延伸模組。 hello 命令 toodisable hello 延伸模組是`azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`。

步驟 1. 建立名為 privateconfig.json 的檔案，以案例 1 所述的 hello 內容的檔案。 建立名為 hello 遵循 PublicConfig.json 的另一個檔案的內容：

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


步驟 2. 執行 **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**。

## <a name="review-your-data"></a>檢閱資料

hello 效能和診斷資料會儲存在 Azure 儲存體資料表中。 檢閱[如何 toouse 從 Ruby 的 Azure 資料表儲存體](../../../cosmos-db/table-storage-how-to-use-ruby.md)toolearn tooaccess hello 儲存體中的 hello 資料資料表使用 Azure CLI 指令碼的方式。

此外，您可以使用下列 UI 工具 tooaccess hello 資料：

1. Visual Studio 伺服器總管。 移 tooyour 儲存體帳戶。 Hello VM 執行大約五分鐘之後，您會看到 hello 四個預設資料表:"LinuxCpu"、"LinuxDisk"、"LinuxMemory 」 和 「 Linuxsyslog"。 按兩下 hello 資料表名稱 tooview hello 資料。
1. [Azure 儲存體總管](https://azurestorageexplorer.codeplex.com/ "Azure 儲存體總管")。

![image](./media/diagnostic-extension/no1.png)

如果您已啟用 fileCfg 或 perfCfg （如案例 2 和 3 所述），您可以使用 Visual Studio 伺服器總管和 Azure 儲存體總管 tooview 非預設的資料。

## <a name="known-issues"></a>已知問題

* hello Rsyslog 資訊和客戶指定記錄檔只可透過指令碼存取。
