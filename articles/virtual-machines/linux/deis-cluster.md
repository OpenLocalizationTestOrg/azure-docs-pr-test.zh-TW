---
title: "3 個節點 Deis 的 aaaDeploy 叢集 |Microsoft 文件"
description: "本文說明如何 toocreate 3 節點 Deis 在 Azure 中使用 Azure Resource Manager 範本上的叢集"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>在 Azure 中部署和設定 3 個節點的 Deis 叢集
本文將指導您逐步完成在 Azure 上佈建 [Deis](http://deis.io/) 叢集。 它涵蓋了所有 hello 步驟建立 hello 必要的憑證 toodeploying 和縮放範例**移**hello 新佈建叢集上的應用程式。

hello 下列圖表顯示 hello 部署的 hello 系統架構。 系統管理員管理 hello 叢集使用例如 Deis 工具**deis**和**deisctl**。 透過 Azure 負載平衡器會將轉送 hello 連線 tooone hello 成員的 hello 叢集上的節點建立連線。 hello 用戶端存取部署的應用程式透過以及 hello 負載平衡器。 在此情況下，hello 負載平衡器轉送 hello 流量 tooa Deis 路由器網狀結構，進一步 routs hello 叢集上裝載的流量 toocorresponding Docker 容器。

  ![已部署之 Desis 叢集的架構圖](./media/deis-cluster/architecture-overview.png)

在透過 hello 步驟順序 toorun，您將需要：

* 有效的 Azure 訂用帳戶。 如果沒有，您可以在 [azure.com](https://azure.microsoft.com/)免費取得一個。
* 工作或學校識別碼 toouse Azure 資源群組。 如果您有個人帳戶和登入 Microsoft id，您需要太[從個人所建立的工作識別碼](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* -根據用戶端作業系統-hello [Azure PowerShell](/powershell/azureps-cmdlets-docs)或 hello [Mac、 Linux 和 Windows Azure CLI](../../cli-install-nodejs.md)。
* [OpenSSL](https://www.openssl.org/)。 OpenSSL 是使用的 toogenerate hello 必要的憑證。
* Git 用戶端，例如 [Git Bash](https://git-scm.com/)。
* tootest hello 範例應用程式，您還需要 DNS 伺服器。 您也可以使用任何 DNS 伺服器或 支援萬用字元 A 記錄的服務。
* 電腦 toorun Deis 用戶端工具。 您可以使用本機電腦或虛擬機器。 您可以執行這些工具在幾乎所有 Linux 散發套件，但是 hello 下列指示使用 Ubuntu。

## <a name="provision-hello-cluster"></a>佈建 hello 叢集
在本節中，您將使用[Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) hello 開放原始碼儲存機制中的範本[azure-快速入門範本](https://github.com/Azure/azure-quickstart-templates)。 首先，您將會複製下 hello 範本。 然後，您會建立用於驗證的新 SSH 金鑰組。 接下來，您會為叢集設定新的識別碼。 最後，您會使用 hello 殼層指令碼或 hello PowerShell 指令碼 tooprovision hello 叢集。

1. 複製 hello 儲存機制： [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates)。
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. 請移 toohello 範本資料夾：
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. 使用 ssh-keygen 建立新的 SSH 金鑰組：
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. 產生使用 hello 上方私密金鑰的憑證：
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. 跳過[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate 新叢集的權杖，看起來類似：
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   每個 CoreOS 叢集中需要 toohave 來自這項免費服務的唯一權杖。 如需詳細資訊，請參閱 [CoreOS 文件](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) 。
6. 修改 hello**雲端 config.yaml**檔案 tooreplace hello 現有**探索**權杖與 hello 新權杖：
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. 修改 hello **azuredeploy parameters.json**檔案： hello 開啟您在文字編輯器中的步驟 4 中建立的憑證。 複製之間的所有文字`----BEGIN CERTIFICATE-----`和`-----END CERTIFICATE-----`到 hello **sshKeyData** （您將需要 tooremove 所有新行字元） 的參數。
8. 修改 hello **newStorageAccountName**參數。 這是 hello VM OS 磁碟的儲存體帳戶。 此帳戶名稱中有全域唯一 toobe。
9. 修改 hello **publicDomainName**參數。 這會成為 hello 與 hello 負載平衡器的公用 IP 相關聯的 DNS 名稱的一部分。 hello 最終的 FQDN 必須 hello 格式*此參數值*。*[地區]*。 cloudapp.azure.com。例如，如果您 hello 名稱指定為 deishbai32，和 hello 資源群組是已部署的 toohello 美國西部地區，則最後的 hello FQDN tooyour 負載平衡器會 deishbai32.westus.cloudapp.azure.com。
10. 儲存 hello 參數檔案。 然後佈建使用 Azure PowerShell hello 叢集：
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    或 Azure CLI：
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. Hello 資源群組已佈建之後，您可以在 Azure 傳統入口網站中看到 hello 群組中的所有 hello 資源。 中所示 hello 下列螢幕擷取畫面，hello 資源群組包含具有三個 Vm 的虛擬網路，這是加入 toohello 相同可用性設定組。 hello 群組也包含負載平衡器，其具有相關聯的公用 IP。
    
    ![hello 佈建在 Azure 傳統入口網站上的資源群組](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a>Hello 用戶端安裝
您需要**deisctl** toocontrol 您 Deis 叢集。 雖然 deisctl 自動安裝在所有 hello 叢集節點中，是很好的作法 toouse deisctl 在不同的系統管理電腦上。 此外，因為所有節點，都皆只有私用 IP 位址，您將需要 toouse 透過 hello 負載平衡器，其具有公用 IP，tooconnect toohello 節點機器的 SSH 通道。 hello 下面是 hello deisctl 個別 Ubuntu 實體或虛擬機器上所設定的步驟。

1. 安裝 deisctl：mkdir deis
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. 加入私用金鑰 toossh 代理程式：
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. 設定 deisctl：
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

hello 範本會定義將 2223 tooinstance 1，對應的輸入的 NAT 規則 2224 tooinstance 2 和 2225 tooinstance 3。 這是使用 hello deisctl 工具提供備援性。 您可以在 Azure 傳統入口網站檢查這些規則：

![Hello 負載平衡器上的 NAT 規則](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> 目前 hello 範本只支援 3 個節點的叢集。 這是因為 Azure 資源管理員範本 NAT 規則定義不支援迴圈與法的限制。
> 
> 

## <a name="install-and-start-hello-deis-platform"></a>安裝並啟動 hello Deis 平台
現在您可以使用 deisctl tooinstall 並啟動 hello Deis 平台：

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> 起始 hello 平台需要一些時間 （最多可達 10 分鐘）。 特別是，啟動 hello builder 服務可能需要很長的時間。 有時需要花幾次嘗試 toosucceed: hello 作業看起來 toohang，如果嘗試輸入`ctrl+c`toobreak 執行 hello 命令和重試。
> 
> 

您可以使用`deisctl list`tooverify 如果所有服務都執行：

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

恭喜！ 您現在有在 Azure 上執行的 Deis 了！ 接下來，讓我們來部署到應用程式 toosee hello 叢集動作中的範例。

## <a name="deploy-and-scale-a-hello-world-application"></a>部署及調整 Hello World 應用程式
hello 下列步驟顯示如何 toodeploy"Hello World"到應用程式 toohello 叢集。 hello 步驟為基礎[Deis 文件](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles)。

1. Hello 路由網狀結構 toowork 正常運作，您將需要 toohave 萬用字元的記錄為指向 toohello 公用 IP hello 負載平衡器的網域。 hello 下列螢幕擷取畫面顯示 hello A 記錄，如範例的網域註冊 GoDaddy 上：
   
    ![Godaddy A 記錄](./media/deis-cluster/go-daddy.png)
   
   <p />
2. 安裝 deis：
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. 建立新的 SSH 金鑰，然後加入 hello 公用金鑰 tooGitHub （當然，您也可以重複使用現有的金鑰）。 toocreate 新的 SSH 金鑰組，使用：
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. 加入 id_rsa.pub 或您的選擇 tooGitHub 的 hello 公開金鑰。 您可以使用 SSH 金鑰組態畫面中的 hello 加入 SSH 金鑰 按鈕：
   
   ![GitHub 金鑰](./media/deis-cluster/github-key.png)
   
   <p />
5. 註冊新的使用者：
   
        deis register http://deis.[your domain]
   <p />
6. 新增 hello SSH 金鑰：
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. 建立應用程式。
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.hello git 推送將會觸發將需要花幾分鐘的時間 Docker 映像 toobe 建置與部署。 我的經驗，有時候，步驟 10 （Pushing 映像 tooprivate 儲存機制） 可能會停止回應。 當發生這種情況時，您可以停止 hello 程序，移除 hello 應用程式使用 ' deis 應用程式： 終結 – <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind 出 hello 應用程式的名稱。 如果一切運作，您應該會看到在命令輸出的 hello 結尾 hello 下列類似：
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. 請確認 hello 應用程式是否正在運作：
   
        curl -S http://[your application name].[your domain]
   您應該會看到：
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. 標尺 hello 應用程式 too3 執行個體：
    
        deis scale cmd=3
    <p />
11. 或者，您可以使用 deis 資訊 tooexamine 詳細資料，您的應用程式。 hello 下列輸出會從我的應用程式部署：
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a>後續步驟
本文逐步進行所有 hello 步驟 tooprovision 新 Deis 作業您在 Azure 中使用 Azure Resource Manager 範本上的叢集。 hello 範本支援備援連線，以及負載平衡提供部署應用程式的工具。 hello 範本也可避免成員在節點上，這可以節省寶貴的公用 IP 資源，並提供更安全的環境 toohost 應用程式中使用公用 Ip。 toolearn 詳細資訊，請參閱下列文章 hello:

[Azure Resource Manager 概觀][resource-group-overview]  
[如何 toouse hello Azure CLI][azure-command-line-tools]  
[搭配使用 Azure PowerShell 與 Azure Resource Manager][powershell-azure-resource-manager]  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
