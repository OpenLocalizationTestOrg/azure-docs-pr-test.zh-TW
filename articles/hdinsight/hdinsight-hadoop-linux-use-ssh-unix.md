---
title: "使用 SSH 搭配 Hadoop - Azure HDInsight | Microsoft Docs"
description: "您可以使用安全殼層 (SSH) 存取 HDInsight。 本文提供從 Windows、Linux、Unix 或 macOS 用戶端使用 ssh 和 scp 命令連線到 HDInsight 的資訊。"
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
ms.openlocfilehash: df0feb51469333bac42c779d860192d46f24ac62
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-hdinsight-hadoop-using-ssh"></a><span data-ttu-id="4ff64-105">使用 SSH 連線到 HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="4ff64-105">Connect to HDInsight (Hadoop) using SSH</span></span>

<span data-ttu-id="4ff64-106">了解如何使用[安全殼層 (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) 安全地連線到 Hadoop on Azure HDInsight。</span><span class="sxs-lookup"><span data-stu-id="4ff64-106">Learn how to use [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) to securely connect to Hadoop on Azure HDInsight.</span></span> 

<span data-ttu-id="4ff64-107">HDInsight 可以使用 Linux (Ubuntu) 作為 Hadoop 叢集節點的作業系統。</span><span class="sxs-lookup"><span data-stu-id="4ff64-107">HDInsight can use Linux (Ubuntu) as the operating system for nodes within the Hadoop cluster.</span></span> <span data-ttu-id="4ff64-108">下表包含使用 SSH 用戶端連線到以 Linux 為基礎的 HDInsight 時所需的位址和連接埠資訊︰</span><span class="sxs-lookup"><span data-stu-id="4ff64-108">The following table contains the address and port information needed when connecting to Linux-based HDInsight using an SSH client:</span></span>

| <span data-ttu-id="4ff64-109">位址</span><span class="sxs-lookup"><span data-stu-id="4ff64-109">Address</span></span> | <span data-ttu-id="4ff64-110">連接埠</span><span class="sxs-lookup"><span data-stu-id="4ff64-110">Port</span></span> | <span data-ttu-id="4ff64-111">連線到...</span><span class="sxs-lookup"><span data-stu-id="4ff64-111">Connects to...</span></span> |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | <span data-ttu-id="4ff64-112">22</span><span class="sxs-lookup"><span data-stu-id="4ff64-112">22</span></span> | <span data-ttu-id="4ff64-113">邊緣節點 (R Server on HDInsight)</span><span class="sxs-lookup"><span data-stu-id="4ff64-113">Edge node (R Server on HDInsight)</span></span> |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="4ff64-114">22</span><span class="sxs-lookup"><span data-stu-id="4ff64-114">22</span></span> | <span data-ttu-id="4ff64-115">邊緣節點 (任何其他叢集類型，如果邊緣節點存在的話)</span><span class="sxs-lookup"><span data-stu-id="4ff64-115">Edge node (any other cluster type, if an edge node exists)</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="4ff64-116">22</span><span class="sxs-lookup"><span data-stu-id="4ff64-116">22</span></span> | <span data-ttu-id="4ff64-117">主要前端節點</span><span class="sxs-lookup"><span data-stu-id="4ff64-117">Primary headnode</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="4ff64-118">23</span><span class="sxs-lookup"><span data-stu-id="4ff64-118">23</span></span> | <span data-ttu-id="4ff64-119">次要前端節點</span><span class="sxs-lookup"><span data-stu-id="4ff64-119">Secondary headnode</span></span> |

> [!NOTE]
> <span data-ttu-id="4ff64-120">將 `<edgenodename>` 替換為邊緣節點的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ff64-120">Replace `<edgenodename>` with the name of the edge node.</span></span>
>
> <span data-ttu-id="4ff64-121">使用您叢集的名稱取代 `<clustername>`。</span><span class="sxs-lookup"><span data-stu-id="4ff64-121">Replace `<clustername>` with the name of your cluster.</span></span>
>
> <span data-ttu-id="4ff64-122">如果您的叢集包含邊緣節點，我們建議您__一律使用 SSH 連線到邊緣節點__。</span><span class="sxs-lookup"><span data-stu-id="4ff64-122">If your cluster contains an edge node, we recommend that you __always connect to the edge node__ using SSH.</span></span> <span data-ttu-id="4ff64-123">前端節點會裝載對於 Hadoop 健康狀態至關重要的服務。</span><span class="sxs-lookup"><span data-stu-id="4ff64-123">The head nodes host services that are critical to the health of Hadoop.</span></span> <span data-ttu-id="4ff64-124">邊緣節點則只會執行您放在上面的服務。</span><span class="sxs-lookup"><span data-stu-id="4ff64-124">The edge node runs only what you put on it.</span></span>
>
> <span data-ttu-id="4ff64-125">如需使用邊緣節點的詳細資訊，請參閱[在 HDInsight 中使用邊緣節點](hdinsight-apps-use-edge-node.md#access-an-edge-node)。</span><span class="sxs-lookup"><span data-stu-id="4ff64-125">For more information on using edge nodes, see [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).</span></span>

## <a name="ssh-clients"></a><span data-ttu-id="4ff64-126">SSH 用戶端</span><span class="sxs-lookup"><span data-stu-id="4ff64-126">SSH clients</span></span>

<span data-ttu-id="4ff64-127">Linux、Unix 和 macOS 系統提供 `ssh` 和 `scp` 命令。</span><span class="sxs-lookup"><span data-stu-id="4ff64-127">Linux, Unix, and macOS systems provide the `ssh` and `scp` commands.</span></span> <span data-ttu-id="4ff64-128">`ssh` 用戶端通常用來建立以 Linux 或 Unix 為基礎之系統的遠端命令列工作階段。</span><span class="sxs-lookup"><span data-stu-id="4ff64-128">The `ssh` client is commonly used to create a remote command-line session with a Linux or Unix-based system.</span></span> <span data-ttu-id="4ff64-129">`scp` 用戶端用來安全地複製用戶端與遠端系統之間的檔案。</span><span class="sxs-lookup"><span data-stu-id="4ff64-129">The `scp` client is used to securely copy files between your client and the remote system.</span></span>

<span data-ttu-id="4ff64-130">Microsoft Windows 預設不會提供任何 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="4ff64-130">Microsoft Windows does not provide any SSH clients by default.</span></span> <span data-ttu-id="4ff64-131">`ssh` 和 `scp` 用戶端均可透過下列套件使用於 Windows︰</span><span class="sxs-lookup"><span data-stu-id="4ff64-131">The `ssh` and `scp` clients are available for Windows through the following packages:</span></span>

* <span data-ttu-id="4ff64-132">[Azure Cloud Shell](../cloud-shell/quickstart.md)：Cloud Shell 在瀏覽器中提供 Bash 環境，並提供`ssh``scp` 和其他一般 Linux 命令。</span><span class="sxs-lookup"><span data-stu-id="4ff64-132">[Azure Cloud Shell](../cloud-shell/quickstart.md): The Cloud Shell provides a Bash environment in your browser, and provides the `ssh`, `scp`, and other common Linux commands.</span></span>

* <span data-ttu-id="4ff64-133">[位於 Windows 10 之 Ubuntu 上的 Bash](https://msdn.microsoft.com/commandline/wsl/about)：`ssh` 和`scp` 命令可透過 Windows 命令列上的 Bash 來取得。</span><span class="sxs-lookup"><span data-stu-id="4ff64-133">[Bash on Ubuntu on Windows 10](https://msdn.microsoft.com/commandline/wsl/about): The `ssh` and `scp` commands are available through the Bash on Windows command line.</span></span>

* <span data-ttu-id="4ff64-134">[Git (https://git-scm.com/)](https://git-scm.com/)：`ssh` 和 `scp` 命令可透過 GitBash 命令列來取得。</span><span class="sxs-lookup"><span data-stu-id="4ff64-134">[Git (https://git-scm.com/)](https://git-scm.com/): The `ssh` and `scp` commands are available through the GitBash command line.</span></span>

* <span data-ttu-id="4ff64-135">[GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/)：`ssh` 和 `scp` 命令可透過 GitHub Shell 命令列來取得。</span><span class="sxs-lookup"><span data-stu-id="4ff64-135">[GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/) The `ssh` and `scp` commands are available through the GitHub Shell command line.</span></span> <span data-ttu-id="4ff64-136">GitHub Desktop 可設定為使用 Bash、Windows 命令提示字元或 PowerShell 來作為 Git Shell 的命令列。</span><span class="sxs-lookup"><span data-stu-id="4ff64-136">GitHub Desktop can be configured to use Bash, the Windows Command Prompt, or PowerShell as the command line for the Git Shell.</span></span>

* <span data-ttu-id="4ff64-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)：PowerShell 小組將會把 OpenSSH 移植到 Windows，並提供測試版本。</span><span class="sxs-lookup"><span data-stu-id="4ff64-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): The PowerShell team is porting OpenSSH to Windows, and provides test releases.</span></span>

    > [!WARNING]
    > <span data-ttu-id="4ff64-138">OpenSSH 套件包含 SSH 伺服器元件 `sshd`。</span><span class="sxs-lookup"><span data-stu-id="4ff64-138">The OpenSSH package includes the SSH server component, `sshd`.</span></span> <span data-ttu-id="4ff64-139">此元件會在您的系統上啟動 SSH 伺服器，讓其他人可與它連線。</span><span class="sxs-lookup"><span data-stu-id="4ff64-139">This component starts an SSH server on your system, allowing others to connect to it.</span></span> <span data-ttu-id="4ff64-140">除非您想要在系統上裝載 SSH 伺服器，否則請勿設定此元件或開啟連接埠 22。</span><span class="sxs-lookup"><span data-stu-id="4ff64-140">Do not configure this component or open port 22 unless you want to host an SSH server on your system.</span></span> <span data-ttu-id="4ff64-141">與 HDInsight 通訊並不需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="4ff64-141">It is not required to communicate with HDInsight.</span></span>

<span data-ttu-id="4ff64-142">另外還有數個圖形化 SSH 用戶端，例如 [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) 和 [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/)。</span><span class="sxs-lookup"><span data-stu-id="4ff64-142">There are also several graphical SSH clients, such as [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) and [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/).</span></span> <span data-ttu-id="4ff64-143">雖然這些用戶端可用來連線到 HDInsight，但連線的程序與使用 `ssh` 公用程式時不同。</span><span class="sxs-lookup"><span data-stu-id="4ff64-143">While these clients can be used to connect to HDInsight, the process of connecting is different than using the `ssh` utility.</span></span> <span data-ttu-id="4ff64-144">如需詳細資訊，請參閱您使用之圖形化用戶端的文件。</span><span class="sxs-lookup"><span data-stu-id="4ff64-144">For more information, see the documentation of the graphical client you are using.</span></span>

## <span data-ttu-id="4ff64-145"><a id="sshkey"></a>驗證︰SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="4ff64-145"><a id="sshkey"></a>Authentication: SSH Keys</span></span>

<span data-ttu-id="4ff64-146">SSH 金鑰會使用[公開金鑰加密](https://en.wikipedia.org/wiki/Public-key_cryptography)來驗證 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="4ff64-146">SSH keys use [Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) to authenticate SSH sessions.</span></span> <span data-ttu-id="4ff64-147">SSH 金鑰比密碼更安全，並提供簡單的方式來保護 Hadoop 叢集的存取。</span><span class="sxs-lookup"><span data-stu-id="4ff64-147">SSH keys are more secure than passwords, and provide an easy way to secure access to your Hadoop cluster.</span></span>

<span data-ttu-id="4ff64-148">如果您使用金鑰來保護 SSH 帳戶，當您連線時，用戶端必須提供對應的私密金鑰︰</span><span class="sxs-lookup"><span data-stu-id="4ff64-148">If your SSH account is secured using a key, the client must provide the matching private key when you connect:</span></span>

* <span data-ttu-id="4ff64-149">大部分用戶端均可設定為使用__預設金鑰__。</span><span class="sxs-lookup"><span data-stu-id="4ff64-149">Most clients can be configured to use a __default key__.</span></span> <span data-ttu-id="4ff64-150">例如，`ssh` 用戶端會在 Linux 和 Unix 環境的 `~/.ssh/id_rsa` 中尋找私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="4ff64-150">For example, the `ssh` client looks for a private key at `~/.ssh/id_rsa` on Linux and Unix environments.</span></span>

* <span data-ttu-id="4ff64-151">您可以指定__私密金鑰的路徑__。</span><span class="sxs-lookup"><span data-stu-id="4ff64-151">You can specify the __path to a private key__.</span></span> <span data-ttu-id="4ff64-152">使用 `ssh` 用戶端時，您可以使用 `-i` 參數來指定私密金鑰的路徑。</span><span class="sxs-lookup"><span data-stu-id="4ff64-152">With the `ssh` client, the `-i` parameter is used to specify the path to private key.</span></span> <span data-ttu-id="4ff64-153">例如： `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`。</span><span class="sxs-lookup"><span data-stu-id="4ff64-153">For example, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span></span>

* <span data-ttu-id="4ff64-154">如果您有__多個私密金鑰__可搭配不同的伺服器使用，請考慮使用 [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent) 之類的公用程式。</span><span class="sxs-lookup"><span data-stu-id="4ff64-154">If you have __multiple private keys__ for use with different servers, consider using a utility such as [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent).</span></span> <span data-ttu-id="4ff64-155">`ssh-agent` 公用程式可用來自動選取在建立 SSH 工作階段時所要使用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="4ff64-155">The `ssh-agent` utility can be used to automatically select the key to use when establishing an SSH session.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="4ff64-156">如果您使用複雜密碼來保護私密金鑰，您必須在使用金鑰時輸入複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="4ff64-156">If you secure your private key with a passphrase, you must enter the passphrase when using the key.</span></span> <span data-ttu-id="4ff64-157">`ssh-agent` 之類的公用程式可以快取密碼以方便您使用。</span><span class="sxs-lookup"><span data-stu-id="4ff64-157">Utilities such as `ssh-agent` can cache the password for your convenience.</span></span>

### <a name="create-an-ssh-key-pair"></a><span data-ttu-id="4ff64-158">建立 SSH 金鑰組</span><span class="sxs-lookup"><span data-stu-id="4ff64-158">Create an SSH key pair</span></span>

<span data-ttu-id="4ff64-159">使用 `ssh-keygen` 命令來建立公開和私密金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="4ff64-159">Use the `ssh-keygen` command to create public and private key files.</span></span> <span data-ttu-id="4ff64-160">下列命令會產生 2048 位元的 RSA 金鑰組，以供搭配 HDInsight 使用︰</span><span class="sxs-lookup"><span data-stu-id="4ff64-160">The following command generates a 2048-bit RSA key pair that can be used with HDInsight:</span></span>

    ssh-keygen -t rsa -b 2048

<span data-ttu-id="4ff64-161">在金鑰建立程序期間，系統會提示您提供資訊。</span><span class="sxs-lookup"><span data-stu-id="4ff64-161">You are prompted for information during the key creation process.</span></span> <span data-ttu-id="4ff64-162">例如，金鑰的儲存位置或是否要使用複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="4ff64-162">For example, where the keys are stored or whether to use a passphrase.</span></span> <span data-ttu-id="4ff64-163">程序完成之後，系統會建立兩個檔案：公開金鑰和私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="4ff64-163">After the process completes, two files are created; a public key and a private key.</span></span>

* <span data-ttu-id="4ff64-164">__公開金鑰__可用來建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="4ff64-164">The __public key__ is used to create an HDInsight cluster.</span></span> <span data-ttu-id="4ff64-165">公開金鑰的副檔名為 `.pub`。</span><span class="sxs-lookup"><span data-stu-id="4ff64-165">The public key has an extension of `.pub`.</span></span>

* <span data-ttu-id="4ff64-166">__私密金鑰__可用來向 HDInsight 叢集驗證用戶端。</span><span class="sxs-lookup"><span data-stu-id="4ff64-166">The __private key__ is used to authenticate your client to the HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ff64-167">您可以使用複雜密碼來保護金鑰。</span><span class="sxs-lookup"><span data-stu-id="4ff64-167">You can secure your keys using a passphrase.</span></span> <span data-ttu-id="4ff64-168">複雜密碼實際上就是私密金鑰的密碼。</span><span class="sxs-lookup"><span data-stu-id="4ff64-168">A passphrase is effectively a password on your private key.</span></span> <span data-ttu-id="4ff64-169">即使有人取得您的私密金鑰，他們必須有複雜密碼才能使用該金鑰。</span><span class="sxs-lookup"><span data-stu-id="4ff64-169">Even if someone obtains your private key, they must have the passphrase to use the key.</span></span>

### <a name="create-hdinsight-using-the-public-key"></a><span data-ttu-id="4ff64-170">使用公開金鑰建立 HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ff64-170">Create HDInsight using the public key</span></span>

| <span data-ttu-id="4ff64-171">建立方法</span><span class="sxs-lookup"><span data-stu-id="4ff64-171">Creation method</span></span> | <span data-ttu-id="4ff64-172">如何使用公開金鑰</span><span class="sxs-lookup"><span data-stu-id="4ff64-172">How to use the public key</span></span> |
| ------- | ------- |
| <span data-ttu-id="4ff64-173">**Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="4ff64-173">**Azure portal**</span></span> | <span data-ttu-id="4ff64-174">取消核取 [使用與叢集登入相同的密碼]，然後選取 [公開金鑰] 作為 SSH 驗證類型。</span><span class="sxs-lookup"><span data-stu-id="4ff64-174">Uncheck __Use same password as cluster login__, and then select __Public Key__ as the SSH authentication type.</span></span> <span data-ttu-id="4ff64-175">最後，選取公開金鑰檔案，或將檔案的文字內容貼到 [SSH 公開金鑰] 欄位。</span><span class="sxs-lookup"><span data-stu-id="4ff64-175">Finally, select the public key file or paste the text contents of the file in the __SSH public key__ field.</span></span></br><span data-ttu-id="4ff64-176">![建立 HDInsight 叢集時的 [SSH 公開金鑰] 對話方塊](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span><span class="sxs-lookup"><span data-stu-id="4ff64-176">![SSH public key dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span></span> |
| <span data-ttu-id="4ff64-177">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="4ff64-177">**Azure PowerShell**</span></span> | <span data-ttu-id="4ff64-178">使用 `New-AzureRmHdinsightCluster` Cmdlet 的 `-SshPublicKey` 參數，並以字串形式傳遞公開金鑰的內容。</span><span class="sxs-lookup"><span data-stu-id="4ff64-178">Use the `-SshPublicKey` parameter of the `New-AzureRmHdinsightCluster` cmdlet and pass the contents of the public key as a string.</span></span>|
| <span data-ttu-id="4ff64-179">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="4ff64-179">**Azure CLI 1.0**</span></span> | <span data-ttu-id="4ff64-180">使用 `azure hdinsight cluster create` 命令的 `--sshPublicKey` 參數，並以字串形式傳遞公開金鑰的內容。</span><span class="sxs-lookup"><span data-stu-id="4ff64-180">Use the `--sshPublicKey` parameter of the `azure hdinsight cluster create` command and pass the contents of the public key as a string.</span></span> |
| <span data-ttu-id="4ff64-181">**Resource Manager 範本**</span><span class="sxs-lookup"><span data-stu-id="4ff64-181">**Resource Manager Template**</span></span> | <span data-ttu-id="4ff64-182">如需對範本使用 SSH 金鑰的範例，請參閱[使用 SSH 金鑰在 Linux 上部署 HDInsight](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/)。</span><span class="sxs-lookup"><span data-stu-id="4ff64-182">For an example of using SSH keys with a template, see [Deploy HDInsight on Linux with SSH key](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/).</span></span> <span data-ttu-id="4ff64-183">[azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) 檔案中的 `publicKeys` 元素可用來在建立叢集時將金鑰傳遞至 Azure。</span><span class="sxs-lookup"><span data-stu-id="4ff64-183">The `publicKeys` element in the [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) file is used to pass the keys to Azure when creating the cluster.</span></span> |

## <span data-ttu-id="4ff64-184"><a id="sshpassword"></a>驗證︰密碼</span><span class="sxs-lookup"><span data-stu-id="4ff64-184"><a id="sshpassword"></a>Authentication: Password</span></span>

<span data-ttu-id="4ff64-185">您可以使用密碼來保護 SSH 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ff64-185">SSH accounts can be secured using a password.</span></span> <span data-ttu-id="4ff64-186">當您使用 SSH 連線到 HDInsight 時，系統會提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="4ff64-186">When you connect to HDInsight using SSH, you are prompted to enter the password.</span></span>

> [!WARNING]
> <span data-ttu-id="4ff64-187">我們不建議您對 SSH 使用密碼驗證。</span><span class="sxs-lookup"><span data-stu-id="4ff64-187">We do not recommend using password authentication for SSH.</span></span> <span data-ttu-id="4ff64-188">密碼可以猜到，因此很容易遭受暴力密碼破解攻擊。</span><span class="sxs-lookup"><span data-stu-id="4ff64-188">Passwords can be guessed and are vulnerable to brute force attacks.</span></span> <span data-ttu-id="4ff64-189">相反地，我們會建議您使用 [SSH 金鑰來進行驗證](#sshkey)。</span><span class="sxs-lookup"><span data-stu-id="4ff64-189">Instead, we recommend that you use [SSH keys for authentication](#sshkey).</span></span>

### <a name="create-hdinsight-using-a-password"></a><span data-ttu-id="4ff64-190">使用密碼建立 HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ff64-190">Create HDInsight using a password</span></span>

| <span data-ttu-id="4ff64-191">建立方法</span><span class="sxs-lookup"><span data-stu-id="4ff64-191">Creation method</span></span> | <span data-ttu-id="4ff64-192">如何指定密碼</span><span class="sxs-lookup"><span data-stu-id="4ff64-192">How to specify the password</span></span> |
| --------------- | ---------------- |
| <span data-ttu-id="4ff64-193">**Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="4ff64-193">**Azure portal**</span></span> | <span data-ttu-id="4ff64-194">根據預設，SSH 使用者帳戶會具有和叢集登入帳戶相同的密碼。</span><span class="sxs-lookup"><span data-stu-id="4ff64-194">By default, the SSH user account has the same password as the cluster login account.</span></span> <span data-ttu-id="4ff64-195">若要使用不同的密碼，請取消核取 [使用與叢集登入相同的密碼]，然後在 [SSH 密碼] 欄位中輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="4ff64-195">To use a different password, uncheck __Use same password as cluster login__, and then enter the password in the __SSH password__ field.</span></span></br><span data-ttu-id="4ff64-196">![建立 HDInsight 叢集時的 [SSH 密碼] 對話方塊](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span><span class="sxs-lookup"><span data-stu-id="4ff64-196">![SSH password dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span></span>|
| <span data-ttu-id="4ff64-197">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="4ff64-197">**Azure PowerShell**</span></span> | <span data-ttu-id="4ff64-198">使用 `New-AzureRmHdinsightCluster` Cmdlet 的 `--SshCredential` 參數，並傳遞包含 SSH 使用者帳戶名稱和密碼的 `PSCredential` 物件。</span><span class="sxs-lookup"><span data-stu-id="4ff64-198">Use the `--SshCredential` parameter of the `New-AzureRmHdinsightCluster` cmdlet and pass a `PSCredential` object that contains the SSH user account name and password.</span></span> |
| <span data-ttu-id="4ff64-199">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="4ff64-199">**Azure CLI 1.0**</span></span> | <span data-ttu-id="4ff64-200">使用 `azure hdinsight cluster create` 命令的 `--sshPassword` 參數，並提供密碼值。</span><span class="sxs-lookup"><span data-stu-id="4ff64-200">Use the `--sshPassword` parameter of the `azure hdinsight cluster create` command and provide the password value.</span></span> |
| <span data-ttu-id="4ff64-201">**Resource Manager 範本**</span><span class="sxs-lookup"><span data-stu-id="4ff64-201">**Resource Manager Template**</span></span> | <span data-ttu-id="4ff64-202">如需對範本使用密碼的範例，請參閱[使用 SSH 密碼在 Linux 上部署 HDInsight](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/)。</span><span class="sxs-lookup"><span data-stu-id="4ff64-202">For an example of using a password with a template, see [Deploy HDInsight on Linux with SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span></span> <span data-ttu-id="4ff64-203">[azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) 檔案中的 `linuxOperatingSystemProfile` 元素可用來在建立叢集時將 SSH 帳戶名稱和密碼傳遞至 Azure。</span><span class="sxs-lookup"><span data-stu-id="4ff64-203">The `linuxOperatingSystemProfile` element in the [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) file is used to pass the SSH account name and password to Azure when creating the cluster.</span></span>|

### <a name="change-the-ssh-password"></a><span data-ttu-id="4ff64-204">變更 SSH 密碼</span><span class="sxs-lookup"><span data-stu-id="4ff64-204">Change the SSH password</span></span>

<span data-ttu-id="4ff64-205">如需有關變更 SSH 使用者帳戶密碼的資訊，請參閱[管理 HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) 文件的__變更密碼__一節。</span><span class="sxs-lookup"><span data-stu-id="4ff64-205">For information on changing the SSH user account password, see the __Change passwords__ section of the [Manage HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) document.</span></span>

## <span data-ttu-id="4ff64-206"><a id="domainjoined"></a>驗證︰已加入網域的 HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ff64-206"><a id="domainjoined"></a>Authentication: Domain-joined HDInsight</span></span>

<span data-ttu-id="4ff64-207">如果您使用__已加入網域的 HDInsight 叢集__，您必須在使用 SSH 連線之後使用 `kinit` 命令。</span><span class="sxs-lookup"><span data-stu-id="4ff64-207">If you are using a __domain-joined HDInsight cluster__, you must use the `kinit` command after connecting with SSH.</span></span> <span data-ttu-id="4ff64-208">此命令會提示您輸入網域使用者和密碼，並向與叢集相關聯的 Azure Active Directory 網域驗證您的工作階段。</span><span class="sxs-lookup"><span data-stu-id="4ff64-208">This command prompts you for a domain user and password, and authenticates your session with the Azure Active Directory domain associated with the cluster.</span></span>

<span data-ttu-id="4ff64-209">如需詳細資訊，請參閱[設定已加入網域的 HDInsight](hdinsight-domain-joined-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="4ff64-209">For more information, see [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md).</span></span>

## <a name="connect-to-nodes"></a><span data-ttu-id="4ff64-210">連線到節點</span><span class="sxs-lookup"><span data-stu-id="4ff64-210">Connect to nodes</span></span>

<span data-ttu-id="4ff64-211">可在連接埠 22 和 23 上透過網際網路存取前端節點和邊緣節點 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="4ff64-211">The head nodes and edge node (if there is one) can be accessed over the internet on ports 22 and 23.</span></span>

* <span data-ttu-id="4ff64-212">連線到__前端節點__時，請使用連接埠 __22__ 連線到主要前端節點，以及使用連接埠 __23__ 連線到次要前端節點。</span><span class="sxs-lookup"><span data-stu-id="4ff64-212">When connecting to the __head nodes__, use port __22__ to connect to the primary head node and port __23__ to connect to the secondary head node.</span></span> <span data-ttu-id="4ff64-213">要使用的完整網域名稱為 `clustername-ssh.azurehdinsight.net`，其中 `clustername` 是您的叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="4ff64-213">The fully qualified domain name to use is `clustername-ssh.azurehdinsight.net`, where `clustername` is the name of your cluster.</span></span>

    ```bash
    # Connect to primary head node
    # port not specified since 22 is the default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect to secondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* <span data-ttu-id="4ff64-214">連線到__邊緣節點__時，請使用通訊埠 22。</span><span class="sxs-lookup"><span data-stu-id="4ff64-214">When connectiung to the __edge node__, use port 22.</span></span> <span data-ttu-id="4ff64-215">完整網域名稱為 `edgenodename.clustername-ssh.azurehdinsight.net`，其中 `edgenodename` 是您建立邊緣節點時提供的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ff64-215">The fully qualified domain name is `edgenodename.clustername-ssh.azurehdinsight.net`, where `edgenodename` is a name you provided when creating the edge node.</span></span> <span data-ttu-id="4ff64-216">`clustername` 是叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ff64-216">`clustername` is the name of the cluster.</span></span>

    ```bash
    # Connect to edge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> <span data-ttu-id="4ff64-217">先前的範例假設您使用密碼驗證，或該憑證驗證自動發生。</span><span class="sxs-lookup"><span data-stu-id="4ff64-217">The previous examples assume that you are using password authentication, or that certificate authentication is occuring automatically.</span></span> <span data-ttu-id="4ff64-218">如果您使用 SSH 金鑰組進行驗證，但未自動使用憑證，請使用 `-i` 參數來指定私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="4ff64-218">If you use an SSH key-pair for authentication, and the certificate is not used automatically, use the `-i` parameter to specify the private key.</span></span> <span data-ttu-id="4ff64-219">例如， `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`。</span><span class="sxs-lookup"><span data-stu-id="4ff64-219">For example, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span></span>

<span data-ttu-id="4ff64-220">連線之後，字元會變更，以指示 SSH 使用者名稱和您所連線的節點。</span><span class="sxs-lookup"><span data-stu-id="4ff64-220">Once connected, the prompt changes to indicate the SSH user name and the node you are connected to.</span></span> <span data-ttu-id="4ff64-221">例如，以 `sshuser` 身分連線到主要前端節點時，提示為 `sshuser@hn0-clustername:~$`。</span><span class="sxs-lookup"><span data-stu-id="4ff64-221">For example, when connected to the primary head node as `sshuser`, the prompt is `sshuser@hn0-clustername:~$`.</span></span>

### <a name="connect-to-worker-and-zookeeper-nodes"></a><span data-ttu-id="4ff64-222">連線至背景工作角色和 Zookeeper 節點</span><span class="sxs-lookup"><span data-stu-id="4ff64-222">Connect to worker and Zookeeper nodes</span></span>

<span data-ttu-id="4ff64-223">無法從網際網路直接存取背景工作角色節點和 Zookeeper 節點。</span><span class="sxs-lookup"><span data-stu-id="4ff64-223">The worker nodes and Zookeeper nodes are not directly accessible from the internet.</span></span> <span data-ttu-id="4ff64-224">從叢集前端節點或邊緣節點即可加以存取。</span><span class="sxs-lookup"><span data-stu-id="4ff64-224">They can be accessed from the cluster head nodes or edge nodes.</span></span> <span data-ttu-id="4ff64-225">以下是連接至其他節點的一般步驟：</span><span class="sxs-lookup"><span data-stu-id="4ff64-225">The following are the general steps to connect to other nodes:</span></span>

1. <span data-ttu-id="4ff64-226">使用 SSH 連接前端或邊緣節點：</span><span class="sxs-lookup"><span data-stu-id="4ff64-226">Use SSH to connect to a head or edge node:</span></span>

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. <span data-ttu-id="4ff64-227">從 SSH 到前端或邊緣節點的連線，使用 `ssh` 命令來連接叢集中的背景工作角色節點︰</span><span class="sxs-lookup"><span data-stu-id="4ff64-227">From the SSH connection to the head or edge node, use the `ssh` command to connect to a worker node in the cluster:</span></span>

        ssh sshuser@wn0-myhdi

    <span data-ttu-id="4ff64-228">若要擷取叢集節點的網域名稱清單，請參閱[使用 Ambari REST API 管理 HDInsight](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) 文件。</span><span class="sxs-lookup"><span data-stu-id="4ff64-228">To retrieve a list of the domain names of the nodes in the cluster, see the [Manage HDInsight by using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) document.</span></span>

<span data-ttu-id="4ff64-229">如果使用__密碼__來保護 SSH 帳戶，請在連線時輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="4ff64-229">If the SSH account is secured using a __password__, enter the password when connecting.</span></span>

<span data-ttu-id="4ff64-230">如果使用 __SSH 金鑰__來保護 SSH 帳戶，請確定用戶端上的 SSH 轉送已啟用。</span><span class="sxs-lookup"><span data-stu-id="4ff64-230">If the SSH account is secured using __SSH keys__, make sure that SSH forwarding is enabled on the client.</span></span>

> [!NOTE]
> <span data-ttu-id="4ff64-231">若要直接存取叢集中的所有節點，另一種方式是將 HDInsight 安裝到 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4ff64-231">Another way to directly access all nodes in the cluster is to install HDInsight into an Azure Virtual Network.</span></span> <span data-ttu-id="4ff64-232">然後，您可以將遠端機器加入相同的虛擬網路，並直接存取叢集中的所有節點。</span><span class="sxs-lookup"><span data-stu-id="4ff64-232">Then, you can join your remote machine to the same virtual network and directly access all nodes in the cluster.</span></span>
>
> <span data-ttu-id="4ff64-233">如需詳細資訊，請參閱[搭配 HDInsight 使用虛擬網路](hdinsight-extend-hadoop-virtual-network.md)。</span><span class="sxs-lookup"><span data-stu-id="4ff64-233">For more information, see [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md).</span></span>

### <a name="configure-ssh-agent-forwarding"></a><span data-ttu-id="4ff64-234">設定 SSH 代理程式轉送</span><span class="sxs-lookup"><span data-stu-id="4ff64-234">Configure SSH agent forwarding</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ff64-235">以下步驟假設您使用以 Linux 或 UNIX 為基礎的系統，並使用 Bash on Windows 10 進行操作。</span><span class="sxs-lookup"><span data-stu-id="4ff64-235">The following steps assume a Linux or UNIX-based system, and work with Bash on Windows 10.</span></span> <span data-ttu-id="4ff64-236">如果這些步驟不適用於您的系統，您可能需要參閱 SSH 用戶端的文件。</span><span class="sxs-lookup"><span data-stu-id="4ff64-236">If these steps do not work for your system, you may need to consult the documentation for your SSH client.</span></span>

1. <span data-ttu-id="4ff64-237">使用文字編輯器開啟 `~/.ssh/config`。</span><span class="sxs-lookup"><span data-stu-id="4ff64-237">Using a text editor, open `~/.ssh/config`.</span></span> <span data-ttu-id="4ff64-238">如果該檔案不存在，您可以藉由在命令列中輸入 `touch ~/.ssh/config` 加以建立。</span><span class="sxs-lookup"><span data-stu-id="4ff64-238">If this file doesn't exist, you can create it by entering `touch ~/.ssh/config` at a command line.</span></span>

2. <span data-ttu-id="4ff64-239">將下列文字新增至 `config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="4ff64-239">Add the following text to the `config` file.</span></span>

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    <span data-ttu-id="4ff64-240">將 __Host__ 資訊替換為您使用 SSH 連線到的節點位址。</span><span class="sxs-lookup"><span data-stu-id="4ff64-240">Replace the __Host__ information with the address of the node you connect to using SSH.</span></span> <span data-ttu-id="4ff64-241">先前的範例使用邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="4ff64-241">The previous example uses the edge node.</span></span> <span data-ttu-id="4ff64-242">這個項目會為指定節點設定 SSH 代理程式轉送。</span><span class="sxs-lookup"><span data-stu-id="4ff64-242">This entry configures SSH agent forwarding for the specified node.</span></span>

3. <span data-ttu-id="4ff64-243">從終端機使用下列命令，測試 SSH 代理程式轉送：</span><span class="sxs-lookup"><span data-stu-id="4ff64-243">Test SSH agent forwarding by using the following command from the terminal:</span></span>

        echo "$SSH_AUTH_SOCK"

    <span data-ttu-id="4ff64-244">此命令會傳回類似以下文字的資訊：</span><span class="sxs-lookup"><span data-stu-id="4ff64-244">This command returns information similar to the following text:</span></span>

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    <span data-ttu-id="4ff64-245">如果未傳回任何資訊，表示 `ssh-agent` 未執行。</span><span class="sxs-lookup"><span data-stu-id="4ff64-245">If nothing is returned, then `ssh-agent` is not running.</span></span> <span data-ttu-id="4ff64-246">如需詳細資訊，請參閱[透過 ssh 使用 ssh-agent (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) 的代理程式啟動指令碼資訊，或參閱 SSH 用戶端文件。</span><span class="sxs-lookup"><span data-stu-id="4ff64-246">For more information, see the agent startup scripts information at [Using ssh-agent with ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) or consult your SSH client documentation.</span></span>

4. <span data-ttu-id="4ff64-247">一旦確認 **ssh-agent** 正在執行，請使用下列項目將您的 SSH 私密金鑰新增至代理程式：</span><span class="sxs-lookup"><span data-stu-id="4ff64-247">Once you have verified that **ssh-agent** is running, use the following to add your SSH private key to the agent:</span></span>

        ssh-add ~/.ssh/id_rsa

    <span data-ttu-id="4ff64-248">如果您的私密金鑰儲存在不同的檔案，請將 `~/.ssh/id_rsa` 取代為檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="4ff64-248">If your private key is stored in a different file, replace `~/.ssh/id_rsa` with the path to the file.</span></span>

5. <span data-ttu-id="4ff64-249">使用 SSH 連線到叢集的邊緣節點或前端節點。</span><span class="sxs-lookup"><span data-stu-id="4ff64-249">Connect to the cluster edge node or head nodes using SSH.</span></span> <span data-ttu-id="4ff64-250">然後，使用 SSH 命令連線到背景工作角色或 Zookeeper 節點。</span><span class="sxs-lookup"><span data-stu-id="4ff64-250">Then use the SSH command to connect to a worker or zookeeper node.</span></span> <span data-ttu-id="4ff64-251">該連線會使用轉送的金鑰來建立。</span><span class="sxs-lookup"><span data-stu-id="4ff64-251">The connection is established using the forwarded key.</span></span>

## <a name="copy-files"></a><span data-ttu-id="4ff64-252">複製檔案</span><span class="sxs-lookup"><span data-stu-id="4ff64-252">Copy files</span></span>

<span data-ttu-id="4ff64-253">`scp` 公用程式可用於雙向複製叢集中個別節點的檔案。</span><span class="sxs-lookup"><span data-stu-id="4ff64-253">The `scp` utility can be used to copy files to and from individual nodes in the cluster.</span></span> <span data-ttu-id="4ff64-254">例如，下列命令可將 `test.txt` 目錄從本機系統複製到主要前端節點：</span><span class="sxs-lookup"><span data-stu-id="4ff64-254">For example, the following command copies the `test.txt` directory from the local system to the primary head node:</span></span>

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

<span data-ttu-id="4ff64-255">因為未在 `:` 之後指定路徑，所以此檔案會置於 `sshuser` 主目錄中。</span><span class="sxs-lookup"><span data-stu-id="4ff64-255">Since no path is specified after the `:`, the file is placed in the `sshuser` home directory.</span></span>

<span data-ttu-id="4ff64-256">下列範例可將 `test.txt` 檔案從主要前端節點上的 `sshuser` 主目錄複製到本機系統：</span><span class="sxs-lookup"><span data-stu-id="4ff64-256">The following example copies the `test.txt` file from the `sshuser` home directory on the primary head node to the local system:</span></span>

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> <span data-ttu-id="4ff64-257">`scp` 只能存取叢集內個別節點的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="4ff64-257">`scp` can only access the file system of individual nodes within the cluster.</span></span> <span data-ttu-id="4ff64-258">它不能用來存取叢集的 HDFS 相容儲存體中的資料。</span><span class="sxs-lookup"><span data-stu-id="4ff64-258">It cannot be used to access data in the HDFS-compatible storage for the cluster.</span></span>
>
> <span data-ttu-id="4ff64-259">當您需要從 SSH 工作階段上傳資源以供使用時，請使用 `scp`。</span><span class="sxs-lookup"><span data-stu-id="4ff64-259">Use `scp` when you need to upload a resource for use from an SSH session.</span></span> <span data-ttu-id="4ff64-260">例如，上傳 Python 指令碼，然後從 SSH 工作階段執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="4ff64-260">For example, upload a Python script and then run the script from an SSH session.</span></span>
>
> <span data-ttu-id="4ff64-261">如需直接將資料載入 HDFS 相容儲存體的資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="4ff64-261">For information on directly loading data into the HDFS-compatible storage, see the following documents:</span></span>
>
> * <span data-ttu-id="4ff64-262">[使用 Azure 儲存體的 HDInsight](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="4ff64-262">[HDInsight using Azure Storage](hdinsight-hadoop-use-blob-storage.md).</span></span>
>
> * <span data-ttu-id="4ff64-263">[使用 Azure Data Lake Store 的 HDInsight](hdinsight-hadoop-use-data-lake-store.md)。</span><span class="sxs-lookup"><span data-stu-id="4ff64-263">[HDInsight using Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ff64-264">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ff64-264">Next steps</span></span>

* [<span data-ttu-id="4ff64-265">對 HDInsight 使用 SSH 通道</span><span class="sxs-lookup"><span data-stu-id="4ff64-265">Use SSH tunneling with HDInsight</span></span>](hdinsight-linux-ambari-ssh-tunnel.md)
* [<span data-ttu-id="4ff64-266">對 HDInsight 使用虛擬網路</span><span class="sxs-lookup"><span data-stu-id="4ff64-266">Use a virtual network with HDInsight</span></span>](hdinsight-extend-hadoop-virtual-network.md)
* [<span data-ttu-id="4ff64-267">在 HDInsight 中使用邊緣節點</span><span class="sxs-lookup"><span data-stu-id="4ff64-267">Use edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md#access-an-edge-node)