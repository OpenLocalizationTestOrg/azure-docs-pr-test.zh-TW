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
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a><span data-ttu-id="f34f2-103">如何在 Azure Vm 上的 tooreset 本機 Linux 密碼</span><span class="sxs-lookup"><span data-stu-id="f34f2-103">How tooreset local Linux password on Azure VMs</span></span>

<span data-ttu-id="f34f2-104">本文介紹幾個方法 tooreset 本機 Linux 虛擬機器 (VM) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="f34f2-104">This article introduces several methods tooreset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="f34f2-105">如果 hello 使用者帳戶已過期，或只是想 toocreate 新帳戶，您可以使用下列方法 toocreate 新的本機系統管理員帳戶的 hello，並重新取得存取 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="f34f2-105">If hello user account is expired or you just want toocreate a new account, you can use hello following methods toocreate a new local admin account and re-gain access toohello VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="f34f2-106">徵兆</span><span class="sxs-lookup"><span data-stu-id="f34f2-106">Symptoms</span></span>

<span data-ttu-id="f34f2-107">您無法登入 toohello VM，並接收一個訊息，指出您使用該 hello 密碼不正確。</span><span class="sxs-lookup"><span data-stu-id="f34f2-107">You can't log in toohello VM, and you receive a message that indicates that hello password that you used is incorrect.</span></span> <span data-ttu-id="f34f2-108">此外，您無法使用 VMAgent tooreset 密碼 hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="f34f2-108">Additionally, you can't use VMAgent tooreset your password on hello Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="f34f2-109">手動密碼重設程序</span><span class="sxs-lookup"><span data-stu-id="f34f2-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="f34f2-110">刪除 hello VM，並保留 hello 附加磁碟。</span><span class="sxs-lookup"><span data-stu-id="f34f2-110">Delete hello VM and keep hello attached disks.</span></span>

2.  <span data-ttu-id="f34f2-111">附加 hello 做為資料磁碟 tooanother 作業系統磁碟機中 hello 時態 VM 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="f34f2-111">Attach hello OS Drive as a data disk tooanother temporal VM in hello same location.</span></span>

3.  <span data-ttu-id="f34f2-112">執行下列 hello 時態 VM toobecome 上的 SSH 命令的 hello 超級使用者。</span><span class="sxs-lookup"><span data-stu-id="f34f2-112">Run hello following SSH command on hello temporal VM toobecome a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="f34f2-113">執行**fdisk l**或系統記錄檔 toofind hello 查看新連接的磁碟。</span><span class="sxs-lookup"><span data-stu-id="f34f2-113">Run **fdisk -l** or look at system logs toofind hello newly attached disk.</span></span> <span data-ttu-id="f34f2-114">找出 hello 磁碟機名稱 toomount。</span><span class="sxs-lookup"><span data-stu-id="f34f2-114">Locate hello drive name toomount.</span></span> <span data-ttu-id="f34f2-115">然後在 hello 時態 VM，查詢中 hello 相關記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f34f2-115">Then on hello temporal VM, look in hello relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="f34f2-116">hello 以下是範例輸出 hello grep 命令：</span><span class="sxs-lookup"><span data-stu-id="f34f2-116">hello following is example output of hello grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="f34f2-117">建立名為 **tempmount** 的掛接點。</span><span class="sxs-lookup"><span data-stu-id="f34f2-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="f34f2-118">Hello OS 磁碟掛接 hello 掛接點上。</span><span class="sxs-lookup"><span data-stu-id="f34f2-118">Mount hello OS disk on hello mount point.</span></span> <span data-ttu-id="f34f2-119">您通常需要 toomount sdc1 或 sdc2。</span><span class="sxs-lookup"><span data-stu-id="f34f2-119">You usually need toomount sdc1 or sdc2.</span></span> <span data-ttu-id="f34f2-120">這將取決於 hello 裝載從 hello 中斷的電腦磁碟的 /etc 目錄中的資料分割。</span><span class="sxs-lookup"><span data-stu-id="f34f2-120">This will depend on hello hosting partition in /etc directory from hello broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="f34f2-121">執行備份，然後再進行任何變更：</span><span class="sxs-lookup"><span data-stu-id="f34f2-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="f34f2-122">您需要重設 hello 使用者的密碼：</span><span class="sxs-lookup"><span data-stu-id="f34f2-122">Reset hello user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="f34f2-123">移動 hello 修改 hello 中斷電腦的磁碟上檔案 toohello 正確位置。</span><span class="sxs-lookup"><span data-stu-id="f34f2-123">Move hello modified files toohello correct location on hello broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    <span data-ttu-id="f34f2-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="f34f2-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
