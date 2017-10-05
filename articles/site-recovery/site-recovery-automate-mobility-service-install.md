---
title: "使用 Azure Automation DSC 來部署 Site Recovery 行動服務 | Microsoft Docs"
description: "說明如何使用 Azure Automation DSC，將 Azure Site Recovery 行動服務和 VMware VM 及實體伺服器複寫的 Azure 代理程式自動部署到 Azure"
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
ms.openlocfilehash: bcc5f11afbecac8fe63935f3401dd3e2d767e8aa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-the-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="d940e-103">使用 Azure Automation DSC 部署行動服務，以進行 VM 複寫</span><span class="sxs-lookup"><span data-stu-id="d940e-103">Deploy the Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="d940e-104">在 Operations Management Suite 中，我們提供您一個全方位的備份和災害復原解決方案，可供您融入到您的商務持續性計畫中。</span><span class="sxs-lookup"><span data-stu-id="d940e-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="d940e-105">我們使用「Hyper-V 複本」來與 Hyper-V 一起展開這個旅程。</span><span class="sxs-lookup"><span data-stu-id="d940e-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="d940e-106">但是我們已擴大到支援異質性設定，因為客戶在其雲端中擁有多個 Hypervisor 與平台。</span><span class="sxs-lookup"><span data-stu-id="d940e-106">But we have expanded to support a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="d940e-107">如果您目前執行的是 VMware 工作負載和/或實體伺服器，當 Azure 是您的目的地時，管理伺服器會執行您環境中的所有 Azure Site Recovery 元件來處理與 Azure 之間的通訊和資料覆寫。</span><span class="sxs-lookup"><span data-stu-id="d940e-107">If you are running VMware workloads and/or physical servers today, a management server runs all of the Azure Site Recovery components in your environment to handle the communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-the-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="d940e-108">使用 Automation DSC 來部署 Site Recovery 行動服務</span><span class="sxs-lookup"><span data-stu-id="d940e-108">Deploy the Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="d940e-109">讓我們從快速分析此管理伺服器的作用著手︰</span><span class="sxs-lookup"><span data-stu-id="d940e-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="d940e-110">管理伺服器執行數個伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="d940e-110">The management server runs several server roles.</span></span> <span data-ttu-id="d940e-111">其中一個角色是「組態」 ，負責協調通訊及管理資料複寫與復原程序。</span><span class="sxs-lookup"><span data-stu-id="d940e-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="d940e-112">此外，「處理」  角色則是作為複寫閘道。</span><span class="sxs-lookup"><span data-stu-id="d940e-112">In addition, the *process* role acts as a replication gateway.</span></span> <span data-ttu-id="d940e-113">這個角色會從受保護的來源機器接收複寫資料、以快取、壓縮及加密將該資料最佳化，然後將它傳送至 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d940e-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it to an Azure storage account.</span></span> <span data-ttu-id="d940e-114">處理角色的其中一個功能就是將行動服務的安裝推送至受保護的機器，並執行 VMWare VM 的自動探索。</span><span class="sxs-lookup"><span data-stu-id="d940e-114">One of the functions for the process role is also to push installation of the Mobility service to protected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="d940e-115">如果發生從 Azure 容錯回復的情況，「主要目標」  角色將會在執行這項作業的過程中處理複寫資料。</span><span class="sxs-lookup"><span data-stu-id="d940e-115">If there's a failback from Azure, the *master target* role will handle the replication data as part of this operation.</span></span>

