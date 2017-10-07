---
title: "有關 Azure microservices 安全性原則 aaaLearn |Microsoft 文件"
description: "了解如何 toorun 系統與本機安全性帳戶 下的 Service Fabric 應用程式，包括應用程式需要 tooperform 一些 hello SetupEntry 點特殊權限動作開始之前"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="06ce2-103">設定應用程式的安全性原則</span><span class="sxs-lookup"><span data-stu-id="06ce2-103">Configure security policies for your application</span></span>
<span data-ttu-id="06ce2-104">藉由使用 Azure Service Fabric，您可以保護在 hello 叢集中不同的使用者帳戶下執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="06ce2-104">By using Azure Service Fabric, you can secure applications that are running in hello cluster under different user accounts.</span></span> <span data-ttu-id="06ce2-105">Service Fabric 也有助於安全 hello 資源所使用的應用程式中的 hello 使用者帳戶-部署的 hello 時段，例如、 檔案、 目錄和憑證。</span><span class="sxs-lookup"><span data-stu-id="06ce2-105">Service Fabric also helps secure hello resources that are used by applications at hello time of deployment under hello user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="06ce2-106">如此一來，即使在共用主控環境中，執行中的應用程式就不會彼此干擾。</span><span class="sxs-lookup"><span data-stu-id="06ce2-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="06ce2-107">根據預設，Service Fabric 應用程式是 hello hello Fabric.exe 程序執行的帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="06ce2-107">By default, Service Fabric applications run under hello account that hello Fabric.exe process runs under.</span></span> <span data-ttu-id="06ce2-108">Service Fabric 還提供 hello 功能 toorun 本機使用者帳戶或本機系統帳戶，hello 應用程式資訊清單內所指定的應用程式。</span><span class="sxs-lookup"><span data-stu-id="06ce2-108">Service Fabric also provides hello capability toorun applications under a local user account or local system account, which is specified within hello application manifest.</span></span> <span data-ttu-id="06ce2-109">支援的本機系統帳戶類型為 **LocalUser**、**NetworkService**、**LocalService** 和 **LocalSystem**。</span><span class="sxs-lookup"><span data-stu-id="06ce2-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="06ce2-110">如果您執行 Service Fabric Windows 伺服器上資料中心內使用 hello 獨立安裝程式，您可以使用 Active Directory 網域帳戶，包括群組受管理的服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="06ce2-110">When you're running Service Fabric on Windows Server in your datacenter by using hello standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="06ce2-111">您可以定義和建立使用者群組，以便新增一或多個使用者 tooeach 群組 toobe 一起管理。</span><span class="sxs-lookup"><span data-stu-id="06ce2-111">You can define and create user groups so that one or more users can be added tooeach group toobe managed together.</span></span> <span data-ttu-id="06ce2-112">有多個不同的服務進入點的使用者，且需要 toohave hello 群組層級的特定一般權限時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="06ce2-112">This is useful when there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span>

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="06ce2-113">設定服務安裝程式的進入點的 hello 原則</span><span class="sxs-lookup"><span data-stu-id="06ce2-113">Configure hello policy for a service setup entry point</span></span>
<span data-ttu-id="06ce2-114">Hello 中所述[應用程式模型](service-fabric-application-model.md)，hello 安裝進入點， **SetupEntryPoint**，是以 hello 相同認證為 Service Fabric 執行特殊權限的進入點 (通常 hello *NetworkService*帳戶) 之前的任何其他的進入點。</span><span class="sxs-lookup"><span data-stu-id="06ce2-114">As described in hello [application model](service-fabric-application-model.md), hello setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="06ce2-115">hello 可執行檔所指定**EntryPoint**通常是 hello 長時間執行的服務主機。</span><span class="sxs-lookup"><span data-stu-id="06ce2-115">hello executable that is specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="06ce2-116">因此需要個別安裝程式的進入點，可避免 toorun hello 服務主機以高的權限可執行需要很長的時間。</span><span class="sxs-lookup"><span data-stu-id="06ce2-116">So having a separate setup entry point avoids having toorun hello service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="06ce2-117">hello 可執行檔的**EntryPoint**指定執行**SetupEntryPoint**成功結束。</span><span class="sxs-lookup"><span data-stu-id="06ce2-117">hello executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="06ce2-118">hello 產生處理序監視，並重新啟動，並重新開始**SetupEntryPoint**如果曾結束，或當機。</span><span class="sxs-lookup"><span data-stu-id="06ce2-118">hello resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="06ce2-119">hello 以下是簡單的服務資訊清單並的範例，顯示 hello SetupEntryPoint hello hello 服務的主要進入點。</span><span class="sxs-lookup"><span data-stu-id="06ce2-119">hello following is a simple service manifest example that shows hello SetupEntryPoint and hello main EntryPoint for hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a><span data-ttu-id="06ce2-120">使用本機帳戶設定 hello 原則</span><span class="sxs-lookup"><span data-stu-id="06ce2-120">Configure hello policy by using a local account</span></span>
<span data-ttu-id="06ce2-121">設定 hello 服務 toohave 安裝進入點之後，您可以變更下執行 hello 應用程式資訊清單中的 hello 安全性權限。</span><span class="sxs-lookup"><span data-stu-id="06ce2-121">After you configure hello service toohave a setup entry point, you can change hello security permissions that it runs under in hello application manifest.</span></span> <span data-ttu-id="06ce2-122">hello 下列範例顯示如何 tooconfigure hello 服務 toorun 使用者系統管理員帳戶權限。</span><span class="sxs-lookup"><span data-stu-id="06ce2-122">hello following example shows how tooconfigure hello service toorun under user administrator account privileges.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

