1. <span data-ttu-id="61d22-101">將安裝程式複製到您想要保護之伺服器上的本機資料夾 (例如 /tmp)。</span><span class="sxs-lookup"><span data-stu-id="61d22-101">Copy the installer to a local folder (for example, /tmp) on the server that you want to protect.</span></span> <span data-ttu-id="61d22-102">在終端機中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="61d22-102">In a terminal, run the following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="61d22-103">若要安裝行動服務，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="61d22-103">To install Mobility Service, run the following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="61d22-104">安裝完成後，行動服務必須向設定伺服器註冊。</span><span class="sxs-lookup"><span data-stu-id="61d22-104">Once installation is complete, the Mobility Service needs to get registered to the configuration server.</span></span> <span data-ttu-id="61d22-105">執行下列命令來向設定伺服器註冊行動服務。</span><span class="sxs-lookup"><span data-stu-id="61d22-105">Run the following command to register the Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="61d22-106">行動服務安裝程式命令列</span><span class="sxs-lookup"><span data-stu-id="61d22-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="61d22-107">參數</span><span class="sxs-lookup"><span data-stu-id="61d22-107">Parameter</span></span>|<span data-ttu-id="61d22-108">類型</span><span class="sxs-lookup"><span data-stu-id="61d22-108">Type</span></span>|<span data-ttu-id="61d22-109">說明</span><span class="sxs-lookup"><span data-stu-id="61d22-109">Description</span></span>|<span data-ttu-id="61d22-110">可能的值</span><span class="sxs-lookup"><span data-stu-id="61d22-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="61d22-111">-r</span><span class="sxs-lookup"><span data-stu-id="61d22-111">-r</span></span> |<span data-ttu-id="61d22-112">強制</span><span class="sxs-lookup"><span data-stu-id="61d22-112">Mandatory</span></span>|<span data-ttu-id="61d22-113">指定應該安裝行動服務 (MS) 或主要目標 (MT)</span><span class="sxs-lookup"><span data-stu-id="61d22-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="61d22-114">MS</span><span class="sxs-lookup"><span data-stu-id="61d22-114">MS</span></span> </br> <span data-ttu-id="61d22-115">MT</span><span class="sxs-lookup"><span data-stu-id="61d22-115">MT</span></span>|
|<span data-ttu-id="61d22-116">-d</span><span class="sxs-lookup"><span data-stu-id="61d22-116">-d</span></span> |<span data-ttu-id="61d22-117">選用</span><span class="sxs-lookup"><span data-stu-id="61d22-117">Optional</span></span>|<span data-ttu-id="61d22-118">將要安裝行動服務的位置</span><span class="sxs-lookup"><span data-stu-id="61d22-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="61d22-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="61d22-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="61d22-120">-v</span><span class="sxs-lookup"><span data-stu-id="61d22-120">-v</span></span>|<span data-ttu-id="61d22-121">強制</span><span class="sxs-lookup"><span data-stu-id="61d22-121">Mandatory</span></span>|<span data-ttu-id="61d22-122">指定要安裝行動服務的平台</span><span class="sxs-lookup"><span data-stu-id="61d22-122">Specifies the platform on which the Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="61d22-123">- **VMware**︰如果您要在「VMware vSphere ESXi 主機」、「Hyper-V 主機」和「實體伺服器」上執行的 VM 上安裝行動服務，請使用此值</span><span class="sxs-lookup"><span data-stu-id="61d22-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="61d22-124">- **Azure**︰如果您要在 Azure IaaS VM 上安裝代理程式，請使用此值</span><span class="sxs-lookup"><span data-stu-id="61d22-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="61d22-125">VMware</span><span class="sxs-lookup"><span data-stu-id="61d22-125">VMware</span></span> </br> <span data-ttu-id="61d22-126">Azure</span><span class="sxs-lookup"><span data-stu-id="61d22-126">Azure</span></span>|
|<span data-ttu-id="61d22-127">-q</span><span class="sxs-lookup"><span data-stu-id="61d22-127">-q</span></span>|<span data-ttu-id="61d22-128">選用</span><span class="sxs-lookup"><span data-stu-id="61d22-128">Optional</span></span>|<span data-ttu-id="61d22-129">指定要以無訊息模式執行安裝程式</span><span class="sxs-lookup"><span data-stu-id="61d22-129">Specifies to run installer in silent mode</span></span>| <span data-ttu-id="61d22-130">N/A</span><span class="sxs-lookup"><span data-stu-id="61d22-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="61d22-131">行動服務設定命令列</span><span class="sxs-lookup"><span data-stu-id="61d22-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="61d22-132">參數</span><span class="sxs-lookup"><span data-stu-id="61d22-132">Parameter</span></span>|<span data-ttu-id="61d22-133">類型</span><span class="sxs-lookup"><span data-stu-id="61d22-133">Type</span></span>|<span data-ttu-id="61d22-134">說明</span><span class="sxs-lookup"><span data-stu-id="61d22-134">Description</span></span>|<span data-ttu-id="61d22-135">可能的值</span><span class="sxs-lookup"><span data-stu-id="61d22-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="61d22-136">-i</span><span class="sxs-lookup"><span data-stu-id="61d22-136">-i</span></span> |<span data-ttu-id="61d22-137">強制</span><span class="sxs-lookup"><span data-stu-id="61d22-137">Mandatory</span></span>|<span data-ttu-id="61d22-138">設定伺服器的 IP</span><span class="sxs-lookup"><span data-stu-id="61d22-138">IP of the Configuration Server</span></span>|<span data-ttu-id="61d22-139">任何有效的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="61d22-139">Any valid IP Address</span></span>|
|<span data-ttu-id="61d22-140">-P</span><span class="sxs-lookup"><span data-stu-id="61d22-140">-P</span></span> |<span data-ttu-id="61d22-141">強制</span><span class="sxs-lookup"><span data-stu-id="61d22-141">Mandatory</span></span>|<span data-ttu-id="61d22-142">儲存連線複雜密碼知檔案的完整檔案路徑</span><span class="sxs-lookup"><span data-stu-id="61d22-142">Full file path the file where the connection passphrase is saved</span></span>|<span data-ttu-id="61d22-143">任何有效的資料夾</span><span class="sxs-lookup"><span data-stu-id="61d22-143">Any valid folder</span></span>|
