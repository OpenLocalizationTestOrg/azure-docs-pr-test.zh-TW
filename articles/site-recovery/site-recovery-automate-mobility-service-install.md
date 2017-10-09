---
title: "aaaDeploy hello 向 Azure 自動化 DSC 的站台復原行動服務 |Microsoft 文件"
description: "描述如何 toouse Azure Automation DSC tooautomatically 部署 hello Azure 站台復原行動服務和 Azure 代理程式適用於 VMware VM 和實體伺服器複寫 tooAzure"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="465f3-103">部署與 Azure Automation DSC 的 VM 複寫的 hello 行動服務</span><span class="sxs-lookup"><span data-stu-id="465f3-103">Deploy hello Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="465f3-104">在 Operations Management Suite 中，我們提供您一個全方位的備份和災害復原解決方案，可供您融入到您的商務持續性計畫中。</span><span class="sxs-lookup"><span data-stu-id="465f3-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="465f3-105">我們使用「Hyper-V 複本」來與 Hyper-V 一起展開這個旅程。</span><span class="sxs-lookup"><span data-stu-id="465f3-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="465f3-106">但是，我們將展開的 toosupport 有異質的安裝程式，因為客戶在其雲端中有多個 hypervisor 和平台。</span><span class="sxs-lookup"><span data-stu-id="465f3-106">But we have expanded toosupport a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="465f3-107">如果目前正在執行 VMware 的工作負載和 （或） 實體伺服器，管理伺服器執行所有 hello Azure Site Recovery 元件在您的環境 toohandle hello 通訊和資料複寫有了 Azure，Azure 時您的目的地。</span><span class="sxs-lookup"><span data-stu-id="465f3-107">If you are running VMware workloads and/or physical servers today, a management server runs all of hello Azure Site Recovery components in your environment toohandle hello communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="465f3-108">使用 Automation DSC 部署 hello 站台復原行動服務</span><span class="sxs-lookup"><span data-stu-id="465f3-108">Deploy hello Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="465f3-109">讓我們從快速分析此管理伺服器的作用著手︰</span><span class="sxs-lookup"><span data-stu-id="465f3-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="465f3-110">hello 管理伺服器會執行數個伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="465f3-110">hello management server runs several server roles.</span></span> <span data-ttu-id="465f3-111">其中一個角色是「組態」 ，負責協調通訊及管理資料複寫與復原程序。</span><span class="sxs-lookup"><span data-stu-id="465f3-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="465f3-112">此外，hello*程序*角色做為複寫閘道。</span><span class="sxs-lookup"><span data-stu-id="465f3-112">In addition, hello *process* role acts as a replication gateway.</span></span> <span data-ttu-id="465f3-113">這個角色接收複寫資料從受保護的來源機器、 最佳化與快取、 壓縮和加密，並再將它傳送 tooan Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="465f3-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it tooan Azure storage account.</span></span> <span data-ttu-id="465f3-114">其中一個 hello 處理角色的 hello 函式也 hello 行動服務 tooprotected 機器 toopush 安裝並執行的 VMware Vm 的自動探索。</span><span class="sxs-lookup"><span data-stu-id="465f3-114">One of hello functions for hello process role is also toopush installation of hello Mobility service tooprotected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="465f3-115">如果沒有從 Azure 容錯回復，hello*主要目標*角色會處理 hello 複寫資料，這項作業的一部分。</span><span class="sxs-lookup"><span data-stu-id="465f3-115">If there's a failback from Azure, hello *master target* role will handle hello replication data as part of this operation.</span></span>

