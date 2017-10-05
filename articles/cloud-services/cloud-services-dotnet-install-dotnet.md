---
title: "在 Azure 雲端服務角色上安裝 .NET | Microsoft Docs"
description: "本文說明如何在雲端服務 Web 和背景工作角色上手動安裝 .NET Framework"
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: a9cffa275ae6b9315b821d3160b17a997a1523f7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="e762f-103">在 Azure 雲端服務角色上安裝 .NET</span><span class="sxs-lookup"><span data-stu-id="e762f-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="e762f-104">本文說明如何安裝未隨附於 Azure 客體 OS 的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="e762f-104">This article describes how to install versions of .NET Framework that don't come with the Azure Guest OS.</span></span> <span data-ttu-id="e762f-105">若要設定雲端服務 web 和背景工作角色，您可以在客體 OS 上使用 .NET。</span><span class="sxs-lookup"><span data-stu-id="e762f-105">You can use .NET on the Guest OS to configure your cloud service web and worker roles.</span></span>

<span data-ttu-id="e762f-106">例如，您可以在未隨附於任何版本之 .NET 4.6.1 的客體 OS 系列 4 上安裝 .NET 4.6。</span><span class="sxs-lookup"><span data-stu-id="e762f-106">For example, you can install .NET 4.6.1 on the Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="e762f-107">(客體 OS 系列 5 會隨附於 .NET 4.6。)如需 Azure 客體 OS 版本的最新資訊，請參閱 [Azure 客體 OS 發行新聞](cloud-services-guestos-update-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="e762f-107">(The Guest OS family 5 does come with .NET 4.6.) For the latest information on the Azure Guest OS releases, see the [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="e762f-108">Azure SDK 2.9 包含客體 OS 系列 4 或更舊版本部署 .NET 4.6 的限制。</span><span class="sxs-lookup"><span data-stu-id="e762f-108">The Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on the Guest OS family 4 or earlier.</span></span> <span data-ttu-id="e762f-109">可在 [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) 網站上取得限制的修正程式。</span><span class="sxs-lookup"><span data-stu-id="e762f-109">A fix for the restriction is available on the [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="e762f-110">若要在您的 web 和背景工作角色上安裝 .NET，請包括 .NET web 安裝程式作為雲端服務專案的一部分。</span><span class="sxs-lookup"><span data-stu-id="e762f-110">To install .NET on your web and worker roles, include the .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="e762f-111">啟動安裝程式作為角色啟動工作的一部分。</span><span class="sxs-lookup"><span data-stu-id="e762f-111">Start the installer as part of the role's startup tasks.</span></span> 

## <a name="add-the-net-installer-to-your-project"></a><span data-ttu-id="e762f-112">將 .NET 安裝程式加入至專案</span><span class="sxs-lookup"><span data-stu-id="e762f-112">Add the .NET installer to your project</span></span>
<span data-ttu-id="e762f-113">若要下載 .NET framework 的 Web 安裝程式，請選擇您需要安裝的版本：</span><span class="sxs-lookup"><span data-stu-id="e762f-113">To download the web installer for the .NET Framework, choose the version that you want to install:</span></span>

* [<span data-ttu-id="e762f-114">.NET 4.7 web 安裝程式</span><span class="sxs-lookup"><span data-stu-id="e762f-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="e762f-115">.NET 4.6.1 web 安裝程式</span><span class="sxs-lookup"><span data-stu-id="e762f-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="e762f-116">若要新增 web 角色的安裝程式：</span><span class="sxs-lookup"><span data-stu-id="e762f-116">To add the installer for a *web* role:</span></span>
  1. <span data-ttu-id="e762f-117">在 [方案總管] 中，於雲端服務專案中的 [角色] 下，以滑鼠右鍵按一下您的 web角色，然後依序選取 [新增] > [新增資料夾]。</span><span class="sxs-lookup"><span data-stu-id="e762f-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="e762f-118">建立名為 **bin** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="e762f-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="e762f-119">在 bin 資料夾上按一下滑鼠右鍵，並依序選取 [新增] > [現有項目]。</span><span class="sxs-lookup"><span data-stu-id="e762f-119">Right-click the bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="e762f-120">選取 .NET 安裝程式，並將它加入至 bin 資料夾。</span><span class="sxs-lookup"><span data-stu-id="e762f-120">Select the .NET installer and add it to the bin folder.</span></span>
  
<span data-ttu-id="e762f-121">若要新增 worker 角色的安裝程式：</span><span class="sxs-lookup"><span data-stu-id="e762f-121">To add the installer for a *worker* role:</span></span>
* <span data-ttu-id="e762f-122">以滑鼠右鍵按一下您的 worker 角色，然後依序選取 [新增] > [現有項目]。</span><span class="sxs-lookup"><span data-stu-id="e762f-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="e762f-123">選取 .NET 安裝程式，並將它加入至角色。</span><span class="sxs-lookup"><span data-stu-id="e762f-123">Select the .NET installer and add it to the role.</span></span> 

<span data-ttu-id="e762f-124">以這個方式將檔案新增至角色內容資料夾時，檔案就會自動新增至雲端服務套件。</span><span class="sxs-lookup"><span data-stu-id="e762f-124">When files are added in this way to the role content folder, they're automatically added to your cloud service package.</span></span> <span data-ttu-id="e762f-125">然後檔案就會部署到虛擬機器上的一致位置。</span><span class="sxs-lookup"><span data-stu-id="e762f-125">The files are then deployed to a consistent location on the virtual machine.</span></span> <span data-ttu-id="e762f-126">為雲端服務中的每個 Web 和背景工作角色重複此程序，以便所有角色都有安裝程式副本。</span><span class="sxs-lookup"><span data-stu-id="e762f-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of the installer.</span></span>

> [!NOTE]
> <span data-ttu-id="e762f-127">即使您的應用程式是以 .NET 4.6 為目標，還是應該在雲端服務角色上安裝 .NET 4.6.1。</span><span class="sxs-lookup"><span data-stu-id="e762f-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="e762f-128">客體 OS 包含知識庫[更新 3098779](https://support.microsoft.com/kb/3098779) 和[更新 3097997](https://support.microsoft.com/kb/3097997)。</span><span class="sxs-lookup"><span data-stu-id="e762f-128">The Guest OS includes the Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="e762f-129">如果 .NET 4.6 是安裝在知識庫更新安裝之上，當您執行 .NET 應用程式時，就可能會發生問題。</span><span class="sxs-lookup"><span data-stu-id="e762f-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of the Knowledge Base updates.</span></span> <span data-ttu-id="e762f-130">若要避免這些問題，請安裝 .NET 4.6.1，而不是 4.6 版。</span><span class="sxs-lookup"><span data-stu-id="e762f-130">To avoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="e762f-131">如需詳細資訊，請參閱[知識庫文章 3118750](https://support.microsoft.com/kb/3118750)。</span><span class="sxs-lookup"><span data-stu-id="e762f-131">For more information, see the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![安裝程式檔案的角色內容][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="e762f-133">定義角色的啟動工作</span><span class="sxs-lookup"><span data-stu-id="e762f-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="e762f-134">您可以利用啟動工作，在角色啟動之前執行作業。</span><span class="sxs-lookup"><span data-stu-id="e762f-134">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="e762f-135">將 .NET Framework 安裝為啟動工作的一部分，可確保在執行任何應用程式程式碼之前就已安裝好 Framework。</span><span class="sxs-lookup"><span data-stu-id="e762f-135">Installing the .NET Framework as part of the startup task ensures that the framework is installed before any application code is run.</span></span> <span data-ttu-id="e762f-136">如需有關啟動工作的詳細資訊，請參閱[在 Azure 中執行啟動工作](cloud-services-startup-tasks.md)。</span><span class="sxs-lookup"><span data-stu-id="e762f-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="e762f-137">將下列內容新增至所有角色的 **WebRole** 或 **WorkerRole** 節點底下的 ServiceDefinition.csdef 檔案：</span><span class="sxs-lookup"><span data-stu-id="e762f-137">Add the following content to the ServiceDefinition.csdef file under the **WebRole** or **WorkerRole** node for all roles:</span></span>
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    <span data-ttu-id="e762f-138">上述組態會使用系統管理員權限來執行主控台命令 `install.cmd`，以便安裝 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="e762f-138">The preceding configuration runs the console command `install.cmd` with administrator privileges to install the .NET Framework.</span></span> <span data-ttu-id="e762f-139">此設定也會建立名為 **NETFXInstall** 的 **LocalStorage** 元素。</span><span class="sxs-lookup"><span data-stu-id="e762f-139">The configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="e762f-140">啟動指令碼會將暫存資料夾設定為使用這個本機儲存資源。</span><span class="sxs-lookup"><span data-stu-id="e762f-140">The startup script sets the temp folder to use this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="e762f-141">若要確保正確安裝架構，請將此資源的大小設定為至少 1,024 MB。</span><span class="sxs-lookup"><span data-stu-id="e762f-141">To ensure correct installation of the framework, set the size of this resource to at least 1,024 MB.</span></span>
    
    <span data-ttu-id="e762f-142">如需有關啟動工作的詳細資訊，請參閱[常見的 Azure 雲端服務啟動工作](cloud-services-startup-tasks-common.md)。</span><span class="sxs-lookup"><span data-stu-id="e762f-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="e762f-143">建立名為 **install.cmd** 的檔案，並將下列安裝指令碼新增至檔案。</span><span class="sxs-lookup"><span data-stu-id="e762f-143">Create a file named **install.cmd** and add the following install script to the file.</span></span>

    <span data-ttu-id="e762f-144">指令碼會透過查詢登錄來檢查指定的 .NET Framework 版本是否已在電腦上安裝。</span><span class="sxs-lookup"><span data-stu-id="e762f-144">The script checks whether the specified version of the .NET Framework is already installed on the machine by querying the registry.</span></span> <span data-ttu-id="e762f-145">如果未安裝該 .NET 版本，.Net Web 安裝程式就會開啟。</span><span class="sxs-lookup"><span data-stu-id="e762f-145">If the .NET version is not installed, then the .NET web installer is opened.</span></span> <span data-ttu-id="e762f-146">為協助針對任何問題進行疑難排解，該指令碼會將所有活動記錄到 startuptasklog-(目前日期和時間).txt 的檔案 (儲存於 **InstallLogs** 本機儲存體)。</span><span class="sxs-lookup"><span data-stu-id="e762f-146">To help troubleshoot any issues, the script logs all activity to the file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e762f-147">使用 Windows 記事本之類的基本文字編輯器來建立 install.cmd 檔案。</span><span class="sxs-lookup"><span data-stu-id="e762f-147">Use a basic text editor like Windows Notepad to create the install.cmd file.</span></span> <span data-ttu-id="e762f-148">如果您是使用 Visual Studio 來建立文字檔案，然後將副檔名變更為 .cmd，檔案可能仍會包含 UTF-8 位元組順序標記。</span><span class="sxs-lookup"><span data-stu-id="e762f-148">If you use Visual Studio to create a text file and change the extension to .cmd, the file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="e762f-149">執行指令碼的第一行時，此標記可能會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="e762f-149">This mark can cause an error when the first line of the script is run.</span></span> <span data-ttu-id="e762f-150">若要避免這個錯誤，請在指令碼的第一行使用 REM 陳述式，位元組順序處理就可以跳過。</span><span class="sxs-lookup"><span data-stu-id="e762f-150">To avoid this error, make the first line of the script a REM statement that can be skipped by the byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set the value of netfx to install appropriate .NET Framework. 
    REM ***** To install .NET 4.5.2 set the variable netfx to "NDP452" *****
    REM ***** To install .NET 4.6 set the variable netfx to "NDP46" *****
    REM ***** To install .NET 4.6.1 set the variable netfx to "NDP461" *****
    REM ***** To install .NET 4.6.2 set the variable netfx to "NDP462" *****
    REM ***** To install .NET 4.7 set the variable netfx to "NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed to correctly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting to complete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="e762f-151">此指令碼會示範如何安裝 .NET 4.5.2 或 4.6 版以取得持續性，即使 Azure 客體 OS 上已有 .NET 4.5.2 可供使用。</span><span class="sxs-lookup"><span data-stu-id="e762f-151">This script shows how to install .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on the Azure Guest OS.</span></span> <span data-ttu-id="e762f-152">您應該直接安裝 .NET 4.6.1 而不是 4.6 版，如[知識庫文章 3118750](https://support.microsoft.com/kb/3118750) 中所述。</span><span class="sxs-lookup"><span data-stu-id="e762f-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="e762f-153">將 install.cmd 檔案新增至每個角色，方法是使用 [方案總管] 中的 [新增] > [現有項目]如本主題中稍早所述。</span><span class="sxs-lookup"><span data-stu-id="e762f-153">Add the install.cmd file to each role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="e762f-154">完成此步驟之後，所有角色應該都有 .NET 安裝程式檔案，以及 install.cmd 檔案。</span><span class="sxs-lookup"><span data-stu-id="e762f-154">After this step is complete, all roles should have the .NET installer file and the install.cmd file.</span></span>

   ![所有檔案的角色內容][2]

## <a name="configure-diagnostics-to-transfer-startup-logs-to-blob-storage"></a><span data-ttu-id="e762f-156">設定診斷以將啟動記錄傳輸到 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e762f-156">Configure Diagnostics to transfer startup logs to Blob storage</span></span>
<span data-ttu-id="e762f-157">如要簡化針對安裝問題進行疑難排解，您可以設定 Azure 診斷，來將啟動工作指令碼或 .NET 安裝程式所產生的所有記錄檔傳輸到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e762f-157">To simplify troubleshooting installation issues, you can configure Azure Diagnostics to transfer any log files generated by the startup script or the .NET installer to Azure Blob storage.</span></span> <span data-ttu-id="e762f-158">您可以使用這種方法，從 Blob 儲存體下載記錄檔，而無需遠端桌面到角色，即可檢視記錄。</span><span class="sxs-lookup"><span data-stu-id="e762f-158">By using this approach, you can view the logs by downloading the log files from Blob storage rather than having to remote desktop into the role.</span></span>

<span data-ttu-id="e762f-159">若要設定診斷，請開啟 diagnostics.wadcfgx 檔案，並在 [目錄] 節點下新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="e762f-159">To configure Diagnostics, open the diagnostics.wadcfgx file and add the following content under the **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="e762f-160">這個 XML 會將診斷設定為將 NETFXInstall 資源下 log 目錄中的檔案，傳輸到 **netfx-install** Blob 容器中的診斷儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e762f-160">This XML configures Diagnostics to transfer the files in the log directory in the **NETFXInstall** resource to the Diagnostics storage account in the **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="e762f-161">部署您的雲端服務</span><span class="sxs-lookup"><span data-stu-id="e762f-161">Deploy your cloud service</span></span>
<span data-ttu-id="e762f-162">部署雲端服務時，啟動工作會安裝 .NET Framework (如果尚未安裝)。</span><span class="sxs-lookup"><span data-stu-id="e762f-162">When you deploy your cloud service, the startup tasks install the .NET Framework if it's not already installed.</span></span> <span data-ttu-id="e762f-163">安裝架構時，雲端服務角色會處於忙碌狀態。</span><span class="sxs-lookup"><span data-stu-id="e762f-163">Your cloud service roles are in the *busy* state while the framework is being installed.</span></span> <span data-ttu-id="e762f-164">如果架構安裝需要重新啟動，服務角色可能也會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="e762f-164">If the framework installation requires a restart, the service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e762f-165">其他資源</span><span class="sxs-lookup"><span data-stu-id="e762f-165">Additional resources</span></span>
* <span data-ttu-id="e762f-166">[安裝 .NET Framework][Installing the .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="e762f-166">[Installing the .NET Framework][Installing the .NET Framework]</span></span>
* <span data-ttu-id="e762f-167">[判斷安裝的 .NET Framework 版本][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="e762f-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="e762f-168">[針對 .NET Framework 安裝進行疑難排解][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="e762f-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing the .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
