---
title: "在 Azure 中的 aaaIntroduction tooLinux |Microsoft 文件"
description: "了解如何使用 Azure 上的 Linux 虛擬機器"
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a>在 Azure 上的簡介 tooLinux
本主題提供在 hello Azure 雲端中使用的 Linux 虛擬機器的某些層面的概觀。 部署 Linux 虛擬機器是簡單的程序，使用從 hello 組件庫的映像。

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>驗證：使用者名稱、密碼和 SSH 金鑰
當建立 Linux 虛擬機器使用 hello Azure 入口網站，系統會要求您 tooprovide 任一使用者名稱和密碼或 SSH 公開金鑰。 hello 選擇部署在 Azure 上的 Linux 虛擬機器的使用者名稱是主體 toohello 遵循條件約束： 系統帳戶的名稱 (UID < 100) hello 中已有虛擬機器不允許，'root' 例如。

* 請參閱[建立執行 Linux 的虛擬機器](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* 請參閱[如何透過在 Azure 上的 Linux SSH tooUse](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>使用 `sudo`
hello 在 Azure 上的虛擬機器執行個體部署期間指定的使用者帳戶是特殊權限的帳戶。 此帳戶蒻謔 hello Azure Linux 代理程式 toobe 無法 tooelevate 權限 tooroot （superuser 帳戶） 使用 hello`sudo`公用程式。 登入使用此使用者帳戶之後，您將無法 toorun 命令根使用 hello 命令語法為：

    # sudo <COMMAND>

您可以選擇使用 **sudo -s**來取得 root shell。

* 請參閱[在 Azure 中的 Linux 虛擬機器上使用根權限](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="firewall-configuration"></a>防火牆設定
Azure 提供限制連線 tooports hello Azure 入口網站中指定的輸入封包篩選器。 根據預設，hello 只允許連接埠是 SSH。 可能存取 tooadditional 連接埠上開啟您的 Linux 虛擬機器在 hello Azure 入口網站中設定的端點：

* 請參閱：[如何 tooSet 端點 tooa 虛擬機器](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

在 hello Azure 組件庫中的 hello Linux 映像不會啟用 hello *iptables*預設的防火牆。 如果需要的話，可能會設定 hello 防火牆 tooprovide 額外的篩選。

## <a name="hostname-changes"></a>主機名稱變更
當您一開始會部署 Linux 映像的執行個體時，您就需要的 tooprovide hello 虛擬機器的主機名稱。 一旦 hello 虛擬機器正在執行，此主機名稱會是已發行的 toohello 平台 DNS 伺服器，讓多個連接的虛擬機器 tooeach 其他可以執行使用主機名稱的 IP 位址搜尋。

如果虛擬機器部署之後，需要主機名稱變更，請使用 hello 命令

    # sudo hostname <newname>

hello Azure Linux 代理程式包含功能 tooautomatically 偵測到此名稱的變更和適當地設定 hello 虛擬機器 toopersist 這項變更，並發佈此變更 toohello 平台 DNS 伺服器。

* [Azure Linux 代理程式使用者指南](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>Cloud-Init
**Ubuntu** 和 **CoreOS** 映像會在 Azure 上利用 Cloud-Init，這可提供用來啟動虛擬機器的額外功能。

* [如何 tooInject 自訂資料](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Microsoft Azure 上的自訂資料和 Cloud-Init](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [使用 Cloud-Init 建立 Azure Swap 磁碟分割](https://wiki.ubuntu.com/AzureSwapPartitions)
* [如何在 Azure 上 CoreOS tooUse](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>擷取虛擬機器映像
Azure 提供現有的虛擬機器的 hello 能力 toocapture hello 狀態納入接下來可以使用的 toodeploy 額外的虛擬機器執行個體的映像。 hello Azure Linux 代理程式可能使用的 toorollback 部分 hello hello 佈建程序期間執行的自訂。 您可以依照下列 toocapture 虛擬機器的 hello 步驟，做為映像：

1. 執行**waagent-取消佈建**tooundo 佈建的自訂。 或者**waagent-取消佈建 + 使用者**toooptionally 刪除 hello 佈建和所有相關聯的資料期間所指定的使用者帳戶。
2. 關閉清單/hello 虛擬機器關機。
3. 按一下**擷取**hello Azure 入口網站或使用 hello PowerShell 或 CLI 工具 toocapture hello 虛擬機器做為映像。
   
   * 請參閱：[如何 tooCapture Linux 虛擬機器 tooUse 做為範本](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>連接磁碟
每個虛擬機器都會連接一個暫時性的本機 *資源磁碟* 。 在重新啟動期間的資源磁碟上的資料可能不會持久，因為它常用的應用程式和暫時性的 hello 虛擬機器中執行的處理序和**暫存**資料的儲存體。 它也是使用的 toostore hello 分頁 hello 作業系統檔案。

在 Linux 上 hello 資源磁碟通常是由管理 hello Azure Linux 代理程式，且自動掛接太**/mnt/retention/ 資源**(或**/mnt** Ubuntu 映像上)。

> [!NOTE]
> 請注意該 hello 資源磁碟是**暫存**磁碟，並可能會刪除並重新格式化 hello VM 重新開機時。
> 
> 

在 Linux 上 hello 資料磁碟可能名為 hello 核心`/dev/sdc`，而且使用者需要 toopartition、 格式化及裝載該資源。 這會涵蓋在 hello 教學課程逐步：[如何 tooAttach 虛擬機器的資料磁碟 tooa](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

* **另請參閱︰**[Linux 上設定軟體 RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  &  [設定 Azure 中 Linux VM 的 LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