<span data-ttu-id="06ce2-123">首先，以使用者名稱 (例如 SetupAdminUser) 建立 **Principals** 區段。</span><span class="sxs-lookup"><span data-stu-id="06ce2-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="06ce2-124">這表示該 hello 使用者 hello Administrators 群組成員的系統。</span><span class="sxs-lookup"><span data-stu-id="06ce2-124">This indicates that hello user is a member of hello Administrators system group.</span></span>

<span data-ttu-id="06ce2-125">下一步 在 hello **ServiceManifestImport**區段中，設定原則 tooapply 這個主體太**SetupEntryPoint**。</span><span class="sxs-lookup"><span data-stu-id="06ce2-125">Next, under hello **ServiceManifestImport** section, configure a policy tooapply this principal too**SetupEntryPoint**.</span></span> <span data-ttu-id="06ce2-126">這會告知 Service Fabric，當 hello **MySetup.bat**執行檔，應該是`RunAs`系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="06ce2-126">This tells Service Fabric that when hello **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="06ce2-127">假設您有*不*套用原則 toohello 主要進入點、 hello 中的程式碼**MyServiceHost.exe** hello 系統下執行**NetworkService**帳戶。</span><span class="sxs-lookup"><span data-stu-id="06ce2-127">Given that you have *not* applied a policy toohello main entry point, hello code in **MyServiceHost.exe** runs under hello system **NetworkService** account.</span></span> <span data-ttu-id="06ce2-128">這是服務的所有進入點都執行身分的 hello 預設帳戶。</span><span class="sxs-lookup"><span data-stu-id="06ce2-128">This is hello default account that all service entry points are run as.</span></span>

<span data-ttu-id="06ce2-129">讓我們現在加入 hello 檔案 MySetup.bat toohello Visual Studio 專案 tootest hello 系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="06ce2-129">Let's now add hello file MySetup.bat toohello Visual Studio project tootest hello administrator privileges.</span></span> <span data-ttu-id="06ce2-130">在 Visual Studio 中，hello 服務專案上按一下滑鼠右鍵並加入新的檔案，稱為 MySetup.bat。</span><span class="sxs-lookup"><span data-stu-id="06ce2-130">In Visual Studio, right-click hello service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="06ce2-131">接下來，確定 hello 服務封裝中包含該 hello MySetup.bat 檔案。</span><span class="sxs-lookup"><span data-stu-id="06ce2-131">Next, ensure that hello MySetup.bat file is included in hello service package.</span></span> <span data-ttu-id="06ce2-132">預設不會包含該檔案。</span><span class="sxs-lookup"><span data-stu-id="06ce2-132">By default, it is not.</span></span> <span data-ttu-id="06ce2-133">選取 hello 檔案，以滑鼠右鍵按一下 tooget hello 操作功能表，然後選擇 **屬性**。</span><span class="sxs-lookup"><span data-stu-id="06ce2-133">Select hello file, right-click tooget hello context menu, and choose **Properties**.</span></span> <span data-ttu-id="06ce2-134">在 hello 內容 對話方塊中，確定**複製 tooOutput 目錄**設定得**更新時才複製**。</span><span class="sxs-lookup"><span data-stu-id="06ce2-134">In hello Properties dialog box, ensure that **Copy tooOutput Directory** is set too**Copy if newer**.</span></span> <span data-ttu-id="06ce2-135">請參閱下列螢幕擷取畫面的 hello。</span><span class="sxs-lookup"><span data-stu-id="06ce2-135">See hello following screenshot.</span></span>

