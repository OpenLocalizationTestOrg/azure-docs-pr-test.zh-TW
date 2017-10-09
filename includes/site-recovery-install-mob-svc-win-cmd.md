1. <span data-ttu-id="5dcf1-101">您想 tooprotect hello 伺服器上複製 hello installer tooa 本機資料夾 (例如 C:\Temp)。</span><span class="sxs-lookup"><span data-stu-id="5dcf1-101">Copy hello installer tooa local folder (for example, C:\Temp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="5dcf1-102">執行下列命令，以系統管理員身分在命令提示字元的 hello:</span><span class="sxs-lookup"><span data-stu-id="5dcf1-102">Run hello following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="5dcf1-103">執行下列命令的 hello tooinstall 行動服務：</span><span class="sxs-lookup"><span data-stu-id="5dcf1-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="5dcf1-104">現在 hello 代理程式必須向組態伺服器 hello toobe。</span><span class="sxs-lookup"><span data-stu-id="5dcf1-104">Now hello agent needs toobe registered with hello Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="5dcf1-105">行動服務安裝程式命令列引數</span><span class="sxs-lookup"><span data-stu-id="5dcf1-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="5dcf1-106">參數</span><span class="sxs-lookup"><span data-stu-id="5dcf1-106">Parameter</span></span>|<span data-ttu-id="5dcf1-107">類型</span><span class="sxs-lookup"><span data-stu-id="5dcf1-107">Type</span></span>|<span data-ttu-id="5dcf1-108">說明</span><span class="sxs-lookup"><span data-stu-id="5dcf1-108">Description</span></span>|<span data-ttu-id="5dcf1-109">可能的值</span><span class="sxs-lookup"><span data-stu-id="5dcf1-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="5dcf1-110">/Role</span><span class="sxs-lookup"><span data-stu-id="5dcf1-110">/Role</span></span>|<span data-ttu-id="5dcf1-111">強制</span><span class="sxs-lookup"><span data-stu-id="5dcf1-111">Mandatory</span></span>|<span data-ttu-id="5dcf1-112">指定應該安裝行動服務 (MS) 或主要目標 (MT)</span><span class="sxs-lookup"><span data-stu-id="5dcf1-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="5dcf1-113">MS</span><span class="sxs-lookup"><span data-stu-id="5dcf1-113">MS</span></span> </br> <span data-ttu-id="5dcf1-114">MT</span><span class="sxs-lookup"><span data-stu-id="5dcf1-114">MT</span></span>|
|<span data-ttu-id="5dcf1-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="5dcf1-115">/InstallLocation</span></span>|<span data-ttu-id="5dcf1-116">選用</span><span class="sxs-lookup"><span data-stu-id="5dcf1-116">Optional</span></span>|<span data-ttu-id="5dcf1-117">行動服務的安裝位置</span><span class="sxs-lookup"><span data-stu-id="5dcf1-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="5dcf1-118">Hello 電腦上的任何資料夾</span><span class="sxs-lookup"><span data-stu-id="5dcf1-118">Any folder on hello computer</span></span>|
|<span data-ttu-id="5dcf1-119">/Platform</span><span class="sxs-lookup"><span data-stu-id="5dcf1-119">/Platform</span></span>|<span data-ttu-id="5dcf1-120">強制</span><span class="sxs-lookup"><span data-stu-id="5dcf1-120">Mandatory</span></span>|<span data-ttu-id="5dcf1-121">指定取得哪些 hello 安裝行動服務的 hello 平台</span><span class="sxs-lookup"><span data-stu-id="5dcf1-121">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="5dcf1-122">- **VMware**︰如果您要在「VMware vSphere ESXi 主機」、「Hyper-V 主機」和「實體伺服器」上執行的 VM 上安裝行動服務，請使用此值</span><span class="sxs-lookup"><span data-stu-id="5dcf1-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="5dcf1-123">- **Azure**︰如果您要在 Azure IaaS VM 上安裝代理程式，請使用此值</span><span class="sxs-lookup"><span data-stu-id="5dcf1-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="5dcf1-124">VMware</span><span class="sxs-lookup"><span data-stu-id="5dcf1-124">VMware</span></span> </br> <span data-ttu-id="5dcf1-125">Azure</span><span class="sxs-lookup"><span data-stu-id="5dcf1-125">Azure</span></span>|
|<span data-ttu-id="5dcf1-126">/Silent</span><span class="sxs-lookup"><span data-stu-id="5dcf1-126">/Silent</span></span>|<span data-ttu-id="5dcf1-127">選用</span><span class="sxs-lookup"><span data-stu-id="5dcf1-127">Optional</span></span>|<span data-ttu-id="5dcf1-128">指定 toorun hello 安裝程式以無訊息模式</span><span class="sxs-lookup"><span data-stu-id="5dcf1-128">Specifies toorun hello installer in silent mode</span></span>| <span data-ttu-id="5dcf1-129">NA</span><span class="sxs-lookup"><span data-stu-id="5dcf1-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="5dcf1-130">您可以找到 %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log hello 安裝程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="5dcf1-130">hello setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="5dcf1-131">行動服務註冊命令列引數</span><span class="sxs-lookup"><span data-stu-id="5dcf1-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="5dcf1-132">參數</span><span class="sxs-lookup"><span data-stu-id="5dcf1-132">Parameter</span></span>|<span data-ttu-id="5dcf1-133">類型</span><span class="sxs-lookup"><span data-stu-id="5dcf1-133">Type</span></span>|<span data-ttu-id="5dcf1-134">說明</span><span class="sxs-lookup"><span data-stu-id="5dcf1-134">Description</span></span>|<span data-ttu-id="5dcf1-135">可能的值</span><span class="sxs-lookup"><span data-stu-id="5dcf1-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="5dcf1-136">/CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="5dcf1-136">/CSEndPoint</span></span> |<span data-ttu-id="5dcf1-137">強制</span><span class="sxs-lookup"><span data-stu-id="5dcf1-137">Mandatory</span></span>|<span data-ttu-id="5dcf1-138">Hello 組態伺服器 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5dcf1-138">IP address of hello configuration server</span></span>| <span data-ttu-id="5dcf1-139">任何有效的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5dcf1-139">Any valid IP address</span></span>|
  |<span data-ttu-id="5dcf1-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="5dcf1-140">/PassphraseFilePath</span></span>|<span data-ttu-id="5dcf1-141">強制</span><span class="sxs-lookup"><span data-stu-id="5dcf1-141">Mandatory</span></span>|<span data-ttu-id="5dcf1-142">Hello 複雜密碼的位置</span><span class="sxs-lookup"><span data-stu-id="5dcf1-142">Location of hello passphrase</span></span> |<span data-ttu-id="5dcf1-143">任何有效的 UNC 或本機檔案路徑</span><span class="sxs-lookup"><span data-stu-id="5dcf1-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="5dcf1-144">您可以找到 %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log hello AgentConfiguration 記錄檔</span><span class="sxs-lookup"><span data-stu-id="5dcf1-144">hello AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
