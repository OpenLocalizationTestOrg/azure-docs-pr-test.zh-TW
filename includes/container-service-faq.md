# <a name="container-service-frequently-asked-questions"></a>容器服務常見問題集

## <a name="orchestrators"></a>Orchestrator

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Azure Container Service 上支援哪些容器 Orchestrator？ 

支援開放原始碼的 DC/OS、Docker Swarm 和 Kubernetes。 如需詳細資訊，請參閱 hello[概觀](../articles/container-service/kubernetes/container-service-intro-kubernetes.md)。
 
### <a name="do-you-support-docker-swarm-mode"></a>是否支援 Docker Swarm 模式？ 

目前不支援群集模式，但在 hello 服務藍圖。 

### <a name="does-azure-container-service-support-windows-containers"></a>Azure Container Service 是否支援 Windows 容器？  

目前支援 Linux 容器使用所有 Orchestrator 。 支援 Windows 容器使用 Kubernetes 處於預覽階段。

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>是否建議在 Azure Container Service 中使用特定 Orchestrator？ 
我們一般不建議使用特定 Orchestrator。 如果您使用其中一個支援的 hello orchestrators 經驗，您可以套用該 Azure 容器服務中的體驗。 不過，資料趨勢表明，DC/OS 已在生產環境中證明適用於巨量資料和 IoT 工作負載，Kubernetes 適合用於雲端原生的工作負載，而 Docker Swarm 則眾所皆知可與 Docker 工具整合且容易上手。

根據您的情況，您也可以使用其他 Azure 服務建置並管理自訂的容器解決方案。 這些服務包括[虛擬機器](../articles/virtual-machines/linux/overview.md)、[Service Fabric](../articles/service-fabric/service-fabric-overview.md)、[Web Apps](../articles/app-service-web/app-service-web-overview.md) 和 [Batch](../articles/batch/batch-technical-overview.md)。  

### <a name="what-is-hello-difference-between-azure-container-service-and-acs-engine"></a>Hello Azure 容器服務與 ACS 引擎之間的差異為何？ 
Azure 容器服務是 hello Azure 入口網站、 Azure 命令列工具，以及 Azure 應用程式開發介面中的功能，SLA 為基礎的 Azure 服務。 hello 服務可讓您 tooquickly 實作和管理執行標準容器的協調流程工具以相對較小的數字的組態選項的叢集。 

