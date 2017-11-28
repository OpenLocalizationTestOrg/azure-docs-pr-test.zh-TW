---
title: "啟用或停用 Azure VM 監視"
description: "說明如何啟用或停用 Azure VM 監視"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 9b2fe579113d6ca6bfd27d82eb9d4657657d44ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="60139-103">啟用或停用 Azure VM 監視</span><span class="sxs-lookup"><span data-stu-id="60139-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="60139-104">本節說明如何在 Azure 上執行的虛擬機器上啟用或停用監視。</span><span class="sxs-lookup"><span data-stu-id="60139-104">This section describes how to enable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="60139-105">您可以使用入口網站或適用於 Mac、Linux 和 Windows (Azure CLI) 的 Azure 命令列介面啟用或停用監視。</span><span class="sxs-lookup"><span data-stu-id="60139-105">You can enable or disable monitoring using the portal or Azure Command-line Interface for Mac, Linux, and Windows (the Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60139-106">本文件說明的 Linux 診斷延伸模組 2.3 版已被取代。</span><span class="sxs-lookup"><span data-stu-id="60139-106">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="60139-107">至 2018 年 6 月 30 日止就不再支援 2.3 版。</span><span class="sxs-lookup"><span data-stu-id="60139-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="60139-108">屆時可以啟用 3.0 版的 Linux 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="60139-108">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="60139-109">如需詳細資訊，請參閱[文件](./diagnostic-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="60139-109">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-the-azure-portal"></a><span data-ttu-id="60139-110">透過 Azure 入口網站啟用/停用監視</span><span class="sxs-lookup"><span data-stu-id="60139-110">Enable / Disable Monitoring through the Azure portal</span></span>

<span data-ttu-id="60139-111">您可以啟用 Azure VM 的監視，在 1 分鐘的期間提供您的執行個體相關資料。</span><span class="sxs-lookup"><span data-stu-id="60139-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="60139-112">(儲存體變更適用)。</span><span class="sxs-lookup"><span data-stu-id="60139-112">(storage changes apply).</span></span> <span data-ttu-id="60139-113">接著，詳細的診斷資料可用於入口網站圖形中的 VM，或透過 API 取得。</span><span class="sxs-lookup"><span data-stu-id="60139-113">Detailed diagnostics data is then available for the VM in the portal graphs or through the API.</span></span> <span data-ttu-id="60139-114">根據預設，Azure 入口網站可針對一組有限的計量進行主機監視。</span><span class="sxs-lookup"><span data-stu-id="60139-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="60139-115">您可以在 VM 正在執行或處於停止狀態時，從 VM 內啟用計量監視。</span><span class="sxs-lookup"><span data-stu-id="60139-115">You can enable monitoring of metrics from within a VM while the VM is running or in stopped state.</span></span>

* <span data-ttu-id="60139-116">開啟 Azure 入口網站，位址是 [https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="60139-116">Open the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="60139-117">在左側導覽中，按一下 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="60139-117">In the left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="60139-118">在 [虛擬機器] 清單中，選取執行中或已停止的執行個體。</span><span class="sxs-lookup"><span data-stu-id="60139-118">In the list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="60139-119">[虛擬機器] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="60139-119">The "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="60139-120">按一下 [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="60139-120">Click All settings.</span></span>
* <span data-ttu-id="60139-121">按一下 [診斷]。</span><span class="sxs-lookup"><span data-stu-id="60139-121">Click Diagnostics.</span></span>
* <span data-ttu-id="60139-122">將狀態變更為 [開啟] 或 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="60139-122">Change status to On or Off.</span></span> <span data-ttu-id="60139-123">您也可以在此刀鋒視窗中挑選您要為虛擬機器啟用的監視層級詳細資料。</span><span class="sxs-lookup"><span data-stu-id="60139-123">You can also pick in this blade the level of monitoring details you would like to enable for your virtual machine.</span></span>

![透過 Azure 入口網站啟用/停用監視。][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="60139-125">使用 Azure CLI 啟用/停用監視</span><span class="sxs-lookup"><span data-stu-id="60139-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="60139-126">啟用 Azure VM 的監視。</span><span class="sxs-lookup"><span data-stu-id="60139-126">To enable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="60139-127">建立檔案，並命名為 PrivateConfig.json：</span><span class="sxs-lookup"><span data-stu-id="60139-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"the storage account to receive data",
        "storageAccountKey":"the key of the account"
}
```

* <span data-ttu-id="60139-128">透過 Azure CLI 啟用延伸模組。</span><span class="sxs-lookup"><span data-stu-id="60139-128">Enable the extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="60139-129">如需詳細資訊，請參閱[使用 Linux 診斷延伸模組監視 Linux VM 的效能和診斷資料](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="60139-129">For more information, see [Using Linux Diagnostic Extension to Monitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
