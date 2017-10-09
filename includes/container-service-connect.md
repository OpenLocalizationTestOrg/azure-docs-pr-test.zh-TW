# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a>進行遠端連線 tooa Kubernetes、 DC/作業系統，或 Docker Swarm 叢集
建立 Azure 容器服務叢集之後, 您會需要 tooconnect toohello 叢集 toodeploy 和管理工作負載。 本文說明 tooconnect toohello 主要 VM 的 hello 從遠端電腦的叢集化。 

hello Kubernetes、 DC/OS，和 Docker Swarm 叢集提供本機 HTTP 端點。 如 Kubernetes，此端點安全地公開所在 hello 網際網路，而且您可以藉由執行 hello 存取`kubectl`命令列工具，從任何連線網際網路的電腦。 

DC/OS 和 Docker Swarm，我們建議您從本機電腦 toohello 叢集管理系統建立安全殼層 (SSH) 通道。 建立 hello 通道之後，您可以執行使用 hello HTTP 端點和檢視 hello orchestrator 的 web 介面 （如果有的話） 從您的本機系統的命令。 

## <a name="prerequisites"></a>必要條件

* [在 Azure Container Service 中部署](../articles/container-service/dcos-swarm/container-service-deployment.md)的 Kubernetes、DC/OS 或 Docker Swarm 叢集。
* SSH RSA 私密金鑰檔案，在部署期間對應 toohello 公用金鑰加入的 toohello 叢集。 這些命令會假設該 hello SSH 私密金鑰是在`$HOME/.ssh/id_rsa`您電腦上。 如需詳細資訊，請參閱 [macOS 及 Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) 或 [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) 的相關指示。 如果 hello SSH 連線沒有運作，您可能需要過[重設 SSH 金鑰](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)。

## <a name="connect-tooa-kubernetes-cluster"></a>Tooa Kubernetes 叢集連線

請遵循這些步驟 tooinstall 及設定`kubectl`您電腦上。

> [!NOTE] 
> 在 Linux 或 macOS，您可能需要 toorun hello 命令中使用此區段`sudo`。
> 

### <a name="install-kubectl"></a>安裝 kubectl
其中一種方式 tooinstall 此工具為 toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 命令。 此命令時，請確定 toorun 您[安裝](/cli/azure/install-az-cli2)hello 最新的 Azure CLI 2.0 和登入 Azure 帳戶 tooan (`az login`)。

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