<span data-ttu-id="465f3-116">對於受保護的 hello 機器我們依賴 hello*行動服務*。</span><span class="sxs-lookup"><span data-stu-id="465f3-116">For hello protected machines, we rely on hello *Mobility service*.</span></span> <span data-ttu-id="465f3-117">此元件是已部署的 tooevery 機器 （VMware VM 或實體伺服器） 的 tooreplicate tooAzure。</span><span class="sxs-lookup"><span data-stu-id="465f3-117">This component is deployed tooevery machine (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="465f3-118">它會擷取 hello 機器上的資料寫入，並將它們轉送 toohello management server （處理序角色）。</span><span class="sxs-lookup"><span data-stu-id="465f3-118">It captures data writes on hello machine and forwards them toohello management server (process role).</span></span>

<span data-ttu-id="465f3-119">當您處理商務持續性時，很重要 toounderstand 牽涉到您的工作負載，您的基礎結構和 hello 元件。</span><span class="sxs-lookup"><span data-stu-id="465f3-119">When you're dealing with business continuity, it's important toounderstand your workloads, your infrastructure, and hello components involved.</span></span> <span data-ttu-id="465f3-120">您接著可以符合您的復原時間目標 (RTO) 和復原點目標 (RPO) 的 hello 需求。</span><span class="sxs-lookup"><span data-stu-id="465f3-120">You can then meet hello requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="465f3-121">在此情況下，hello 行動服務是金鑰 tooensuring 如您所預期，保護您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="465f3-121">In this context, hello Mobility service is key tooensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="465f3-122">因此，您要如何在某些 Operations Management Suite 元件的協助下，以最佳化的方式確保您有可靠的受保護設定？</span><span class="sxs-lookup"><span data-stu-id="465f3-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="465f3-123">這篇文章提供範例將示範如何使用 Azure 自動化預期狀態設定 (DSC)，以及站台復原，tooensure 的：</span><span class="sxs-lookup"><span data-stu-id="465f3-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, tooensure that:</span></span>

* <span data-ttu-id="465f3-124">hello 行動服務和 Azure VM 代理程式是您想 tooprotect 部署的 toohello Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="465f3-124">hello Mobility service and Azure VM agent are deployed toohello Windows machines that you want tooprotect.</span></span>
* <span data-ttu-id="465f3-125">hello 複寫目標 Azure 時，一律會執行 hello 行動服務和 Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="465f3-125">hello Mobility service and Azure VM agent are always running when Azure is hello replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="465f3-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="465f3-126">Prerequisites</span></span>
* <span data-ttu-id="465f3-127">儲存機制 toostore hello 必要設定</span><span class="sxs-lookup"><span data-stu-id="465f3-127">A repository toostore hello required setup</span></span>
* <span data-ttu-id="465f3-128">儲存機制 toostore hello 需要複雜密碼 tooregister 與 hello 管理伺服器</span><span class="sxs-lookup"><span data-stu-id="465f3-128">A repository toostore hello required passphrase tooregister with hello management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="465f3-129">系統會為每一部管理伺服器產生一個唯一的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="465f3-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="465f3-130">如果您正在 toodeploy 多部管理伺服器，您必須 tooensure 該 hello 正確複雜密碼儲存在 hello passphrase.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="465f3-130">If you are going toodeploy multiple management servers, you have tooensure that hello correct passphrase is stored in hello passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="465f3-131">Windows Management Framework (WMF) 5.0 hello tooenable 需保護 （Automation dsc 的需求） 的電腦上安裝</span><span class="sxs-lookup"><span data-stu-id="465f3-131">Windows Management Framework (WMF) 5.0 installed on hello machines that you want tooenable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="465f3-132">如果您想 toouse DSC 適用於 Windows 的電腦安裝 WMF 4.0，請參閱 hello 節[已中斷連線的環境中使用 DSC](## Use DSC in disconnected environments)。</span><span class="sxs-lookup"><span data-stu-id="465f3-132">If you want toouse DSC for Windows machines that have WMF 4.0 installed, see hello section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="465f3-133">hello 行動服務可透過 hello 命令列安裝，並接受數個引數。</span><span class="sxs-lookup"><span data-stu-id="465f3-133">hello Mobility service can be installed through hello command line and accepts several arguments.</span></span> <span data-ttu-id="465f3-134">這就是為什麼您需要 toohave hello 二進位檔 （解壓縮之後它們從您的安裝程式），並將其儲存在其中擷取這些使用 DSC 設定的地方。</span><span class="sxs-lookup"><span data-stu-id="465f3-134">That’s why you need toohave hello binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="465f3-135">步驟 1：擷取二進位檔</span><span class="sxs-lookup"><span data-stu-id="465f3-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="465f3-136">對於此設定，所需的 tooextract hello 檔案瀏覽 toohello 管理伺服器上下列目錄：</span><span class="sxs-lookup"><span data-stu-id="465f3-136">tooextract hello files that you need for this setup, browse toohello following directory on your management server:</span></span>

    <span data-ttu-id="465f3-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="465f3-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="465f3-138">在此資料夾中，您應該會看到具有下列名稱的 MSI 檔案：</span><span class="sxs-lookup"><span data-stu-id="465f3-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="465f3-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="465f3-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="465f3-140">使用下列命令 tooextract hello installer hello:</span><span class="sxs-lookup"><span data-stu-id="465f3-140">Use hello following command tooextract hello installer:</span></span>

    <span data-ttu-id="465f3-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="465f3-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="465f3-142">選取 所有檔案，並將它們傳送 tooa 壓縮 (zipped) 資料夾。</span><span class="sxs-lookup"><span data-stu-id="465f3-142">Select all files and send them tooa compressed (zipped) folder.</span></span>

<span data-ttu-id="465f3-143">您現在可以使用自動化 DSC，需要 tooautomate hello 安裝 hello 行動服務的 hello 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="465f3-143">You now have hello binaries that you need tooautomate hello setup of hello Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="465f3-144">複雜密碼</span><span class="sxs-lookup"><span data-stu-id="465f3-144">Passphrase</span></span>
<span data-ttu-id="465f3-145">接下來，您需要的 toodetermine 想 tooplace 這個 zip 壓縮的資料夾。</span><span class="sxs-lookup"><span data-stu-id="465f3-145">Next, you need toodetermine where you want tooplace this zipped folder.</span></span> <span data-ttu-id="465f3-146">您可以使用 Azure 儲存體帳戶，做為顯示更新的版本，toostore hello 複雜密碼所需的 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="465f3-146">You can use an Azure storage account, as shown later, toostore hello passphrase that you need for hello setup.</span></span> <span data-ttu-id="465f3-147">hello 代理程式接著會向 hello 管理伺服器 hello 程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="465f3-147">hello agent will then register with hello management server as part of hello process.</span></span>

<span data-ttu-id="465f3-148">您已部署的 hello 管理伺服器時所得的 hello 複雜密碼可以儲存為 passphrase.txt tooa 文字檔案。</span><span class="sxs-lookup"><span data-stu-id="465f3-148">hello passphrase that you got when you deployed hello management server can be saved tooa text file as passphrase.txt.</span></span>

<span data-ttu-id="465f3-149">Hello zip 的資料夾和 hello 複雜密碼放置於容器 hello Azure 儲存體帳戶中的專用。</span><span class="sxs-lookup"><span data-stu-id="465f3-149">Place both hello zipped folder and hello passphrase in a dedicated container in hello Azure storage account.</span></span>

![資料夾位置](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="465f3-151">如果您偏好 tookeep 共用上的這些檔案在網路上，您可以這樣做。</span><span class="sxs-lookup"><span data-stu-id="465f3-151">If you prefer tookeep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="465f3-152">您只需要 tooensure hello DSC 資源，稍後您將會使用有權存取，並可以取得 hello 安裝程式和複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="465f3-152">You just need tooensure that hello DSC resource that you will be using later has access and can get hello setup and passphrase.</span></span>

## <a name="step-2-create-hello-dsc-configuration"></a><span data-ttu-id="465f3-153">步驟 2： 建立 hello DSC 設定</span><span class="sxs-lookup"><span data-stu-id="465f3-153">Step 2: Create hello DSC configuration</span></span>
<span data-ttu-id="465f3-154">hello 安裝 WMF 5.0 而定。</span><span class="sxs-lookup"><span data-stu-id="465f3-154">hello setup depends on WMF 5.0.</span></span> <span data-ttu-id="465f3-155">Hello 機器 toosuccessfully 適用於透過自動化 DSC hello 組態，WMF 5.0 toobe 存在。</span><span class="sxs-lookup"><span data-stu-id="465f3-155">For hello machine toosuccessfully apply hello configuration through Automation DSC, WMF 5.0 needs toobe present.</span></span>

<span data-ttu-id="465f3-156">hello 環境會使用下列範例 DSC 組態中的 hello:</span><span class="sxs-lookup"><span data-stu-id="465f3-156">hello environment uses hello following example DSC configuration:</span></span>

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
<span data-ttu-id="465f3-157">hello 組態將會執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="465f3-157">hello configuration will do hello following:</span></span>

* <span data-ttu-id="465f3-158">hello 變數會告訴 hello 組態將 tooget hello 複雜密碼，而其中 toostore hello 輸出 tooget hello hello 行動服務與 hello Azure VM 代理程式，二進位檔的位置。</span><span class="sxs-lookup"><span data-stu-id="465f3-158">hello variables will tell hello configuration where tooget hello binaries for hello Mobility service and hello Azure VM agent, where tooget hello passphrase, and where toostore hello output.</span></span>
* <span data-ttu-id="465f3-159">hello 組態將會匯入 hello xPSDesiredStateConfiguration DSC 資源，好讓您可以使用`xRemoteFile`toodownload hello 檔案從 hello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="465f3-159">hello configuration will import hello xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` toodownload hello files from hello repository.</span></span>
* <span data-ttu-id="465f3-160">hello 組態會建立您想要 toostore hello 二進位檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="465f3-160">hello configuration will create a directory where you want toostore hello binaries.</span></span>
* <span data-ttu-id="465f3-161">hello 封存資源會從 hello 壓縮資料夾解壓縮 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="465f3-161">hello archive resource will extract hello files from hello zipped folder.</span></span>
* <span data-ttu-id="465f3-162">hello 套件安裝資源將會從 hello UNIFIEDAGENT 安裝 hello 行動服務。EXE 安裝程式與 hello 特定引數。</span><span class="sxs-lookup"><span data-stu-id="465f3-162">hello package Install resource will install hello Mobility service from hello UNIFIEDAGENT.EXE installer with hello specific arguments.</span></span> <span data-ttu-id="465f3-163">（hello 建構 hello 引數的變數需要 tooreflect toobe 變更您的環境）。</span><span class="sxs-lookup"><span data-stu-id="465f3-163">(hello variables that construct hello arguments need toobe changed tooreflect your environment.)</span></span>
* <span data-ttu-id="465f3-164">hello 套件 AzureAgent 資源將會安裝 hello Azure VM 代理程式，建議在 Azure 中執行每個 VM 上。</span><span class="sxs-lookup"><span data-stu-id="465f3-164">hello package AzureAgent resource will install hello Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="465f3-165">hello Azure VM 代理程式也可讓可能 tooadd 延伸 toohello VM 容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="465f3-165">hello Azure VM agent also makes it possible tooadd extensions toohello VM after failover.</span></span>
* <span data-ttu-id="465f3-166">hello 服務資源會確保 hello 相關的行動服務並 hello Azure 服務一律會持續執行。</span><span class="sxs-lookup"><span data-stu-id="465f3-166">hello service resource or resources will ensure that hello related Mobility services and hello Azure services are always running.</span></span>

<span data-ttu-id="465f3-167">儲存為 hello 設定**ASRMobilityService**。</span><span class="sxs-lookup"><span data-stu-id="465f3-167">Save hello configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="465f3-168">請記住 tooreplace hello CSIP 在您設定 tooreflect hello 實際管理伺服器中，以便 hello 代理程式將會正確地連接並將使用 hello 正確複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="465f3-168">Remember tooreplace hello CSIP in your configuration tooreflect hello actual management server, so that hello agent will be connected correctly and will use hello correct passphrase.</span></span>
>
>

## <a name="step-3-upload-tooautomation-dsc"></a><span data-ttu-id="465f3-169">步驟 3： 上傳 tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="465f3-169">Step 3: Upload tooAutomation DSC</span></span>
<span data-ttu-id="465f3-170">因為您所做的 hello DSC 組態將會匯入必要的 DSC 資源模組 (xPSDesiredStateConfiguration)，您需要 tooimport 自動化中的該模組之前 hello DSC 組態上傳。</span><span class="sxs-lookup"><span data-stu-id="465f3-170">Because hello DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need tooimport that module in Automation before you upload hello DSC configuration.</span></span>

<span data-ttu-id="465f3-171">登入 tooyour 自動化帳戶中，瀏覽過**資產** > **模組**，然後按一下**瀏覽圖庫**。</span><span class="sxs-lookup"><span data-stu-id="465f3-171">Sign in tooyour Automation account, browse too**Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="465f3-172">您可以在這裡搜尋 hello 模組和 tooyour 帳戶匯入。</span><span class="sxs-lookup"><span data-stu-id="465f3-172">Here you can search for hello module and import it tooyour account.</span></span>

![匯入模組](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="465f3-174">當您完成此動作時，請移 tooyour 機器必須已安裝的 hello Azure 資源管理員模組，並繼續 tooimport hello 新建立的 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="465f3-174">When you finish this, go tooyour machine where you have hello Azure Resource Manager modules installed and proceed tooimport hello newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="465f3-175">匯入 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="465f3-175">Import cmdlets</span></span>
<span data-ttu-id="465f3-176">在 PowerShell 中，登入 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="465f3-176">In PowerShell, sign in tooyour Azure subscription.</span></span> <span data-ttu-id="465f3-177">修改您的環境的 hello cmdlet tooreflect 和擷取您在變數中的自動化帳戶資訊：</span><span class="sxs-lookup"><span data-stu-id="465f3-177">Modify hello cmdlets tooreflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="465f3-178">使用下列 cmdlet 的 hello 傳 hello 設定 tooAutomation DSC:</span><span class="sxs-lookup"><span data-stu-id="465f3-178">Upload hello configuration tooAutomation DSC by using hello following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a><span data-ttu-id="465f3-179">Hello 設定自動化的 dsc 編譯</span><span class="sxs-lookup"><span data-stu-id="465f3-179">Compile hello configuration in Automation DSC</span></span>
<span data-ttu-id="465f3-180">接著，您必須在自動化 DSC toocompile hello 組態，讓您可以啟動 tooregister 節點 tooit。</span><span class="sxs-lookup"><span data-stu-id="465f3-180">Next, you need toocompile hello configuration in Automation DSC, so that you can start tooregister nodes tooit.</span></span> <span data-ttu-id="465f3-181">藉由執行下列 cmdlet 的 hello 達成此目標：</span><span class="sxs-lookup"><span data-stu-id="465f3-181">You achieve that by running hello following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="465f3-182">這可能需要幾分鐘的時間，因為基本上要部署的 hello 設定 toohello 裝載 DSC 提取服務。</span><span class="sxs-lookup"><span data-stu-id="465f3-182">This can take a few minutes, because you're basically deploying hello configuration toohello hosted DSC pull service.</span></span>

<span data-ttu-id="465f3-183">編譯 hello 組態之後，您可以使用 PowerShell (Get AzureRmAutomationDscCompilationJob)，或使用 hello 擷取 hello 作業資訊[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="465f3-183">After you compile hello configuration, you can retrieve hello job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using hello [Azure portal](https://portal.azure.com/).</span></span>

![擷取作業](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="465f3-185">您現在已成功發行並將上傳您的 DSC 組態 tooAutomation DSC。</span><span class="sxs-lookup"><span data-stu-id="465f3-185">You have now successfully published and uploaded your DSC configuration tooAutomation DSC.</span></span>

## <a name="step-4-onboard-machines-tooautomation-dsc"></a><span data-ttu-id="465f3-186">步驟 4： 上架的機器 tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="465f3-186">Step 4: Onboard machines tooAutomation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="465f3-187">完成此案例中的 hello 必要條件是 hello 最新版本的 WMF 會更新您的 Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="465f3-187">One of hello prerequisites for completing this scenario is that your Windows machines are updated with hello latest version of WMF.</span></span> <span data-ttu-id="465f3-188">您可以下載並安裝您的平台從 hello hello 正確版本[下載中心](https://www.microsoft.com/download/details.aspx?id=50395)。</span><span class="sxs-lookup"><span data-stu-id="465f3-188">You can download and install hello correct version for your platform from hello [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="465f3-189">您即將建立 metaconfig dsc，所以要套用 tooyour 節點。</span><span class="sxs-lookup"><span data-stu-id="465f3-189">You will now create a metaconfig for DSC that you will apply tooyour nodes.</span></span> <span data-ttu-id="465f3-190">與這個 toosucceed，您需要 tooretrieve hello 端點 URL 和 hello 主索引鍵在 Azure 中您選取的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="465f3-190">toosucceed with this, you need tooretrieve hello endpoint URL and hello primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="465f3-191">您可以找到這些值在**金鑰**上 hello**所有設定**刀鋒視窗中的 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="465f3-191">You can find these values under **Keys** on hello **All settings** blade for hello Automation account.</span></span>

![金鑰值](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="465f3-193">在此範例中，您有 Windows Server 2012 R2 的實體伺服器，您想 tooprotect，使用站台復原。</span><span class="sxs-lookup"><span data-stu-id="465f3-193">In this example, you have a Windows Server 2012 R2 physical server that you want tooprotect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a><span data-ttu-id="465f3-194">檢查有任何暫止檔案重新命名作業 hello 登錄中</span><span class="sxs-lookup"><span data-stu-id="465f3-194">Check for any pending file rename operations in hello registry</span></span>
<span data-ttu-id="465f3-195">您開始 tooassociate hello 伺服器 hello Automation DSC 端點之前，我們建議您檢查有任何暫止檔案重新命名作業 hello 登錄中。</span><span class="sxs-lookup"><span data-stu-id="465f3-195">Before you start tooassociate hello server with hello Automation DSC endpoint, we recommend that you check for any pending file rename operations in hello registry.</span></span> <span data-ttu-id="465f3-196">它們可能會禁止 hello 安裝程式完成到期 tooa 暫止的重新開機。</span><span class="sxs-lookup"><span data-stu-id="465f3-196">They might prohibit hello setup from finishing due tooa pending reboot.</span></span>

<span data-ttu-id="465f3-197">執行下列 cmdlet tooverify 是 hello 伺服器上沒有擱置的重新開機的 hello:</span><span class="sxs-lookup"><span data-stu-id="465f3-197">Run hello following cmdlet tooverify that there’s no pending reboot on hello server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="465f3-198">如果這會顯示空白，您必須確定 tooproceed。</span><span class="sxs-lookup"><span data-stu-id="465f3-198">If this shows empty, you are OK tooproceed.</span></span> <span data-ttu-id="465f3-199">如果沒有，您應該解決此問題由 hello 伺服器重新啟動在維護期間。</span><span class="sxs-lookup"><span data-stu-id="465f3-199">If not, you should address this by rebooting hello server during a maintenance window.</span></span>

<span data-ttu-id="465f3-200">tooapply hello 組態 hello 在伺服器上，啟動 hello PowerShell 整合式指令碼環境 (ISE)，並執行下列指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="465f3-200">tooapply hello configuration on hello server, start hello PowerShell Integrated Scripting Environment (ISE) and run hello following script.</span></span> <span data-ttu-id="465f3-201">這是基本上 DSC 本機設定會指示以 hello Automation DSC 服務的 hello 本機設定管理員引擎 tooregister 並擷取 hello 特定組態 (ASRMobilityService.localhost)。</span><span class="sxs-lookup"><span data-stu-id="465f3-201">This is essentially a DSC local configuration that will instruct hello Local Configuration Manager engine tooregister with hello Automation DSC service and retrieve hello specific configuration (ASRMobilityService.localhost).</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

<span data-ttu-id="465f3-202">此設定會導致 hello 本機設定管理員本身引擎 tooregister 並且自動化 DSC。</span><span class="sxs-lookup"><span data-stu-id="465f3-202">This configuration will cause hello Local Configuration Manager engine tooregister itself with Automation DSC.</span></span> <span data-ttu-id="465f3-203">它也會決定如何運作 hello 引擎應該時設定漂移 (ApplyAndAutoCorrect)，它應該執行的動作，應該如何進行 hello 組態是否需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="465f3-203">It will also determine how hello engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with hello configuration if a reboot is required.</span></span>

<span data-ttu-id="465f3-204">執行這個指令碼之後，hello 節點開頭應該 tooregister Automation DSC。</span><span class="sxs-lookup"><span data-stu-id="465f3-204">After you run this script, hello node should start tooregister with Automation DSC.</span></span>

![進行中的節點註冊](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="465f3-206">如果您往回 toohello Azure 入口網站，您可以看到該 hello 新註冊的節點現在已出現在 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="465f3-206">If you go back toohello Azure portal, you can see that hello newly registered node has now appeared in hello portal.</span></span>

![Hello 入口網站中已註冊的節點](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="465f3-208">Hello 在伺服器上，您可以執行下列的 PowerShell 指令程式 tooverify hello 節點的正確登錄的 hello:</span><span class="sxs-lookup"><span data-stu-id="465f3-208">On hello server, you can run hello following PowerShell cmdlet tooverify that hello node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="465f3-209">Hello 設定已提取和套用 toohello 伺服器之後，您可以確認這藉由執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="465f3-209">After hello configuration has been pulled and applied toohello server, you can verify this by running hello following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="465f3-210">hello 輸出會顯示該 hello 伺服器已順利提取其組態：</span><span class="sxs-lookup"><span data-stu-id="465f3-210">hello output shows that hello server has successfully pulled its configuration:</span></span>

![輸出](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="465f3-212">此外，hello 行動服務安裝程式已有它自己的記錄可以找到的*SystemDrive*\ProgramData\ASRSetupLogs。</span><span class="sxs-lookup"><span data-stu-id="465f3-212">In addition, hello Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="465f3-213">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="465f3-213">That’s it.</span></span> <span data-ttu-id="465f3-214">您現在已成功部署並註冊您想 tooprotect，使用站台復原的 hello 電腦上的 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="465f3-214">You have now successfully deployed and registered hello Mobility service on hello machine that you want tooprotect by using Site Recovery.</span></span> <span data-ttu-id="465f3-215">DSC 可確保一律執行所需的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="465f3-215">DSC will make sure that hello required services are always running.</span></span>

![部署成功](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="465f3-217">Hello 管理伺服器偵測到 hello 成功部署之後，您可以設定保護，然後機器上啟用複寫 hello 使用站台復原。</span><span class="sxs-lookup"><span data-stu-id="465f3-217">After hello management server detects hello successful deployment, you can configure protection and enable replication on hello machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="465f3-218">在中斷連線的環境中使用 DSC</span><span class="sxs-lookup"><span data-stu-id="465f3-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="465f3-219">如果您的電腦無法連線的 toohello 網際網路，仍可以依賴 DSC toodeploy 及設定您想 tooprotect hello 工作負載的 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="465f3-219">If your machines aren’t connected toohello Internet, you can still rely on DSC toodeploy and configure hello Mobility service on hello workloads that you want tooprotect.</span></span>

<span data-ttu-id="465f3-220">您可以在環境中執行個體化自己 DSC 提取伺服器 tooessentially 提供 hello 相同的功能，您會得到從 Automation DSC。</span><span class="sxs-lookup"><span data-stu-id="465f3-220">You can instantiate your own DSC pull server in your environment tooessentially provide hello same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="465f3-221">也就是說，hello 用戶端將會提取 hello 組態 （註冊） 後 toohello DSC 端點。</span><span class="sxs-lookup"><span data-stu-id="465f3-221">That is, hello clients will pull hello configuration (after it's registered) toohello DSC endpoint.</span></span> <span data-ttu-id="465f3-222">不過，另一個選項為 toomanually 發送 hello DSC 組態 tooyour 機器，在本機或遠端。</span><span class="sxs-lookup"><span data-stu-id="465f3-222">However, another option is toomanually push hello DSC configuration tooyour machines, either locally or remotely.</span></span>

<span data-ttu-id="465f3-223">請注意，在此範例中，加入的參數 hello 電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="465f3-223">Note that in this example, there's an added parameter for hello computer name.</span></span> <span data-ttu-id="465f3-224">必須能夠存取在遠端共用上的 tooprotect hello 機器現在位於 hello 遠端檔案。</span><span class="sxs-lookup"><span data-stu-id="465f3-224">hello remote files are now located on a remote share that should be accessible by hello machines that you want tooprotect.</span></span> <span data-ttu-id="465f3-225">hello hello 指令碼結尾制定 hello 組態，然後啟動 tooapply hello DSC 組態 toohello 目標電腦。</span><span class="sxs-lookup"><span data-stu-id="465f3-225">hello end of hello script enacts hello configuration and then starts tooapply hello DSC configuration toohello target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="465f3-226">必要條件</span><span class="sxs-lookup"><span data-stu-id="465f3-226">Prerequisites</span></span>
<span data-ttu-id="465f3-227">請確定已安裝該 hello xPSDesiredStateConfiguration PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="465f3-227">Make sure that hello xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="465f3-228">對於 Windows 電腦已安裝 WMF 5.0，您可以執行 hello hello 目標電腦上下列指令程式來安裝 hello xPSDesiredStateConfiguration 模組：</span><span class="sxs-lookup"><span data-stu-id="465f3-228">For Windows machines where WMF 5.0 is installed, you can install hello xPSDesiredStateConfiguration module by running hello following cmdlet on hello target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="465f3-229">您也可以下載並儲存 hello 模組，以防您需要 toodistribute 它 tooWindows 機器安裝 WMF 4.0。</span><span class="sxs-lookup"><span data-stu-id="465f3-229">You can also download and save hello module in case you need toodistribute it tooWindows machines that have WMF 4.0.</span></span> <span data-ttu-id="465f3-230">請在具有 PowerShellGet (WMF 5.0) 的機器上執行下列 Cmdlet︰</span><span class="sxs-lookup"><span data-stu-id="465f3-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="465f3-231">也 WMF 4.0，請確定該 hello [Windows 8.1 更新 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) hello 機器上安裝。</span><span class="sxs-lookup"><span data-stu-id="465f3-231">Also for WMF 4.0, ensure that hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on hello machines.</span></span>

<span data-ttu-id="465f3-232">hello 下列組態可以推入安裝 WMF 5.0 和 WMF 4.0 的 tooWindows 電腦：</span><span class="sxs-lookup"><span data-stu-id="465f3-232">hello following configuration can be pushed tooWindows machines that have WMF 5.0 and WMF 4.0:</span></span>

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

<span data-ttu-id="465f3-233">如果您想 tooinstantiate 自己 DSC 提取伺服器上，就可以從 Automation DSC 您公司網路 toomimic hello 的能力，請參閱[設定 DSC web 提取伺服器](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396)。</span><span class="sxs-lookup"><span data-stu-id="465f3-233">If you want tooinstantiate your own DSC pull server on your corporate network toomimic hello capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="465f3-234">選擇性：使用 Azure Resource Manager 範本來部署 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="465f3-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="465f3-235">本文著重在如何建立您自己的 DSC 組態 tooautomatically 部署 hello 行動服務與 hello Azure VM 代理程式-，以及確保它們執行 hello 機器上的 tooprotect。</span><span class="sxs-lookup"><span data-stu-id="465f3-235">This article has focused on how you can create your own DSC configuration tooautomatically deploy hello Mobility service and hello Azure VM Agent--and ensure that they are running on hello machines that you want tooprotect.</span></span> <span data-ttu-id="465f3-236">我們也必須將部署此 DSC 組態 tooa 新的或現有 Azure 自動化帳戶的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="465f3-236">We also have an Azure Resource Manager template that will deploy this DSC configuration tooa new or existing Azure Automation account.</span></span> <span data-ttu-id="465f3-237">hello 範本將會使用輸入的參數將包含您的環境的 hello 變數 toocreate 自動化資產。</span><span class="sxs-lookup"><span data-stu-id="465f3-237">hello template will use input parameters toocreate Automation assets that will contain hello variables for your environment.</span></span>

<span data-ttu-id="465f3-238">部署 hello 範本之後，您可以直接參考 toostep 4 在此指南 tooonboard 您的電腦。</span><span class="sxs-lookup"><span data-stu-id="465f3-238">After you deploy hello template, you can simply refer toostep 4 in this guide tooonboard your machines.</span></span>

<span data-ttu-id="465f3-239">hello 範本將會執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="465f3-239">hello template will do hello following:</span></span>

1. <span data-ttu-id="465f3-240">使用現有的「自動化」帳戶或建立一個新帳戶</span><span class="sxs-lookup"><span data-stu-id="465f3-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="465f3-241">採用下列各項的輸入參數︰</span><span class="sxs-lookup"><span data-stu-id="465f3-241">Take input parameters for:</span></span>
   * <span data-ttu-id="465f3-242">ASRRemoteFile-hello 位置 hello 行動服務安裝程式的儲存位置</span><span class="sxs-lookup"><span data-stu-id="465f3-242">ASRRemoteFile--hello location where you have stored hello Mobility service setup</span></span>
   * <span data-ttu-id="465f3-243">ASRPassphrase-hello 位置 hello passphrase.txt 檔案的儲存位置</span><span class="sxs-lookup"><span data-stu-id="465f3-243">ASRPassphrase--hello location where you have stored hello passphrase.txt file</span></span>
   * <span data-ttu-id="465f3-244">ASRCSEndpoint-hello 的管理伺服器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="465f3-244">ASRCSEndpoint--hello IP address of your management server</span></span>
3. <span data-ttu-id="465f3-245">匯入 hello xPSDesiredStateConfiguration PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="465f3-245">Import hello xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="465f3-246">建立及編譯 hello DSC 設定</span><span class="sxs-lookup"><span data-stu-id="465f3-246">Create and compile hello DSC configuration</span></span>

<span data-ttu-id="465f3-247">讓您可以啟動登入您的機器進行保護，將會在 hello 正確的順序，進行所有先前步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="465f3-247">All hello preceding steps will happen in hello right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="465f3-248">hello 範本的指示部署中，位於[GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC)。</span><span class="sxs-lookup"><span data-stu-id="465f3-248">hello template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="465f3-249">使用 PowerShell 部署 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="465f3-249">Deploy hello template by using PowerShell:</span></span>

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a><span data-ttu-id="465f3-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="465f3-250">Next steps</span></span>
<span data-ttu-id="465f3-251">在您部署的 hello 行動服務代理程式之後，您可以[啟用複寫](site-recovery-vmware-to-azure.md)hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="465f3-251">After you deploy hello Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for hello virtual machines.</span></span>
