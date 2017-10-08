---
title: "aaaCommon 雲端服務的啟動工作 |Microsoft 文件"
description: "提供一些範例常見的啟動工作中，您可能想 tooperform 在您的雲端服務 web 角色或背景工作角色。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: a7095dad-1ee7-4141-bc6a-ef19a6e570f1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: c80fac4079439410dfc3795e4bce0fbc07dbbfab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="common-cloud-service-startup-tasks"></a>常見的雲端服務啟動工作
本文提供一些範例常見的啟動工作可能會想 tooperform 雲端服務中。 在角色啟動之前，您可以使用啟動工作 tooperform 作業。 您可能想 tooperform 的作業包括安裝元件、 註冊 COM 元件、 設定登錄機碼，或啟動長時間執行的處理程序。 

請參閱[本文](cloud-services-startup-tasks.md)toounderstand 啟動工作的運作方式，以及特別是如何 toocreate hello 的定義的啟動工作項目。

> [!NOTE]
> 不適用 tooVirtual 機器，只有 tooCloud 服務 Web 和背景工作角色啟動工作。
> 

## <a name="define-environment-variables-before-a-role-starts"></a>定義角色啟動前的環境變數
如果您需要針對特定的工作定義的環境變數，請使用 hello[環境]元素內 hello[工作]項目。

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
                <Environment>
                    <Variable name="MyEnvironmentVariable" value="MyVariableValue" />
                </Environment>
            </Task>
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

變數也可以使用[有效的 Azure XPath 值](cloud-services-role-config-xpath.md)tooreference hello 部署相關的項目。 而不是使用 hello`value`屬性，定義[RoleInstanceValue]子項目。

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a>使用 AppCmd.exe 設定 IIS 啟動
hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx)命令列工具都可以在 Azure 上啟動使用的 toomanage IIS 設定。 *AppCmd.exe*提供方便、 命令列存取 tooconfiguration 設定，以用於啟動工作在 Azure 上。 使用 *AppCmd.exe*，即可針對應用程式和網站，新增、修改或移除網站設定。

不過，有幾件事 toowatch 出的 hello 使用*AppCmd.exe*做為啟動工作：

* 啟動工作可以在重新開機之間執行多次。 例如，角色回收時。
* 如果 *AppCmd.exe* 動作執行一次以上，可能會產生錯誤。 例如，嘗試過 tooadd 區段*Web.config*兩次就會產生錯誤。
* 若啟動工作傳回非零的結束代碼或 **errorlevel**，就會執行失敗。 例如，*AppCmd.exe* 產生錯誤時。

它是很好的作法 toocheck hello **errorlevel**之後呼叫*AppCmd.exe*，這是簡單 toodo 如果 hello 呼叫包裝太*AppCmd.exe*與*.cmd*檔案。 如果偵測到已知的 **errorlevel** 回應，可以予以忽略，或是回傳。

hello 所傳回的 errorlevel *AppCmd.exe*會列在 hello winerror.h 檔案中，而且可能也會發生[MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx)。

### <a name="example-of-managing-hello-error-level"></a>管理 hello 錯誤層級的範例
此範例加入的壓縮區段和壓縮項目，如 JSON toohello *Web.config*錯誤處理和記錄檔。

hello 相關章節 hello [ServiceDefinition.csdef]檔案如下所示，其中包含設定 hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task)屬性太`elevated`toogive *AppCmd.exe*中 hello 足夠的權限 toochange hello 設定*Web.config*檔案：

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

hello *Startup.cmd*批次檔使用*AppCmd.exe* tooadd 的壓縮區段和壓縮項目，如 JSON toohello *Web.config*檔案。 預期的 hello **errorlevel**設定 toozero 使用 hello 確認值為 183 結束。命令列程式 EXE。 未預期的 errorlevel 是記錄的 tooStartupErrorLog.txt。

