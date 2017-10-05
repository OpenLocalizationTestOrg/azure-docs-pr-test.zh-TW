---
title: "使用 SCP 將檔案移入和移出 Azure Linux VM | Microsoft Docs"
description: "使用 SCP 和 SSH 金鑰組將檔案安全地移入和移出 Azure 中的 Linux VM。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 736f7c11ec3de04f1ad52ee29d0a4c952c9b0545
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="move-files-to-and-from-a-linux-vm-using-scp"></a><span data-ttu-id="16a8f-103">使用 SCP 將檔案移入和移出 Linux VM</span><span class="sxs-lookup"><span data-stu-id="16a8f-103">Move files to and from a Linux VM using SCP</span></span>

<span data-ttu-id="16a8f-104">本文說明如何使用安全複製 (SCP) 從您的工作站將檔案上移至 Azure Linux VM，或從 Azure Linux VM 下移至您的工作站。</span><span class="sxs-lookup"><span data-stu-id="16a8f-104">This article shows how to move files from your workstation up to an Azure Linux VM, or from an Azure Linux VM down to your workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="16a8f-105">在您的工作站與 Linux VM 之間快速又安全地移動檔案，對於管理您的 Azure 基礎結構來說相當重要。</span><span class="sxs-lookup"><span data-stu-id="16a8f-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="16a8f-106">針對本文，您需要一個使用 [SSH 公開和私密金鑰檔案](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)在 Azure 中部署的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="16a8f-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="16a8f-107">此外，還需要一個用於您本機電腦的 SCP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="16a8f-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="16a8f-108">此工具建置在 SSH 之上，並包含在大多數 Linux 和 Mac 電腦的預設 Bash 殼層中，以及部分 Windows 殼層中。</span><span class="sxs-lookup"><span data-stu-id="16a8f-108">It is built on top of SSH and included in the default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="16a8f-109">快速命令</span><span class="sxs-lookup"><span data-stu-id="16a8f-109">Quick commands</span></span>

<span data-ttu-id="16a8f-110">將檔案向上複製到 Linux VM</span><span class="sxs-lookup"><span data-stu-id="16a8f-110">Copy a file up to the Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="16a8f-111">從 Linux VM 向下複製檔案</span><span class="sxs-lookup"><span data-stu-id="16a8f-111">Copy a file down from the Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="16a8f-112">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="16a8f-112">Detailed walkthrough</span></span>

<span data-ttu-id="16a8f-113">作為範例，我們會將 Azure 組態檔上移至 Linux VM，以及將記錄檔目錄下拉，兩者皆使用 SCP 和 SSH 金鑰來完成。</span><span class="sxs-lookup"><span data-stu-id="16a8f-113">As examples, we move an Azure configuration file up to a Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="16a8f-114">SSH 金鑰組驗證</span><span class="sxs-lookup"><span data-stu-id="16a8f-114">SSH key pair authentication</span></span>

<span data-ttu-id="16a8f-115">SCP 會針對傳輸層使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="16a8f-115">SCP uses SSH for the transport layer.</span></span> <span data-ttu-id="16a8f-116">SSH 會處理目的地主機上的驗證，它會在 SSH 預設提供的加密通道中移動檔案。</span><span class="sxs-lookup"><span data-stu-id="16a8f-116">SSH handles the authentication on the destination host, and it moves the file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="16a8f-117">針對 SSH 驗證，可以使用使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="16a8f-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="16a8f-118">不過，建議的安全性最佳做法是使用 SSH 公用和私密金鑰驗證。</span><span class="sxs-lookup"><span data-stu-id="16a8f-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="16a8f-119">在 SSH 驗證連線之後，SCP 就會開始複製檔案。</span><span class="sxs-lookup"><span data-stu-id="16a8f-119">Once SSH has authenticated the connection, SCP then begins copying the file.</span></span> <span data-ttu-id="16a8f-120">藉由使用已正確設定的 `~/.ssh/config` 和 SSH 公用與私密金鑰，只要使用伺服器名稱 (或 IP 位址)，即可建立 SCP 連線。</span><span class="sxs-lookup"><span data-stu-id="16a8f-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, the SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="16a8f-121">如果您只有一個 SSH 金鑰，SCP 會在 `~/.ssh/` 目錄中尋找它，並預設使用它來登入 VM。</span><span class="sxs-lookup"><span data-stu-id="16a8f-121">If you only have one SSH key, SCP looks for it in the `~/.ssh/` directory, and uses it by default to log in to the VM.</span></span>

