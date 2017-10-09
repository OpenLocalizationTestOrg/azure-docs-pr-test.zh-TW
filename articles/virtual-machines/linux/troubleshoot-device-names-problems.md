---
title: "在 Azure 中會變更 aaaLinux VM 裝置名稱 |Microsoft 文件"
description: "說明的 hello 為何裝置名稱已變更，並提供此問題的解決方案。"
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
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="95c69-103">疑難排解：Linux VM 裝置名稱已變更</span><span class="sxs-lookup"><span data-stu-id="95c69-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="95c69-104">hello 文件說明之後您重新啟動 Linux 虛擬機器 (VM)，或重新附加 hello 磁碟的裝置名稱變更原因。</span><span class="sxs-lookup"><span data-stu-id="95c69-104">hello article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach hello disks.</span></span> <span data-ttu-id="95c69-105">它也會提供有關此問題的 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="95c69-105">It also provides hello solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="95c69-106">徵狀</span><span class="sxs-lookup"><span data-stu-id="95c69-106">Symptom</span></span>

<span data-ttu-id="95c69-107">您可能會遇到 hello 在 Microsoft Azure 中執行 Linux Vm 時，下列問題。</span><span class="sxs-lookup"><span data-stu-id="95c69-107">You may experience hello following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="95c69-108">hello VM 會 tooboot 失敗後重新啟動。</span><span class="sxs-lookup"><span data-stu-id="95c69-108">hello VM fails tooboot after a restart.</span></span>

- <span data-ttu-id="95c69-109">如果會卸離資料磁碟，並將其重新附加，則會變更磁碟的 hello 裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="95c69-109">If data disks are detached and reattached, hello devices names for disks are changed.</span></span>

- <span data-ttu-id="95c69-110">使用裝置名稱參考磁碟的應用程式或指令碼就會失敗。</span><span class="sxs-lookup"><span data-stu-id="95c69-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="95c69-111">您會發現該 hello hello 磁碟裝置名稱會變更。</span><span class="sxs-lookup"><span data-stu-id="95c69-111">You find that hello device name of hello disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="95c69-112">原因</span><span class="sxs-lookup"><span data-stu-id="95c69-112">Cause</span></span>

<span data-ttu-id="95c69-113">在 Linux 中的裝置路徑不保證 toobe 一致重新啟動時。</span><span class="sxs-lookup"><span data-stu-id="95c69-113">Device paths in Linux are not guaranteed toobe consistent across restarts.</span></span> <span data-ttu-id="95c69-114">裝置名稱是由主要 (字母) 和次要的數字所組成。</span><span class="sxs-lookup"><span data-stu-id="95c69-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="95c69-115">當 hello Linux 儲存裝置驅動程式偵測到新的裝置時，則它會將主要和次要的裝置數字 tooit 指派從 hello 可用範圍。</span><span class="sxs-lookup"><span data-stu-id="95c69-115">When hello Linux storage device driver detects a new device, it assigns major and minor device numbers tooit from hello available range.</span></span> <span data-ttu-id="95c69-116">移除裝置時，hello 裝置號碼將會釋放的 toobe 稍後重複使用。</span><span class="sxs-lookup"><span data-stu-id="95c69-116">When a device is removed, hello device numbers are freed toobe reused later.</span></span>

<span data-ttu-id="95c69-117">hello 問題起因 hello 裝置中 Linux hello SCSI 子系統所排定的掃描會以非同步的方式。</span><span class="sxs-lookup"><span data-stu-id="95c69-117">hello problem occurs because hello device scanning in Linux scheduled by hello SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="95c69-118">重新啟動時可能會有所不同 hello 最終的裝置路徑命名。</span><span class="sxs-lookup"><span data-stu-id="95c69-118">hello final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="95c69-119">方案</span><span class="sxs-lookup"><span data-stu-id="95c69-119">Solution</span></span>