或者，您可以最新版本下載 hello`kubectl`用戶端直接從 hello [Kubernetes 釋放頁面](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md)。 如需詳細資訊，請參閱[安裝和設定 kubectl](https://kubernetes.io/docs/tasks/kubectl/install/)。

### <a name="download-cluster-credentials"></a>下載叢集認證
一旦`kubectl`安裝，您需要 toocopy hello 叢集認證 tooyour 機器。 其中一種方式 toodo get hello 認證是以 hello`az acs kubernetes get-credentials`命令。 傳遞 hello hello 資源群組名稱和 hello hello 容器服務資源名稱：

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

這個命令會下載太 hello 叢集認證`$HOME/.kube/config`，其中`kubectl`toobe 位於也需要它。

或者，您可以使用`scp`toosecurely 複製 hello 檔案從`$HOME/.kube/config`hello 主要 VM tooyour 本機電腦上。 例如：

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

如果您是在 Windows 上，您可以在 Windows、 hello PuTTy 安全的檔案複製用戶端或類似的工具上的 Ubuntu 上使用 Bash。

### <a name="use-kubectl"></a>使用 kubectl

一旦`kubectl`設定，藉由列出 hello 叢集中的節點測試 hello 連線：

```bash
kubectl get nodes
```

您可以嘗試其他 `kubectl` 命令。 例如，您可以檢視 hello Kubernetes 儀表板。 首先，執行 proxy toohello Kubernetes API 伺服器：

```bash
kubectl proxy
```

hello Kubernetes UI 現在已經提供： `http://localhost:8001/ui`。

如需詳細資訊，請參閱 hello [Kubernetes 快速入門](http://kubernetes.io/docs/user-guide/quick-start/)。

## <a name="connect-tooa-dcos-or-swarm-cluster"></a>Tooa DC/OS 或群集叢集連線

toouse hello DC/OS 和 Docker Swarm 叢集部署 Azure 容器服務，請遵循這些指示 toocreate SSH 通道，從本機 Linux、 macOS、 或 Windows 系統。 

> [!NOTE]
> 這些是透過 SSH 通道傳送 TCP 流量的指示。 您也可以使用其中一個 hello 內部叢集管理系統，開始的互動式的 SSH 工作階段，但我們不建議您這樣做。 直接使用內部系統可能會不小心變更設定。  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a>在 Linux 或 macOS 上建立 SSH 通道
您在執行 Linux 或 macOS 上建立的 SSH 通道時的 hello 第一件事是 toolocate hello 公開 DNS 名稱的 hello 負載平衡的主機。 請遵循下列步驟：


1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽包含您的容器服務叢集 toohello 資源群組。 展開 hello 資源群組，會顯示每個資源。 

2. 按一下 hello**容器服務**資源，然後按一下**概觀**。 hello**主要 FQDN**叢集出現在下方的 hello **Essentials**。 儲存這個名稱供稍後使用。 

    ![公用 DNS 名稱](./media/container-service-connect/pubdns.png)

    或者，執行 hello`az acs show`容器服務命令。 尋找 hello**主要設定檔： fqdn** hello 命令輸出中的屬性。

3. 現在開啟 shell，並執行 hello`ssh`命令藉由指定下列值的 hello: 

    **LOCAL_PORT**為 hello 以 hello 通道 tooconnect hello 服務端上的 TCP 通訊埠。 對於群集，來設定此 too2375。 DC/OS，設定此 too80。 
    **REMOTE_PORT**是您想 tooexpose hello 端點的 hello 連接埠。 針對 Swarm，使用連接埠 2375。 若為 DC/OS，則使用連接埠 80。  
    **使用者名稱**是當您部署的 hello 叢集時所提供的 hello 使用者名稱。  
    **DNSPREFIX**是您部署 hello 叢集時，您所提供的 hello DNS 前置詞。  
    **區域**是資源群組所在的 hello 區域。  
    **PATH_TO_PRIVATE_KEY** [選擇性] 是 hello 路徑 toohello 對應私密金鑰 toohello 建立 hello 叢集時所提供的公開金鑰。 使用此選項以 hello`-i`旗標。

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > hello SSH 連接埠是 2200年，而且不 hello 標準通訊埠 22。 在具有一個以上的主要 VM 的叢集中，這會是 hello 連接埠 toohello 第一個主要 VM。
  > 

  hello 命令會傳回沒有輸出。

請參閱 DC/OS 和群集 hello 下列各節中的 hello 範例。    

### <a name="dcos-tunnel"></a>DC/OS 通道
tooopen DC/OS 端點通道執行 hello 下列類似的命令：

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> 確定您沒有另一個繫結連接埠 80 的本機處理序。 如有需要，您可以指定連接埠 80 以外的本機連接埠 (例如連接埠 8080)。 不過，當您使用此連接埠時，某些網頁 UI 連結可能無法運作。
>

您現在可以從您的本機系統，透過 hello 下列 Url （假設本機連接埠 80） 存取 hello DC/OS 端點：

* DC/OS： `http://localhost:80/`
* Marathon： `http://localhost:80/marathon`
* Mesos： `http://localhost:80/mesos`

同樣地，您可能會達到每個應用程式，透過這個通道的 hello rest Api。

### <a name="swarm-tunnel"></a>Swarm 通道
tooopen 通道 toohello 群集結束點執行類似 hello 下列命令：

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> 確定您沒有另一個繫結連接埠 2375 的本機處理序。 例如，如果您在本機執行 hello Docker 精靈，它會設定預設 toouse 連接埠 2375年。 如有需要，您可以指定連接埠 2375 以外的本機連接埠。
>

現在您可以存取您的本機系統上使用 hello Docker 命令列介面 (Docker CLI) 的 hello Docker Swarm 叢集。 如需安裝指示，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。

設定您 DOCKER_HOST 環境變數 toohello 您設定 hello 通道的本機連接埠。 

```bash
export DOCKER_HOST=:2375
```

該通道 toohello Docker Swarm 叢集中執行 Docker 命令。 例如：

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a>在 Windows 上建立 SSH 通道
在 Windows 上建立 SSH 通道有很多選項。 如果您在 Ubuntu 上執行 Bash Windows 或類似的工具上，您可以遵循 hello SSH 通道指示 macOS 和 Linux 適用的本文稍早所示。 或者在 Windows 上，本章節描述如何 toouse PuTTY toocreate hello 通道。

1. [下載 PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows 系統。

2. 執行 hello 應用程式。

3. 輸入主機名稱所組成的 hello 叢集系統管理員使用者名稱和 hello hello 叢集中的第一個主要的 hello 公開 DNS 名稱。 hello**主機名稱**看起來太`azureuser@PublicDNSName`。 輸入 hello 2200**連接埠**。

    ![PuTTY 組態 1](./media/container-service-connect/putty1.png)

4. 選取 [SSH] > [Auth]。新增路徑 tooyour 私密金鑰檔 （.ppk 格式） 進行驗證。 您可以使用一種工具，例如[Ssh-keygen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate 這個檔案從 hello SSH 金鑰的使用的 toocreate hello 叢集。

    ![PuTTY 組態 2](./media/container-service-connect/putty2.png)

5. 選取**SSH > 通道**和設定轉送連接埠的 hello 下列：

    * **來源連接埠：**DC/OS 使用 80 或 Swarm 使用 2375。
    * **目的地：** DC/OS 使用 localhost:80 或 Swarm 使用 localhost:2375。

    下列範例中的 hello 已針對 DC/OS，，但看起來類似的 Docker Swarm。

    > [!NOTE]
    > 建立此通道時，連接埠 80 不得使用中。
    > 

    ![PuTTY 組態 3](./media/container-service-connect/putty3.png)

6. 當您完成時，按一下 **工作階段 > 儲存**toosave hello 連接組態。

7. tooconnect toohello PuTTY 工作階段中，按一下**開啟**。 當您連線時，您可以看到 hello hello PuTTY 事件記錄檔中的連接埠設定。

    ![PuTTY 事件記錄檔](./media/container-service-connect/putty4.png)

您設定 DC/OS hello 通道之後，您可以存取 hello 相關上的端點：

* DC/OS： `http://localhost/`
* Marathon： `http://localhost/marathon`
* Mesos： `http://localhost/mesos`

您的 Docker Swarm 設定 hello 通道之後，開啟您的 Windows 設定 tooconfigure 系統環境變數，名為`DOCKER_HOST`值是`:2375`。 然後，您可以透過 Docker CLI hello 存取 hello 群集叢集。

## <a name="next-steps"></a>後續步驟
部署及管理叢集中的容器：

* [使用 Azure Container Service 和 Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [使用 Azure Container Service 和 DC/OS](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [使用 hello Azure 容器服務和 Docker Swarm](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

