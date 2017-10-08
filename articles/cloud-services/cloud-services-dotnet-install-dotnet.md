---
title: "在 Azure 雲端服務角色 aaaInstall.NET |Microsoft 文件"
description: "本文說明 toomanually 在雲端服務 web 和背景工作角色上所安裝的.NET Framework hello"
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
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="28dbe-103">在 Azure 雲端服務角色上安裝 .NET</span><span class="sxs-lookup"><span data-stu-id="28dbe-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="28dbe-104">本文說明如何 tooinstall 不隨附的.NET Framework 版本 hello Azure 客體作業系統。</span><span class="sxs-lookup"><span data-stu-id="28dbe-104">This article describes how tooinstall versions of .NET Framework that don't come with hello Azure Guest OS.</span></span> <span data-ttu-id="28dbe-105">您可以使用.NET hello 客體 OS tooconfigure 上將雲端服務 web 和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="28dbe-105">You can use .NET on hello Guest OS tooconfigure your cloud service web and worker roles.</span></span>

<span data-ttu-id="28dbe-106">比方說，您可以在 hello 客體 OS 系列 4，並未隨附任何版本的.NET 4.6 上安裝.NET 4.6.1。</span><span class="sxs-lookup"><span data-stu-id="28dbe-106">For example, you can install .NET 4.6.1 on hello Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="28dbe-107">（.NET 4.6 會帶來 hello 客體 OS 系列 5）。Azure 客體作業系統版本上 hello hello 最新資訊，請參閱 hello [Azure 客體作業系統版次新聞](cloud-services-guestos-update-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="28dbe-107">(hello Guest OS family 5 does come with .NET 4.6.) For hello latest information on hello Azure Guest OS releases, see hello [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="28dbe-108">hello Azure SDK 2.9 中包含限制 hello 客體 OS 系列 4 或更早版本上部署.NET 4.6。</span><span class="sxs-lookup"><span data-stu-id="28dbe-108">hello Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on hello Guest OS family 4 or earlier.</span></span> <span data-ttu-id="28dbe-109">修正 hello 限制位於 hello [Microsoft 文件](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9)站台。</span><span class="sxs-lookup"><span data-stu-id="28dbe-109">A fix for hello restriction is available on hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="28dbe-110">在 web 和背景工作角色中，tooinstall.NET 包含 hello.NET web 安裝程式，做為雲端服務專案的一部分。</span><span class="sxs-lookup"><span data-stu-id="28dbe-110">tooinstall .NET on your web and worker roles, include hello .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="28dbe-111">啟動 hello installer hello 角色啟動工作的一部分。</span><span class="sxs-lookup"><span data-stu-id="28dbe-111">Start hello installer as part of hello role's startup tasks.</span></span> 

## <a name="add-hello-net-installer-tooyour-project"></a><span data-ttu-id="28dbe-112">新增 hello.NET 安裝程式 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="28dbe-112">Add hello .NET installer tooyour project</span></span>
<span data-ttu-id="28dbe-113">toodownload hello web 安裝程式 hello.NET Framework 中，選擇您想 tooinstall hello 版本：</span><span class="sxs-lookup"><span data-stu-id="28dbe-113">toodownload hello web installer for hello .NET Framework, choose hello version that you want tooinstall:</span></span>

* [<span data-ttu-id="28dbe-114">.NET 4.7 web 安裝程式</span><span class="sxs-lookup"><span data-stu-id="28dbe-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="28dbe-115">.NET 4.6.1 web 安裝程式</span><span class="sxs-lookup"><span data-stu-id="28dbe-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="28dbe-116">tooadd hello 安裝程式*web*角色：</span><span class="sxs-lookup"><span data-stu-id="28dbe-116">tooadd hello installer for a *web* role:</span></span>
  1. <span data-ttu-id="28dbe-117">在 [方案總管] 中，於雲端服務專案中的 [角色] 下，以滑鼠右鍵按一下您的 web角色，然後依序選取 [新增] > [新增資料夾]。</span><span class="sxs-lookup"><span data-stu-id="28dbe-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="28dbe-118">建立名為 **bin** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="28dbe-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="28dbe-119">以滑鼠右鍵按一下 hello bin 資料夾，然後選取**新增** > **現有項目**。</span><span class="sxs-lookup"><span data-stu-id="28dbe-119">Right-click hello bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="28dbe-120">選取 hello.NET 安裝程式，並將它加入 toohello bin 資料夾。</span><span class="sxs-lookup"><span data-stu-id="28dbe-120">Select hello .NET installer and add it toohello bin folder.</span></span>
  
<span data-ttu-id="28dbe-121">tooadd hello 安裝程式*工作者*角色：</span><span class="sxs-lookup"><span data-stu-id="28dbe-121">tooadd hello installer for a *worker* role:</span></span>
* <span data-ttu-id="28dbe-122">以滑鼠右鍵按一下您的 worker 角色，然後依序選取 [新增] > [現有項目]。</span><span class="sxs-lookup"><span data-stu-id="28dbe-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="28dbe-123">選取 hello.NET 安裝程式，並將它加入 toohello 角色。</span><span class="sxs-lookup"><span data-stu-id="28dbe-123">Select hello .NET installer and add it toohello role.</span></span> 

<span data-ttu-id="28dbe-124">當檔案加入這個方式 toohello 角色內容資料夾中時，使用者在自動新增 tooyour 雲端服務封裝。</span><span class="sxs-lookup"><span data-stu-id="28dbe-124">When files are added in this way toohello role content folder, they're automatically added tooyour cloud service package.</span></span> <span data-ttu-id="28dbe-125">hello 檔案就已部署的 tooa hello 虛擬機器上的一致位置。</span><span class="sxs-lookup"><span data-stu-id="28dbe-125">hello files are then deployed tooa consistent location on hello virtual machine.</span></span> <span data-ttu-id="28dbe-126">重複此程序針對雲端服務中的每個 web 和背景工作角色，如此所有角色都有一份 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="28dbe-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of hello installer.</span></span>

> [!NOTE]
> <span data-ttu-id="28dbe-127">即使您的應用程式是以 .NET 4.6 為目標，還是應該在雲端服務角色上安裝 .NET 4.6.1。</span><span class="sxs-lookup"><span data-stu-id="28dbe-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="28dbe-128">hello 客體作業系統包括 hello 知識庫[更新 3098779](https://support.microsoft.com/kb/3098779)和[更新 3097997](https://support.microsoft.com/kb/3097997)。</span><span class="sxs-lookup"><span data-stu-id="28dbe-128">hello Guest OS includes hello Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="28dbe-129">當您執行.NET 應用程式如果之上 hello 知識庫更新安裝.NET 4.6 時，可能會發生問題。</span><span class="sxs-lookup"><span data-stu-id="28dbe-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of hello Knowledge Base updates.</span></span> <span data-ttu-id="28dbe-130">tooavoid 這些問題，安裝.NET 4.6.1，而不是版本 4.6。</span><span class="sxs-lookup"><span data-stu-id="28dbe-130">tooavoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="28dbe-131">如需詳細資訊，請參閱 hello [Knowledge Base 文章 3118750](https://support.microsoft.com/kb/3118750)。</span><span class="sxs-lookup"><span data-stu-id="28dbe-131">For more information, see hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![安裝程式檔案的角色內容][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="28dbe-133">定義角色的啟動工作</span><span class="sxs-lookup"><span data-stu-id="28dbe-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="28dbe-134">在角色啟動之前，您可以使用啟動工作 tooperform 作業。</span><span class="sxs-lookup"><span data-stu-id="28dbe-134">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="28dbe-135">安裝.NET Framework hello hello 啟動工作的一部分，可確保該 hello framework 已安裝任何應用程式程式碼執行之前。</span><span class="sxs-lookup"><span data-stu-id="28dbe-135">Installing hello .NET Framework as part of hello startup task ensures that hello framework is installed before any application code is run.</span></span> <span data-ttu-id="28dbe-136">如需有關啟動工作的詳細資訊，請參閱[在 Azure 中執行啟動工作](cloud-services-startup-tasks.md)。</span><span class="sxs-lookup"><span data-stu-id="28dbe-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="28dbe-137">新增下列內容 toohello ServiceDefinition.csdef 檔下 hello hello **WebRole**或**WorkerRole**所有角色的節點：</span><span class="sxs-lookup"><span data-stu-id="28dbe-137">Add hello following content toohello ServiceDefinition.csdef file under hello **WebRole** or **WorkerRole** node for all roles:</span></span>
   
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
   
    <span data-ttu-id="28dbe-138">hello 前面的組態中執行 hello 主控台命令`install.cmd`與系統管理員權限 tooinstall hello .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="28dbe-138">hello preceding configuration runs hello console command `install.cmd` with administrator privileges tooinstall hello .NET Framework.</span></span> <span data-ttu-id="28dbe-139">hello 組態也會建立**LocalStorage**名**NETFXInstall**。</span><span class="sxs-lookup"><span data-stu-id="28dbe-139">hello configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="28dbe-140">hello 啟動指令碼設定 hello 暫存資料夾 toouse 這個本機儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="28dbe-140">hello startup script sets hello temp folder toouse this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="28dbe-141">tooensure 更正安裝 hello framework，此資源 tooat 組 hello 大小至少 1024 MB。</span><span class="sxs-lookup"><span data-stu-id="28dbe-141">tooensure correct installation of hello framework, set hello size of this resource tooat least 1,024 MB.</span></span>
    
    <span data-ttu-id="28dbe-142">如需有關啟動工作的詳細資訊，請參閱[常見的 Azure 雲端服務啟動工作](cloud-services-startup-tasks-common.md)。</span><span class="sxs-lookup"><span data-stu-id="28dbe-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="28dbe-143">建立名為**install.cmd**並加入 hello 下列安裝指令碼 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="28dbe-143">Create a file named **install.cmd** and add hello following install script toohello file.</span></span>

    <span data-ttu-id="28dbe-144">hello 指令碼會檢查是否 hello 指定的 hello.NET Framework 版本已安裝在 hello 機器上藉由查詢 hello 登錄。</span><span class="sxs-lookup"><span data-stu-id="28dbe-144">hello script checks whether hello specified version of hello .NET Framework is already installed on hello machine by querying hello registry.</span></span> <span data-ttu-id="28dbe-145">如果未安裝 hello.NET 版本，會開啟 hello.NET web 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="28dbe-145">If hello .NET version is not installed, then hello .NET web installer is opened.</span></span> <span data-ttu-id="28dbe-146">toohelp 疑難排解任何問題，請 hello 指令碼會記錄所有活動 toohello 檔案 startuptasklog-（目前的日期和時間）.txt，其中會儲存在**InstallLogs**本機儲存體。</span><span class="sxs-lookup"><span data-stu-id="28dbe-146">toohelp troubleshoot any issues, hello script logs all activity toohello file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="28dbe-147">就像 Windows 記事本 toocreate hello install.cmd 檔案一樣使用基本的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="28dbe-147">Use a basic text editor like Windows Notepad toocreate hello install.cmd file.</span></span> <span data-ttu-id="28dbe-148">如果您使用 Visual Studio toocreate 文字檔案，並變更 hello 延伸 too.cmd hello 檔案可能仍會包含 utf-8 位元組順序標記。</span><span class="sxs-lookup"><span data-stu-id="28dbe-148">If you use Visual Studio toocreate a text file and change hello extension too.cmd, hello file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="28dbe-149">Hello 第一行 hello 指令碼執行時，此標記可能會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="28dbe-149">This mark can cause an error when hello first line of hello script is run.</span></span> <span data-ttu-id="28dbe-150">tooavoid 這個錯誤，請 hello 第一行 hello hello 位元組順序處理可以略過 REM 陳述式的指令碼。</span><span class="sxs-lookup"><span data-stu-id="28dbe-150">tooavoid this error, make hello first line of hello script a REM statement that can be skipped by hello byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
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
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="28dbe-151">此指令碼會示範如何 tooinstall.NET 4.5.2 或 4.6 版本持續性，即使已經裝有.NET 4.5.2 hello Azure 客體作業系統。</span><span class="sxs-lookup"><span data-stu-id="28dbe-151">This script shows how tooinstall .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on hello Azure Guest OS.</span></span> <span data-ttu-id="28dbe-152">您應該直接安裝.NET 4.6.1，而不是版本 4.6 hello 中所述[Knowledge Base 文章 3118750](https://support.microsoft.com/kb/3118750)。</span><span class="sxs-lookup"><span data-stu-id="28dbe-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="28dbe-153">新增 hello install.cmd 檔案 tooeach 角色使用**新增** > **現有項目**中**方案總管 中**稍早在本主題中所述。</span><span class="sxs-lookup"><span data-stu-id="28dbe-153">Add hello install.cmd file tooeach role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="28dbe-154">完成此步驟之後，所有角色都應該都有 hello.NET 安裝程式檔案和 hello install.cmd 檔案。</span><span class="sxs-lookup"><span data-stu-id="28dbe-154">After this step is complete, all roles should have hello .NET installer file and hello install.cmd file.</span></span>

   ![所有檔案的角色內容][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a><span data-ttu-id="28dbe-156">設定診斷 tootransfer 啟動記錄 tooBlob 存放裝置</span><span class="sxs-lookup"><span data-stu-id="28dbe-156">Configure Diagnostics tootransfer startup logs tooBlob storage</span></span>
<span data-ttu-id="28dbe-157">toosimplify 疑難排解安裝問題，您可以設定 Azure 診斷 tootransfer hello 啟動所產生任何記錄檔指令碼或 hello.NET 安裝程式 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="28dbe-157">toosimplify troubleshooting installation issues, you can configure Azure Diagnostics tootransfer any log files generated by hello startup script or hello .NET installer tooAzure Blob storage.</span></span> <span data-ttu-id="28dbe-158">使用這種方法，您可以從 Blob 儲存體下載 hello 記錄檔，而不是需要 tooremote 桌面連入 hello 角色，以檢視 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="28dbe-158">By using this approach, you can view hello logs by downloading hello log files from Blob storage rather than having tooremote desktop into hello role.</span></span>

<span data-ttu-id="28dbe-159">tooconfigure 診斷開啟 hello diagnostics.wadcfgx 檔案，並新增下列內容在 hello hello**目錄**節點：</span><span class="sxs-lookup"><span data-stu-id="28dbe-159">tooconfigure Diagnostics, open hello diagnostics.wadcfgx file and add hello following content under hello **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="28dbe-160">這段 XML 會在 hello hello 記錄目錄中來設定診斷 tootransfer hello 檔案**NETFXInstall**資源 toohello 診斷儲存體帳戶中 hello **netfx 安裝**blob 容器。</span><span class="sxs-lookup"><span data-stu-id="28dbe-160">This XML configures Diagnostics tootransfer hello files in hello log directory in hello **NETFXInstall** resource toohello Diagnostics storage account in hello **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="28dbe-161">部署您的雲端服務</span><span class="sxs-lookup"><span data-stu-id="28dbe-161">Deploy your cloud service</span></span>
<span data-ttu-id="28dbe-162">當您部署雲端服務時，hello 啟動工作安裝 hello.NET Framework，如果尚未安裝。</span><span class="sxs-lookup"><span data-stu-id="28dbe-162">When you deploy your cloud service, hello startup tasks install hello .NET Framework if it's not already installed.</span></span> <span data-ttu-id="28dbe-163">將雲端服務角色位於 hello*忙碌*hello 架構在安裝時的狀態。</span><span class="sxs-lookup"><span data-stu-id="28dbe-163">Your cloud service roles are in hello *busy* state while hello framework is being installed.</span></span> <span data-ttu-id="28dbe-164">如果 hello framework 安裝需要重新啟動，可能也會重新啟動 hello 服務角色。</span><span class="sxs-lookup"><span data-stu-id="28dbe-164">If hello framework installation requires a restart, hello service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="28dbe-165">其他資源</span><span class="sxs-lookup"><span data-stu-id="28dbe-165">Additional resources</span></span>
* <span data-ttu-id="28dbe-166">[安裝.NET Framework hello][Installing hello .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="28dbe-166">[Installing hello .NET Framework][Installing hello .NET Framework]</span></span>
* <span data-ttu-id="28dbe-167">[判斷安裝的 .NET Framework 版本][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="28dbe-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="28dbe-168">[針對 .NET Framework 安裝進行疑難排解][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="28dbe-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