![Visual Studio CopyToOutput for SetupEntryPoint 批次檔][image1]

<span data-ttu-id="06ce2-137">現在開啟 hello MySetup.bat 檔案，並加入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="06ce2-137">Now open hello MySetup.bat file and add hello following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="06ce2-138">接下來，建置和部署 hello 方案 tooa 本機開發叢集。</span><span class="sxs-lookup"><span data-stu-id="06ce2-138">Next, build and deploy hello solution tooa local development cluster.</span></span> <span data-ttu-id="06ce2-139">Hello 服務已啟動，Service Fabric 總管中所示之後，您可以看到該 hello MySetup.bat 檔案已成功在兩種方式。</span><span class="sxs-lookup"><span data-stu-id="06ce2-139">After hello service has started, as shown in Service Fabric Explorer, you can see that hello MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="06ce2-140">開啟 PowerShell 命令提示字元並輸入：</span><span class="sxs-lookup"><span data-stu-id="06ce2-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="06ce2-141">然後，請注意 hello 節點名稱的 hello hello 服務部署，而在啟動 Service Fabric 總管-例如，節點 2。</span><span class="sxs-lookup"><span data-stu-id="06ce2-141">Then, note hello name of hello node where hello service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="06ce2-142">接下來，瀏覽 toohello 應用程式執行個體的工作資料夾 toofind hello out.txt 檔案會顯示 hello 值**TestVariable**。</span><span class="sxs-lookup"><span data-stu-id="06ce2-142">Next, navigate toohello application instance work folder toofind hello out.txt file that shows hello value of **TestVariable**.</span></span> <span data-ttu-id="06ce2-143">例如，如果此服務已部署的 tooNode 2，接著您可以移 hello toothis 路徑**MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="06ce2-143">For example, if this service was deployed tooNode 2, then you can go toothis path for hello **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a><span data-ttu-id="06ce2-144">使用本機系統帳戶來設定 hello 原則</span><span class="sxs-lookup"><span data-stu-id="06ce2-144">Configure hello policy by using local system accounts</span></span>
<span data-ttu-id="06ce2-145">通常，它會使用本機系統帳戶，而不是系統管理員帳戶是最好的 toorun hello 啟動指令碼。</span><span class="sxs-lookup"><span data-stu-id="06ce2-145">Often, it's preferable toorun hello startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="06ce2-146">Hello Administrators 群組通常無法運作良好，因為電腦有使用者存取控制 (UAC) 預設啟用的成員身分執行 hello RunAs 原則。</span><span class="sxs-lookup"><span data-stu-id="06ce2-146">Running hello RunAs policy as a member of hello Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="06ce2-147">在這種情況下， **hello 建議 toorun hello SetupEntryPoint 以 localsystem 身分，而不是以本機使用者新增的 tooAdministrators 群組**。</span><span class="sxs-lookup"><span data-stu-id="06ce2-147">In such cases, **hello recommendation is toorun hello SetupEntryPoint as LocalSystem, instead of as a local user added tooAdministrators group**.</span></span> <span data-ttu-id="06ce2-148">hello 下列範例示範設定 hello SetupEntryPoint toorun 以 localsystem 身分：</span><span class="sxs-lookup"><span data-stu-id="06ce2-148">hello following example shows setting hello SetupEntryPoint toorun as LocalSystem:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="06ce2-149">從安裝程式進入點啟動 PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="06ce2-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="06ce2-150">從 hello toorun PowerShell **SetupEntryPoint**點，您可以執行**PowerShell.exe**點 tooa PowerShell 批次檔中的檔案。</span><span class="sxs-lookup"><span data-stu-id="06ce2-150">toorun PowerShell from hello **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points tooa PowerShell file.</span></span> <span data-ttu-id="06ce2-151">首先，比方說，新增 PowerShell 檔案 toohello 服務專案- **MySetup.ps1**。</span><span class="sxs-lookup"><span data-stu-id="06ce2-151">First, add a PowerShell file toohello service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="06ce2-152">請記住 tooset hello*更新時才複製*因此 hello 檔案也包含 hello 服務封裝中的屬性。</span><span class="sxs-lookup"><span data-stu-id="06ce2-152">Remember tooset hello *Copy if newer* property so that hello file is also included in hello service package.</span></span> <span data-ttu-id="06ce2-153">hello 下列範例示範的範例批次檔啟動 PowerShell 檔案呼叫 MySetup.ps1，設定系統環境變數，呼叫**TestVariable**。</span><span class="sxs-lookup"><span data-stu-id="06ce2-153">hello following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="06ce2-154">MySetup.bat toostart PowerShell 檔案：</span><span class="sxs-lookup"><span data-stu-id="06ce2-154">MySetup.bat toostart a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="06ce2-155">在 hello PowerShell 檔案中，加入下列 tooset 系統環境變數的 hello:</span><span class="sxs-lookup"><span data-stu-id="06ce2-155">In hello PowerShell file, add hello following tooset a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="06ce2-156">根據預設，當 hello 批次檔執行時，它會查看 hello 應用程式資料夾，稱為**運作**檔案。</span><span class="sxs-lookup"><span data-stu-id="06ce2-156">By default, when hello batch file runs, it looks at hello application folder called **work** for files.</span></span> <span data-ttu-id="06ce2-157">在此情況下，當 MySetup.bat 執行時，我們想要這個 toofind hello MySetup.ps1 檔案 hello 中相同資料夾中，也就是 hello 應用程式**程式碼封裝**資料夾。</span><span class="sxs-lookup"><span data-stu-id="06ce2-157">In this case, when MySetup.bat runs, we want this toofind hello MySetup.ps1 file in hello same folder, which is hello application **code package** folder.</span></span> <span data-ttu-id="06ce2-158">toochange 這個資料夾、 組 hello 工作資料夾：</span><span class="sxs-lookup"><span data-stu-id="06ce2-158">toochange this folder, set hello working folder:</span></span>
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="06ce2-159">使用主控台重新導向進行本機偵錯</span><span class="sxs-lookup"><span data-stu-id="06ce2-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="06ce2-160">有時候，它會從執行的指令碼進行偵錯的有用 toosee hello 主控台輸出。</span><span class="sxs-lookup"><span data-stu-id="06ce2-160">Occasionally, it's useful toosee hello console output from running a script for debugging purposes.</span></span> <span data-ttu-id="06ce2-161">toodo，您可以設定將 hello 輸出 tooa 檔案寫入主控台重新導向原則。</span><span class="sxs-lookup"><span data-stu-id="06ce2-161">toodo this, you can set a console redirection policy, which writes hello output tooa file.</span></span> <span data-ttu-id="06ce2-162">hello 檔案輸出寫入的 toohello 應用程式資料夾稱為**記錄**其中 hello 應用程式是部署而執行的 hello 節點上。</span><span class="sxs-lookup"><span data-stu-id="06ce2-162">hello file output is written toohello application folder called **log** on hello node where hello application is deployed and run.</span></span> <span data-ttu-id="06ce2-163">(請參閱 where toofind 這 hello 前面範例中。)</span><span class="sxs-lookup"><span data-stu-id="06ce2-163">(See where toofind this in hello preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="06ce2-164">絕對不要使用的應用程式，因為這可能會影響 hello 應用程式容錯移轉，在生產環境中部署的 hello 主控台重新導向原則。</span><span class="sxs-lookup"><span data-stu-id="06ce2-164">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="06ce2-165">僅將此原則用於本機開發及偵錯。</span><span class="sxs-lookup"><span data-stu-id="06ce2-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="06ce2-166">hello 下列範例示範設定 hello 主控台重新導向 FileRetentionCount 值：</span><span class="sxs-lookup"><span data-stu-id="06ce2-166">hello following example shows setting hello console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="06ce2-167">如果您現在變更 hello MySetup.ps1 檔案 toowrite **Echo**命令時，這將會寫入 toohello 輸出檔，以進行偵錯：</span><span class="sxs-lookup"><span data-stu-id="06ce2-167">If you now change hello MySetup.ps1 file toowrite an **Echo** command, this will write toohello output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

