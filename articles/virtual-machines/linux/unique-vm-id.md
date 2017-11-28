---
title: "Azure Linux VM 識別碼 aaaGet |Microsoft 文件"
description: "描述如何 tooget 和使用 Azure Linux VM 唯一識別碼。"
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
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="88c2f-103">存取和使用 Azure VM 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="88c2f-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="88c2f-104">Azure VM 的唯一識別碼是在所有 Azure IaaS VM 的 SMBIOS 中編碼並儲存的一個 128 位元識別碼，而且目前可以使用平台的 BIOS 命令讀取。</span><span class="sxs-lookup"><span data-stu-id="88c2f-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="88c2f-105">Azure VM 的唯一識別碼是唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="88c2f-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="88c2f-106">在重新開機關機 (計劃中或未計劃)、開始/停止解除配置、服務修復或就地還原之後，Azure 的唯一 VM 識別碼並不會變更。</span><span class="sxs-lookup"><span data-stu-id="88c2f-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="88c2f-107">不過，如果 hello VM 是快照式和複製 toocreate 的新執行個體，就會設定新的 Azure VM 識別碼。</span><span class="sxs-lookup"><span data-stu-id="88c2f-107">However, if hello VM is a snapshot and copied toocreate a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="88c2f-108">如果您有舊版所建立的 Vm，並執行，因為這項新功能已推出 (2014 年 9 月 18 日)，請重新啟動 VM tooautomatically 取得 Azure 的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="88c2f-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM tooautomatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="88c2f-109">tooaccess 從 Azure 唯一 VM 識別碼 hello VM 內：</span><span class="sxs-lookup"><span data-stu-id="88c2f-109">tooaccess Azure Unique VM ID from within hello VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="88c2f-110">建立 VM</span><span class="sxs-lookup"><span data-stu-id="88c2f-110">Create a VM</span></span>
<span data-ttu-id="88c2f-111">如需詳細資訊，請參閱[建立虛擬機器](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="88c2f-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-toohello-vm"></a><span data-ttu-id="88c2f-112">連接 toohello VM</span><span class="sxs-lookup"><span data-stu-id="88c2f-112">Connect toohello VM</span></span>
<span data-ttu-id="88c2f-113">如需詳細資訊，請參閱 [Linux 中的 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="88c2f-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="88c2f-114">查詢 VM 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="88c2f-114">Query VM Unique ID</span></span>
<span data-ttu-id="88c2f-115">命令 (範例使用 **Ubuntu**)：</span><span class="sxs-lookup"><span data-stu-id="88c2f-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="88c2f-116">範例預期的結果：</span><span class="sxs-lookup"><span data-stu-id="88c2f-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="88c2f-117">TooBig 位元組由小到大位元順序，因為 hello 實際唯一 VM 識別碼在此情況下會是：</span><span class="sxs-lookup"><span data-stu-id="88c2f-117">Due tooBig Endian bit ordering, hello actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="88c2f-118">Azure VM 的唯一識別碼 hello VM 正執行於 Azure 或內部部署且可協助您授權、 報告或一般追蹤的需求可能對您的 Azure IaaS 部署是否可以用於不同的案例。</span><span class="sxs-lookup"><span data-stu-id="88c2f-118">Azure VM unique ID can be used in different scenarios whether hello VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="88c2f-119">許多的獨立軟體廠商建置應用程式和認證它們在 Azure 上可能需要 tooidentify 透過其生命週期和 tootell Azure VM，如果 hello VM 在 Azure 中，在內部部署或其他雲端提供者上執行。</span><span class="sxs-lookup"><span data-stu-id="88c2f-119">Many independent software vendors building applications and certifying them on Azure may require tooidentify an Azure VM throughout its lifecycle and tootell if hello VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="88c2f-120">此平台識別項例如有助於偵測 hello 軟體是否已正確授權或協助 toocorrelate 例如 tooassist 設定 hello 右 hello 右平台和度量 tootrack 任何 VM 資料 tooits 來源並將這些計量之間的相互關聯其他用途。</span><span class="sxs-lookup"><span data-stu-id="88c2f-120">This platform identifier can for example help detect if hello software is properly licensed or help toocorrelate any VM data tooits source such as tooassist on setting hello right metrics for hello right platform and tootrack and correlate these metrics amongst other uses.</span></span>

