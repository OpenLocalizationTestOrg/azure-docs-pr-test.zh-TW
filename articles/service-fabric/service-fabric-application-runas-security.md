---
title: "了解 Azure 微服務安全性原則 | Microsoft Docs"
description: "如何以系統和本機安全性帳戶執行 Service Fabric 應用程式的概觀，包括應用程式在啟動前需要執行某些特殊權限動作的 SetupEntry 點"
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
ms.openlocfilehash: e673b45a43a06d18040c3437caf8765704d5c36a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="fa974-103">設定應用程式的安全性原則</span><span class="sxs-lookup"><span data-stu-id="fa974-103">Configure security policies for your application</span></span>
<span data-ttu-id="fa974-104">藉由使用 Azure Service Fabric，您便可以保護在叢集中以不同使用者帳戶執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa974-104">By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts.</span></span> <span data-ttu-id="fa974-105">在以該使用者帳戶部署時，Service Fabric 也會協助保護應用程式所使用的資源，例如檔案、目錄和憑證。</span><span class="sxs-lookup"><span data-stu-id="fa974-105">Service Fabric also helps secure the resources that are used by applications at the time of deployment under the user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="fa974-106">如此一來，即使在共用主控環境中，執行中的應用程式就不會彼此干擾。</span><span class="sxs-lookup"><span data-stu-id="fa974-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="fa974-107">根據預設，Service Fabric 應用程式會在用以執行 Fabric.exe 程序的帳戶之下執行。</span><span class="sxs-lookup"><span data-stu-id="fa974-107">By default, Service Fabric applications run under the account that the Fabric.exe process runs under.</span></span> <span data-ttu-id="fa974-108">Service Fabric 也能夠以本機使用者帳戶或本機系統帳戶 (在應用程式的資訊清單內指定) 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa974-108">Service Fabric also provides the capability to run applications under a local user account or local system account, which is specified within the application manifest.</span></span> <span data-ttu-id="fa974-109">支援的本機系統帳戶類型為 **LocalUser**、**NetworkService**、**LocalService** 和 **LocalSystem**。</span><span class="sxs-lookup"><span data-stu-id="fa974-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="fa974-110">當您使用獨立安裝程式在資料中心的 Windows Server 上執行 Service Fabric 時，您可以使用 Active Directory 網域帳戶，包括群組受管理服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa974-110">When you're running Service Fabric on Windows Server in your datacenter by using the standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="fa974-111">您可以定義和建立使用者群組，以便將一或多個使用者新增至每個群組一起管理。</span><span class="sxs-lookup"><span data-stu-id="fa974-111">You can define and create user groups so that one or more users can be added to each group to be managed together.</span></span> <span data-ttu-id="fa974-112">當不同的服務進入點有多個使用者，而且他們需要具備可在群組層級取得的某些常見權限時，這會很有用。</span><span class="sxs-lookup"><span data-stu-id="fa974-112">This is useful when there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span>

