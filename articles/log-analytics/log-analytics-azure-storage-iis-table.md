---
title: "aaaUse 中 Azure 記錄分析的事件的 IIS 和資料表儲存體的 blob 儲存體 |Microsoft 文件"
description: "Hello 記錄檔寫入診斷 tootable 儲存體的 Azure 服務或 IIS 記錄檔寫入 tooblob 儲存體，可讀取記錄分析。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a>針對 Log Analytics 的事件，使用 IIS 和 Azure 表格儲存體的 Azure blob 儲存體

記錄分析可讀取 hello 記錄檔中的下列撰寫 tootable 診斷儲存體或 IIS 記錄檔中寫入的 tooblob 儲存體服務的 hello:

* Service Fabric 叢集 (預覽)
* 虛擬機器
* Web/背景工作角色

您必須先啟用 Azure 診斷，Log Analytics 才能收集這些資源的資料。

一旦啟用診斷，您可以使用 hello Azure 入口網站或 PowerShell 設定記錄分析 toocollect hello 記錄檔。

Azure 診斷是 Azure 擴充功能，可讓您從背景工作角色、 web 角色或在 Azure 中執行的虛擬機器的 toocollect 診斷資料。 hello 資料儲存在 Azure 儲存體帳戶，然後可以記錄分析所收集。

記錄分析 toocollect 的 Azure 診斷記錄檔，hello 記錄檔必須位於下列位置的 hello:

| 記錄類型 | 資源類型 | 位置 |
| --- | --- | --- |
| IIS 記錄檔 |虛擬機器 <br> Web 角色 <br> 背景工作角色 |wad-iis-logfiles (Blob 儲存體) |
| syslog |虛擬機器 |LinuxsyslogVer2v0 (表格儲存體) |
| Service Fabric 運作事件 |Service Fabric 節點 |WADServiceFabricSystemEventTable |
| Service Fabric Reliable Actor 事件 |Service Fabric 節點 |WADServiceFabricReliableActorEventTable |
| Service Fabric Reliable Service 事件 |Service Fabric 節點 |WADServiceFabricReliableServiceEventTable |
| Windows 事件記錄檔 |Service Fabric 節點 <br> 虛擬機器 <br> Web 角色 <br> 背景工作角色 |WADWindowsEventLogsTable (表格儲存體) |
| Windows ETW 記錄檔 |Service Fabric 節點 <br> 虛擬機器 <br> Web 角色 <br> 背景工作角色 |WADETWEventTable (表格儲存體) |

> [!NOTE]
> 的 IIS 記錄檔，以啟用額外的見解。
>
>

虛擬機器，您可以選擇安裝 hello hello 選項[記錄分析代理程式](log-analytics-azure-vm-extension.md)到您的虛擬機器 tooenable 額外的見解。 此外 toobeing 無法 tooanalyze IIS 記錄檔和事件記錄檔，您可以執行其他分析，包括組態變更追蹤、 SQL 評估及更新評估。

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a>為事件記錄檔和 IIS 記錄檔集合啟用虛擬機器中的 Azure 診斷
使用下列程序 tooenable 中虛擬機器的 Azure 診斷，為事件記錄檔和 IIS 記錄檔集合使用 hello Microsoft Azure 入口網站的 hello。

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a>tooenable hello Azure 入口網站與虛擬機器中的 Azure 診斷
1. 當您建立虛擬機器時，請安裝 hello VM 代理程式。 如果 hello 虛擬機器已存在，請確認已安裝 VM 代理程式的 hello。

   * 在 hello Azure 入口網站，瀏覽 toohello 虛擬機器，選取**選擇性組態**，然後**診斷**並設定**狀態**太**上**.

     完成時，hello VM 有 hello Azure 診斷擴充功能安裝並執行。 此擴充功能會負責收集您的診斷資料。
2. 在現有的 VM 上啟用監視和設定事件記錄。 您可以啟用診斷在 hello VM 層級。 tooenable 診斷然後設定事件記錄，執行下列步驟的 hello:

   1. 選取 hello VM。
   2. 按一下 [監視] 。
   3. 按一下 [診斷] 。
   4. 設定 hello**狀態**太**ON**。
   5. 選取您想 toocollect 每個診斷記錄檔。
   6. 按一下 [確定] 。

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a>在 Web 角色中針對 IIS 記錄檔和事件集合啟用 Azure 診斷
請參閱太[如何 tooEnable 雲端服務中的診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)如需啟用 Azure 診斷功能的一般步驟。 下列 hello 指示使用這項資訊和自訂用於記錄分析。

