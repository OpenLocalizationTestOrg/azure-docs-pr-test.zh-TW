---
title: "取得 Azure Linux VM 識別碼 | Microsoft Docs"
description: "說明如何取得和使用「Azure Linux VM 唯一識別碼」。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 258ce425d5692730011cf2f4468dc0ba77f4cb79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="146c7-103">存取和使用 Azure VM 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="146c7-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="146c7-104">Azure VM 的唯一識別碼是在所有 Azure IaaS VM 的 SMBIOS 中編碼並儲存的一個 128 位元識別碼，而且目前可以使用平台的 BIOS 命令讀取。</span><span class="sxs-lookup"><span data-stu-id="146c7-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="146c7-105">Azure VM 的唯一識別碼是唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="146c7-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="146c7-106">在重新開機關機 (計劃中或未計劃)、開始/停止解除配置、服務修復或就地還原之後，Azure 的唯一 VM 識別碼並不會變更。</span><span class="sxs-lookup"><span data-stu-id="146c7-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="146c7-107">不過，如果 VM 是一個快照，而且是為了建立新的執行個體而複製，就會設定新的 Azure VM 識別碼。</span><span class="sxs-lookup"><span data-stu-id="146c7-107">However, if the VM is a snapshot and copied to create a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="146c7-108">如果您自這項新功能推出 (2014 年 9 月 18 日) 之後，已經建立並執行較舊的 VM，請重新啟動您的 VM 以自動取得 Azure 的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="146c7-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM to automatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="146c7-109">從 VM 內存取 Azure 的唯一 VM 識別碼︰</span><span class="sxs-lookup"><span data-stu-id="146c7-109">To access Azure Unique VM ID from within the VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="146c7-110">建立 VM</span><span class="sxs-lookup"><span data-stu-id="146c7-110">Create a VM</span></span>
<span data-ttu-id="146c7-111">如需詳細資訊，請參閱[建立虛擬機器](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="146c7-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="146c7-112">連接至 VM</span><span class="sxs-lookup"><span data-stu-id="146c7-112">Connect to the VM</span></span>
<span data-ttu-id="146c7-113">如需詳細資訊，請參閱 [Linux 中的 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="146c7-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="146c7-114">查詢 VM 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="146c7-114">Query VM Unique ID</span></span>
<span data-ttu-id="146c7-115">命令 (範例使用 **Ubuntu**)：</span><span class="sxs-lookup"><span data-stu-id="146c7-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="146c7-116">範例預期的結果：</span><span class="sxs-lookup"><span data-stu-id="146c7-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="146c7-117">由於 Big Endian 位元順序的緣故，此案例中實際的唯一 VM 識別碼將是︰</span><span class="sxs-lookup"><span data-stu-id="146c7-117">Due to Big Endian bit ordering, the actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="146c7-118">不論 VM 是在 Azure 上還是內部部署執行，都可以在不同的案例中使用 Azure VM 的唯一識別碼，而且可以協助您在 Azure IaaS 部署中可能會有的授權、報告或一般追蹤需求。</span><span class="sxs-lookup"><span data-stu-id="146c7-118">Azure VM unique ID can be used in different scenarios whether the VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="146c7-119">建置應用程式並在 Azure 上進行驗證的許多獨立軟體廠商可能需要在整個生命週期找出 Azure VM，並辨別 VM 是在 Azure、內部部署，或其他雲端提供者上執行。</span><span class="sxs-lookup"><span data-stu-id="146c7-119">Many independent software vendors building applications and certifying them on Azure may require to identify an Azure VM throughout its lifecycle and to tell if the VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="146c7-120">例如，此平台識別碼可協助偵測軟體是否獲得正確授權，或協助將任何 VM 資料及其來源相互關聯，以協助為適當的平台設定適當的計量，並在其他用途之間追蹤和相互關聯這些度量。</span><span class="sxs-lookup"><span data-stu-id="146c7-120">This platform identifier can for example help detect if the software is properly licensed or help to correlate any VM data to its source such as to assist on setting the right metrics for the right platform and to track and correlate these metrics amongst other uses.</span></span>