[ACS 引擎](http://github.com/Azure/acs-engine)是開放原始碼專案，可讓電源使用者 toocustomize hello 叢集設定每個層級。 此功能 tooalter hello 設定基礎結構及軟體表示我們 ACS 引擎提供任何 SLA。 支援是透過 hello GitHub 上的開放原始碼專案，而不是透過官方 Microsoft 管道進行處理。 

## <a name="cluster-management"></a>叢集管理

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>如何為叢集建立 SSH 金鑰？

您可以使用標準工具，在您的作業系統 toocreate SSH RSA 公開 / 私密金鑰組針對 hello Linux 虛擬機器進行驗證為您的叢集。 如需步驟，請參閱 hello [OS X 和 Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md)或[Windows](../articles/virtual-machines/linux/ssh-from-windows.md)指引。 

如果您使用[Azure CLI 2.0 命令](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md)toodeploy 容器的叢集服務、 SSH 金鑰會自動產生，供您的叢集。

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>如何為 Kubernetes 叢集建立服務主體？

Azure Active Directory 服務主體的識別碼和密碼也會需要的 toocreate Kubernetes 叢集 Azure 容器服務中。 如需詳細資訊，請參閱[hello Kubernetes 叢集的服務主體相關](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md)。

如果您使用[Azure CLI 2.0 命令](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md)toodeploy Kubernetes 叢集，服務主體的認證會自動產生，供您的叢集。

### <a name="how-large-a-cluster-can-i-create"></a>可以建立多大的叢集？
您可以建立含有 1、3 或 5 個主要節點的叢集。 您可以選擇向上 too100 代理程式節點。

> [!IMPORTANT]
> 較大叢集以及根據 hello 您選擇用於節點的 VM 大小而定，您可能需要 tooincrease hello 核心配額，您的訂用帳戶中。 toorequest 增加配額，開啟[線上客戶支援要求](../articles/azure-supportability/how-to-create-azure-support-request.md)不收費。 如果您使用 [Azure 免費帳戶](https://azure.microsoft.com/free/)，您只能使用有限數目的 Azure 計算核心。
> 

### <a name="how-do-i-increase-hello-number-of-masters-after-a-cluster-is-created"></a>如何建立叢集之後增加母片 hello 的數目？ 
一旦建立 hello 叢集後，hello 母片數目固定的無法變更。 Hello hello 叢集建立期間，您應該在理想情況下選取多個主機的高可用性。

### <a name="how-do-i-increase-hello-number-of-agents-after-a-cluster-is-created"></a>如何建立叢集之後增加 hello 代理程式數目？ 
您可以調整 hello 叢集中的代理程式的 hello 數目使用 hello Azure 入口網站或命令列工具。 請參閱[調整 Azure Container Service 叢集](../articles/container-service/kubernetes/container-service-scale.md)。

### <a name="what-are-hello-urls-of-my-masters-and-agents"></a>Hello my 隊長和代理程式的 Url 有哪些？ 
hello Url 的 Azure 容器服務中的資源會根據 hello 叢集 DNS 名稱前置詞，您提供並 hello hello 您選擇部署的 Azure 地區的名稱。 例如，hello 主要節點的 hello 完整的網域名稱 (FQDN) 是這種形式的：

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

您可以為您的叢集 hello Azure 入口網站、 hello Azure 資源總管 中或其他 Azure tools 中找到常用的 Url。

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>如何分辨在我的叢集中執行哪個 Orchestrator 版本？

* DC/OS： 請參閱 hello [Mesosphere 文件](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* Docker Swarm：請執行 `docker version`
* Kubernetes：請執行 `kubectl version`

### <a name="how-do-i-upgrade-hello-orchestrator-after-deployment"></a>如何在部署後升級 hello orchestrator？

目前，Azure 容器服務不會提供您在叢集部署的 hello orchestrator 工具 tooupgrade hello 版本。 如果 Container Service 支援較新版本，您可以部署新的叢集。 在有可用的 tooupgrade 叢集的就地，另一個選項是 toouse orchestrator 特定工具。 例如，請參閱 [DC/OS 升級](https://dcos.io/docs/1.8/administration/upgrading/)。
 
### <a name="where-do-i-find-hello-ssh-connection-string-toomy-cluster"></a>哪裡可以找到 hello SSH 連線字串 toomy 叢集？

在 hello Azure 入口網站，或使用 Azure 命令列工具，您可以找到 hello 連接字串。 

1. 在 hello 入口網站中，瀏覽 toohello hello 叢集部署的資源群組。  

2. 按一下**概觀**按一下 hello 連結**部署**下**Essentials**。 

3. 在 hello**部署歷程記錄**刀鋒視窗中，按一下名稱開頭的 hello 部署**microsoft acs**後面部署日期。 範例︰microsoft-acs-201701310000。  

4. 在 hello**摘要**頁面的 **輸出**，便會提供數個叢集的連結。 **SSHMaster0**提供 SSH 連線字串 toohello 第一個主要容器服務叢集中。 

如先前所述，您也可以使用 Azure tools toofind hello hello 主機的 FQDN。 建立 SSH 連線 toohello 主要使用 hello hello master 和 hello 建立 hello 叢集時，您所指定的使用者名稱的 FQDN。 例如：

```bash
ssh userName@masterFQDN –A –p 22 
```

如需詳細資訊，請參閱[連接 tooan Azure 容器服務叢集](../articles/container-service/kubernetes/container-service-connect.md)。

## <a name="next-steps"></a>後續步驟

* [深入了解](../articles/container-service/kubernetes/container-service-intro-kubernetes.md) Azure Container Service。
* 部署使用 hello 的容器服務叢集[入口網站](../articles/container-service/dcos-swarm/container-service-deployment.md)或[Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md)。