```cmd
REM   *** Add a compression section toohello Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying tooadd a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. toohandle this situation, set hello ERRORLEVEL toozero by using hello Verify command. hello Verify
REM   command will safely set hello ERRORLEVEL toozero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If hello ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding hello JSON compression type toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report hello date, time, and ERRORLEVEL of hello error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a>新增防火牆規則
Azure 實際上擁有兩個防火牆。 hello 第一個防火牆控制 hello 虛擬機器與外部世界 hello 之間的連接。 此防火牆由 hello[端點]hello 中的項目[ServiceDefinition.csdef]檔案。

hello 第二個防火牆控制 hello 虛擬機器與該虛擬機器中的 hello 程序之間的連接。 此防火牆可以控制 hello`netsh advfirewall firewall`命令列工具。

Azure 會建立防火牆規則 hello 角色內啟動的處理程序。 例如，當您啟動服務或程式，Azure 會自動建立 hello 必要的防火牆規則 tooallow 該服務 toocommunicate 以 hello 網際網路。 不過，如果您建立由角色外部的 （例如 COM + 服務或 Windows 已排程工作） 的處理序啟動服務，您需要 toomanually 建立防火牆規則 tooallow 存取 toothat 服務。 您可以使用啟動工作建立這些防火牆規則。

建立防火牆規則的啟動工作必須具有 [executionContext][工作] (提高權限) 的 **executionContext**，就會執行失敗。 加入下列啟動工作 toohello hello [ServiceDefinition.csdef]檔案。

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="AddFirewallRules.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

tooadd hello 防火牆規則，您必須使用適當的 hello`netsh advfirewall firewall`啟動批次檔中的命令。 在此範例中，hello 啟動工作需要安全性及加密的 TCP 連接埠 80。

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a>封鎖特定的 IP 位址
您可以透過修改 IIS 限制指定的 IP 位址的 Azure web 角色存取 tooa 集**web.config**檔案。 您也需要 toouse hello 會解除鎖定的命令檔**ip 安全性**區段 hello **ApplicationHost.config**檔案。

toodo 解除鎖定 hello **ip 安全性**區段 hello **ApplicationHost.config**檔案中，建立會在角色啟動時執行的命令檔。 在您的 web 角色稱為 hello 根層級建立資料夾**啟動**此外，在此資料夾中，建立批次檔呼叫**startup.cmd**。 此檔案 tooyour Visual Studio 將專案加入並設定 hello 屬性太**永遠複製**tooensure 納入您的封裝。

加入下列啟動工作 toohello hello [ServiceDefinition.csdef]檔案。

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WebRole name="WebRole1">
        ...
        <Startup>
            <Task commandLine="startup.cmd" executionContext="elevated" />
        </Startup>
    </WebRole>
</ServiceDefinition>
```

新增此指令 toohello **startup.cmd**檔案：

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

此工作將導致 hello **startup.cmd**批次檔 toobe 執行每次初始化 hello web 角色時，確保所需的 hello **ip 安全性**區段會解除鎖定。

最後，修改 hello [system.webServer 區段才能](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005)web 角色的**web.config**檔案 tooadd 的被授與存取，IP 位址清單中 hello 下列範例所示：

此範例組態**允許**所有 Ip tooaccess 都 hello 除了都 hello 兩個定義的伺服器

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--hello following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

此範例組態**拒絕**存取 hello 伺服器除了 hello 兩個定義的所有 Ip。

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--hello following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a>建立 PowerShell 啟動工作
Windows PowerShell 指令碼無法直接從 hello 呼叫[ServiceDefinition.csdef]檔案，但它們可以叫用從啟動批次檔內。

PowerShell (依預設) 不會執行未簽署的指令碼。 除非您登入您的指令碼，您需要 tooconfigure PowerShell toorun 未簽署指令碼。 toorun 未簽署指令碼，hello **ExecutionPolicy**必須設定得**Unrestricted**。 hello **ExecutionPolicy**設定您使用根據 hello 版的 Windows PowerShell。

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

如果您使用會 PowerShell 2.0 中執行的客體 OS 或 1.0 您可以強制第 2 版 toorun，而且無法使用，請使用第 1 版。

```cmd
REM   Attempt tooset hello execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set hello execution policy by using hello PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a>透過啟動工作在本機儲存體中建立檔案
您可以使用本機儲存體資源 toostore 稍後存取您的應用程式的啟動工作所建立的檔案。

toocreate hello 本機儲存體資源，加入[LocalResources]區段 toohello [ServiceDefinition.csdef]檔案，然後再加入 hello [LocalStorage]子項目。 啟動工作提供 hello 本機儲存體資源的唯一名稱和適當的大小。

toouse 啟動工作中的本機儲存體資源，您需要 toocreate 環境變數 tooreference hello 本機儲存體資源的位置。 然後 hello 啟動工作和 hello 應用程式都可以 tooread 寫入檔案 toohello 本機儲存體資源。

hello 相關章節 hello **ServiceDefinition.csdef**檔案如下所示：

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">
    ...

    <LocalResources>
      <LocalStorage name="StartupLocalStorage" sizeInMB="5"/>
    </LocalResources>

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="PathToStartupStorage">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
  </WorkerRole>
</ServiceDefinition>
```

