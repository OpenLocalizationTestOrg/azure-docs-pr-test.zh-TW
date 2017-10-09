---
title: "在 Azure 中 Linux 虛擬機器的 aaaBoot 診斷 |Microsoft 文件"
description: "Hello 兩個偵錯的功能在 Azure 中 Linux 虛擬機器概觀"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="c521c-103">Toouse 開機診斷 tootroubleshoot Linux 虛擬機器在 Azure 中的方式</span><span class="sxs-lookup"><span data-stu-id="c521c-103">How toouse boot diagnostics tootroubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="c521c-104">Azure 現在提供兩個偵錯功能的支援︰Azure 虛擬機器 Resource Manager 部署模型的主控台輸出和螢幕擷取畫面支援。</span><span class="sxs-lookup"><span data-stu-id="c521c-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="c521c-105">時攜帶您自己的映像 tooAzure 或甚至開機的 hello 平台映像，可能會因許多原因而虛擬機器進入非可開機的狀態。</span><span class="sxs-lookup"><span data-stu-id="c521c-105">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="c521c-106">這些功能可讓您 tooeasily 診斷和復原虛擬機器的開機失敗。</span><span class="sxs-lookup"><span data-stu-id="c521c-106">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="c521c-107">適用於 Linux 虛擬機器中，您可以輕鬆地檢視 hello 輸出的主控台記錄檔，從 hello 入口網站：</span><span class="sxs-lookup"><span data-stu-id="c521c-107">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure 入口網站](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="c521c-109">不過，針對 Windows 和 Linux 虛擬機器，Azure 也可讓您 toosee hello VM 從 hello hypervisor 的螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="c521c-109">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![錯誤](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="c521c-111">所有區域中的 Azure 虛擬機器都支援這兩項功能。</span><span class="sxs-lookup"><span data-stu-id="c521c-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="c521c-112">請注意，螢幕擷取畫面，輸出可能會佔用 too10 分鐘 tooappear 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="c521c-112">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="c521c-113">常見的開機錯誤</span><span class="sxs-lookup"><span data-stu-id="c521c-113">Common boot errors</span></span>

- [<span data-ttu-id="c521c-114">檔案系統問題</span><span class="sxs-lookup"><span data-stu-id="c521c-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="c521c-115">核心問題</span><span class="sxs-lookup"><span data-stu-id="c521c-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="c521c-116">FSTAB 錯誤</span><span class="sxs-lookup"><span data-stu-id="c521c-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="c521c-117">在新的虛擬機器上啟用診斷</span><span class="sxs-lookup"><span data-stu-id="c521c-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="c521c-118">當從 hello 預覽入口網站中建立新的虛擬機器，選取 hello **Azure Resource Manager**從 hello 部署模型 下拉式清單：</span><span class="sxs-lookup"><span data-stu-id="c521c-118">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="c521c-120">這些診斷檔案設定 hello 監視選項 tooselect hello 儲存體帳戶 tooplace 的位置。</span><span class="sxs-lookup"><span data-stu-id="c521c-120">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![建立 VM](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="c521c-122">如果您要部署的 Azure 資源管理員範本，請瀏覽 tooyour 虛擬機器的資源，並附加 hello 診斷設定檔區段。</span><span class="sxs-lookup"><span data-stu-id="c521c-122">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="c521c-123">請記住 toouse hello"2015年-06-15"應用程式開發介面版本標頭。</span><span class="sxs-lookup"><span data-stu-id="c521c-123">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="c521c-124">hello 診斷設定檔可讓您 tooselect hello 儲存體帳戶，而您希望 tooput 這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c521c-124">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="c521c-125">更新現有的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c521c-125">Update an existing virtual machine</span></span>

<span data-ttu-id="c521c-126">tooenable 開機診斷，透過 hello 入口網站，您也可以更新現有的虛擬機器透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c521c-126">tooenable boot diagnostics through hello portal, you can also update an existing virtual machine through hello portal.</span></span> <span data-ttu-id="c521c-127">選取 hello 開機診斷選項，並儲存。</span><span class="sxs-lookup"><span data-stu-id="c521c-127">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="c521c-128">重新啟動 hello VM tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="c521c-128">Restart hello VM tootake effect.</span></span>

![更新現有的 VM](./media/boot-diagnostics/screenshot5.png)