<span data-ttu-id="d940e-116">針對受保護的機器，我們會倚賴「行動服務」 。</span><span class="sxs-lookup"><span data-stu-id="d940e-116">For the protected machines, we rely on the *Mobility service*.</span></span> <span data-ttu-id="d940e-117">在您想要複寫到 Azure 的每部機器 (VMware VM 或實體伺服器) 上都會部署此元件。</span><span class="sxs-lookup"><span data-stu-id="d940e-117">This component is deployed to every machine (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="d940e-118">它會擷取機器上的資料寫入，然後將其轉送到管理伺服器 (處理角色)。</span><span class="sxs-lookup"><span data-stu-id="d940e-118">It captures data writes on the machine and forwards them to the management server (process role).</span></span>

<span data-ttu-id="d940e-119">處理商務持續性時，請務必了解您的工作負載、您的基礎結構，以及牽涉到的元件。</span><span class="sxs-lookup"><span data-stu-id="d940e-119">When you're dealing with business continuity, it's important to understand your workloads, your infrastructure, and the components involved.</span></span> <span data-ttu-id="d940e-120">這樣您就可以滿足您的復原時間目標 (RTO) 和復原點目標 (RPO) 的需求。</span><span class="sxs-lookup"><span data-stu-id="d940e-120">You can then meet the requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="d940e-121">在此情況下，行動服務是確保您的工作負載如您所預期受到保護的關鍵。</span><span class="sxs-lookup"><span data-stu-id="d940e-121">In this context, the Mobility service is key to ensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="d940e-122">因此，您要如何在某些 Operations Management Suite 元件的協助下，以最佳化的方式確保您有可靠的受保護設定？</span><span class="sxs-lookup"><span data-stu-id="d940e-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="d940e-123">本文提供範例來說明如何使用「Azure 自動化預期狀態設定」(DSC) 搭配 Site Recovery 來確保︰</span><span class="sxs-lookup"><span data-stu-id="d940e-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, to ensure that:</span></span>

* <span data-ttu-id="d940e-124">將行動服務和 Azure VM 代理程式部署到您想要保護 Windows 機器。</span><span class="sxs-lookup"><span data-stu-id="d940e-124">The Mobility service and Azure VM agent are deployed to the Windows machines that you want to protect.</span></span>
* <span data-ttu-id="d940e-125">當 Azure 是複寫目標時，行動服務和 Azure VM 代理程式一律都會處於執行狀態。</span><span class="sxs-lookup"><span data-stu-id="d940e-125">The Mobility service and Azure VM agent are always running when Azure is the replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d940e-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="d940e-126">Prerequisites</span></span>
* <span data-ttu-id="d940e-127">用來儲存必要安裝程式的儲存機制</span><span class="sxs-lookup"><span data-stu-id="d940e-127">A repository to store the required setup</span></span>
* <span data-ttu-id="d940e-128">用來儲存必要複雜密碼以向管理伺服器註冊的儲存機制</span><span class="sxs-lookup"><span data-stu-id="d940e-128">A repository to store the required passphrase to register with the management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="d940e-129">系統會為每一部管理伺服器產生一個唯一的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="d940e-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="d940e-130">如果您將部署多部管理伺服器，您就必須確保 passphrase.txt 檔案中儲存了正確的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="d940e-130">If you are going to deploy multiple management servers, you have to ensure that the correct passphrase is stored in the passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="d940e-131">安裝在您想要啟用保護功能之機器上的 Windows Management Framework (WMF) 5.0 (Automation DSC 的需求)</span><span class="sxs-lookup"><span data-stu-id="d940e-131">Windows Management Framework (WMF) 5.0 installed on the machines that you want to enable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="d940e-132">如果您想要針對已安裝 WMF 4.0 的 Windows 機器使用 DSC，請參閱[在中斷連線的環境中使用 DSC](## Use DSC in disconnected environments)。</span><span class="sxs-lookup"><span data-stu-id="d940e-132">If you want to use DSC for Windows machines that have WMF 4.0 installed, see the section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="d940e-133">行動服務可以透過命令列來安裝並接受數個引數。</span><span class="sxs-lookup"><span data-stu-id="d940e-133">The Mobility service can be installed through the command line and accepts several arguments.</span></span> <span data-ttu-id="d940e-134">這就是為什麼您需要有二進位檔 (在從您的設定擷取它們之後)，並將它們儲存在您能夠使用 DSC 組態進行擷取的地方。</span><span class="sxs-lookup"><span data-stu-id="d940e-134">That’s why you need to have the binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="d940e-135">步驟 1：擷取二進位檔</span><span class="sxs-lookup"><span data-stu-id="d940e-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="d940e-136">若要擷取此設定所需的檔案，請瀏覽至管理伺服器上的下列目錄︰</span><span class="sxs-lookup"><span data-stu-id="d940e-136">To extract the files that you need for this setup, browse to the following directory on your management server:</span></span>

    <span data-ttu-id="d940e-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="d940e-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="d940e-138">在此資料夾中，您應該會看到具有下列名稱的 MSI 檔案：</span><span class="sxs-lookup"><span data-stu-id="d940e-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="d940e-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="d940e-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="d940e-140">使用下列命令來擷取安裝程式：</span><span class="sxs-lookup"><span data-stu-id="d940e-140">Use the following command to extract the installer:</span></span>

    <span data-ttu-id="d940e-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="d940e-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="d940e-142">選取所有檔案並將它們傳送到壓縮的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d940e-142">Select all files and send them to a compressed (zipped) folder.</span></span>

<span data-ttu-id="d940e-143">您現在已擁有使用 Automation DSC 來自動執行行動服務設定所需的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="d940e-143">You now have the binaries that you need to automate the setup of the Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="d940e-144">複雜密碼</span><span class="sxs-lookup"><span data-stu-id="d940e-144">Passphrase</span></span>
<span data-ttu-id="d940e-145">接著，您必須決定要放置此壓縮資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="d940e-145">Next, you need to determine where you want to place this zipped folder.</span></span> <span data-ttu-id="d940e-146">您可以使用 Azure 儲存體帳戶 (如稍後所示) 來儲存設定所需的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="d940e-146">You can use an Azure storage account, as shown later, to store the passphrase that you need for the setup.</span></span> <span data-ttu-id="d940e-147">接著，代理程式會在此過程中向管理伺服器註冊。</span><span class="sxs-lookup"><span data-stu-id="d940e-147">The agent will then register with the management server as part of the process.</span></span>

<span data-ttu-id="d940e-148">您在部署管理伺服器時取得的複雜密碼可以儲存為 passphrase.txt 文字檔。</span><span class="sxs-lookup"><span data-stu-id="d940e-148">The passphrase that you got when you deployed the management server can be saved to a text file as passphrase.txt.</span></span>

<span data-ttu-id="d940e-149">請將壓縮的資料夾和複雜密碼放在 Azure 儲存體帳戶裡的專用容器中。</span><span class="sxs-lookup"><span data-stu-id="d940e-149">Place both the zipped folder and the passphrase in a dedicated container in the Azure storage account.</span></span>

![資料夾位置](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="d940e-151">如果您偏好將這些檔案保留在您網路中的共用上，您也可以這樣做。</span><span class="sxs-lookup"><span data-stu-id="d940e-151">If you prefer to keep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="d940e-152">您只需要確保稍後將會使用的 DSC 資源具有存取權，而且可以取得設定和複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="d940e-152">You just need to ensure that the DSC resource that you will be using later has access and can get the setup and passphrase.</span></span>

## <a name="step-2-create-the-dsc-configuration"></a><span data-ttu-id="d940e-153">步驟 2：建立 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="d940e-153">Step 2: Create the DSC configuration</span></span>
<span data-ttu-id="d940e-154">此設定需倚賴 WMF 5.0。</span><span class="sxs-lookup"><span data-stu-id="d940e-154">The setup depends on WMF 5.0.</span></span> <span data-ttu-id="d940e-155">為了讓機器能夠順利透過 Automation DSC 套用組態，必須要有 WMF 5.0。</span><span class="sxs-lookup"><span data-stu-id="d940e-155">For the machine to successfully apply the configuration through Automation DSC, WMF 5.0 needs to be present.</span></span>

<span data-ttu-id="d940e-156">此環境使用下列範例 DSC 組態︰</span><span class="sxs-lookup"><span data-stu-id="d940e-156">The environment uses the following example DSC configuration:</span></span>

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
<span data-ttu-id="d940e-157">此組態將會執行下列各項操作：</span><span class="sxs-lookup"><span data-stu-id="d940e-157">The configuration will do the following:</span></span>

* <span data-ttu-id="d940e-158">變數會告訴組態可在哪裡取得行動服務和 Azure VM 代理程式的二進位檔、可在哪裡取得複雜密碼，以及可在哪裡儲存輸出。</span><span class="sxs-lookup"><span data-stu-id="d940e-158">The variables will tell the configuration where to get the binaries for the Mobility service and the Azure VM agent, where to get the passphrase, and where to store the output.</span></span>
* <span data-ttu-id="d940e-159">組態會匯入 xPSDesiredStateConfiguration DSC 資源，以便讓您可以使用 `xRemoteFile` 從儲存機制下載檔案。</span><span class="sxs-lookup"><span data-stu-id="d940e-159">The configuration will import the xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` to download the files from the repository.</span></span>
* <span data-ttu-id="d940e-160">組態會建立您想要用來儲存二進位檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="d940e-160">The configuration will create a directory where you want to store the binaries.</span></span>
* <span data-ttu-id="d940e-161">封存資源會將從壓縮的資料夾中擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="d940e-161">The archive resource will extract the files from the zipped folder.</span></span>
* <span data-ttu-id="d940e-162">套件 Install 資源會使用特定的引數從 UNIFIEDAGENT.EXE 安裝程式安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="d940e-162">The package Install resource will install the Mobility service from the UNIFIEDAGENT.EXE installer with the specific arguments.</span></span> <span data-ttu-id="d940e-163">(您必須變更建構引數的變數以反映您的環境)。</span><span class="sxs-lookup"><span data-stu-id="d940e-163">(The variables that construct the arguments need to be changed to reflect your environment.)</span></span>
* <span data-ttu-id="d940e-164">套件 AzureAgent 資源會安裝 Azure VM 代理程式，這是針對在 Azure 中執行的每部 VM 建議安裝的代理程式。</span><span class="sxs-lookup"><span data-stu-id="d940e-164">The package AzureAgent resource will install the Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="d940e-165">Azure VM 代理程式也可讓您在容錯移轉之後，在 VM 上新增擴充功能。</span><span class="sxs-lookup"><span data-stu-id="d940e-165">The Azure VM agent also makes it possible to add extensions to the VM after failover.</span></span>
* <span data-ttu-id="d940e-166">服務資源將會確保相關的行動服務與 Azure 服務一律都處於執行狀態。</span><span class="sxs-lookup"><span data-stu-id="d940e-166">The service resource or resources will ensure that the related Mobility services and the Azure services are always running.</span></span>

<span data-ttu-id="d940e-167">將組態儲存為 **ASRMobilityService**。</span><span class="sxs-lookup"><span data-stu-id="d940e-167">Save the configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="d940e-168">請記得取代組態中的 CSIP 以反映實際的管理伺服器，以便代理程式能夠正確連線並使用正確的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="d940e-168">Remember to replace the CSIP in your configuration to reflect the actual management server, so that the agent will be connected correctly and will use the correct passphrase.</span></span>
>
>

## <a name="step-3-upload-to-automation-dsc"></a><span data-ttu-id="d940e-169">步驟 3：上傳至 Automation DSC</span><span class="sxs-lookup"><span data-stu-id="d940e-169">Step 3: Upload to Automation DSC</span></span>
<span data-ttu-id="d940e-170">由於您所產生的 DSC 組態會匯入必要的 DSC 資源模組 (xPSDesiredStateConfiguration)，因此在上傳 DSC 組態之前，您必須先在 Automation 中匯入該模組。</span><span class="sxs-lookup"><span data-stu-id="d940e-170">Because the DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need to import that module in Automation before you upload the DSC configuration.</span></span>

<span data-ttu-id="d940e-171">登入您的「自動化」帳戶、瀏覽至 [資產]  >  [模組]，然後按一下 [瀏覽資源庫]。</span><span class="sxs-lookup"><span data-stu-id="d940e-171">Sign in to your Automation account, browse to **Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="d940e-172">您可以在這裡搜尋模組並將它匯入您的帳戶中。</span><span class="sxs-lookup"><span data-stu-id="d940e-172">Here you can search for the module and import it to your account.</span></span>

![匯入模組](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="d940e-174">完成此動作之後，請前往已安裝 Azure Resource Manager 模組的機器，然後繼續匯入新建立的 DSC 組態。</span><span class="sxs-lookup"><span data-stu-id="d940e-174">When you finish this, go to your machine where you have the Azure Resource Manager modules installed and proceed to import the newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="d940e-175">匯入 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="d940e-175">Import cmdlets</span></span>
<span data-ttu-id="d940e-176">在 PowerShell 中，登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d940e-176">In PowerShell, sign in to your Azure subscription.</span></span> <span data-ttu-id="d940e-177">修改 Cmdlet 以反映您的環境，並擷取變數中的「自動化」帳戶資訊：</span><span class="sxs-lookup"><span data-stu-id="d940e-177">Modify the cmdlets to reflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="d940e-178">使用下列 Cmdlet 將組態上傳至 Automation DSC︰</span><span class="sxs-lookup"><span data-stu-id="d940e-178">Upload the configuration to Automation DSC by using the following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-the-configuration-in-automation-dsc"></a><span data-ttu-id="d940e-179">在 Automation DSC 中編譯組態</span><span class="sxs-lookup"><span data-stu-id="d940e-179">Compile the configuration in Automation DSC</span></span>
<span data-ttu-id="d940e-180">接下來，您必須在 Automation DSC 中編譯組態，以便開始向它註冊節點。</span><span class="sxs-lookup"><span data-stu-id="d940e-180">Next, you need to compile the configuration in Automation DSC, so that you can start to register nodes to it.</span></span> <span data-ttu-id="d940e-181">您將透過執行下列 Cmdlet 來達成目的：</span><span class="sxs-lookup"><span data-stu-id="d940e-181">You achieve that by running the following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="d940e-182">這可能需要幾分鐘的時間，因為您基本上是將組態部署到裝載的 DSC 提取服務。</span><span class="sxs-lookup"><span data-stu-id="d940e-182">This can take a few minutes, because you're basically deploying the configuration to the hosted DSC pull service.</span></span>

<span data-ttu-id="d940e-183">編譯組態之後，您可以使用 PowerShell (Get-AzureRmAutomationDscCompilationJob) 或使用 [Azure 入口網站](https://portal.azure.com/)來擷取作業資訊。</span><span class="sxs-lookup"><span data-stu-id="d940e-183">After you compile the configuration, you can retrieve the job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using the [Azure portal](https://portal.azure.com/).</span></span>

![擷取作業](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="d940e-185">您現在已成功發佈 DSC 組態並將它上傳到 Automation DSC。</span><span class="sxs-lookup"><span data-stu-id="d940e-185">You have now successfully published and uploaded your DSC configuration to Automation DSC.</span></span>

## <a name="step-4-onboard-machines-to-automation-dsc"></a><span data-ttu-id="d940e-186">步驟 4：讓機器在 Automation DSC 上線</span><span class="sxs-lookup"><span data-stu-id="d940e-186">Step 4: Onboard machines to Automation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="d940e-187">完成此案例的其中一個必要條件是使用最新版的 WMF 更新您的 Windows 機器。</span><span class="sxs-lookup"><span data-stu-id="d940e-187">One of the prerequisites for completing this scenario is that your Windows machines are updated with the latest version of WMF.</span></span> <span data-ttu-id="d940e-188">您可以從 [下載中心](https://www.microsoft.com/download/details.aspx?id=50395)下載並安裝適用於您平台的正確版本。</span><span class="sxs-lookup"><span data-stu-id="d940e-188">You can download and install the correct version for your platform from the [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="d940e-189">現在，您將為 DSC 建立將套用至節點的 metaconfig。</span><span class="sxs-lookup"><span data-stu-id="d940e-189">You will now create a metaconfig for DSC that you will apply to your nodes.</span></span> <span data-ttu-id="d940e-190">若要順利完成此作業，您必須針對在 Azure 中選取的自動化帳戶擷取端點 URL 和主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="d940e-190">To succeed with this, you need to retrieve the endpoint URL and the primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="d940e-191">您可以在「自動化」帳戶 [所有設定] 刀鋒視窗上的 [金鑰] 底下找到這些值。</span><span class="sxs-lookup"><span data-stu-id="d940e-191">You can find these values under **Keys** on the **All settings** blade for the Automation account.</span></span>

![金鑰值](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="d940e-193">在此範例中，您有一部想要使用 Site Recovery 來保護的 Windows Server 2012 R2 實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="d940e-193">In this example, you have a Windows Server 2012 R2 physical server that you want to protect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-the-registry"></a><span data-ttu-id="d940e-194">檢查登錄中是否有任何擱置的檔案重新命名作業</span><span class="sxs-lookup"><span data-stu-id="d940e-194">Check for any pending file rename operations in the registry</span></span>
<span data-ttu-id="d940e-195">在您開始將伺服器與 Automation DSC 端點建立關聯之前，建議您檢查登錄中是否有任何擱置的檔案重新命名作業。</span><span class="sxs-lookup"><span data-stu-id="d940e-195">Before you start to associate the server with the Automation DSC endpoint, we recommend that you check for any pending file rename operations in the registry.</span></span> <span data-ttu-id="d940e-196">因為若有擱置的重新開機，它們可能會讓設定無法完成。</span><span class="sxs-lookup"><span data-stu-id="d940e-196">They might prohibit the setup from finishing due to a pending reboot.</span></span>

<span data-ttu-id="d940e-197">執行下列 Cmdlet 以確認伺服器上沒有擱置的重新開機︰</span><span class="sxs-lookup"><span data-stu-id="d940e-197">Run the following cmdlet to verify that there’s no pending reboot on the server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="d940e-198">如果呈現空白，您就可以繼續作業。</span><span class="sxs-lookup"><span data-stu-id="d940e-198">If this shows empty, you are OK to proceed.</span></span> <span data-ttu-id="d940e-199">若非如此，您必須在維護期間重新啟動伺服器以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="d940e-199">If not, you should address this by rebooting the server during a maintenance window.</span></span>

<span data-ttu-id="d940e-200">若要在伺服器上套用組態，請啟動「Windows PowerShell 整合式指令碼環境」(ISE) 並執行下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="d940e-200">To apply the configuration on the server, start the PowerShell Integrated Scripting Environment (ISE) and run the following script.</span></span> <span data-ttu-id="d940e-201">這基本上是 DSC 本機組態，此組態會指示「本機組態管理員」引擎向 Automation DSC 服務註冊並擷取特定的組態 (ASRMobilityService.localhost)。</span><span class="sxs-lookup"><span data-stu-id="d940e-201">This is essentially a DSC local configuration that will instruct the Local Configuration Manager engine to register with the Automation DSC service and retrieve the specific configuration (ASRMobilityService.localhost).</span></span>

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

<span data-ttu-id="d940e-202">此組態會導致「本機組態管理員」引擎向 Automation DSC 註冊它自己。</span><span class="sxs-lookup"><span data-stu-id="d940e-202">This configuration will cause the Local Configuration Manager engine to register itself with Automation DSC.</span></span> <span data-ttu-id="d940e-203">它也會決定引擎應有的運作方式、如果有組態漂移 (ApplyAndAutoCorrect) 的情況應該如何處理，以及如果必須重新開機，應該如何繼續進行組態設定。</span><span class="sxs-lookup"><span data-stu-id="d940e-203">It will also determine how the engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with the configuration if a reboot is required.</span></span>

<span data-ttu-id="d940e-204">執行此指令碼之後，節點應該就會開始向 Automation DSC 註冊。</span><span class="sxs-lookup"><span data-stu-id="d940e-204">After you run this script, the node should start to register with Automation DSC.</span></span>

![進行中的節點註冊](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="d940e-206">如果您返回 Azure 入口網站，便可以看到新註冊的節點現已出現在入口網站中。</span><span class="sxs-lookup"><span data-stu-id="d940e-206">If you go back to the Azure portal, you can see that the newly registered node has now appeared in the portal.</span></span>

![入口網站中的已註冊節點](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="d940e-208">在伺服器上，您可以執行下列 PowerShell Cmdlet 來確認是否已正確註冊節點︰</span><span class="sxs-lookup"><span data-stu-id="d940e-208">On the server, you can run the following PowerShell cmdlet to verify that the node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="d940e-209">提取此組態並套用到伺服器之後，您可以透過執行下列 Cmdlet 來進行確認︰</span><span class="sxs-lookup"><span data-stu-id="d940e-209">After the configuration has been pulled and applied to the server, you can verify this by running the following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="d940e-210">輸出會顯示伺服器已成功提取其組態︰</span><span class="sxs-lookup"><span data-stu-id="d940e-210">The output shows that the server has successfully pulled its configuration:</span></span>

![輸出](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="d940e-212">此外，行動服務設定有自己的記錄檔，您可在 SystemDrive\ProgramData\ASRSetupLogs 找到該記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d940e-212">In addition, the Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="d940e-213">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="d940e-213">That’s it.</span></span> <span data-ttu-id="d940e-214">您現在已在想要使用 Site Recovery 來保護的機器上成功部署和註冊行動服務。</span><span class="sxs-lookup"><span data-stu-id="d940e-214">You have now successfully deployed and registered the Mobility service on the machine that you want to protect by using Site Recovery.</span></span> <span data-ttu-id="d940e-215">DSC 將會確保所需的服務一律都處於執行狀態。</span><span class="sxs-lookup"><span data-stu-id="d940e-215">DSC will make sure that the required services are always running.</span></span>

![部署成功](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="d940e-217">在管理伺服器偵測到部署成功之後，您可以使用 Site Recovery 在機器上設定保護及啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="d940e-217">After the management server detects the successful deployment, you can configure protection and enable replication on the machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="d940e-218">在中斷連線的環境中使用 DSC</span><span class="sxs-lookup"><span data-stu-id="d940e-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="d940e-219">如果您的機器未連線到網際網路，您仍然可依賴 DSC 在您想要保護的工作負載上部署和設定行動服務。</span><span class="sxs-lookup"><span data-stu-id="d940e-219">If your machines aren’t connected to the Internet, you can still rely on DSC to deploy and configure the Mobility service on the workloads that you want to protect.</span></span>

<span data-ttu-id="d940e-220">您可以在您的環境中將自己的 DSC 具現化，以基本上提供與從 Automation DSC 取得之功能相同的功能。</span><span class="sxs-lookup"><span data-stu-id="d940e-220">You can instantiate your own DSC pull server in your environment to essentially provide the same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="d940e-221">亦即，用戶端會將組態 (在註冊後) 提取到 DSC 端點。</span><span class="sxs-lookup"><span data-stu-id="d940e-221">That is, the clients will pull the configuration (after it's registered) to the DSC endpoint.</span></span> <span data-ttu-id="d940e-222">不過，另一個選項是將 DSC 組態手動推送到您的機器 (不論是在本機還是遠端)。</span><span class="sxs-lookup"><span data-stu-id="d940e-222">However, another option is to manually push the DSC configuration to your machines, either locally or remotely.</span></span>

<span data-ttu-id="d940e-223">請注意，在此範例中，為電腦名稱新增了一個參數。</span><span class="sxs-lookup"><span data-stu-id="d940e-223">Note that in this example, there's an added parameter for the computer name.</span></span> <span data-ttu-id="d940e-224">遠端檔案現在位於您想要保護之機器應可存取的遠端共用上。</span><span class="sxs-lookup"><span data-stu-id="d940e-224">The remote files are now located on a remote share that should be accessible by the machines that you want to protect.</span></span> <span data-ttu-id="d940e-225">指令碼的最後會頒布組態，然後開始將 DSC 組態套用到目標電腦。</span><span class="sxs-lookup"><span data-stu-id="d940e-225">The end of the script enacts the configuration and then starts to apply the DSC configuration to the target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d940e-226">必要條件</span><span class="sxs-lookup"><span data-stu-id="d940e-226">Prerequisites</span></span>
<span data-ttu-id="d940e-227">確定已安裝 xPSDesiredStateConfiguration PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="d940e-227">Make sure that the xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="d940e-228">針對已安裝 WMF 5.0 的 Windows 電腦，您可以在目標機器上執行下列 Cmdlet 來安裝 xPSDesiredStateConfiguration 模組：</span><span class="sxs-lookup"><span data-stu-id="d940e-228">For Windows machines where WMF 5.0 is installed, you can install the xPSDesiredStateConfiguration module by running the following cmdlet on the target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="d940e-229">如果您需要將此模組散佈到具有 WMF 4.0 的 Windows 機器，您也可以下載並儲存此模組。</span><span class="sxs-lookup"><span data-stu-id="d940e-229">You can also download and save the module in case you need to distribute it to Windows machines that have WMF 4.0.</span></span> <span data-ttu-id="d940e-230">請在具有 PowerShellGet (WMF 5.0) 的機器上執行下列 Cmdlet︰</span><span class="sxs-lookup"><span data-stu-id="d940e-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="d940e-231">此外，針對 WMF 4.0，請確定機器上已安裝 [Windows 8.1 更新 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) 。</span><span class="sxs-lookup"><span data-stu-id="d940e-231">Also for WMF 4.0, ensure that the [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on the machines.</span></span>

<span data-ttu-id="d940e-232">下列組態可以推送到具有 WMF 5.0 和 WMF 4.0 的 Windows 機器：</span><span class="sxs-lookup"><span data-stu-id="d940e-232">The following configuration can be pushed to Windows machines that have WMF 5.0 and WMF 4.0:</span></span>

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

<span data-ttu-id="d940e-233">如果您想要在公司網路上將自己的 DSC 提取伺服器具現化，以模擬您可以從 Automation DSC 取得的相同功能，請參閱 [設定 DSC Web 提取伺服器](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396)。</span><span class="sxs-lookup"><span data-stu-id="d940e-233">If you want to instantiate your own DSC pull server on your corporate network to mimic the capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="d940e-234">選擇性：使用 Azure Resource Manager 範本來部署 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="d940e-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="d940e-235">本文的重點在於如何建立您自己的 DSC 組態，以自動部署行動服務和 Azure VM 代理程式，並確保它們在您想要保護的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="d940e-235">This article has focused on how you can create your own DSC configuration to automatically deploy the Mobility service and the Azure VM Agent--and ensure that they are running on the machines that you want to protect.</span></span> <span data-ttu-id="d940e-236">我們也有會將此 DSC 組態部署到新的或現有 Automation DSC 帳戶的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="d940e-236">We also have an Azure Resource Manager template that will deploy this DSC configuration to a new or existing Azure Automation account.</span></span> <span data-ttu-id="d940e-237">此範本會使用輸入參數來建立將包含您環境之變數的「自動化」資產。</span><span class="sxs-lookup"><span data-stu-id="d940e-237">The template will use input parameters to create Automation assets that will contain the variables for your environment.</span></span>

<span data-ttu-id="d940e-238">部署範本之後，您可以直接參考本指南中的步驟 4 來讓您的機器上線。</span><span class="sxs-lookup"><span data-stu-id="d940e-238">After you deploy the template, you can simply refer to step 4 in this guide to onboard your machines.</span></span>

<span data-ttu-id="d940e-239">此範本會執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="d940e-239">The template will do the following:</span></span>

1. <span data-ttu-id="d940e-240">使用現有的「自動化」帳戶或建立一個新帳戶</span><span class="sxs-lookup"><span data-stu-id="d940e-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="d940e-241">採用下列各項的輸入參數︰</span><span class="sxs-lookup"><span data-stu-id="d940e-241">Take input parameters for:</span></span>
   * <span data-ttu-id="d940e-242">ASRRemoteFile -- 您儲存行動服務設定的位置</span><span class="sxs-lookup"><span data-stu-id="d940e-242">ASRRemoteFile--the location where you have stored the Mobility service setup</span></span>
   * <span data-ttu-id="d940e-243">ASRPassphrase -- 您儲存 passphrase.txt 檔案的位置</span><span class="sxs-lookup"><span data-stu-id="d940e-243">ASRPassphrase--the location where you have stored the passphrase.txt file</span></span>
   * <span data-ttu-id="d940e-244">ASRCSEndpoint -- 您管理伺服器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d940e-244">ASRCSEndpoint--the IP address of your management server</span></span>
3. <span data-ttu-id="d940e-245">匯入 xPSDesiredStateConfiguration PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="d940e-245">Import the xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="d940e-246">建立及編譯 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="d940e-246">Create and compile the DSC configuration</span></span>

<span data-ttu-id="d940e-247">所有上述步驟都會依正確順序進行，以便您能夠開始將機器上線來進行保護。</span><span class="sxs-lookup"><span data-stu-id="d940e-247">All the preceding steps will happen in the right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="d940e-248">包含部署指示的範本位於 [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC)。</span><span class="sxs-lookup"><span data-stu-id="d940e-248">The template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="d940e-249">使用 PowerShell 來部署範本：</span><span class="sxs-lookup"><span data-stu-id="d940e-249">Deploy the template by using PowerShell:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d940e-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d940e-250">Next steps</span></span>
<span data-ttu-id="d940e-251">部署行動服務代理程式之後，您可以為虛擬機器 [啟用複寫](site-recovery-vmware-to-azure.md) 。</span><span class="sxs-lookup"><span data-stu-id="d940e-251">After you deploy the Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for the virtual machines.</span></span>
