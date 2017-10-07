---
title: "aaaUsing hello Windows 上的 Azure CLI |Microsoft 文件"
description: "使用 Windows hello Azure CLI"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a><span data-ttu-id="dfe05-103">使用 Windows hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dfe05-103">Using hello Azure CLI on Windows</span></span>

<span data-ttu-id="dfe05-104">hello Azure 命令列介面 (CLI) 會提供命令列和指令碼環境來建立和管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="dfe05-104">hello Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="dfe05-105">hello Azure CLI 可用 macOS、 Linux 及 Windows 作業系統。</span><span class="sxs-lookup"><span data-stu-id="dfe05-105">hello Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="dfe05-106">在這些作業系統，hello CLI 命令是相同的但是可以在不同作業系統特定的指令碼語法。</span><span class="sxs-lookup"><span data-stu-id="dfe05-106">Across these operating systems, hello CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="dfe05-107">Hello Azure CLI 此文件詳細資料 hello 方法可以安裝和執行 Windows 和詳細資料每個語法的考量。</span><span class="sxs-lookup"><span data-stu-id="dfe05-107">This document details hello ways that hello Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="dfe05-108">如需深入的 Azure CLI 文件，請參閱 [Azure CLI 文件]( https://docs.microsoft.com/en-us/cli/azure/overview) (英文)。</span><span class="sxs-lookup"><span data-stu-id="dfe05-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="dfe05-109">適用於 Linux 的 Windows 子系統</span><span class="sxs-lookup"><span data-stu-id="dfe05-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="dfe05-110">hello Windows 子系統 Linux (WSL) 提供 Windows 10 年度和更新版本上的 Ubuntu Linux 環境。</span><span class="sxs-lookup"><span data-stu-id="dfe05-110">hello Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="dfe05-111">啟用時，WSL 會提供原生 Bash 體驗，以供用來建立和執行 Azure CLI 指令碼。</span><span class="sxs-lookup"><span data-stu-id="dfe05-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="dfe05-112">因為 WSL 會提供原生 Bash 體驗，Azure CLI 指令碼可以在 Mac OS、Linux 和 Windows 之間共用而不需要修改。</span><span class="sxs-lookup"><span data-stu-id="dfe05-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="dfe05-113">toouse hello Azure CLI 中 WSL，完成下列 hello。</span><span class="sxs-lookup"><span data-stu-id="dfe05-113">toouse hello Azure CLI in WSL, complete hello following.</span></span>

|<span data-ttu-id="dfe05-114">Task</span><span class="sxs-lookup"><span data-stu-id="dfe05-114">Task</span></span> | <span data-ttu-id="dfe05-115">範例的指示</span><span class="sxs-lookup"><span data-stu-id="dfe05-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="dfe05-116">啟用 WSL</span><span class="sxs-lookup"><span data-stu-id="dfe05-116">Enable WSL</span></span> | [<span data-ttu-id="dfe05-117">安裝 WSL 文件</span><span class="sxs-lookup"><span data-stu-id="dfe05-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="dfe05-118">安裝 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dfe05-118">Install hello Azure CLI</span></span> |[<span data-ttu-id="dfe05-119">WSL/Ubuntu 14.04 上安裝 hello CLI</span><span class="sxs-lookup"><span data-stu-id="dfe05-119">Install hello CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="dfe05-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfe05-120">PowerShell</span></span>

<span data-ttu-id="dfe05-121">hello Azure CLI 可以在 Windows 中的原生方式執行。</span><span class="sxs-lookup"><span data-stu-id="dfe05-121">hello Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="dfe05-122">在此組態中，hello Windows 作業系統上安裝 hello Azure CLI 封裝，可以從 PowerShell 執行命令。</span><span class="sxs-lookup"><span data-stu-id="dfe05-122">In this configuration, hello Azure CLI package is installed on hello Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="dfe05-123">在此組態中，Azure CLI 命令和指令碼可以執行於任何受支援的 Windows 版本，但必須使用平台特定的指令碼語法。</span><span class="sxs-lookup"><span data-stu-id="dfe05-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="dfe05-124">因此，指令碼不一定能在 Mac OS、Linux 和 Windows 之間共用而不需要修改。</span><span class="sxs-lookup"><span data-stu-id="dfe05-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="dfe05-125">toouse hello Azure CLI 在 Windows 中，安裝使用這些指示，hello 封裝[安裝 hello Windows 上的 CLI](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows)。</span><span class="sxs-lookup"><span data-stu-id="dfe05-125">toouse hello Azure CLI on Windows, install hello package using these instructions, [Install hello CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="dfe05-126">Docker 映像</span><span class="sxs-lookup"><span data-stu-id="dfe05-126">Docker Image</span></span>

<span data-ttu-id="dfe05-127">當使用 Docker for Windows，Docker 映像可以啟動包含 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="dfe05-127">When using Docker for Windows, a Docker image can be started that includes hello Azure CLI.</span></span> <span data-ttu-id="dfe05-128">此映像是以 Linux 為基礎，並包含原生 Bash 體驗。</span><span class="sxs-lookup"><span data-stu-id="dfe05-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="dfe05-129">當使用 Docker for Windows 和 hello Azure CLI 映像、 指令碼 toobe macOS、 Linux 及 Windows 之間共用。</span><span class="sxs-lookup"><span data-stu-id="dfe05-129">When using Docker for Windows and hello Azure CLI image, scripts toobe shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="dfe05-130">Docker for Windows 正在執行，並執行下列命令的 hello，請確定 toouse hello Azure CLI Docker for Windows 上。</span><span class="sxs-lookup"><span data-stu-id="dfe05-130">toouse hello Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run hello following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="dfe05-131">一旦完成，也就是啟動工作階段，將 Bash 預先載入 hello Azure CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="dfe05-131">Once completed, a Bash session will start that is preloaded with hello Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfe05-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfe05-132">Next Steps</span></span>

[<span data-ttu-id="dfe05-133">Azure 虛擬機器的 CLI 範例</span><span class="sxs-lookup"><span data-stu-id="dfe05-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="dfe05-134">Azure Web Apps 的 CLI 範例</span><span class="sxs-lookup"><span data-stu-id="dfe05-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="dfe05-135">Azure SQL 的 CLI 範例</span><span class="sxs-lookup"><span data-stu-id="dfe05-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
