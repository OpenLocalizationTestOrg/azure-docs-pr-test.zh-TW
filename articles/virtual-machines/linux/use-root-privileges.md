---
title: "在 Linux 虛擬機器上的 aaaUse 根權限 |Microsoft 文件"
description: "了解 toouse 根在 Azure 中 Linux 虛擬機器上的權限。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="8d4b2-103">在 Azure 中的 Linux 虛擬機器上使用根權限</span><span class="sxs-lookup"><span data-stu-id="8d4b2-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="8d4b2-104">根據預設，hello`root`在 Azure 中 Linux 虛擬機器上停用使用者。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-104">By default, hello `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="8d4b2-105">使用者可以執行使用更高權限命令使用 hello`sudo`命令。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-105">Users can run commands with elevated privileges by using hello `sudo` command.</span></span> <span data-ttu-id="8d4b2-106">不過，hello 經驗會根據 hello 系統已佈建方式而有所不同。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-106">However, hello experience may vary depending on how hello system was provisioned.</span></span>

1. <span data-ttu-id="8d4b2-107">**SSH 金鑰和密碼只能使用 OR 密碼**-hello 虛擬機器佈建並提供兩個憑證 (`.CER`檔案) 或 SSH 金鑰，以及密碼，或只要使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-107">**SSH key and password OR password only** - hello virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="8d4b2-108">在此情況下`sudo`會提示輸入 hello 使用者的密碼，然後再執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-108">In this case `sudo` will prompt for hello user's password before executing hello command.</span></span>
2. <span data-ttu-id="8d4b2-109">**僅使用 SSH 金鑰**-hello 虛擬機器所使用的憑證佈建 (`.cer`， `.pem`，或`.pub`檔案) 或 SSH 金鑰，但沒有密碼。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-109">**SSH key only** - hello virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="8d4b2-110">在此情況下`sudo`**則不會**hello 使用者的密碼，才能執行 hello 命令提示。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-110">In this case `sudo` **will not** prompt for hello user's password before executing hello command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="8d4b2-111">SSH 金鑰和密碼，或僅密碼</span><span class="sxs-lookup"><span data-stu-id="8d4b2-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="8d4b2-112">登入使用 SSH 金鑰或密碼驗證時，hello Linux 虛擬機器，然後再執行命令使用`sudo`，例如：</span><span class="sxs-lookup"><span data-stu-id="8d4b2-112">Log into hello Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="8d4b2-113">在此情況下 hello 使用者將會提示輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-113">In this case hello user will be prompted for a password.</span></span> <span data-ttu-id="8d4b2-114">輸入 hello 密碼之後`sudo`會執行與 hello 命令`root`權限。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-114">After entering hello password `sudo` will run hello command with `root` privileges.</span></span>

<span data-ttu-id="8d4b2-115">您也可以藉由編輯 hello 啟用 passwordless sudo`/etc/sudoers.d/waagent`檔案，例如：</span><span class="sxs-lookup"><span data-stu-id="8d4b2-115">You can also enable passwordless sudo by editing hello `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="8d4b2-116">這項變更可讓 passwordless sudo hello 使用者 」 azureuser"。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-116">This change will allow for passwordless sudo by hello user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="8d4b2-117">僅 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="8d4b2-117">SSH Key Only</span></span>
<span data-ttu-id="8d4b2-118">登入 hello Linux 虛擬機器使用 SSH 金鑰驗證，然後再執行命令使用`sudo`，例如：</span><span class="sxs-lookup"><span data-stu-id="8d4b2-118">Log into hello Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="8d4b2-119">在此情況下 hello 使用者將**不**提示輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-119">In this case hello user will **not** be prompted for a password.</span></span> <span data-ttu-id="8d4b2-120">按下之後`<enter>`，`sudo`會執行與 hello 命令`root`權限。</span><span class="sxs-lookup"><span data-stu-id="8d4b2-120">After pressing `<enter>`, `sudo` will run hello command with `root` privileges.</span></span>

