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
# <a name="install-net-on-azure-cloud-services-roles"></a>在 Azure 雲端服務角色上安裝 .NET
本文說明如何 tooinstall 不隨附的.NET Framework 版本 hello Azure 客體作業系統。 您可以使用.NET hello 客體 OS tooconfigure 上將雲端服務 web 和背景工作角色。

比方說，您可以在 hello 客體 OS 系列 4，並未隨附任何版本的.NET 4.6 上安裝.NET 4.6.1。 （.NET 4.6 會帶來 hello 客體 OS 系列 5）。Azure 客體作業系統版本上 hello hello 最新資訊，請參閱 hello [Azure 客體作業系統版次新聞](cloud-services-guestos-update-matrix.md)。 

>[!IMPORTANT]
>hello Azure SDK 2.9 中包含限制 hello 客體 OS 系列 4 或更早版本上部署.NET 4.6。 修正 hello 限制位於 hello [Microsoft 文件](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9)站台。

在 web 和背景工作角色中，tooinstall.NET 包含 hello.NET web 安裝程式，做為雲端服務專案的一部分。 啟動 hello installer hello 角色啟動工作的一部分。 

## <a name="add-hello-net-installer-tooyour-project"></a>新增 hello.NET 安裝程式 tooyour 專案
toodownload hello web 安裝程式 hello.NET Framework 中，選擇您想 tooinstall hello 版本：

