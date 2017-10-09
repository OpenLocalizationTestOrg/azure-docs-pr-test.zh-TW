---
title: "aaaEnable 或停用 Azure VM 監視"
description: "描述如何 tooEnable] 或 [停用 Azure VM 監視"
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
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="420c0-103">啟用或停用 Azure VM 監視</span><span class="sxs-lookup"><span data-stu-id="420c0-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="420c0-104">本章節描述如何 tooenable 或停用監視上虛擬機器在 Azure 上執行。</span><span class="sxs-lookup"><span data-stu-id="420c0-104">This section describes how tooenable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="420c0-105">您可以啟用或停用監視使用 hello 入口網站或 Azure 命令列介面的 Mac、 Linux 及 Windows (hello Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="420c0-105">You can enable or disable monitoring using hello portal or Azure Command-line Interface for Mac, Linux, and Windows (hello Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="420c0-106">本文件說明 2.3 版 hello Linux 診斷延伸，其中已被取代。</span><span class="sxs-lookup"><span data-stu-id="420c0-106">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="420c0-107">至 2018 年 6 月 30 日止就不再支援 2.3 版。</span><span class="sxs-lookup"><span data-stu-id="420c0-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="420c0-108">3.0 版的 hello Linux 診斷延伸模組可以改為啟用。</span><span class="sxs-lookup"><span data-stu-id="420c0-108">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="420c0-109">如需詳細資訊，請參閱[hello 文件](./diagnostic-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="420c0-109">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a><span data-ttu-id="420c0-110">啟用/停用監視 hello 透過 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="420c0-110">Enable / Disable Monitoring through hello Azure portal</span></span>

<span data-ttu-id="420c0-111">您可以啟用 Azure VM 的監視，在 1 分鐘的期間提供您的執行個體相關資料。</span><span class="sxs-lookup"><span data-stu-id="420c0-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="420c0-112">(儲存體變更適用)。</span><span class="sxs-lookup"><span data-stu-id="420c0-112">(storage changes apply).</span></span> <span data-ttu-id="420c0-113">然後使用 hello VM hello 入口網站圖表或透過 hello API 詳細的診斷資料。</span><span class="sxs-lookup"><span data-stu-id="420c0-113">Detailed diagnostics data is then available for hello VM in hello portal graphs or through hello API.</span></span> <span data-ttu-id="420c0-114">根據預設，Azure 入口網站可針對一組有限的計量進行主機監視。</span><span class="sxs-lookup"><span data-stu-id="420c0-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="420c0-115">您可以啟用來自 hello 執行 VM 時或在已停止狀態，在 VM 內的度量的監視。</span><span class="sxs-lookup"><span data-stu-id="420c0-115">You can enable monitoring of metrics from within a VM while hello VM is running or in stopped state.</span></span>

* <span data-ttu-id="420c0-116">開啟 hello Azure 入口網站在[https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="420c0-116">Open hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="420c0-117">在左瀏覽 hello，按一下 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="420c0-117">In hello left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="420c0-118">在 hello 列出虛擬機器，選取 執行中或已停止的執行個體。</span><span class="sxs-lookup"><span data-stu-id="420c0-118">In hello list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="420c0-119">hello 「 虛擬機器 」 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="420c0-119">hello "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="420c0-120">按一下 [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="420c0-120">Click All settings.</span></span>
* <span data-ttu-id="420c0-121">按一下 [診斷]。</span><span class="sxs-lookup"><span data-stu-id="420c0-121">Click Diagnostics.</span></span>
* <span data-ttu-id="420c0-122">變更狀態 tooOn 或設為 Off。</span><span class="sxs-lookup"><span data-stu-id="420c0-122">Change status tooOn or Off.</span></span> <span data-ttu-id="420c0-123">您也可以挑選此刀鋒視窗 hello 層級監視您想要 tooenable 虛擬機器的詳細資料中。</span><span class="sxs-lookup"><span data-stu-id="420c0-123">You can also pick in this blade hello level of monitoring details you would like tooenable for your virtual machine.</span></span>

![啟用/停用透過 hello Azure 入口網站的監視。][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="420c0-125">使用 Azure CLI 啟用/停用監視</span><span class="sxs-lookup"><span data-stu-id="420c0-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="420c0-126">tooenable 監視的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="420c0-126">tooenable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="420c0-127">建立檔案，並命名為 PrivateConfig.json：</span><span class="sxs-lookup"><span data-stu-id="420c0-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* <span data-ttu-id="420c0-128">啟用透過 Azure CLI hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="420c0-128">Enable hello extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="420c0-129">如需詳細資訊，請參閱[使用 Linux 診斷延伸模組 tooMonitor Linux VM 的效能和診斷資料](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="420c0-129">For more information, see [Using Linux Diagnostic Extension tooMonitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
