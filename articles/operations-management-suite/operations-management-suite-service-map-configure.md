---
title: "aaaConfigure Operations Management Suite 中的服務對應 |Microsoft 文件"
description: "服務對應是一種 Operations Management Suite 解決方案，它會自動探索 Windows 上的應用程式元件和 Linux 系統和對應 hello 服務之間的通訊。 本文會詳細說明如何在環境中部署服務對應並將它用於各種案例。"
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>設定 Operations Management Suite 中的服務對應
服務對應會自動探索 Windows 和 Linux 系統上的應用程式元件和對應 hello 服務之間的通訊。 您可以使用您的伺服器，做為您將它們-提供重要服務的互連系統 tooview。 不需要進行任何設定，只要安裝了代理程式，服務對應就會顯示橫跨任何 TCP 連線架構的伺服器、處理序和連接埠之間的連線。

本文說明 hello 的服務對應和入門訓練的代理程式設定的詳細資料。 如需使用服務對應的資訊，請參閱[使用 Operations Management Suite 中的 hello 服務對應解決方案](operations-management-suite-service-map.md)。

## <a name="dependency-agent-downloads"></a>相依性代理程式下載
| 檔案 | 作業系統 | 版本 | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>連接的來源
服務對應由 hello Microsoft 相依性代理程式取得資料。 hello 相依性代理程式，取決於其連線 tooOperations Management Suite 的 hello OMS 代理程式。 這表示伺服器必須擁有的 hello OMS 代理程式安裝和設定，然後再 hello 可以安裝相依性代理程式。 hello 下表描述 hello 服務對應解決方案支援的 hello 連接來源。

