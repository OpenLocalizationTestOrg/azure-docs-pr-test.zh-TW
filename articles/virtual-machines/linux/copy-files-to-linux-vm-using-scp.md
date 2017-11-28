---
title: "aaaMove 檔案從與 SCP Azure Linux Vm tooand |Microsoft 文件"
description: "安全地移動檔案 tooand 從 Linux VM 在 Azure 中使用 SCP 和 SSH 金鑰組。"
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
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a><span data-ttu-id="14fa6-103">移動檔案 tooand 從 Linux VM 使用 SCP</span><span class="sxs-lookup"><span data-stu-id="14fa6-103">Move files tooand from a Linux VM using SCP</span></span>

<span data-ttu-id="14fa6-104">本文將說明如何 toomove 檔案從您的工作站上 tooan Azure Linux VM，或從 Azure Linux VM 關閉 tooyour 工作站上，使用安全複製 (SCP)。</span><span class="sxs-lookup"><span data-stu-id="14fa6-104">This article shows how toomove files from your workstation up tooan Azure Linux VM, or from an Azure Linux VM down tooyour workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="14fa6-105">在您的工作站與 Linux VM 之間快速又安全地移動檔案，對於管理您的 Azure 基礎結構來說相當重要。</span><span class="sxs-lookup"><span data-stu-id="14fa6-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="14fa6-106">針對本文，您需要一個使用 [SSH 公開和私密金鑰檔案](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)在 Azure 中部署的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="14fa6-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="14fa6-107">此外，還需要一個用於您本機電腦的 SCP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="14fa6-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="14fa6-108">它是之上 SSH，而且包含在大部分的 Linux 和 Mac 電腦和一些 Windows 殼層 hello 預設 Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="14fa6-108">It is built on top of SSH and included in hello default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="14fa6-109">快速命令</span><span class="sxs-lookup"><span data-stu-id="14fa6-109">Quick commands</span></span>

<span data-ttu-id="14fa6-110">複製 toohello Linux VM 上的檔案</span><span class="sxs-lookup"><span data-stu-id="14fa6-110">Copy a file up toohello Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="14fa6-111">從 hello Linux VM，向下複製檔案</span><span class="sxs-lookup"><span data-stu-id="14fa6-111">Copy a file down from hello Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="14fa6-112">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="14fa6-112">Detailed walkthrough</span></span>

<span data-ttu-id="14fa6-113">做為範例，我們移動 tooa Linux VM 上的 Azure 組態檔，並提取的記錄檔目錄，同時使用 SCP 和 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="14fa6-113">As examples, we move an Azure configuration file up tooa Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="14fa6-114">SSH 金鑰組驗證</span><span class="sxs-lookup"><span data-stu-id="14fa6-114">SSH key pair authentication</span></span>

<span data-ttu-id="14fa6-115">SCP hello 傳輸層使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="14fa6-115">SCP uses SSH for hello transport layer.</span></span> <span data-ttu-id="14fa6-116">SSH 控點 hello hello 目的地主機上，驗證並移動透過 SSH 預設提供的加密通道中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="14fa6-116">SSH handles hello authentication on hello destination host, and it moves hello file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="14fa6-117">針對 SSH 驗證，可以使用使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="14fa6-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="14fa6-118">不過，建議的安全性最佳做法是使用 SSH 公用和私密金鑰驗證。</span><span class="sxs-lookup"><span data-stu-id="14fa6-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="14fa6-119">SSH 驗證 hello 連接，一旦 SCP，就會開始將 hello 檔案複製。</span><span class="sxs-lookup"><span data-stu-id="14fa6-119">Once SSH has authenticated hello connection, SCP then begins copying hello file.</span></span> <span data-ttu-id="14fa6-120">使用已正確設定`~/.ssh/config`和 SSH 公用和私用索引鍵，hello SCP 連線可以建立只使用伺服器名稱 （或 IP 位址）。</span><span class="sxs-lookup"><span data-stu-id="14fa6-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, hello SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="14fa6-121">如果您只有一個 SSH 金鑰，SCP 它會以尋找 hello`~/.ssh/`目錄，並使用它的預設 toolog toohello VM 中。</span><span class="sxs-lookup"><span data-stu-id="14fa6-121">If you only have one SSH key, SCP looks for it in hello `~/.ssh/` directory, and uses it by default toolog in toohello VM.</span></span>

