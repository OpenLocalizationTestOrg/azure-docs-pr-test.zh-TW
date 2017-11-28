---
title: "建立及上傳 FreeBSD VM 映像 | Microsoft Docs"
description: "了解如何建立及上傳包含 FreeBSD 作業系統的虛擬硬碟 (VHD)，以建立 Azure 虛擬機器。"
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
ms.openlocfilehash: 918f454784a9676297077c2e94c3e49ab2872d2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-freebsd-vhd-to-azure"></a><span data-ttu-id="a2377-103">建立並上傳 FreeBSD VHD 到 Azure</span><span class="sxs-lookup"><span data-stu-id="a2377-103">Create and upload a FreeBSD VHD to Azure</span></span>
<span data-ttu-id="a2377-104">本文說明如何建立及上傳包含 FreeBSD 作業系統的虛擬硬碟 (VHD)。</span><span class="sxs-lookup"><span data-stu-id="a2377-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the FreeBSD operating system.</span></span> <span data-ttu-id="a2377-105">上傳之後，您可以使用它做為您自己的映像在 Azure 中建立虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="a2377-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a2377-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="a2377-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a2377-107">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="a2377-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="a2377-108">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="a2377-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="a2377-109">如需使用 Resource Manager 模型上傳 VHD 的詳細資訊，請參閱[這裡](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a2377-109">For information about uploading a VHD using the Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2377-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a2377-110">Prerequisites</span></span>
<span data-ttu-id="a2377-111">本文假設您具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="a2377-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="a2377-112">**Azure 訂用帳戶**-- 如果您沒有，只需要幾分鐘的時間就可以建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2377-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="a2377-113">如果您有 MSDN 訂用帳戶，請參閱 [Visual Studio 訂閱者的每月 Azure 點數](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。</span><span class="sxs-lookup"><span data-stu-id="a2377-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="a2377-114">否則，請參閱 [建立免費試用帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a2377-114">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="a2377-115">**Azure PowerShell 工具**-- 必須已安裝 Azure PowerShell 模組，並設定為使用您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2377-115">**Azure PowerShell tools**--The Azure PowerShell module must be installed and configured to use your Azure subscription.</span></span> <span data-ttu-id="a2377-116">若要下載此模組，請參閱 [Azure 下載](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="a2377-116">To download the module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="a2377-117">這裡有一個說明如何安裝和設定此模組的教學課程。</span><span class="sxs-lookup"><span data-stu-id="a2377-117">A tutorial that describes how to install and configure the module is available here.</span></span> <span data-ttu-id="a2377-118">使用 [Azure Downloads](https://azure.microsoft.com/downloads/) Cmdlet 上傳 VHD。</span><span class="sxs-lookup"><span data-stu-id="a2377-118">Use the [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet to upload the VHD.</span></span>
* <span data-ttu-id="a2377-119">**安裝在 .vhd 檔案中的 FreeBSD 作業系統** -- 支援的 FreeBSD 作業系統必須已安裝到虛擬硬碟中。</span><span class="sxs-lookup"><span data-stu-id="a2377-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed to a virtual hard disk.</span></span> <span data-ttu-id="a2377-120">有多項工具可用來建立 .vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="a2377-120">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="a2377-121">例如，您可以使用虛擬化解決方案 (例如 Hyper-V) 建立 .vhd 檔案，並安裝作業系統。</span><span class="sxs-lookup"><span data-stu-id="a2377-121">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="a2377-122">如需相關指示，請參閱 [安裝 Hyper-V 和建立虛擬機器](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a2377-122">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="a2377-123">Azure 不支援較新的 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="a2377-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="a2377-124">您可以使用 Hyper-V 管理員或 [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx)Cmdlet，將磁碟轉換為 VHD 格式。</span><span class="sxs-lookup"><span data-stu-id="a2377-124">You can convert the disk to VHD format by using Hyper-V Manager or the cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="a2377-125">此外，還有 [MSDN 上有關如何使用 FreeBSD 搭配 Hyper-V 的教學課程](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a2377-125">In addition, there is a [tutorial on MSDN about how to use FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="a2377-126">這項工作包含下列五個步驟：</span><span class="sxs-lookup"><span data-stu-id="a2377-126">This task includes the following five steps:</span></span>

## <a name="step-1-prepare-the-image-for-upload"></a><span data-ttu-id="a2377-127">步驟 1：準備要上傳的映像</span><span class="sxs-lookup"><span data-stu-id="a2377-127">Step 1: Prepare the image for upload</span></span>
<span data-ttu-id="a2377-128">在您已安裝 FreeBSD 作業系統的虛擬機器上，完成下列程序：</span><span class="sxs-lookup"><span data-stu-id="a2377-128">On the virtual machine where you installed the FreeBSD operating system, complete the following procedures:</span></span>

1. <span data-ttu-id="a2377-129">啟用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="a2377-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="a2377-130">啟用 SSH。</span><span class="sxs-lookup"><span data-stu-id="a2377-130">Enable SSH.</span></span>

    <span data-ttu-id="a2377-131">確定您已安裝 SSH 伺服器，並已設定為在開機時啟動。</span><span class="sxs-lookup"><span data-stu-id="a2377-131">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="a2377-132">根據預設，它從 FreeBSD 光碟安裝之後就會啟用。</span><span class="sxs-lookup"><span data-stu-id="a2377-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="a2377-133">設定序列主控台。</span><span class="sxs-lookup"><span data-stu-id="a2377-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="a2377-134">安裝 sudo。</span><span class="sxs-lookup"><span data-stu-id="a2377-134">Install sudo.</span></span>

    <span data-ttu-id="a2377-135">在 Azure 中已停用 root 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2377-135">The root account is disabled in Azure.</span></span> <span data-ttu-id="a2377-136">這表示您必須利用未授權的使用者 sudo 從較高權限執行命令。</span><span class="sxs-lookup"><span data-stu-id="a2377-136">This means you need to utilize sudo from an unprivileged user to run commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="a2377-137">Azure 代理程式的必要條件。</span><span class="sxs-lookup"><span data-stu-id="a2377-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="a2377-138">安裝 Azure 代理程式。</span><span class="sxs-lookup"><span data-stu-id="a2377-138">Install Azure Agent.</span></span>

    <span data-ttu-id="a2377-139">最新版的 Azure 代理程式一律可以在 [github](https://github.com/Azure/WALinuxAgent/releases)上找到。</span><span class="sxs-lookup"><span data-stu-id="a2377-139">The latest release of the Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="a2377-140">2.0.10 + 版正式支援 FreeBSD 10 和 10.1，2.1.4 版 (包括 2.2.x) 正式支援 FreeBSD 10.2 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="a2377-140">The version 2.0.10 + officially supports FreeBSD 10 & 10.1, and the version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="a2377-141">針對 2.0 版，以下使用 2.0.16 做為範例：</span><span class="sxs-lookup"><span data-stu-id="a2377-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="a2377-142">針對 2.1 版，以下使用 2.1.4 做為範例：</span><span class="sxs-lookup"><span data-stu-id="a2377-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="a2377-143">安裝 Azure 代理程式之後，最好先確認它正在執行︰</span><span class="sxs-lookup"><span data-stu-id="a2377-143">After you install Azure Agent, it's a good idea to verify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="a2377-144">取消佈建系統。</span><span class="sxs-lookup"><span data-stu-id="a2377-144">Deprovision the system.</span></span>

    <span data-ttu-id="a2377-145">取消佈建系統以清理系統，使之適合重新佈建。</span><span class="sxs-lookup"><span data-stu-id="a2377-145">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="a2377-146">下列命令也會刪除最後佈建的使用者帳戶和相關聯的資料：</span><span class="sxs-lookup"><span data-stu-id="a2377-146">The following command also deletes the last provisioned user account and the associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="a2377-147">現在您可以關閉您的 VM。</span><span class="sxs-lookup"><span data-stu-id="a2377-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="a2377-148">步驟 2：在 Azure 中建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a2377-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="a2377-149">必須要有 Azure 中的儲存體帳戶才能上傳 .vhd 檔案，以用來建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a2377-149">You need a storage account in Azure to upload a .vhd file so it can be used to create a virtual machine.</span></span> <span data-ttu-id="a2377-150">您可以使用 Azure 傳統入口網站來建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2377-150">You can use the Azure classic portal to create a storage account.</span></span>

1. <span data-ttu-id="a2377-151">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a2377-151">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a2377-152">在命令列上選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="a2377-152">On the command bar, select **New**.</span></span>
3. <span data-ttu-id="a2377-153">選取 [資料服務] > [儲存體]  > [快速建立]。</span><span class="sxs-lookup"><span data-stu-id="a2377-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![快速建立儲存體帳戶](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="a2377-155">依照下列方式填入欄位：</span><span class="sxs-lookup"><span data-stu-id="a2377-155">Fill out the fields as follows:</span></span>

   * <span data-ttu-id="a2377-156">在 [URL]  欄位中，輸入要在儲存體帳戶 URL 中使用的子網域名稱。</span><span class="sxs-lookup"><span data-stu-id="a2377-156">In the **URL** field, type a subdomain name to use in the storage account URL.</span></span> <span data-ttu-id="a2377-157">此項目可以包含 3 至 24 個數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="a2377-157">The entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="a2377-158">這個名稱會成為 URL 內用來為訂用帳戶的 Azure Blob 儲存體、Azure 佇列儲存體、或Azure 表格儲存體資源定址的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="a2377-158">This name becomes the host name within the URL that is used to address Azure Blob storage, Azure Queue storage, or Azure Table storage resources for the subscription.</span></span>
   * <span data-ttu-id="a2377-159">從 [位置/同質群組] 下拉式清單中，選取儲存體帳戶的 [位置或同質群組]。</span><span class="sxs-lookup"><span data-stu-id="a2377-159">In the **Location/Affinity Group** drop-down menu, choose the **location or affinity group** for the storage account.</span></span> <span data-ttu-id="a2377-160">同質群組可讓您將雲端服務和儲存體放在相同的資料中心。</span><span class="sxs-lookup"><span data-stu-id="a2377-160">An affinity group lets you put your cloud services and storage in the same data center.</span></span>
   * <span data-ttu-id="a2377-161">在 [複寫] 欄位中，決定儲存體帳戶是否要使用 [異地備援] 複寫。</span><span class="sxs-lookup"><span data-stu-id="a2377-161">In the **Replication** field, decide whether to use **Geo-Redundant** replication for the storage account.</span></span> <span data-ttu-id="a2377-162">依預設會開啟異地複寫。</span><span class="sxs-lookup"><span data-stu-id="a2377-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="a2377-163">此選項可讓您免費將資料複寫至次要位置，使您在主要位置發生重大錯誤時，可將儲存體容錯移轉至該位置。</span><span class="sxs-lookup"><span data-stu-id="a2377-163">This option replicates your data to a secondary location, at no cost to you, so that your storage fails over to that location if a major failure occurs at the primary location.</span></span> <span data-ttu-id="a2377-164">次要位置會自動指派，且無法變更。</span><span class="sxs-lookup"><span data-stu-id="a2377-164">The secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="a2377-165">如果您因為法律規定或組織原則而需要更充分掌控您以雲端為基礎的儲存體所在的位置，您可以關閉地理複寫。</span><span class="sxs-lookup"><span data-stu-id="a2377-165">If you need more control over the location of your cloud-based storage due to legal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="a2377-166">但請注意，如果您後續又開啟異地複寫，在您將現有的資料複寫至次要位置時，將會產生一次性的資料傳輸費用。</span><span class="sxs-lookup"><span data-stu-id="a2377-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee to replicate your existing data to the secondary location.</span></span> <span data-ttu-id="a2377-167">不含異地複寫的儲存服務會有相對的折扣。</span><span class="sxs-lookup"><span data-stu-id="a2377-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="a2377-168">如需深入了解如何管理儲存體帳戶的異地複寫，請參閱：[Azure 儲存體複寫](../../../storage/common/storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="a2377-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![輸入儲存體帳戶詳細資料](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="a2377-170">選取 [建立儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="a2377-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="a2377-171">帳戶現在會出現在 [儲存體] 下方。</span><span class="sxs-lookup"><span data-stu-id="a2377-171">The account now appears under **storage**.</span></span>

    ![已成功建立儲存體帳戶](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="a2377-173">接下來，為您上傳的 .vhd 檔案建立容器。</span><span class="sxs-lookup"><span data-stu-id="a2377-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="a2377-174">選取儲存體帳戶名稱，然後選取 [容器] 。</span><span class="sxs-lookup"><span data-stu-id="a2377-174">Select the storage account name, and then select **Containers**.</span></span>

    ![儲存體帳戶詳細資訊](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="a2377-176">選取 [建立容器] 。</span><span class="sxs-lookup"><span data-stu-id="a2377-176">Select **Create a Container**.</span></span>

    ![儲存體帳戶詳細資訊](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="a2377-178">在 [名稱]  欄位中，輸入容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="a2377-178">In the **Name** field, type a name for your container.</span></span> <span data-ttu-id="a2377-179">然後，在 [存取]  下拉式選單中，選取您想要的存取原則的類型。</span><span class="sxs-lookup"><span data-stu-id="a2377-179">Then, in the **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![容器名稱](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="a2377-181">容器預設為私人，且只能由帳戶擁有者存取。</span><span class="sxs-lookup"><span data-stu-id="a2377-181">By default, the container is private and can only be accessed by the account owner.</span></span> <span data-ttu-id="a2377-182">若要允許對容器中的 Blob 進行公開讀取存取，但不允許存取容器屬性和中繼資料，請使用 [公用 Blob] 選項。</span><span class="sxs-lookup"><span data-stu-id="a2377-182">To allow public read access to the blobs in the container, but not to the container properties and metadata, use the **Public Blob** option.</span></span> <span data-ttu-id="a2377-183">若要允許對容器和 Blob 進行完整的公開讀取存取，請使用 [ **公開容器** ] 選項。</span><span class="sxs-lookup"><span data-stu-id="a2377-183">To allow full public read access for the container and blobs, use the **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-the-connection-to-azure"></a><span data-ttu-id="a2377-184">步驟 3：準備 Azure 的連線</span><span class="sxs-lookup"><span data-stu-id="a2377-184">Step 3: Prepare the connection to Azure</span></span>
<span data-ttu-id="a2377-185">您必須先在電腦與 Azure 訂用帳戶之間建立安全連線，才能上傳 .vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="a2377-185">Before you can upload a .vhd file, you need to establish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="a2377-186">您可以使用 Azure Active Directory (Azure AD) 方法或憑證方法來這樣做。</span><span class="sxs-lookup"><span data-stu-id="a2377-186">You can use the Azure Active Directory (Azure AD) method or the certificate method to do it.</span></span>

### <a name="use-the-azure-ad-method-to-upload-a-vhd-file"></a><span data-ttu-id="a2377-187">使用 Azure AD 方法上傳 .vhd 檔案</span><span class="sxs-lookup"><span data-stu-id="a2377-187">Use the Azure AD method to upload a .vhd file</span></span>
1. <span data-ttu-id="a2377-188">開啟 Azure PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="a2377-188">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="a2377-189">輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="a2377-189">Type the following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="a2377-190">這個命令會開啟登入視窗，您可在此以您的工作或學校帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="a2377-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![PowerShell Window](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="a2377-192">Azure 會驗證並儲存認證資訊。</span><span class="sxs-lookup"><span data-stu-id="a2377-192">Azure authenticates and saves the credential information.</span></span> <span data-ttu-id="a2377-193">然後關閉視窗。</span><span class="sxs-lookup"><span data-stu-id="a2377-193">Then it closes the window.</span></span>

### <a name="use-the-certificate-method-to-upload-a-vhd-file"></a><span data-ttu-id="a2377-194">使用憑證方法上傳 .vhd 檔案</span><span class="sxs-lookup"><span data-stu-id="a2377-194">Use the certificate method to upload a .vhd file</span></span>
1. <span data-ttu-id="a2377-195">開啟 Azure PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="a2377-195">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="a2377-196">輸入：`Get-AzurePublishSettingsFile`。</span><span class="sxs-lookup"><span data-stu-id="a2377-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="a2377-197">隨即會開啟瀏覽器視窗，並提示您下載 .publishsettings 檔案。</span><span class="sxs-lookup"><span data-stu-id="a2377-197">A browser window opens and prompts you to download the .publishsettings file.</span></span> <span data-ttu-id="a2377-198">此檔案包含您 Azure 訂用帳戶的資訊和憑證。</span><span class="sxs-lookup"><span data-stu-id="a2377-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![瀏覽器下載頁面](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="a2377-200">儲存 .publishsettings 檔案。</span><span class="sxs-lookup"><span data-stu-id="a2377-200">Save the .publishsettings file.</span></span>
5. <span data-ttu-id="a2377-201">輸入：`Import-AzurePublishSettingsFile <PathToFile>`，其中的 `<PathToFile>` 是 .publishsettings 檔案的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="a2377-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is the full path to the .publishsettings file.</span></span>

   <span data-ttu-id="a2377-202">如需詳細資訊，請參閱 [開始使用 Azure Cmdlet](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a2377-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="a2377-203">如需安裝和設定 PowerShell 的詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a2377-203">For more information about installing and configuring PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-the-vhd-file"></a><span data-ttu-id="a2377-204">步驟 4：上傳 .vhd 檔案</span><span class="sxs-lookup"><span data-stu-id="a2377-204">Step 4: Upload the .vhd file</span></span>
<span data-ttu-id="a2377-205">在上傳 .vhd 檔案時，可以將 .vhd 檔案放在 Blob 儲存體中的任一處。</span><span class="sxs-lookup"><span data-stu-id="a2377-205">When you upload the .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="a2377-206">以下是您上傳檔案時將使用的一些詞彙︰</span><span class="sxs-lookup"><span data-stu-id="a2377-206">Following are some terms you will use when you upload the file:</span></span>

* <span data-ttu-id="a2377-207">**BlobStorageURL** 是您在步驟 2 建立的儲存體帳戶的 URL。</span><span class="sxs-lookup"><span data-stu-id="a2377-207">**BlobStorageURL** is the URL for the storage account that you created in Step 2.</span></span>
* <span data-ttu-id="a2377-208">**YourImagesFolder** 是您要用來儲存映像之 Blob 儲存體中的容器。</span><span class="sxs-lookup"><span data-stu-id="a2377-208">**YourImagesFolder** is the container within Blob storage where you want to store your images.</span></span>
* <span data-ttu-id="a2377-209">**VHDName** 是 Azure 傳統入口網站中，用來識別虛擬硬碟的顯示標籤。</span><span class="sxs-lookup"><span data-stu-id="a2377-209">**VHDName** is the label that appears in the Azure classic portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="a2377-210">**PathToVHDFile** 是 .vhd 檔案的完整路徑和名稱。</span><span class="sxs-lookup"><span data-stu-id="a2377-210">**PathToVHDFile** is the full path and name of the .vhd file.</span></span>

<span data-ttu-id="a2377-211">從您在上一個步驟使用的 Azure PowerShell 視窗中，輸入：</span><span class="sxs-lookup"><span data-stu-id="a2377-211">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-the-uploaded-vhd-file"></a><span data-ttu-id="a2377-212">步驟 5：以上傳的 .vhd 檔案建立 VM</span><span class="sxs-lookup"><span data-stu-id="a2377-212">Step 5: Create a VM with the uploaded .vhd file</span></span>
<span data-ttu-id="a2377-213">上傳 .vhd 檔案之後，您可以將其新增為與訂用帳戶相關之自訂映像清單中的映像，並使用此自訂映像建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a2377-213">After you upload the .vhd file, you can add it as an image to the list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="a2377-214">從您在上一個步驟使用的 Azure PowerShell 視窗中，輸入：</span><span class="sxs-lookup"><span data-stu-id="a2377-214">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of the VHD> -OS <Type of the OS on the VHD>

   > [!NOTE]
   > <span data-ttu-id="a2377-215">使用 Linux 做為作業系統類型。</span><span class="sxs-lookup"><span data-stu-id="a2377-215">Use Linux as the OS type.</span></span> <span data-ttu-id="a2377-216">目前的 Azure PowerShell 版本只接受 "Linux" 或 "Windows" 為參數。</span><span class="sxs-lookup"><span data-stu-id="a2377-216">The current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="a2377-217">完成前面的步驟之後，當您在 Azure 傳統入口網站上選擇 [映像]  索引標籤時，將會列出新的映像。</span><span class="sxs-lookup"><span data-stu-id="a2377-217">After you complete the previous steps, the new image is listed when you choose the **Images** tab on the Azure classic portal.</span></span>  

    ![Choose an image](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="a2377-219">從資源庫建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a2377-219">Create a virtual machine from the gallery.</span></span> <span data-ttu-id="a2377-220">這個新映像現在會出現在 [我的映像] 下。</span><span class="sxs-lookup"><span data-stu-id="a2377-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="a2377-221">選取新映像。</span><span class="sxs-lookup"><span data-stu-id="a2377-221">Select the new image.</span></span> <span data-ttu-id="a2377-222">接著，依照提示設定主機名稱、密碼、SSH 金鑰等項目。</span><span class="sxs-lookup"><span data-stu-id="a2377-222">Next, go through the prompts to set up a host name, password, SSH key, and so on.</span></span>

    ![自訂映像](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="a2377-224">佈建完成後，您會看到您的 FreeBSD VM 在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="a2377-224">After you complete the provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Azure 中的 FreeBSD 映像](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
