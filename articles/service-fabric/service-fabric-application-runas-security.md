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
# <a name="configure-security-policies-for-your-application"></a>設定應用程式的安全性原則
藉由使用 Azure Service Fabric，您可以保護在 hello 叢集中不同的使用者帳戶下執行的應用程式。 Service Fabric 也有助於安全 hello 資源所使用的應用程式中的 hello 使用者帳戶-部署的 hello 時段，例如、 檔案、 目錄和憑證。 如此一來，即使在共用主控環境中，執行中的應用程式就不會彼此干擾。

根據預設，Service Fabric 應用程式是 hello hello Fabric.exe 程序執行的帳戶下執行。 Service Fabric 還提供 hello 功能 toorun 本機使用者帳戶或本機系統帳戶，hello 應用程式資訊清單內所指定的應用程式。 支援的本機系統帳戶類型為 **LocalUser**、**NetworkService**、**LocalService** 和 **LocalSystem**。

 如果您執行 Service Fabric Windows 伺服器上資料中心內使用 hello 獨立安裝程式，您可以使用 Active Directory 網域帳戶，包括群組受管理的服務帳戶。

您可以定義和建立使用者群組，以便新增一或多個使用者 tooeach 群組 toobe 一起管理。 有多個不同的服務進入點的使用者，且需要 toohave hello 群組層級的特定一般權限時，這非常有用。

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a>設定服務安裝程式的進入點的 hello 原則
Hello 中所述[應用程式模型](service-fabric-application-model.md)，hello 安裝進入點， **SetupEntryPoint**，是以 hello 相同認證為 Service Fabric 執行特殊權限的進入點 (通常 hello *NetworkService*帳戶) 之前的任何其他的進入點。 hello 可執行檔所指定**EntryPoint**通常是 hello 長時間執行的服務主機。 因此需要個別安裝程式的進入點，可避免 toorun hello 服務主機以高的權限可執行需要很長的時間。 hello 可執行檔的**EntryPoint**指定執行**SetupEntryPoint**成功結束。 hello 產生處理序監視，並重新啟動，並重新開始**SetupEntryPoint**如果曾結束，或當機。

hello 以下是簡單的服務資訊清單並的範例，顯示 hello SetupEntryPoint hello hello 服務的主要進入點。

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

### <a name="configure-hello-policy-by-using-a-local-account"></a>使用本機帳戶設定 hello 原則
設定 hello 服務 toohave 安裝進入點之後，您可以變更下執行 hello 應用程式資訊清單中的 hello 安全性權限。 hello 下列範例顯示如何 tooconfigure hello 服務 toorun 使用者系統管理員帳戶權限。

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

首先，以使用者名稱 (例如 SetupAdminUser) 建立 **Principals** 區段。 這表示該 hello 使用者 hello Administrators 群組成員的系統。

下一步 在 hello **ServiceManifestImport**區段中，設定原則 tooapply 這個主體太**SetupEntryPoint**。 這會告知 Service Fabric，當 hello **MySetup.bat**執行檔，應該是`RunAs`系統管理員權限。 假設您有*不*套用原則 toohello 主要進入點、 hello 中的程式碼**MyServiceHost.exe** hello 系統下執行**NetworkService**帳戶。 這是服務的所有進入點都執行身分的 hello 預設帳戶。

讓我們現在加入 hello 檔案 MySetup.bat toohello Visual Studio 專案 tootest hello 系統管理員權限。 在 Visual Studio 中，hello 服務專案上按一下滑鼠右鍵並加入新的檔案，稱為 MySetup.bat。

接下來，確定 hello 服務封裝中包含該 hello MySetup.bat 檔案。 預設不會包含該檔案。 選取 hello 檔案，以滑鼠右鍵按一下 tooget hello 操作功能表，然後選擇 **屬性**。 在 hello 內容 對話方塊中，確定**複製 tooOutput 目錄**設定得**更新時才複製**。 請參閱下列螢幕擷取畫面的 hello。

![Visual Studio CopyToOutput for SetupEntryPoint 批次檔][image1]

現在開啟 hello MySetup.bat 檔案，並加入下列命令的 hello:

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

