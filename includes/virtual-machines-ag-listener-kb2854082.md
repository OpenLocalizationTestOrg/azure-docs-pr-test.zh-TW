接下來，如果 hello 叢集上的任何伺服器執行 Windows Server 2008 R2 或 Windows Server 2012，您必須確認該 hello hotfix [KB2854082](http://support.microsoft.com/kb/2854082)安裝在每一個 hello 在內部部署伺服器或 Azure Vm 的 hello 叢集的一部分。 任何伺服器或 VM 若是位於 hello 叢集中，但不是在 hello 可用性群組中，也應該安裝這個 hotfix。

Hello 遠端桌面工作階段中每個 hello 叢集節點，下載[KB2854082](http://support.microsoft.com/kb/2854082) tooa 本機目錄。 然後，依序在每個叢集節點上安裝 hello hotfix。 如果 hello 叢集服務目前在 hello 叢集節點上執行，hello 伺服器也會在 hello hello hotfix 安裝結束時會重新啟動。

> [!WARNING]
> 停止 hello 叢集服務或重新啟動伺服器 hello 會影響叢集和 hello availability group，hello 仲裁健全狀況，而且它可能會導致您的叢集 toogo 離線。 toomaintain hello 高可用性的叢集安裝期間，請確認：
> 
> * hello 叢集處於最佳仲裁健全狀況。 
> * 在任何節點上安裝 hello hotfix 之前，所有叢集節點都都在線上。
> * Hello 叢集中任一其他節點上安裝 hello hotfix 之前，允許 hello hotfix 安裝 toorun toocompletion 上一個節點，包括完整重新啟動伺服器 hello。
> 
> 

