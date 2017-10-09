# <a name="scale-agent-nodes-in-a-container-service-cluster"></a>調整 Container Service 叢集中的代理程式節點
之後[部署 Azure 容器服務叢集](../articles/container-service/dcos-swarm/container-service-deployment.md)，您可能需要的代理程式節點的 toochange hello 數目。 例如，您可能需要更多代理程式，以便可以執行更多的容器應用程式或執行個體。 

您可以使用 hello Azure 入口網站來變更 hello DC/OS、 Docker Swarm，或 Kubernetes 叢集中的代理程式節點的數目或 hello Azure CLI 2.0。 

## <a name="scale-with-hello-azure-portal"></a>調整以 hello Azure 入口網站

1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽**容器服務**，然後按一下您想 toomodify hello 容器服務。
2. 在 hello**容器服務**刀鋒視窗中，按一下 **代理程式**。
3. 在**VM 計數**，輸入想要的 hello 代理程式節點的數目。

    ![調整 hello 入口網站中的集區](./media/container-service-scale/container-service-scale-portal.png)

4. toosave hello 組態中，按一下 **儲存**。

## <a name="scale-with-hello-azure-cli-20"></a>調整以 hello Azure CLI 2.0

請確定您[安裝](/cli/azure/install-az-cli2)hello 最新的 Azure CLI 2.0 和登入 tooan azure 帳戶 (`az login`)。

### <a name="see-hello-current-agent-count"></a>請參閱 hello 目前的代理程式計數
代理程式目前的 toosee hello 數目 hello 叢集中執行 hello`az acs show`命令。 這會顯示 hello 叢集設定。 例如，下列命令會顯示 hello 名為 hello 容器服務的組態來 hello `containerservice-myACSName` hello 資源群組中`myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

hello 命令會傳回 hello 代理程式數目的 hello`Count`值下`AgentPoolProfiles`。

### <a name="use-hello-az-acs-scale-command"></a>使用 hello az acs 小數位數的命令
toochange hello 代理程式節點數目，執行 hello`az acs scale`命令和提供 hello**資源群組**，**容器服務名稱**，並想要的 hello**新代理程式計數**. 藉由使用較少或更高的數字，即可分別相應減少或相應增加。

例如，在上一個叢集 too10 hello，代理程式的 toochange hello 數目輸入 hello 下列命令：

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

hello Azure CLI 2.0 傳回 JSON 字串，代表 hello 新服務的組態 hello 容器，包括 hello 新代理程式計數。

如需更多的命令選項，請執行 `az acs scale --help`。

## <a name="scaling-considerations"></a>調整考量

* hello 代理程式節點的數目必須是介於 1 到 100 (含) 之間。 

* 核心配額可以限制 hello 叢集中的代理程式節點的數目。

* 代理程式節點的縮放作業是套用的 tooan Azure 虛擬機器規模集包含 hello 代理程式集區。 在 DC/OS 叢集中，只有代理程式節點 hello 私用的集區中縮放 hello 本文中所顯示的作業。

* 根據您在叢集中部署的 hello orchestrator，您可以分開調整 hello hello 叢集上執行的容器的執行個體數目。 例如，在 DC/OS 叢集中，使用 hello[馬拉松 UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello 數目的容器應用程式執行個體。

* 目前並不支援在容器服務叢集中自動調整代理程式節點。

## <a name="next-steps"></a>後續步驟
* 請參閱[更多範例](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md)，以了解如何搭配使用 Azure CLI 2.0 命令與 Azure Container Service。
* 深入了解 Azure Container Service 中的 [DC/OS 代理程式集區](../articles/container-service/dcos-swarm/container-service-dcos-agents.md)。

