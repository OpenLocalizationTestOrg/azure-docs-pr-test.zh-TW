# <a name="securing-docker-containers-in-azure-container-service"></a>保護 Azure Container Service 中的 Docker 容器

本文將介紹為部署在 Azure Container Service 中的 Docker 容器提供保護時的注意事項和建議。 許多這些考量通常套用 tooDocker 容器部署在 Azure 或其他環境。 

## <a name="image-security"></a>映像安全性

容器是透過一或多個存放庫中所儲存的映像來建立的。 這些機制可以隸屬 toopublic 或私用容器。 公用登錄的範例是 [Docker Hub](https://hub.docker.com/)。 私用登錄的範例為 hello [Docker Trusted Registry](https://docs.docker.com/datacenter/dtr/2.0/)，它可以是安裝在內部部署或虛擬的私人雲端中。 另外還有以雲端為基礎的私人容器登錄服務，包括 [Azure Container Registry](../articles/container-registry/container-registry-intro.md)。

### <a name="public-and-private-images"></a>公用和私人映像
一般情況下，可公開取得的容器映像並無法保證安全性，這個情況就和任何已公開發佈的軟體套件一樣。 容器映像包含多個軟體層，每個軟體層可能各有弱點。 它是 hello 容器映像的索引鍵 toounderstand hello 原點、 hello hello 映像 (toodetermine 如果不可靠的來源) 的擁有者包括 hello 軟體層而它所組成，而且 hello 軟體版本。 

比方說，如果您移 toohello 官方[nginx 儲存機制](https://hub.docker.com/_/nginx/)Docker 中樞中，瀏覽 toohello**標記**索引標籤上，您會看到每個映像中的弱點可能會以色彩標示。 每個色彩描述 hello 弱點 hello 映像的軟體層。 如需有關 Docker Hub 弱點掃描的詳細資訊，請參閱[了解 Docker Hub 的官方存放庫](https://blog.docker.com/2015/06/understanding-official-repos-docker-hub/)。

![Docker Hub 中的 Nginx 映像](./media/container-service-security/docker-hub-nginx.png)

企業深處理有關的安全性和 tooprotect 本身受到安全性攻擊應該儲存，以及從私人登錄中，例如 Azure 容器登錄中或 Docker Trusted Registry 擷取映像。 在加法 tooproviding 受管理的私人登錄，Azure 容器登錄中支援[服務主體為基礎的驗證](../articles/container-registry/container-registry-authentication.md)透過 Azure Active Directory 的基本驗證的流量，包括以角色為基礎的存取唯讀、 寫入和擁有者權限。

### <a name="image-security-scanning"></a>映像安全性掃描

即使使用私用的登錄，它就會是個不錯的主意 toouse 的映像，掃描其他安全性驗證的方案。 容器映像中的每個軟體層是獨立的 hello 容器映像中的其他圖層可能容易出錯 toovulnerabilities。 當越來越多公司開始部署其容器技術為基礎的生產工作負載時，掃描映像會變成重要 tooensure 防止對其組織的安全性威脅。 

監視和掃描的解決方案，例如安全性[Twistlock](https://www.twistlock.com/2016/11/07/twistlock-supports-azure-container-registry)和[青色安全性](http://blog.aquasec.com/image-vulnerability-scanning-in-azure-container-registry)，和其他項目，可以使用的 tooscan 私人登錄中的容器映像並識別潛在的弱點。 請務必提供 toounderstand hello 深度掃描該 hello 不同解決方案。 例如，某些解決方案可能只會就已知弱點對映像層進行交叉驗證。 這些解決方案可能無法建置透過特定的封裝管理員軟體可以 tooverify 映像層軟體。 其他解決方案則可能已更加深入地整合掃描功能，因此可以找出任何已封裝軟體中的弱點。

### <a name="production-deployment-rules-and-audit"></a>生產部署的規則和稽核
一旦應用程式部署在生產環境中，就是不可或缺的 tooset 映像用於實際執行環境的一些規則 tooensure 安全，而且包含沒有弱點。

* 一般而言，弱點，即使次要、 映像應該不允許 toorun 實際執行環境中。 此外，在生產環境中部署的所有映像應該在理想情況下儲存在私人登錄存取 tooa 選取少。 它也是重要 tookeep hello 數的實際執行映像小 tooensure，它們可以受到管理有效。

* 因為硬碟 toopinpoint hello 原點的公開可用的容器映像從軟體，是很好的作法 toobuild 映像中的 hello 圖層的 hello 原始來源 tooensure 知識。 當內建自我容器映像中的弱點可能會呈現時，客戶就可以找到更快速的路徑 tooa 解析。 具有公用的映像，客戶需要 toofind hello 根目錄的 公用映像 toofix 它，或從 hello 發行者取得另一個安全映像。

* 部署在生產環境中徹底掃描的影像不保證向上 toodate toobe hello hello 應用程式存留期。 安全性弱點可能會報告 hello 映像層上，不知道先前或引進之後 hello 生產環境部署。 定期稽核的映像部署在生產環境中是已過期或尚未更新一點的必要 tooidentify 映像。 其中一個可能會使用藍綠色部署方法，並輪流升級的機制 tooupdate 容器映像，而不需要停機。 掃描映像可以利用 hello 前面一節中所述的工具來完成。 

* 持續整合 (CI) 管線 toobuild 映像和整合式的安全性掃描可以協助維護安全的私人登錄，以安全的容器映像。 hello hello CI 解決方案內建的弱點可能會掃描可確保通過 hello 的所有測試的映像會推入 toohello 私人登錄從哪一個實際執行部署工作負載。 CI 管線失敗可確保易受攻擊的映像不會用於實際執行工作負載部署的 hello 私人登錄推入。 它也會在有大量映像時自動掃描映像是否安全。 否則，手動稽核映像中是否有安全性弱點會是一件痛苦、冗長又容易出錯的工作。

## <a name="host-level-container-isolation"></a>主機層級的容器隔離
當客戶在 Azure 資源上部署容器應用程式時，這些應用程式會部署在資源群組的訂用帳戶層級，而且不會是多租用戶。 這表示如果客戶與其他人共用訂用帳戶，沒有界限可建置 hello 中的兩個部署之間相同訂用帳戶。 因此，系統無法保證容器層級的安全性。 

它也是關鍵 toounderstand 容器共用核心 hello 與 hello 資源 hello 主機 （這在 Azure 容器服務是在叢集中的 Azure VM）。 因此，在生產環境中執行的容器必須以不具權限的使用者模式執行。 以根權限執行的容器可能會危害整個環境的 hello。 透過在容器中的根層級存取權，駭客就可以存取 toohello hello 主機上的完整根權限。 此外，它是唯讀的檔案系統的重要 toorun 容器。 這可防止其他人已存取 toohello 危害容器 toowrite 惡意指令碼 toohello 檔案系統，以及存取 tooother 檔案。 同樣地，它是重要的 toolimit hello 配置的資源 （例如記憶體、 CPU 和網路頻寬） tooa 容器。 這有助於防止駭客，阻止霸佔資源以及不合法的活動，例如信用卡詐欺或 bitcoin 採礦，可防止其他容器 hello 主機或叢集上執行。

## <a name="orchestrator-considerations"></a>Orchestrator 的注意事項

Azure Container Service 中提供的每個 Orchestrator 都有它自己的安全性注意事項。 例如，您應該限制直接 SSH 存取 tooorchestrator 容器服務中的節點。 相反地，您應該使用每個 orchestrator UI 或命令列工具 (例如`kubectl`如 Kubernetes) 沒有存取主機 hello toomanage hello 容器的環境。 如需詳細資訊，請參閱[進行遠端連線 tooa Kubernetes、 DC/作業系統，或 Docker Swarm 叢集](../articles/container-service/kubernetes/container-service-connect.md)。

其他 orchestrator 特定安全性資訊，請參閱下列資源的 hello:

* **Kubernetes**：[Kubernetes 部署的安全性最佳做法](http://blog.kubernetes.io/2016/08/security-best-practices-kubernetes-deployment.html)

* **DC/OS**：[保護您的叢集](https://dcos.io/docs/1.8/administration/securing-your-cluster/)

* **Docker Swarm**：[Docker 安全性](https://www.docker.com/docker-security)

## <a name="next-steps"></a>後續步驟

* 如需 Docker 架構和容器的安全性相關資訊，請參閱[簡介 tooContainer 安全性](https://www.docker.com/sites/default/files/WP_IntrotoContainerSecurity_08.19.2016.pdf)。

* 如需 Azure 平台安全性的資訊，請參閱 hello [Azure 資訊安全中心](https://www.microsoft.com/en-us/trustcenter/cloudservices/azure)。
