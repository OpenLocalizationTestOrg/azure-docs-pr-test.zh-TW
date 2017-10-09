---
title: "aaaCreate 和上傳 FreeBSD VM 映像 |Microsoft 文件"
description: "了解 toocreate 並上傳虛擬硬碟 (VHD)，其中包含 hello FreeBSD 作業系統 toocreate Azure 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a><span data-ttu-id="c778c-103">建立及上傳 VHD FreeBSD tooAzure</span><span class="sxs-lookup"><span data-stu-id="c778c-103">Create and upload a FreeBSD VHD tooAzure</span></span>
<span data-ttu-id="c778c-104">本文章將示範如何 toocreate 和上傳虛擬硬碟 (VHD)，其中包含 hello FreeBSD 作業系統。</span><span class="sxs-lookup"><span data-stu-id="c778c-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello FreeBSD operating system.</span></span> <span data-ttu-id="c778c-105">將它上傳之後，您可以為您自己的映像 toocreate Azure 中的虛擬機器 (VM) 使用它。</span><span class="sxs-lookup"><span data-stu-id="c778c-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c778c-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="c778c-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c778c-107">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="c778c-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="c778c-108">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="c778c-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="c778c-109">如需上傳 VHD 使用 hello 資源管理員模型資訊，請參閱[這裡](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c778c-109">For information about uploading a VHD using hello Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c778c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c778c-110">Prerequisites</span></span>
<span data-ttu-id="c778c-111">本文假設您有下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c778c-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="c778c-112">**Azure 訂用帳戶**-- 如果您沒有，只需要幾分鐘的時間就可以建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="c778c-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="c778c-113">如果您有 MSDN 訂用帳戶，請參閱 [Visual Studio 訂閱者的每月 Azure 點數](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。</span><span class="sxs-lookup"><span data-stu-id="c778c-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="c778c-114">否則，了解如何太[建立免費的試用帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="c778c-114">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="c778c-115">**Azure PowerShell 工具**-hello Azure PowerShell 模組必須安裝並設定 toouse 您 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c778c-115">**Azure PowerShell tools**--hello Azure PowerShell module must be installed and configured toouse your Azure subscription.</span></span> <span data-ttu-id="c778c-116">toodownload hello 模組，請參閱[Azure 下載](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="c778c-116">toodownload hello module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="c778c-117">教學課程，描述如何 tooinstall 及設定這裡會提供 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="c778c-117">A tutorial that describes how tooinstall and configure hello module is available here.</span></span> <span data-ttu-id="c778c-118">使用 hello [Azure 下載](https://azure.microsoft.com/downloads/)cmdlet tooupload hello VHD。</span><span class="sxs-lookup"><span data-stu-id="c778c-118">Use hello [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.</span></span>
* <span data-ttu-id="c778c-119">**安裝中的.vhd 檔案的 FreeBSD 作業系統**-支援的 FreeBSD 作業系統必須安裝 tooa 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="c778c-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="c778c-120">多個工具存在 toocreate.vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="c778c-120">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="c778c-121">例如，您可以使用的虛擬化解決方案，例如 HYPER-V toocreate hello.vhd 檔案，並安裝 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="c778c-121">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="c778c-122">如需有關如何 tooinstall 並使用 HYPER-V，請參閱指示[安裝 HYPER-V 並建立虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c778c-122">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c778c-123">在 Azure 中不支援 hello 較新的 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="c778c-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="c778c-124">您可以使用 HYPER-V 管理員轉換 hello 磁碟 tooVHD 格式或 hello cmdlet[轉換-vhd](https://technet.microsoft.com/library/hh848454.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c778c-124">You can convert hello disk tooVHD format by using Hyper-V Manager or hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="c778c-125">此外，還有[MSDN 上的方式相關教學課程 toouse hyper-v FreeBSD](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c778c-125">In addition, there is a [tutorial on MSDN about how toouse FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="c778c-126">這項工作包含五個步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c778c-126">This task includes hello following five steps:</span></span>

## <a name="step-1-prepare-hello-image-for-upload"></a><span data-ttu-id="c778c-127">步驟 1： 準備上傳 hello 映像</span><span class="sxs-lookup"><span data-stu-id="c778c-127">Step 1: Prepare hello image for upload</span></span>
<span data-ttu-id="c778c-128">Hello 虛擬機器上安裝 hello FreeBSD 作業系統，完成下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="c778c-128">On hello virtual machine where you installed hello FreeBSD operating system, complete hello following procedures:</span></span>

1. <span data-ttu-id="c778c-129">啟用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="c778c-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="c778c-130">啟用 SSH。</span><span class="sxs-lookup"><span data-stu-id="c778c-130">Enable SSH.</span></span>

    <span data-ttu-id="c778c-131">請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。</span><span class="sxs-lookup"><span data-stu-id="c778c-131">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="c778c-132">根據預設，它從 FreeBSD 光碟安裝之後就會啟用。</span><span class="sxs-lookup"><span data-stu-id="c778c-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="c778c-133">設定序列主控台。</span><span class="sxs-lookup"><span data-stu-id="c778c-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="c778c-134">安裝 sudo。</span><span class="sxs-lookup"><span data-stu-id="c778c-134">Install sudo.</span></span>

    <span data-ttu-id="c778c-135">hello 根帳戶已停用在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="c778c-135">hello root account is disabled in Azure.</span></span> <span data-ttu-id="c778c-136">這表示您需要以提高權限的無特殊權限的使用者 toorun 命令 tooutilize sudo。</span><span class="sxs-lookup"><span data-stu-id="c778c-136">This means you need tooutilize sudo from an unprivileged user toorun commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="c778c-137">Azure 代理程式的必要條件。</span><span class="sxs-lookup"><span data-stu-id="c778c-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="c778c-138">安裝 Azure 代理程式。</span><span class="sxs-lookup"><span data-stu-id="c778c-138">Install Azure Agent.</span></span>

    <span data-ttu-id="c778c-139">hello hello Azure 代理程式的最新版本能找到上[github](https://github.com/Azure/WALinuxAgent/releases)。</span><span class="sxs-lookup"><span data-stu-id="c778c-139">hello latest release of hello Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="c778c-140">hello 版本 2.0.10 + 正式支援 FreeBSD 10 10.1，與 hello 2.1.4 + （包括 2.2.x） 正式支援 FreeBSD 10.2 和更新版本的版本。</span><span class="sxs-lookup"><span data-stu-id="c778c-140">hello version 2.0.10 + officially supports FreeBSD 10 & 10.1, and hello version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="c778c-141">針對 2.0 版，以下使用 2.0.16 做為範例：</span><span class="sxs-lookup"><span data-stu-id="c778c-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="c778c-142">針對 2.1 版，以下使用 2.1.4 做為範例：</span><span class="sxs-lookup"><span data-stu-id="c778c-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="c778c-143">安裝 Azure 代理程式之後，它是個不錯的主意 tooverify 它正在執行：</span><span class="sxs-lookup"><span data-stu-id="c778c-143">After you install Azure Agent, it's a good idea tooverify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="c778c-144">取消佈建 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="c778c-144">Deprovision hello system.</span></span>

    <span data-ttu-id="c778c-145">取消佈建 hello 系統 tooclean，並讓它適用於重新佈建。</span><span class="sxs-lookup"><span data-stu-id="c778c-145">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="c778c-146">hello 下列命令也會刪除 hello 最後一個佈建的使用者帳戶和相關聯的 hello 資料：</span><span class="sxs-lookup"><span data-stu-id="c778c-146">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="c778c-147">現在您可以關閉您的 VM。</span><span class="sxs-lookup"><span data-stu-id="c778c-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="c778c-148">步驟 2：在 Azure 中建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c778c-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="c778c-149">您需要 Azure tooupload.vhd 檔案的儲存體帳戶，所以您可能會使用的 toocreate 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c778c-149">You need a storage account in Azure tooupload a .vhd file so it can be used toocreate a virtual machine.</span></span> <span data-ttu-id="c778c-150">您可以使用 hello Azure 傳統入口網站 toocreate 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c778c-150">You can use hello Azure classic portal toocreate a storage account.</span></span>

1. <span data-ttu-id="c778c-151">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="c778c-151">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c778c-152">在 hello 命令列中，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="c778c-152">On hello command bar, select **New**.</span></span>
3. <span data-ttu-id="c778c-153">選取 [資料服務] > [儲存體]  > [快速建立]。</span><span class="sxs-lookup"><span data-stu-id="c778c-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![快速建立儲存體帳戶](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="c778c-155">填滿 hello 的欄位，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c778c-155">Fill out hello fields as follows:</span></span>

   * <span data-ttu-id="c778c-156">在 hello **URL**欄位中，輸入子網域名稱 toouse hello 儲存體帳戶 URL。</span><span class="sxs-lookup"><span data-stu-id="c778c-156">In hello **URL** field, type a subdomain name toouse in hello storage account URL.</span></span> <span data-ttu-id="c778c-157">hello 項目可以包含 3-24 數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="c778c-157">hello entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="c778c-158">這個名稱會變成 hello hello URL 使用的 tooaddress Azure Blob 儲存體、 Azure 佇列儲存體或 Azure 資料表儲存體資源 hello 訂用帳戶內的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="c778c-158">This name becomes hello host name within hello URL that is used tooaddress Azure Blob storage, Azure Queue storage, or Azure Table storage resources for hello subscription.</span></span>
   * <span data-ttu-id="c778c-159">在 hello**位置/同質群組**下拉式選單中，選擇 hello**位置或同質群組**hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c778c-159">In hello **Location/Affinity Group** drop-down menu, choose hello **location or affinity group** for hello storage account.</span></span> <span data-ttu-id="c778c-160">同質群組可讓您將雲端服務和儲存體放在 hello 相同的資料中心。</span><span class="sxs-lookup"><span data-stu-id="c778c-160">An affinity group lets you put your cloud services and storage in hello same data center.</span></span>
   * <span data-ttu-id="c778c-161">在 hello**複寫**欄位中，決定是否 toouse**異地備援**hello 儲存體帳戶的複寫。</span><span class="sxs-lookup"><span data-stu-id="c778c-161">In hello **Replication** field, decide whether toouse **Geo-Redundant** replication for hello storage account.</span></span> <span data-ttu-id="c778c-162">依預設會開啟異地複寫。</span><span class="sxs-lookup"><span data-stu-id="c778c-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="c778c-163">此選項會將複寫資料 tooa 次要位置，在沒有成本 tooyou，使您的儲存體容錯移轉 toothat 位置，如果主要的失敗，就會發生在 hello 主要位置。</span><span class="sxs-lookup"><span data-stu-id="c778c-163">This option replicates your data tooa secondary location, at no cost tooyou, so that your storage fails over toothat location if a major failure occurs at hello primary location.</span></span> <span data-ttu-id="c778c-164">hello 次要位置會自動指派，而且無法變更。</span><span class="sxs-lookup"><span data-stu-id="c778c-164">hello secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="c778c-165">如果您需要更充分掌控您的雲端儲存體 toolegal 需求或組織的原則到期的 hello 位置時，您可以關閉地理複寫。</span><span class="sxs-lookup"><span data-stu-id="c778c-165">If you need more control over hello location of your cloud-based storage due toolegal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="c778c-166">不過，請注意，如果您稍後啟用異地複寫，您將會產生單次資料傳輸費用 tooreplicate 您現有的資料 toohello 次要位置。</span><span class="sxs-lookup"><span data-stu-id="c778c-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee tooreplicate your existing data toohello secondary location.</span></span> <span data-ttu-id="c778c-167">不含異地複寫的儲存服務會有相對的折扣。</span><span class="sxs-lookup"><span data-stu-id="c778c-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="c778c-168">如需深入了解如何管理儲存體帳戶的異地複寫，請參閱：[Azure 儲存體複寫](../../../storage/common/storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="c778c-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![輸入儲存體帳戶詳細資料](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="c778c-170">選取 [建立儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="c778c-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="c778c-171">hello 帳戶現在會出現在**儲存體**。</span><span class="sxs-lookup"><span data-stu-id="c778c-171">hello account now appears under **storage**.</span></span>

    ![已成功建立儲存體帳戶](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="c778c-173">接下來，為您上傳的 .vhd 檔案建立容器。</span><span class="sxs-lookup"><span data-stu-id="c778c-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="c778c-174">選取 hello 儲存體帳戶名稱，然後再選取**容器**。</span><span class="sxs-lookup"><span data-stu-id="c778c-174">Select hello storage account name, and then select **Containers**.</span></span>

    ![儲存體帳戶詳細資訊](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="c778c-176">選取 [建立容器] 。</span><span class="sxs-lookup"><span data-stu-id="c778c-176">Select **Create a Container**.</span></span>

    ![儲存體帳戶詳細資訊](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="c778c-178">在 hello**名稱**欄位中，輸入您的容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="c778c-178">In hello **Name** field, type a name for your container.</span></span> <span data-ttu-id="c778c-179">然後，在 hello**存取**下拉式功能表上，選取您想要的存取原則的型別。</span><span class="sxs-lookup"><span data-stu-id="c778c-179">Then, in hello **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![容器名稱](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="c778c-181">根據預設，hello 容器是私人的而且只能存取 hello 帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="c778c-181">By default, hello container is private and can only be accessed by hello account owner.</span></span> <span data-ttu-id="c778c-182">tooallow 公用讀取權限 toohello blob，在 [hello] 容器中，但 toohello 容器屬性和中繼資料，使用 hello**公用 Blob**選項。</span><span class="sxs-lookup"><span data-stu-id="c778c-182">tooallow public read access toohello blobs in hello container, but not toohello container properties and metadata, use hello **Public Blob** option.</span></span> <span data-ttu-id="c778c-183">tooallow 完整公開讀取權限 hello 容器和 blob，請使用 hello**公用容器**選項。</span><span class="sxs-lookup"><span data-stu-id="c778c-183">tooallow full public read access for hello container and blobs, use hello **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a><span data-ttu-id="c778c-184">步驟 3： 準備 hello 連接 tooAzure</span><span class="sxs-lookup"><span data-stu-id="c778c-184">Step 3: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="c778c-185">您可以上傳.vhd 檔案之前，您會需要您的電腦與您 Azure 訂用帳戶之間 tooestablish 安全連線。</span><span class="sxs-lookup"><span data-stu-id="c778c-185">Before you can upload a .vhd file, you need tooestablish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="c778c-186">您可以使用 hello Azure Active Directory (Azure AD) 方法或 hello 憑證方法 toodo 它。</span><span class="sxs-lookup"><span data-stu-id="c778c-186">You can use hello Azure Active Directory (Azure AD) method or hello certificate method toodo it.</span></span>

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a><span data-ttu-id="c778c-187">使用 Azure AD hello 方法 tooupload.vhd 檔案</span><span class="sxs-lookup"><span data-stu-id="c778c-187">Use hello Azure AD method tooupload a .vhd file</span></span>
1. <span data-ttu-id="c778c-188">開啟 hello Azure PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="c778c-188">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="c778c-189">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="c778c-189">Type hello following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="c778c-190">這個命令會開啟登入視窗，您可在此以您的工作或學校帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="c778c-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![PowerShell Window](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="c778c-192">Azure 驗證，並將儲存 hello 認證資訊。</span><span class="sxs-lookup"><span data-stu-id="c778c-192">Azure authenticates and saves hello credential information.</span></span> <span data-ttu-id="c778c-193">然後它會關閉 hello 視窗。</span><span class="sxs-lookup"><span data-stu-id="c778c-193">Then it closes hello window.</span></span>

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a><span data-ttu-id="c778c-194">使用 hello 憑證方法 tooupload.vhd 檔案</span><span class="sxs-lookup"><span data-stu-id="c778c-194">Use hello certificate method tooupload a .vhd file</span></span>
1. <span data-ttu-id="c778c-195">開啟 hello Azure PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="c778c-195">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="c778c-196">輸入：`Get-AzurePublishSettingsFile`。</span><span class="sxs-lookup"><span data-stu-id="c778c-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="c778c-197">在瀏覽器視窗開啟，並提示您 toodownload hello.publishsettings 檔案。</span><span class="sxs-lookup"><span data-stu-id="c778c-197">A browser window opens and prompts you toodownload hello .publishsettings file.</span></span> <span data-ttu-id="c778c-198">此檔案包含您 Azure 訂用帳戶的資訊和憑證。</span><span class="sxs-lookup"><span data-stu-id="c778c-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![瀏覽器下載頁面](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="c778c-200">儲存 hello.publishsettings 檔案。</span><span class="sxs-lookup"><span data-stu-id="c778c-200">Save hello .publishsettings file.</span></span>
5. <span data-ttu-id="c778c-201">類型： `Import-AzurePublishSettingsFile <PathToFile>`，其中`<PathToFile>`hello 完整路徑 toohello.publishsettings 檔案。</span><span class="sxs-lookup"><span data-stu-id="c778c-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is hello full path toohello .publishsettings file.</span></span>

   <span data-ttu-id="c778c-202">如需詳細資訊，請參閱 [開始使用 Azure Cmdlet](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c778c-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="c778c-203">如需有關安裝和設定 PowerShell 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c778c-203">For more information about installing and configuring PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-hello-vhd-file"></a><span data-ttu-id="c778c-204">步驟 4: Hello.vhd 檔案上傳</span><span class="sxs-lookup"><span data-stu-id="c778c-204">Step 4: Upload hello .vhd file</span></span>
<span data-ttu-id="c778c-205">當您上傳 hello.vhd 檔案時，您可以將它放 Blob 儲存的地方。</span><span class="sxs-lookup"><span data-stu-id="c778c-205">When you upload hello .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="c778c-206">以下是您上傳 hello 檔案時要使用的一些術語：</span><span class="sxs-lookup"><span data-stu-id="c778c-206">Following are some terms you will use when you upload hello file:</span></span>

* <span data-ttu-id="c778c-207">**BlobStorageURL**是 hello hello 您在步驟 2 中建立的儲存體帳戶的 URL。</span><span class="sxs-lookup"><span data-stu-id="c778c-207">**BlobStorageURL** is hello URL for hello storage account that you created in Step 2.</span></span>
* <span data-ttu-id="c778c-208">**YourImagesFolder**是 hello Blob 儲存容器所在 toostore 您的映像。</span><span class="sxs-lookup"><span data-stu-id="c778c-208">**YourImagesFolder** is hello container within Blob storage where you want toostore your images.</span></span>
* <span data-ttu-id="c778c-209">**VHDName** hello 標籤出現在 hello Azure 傳統入口網站 tooidentify hello 虛擬硬碟中。</span><span class="sxs-lookup"><span data-stu-id="c778c-209">**VHDName** is hello label that appears in hello Azure classic portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="c778c-210">**PathToVHDFile**是 hello 完整路徑和 hello.vhd 檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="c778c-210">**PathToVHDFile** is hello full path and name of hello .vhd file.</span></span>

<span data-ttu-id="c778c-211">從 hello Azure PowerShell 視窗 hello 先前步驟中，輸入：</span><span class="sxs-lookup"><span data-stu-id="c778c-211">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a><span data-ttu-id="c778c-212">步驟 5： 建立 VM 與 hello 上傳的.vhd 檔案</span><span class="sxs-lookup"><span data-stu-id="c778c-212">Step 5: Create a VM with hello uploaded .vhd file</span></span>
<span data-ttu-id="c778c-213">Hello.vhd 檔案上傳之後，您可以將它當做自訂映像，都與您訂用帳戶相關聯的自訂映像建立虛擬機器的映像 toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="c778c-213">After you upload hello .vhd file, you can add it as an image toohello list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="c778c-214">從 hello Azure PowerShell 視窗 hello 先前步驟中，輸入：</span><span class="sxs-lookup"><span data-stu-id="c778c-214">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > <span data-ttu-id="c778c-215">使用 Linux hello OS 類型。</span><span class="sxs-lookup"><span data-stu-id="c778c-215">Use Linux as hello OS type.</span></span> <span data-ttu-id="c778c-216">hello 新版 Azure PowerShell 接受只有"Linux"或"Windows"做為參數。</span><span class="sxs-lookup"><span data-stu-id="c778c-216">hello current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="c778c-217">當您選擇 hello，完成 hello 上述步驟後，會列出 hello 新映像**映像**hello Azure 傳統入口網站上的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c778c-217">After you complete hello previous steps, hello new image is listed when you choose hello **Images** tab on hello Azure classic portal.</span></span>  

    ![Choose an image](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="c778c-219">從 hello 組件庫中建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c778c-219">Create a virtual machine from hello gallery.</span></span> <span data-ttu-id="c778c-220">這個新映像現在會出現在 [我的映像] 下。</span><span class="sxs-lookup"><span data-stu-id="c778c-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="c778c-221">選取 hello 新映像。</span><span class="sxs-lookup"><span data-stu-id="c778c-221">Select hello new image.</span></span> <span data-ttu-id="c778c-222">接下來，瀏覽 hello 提示 tooset 註冊主機名稱、 密碼、 SSH 金鑰和等等。</span><span class="sxs-lookup"><span data-stu-id="c778c-222">Next, go through hello prompts tooset up a host name, password, SSH key, and so on.</span></span>

    ![自訂映像](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="c778c-224">Hello 佈建完成之後，您會看到 FreeBSD VM 在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="c778c-224">After you complete hello provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Azure 中的 FreeBSD 映像](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
