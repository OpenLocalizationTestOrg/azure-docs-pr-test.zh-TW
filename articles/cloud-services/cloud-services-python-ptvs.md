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
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="b9cb9-103">採用 Python Tools for Visual Studio 的 Python Web 和背景工作角色</span><span class="sxs-lookup"><span data-stu-id="b9cb9-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="b9cb9-104">本文提供在 [Python Tools for Visual Studio][Python Tools for Visual Studio] 中使用 Python Web 和背景工作角色的概觀。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="b9cb9-105">深入了解如何 toouse Visual Studio toocreate 及部署基本的雲端服務使用 Python。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-105">Learn how toouse Visual Studio toocreate and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9cb9-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="b9cb9-106">Prerequisites</span></span>
* [<span data-ttu-id="b9cb9-107">Visual Studio 2013、2015 或 2017</span><span class="sxs-lookup"><span data-stu-id="b9cb9-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="b9cb9-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="b9cb9-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="b9cb9-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] 或</span><span class="sxs-lookup"><span data-stu-id="b9cb9-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="b9cb9-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] 或</span><span class="sxs-lookup"><span data-stu-id="b9cb9-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="b9cb9-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="b9cb9-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="b9cb9-112">[Python 2.7 32 位元][Python 2.7 32-bit]或 [Python 3.5 32 位元][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="b9cb9-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="b9cb9-113">什麼是 Python Web 和背景工作角色？</span><span class="sxs-lookup"><span data-stu-id="b9cb9-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="b9cb9-114">Azure 提供三種運算模型來執行應用程式：[Azure App Service 中的 Web Apps 功能][execution model-web sites]、[Azure 虛擬機器][execution model-vms]和 [Azure 雲端服務][execution model-cloud services]。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="b9cb9-115">這三種模型都支援 Python。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-115">All three models support Python.</span></span> <span data-ttu-id="b9cb9-116">雲端服務 (包含 Web 和背景工作角色) 可提供*平台即服務 (PaaS)*。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="b9cb9-117">在雲端服務中，web 角色提供專用的網際網路資訊服務 (IIS) web 伺服器 toohost 前端 web 應用程式，而背景工作角色可以執行非同步、 長時間執行或永久工作與使用者互動或輸入無關。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="b9cb9-118">如需詳細資訊，請參閱[什麼是雲端服務？] (英文)。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="b9cb9-119">*要尋找 toobuild 簡單網站嗎？*</span><span class="sxs-lookup"><span data-stu-id="b9cb9-119">*Looking toobuild a simple website?*</span></span>
> <span data-ttu-id="b9cb9-120">如果您的案例牽涉到只簡單網站前端，請考慮使用 Azure App Service 中的 hello 輕量級 Web 應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-120">If your scenario involves just a simple website front end, consider using hello lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="b9cb9-121">您的網站會成長並變更您的需求，您可以輕鬆地升級 tooa 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-121">You can easily upgrade tooa Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="b9cb9-122">請參閱 hello <a href="/develop/python/">Python 開發人員中心</a>涵蓋開發的 Azure App Service 中的 hello Web 應用程式功能之發行項。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-122">See hello <a href="/develop/python/">Python Developer Center</a> for articles that cover development of hello Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="b9cb9-123">建立專案</span><span class="sxs-lookup"><span data-stu-id="b9cb9-123">Project creation</span></span>
<span data-ttu-id="b9cb9-124">在 Visual Studio 中，您可以選取**Azure 雲端服務**在 hello**新專案**對話方塊的  **Python**。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-124">In Visual Studio, you can select **Azure Cloud Service** in hello **New Project** dialog box, under **Python**.</span></span>

