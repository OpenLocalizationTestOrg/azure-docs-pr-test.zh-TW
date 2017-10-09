---
title: "aaaWire 中記錄分析資料方案 |Microsoft 文件"
description: "網路資料是來自具有 OMS 代理程式 (包括 Operations Manager 和 Windows 連線的代理程式) 的電腦的網路和效能彙總資料。 網路資料會結合您的記錄檔資料 toohelp 與相互關聯資料。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a>Log Analytics 中的 Wire Data 2.0 (預覽) 解決方案

![Wire Data 符號](./media/log-analytics-wire-data/wire-data2-symbol.png)

連線資料是來自具有 OMS 代理程式 (包括 Operations Manager、Windows 連線和 Linux 代理程式) 之電腦的網路和效能彙總資料。 網路資料會結合您其他的記錄檔資料 toohelp 與相互關聯資料。

此外 tooOMS 代理程式，hello 網路資料 」 解決方案會使用您電腦安裝在您的 IT 基礎結構的 Microsoft 相依性代理程式。 相依性代理程式監視網路傳送資料 tooand 從您的電腦以網路層級 2-3 中的 hello [OSI 模型](https://en.wikipedia.org/wiki/OSI_model)，包括 hello 各種通訊協定和連接埠。 然後資料會傳送 tooLog 分析使用代理程式。

> [!NOTE]
> 您無法加入 hello 舊版 hello 網路資料解決方案 toonew 工作區。 如果您擁有 hello 啟用原始網路資料解決方案，您可以繼續 toouse 它。 不過，toouse 網路資料 2.0，您必須先移除 hello 原始版本。

根據預設，Log Analytics 會從 Windows 內建的計數器收集記錄的資料，包括 CPU、記憶體、磁碟和網路效能資料。 網路和其他資料收集會即時進行每個代理程式，包括子網路和 hello 電腦正在使用的應用程式層級通訊協定。 Hello hello 記錄檔 索引標籤上設定 頁面上，您可以加入其他效能計數器。

如果您曾經使用[sFlow](http://www.sflow.org/)或其他軟體搭配[Cisco NetFlow 通訊協定](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html)然後 hello 統計資料，您會看到來自網路資料的資料將會熟悉 tooyou。

內建的記錄搜尋查詢的 hello 類型包括：

- 提供連線資料的代理程式
- 提供連線資料的代理程式的 IP 位址
- 依 IP 位址的輸出通訊
- 應用程式通訊協定傳送的位元組數目
- 應用程式服務傳送的位元組數目
- 不同通訊協定接收的位元組數目
- IP 版本傳送及接收的位元組總數
- 可靠測量的連線平均延遲
- 起始或接收網路流量的電腦處理程序
- 處理程序的網路流量

當您使用網路資料搜尋時，您可以篩選和群組資料 tooview 資訊 hello 最上層的代理程式 」 和 「 最上層通訊協定。 或者，您可以檢視某些電腦 (IP 位址/MAC 位址) 何時彼此通訊、持續時間，以及已傳送的資料量；基本上，就是在檢視以搜尋為基礎之網路流量的相關中繼資料。

不過，因為是檢視中繼資料，在深入的疑難排解中不見得實用。 Log Analytics 中的連線資料不是完整擷取的網路資料。 因此，不適用於封包層級的深入疑難排解。 hello 使用 hello 代理程式的優點，比較 tooother 收集方法，是您不具有 tooinstall 應用裝置、 重新設定網路交換器，或執行複雜的組態。 網路資料就是以代理程式為基礎，您的電腦上安裝 hello 代理程式，它會監視自己的網路流量。 另一個優點是當您想 toomonitor 雲端提供者或主機服務提供者或 Microsoft Azure，情形 hello 使用者並未擁有 hello 網狀架構圖層中執行的工作負載。

## <a name="connected-sources"></a>連接的來源

網路資料會從 hello Microsoft 相依性代理程式取得其資料。 hello 相依性代理程式，取決於其連線 tooLog 分析的 hello OMS 代理程式。 這表示，伺服器必須擁有的 hello OMS 代理程式安裝和設定第一個，然後安裝 hello 相依性代理程式。 hello 下表描述 hello 網路資料解決方案支援的 hello 連接來源。

| **連線的來源** | **支援** | **說明** |
| --- | --- | --- |
| Windows 代理程式 | 是 | Wire Data 會分析並收集來自 Windows 代理程式電腦的資料。 <br><br> 在加法 toohello [OMS Agent](log-analytics-windows-agents.md)，Windows 代理程式需要 hello Microsoft 相依性代理程式。 請參閱 hello[支援的作業系統](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems)如需完整的作業系統版本清單。 |
| Linux 代理程式 | 是 | Wire Data 會分析並收集來自 Linux 代理程式電腦的資料。<br><br> 在加法 toohello [OMS Agent](log-analytics-linux-agents.md)，Linux 代理程式需要 hello Microsoft 相依性代理程式。 請參閱 hello[支援的作業系統](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems)如需完整的作業系統版本清單。 |
| System Center Operations Manager 管理群組 | 是 | Wire Data 會在連線的 [System Center Operations Manager 管理群組](log-analytics-om-agents.md)中，分析並收集來自 Windows 和 Linux 代理程式的資料。 <br><br> 直接從 hello System Center Operations Manager 代理程式電腦 tooLog 分析需要連接。 從 hello 管理群組 tooLog 分析，就會轉送資料。 |
| Azure 儲存體帳戶 | 否 | 網路資料收集資料從代理程式的電腦，所以沒有從其資料從 Azure 儲存體 toocollect。 |

在 Windows 中，由 System Center Operations Manager 和記錄分析 toogather hello Microsoft Monitoring Agent (MMA)，並傳送資料。 根據 hello 內容 hello 代理程式稱為 hello System Center Operations Manager 代理程式、 OMS 代理程式、 記錄分析代理程式、 MMA 或直接代理程式。 System Center Operations Manager 和 Log Analytics 提供的 hello MMA 稍有不同的版本。 這些版本可以每個報告 tooSystem Center Operations Manager、 tooLog 分析或 tooboth。

在 Linux 上 hello OMS Agent for Linux 收集並傳送資料 tooLog 分析。 附加的 tooLog 分析透過 System Center Operations Manager 管理群組的伺服器或與 OMS 直接代理程式伺服器上，您可以使用網路資料。

在本文中，參考 tooall 代理程式，是否 Linux 或 Windows 中，連接的 tooa System Center Operations Manager 管理群組，或直接 tooLog 分析是否會稱為 hello _OMS agent_。 只有當它所需的內容，我們將使用 hello hello 代理程式的特定部署名稱。

hello 相依性代理程式不會傳輸任何資料本身，並不需要任何變更 toofirewalls 或連接埠。 網路資料中的 hello 資料永遠傳輸的 hello OMS 代理程式 tooLog 分析，請直接或使用 hello OMS 閘道。

![代理程式圖表](./media/log-analytics-wire-data/agents.png)

如果您是 System Center Operations Manager 使用者與管理群組連線 tooLog 分析：

- System Center Operations Manager 代理程式可以存取 hello 網際網路 tooconnect tooLog 分析不時，需要任何額外的設定。
- System Center Operations Manager 代理程式無法存取記錄分析透過 hello 網際網路時，您會需要 tooconfigure hello OMS 閘道 toowork 與 System Center Operations Manager。

如果您使用 hello 直接代理程式，您需要 tooconfigure hello OMS 代理程式本身，tooconnect tooLog 分析或 tooyour OMS 閘道也一樣。 您可以從 hello 下載 hello OMS 閘道[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666)。

## <a name="prerequisites"></a>必要條件

- 需要 hello[深入剖析和分析](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing)解決方案供應項目。
- 如果您使用網路資料解決方案 hello hello 舊版本，您必須先將它移除。 不過，透過 hello 原始的網路資料解決方案擷取所有資料都是網路資料 2.0 和記錄搜尋中仍然可用。
- 系統管理員權限需要的 tooinstall 或解除安裝 hello 相依性代理程式。
- hello 相依性代理程式必須安裝具有 64 位元作業系統的電腦上。

### <a name="operating-systems"></a>作業系統

hello 下列各節列出 hello 支援的作業系統 hello 相依性代理程式。 Wire Data 不支援任何 32 位元架構的作業系統。

#### <a name="windows-server"></a>Windows Server

- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

#### <a name="windows-desktop"></a>Windows 桌面

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux、CentOS Linux 和 Oracle Linux (搭載 RHEL 核心)

- 只支援預設版本和 SMP Linux 核心版本。
- 所有 Linux 散發套件皆不支援非標準的核心版本 (例如 PAE 和 Xen)。 例如，與 hello 版本字串的系統_2.6.16.21-0.8-xen_不支援。
- 不支援自訂核心，包括重新編譯的標準核心。
- 不支援 CentOSPlus 核心。
- Oracle Unbreakable Enterprise Kernel (UEK) 在本文稍後的章節有相關討論。

#### <a name="red-hat-linux-7"></a>Red Hat Linux 7

| **作業系統版本** | **核心版本** |
| --- | --- |
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7.2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6

| **作業系統版本** | **核心版本** |
| --- | --- |
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

| **作業系統版本** | **核心版本** |
| --- | --- |
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398 <br> 2.6.18-400 <br>2.6.18-402 <br>2.6.18-404 <br>2.6.18-406 <br> 2.6.18-407 <br> 2.6.18-408 <br> 2.6.18-409 <br> 2.6.18-410 <br> 2.6.18-411 <br> 2.6.18-412 <br> 2.6.18-416 <br> 2.6.18-417 <br> 2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux 搭載 Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6

| **作業系統版本** | **核心版本** |
| --- | --- |
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| **作業系統版本** | **核心版本** |
| --- | --- |
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11

| **作業系統版本** | **核心版本** |
| --- | --- |
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10

| **作業系統版本** | **核心版本** |
| --- | --- |
| 10 SP4 | 2.6.16.60 |

#### <a name="dependency-agent-downloads"></a>相依性代理程式下載

| **檔案** | **作業系統** | **版本** | **SHA-256** |
| --- | --- | --- | --- |
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |



## <a name="configuration"></a>組態

執行下列步驟 tooconfigure hello 您工作區的網路資料解決方案的 hello。

1. 啟用從 hello hello 活動記錄分析解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。
2. 您要 tooget 資料所在的每一部電腦上安裝 hello 相依性代理程式。 hello 相依性代理程式可以監視連線 tooimmediate 鄰近項目，因此您可能不需要在每一部電腦上的代理程式。

### <a name="install-hello-dependency-agent-on-windows"></a>在 Windows 上安裝 hello 相依性代理程式

系統管理員權限需要的 tooinstall 或解除安裝 hello 代理程式。

hello 相依性代理程式會透過 InstallDependencyAgent Windows.exe 執行 Windows 的電腦上安裝。 如果您執行這個可執行檔不使用任何選項時，它會啟動精靈，您可以依照 tooinstall 以互動方式。

使用下列步驟 tooinstall hello 相依性代理程式在每一部執行 Windows 的電腦上的 hello:

1. 安裝 hello OMS 代理程式使用 hello 指示[連接 Windows Azure 中的記錄分析服務的電腦 toohello](log-analytics-windows-agents.md)。
2. 下載使用 hello 連結 hello 前一節中的 hello Windows 代理程式，然後使用下列命令的 hello 執行它： InstallDependencyAgent Windows.exe
3. 請遵循 hello 精靈 tooinstall hello 代理程式。
4. Toostart hello 相依性代理程式時，請檢查 hello 記錄檔以取得詳細的錯誤資訊。 Windows 代理程式上, hello 記錄檔目錄為 %Programfiles%\Microsoft 相依性 Agent\logs。

#### <a name="windows-command-line"></a>Windows 命令列

使用命令列中的下列資料表 tooinstall hello 的選項。 toosee hello 安裝旗標，使用 hello 執行 hello 安裝程式的清單 /？ 如下所示。

InstallDependencyAgent-Windows.exe /?

| **旗標** | **說明** |
| --- | --- |
| <code>/?</code> | 取得 hello 命令列選項的清單。 |
| <code>/S</code> | 執行無訊息安裝，不會出現任何使用者提示。 |

根據預設，hello Windows 相依性代理程式的檔案會放置於 C:\Program Files\Microsoft 相依性代理程式。

### <a name="install-hello-dependency-agent-on-linux"></a>Linux 上安裝 hello 相依性代理程式

將根目錄存取必要的 tooinstall 或 hello 代理程式設定。

hello 相依性代理程式會安裝在透過 InstallDependencyAgent Linux64.bin，與自我解壓縮二進位的殼層指令碼的 Linux 電腦上。 您可以使用執行 hello 檔_sh_ ，或將執行權限 toohello 檔案本身。

使用下列步驟 tooinstall hello 相依性代理程式在每一部 Linux 電腦上的 hello:

1. 安裝 hello OMS 代理程式使用 hello 指示[收集和管理資料從 Linux 電腦](log-analytics-agent-linux.md)。
2. 下載使用 hello 連結 hello 前一節中的 hello Linux 相依性代理程式，然後將它安裝為根，使用下列命令的 hello: sh InstallDependencyAgent Linux64.bin
3. Toostart hello 相依性代理程式時，請檢查 hello 記錄檔以取得詳細的錯誤資訊。 在 Linux 代理程式上, hello 記錄檔目錄是： /var/opt/microsoft/dependency-agent/log。

toosee hello 安裝旗標，以 hello 執行 hello 安裝程式的清單`-help`旗標，如下所示。

```
InstallDependencyAgent-Linux64.bin -help
```

| **旗標** | **說明** |
| --- | --- |
| <code>-help</code> | 取得 hello 命令列選項的清單。 |
| <code>-s</code> | 執行無訊息安裝，不會出現任何使用者提示。 |
| <code>--check</code> | 檢查權限與 hello 作業系統，但不是安裝 hello 代理程式。 |

Hello 相依性代理程式的檔案會放置於 hello 下列目錄：

| **檔案** | **位置** |
| --- | --- |
| 核心檔案 | /opt/microsoft/dependency-agent |
| 記錄檔 | /var/opt/microsoft/dependency-agent/log |
| 組態檔 | /etc/opt/microsoft/dependency-agent/config |
| 服務可執行檔 | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br><br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| 二進位儲存體檔案 | /var/opt/microsoft/dependency-agent/storage |

### <a name="installation-script-examples"></a>安裝指令碼範例

tooeasily 部署 hello 相依性代理程式在許多伺服器上的一次，它可協助 toouse 指令碼。 您可以使用下列指令碼範例 toodownload hello 和 hello 相依性代理程式安裝在 Windows 或 Linux。

#### <a name="powershell-script-for-windows"></a>適用於 Windows 的 PowerShell 指令碼

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a>適用於 Linux 的殼層指令碼

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a>期望的狀態設定

toodeploy hello 相依性代理程式透過預期狀態設定，您可以使用 hello xPSDesiredStateConfiguration 模組和有點類似 hello 下列程式碼：

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a>解除安裝 hello 相依性代理程式

使用下列各節 toohelp 移除 hello 相依性代理程式的 hello。

#### <a name="uninstall-hello-dependency-agent-on-windows"></a>解除安裝相依性代理程式在 Windows hello

系統管理員可以解除安裝 hello 相依性代理程式的 Windows 控制台。

系統管理員也可以執行 %Programfiles%\Microsoft 相依性 Agent\Uninstall.exe toouninstall hello 相依性代理程式。

#### <a name="uninstall-hello-dependency-agent-on-linux"></a>解除安裝 hello Linux 上的相依性代理程式

toocompletely 解除安裝 hello 相依性代理程式從 Linux，您必須移除 hello 代理程式本身並 hello hello 代理程式會自動安裝的連接器。 您可以使用下列單一命令的 hello 同時解除安裝：

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a>管理組件

啟動網路資料時，記錄分析工作區中，300 KB 管理組件會傳送 tooall hello Windows 伺服器，該工作區中。 如果您使用 System Center Operations Manager 代理程式在[連線的管理群組](log-analytics-om-agents.md)，hello 相依性監視管理組件從 System Center Operations Manager 部署。 如果 hello 代理程式並直接連接，記錄分析會傳遞 hello 管理組件。

hello 管理組件是名為 Microsoft.IntelligencePacks.ApplicationDependencyMonitor。 它會寫入至 %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs。 hello hello 管理組件使用的資料來源是: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll。

## <a name="using-hello-solution"></a>使用 hello 解決方案

**安裝和設定 hello 方案**

使用下列資訊 tooinstall hello 並設定 hello 方案。

- hello 網路資料解決方案擷取資料，從執行 Windows Server 2012 R2、 Windows 8.1 和更新版本的作業系統的電腦。
- 您想要從 tooacquire 網路資料的電腦上需要 Microsoft.NET Framework 4.0 或更新版本。
- 新增 hello 網路資料解決方案 tooyour 記錄分析工作區中使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。 不需要進一步的組態。
- 如果您想要特定解決方案 tooview 網路資料，您需要已加入的 toohave hello 解決方案 tooyour 工作區。

已安裝的代理程式並安裝 hello 方案之後，hello 網路資料 2.0 磚會出現在您的工作區中。

> [!NOTE]
> 目前，您必須使用 hello OMS 入口網站 tooview 網路資料。 您無法使用 hello Azure 入口網站 tooview 網路資料。

![Wire Data 磚](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a>使用網路資料 2.0 hello 解決方案

在 hello OMS 入口網站中，按一下 hello**網路資料 2.0**磚 tooopen hello 網路資料儀表板。 hello 儀表板會納入 hello 下表中的 hello 刀鋒視窗。 每個刀鋒視窗會列出 too10 hello 刀鋒視窗的準則指定領域和時間範圍比對的項目。 您可以執行，即可傳回的所有記錄的記錄搜尋**查看所有**底部 hello 的 hello 刀鋒視窗，或按一下 hello 刀鋒視窗中的標頭。

| **刀鋒視窗** | **說明** |
| --- | --- |
| 擷取網路流量的代理程式數 | 顯示 hello 會擷取網路流量的代理程式數目，並列出 hello top 10 的電腦所擷取的流量。 按一下 記錄搜尋 hello 數字 toorun <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>。 按一下電腦，在 hello 清單 toorun 傳回 hello 的總位元組數所擷取的記錄搜尋。 |
| 區域子網路數 | 顯示 hello 本機子網路探索代理程式數目。  按一下 記錄搜尋 hello 數字 toorun<code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code>其中列出所有子網路與 hello 透過每個傳送的位元組數目。 按一下 子網路中 hello 清單 toorun 傳回 hello 的總位元組數 hello 子網路上傳送的記錄搜尋。 |
| 應用程式層級通訊協定數 | 探索到代理程式，請在使用中，顯示 hello 一些應用程式層級通訊協定。 按一下 記錄搜尋 hello 數字 toorun <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>。 按一下 通訊協定 toorun 傳回 hello 的總位元組數傳送嗨通訊協定的使用記錄搜尋。 |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Wire Data 儀表板](./media/log-analytics-wire-data/wire-data-dash.png)

您可以使用 hello**擷取網路流量的代理程式**刀鋒視窗 toodetermine 電腦使用多少網路頻寬。 此刀鋒視窗可協助您輕鬆地尋找 hello _chattiest_您環境中的電腦。 這類電腦可能超載、運作異常，或使用的網路資源不尋常地過多。

![記錄搜尋範例](./media/log-analytics-wire-data/log-search-example01.png)

同樣地，您可以使用 hello**本機子網路**刀鋒視窗 toodetermine 網路流量移動您的子網路。 使用者通常會為其應用程式定義重要區域周圍的子網路。 此刀鋒視窗會提供這些區域的檢視。

![記錄搜尋範例](./media/log-analytics-wire-data/log-search-example02.png)

hello**應用程式層級通訊協定**刀鋒視窗中很有用，所以很有幫助知道通訊協定正在使用中。 例如，您可能預期 SSH toonot 在您的網路環境中使用。 檢視可用在 hello 刀鋒視窗中的資訊可以快速地確認，或 disprove 您預期的情況。

![記錄搜尋範例](./media/log-analytics-wire-data/log-search-example03.png)

在此範例中，您可以向下切入到 SSH 詳細資料 toosee 哪些電腦使用 SSH 和許多其他的通訊詳細資料。

![sh 搜尋結果](./media/log-analytics-wire-data/ssh-details.png)

它也是很有用的 tooknow 如果通訊協定流量會增加或減少一段時間。 比方說，如果資料是應用程式所傳送的 hello 數量增加，這可能是一些您應該注意，或者，您可能會發現值得注意。

## <a name="input-data"></a>輸入資料

網路資料會收集網路流量使用您已啟用的 hello 代理程式的相關中繼資料。 每個代理程式約每隔 15 秒傳送一次資料。

## <a name="output-data"></a>輸出資料

對於每種類型的輸入資料，系統會建立 _WireData_ 類型的記錄。 WireData 記錄都有屬性 hello 下表所示：

| 屬性 | 說明 |
|---|---|
| 電腦 | 收集資料所在的電腦名稱 |
| TimeGenerated | Hello 記錄的時間 |
| LocalIP | Hello 本機電腦的 IP 位址 |
| SessionState | 已連線或已中斷連線 |
| ReceivedBytes | 接收的位元組數目 |
| ProtocolName | 使用 hello 網路通訊協定名稱 |
| IPVersion | IP 版本 |
| 方向 | 輸入或輸出 |
| MaliciousIP | 已知惡意來源的 IP 位址 |
| 嚴重性 | 可疑惡意程式碼嚴重性 |
| RemoteIPCountry | 國家/地區的 hello 遠端 IP 位址 |
| ManagementGroupName | Hello Operations Manager 管理群組的名稱 |
| SourceSystem | 收集資料所在的來源 |
| SessionStartTime | 工作階段的開始時間 |
| SessionEndTime | 工作階段的結束時間 |
| LocalSubnet | 收集資料所在的子網路 |
| LocalPortNumber | 本機連接埠號碼 |
| RemoteIP | 使用 hello 遠端電腦的遠端 IP 位址 |
| RemotePortNumber | Hello 遠端 IP 位址所使用的通訊埠編號 |
| SessionID | 識別兩個 IP 位址之間通訊工作階段的唯一值 |
| SentBytes | 傳送的位元組數目 |
| TotalBytes | 工作階段期間傳送的位元組總數 |
| ApplicationProtocol | 使用的網路通訊協定類型   |
| ProcessID | Windows 處理序識別碼 |
| ProcessName | Hello 處理程序路徑和檔案名稱 |
| RemoteIPLongitude | IP 經度值 |
| RemoteIPLatitude | IP 緯度值 |


## <a name="next-steps"></a>後續步驟

- [搜尋記錄](log-analytics-log-searches.md)tooview 詳細的網路資料搜尋記錄。