<span data-ttu-id="06ce2-168">**您為您的指令碼偵錯之後，請立即移除這個主控台重新導向原則**。</span><span class="sxs-lookup"><span data-stu-id="06ce2-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="06ce2-169">設定服務程式碼封裝的原則</span><span class="sxs-lookup"><span data-stu-id="06ce2-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="06ce2-170">在 hello 先前步驟中，您已看到如何 tooapply RunAs 原則 tooSetupEntryPoint。</span><span class="sxs-lookup"><span data-stu-id="06ce2-170">In hello preceding steps, you saw how tooapply a RunAs policy tooSetupEntryPoint.</span></span> <span data-ttu-id="06ce2-171">讓我們來看更到 toocreate 不同主體可以當做套用服務原則的方式。</span><span class="sxs-lookup"><span data-stu-id="06ce2-171">Let's look a little deeper into how toocreate different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="06ce2-172">建立本機使用者群組</span><span class="sxs-lookup"><span data-stu-id="06ce2-172">Create local user groups</span></span>
<span data-ttu-id="06ce2-173">您可以定義和建立使用者群組，可讓一或多個使用者 toobe 加入 tooa 群組。</span><span class="sxs-lookup"><span data-stu-id="06ce2-173">You can define and create user groups that allow one or more users toobe added tooa group.</span></span> <span data-ttu-id="06ce2-174">如果有多個不同的服務進入點的使用者，而且他們需要 toohave hello 群組層級的特定一般權限，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="06ce2-174">This is useful if there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span> <span data-ttu-id="06ce2-175">hello 下列範例將示範名為的本機群組**LocalAdminGroup**具有系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="06ce2-175">hello following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="06ce2-176">Customer1 和 Customer2 這兩個使用者會成為此本機群組的成員。</span><span class="sxs-lookup"><span data-stu-id="06ce2-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a><span data-ttu-id="06ce2-177">建立本機使用者</span><span class="sxs-lookup"><span data-stu-id="06ce2-177">Create local users</span></span>
<span data-ttu-id="06ce2-178">您可以建立本機使用者可以安全使用的 toohelp hello 應用程式內的服務。</span><span class="sxs-lookup"><span data-stu-id="06ce2-178">You can create a local user that can be used toohelp secure a service within hello application.</span></span> <span data-ttu-id="06ce2-179">當**LocalUser**帳戶類型指定在 hello 主體區段 hello 應用程式資訊清單中，Service Fabric hello 應用程式部署所在的電腦上建立本機使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="06ce2-179">When a **LocalUser** account type is specified in hello principals section of hello application manifest, Service Fabric creates local user accounts on machines where hello application is deployed.</span></span> <span data-ttu-id="06ce2-180">根據預設，這些帳戶沒有的 hello 與 hello 應用程式中所指定的相同名稱的資訊清單 （例如，在下列範例中的 hello Customer3）。</span><span class="sxs-lookup"><span data-stu-id="06ce2-180">By default, these accounts do not have hello same names as those specified in hello application manifest (for example, Customer3 in hello following sample).</span></span> <span data-ttu-id="06ce2-181">相反地，它們會動態產生並具有隨機密碼。</span><span class="sxs-lookup"><span data-stu-id="06ce2-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="06ce2-182">如果應用程式需要 hello 使用者帳戶和密碼是相同的所有電腦 （例如，tooenable NTLM 驗證） 上，hello 叢集資訊清單必須設定 NTLMAuthenticationEnabled tootrue。</span><span class="sxs-lookup"><span data-stu-id="06ce2-182">If an application requires that hello user account and password be same on all machines (for example, tooenable NTLM authentication), hello cluster manifest must set NTLMAuthenticationEnabled tootrue.</span></span> <span data-ttu-id="06ce2-183">hello 叢集資訊清單也必須指定使用 NTLMAuthenticationPasswordSecret toogenerate hello 相同的密碼在所有機器上。</span><span class="sxs-lookup"><span data-stu-id="06ce2-183">hello cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used toogenerate hello same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a><span data-ttu-id="06ce2-184">指派原則 toohello 服務程式碼封裝</span><span class="sxs-lookup"><span data-stu-id="06ce2-184">Assign policies toohello service code packages</span></span>
<span data-ttu-id="06ce2-185">hello **RunAsPolicy**區段**ServiceManifestImport**指定應該使用的 toorun 程式碼封裝的 hello 主體區段中的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="06ce2-185">hello **RunAsPolicy** section for a **ServiceManifestImport** specifies hello account from hello principals section that should be used toorun a code package.</span></span> <span data-ttu-id="06ce2-186">它也將封裝從 hello 服務資訊清單的程式碼與 hello 主體區段中的使用者帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="06ce2-186">It also associates code packages from hello service manifest with user accounts in hello principals section.</span></span> <span data-ttu-id="06ce2-187">您可以指定此 hello 安裝程式或主要進入點，或者您可以指定`All`tooapply 它 tooboth。</span><span class="sxs-lookup"><span data-stu-id="06ce2-187">You can specify this for hello setup or main entry points, or you can specify `All` tooapply it tooboth.</span></span> <span data-ttu-id="06ce2-188">hello 下列範例顯示不同的原則套用：</span><span class="sxs-lookup"><span data-stu-id="06ce2-188">hello following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="06ce2-189">如果**EntryPointType**未指定，hello 預設設 tooEntryPointType ="Main"。</span><span class="sxs-lookup"><span data-stu-id="06ce2-189">If **EntryPointType** is not specified, hello default is set tooEntryPointType=”Main”.</span></span> <span data-ttu-id="06ce2-190">指定**SetupEntryPoint** ，特別適用於您想要 toorun 系統帳戶下的某些高特殊權限安裝程式作業。</span><span class="sxs-lookup"><span data-stu-id="06ce2-190">Specifying **SetupEntryPoint** is especially useful when you want toorun certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="06ce2-191">hello 實際服務程式碼可以在較低權限的帳戶下執行。</span><span class="sxs-lookup"><span data-stu-id="06ce2-191">hello actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-tooall-service-code-packages"></a><span data-ttu-id="06ce2-192">套用預設原則 tooall 服務程式碼封裝</span><span class="sxs-lookup"><span data-stu-id="06ce2-192">Apply a default policy tooall service code packages</span></span>
<span data-ttu-id="06ce2-193">使用 hello **DefaultRunAsPolicy**區段 toospecify 預設使用者帳戶沒有特定的所有程式碼封裝**RunAsPolicy**定義。</span><span class="sxs-lookup"><span data-stu-id="06ce2-193">You use hello **DefaultRunAsPolicy** section toospecify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="06ce2-194">如果大部分的 hello hello 應用程式所使用的服務資訊清單中指定的程式碼封裝需要下的 toorun hello 相同的使用者，hello 應用程式就可以定義預設 RunAs 原則以該使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="06ce2-194">If most of hello code packages that are specified in hello service manifest used by an application need toorun under hello same user, hello application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="06ce2-195">hello 下列範例會指定如果程式碼封裝沒有**RunAsPolicy**指定，hello 程式碼封裝執行的 hello **MyDefaultAccount** hello 主體區段中指定。</span><span class="sxs-lookup"><span data-stu-id="06ce2-195">hello following example specifies that if a code package does not have a **RunAsPolicy** specified, hello code package should run under hello **MyDefaultAccount** specified in hello principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="06ce2-196">使用 Active Directory 網域群組或使用者</span><span class="sxs-lookup"><span data-stu-id="06ce2-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="06ce2-197">使用 hello 獨立安裝程式在 Windows Server 已安裝的 Service Fabric 執行個體，您可以執行 Active Directory 使用者或群組帳戶 hello credentials hello 服務。</span><span class="sxs-lookup"><span data-stu-id="06ce2-197">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service under hello credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="06ce2-198">這是在您網域內的內部部署 Active Directory，與 Azure Active Directory (Azure AD) 無關。</span><span class="sxs-lookup"><span data-stu-id="06ce2-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="06ce2-199">使用網域使用者或群組，然後您可以存取其他資源 （例如，檔案共用） 的 hello 網域中已授與權限。</span><span class="sxs-lookup"><span data-stu-id="06ce2-199">By using a domain user or group, you can then access other resources in hello domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="06ce2-200">hello 下列範例會示範呼叫的 Active Directory 使用者*TestUser*其網域使用憑證來加密的密碼稱為*MyCert*。</span><span class="sxs-lookup"><span data-stu-id="06ce2-200">hello following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="06ce2-201">您可以使用 hello `Invoke-ServiceFabricEncryptText` PowerShell 命令 toocreate hello 密碼的加密文字。</span><span class="sxs-lookup"><span data-stu-id="06ce2-201">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text.</span></span> <span data-ttu-id="06ce2-202">如需詳細資訊，請參閱[管理 Service Fabric 應用程式中的密碼](service-fabric-application-secret-management.md)。</span><span class="sxs-lookup"><span data-stu-id="06ce2-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="06ce2-203">您必須將 hello 私密金鑰 hello 憑證 toodecrypt hello 密碼 toohello 本機電腦的部署使用不足的頻外方法 （在 Azure 中，這是透過 Azure Resource Manager）。</span><span class="sxs-lookup"><span data-stu-id="06ce2-203">You must deploy hello private key of hello certificate toodecrypt hello password toohello local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="06ce2-204">然後，當 Service Fabric 部署 hello 服務封裝 toohello 電腦，是無法 toodecrypt hello 密碼，並且使用 Active Directory toorun 下這些認證進行驗證 （以及 hello 使用者名稱）。</span><span class="sxs-lookup"><span data-stu-id="06ce2-204">Then, when Service Fabric deploys hello service package toohello machine, it is able toodecrypt hello secret and (along with hello user name) authenticate with Active Directory toorun under those credentials.</span></span>

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="06ce2-205">使用群組受管理服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="06ce2-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="06ce2-206">Windows Server 使用 hello 獨立安裝程式已安裝的 Service Fabric 執行個體，您可以執行 hello 服務當做群組受管理的服務帳戶 (gMSA)。</span><span class="sxs-lookup"><span data-stu-id="06ce2-206">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="06ce2-207">注意︰這是您的網域內部部署的 Active Directory，與 Azure Active Directory (Azure AD) 無關。</span><span class="sxs-lookup"><span data-stu-id="06ce2-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="06ce2-208">使用 gMSA 中，沒有任何密碼或加密的密碼儲存在 hello `Application Manifest`。</span><span class="sxs-lookup"><span data-stu-id="06ce2-208">By using a gMSA there is no password or encrypted password stored in hello `Application Manifest`.</span></span>