接下來，建置和部署 hello 方案 tooa 本機開發叢集。 Hello 服務已啟動，Service Fabric 總管中所示之後，您可以看到該 hello MySetup.bat 檔案已成功在兩種方式。 開啟 PowerShell 命令提示字元並輸入：

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

然後，請注意 hello 節點名稱的 hello hello 服務部署，而在啟動 Service Fabric 總管-例如，節點 2。 接下來，瀏覽 toohello 應用程式執行個體的工作資料夾 toofind hello out.txt 檔案會顯示 hello 值**TestVariable**。 例如，如果此服務已部署的 tooNode 2，接著您可以移 hello toothis 路徑**MyApplicationType**:

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a>使用本機系統帳戶來設定 hello 原則
通常，它會使用本機系統帳戶，而不是系統管理員帳戶是最好的 toorun hello 啟動指令碼。 Hello Administrators 群組通常無法運作良好，因為電腦有使用者存取控制 (UAC) 預設啟用的成員身分執行 hello RunAs 原則。 在這種情況下， **hello 建議 toorun hello SetupEntryPoint 以 localsystem 身分，而不是以本機使用者新增的 tooAdministrators 群組**。 hello 下列範例示範設定 hello SetupEntryPoint toorun 以 localsystem 身分：

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>從安裝程式進入點啟動 PowerShell 命令
從 hello toorun PowerShell **SetupEntryPoint**點，您可以執行**PowerShell.exe**點 tooa PowerShell 批次檔中的檔案。 首先，比方說，新增 PowerShell 檔案 toohello 服務專案- **MySetup.ps1**。 請記住 tooset hello*更新時才複製*因此 hello 檔案也包含 hello 服務封裝中的屬性。 hello 下列範例示範的範例批次檔啟動 PowerShell 檔案呼叫 MySetup.ps1，設定系統環境變數，呼叫**TestVariable**。

MySetup.bat toostart PowerShell 檔案：

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

在 hello PowerShell 檔案中，加入下列 tooset 系統環境變數的 hello:

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> 根據預設，當 hello 批次檔執行時，它會查看 hello 應用程式資料夾，稱為**運作**檔案。 在此情況下，當 MySetup.bat 執行時，我們想要這個 toofind hello MySetup.ps1 檔案 hello 中相同資料夾中，也就是 hello 應用程式**程式碼封裝**資料夾。 toochange 這個資料夾、 組 hello 工作資料夾：
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

## <a name="use-console-redirection-for-local-debugging"></a>使用主控台重新導向進行本機偵錯
有時候，它會從執行的指令碼進行偵錯的有用 toosee hello 主控台輸出。 toodo，您可以設定將 hello 輸出 tooa 檔案寫入主控台重新導向原則。 hello 檔案輸出寫入的 toohello 應用程式資料夾稱為**記錄**其中 hello 應用程式是部署而執行的 hello 節點上。 (請參閱 where toofind 這 hello 前面範例中。)

> [!WARNING]
> 絕對不要使用的應用程式，因為這可能會影響 hello 應用程式容錯移轉，在生產環境中部署的 hello 主控台重新導向原則。 僅將此原則用於本機開發及偵錯。  
> 
> 

hello 下列範例示範設定 hello 主控台重新導向 FileRetentionCount 值：

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

如果您現在變更 hello MySetup.ps1 檔案 toowrite **Echo**命令時，這將會寫入 toohello 輸出檔，以進行偵錯：

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

**您為您的指令碼偵錯之後，請立即移除這個主控台重新導向原則**。

## <a name="configure-a-policy-for-service-code-packages"></a>設定服務程式碼封裝的原則
在 hello 先前步驟中，您已看到如何 tooapply RunAs 原則 tooSetupEntryPoint。 讓我們來看更到 toocreate 不同主體可以當做套用服務原則的方式。

### <a name="create-local-user-groups"></a>建立本機使用者群組
您可以定義和建立使用者群組，可讓一或多個使用者 toobe 加入 tooa 群組。 如果有多個不同的服務進入點的使用者，而且他們需要 toohave hello 群組層級的特定一般權限，這非常有用。 hello 下列範例將示範名為的本機群組**LocalAdminGroup**具有系統管理員權限。 Customer1 和 Customer2 這兩個使用者會成為此本機群組的成員。

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