<span data-ttu-id="95c69-120">tooresolve 這個問題，請使用持續性命名。</span><span class="sxs-lookup"><span data-stu-id="95c69-120">tooresolve this problem, use persistent naming.</span></span> <span data-ttu-id="95c69-121">有四個方法 toopersistent 命名的檔案系統標籤、 uuid、 識別碼以及依路徑。</span><span class="sxs-lookup"><span data-stu-id="95c69-121">There are four methods toopersistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="95c69-122">我們建議 hello 檔案系統標籤和 UUID 方法適用於 Azure Linux Vm。</span><span class="sxs-lookup"><span data-stu-id="95c69-122">We recommend hello filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="95c69-123">多數散發也提供任一 hello **nofail**或**nobootwait** fstab 選項。</span><span class="sxs-lookup"><span data-stu-id="95c69-123">Most distributions also provide either hello **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="95c69-124">這些選項可讓系統 tooboot 即使 hello 磁碟失敗 toomount 在啟動時。</span><span class="sxs-lookup"><span data-stu-id="95c69-124">These options enable a system tooboot even if hello disk fails toomount at startup.</span></span> <span data-ttu-id="95c69-125">查看 hello 發佈文件，如需有關這些參數。</span><span class="sxs-lookup"><span data-stu-id="95c69-125">Check hello distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="95c69-126">如需有關如何 tooconfigure Linux VM toouse UUID，當您將加入資料磁碟，請參閱[連接 toohello Linux VM toomount hello 新磁碟](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk)。</span><span class="sxs-lookup"><span data-stu-id="95c69-126">For more information about how tooconfigure a Linux VM toouse a UUID when you add a data disk, see [Connect toohello Linux VM toomount hello new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="95c69-127">在 VM 上安裝 hello Azure Linux 代理程式時，它會使用 Udev 規則 tooconstruct 符號連結，在下一組**/dev/disk/azure**。</span><span class="sxs-lookup"><span data-stu-id="95c69-127">When hello Azure Linux agent is installed on a VM, it uses Udev rules tooconstruct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="95c69-128">應用程式可以使用這些 Udev 規則和指令碼 tooidentify 磁碟都連接的 toohello VM，其類型 hello LUN。</span><span class="sxs-lookup"><span data-stu-id="95c69-128">These Udev rules can be used by applications and scripts tooidentify disks are attached toohello VM, their type, and hello LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="95c69-129">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="95c69-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="95c69-130">識別磁碟 LUN</span><span class="sxs-lookup"><span data-stu-id="95c69-130">Identify disk LUNs</span></span>

<span data-ttu-id="95c69-131">應用程式可以使用 Lun toofind 所有 hello 附加磁碟及建構的符號連結。</span><span class="sxs-lookup"><span data-stu-id="95c69-131">An application can use LUNs toofind all hello attached disks and constructing symbolic links.</span></span> <span data-ttu-id="95c69-132">hello Azure Linux 代理程式現在包含 udev 規則設定符號連結，並從 LUN toohello 裝置，如下所示：</span><span class="sxs-lookup"><span data-stu-id="95c69-132">hello Azure Linux agent now includes udev rules that set up symbolic links from a LUN toohello devices, as follows:</span></span>

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
                                 

<span data-ttu-id="95c69-133">LUN 資訊也可以擷取從 hello Linux 客體使用 lsscsi 或類似的工具，如下所示。</span><span class="sxs-lookup"><span data-stu-id="95c69-133">LUN information can also be retrieved from hello Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="95c69-134">此客體 LUN 資訊可以搭配 Azure 訂用帳戶中繼資料 tooidentify hello Azure 儲存體中的位置 hello 可儲存 hello 分割區資料的 VHD。</span><span class="sxs-lookup"><span data-stu-id="95c69-134">This guest LUN information can be used with Azure subscription metadata tooidentify hello location in Azure storage of hello VHD which stores hello partition data.</span></span> <span data-ttu-id="95c69-135">例如，使用 hello az cli:</span><span class="sxs-lookup"><span data-stu-id="95c69-135">For example, use hello az cli:</span></span>

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="95c69-136">使用 blkid 探索 filesystem UUID</span><span class="sxs-lookup"><span data-stu-id="95c69-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="95c69-137">指令碼或應用程式可以讀取 hello 輸出 blkid 或類似的資訊來源，並建構中的符號連結**/dev**供使用。</span><span class="sxs-lookup"><span data-stu-id="95c69-137">A script or application can read hello output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="95c69-138">hello 輸出會顯示 hello 的所有磁碟 Uuid 附加 toohello VM 和 hello 裝置檔案 toowhich 與其相關聯：</span><span class="sxs-lookup"><span data-stu-id="95c69-138">hello output will show hello UUIDs of all disks attached toohello VM and hello device file toowhich they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="95c69-139">hello waagent udev 規則建構符號 下的連結集**/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="95c69-139">hello waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="95c69-140">hello 應用程式可以使用這項資訊找出 hello 開機磁碟裝置與 hello 資源 （臨時） 磁碟。</span><span class="sxs-lookup"><span data-stu-id="95c69-140">hello application can use this information identify hello boot disk device and hello resource (ephemeral) disk.</span></span> <span data-ttu-id="95c69-141">在 Azure 中，應用程式應該會參考太**/dev/disk/azure/root-part1**或**/dev/disk/azure-resource-part1** toodiscover 這些資料分割。</span><span class="sxs-lookup"><span data-stu-id="95c69-141">In Azure, applications should refer too**/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** toodiscover these partitions.</span></span>

<span data-ttu-id="95c69-142">如果沒有其他分割區從 hello blkid 清單，它們位於資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="95c69-142">If there are additional partitions from hello blkid list, they reside on a data disk.</span></span> <span data-ttu-id="95c69-143">應用程式可以維護這些資料分割的 hello UUID 和在執行階段使用的路徑，如 toodiscover hello 裝置名稱下方的 hello:</span><span class="sxs-lookup"><span data-stu-id="95c69-143">Applications can maintain hello UUID for these partitions and use a path like hello below toodiscover hello device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a><span data-ttu-id="95c69-144">取得最新 Azure 儲存體規則 hello</span><span class="sxs-lookup"><span data-stu-id="95c69-144">Get hello latest Azure storage rules</span></span>

<span data-ttu-id="95c69-145">toohello 最新的 Azure 儲存體規則，執行下列命令的第個：</span><span class="sxs-lookup"><span data-stu-id="95c69-145">toohello latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="95c69-146">如需詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="95c69-146">For more information, see hello following articles:</span></span>

- <span data-ttu-id="95c69-147">[Ubuntu：使用 UUID](https://help.ubuntu.com/community/UsingUUID) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="95c69-147">[Ubuntu: Using UUID](https://help.ubuntu.com/community/UsingUUID)</span></span>

- <span data-ttu-id="95c69-148">[Red Hat：永續性命名](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="95c69-148">[Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)</span></span>

- <span data-ttu-id="95c69-149">[Linux：UUID 可為您做些什麼](https://www.linux.com/news/what-uuids-can-do-you) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="95c69-149">[Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you)</span></span>

- [<span data-ttu-id="95c69-150">Udev： 簡介 tooDevice 現代 Linux 系統中管理</span><span class="sxs-lookup"><span data-stu-id="95c69-150">Udev: Introduction tooDevice Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