* [.NET 4.7 web 安裝程式](http://go.microsoft.com/fwlink/?LinkId=825298)
* [.NET 4.6.1 web 安裝程式](http://go.microsoft.com/fwlink/?LinkId=671729)

tooadd hello 安裝程式*web*角色：
  1. 在 [方案總管] 中，於雲端服務專案中的 [角色] 下，以滑鼠右鍵按一下您的 web角色，然後依序選取 [新增] > [新增資料夾]。 建立名為 **bin** 的資料夾。
  2. 以滑鼠右鍵按一下 hello bin 資料夾，然後選取**新增** > **現有項目**。 選取 hello.NET 安裝程式，並將它加入 toohello bin 資料夾。
  
tooadd hello 安裝程式*工作者*角色：
* 以滑鼠右鍵按一下您的 worker 角色，然後依序選取 [新增] > [現有項目]。 選取 hello.NET 安裝程式，並將它加入 toohello 角色。 

當檔案加入這個方式 toohello 角色內容資料夾中時，使用者在自動新增 tooyour 雲端服務封裝。 hello 檔案就已部署的 tooa hello 虛擬機器上的一致位置。 重複此程序針對雲端服務中的每個 web 和背景工作角色，如此所有角色都有一份 hello 安裝程式。

> [!NOTE]
> 即使您的應用程式是以 .NET 4.6 為目標，還是應該在雲端服務角色上安裝 .NET 4.6.1。 hello 客體作業系統包括 hello 知識庫[更新 3098779](https://support.microsoft.com/kb/3098779)和[更新 3097997](https://support.microsoft.com/kb/3097997)。 當您執行.NET 應用程式如果之上 hello 知識庫更新安裝.NET 4.6 時，可能會發生問題。 tooavoid 這些問題，安裝.NET 4.6.1，而不是版本 4.6。 如需詳細資訊，請參閱 hello [Knowledge Base 文章 3118750](https://support.microsoft.com/kb/3118750)。
> 
> 

![安裝程式檔案的角色內容][1]

## <a name="define-startup-tasks-for-your-roles"></a>定義角色的啟動工作
在角色啟動之前，您可以使用啟動工作 tooperform 作業。 安裝.NET Framework hello hello 啟動工作的一部分，可確保該 hello framework 已安裝任何應用程式程式碼執行之前。 如需有關啟動工作的詳細資訊，請參閱[在 Azure 中執行啟動工作](cloud-services-startup-tasks.md)。 

1. 新增下列內容 toohello ServiceDefinition.csdef 檔下 hello hello **WebRole**或**WorkerRole**所有角色的節點：
   
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
   
    hello 前面的組態中執行 hello 主控台命令`install.cmd`與系統管理員權限 tooinstall hello .NET Framework。 hello 組態也會建立**LocalStorage**名**NETFXInstall**。 hello 啟動指令碼設定 hello 暫存資料夾 toouse 這個本機儲存體資源。 
    
    > [!IMPORTANT]
    > tooensure 更正安裝 hello framework，此資源 tooat 組 hello 大小至少 1024 MB。
    
    如需有關啟動工作的詳細資訊，請參閱[常見的 Azure 雲端服務啟動工作](cloud-services-startup-tasks-common.md)。

2. 建立名為**install.cmd**並加入 hello 下列安裝指令碼 toohello 檔案。

    hello 指令碼會檢查是否 hello 指定的 hello.NET Framework 版本已安裝在 hello 機器上藉由查詢 hello 登錄。 如果未安裝 hello.NET 版本，會開啟 hello.NET web 安裝程式。 toohelp 疑難排解任何問題，請 hello 指令碼會記錄所有活動 toohello 檔案 startuptasklog-（目前的日期和時間）.txt，其中會儲存在**InstallLogs**本機儲存體。

    > [!IMPORTANT]
    > 就像 Windows 記事本 toocreate hello install.cmd 檔案一樣使用基本的文字編輯器。 如果您使用 Visual Studio toocreate 文字檔案，並變更 hello 延伸 too.cmd hello 檔案可能仍會包含 utf-8 位元組順序標記。 Hello 第一行 hello 指令碼執行時，此標記可能會導致錯誤。 tooavoid 這個錯誤，請 hello 第一行 hello hello 位元組順序處理可以略過 REM 陳述式的指令碼。 
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
   > 此指令碼會示範如何 tooinstall.NET 4.5.2 或 4.6 版本持續性，即使已經裝有.NET 4.5.2 hello Azure 客體作業系統。 您應該直接安裝.NET 4.6.1，而不是版本 4.6 hello 中所述[Knowledge Base 文章 3118750](https://support.microsoft.com/kb/3118750)。
   > 
   > 

3. 新增 hello install.cmd 檔案 tooeach 角色使用**新增** > **現有項目**中**方案總管 中**稍早在本主題中所述。 

    完成此步驟之後，所有角色都應該都有 hello.NET 安裝程式檔案和 hello install.cmd 檔案。

   ![所有檔案的角色內容][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a>設定診斷 tootransfer 啟動記錄 tooBlob 存放裝置
toosimplify 疑難排解安裝問題，您可以設定 Azure 診斷 tootransfer hello 啟動所產生任何記錄檔指令碼或 hello.NET 安裝程式 tooAzure Blob 儲存體。 使用這種方法，您可以從 Blob 儲存體下載 hello 記錄檔，而不是需要 tooremote 桌面連入 hello 角色，以檢視 hello 記錄檔。

tooconfigure 診斷開啟 hello diagnostics.wadcfgx 檔案，並新增下列內容在 hello hello**目錄**節點： 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

這段 XML 會在 hello hello 記錄目錄中來設定診斷 tootransfer hello 檔案**NETFXInstall**資源 toohello 診斷儲存體帳戶中 hello **netfx 安裝**blob 容器。

## <a name="deploy-your-cloud-service"></a>部署您的雲端服務
當您部署雲端服務時，hello 啟動工作安裝 hello.NET Framework，如果尚未安裝。 將雲端服務角色位於 hello*忙碌*hello 架構在安裝時的狀態。 如果 hello framework 安裝需要重新啟動，可能也會重新啟動 hello 服務角色。 

## <a name="additional-resources"></a>其他資源
* [安裝.NET Framework hello][Installing hello .NET Framework]
* [判斷安裝的 .NET Framework 版本][How to: Determine Which .NET Framework Versions Are Installed]
* [針對 .NET Framework 安裝進行疑難排解][Troubleshooting .NET Framework Installations]

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
