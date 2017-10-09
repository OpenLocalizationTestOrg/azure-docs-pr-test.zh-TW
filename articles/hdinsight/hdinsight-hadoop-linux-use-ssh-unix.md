---
title: "SSH 的 Hadoop-Azure HDInsight aaaUse |Microsoft 文件"
description: "您可以使用安全殼層 (SSH) 存取 HDInsight。 本文件提供從 Windows、 Linux、 Unix 或 macOS 用戶端連線使用 hello ssh tooHDInsight 與 scp 命令的資訊。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "linux 中的 hadoop 命令,hadoop linux 命令,hadoop macos,ssh hadoop,ssh hadoop 叢集"
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a><span data-ttu-id="b66a2-105">連接 tooHDInsight (Hadoop) 使用 SSH</span><span class="sxs-lookup"><span data-stu-id="b66a2-105">Connect tooHDInsight (Hadoop) using SSH</span></span>

<span data-ttu-id="b66a2-106">深入了解如何 toouse[安全殼層 (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely 連接 tooHadoop Azure HDInsight 上的。</span><span class="sxs-lookup"><span data-stu-id="b66a2-106">Learn how toouse [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely connect tooHadoop on Azure HDInsight.</span></span> 

<span data-ttu-id="b66a2-107">HDInsight 可用於 Linux (Ubuntu) 做為 hello 作業系統 hello Hadoop 叢集內的節點。</span><span class="sxs-lookup"><span data-stu-id="b66a2-107">HDInsight can use Linux (Ubuntu) as hello operating system for nodes within hello Hadoop cluster.</span></span> <span data-ttu-id="b66a2-108">hello 下表包含連接 tooLinux 為基礎的 HDInsight 的 SSH 用戶端時所需的 hello 位址和連接埠資訊：</span><span class="sxs-lookup"><span data-stu-id="b66a2-108">hello following table contains hello address and port information needed when connecting tooLinux-based HDInsight using an SSH client:</span></span>

| <span data-ttu-id="b66a2-109">位址</span><span class="sxs-lookup"><span data-stu-id="b66a2-109">Address</span></span> | <span data-ttu-id="b66a2-110">連接埠</span><span class="sxs-lookup"><span data-stu-id="b66a2-110">Port</span></span> | <span data-ttu-id="b66a2-111">連線到...</span><span class="sxs-lookup"><span data-stu-id="b66a2-111">Connects to...</span></span> |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | <span data-ttu-id="b66a2-112">22</span><span class="sxs-lookup"><span data-stu-id="b66a2-112">22</span></span> | <span data-ttu-id="b66a2-113">邊緣節點 (R Server on HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b66a2-113">Edge node (R Server on HDInsight)</span></span> |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="b66a2-114">22</span><span class="sxs-lookup"><span data-stu-id="b66a2-114">22</span></span> | <span data-ttu-id="b66a2-115">邊緣節點 (任何其他叢集類型，如果邊緣節點存在的話)</span><span class="sxs-lookup"><span data-stu-id="b66a2-115">Edge node (any other cluster type, if an edge node exists)</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="b66a2-116">22</span><span class="sxs-lookup"><span data-stu-id="b66a2-116">22</span></span> | <span data-ttu-id="b66a2-117">主要前端節點</span><span class="sxs-lookup"><span data-stu-id="b66a2-117">Primary headnode</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="b66a2-118">23</span><span class="sxs-lookup"><span data-stu-id="b66a2-118">23</span></span> | <span data-ttu-id="b66a2-119">次要前端節點</span><span class="sxs-lookup"><span data-stu-id="b66a2-119">Secondary headnode</span></span> |

> [!NOTE]
> <span data-ttu-id="b66a2-120">取代`<edgenodename>`hello hello 邊緣節點名稱。</span><span class="sxs-lookup"><span data-stu-id="b66a2-120">Replace `<edgenodename>` with hello name of hello edge node.</span></span>
>
> <span data-ttu-id="b66a2-121">取代`<clustername>`與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="b66a2-121">Replace `<clustername>` with hello name of your cluster.</span></span>
>
> <span data-ttu-id="b66a2-122">如果您的叢集包含邊緣節點，我們建議您__永遠連線 toohello 邊緣節點__使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="b66a2-122">If your cluster contains an edge node, we recommend that you __always connect toohello edge node__ using SSH.</span></span> <span data-ttu-id="b66a2-123">hello 前端節點裝載的 Hadoop 的重要 toohello 健全狀況服務。</span><span class="sxs-lookup"><span data-stu-id="b66a2-123">hello head nodes host services that are critical toohello health of Hadoop.</span></span> <span data-ttu-id="b66a2-124">hello 邊緣節點執行只什麼您暫停它。</span><span class="sxs-lookup"><span data-stu-id="b66a2-124">hello edge node runs only what you put on it.</span></span>
>
> <span data-ttu-id="b66a2-125">如需使用邊緣節點的詳細資訊，請參閱[在 HDInsight 中使用邊緣節點](hdinsight-apps-use-edge-node.md#access-an-edge-node)。</span><span class="sxs-lookup"><span data-stu-id="b66a2-125">For more information on using edge nodes, see [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).</span></span>

## <a name="ssh-clients"></a><span data-ttu-id="b66a2-126">SSH 用戶端</span><span class="sxs-lookup"><span data-stu-id="b66a2-126">SSH clients</span></span>

<span data-ttu-id="b66a2-127">Linux、 Unix 及 macOS 系統提供 hello`ssh`和`scp`命令。</span><span class="sxs-lookup"><span data-stu-id="b66a2-127">Linux, Unix, and macOS systems provide hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="b66a2-128">hello`ssh`用戶端是常用的 toocreate 與 Linux 或 unix 系統的遠端命令列工作階段。</span><span class="sxs-lookup"><span data-stu-id="b66a2-128">hello `ssh` client is commonly used toocreate a remote command-line session with a Linux or Unix-based system.</span></span> <span data-ttu-id="b66a2-129">hello`scp`用戶端是用戶端與 hello 遠端系統之間使用的 toosecurely 複製檔案。</span><span class="sxs-lookup"><span data-stu-id="b66a2-129">hello `scp` client is used toosecurely copy files between your client and hello remote system.</span></span>

<span data-ttu-id="b66a2-130">Microsoft Windows 預設不會提供任何 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b66a2-130">Microsoft Windows does not provide any SSH clients by default.</span></span> <span data-ttu-id="b66a2-131">hello`ssh`和`scp`用戶端會經由 windows hello 下列封裝：</span><span class="sxs-lookup"><span data-stu-id="b66a2-131">hello `ssh` and `scp` clients are available for Windows through hello following packages:</span></span>

* <span data-ttu-id="b66a2-132">[Azure 雲端殼層](../cloud-shell/quickstart.md): hello 雲端殼層提供 Bash 環境，在瀏覽器，並提供 hello `ssh`， `scp`，和其他常見的 Linux 命令。</span><span class="sxs-lookup"><span data-stu-id="b66a2-132">[Azure Cloud Shell](../cloud-shell/quickstart.md): hello Cloud Shell provides a Bash environment in your browser, and provides hello `ssh`, `scp`, and other common Linux commands.</span></span>

* <span data-ttu-id="b66a2-133">[在 Windows 10 上的 Ubuntu 上撞](https://msdn.microsoft.com/commandline/wsl/about): hello`ssh`和`scp`命令都是透過在 Windows 命令列上的 hello Bash。</span><span class="sxs-lookup"><span data-stu-id="b66a2-133">[Bash on Ubuntu on Windows 10](https://msdn.microsoft.com/commandline/wsl/about): hello `ssh` and `scp` commands are available through hello Bash on Windows command line.</span></span>

* <span data-ttu-id="b66a2-134">[Git (https://git-scm.com/)](https://git-scm.com/): hello`ssh`和`scp`命令都是透過 hello GitBash 命令列。</span><span class="sxs-lookup"><span data-stu-id="b66a2-134">[Git (https://git-scm.com/)](https://git-scm.com/): hello `ssh` and `scp` commands are available through hello GitBash command line.</span></span>

* <span data-ttu-id="b66a2-135">[GitHub 桌面 (https://desktop.github.com/)](https://desktop.github.com/) hello`ssh`和`scp`命令都是透過 hello GitHub 命令介面命令列。</span><span class="sxs-lookup"><span data-stu-id="b66a2-135">[GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` and `scp` commands are available through hello GitHub Shell command line.</span></span> <span data-ttu-id="b66a2-136">GitHub 桌面可以為 hello hello Git 殼層命令列設定的 toouse Bash，hello Windows 命令提示字元或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b66a2-136">GitHub Desktop can be configured toouse Bash, hello Windows Command Prompt, or PowerShell as hello command line for hello Git Shell.</span></span>

* <span data-ttu-id="b66a2-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello PowerShell 小組移植 OpenSSH tooWindows，並提供測試版本。</span><span class="sxs-lookup"><span data-stu-id="b66a2-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello PowerShell team is porting OpenSSH tooWindows, and provides test releases.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b66a2-138">hello OpenSSH 封裝包括 hello SSH 伺服器元件， `sshd`。</span><span class="sxs-lookup"><span data-stu-id="b66a2-138">hello OpenSSH package includes hello SSH server component, `sshd`.</span></span> <span data-ttu-id="b66a2-139">此元件啟動 SSH 伺服器上您的系統，讓其他人 tooconnect tooit。</span><span class="sxs-lookup"><span data-stu-id="b66a2-139">This component starts an SSH server on your system, allowing others tooconnect tooit.</span></span> <span data-ttu-id="b66a2-140">請勿設定此元件，或開啟通訊埠 22，除非您想 toohost SSH 伺服器系統上。</span><span class="sxs-lookup"><span data-stu-id="b66a2-140">Do not configure this component or open port 22 unless you want toohost an SSH server on your system.</span></span> <span data-ttu-id="b66a2-141">不需要與 HDInsight toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="b66a2-141">It is not required toocommunicate with HDInsight.</span></span>

<span data-ttu-id="b66a2-142">另外還有數個圖形化 SSH 用戶端，例如 [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) 和 [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/)。</span><span class="sxs-lookup"><span data-stu-id="b66a2-142">There are also several graphical SSH clients, such as [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) and [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/).</span></span> <span data-ttu-id="b66a2-143">雖然這些用戶端可以使用的 tooconnect tooHDInsight，連接的 hello 程序是不同於使用 hello`ssh`公用程式。</span><span class="sxs-lookup"><span data-stu-id="b66a2-143">While these clients can be used tooconnect tooHDInsight, hello process of connecting is different than using hello `ssh` utility.</span></span> <span data-ttu-id="b66a2-144">如需詳細資訊，請參閱 hello 文件的 hello 您所使用的圖形化用戶端。</span><span class="sxs-lookup"><span data-stu-id="b66a2-144">For more information, see hello documentation of hello graphical client you are using.</span></span>

## <span data-ttu-id="b66a2-145"><a id="sshkey"></a>驗證︰SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="b66a2-145"><a id="sshkey"></a>Authentication: SSH Keys</span></span>

<span data-ttu-id="b66a2-146">SSH 金鑰會使用[公開金鑰密碼編譯](https://en.wikipedia.org/wiki/Public-key_cryptography)tooauthenticate SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="b66a2-146">SSH keys use [Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate SSH sessions.</span></span> <span data-ttu-id="b66a2-147">SSH 金鑰的密碼，比更安全，並提供輕鬆 toosecure 存取 tooyour Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="b66a2-147">SSH keys are more secure than passwords, and provide an easy way toosecure access tooyour Hadoop cluster.</span></span>

<span data-ttu-id="b66a2-148">SSH 帳戶受到保護使用索引鍵，如果 hello 用戶端必須提供符合私用的索引鍵，當您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="b66a2-148">If your SSH account is secured using a key, hello client must provide hello matching private key when you connect:</span></span>

* <span data-ttu-id="b66a2-149">大部分的用戶端可以設定的 toouse__預設金鑰__。</span><span class="sxs-lookup"><span data-stu-id="b66a2-149">Most clients can be configured toouse a __default key__.</span></span> <span data-ttu-id="b66a2-150">例如，hello`ssh`私密金鑰在用戶端會尋找`~/.ssh/id_rsa`在 Linux 和 Unix 環境。</span><span class="sxs-lookup"><span data-stu-id="b66a2-150">For example, hello `ssh` client looks for a private key at `~/.ssh/id_rsa` on Linux and Unix environments.</span></span>

* <span data-ttu-id="b66a2-151">您可以指定 hello__路徑 tooa 私密金鑰__。</span><span class="sxs-lookup"><span data-stu-id="b66a2-151">You can specify hello __path tooa private key__.</span></span> <span data-ttu-id="b66a2-152">以 hello`ssh`用戶端、 hello`-i`參數是使用的 toospecify hello 路徑 tooprivate 機碼。</span><span class="sxs-lookup"><span data-stu-id="b66a2-152">With hello `ssh` client, hello `-i` parameter is used toospecify hello path tooprivate key.</span></span> <span data-ttu-id="b66a2-153">例如： `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`。</span><span class="sxs-lookup"><span data-stu-id="b66a2-153">For example, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span></span>

* <span data-ttu-id="b66a2-154">如果您有__多個私密金鑰__可搭配不同的伺服器使用，請考慮使用 [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent) 之類的公用程式。</span><span class="sxs-lookup"><span data-stu-id="b66a2-154">If you have __multiple private keys__ for use with different servers, consider using a utility such as [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent).</span></span> <span data-ttu-id="b66a2-155">hello`ssh-agent`公用程式時，才能使用的 tooautomatically 選取 hello 金鑰 toouse 建立的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="b66a2-155">hello `ssh-agent` utility can be used tooautomatically select hello key toouse when establishing an SSH session.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="b66a2-156">如果您保護您的複雜密碼的私密金鑰，您必須在使用 hello 金鑰時，輸入 hello 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="b66a2-156">If you secure your private key with a passphrase, you must enter hello passphrase when using hello key.</span></span> <span data-ttu-id="b66a2-157">公用程式，例如`ssh-agent`可以快取 hello，方便您使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="b66a2-157">Utilities such as `ssh-agent` can cache hello password for your convenience.</span></span>

### <a name="create-an-ssh-key-pair"></a><span data-ttu-id="b66a2-158">建立 SSH 金鑰組</span><span class="sxs-lookup"><span data-stu-id="b66a2-158">Create an SSH key pair</span></span>

<span data-ttu-id="b66a2-159">使用 hello`ssh-keygen`命令 toocreate 公用和私用金鑰檔。</span><span class="sxs-lookup"><span data-stu-id="b66a2-159">Use hello `ssh-keygen` command toocreate public and private key files.</span></span> <span data-ttu-id="b66a2-160">hello 下列命令會產生 2048年位元 RSA 金鑰組，可以搭配 HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b66a2-160">hello following command generates a 2048-bit RSA key pair that can be used with HDInsight:</span></span>

    ssh-keygen -t rsa -b 2048

<span data-ttu-id="b66a2-161">會提示您輸入 hello 金鑰的建立程序期間的資訊。</span><span class="sxs-lookup"><span data-stu-id="b66a2-161">You are prompted for information during hello key creation process.</span></span> <span data-ttu-id="b66a2-162">例如，其中 hello 金鑰會儲存或是否 toouse 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="b66a2-162">For example, where hello keys are stored or whether toouse a passphrase.</span></span> <span data-ttu-id="b66a2-163">Hello 程序完成之後，會建立兩個檔案。公開金鑰和私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="b66a2-163">After hello process completes, two files are created; a public key and a private key.</span></span>

* <span data-ttu-id="b66a2-164">hello__公開金鑰__是使用的 toocreate HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b66a2-164">hello __public key__ is used toocreate an HDInsight cluster.</span></span> <span data-ttu-id="b66a2-165">hello 公開金鑰副檔名為`.pub`。</span><span class="sxs-lookup"><span data-stu-id="b66a2-165">hello public key has an extension of `.pub`.</span></span>

* <span data-ttu-id="b66a2-166">hello__私密金鑰__是使用的 tooauthenticate 用戶端 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b66a2-166">hello __private key__ is used tooauthenticate your client toohello HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b66a2-167">您可以使用複雜密碼來保護金鑰。</span><span class="sxs-lookup"><span data-stu-id="b66a2-167">You can secure your keys using a passphrase.</span></span> <span data-ttu-id="b66a2-168">複雜密碼實際上就是私密金鑰的密碼。</span><span class="sxs-lookup"><span data-stu-id="b66a2-168">A passphrase is effectively a password on your private key.</span></span> <span data-ttu-id="b66a2-169">即使其他人取得您的私密金鑰，它們必須擁有 hello 複雜密碼 toouse hello 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b66a2-169">Even if someone obtains your private key, they must have hello passphrase toouse hello key.</span></span>

### <a name="create-hdinsight-using-hello-public-key"></a><span data-ttu-id="b66a2-170">建立 HDInsight 使用 hello 公開金鑰</span><span class="sxs-lookup"><span data-stu-id="b66a2-170">Create HDInsight using hello public key</span></span>

| <span data-ttu-id="b66a2-171">建立方法</span><span class="sxs-lookup"><span data-stu-id="b66a2-171">Creation method</span></span> | <span data-ttu-id="b66a2-172">如何 toouse hello 公開金鑰</span><span class="sxs-lookup"><span data-stu-id="b66a2-172">How toouse hello public key</span></span> |
| ------- | ------- |
| <span data-ttu-id="b66a2-173">**Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="b66a2-173">**Azure portal**</span></span> | <span data-ttu-id="b66a2-174">取消核取__使用與叢集登入相同的密碼__，然後選取__公開金鑰__為 hello SSH 驗證類型。</span><span class="sxs-lookup"><span data-stu-id="b66a2-174">Uncheck __Use same password as cluster login__, and then select __Public Key__ as hello SSH authentication type.</span></span> <span data-ttu-id="b66a2-175">最後，選取 hello 公開金鑰檔案或 hello 檔案 hello 文字內容貼在 hello __SSH 公開金鑰__欄位。</span><span class="sxs-lookup"><span data-stu-id="b66a2-175">Finally, select hello public key file or paste hello text contents of hello file in hello __SSH public key__ field.</span></span></br><span data-ttu-id="b66a2-176">![建立 HDInsight 叢集時的 [SSH 公開金鑰] 對話方塊](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span><span class="sxs-lookup"><span data-stu-id="b66a2-176">![SSH public key dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span></span> |
| <span data-ttu-id="b66a2-177">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b66a2-177">**Azure PowerShell**</span></span> | <span data-ttu-id="b66a2-178">使用 hello `-SshPublicKey` hello 參數`New-AzureRmHdinsightCluster`hello 公開金鑰，做為字串的 cmdlet 並傳遞 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="b66a2-178">Use hello `-SshPublicKey` parameter of hello `New-AzureRmHdinsightCluster` cmdlet and pass hello contents of hello public key as a string.</span></span>|
| <span data-ttu-id="b66a2-179">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="b66a2-179">**Azure CLI 1.0**</span></span> | <span data-ttu-id="b66a2-180">使用 hello `--sshPublicKey` hello 參數`azure hdinsight cluster create`命令，並以字串形式傳遞的 hello 公開金鑰的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="b66a2-180">Use hello `--sshPublicKey` parameter of hello `azure hdinsight cluster create` command and pass hello contents of hello public key as a string.</span></span> |
| <span data-ttu-id="b66a2-181">**Resource Manager 範本**</span><span class="sxs-lookup"><span data-stu-id="b66a2-181">**Resource Manager Template**</span></span> | <span data-ttu-id="b66a2-182">如需對範本使用 SSH 金鑰的範例，請參閱[使用 SSH 金鑰在 Linux 上部署 HDInsight](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/)。</span><span class="sxs-lookup"><span data-stu-id="b66a2-182">For an example of using SSH keys with a template, see [Deploy HDInsight on Linux with SSH key](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/).</span></span> <span data-ttu-id="b66a2-183">hello `publicKeys` hello 中的項目[azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json)檔案時，才能使用的 toopass hello 金鑰 tooAzure 建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b66a2-183">hello `publicKeys` element in hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) file is used toopass hello keys tooAzure when creating hello cluster.</span></span> |

## <span data-ttu-id="b66a2-184"><a id="sshpassword"></a>驗證︰密碼</span><span class="sxs-lookup"><span data-stu-id="b66a2-184"><a id="sshpassword"></a>Authentication: Password</span></span>

<span data-ttu-id="b66a2-185">您可以使用密碼來保護 SSH 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b66a2-185">SSH accounts can be secured using a password.</span></span> <span data-ttu-id="b66a2-186">當您連接使用 SSH tooHDInsight 時，您都會有提示的 tooenter hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="b66a2-186">When you connect tooHDInsight using SSH, you are prompted tooenter hello password.</span></span>

> [!WARNING]
> <span data-ttu-id="b66a2-187">我們不建議您對 SSH 使用密碼驗證。</span><span class="sxs-lookup"><span data-stu-id="b66a2-187">We do not recommend using password authentication for SSH.</span></span> <span data-ttu-id="b66a2-188">密碼可以猜到，而且是 toobrute 容易遭受攻擊。</span><span class="sxs-lookup"><span data-stu-id="b66a2-188">Passwords can be guessed and are vulnerable toobrute force attacks.</span></span> <span data-ttu-id="b66a2-189">相反地，我們會建議您使用 [SSH 金鑰來進行驗證](#sshkey)。</span><span class="sxs-lookup"><span data-stu-id="b66a2-189">Instead, we recommend that you use [SSH keys for authentication](#sshkey).</span></span>

### <a name="create-hdinsight-using-a-password"></a><span data-ttu-id="b66a2-190">使用密碼建立 HDInsight</span><span class="sxs-lookup"><span data-stu-id="b66a2-190">Create HDInsight using a password</span></span>

| <span data-ttu-id="b66a2-191">建立方法</span><span class="sxs-lookup"><span data-stu-id="b66a2-191">Creation method</span></span> | <span data-ttu-id="b66a2-192">如何 toospecify hello 密碼</span><span class="sxs-lookup"><span data-stu-id="b66a2-192">How toospecify hello password</span></span> |
| --------------- | ---------------- |
| <span data-ttu-id="b66a2-193">**Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="b66a2-193">**Azure portal**</span></span> | <span data-ttu-id="b66a2-194">根據預設，hello SSH 使用者帳戶具有 hello hello 叢集登入帳戶為相同的密碼。</span><span class="sxs-lookup"><span data-stu-id="b66a2-194">By default, hello SSH user account has hello same password as hello cluster login account.</span></span> <span data-ttu-id="b66a2-195">toouse 不同的密碼，取消核取__使用與叢集登入相同的密碼__，然後輸入 hello 密碼在 hello __SSH 密碼__欄位。</span><span class="sxs-lookup"><span data-stu-id="b66a2-195">toouse a different password, uncheck __Use same password as cluster login__, and then enter hello password in hello __SSH password__ field.</span></span></br><span data-ttu-id="b66a2-196">![建立 HDInsight 叢集時的 [SSH 密碼] 對話方塊](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span><span class="sxs-lookup"><span data-stu-id="b66a2-196">![SSH password dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span></span>|
| <span data-ttu-id="b66a2-197">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b66a2-197">**Azure PowerShell**</span></span> | <span data-ttu-id="b66a2-198">使用 hello `--SshCredential` hello 參數`New-AzureRmHdinsightCluster`cmdlet 並傳遞`PSCredential`物件，其中包含 hello SSH 使用者帳戶名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b66a2-198">Use hello `--SshCredential` parameter of hello `New-AzureRmHdinsightCluster` cmdlet and pass a `PSCredential` object that contains hello SSH user account name and password.</span></span> |
| <span data-ttu-id="b66a2-199">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="b66a2-199">**Azure CLI 1.0**</span></span> | <span data-ttu-id="b66a2-200">使用 hello `--sshPassword` hello 參數`azure hdinsight cluster create`命令，並提供 hello 密碼值。</span><span class="sxs-lookup"><span data-stu-id="b66a2-200">Use hello `--sshPassword` parameter of hello `azure hdinsight cluster create` command and provide hello password value.</span></span> |
| <span data-ttu-id="b66a2-201">**Resource Manager 範本**</span><span class="sxs-lookup"><span data-stu-id="b66a2-201">**Resource Manager Template**</span></span> | <span data-ttu-id="b66a2-202">如需對範本使用密碼的範例，請參閱[使用 SSH 密碼在 Linux 上部署 HDInsight](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/)。</span><span class="sxs-lookup"><span data-stu-id="b66a2-202">For an example of using a password with a template, see [Deploy HDInsight on Linux with SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span></span> <span data-ttu-id="b66a2-203">hello `linuxOperatingSystemProfile` hello 中的項目[azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json)檔案時，才能使用的 toopass hello SSH 帳戶名稱和密碼 tooAzure 建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b66a2-203">hello `linuxOperatingSystemProfile` element in hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) file is used toopass hello SSH account name and password tooAzure when creating hello cluster.</span></span>|

### <a name="change-hello-ssh-password"></a><span data-ttu-id="b66a2-204">變更 hello SSH 密碼</span><span class="sxs-lookup"><span data-stu-id="b66a2-204">Change hello SSH password</span></span>

<span data-ttu-id="b66a2-205">如需變更 hello SSH 使用者帳戶密碼的資訊，請參閱 hello__變更密碼__區段 hello[管理 HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords)文件。</span><span class="sxs-lookup"><span data-stu-id="b66a2-205">For information on changing hello SSH user account password, see hello __Change passwords__ section of hello [Manage HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) document.</span></span>

## <span data-ttu-id="b66a2-206"><a id="domainjoined"></a>驗證︰已加入網域的 HDInsight</span><span class="sxs-lookup"><span data-stu-id="b66a2-206"><a id="domainjoined"></a>Authentication: Domain-joined HDInsight</span></span>

<span data-ttu-id="b66a2-207">如果您使用__已加入網域的 HDInsight 叢集__，您必須使用 hello`kinit`透過 SSH 連線後命令。</span><span class="sxs-lookup"><span data-stu-id="b66a2-207">If you are using a __domain-joined HDInsight cluster__, you must use hello `kinit` command after connecting with SSH.</span></span> <span data-ttu-id="b66a2-208">此命令會提示您輸入網域使用者和密碼，並驗證您的工作階段與 hello 與 hello 叢集相關聯的 Azure Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="b66a2-208">This command prompts you for a domain user and password, and authenticates your session with hello Azure Active Directory domain associated with hello cluster.</span></span>

<span data-ttu-id="b66a2-209">如需詳細資訊，請參閱[設定已加入網域的 HDInsight](hdinsight-domain-joined-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="b66a2-209">For more information, see [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md).</span></span>

## <a name="connect-toonodes"></a><span data-ttu-id="b66a2-210">連接 toonodes</span><span class="sxs-lookup"><span data-stu-id="b66a2-210">Connect toonodes</span></span>

<span data-ttu-id="b66a2-211">hello 前端節點與邊緣節點 （如果有的話） 是否可透過 hello 存取網際網路的連接埠 22 和 23。</span><span class="sxs-lookup"><span data-stu-id="b66a2-211">hello head nodes and edge node (if there is one) can be accessed over hello internet on ports 22 and 23.</span></span>

* <span data-ttu-id="b66a2-212">當連接 toohello__前端節點__，使用連接埠__22__ tooconnect toohello 主要前端節點和連接埠__23__ tooconnect toohello 次要前端節點。</span><span class="sxs-lookup"><span data-stu-id="b66a2-212">When connecting toohello __head nodes__, use port __22__ tooconnect toohello primary head node and port __23__ tooconnect toohello secondary head node.</span></span> <span data-ttu-id="b66a2-213">hello 完整的網域名稱 toouse 是`clustername-ssh.azurehdinsight.net`，其中`clustername`是 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="b66a2-213">hello fully qualified domain name toouse is `clustername-ssh.azurehdinsight.net`, where `clustername` is hello name of your cluster.</span></span>

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* <span data-ttu-id="b66a2-214">當 connectiung toohello__邊緣節點__，使用通訊埠 22。</span><span class="sxs-lookup"><span data-stu-id="b66a2-214">When connectiung toohello __edge node__, use port 22.</span></span> <span data-ttu-id="b66a2-215">hello 完整的網域名稱是`edgenodename.clustername-ssh.azurehdinsight.net`，其中`edgenodename`時提供的名稱建立 hello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="b66a2-215">hello fully qualified domain name is `edgenodename.clustername-ssh.azurehdinsight.net`, where `edgenodename` is a name you provided when creating hello edge node.</span></span> <span data-ttu-id="b66a2-216">`clustername`這是 hello hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="b66a2-216">`clustername` is hello name of hello cluster.</span></span>

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> <span data-ttu-id="b66a2-217">hello 前一個範例假設您使用密碼驗證，或該憑證驗證會自動發生。</span><span class="sxs-lookup"><span data-stu-id="b66a2-217">hello previous examples assume that you are using password authentication, or that certificate authentication is occuring automatically.</span></span> <span data-ttu-id="b66a2-218">如果您使用 SSH 金鑰組進行驗證，不會自動使用 hello 憑證，請使用 hello`-i`參數 toospecify hello 私用金鑰。</span><span class="sxs-lookup"><span data-stu-id="b66a2-218">If you use an SSH key-pair for authentication, and hello certificate is not used automatically, use hello `-i` parameter toospecify hello private key.</span></span> <span data-ttu-id="b66a2-219">例如： `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`。</span><span class="sxs-lookup"><span data-stu-id="b66a2-219">For example, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span></span>

<span data-ttu-id="b66a2-220">一旦連接之後，hello 提示字元會變成 tooindicate hello SSH 使用者名稱和 hello 節點連線到。</span><span class="sxs-lookup"><span data-stu-id="b66a2-220">Once connected, hello prompt changes tooindicate hello SSH user name and hello node you are connected to.</span></span> <span data-ttu-id="b66a2-221">例如，當連線 toohello 主要標頭的節點做為`sshuser`，hello 提示是`sshuser@hn0-clustername:~$`。</span><span class="sxs-lookup"><span data-stu-id="b66a2-221">For example, when connected toohello primary head node as `sshuser`, hello prompt is `sshuser@hn0-clustername:~$`.</span></span>

### <a name="connect-tooworker-and-zookeeper-nodes"></a><span data-ttu-id="b66a2-222">連接 tooworker 和動物園管理員節點</span><span class="sxs-lookup"><span data-stu-id="b66a2-222">Connect tooworker and Zookeeper nodes</span></span>

<span data-ttu-id="b66a2-223">hello 背景工作節點和節點不是直接存取從動物園管理員 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="b66a2-223">hello worker nodes and Zookeeper nodes are not directly accessible from hello internet.</span></span> <span data-ttu-id="b66a2-224">Hello 叢集前端節點或邊緣節點，可以存取它們。</span><span class="sxs-lookup"><span data-stu-id="b66a2-224">They can be accessed from hello cluster head nodes or edge nodes.</span></span> <span data-ttu-id="b66a2-225">hello 下面是 hello 的一般步驟 tooconnect tooother 節點：</span><span class="sxs-lookup"><span data-stu-id="b66a2-225">hello following are hello general steps tooconnect tooother nodes:</span></span>

1. <span data-ttu-id="b66a2-226">使用 SSH tooconnect tooa head 或邊緣節點：</span><span class="sxs-lookup"><span data-stu-id="b66a2-226">Use SSH tooconnect tooa head or edge node:</span></span>

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. <span data-ttu-id="b66a2-227">從 hello SSH 連線 toohello head 或邊緣節點，使用 hello`ssh`命令 tooconnect tooa hello 叢集中的背景工作節點：</span><span class="sxs-lookup"><span data-stu-id="b66a2-227">From hello SSH connection toohello head or edge node, use hello `ssh` command tooconnect tooa worker node in hello cluster:</span></span>

        ssh sshuser@wn0-myhdi

    <span data-ttu-id="b66a2-228">tooretrieve hello 叢集中的節點 hello，hello 網域名稱的清單，請參閱 「 hello[管理 HDInsight 使用 hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes)文件。</span><span class="sxs-lookup"><span data-stu-id="b66a2-228">tooretrieve a list of hello domain names of hello nodes in hello cluster, see hello [Manage HDInsight by using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) document.</span></span>

<span data-ttu-id="b66a2-229">如果使用保護 hello SSH 帳戶__密碼__，連接時，請輸入 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="b66a2-229">If hello SSH account is secured using a __password__, enter hello password when connecting.</span></span>

<span data-ttu-id="b66a2-230">如果使用保護 hello SSH 帳戶__SSH 金鑰__，請確定 SSH 轉送已啟用 hello 用戶端上。</span><span class="sxs-lookup"><span data-stu-id="b66a2-230">If hello SSH account is secured using __SSH keys__, make sure that SSH forwarding is enabled on hello client.</span></span>

> [!NOTE]
> <span data-ttu-id="b66a2-231">Toodirectly 存取 hello 叢集中所有節點的另一個方法是 tooinstall HDInsight，在 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b66a2-231">Another way toodirectly access all nodes in hello cluster is tooinstall HDInsight into an Azure Virtual Network.</span></span> <span data-ttu-id="b66a2-232">然後，您可以在其中加入遠端機器 toohello 相同虛擬網路，並直接存取 hello 叢集中所有節點。</span><span class="sxs-lookup"><span data-stu-id="b66a2-232">Then, you can join your remote machine toohello same virtual network and directly access all nodes in hello cluster.</span></span>
>
> <span data-ttu-id="b66a2-233">如需詳細資訊，請參閱[搭配 HDInsight 使用虛擬網路](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="b66a2-233">For more information, see [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md).</span></span>

### <a name="configure-ssh-agent-forwarding"></a><span data-ttu-id="b66a2-234">設定 SSH 代理程式轉送</span><span class="sxs-lookup"><span data-stu-id="b66a2-234">Configure SSH agent forwarding</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b66a2-235">hello 下列步驟假設 Linux 或 UNIX 為基礎的系統，並使用 Windows 10 上 Bash。</span><span class="sxs-lookup"><span data-stu-id="b66a2-235">hello following steps assume a Linux or UNIX-based system, and work with Bash on Windows 10.</span></span> <span data-ttu-id="b66a2-236">如果這些步驟不適用於您的系統，您可能需要 tooconsult hello 文件 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b66a2-236">If these steps do not work for your system, you may need tooconsult hello documentation for your SSH client.</span></span>

1. <span data-ttu-id="b66a2-237">使用文字編輯器開啟 `~/.ssh/config`。</span><span class="sxs-lookup"><span data-stu-id="b66a2-237">Using a text editor, open `~/.ssh/config`.</span></span> <span data-ttu-id="b66a2-238">如果該檔案不存在，您可以藉由在命令列中輸入 `touch ~/.ssh/config` 加以建立。</span><span class="sxs-lookup"><span data-stu-id="b66a2-238">If this file doesn't exist, you can create it by entering `touch ~/.ssh/config` at a command line.</span></span>

2. <span data-ttu-id="b66a2-239">加入下列文字 toohello hello`config`檔案。</span><span class="sxs-lookup"><span data-stu-id="b66a2-239">Add hello following text toohello `config` file.</span></span>

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    <span data-ttu-id="b66a2-240">取代 hello__主機__資訊 hello hello 節點位址與連接 toousing SSH。</span><span class="sxs-lookup"><span data-stu-id="b66a2-240">Replace hello __Host__ information with hello address of hello node you connect toousing SSH.</span></span> <span data-ttu-id="b66a2-241">hello 前一個範例會使用 hello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="b66a2-241">hello previous example uses hello edge node.</span></span> <span data-ttu-id="b66a2-242">此項目會設定轉送 hello 指定節點的 SSH 代理程式。</span><span class="sxs-lookup"><span data-stu-id="b66a2-242">This entry configures SSH agent forwarding for hello specified node.</span></span>

3. <span data-ttu-id="b66a2-243">測試 SSH 代理程式轉寄使用 hello hello 終端機中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="b66a2-243">Test SSH agent forwarding by using hello following command from hello terminal:</span></span>

        echo "$SSH_AUTH_SOCK"

    <span data-ttu-id="b66a2-244">此命令會傳回資訊的類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="b66a2-244">This command returns information similar toohello following text:</span></span>

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    <span data-ttu-id="b66a2-245">如果未傳回任何資訊，表示 `ssh-agent` 未執行。</span><span class="sxs-lookup"><span data-stu-id="b66a2-245">If nothing is returned, then `ssh-agent` is not running.</span></span> <span data-ttu-id="b66a2-246">如需詳細資訊，請參閱 < 在 hello 代理程式啟動指令碼資訊[使用 ssh 代理程式與 ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) ，或連絡您的 SSH 用戶端文件。</span><span class="sxs-lookup"><span data-stu-id="b66a2-246">For more information, see hello agent startup scripts information at [Using ssh-agent with ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) or consult your SSH client documentation.</span></span>

4. <span data-ttu-id="b66a2-247">一旦確認**ssh 代理**正在執行，使用 hello 遵循 tooadd SSH 私用金鑰 toohello 代理程式：</span><span class="sxs-lookup"><span data-stu-id="b66a2-247">Once you have verified that **ssh-agent** is running, use hello following tooadd your SSH private key toohello agent:</span></span>

        ssh-add ~/.ssh/id_rsa

    <span data-ttu-id="b66a2-248">如果您的私密金鑰會儲存在不同的檔案，取代`~/.ssh/id_rsa`與 hello 路徑 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="b66a2-248">If your private key is stored in a different file, replace `~/.ssh/id_rsa` with hello path toohello file.</span></span>

5. <span data-ttu-id="b66a2-249">Toohello 叢集邊緣節點或前端節點使用 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="b66a2-249">Connect toohello cluster edge node or head nodes using SSH.</span></span> <span data-ttu-id="b66a2-250">接著使用 hello SSH 命令 tooconnect tooa 背景工作或動物園管理員節點。</span><span class="sxs-lookup"><span data-stu-id="b66a2-250">Then use hello SSH command tooconnect tooa worker or zookeeper node.</span></span> <span data-ttu-id="b66a2-251">使用轉送 hello 索引鍵來建立 hello 連接。</span><span class="sxs-lookup"><span data-stu-id="b66a2-251">hello connection is established using hello forwarded key.</span></span>

## <a name="copy-files"></a><span data-ttu-id="b66a2-252">複製檔案</span><span class="sxs-lookup"><span data-stu-id="b66a2-252">Copy files</span></span>

<span data-ttu-id="b66a2-253">hello`scp`公用程式可以使用的 toocopy 檔案 tooand 從 hello 叢集中的個別節點。</span><span class="sxs-lookup"><span data-stu-id="b66a2-253">hello `scp` utility can be used toocopy files tooand from individual nodes in hello cluster.</span></span> <span data-ttu-id="b66a2-254">例如，下列命令複製 hello 來 hello`test.txt`目錄從 hello 本機系統 toohello 主要前端節點：</span><span class="sxs-lookup"><span data-stu-id="b66a2-254">For example, hello following command copies hello `test.txt` directory from hello local system toohello primary head node:</span></span>

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

<span data-ttu-id="b66a2-255">因為未指定路徑之後 hello `:`，hello 檔案置於 hello`sshuser`主目錄。</span><span class="sxs-lookup"><span data-stu-id="b66a2-255">Since no path is specified after hello `:`, hello file is placed in hello `sshuser` home directory.</span></span>

<span data-ttu-id="b66a2-256">下列範例複製 hello hello`test.txt`檔案從 hello `sshuser` hello 主要的前端節點 toohello 本機系統上的主目錄：</span><span class="sxs-lookup"><span data-stu-id="b66a2-256">hello following example copies hello `test.txt` file from hello `sshuser` home directory on hello primary head node toohello local system:</span></span>

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> <span data-ttu-id="b66a2-257">`scp`只能存取 hello hello 叢集內的個別節點的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="b66a2-257">`scp` can only access hello file system of individual nodes within hello cluster.</span></span> <span data-ttu-id="b66a2-258">它不能使用的 tooaccess hello 叢集 hello HDFS 相容儲存體中的資料。</span><span class="sxs-lookup"><span data-stu-id="b66a2-258">It cannot be used tooaccess data in hello HDFS-compatible storage for hello cluster.</span></span>
>
> <span data-ttu-id="b66a2-259">使用`scp`何時該添 tooupload 資源從的 SSH 工作階段使用。</span><span class="sxs-lookup"><span data-stu-id="b66a2-259">Use `scp` when you need tooupload a resource for use from an SSH session.</span></span> <span data-ttu-id="b66a2-260">例如上, 傳的 Python 指令碼，然後再執行的 SSH 工作階段中的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b66a2-260">For example, upload a Python script and then run hello script from an SSH session.</span></span>
>
> <span data-ttu-id="b66a2-261">直接將資料載入 hello HDFS 相容存放裝置上的資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="b66a2-261">For information on directly loading data into hello HDFS-compatible storage, see hello following documents:</span></span>
>
> * <span data-ttu-id="b66a2-262">[使用 Azure 儲存體的 HDInsight](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="b66a2-262">[HDInsight using Azure Storage](hdinsight-hadoop-use-blob-storage.md).</span></span>
>
> * <span data-ttu-id="b66a2-263">[使用 Azure Data Lake Store 的 HDInsight](hdinsight-hadoop-use-data-lake-store.md)。</span><span class="sxs-lookup"><span data-stu-id="b66a2-263">[HDInsight using Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b66a2-264">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b66a2-264">Next steps</span></span>

* [<span data-ttu-id="b66a2-265">對 HDInsight 使用 SSH 通道</span><span class="sxs-lookup"><span data-stu-id="b66a2-265">Use SSH tunneling with HDInsight</span></span>](hdinsight-linux-ambari-ssh-tunnel.md)
* [<span data-ttu-id="b66a2-266">對 HDInsight 使用虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b66a2-266">Use a virtual network with HDInsight</span></span>](hdinsight-extend-hadoop-virtual-network.md)
* [<span data-ttu-id="b66a2-267">在 HDInsight 中使用邊緣節點</span><span class="sxs-lookup"><span data-stu-id="b66a2-267">Use edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md#access-an-edge-node)