<span data-ttu-id="16a8f-122">如需有關設定您的 `~/.ssh/config` 和 SSH 公用與私密金鑰的詳細資訊，請參閱[建立 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="16a8f-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-to-a-linux-vm"></a><span data-ttu-id="16a8f-123">SCP 檔案至 Linux VM</span><span class="sxs-lookup"><span data-stu-id="16a8f-123">SCP a file to a Linux VM</span></span>

<span data-ttu-id="16a8f-124">針對第一個範例，我們會將用來部署自動化的 Azure 組態檔向上複製到 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="16a8f-124">For the first example, we copy an Azure configuration file up to a Linux VM that is used to deploy automation.</span></span> <span data-ttu-id="16a8f-125">由於這個檔案包含 Azure API 認證，其中包含祕密，因此安全性很重要。</span><span class="sxs-lookup"><span data-stu-id="16a8f-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="16a8f-126">SSH 提供的加密通道可保護此檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="16a8f-126">The encrypted tunnel provided by SSH protects the contents of the file.</span></span>

<span data-ttu-id="16a8f-127">下列命令會將本機 *.azure/config* 檔案複製到 FQDN 為 *myserver.eastus.cloudapp.azure.com* 的 Azure VM。Azure VM 上的管理使用者名稱是 *azureuser*。</span><span class="sxs-lookup"><span data-stu-id="16a8f-127">The following command copies the local *.azure/config* file to an Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. The admin user name on the Azure VM is *azureuser*.</span></span> <span data-ttu-id="16a8f-128">此檔案的目標為 */home/azureuser/* 目錄。</span><span class="sxs-lookup"><span data-stu-id="16a8f-128">The file is targeted to the */home/azureuser/* directory.</span></span> <span data-ttu-id="16a8f-129">請在此命令中使用您自己的值來替代。</span><span class="sxs-lookup"><span data-stu-id="16a8f-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="16a8f-130">從 Linux VM SCP 目錄</span><span class="sxs-lookup"><span data-stu-id="16a8f-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="16a8f-131">針對此範例，我們會從 Linux VM 將記錄檔目錄向下複製到您的工作站。</span><span class="sxs-lookup"><span data-stu-id="16a8f-131">For this example, we copy a directory of log files from the Linux VM down to your workstation.</span></span> <span data-ttu-id="16a8f-132">記錄檔可能包含也可能不包含敏感或祕密資料。</span><span class="sxs-lookup"><span data-stu-id="16a8f-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="16a8f-133">不過，使用 SCP 可確保將記錄檔的內容加密。</span><span class="sxs-lookup"><span data-stu-id="16a8f-133">However, using SCP ensures the contents of the log files are encrypted.</span></span> <span data-ttu-id="16a8f-134">使用 SCP 來傳輸檔案，不僅是將記錄檔目錄和檔案向下移到您工作站的最簡單方式，同時也很安全。</span><span class="sxs-lookup"><span data-stu-id="16a8f-134">Using SCP to transfer the files is the easiest way to get the log directory and files down to your workstation while also being secure.</span></span>

<span data-ttu-id="16a8f-135">下列命令會將 Azure VM 上 */home/azureuser/logs/* 目錄中的檔案複製到本機 /tmp 目錄：</span><span class="sxs-lookup"><span data-stu-id="16a8f-135">The following command copies files in the */home/azureuser/logs/* directory on the Azure VM to the local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="16a8f-136">`-r` CLI 旗標指示 SCP 以遞迴方式從命令中列出的目錄點複製檔案和目錄。</span><span class="sxs-lookup"><span data-stu-id="16a8f-136">The `-r` cli flag instructs SCP to recursively copy the files and directories from the point of the directory listed in the command.</span></span>  <span data-ttu-id="16a8f-137">另請注意，命令列語法類似 `cp` 複製命令。</span><span class="sxs-lookup"><span data-stu-id="16a8f-137">Also notice that the command-line syntax is similar to a `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16a8f-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16a8f-138">Next steps</span></span>

* [<span data-ttu-id="16a8f-139">管理使用者、SSH，並使用 VMAccess 擴充功能檢查或修復 Azure Linux VM 上的磁碟</span><span class="sxs-lookup"><span data-stu-id="16a8f-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)