### <a name="create-local-users"></a>建立本機使用者
您可以建立本機使用者可以安全使用的 toohelp hello 應用程式內的服務。 當**LocalUser**帳戶類型指定在 hello 主體區段 hello 應用程式資訊清單中，Service Fabric hello 應用程式部署所在的電腦上建立本機使用者帳戶。 根據預設，這些帳戶沒有的 hello 與 hello 應用程式中所指定的相同名稱的資訊清單 （例如，在下列範例中的 hello Customer3）。 相反地，它們會動態產生並具有隨機密碼。

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

如果應用程式需要 hello 使用者帳戶和密碼是相同的所有電腦 （例如，tooenable NTLM 驗證） 上，hello 叢集資訊清單必須設定 NTLMAuthenticationEnabled tootrue。 hello 叢集資訊清單也必須指定使用 NTLMAuthenticationPasswordSecret toogenerate hello 相同的密碼在所有機器上。

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a>指派原則 toohello 服務程式碼封裝
hello **RunAsPolicy**區段**ServiceManifestImport**指定應該使用的 toorun 程式碼封裝的 hello 主體區段中的 hello 帳戶。 它也將封裝從 hello 服務資訊清單的程式碼與 hello 主體區段中的使用者帳戶產生關聯。 您可以指定此 hello 安裝程式或主要進入點，或者您可以指定`All`tooapply 它 tooboth。 hello 下列範例顯示不同的原則套用：

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

如果**EntryPointType**未指定，hello 預設設 tooEntryPointType ="Main"。 指定**SetupEntryPoint** ，特別適用於您想要 toorun 系統帳戶下的某些高特殊權限安裝程式作業。 hello 實際服務程式碼可以在較低權限的帳戶下執行。

### <a name="apply-a-default-policy-tooall-service-code-packages"></a>套用預設原則 tooall 服務程式碼封裝
使用 hello **DefaultRunAsPolicy**區段 toospecify 預設使用者帳戶沒有特定的所有程式碼封裝**RunAsPolicy**定義。 如果大部分的 hello hello 應用程式所使用的服務資訊清單中指定的程式碼封裝需要下的 toorun hello 相同的使用者，hello 應用程式就可以定義預設 RunAs 原則以該使用者帳戶。 hello 下列範例會指定如果程式碼封裝沒有**RunAsPolicy**指定，hello 程式碼封裝執行的 hello **MyDefaultAccount** hello 主體區段中指定。

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>使用 Active Directory 網域群組或使用者
使用 hello 獨立安裝程式在 Windows Server 已安裝的 Service Fabric 執行個體，您可以執行 Active Directory 使用者或群組帳戶 hello credentials hello 服務。 這是在您網域內的內部部署 Active Directory，與 Azure Active Directory (Azure AD) 無關。 使用網域使用者或群組，然後您可以存取其他資源 （例如，檔案共用） 的 hello 網域中已授與權限。

hello 下列範例會示範呼叫的 Active Directory 使用者*TestUser*其網域使用憑證來加密的密碼稱為*MyCert*。 您可以使用 hello `Invoke-ServiceFabricEncryptText` PowerShell 命令 toocreate hello 密碼的加密文字。 如需詳細資訊，請參閱[管理 Service Fabric 應用程式中的密碼](service-fabric-application-secret-management.md)。

您必須將 hello 私密金鑰 hello 憑證 toodecrypt hello 密碼 toohello 本機電腦的部署使用不足的頻外方法 （在 Azure 中，這是透過 Azure Resource Manager）。 然後，當 Service Fabric 部署 hello 服務封裝 toohello 電腦，是無法 toodecrypt hello 密碼，並且使用 Active Directory toorun 下這些認證進行驗證 （以及 hello 使用者名稱）。

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
### <a name="use-a-group-managed-service-account"></a>使用群組受管理服務帳戶。
Windows Server 使用 hello 獨立安裝程式已安裝的 Service Fabric 執行個體，您可以執行 hello 服務當做群組受管理的服務帳戶 (gMSA)。 注意︰這是您的網域內部部署的 Active Directory，與 Azure Active Directory (Azure AD) 無關。 使用 gMSA 中，沒有任何密碼或加密的密碼儲存在 hello `Application Manifest`。