<span data-ttu-id="06ce2-209">hello 下列範例顯示如何 toocreate gMSA 帳戶呼叫*svc 測試 $*; 如何 toodeploy 管理的服務帳戶 toohello 叢集節點，和如何 tooconfigure hello 使用者主體。</span><span class="sxs-lookup"><span data-stu-id="06ce2-209">hello following example shows how toocreate a gMSA account called *svc-Test$*; how toodeploy that managed service account toohello cluster nodes; and how tooconfigure hello user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="06ce2-210">必要條件。</span><span class="sxs-lookup"><span data-stu-id="06ce2-210">Prerequisites.</span></span>
- <span data-ttu-id="06ce2-211">hello 網域必須 KDS 根金鑰。</span><span class="sxs-lookup"><span data-stu-id="06ce2-211">hello domain needs a KDS root key.</span></span>
- <span data-ttu-id="06ce2-212">需要在 Windows Server 2012 或更新版本的功能層級 toobe hello 網域。</span><span class="sxs-lookup"><span data-stu-id="06ce2-212">hello domain needs toobe at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="06ce2-213">範例</span><span class="sxs-lookup"><span data-stu-id="06ce2-213">Example</span></span>
1. <span data-ttu-id="06ce2-214">已建立群組受管理的服務帳戶使用 hello active directory 網域管理員`New-ADServiceAccount`指令程式，並確保該 hello`PrincipalsAllowedToRetrieveManagedPassword`包含所有 hello service fabric 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="06ce2-214">Have an active directory domain administrator create a group managed service account using hello `New-ADServiceAccount` commandlet and ensure that hello `PrincipalsAllowedToRetrieveManagedPassword` includes all of hello service fabric cluster nodes.</span></span> <span data-ttu-id="06ce2-215">請注意，`AccountName`、`DnsHostName` 和 `ServicePrincipalName` 必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="06ce2-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="06ce2-216">每個 hello service fabric 叢集節點上 (例如， `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`)、 安裝和測試 hello gMSA。</span><span class="sxs-lookup"><span data-stu-id="06ce2-216">On each of hello service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test hello gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="06ce2-217">設定 hello 使用者主體，並設定 hello RunAsPolicy tooreference hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="06ce2-217">Configure hello User principal, and configure hello RunAsPolicy tooreference hello user.</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="06ce2-218">為 HTTP 和 HTTPS 端點指派安全性存取原則</span><span class="sxs-lookup"><span data-stu-id="06ce2-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="06ce2-219">如果您套用 RunAs 原則 tooa 服務以及 hello 服務資訊清單宣告使用 hello HTTP 通訊協定的端點資源，您必須指定**SecurityAccessPolicy** tooensure 連接埠配置 toothese 端點可正常存取控制列 hello 服務執行的 RunAs 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="06ce2-219">If you apply a RunAs policy tooa service and hello service manifest declares endpoint resources with hello HTTP protocol, you must specify a **SecurityAccessPolicy** tooensure that ports allocated toothese endpoints are correctly access-control listed for hello RunAs user account that hello service runs under.</span></span> <span data-ttu-id="06ce2-220">否則， **http.sys**沒有存取 toohello 服務，並呼叫失敗收到 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="06ce2-220">Otherwise, **http.sys** does not have access toohello service, and you get failures with calls from hello client.</span></span> <span data-ttu-id="06ce2-221">hello 下列範例會套用 hello Customer1 帳戶 tooan 端點呼叫**EndpointName**，讓它的完整存取權限。</span><span class="sxs-lookup"><span data-stu-id="06ce2-221">hello following example applies hello Customer1 account tooan endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="06ce2-222">Hello HTTPS 端點，您也可以 tooindicate hello hello 憑證 tooreturn toohello 用戶端名稱。</span><span class="sxs-lookup"><span data-stu-id="06ce2-222">For hello HTTPS endpoint, you also have tooindicate hello name of hello certificate tooreturn toohello client.</span></span> <span data-ttu-id="06ce2-223">您可以使用**EndpointBindingPolicy**，hello hello 應用程式資訊清單中的憑證 > 一節中所定義的憑證。</span><span class="sxs-lookup"><span data-stu-id="06ce2-223">You can do this by using **EndpointBindingPolicy**, with hello certificate defined in a certificates section in hello application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="06ce2-224">使用 https 端點來升級多個應用程式</span><span class="sxs-lookup"><span data-stu-id="06ce2-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="06ce2-225">您需要小心 toobe 不 toouse hello**相同的連接埠**hello 的不同執行個體相同的應用程式使用 http 時**s**。</span><span class="sxs-lookup"><span data-stu-id="06ce2-225">You need toobe careful not toouse hello **same port** for different instances of hello same application when using http**s**.</span></span> <span data-ttu-id="06ce2-226">hello 原因是 Service Fabric 無法能 tooupgrade hello 憑證之其中一個 hello 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="06ce2-226">hello reason is that Service Fabric won't be able tooupgrade hello cert for one of hello application instances.</span></span> <span data-ttu-id="06ce2-227">例如，如果應用程式 1 或應用程式 2 同時想 tooupgrade 其 cert 1 toocert 2。</span><span class="sxs-lookup"><span data-stu-id="06ce2-227">For example, if application 1 or application 2 both want tooupgrade their cert 1 toocert 2.</span></span> <span data-ttu-id="06ce2-228">Hello 升級發生失敗時，Service Fabric 可能清除 hello cert 1 註冊 http.sys 即使 hello 其他應用程式仍在使用它。</span><span class="sxs-lookup"><span data-stu-id="06ce2-228">When hello upgrade happens, Service Fabric might have cleaned up hello cert 1 registration with http.sys even though hello other application is still using it.</span></span> <span data-ttu-id="06ce2-229">tooprevent，Service Fabric 偵測到已經有另一個 hello hello 憑證的通訊埠上註冊的應用程式執行個體 (因為 toohttp.sys) 和失敗 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="06ce2-229">tooprevent this, Service Fabric detects that there is already another application instance registered on hello port with hello certificate (due toohttp.sys) and fails hello operation.</span></span>

