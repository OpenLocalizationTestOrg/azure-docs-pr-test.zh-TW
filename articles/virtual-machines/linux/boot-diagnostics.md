---
title: "Azure 中 Linux 虛擬機器的開機診斷 | Microsoft Docs"
description: "Azure 中 Linux 虛擬機器的兩個偵錯功能概觀"
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
ms.openlocfilehash: 70254d39b5c6326166f7e29fdfc99533835502f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-boot-diagnostics-to-troubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="53544-103">如何使用開機診斷為 Azure 中的 Linux 虛擬機器進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="53544-103">How to use boot diagnostics to troubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="53544-104">Azure 現在提供兩個偵錯功能的支援︰Azure 虛擬機器 Resource Manager 部署模型的主控台輸出和螢幕擷取畫面支援。</span><span class="sxs-lookup"><span data-stu-id="53544-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="53544-105">將自己的映像送至 Azure 或甚至啟動其中一個平台映像時，虛擬機器進入不可開機狀態的原因有很多。</span><span class="sxs-lookup"><span data-stu-id="53544-105">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="53544-106">這些功能可讓您輕鬆地診斷及復原開機失敗的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="53544-106">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="53544-107">若為 Linux 虛擬機器，您可以從入口網站輕鬆地檢視主控台記錄的輸出︰</span><span class="sxs-lookup"><span data-stu-id="53544-107">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Azure 入口網站](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="53544-109">不過，若為 Windows 和 Linux 虛擬機器，Azure 也可讓您從 Hypervisor 查看 VM 的螢幕擷取畫面︰</span><span class="sxs-lookup"><span data-stu-id="53544-109">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![錯誤](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="53544-111">所有區域中的 Azure 虛擬機器都支援這兩項功能。</span><span class="sxs-lookup"><span data-stu-id="53544-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="53544-112">請注意，螢幕擷取畫面和輸出最多可能需要 10 分鐘的時間才會出現在您的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="53544-112">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="53544-113">常見的開機錯誤</span><span class="sxs-lookup"><span data-stu-id="53544-113">Common boot errors</span></span>

- [<span data-ttu-id="53544-114">檔案系統問題</span><span class="sxs-lookup"><span data-stu-id="53544-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="53544-115">核心問題</span><span class="sxs-lookup"><span data-stu-id="53544-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="53544-116">FSTAB 錯誤</span><span class="sxs-lookup"><span data-stu-id="53544-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="53544-117">在新的虛擬機器上啟用診斷</span><span class="sxs-lookup"><span data-stu-id="53544-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="53544-118">從預覽入口網站建立新的虛擬機器時，從部署模型下拉式清單中選取 [Azure Resource Manager]︰</span><span class="sxs-lookup"><span data-stu-id="53544-118">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![資源管理員](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="53544-120">設定 [監視] 選項來選取您想要放置這些診斷檔案的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="53544-120">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![建立 VM](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="53544-122">如果您正從 Azure Resource Manager 範本進行部署，請瀏覽至您的虛擬機器的資源並附加診斷設定檔區段。</span><span class="sxs-lookup"><span data-stu-id="53544-122">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="53544-123">請記得使用 “2015-06-15” API 版本標頭。</span><span class="sxs-lookup"><span data-stu-id="53544-123">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="53544-124">診斷設定檔可讓您選取想要放置這些記錄的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="53544-124">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

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

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="53544-125">更新現有的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="53544-125">Update an existing virtual machine</span></span>

<span data-ttu-id="53544-126">若要透過入口網站啟用開機診斷，您也可以透過入口網站更新現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="53544-126">To enable boot diagnostics through the portal, you can also update an existing virtual machine through the portal.</span></span> <span data-ttu-id="53544-127">選取 [開機診斷] 選項和 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="53544-127">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="53544-128">重新啟動 VM 才會生效。</span><span class="sxs-lookup"><span data-stu-id="53544-128">Restart the VM to take effect.</span></span>

![更新現有的 VM](./media/boot-diagnostics/screenshot5.png)