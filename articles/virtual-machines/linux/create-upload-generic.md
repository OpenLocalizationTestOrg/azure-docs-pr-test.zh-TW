---
title: "aaaCreate 和上傳 Linux VHD 在 Azure 中"
description: "了解 toocreate 和上傳 Azure 虛擬硬碟 (VHD)，其中包含 Linux 作業系統。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 208e15c035edb5520fc29ba8e4e71c42b041864d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="information-for-non-endorsed-distributions"></a>非背書散發套件的資訊
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

hello Azure 平台 SLA 適用於執行 Linux 作業系統，僅當一 hello toovirtual 機器的 hello[背書分佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)用。 在 hello Azure 映像庫所提供的所有 Linux 散發都背書分佈利用 hello 必要的設定。

* [Azure 背書散發套件上的 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [支援 Microsoft Azure 中的 Linux 映像](https://support.microsoft.com/kb/2941892)

在 Azure 上執行的所有分佈都需要 toomeet 必要條件 toohave hello 平台上執行的機率 tooproperly 數。  本文並不是完整因為每個分佈是不同;然而，很可能即使您符合所有 hello 下列條件仍然需要 toosignificantly 調整您 Linux 系統 tooensure hello 平台上正常執行。

基於這個原因，我們建議您盡可能從其中一個 [Azure 背書散發套件上的 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 開始著手。 hello 下列文件將引導您完成 tooprepare 如何 hello 各種背書在 Azure 受支援的 Linux 散發套件：

* **[CentOS 型散發套件](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES 和 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

hello 本文其餘部分將著重在 Azure 上執行您的 Linux 散發套件的一般指引。

## <a name="general-linux-installation-notes"></a>一般 Linux 安裝注意事項
* hello VHDX 格式不支援在 Azure 中，只有**固定 VHD**。  您可以將使用 HYPER-V 管理員 hello 磁碟 tooVHD 格式轉換或 hello convert-vhd 指令程式。 如果您使用 VirtualBox 這表示選取**固定大小**為相對於 toohello 預設建立 hello 磁碟時，動態配置。
* Azure 僅支援第 1 代虛擬機器。 您可以將某個層代 1 個虛擬機器從 VHDX toohello VHD 檔案格式及動態擴充 tooa 固定大小磁碟的轉換。 但您無法變更虛擬機器的世代。 如需詳細資訊，請參閱[應該在 Hyper-V 中建立第 1 代還是第 2 代的虛擬機器？](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)
* hello 最大允許 hello VHD 為 1023 GB。
* 安裝 hello Linux 系統時*建議*您使用標準的資料分割，而非 LVM （通常 hello 預設值為許多安裝）。 這樣可避免與複製 Vm，LVM 名稱衝突，特別是當作業系統磁碟需要附加 toobe tooanother 相同的 VM 進行疑難排解。 如果願意，您可以在資料磁碟上使用 [LVM](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或 [RAID](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 需要掛接 UDF 檔案系統的核心支援。 在第一次開機 Azure hello 上佈建組態會透過附加的 toohello 客體的 UDF 格式化媒體傳遞 toohello Linux VM。 hello Azure Linux 代理程式必須要能夠 toomount hello UDF 檔案系統 tooread 其組態，並佈建 hello VM。
* Linux Kernel 2.6.37 以下的版本不支援較大 VM 大小 Hyper-V 上的NUMA。 這個問題主要會影響較舊的分佈上游使用 hello Red Hat 2.6.32 核心及已修正 RHEL 6.6 (核心-2.6.32-504) 中。 執行自訂的核心超過 2.6.37 或較舊 RHEL 基礎核心非 2.6.32-504 必須設定系統 hello 開機參數`numa=off`hello 核心 grub.conf 在命令列上。 如需詳細資訊，請參閱 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)。
* 請勿設定 hello OS 磁碟交換資料分割。 hello Linux 代理程式可以設定的 toocreate 交換磁碟上的檔案 hello 暫存資源。  相關資訊位於下列 hello 步驟。
* 所有 hello Vhd 必須是 1 MB 的倍數的大小。

### <a name="installing-kernel-modules-without-hyper-v"></a>安裝不含 Hyper-V 的核心模組
因此 Linux 需要特定的核心模組會安裝在 Azure 中的順序 toorun 時，azure 會 hello HYPER-V hypervisor 上執行。 如果您有建立於 HYPER-V 之外的 VM，hello Linux 的安裝程式不能包含 hello 驅動程式的 HYPER-V 中 （initrd 或 initramfs） hello 初始 ramdisk 除非其偵測它正在執行的 HYPER-V 環境。 當使用不同虛擬化 （亦即 Virtualbox、 KVM 等） 的系統 tooprepare Linux 映像，您可能需要至少 hello toorebuild hello initrd tooensure`hv_vmbus`和`hv_storvsc`hello 初始 ramdisk 核心模組可用。  這在至少 hello 上游 Red Hat 發佈為基礎的系統上是已知的問題。

重建 hello initrd 或 initramfs 映像的 hello 機制可能有所不同 hello 發佈。 請參閱您的發佈文件，或支援 hello 適當的程序。  以下是一個範例的方式 toorebuild hello initrd 使用 hello`mkinitrd`公用程式：

首先，請備份 hello 現有 initrd 映像：

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

接下來，重建以 hello hello initrd`hv_vmbus`和`hv_storvsc`核心模組：

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a>調整 VHD 的大小
在 Azure 上的 VHD 映像必須對齊的虛擬大小 too1MB。  一般而言，使用 Hyper-V 建立的 VHD 應已正確對應。  如果可能會收到錯誤訊息類似 toohello 遵循當您嘗試 toocreate 未正確對齊 hello VHD*映像*從您的 VHD:

    "hello VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. hello size must be a whole number (in MBs).”

tooremedy 這可以調整大小 hello VM 使用 hello HYPER-V 管理員主控台或 hello [RESIZE-VHD](http://technet.microsoft.com/library/hh848535.aspx) Powershell cmdlet。  如果您不在 Windows 環境中執行它，建議您使用 toouse qemu img tooconvert （如有需要），並調整 hello VHD 的大小。

> [!NOTE]
> qemu-img >=2.2.1 的版本中已知有 Bug 會導致 VHD 的格式不正確。 hello 問題已修正在 QEMU 2.6。 建議 toouse qemu img 2.2.0 或較低或更新 too2.6 或更高版本。 參考︰https://bugs.launchpad.net/qemu/+bug/1490611。
> 
> 

1. 調整大小 hello 直接使用工具，例如 VHD`qemu-img`或`vbox-manage`可能會導致無法開機的 VHD。  因此，建議您使用 toofirst convert hello VHD tooa 原始磁碟映像。  如果已經建立 hello VM 映像做為原始磁碟映像 （例如 KVM 有些 Hypervisor 的 hello 預設值），您可能會略過此步驟：
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. 計算 hello 所需的 hello 虛擬大小的 hello 磁碟映像 tooensure 大小是對齊的 too1MB。  這可以協助 hello 遵循 bash 殼層指令碼。  hello 指令碼會使用 「`qemu-img info`"toodetermine hello hello 磁碟映像的虛擬大小，然後計算 hello 大小 toohello 下一步 1MB:
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. 調整在 hello 上述指令碼中使用 rounded_size hello 原始磁碟的大小：
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. 現在，將轉換 hello 原始磁碟回復 tooa 固定大小的 VHD:
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   或 qemu 版本**2.6 +**包含 hello`force_size`選項：

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a>Linux Kernel 需求
hello HYPER-V 和 Azure 的 Linux Integration Services (LIS) 驅動程式提供直接 toohello 上游 Linux 核心。 許多包括最新 Linux kernel 版本 (例如 3.x) 的散發套件已經有這些驅動程式，或提供這些驅動程式及其核心的 Backport 版本。  這些驅動程式會經常更新 hello 上游核心與新的修正程式和功能，因此建議盡可能 toorun[背書發佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，將包含這些修正程式和更新。

如果您執行 Red Hat Enterprise Linux 版本的 variant **6.0-6.3**，則您必須針對 HYPER-V tooinstall hello 最新 LIS 驅動程式。 您可以找到 hello 驅動程式[此位置](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409)。 為準，RHEL **6.4 +** （與衍生項目） hello LIS 驅動程式已隨附 hello 核心，所以沒有額外的安裝封裝會需要的 toorun 這些系統在 Azure 上的。

如果需要自訂的核心，則建議 toouse 較新的核心版本 (也就是**3.8 +**)。 對於這些散發或廠商維護自己的核心，某些投入時間會需要的 tooregularly backport hello LIS 驅動程式從 hello 上游核心 tooyour 自訂的核心。  即使您已經執行較新的核心版本，強烈建議 tookeep 追蹤任何上游的修正 hello LIS 驅動程式和 backport 那些視。 hello hello LIS 驅動程式來源檔案的位置位於 hello[維護程式](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS)hello Linux 核心來源樹狀目錄中的檔案：

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

在非常小，hello 缺乏 hello 遵循修補程式已知 toocause 在 Azure 上的問題，因此這些必須包含在 hello 核心。 這絕對不是詳盡或完整的所有散發套件清單：

* [ata_piix： 預設延遲磁碟 toohello HYPER-V 驅動程式](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [storvsc： 中傳輸封包 hello 重設路徑中的帳戶](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [storvsc：避免使用 WRITE_SAME](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [storvsc：針對 RAID 和虛擬主機介面卡驅動程式停用 WRITE SAME](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [storvsc：NULL 指標取值修正](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [storvsc：信號緩衝區失敗可能導致 I/O 凍結](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [scsi_sysfs︰防範 __scsi_remove_device 雙重執行](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="hello-azure-linux-agent"></a>hello Azure Linux 代理程式
hello [Azure Linux 代理程式](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(waagent) 無須 tooproperly 佈建在 Azure 中 Linux 虛擬機器。 您可以取得 hello 最新版本、 檔案問題或提交提取要求在 hello [Linux 代理程式 GitHub 儲存機制](https://github.com/Azure/WALinuxAgent)。

* hello Linux 代理程式會釋放 hello Apache 2.0 授權。 許多發行已提供 RPM 或 deb 套件 hello 代理程式，因此在某些情況下這也可以和安裝更新工程。
* hello Azure Linux 代理程式需要 Python v2.6 +。
* hello 代理程式也需要 hello python pyasn1 模組。 大多數的散發套件會以可個別安裝的套件形式提供此項目。
* 在某些情況下可能無法相容於 NetworkManager hello Azure Linux 代理程式。 Hello RPM/Deb 套件由分佈所提供的許多設定 NetworkManager 衝突 toohello waagent 套件，並因此將解除安裝 NetworkManager 當您安裝 hello Linux 代理程式封裝。

## <a name="general-linux-system-requirements"></a>一般的 Linux 系統需求

* 修改下列參數的幼蟲或 GRUB2 tooinclude hello hello 核心開機一行。 這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援：
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    這也可確保所有的主控台訊息都會傳送 toohello 第一個序列連接埠，這可協助 Azure 偵錯問題的支援。
  
    除了上述 toohello 建議太*移除*hello 參數之後，如果它們存在：
  
        rhgb quiet crashkernel=auto
  
    沒有適用於雲端環境，我們想要傳送 toohello 序列連接埠的所有 hello 記錄 toobe 圖形和無訊息的開機。 hello`crashkernel`選項可能會是左設定如有需要，但請注意，這個參數會減少 hello hello 128 MB 以上，VM 中可用的記憶體數量可能會造成問題 hello 較小的 VM 大小。

* 安裝 hello Azure Linux 代理程式
  
    hello Azure Linux 代理程式，才能佈建在 Azure 上的 Linux 映像。  許多發行中提供作為 RPM 或 Deb 套件 hello 代理程式 （hello 封裝通常稱為 'WALinuxAgent' 或 'walinuxagent'）。  hello 代理程式也可以安裝以手動方式 hello 中的 hello 步驟[Linux 代理程式的指南](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

* 請確定該 hello SSH 伺服器是在安裝並設定 toostart 開機時間。  這通常是 hello 預設值。

* 不要在 hello OS 磁碟上建立的交換空間
  
    hello Azure Linux 代理程式可以自動設定使用之後附加的 toohello VM 在 Azure 上佈建的 hello 本機資源磁碟的交換空間。 請注意該 hello 本機資源磁碟是*暫存*磁碟，以及可能會在取消佈建 hello VM 時清空。 在安裝之後 hello Azure Linux 代理程式 （請參閱上一個步驟），修改適當地遵循 /etc/waagent.conf 中的參數的 hello:
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

* 最後一個步驟中，執行下列命令 toodeprovision hello 虛擬機器的 hello:
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > Virtualbox 上，您可能會看到下列錯誤，開始執行之後的 hello ' waagent-force-取消佈建 ': `[Errno 5] Input/output error`。 此錯誤訊息並不重要，您可以忽略。
  > 
  > 

* 您接著需要 tooshut 關閉 hello 虛擬機器，並上傳 hello VHD tooAzure。

