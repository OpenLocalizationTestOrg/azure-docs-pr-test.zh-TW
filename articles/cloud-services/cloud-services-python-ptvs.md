---
title: "aaaGet 開始使用 Python 和 Azure 雲端服務 |Microsoft 文件"
description: "使用 Python Tools for Visual Studio toocreate Azure 雲端服務包含 web 角色和背景工作角色的概觀。"
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: 
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: f5fd85e754839f146abe912351c59dc4a148c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a>採用 Python Tools for Visual Studio 的 Python Web 和背景工作角色

本文提供在 [Python Tools for Visual Studio][Python Tools for Visual Studio] 中使用 Python Web 和背景工作角色的概觀。 深入了解如何 toouse Visual Studio toocreate 及部署基本的雲端服務使用 Python。

## <a name="prerequisites"></a>必要條件
* [Visual Studio 2013、2015 或 2017](https://www.visualstudio.com/)
* [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)
* [Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] 或  
[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] 或  
[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]
* [Python 2.7 32 位元][Python 2.7 32-bit]或 [Python 3.5 32 位元][Python 3.5 32-bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a>什麼是 Python Web 和背景工作角色？
Azure 提供三種運算模型來執行應用程式：[Azure App Service 中的 Web Apps 功能][execution model-web sites]、[Azure 虛擬機器][execution model-vms]和 [Azure 雲端服務][execution model-cloud services]。 這三種模型都支援 Python。 雲端服務 (包含 Web 和背景工作角色) 可提供*平台即服務 (PaaS)*。 在雲端服務中，web 角色提供專用的網際網路資訊服務 (IIS) web 伺服器 toohost 前端 web 應用程式，而背景工作角色可以執行非同步、 長時間執行或永久工作與使用者互動或輸入無關。

如需詳細資訊，請參閱[什麼是雲端服務？] (英文)。

> [!NOTE]
> *要尋找 toobuild 簡單網站嗎？*
> 如果您的案例牽涉到只簡單網站前端，請考慮使用 Azure App Service 中的 hello 輕量級 Web 應用程式功能。 您的網站會成長並變更您的需求，您可以輕鬆地升級 tooa 雲端服務。 請參閱 hello <a href="/develop/python/">Python 開發人員中心</a>涵蓋開發的 Azure App Service 中的 hello Web 應用程式功能之發行項。
> <br />
> 
> 

## <a name="project-creation"></a>建立專案
在 Visual Studio 中，您可以選取**Azure 雲端服務**在 hello**新專案**對話方塊的  **Python**。

![New Project Dialog](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

您可以在 hello Azure 雲端服務精靈 建立新 web 和背景工作角色。

![Azure Cloud Service Dialog](./media/cloud-services-python-ptvs/new-service-wizard.png)

hello 背景工作角色範本隨附未定案程式碼 tooconnect tooan Azure 儲存體帳戶或 Azure 服務匯流排。

![Cloud Service Solution](./media/cloud-services-python-ptvs/worker.png)

您可以隨時加入 web 或背景工作角色 tooan 現有的雲端服務。  您可以在方案中，選擇 tooadd 現有專案，或建立新的。

![Add Role Command](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

雲端服務可以包含以不同語言實作的角色。  例如，您可以有使用 Django 實作的 Python Web 角色，以及 Python 或 C# 背景工作角色。  您可以使用服務匯流排佇列或儲存體佇列，輕鬆地與角色進行通訊。

## <a name="install-python-on-hello-cloud-service"></a>安裝 Python hello 雲端服務
> [!WARNING]
> （在上次更新此文件的 hello 時間） 與 Visual Studio 一起安裝的 hello 安裝指令碼無法運作。 本節說明因應措施。
> 
> 

hello 安裝指令碼 hello 主要問題是它們未安裝 python。 首先，會定義兩個[啟動工作](cloud-services-startup-tasks.md)在 hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef)檔案。 hello 第一個工作 (**PrepPython.ps1**) 下載並安裝 hello Python 執行階段。 hello 第二個工作 (**PipInstaller.ps1**) 執行 pip tooinstall 您可能會有任何相依性。

下列指令碼的 hello 撰寫以 Python 3.5 為目標。 如果您想 toouse hello 版本 2.x 的 python，設定 hello **PYTHON2**變數檔案太**上**hello 兩個啟動工作及 hello 執行階段工作： `<Variable name="PYTHON2" value="<mark>on</mark>" />`。

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

hello **PYTHON2**和**PYPATH** toohello 背景工作啟動工作必須加入變數。 hello **PYPATH**變數只有時才使用 hello **PYTHON2**變數設定得**上**。

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a>範例 ServiceDefinition.csdef
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



接下來，建立 hello **PrepPython.ps1**和**PipInstaller.ps1**檔案在 hello **。 / bin**資料夾的角色。

#### <a name="preppythonps1"></a>PrepPython.ps1
此指令碼會安裝 python。 如果 hello **PYTHON2**環境變數設定得**上**，然後安裝 Python 2.7，否則 Python 安裝 3.5。

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url too$outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a>PipInstaller.ps1
此指令碼呼叫 pip，並將所有 hello 相依性安裝中 hello **requirements.txt**檔案。 如果 hello **PYTHON2**環境變數設定得**上**，則會使用 Python 2.7，否則會使用 Python 3.5。

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a>修改 LaunchWorker.ps1
> [!NOTE]
> 中的 hello 案例**背景工作角色**專案， **LauncherWorker.ps1**檔案是必要的 tooexecute hello 啟動檔案。 在**web 角色**專案中，hello 啟動檔案定義在 hello 專案屬性中。
> 
> 

hello **bin\LaunchWorker.ps1**最初建立的 toodo 大量的準備工作，但它並沒有用。 以下列指令碼的 hello 取代該檔案中的 hello 內容。

此指令碼會呼叫 hello **worker.py**來自 python 專案檔。 如果 hello **PYTHON2**環境變數設定得**上**，則會使用 Python 2.7，否則會使用 Python 3.5。

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize tooyour local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a>ps.cmd
應該建立 hello Visual Studio 範本**ps.cmd**檔案在 hello **。 / bin**資料夾。 此殼層指令碼呼叫 hello PowerShell 上述的包裝函式指令碼，並提供 hello hello PowerShell 包裝函式呼叫名稱為基礎的記錄。 如果未建立此檔案，以下是該檔案所應包含的內容。 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a>在本機執行
如果您將雲端服務專案設定為 hello 啟始專案，並按下 F5，執行 hello 的本機 Azure 模擬器中的 hello 雲端服務。

雖然 PTVS 支援啟動 hello 在模擬器中偵錯 （例如，中斷點） 無法運作。

toodebug web 和背景工作角色，您可以將 hello 角色專案設定為 hello 啟始專案和偵錯，而是。  您也可以設定多個啟始專案。  Hello 方案上按一下滑鼠右鍵，然後選取**設定啟始專案**。

![Solution Startup Project Properties](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a>發行 tooAzure
toopublish，hello 方案中的 hello 雲端服務專案上按一下滑鼠右鍵，然後選取**發行**。

![Microsoft Azure Publish Sign In](./media/cloud-services-python-ptvs/publish-sign-in.png)

請遵循 hello 精靈。 如有需要，請啟用遠端桌面。 當您需要 toodebug 一些項目時，遠端桌面是很有幫助。

組態設定完成之後，按一下 [發行]。

在 hello 輸出視窗中，將會出現一些進度，然後您會看見 hello Microsoft Azure 活動記錄視窗。

![Microsoft Azure Activity Log Window](./media/cloud-services-python-ptvs/publish-activity-log.png)

部署需要數分鐘 toocomplete，然後您的 web 和/或在 Azure 上執行的背景工作角色 ！

### <a name="investigate-logs"></a>調查記錄檔
Hello 雲端服務的虛擬機器會啟動並安裝 Python 之後，您可以查看 hello 記錄 toofind 任何失敗的訊息。 這些記錄檔位於 hello **C:\Resources\Directory\\{角色} \LogFiles**資料夾。 **PrepPython.err.txt**中有至少一個錯誤，從 hello 指令碼時嘗試 toodetect，如果已安裝 Python 和**PipInstaller.err.txt**可能能投訴地過期的 pip 的版本。

## <a name="next-steps"></a>後續步驟
如需詳細使用 Visual studio 的 Python 工具中的 web 和背景工作角色的詳細資訊，請參閱 hello PTVS 文件：

* [雲端服務專案][Cloud Service Projects]

如需有關使用從您的 web 和背景工作角色，例如使用 Azure 儲存體或服務匯流排的 Azure 服務的詳細資訊，請參閱下列文章 hello:

* [Blob 服務][Blob Service]
* [表格服務][Table Service]
* [佇列服務][Queue Service]
* [服務匯流排佇列][Service Bus Queues]
* [服務匯流排主題][Service Bus Topics]

<!--Link references-->

[什麼是雲端服務？]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/overview.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]:../storage/blobs/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/queues/storage-python-how-to-use-queue-storage.md
[Table Service]:../cosmos-db/table-storage-how-to-use-python.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/
