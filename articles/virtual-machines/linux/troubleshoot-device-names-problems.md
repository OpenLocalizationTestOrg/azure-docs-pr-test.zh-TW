---
title: "在 Azure 中 Linux VM 裝置名稱已變更 | Microsoft Docs"
description: "說明裝置名稱變更的原因，並提供此問題的解決方案。"
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 789f4580901a22dc3aaae9599c7205c76f268403
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="c8619-103">疑難排解：Linux VM 裝置名稱已變更</span><span class="sxs-lookup"><span data-stu-id="c8619-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="c8619-104">本文說明在您重新啟動 Linux 虛擬機器 (VM) 或重新連接磁碟之後，裝置名稱變更的原因。</span><span class="sxs-lookup"><span data-stu-id="c8619-104">The article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach the disks.</span></span> <span data-ttu-id="c8619-105">它也會提供此問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="c8619-105">It also provides the solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="c8619-106">徵狀</span><span class="sxs-lookup"><span data-stu-id="c8619-106">Symptom</span></span>

<span data-ttu-id="c8619-107">在 Microsoft Azure 中執行 Linux VM 時，您可能會遇到下列問題。</span><span class="sxs-lookup"><span data-stu-id="c8619-107">You may experience the following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="c8619-108">VM 在重新啟動之後無法開機。</span><span class="sxs-lookup"><span data-stu-id="c8619-108">The VM fails to boot after a restart.</span></span>

- <span data-ttu-id="c8619-109">如果中斷連結並重新連接資料磁碟，磁碟的裝置名稱即會變更。</span><span class="sxs-lookup"><span data-stu-id="c8619-109">If data disks are detached and reattached, the devices names for disks are changed.</span></span>

- <span data-ttu-id="c8619-110">使用裝置名稱參考磁碟的應用程式或指令碼就會失敗。</span><span class="sxs-lookup"><span data-stu-id="c8619-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="c8619-111">您發現磁碟的裝置名稱已變更。</span><span class="sxs-lookup"><span data-stu-id="c8619-111">You find that the device name of the disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="c8619-112">原因</span><span class="sxs-lookup"><span data-stu-id="c8619-112">Cause</span></span>

<span data-ttu-id="c8619-113">Linux 中的裝置路徑不保證會在重新啟動之間保持一致。</span><span class="sxs-lookup"><span data-stu-id="c8619-113">Device paths in Linux are not guaranteed to be consistent across restarts.</span></span> <span data-ttu-id="c8619-114">裝置名稱是由主要 (字母) 和次要的數字所組成。</span><span class="sxs-lookup"><span data-stu-id="c8619-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="c8619-115">當 Linux 儲存裝置驅動程式偵測到新的裝置時，它會從可用範圍中指派主要和次要裝置號碼給它。</span><span class="sxs-lookup"><span data-stu-id="c8619-115">When the Linux storage device driver detects a new device, it assigns major and minor device numbers to it from the available range.</span></span> <span data-ttu-id="c8619-116">移除裝置時，即會釋放裝置號碼，以供稍後重複使用。</span><span class="sxs-lookup"><span data-stu-id="c8619-116">When a device is removed, the device numbers are freed to be reused later.</span></span>

<span data-ttu-id="c8619-117">問題發生原因是 Linux 中由 SCSI 子系統所排定的裝置掃描以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="c8619-117">The problem occurs because the device scanning in Linux scheduled by the SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="c8619-118">最終的裝置路徑命名可能會在重新啟動之間有所不同。</span><span class="sxs-lookup"><span data-stu-id="c8619-118">The final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="c8619-119">方案</span><span class="sxs-lookup"><span data-stu-id="c8619-119">Solution</span></span>

<span data-ttu-id="c8619-120">若要解決這個問題，請使用永續性命名。</span><span class="sxs-lookup"><span data-stu-id="c8619-120">To resolve this problem, use persistent naming.</span></span> <span data-ttu-id="c8619-121">有四種方法可用於永續性命名：依檔案系統標籤、依 uuid、依識別碼，以及依路徑。</span><span class="sxs-lookup"><span data-stu-id="c8619-121">There are four methods to persistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="c8619-122">我們建議針對 Azure Linux VM 使用檔案系統標籤和 UUID 方法。</span><span class="sxs-lookup"><span data-stu-id="c8619-122">We recommend the filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="c8619-123">大多數的發行版本也提供 **nofail** 或 **nobootwait** fstab 選項。</span><span class="sxs-lookup"><span data-stu-id="c8619-123">Most distributions also provide either the **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="c8619-124">即使磁碟在啟動時無法掛接，這些選項也能讓系統開機。</span><span class="sxs-lookup"><span data-stu-id="c8619-124">These options enable a system to boot even if the disk fails to mount at startup.</span></span> <span data-ttu-id="c8619-125">請檢查發行版本的文件，以取得這些參數的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c8619-125">Check the distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="c8619-126">如需如何在您新增資料磁碟時設定 Linux VM 以使用 UUID 的詳細資訊，請參閱[連接到 Linux VM 以掛接新磁碟](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk)。</span><span class="sxs-lookup"><span data-stu-id="c8619-126">For more information about how to configure a Linux VM to use a UUID when you add a data disk, see [Connect to the Linux VM to mount the new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="c8619-127">在 VM 上安裝 Azure Linux 代理程式時，它會使用 Udev 規則，在 **/dev/disk/azure** 下方建構一組符號連結。</span><span class="sxs-lookup"><span data-stu-id="c8619-127">When the Azure Linux agent is installed on a VM, it uses Udev rules to construct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="c8619-128">應用程式和指令碼可以使用這些 Udev 規則，來識別已將磁碟連接到 VM、其類型及 LUN。</span><span class="sxs-lookup"><span data-stu-id="c8619-128">These Udev rules can be used by applications and scripts to identify disks are attached to the VM, their type, and the LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="c8619-129">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="c8619-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="c8619-130">識別磁碟 LUN</span><span class="sxs-lookup"><span data-stu-id="c8619-130">Identify disk LUNs</span></span>

