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
# <a name="connect-toohdinsight-hadoop-using-ssh"></a>連接 tooHDInsight (Hadoop) 使用 SSH

深入了解如何 toouse[安全殼層 (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely 連接 tooHadoop Azure HDInsight 上的。 

HDInsight 可用於 Linux (Ubuntu) 做為 hello 作業系統 hello Hadoop 叢集內的節點。 hello 下表包含連接 tooLinux 為基礎的 HDInsight 的 SSH 用戶端時所需的 hello 位址和連接埠資訊：

| 位址 | 連接埠 | 連線到... |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | 22 | 邊緣節點 (R Server on HDInsight) |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | 邊緣節點 (任何其他叢集類型，如果邊緣節點存在的話) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | 主要前端節點 |
| `<clustername>-ssh.azurehdinsight.net` | 23 | 次要前端節點 |

> [!NOTE]
> 取代`<edgenodename>`hello hello 邊緣節點名稱。
>
> 取代`<clustername>`與 hello 叢集的名稱。
>
> 如果您的叢集包含邊緣節點，我們建議您__永遠連線 toohello 邊緣節點__使用 SSH。 hello 前端節點裝載的 Hadoop 的重要 toohello 健全狀況服務。 hello 邊緣節點執行只什麼您暫停它。
>
> 如需使用邊緣節點的詳細資訊，請參閱[在 HDInsight 中使用邊緣節點](hdinsight-apps-use-edge-node.md#access-an-edge-node)。

## <a name="ssh-clients"></a>SSH 用戶端

Linux、 Unix 及 macOS 系統提供 hello`ssh`和`scp`命令。 hello`ssh`用戶端是常用的 toocreate 與 Linux 或 unix 系統的遠端命令列工作階段。 hello`scp`用戶端是用戶端與 hello 遠端系統之間使用的 toosecurely 複製檔案。

Microsoft Windows 預設不會提供任何 SSH 用戶端。 hello`ssh`和`scp`用戶端會經由 windows hello 下列封裝：

* [Azure 雲端殼層](../cloud-shell/quickstart.md): hello 雲端殼層提供 Bash 環境，在瀏覽器，並提供 hello `ssh`， `scp`，和其他常見的 Linux 命令。

* [在 Windows 10 上的 Ubuntu 上撞](https://msdn.microsoft.com/commandline/wsl/about): hello`ssh`和`scp`命令都是透過在 Windows 命令列上的 hello Bash。

* [Git (https://git-scm.com/)](https://git-scm.com/): hello`ssh`和`scp`命令都是透過 hello GitBash 命令列。

* [GitHub 桌面 (https://desktop.github.com/)](https://desktop.github.com/) hello`ssh`和`scp`命令都是透過 hello GitHub 命令介面命令列。 GitHub 桌面可以為 hello hello Git 殼層命令列設定的 toouse Bash，hello Windows 命令提示字元或 PowerShell。

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello PowerShell 小組移植 OpenSSH tooWindows，並提供測試版本。

    > [!WARNING]
    > hello OpenSSH 封裝包括 hello SSH 伺服器元件， `sshd`。 此元件啟動 SSH 伺服器上您的系統，讓其他人 tooconnect tooit。 請勿設定此元件，或開啟通訊埠 22，除非您想 toohost SSH 伺服器系統上。 不需要與 HDInsight toocommunicate。

另外還有數個圖形化 SSH 用戶端，例如 [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) 和 [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/)。 雖然這些用戶端可以使用的 tooconnect tooHDInsight，連接的 hello 程序是不同於使用 hello`ssh`公用程式。 如需詳細資訊，請參閱 hello 文件的 hello 您所使用的圖形化用戶端。

## <a id="sshkey"></a>驗證︰SSH 金鑰

SSH 金鑰會使用[公開金鑰密碼編譯](https://en.wikipedia.org/wiki/Public-key_cryptography)tooauthenticate SSH 工作階段。 SSH 金鑰的密碼，比更安全，並提供輕鬆 toosecure 存取 tooyour Hadoop 叢集。

SSH 帳戶受到保護使用索引鍵，如果 hello 用戶端必須提供符合私用的索引鍵，當您連接的 hello:

* 大部分的用戶端可以設定的 toouse__預設金鑰__。 例如，hello`ssh`私密金鑰在用戶端會尋找`~/.ssh/id_rsa`在 Linux 和 Unix 環境。

* 您可以指定 hello__路徑 tooa 私密金鑰__。 以 hello`ssh`用戶端、 hello`-i`參數是使用的 toospecify hello 路徑 tooprivate 機碼。 例如： `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`。

* 如果您有__多個私密金鑰__可搭配不同的伺服器使用，請考慮使用 [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent) 之類的公用程式。 hello`ssh-agent`公用程式時，才能使用的 tooautomatically 選取 hello 金鑰 toouse 建立的 SSH 工作階段。

> [!IMPORTANT]
>
> 如果您保護您的複雜密碼的私密金鑰，您必須在使用 hello 金鑰時，輸入 hello 複雜密碼。 公用程式，例如`ssh-agent`可以快取 hello，方便您使用的密碼。

### <a name="create-an-ssh-key-pair"></a>建立 SSH 金鑰組

使用 hello`ssh-keygen`命令 toocreate 公用和私用金鑰檔。 hello 下列命令會產生 2048年位元 RSA 金鑰組，可以搭配 HDInsight:

    ssh-keygen -t rsa -b 2048

會提示您輸入 hello 金鑰的建立程序期間的資訊。 例如，其中 hello 金鑰會儲存或是否 toouse 複雜密碼。 Hello 程序完成之後，會建立兩個檔案。公開金鑰和私密金鑰。

* hello__公開金鑰__是使用的 toocreate HDInsight 叢集。 hello 公開金鑰副檔名為`.pub`。

* hello__私密金鑰__是使用的 tooauthenticate 用戶端 toohello HDInsight 叢集。

> [!IMPORTANT]
> 您可以使用複雜密碼來保護金鑰。 複雜密碼實際上就是私密金鑰的密碼。 即使其他人取得您的私密金鑰，它們必須擁有 hello 複雜密碼 toouse hello 金鑰。

### <a name="create-hdinsight-using-hello-public-key"></a>建立 HDInsight 使用 hello 公開金鑰

| 建立方法 | 如何 toouse hello 公開金鑰 |
| ------- | ------- |
| **Azure 入口網站** | 取消核取__使用與叢集登入相同的密碼__，然後選取__公開金鑰__為 hello SSH 驗證類型。 最後，選取 hello 公開金鑰檔案或 hello 檔案 hello 文字內容貼在 hello __SSH 公開金鑰__欄位。</br>![建立 HDInsight 叢集時的 [SSH 公開金鑰] 對話方塊](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **Azure PowerShell** | 使用 hello `-SshPublicKey` hello 參數`New-AzureRmHdinsightCluster`hello 公開金鑰，做為字串的 cmdlet 並傳遞 hello 內容。|
| **Azure CLI 1.0** | 使用 hello `--sshPublicKey` hello 參數`azure hdinsight cluster create`命令，並以字串形式傳遞的 hello 公開金鑰的 hello 內容。 |
| **Resource Manager 範本** | 如需對範本使用 SSH 金鑰的範例，請參閱[使用 SSH 金鑰在 Linux 上部署 HDInsight](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/)。 hello `publicKeys` hello 中的項目[azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json)檔案時，才能使用的 toopass hello 金鑰 tooAzure 建立 hello 叢集。 |

## <a id="sshpassword"></a>驗證︰密碼

您可以使用密碼來保護 SSH 帳戶。 當您連接使用 SSH tooHDInsight 時，您都會有提示的 tooenter hello 密碼。

> [!WARNING]
> 我們不建議您對 SSH 使用密碼驗證。 密碼可以猜到，而且是 toobrute 容易遭受攻擊。 相反地，我們會建議您使用 [SSH 金鑰來進行驗證](#sshkey)。

### <a name="create-hdinsight-using-a-password"></a>使用密碼建立 HDInsight

| 建立方法 | 如何 toospecify hello 密碼 |
| --------------- | ---------------- |
| **Azure 入口網站** | 根據預設，hello SSH 使用者帳戶具有 hello hello 叢集登入帳戶為相同的密碼。 toouse 不同的密碼，取消核取__使用與叢集登入相同的密碼__，然後輸入 hello 密碼在 hello __SSH 密碼__欄位。</br>![建立 HDInsight 叢集時的 [SSH 密碼] 對話方塊](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **Azure PowerShell** | 使用 hello `--SshCredential` hello 參數`New-AzureRmHdinsightCluster`cmdlet 並傳遞`PSCredential`物件，其中包含 hello SSH 使用者帳戶名稱和密碼。 |
| **Azure CLI 1.0** | 使用 hello `--sshPassword` hello 參數`azure hdinsight cluster create`命令，並提供 hello 密碼值。 |
| **Resource Manager 範本** | 如需對範本使用密碼的範例，請參閱[使用 SSH 密碼在 Linux 上部署 HDInsight](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/)。 hello `linuxOperatingSystemProfile` hello 中的項目[azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json)檔案時，才能使用的 toopass hello SSH 帳戶名稱和密碼 tooAzure 建立 hello 叢集。|

### <a name="change-hello-ssh-password"></a>變更 hello SSH 密碼

如需變更 hello SSH 使用者帳戶密碼的資訊，請參閱 hello__變更密碼__區段 hello[管理 HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords)文件。

## <a id="domainjoined"></a>驗證︰已加入網域的 HDInsight

如果您使用__已加入網域的 HDInsight 叢集__，您必須使用 hello`kinit`透過 SSH 連線後命令。 此命令會提示您輸入網域使用者和密碼，並驗證您的工作階段與 hello 與 hello 叢集相關聯的 Azure Active Directory 網域。

如需詳細資訊，請參閱[設定已加入網域的 HDInsight](hdinsight-domain-joined-configure.md)。

## <a name="connect-toonodes"></a>連接 toonodes

hello 前端節點與邊緣節點 （如果有的話） 是否可透過 hello 存取網際網路的連接埠 22 和 23。

* 當連接 toohello__前端節點__，使用連接埠__22__ tooconnect toohello 主要前端節點和連接埠__23__ tooconnect toohello 次要前端節點。 hello 完整的網域名稱 toouse 是`clustername-ssh.azurehdinsight.net`，其中`clustername`是 hello 叢集的名稱。

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* 當 connectiung toohello__邊緣節點__，使用通訊埠 22。 hello 完整的網域名稱是`edgenodename.clustername-ssh.azurehdinsight.net`，其中`edgenodename`時提供的名稱建立 hello 邊緣節點。 `clustername`這是 hello hello 叢集名稱。

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> hello 前一個範例假設您使用密碼驗證，或該憑證驗證會自動發生。 如果您使用 SSH 金鑰組進行驗證，不會自動使用 hello 憑證，請使用 hello`-i`參數 toospecify hello 私用金鑰。 例如： `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`。

一旦連接之後，hello 提示字元會變成 tooindicate hello SSH 使用者名稱和 hello 節點連線到。 例如，當連線 toohello 主要標頭的節點做為`sshuser`，hello 提示是`sshuser@hn0-clustername:~$`。

### <a name="connect-tooworker-and-zookeeper-nodes"></a>連接 tooworker 和動物園管理員節點

hello 背景工作節點和節點不是直接存取從動物園管理員 hello 網際網路。 Hello 叢集前端節點或邊緣節點，可以存取它們。 hello 下面是 hello 的一般步驟 tooconnect tooother 節點：

1. 使用 SSH tooconnect tooa head 或邊緣節點：

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. 從 hello SSH 連線 toohello head 或邊緣節點，使用 hello`ssh`命令 tooconnect tooa hello 叢集中的背景工作節點：

        ssh sshuser@wn0-myhdi

    tooretrieve hello 叢集中的節點 hello，hello 網域名稱的清單，請參閱 「 hello[管理 HDInsight 使用 hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes)文件。

如果使用保護 hello SSH 帳戶__密碼__，連接時，請輸入 hello 密碼。

如果使用保護 hello SSH 帳戶__SSH 金鑰__，請確定 SSH 轉送已啟用 hello 用戶端上。

> [!NOTE]
> Toodirectly 存取 hello 叢集中所有節點的另一個方法是 tooinstall HDInsight，在 Azure 虛擬網路。 然後，您可以在其中加入遠端機器 toohello 相同虛擬網路，並直接存取 hello 叢集中所有節點。
>
> 如需詳細資訊，請參閱[搭配 HDInsight 使用虛擬網路](hdinsight-extend-hadoop-virtual-network.md)。

### <a name="configure-ssh-agent-forwarding"></a>設定 SSH 代理程式轉送

> [!IMPORTANT]
> hello 下列步驟假設 Linux 或 UNIX 為基礎的系統，並使用 Windows 10 上 Bash。 如果這些步驟不適用於您的系統，您可能需要 tooconsult hello 文件 SSH 用戶端。

1. 使用文字編輯器開啟 `~/.ssh/config`。 如果該檔案不存在，您可以藉由在命令列中輸入 `touch ~/.ssh/config` 加以建立。

2. 加入下列文字 toohello hello`config`檔案。

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    取代 hello__主機__資訊 hello hello 節點位址與連接 toousing SSH。 hello 前一個範例會使用 hello 邊緣節點。 此項目會設定轉送 hello 指定節點的 SSH 代理程式。

3. 測試 SSH 代理程式轉寄使用 hello hello 終端機中的下列命令：

        echo "$SSH_AUTH_SOCK"

    此命令會傳回資訊的類似 toohello 下列文字：

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    如果未傳回任何資訊，表示 `ssh-agent` 未執行。 如需詳細資訊，請參閱 < 在 hello 代理程式啟動指令碼資訊[使用 ssh 代理程式與 ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) ，或連絡您的 SSH 用戶端文件。

4. 一旦確認**ssh 代理**正在執行，使用 hello 遵循 tooadd SSH 私用金鑰 toohello 代理程式：

        ssh-add ~/.ssh/id_rsa

    如果您的私密金鑰會儲存在不同的檔案，取代`~/.ssh/id_rsa`與 hello 路徑 toohello 檔案。

5. Toohello 叢集邊緣節點或前端節點使用 SSH 連線。 接著使用 hello SSH 命令 tooconnect tooa 背景工作或動物園管理員節點。 使用轉送 hello 索引鍵來建立 hello 連接。

## <a name="copy-files"></a>複製檔案

hello`scp`公用程式可以使用的 toocopy 檔案 tooand 從 hello 叢集中的個別節點。 例如，下列命令複製 hello 來 hello`test.txt`目錄從 hello 本機系統 toohello 主要前端節點：

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

因為未指定路徑之後 hello `:`，hello 檔案置於 hello`sshuser`主目錄。

下列範例複製 hello hello`test.txt`檔案從 hello `sshuser` hello 主要的前端節點 toohello 本機系統上的主目錄：

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> `scp`只能存取 hello hello 叢集內的個別節點的檔案系統。 它不能使用的 tooaccess hello 叢集 hello HDFS 相容儲存體中的資料。
>
> 使用`scp`何時該添 tooupload 資源從的 SSH 工作階段使用。 例如上, 傳的 Python 指令碼，然後再執行的 SSH 工作階段中的 hello 指令碼。
>
> 直接將資料載入 hello HDFS 相容存放裝置上的資訊，請參閱下列文件的 hello:
>
> * [使用 Azure 儲存體的 HDInsight](hdinsight-hadoop-use-blob-storage.md)。
>
> * [使用 Azure Data Lake Store 的 HDInsight](hdinsight-hadoop-use-data-lake-store.md)。

## <a name="next-steps"></a>後續步驟

* [對 HDInsight 使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)
* [對 HDInsight 使用虛擬網路](hdinsight-extend-hadoop-virtual-network.md)
* [在 HDInsight 中使用邊緣節點](hdinsight-apps-use-edge-node.md#access-an-edge-node)