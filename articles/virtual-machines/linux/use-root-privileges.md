---
title: "在 Linux 虛擬機器上使用根權限 | Microsoft Docs"
description: "了解如何在 Azure 中的 Linux 虛擬機器上使用根權限。"
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
ms.openlocfilehash: dc39db1f5fecffb60499a5420bfe72850e2fffd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="cda50-103">在 Azure 中的 Linux 虛擬機器上使用根權限</span><span class="sxs-lookup"><span data-stu-id="cda50-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="cda50-104">在 Azure 中的 Linux 虛擬機器上，依預設會停用 `root` 使用者。</span><span class="sxs-lookup"><span data-stu-id="cda50-104">By default, the `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="cda50-105">使用者可以使用 `sudo` 命令，以提高的權限來執行命令。</span><span class="sxs-lookup"><span data-stu-id="cda50-105">Users can run commands with elevated privileges by using the `sudo` command.</span></span> <span data-ttu-id="cda50-106">不過，根據系統如何佈建而定，操作過程可能不同。</span><span class="sxs-lookup"><span data-stu-id="cda50-106">However, the experience may vary depending on how the system was provisioned.</span></span>

1. <span data-ttu-id="cda50-107">**SSH 金鑰和密碼，或僅密碼** - 虛擬機器是以憑證 (`.CER` 檔案) 或 SSH 金鑰和密碼來佈建，或只以使用者名稱和密碼來佈建。</span><span class="sxs-lookup"><span data-stu-id="cda50-107">**SSH key and password OR password only** - the virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="cda50-108">在此情況下，執行命令之前， `sudo` 會提示輸入使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="cda50-108">In this case `sudo` will prompt for the user's password before executing the command.</span></span>
2. <span data-ttu-id="cda50-109">**僅 SSH 金鑰** - 虛擬機器是以憑證 (`.cer`、`.pem` 或 `.pub` 檔案) 或 SSH 金鑰來佈建，而未使用密碼。</span><span class="sxs-lookup"><span data-stu-id="cda50-109">**SSH key only** - the virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="cda50-110">在此情況下，執行命令之前， `sudo` **不會** 提示輸入使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="cda50-110">In this case `sudo` **will not** prompt for the user's password before executing the command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="cda50-111">SSH 金鑰和密碼，或僅密碼</span><span class="sxs-lookup"><span data-stu-id="cda50-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="cda50-112">使用 SSH 金鑰或密碼驗證來登入 Linux 虛擬機器，然後使用 `sudo`執行命令，例如：</span><span class="sxs-lookup"><span data-stu-id="cda50-112">Log into the Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="cda50-113">在此例子中，將會提示使用者輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="cda50-113">In this case the user will be prompted for a password.</span></span> <span data-ttu-id="cda50-114">輸入密碼之後，`sudo` 將會以 `root` 權限執行命令。</span><span class="sxs-lookup"><span data-stu-id="cda50-114">After entering the password `sudo` will run the command with `root` privileges.</span></span>

<span data-ttu-id="cda50-115">您也可以編輯 `/etc/sudoers.d/waagent` 檔案來啟用 passwordless sudo，例如：</span><span class="sxs-lookup"><span data-stu-id="cda50-115">You can also enable passwordless sudo by editing the `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="cda50-116">這項變更將允許「azureuser」使用者的 passwordless sudo。</span><span class="sxs-lookup"><span data-stu-id="cda50-116">This change will allow for passwordless sudo by the user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="cda50-117">僅 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="cda50-117">SSH Key Only</span></span>
<span data-ttu-id="cda50-118">使用 SSH 金鑰驗證來登入 Linux 虛擬機器，然後使用 `sudo`執行命令，例如：</span><span class="sxs-lookup"><span data-stu-id="cda50-118">Log into the Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="cda50-119">在此例子中，將 **不會** 提示使用者輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="cda50-119">In this case the user will **not** be prompted for a password.</span></span> <span data-ttu-id="cda50-120">按 `<enter>` 鍵之後，`sudo` 將會以 `root` 權限執行命令。</span><span class="sxs-lookup"><span data-stu-id="cda50-120">After pressing `<enter>`, `sudo` will run the command with `root` privileges.</span></span>

