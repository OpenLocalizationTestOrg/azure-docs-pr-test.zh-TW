1. <span data-ttu-id="94109-101">將複製 hello installer tooa 本機資料夾 (例如，tec_rule 位於 /tmp) 您想 tooprotect hello 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="94109-101">Copy hello installer tooa local folder (for example, /tmp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="94109-102">在終端機中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="94109-102">In a terminal, run hello following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="94109-103">執行下列命令的 hello tooinstall 行動服務：</span><span class="sxs-lookup"><span data-stu-id="94109-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="94109-104">安裝完成之後，hello 行動服務需要 tooget toohello 註冊的組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="94109-104">Once installation is complete, hello Mobility Service needs tooget registered toohello configuration server.</span></span> <span data-ttu-id="94109-105">執行下列命令 tooregister hello 行動服務使用組態伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="94109-105">Run hello following command tooregister hello Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="94109-106">行動服務安裝程式命令列</span><span class="sxs-lookup"><span data-stu-id="94109-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="94109-107">參數</span><span class="sxs-lookup"><span data-stu-id="94109-107">Parameter</span></span>|<span data-ttu-id="94109-108">類型</span><span class="sxs-lookup"><span data-stu-id="94109-108">Type</span></span>|<span data-ttu-id="94109-109">說明</span><span class="sxs-lookup"><span data-stu-id="94109-109">Description</span></span>|<span data-ttu-id="94109-110">可能的值</span><span class="sxs-lookup"><span data-stu-id="94109-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="94109-111">-r</span><span class="sxs-lookup"><span data-stu-id="94109-111">-r</span></span> |<span data-ttu-id="94109-112">強制</span><span class="sxs-lookup"><span data-stu-id="94109-112">Mandatory</span></span>|<span data-ttu-id="94109-113">指定應該安裝行動服務 (MS) 或主要目標 (MT)</span><span class="sxs-lookup"><span data-stu-id="94109-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="94109-114">MS</span><span class="sxs-lookup"><span data-stu-id="94109-114">MS</span></span> </br> <span data-ttu-id="94109-115">MT</span><span class="sxs-lookup"><span data-stu-id="94109-115">MT</span></span>|
|<span data-ttu-id="94109-116">-d</span><span class="sxs-lookup"><span data-stu-id="94109-116">-d</span></span> |<span data-ttu-id="94109-117">選用</span><span class="sxs-lookup"><span data-stu-id="94109-117">Optional</span></span>|<span data-ttu-id="94109-118">將要安裝行動服務的位置</span><span class="sxs-lookup"><span data-stu-id="94109-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="94109-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="94109-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="94109-120">-v</span><span class="sxs-lookup"><span data-stu-id="94109-120">-v</span></span>|<span data-ttu-id="94109-121">強制</span><span class="sxs-lookup"><span data-stu-id="94109-121">Mandatory</span></span>|<span data-ttu-id="94109-122">指定取得哪些 hello 安裝行動服務的 hello 平台</span><span class="sxs-lookup"><span data-stu-id="94109-122">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="94109-123">- **VMware**︰如果您要在「VMware vSphere ESXi 主機」、「Hyper-V 主機」和「實體伺服器」上執行的 VM 上安裝行動服務，請使用此值</span><span class="sxs-lookup"><span data-stu-id="94109-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="94109-124">- **Azure**︰如果您要在 Azure IaaS VM 上安裝代理程式，請使用此值</span><span class="sxs-lookup"><span data-stu-id="94109-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="94109-125">VMware</span><span class="sxs-lookup"><span data-stu-id="94109-125">VMware</span></span> </br> <span data-ttu-id="94109-126">Azure</span><span class="sxs-lookup"><span data-stu-id="94109-126">Azure</span></span>|
|<span data-ttu-id="94109-127">-q</span><span class="sxs-lookup"><span data-stu-id="94109-127">-q</span></span>|<span data-ttu-id="94109-128">選用</span><span class="sxs-lookup"><span data-stu-id="94109-128">Optional</span></span>|<span data-ttu-id="94109-129">指定 toorun 安裝程式以無訊息模式</span><span class="sxs-lookup"><span data-stu-id="94109-129">Specifies toorun installer in silent mode</span></span>| <span data-ttu-id="94109-130">N/A</span><span class="sxs-lookup"><span data-stu-id="94109-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="94109-131">行動服務設定命令列</span><span class="sxs-lookup"><span data-stu-id="94109-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="94109-132">參數</span><span class="sxs-lookup"><span data-stu-id="94109-132">Parameter</span></span>|<span data-ttu-id="94109-133">類型</span><span class="sxs-lookup"><span data-stu-id="94109-133">Type</span></span>|<span data-ttu-id="94109-134">說明</span><span class="sxs-lookup"><span data-stu-id="94109-134">Description</span></span>|<span data-ttu-id="94109-135">可能的值</span><span class="sxs-lookup"><span data-stu-id="94109-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="94109-136">-i</span><span class="sxs-lookup"><span data-stu-id="94109-136">-i</span></span> |<span data-ttu-id="94109-137">強制</span><span class="sxs-lookup"><span data-stu-id="94109-137">Mandatory</span></span>|<span data-ttu-id="94109-138">Hello 組態伺服器的 IP</span><span class="sxs-lookup"><span data-stu-id="94109-138">IP of hello Configuration Server</span></span>|<span data-ttu-id="94109-139">任何有效的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="94109-139">Any valid IP Address</span></span>|
|<span data-ttu-id="94109-140">-P</span><span class="sxs-lookup"><span data-stu-id="94109-140">-P</span></span> |<span data-ttu-id="94109-141">強制</span><span class="sxs-lookup"><span data-stu-id="94109-141">Mandatory</span></span>|<span data-ttu-id="94109-142">Hello 連接複雜密碼的儲存位置的完整檔案路徑 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="94109-142">Full file path hello file where hello connection passphrase is saved</span></span>|<span data-ttu-id="94109-143">任何有效的資料夾</span><span class="sxs-lookup"><span data-stu-id="94109-143">Any valid folder</span></span>|