## <a name="configure-the-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="fa974-113">設定服務安裝程式進入點的原則</span><span class="sxs-lookup"><span data-stu-id="fa974-113">Configure the policy for a service setup entry point</span></span>
<span data-ttu-id="fa974-114">如[應用程式模型](service-fabric-application-model.md)所述，安裝程式進入點 **SetupEntryPoint** 是以與 Service Fabric 相同的認證執行的特殊權限進入點 (通常為 *NetworkService* 帳戶)，優先於其他任何進入點。</span><span class="sxs-lookup"><span data-stu-id="fa974-114">As described in the [application model](service-fabric-application-model.md), the setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with the same credentials as Service Fabric (typically the *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="fa974-115">**EntryPoint** 指定的可執行檔通常是長時間執行的服務主機。</span><span class="sxs-lookup"><span data-stu-id="fa974-115">The executable that is specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="fa974-116">因此有個別安裝程式的進入點，就不需要使用較高權限來長時間執行服務主機可執行檔。</span><span class="sxs-lookup"><span data-stu-id="fa974-116">So having a separate setup entry point avoids having to run the service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="fa974-117">**EntryPoint** 指定的可執行檔是在 **SetupEntryPoint** 成功結束之後執行。</span><span class="sxs-lookup"><span data-stu-id="fa974-117">The executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="fa974-118">產生的程序會受到監視，萬一終止或當機，則會同樣從 **SetupEntryPoint** 開始來重新啟動。</span><span class="sxs-lookup"><span data-stu-id="fa974-118">The resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="fa974-119">以下簡單的服務資訊清單範例會顯示服務的 SetupEntryPoint 和主要的 EntryPoint。</span><span class="sxs-lookup"><span data-stu-id="fa974-119">The following is a simple service manifest example that shows the SetupEntryPoint and the main EntryPoint for the service.</span></span>

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

### <a name="configure-the-policy-by-using-a-local-account"></a><span data-ttu-id="fa974-120">使用本機帳戶設定原則</span><span class="sxs-lookup"><span data-stu-id="fa974-120">Configure the policy by using a local account</span></span>
<span data-ttu-id="fa974-121">在您設定服務以擁有安裝進入點之後，就能在應用程式資訊清單中變更用以執行的安全性權限。</span><span class="sxs-lookup"><span data-stu-id="fa974-121">After you configure the service to have a setup entry point, you can change the security permissions that it runs under in the application manifest.</span></span> <span data-ttu-id="fa974-122">下列範例示範如何將服務設定成以使用者系統管理員帳戶權限執行。</span><span class="sxs-lookup"><span data-stu-id="fa974-122">The following example shows how to configure the service to run under user administrator account privileges.</span></span>

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

<span data-ttu-id="fa974-123">首先，以使用者名稱 (例如 SetupAdminUser) 建立 **Principals** 區段。</span><span class="sxs-lookup"><span data-stu-id="fa974-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="fa974-124">這表示使用者是 Administrators 系統群組的成員。</span><span class="sxs-lookup"><span data-stu-id="fa974-124">This indicates that the user is a member of the Administrators system group.</span></span>

<span data-ttu-id="fa974-125">接著在 **ServiceManifestImport** 區段下方設定原則，以將此主體套用至 **SetupEntryPoint**。</span><span class="sxs-lookup"><span data-stu-id="fa974-125">Next, under the **ServiceManifestImport** section, configure a policy to apply this principal to **SetupEntryPoint**.</span></span> <span data-ttu-id="fa974-126">這會告知 Service Fabric，當 **MySetup.bat** 檔案執行時，執行身分 `RunAs` 應該具備系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="fa974-126">This tells Service Fabric that when the **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="fa974-127">假設您「尚未」將原則套用至主要進入點，則 **MyServiceHost.exe** 中的程式碼將會以系統 **NetworkService** 帳戶執行。</span><span class="sxs-lookup"><span data-stu-id="fa974-127">Given that you have *not* applied a policy to the main entry point, the code in **MyServiceHost.exe** runs under the system **NetworkService** account.</span></span> <span data-ttu-id="fa974-128">這是用來執行所有服務進入點的預設帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa974-128">This is the default account that all service entry points are run as.</span></span>

<span data-ttu-id="fa974-129">現在讓我們將 MySetup.bat 檔案加入 Visual Studio 專案，以測試系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="fa974-129">Let's now add the file MySetup.bat to the Visual Studio project to test the administrator privileges.</span></span> <span data-ttu-id="fa974-130">在 Visual Studio 中，以滑鼠右鍵按一下服務專案，並新增名為 MySetup.bat 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="fa974-130">In Visual Studio, right-click the service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="fa974-131">接下來，確定 MySetup.bat 檔案已包含於服務封裝中。</span><span class="sxs-lookup"><span data-stu-id="fa974-131">Next, ensure that the MySetup.bat file is included in the service package.</span></span> <span data-ttu-id="fa974-132">預設不會包含該檔案。</span><span class="sxs-lookup"><span data-stu-id="fa974-132">By default, it is not.</span></span> <span data-ttu-id="fa974-133">選取該檔案、以滑鼠右鍵按一下操作功能表，然後選擇 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="fa974-133">Select the file, right-click to get the context menu, and choose **Properties**.</span></span> <span data-ttu-id="fa974-134">在 [屬性] 對話方塊中，確定已將 [複製到輸出目錄] 設為 [有更新時才複製]。</span><span class="sxs-lookup"><span data-stu-id="fa974-134">In the Properties dialog box, ensure that **Copy to Output Directory** is set to **Copy if newer**.</span></span> <span data-ttu-id="fa974-135">請參閱下列螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="fa974-135">See the following screenshot.</span></span>

![Visual Studio CopyToOutput for SetupEntryPoint 批次檔][image1]

<span data-ttu-id="fa974-137">現在開啟 MySetup.bat 檔案並加入下列命令：</span><span class="sxs-lookup"><span data-stu-id="fa974-137">Now open the MySetup.bat file and add the following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set to > out.txt
echo %TestVariable% >> out.txt

REM To delete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="fa974-138">接下來，建置解決方案並部署至本機開發叢集。</span><span class="sxs-lookup"><span data-stu-id="fa974-138">Next, build and deploy the solution to a local development cluster.</span></span> <span data-ttu-id="fa974-139">啟動服務之後 (如 Service Fabric 總管中所示)，您就可以看到 MySetup.bat 檔案成功的方式有兩種。</span><span class="sxs-lookup"><span data-stu-id="fa974-139">After the service has started, as shown in Service Fabric Explorer, you can see that the MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="fa974-140">開啟 PowerShell 命令提示字元並輸入：</span><span class="sxs-lookup"><span data-stu-id="fa974-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="fa974-141">接著，記下已在 Service Fabric 總管中部署並啟動服務的節點名稱，例如節點 2。</span><span class="sxs-lookup"><span data-stu-id="fa974-141">Then, note the name of the node where the service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="fa974-142">接下來，瀏覽至應用程式執行個體工作資料夾，尋出 out.txt 檔案，其中顯示 **TestVariable**的值。</span><span class="sxs-lookup"><span data-stu-id="fa974-142">Next, navigate to the application instance work folder to find the out.txt file that shows the value of **TestVariable**.</span></span> <span data-ttu-id="fa974-143">例如，如果此服務已部署至節點 2，則您可以移至 **MyApplicationType** 的這個路徑：</span><span class="sxs-lookup"><span data-stu-id="fa974-143">For example, if this service was deployed to Node 2, then you can go to this path for the **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-the-policy-by-using-local-system-accounts"></a><span data-ttu-id="fa974-144">使用本機系統帳戶設定原則</span><span class="sxs-lookup"><span data-stu-id="fa974-144">Configure the policy by using local system accounts</span></span>
<span data-ttu-id="fa974-145">通常最好是使用本機系統帳戶 (而不是系統管理員帳戶) 執行啟動指令碼。</span><span class="sxs-lookup"><span data-stu-id="fa974-145">Often, it's preferable to run the startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="fa974-146">使用系統管理員群組成員的身分執行 RunAs 原則通常沒有作用，因為電腦預設啟用使用者存取控制 (UAC)。</span><span class="sxs-lookup"><span data-stu-id="fa974-146">Running the RunAs policy as a member of the Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="fa974-147">在此情況下，**建議是以 LocalSystem 身分 (而不是以新增到系統管理員群組的本機使用者身分) 執行 SetupEntryPoint**。</span><span class="sxs-lookup"><span data-stu-id="fa974-147">In such cases, **the recommendation is to run the SetupEntryPoint as LocalSystem, instead of as a local user added to Administrators group**.</span></span> <span data-ttu-id="fa974-148">下列範例示範如何設定 SetupEntryPoint 以 LocalSystem 身分執行：</span><span class="sxs-lookup"><span data-stu-id="fa974-148">The following example shows setting the SetupEntryPoint to run as LocalSystem:</span></span>

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="fa974-149">從安裝程式進入點啟動 PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="fa974-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="fa974-150">若要從 **SetupEntryPoint** 點執行 PowerShell，您可以在指向 PowerShell 檔案的批次檔中執行 **PowerShell.exe**。</span><span class="sxs-lookup"><span data-stu-id="fa974-150">To run PowerShell from the **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points to a PowerShell file.</span></span> <span data-ttu-id="fa974-151">首先，將 PowerShell 檔案新增至服務專案，例如 **MySetup.ps1**。</span><span class="sxs-lookup"><span data-stu-id="fa974-151">First, add a PowerShell file to the service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="fa974-152">請記得設定 [有更新時才複製]  屬性，讓這個檔案也會包含於服務封裝內。</span><span class="sxs-lookup"><span data-stu-id="fa974-152">Remember to set the *Copy if newer* property so that the file is also included in the service package.</span></span> <span data-ttu-id="fa974-153">下列範例顯示的範例批次檔可啟動名為 MySetup.ps1 的 PowerShell 檔案，以設定名為 **TestVariable** 的系統環境變數。</span><span class="sxs-lookup"><span data-stu-id="fa974-153">The following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="fa974-154">MySetup.bat 可啟動 PowerShell 檔案：</span><span class="sxs-lookup"><span data-stu-id="fa974-154">MySetup.bat to start a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="fa974-155">在 PowerShell 檔案中，加入以下項目來設定系統環境變數：</span><span class="sxs-lookup"><span data-stu-id="fa974-155">In the PowerShell file, add the following to set a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="fa974-156">當批次檔執行時，預設會在稱為 **work** 的應用程式資料夾中查看檔案。</span><span class="sxs-lookup"><span data-stu-id="fa974-156">By default, when the batch file runs, it looks at the application folder called **work** for files.</span></span> <span data-ttu-id="fa974-157">在此情況下，當 MySetup.bat 執行時，我們希望它會在相同資料夾 (也就是應用程式的 **code package** 資料夾) 中尋找 MySetup.ps1 檔。</span><span class="sxs-lookup"><span data-stu-id="fa974-157">In this case, when MySetup.bat runs, we want this to find the MySetup.ps1 file in the same folder, which is the application **code package** folder.</span></span> <span data-ttu-id="fa974-158">若要變更此資料夾，請設定工作資料夾：</span><span class="sxs-lookup"><span data-stu-id="fa974-158">To change this folder, set the working folder:</span></span>
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

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="fa974-159">使用主控台重新導向進行本機偵錯</span><span class="sxs-lookup"><span data-stu-id="fa974-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="fa974-160">基於偵錯的目的，查看執行指令碼後的主控台輸出偶爾會有幫助。</span><span class="sxs-lookup"><span data-stu-id="fa974-160">Occasionally, it's useful to see the console output from running a script for debugging purposes.</span></span> <span data-ttu-id="fa974-161">若要這樣做，您可以設定主控台重新導向原則，將輸出寫入至檔案。</span><span class="sxs-lookup"><span data-stu-id="fa974-161">To do this, you can set a console redirection policy, which writes the output to a file.</span></span> <span data-ttu-id="fa974-162">檔案輸出會寫入至部署並執行應用程式所在的節點上，稱為 **log** 的應用程式資料夾中。</span><span class="sxs-lookup"><span data-stu-id="fa974-162">The file output is written to the application folder called **log** on the node where the application is deployed and run.</span></span> <span data-ttu-id="fa974-163">(請參閱先前範例中在何處可以找到此資料夾。)</span><span class="sxs-lookup"><span data-stu-id="fa974-163">(See where to find this in the preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="fa974-164">切勿在實際部署的應用程式中使用主控台重新導向原則，因為這可能會影響應用程式容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="fa974-164">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="fa974-165">僅將此原則用於本機開發及偵錯。</span><span class="sxs-lookup"><span data-stu-id="fa974-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="fa974-166">下列範例示範如何使用 FileRetentionCount 值設定主控台重新導向：</span><span class="sxs-lookup"><span data-stu-id="fa974-166">The following example shows setting the console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="fa974-167">如果您現在變更 MySetup.ps1 檔案來撰寫 **Echo** 命令，這將會寫入至輸出檔案以進行偵錯：</span><span class="sxs-lookup"><span data-stu-id="fa974-167">If you now change the MySetup.ps1 file to write an **Echo** command, this will write to the output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes to the application log folder on the node that the application is deployed to"
```

<span data-ttu-id="fa974-168">**您為您的指令碼偵錯之後，請立即移除這個主控台重新導向原則**。</span><span class="sxs-lookup"><span data-stu-id="fa974-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="fa974-169">設定服務程式碼封裝的原則</span><span class="sxs-lookup"><span data-stu-id="fa974-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="fa974-170">在前述步驟中，您看到了如何將 RunAs 原則套用到 SetupEntryPoint。</span><span class="sxs-lookup"><span data-stu-id="fa974-170">In the preceding steps, you saw how to apply a RunAs policy to SetupEntryPoint.</span></span> <span data-ttu-id="fa974-171">讓我們深入了解如何建立可當作服務原則套用的不同主體。</span><span class="sxs-lookup"><span data-stu-id="fa974-171">Let's look a little deeper into how to create different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="fa974-172">建立本機使用者群組</span><span class="sxs-lookup"><span data-stu-id="fa974-172">Create local user groups</span></span>
<span data-ttu-id="fa974-173">您可以定義和建立使用者群組，然後將一或多個使用者新增至群組。</span><span class="sxs-lookup"><span data-stu-id="fa974-173">You can define and create user groups that allow one or more users to be added to a group.</span></span> <span data-ttu-id="fa974-174">當不同的服務進入點有多個使用者，而他們需要具備可在群組層級取得的某些通用權限時，這會很有用。</span><span class="sxs-lookup"><span data-stu-id="fa974-174">This is useful if there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span> <span data-ttu-id="fa974-175">下列範例顯示名為 **LocalAdminGroup** 且具有系統管理員權限的本機群組。</span><span class="sxs-lookup"><span data-stu-id="fa974-175">The following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="fa974-176">Customer1 和 Customer2 這兩個使用者會成為此本機群組的成員。</span><span class="sxs-lookup"><span data-stu-id="fa974-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

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

### <a name="create-local-users"></a><span data-ttu-id="fa974-177">建立本機使用者</span><span class="sxs-lookup"><span data-stu-id="fa974-177">Create local users</span></span>
<span data-ttu-id="fa974-178">您可以建立一個本機使用者，以便用來協助保護應用程式內的服務。</span><span class="sxs-lookup"><span data-stu-id="fa974-178">You can create a local user that can be used to help secure a service within the application.</span></span> <span data-ttu-id="fa974-179">在應用程式資訊清單的主體區段中指定 **LocalUser** 帳戶類型時，Service Fabric 會在部署應用程式所在的電腦上建立本機使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa974-179">When a **LocalUser** account type is specified in the principals section of the application manifest, Service Fabric creates local user accounts on machines where the application is deployed.</span></span> <span data-ttu-id="fa974-180">根據預設，這些帳戶的名稱不會與應用程式資訊清單中所指定的名稱一樣 (例如，下列範例中的 Customer3)。</span><span class="sxs-lookup"><span data-stu-id="fa974-180">By default, these accounts do not have the same names as those specified in the application manifest (for example, Customer3 in the following sample).</span></span> <span data-ttu-id="fa974-181">相反地，它們會動態產生並具有隨機密碼。</span><span class="sxs-lookup"><span data-stu-id="fa974-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="fa974-182">如果應用程式要求使用者帳戶和密碼在所有機器上必須都相同 (例如，為了啟用 NTLM 驗證)，叢集資訊清單就必須將 NTLMAuthenticationEnabled 設定為 true。</span><span class="sxs-lookup"><span data-stu-id="fa974-182">If an application requires that the user account and password be same on all machines (for example, to enable NTLM authentication), the cluster manifest must set NTLMAuthenticationEnabled to true.</span></span> <span data-ttu-id="fa974-183">叢集資訊清單也必須指定用來在所有機器產生相同密碼的 NTLMAuthenticationPasswordSecret。</span><span class="sxs-lookup"><span data-stu-id="fa974-183">The cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used to generate the same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-to-the-service-code-packages"></a><span data-ttu-id="fa974-184">將原則指派給服務程式碼封裝</span><span class="sxs-lookup"><span data-stu-id="fa974-184">Assign policies to the service code packages</span></span>
<span data-ttu-id="fa974-185">**ServiceManifestImport** 的 **RunAsPolicy** 區段會指定主體區段中應用來執行程式碼封裝的帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa974-185">The **RunAsPolicy** section for a **ServiceManifestImport** specifies the account from the principals section that should be used to run a code package.</span></span> <span data-ttu-id="fa974-186">它也會將服務資訊清單中的程式碼封裝關聯至主體區段中的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa974-186">It also associates code packages from the service manifest with user accounts in the principals section.</span></span> <span data-ttu-id="fa974-187">您可以為安裝或主要進入點指定此原則，或指定 `All` 以將其套用到兩者。</span><span class="sxs-lookup"><span data-stu-id="fa974-187">You can specify this for the setup or main entry points, or you can specify `All` to apply it to both.</span></span> <span data-ttu-id="fa974-188">下列範例顯示套用不同的原則：</span><span class="sxs-lookup"><span data-stu-id="fa974-188">The following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="fa974-189">如果未指定 **EntryPointType** ，則預設值會設定為 EntryPointType ="Main"。</span><span class="sxs-lookup"><span data-stu-id="fa974-189">If **EntryPointType** is not specified, the default is set to EntryPointType=”Main”.</span></span> <span data-ttu-id="fa974-190">當您想要以系統帳戶執行某些高權限設定作業時，指定 **SetupEntryPoint** 特別有用。</span><span class="sxs-lookup"><span data-stu-id="fa974-190">Specifying **SetupEntryPoint** is especially useful when you want to run certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="fa974-191">實際的服務程式碼可利用較低權限的帳戶來執行。</span><span class="sxs-lookup"><span data-stu-id="fa974-191">The actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-to-all-service-code-packages"></a><span data-ttu-id="fa974-192">將預設原則套用到所有的服務程式碼封裝</span><span class="sxs-lookup"><span data-stu-id="fa974-192">Apply a default policy to all service code packages</span></span>
<span data-ttu-id="fa974-193">您使用 **DefaultRunAsPolicy** 區段來針對未定義特定 **RunAsPolicy** 的所有程式碼套件，指定預設的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa974-193">You use the **DefaultRunAsPolicy** section to specify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="fa974-194">如果在應用程式所使用的服務資訊清單中指定的大部分程式碼封裝必須以相同的使用者身分執行，則應用程式可以只使用該使用者帳戶定義預設的 RunAs 原則。</span><span class="sxs-lookup"><span data-stu-id="fa974-194">If most of the code packages that are specified in the service manifest used by an application need to run under the same user, the application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="fa974-195">下列範例指定某個程式碼封裝未指定 **RunAsPolicy** 時，該程式碼封裝應該以主體區段中指定的 **MyDefaultAccount** 執行。</span><span class="sxs-lookup"><span data-stu-id="fa974-195">The following example specifies that if a code package does not have a **RunAsPolicy** specified, the code package should run under the **MyDefaultAccount** specified in the principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="fa974-196">使用 Active Directory 網域群組或使用者</span><span class="sxs-lookup"><span data-stu-id="fa974-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="fa974-197">對於安裝在 Windows Server 上的 Service Fabric 執行個體，獨立安裝程式可讓您以 Active Directory 使用者或群組帳戶的認證來執行服務。</span><span class="sxs-lookup"><span data-stu-id="fa974-197">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service under the credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="fa974-198">這是在您網域內的內部部署 Active Directory，與 Azure Active Directory (Azure AD) 無關。</span><span class="sxs-lookup"><span data-stu-id="fa974-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="fa974-199">然後，您可以使用網域使用者或群組，存取網域中已經被授與權限的其他資源 (例如檔案共用)。</span><span class="sxs-lookup"><span data-stu-id="fa974-199">By using a domain user or group, you can then access other resources in the domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="fa974-200">下列範例顯示的 Active Directory 使用者稱為 *TestUser*，其網域密碼以稱為 *MyCert* 的憑證加密。</span><span class="sxs-lookup"><span data-stu-id="fa974-200">The following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="fa974-201">您可以使用 `Invoke-ServiceFabricEncryptText` Powershell 命令來建立密碼加密文字。</span><span class="sxs-lookup"><span data-stu-id="fa974-201">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text.</span></span> <span data-ttu-id="fa974-202">如需詳細資訊，請參閱[管理 Service Fabric 應用程式中的密碼](service-fabric-application-secret-management.md)。</span><span class="sxs-lookup"><span data-stu-id="fa974-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="fa974-203">您必須將密碼解密的憑證私密金鑰以頻外方法部署到本機電腦 (在 Azure 中，這是透過 Azure Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="fa974-203">You must deploy the private key of the certificate to decrypt the password to the local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="fa974-204">然後，當 Service Fabric 將服務封裝部署到電腦時，它就能夠將密碼解密，並連同使用者名稱向 Active Directory 進行驗證，而在這些認證下執行。</span><span class="sxs-lookup"><span data-stu-id="fa974-204">Then, when Service Fabric deploys the service package to the machine, it is able to decrypt the secret and (along with the user name) authenticate with Active Directory to run under those credentials.</span></span>

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
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="fa974-205">使用群組受管理服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa974-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="fa974-206">對於使用獨立安裝程式安裝於 Windows Server 上的 Service Fabric 執行個體，您可以群組受管理服務帳戶 (gMSA) 來執行服務。</span><span class="sxs-lookup"><span data-stu-id="fa974-206">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="fa974-207">注意︰這是您的網域內部部署的 Active Directory，與 Azure Active Directory (Azure AD) 無關。</span><span class="sxs-lookup"><span data-stu-id="fa974-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="fa974-208">使用 gMSA，就不需將密碼或加密的密碼儲存於 `Application Manifest`。</span><span class="sxs-lookup"><span data-stu-id="fa974-208">By using a gMSA there is no password or encrypted password stored in the `Application Manifest`.</span></span>

<span data-ttu-id="fa974-209">下列範例示範如何建立名為 *svc-Test$* 的 gMSA 帳戶；如何將受管理的服務帳戶部署至叢集節點；以及如何設定使用者主體。</span><span class="sxs-lookup"><span data-stu-id="fa974-209">The following example shows how to create a gMSA account called *svc-Test$*; how to deploy that managed service account to the cluster nodes; and how to configure the user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="fa974-210">必要條件。</span><span class="sxs-lookup"><span data-stu-id="fa974-210">Prerequisites.</span></span>
- <span data-ttu-id="fa974-211">網域需要一個 KDS 根金鑰。</span><span class="sxs-lookup"><span data-stu-id="fa974-211">The domain needs a KDS root key.</span></span>
- <span data-ttu-id="fa974-212">網域必須位於 Windows Server 2012 或更新版本的功能層級上。</span><span class="sxs-lookup"><span data-stu-id="fa974-212">The domain needs to be at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="fa974-213">範例</span><span class="sxs-lookup"><span data-stu-id="fa974-213">Example</span></span>
1. <span data-ttu-id="fa974-214">讓 Active Directory 網域系統管理員能夠使用 `New-ADServiceAccount` 指令程式來建立群組受管理服務帳戶，並確定 `PrincipalsAllowedToRetrieveManagedPassword` 包括所有 Service Fabric 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="fa974-214">Have an active directory domain administrator create a group managed service account using the `New-ADServiceAccount` commandlet and ensure that the `PrincipalsAllowedToRetrieveManagedPassword` includes all of the service fabric cluster nodes.</span></span> <span data-ttu-id="fa974-215">請注意，`AccountName`、`DnsHostName` 和 `ServicePrincipalName` 必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="fa974-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="fa974-216">在每個 Service Fabric 叢集節點 (例如 `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`) 上，安裝並測試 gMSA。</span><span class="sxs-lookup"><span data-stu-id="fa974-216">On each of the service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test the gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="fa974-217">設定使用者主體，並設定 RunAsPolicy 來參考使用者。</span><span class="sxs-lookup"><span data-stu-id="fa974-217">Configure the User principal, and configure the RunAsPolicy to reference the user.</span></span>
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="fa974-218">為 HTTP 和 HTTPS 端點指派安全性存取原則</span><span class="sxs-lookup"><span data-stu-id="fa974-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="fa974-219">如果您將 RunAs 原則套用到服務，而且服務資訊清單宣告具有 HTTP 通訊協定的端點資源，則您必須指定 **SecurityAccessPolicy**，以確保配置給這些端點的連接埠都已針對用以執行服務的 RunAs 使用者帳戶，正確列入存取控制清單中。</span><span class="sxs-lookup"><span data-stu-id="fa974-219">If you apply a RunAs policy to a service and the service manifest declares endpoint resources with the HTTP protocol, you must specify a **SecurityAccessPolicy** to ensure that ports allocated to these endpoints are correctly access-control listed for the RunAs user account that the service runs under.</span></span> <span data-ttu-id="fa974-220">否則， **http.sys** 無法存取服務，而且您從用戶端呼叫時將會失敗。</span><span class="sxs-lookup"><span data-stu-id="fa974-220">Otherwise, **http.sys** does not have access to the service, and you get failures with calls from the client.</span></span> <span data-ttu-id="fa974-221">下列範例會將 Customer1 帳戶套用到名為 **EndpointName** 的端點，這會給予它完整的存取權限。</span><span class="sxs-lookup"><span data-stu-id="fa974-221">The following example applies the Customer1 account to an endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="fa974-222">針對 HTTPS 端點，您也必須指出要傳回給用戶端的憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="fa974-222">For the HTTPS endpoint, you also have to indicate the name of the certificate to return to the client.</span></span> <span data-ttu-id="fa974-223">在作法上，您可以使用 **EndpointBindingPolicy**，並搭配應用程式資訊清單之憑證區段中定義的憑證。</span><span class="sxs-lookup"><span data-stu-id="fa974-223">You can do this by using **EndpointBindingPolicy**, with the certificate defined in a certificates section in the application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if the EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="fa974-224">使用 https 端點來升級多個應用程式</span><span class="sxs-lookup"><span data-stu-id="fa974-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="fa974-225">使用 http**s** 時，請務必小心，不要將「相同的連接埠」用於相同應用程式的不同執行個體。</span><span class="sxs-lookup"><span data-stu-id="fa974-225">You need to be careful not to use the **same port** for different instances of the same application when using http**s**.</span></span> <span data-ttu-id="fa974-226">原因是 Service Fabric 將無法升級其中一個應用程式執行個體的憑證。</span><span class="sxs-lookup"><span data-stu-id="fa974-226">The reason is that Service Fabric won't be able to upgrade the cert for one of the application instances.</span></span> <span data-ttu-id="fa974-227">舉例來說，如果應用程式 1 或應用程式 2 都想要將其憑證 1 升級至憑證 2。</span><span class="sxs-lookup"><span data-stu-id="fa974-227">For example, if application 1 or application 2 both want to upgrade their cert 1 to cert 2.</span></span> <span data-ttu-id="fa974-228">當進行升級時，Service Fabric 可能已清除憑證 1 在 http.sys 的註冊，儘管另一個應用程式仍然在使用它。</span><span class="sxs-lookup"><span data-stu-id="fa974-228">When the upgrade happens, Service Fabric might have cleaned up the cert 1 registration with http.sys even though the other application is still using it.</span></span> <span data-ttu-id="fa974-229">為了防止這種情況，Service Fabric 會偵測到該連接埠上已經有另一個應用程式以該憑證註冊 (因為 http.sys)，而讓作業失敗。</span><span class="sxs-lookup"><span data-stu-id="fa974-229">To prevent this, Service Fabric detects that there is already another application instance registered on the port with the certificate (due to http.sys) and fails the operation.</span></span>

<span data-ttu-id="fa974-230">因此，Service Fabric 不支援在不同的應用程式執行個體中，使用「相同的連接埠」來升級兩個不同的服務。</span><span class="sxs-lookup"><span data-stu-id="fa974-230">Hence Service Fabric does not support upgrading two different services using **the same port** in different application instances.</span></span> <span data-ttu-id="fa974-231">換句話說，您無法在相同連接埠的不同服務上使用相同的憑證。</span><span class="sxs-lookup"><span data-stu-id="fa974-231">In other words, you cannot use the same certificate on different services on the same port.</span></span> <span data-ttu-id="fa974-232">如果您需要在相同的連接埠上使用共用憑證，就必須使用放置條件約束，以確保將這些服務放在不同的機器上。</span><span class="sxs-lookup"><span data-stu-id="fa974-232">If you need to have a shared certificate on the same port, you need to ensure that the services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="fa974-233">或者，可能的話，考慮針對每個應用程式執行個體中的每個服務，使用 Service Fabric 動態連接埠。</span><span class="sxs-lookup"><span data-stu-id="fa974-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="fa974-234">如果您看到使用 https 進行升級失敗，系統將會顯示錯誤警告「Windows HTTP 伺服器 API 針對共用連接埠的應用程式不支援多個憑證」。</span><span class="sxs-lookup"><span data-stu-id="fa974-234">If you see an upgrade fail with https, an error warning saying "The Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="fa974-235">完整的應用程式資訊清單範例</span><span class="sxs-lookup"><span data-stu-id="fa974-235">A complete application manifest example</span></span>
<span data-ttu-id="fa974-236">下列應用程式資訊清單顯示許多不同的設定：</span><span class="sxs-lookup"><span data-stu-id="fa974-236">The following application manifest shows many of the different settings:</span></span>

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
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed the EndpointName is secured with https -->
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


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="fa974-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa974-237">Next steps</span></span>
* [<span data-ttu-id="fa974-238">了解應用程式模型</span><span class="sxs-lookup"><span data-stu-id="fa974-238">Understand the application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="fa974-239">在服務資訊清單中指定資源</span><span class="sxs-lookup"><span data-stu-id="fa974-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="fa974-240">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="fa974-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
