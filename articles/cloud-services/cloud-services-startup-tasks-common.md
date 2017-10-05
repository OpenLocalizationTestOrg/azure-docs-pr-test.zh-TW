---
title: "雲端服務的常見啟動工作 | Microsoft Docs"
description: "提供一些常見的啟動工作範例，做為您在雲端服務 Web 角色或背景工作角色中執行的參考。"
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
ms.openlocfilehash: cee23da5b089b02bfc0ef10afd60f0f2272585b1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="ce8fb-103">常見的雲端服務啟動工作</span><span class="sxs-lookup"><span data-stu-id="ce8fb-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="ce8fb-104">本文提供一些常見的啟動工作範例，做為您在雲端服務中執行的參考。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-104">This article provides some examples of common startup tasks you may want to perform in your cloud service.</span></span> <span data-ttu-id="ce8fb-105">您可以利用啟動工作，在角色啟動之前執行作業。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="ce8fb-106">您可能想要執行的作業包括安裝元件、註冊 COM 元件、設定登錄機碼，或啟動長時間執行的處理序。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="ce8fb-107">請參閱 [這篇文章](cloud-services-startup-tasks.md) ，了解啟動工作的運作方式，特別是該如何建立定義啟動工作的項目。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-107">See [this article](cloud-services-startup-tasks.md) to understand how startup tasks work, and specifically how to create the entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="ce8fb-108">啟動工作不適用於虛擬機器，只適用於雲端服務 Web 和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-108">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="ce8fb-109">定義角色啟動前的環境變數</span><span class="sxs-lookup"><span data-stu-id="ce8fb-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="ce8fb-110">如果您需要針對特定工作定義的環境變數，可以使用 [Task] 項目中的 [Environment] 項目。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-110">If you need environment variables defined for a specific task, use the [Environment] element inside the [Task] element.</span></span>

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

<span data-ttu-id="ce8fb-111">變數也可以使用[有效的 Azure XPath 值](cloud-services-role-config-xpath.md)，以參考部署的相關項目。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) to reference something about the deployment.</span></span> <span data-ttu-id="ce8fb-112">而不是使用 `value` 屬性定義 [RoleInstanceValue] 子項目。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-112">Instead of using the `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="ce8fb-113">使用 AppCmd.exe 設定 IIS 啟動</span><span class="sxs-lookup"><span data-stu-id="ce8fb-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="ce8fb-114">[AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) 命令列工具可用來管理在 Azure 上啟動時的 IIS 設定。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-114">The [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used to manage IIS settings at startup on Azure.</span></span> <span data-ttu-id="ce8fb-115">*AppCmd.exe* 提供方便的命令列，可存取 Azure 上啟動工作所使用的組態設定。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-115">*AppCmd.exe* provides convenient, command-line access to configuration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="ce8fb-116">使用 *AppCmd.exe*，即可針對應用程式和網站，新增、修改或移除網站設定。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="ce8fb-117">不過，使用 *AppCmd.exe* 做為啟動工作時，需要注意幾件事情：</span><span class="sxs-lookup"><span data-stu-id="ce8fb-117">However, there are a few things to watch out for in the use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="ce8fb-118">啟動工作可以在重新開機之間執行多次。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="ce8fb-119">例如，角色回收時。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="ce8fb-120">如果 *AppCmd.exe* 動作執行一次以上，可能會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="ce8fb-121">例如，嘗試將區段新增至 *Web.config* 兩次，就可能會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-121">For example, attempting to add a section to *Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="ce8fb-122">若啟動工作傳回非零的結束代碼或 **errorlevel**，就會執行失敗。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="ce8fb-123">例如，*AppCmd.exe* 產生錯誤時。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="ce8fb-124">呼叫 *AppCmd.exe* 之後，最好檢查 **errorlevel**，如果您是使用 *.cmd* 檔案包裝 *AppCmd.exe* 的呼叫，可讓這項檢查作業更容易進行。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-124">It is a good practice to check the **errorlevel** after calling *AppCmd.exe*, which is easy to do if you wrap the call to *AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="ce8fb-125">如果偵測到已知的 **errorlevel** 回應，可以予以忽略，或是回傳。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="ce8fb-126">*AppCmd.exe* 傳回的 errorlevel 會列在 winerror.h 檔案中，[MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx) 中也會顯示。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-126">The errorlevel returned by *AppCmd.exe* are listed in the winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-the-error-level"></a><span data-ttu-id="ce8fb-127">管理錯誤層級的範例</span><span class="sxs-lookup"><span data-stu-id="ce8fb-127">Example of managing the error level</span></span>
<span data-ttu-id="ce8fb-128">此範例會在 *Web.config* 檔案中，加入 JSON 的 compression 區段和壓縮項目，以及錯誤處理和記錄。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-128">This example adds a compression section and a compression entry for JSON to the *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="ce8fb-129">這裡會顯示 [ServiceDefinition.csdef] 檔案的相關區段，其中包括將 [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) 屬性設為 `elevated`，藉此提供 *AppCmd.exe* 足夠的權限，以變更 *Web.config* 檔案中的設定：</span><span class="sxs-lookup"><span data-stu-id="ce8fb-129">The relevant sections of the [ServiceDefinition.csdef] file are shown here, which include setting the [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute to `elevated` to give *AppCmd.exe* sufficient permissions to change the settings in the *Web.config* file:</span></span>

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