<span data-ttu-id="c8619-131">應用程式可以使用 LUN，來尋找所有連接的磁碟和建構符號連結。</span><span class="sxs-lookup"><span data-stu-id="c8619-131">An application can use LUNs to find all the attached disks and constructing symbolic links.</span></span> <span data-ttu-id="c8619-132">Azure Linux 代理程式現在包含 udev 規則，可將符號連結從 LUN 設定到裝置，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c8619-132">The Azure Linux agent now includes udev rules that set up symbolic links from a LUN to the devices, as follows:</span></span>

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

<span data-ttu-id="c8619-133">您也可以使用 lsscsi 或類似的工具，從 Linux 客體擷取 LUN 資訊，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c8619-133">LUN information can also be retrieved from the Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="c8619-134">此客體 LUN 資訊可以與 Azure 訂用帳戶中繼資料搭配使用，在儲存分割區資料之 VHD 的 Azure 儲存體中識別位置。</span><span class="sxs-lookup"><span data-stu-id="c8619-134">This guest LUN information can be used with Azure subscription metadata to identify the location in Azure storage of the VHD which stores the partition data.</span></span> <span data-ttu-id="c8619-135">例如，使用 az cli：</span><span class="sxs-lookup"><span data-stu-id="c8619-135">For example, use the az cli:</span></span>

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="c8619-136">使用 blkid 探索 filesystem UUID</span><span class="sxs-lookup"><span data-stu-id="c8619-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="c8619-137">指令碼或應用程式可以讀取 blkid 的輸出或類似的資訊來源，並在 **/dev** 中建構符號連結以供使用。</span><span class="sxs-lookup"><span data-stu-id="c8619-137">A script or application can read the output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="c8619-138">輸出將會顯示連接至 VM 之所有磁碟的 UUID，以及與其相關聯的裝置檔案：</span><span class="sxs-lookup"><span data-stu-id="c8619-138">The output will show the UUIDs of all disks attached to the VM and the device file to which they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="c8619-139">Waagent udev 規則會在 **/dev/disk/azure** 下方建構一組符號連結：</span><span class="sxs-lookup"><span data-stu-id="c8619-139">The waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="c8619-140">應用程式可以使用此資訊來識別開機磁碟裝置和資源 (暫時) 磁碟。</span><span class="sxs-lookup"><span data-stu-id="c8619-140">The application can use this information identify the boot disk device and the resource (ephemeral) disk.</span></span> <span data-ttu-id="c8619-141">在 Azure 中，應用程式應該參考 **/dev/disk/azure/root-part1** 或 **/dev/disk/azure-resource-part1**，以探索這些分割區。</span><span class="sxs-lookup"><span data-stu-id="c8619-141">In Azure, applications should refer to **/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** to discover these partitions.</span></span>

<span data-ttu-id="c8619-142">如果有其他來自 blkid 清單的分割區，則它們會位於資料磁碟上。</span><span class="sxs-lookup"><span data-stu-id="c8619-142">If there are additional partitions from the blkid list, they reside on a data disk.</span></span> <span data-ttu-id="c8619-143">應用程式可以維護這些分割區的 UUID，並使用如下的路徑，在執行階段探索裝置名稱：</span><span class="sxs-lookup"><span data-stu-id="c8619-143">Applications can maintain the UUID for these partitions and use a path like the below to discover the device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-the-latest-azure-storage-rules"></a><span data-ttu-id="c8619-144">取得最新的 Azure 儲存體規則</span><span class="sxs-lookup"><span data-stu-id="c8619-144">Get the latest Azure storage rules</span></span>

<span data-ttu-id="c8619-145">若要取得最新的 Azure 儲存體規則，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="c8619-145">To the latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="c8619-146">如需詳細資訊，請參閱下列文章。</span><span class="sxs-lookup"><span data-stu-id="c8619-146">For more information, see the following articles:</span></span>

- <span data-ttu-id="c8619-147">[Ubuntu：使用 UUID](https://help.ubuntu.com/community/UsingUUID) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="c8619-147">[Ubuntu: Using UUID](https://help.ubuntu.com/community/UsingUUID)</span></span>

- <span data-ttu-id="c8619-148">[Red Hat：永續性命名](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="c8619-148">[Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)</span></span>

- <span data-ttu-id="c8619-149">[Linux：UUID 可為您做些什麼](https://www.linux.com/news/what-uuids-can-do-you) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="c8619-149">[Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you)</span></span>

- <span data-ttu-id="c8619-150">[Udev：現代 Linux 系統中的裝置管理簡介](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="c8619-150">[Udev: Introduction to Device Management In Modern Linux System](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)</span></span>