例如，這**Startup.cmd**批次檔使用 hello **PathToStartupStorage**環境變數 toocreate hello 檔案**MyTest.txt**在 hello 本機儲存體位置。

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

您可以從 Azure SDK hello 存取本機儲存體資料夾使用 hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx)方法。

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a>在 hello 模擬器或雲端中執行
您可以讓啟動工作在 hello 雲端比較的 toowhen hello 計算模擬器中是其運作時，執行不同的步驟。 比方說，您可能在 hello 模擬器中執行時，才想 toouse 全新的 SQL 資料。 或者，您可能會想 toodo hello 雲端 hello 模擬器中執行時，您不需要 toodo 某些效能最佳化。

這個動作在 hello 計算模擬器以及 hello 雲端可藉由在 hello 中建立環境變數不同的能力 tooperform [ServiceDefinition.csdef]檔案。 然後，您會在啟動工作中測試該環境變數的值。

toocreate hello 環境變數，新增 hello[變數]/[RoleInstanceValue]項目，並建立的 XPath 值`/RoleEnvironment/Deployment/@emulated`。 hello 值 hello **%computeemulatorrunning**環境變數是`true`hello 計算模擬器上執行時和`false`hello 雲端上執行時。

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">

    ...

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>

  </WorkerRole>
</ServiceDefinition>
```

hello 工作現在可以檢查 hello **%computeemulatorrunning**環境變數 tooperform 不同的動作根據 hello 角色執行在 hello 雲端或 hello 模擬器。 以下是檢查該環境變數的 .cmd 命令介面指令碼。

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a>偵測工作是否已在執行
hello 角色可能會導致您的啟動工作 toorun 一次重新開機回收。 沒有任何工作已執行 hello 裝載 VM 的旗標 tooindicate。 可能有些工作即便多次執行也沒關係。 不過，您可以執行的情況，您需要 tooprevent 工作執行一次以上。

hello 最簡單方式 toodetect 工作已執行的是 toocreate hello 中的檔案**%TEMP%** hello 工作成功時 資料夾並尋找它在 hello 開頭 hello 工作。 以下是可為您執行此作業的範例 cmd Shell 指令碼。

```cmd
REM   If Task1_Success.txt exists, then Application 1 is already installed.
IF EXIST "%RoleRoot%\Task1_Success.txt" (
  ECHO Application 1 is already installed. Exiting. >> "%TEMP%\StartupLog.txt" 2>&1
  GOTO Finish
)

REM   Run your real exe task
ECHO Running XYZ >> "%TEMP%\StartupLog.txt" 2>&1
"%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (
  REM   hello application installed without error. Create a file tooindicate that hello task
  REM   does not need toobe run again.

  ECHO This line will create a file tooindicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log hello error and exit with hello error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a>工作最佳作法
為 Web 或背景工作角色設定工作時，應該遵循的最佳作法如下。

### <a name="always-log-startup-activities"></a>務必記錄啟動活動
Visual Studio 不提供偵錯工具 toostep 透過批次檔，因此您很好的 tooget 資料量 hello 的批次檔中的作業越好。 記錄的批次檔的 hello 輸出兩者**stdout**和**stderr**、 可以讓您有重要的資訊時，嘗試 toodebug 及修正批次檔。 這兩個 toolog **stdout**和**stderr** toohello hello 目錄指向的 tooby hello 中的 StartupLog.txt 檔案**%TEMP%**環境變數加入 hello 文字`>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello 結尾的特定程式碼行您想 toolog。 例如，在 hello tooexecute setup.exe **%pathtoapp1install%**目錄：

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

toosimplify 您的 xml，您可以建立包裝函式*cmd*呼叫所有啟動的檔案以及記錄工作，並確保每一個子工作共用 hello 相同的環境變數。

您可能會發現它雖然惱人 toouse`>> "%TEMP%\StartupLog.txt" 2>&1`一端的每個啟動工作 hello。 您可以建立會為您處理記錄的包裝函式，以強制執行工作記錄。 這個包裝函式會呼叫您想要 toorun hello 真實的批次檔。 Hello 目標批次檔中的任何輸出將會重新導向的 toohello *Startuplog.txt*檔案。

hello 啟動批次檔中的下列範例會示範如何 tooredirect 所有輸出。 在此範例中，hello ServerDefinition.csdef 檔會建立啟動工作呼叫*logwrap.cmd*。 *logwrap.cmd*呼叫*Startup2.cmd*，將所有輸出重新都導向太**%TEMP%\\StartupLog.txt**。

ServiceDefinition.cmd：

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

**logwrap.cmd：**

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output toohello StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call hello child command batch file, redirecting all output toohello StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log hello completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log hello error.
   ECHO [%date% %time%] An error occurred. hello ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

**Startup2.cmd：**

```cmd
@ECHO OFF

