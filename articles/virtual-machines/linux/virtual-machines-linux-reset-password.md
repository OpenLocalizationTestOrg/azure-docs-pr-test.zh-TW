---
title: "aaaHow tooreset 本機 Linux 密碼 Azure Vm 上的 |Microsoft 文件"
description: "導入 hello 步驟 tooreset hello 本機 Linux 密碼在 Azure VM"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: 3827e32186c5f034d9bb6fc502dc26708b52a00a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a>如何在 Azure Vm 上的 tooreset 本機 Linux 密碼

本文介紹幾個方法 tooreset 本機 Linux 虛擬機器 (VM) 的密碼。 如果 hello 使用者帳戶已過期，或只是想 toocreate 新帳戶，您可以使用下列方法 toocreate 新的本機系統管理員帳戶的 hello，並重新取得存取 toohello VM。

## <a name="symptoms"></a>徵兆

您無法登入 toohello VM，並接收一個訊息，指出您使用該 hello 密碼不正確。 此外，您無法使用 VMAgent tooreset 密碼 hello Azure 入口網站上。 

## <a name="manual-password-reset-procedure"></a>手動密碼重設程序

1.  刪除 hello VM，並保留 hello 附加磁碟。

2.  附加 hello 做為資料磁碟 tooanother 作業系統磁碟機中 hello 時態 VM 相同的位置。

3.  執行下列 hello 時態 VM toobecome 上的 SSH 命令的 hello 超級使用者。


    ~~~~
    sudo su
    ~~~~

4.  執行**fdisk l**或系統記錄檔 toofind hello 查看新連接的磁碟。 找出 hello 磁碟機名稱 toomount。 然後在 hello 時態 VM，查詢中 hello 相關記錄檔。

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    hello 以下是範例輸出 hello grep 命令：

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  建立名為 **tempmount** 的掛接點。

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Hello OS 磁碟掛接 hello 掛接點上。 您通常需要 toomount sdc1 或 sdc2。 這將取決於 hello 裝載從 hello 中斷的電腦磁碟的 /etc 目錄中的資料分割。

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  執行備份，然後再進行任何變更：

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  您需要重設 hello 使用者的密碼：

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  移動 hello 修改 hello 中斷電腦的磁碟上檔案 toohello 正確位置。

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    cd / umount /tempmount
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
