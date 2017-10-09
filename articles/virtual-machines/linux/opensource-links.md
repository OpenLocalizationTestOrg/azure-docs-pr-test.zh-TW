---
title: "aaaLinux，並在 Azure 上的開放原始碼計算 |Microsoft 文件"
description: "列出 Azure 上的 Linux 和開放原始碼運算文章，其中包括基本的 Linux 使用方式、有關在 Azure 上執行或上傳 Linux 映像的一些基本概念，以及其他有關特定技術與最佳化的內容。"
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: a7e608b5-26ea-41e0-b46b-1a483a257754
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/27/2016
ms.author: rasquill
ms.openlocfilehash: 3ce0dcc65f28d0dddb29f654409f6dae56213bc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="linux-and-open-source-computing-on-azure"></a>Azure 上的 Linux 和開放原始碼運算
找到您需要 toocreate 並管理 Linux 型虛擬機器 hello 傳統部署模型中所有的 hello 文件。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

## <a name="get-started"></a>開始使用
* [Azure 上的 Linux 簡介](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [常見問題集的問題有關 Azure 虛擬機器建立 hello 傳統部署模型](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [關於虛擬機器的映像](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [上傳您自己的 Distro 映像](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (以及使用 [Azure 背書散發版本](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)的指示)
* [登入 tooa Linux VM 使用 hello Azure 傳統入口網站](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a>設定
* [安裝 Azure 命令列介面 (Azure CLI)](../../cli-install-nodejs.md)

## <a name="tutorials"></a>教學課程
* [在 Azure 中的 Linux 虛擬機器上安裝 hello LAMP 堆疊](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VM 上的 Ruby on Rails Web 應用程式](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [做法：安裝 Apache Qpid Proton-C for AMQP 和服務匯流排](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a>資料庫
* [在 Azure 上最佳化 MySQL 的效能](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [MySQL 叢集](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [在 Azure 上執行 Cassandra 搭配 Linux 並透過 Node.js 進行存取](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [建立 MariaDbs 的多重主機叢集](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a>HPC
* [開始在 Azure 中的 HPC Pack 叢集使用 Linux 運算節點](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [在 Azure 中的 Linux 運算節點以 Microsoft HPC Pack 執行 NAMD](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [設定 Linux RDMA 叢集 toorun MPI 應用程式](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a>Docker
* [使用從 hello Azure 命令列介面 (Azure CLI) hello Docker VM 擴充功能](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [使用從 hello Azure 入口網站的 hello Docker VM 擴充功能](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [如何 toouse docker 電腦在 Azure 上](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a>Ubuntu
* [做法：MySQL 叢集](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [做法：Node.js 和 Cassandra](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a>OpenSUSE
* [做法：安裝和執行 MySQL](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a>CoreOS
* [做法：在 Azure 上使用 CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a>規劃
* [Azure 基礎結構服務實作指導方針](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [選取 Linux 使用者名稱](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [如何 tooconfigure 可用性設定組 hello 傳統部署模型中的虛擬機器](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [如何在 Azure Vm 上的計劃中維護 tooSchedule](classic/planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [管理虛擬機器 hello 可用性](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure 中 Linux 虛擬機器預定進行的維修](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a>部署
* [建立執行 Linux 的自訂虛擬機器](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [hello 基本概念： 擷取 Linux VM tooMake 範本](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [非背書散發套件的資訊](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a>管理
* [SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [如何 tooReset 密碼或 SSH 屬性適用於 Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [使用 Root](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a>Azure 資源
* [hello Azure Linux 代理程式](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VM 延伸模組與功能](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [將自訂資料插入 VM toouse 以便與雲端初始化](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a>儲存體
* [附加資料磁碟 tooa Linux VM](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [從 Linux VM 卸離資料磁碟](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>網路
* [如何 tooset 個端點在 Azure 中的傳統虛擬機器](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a>疑難排解
* [疑難排解安全殼層 (SSH) 連線 tooa Linux 型 Azure 虛擬機器](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [針對在 Azure 中建立新 Linux 虛擬機器的傳統部署問題進行疑難排解](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器的傳統部署問題進行疑難排解](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a>參考
* [Azure 服務管理 (asm) 模式中的 Azure CLI 命令](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Azure 服務管理 REST API](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a>一般連結
下列連結查看 hello 適用於 Microsoft 部落格、 Technet 網頁和外部網站，而上述 Azure.com 文件。 為 Azure 與 hello 的開放原始碼電腦世界會快速移動目標，它是幾乎某些 hello 下列連結已過期，*儘管*我們應該執行我們的最佳 toocontinually hello 事實加入較新的主題和移除過時的項目。 如果我們已遺失其中一個，請讓我們知道 hello 的註解或提交提取要求 tooour [GitHub 儲存機制](https://github.com/Azure/azure-content/)。

* [在 Linux 上使用 Docker 容器執行 ASP.NET 5](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [如何 tooDeploy CentOS VM 映像來自 OpenLogic，](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [SUSE 更新基礎結構](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [SUSE Linux Enterprise Server for SAP 雲端應用裝置程式庫](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [以 12 個步驟在 Azure 上建置高可用性的 Linux](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [透過 Azure CLI、node.js、jhawk 在 Azure 上自動佈建 Linux](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [Azure 上的 GlusterFS](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a>FreeBSD
* [在 Azure 中執行 FreeBSD](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [輕鬆部署 FreeBSD](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [部署自訂的 FreeBSD 映像](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [適用於 Linux 檔案伺服器的 Kaspersky AV](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a>NoSQL
* [Azure 的 8 個開放原始碼 NoSql 資料庫](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [Slideshare (MSOpenTech)︰Azure 上的 CouchDb 經驗](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [透過 node.js、CORS 和 Grunt 執行 CouchDB 即服務](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [在 Windows 上 redis 在 hello Azure Redis 快取服務](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [宣佈 Redis 預覽版本的 ASP.NET 工作階段狀態提供者](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [部落格： RavenHQ 目前可在 hello Azure Marketplace](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a>巨量資料
* [在 Azure Linux VM 上安裝 Hadoop](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a>關聯式資料庫
* [Microsoft Azure 中的 MySQL 高可用性架構](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [使用 corosync 安裝 Postgres，使用 ILB 安裝 pg_bouncer](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a>Linux 高效能運算 (HPC)
* [快速入門範本：加速 SLURM 叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (以及[部落格文章](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))
* [快速入門範本：建立 Linux 計算節點的 HPC 叢集](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a>開發、管理和最佳化
Hello world 的 devops、 管理及最佳化是相當以免受到擴充和非常快速地變更，您應該考慮 hello 清單下方的起始點。

* [影片：Azure CLI 虛擬機器：使用 Chef、Puppet 和 Docker 管理 Linux VM](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [完成 CoreOS 與針織紋指南 tooautomated Kubernetes 叢集部署](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [適用於 Azure 的 Jenkins 從屬外掛程式](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [GitHub 儲存機制︰適用於 Azure 的 Jenkins 儲存體外掛程式](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [協力廠商︰適用於 Azure 的 Hudson 從屬外掛程式](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [協力廠商︰適用於 Azure 的 Hudson 儲存體外掛程式](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [影片：Chef 是什麼，以及如何運作？](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [影片： 如何 tooUse 使用 Linux Vm 的 Azure 自動化](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [部落格： 如何 toodo Powershell DSC for Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [GitHub：Docker 用戶端 DSC](https://github.com/anweiss/DockerClientDSC)
* [Azure 的 Packer 外掛程式](https://github.com/msopentech/packer-azure)

