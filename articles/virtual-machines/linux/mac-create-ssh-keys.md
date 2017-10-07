---
title: "aaaCreate 及使用 SSH 金鑰組適用於 Linux Vm 在 Azure 中 |Microsoft 文件"
description: "如何 toocreate，SSH 公開金鑰和私密金鑰組適用於 Linux Vm 中的使用 Azure tooimprove hello hello 驗證程序的安全性。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="7abd4-103">適用於在 Azure 中的 Linux Vm 配對 toocreate 及使用 SSH 公用和私用金鑰的方式</span><span class="sxs-lookup"><span data-stu-id="7abd4-103">How toocreate and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="7abd4-104">使用安全殼層 (SSH) 金鑰組，您可以使用 SSH 金鑰進行驗證，免除對密碼 toolog 中的 hello 需要的 Azure 中建立虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="7abd4-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="7abd4-105">本文章將示範如何 tooquickly 產生及使用 SSH 通訊協定第 2 版 RSA 公開金鑰和私密金鑰的金鑰檔組適用於 Linux Vm。</span><span class="sxs-lookup"><span data-stu-id="7abd4-105">This article shows you how tooquickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="7abd4-106">如需詳細步驟和其他範例，請參閱[詳細步驟 toocreate SSH 金鑰組和憑證](create-ssh-keys-detailed.md)。</span><span class="sxs-lookup"><span data-stu-id="7abd4-106">For more detailed steps and additional examples, see [detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="7abd4-107">建立 SSH 金鑰組</span><span class="sxs-lookup"><span data-stu-id="7abd4-107">Create an SSH key pair</span></span>
<span data-ttu-id="7abd4-108">使用 hello`ssh-keygen`命令 toocreate SSH 公開金鑰和私密金鑰檔案預設建立在 hello`~/.ssh`目錄，但您可以指定不同的位置和其他的複雜密碼 （密碼 tooaccess hello 私密金鑰檔案） 時提示您。</span><span class="sxs-lookup"><span data-stu-id="7abd4-108">Use hello `ssh-keygen` command toocreate SSH public and private key files that are by default created in hello `~/.ssh` directory, but you can specify a different location and additional passphrase (a password tooaccess hello private key file) when prompted.</span></span> <span data-ttu-id="7abd4-109">執行 hello Bash 殼層中的下列命令，建立回答 hello 提示與您自己的資訊。</span><span class="sxs-lookup"><span data-stu-id="7abd4-109">Run hello following command from a Bash shell, answering hello prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a><span data-ttu-id="7abd4-110">使用 hello SSH 金鑰組</span><span class="sxs-lookup"><span data-stu-id="7abd4-110">Use hello SSH key pair</span></span>
<span data-ttu-id="7abd4-111">hello 您放在 Azure 中 Linux VM 的公用金鑰是儲存在預設`~/.ssh/id_rsa.pub`，除非您在建立時，變更 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="7abd4-111">hello public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed hello location when you created them.</span></span> <span data-ttu-id="7abd4-112">如果您使用 hello [Azure CLI 2.0](/cli/azure) toocreate VM，指定此公開金鑰 hello 位置，當您使用 hello [az vm 建立](/cli/azure/vm#create)以 hello`--ssh-key-path`選項。</span><span class="sxs-lookup"><span data-stu-id="7abd4-112">If you use hello [Azure CLI 2.0](/cli/azure) toocreate your VM, specify hello location of this public key when you use hello [az vm create](/cli/azure/vm#create) with hello `--ssh-key-path` option.</span></span> <span data-ttu-id="7abd4-113">如果您複製並貼上 hello Azure 入口網站或資源管理員範本中的 hello 公開金鑰檔案 toouse hello 內容，請確定您沒有複製任何額外的空白字元。</span><span class="sxs-lookup"><span data-stu-id="7abd4-113">If you copy and paste hello contents of hello public key file toouse in hello Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="7abd4-114">例如，如果您使用 OS X，您可以使用管線傳送 hello 公開金鑰檔案 (根據預設， **~/.ssh/id_rsa.pub**) 太**pbcopy** toocopy hello 內容 （有沒有 hello 相同的事物，例如其他Linux程式`xclip`).</span><span class="sxs-lookup"><span data-stu-id="7abd4-114">For example, if you use OS X, you can pipe hello public key file (by default, **~/.ssh/id_rsa.pub**) too**pbcopy** toocopy hello contents (there are other Linux programs that do hello same thing, such as `xclip`).</span></span>

<span data-ttu-id="7abd4-115">如果您不熟悉 SSH 公開金鑰，您可以如下所示執行 `cat`，並以您自己的公開金鑰檔案位置取代 `~/.ssh/id_rsa.pub`，來看到您的公開金鑰︰</span><span class="sxs-lookup"><span data-stu-id="7abd4-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="7abd4-116">使用 hello Azure VM 上的公用金鑰，SSH tooyour VM 使用 hello IP 位址或 DNS 名稱的 VM (請記住 tooreplace`azureuser`和`myvm.westus.cloudapp.azure.com`底下具有 hello 管理員使用者名稱和 hello 完整的網域名稱或 IP 位址):</span><span class="sxs-lookup"><span data-stu-id="7abd4-116">With hello public key on your Azure VM, SSH tooyour VM using hello IP address or DNS name of your VM (remember tooreplace `azureuser` and `myvm.westus.cloudapp.azure.com` below with hello admin username and hello fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="7abd4-117">如果您在建立您的金鑰組時，您會提供複雜密碼，請輸入 hello 複雜密碼 hello 登入程序期間出現提示時。</span><span class="sxs-lookup"><span data-stu-id="7abd4-117">If you provided a passphrase when you created your key pair, enter hello passphrase when prompted during hello login process.</span></span> <span data-ttu-id="7abd4-118">(hello 伺服器新增 tooyour`~/.ssh/known_hosts`資料夾，而您就不會要求 tooconnect 一次，直到 hello 公開金鑰的 Azure VM 變更或移除 hello 伺服器名稱是`~/.ssh/known_hosts`。)</span><span class="sxs-lookup"><span data-stu-id="7abd4-118">(hello server is added tooyour `~/.ssh/known_hosts` folder, and you won't be asked tooconnect again until hello public key on your Azure VM changes or hello server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7abd4-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7abd4-119">Next steps</span></span>

<span data-ttu-id="7abd4-120">依預設停用的密碼設定是使用 SSH 金鑰建立的 Vm，大幅更耗費資源，因此難以猜測 toomake 暴力密碼破解強制嘗試。</span><span class="sxs-lookup"><span data-stu-id="7abd4-120">VMs created using SSH keys are by default configured with passwords disabled, toomake brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="7abd4-121">本主題描述如何建立簡單的 SSH 金鑰組以供快速使用。</span><span class="sxs-lookup"><span data-stu-id="7abd4-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="7abd4-122">如果您需要更多協助建立您的 SSH 金鑰組，或需要其他憑證，請參閱[詳細步驟 toocreate SSH 金鑰組和憑證](create-ssh-keys-detailed.md)。</span><span class="sxs-lookup"><span data-stu-id="7abd4-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="7abd4-123">您可以建立使用您使用 hello Azure 入口網站、 CLI 和範本的 SSH 金鑰組的 Vm:</span><span class="sxs-lookup"><span data-stu-id="7abd4-123">You can create VMs that use your SSH key pair using hello Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="7abd4-124">建立安全的 Linux VM，使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7abd4-124">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7abd4-125">建立安全的 Linux VM，使用 hello Azure CLI 2.0）</span><span class="sxs-lookup"><span data-stu-id="7abd4-125">Create a secure Linux VM using hello Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7abd4-126">使用 Azure 範本建立安全的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="7abd4-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
