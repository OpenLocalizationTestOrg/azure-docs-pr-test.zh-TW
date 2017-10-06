---
title: "Microsoft Azure SUSE Linux Vm 上的 SAP NetWeaver aaaTesting |Microsoft 文件"
description: "在 Microsoft Azure SUSE Linux VM 上測試 SAP NetWeaver"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 645e358b-3ca1-4d3d-bf70-b0f287498d7a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: hermannd
ms.openlocfilehash: 0e3faab05417a1a15541e2b79aa7eddacda44611
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a>在 Microsoft Azure SUSE Linux VM 上執行 SAP NetWeaver
如果您在 Microsoft Azure SUSE Linux 虛擬機器 (Vm) 上執行的 SAP NetWeaver，本文將說明各種項目 tooconsider。 自 2016 年 5 月 19 日起，在 Azure 的 SUSE Linux VM 上已正式支援 SAP NetWeaver。 如需有關 Linux 版本、SAP 核心版本等等的所有詳細資料，請參閱 SAP 附註 1928533＜Azure 上的 SAP 應用程式︰支援的產品和 Azure VM 類型＞。
如需 Linux VM 上 SAP 的進一步相關文件，請參閱︰[在 Linux 虛擬機器 (VM) 上使用 SAP](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

hello 下列資訊應可協助您避免某些可能出現的錯誤。

## <a name="suse-images-on-azure-for-running-sap"></a>Azure 上用來執行 SAP 的 SUSE 映像
若要在 Azure 上執行 SAP NetWeaver，請只使用 SUSE Linux Enterprise Server SLES 12 (SPx) - 另請參閱 SAP 附註 1928533。 特殊的 SUSE 映像處於 hello Azure Marketplace (「 SLES 11 SP3 的 SAP CAL")，但這並不適用於一般使用方式。 請勿使用此映像，因為它保留供 hello [SAP 雲端應用裝置程式庫](https://cal.sap.com/)方案。  

針對 Azure 上的所有新測試和安裝，您應該使用 Azure Resource Manager。 toolook SUSE SLES 映像及使用 Azure PowerShell 或 hello Azure 命令列介面 (CLI)，下列命令使用 hello 的版本。 然後，您可以使用 hello 輸出，例如 toodefine hello 中作業系統映像部署新的 SUSE Linux VM 的 JSON 範本。
下列 PowerShell 命令適用於 Azure Powershell 版本 1.0.1 或更新版本。

建議您使用時仍有可能 toouse hello 標準 SLES 映像為 SAP 安裝 toomake 使用 hello 新 SLES，也就是可用的 SAP 映像現在 hello Azure 上影像的影像圖庫。 可以找到這些映像的詳細資訊，在 hello 對應[Azure Marketplace 頁面]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP )或 hello [SUSE 常見問題集相關網頁適用於 SAP 的 SLES]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ )。


* 尋找現有的發佈者，包括 SUSE：
  
   ```
   PS  : Get-AzureRmVMImagePublisher -Location "West Europe"  | where-object { $_.publishername -like "*US*"  }
   CLI : azure vm image list-publishers westeurope | grep "US"
   ```
* 從 SUSE 尋找現有的供應項目：
  
   ```
   PS  : Get-AzureRmVMImageOffer -Location "West Europe" -Publisher "SUSE"
   CLI : azure vm image list-offers westeurope SUSE
   ```
* 尋找 SUSE SLES 供應項目：
  
   ```
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES"
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP"
   CLI : azure vm image list-skus westeurope SUSE SLES
   CLI : azure vm image list-skus westeurope SUSE SLES-SAP
   ```
* 尋找 SLES SKU 的特定版本：
  
   ```
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES" -skus "12-SP2"
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP" -skus "12-SP2"
   CLI : azure vm image list westeurope SUSE SLES 12-SP2
   CLI : azure vm image list westeurope SUSE SLES-SAP 12-SP2
   ```

## <a name="installing-walinuxagent-in-a-suse-vm"></a>在 SUSE VM 中安裝 WALinuxAgent
呼叫 WALinuxAgent hello 代理程式是在 hello Azure Marketplace 中的 hello SLES 映像的一部分。 如需手動安裝 (例如從內部部署上傳 SLES OS 虛擬磁碟 (VHD)) 的相關資訊，請參閱：

