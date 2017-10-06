---
title: "在 Azure 雲端服務的啟動工作 aaaRun |Microsoft 文件"
description: "啟動工作可協助您為應用程式備妥雲端服務環境。 這會告訴您如何啟動工作的工作以及如何 toomake 它們"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="de202-104">影響 tooconfigure] 和 [執行啟動工作的雲端服務</span><span class="sxs-lookup"><span data-stu-id="de202-104">How tooconfigure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="de202-105">在角色啟動之前，您可以使用啟動工作 tooperform 作業。</span><span class="sxs-lookup"><span data-stu-id="de202-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="de202-106">您可能想 tooperform 的作業包括安裝元件、 註冊 COM 元件、 設定登錄機碼，或啟動長時間執行的處理程序。</span><span class="sxs-lookup"><span data-stu-id="de202-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="de202-107">不適用 tooVirtual 機器，只有 tooCloud 服務 Web 和背景工作角色啟動工作。</span><span class="sxs-lookup"><span data-stu-id="de202-107">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="de202-108">啟動工作的運作方式</span><span class="sxs-lookup"><span data-stu-id="de202-108">How startup tasks work</span></span>
<span data-ttu-id="de202-109">啟動工作是您的角色開始，且已定義在 hello 之前採取的動作[ServiceDefinition.csdef]檔案使用 hello[工作]hello 內的項目[啟動]項目。</span><span class="sxs-lookup"><span data-stu-id="de202-109">Startup tasks are actions that are taken before your roles begin and are defined in hello [ServiceDefinition.csdef] file by using hello [Task] element within hello [Startup] element.</span></span> <span data-ttu-id="de202-110">啟動工作經常是批次檔，但也可以是主控台應用程式，或是啟動 PowerShell 指令碼的批次檔。</span><span class="sxs-lookup"><span data-stu-id="de202-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="de202-111">環境變數會將資訊傳入啟動工作，並本機儲存體可以是使用的 toopass 從啟動工作的資訊。</span><span class="sxs-lookup"><span data-stu-id="de202-111">Environment variables pass information into a startup task, and local storage can be used toopass information out of a startup task.</span></span> <span data-ttu-id="de202-112">例如，環境變數可以指定 hello 路徑 tooa 程式您想 tooinstall，而且可以讀取稍後供您的角色的 toolocal 儲存體可以寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="de202-112">For example, an environment variable can specify hello path tooa program you want tooinstall, and files can be written toolocal storage that can then be read later by your roles.</span></span>

<span data-ttu-id="de202-113">啟動工作可以將資訊和 hello 所指定的錯誤 toohello 目錄記錄**TEMP**環境變數。</span><span class="sxs-lookup"><span data-stu-id="de202-113">Your startup task can log information and errors toohello directory specified by hello **TEMP** environment variable.</span></span> <span data-ttu-id="de202-114">Hello 啟動工作，期間 hello **TEMP**環境變數會解析 toohello *c:\\資源\\temp\\[guid]。 [rolename]\\RoleTemp* hello 雲端上執行時的目錄。</span><span class="sxs-lookup"><span data-stu-id="de202-114">During hello startup task, hello **TEMP** environment variable resolves toohello *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on hello cloud.</span></span>

<span data-ttu-id="de202-115">啟動工作也可以在重新開機之間執行數次。</span><span class="sxs-lookup"><span data-stu-id="de202-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="de202-116">例如，hello 角色回收時，每次將執行 hello 啟動工作，而角色回收不一定都包括重新開機。</span><span class="sxs-lookup"><span data-stu-id="de202-116">For example, hello startup task will be run each time hello role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="de202-117">啟動工作應該寫入外面 toorun 數次不會有問題的方式。</span><span class="sxs-lookup"><span data-stu-id="de202-117">Startup tasks should be written in a way that allows them toorun several times without problems.</span></span>

<span data-ttu-id="de202-118">啟動工作的結尾必須**errorlevel** （或結束代碼） 為 hello 啟動處理序 toocomplete 零。</span><span class="sxs-lookup"><span data-stu-id="de202-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for hello startup process toocomplete.</span></span> <span data-ttu-id="de202-119">如果啟動工作結束非零值**errorlevel**，hello 角色將不會啟動。</span><span class="sxs-lookup"><span data-stu-id="de202-119">If a startup task ends with a non-zero **errorlevel**, hello role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="de202-120">角色啟動順序</span><span class="sxs-lookup"><span data-stu-id="de202-120">Role startup order</span></span>
<span data-ttu-id="de202-121">hello 以下列出 Azure 中的 hello 角色啟動程序：</span><span class="sxs-lookup"><span data-stu-id="de202-121">hello following lists hello role startup procedure in Azure:</span></span>

1. <span data-ttu-id="de202-122">hello 執行個體標示為**起始**而且不會接收流量。</span><span class="sxs-lookup"><span data-stu-id="de202-122">hello instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="de202-123">所有啟動工作會都執行根據 tootheir **taskType**屬性。</span><span class="sxs-lookup"><span data-stu-id="de202-123">All startup tasks are executed according tootheir **taskType** attribute.</span></span>
   
   * <span data-ttu-id="de202-124">hello**簡單**工作會以同步方式，執行一次。</span><span class="sxs-lookup"><span data-stu-id="de202-124">hello **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="de202-125">hello**背景**和**前景**工作會以非同步方式啟動的平行 toohello 啟動工作。</span><span class="sxs-lookup"><span data-stu-id="de202-125">hello **background** and **foreground** tasks are started asynchronously, parallel toohello startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="de202-126">IIS 可能未完全設定在 hello 啟動處理序中的 hello 啟動工作階段期間讓角色專屬的資料可能無法使用。</span><span class="sxs-lookup"><span data-stu-id="de202-126">IIS may not be fully configured during hello startup task stage in hello startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="de202-127">需要特定角色資料的啟動工作應該使用 [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx)。</span><span class="sxs-lookup"><span data-stu-id="de202-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="de202-128">hello 角色主機處理序會啟動，且在 IIS 中建立 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="de202-128">hello role host process is started and hello site is created in IIS.</span></span>
4. <span data-ttu-id="de202-129">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx)方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="de202-129">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="de202-130">hello 執行個體標示為**準備**並且流量會路由的 toohello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="de202-130">hello instance is marked as **Ready** and traffic is routed toohello instance.</span></span>
6. <span data-ttu-id="de202-131">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="de202-131">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="de202-132">啟動工作範例</span><span class="sxs-lookup"><span data-stu-id="de202-132">Example of a startup task</span></span>
<span data-ttu-id="de202-133">啟動工作定義在 hello [ServiceDefinition.csdef]檔案，請在 hello**工作**項目。</span><span class="sxs-lookup"><span data-stu-id="de202-133">Startup tasks are defined in hello [ServiceDefinition.csdef] file, in hello **Task** element.</span></span> <span data-ttu-id="de202-134">hello **commandLine**屬性會指定 hello 名稱和參數的 hello 啟動批次檔案或主控台命令，hello **executionContext**屬性會指定 hello hello 啟動權限層級工作及 hello **taskType**屬性會指定 hello 工作執行的方式。</span><span class="sxs-lookup"><span data-stu-id="de202-134">hello **commandLine** attribute specifies hello name and parameters of hello startup batch file or console command, hello **executionContext** attribute specifies hello privilege level of hello startup task, and hello **taskType** attribute specifies how hello task will be executed.</span></span>

