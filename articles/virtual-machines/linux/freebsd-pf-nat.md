---
title: "aaaUse FreeBSD 封包篩選器 toocreate 在 Azure 中的防火牆 |Microsoft 文件"
description: "深入了解如何 toodeploy NAT 防火牆使用 FreeBSD 的 PF 在 Azure 中的。"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: 3d3a5dde2ca03ba6fc384581c786f5eb746e6d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-freebsds-packet-filter-toocreate-a-secure-firewall-in-azure"></a>如何 toouse FreeBSD 封包篩選器 toocreate 安全的防火牆，在 Azure 中
本文介紹如何 toodeploy NAT 防火牆 FreeBSD 的 Packer 篩選器，透過 Azure Resource Manager 範本使用常見的 web 伺服器案例。

## <a name="what-is-pf"></a>什麼是 PF？
PF (封包篩選器，也寫成 pf) 是一個 BSD 授權的具狀態封包篩選器，是防火牆軟體的一個核心部分。 PF 一直以來快速發展，現在已有數個超越其他可用防火牆的優點。 網路位址轉譯 (NAT) 為 PF 自第一天，然後封包排程器，並使用中佇列管理已經整合至 PF，透過整合 hello ALTQ，並且讓它成為可透過 PF 的組態設定。 容錯移轉與備援、 authpf 工作階段驗證以及 ftp proxy tooease 防火牆 hello 困難 FTP 通訊協定，例如 pfsync 和 CARP 功能也有擴充 PF. 簡單說來，PF 就是一個強大且功能豐富的防火牆。 

## <a name="get-started"></a>開始使用
如果您想要在您的 web 伺服器的 hello 雲端中設定安全的防火牆，請讓我們開始吧。 您也可以套用這個 Azure Resource Manager 範本 tooset，註冊您的網路拓撲中使用的 hello 指令碼。
hello Azure Resource Manager 範本設定 FreeBSD 虛擬機器執行之 NAT /redirection hello Nginx 網頁伺服器安裝並設定搭配使用 PF 和兩個 FreeBSD 虛擬機器。 此外 tooperforming NAT hello 兩部 web 伺服器的輸出流量，hello NAT/重新導向虛擬機器會攔截 HTTP 要求，並將他們重新導向以循環配置資源方式 toohello 兩部 web 伺服器。 hello VNet 使用 hello 私用路由的內部 IP 位址空間 10.0.0.2/24，而且您可以修改 hello 樣板的 hello 參數。 hello Azure Resource Manager 範本也會定義的 hello 是個別的路由集合中的整個 VNet 使用 toooverride Azure 的預設路由 hello 目的地 IP 位址為基礎的路由表。 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a>透過 Azure CLI 進行部署
您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。 使用 [az group create](/cli/azure/group#create) 來建立資源群組。 hello 下列範例會建立資源群組名稱`myResourceGroup`在 hello`West US`位置。

```azurecli
az group create --name myResourceGroup --location westus
```

接下來，部署 hello 範本[pf freebsd 設定](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup)與[az 群組部署建立](/cli/azure/group/deployment#create)。 下載[azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json)底下 hello 相同的路徑，以及定義您自己的資源值，例如`adminPassword`， `networkPrefix`，和`domainNamePrefix`。 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

約五分鐘之後, 您會收到 hello 資訊的`"provisioningState": "Succeeded"`。 然後您可以 ssh toohello 前端 VM (NAT) 或存取 Nginx 網頁伺服器，在瀏覽器中的 hello 前端 VM (NAT) hello 公用 IP 位址或者 FQDN。 hello 下列範例會列出 FQDN 和公用 IP 位址指派 toohello 前端 VM (NAT) 在 hello`myResourceGroup`資源群組。 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a>後續步驟
您想 tooset 註冊您自己在 Azure 中的 NAT？ 需要是開放原始碼、免費但具有強大功能嗎？ 那麼，PF 會是一個理想的選擇。 使用 hello 範本[pf freebsd 設定](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup)，您只需要五分鐘 tooset NAT 防火牆設定具有循環配置資源負載平衡使用 FreeBSD 的 PF 在 Azure 中常見的 web 伺服器案例。 

如果您想在 Azure 中的 FreeBSD toolearn hello 供應項目，請參閱太[在 Azure 上的簡介 tooFreeBSD](freebsd-intro-on-azure.md)。

如果您想深入了解 PF tooknow，請參閱太[FreeBSD 手冊](https://www.freebsd.org/doc/handbook/firewalls-pf.html)或[PF 使用者的指南](https://www.freebsd.org/doc/handbook/firewalls-pf.html)。
