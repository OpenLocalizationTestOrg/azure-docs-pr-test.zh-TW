Azure 雲端解決方案建置於虛擬機器 (實體電腦硬體的模擬) 上，而虛擬機器可靈活封裝軟體部署，並且比實體硬體更能強化資源的彙總。 [Docker](https://www.docker.com)容器和 hello docker 生態系統有大幅擴充的 hello 方式，您可以開發、 出貨，及管理軟體發佈。 在容器中的應用程式程式碼隔離從 hello 主機 VM，並在其他容器 hello 相同的 VM。 這種隔離方式可讓您擁有更多的開發和部署靈活度。

Azure 會提供下列 Docker 值 hello:

* [許多](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)[不同](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)方式 toocreate Docker 容器 toosuit 為您的情況下裝載
* hello [Azure 容器服務](https://azure.microsoft.com/documentation/services/container-service/)會建立使用像是 orchestrators 容器主機的叢集**馬拉松**和**廣域**。
* [Azure 資源管理員](../articles/azure-resource-manager/resource-group-overview.md)和[資源群組範本](../articles/resource-group-authoring-templates.md)toosimplify 部署及更新複雜分散式應用程式
* 能與大量專屬和開放原始碼組態管理工具進行整合

而且因為您可以透過程式設計方式建立 Vm 和 Linux 容器在 Azure 上，您也可以使用 VM 和容器*協調流程*工具 toocreate 群組虛擬機器 (Vm) 及兩個 Linux 內的 toodeploy 應用程式容器並立即[Windows 容器](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)。

這篇文章不只會討論這些高層級的概念，它也包含連結 toomore 資訊、 教學課程，噸和產品相關 toocontainer 和叢集的使用方式，在 Azure 上。 如果您知道所有，並只是想 hello 連結時，它們直接在[容器所使用的工具](#tools-for-working-with-azure-vms-and-containers)。

## <a name="hello-difference-between-virtual-machines-and-containers"></a>hello 虛擬機器與容器之間的差異
虛擬機器是在 [Hypervisor](http://en.wikipedia.org/wiki/Hypervisor)提供的獨立硬體虛擬化環境內執行。 在 Azure 中，hello[虛擬機器](https://azure.microsoft.com/services/virtual-machines/)為您的服務控制代碼： 您建立虛擬機器選擇 hello 作業系統並設定&mdash;或上傳自訂 VM 映像。 虛擬機器會經得起時間考驗"戰鬥強行寫入 」 技術，而且有許多工具，它們包含可用 toomanage hello 作業系統和應用程式。  Hello 主機作業系統中，會隱藏在 VM 中的應用程式。 Hello 的觀點的應用程式或在 VM 上的使用者，從 hello VM 會出現 toobe 自發的實體電腦。

[Linux 容器](http://en.wikipedia.org/wiki/LXC)而且所建立及裝載使用 docker 工具不會使用 hypervisor tooprovide 隔離。 透過容器，hello 容器主機會使用處理序和 hello Linux 核心 tooexpose toohello 容器檔案系統隔離功能，其應用程式、 特定的核心功能與它自己的隔離的檔案系統。 Hello 觀點來看的容器內執行的應用程式，從 hello 會顯示容器 toobe 唯一的作業系統執行個體。 包含在其中的應用程式看不見處理程序或其容器以外的任何其他資源。

Docker 容器中使用的資源遠少於 VM 中使用的資源。 Docker 容器會採用應用程式隔離和執行的模型，不會共用 hello 核心的 hello Docker 主機。 hello 容器有太多較低的磁碟使用量因為它不會包含 hello 整個作業系統。 啟動時間和所需磁碟空間大幅低於 VM。
Windows 容器所提供用於在 Windows 執行的應用程式相同的優點，做為 Linux 容器 hello。 Windows 容器支援 hello Docker 映像格式與 Docker 的 API，但也可以管理這些使用 PowerShell。 Windows 容器可以使用二種容器執行階段：Windows 伺服器容器和 Hyper-V 容器。 Hyper-V 容器將每個容器裝載在高度最佳化的 VM，以提供額外的隔離。 關於 Windows 容器，請參閱的 toolearn[關於 Windows 容器](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)。 在 Azure 中，Windows 容器啟動的 tooget 深入了解如何太[部署 Azure 容器服務叢集](../articles/container-service/dcos-swarm/container-service-deployment.md)。

## <a name="what-are-containers-good-for"></a>容器適用的情況？

容器可以提升︰

* 開發和廣泛共用 hello 速度應用程式程式碼
* hello 速度和您可以測試應用程式的信心
* hello 速度和可以部署應用程式的信心

容器是在容器主機 (&mdash;作業系統) 上執行，而在 Azure 中是在 Azure 虛擬機器中執行。 即使您已經愛上 hello 概念的容器，您仍然要 tooneed 主控 hello 容器的 VM 基礎結構，但 hello 好處是容器並不在意哪些 VM 上執行 （雖然 hello 容器是否要在 Linux 或 Windows執行環境很重要，例如）。


## <a name="what-are-containers-good-for"></a>容器適用的情況？
它們是最適合用於許多項目，但它們建議&mdash;一樣[Azure 雲端服務](https://azure.microsoft.com/services/cloud-services/)和[Azure Service Fabric](../articles/service-fabric/service-fabric-overview.md)&mdash;hello 建立單一服務，微服務導向分散式應用程式，應用程式的設計根據多個小型、 可組合的部分而非較大、 更強固結合元件。

尤其是對於像 Azure 這種您在需要時可以租用 VM 的公用雲端環境，特別適合。 您不只可以獲得隔離、快速的部署以及協調流程工具，還能更有效率決定應用程式基礎結構。

例如，您目前有一個部署，有一個大型、高可用性的分散式應用程式，由 9 個 Azure VM 組成。 如果 hello 這個應用程式元件可以部署在容器中，您可能會是能 toouse 只有 4 個 Vm，並部署應用程式元件的備援和負載平衡的 20 容器內。

這只是範例，當然，但如果您的案例中，您可以執行這項操作，您可以調整 toousage 失效的多個容器，而不是多個 Azure Vm，並使用 hello 比先前更有效率地剩餘整體的 CPU 負載。

此外，還有許多情況不要不 tooa microservices 方法;您將最知道是否 microservices 和容器會協助您。

### <a name="container-benefits-for-developers"></a>容器對開發人員的優點
一般情況下，很容易 toosee 容器技術是轉送的步驟，但有更具體的好處。 讓我們 Docker 容器的 hello 的範例。 本主題將不深入了解深 Docker 現在 (讀取[Docker 是什麼？](https://www.docker.com/whatisdocker/)該劇本，或[維基百科](http://wikipedia.org/wiki/Docker_%28software%29))，但 Docker 和其生態系統提供極大的優點 tooboth 開發人員和 IT專業人員。

快速，因為它優先於所有可使用簡單的 Linux 和 Windows 容器時，開發人員將採取 tooDocker 容器：

* 他們可以使用簡單、 累加命令 toocreate 固定的映像的簡單 toodeploy，並可自動建置使用 dockerfile 這些映像
* 它們可共用這些映像，輕鬆地使用簡單， [git](https://git-scm.com/)-樣式推入和提取命令太[公用](https://registry.hub.docker.com/)或[私用 docker 登錄](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* 開發人員可以考慮隔離應用程式元件，而不是電腦
* 開發人員可以使用大量的工具，了解 docker 容器和不同的基本映像

### <a name="container-benefits-for-operations-and-it-professionals"></a>容器對作業人員和 IT 專業人員的優點
IT 作業專業人員也受益於 hello 組合容器和虛擬機器。

* 內含的服務與 VM 主機執行環境隔離
* 內含的程式碼可驗證為完全相同
* 內含的服務可以啟動、停止，以及在開發、測試和生產環境之間快速移動

這些等功能&mdash;而且有多個&mdash;激發專業人員的資訊技術組織有的調整資源中的 hello 作業的位置建立的企業&mdash;包括單純的處理能力&mdash;toohello 工作需要的 toonot 只停留在商務，但提升客戶滿意度而抵達。 小型企業、 Isv 和啟動沒有完全 hello 相同需求，但是它們可能會描述它以不同的方式。

## <a name="what-are-virtual-machines-good-for"></a>虛擬機器適用的情況？
虛擬機器提供雲端運算的 hello 骨幹和，並不會變更。 如果虛擬機器啟動速度更慢、 較大的磁碟使用量，而且不會將直接 tooa microservices 架構，它們是否有非常重要的優點：

1. 虛擬機器預設能為主機電腦提供更穩固的預設安全性保護
2. 虛擬機器支援任何主要的作業系統和應用程式組態
3. 虛擬機器具備存在已久的工具生態系統進行命令與控制
4. 它們提供 hello 執行環境 toohost 容器

hello 最後一個項目很重要，因為包含的應用程式仍然需要特定作業系統和 CPU 類型，視 hello 呼叫 hello 應用程式會進行。 它是您在 Vm 上安裝的容器，因為它們包含您想要 toodeploy; hello 應用程式的重要 tooremember容器不會取代 Vm 或作業系統。

## <a name="high-level-feature-comparison-of-vms-and-containers"></a>VM 和容器的高階功能比較
hello 下表描述在極高功能層級的 hello 種類的差異，&mdash;沒有額外的工作量&mdash;Linux Vm 之間存在的容器。 請注意，某些功能可能增加或減少需要根據自己的應用程式需要而且，如同所有軟體，額外的工作提供增加的功能支援，尤其是在 hello 區域的安全性。

| 功能 | VM | 容器 |
|:--- | --- | --- |
| 「預設」安全性支援 |tooa 更大程度 |tooa 稍微較低刻度 |
| 磁碟上需有記憶體 |整套作業系統及應用程式 |僅限應用程式需求 |
| 時間佔用 toostart |相當長的時間：作業系統啟動和應用程式載入 |大幅縮短： 只因為核心已在執行中，應用程式需要 toostart |
| 可攜性 |經過適當準備則可攜 |在映像格式內可攜；通常較小 |
| 映像自動化 |根據 OS 和應用程式有很大的差異 |[Docker 登錄](https://registry.hub.docker.com/)；其他 |

## <a name="creating-and-managing-groups-of-vms-and-containers"></a>建立和管理 VM 群組和容器群組
到目前為止，任何架構師、開發人員或 IT 作業專家可能會想：「我如果可以自動化所有這些事物，這就真的是「資料中心即服務！」。

您已正確、 可能造成，和任何數目的系統，其中有許多您可能已經使用，可以管理 Azure Vm 的群組，並插入自訂程式碼，使用指令碼，通常以 hello [CustomScriptingExtension 適用於 Windows 的](https://msdn.microsoft.com/library/azure/dn781373.aspx)或hello[適用於 Linux CustomScriptingExtension](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)。 您可以 (而且可能已經在) 使用 PowerShell 或 Azure CLI 指令碼自動化您的 Azure 部署。

這些功能通常是，則移轉的 tootools 喜歡[Puppet](https://puppetlabs.com/)和[Chef](https://www.chef.io/) tooautomate hello 的建立和小數位數的 Vm 組態。 (這裡是一些連結太[搭配 Azure 使用這些工具](#tools-for-working-with-containers)。)

### <a name="azure-resource-group-templates"></a>Azure 資源群組範本
Azure 還要新，釋出 hello [Azure 資源管理](../articles/resource-manager-deployment-model.md)REST API 和更新的 PowerShell 和 Azure CLI 工具 toouse 它輕鬆。 您可以部署、 修改或重新部署整個應用程式使用的拓撲[Azure 資源管理員範本](../articles/resource-group-authoring-templates.md)hello Azure 資源管理 API 使用：

* hello [Azure 入口網站使用範本](https://github.com/Azure/azure-quickstart-templates)&mdash;提示，請使用 hello"DeployToAzure 」 按鈕
* hello [Azure CLI](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="deployment-and-management-of-entire-groups-of-azure-vms-and-containers"></a>部署和管理整個 Azure VM 群組和容器群組
有幾個很受歡迎的系統可以部署整個 VM 群組，並且在系統上面安裝 Docker (或其他 Linux 容器主機系統) 做為可自動化的群組。 直接連結，請參閱 hello[容器和工具](#containers-and-vm-technologies)以下區段。 有數個系統執行此 tooa 更高或較低範圍，此清單未全部列出。 這要視您的技能和案例而定，可能不一定有用。

Docker 有自己的 VM 建立工具 ([docker-machine](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) 以及一個負載平衡、docker-container 叢集管理工具 ([swarm](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。 此外，hello [Azure Docker VM 擴充功能](https://github.com/Azure/azure-docker-extension/blob/master/README.md)隨附的預設支援[ `docker-compose` ](https://docs.docker.com/compose/)，它可以部署在多個容器設定應用程式容器。

此外，您可以試試 [Mesosphere 的資料中心作業系統 (DCOS)](http://docs.mesosphere.com)。 DCOS 根據 hello 開放原始碼[mesos](http://mesos.apache.org/) "分散式的系統核心 」，可讓您 tootreat 可定址的一項服務當做您資料中心。 DCOS 擁有幾個重要系統的內建套件，例如 [Spark](http://spark.apache.org/) 和 [Kafka](http://kafka.apache.org/) (以及其他)，以及例如 [Marathon](https://mesosphere.github.io/marathon/) (容器控制系統) 和 [Chronos](https://mesos.github.io/chronos/) (分散式排程器) 的內建服務。 Mesos 衍生自在 Twitter、AirBnb 和其他 Web 規模的企業學習到的工作。 您也可以使用**廣域**做為 hello 協調流程引擎。

而 [Kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/) 則是一個 VM 和容器群組管理的開放原始碼系統，衍生自在 Google 學習到的工作。 您甚至可以使用[與 kubernetes 逐漸 tooprovide 網路支援](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)。

[Deis](http://deis.io/overview/)是開放來源 「 平台為-服務 」 (PaaS)，可讓您輕鬆 toodeploy 並管理您自己的伺服器上的應用程式。 Deis Docker 和 CoreOS tooprovide Heroku 啟發的工作流程的輕量級 PaaS 為基礎。

[CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html) 是一個 Linux 散發套件，有最佳化的使用量、Docker 支援以及稱為 [rkt](https://github.com/coreos/rkt) 的自有容器系統，也有一個稱為 [fleet](https://coreos.com/fleet/docs/latest/) 的容器群組管理工具。

Ubuntu 是另一個非常受歡迎的 Linux 散發套件，能完整支援 Docker，也支援 [Linux (LXC 式) 叢集](https://help.ubuntu.com/lts/serverguide/lxc.html)。

## <a name="tools-for-working-with-azure-vms-and-containers"></a>使用 Azure VM 和容器的工具
要使用容器和 Azure VM 必須使用工具。 本節提供一份只有部分 hello 最有用或重要概念與工具，關於容器、 群組和 hello 更大的設定和協調流程所使用的工具。

> [!NOTE]
> 這個區域會變更非常快速，，但在我們將在本主題並向上 toodate 其連結需要我們最佳 tookeep，它可能是不可能的工作。 請確定您在有趣的主旨 tookeep toodate 向上搜尋 ！
>
>

### <a name="containers-and-vm-technologies"></a>容器和 VM 技術
一些 Linux 的容器技術：

* [Docker](https://www.docker.com)
* [LXC](https://linuxcontainers.org/)
* [CoreOS 和 rkt](https://github.com/coreos/rkt)
* [Open Container Project](http://opencontainers.org/)
* [RancherOS](http://rancher.com/rancher-os/)

Windows 容器連結：

* [Windows 容器](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)

Visual Studio Docker 連結：

* [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/core/docker/visual-studio-tools-for-docker)

Docker 工具：

* [Docker daemon](https://docs.docker.com/installation/#installation)
* Docker 用戶端
  * [Windows Docker Client on Chocolatey](https://chocolatey.org/packages/docker)
  * [Docker 安裝指示](https://docs.docker.com/installation/#installation)

Microsoft Azure 上的 Docker：

* [Azure 上 Linux 的 Docker VM 延伸模組](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure Docker VM 延伸模組使用者指南](https://github.com/Azure/azure-docker-extension/blob/master/README.md)
* [使用從 hello Azure 命令列介面 (Azure CLI) hello Docker VM 擴充功能](../articles/virtual-machines/linux/classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [使用從 hello Azure 入口網站的 hello Docker VM 擴充功能](../articles/virtual-machines/linux/classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [如何 toouse docker 電腦在 Azure 上](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [如何在 Azure 上的群集與 toouse docker](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [在 Azure 上開始使用 Docker 和 Compose](../articles/virtual-machines/linux/docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [在 Azure 上快速地使用 Azure 資源群組範本 toocreate Docker 主機](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)
* [hello 的內建支援`compose`](https://github.com/Azure/azure-docker-extension#11-public-configuration-keys)所包含的應用程式
* [在 Azure 上實作 Docker 私用登錄](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Linux 散發套件和 Azure 範例：

* [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

組態、叢集管理以及容器協調流程：

* [CoreOS 上的 Fleet](https://coreos.com/fleet/docs/latest/)
* Deis

  * [完成 CoreOS 與針織紋指南 tooautomated Kubernetes 叢集部署](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
  * [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Mesos](http://mesos.apache.org/)

  * [Mesosphere 的資料中心作業系統 (DCOS)。](https://docs.mesosphere.com/1.7/overview/design/azure-container-service/)
* [Jenkins](https://jenkins.io/) 和 [Hudson](http://hudson-ci.org/)

  * [適用於 Azure 的 Jenkins VM 代理程式外掛程式](https://wiki.jenkins.io/display/JENKINS/Azure+VM+Agents+plugin)
  * [GitHub 儲存機制︰適用於 Azure 的 Jenkins 儲存體外掛程式](https://github.com/jenkinsci/windows-azure-storage-plugin)
  * [協力廠商︰適用於 Azure 的 Hudson 從屬外掛程式](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
  * [協力廠商︰適用於 Azure 的 Hudson 儲存體外掛程式](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Azure 自動化](https://azure.microsoft.com/services/automation/)

  * [影片： 如何 tooUse 使用 Linux Vm 的 Azure 自動化](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* Powershell DSC for Linux

  * [部落格： 如何 toodo Powershell DSC for Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
  * [GitHub：Docker 用戶端 DSC](https://github.com/anweiss/DockerClientDSC)

## <a name="next-steps"></a>後續步驟
認識 [Docker](https://www.docker.com) 和 [Windows Server 容器](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)。

<!--Anchors-->
[microservices]: http://martinfowler.com/articles/microservices.html
[microservice]: http://martinfowler.com/articles/microservices.html
<!--Image references-->