<span data-ttu-id="06ce2-230">因此 Service Fabric 不支援升級兩個不同的服務使用**hello 相同的連接埠**中不同的應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="06ce2-230">Hence Service Fabric does not support upgrading two different services using **hello same port** in different application instances.</span></span> <span data-ttu-id="06ce2-231">換句話說，您不能使用相同憑證的 hello 在 hello 上的不同服務相同的連接埠。</span><span class="sxs-lookup"><span data-stu-id="06ce2-231">In other words, you cannot use hello same certificate on different services on hello same port.</span></span> <span data-ttu-id="06ce2-232">如果您需要 toohave 共用憑證在 hello 相同連接埠，您需要該服務位於不同位置條件約束使用的電腦的 hello tooensure。</span><span class="sxs-lookup"><span data-stu-id="06ce2-232">If you need toohave a shared certificate on hello same port, you need tooensure that hello services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="06ce2-233">或者，可能的話，考慮針對每個應用程式執行個體中的每個服務，使用 Service Fabric 動態連接埠。</span><span class="sxs-lookup"><span data-stu-id="06ce2-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="06ce2-234">如果您看到使用 https，升級失敗錯誤警告，指出 「 hello Windows HTTP 伺服器 API 不支援多個憑證共用連接埠的應用程式。 」</span><span class="sxs-lookup"><span data-stu-id="06ce2-234">If you see an upgrade fail with https, an error warning saying "hello Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="06ce2-235">完整的應用程式資訊清單範例</span><span class="sxs-lookup"><span data-stu-id="06ce2-235">A complete application manifest example</span></span>
<span data-ttu-id="06ce2-236">下列應用程式資訊清單的 hello 顯示 hello 的許多不同的設定：</span><span class="sxs-lookup"><span data-stu-id="06ce2-236">hello following application manifest shows many of hello different settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="06ce2-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="06ce2-237">Next steps</span></span>
* [<span data-ttu-id="06ce2-238">了解 hello 應用程式模型</span><span class="sxs-lookup"><span data-stu-id="06ce2-238">Understand hello application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="06ce2-239">在服務資訊清單中指定資源</span><span class="sxs-lookup"><span data-stu-id="06ce2-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="06ce2-240">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="06ce2-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