hello 下列範例顯示如何 toocreate gMSA 帳戶呼叫*svc 測試 $*; 如何 toodeploy 管理的服務帳戶 toohello 叢集節點，和如何 tooconfigure hello 使用者主體。

##### <a name="prerequisites"></a>必要條件。
- hello 網域必須 KDS 根金鑰。
- 需要在 Windows Server 2012 或更新版本的功能層級 toobe hello 網域。

##### <a name="example"></a>範例
1. 已建立群組受管理的服務帳戶使用 hello active directory 網域管理員`New-ADServiceAccount`指令程式，並確保該 hello`PrincipalsAllowedToRetrieveManagedPassword`包含所有 hello service fabric 叢集節點。 請注意，`AccountName`、`DnsHostName` 和 `ServicePrincipalName` 必須是唯一的。
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. 每個 hello service fabric 叢集節點上 (例如， `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`)、 安裝和測試 hello gMSA。
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. 設定 hello 使用者主體，並設定 hello RunAsPolicy tooreference hello 使用者。
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a>為 HTTP 和 HTTPS 端點指派安全性存取原則
如果您套用 RunAs 原則 tooa 服務以及 hello 服務資訊清單宣告使用 hello HTTP 通訊協定的端點資源，您必須指定**SecurityAccessPolicy** tooensure 連接埠配置 toothese 端點可正常存取控制列 hello 服務執行的 RunAs 使用者帳戶。 否則， **http.sys**沒有存取 toohello 服務，並呼叫失敗收到 hello 用戶端。 hello 下列範例會套用 hello Customer1 帳戶 tooan 端點呼叫**EndpointName**，讓它的完整存取權限。

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Hello HTTPS 端點，您也可以 tooindicate hello hello 憑證 tooreturn toohello 用戶端名稱。 您可以使用**EndpointBindingPolicy**，hello hello 應用程式資訊清單中的憑證 > 一節中所定義的憑證。

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>使用 https 端點來升級多個應用程式
您需要小心 toobe 不 toouse hello**相同的連接埠**hello 的不同執行個體相同的應用程式使用 http 時**s**。 hello 原因是 Service Fabric 無法能 tooupgrade hello 憑證之其中一個 hello 應用程式執行個體。 例如，如果應用程式 1 或應用程式 2 同時想 tooupgrade 其 cert 1 toocert 2。 Hello 升級發生失敗時，Service Fabric 可能清除 hello cert 1 註冊 http.sys 即使 hello 其他應用程式仍在使用它。 tooprevent，Service Fabric 偵測到已經有另一個 hello hello 憑證的通訊埠上註冊的應用程式執行個體 (因為 toohttp.sys) 和失敗 hello 作業。

因此 Service Fabric 不支援升級兩個不同的服務使用**hello 相同的連接埠**中不同的應用程式執行個體。 換句話說，您不能使用相同憑證的 hello 在 hello 上的不同服務相同的連接埠。 如果您需要 toohave 共用憑證在 hello 相同連接埠，您需要該服務位於不同位置條件約束使用的電腦的 hello tooensure。 或者，可能的話，考慮針對每個應用程式執行個體中的每個服務，使用 Service Fabric 動態連接埠。 

如果您看到使用 https，升級失敗錯誤警告，指出 「 hello Windows HTTP 伺服器 API 不支援多個憑證共用連接埠的應用程式。 」

## <a name="a-complete-application-manifest-example"></a>完整的應用程式資訊清單範例
下列應用程式資訊清單的 hello 顯示 hello 的許多不同的設定：

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
## <a name="next-steps"></a>後續步驟
* [了解 hello 應用程式模型](service-fabric-application-model.md)
* [在服務資訊清單中指定資源](service-fabric-service-manifest-resources.md)
* [部署應用程式](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