![New Project Dialog](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="b9cb9-126">您可以在 hello Azure 雲端服務精靈 建立新 web 和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-126">In hello Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Azure Cloud Service Dialog](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="b9cb9-128">hello 背景工作角色範本隨附未定案程式碼 tooconnect tooan Azure 儲存體帳戶或 Azure 服務匯流排。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-128">hello worker role template comes with boilerplate code tooconnect tooan Azure storage account or Azure Service Bus.</span></span>

![Cloud Service Solution](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="b9cb9-130">您可以隨時加入 web 或背景工作角色 tooan 現有的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-130">You can add web or worker roles tooan existing cloud service at any time.</span></span>  <span data-ttu-id="b9cb9-131">您可以在方案中，選擇 tooadd 現有專案，或建立新的。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-131">You can choose tooadd existing projects in your solution, or create new ones.</span></span>

![Add Role Command](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="b9cb9-133">雲端服務可以包含以不同語言實作的角色。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="b9cb9-134">例如，您可以有使用 Django 實作的 Python Web 角色，以及 Python 或 C# 背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="b9cb9-135">您可以使用服務匯流排佇列或儲存體佇列，輕鬆地與角色進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-hello-cloud-service"></a><span data-ttu-id="b9cb9-136">安裝 Python hello 雲端服務</span><span class="sxs-lookup"><span data-stu-id="b9cb9-136">Install Python on hello cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="b9cb9-137">（在上次更新此文件的 hello 時間） 與 Visual Studio 一起安裝的 hello 安裝指令碼無法運作。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-137">hello setup scripts that are installed with Visual Studio (at hello time this article was last updated) do not work.</span></span> <span data-ttu-id="b9cb9-138">本節說明因應措施。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="b9cb9-139">hello 安裝指令碼 hello 主要問題是它們未安裝 python。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-139">hello main problem with hello setup scripts is that they do not install python.</span></span> <span data-ttu-id="b9cb9-140">首先，會定義兩個[啟動工作](cloud-services-startup-tasks.md)在 hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef)檔案。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="b9cb9-141">hello 第一個工作 (**PrepPython.ps1**) 下載並安裝 hello Python 執行階段。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-141">hello first task (**PrepPython.ps1**) downloads and installs hello Python runtime.</span></span> <span data-ttu-id="b9cb9-142">hello 第二個工作 (**PipInstaller.ps1**) 執行 pip tooinstall 您可能會有任何相依性。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-142">hello second task (**PipInstaller.ps1**) runs pip tooinstall any dependencies you may have.</span></span>

<span data-ttu-id="b9cb9-143">下列指令碼的 hello 撰寫以 Python 3.5 為目標。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-143">hello following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="b9cb9-144">如果您想 toouse hello 版本 2.x 的 python，設定 hello **PYTHON2**變數檔案太**上**hello 兩個啟動工作及 hello 執行階段工作： `<Variable name="PYTHON2" value="<mark>on</mark>" />`。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-144">If you want toouse hello version 2.x of python, set hello **PYTHON2** variable file too**on** for hello two startup tasks and hello runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

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

<span data-ttu-id="b9cb9-145">hello **PYTHON2**和**PYPATH** toohello 背景工作啟動工作必須加入變數。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-145">hello **PYTHON2** and **PYPATH** variables must be added toohello worker startup task.</span></span> <span data-ttu-id="b9cb9-146">hello **PYPATH**變數只有時才使用 hello **PYTHON2**變數設定得**上**。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-146">hello **PYPATH** variable is only used if hello **PYTHON2** variable is set too**on**.</span></span>

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

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="b9cb9-147">範例 ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="b9cb9-147">Sample ServiceDefinition.csdef</span></span>
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



<span data-ttu-id="b9cb9-148">接下來，建立 hello **PrepPython.ps1**和**PipInstaller.ps1**檔案在 hello **。 / bin**資料夾的角色。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-148">Next, create hello **PrepPython.ps1** and **PipInstaller.ps1** files in hello **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="b9cb9-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="b9cb9-149">PrepPython.ps1</span></span>
<span data-ttu-id="b9cb9-150">此指令碼會安裝 python。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-150">This script installs python.</span></span> <span data-ttu-id="b9cb9-151">如果 hello **PYTHON2**環境變數設定得**上**，然後安裝 Python 2.7，否則 Python 安裝 3.5。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-151">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

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

#### <a name="pipinstallerps1"></a><span data-ttu-id="b9cb9-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="b9cb9-152">PipInstaller.ps1</span></span>
<span data-ttu-id="b9cb9-153">此指令碼呼叫 pip，並將所有 hello 相依性安裝中 hello **requirements.txt**檔案。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-153">This script calls up pip and installs all of hello dependencies in hello **requirements.txt** file.</span></span> <span data-ttu-id="b9cb9-154">如果 hello **PYTHON2**環境變數設定得**上**，則會使用 Python 2.7，否則會使用 Python 3.5。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-154">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="b9cb9-155">修改 LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="b9cb9-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="b9cb9-156">中的 hello 案例**背景工作角色**專案， **LauncherWorker.ps1**檔案是必要的 tooexecute hello 啟動檔案。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-156">In hello case of a **worker role** project, **LauncherWorker.ps1** file is required tooexecute hello startup file.</span></span> <span data-ttu-id="b9cb9-157">在**web 角色**專案中，hello 啟動檔案定義在 hello 專案屬性中。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-157">In a **web role** project, hello startup file is instead defined in hello project properties.</span></span>
> 
> 

<span data-ttu-id="b9cb9-158">hello **bin\LaunchWorker.ps1**最初建立的 toodo 大量的準備工作，但它並沒有用。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-158">hello **bin\LaunchWorker.ps1** was originally created toodo a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="b9cb9-159">以下列指令碼的 hello 取代該檔案中的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-159">Replace hello contents in that file with hello following script.</span></span>

<span data-ttu-id="b9cb9-160">此指令碼會呼叫 hello **worker.py**來自 python 專案檔。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-160">This script calls hello **worker.py** file from your python project.</span></span> <span data-ttu-id="b9cb9-161">如果 hello **PYTHON2**環境變數設定得**上**，則會使用 Python 2.7，否則會使用 Python 3.5。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-161">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="pscmd"></a><span data-ttu-id="b9cb9-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="b9cb9-162">ps.cmd</span></span>
<span data-ttu-id="b9cb9-163">應該建立 hello Visual Studio 範本**ps.cmd**檔案在 hello **。 / bin**資料夾。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-163">hello Visual Studio templates should have created a **ps.cmd** file in hello **./bin** folder.</span></span> <span data-ttu-id="b9cb9-164">此殼層指令碼呼叫 hello PowerShell 上述的包裝函式指令碼，並提供 hello hello PowerShell 包裝函式呼叫名稱為基礎的記錄。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-164">This shell script calls out hello PowerShell wrapper scripts above and provides logging based on hello name of hello PowerShell wrapper called.</span></span> <span data-ttu-id="b9cb9-165">如果未建立此檔案，以下是該檔案所應包含的內容。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="b9cb9-166">在本機執行</span><span class="sxs-lookup"><span data-stu-id="b9cb9-166">Run locally</span></span>
<span data-ttu-id="b9cb9-167">如果您將雲端服務專案設定為 hello 啟始專案，並按下 F5，執行 hello 的本機 Azure 模擬器中的 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-167">If you set your cloud service project as hello startup project and press F5, hello cloud service runs in hello local Azure emulator.</span></span>

<span data-ttu-id="b9cb9-168">雖然 PTVS 支援啟動 hello 在模擬器中偵錯 （例如，中斷點） 無法運作。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-168">Although PTVS supports launching in hello emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="b9cb9-169">toodebug web 和背景工作角色，您可以將 hello 角色專案設定為 hello 啟始專案和偵錯，而是。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-169">toodebug your web and worker roles, you can set hello role project as hello startup project and debug that instead.</span></span>  <span data-ttu-id="b9cb9-170">您也可以設定多個啟始專案。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="b9cb9-171">Hello 方案上按一下滑鼠右鍵，然後選取**設定啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-171">Right-click hello solution and then select **Set StartUp Projects**.</span></span>

![Solution Startup Project Properties](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a><span data-ttu-id="b9cb9-173">發行 tooAzure</span><span class="sxs-lookup"><span data-stu-id="b9cb9-173">Publish tooAzure</span></span>
<span data-ttu-id="b9cb9-174">toopublish，hello 方案中的 hello 雲端服務專案上按一下滑鼠右鍵，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-174">toopublish, right-click hello cloud service project in hello solution and then select **Publish**.</span></span>

![Microsoft Azure Publish Sign In](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="b9cb9-176">請遵循 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-176">Follow hello wizard.</span></span> <span data-ttu-id="b9cb9-177">如有需要，請啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="b9cb9-178">當您需要 toodebug 一些項目時，遠端桌面是很有幫助。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-178">Remote desktop is helpful when you need toodebug something.</span></span>

<span data-ttu-id="b9cb9-179">組態設定完成之後，按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="b9cb9-180">在 hello 輸出視窗中，將會出現一些進度，然後您會看見 hello Microsoft Azure 活動記錄視窗。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-180">Some progress appears in hello output window, then you'll see hello Microsoft Azure Activity Log window.</span></span>

![Microsoft Azure Activity Log Window](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="b9cb9-182">部署需要數分鐘 toocomplete，然後您的 web 和/或在 Azure 上執行的背景工作角色 ！</span><span class="sxs-lookup"><span data-stu-id="b9cb9-182">Deployment takes several minutes toocomplete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="b9cb9-183">調查記錄檔</span><span class="sxs-lookup"><span data-stu-id="b9cb9-183">Investigate logs</span></span>
<span data-ttu-id="b9cb9-184">Hello 雲端服務的虛擬機器會啟動並安裝 Python 之後，您可以查看 hello 記錄 toofind 任何失敗的訊息。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-184">After hello cloud service virtual machine starts up and installs Python, you can look at hello logs toofind any failure messages.</span></span> <span data-ttu-id="b9cb9-185">這些記錄檔位於 hello **C:\Resources\Directory\\{角色} \LogFiles**資料夾。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-185">These logs are located in hello **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="b9cb9-186">**PrepPython.err.txt**中有至少一個錯誤，從 hello 指令碼時嘗試 toodetect，如果已安裝 Python 和**PipInstaller.err.txt**可能能投訴地過期的 pip 的版本。</span><span class="sxs-lookup"><span data-stu-id="b9cb9-186">**PrepPython.err.txt** has at least one error in it from when hello script tries toodetect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9cb9-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9cb9-187">Next steps</span></span>
<span data-ttu-id="b9cb9-188">如需詳細使用 Visual studio 的 Python 工具中的 web 和背景工作角色的詳細資訊，請參閱 hello PTVS 文件：</span><span class="sxs-lookup"><span data-stu-id="b9cb9-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see hello PTVS documentation:</span></span>

* <span data-ttu-id="b9cb9-189">[雲端服務專案][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="b9cb9-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="b9cb9-190">如需有關使用從您的 web 和背景工作角色，例如使用 Azure 儲存體或服務匯流排的 Azure 服務的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="b9cb9-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see hello following articles:</span></span>

* <span data-ttu-id="b9cb9-191">[Blob 服務][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="b9cb9-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="b9cb9-192">[表格服務][Table Service]</span><span class="sxs-lookup"><span data-stu-id="b9cb9-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="b9cb9-193">[佇列服務][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="b9cb9-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="b9cb9-194">[服務匯流排佇列][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="b9cb9-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="b9cb9-195">[服務匯流排主題][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="b9cb9-195">[Service Bus Topics][Service Bus Topics]</span></span>

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