| 連線的來源 | 支援 | 說明 |
|:--|:--|:--|
| Windows 代理程式 | 是 | 服務對應會分析並收集來自 Windows 代理程式電腦的資料。 <br><br>在加法 toohello [OMS Agent](../log-analytics/log-analytics-windows-agents.md)，Windows 代理程式需要 hello Microsoft 相依性代理程式。 請參閱 hello[支援的作業系統](#supported-operating-systems)如需完整的作業系統版本清單。 |
| Linux 代理程式 | 是 | 服務對應會分析並收集來自 Linux 代理程式電腦的資料。 <br><br>在加法 toohello [OMS Agent](../log-analytics/log-analytics-linux-agents.md)，Linux 代理程式需要 hello Microsoft 相依性代理程式。 請參閱 hello[支援的作業系統](#supported-operating-systems)如需完整的作業系統版本清單。 |
| System Center Operations Manager 管理群組 | 是 | 服務對應會在連線的 [System Center Operations Manager 管理群組](../log-analytics/log-analytics-om-agents.md)中，分析並收集來自 Windows 和 Linux 代理程式的資料。 <br><br>直接從 hello System Center Operations Manager 代理程式電腦 tooOperations Management Suite 的資訊需要連接。 從 hello 管理群組 toohello Operations Management Suite 儲存機制，就會轉送資料。|
| Azure 儲存體帳戶 | 否 | 服務對應收集資料從代理程式的電腦，所以沒有從其資料從 Azure 儲存體 toocollect。 |

服務對應僅支援 64 位元平台。

在 Windows 中，hello Microsoft Monitoring Agent (MMA) 會使用 System Center Operations Manager 和 Operations Management Suite toogather 和監視資料傳送。 （此代理程式稱為 hello System Center Operations Manager 代理程式、 OMS 代理程式、 記錄分析代理程式、 MMA 或直接代理程式，視 hello 內容而定）。System Center Operations Manager 和 Operations Management Suite 提供不同外的 hello 方塊 hello MMA 版本。 這些版本可以每個報告 tooSystem Center Operations Manager、 tooOperations Management Suite 或 tooboth。  

在 Linux 上 hello Linux 收集和監視資料 tooOperations Management Suite 的資訊傳送的 OMS 代理程式。 附加的 tooOperations Management Suite，透過 System Center Operations Manager 管理群組的伺服器或與 OMS 直接代理程式伺服器上，您可以使用服務對應。  

在本文中，我們將是否參照 tooall 代理程式-Linux 或 Windows 中，是否連接 tooa System Center Operations Manager 管理群組，或直接 tooOperations Management Suite-如 hello 「 OMS 代理程式 」。 只有當它所需的內容，我們將使用 hello hello 代理程式的特定部署名稱。

hello 服務對應的代理程式不會傳輸任何資料本身，並不需要任何變更 toofirewalls 或連接埠。 服務對應中的 hello 資料一律被經由 hello OMS Agent tooOperations Management Suite，直接或透過 hello OMS 閘道。

![服務對應代理程式](media/oms-service-map/agents.png)

如果您是 System Center Operations Manager 的客戶與管理群組連線 tooOperations Management Suite 的資訊：

- 如果您的 System Center Operations Manager 代理程式能夠存取 hello 網際網路 tooconnect tooOperations Management Suite，其他就不需要設定。  
- 如果您的 System Center Operations Manager 代理程式無法透過 hello 網際網路存取 Operations Management Suite，您需要 tooconfigure hello OMS 閘道 toowork 與 System Center Operations Manager。
  
如果您使用 hello OMS 直接代理程式，您需要 tooconfigure hello OMS 代理程式本身，tooconnect tooOperations Management Suite 的資訊或 tooyour OMS 閘道也一樣。 hello OMS 閘道可以從下載 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666)。

### <a name="management-packs"></a>管理組件
Operations Management Suite 工作區中啟動服務對應時，300 KB 管理組件會傳送 tooall hello Windows 伺服器，該工作區中。 如果您使用 System Center Operations Manager 代理程式在[連線的管理群組](../log-analytics/log-analytics-om-agents.md)，hello 服務對應管理組件從 System Center Operations Manager 部署。 如果 hello 代理程式直接連接，Operations Management Suite 提供 hello 管理組件。

hello 管理組件是名為 Microsoft.IntelligencePacks.ApplicationDependencyMonitor。 它的書面的 too%Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management packs\<。 hello hello 管理組件使用的資料來源為 %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID > \Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll。

## <a name="installation"></a>安裝
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a>在 Microsoft Windows 上安裝 hello 相依性代理程式
系統管理員權限需要的 tooinstall 或解除安裝 hello 代理程式。

hello 相依性代理程式已安裝於 Windows 電腦透過 InstallDependencyAgent Windows.exe。 如果您執行這個可執行檔不使用任何選項時，它會啟動精靈，您可以依照 tooinstall 以互動方式。  

使用下列步驟 tooinstall hello 相依性代理程式在每一部 Windows 電腦上的 hello:

1.  安裝 hello OMS 代理程式使用 hello 指示[連接 Windows Azure 中的記錄分析服務的電腦 toohello](../log-analytics/log-analytics-windows-agents.md)。
2.  下載 hello Windows 代理程式，並執行，請使用下列命令的 hello: <br>`InstallDependencyAgent-Windows.exe`
3.  請遵循 hello 精靈 tooinstall hello 代理程式。
4.  Toostart hello 相依性代理程式時，請檢查 hello 記錄檔以取得詳細的錯誤資訊。 Windows 代理程式上, hello 記錄檔目錄為 %Programfiles%\Microsoft 相依性 Agent\logs。 

#### <a name="windows-command-line"></a>Windows 命令列
使用命令列中的下列資料表 tooinstall hello 的選項。 toosee hello 安裝旗標，使用 hello 執行 hello 安裝程式的清單 /？ 如下所示。

    InstallDependencyAgent-Windows.exe /?

| 旗標 | 說明 |
|:--|:--|
| /? | 取得 hello 命令列選項的清單。 |
| /S | 執行無訊息安裝，不會出現任何使用者提示。 |

根據預設，hello Windows 相依性代理程式的檔案會放置於 C:\Program Files\Microsoft 相依性代理程式。

### <a name="install-hello-dependency-agent-on-linux"></a>Linux 上安裝 hello 相依性代理程式
將根目錄存取必要的 tooinstall 或 hello 代理程式設定。

hello 相依性代理程式會安裝在透過 InstallDependencyAgent Linux64.bin，與自我解壓縮二進位的殼層指令碼的 Linux 電腦上。 您可以使用 sh 執行 hello 檔案或新增執行權限 toohello 檔案本身。
 
使用下列步驟 tooinstall hello 相依性代理程式在每一部 Linux 電腦上的 hello:

1.  安裝 hello OMS 代理程式使用 hello 指示[收集和管理資料從 Linux 電腦](https://technet.microsoft.com/library/mt622052.aspx)。
2.  使用下列命令的 hello，hello Linux 相依性代理程式安裝為根：<br>`sh InstallDependencyAgent-Linux64.bin`
3.  Toostart hello 相依性代理程式時，請檢查 hello 記錄檔以取得詳細的錯誤資訊。 Linux 代理程式，在 hello 記錄目錄不是 /var/opt/microsoft/dependency-agent/log。

toosee hello 安裝旗標，執行與 hello 安裝程式的清單 hello-說明旗標，如下所示。

    InstallDependencyAgent-Linux64.bin -help

| 旗標 | 說明 |
|:--|:--|
| -help | 取得 hello 命令列選項的清單。 |
| -s | 執行無訊息安裝，不會出現任何使用者提示。 |
| --check | 檢查權限與 hello 作業系統，但不是安裝 hello 代理程式。 |

Hello 相依性代理程式的檔案會放置於 hello 下列目錄：

| 檔案 | 位置 |
|:--|:--|
| 核心檔案 | /opt/microsoft/dependency-agent |
| 記錄檔 | /var/opt/microsoft/dependency-agent/log |
| 組態檔 | /etc/opt/microsoft/dependency-agent/config |
| 服務可執行檔 | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| 二進位儲存體檔案 | /var/opt/microsoft/dependency-agent/storage |

## <a name="installation-script-examples"></a>安裝指令碼範例
tooeasily 部署 hello 相依性代理程式在許多伺服器上的一次，它可協助 toouse 指令碼。 您可以使用下列指令碼範例 toodownload hello 和 hello 相依性代理程式安裝在 Windows 或 Linux。

### <a name="powershell-script-for-windows"></a>適用於 Windows 的 PowerShell 指令碼
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>適用於 Linux 的殼層指令碼
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a>期望的狀態設定
toodeploy hello 相依性代理程式透過預期狀態設定，您可以使用 hello xPSDesiredStateConfiguration 模組和有點類似 hello 下列程式碼：
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a>解除安裝
### <a name="uninstall-hello-dependency-agent-on-windows"></a>解除安裝相依性代理程式在 Windows hello
系統管理員可以解除安裝 hello 相依性代理程式的 Windows 控制台。

系統管理員也可以執行 %Programfiles%\Microsoft 相依性 Agent\Uninstall.exe toouninstall hello 相依性代理程式。

### <a name="uninstall-hello-dependency-agent-on-linux"></a>解除安裝 hello Linux 上的相依性代理程式
toocompletely 解除安裝 hello 相依性代理程式從 Linux，您必須移除 hello 代理程式本身並 hello hello 代理程式會自動安裝的連接器。 您可以使用下列單一命令的 hello 同時解除安裝：

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>疑難排解
如果您在安裝或執行服務對應時遇到任何問題，本節內容可以提供協助。 如果您仍然無法解決問題，請連絡 Microsoft 支援服務。

### <a name="dependency-agent-installation-problems"></a>相依性代理程式安裝問題
#### <a name="installer-asks-for-a-reboot"></a>安裝程式會要求重新開機
相依性代理程式 hello*通常*不需要安裝或解除安裝後的重新開機。 不過，在某些罕見的情況下，Windows Server 需要重新開機 toocontinue 與安裝。 這會為相依性，通常 hello Microsoft Visual c + + 可轉散發套件，因為鎖定的檔案需要重新開機。

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a>訊息 「 無法 tooinstall 相依性代理程式： Visual Studio 執行階段程式庫無法 tooinstall (程式碼 = [code_number])"會出現

hello Microsoft 相依性代理程式是建置在 hello Microsoft Visual Studio 執行階段程式庫。 如果在 hello 程式庫安裝期間發生問題，您會收到訊息。 

安裝程式-執行階段程式庫 hello hello %LOCALAPPDATA%\temp 資料夾中建立記錄檔。 hello 檔案是 dd_vcredist_arch_yyyymmddhhmmss.log，其中*arch* 「 x86 」 或 「 amd64 」 和*yyyymmddhhmmss*是 hello 日期和時間 （24 小時制） 建立 hello 記錄時。 hello 記錄提供有關 hello 問題會封鎖安裝詳細資料。

它可能會很有用的 tooinstall hello[最新的執行階段程式庫](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)自行第一次。

hello 下表列出程式碼數字和建議的解決方式。

| 代碼 | 說明 | 解決方案 |
|:--|:--|:--|
| 0x17 | hello 程式庫安裝程式需要尚未安裝 Windows update。 | 查看 hello 最新文件庫安裝程式記錄檔中。<br><br>如果參考太"Windows8.1-KB2999226-x64.msu 」 後面接著一條線 」 錯誤 0x80240017： 失敗的 tooexecute MSU 封裝時，「 您沒有 hello 必要條件 tooinstall KB2999226。 請依照下列中的 hello 必要條件 > 一節中的 hello 指示[通用的 C 執行階段中 Windows](https://support.microsoft.com/kb/2999226)。 您可能會需要 toorun Windows Update 並多次重新開機順序 tooinstall hello 必要條件。<br><br>重新執行 hello Microsoft 相依性代理程式安裝程式。 |

### <a name="post-installation-issues"></a>安裝後問題
#### <a name="server-doesnt-appear-in-service-map"></a>伺服器未出現在服務對應中
如果您的相依性代理程式安裝成功，但您沒有看到您的伺服器 hello 服務對應方案：
* Hello 相依性代理程式安裝成功？ 您可以藉由檢查 toosee，如果 hello 服務已安裝並執行驗證這點。<br><br>
**Windows**： 尋找 hello 服務名為 「 Microsoft 相依性代理程式 」。<br>
**Linux**： 尋找 hello 執行程序 「 microsoft-相依性-代理程式。 」

* 您位於 hello[免費定價層的 Operations Management Suite/Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)？ hello 免費方案允許 toofive 唯一的服務對應伺服器。 任何後續伺服器則不會顯示在服務對應，即使 hello 先前五個不會再傳送資料。

* 是您伺服器傳送記錄檔和效能資料 tooOperations Management Suite 的資訊？ 移 tooLog 搜尋，並執行下列查詢，為您的電腦的 hello: 

        * Computer="<your computer name here>" | measure count() by Type
        
  您在 hello 結果中取得各種事件？ 是新 hello 資料嗎？ 如果是這樣，您的 OMS 代理程式是運作正常，而與 hello Operations Management Suite 服務通訊。 如果沒有，請檢查您的伺服器上的 OMS 代理程式 hello: [OMS Agent for Windows 疑難排解](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues)或[OMS Agent for Linux 疑難排解](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md)。

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>伺服器顯示在服務對應中，但是沒有任何處理序
如果您看到您在服務對應的伺服器，但有任何程序或連接的資料，表示該 hello 相依性代理程式已安裝且正在執行，但未載入 hello 核心驅動程式。 

請檢查 hello C:\Program Files\Microsoft 相依性 Agent\logs\wrapper.log 檔案 (Windows) 或 /var/opt/microsoft/dependency-agent/log/service.log 檔案 (Linux)。 hello hello 檔案最後一行應該指出為什麼 hello 核心未載入。 例如，hello 核心可能不支援在 Linux 上如果更新您的核心。

## <a name="data-collection"></a>資料收集
您可以預期每個代理程式 tootransmit 大約每日，視您系統相依性是在多複雜的 25 MB。 每個代理程式每隔 15 秒就會傳送服務對應相依性資料。  

hello 相依性代理程式通常會耗用 0.1%的系統記憶體和 0.1%的系統 CPU。

## <a name="supported-azure-regions"></a>支援的 Azure 區域
服務對應是目前可用於下列 Azure 區域的 hello:
- 美國東部
- 西歐
- 美國中西部


## <a name="supported-operating-systems"></a>受支援的作業系統
hello 下列各節列出 hello 支援的作業系統 hello 相依性代理程式。 服務對應不支援任何 32 位元架構的作業系統。

### <a name="windows-server"></a>Windows Server
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

### <a name="windows-desktop"></a>Windows 桌面
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux、CentOS Linux 和 Oracle Linux (搭載 RHEL 核心)
- 只支援預設版本和 SMP Linux 核心版本。
- 所有 Linux 散發套件皆不支援非標準的核心版本 (例如 PAE 和 Xen)。 例如，"2.6.16.21-0.8-xen"hello 版本字串的系統不支援。
- 不支援自訂核心，包括重新編譯的標準核心。
- 不支援 CentOSPlus 核心。
- Oracle Unbreakable Enterprise Kernel (UEK) 在本文稍後的章節有相關討論。


#### <a name="red-hat-linux-7"></a>Red Hat Linux 7
| 作業系統版本 | 核心版本 |
|:--|:--|
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7.2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6
| 作業系統版本 | 核心版本 |
|:--|:--|
| 6.0 | 2.6.32-71 |
| 6.1 | 2.6.32-131 |
| 6.2 | 2.6.32-220 |
| 6.3 | 2.6.32-279 |
| 6.4 | 2.6.32-358 |
| 6.5 | 2.6.32-431 |
| 6.6 | 2.6.32-504 |
| 6.7 | 2.6.32-573 |
| 6.8 | 2.6.32-642 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5
| 作業系統版本 | 核心版本 |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18-417<br>2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux 搭載 Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6
| 作業系統版本 | 核心版本
|:--|:--|
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| 作業系統版本 | 核心版本
|:--|:--|
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11
| 作業系統版本 | 核心版本
|:--|:--|
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10
| 作業系統版本 | 核心版本
|:--|:--|
| 10 SP4 | 2.6.16.60 |

## <a name="diagnostic-and-usage-data"></a>診斷和使用量資料
Microsoft 會自動收集貴用戶使用服務對應服務的 hello 的使用方式和效能資料。 Microsoft 會使用此資料 tooprovide 並提升 hello 品質、 安全性與 hello 服務對應服務的完整性。 資料包括您的軟體，如作業系統和版本 hello 組態相關資訊。 它也會包含 IP 位址、 DNS 名稱和工作站名稱中順序 tooprovide 正確且有效率地疑難排解功能。 我們不會收集姓名、地址或其他連絡資訊。

如需有關資料收集與使用方式的詳細資訊，請參閱 hello [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132)。



## <a name="next-steps"></a>後續步驟
- 了解如何太[使用服務對應](operations-management-suite-service-map.md)部署和設定之後。