REM   This is hello batch file where hello startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in hello directory pointed tooby hello TEMP environment variable.

REM   If an error occurs, hello following command will pass hello ERRORLEVEL back toothe
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

範例輸出中 hello **StartupLog.txt**檔案：

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> hello **StartupLog.txt**檔案位於 hello *C:\Resources\temp\\{角色識別碼} \RoleTemp*資料夾。
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a>正確設定啟動工作的 executionContext
設定適用於 hello 啟動工作的權限。 有時啟動工作必須執行以提高權限，即使 hello 角色是執行具有標準權限。

hello [executionContext][工作]屬性會設定權限層級 hello hello 啟動工作。 使用`executionContext="limited"`hello 啟動工作的表示 hello hello 角色相同的權限層級。 使用`executionContext="elevated"`表示 hello 啟動工作具有系統管理員權限，讓 hello 啟動工作 tooperform 系統管理員工作而不需給予系統管理員權限 tooyour 角色。

需要更高權的限的啟動工作的範例是使用的啟動工作**AppCmd.exe** tooconfigure IIS。 **AppCmd.exe** 需使用 `executionContext="elevated"`。

### <a name="use-hello-appropriate-tasktype"></a>使用 hello 適當的 taskType
hello [taskType][工作]屬性會決定 hello 方式 hello 啟動工作的執行。 此屬性有三個值：**simple**、**background** 和 **foreground**。 hello 背景和前景工作會以非同步方式啟動，並且再 hello 簡單的工作會以同步方式執行一次。

與**簡單**啟動工作，您可以設定 hello hello 工作執行的順序 hello hello ServiceDefinition.csdef 檔案中列出的 hello 工作的順序。 如果**簡單**工作結束非零值結束代碼，則 hello 啟動程序會停止而且 hello 角色無法啟動。

hello 差異**背景**啟動工作和**前景**啟動工作是**前景**工作保留 hello 角色執行，直到 hello **前景**工作結束。 這也表示，如果 hello**前景**工作停止回應或當機，hello 才會回收角色直到 hello**前景**工作強制關閉。 基於這個理由，**背景**工作建議您使用非同步啟動工作除非需要該功能的 hello**前景**工作。

### <a name="end-batch-files-with-exit-b-0"></a>以 EXIT /B 0 結束批次檔
hello 角色，才會開始如果 hello **errorlevel**從每個簡單啟動工作是零。 並非所有的程式設定 hello **errorlevel** （結束代碼） 正確，因此 hello 批次檔應以結尾`EXIT /B 0`如果所有項目是否正確執行。

遺漏`EXIT /B 0`hello 啟動批次檔的結尾是角色未啟動的常見原因。

> [!NOTE]
> 偶發性該巢狀的批次檔案有時停止回應時使用 hello`/B`參數。 您可能會想確定這個停止回應問題不會發生另一個批次檔呼叫目前的批次檔，例如如果您使用 hello toomake[記錄包裝函式](#always-log-startup-activities)。 您可以省略 hello`/B`參數在此情況下。
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a>預期啟動工作 toorun 一次以上
並非所有角色回收都會重新開機，但所有角色回收都會執行全部的啟動工作。 這表示啟動工作必須能夠 toorun 多次接連不會有任何問題。 Hello 討論這[前面一節](#detect-that-your-task-has-already-run)。

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a>使用本機儲存體 toostore 檔案必須在 hello 角色中存取
如果您想要 toocopy 或啟動工作期間建立的檔案，然後存取 tooyour 角色，則該檔案必須放在本機儲存體。 請參閱 hello[前面一節](#create-files-in-local-storage-from-a-startup-task)。

## <a name="next-steps"></a>後續步驟
檢閱 hello 雲端[服務模型和封裝](cloud-services-model-and-package.md)

深入了解 [工作](cloud-services-startup-tasks.md) 如何運作。

[建立和部署](cloud-services-how-to-create-deploy-portal.md) 雲端服務封裝。

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[工作]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[環境]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[變數]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
[EndPoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints
[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage
[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