<span data-ttu-id="de202-135">在此範例中，環境變數， **MyVersionNumber**為 hello 啟動工作建立並設定 toohello 值、 「**1.0.0.0**"。</span><span class="sxs-lookup"><span data-stu-id="de202-135">In this example, an environment variable, **MyVersionNumber**, is created for hello startup task and set toohello value "**1.0.0.0**".</span></span>

<span data-ttu-id="de202-136">**ServiceDefinition.csdef**：</span><span class="sxs-lookup"><span data-stu-id="de202-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="de202-137">在下列範例的 hello，hello **Startup.cmd**批次檔會將 hello 行"hello 新版 is 1.0.0.0"toohello StartupLog.txt 檔案寫入 hello hello TEMP 環境變數所指定的目錄中。</span><span class="sxs-lookup"><span data-stu-id="de202-137">In hello following example, hello **Startup.cmd** batch file writes hello line "hello current version is 1.0.0.0" toohello StartupLog.txt file in hello directory specified by hello TEMP environment variable.</span></span> <span data-ttu-id="de202-138">hello`EXIT /B 0`行將確保該 hello 的啟動工作以**errorlevel**為零。</span><span class="sxs-lookup"><span data-stu-id="de202-138">hello `EXIT /B 0` line ensures that hello startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="de202-139">在 Visual Studio 中的 hello**複製 tooOutput 目錄**啟動批次檔的屬性應該設定太**永遠複製**toobe 確定啟動批次檔是否正確部署在 Azure 上的 tooyour 專案(**approot\\bin** Web 角色和**approot**背景工作角色)。</span><span class="sxs-lookup"><span data-stu-id="de202-139">In Visual Studio, hello **Copy tooOutput Directory** property for your startup batch file should be set too**Copy Always** toobe sure that your startup batch file is properly deployed tooyour project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="de202-140">工作屬性說明</span><span class="sxs-lookup"><span data-stu-id="de202-140">Description of task attributes</span></span>
<span data-ttu-id="de202-141">hello 以下描述的 hello hello 屬性**工作**hello 中的項目[ServiceDefinition.csdef]檔案：</span><span class="sxs-lookup"><span data-stu-id="de202-141">hello following describes hello attributes of hello **Task** element in hello [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="de202-142">**commandLine** -指定 hello hello 啟動工作的命令列：</span><span class="sxs-lookup"><span data-stu-id="de202-142">**commandLine** - Specifies hello command line for hello startup task:</span></span>

* <span data-ttu-id="de202-143">hello 命令，以選擇性的命令列參數開始 hello 啟動工作。</span><span class="sxs-lookup"><span data-stu-id="de202-143">hello command, with optional command line parameters, which begins hello startup task.</span></span>
* <span data-ttu-id="de202-144">這通常是.cmd 或.bat 批次檔的 hello 檔名。</span><span class="sxs-lookup"><span data-stu-id="de202-144">Frequently this is hello filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="de202-145">hello 工作是相對 toohello AppRoot\\hello 部署的 Bin 資料夾。</span><span class="sxs-lookup"><span data-stu-id="de202-145">hello task is relative toohello AppRoot\\Bin folder for hello deployment.</span></span> <span data-ttu-id="de202-146">在決定 hello 路徑和檔案的 hello 工作，不會展開環境變數。</span><span class="sxs-lookup"><span data-stu-id="de202-146">Environment variables are not expanded in determining hello path and file of hello task.</span></span> <span data-ttu-id="de202-147">如果需要展開環境變數，可以建立小型 .cmd 指令碼，藉以呼叫啟動工作。</span><span class="sxs-lookup"><span data-stu-id="de202-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="de202-148">可以是主控台應用程式，或啟動 [PowerShell 指令碼](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task)的批次檔。</span><span class="sxs-lookup"><span data-stu-id="de202-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="de202-149">**executionContext** -指定 hello hello 啟動工作的權限層級。</span><span class="sxs-lookup"><span data-stu-id="de202-149">**executionContext** - Specifies hello privilege level for hello startup task.</span></span> <span data-ttu-id="de202-150">hello 權限層級可以限制或提高權限：</span><span class="sxs-lookup"><span data-stu-id="de202-150">hello privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="de202-151">**limited**</span><span class="sxs-lookup"><span data-stu-id="de202-151">**limited**</span></span>  
  <span data-ttu-id="de202-152">hello 啟動工作執行與 hello 相同 hello 角色權限。</span><span class="sxs-lookup"><span data-stu-id="de202-152">hello startup task runs with hello same privileges as hello role.</span></span> <span data-ttu-id="de202-153">當 hello **executionContext**屬性 hello[執行階段]項目也是**有限**，則會使用使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="de202-153">When hello **executionContext** attribute for hello [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="de202-154">**elevated**</span><span class="sxs-lookup"><span data-stu-id="de202-154">**elevated**</span></span>  
  <span data-ttu-id="de202-155">hello 啟動工作執行系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="de202-155">hello startup task runs with administrator privileges.</span></span> <span data-ttu-id="de202-156">這可讓啟動工作 tooinstall 程式、 進行 IIS 組態變更、 執行登錄變更，以及其他系統管理員層級工作，而不會增加權限層級 hello hello 角色本身。</span><span class="sxs-lookup"><span data-stu-id="de202-156">This allows startup tasks tooinstall programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing hello privilege level of hello role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="de202-157">hello 的啟動工作的權限層級不需要 toobe hello 相同 hello 角色本身。</span><span class="sxs-lookup"><span data-stu-id="de202-157">hello privilege level of a startup task does not need toobe hello same as hello role itself.</span></span>
> 
> 

<span data-ttu-id="de202-158">**taskType** -指定要執行 hello 方式啟動工作。</span><span class="sxs-lookup"><span data-stu-id="de202-158">**taskType** - Specifies hello way a startup task is executed.</span></span>

* <span data-ttu-id="de202-159">**simple**</span><span class="sxs-lookup"><span data-stu-id="de202-159">**simple**</span></span>  
  <span data-ttu-id="de202-160">執行工作時同步執行，一次一個，hello 順序 hello 中指定[ServiceDefinition.csdef]檔案。</span><span class="sxs-lookup"><span data-stu-id="de202-160">Tasks are executed synchronously, one at a time, in hello order specified in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="de202-161">當一**簡單**啟動工作以**errorlevel**為零，hello 接下來**簡單**啟動工作的執行。</span><span class="sxs-lookup"><span data-stu-id="de202-161">When one **simple** startup task ends with an **errorlevel** of zero, hello next **simple** startup task is executed.</span></span> <span data-ttu-id="de202-162">如果已無其他**簡單**啟動工作 tooexecute，然後將啟動 hello 角色本身。</span><span class="sxs-lookup"><span data-stu-id="de202-162">If there are no more **simple** startup tasks tooexecute, then hello role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="de202-163">如果 hello**簡單**非零值結束工作**errorlevel**，hello 執行個體將會被封鎖。</span><span class="sxs-lookup"><span data-stu-id="de202-163">If hello **simple** task ends with a non-zero **errorlevel**, hello instance will be blocked.</span></span> <span data-ttu-id="de202-164">後續**簡單**啟動工作和 hello 角色本身，將不會啟動。</span><span class="sxs-lookup"><span data-stu-id="de202-164">Subsequent **simple** startup tasks, and hello role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="de202-165">批次檔結尾的 tooensure **errorlevel**為零，執行 hello 命令`EXIT /B 0`hello 批次的檔案處理序的結尾處。</span><span class="sxs-lookup"><span data-stu-id="de202-165">tooensure that your batch file ends with an **errorlevel** of zero, execute hello command `EXIT /B 0` at hello end of your batch file process.</span></span>
* <span data-ttu-id="de202-166">**background**</span><span class="sxs-lookup"><span data-stu-id="de202-166">**background**</span></span>  
  <span data-ttu-id="de202-167">以非同步方式執行工作與 hello hello 角色啟動並行。</span><span class="sxs-lookup"><span data-stu-id="de202-167">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span>
* <span data-ttu-id="de202-168">**foreground**</span><span class="sxs-lookup"><span data-stu-id="de202-168">**foreground**</span></span>  
  <span data-ttu-id="de202-169">以非同步方式執行工作與 hello hello 角色啟動並行。</span><span class="sxs-lookup"><span data-stu-id="de202-169">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span> <span data-ttu-id="de202-170">hello 之間的主要差異**前景**和**背景**工作是**前景**工作會導致 hello 角色回收或直到 hello 工作已關閉結束。</span><span class="sxs-lookup"><span data-stu-id="de202-170">hello key difference between a **foreground** and a **background** task is that a **foreground** task prevents hello role from recycling or shutting down until hello task has ended.</span></span> <span data-ttu-id="de202-171">hello**背景**工作沒有這項限制。</span><span class="sxs-lookup"><span data-stu-id="de202-171">hello **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="de202-172">環境變數</span><span class="sxs-lookup"><span data-stu-id="de202-172">Environment variables</span></span>
<span data-ttu-id="de202-173">環境變數是方式 toopass 資訊 tooa 啟動工作。</span><span class="sxs-lookup"><span data-stu-id="de202-173">Environment variables are a way toopass information tooa startup task.</span></span> <span data-ttu-id="de202-174">例如，您可以放入 hello 路徑 tooa blob，其中包含程式 tooinstall，或連接埠號碼，將使用您的角色或啟動工作設定 toocontrol 功能。</span><span class="sxs-lookup"><span data-stu-id="de202-174">For example, you can put hello path tooa blob that contains a program tooinstall, or port numbers that your role will use, or settings toocontrol features of your startup task.</span></span>

<span data-ttu-id="de202-175">有兩種類型的啟動工作; 的環境變數靜態環境變數和環境變數根據成員的 hello [RoleEnvironment]類別。</span><span class="sxs-lookup"><span data-stu-id="de202-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="de202-176">兩者都是在 hello[環境]區段 hello [ServiceDefinition.csdef]檔案，以及這兩個使用 hello[變數]項目和**名稱**屬性。</span><span class="sxs-lookup"><span data-stu-id="de202-176">Both are in hello [Environment] section of hello [ServiceDefinition.csdef] file, and both use hello [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="de202-177">靜態環境變數使用 hello**值**屬性 hello[變數]項目。</span><span class="sxs-lookup"><span data-stu-id="de202-177">Static environment variables uses hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="de202-178">上述的 hello 範例會建立 hello 環境變數**MyVersionNumber**具有靜態值為"**1.0.0.0**"。</span><span class="sxs-lookup"><span data-stu-id="de202-178">hello example above creates hello environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="de202-179">另一個範例就是 toocreate **StagingOrProduction**環境變數，您可以手動設定的 toovalues"**暫存**「 或 」**生產**"tooperform不同的啟動動作為基礎的 hello hello 值**StagingOrProduction**環境變數。</span><span class="sxs-lookup"><span data-stu-id="de202-179">Another example would be toocreate a **StagingOrProduction** environment variable which you can manually set toovalues of "**staging**" or "**production**" tooperform different startup actions based on hello value of hello **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="de202-180">依據的 hello RoleEnvironment 類別成員的環境變數不會使用 hello**值**屬性 hello[變數]項目。</span><span class="sxs-lookup"><span data-stu-id="de202-180">Environment variables based on members of hello RoleEnvironment class do not use hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="de202-181">相反地，hello [RoleInstanceValue]子項目，以適當的 hello **XPath**屬性值，根據 hello 的特定成員的環境變數會使用的 toocreate [RoleEnvironment]類別。</span><span class="sxs-lookup"><span data-stu-id="de202-181">Instead, hello [RoleInstanceValue] child element, with hello appropriate **XPath** attribute value, are used toocreate an environment variable based on a specific member of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="de202-182">值為 hello **XPath**各種屬性 tooaccess [RoleEnvironment]可以找到值[這裡](cloud-services-role-config-xpath.md)。</span><span class="sxs-lookup"><span data-stu-id="de202-182">Values for hello **XPath** attribute tooaccess various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="de202-183">比方說，toocreate 是環境變數"**true**"hello 執行個體在 hello 計算模擬器中，執行時和"**false**"hello 雲端中執行時，使用 hello 下列[變數]和[RoleInstanceValue]項目：</span><span class="sxs-lookup"><span data-stu-id="de202-183">For example, toocreate an environment variable that is "**true**" when hello instance is running in hello compute emulator, and "**false**" when running in hello cloud, use hello following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="de202-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="de202-184">Next steps</span></span>
<span data-ttu-id="de202-185">深入了解如何 tooperform 某些[常見的啟動工作](cloud-services-startup-tasks-common.md)與雲端服務。</span><span class="sxs-lookup"><span data-stu-id="de202-185">Learn how tooperform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="de202-186">[封裝](cloud-services-model-and-package.md) 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="de202-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[工作]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[啟動]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[執行階段]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[環境]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[變數]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
