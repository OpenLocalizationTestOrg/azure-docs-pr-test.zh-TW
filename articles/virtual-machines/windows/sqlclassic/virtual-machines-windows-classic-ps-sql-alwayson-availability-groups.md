---
title: "aaaConfigure hello Always On 可用性群組使用 PowerShell 的 Azure VM 上 |Microsoft 文件"
description: "本教學課程會使用與 hello 傳統部署模型所建立的資源。 您可以在 Azure 中使用 PowerShell toocreate Always On 可用性群組。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="34bbf-104">使用 PowerShell 的 Azure VM 上設定 hello Always On 可用性群組</span><span class="sxs-lookup"><span data-stu-id="34bbf-104">Configure hello Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34bbf-105">傳統：UI</span><span class="sxs-lookup"><span data-stu-id="34bbf-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="34bbf-106">[傳統：PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="34bbf-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="34bbf-107">在開始之前，請考量您現在可以在 Azure Resource Manager 模型中完成這項工作。</span><span class="sxs-lookup"><span data-stu-id="34bbf-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="34bbf-108">我們建議針對新的部署使用 Azure Resource Manager 模型。</span><span class="sxs-lookup"><span data-stu-id="34bbf-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="34bbf-109">請參閱 [Azure 虛擬機器上的 SQL Server Always On 可用性群組](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="34bbf-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34bbf-110">建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="34bbf-110">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="34bbf-111">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="34bbf-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="34bbf-112">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="34bbf-112">This article covers using hello classic deployment model.</span></span>

<span data-ttu-id="34bbf-113">Azure 虛擬機器 (Vm) 可協助資料庫的高可用性 SQL Server 系統管理員 toolower hello 成本。</span><span class="sxs-lookup"><span data-stu-id="34bbf-113">Azure virtual machines (VMs) can help database administrators toolower hello cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="34bbf-114">本教學課程會示範如何 tooimplement 可用性群組使用 SQL Server Alwayson 端對端在 Azure 環境。</span><span class="sxs-lookup"><span data-stu-id="34bbf-114">This tutorial shows you how tooimplement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="34bbf-115">結尾 hello hello 教學課程中，在 Azure 中的 SQL Server Alwayson 方案將會包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="34bbf-115">At hello end of hello tutorial, your SQL Server Always On solution in Azure will consist of hello following elements:</span></span>

* <span data-ttu-id="34bbf-116">包含多個子網路 (前端和後端子網路) 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="34bbf-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="34bbf-117">具有 Active Directory 網域的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="34bbf-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="34bbf-118">兩個 SQL Server Vm 已部署的 toohello 後端子和聯結的 toohello Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="34bbf-118">Two SQL Server VMs that are deployed toohello back-end subnet and joined toohello Active Directory domain.</span></span>
* <span data-ttu-id="34bbf-119">Hello 節點多數 仲裁模型具有三個節點 Windows 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="34bbf-119">A three-node Windows failover cluster with hello Node Majority quorum model.</span></span>
* <span data-ttu-id="34bbf-120">具有兩份可用性資料庫同步認可複本的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="34bbf-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="34bbf-121">此案例在 Azure 中是好選擇的原因是其單純性，而非因為其具有成本效益或其他因素。</span><span class="sxs-lookup"><span data-stu-id="34bbf-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="34bbf-122">例如，您也可以使用 hello 網域控制站為 hello 雙節點容錯移轉叢集中仲裁檔案共用見證，以減少 hello Vm 數目的兩個複本的可用性群組 toosave 在 Azure 中的計算時數。</span><span class="sxs-lookup"><span data-stu-id="34bbf-122">For example, you can minimize hello number of VMs for a two-replica availability group toosave on compute hours in Azure by using hello domain controller as hello quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="34bbf-123">這個方法可以減少從 hello 組態之上一個 hello VM 計數。</span><span class="sxs-lookup"><span data-stu-id="34bbf-123">This method reduces hello VM count by one from hello above configuration.</span></span>

<span data-ttu-id="34bbf-124">這個教學課程被專門 tooshow hello 必要的 tooset hello 註冊的步驟所述但不會闡述每個步驟的 hello 詳細資料的上述方案。</span><span class="sxs-lookup"><span data-stu-id="34bbf-124">This tutorial is intended tooshow you hello steps that are required tooset up hello described solution above, without elaborating on hello details of each step.</span></span> <span data-ttu-id="34bbf-125">因此，而不是它會使用 PowerShell 指令碼 tootake hello GUI 設定步驟，提供您快速地透過每個步驟。</span><span class="sxs-lookup"><span data-stu-id="34bbf-125">Therefore, instead of providing hello GUI configuration steps, it uses PowerShell scripting tootake you quickly through each step.</span></span> <span data-ttu-id="34bbf-126">本教學課程假設 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="34bbf-126">This tutorial assumes hello following:</span></span>

* <span data-ttu-id="34bbf-127">您已經有 Azure 帳戶與 hello 虛擬機器的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="34bbf-127">You already have an Azure account with hello virtual machine subscription.</span></span>
* <span data-ttu-id="34bbf-128">您已安裝 hello [Azure PowerShell cmdlet](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="34bbf-128">You've installed hello [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="34bbf-129">您已非常熟悉內部部署解決方案的 Always On 可用性群組的功能。</span><span class="sxs-lookup"><span data-stu-id="34bbf-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="34bbf-130">如需詳細資訊，請參閱 [Always On 可用性群組 (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)。</span><span class="sxs-lookup"><span data-stu-id="34bbf-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a><span data-ttu-id="34bbf-131">連接 tooyour Azure 訂用帳戶，並建立 hello 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="34bbf-131">Connect tooyour Azure subscription and create hello virtual network</span></span>
1. <span data-ttu-id="34bbf-132">在 PowerShell 視窗中本機電腦上，匯入 hello Azure 模組，請下載 hello 發行設定檔案 tooyour 電腦，並連接您的 PowerShell 工作階段 tooyour Azure 訂用帳戶匯入 hello 下載發行設定。</span><span class="sxs-lookup"><span data-stu-id="34bbf-132">In a PowerShell window on your local computer, import hello Azure module, download hello publishing settings file tooyour machine, and connect your PowerShell session tooyour Azure subscription by importing hello downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="34bbf-133">hello **Get-azurepublishsettingsfile**命令自動產生與 Azure 管理憑證，並將它下載 tooyour 機器。</span><span class="sxs-lookup"><span data-stu-id="34bbf-133">hello **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it tooyour machine.</span></span> <span data-ttu-id="34bbf-134">瀏覽器會自動開啟，而且您所在的 Azure 訂用帳戶的提示的 tooenter hello Microsoft 帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="34bbf-134">A browser is automatically opened, and you're prompted tooenter hello Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="34bbf-135">下載的 hello **.publishsettings**檔案包含所有您需要 toomanage 您 Azure 訂用帳戶的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="34bbf-135">hello downloaded **.publishsettings** file contains all hello information that you need toomanage your Azure subscription.</span></span> <span data-ttu-id="34bbf-136">儲存這個檔案 tooa 本機目錄之後, 將它匯入使用 hello **Import-azurepublishsettingsfile**命令。</span><span class="sxs-lookup"><span data-stu-id="34bbf-136">After saving this file tooa local directory, import it by using hello **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="34bbf-137">hello.publishsettings 檔案包含的認證 （未編碼） 會使用的 tooadminister 您的 Azure 訂用帳戶和服務。</span><span class="sxs-lookup"><span data-stu-id="34bbf-137">hello .publishsettings file contains your credentials (unencoded) that are used tooadminister your Azure subscriptions and services.</span></span> <span data-ttu-id="34bbf-138">這個檔案的 hello 安全性最佳作法是 toostore 暫時在來源目錄之外 （例如，在 hello Libraries\Documents 資料夾），它和 hello 匯入已完成後再刪除它。</span><span class="sxs-lookup"><span data-stu-id="34bbf-138">hello security best practice for this file is toostore it temporarily outside your source directories (for example, in hello Libraries\Documents folder), and then delete it after hello import has finished.</span></span> <span data-ttu-id="34bbf-139">取得存取 toohello.publishsettings 檔案的惡意使用者可以編輯、 建立，並刪除您的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="34bbf-139">A malicious user who gains access toohello .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="34bbf-140">定義一系列您將使用 toocreate 您的雲端 IT 基礎結構的變數。</span><span class="sxs-lookup"><span data-stu-id="34bbf-140">Define a series of variables that you'll use toocreate your cloud IT infrastructure.</span></span>

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    <span data-ttu-id="34bbf-141">請特別注意 toohello 遵循您的命令稍後不會失敗的 tooensure:</span><span class="sxs-lookup"><span data-stu-id="34bbf-141">Pay attention toohello following tooensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="34bbf-142">變數**$storageAccountName**和**$dcServiceName**必須是唯一的因為它們使用 tooidentify 您的雲端儲存體帳戶和雲端伺服器，分別在 hello 網際網路上。</span><span class="sxs-lookup"><span data-stu-id="34bbf-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used tooidentify your cloud storage account and cloud server, respectively, on hello Internet.</span></span>
   * <span data-ttu-id="34bbf-143">您指定的變數名稱的 hello **$affinityGroupName**和**$virtualNetworkName** hello 虛擬網路組態文件中稍後會使用設定。</span><span class="sxs-lookup"><span data-stu-id="34bbf-143">hello names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in hello virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="34bbf-144">**$sqlImageName**指定 hello 更新包含 SQL Server 2012 Service Pack 1 Enterprise Edition 的 hello VM 映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="34bbf-144">**$sqlImageName** specifies hello updated name of hello VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="34bbf-145">為了簡單起見， **Contoso ！ 000** hello 相同整個 hello 整個教學課程所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="34bbf-145">For simplicity, **Contoso!000** is hello same password that's used throughout hello entire tutorial.</span></span>

3. <span data-ttu-id="34bbf-146">建立同質群組。</span><span class="sxs-lookup"><span data-stu-id="34bbf-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="34bbf-147">匯入組態檔以建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="34bbf-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="34bbf-148">hello 設定檔包含下列 XML 文件的 hello。</span><span class="sxs-lookup"><span data-stu-id="34bbf-148">hello configuration file contains hello following XML document.</span></span> <span data-ttu-id="34bbf-149">簡單地說，它會指定虛擬網路稱為**ContosoNET**呼叫 hello 同質群組中**ContosoAG**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-149">In brief, it specifies a virtual network called **ContosoNET** in hello affinity group called **ContosoAG**.</span></span> <span data-ttu-id="34bbf-150">它有 hello 位址空間**10.10.0.0/16**兩個子網路，且**10.10.1.0/24**和**10.10.2.0/24**，這分別是 hello 前端網路和背景的子網路。</span><span class="sxs-lookup"><span data-stu-id="34bbf-150">It has hello address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are hello front subnet and back subnet, respectively.</span></span> <span data-ttu-id="34bbf-151">hello 前端子網路是您可以在其中放置 Microsoft SharePoint 之類的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="34bbf-151">hello front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="34bbf-152">hello 端網路是您將放置 hello SQL Server Vm。</span><span class="sxs-lookup"><span data-stu-id="34bbf-152">hello back subnet is where you'll place hello SQL Server VMs.</span></span> <span data-ttu-id="34bbf-153">如果您變更 hello **$affinityGroupName**和**$virtualNetworkName**變數，您也必須變更對應下列名稱的 hello。</span><span class="sxs-lookup"><span data-stu-id="34bbf-153">If you change hello **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change hello corresponding names below.</span></span>

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. <span data-ttu-id="34bbf-154">建立與您建立，並將它設為 hello 目前的儲存體帳戶中，您的訂用帳戶中的 hello 同質群組相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="34bbf-154">Create a storage account that's associated with hello affinity group that you created, and set it as hello current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="34bbf-155">建立 hello 新雲端服務和可用性設定組中的 hello 網域控制站伺服器。</span><span class="sxs-lookup"><span data-stu-id="34bbf-155">Create hello domain controller server in hello new cloud service and availability set.</span></span>

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    <span data-ttu-id="34bbf-156">這些管道的命令 hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="34bbf-156">These piped commands do hello following things:</span></span>

   * <span data-ttu-id="34bbf-157">**New-AzureVMConfig** 可建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="34bbf-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="34bbf-158">**新增 AzureProvisioningConfig**提供 hello 的獨立 Windows 伺服器的組態參數。</span><span class="sxs-lookup"><span data-stu-id="34bbf-158">**Add-AzureProvisioningConfig** gives hello configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="34bbf-159">**新增 AzureDataDisk**加入您將用於儲存 Active Directory 資料，以快取選項集 tooNone hello 的 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="34bbf-159">**Add-AzureDataDisk** adds hello data disk that you'll use for storing Active Directory data, with hello caching option set tooNone.</span></span>
   * <span data-ttu-id="34bbf-160">**New-azurevm**建立新的雲端服務，並建立 hello hello 新的雲端服務中新的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="34bbf-160">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span>

7. <span data-ttu-id="34bbf-161">等候 hello 完整佈建，新 VM toobe 並下載 hello 遠端桌面檔案 tooyour 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="34bbf-161">Wait for hello new VM toobe fully provisioned, and download hello remote desktop file tooyour working directory.</span></span> <span data-ttu-id="34bbf-162">因為 hello 新的 Azure VM 需要很長的時間 tooprovision，hello`while`迴圈會繼續 toopoll hello 新的 VM，直到它可供使用。</span><span class="sxs-lookup"><span data-stu-id="34bbf-162">Because hello new Azure VM takes a long time tooprovision, hello `while` loop continues toopoll hello new VM until it's ready for use.</span></span>

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

<span data-ttu-id="34bbf-163">hello 網域控制站伺服器現在已成功佈建。</span><span class="sxs-lookup"><span data-stu-id="34bbf-163">hello domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="34bbf-164">接下來，您需要在此網域控制站伺服器上設定 hello Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="34bbf-164">Next, you'll configure hello Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="34bbf-165">在本機電腦上保持 hello PowerShell 視窗中開啟。</span><span class="sxs-lookup"><span data-stu-id="34bbf-165">Leave hello PowerShell window open on your local computer.</span></span> <span data-ttu-id="34bbf-166">您將使用它一次更新 toocreate hello 兩個 SQL Server Vm。</span><span class="sxs-lookup"><span data-stu-id="34bbf-166">You'll use it again later toocreate hello two SQL Server VMs.</span></span>

## <a name="configure-hello-domain-controller"></a><span data-ttu-id="34bbf-167">設定 hello 網域控制站</span><span class="sxs-lookup"><span data-stu-id="34bbf-167">Configure hello domain controller</span></span>
1. <span data-ttu-id="34bbf-168">透過啟動 hello 遠端桌面檔案連接 toohello 網域控制站伺服器。</span><span class="sxs-lookup"><span data-stu-id="34bbf-168">Connect toohello domain controller server by launching hello remote desktop file.</span></span> <span data-ttu-id="34bbf-169">使用 hello 電腦系統管理員的 AzureAdmin 的使用者名稱和密碼**Contoso ！ 000**，這是您指定當您建立 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="34bbf-169">Use hello machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created hello new VM.</span></span>
2. <span data-ttu-id="34bbf-170">在系統管理員模式下開啟 [Azure PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="34bbf-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="34bbf-171">執行下列 hello **DCPROMO。EXE**向上 hello 命令 tooset **corp.contoso.com**含有 hello M 磁碟機上的資料目錄。</span><span class="sxs-lookup"><span data-stu-id="34bbf-171">Run hello following **DCPROMO.EXE** command tooset up hello **corp.contoso.com** domain, with hello data directories on drive M.</span></span>

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    <span data-ttu-id="34bbf-172">Hello 命令執行完成之後，hello VM 會自動重新啟動。</span><span class="sxs-lookup"><span data-stu-id="34bbf-172">After hello command finishes, hello VM restarts automatically.</span></span>

4. <span data-ttu-id="34bbf-173">透過啟動 hello 遠端桌面檔案再次連接 toohello 網域控制站伺服器。</span><span class="sxs-lookup"><span data-stu-id="34bbf-173">Connect toohello domain controller server again by launching hello remote desktop file.</span></span> <span data-ttu-id="34bbf-174">這次，改用 **CORP\Administrator** 身分登入。</span><span class="sxs-lookup"><span data-stu-id="34bbf-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="34bbf-175">以系統管理員模式開啟 PowerShell 視窗，並使用下列命令的 hello 匯入 hello Active Directory PowerShell 模組：</span><span class="sxs-lookup"><span data-stu-id="34bbf-175">Open a PowerShell window in administrator mode, and import hello Active Directory PowerShell module by using hello following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="34bbf-176">執行下列命令 tooadd 三個使用者 toohello 網域 hello。</span><span class="sxs-lookup"><span data-stu-id="34bbf-176">Run hello following commands tooadd three users toohello domain.</span></span>

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    <span data-ttu-id="34bbf-177">**CORP\Install**都是使用的 tooconfigure 相關 toohello SQL Server 服務執行個體、 hello 容錯移轉叢集，以及 hello 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="34bbf-177">**CORP\Install** is used tooconfigure everything related toohello SQL Server service instances, hello failover cluster, and hello availability group.</span></span> <span data-ttu-id="34bbf-178">**CORP\SQLSvc1**和**CORP\SQLSvc2**作為 hello 兩個 SQL Server Vm 的 hello SQL Server 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="34bbf-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as hello SQL Server service accounts for hello two SQL Server VMs.</span></span>
7. <span data-ttu-id="34bbf-179">Hello 接下來，執行下列命令 toogive **CORP\Install** hello hello 網域中的權限 toocreate 電腦物件。</span><span class="sxs-lookup"><span data-stu-id="34bbf-179">Next, run hello following commands toogive **CORP\Install** hello permissions toocreate computer objects in hello domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="34bbf-180">hello 上述指定的 GUID 是 hello GUID hello 電腦物件類型。</span><span class="sxs-lookup"><span data-stu-id="34bbf-180">hello GUID specified above is hello GUID for hello computer object type.</span></span> <span data-ttu-id="34bbf-181">hello **CORP\Install**帳戶需要 hello**讀取全部內容**和**建立電腦物件**hello 容錯移轉的物件權限 toocreate hello Active Directory叢集。</span><span class="sxs-lookup"><span data-stu-id="34bbf-181">hello **CORP\Install** account needs hello **Read All Properties** and **Create Computer Objects** permission toocreate hello Active Direct objects for hello failover cluster.</span></span> <span data-ttu-id="34bbf-182">hello**讀取全部內容**權限已被 tooCORP\Install 根據預設，因此您不需要 toogrant 它明確。</span><span class="sxs-lookup"><span data-stu-id="34bbf-182">hello **Read All Properties** permission is already given tooCORP\Install by default, so you don't need toogrant it explicitly.</span></span> <span data-ttu-id="34bbf-183">如需資訊的權限需要 toocreate hello 容錯移轉叢集，請參閱 <<c0> [ 容錯移轉叢集逐步指南： 設定 Active Directory 中的帳戶](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="34bbf-183">For more information on permissions that are needed toocreate hello failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="34bbf-184">既然您已經完成設定 Active Directory 與 hello 使用者物件，您將建立兩個 SQL Server Vm，並將它們 toothis 網域。</span><span class="sxs-lookup"><span data-stu-id="34bbf-184">Now that you've finished configuring Active Directory and hello user objects, you'll create two SQL Server VMs and join them toothis domain.</span></span>

## <a name="create-hello-sql-server-vms"></a><span data-ttu-id="34bbf-185">建立 hello SQL Server Vm</span><span class="sxs-lookup"><span data-stu-id="34bbf-185">Create hello SQL Server VMs</span></span>
1. <span data-ttu-id="34bbf-186">繼續已在本機電腦上開啟的 toouse hello PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="34bbf-186">Continue toouse hello PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="34bbf-187">定義下列其他變數的 hello:</span><span class="sxs-lookup"><span data-stu-id="34bbf-187">Define hello following additional variables:</span></span>

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    <span data-ttu-id="34bbf-188">hello IP 位址**10.10.0.4**通常會指派 toohello hello 中建立的第一個 VM **10.10.0.0/16** Azure 虛擬網路的子網路。</span><span class="sxs-lookup"><span data-stu-id="34bbf-188">hello IP address **10.10.0.4** is typically assigned toohello first VM that you create in hello **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="34bbf-189">您應該確認這是您的網域控制站伺服器 hello 位址，藉由執行**IPCONFIG**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-189">You should verify that this is hello address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="34bbf-190">執行下列管道的命令 toocreate hello 第一次的 hello VM 在 hello 容錯移轉叢集中，名為**ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="34bbf-190">Run hello following piped commands toocreate hello first VM in hello failover cluster, named **ContosoQuorum**:</span></span>

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    <span data-ttu-id="34bbf-191">請注意上述的 hello 命令相關的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="34bbf-191">Note hello following regarding hello command above:</span></span>

   * <span data-ttu-id="34bbf-192">**New-azurevmconfig**與 hello 所需的可用性設定組名稱建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="34bbf-192">**New-AzureVMConfig** creates a VM configuration with hello desired availability set name.</span></span> <span data-ttu-id="34bbf-193">hello 後續 Vm 將會建立以 hello 相同可用性設定組名稱，使其正在加入 toohello 相同可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="34bbf-193">hello subsequent VMs will be created with hello same availability set name so that they're joined toohello same availability set.</span></span>
   * <span data-ttu-id="34bbf-194">**新增 AzureProvisioningConfig**聯結 hello 您所建立的 VM toohello Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="34bbf-194">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="34bbf-195">**Set-azuresubnet**數位 hello hello 後的子網路中的 VM。</span><span class="sxs-lookup"><span data-stu-id="34bbf-195">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="34bbf-196">**New-azurevm**建立新的雲端服務，並建立 hello hello 新的雲端服務中新的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="34bbf-196">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span> <span data-ttu-id="34bbf-197">hello **DnsSettings**參數指定該 hello DNS 伺服器 hello hello 新的雲端服務中的伺服器具有 hello IP 位址**10.10.0.4**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-197">hello **DnsSettings** parameter specifies that hello DNS server for hello servers in hello new cloud service has hello IP address **10.10.0.4**.</span></span> <span data-ttu-id="34bbf-198">這是 hello hello 網域控制站伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="34bbf-198">This is hello IP address of hello domain controller server.</span></span> <span data-ttu-id="34bbf-199">需要這個參數 tooenable hello hello 雲端服務 toojoin toohello Active Directory 網域中的新 Vm 成功。</span><span class="sxs-lookup"><span data-stu-id="34bbf-199">This parameter is needed tooenable hello new VMs in hello cloud service toojoin toohello Active Directory domain successfully.</span></span> <span data-ttu-id="34bbf-200">如果沒有這個參數，您必須手動設定 hello IPv4 設定 VM toouse hello 網域控制站伺服器中的主要 DNS 伺服器 hello 之後 hello VM 已佈建，然後再將 hello VM toohello Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="34bbf-200">Without this parameter, you must manually set hello IPv4 settings in your VM toouse hello domain controller server as hello primary DNS server after hello VM is provisioned, and then join hello VM toohello Active Directory domain.</span></span>
3. <span data-ttu-id="34bbf-201">執行的 hello 下列管道命令 toocreate hello SQL Server Vm，名為**ContosoSQL1**和**ContosoSQL2**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-201">Run hello following piped commands toocreate hello SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    <span data-ttu-id="34bbf-202">請注意上述的 hello 命令相關的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="34bbf-202">Note hello following regarding hello commands above:</span></span>

   * <span data-ttu-id="34bbf-203">**New-azurevmconfig**使用 hello hello 網域控制站伺服器，為相同可用性設定組名稱，並使用 hello hello 虛擬機器映像庫中的 SQL Server 2012 Service Pack 1 Enterprise Edition 映像。</span><span class="sxs-lookup"><span data-stu-id="34bbf-203">**New-AzureVMConfig** uses hello same availability set name as hello domain controller server, and uses hello SQL Server 2012 Service Pack 1 Enterprise Edition image in hello virtual machine gallery.</span></span> <span data-ttu-id="34bbf-204">它也會設定 hello 操作系統磁碟 tooread 快取 （無寫入快取）。</span><span class="sxs-lookup"><span data-stu-id="34bbf-204">It also sets hello operating system disk tooread-caching only (no write caching).</span></span> <span data-ttu-id="34bbf-205">我們建議您移轉 hello 資料庫檔案 tooa 個別資料磁碟您附加 toohello VM，並將它設定為無讀取或寫入快取。</span><span class="sxs-lookup"><span data-stu-id="34bbf-205">We recommend that you migrate hello database files tooa separate data disk that you attach toohello VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="34bbf-206">不過，hello 求其次的 tooremove 寫入快取 hello 作業系統磁碟上因為您無法移除讀取 hello 作業系統磁碟的快取。</span><span class="sxs-lookup"><span data-stu-id="34bbf-206">However, hello next best thing is tooremove write caching on hello operating system disk because you can't remove read caching on hello operating system disk.</span></span>
   * <span data-ttu-id="34bbf-207">**新增 AzureProvisioningConfig**聯結 hello 您所建立的 VM toohello Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="34bbf-207">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="34bbf-208">**Set-azuresubnet**數位 hello hello 後的子網路中的 VM。</span><span class="sxs-lookup"><span data-stu-id="34bbf-208">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="34bbf-209">**新增 AzureEndpoint**會加入存取端點，讓用戶端應用程式可以存取 hello 網際網路上的這些 SQL Server 服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="34bbf-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on hello Internet.</span></span> <span data-ttu-id="34bbf-210">TooContosoSQL1 和 ContosoSQL2，會提供不同的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="34bbf-210">Different ports are given tooContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="34bbf-211">**New-azurevm**會建立新的 SQL Server VM 的 hello hello 在相同雲端 ContosoQuorum 為服務。</span><span class="sxs-lookup"><span data-stu-id="34bbf-211">**New-AzureVM** creates hello new SQL Server VM in hello same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="34bbf-212">您必須將 hello Vm 放在相同雲端服務如果您想要它們在 toobe hello hello 相同可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="34bbf-212">You must place hello VMs in hello same cloud service if you want them toobe in hello same availability set.</span></span>
4. <span data-ttu-id="34bbf-213">等候每個完整佈建的 VM toobe 且每個 VM toodownload 其遠端桌面檔案 tooyour 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="34bbf-213">Wait for each VM toobe fully provisioned and for each VM toodownload its remote desktop file tooyour working directory.</span></span> <span data-ttu-id="34bbf-214">hello`for`迴圈逐一循環顯示 hello 三個新的 Vm，並為每個執行 hello hello 最上層大括號內的命令。</span><span class="sxs-lookup"><span data-stu-id="34bbf-214">hello `for` loop cycles through hello three new VMs and executes hello commands inside hello top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    <span data-ttu-id="34bbf-215">hello SQL Server Vm 現在已佈建並執行，但它們隨 SQL Server 安裝使用預設選項。</span><span class="sxs-lookup"><span data-stu-id="34bbf-215">hello SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-hello-failover-cluster-vms"></a><span data-ttu-id="34bbf-216">初始化 hello 容錯移轉叢集的 Vm</span><span class="sxs-lookup"><span data-stu-id="34bbf-216">Initialize hello failover cluster VMs</span></span>
<span data-ttu-id="34bbf-217">在本節中，您會需要 toomodify hello 三部伺服器，您將使用在 hello 容錯移轉叢集與 hello SQL Server 安裝。</span><span class="sxs-lookup"><span data-stu-id="34bbf-217">In this section, you need toomodify hello three servers that you'll use in hello failover cluster and hello SQL Server installation.</span></span> <span data-ttu-id="34bbf-218">具體而言：</span><span class="sxs-lookup"><span data-stu-id="34bbf-218">Specifically:</span></span>

* <span data-ttu-id="34bbf-219">所有伺服器： 您需要 tooinstall hello**容錯移轉叢集**功能。</span><span class="sxs-lookup"><span data-stu-id="34bbf-219">All servers: You need tooinstall hello **Failover Clustering** feature.</span></span>
* <span data-ttu-id="34bbf-220">所有伺服器： 您需要 tooadd **CORP\Install**為 hello 機器**管理員**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-220">All servers: You need tooadd **CORP\Install** as hello machine **administrator**.</span></span>
* <span data-ttu-id="34bbf-221">僅 ContosoSQL1 和 ContosoSQL2： 需要 tooadd **CORP\Install**為**sysadmin** hello 預設資料庫中的角色。</span><span class="sxs-lookup"><span data-stu-id="34bbf-221">ContosoSQL1 and ContosoSQL2 only: You need tooadd **CORP\Install** as a **sysadmin** role in hello default database.</span></span>
* <span data-ttu-id="34bbf-222">僅 ContosoSQL1 和 ContosoSQL2： 需要 tooadd **NT AUTHORITY\System**做為登入，以下列權限的 hello:</span><span class="sxs-lookup"><span data-stu-id="34bbf-222">ContosoSQL1 and ContosoSQL2 only: You need tooadd **NT AUTHORITY\System** as a sign-in with hello following permissions:</span></span>

  * <span data-ttu-id="34bbf-223">更改所有可用性群組</span><span class="sxs-lookup"><span data-stu-id="34bbf-223">Alter any availability group</span></span>
  * <span data-ttu-id="34bbf-224">連接 SQL</span><span class="sxs-lookup"><span data-stu-id="34bbf-224">Connect SQL</span></span>
  * <span data-ttu-id="34bbf-225">檢視伺服器狀態</span><span class="sxs-lookup"><span data-stu-id="34bbf-225">View server state</span></span>
* <span data-ttu-id="34bbf-226">僅 ContosoSQL1 和 ContosoSQL2: hello **TCP** hello SQL Server VM 上的通訊協定已啟用。</span><span class="sxs-lookup"><span data-stu-id="34bbf-226">ContosoSQL1 and ContosoSQL2 only: hello **TCP** protocol is already enabled on hello SQL Server VM.</span></span> <span data-ttu-id="34bbf-227">不過，您仍然需要 tooopen hello 防火牆供 SQL server 的遠端存取。</span><span class="sxs-lookup"><span data-stu-id="34bbf-227">However, you still need tooopen hello firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="34bbf-228">現在，您已準備好 toostart。</span><span class="sxs-lookup"><span data-stu-id="34bbf-228">Now, you're ready toostart.</span></span> <span data-ttu-id="34bbf-229">開頭為**ContosoQuorum**，依照下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="34bbf-229">Beginning with **ContosoQuorum**, follow hello steps below:</span></span>

1. <span data-ttu-id="34bbf-230">連接太**ContosoQuorum**透過啟動 hello 遠端桌面檔案。</span><span class="sxs-lookup"><span data-stu-id="34bbf-230">Connect too**ContosoQuorum** by launching hello remote desktop files.</span></span> <span data-ttu-id="34bbf-231">使用 hello 電腦系統管理員的使用者名稱**AzureAdmin**和密碼**Contoso ！ 000**，這是您指定當您建立 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="34bbf-231">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="34bbf-232">請確認該 hello 電腦已成功加入太**corp.contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-232">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="34bbf-233">等候 hello SQL Server 安裝 toofinish 執行 hello 自動初始化工作，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="34bbf-233">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="34bbf-234">在系統管理員模式下開啟 [Azure PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="34bbf-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="34bbf-235">安裝 hello Windows 容錯移轉叢集功能。</span><span class="sxs-lookup"><span data-stu-id="34bbf-235">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="34bbf-236">以本機系統管理員的身分新增 **CORP\Install**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="34bbf-237">登出 ContosoQuorum。</span><span class="sxs-lookup"><span data-stu-id="34bbf-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="34bbf-238">此伺服器的相關作業完成。</span><span class="sxs-lookup"><span data-stu-id="34bbf-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="34bbf-239">接下來，初始化 **ContosoSQL1** 和 **ContosoSQL2**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="34bbf-240">請遵循下列 hello 步驟，也就是相同的兩個 SQL Server Vm。</span><span class="sxs-lookup"><span data-stu-id="34bbf-240">Follow hello steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="34bbf-241">透過啟動 hello 遠端桌面檔案連接 toohello 兩個 SQL Server Vm。</span><span class="sxs-lookup"><span data-stu-id="34bbf-241">Connect toohello two SQL Server VMs by launching hello remote desktop files.</span></span> <span data-ttu-id="34bbf-242">使用 hello 電腦系統管理員的使用者名稱**AzureAdmin**和密碼**Contoso ！ 000**，這是您指定當您建立 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="34bbf-242">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="34bbf-243">請確認該 hello 電腦已成功加入太**corp.contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-243">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="34bbf-244">等候 hello SQL Server 安裝 toofinish 執行 hello 自動初始化工作，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="34bbf-244">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="34bbf-245">在系統管理員模式下開啟 [Azure PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="34bbf-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="34bbf-246">安裝 hello Windows 容錯移轉叢集功能。</span><span class="sxs-lookup"><span data-stu-id="34bbf-246">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="34bbf-247">以本機系統管理員的身分新增 **CORP\Install**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="34bbf-248">匯入 hello SQL Server PowerShell 提供者。</span><span class="sxs-lookup"><span data-stu-id="34bbf-248">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="34bbf-249">新增**CORP\Install** hello hello 預設 SQL Server 執行個體的 sysadmin 角色。</span><span class="sxs-lookup"><span data-stu-id="34bbf-249">Add **CORP\Install** as hello sysadmin role for hello default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="34bbf-250">新增**NT AUTHORITY\System**做為登入，以上面所述的 hello 三個權限。</span><span class="sxs-lookup"><span data-stu-id="34bbf-250">Add **NT AUTHORITY\System** as a sign-in with hello three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="34bbf-251">開啟 SQL server 的遠端存取的 hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="34bbf-251">Open hello firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="34bbf-252">登出兩個 VM。</span><span class="sxs-lookup"><span data-stu-id="34bbf-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="34bbf-253">最後，您已準備好 tooconfigure hello 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="34bbf-253">Finally, you're ready tooconfigure hello availability group.</span></span> <span data-ttu-id="34bbf-254">您將使用 hello hello 的所有工作的 SQL Server PowerShell 提供者 tooperform **ContosoSQL1**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-254">You'll use hello SQL Server PowerShell Provider tooperform all of hello work on **ContosoSQL1**.</span></span>

## <a name="configure-hello-availability-group"></a><span data-ttu-id="34bbf-255">Hello 可用性群組設定</span><span class="sxs-lookup"><span data-stu-id="34bbf-255">Configure hello availability group</span></span>
1. <span data-ttu-id="34bbf-256">連接太**ContosoSQL1**透過啟動 hello 遠端桌面檔案再次。</span><span class="sxs-lookup"><span data-stu-id="34bbf-256">Connect too**ContosoSQL1** again by launching hello remote desktop files.</span></span> <span data-ttu-id="34bbf-257">而不是使用 hello 機器帳戶登入，使用登入**CORP\Install**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-257">Instead of signing in by using hello machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="34bbf-258">在系統管理員模式下開啟 [Azure PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="34bbf-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="34bbf-259">定義下列變數的 hello:</span><span class="sxs-lookup"><span data-stu-id="34bbf-259">Define hello following variables:</span></span>

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. <span data-ttu-id="34bbf-260">匯入 hello SQL Server PowerShell 提供者。</span><span class="sxs-lookup"><span data-stu-id="34bbf-260">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="34bbf-261">ContosoSQL1 tooCORP\SQLSvc1 hello SQL Server 服務帳戶變更。</span><span class="sxs-lookup"><span data-stu-id="34bbf-261">Change hello SQL Server service account for ContosoSQL1 tooCORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="34bbf-262">ContosoSQL2 tooCORP\SQLSvc2 hello SQL Server 服務帳戶變更。</span><span class="sxs-lookup"><span data-stu-id="34bbf-262">Change hello SQL Server service account for ContosoSQL2 tooCORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="34bbf-263">下載**CreateAzureFailoverCluster.ps1**從[Alwayson 可用性群組的 Azure VM 中建立容錯移轉叢集](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)toohello 本機工作目錄。</span><span class="sxs-lookup"><span data-stu-id="34bbf-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello local working directory.</span></span> <span data-ttu-id="34bbf-264">您將使用此指令碼 toohelp，建立運作的容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="34bbf-264">You'll use this script toohelp you create a functional failover cluster.</span></span> <span data-ttu-id="34bbf-265">如需 Windows 容錯移轉叢集的互動方式 hello Azure 的重要資訊網路，請參閱[Azure 虛擬機器中 SQL Server 的高可用性和災害復原](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="34bbf-265">For important information on how Windows Failover Clustering interacts with hello Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="34bbf-266">變更 tooyour 工作目錄，並建立 hello 容錯移轉叢集與 hello 下載指令碼。</span><span class="sxs-lookup"><span data-stu-id="34bbf-266">Change tooyour working directory and create hello failover cluster with hello downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="34bbf-267">啟用 Alwayson 可用性群組 hello 預設 SQL Server 執行個體上**ContosoSQL1**和**ContosoSQL2**。</span><span class="sxs-lookup"><span data-stu-id="34bbf-267">Enable Always On availability groups for hello default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. <span data-ttu-id="34bbf-268">建立備份目錄，並授與 hello SQL Server 服務帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="34bbf-268">Create a backup directory and grant permissions for hello SQL Server service accounts.</span></span> <span data-ttu-id="34bbf-269">Hello 次要複本上，您將使用此目錄 tooprepare hello 可用性資料庫。</span><span class="sxs-lookup"><span data-stu-id="34bbf-269">You'll use this directory tooprepare hello availability database on hello secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="34bbf-270">上建立資料庫**ContosoSQL1**呼叫**MyDB1**、 需要完整備份和記錄備份，並在進行還原**ContosoSQL2**以 hello **WITHNORECOVERY**選項。</span><span class="sxs-lookup"><span data-stu-id="34bbf-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with hello **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="34bbf-271">Hello SQL Server Vm 上建立 hello 可用性群組端點，hello 端點上設定 hello 適當的權限。</span><span class="sxs-lookup"><span data-stu-id="34bbf-271">Create hello availability group endpoints on hello SQL Server VMs and set hello proper permissions on hello endpoints.</span></span>

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. <span data-ttu-id="34bbf-272">建立 hello 可用性複本。</span><span class="sxs-lookup"><span data-stu-id="34bbf-272">Create hello availability replicas.</span></span>

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. <span data-ttu-id="34bbf-273">最後，建立 hello 可用性群組和聯結 hello 次要複本 toohello 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="34bbf-273">Finally, create hello availability group and join hello secondary replica toohello availability group.</span></span>

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a><span data-ttu-id="34bbf-274">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34bbf-274">Next steps</span></span>
<span data-ttu-id="34bbf-275">現在，您已透過在 Azure 中建立可用性群組的方式，成功實作 SQL Server Always On。</span><span class="sxs-lookup"><span data-stu-id="34bbf-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="34bbf-276">tooconfigure 這個可用性群組接聽程式，請參閱[在 Azure 中設定 Alwayson 可用性群組的 ILB 接聽程式](../classic/ps-sql-int-listener.md)。</span><span class="sxs-lookup"><span data-stu-id="34bbf-276">tooconfigure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="34bbf-277">如需在 Azure 中使用 SQL Server 的其他資訊，請參閱 [Azure 虛擬機器上的 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="34bbf-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