啟用 Azure 診斷時：

* 根據預設，會儲存 IIS 記錄檔，與在 hello scheduledTransferPeriod 傳輸間隔傳輸記錄資料。
* 預設不會傳輸 Windows 事件記錄檔。

### <a name="tooenable-diagnostics"></a>tooenable 診斷
tooenable Windows 事件記錄檔或 toochange hello scheduledTransferPeriod，請使用來設定 Azure 診斷 hello XML 組態檔 (diagnostics.wadcfg)，如中所示[步驟 4： 建立您的診斷組態檔並安裝 hello擴充功能](../cloud-services/cloud-services-dotnet-diagnostics.md)

hello 下列範例組態檔會收集 IIS 記錄檔和所有 hello 應用程式中的事件和系統記錄檔：

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

請確定您的 ConfigurationSettings 會指定儲存體帳戶，如 hello 下列範例所示：

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

hello **AccountName**和**AccountKey**值中找到 hello hello 儲存體帳戶儀表板中，在管理存取金鑰 底下的 Azure 入口網站。 hello hello 連接字串的通訊協定必須為**https**。

一旦 hello 更新診斷組態套用 tooyour 雲端服務和它正在寫入診斷 tooAzure 存放裝置，則您必須準備好 tooconfigure 記錄分析。

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a>使用 Azure 儲存體中的 hello Azure 入口網站 toocollect 記錄檔
您可以使用下列 Azure 服務的 hello hello Azure 入口網站 tooconfigure 記錄分析 toocollect hello 記錄檔：

* Service Fabric 叢集
* 虛擬機器
* Web/背景工作角色

在 hello Azure 入口網站，瀏覽 tooyour 記錄分析工作區，並執行下列工作的 hello:

1. 按一下 [儲存體帳戶記錄]
2. 按一下 hello*新增*工作
3. 選取包含 hello 診斷記錄檔的 hello 儲存體帳戶
   * 這可以是傳統儲存體帳戶或 Azure Resource Manager 儲存體帳戶
4. 選取 hello 想 toocollect 記錄檔中的資料類型
   * hello 選項包括 IIS 記錄檔。事件。Syslog (Linux);ETW 記錄檔。Service Fabric 事件
5. 根據資料類型，而且無法變更的 hello 自動填入來源 hello 值
6. 按一下 [確定] toosave hello 組態

針對您想記錄分析 toocollect 額外的儲存體帳戶和資料類型重複步驟 2-6。

在大約 30 分鐘內，您就可以 toosee hello 記錄分析儲存體帳戶的資料。 您只會看到寫入 toostorage 套用 hello 設定後的資料。 記錄分析不會從 hello 儲存體帳戶讀取 hello 預先存在的資料。

> [!NOTE]
> hello 入口網站不會驗證該來源存在 hello 儲存體帳戶中的 hello，或如果正在寫入新的資料。
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a>在虛擬機器中使用 PowerShell 來啟用 Azure 診斷以收集事件記錄檔和 IIS 記錄檔
中的步驟使用 hello[設定記錄分析 tooindex Azure 診斷](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics)toouse PowerShell tooread 來自 Azure 診斷寫入 tootable 儲存體。

使用 Azure PowerShell 您可以更精確地指定寫入 tooAzure 儲存體的 hello 事件。
如需詳細資訊，請參閱[在 Azure 虛擬機器中啟用診斷](../virtual-machines-dotnet-diagnostics.md)。

您可以啟用和更新使用下列 PowerShell 指令碼的 hello Azure 診斷。
您也可以搭配使用此指令碼與自訂記錄組態。
修改 hello 指令碼 tooset hello 儲存體帳戶、 服務名稱和虛擬機器名稱。
hello 指令碼會使用傳統的虛擬機器的 cmdlet。

檢閱下列指令碼範例的 hello、 複製它、 視需要修改它、 hello 範例儲存為 PowerShell 指令碼檔案，然後再執行 hello 指令碼。

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a>後續步驟
* 針對支援的 Azure 服務[收集 Azure 服務的記錄檔與計量](log-analytics-azure-storage.md)。
* [啟用方案](log-analytics-add-solutions.md)tooprovide 深入了解 hello 資料。
* [使用搜尋查詢](log-analytics-log-searches.md)tooanalyze hello 資料。