<span data-ttu-id="ce8fb-130">*Startup.cmd* 批次檔會使用 *AppCmd.exe*，在 *Web.config* 檔案中新增 JSON 的 compression 區段和 compression 項目。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-130">The *Startup.cmd* batch file uses *AppCmd.exe* to add a compression section and a compression entry for JSON to the *Web.config* file.</span></span> <span data-ttu-id="ce8fb-131">預期的 **errorlevel** = 183 會使用 VERIFY.EXE 命令列程式設為零。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-131">The expected **errorlevel** of 183 is set to zero using the VERIFY.EXE command-line program.</span></span> <span data-ttu-id="ce8fb-132">非預期的 errorlevel 會記錄至 StartupErrorLog.txt。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-132">Unexpected errorlevels are logged to StartupErrorLog.txt.</span></span>

```cmd
REM   *** Add a compression section to the Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying to add a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. To handle this situation, set the ERRORLEVEL to zero by using the Verify command. The Verify
REM   command will safely set the ERRORLEVEL to zero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If the ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding the JSON compression type to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report the date, time, and ERRORLEVEL of the error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a><span data-ttu-id="ce8fb-133">新增防火牆規則</span><span class="sxs-lookup"><span data-stu-id="ce8fb-133">Add firewall rules</span></span>
<span data-ttu-id="ce8fb-134">Azure 實際上擁有兩個防火牆。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="ce8fb-135">第一道防火牆會控制虛擬機器與外界之間的連結。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-135">The first firewall controls connections between the virtual machine and the outside world.</span></span> <span data-ttu-id="ce8fb-136">此防火牆是由 [ServiceDefinition.csdef] 檔案中的 [EndPoints] 項目所控制。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-136">This firewall is controlled by the [EndPoints] element in the [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="ce8fb-137">第二道防火牆會控制虛擬機器與該虛擬機器中處理序之間的連結。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-137">The second firewall controls connections between the virtual machine and the processes within that virtual machine.</span></span> <span data-ttu-id="ce8fb-138">可以透過 `netsh advfirewall firewall` 命令列工具來控制此防火牆。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-138">This firewall can be controlled by the `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="ce8fb-139">Azure 會針對在角色內啟動的處理序建立防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-139">Azure creates firewall rules for the processes started within your roles.</span></span> <span data-ttu-id="ce8fb-140">例如，在您啟動服務或程式時，Azure 會自動建立必要的防火牆規則，藉此允許該服務與網際網路通訊。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-140">For example, when you start a service or program, Azure automatically creates the necessary firewall rules to allow that service to communicate with the Internet.</span></span> <span data-ttu-id="ce8fb-141">不過，如果您建立的服務是由角色外部的處理序啟動 (像是 COM+ 服務，或是 Windows 排程器工作)，您就必須手動建立防火牆規則以允許存取該服務。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need to manually create a firewall rule to allow access to that service.</span></span> <span data-ttu-id="ce8fb-142">您可以使用啟動工作建立這些防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="ce8fb-143">建立防火牆規則的啟動工作必須具有 [executionContext][Environment] (提高權限) 的 **executionContext**，就會執行失敗。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="ce8fb-144">將以下啟動工作加入 [ServiceDefinition.csdef] 檔案。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-144">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="ce8fb-145">若要加入防火牆規則，您必須在啟動批次檔中使用適當的 `netsh advfirewall firewall` 命令。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-145">To add the firewall rule, you must use the appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="ce8fb-146">在此範例中，啟動工作的 TCP 連接埠 80 需要具備高安全性與加密功能。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-146">In this example, the startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="ce8fb-147">封鎖特定的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="ce8fb-147">Block a specific IP address</span></span>
<span data-ttu-id="ce8fb-148">您可以透過修改 IIS **web.config** 檔來限制 Azure Web 角色只能存取一組指定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-148">You can restrict an Azure web role access to a set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="ce8fb-149">您也必須使用命令檔來解除鎖定 **ApplicationHost.config** 檔案的 **ipSecurity** 區段。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-149">You also need to use a command file which unlocks the **ipSecurity** section of the **ApplicationHost.config** file.</span></span>

