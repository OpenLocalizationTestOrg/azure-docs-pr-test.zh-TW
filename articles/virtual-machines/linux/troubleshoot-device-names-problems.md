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
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>疑難排解：Linux VM 裝置名稱已變更

hello 文件說明之後您重新啟動 Linux 虛擬機器 (VM)，或重新附加 hello 磁碟的裝置名稱變更原因。 它也會提供有關此問題的 hello 方案。

## <a name="symptom"></a>徵狀

您可能會遇到 hello 在 Microsoft Azure 中執行 Linux Vm 時，下列問題。

- hello VM 會 tooboot 失敗後重新啟動。

- 如果會卸離資料磁碟，並將其重新附加，則會變更磁碟的 hello 裝置名稱。

- 使用裝置名稱參考磁碟的應用程式或指令碼就會失敗。 您會發現該 hello hello 磁碟裝置名稱會變更。

## <a name="cause"></a>原因

在 Linux 中的裝置路徑不保證 toobe 一致重新啟動時。 裝置名稱是由主要 (字母) 和次要的數字所組成。  當 hello Linux 儲存裝置驅動程式偵測到新的裝置時，則它會將主要和次要的裝置數字 tooit 指派從 hello 可用範圍。 移除裝置時，hello 裝置號碼將會釋放的 toobe 稍後重複使用。

hello 問題起因 hello 裝置中 Linux hello SCSI 子系統所排定的掃描會以非同步的方式。 重新啟動時可能會有所不同 hello 最終的裝置路徑命名。 

## <a name="solution"></a>方案

tooresolve 這個問題，請使用持續性命名。 有四個方法 toopersistent 命名的檔案系統標籤、 uuid、 識別碼以及依路徑。 我們建議 hello 檔案系統標籤和 UUID 方法適用於 Azure Linux Vm。 

多數散發也提供任一 hello **nofail**或**nobootwait** fstab 選項。 這些選項可讓系統 tooboot 即使 hello 磁碟失敗 toomount 在啟動時。 查看 hello 發佈文件，如需有關這些參數。 如需有關如何 tooconfigure Linux VM toouse UUID，當您將加入資料磁碟，請參閱[連接 toohello Linux VM toomount hello 新磁碟](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk)。 

在 VM 上安裝 hello Azure Linux 代理程式時，它會使用 Udev 規則 tooconstruct 符號連結，在下一組**/dev/disk/azure**。 應用程式可以使用這些 Udev 規則和指令碼 tooidentify 磁碟都連接的 toohello VM，其類型 hello LUN。

## <a name="more-information"></a>詳細資訊

### <a name="identify-disk-luns"></a>識別磁碟 LUN

應用程式可以使用 Lun toofind 所有 hello 附加磁碟及建構的符號連結。 hello Azure Linux 代理程式現在包含 udev 規則設定符號連結，並從 LUN toohello 裝置，如下所示：

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
                                 

LUN 資訊也可以擷取從 hello Linux 客體使用 lsscsi 或類似的工具，如下所示。

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

此客體 LUN 資訊可以搭配 Azure 訂用帳戶中繼資料 tooidentify hello Azure 儲存體中的位置 hello 可儲存 hello 分割區資料的 VHD。 例如，使用 hello az cli:

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a>使用 blkid 探索 filesystem UUID

指令碼或應用程式可以讀取 hello 輸出 blkid 或類似的資訊來源，並建構中的符號連結**/dev**供使用。 hello 輸出會顯示 hello 的所有磁碟 Uuid 附加 toohello VM 和 hello 裝置檔案 toowhich 與其相關聯：

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

hello waagent udev 規則建構符號 下的連結集**/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


hello 應用程式可以使用這項資訊找出 hello 開機磁碟裝置與 hello 資源 （臨時） 磁碟。 在 Azure 中，應用程式應該會參考太**/dev/disk/azure/root-part1**或**/dev/disk/azure-resource-part1** toodiscover 這些資料分割。

如果沒有其他分割區從 hello blkid 清單，它們位於資料磁碟。 應用程式可以維護這些資料分割的 hello UUID 和在執行階段使用的路徑，如 toodiscover hello 裝置名稱下方的 hello:

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a>取得最新 Azure 儲存體規則 hello

toohello 最新的 Azure 儲存體規則，執行下列命令的第個：

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


如需詳細資訊，請參閱下列文章 hello:

- [Ubuntu：使用 UUID](https://help.ubuntu.com/community/UsingUUID) \(英文\)

- [Red Hat：永續性命名](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html) \(英文\)

- [Linux：UUID 可為您做些什麼](https://www.linux.com/news/what-uuids-can-do-you) \(英文\)

- [Udev： 簡介 tooDevice 現代 Linux 系統中管理](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