<span data-ttu-id="14fa6-122">如需有關設定您的 `~/.ssh/config` 和 SSH 公用與私密金鑰的詳細資訊，請參閱[建立 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="14fa6-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-tooa-linux-vm"></a><span data-ttu-id="14fa6-123">SCP 檔案 tooa Linux VM</span><span class="sxs-lookup"><span data-stu-id="14fa6-123">SCP a file tooa Linux VM</span></span>

<span data-ttu-id="14fa6-124">Hello 第一個範例中，我們要複製 tooa 是使用的 toodeploy 自動化的 Linux VM 上的 Azure 組態檔。</span><span class="sxs-lookup"><span data-stu-id="14fa6-124">For hello first example, we copy an Azure configuration file up tooa Linux VM that is used toodeploy automation.</span></span> <span data-ttu-id="14fa6-125">由於這個檔案包含 Azure API 認證，其中包含祕密，因此安全性很重要。</span><span class="sxs-lookup"><span data-stu-id="14fa6-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="14fa6-126">提供的 SSH hello 加密的通道保護 hello hello 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="14fa6-126">hello encrypted tunnel provided by SSH protects hello contents of hello file.</span></span>

<span data-ttu-id="14fa6-127">下列命令複製 hello 本機 hello *.azure/config*檔案 tooan fqdn 的 Azure VM *myserver.eastus.cloudapp.azure.com*。 hello Azure VM 上的 hello 系統管理員使用者名稱是*azureuser*.</span><span class="sxs-lookup"><span data-stu-id="14fa6-127">hello following command copies hello local *.azure/config* file tooan Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. hello admin user name on hello Azure VM is *azureuser*.</span></span> <span data-ttu-id="14fa6-128">hello 檔案是目標的 toohello */首頁/azureuser/*目錄。</span><span class="sxs-lookup"><span data-stu-id="14fa6-128">hello file is targeted toohello */home/azureuser/* directory.</span></span> <span data-ttu-id="14fa6-129">請在此命令中使用您自己的值來替代。</span><span class="sxs-lookup"><span data-stu-id="14fa6-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="14fa6-130">從 Linux VM SCP 目錄</span><span class="sxs-lookup"><span data-stu-id="14fa6-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="14fa6-131">針對此範例中，我們要複製記錄檔的目錄從 hello Linux VM 關閉 tooyour 工作站。</span><span class="sxs-lookup"><span data-stu-id="14fa6-131">For this example, we copy a directory of log files from hello Linux VM down tooyour workstation.</span></span> <span data-ttu-id="14fa6-132">記錄檔可能包含也可能不包含敏感或祕密資料。</span><span class="sxs-lookup"><span data-stu-id="14fa6-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="14fa6-133">不過，使用 SCP，確保加密 hello hello 記錄檔的內容。</span><span class="sxs-lookup"><span data-stu-id="14fa6-133">However, using SCP ensures hello contents of hello log files are encrypted.</span></span> <span data-ttu-id="14fa6-134">使用 SCP tootransfer hello 檔案是最簡單方式 tooget hello hello 記錄目錄和檔案向 tooyour 工作站，同時也會安全。</span><span class="sxs-lookup"><span data-stu-id="14fa6-134">Using SCP tootransfer hello files is hello easiest way tooget hello log directory and files down tooyour workstation while also being secure.</span></span>

<span data-ttu-id="14fa6-135">hello 下列命令會將複製檔案在 hello */首頁/azureuser/記錄檔/*目錄 hello Azure VM toohello 本機 tec_rule 位於 /tmp 目錄：</span><span class="sxs-lookup"><span data-stu-id="14fa6-135">hello following command copies files in hello */home/azureuser/logs/* directory on hello Azure VM toohello local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="14fa6-136">hello `-r` cli 旗標指示中列出 hello 命令中的 hello 目錄 hello 點 SCP toorecursively 複製 hello 檔案及目錄。</span><span class="sxs-lookup"><span data-stu-id="14fa6-136">hello `-r` cli flag instructs SCP toorecursively copy hello files and directories from hello point of hello directory listed in hello command.</span></span>  <span data-ttu-id="14fa6-137">請注意，hello 命令列語法也是類似 tooa`cp`複製命令。</span><span class="sxs-lookup"><span data-stu-id="14fa6-137">Also notice that hello command-line syntax is similar tooa `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14fa6-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14fa6-138">Next steps</span></span>

* [<span data-ttu-id="14fa6-139">管理使用者、 SSH 和核取，或使用 Azure Linux Vm 上的修復磁片 hello VMAccess 擴充功能</span><span class="sxs-lookup"><span data-stu-id="14fa6-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