<span data-ttu-id="ce8fb-150">若要解除鎖定 **ApplicationHost.config** 檔案的 **ipSecurity** 區段，請建立會在角色啟動時執行的命令檔。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-150">To do unlock the **ipSecurity** section of the **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="ce8fb-151">在 Web 角色的根層級建立名為 **startup** 的資料夾，然後在此資料夾中建立名為 **startup.cmd** 的批次檔。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-151">Create a folder at the root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="ce8fb-152">將這個檔案新增至 Visual Studio 專案，並將屬性設為 [一律複製]，以確保將它納入套件中。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-152">Add this file to your Visual Studio project and set the properties to **Copy Always** to ensure that it is included in your package.</span></span>

<span data-ttu-id="ce8fb-153">將以下啟動工作加入 [ServiceDefinition.csdef] 檔案。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-153">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="ce8fb-154">將此命令加入 **startup.cmd** 檔案:</span><span class="sxs-lookup"><span data-stu-id="ce8fb-154">Add this command to the **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="ce8fb-155">此工作可讓 **startup.cmd** 批次檔在 Web 角色每次初始化時一併執行，以確保將必要的 **ipSecurity** 區段解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-155">This task causes the **startup.cmd** batch file to be run every time the web role is initialized, ensuring that the required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="ce8fb-156">最後，修改 Web 角色 [web.config](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) 檔案中的 **system.webServer** 區段，新增具有存取權的 IP 位址清單，如以下範例所示：</span><span class="sxs-lookup"><span data-stu-id="ce8fb-156">Finally, modify the [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file to add a list of IP addresses that are granted access, as shown in the following example:</span></span>

<span data-ttu-id="ce8fb-157">此範例組態 **允許** 所有 IP 存取伺服器 (另外定義的 2 個 IP 除外)。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-157">This sample config **allows** all IPs to access the server except the two defined</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--The following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

<span data-ttu-id="ce8fb-158">此範例組態 **拒絕** 所有 IP 存取伺服器 (另外定義的 2 個 IP 除外)。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-158">This sample config **denies** all IPs from accessing the server except for the two defined.</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--The following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="ce8fb-159">建立 PowerShell 啟動工作</span><span class="sxs-lookup"><span data-stu-id="ce8fb-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="ce8fb-160">Windows PowerShell 指令碼不能從 [ServiceDefinition.csdef] 檔案直接呼叫，但可以從啟動批次檔內叫用。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-160">Windows PowerShell scripts cannot be called directly from the [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="ce8fb-161">PowerShell (依預設) 不會執行未簽署的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="ce8fb-162">除非簽署指令碼，否則需要將 PowerShell 設為執行未簽署的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-162">Unless you sign your script, you need to configure PowerShell to run unsigned scripts.</span></span> <span data-ttu-id="ce8fb-163">若要執行未簽署的指令碼，**ExecutionPolicy** 必須設為 **Unrestricted**。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-163">To run unsigned scripts, the **ExecutionPolicy** must be set to **Unrestricted**.</span></span> <span data-ttu-id="ce8fb-164">您使用的 **ExecutionPolicy** 設定需取決於 Windows PowerShell 的版本。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-164">The **ExecutionPolicy** setting that you use is based on the version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log the output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="ce8fb-165">如果您使用的客體 OS 是執行 PowerShell 2.0 或 1.0，可以強制執行第 2 版，如果無法這麼做，請改用第 1 版。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 to run, and if unavailable, use version 1.</span></span>

```cmd
REM   Attempt to set the execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set the execution policy by using the PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="ce8fb-166">透過啟動工作在本機儲存體中建立檔案</span><span class="sxs-lookup"><span data-stu-id="ce8fb-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="ce8fb-167">您可以使用本機儲存資源，儲存啟動工作所建立的檔案，以便日後供您的應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-167">You can use a local storage resource to store files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="ce8fb-168">若要建立本機儲存資源，請將 [LocalResources] 區段新增至 [ServiceDefinition.csdef] 檔案，然後新增 [LocalStorage] 子項目。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-168">To create the local storage resource, add a [LocalResources] section to the [ServiceDefinition.csdef] file and then add the [LocalStorage] child element.</span></span> <span data-ttu-id="ce8fb-169">將本機儲存體資源命名為不重複的名稱，然後為啟動工作提供適當的大小。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-169">Give the local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="ce8fb-170">若要在啟動工作中使用本機儲存體資源，您需要建立環境變數來參考本機儲存體資源的位置。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-170">To use a local storage resource in your startup task, you need to create an environment variable to reference the local storage resource location.</span></span> <span data-ttu-id="ce8fb-171">接著，啟動工作和應用程式就能對本機儲存資源讀取及寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-171">Then the startup task and the application are able to read and write files to the local storage resource.</span></span>

<span data-ttu-id="ce8fb-172">**ServiceDefinition.csdef** 檔案的相關區段如下：</span><span class="sxs-lookup"><span data-stu-id="ce8fb-172">The relevant sections of the **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="ce8fb-173">在範例中，此 **Startup.cmd** 批次檔使用 **PathToStartupStorage** 環境變數，在本機儲存體位置上建立 **MyTest.txt** 檔案。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-173">As an example, this **Startup.cmd** batch file uses the **PathToStartupStorage** environment variable to create the file **MyTest.txt** on the local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into the MyTest.txt file which will be in the    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed to by the PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO The contents of the PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit the batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="ce8fb-174">您可以使用 [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) 方法，從 Azure SDK 存取本機儲存體資料夾。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-174">You can access local storage folder from the Azure SDK by using the [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-the-emulator-or-cloud"></a><span data-ttu-id="ce8fb-175">在模擬器或雲端中執行</span><span class="sxs-lookup"><span data-stu-id="ce8fb-175">Run in the emulator or cloud</span></span>
<span data-ttu-id="ce8fb-176">當啟動工作在雲端中運作時，您可以讓啟動工作執行有別於在計算模擬器中運作時的步驟。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-176">You can have your startup task perform different steps when it is operating in the cloud compared to when it is in the compute emulator.</span></span> <span data-ttu-id="ce8fb-177">例如，在模擬器中執行時，您可能只想使用 SQL 資料的全新複本。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-177">For example, you may want to use a fresh copy of your SQL data only when running in the emulator.</span></span> <span data-ttu-id="ce8fb-178">或者，您可能想針對雲端執行一些效能最佳化作業，而這是不需要的作業。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-178">Or you may want to do some performance optimizations for the cloud that you don't need to do when running in the emulator.</span></span>

<span data-ttu-id="ce8fb-179">在 [ServiceDefinition.csdef] 檔案中建立環境變數，即可在計算模擬器和雲端上完成執行不同動作的作業。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-179">This ability to perform different actions on the compute emulator and the cloud can be accomplished by creating an environment variable in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="ce8fb-180">然後，您會在啟動工作中測試該環境變數的值。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="ce8fb-181">若要建立環境變數，請新增 [Variable]/[RoleInstanceValue] 項目，並建立值為 `/RoleEnvironment/Deployment/@emulated` 的 XPath。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-181">To create the environment variable, add the [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="ce8fb-182">在計算模擬器上執行時，**%ComputeEmulatorRunning%** 環境變數的值會是 `true`；在雲端上執行時則為 `false`。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-182">The value of the **%ComputeEmulatorRunning%** environment variable is `true` when running on the compute emulator, and `false` when running on the cloud.</span></span>

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

<span data-ttu-id="ce8fb-183">工作現在可以檢查 **%ComputeEmulatorRunning%** 環境變數，並根據角色是在雲端或模擬器中執行，而執行不同的動作。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-183">The task can now check the **%ComputeEmulatorRunning%** environment variable to perform different actions based on whether the role is running in the cloud or the emulator.</span></span> <span data-ttu-id="ce8fb-184">以下是檢查該環境變數的 .cmd 命令介面指令碼。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on the compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on the compute emulator. Perform tasks that must be run only in the compute emulator.
) ELSE (
    REM   This task is running on the cloud. Perform tasks that must be run only in the cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="ce8fb-185">偵測工作是否已在執行</span><span class="sxs-lookup"><span data-stu-id="ce8fb-185">Detect that your task has already run</span></span>
<span data-ttu-id="ce8fb-186">角色可能會未經重新開機便進行回收，導致您的啟動工作再執行一次。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-186">The role may recycle without a reboot causing your startup tasks to run again.</span></span> <span data-ttu-id="ce8fb-187">沒有標幟可指出工作是否已在裝載的 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-187">There is no flag to indicate that a task has already run on the hosting VM.</span></span> <span data-ttu-id="ce8fb-188">可能有些工作即便多次執行也沒關係。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="ce8fb-189">不過，在某些情況下，您必須避免工作執行一次以上。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-189">However, you may run into a situation where you need to prevent a task from running more than once.</span></span>

<span data-ttu-id="ce8fb-190">若要偵測工作是否已在執行，最簡單的方式，是在工作成功執行時於 **%TEMP%** 資料夾中建立檔案，並在工作開始時尋找這個檔案。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-190">The simplest way to detect that a task has already run is to create a file in the **%TEMP%** folder when the task is successful and look for it at the start of the task.</span></span> <span data-ttu-id="ce8fb-191">以下是可為您執行此作業的範例 cmd Shell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-191">Here is a sample cmd shell script that does that for you.</span></span>

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
  REM   The application installed without error. Create a file to indicate that the task
  REM   does not need to be run again.

  ECHO This line will create a file to indicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log the error and exit with the error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a><span data-ttu-id="ce8fb-192">工作最佳作法</span><span class="sxs-lookup"><span data-stu-id="ce8fb-192">Task best practices</span></span>
<span data-ttu-id="ce8fb-193">為 Web 或背景工作角色設定工作時，應該遵循的最佳作法如下。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="ce8fb-194">務必記錄啟動活動</span><span class="sxs-lookup"><span data-stu-id="ce8fb-194">Always log startup activities</span></span>
<span data-ttu-id="ce8fb-195">Visual Studio 並未提供可逐步執行批次檔的偵錯工具，因此最好盡可能取得越多批次檔作業上的資料。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-195">Visual Studio does not provide a debugger to step through batch files, so it's good to get as much data on the operation of batch files as possible.</span></span> <span data-ttu-id="ce8fb-196">記錄批次檔的輸出 (包括 **stdout** 和 **stderr**)，在您嘗試偵錯及修正批次檔時，這些資料可以提供重要資訊。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-196">Logging the output of batch files, both **stdout** and **stderr**, can give you important information when trying to debug and fix batch files.</span></span> <span data-ttu-id="ce8fb-197">若要將 **stdout** 和 **stderr** 記錄到 **%TEMP%** 環境變數所指目錄中的 StartupLog.txt 檔案，請在您想要記錄的特定行結尾加上 `>>  "%TEMP%\\StartupLog.txt" 2>&1` 文字。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-197">To log both **stdout** and **stderr** to the StartupLog.txt file in the directory pointed to by the **%TEMP%** environment variable, add the text `>>  "%TEMP%\\StartupLog.txt" 2>&1` to the end of specific lines you want to log.</span></span> <span data-ttu-id="ce8fb-198">例如，執行 **%PathToApp1Install%** 目錄中的 setup.exe 時：</span><span class="sxs-lookup"><span data-stu-id="ce8fb-198">For example, to execute setup.exe in the **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="ce8fb-199">若要簡化您的 XML，您可以建立包裝函式 *cmd* 檔案，該檔案會呼叫您的所有啟動工作與記錄，並確保每項子工作都共用相同的環境變數。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-199">To simplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares the same environment variables.</span></span>

<span data-ttu-id="ce8fb-200">不過，您可能會覺得在每個啟動工作的一端使用 `>> "%TEMP%\StartupLog.txt" 2>&1` 很麻煩。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-200">You may find it annoying though to use `>> "%TEMP%\StartupLog.txt" 2>&1` on the end of each startup task.</span></span> <span data-ttu-id="ce8fb-201">您可以建立會為您處理記錄的包裝函式，以強制執行工作記錄。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="ce8fb-202">此包裝函式會呼叫您要執行的實際批次檔。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-202">This wrapper calls the real batch file you want to run.</span></span> <span data-ttu-id="ce8fb-203">來自目標批次檔的任何輸出會被重新導向至 *Startuplog.txt* 檔案。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-203">Any output from the target batch file will be redirected to the *Startuplog.txt* file.</span></span>

<span data-ttu-id="ce8fb-204">以下範例示範如何從啟動批次檔重新導向所有的輸出。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-204">The following example shows how to redirect all output from a startup batch file.</span></span> <span data-ttu-id="ce8fb-205">在此範例中，ServerDefinition.csdef 檔案會建立啟動工作，以呼叫 *logwrap.cmd*。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-205">In this example, the ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="ce8fb-206">*logwrap.cmd* 會呼叫 *Startup2.cmd*，並將所有輸出重新導向至 **%TEMP%\\StartupLog.txt**。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output to **%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="ce8fb-207">ServiceDefinition.cmd：</span><span class="sxs-lookup"><span data-stu-id="ce8fb-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="ce8fb-208">**logwrap.cmd：**</span><span class="sxs-lookup"><span data-stu-id="ce8fb-208">**logwrap.cmd:**</span></span>

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output to the StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call the child command batch file, redirecting all output to the StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log the completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log the error.
   ECHO [%date% %time%] An error occurred. The ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

<span data-ttu-id="ce8fb-209">**Startup2.cmd：**</span><span class="sxs-lookup"><span data-stu-id="ce8fb-209">**Startup2.cmd:**</span></span>

```cmd
@ECHO OFF

REM   This is the batch file where the startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in the directory pointed to by the TEMP environment variable.

REM   If an error occurs, the following command will pass the ERRORLEVEL back to the
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

<span data-ttu-id="ce8fb-210">**StartupLog.txt** 檔案中的範例輸出：</span><span class="sxs-lookup"><span data-stu-id="ce8fb-210">Sample output in the **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="ce8fb-211">**StartupLog.txt** 檔案位於 *C:\Resources\temp\\{角色識別碼} \RoleTemp* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-211">The **StartupLog.txt** file is located in the *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="ce8fb-212">正確設定啟動工作的 executionContext</span><span class="sxs-lookup"><span data-stu-id="ce8fb-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="ce8fb-213">正確設定啟動工作的權限。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-213">Set privileges appropriately for the startup task.</span></span> <span data-ttu-id="ce8fb-214">有時候，即使角色是以正常的權限執行，啟動工作也必須以較高的權限執行。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-214">Sometimes startup tasks must run with elevated privileges even though the role runs with normal privileges.</span></span>

<span data-ttu-id="ce8fb-215">[elevated][Environment] 屬性會設定啟動工作的權限等級。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-215">The [executionContext][Task] attribute sets the privilege level of the startup task.</span></span> <span data-ttu-id="ce8fb-216">使用 `executionContext="limited"` 表示啟動工作有和角色相同的權限等級。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-216">Using `executionContext="limited"` means the startup task has the same privilege level as the role.</span></span> <span data-ttu-id="ce8fb-217">使用 `executionContext="elevated"` 表示啟動工作有系統管理員權限，您不用將系統管理員權限提供給您的角色，便可讓啟動工作執行系統管理員工作。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-217">Using `executionContext="elevated"` means the startup task has administrator privileges, which allows the startup task to perform administrator tasks without giving administrator privileges to your role.</span></span>

<span data-ttu-id="ce8fb-218">需要提高權限的啟動工作範例，是使用 **AppCmd.exe** 設定 IIS 的啟動工作。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** to configure IIS.</span></span> <span data-ttu-id="ce8fb-219">**AppCmd.exe** 需使用 `executionContext="elevated"`。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-the-appropriate-tasktype"></a><span data-ttu-id="ce8fb-220">使用正確的 taskType</span><span class="sxs-lookup"><span data-stu-id="ce8fb-220">Use the appropriate taskType</span></span>
<span data-ttu-id="ce8fb-221">[taskType][Environment] 屬性會決定執行啟動工作的方式。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-221">The [taskType][Task] attribute determines the way the startup task is executed.</span></span> <span data-ttu-id="ce8fb-222">此屬性有三個值：**simple**、**background** 和 **foreground**。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="ce8fb-223">background 和 foreground 工作會以非同步方式啟動，而 simple 工作會以同步方式執行，一次一個。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-223">The background and foreground tasks are started asynchronously, and then the simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="ce8fb-224">利用 **simple** 啟動工作後，您就可以設定工作發生的順序，亦即工作在 ServiceDefinition.csdef 檔案中列出的順序。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-224">With **simple** startup tasks, you can set the order in which the tasks run by the order in which the tasks are listed in the ServiceDefinition.csdef file.</span></span> <span data-ttu-id="ce8fb-225">如果 **simple** 工作以非零的結束代碼結束，則啟動程序會隨即停止，而角色也將不會啟動。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-225">If a **simple** task ends with a non-zero exit code, then the startup procedure stops and the role does not start.</span></span>

<span data-ttu-id="ce8fb-226">**background** 啟動工作和 **foreground** 啟動工作之間的差異，在於 **foreground** 工作會讓角色不斷執行，直到 **foreground** 工作結束為止。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-226">The difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep the role running until the **foreground** task ends.</span></span> <span data-ttu-id="ce8fb-227">換句話說，如果 **foreground** 工作停止回應或當機，那麼在 **foreground** 工作強制關閉前，都不會回收角色。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-227">This also means that if the **foreground** task hangs or crashes, the role will not recycle until the **foreground** task is forced closed.</span></span> <span data-ttu-id="ce8fb-228">基於這個理由，除非需要使用 **foreground** 工作的功能，否則建議您將 **background** 工作用於非同步的啟動工作。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of the **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="ce8fb-229">以 EXIT /B 0 結束批次檔</span><span class="sxs-lookup"><span data-stu-id="ce8fb-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="ce8fb-230">如果每個 simple 啟動工作的 **errorlevel** 是零，角色才會啟動。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-230">The role will only start if the **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="ce8fb-231">並非所有程式都會正確設定 **errorlevel** (結束代碼)，因此如果一切要正確執行，批次檔應該要以 `EXIT /B 0` 結束。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-231">Not all programs set the **errorlevel** (exit code) correctly, so the batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="ce8fb-232">啟動批次檔的結尾遺漏 `EXIT /B 0` ，是角色無法啟動的常見原因。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-232">A missing `EXIT /B 0` at the end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="ce8fb-233">我注意到使用 `/B` 參數時，巢狀批次檔有時會停滯。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-233">I've noticed that nested batch files sometimes hang when using the `/B` parameter.</span></span> <span data-ttu-id="ce8fb-234">您可能想要確定另一個批次檔呼叫目前的批次檔時，不會發生此停滯問題，就像是使用[記錄包裝函式](#always-log-startup-activities)一般。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-234">You may want to make sure that this hang problem does not happen if another batch file calls your current batch file, like if you use the [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="ce8fb-235">在此案例中，您可以省略 `/B` 參數。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-235">You can omit the `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-to-run-more-than-once"></a><span data-ttu-id="ce8fb-236">啟動工作預計會執行一次以上</span><span class="sxs-lookup"><span data-stu-id="ce8fb-236">Expect startup tasks to run more than once</span></span>
<span data-ttu-id="ce8fb-237">並非所有角色回收都會重新開機，但所有角色回收都會執行全部的啟動工作。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="ce8fb-238">換句話說，啟動工作必須能夠在重新開機之間，順利地執行多次。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-238">This means that startup tasks must be able to run multiple times between reboots without any problems.</span></span> <span data-ttu-id="ce8fb-239">這在[上一節](#detect-that-your-task-has-already-run)中討論。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-239">This is discussed in the [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-to-store-files-that-must-be-accessed-in-the-role"></a><span data-ttu-id="ce8fb-240">使用本機儲存體儲存必須在角色中存取的檔案</span><span class="sxs-lookup"><span data-stu-id="ce8fb-240">Use local storage to store files that must be accessed in the role</span></span>
<span data-ttu-id="ce8fb-241">如果您想要在啟動工作期間複製或建立檔案，然後供您的角色存取，則該檔案必須放在本機儲存體中。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-241">If you want to copy or create a file during your startup task that is then accessible to your role, then that file must be placed in local storage.</span></span> <span data-ttu-id="ce8fb-242">請參閱[上一節](#create-files-in-local-storage-from-a-startup-task)。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-242">See the [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce8fb-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ce8fb-243">Next steps</span></span>
<span data-ttu-id="ce8fb-244">檢視雲端 [服務模型和封裝](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="ce8fb-244">Review the cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="ce8fb-245">深入了解 [工作](cloud-services-startup-tasks.md) 如何運作。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="ce8fb-246">[建立和部署](cloud-services-how-to-create-deploy-portal.md) 雲端服務封裝。</span><span class="sxs-lookup"><span data-stu-id="ce8fb-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

<span data-ttu-id="ce8fb-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="ce8fb-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="ce8fb-248">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="ce8fb-248">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
<span data-ttu-id="ce8fb-249">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="ce8fb-249">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="ce8fb-250">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="ce8fb-250">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="ce8fb-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="ce8fb-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
<span data-ttu-id="ce8fb-252">[EndPoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span><span class="sxs-lookup"><span data-stu-id="ce8fb-252">[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span></span>
<span data-ttu-id="ce8fb-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span><span class="sxs-lookup"><span data-stu-id="ce8fb-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span></span>
<span data-ttu-id="ce8fb-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span><span class="sxs-lookup"><span data-stu-id="ce8fb-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span></span>
<span data-ttu-id="ce8fb-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="ce8fb-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