* [OpenSUSE](http://software.opensuse.org/package/WALinuxAgent)
* [Azure](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SUSE](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a>SAP「增強型監視」
SAP 「 增強監視 」 是必要的先決條件 toorun SAP on Azure。 請查看 SAP 附註 2191498＜Linux 搭配 Azure 上的 SAP：增強型監視＞中的詳細資料。

## <a name="attaching-azure-data-disks-tooan-azure-linux-vm"></a>附加的 Azure 資料磁碟 tooan Azure Linux VM
使用 hello 裝置識別碼，您應該永遠不會掛接 Azure 資料磁碟 tooan Azure Linux VM 請改用 hello 通用唯一識別碼 (UUID)。 當您使用圖形化工具 toomount Azure 資料磁碟，例如，請格外小心。 請仔細檢查 hello /etc/fstab 中的項目。

hello 裝置識別碼 hello 問題是，它可能會變更，然後 hello Azure VM 可能會停止回應 hello 開機程序。 toomitigate hello 問題，您可以在 /etc/fstab 中新增 hello nofail 參數。 但是，請謹慎使用 nofail，因此應用程式可能會使用 hello 掛接點，做為前，以防外部的 Azure 資料磁碟未掛接 hello 開機期間，可能會寫入 hello 根檔案系統。

hello 唯一的例外狀況 toomounting 透過 UUID 附加為疑難排解 hello 之後 > 一節中所述的用途，作業系統磁碟。

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a>針對無法再存取的 SUSE VM 進行疑難排解
可能會有其中 SUSE VM 在 Azure 上停止回應 hello 開機程序 （例如，具有與掛接的磁碟相關的錯誤） 的情況。 您可以使用 Azure 虛擬機器 v2 hello Azure 入口網站中的 hello 開機診斷功能來確認此問題。 如需詳細資訊，請參閱 [開機診斷](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/)。

其中一種方式 toosolve hello 問題是從 hello tooattach hello OS 磁碟損毀 VM tooanother SUSE VM 在 Azure 上。 Hello 下一節中所述，然後進行適當的變更，例如編輯 /etc/fstab 或移除網路 udev 規則。

還有一個很重要的事 tooconsider。 部署數個 SUSE Vm 從相同的 Azure Marketplace 映像 (例如，SLES 11 SP4) 會導致的 hello hello OS 磁碟 tooalways hello 由裝載 UUID 相同。 因此，使用 hello UUID tooattach 從不同的 VM 部署使用相同的 Azure Marketplace 映像會導致兩個相同的 Uuid hello 作業系統磁碟。 這會造成問題，可能表示 hello 適用於疑難排解的 VM 實際上會從附加的 hello 開機，及損毀的作業系統磁碟，而不是 hello 原始。

有兩種方式 tooavoid 這樣：

* 使用不同的 Azure Marketplace 映像的 hello 疑難排解 VM (例如，SLES 11 SPx 而不是 SLES 12)。
* 從另一個 VM 不附加的損毀的 hello OS 磁碟使用 UUID-使用其他項目。

## <a name="uploading-a-suse-vm-from-on-premises-tooazure"></a>上傳 SUSE VM 從內部部署 tooAzure
如需 hello 步驟 tooupload SUSE VM 從內部部署 tooAzure 的說明，請參閱[SLES 或 openSUSE 虛擬機器做好 Azure](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

如果您想的 tooupload hello 端 （例如，tookeep 現有 SAP 安裝，以及 hello 主機名稱） 步驟沒有 hello 解除佈建 VM，請檢查下列項目 hello:

* 請確定該 hello OS 磁碟掛接使用 UUID 和不 hello 裝置識別碼。 變更只是在 /etc/fstab tooUUID 是不夠的 hello 作業系統磁碟。 此外，別忘了 tooadapt hello 開機載入器透過 YaST 或藉由編輯 /boot/grub/menu.lst。
* 如果您使用 hello VHDX 格式的 hello SUSE 作業系統磁碟，並將它轉換為上傳 tooAzure tooVHD，很可能是該 hello 網路裝置，將變更 eth0 tooeth1。 中所述，tooavoid 問題時要在 Azure 上啟動更新版本中，變更後 tooeth0[修正 eth0 中的複製 SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/)。

Toowhat 的此外 hello 文章所述，我們建議您移除這個：

   /lib/udev/rules.d/75-persistent-net-generator.rules

您也可以安裝 hello Azure Linux 代理程式 (waagent) toohelp 您避免潛在的問題，只要不是多個 Nic。

## <a name="deploying-a-suse-vm-on-azure"></a>在 Azure 上部署 SUSE VM
您應該使用 hello 新的 Azure Resource Manager 模型中的 JSON 範本檔案來建立新的 SUSE Vm。 Hello JSON 範本檔案建立之後，您可以使用下列替代 tooPowerShell 為 CLI 命令的 hello 部署 hello VM:

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
如需有關 JSON 範本檔案的更多詳細資料，請參閱[編寫 Azure Resource Manager 範本](../../../resource-group-authoring-templates.md)和 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。

如需 CLI 和 Azure 資源管理員的詳細資訊，請參閱[使用 hello for Mac、 Linux 及 Windows Azure 資源管理員使用 Azure CLI](../../../xplat-cli-azure-resource-manager.md)。

## <a name="sap-license-and-hardware-key"></a>SAP 授權與硬體金鑰
官方 SAP Azure 認證 hello，新的機制已導入了的 toocalculate hello SAP 硬體金鑰用於 hello SAP 授權。 hello SAP 核心必須調整 toobe toomake 的用法。 Linux 先前的 SAP 核心版本不包括此程式碼變更。 因此，在某些情況下 (例如，Azure VM 調整大小)、 變更 hello SAP 硬體金鑰與 hello SAP 授權已不再有效。 在最新 SAP Linux 核心 hello 可解決此問題。 如需詳細資料，請查看 SAP 附註 1928533。

## <a name="suse-sapconf-package--tuned-adm"></a>SUSE sapconf 封裝 / tuned-adm
SUSE 提供稱為 "sapconf" 的封裝，這組封裝負責管理一組 SAP 特定設定。 如詳細什麼此封裝，以及如何 tooinstall 並使用它，請參閱[使用 sapconf tooprepare SUSE Linux Enterprise Server toorun SAP 系統](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/)和[何謂 sapconf 或如何 tooprepare SUSE Linux Enterprise用於執行 SAP 系統的伺服器嗎？](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).

在 hello 同時有這項新工具取代 sapconf-微調.adm 其中一個可以找到下列 hello 下方的兩個連結此工具的更多詳細。

您可以在 [這裡](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html) 

您可以在第 6.2 章中的 [這裡](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) ，找到如何利用 tuned-adm 針對 SAP 工作負載微調系統

## <a name="nfs-share-in-distributed-sap-installations"></a>分散式 SAP 安裝中的 NFS 共用
如果您擁有分散式的安裝中-例如，您想要 tooinstall hello 資料庫並 hello SAP 應用程式伺服器在不同的 Vm--您可以共用 hello /sapmnt 目錄透過網路檔案系統 (NFS)。 如果您建立 NFS 共用的 /sapmnt hello 之後，您就會發生問題 hello 安裝步驟，請檢查 toosee 如果"no_root_squash"hello 共用設定。

## <a name="logical-volumes"></a>邏輯磁碟區
在過去的 hello 視其中一個大型的邏輯磁碟區跨多個 Azure 資料磁碟 （例如，適用於 hello SAP 資料庫），被建議 toouse mdadm lvm 未完全在 Azure 上尚未驗證。 如何使用 mdadm，在 Azure 上的 Linux RAID 向上 tooset 參閱的 toolearn[設定軟體 RAID on Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 在同時從 2016 年的開頭開始 hello 也 lvm 完全支援在 Azure 上，可用來當做替代 toomdadm。 如需有關 Azure 上 lvm 的其他資訊，請參閱[在 Azure 中的 Linux VM 上設定 LVM](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="azure-suse-repository"></a>Azure SUSE 儲存機制
如果您有存取 toohello 標準 Azure SUSE 儲存機制的問題，您可以使用簡單的命令 tooreset 它。 如果您的 Azure 區域，然後複製 hello 映像 tooa 不同區域想 toodeploy 建立私用的作業系統映像，可能會發生這個狀況根據此私用的作業系統映像的新 Vm。 只要執行下列命令 hello VM 內的 hello:

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a>Gnome 桌面
如果您想 toouse hello Gnome 桌面 tooinstall 完整的 SAP 示範系統包括 SAP GUI，在單一 VM-內部瀏覽器，然後 SAP 管理主控台--使用此提示 tooinstall 它 hello Azure SLES 影像：

   SLES 11：

   ```
   zypper in -t pattern gnome
   ```

   SLES 12：

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-hello-cloud"></a>Oracle Linux hello 雲端上的 SAP 支援
在虛擬環境中，Oracle 對 Linux 的支援有所限制。 雖然這不是 Azure 特定主題，是重要的 toounderstand。 SAP 不支援 SUSE 上的 Oracle 或類似 Azure 之公用雲端中的 Red Hat。 toodiscuss 本主題中，請直接連絡 Oracle。

