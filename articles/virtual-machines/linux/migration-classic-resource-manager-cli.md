---
title: "aaaMigrate Vm tooResource 管理員使用 Azure CLI |Microsoft 文件"
description: "本文逐步 hello 平台支援移轉的資源從傳統 tooAzure 資源管理員使用 Azure CLI"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a>從傳統 tooAzure 資源管理員移轉 IaaS 資源，使用 Azure CLI
這些步驟顯示如何 toouse Azure 命令列介面 (CLI) 的命令 toomigrate 基礎結構為從 hello 傳統部署模型 toohello Azure Resource Manager 部署模型的服務 (IaaS) 資源。 hello 文章需要 hello [Azure CLI](../../cli-install-nodejs.md)。

> [!NOTE]
> 此處所述的所有 hello 作業都是等冪。 如果您有不支援的功能或設定錯誤以外的問題，我們建議您重試 hello 準備、 中止或認可作業。 hello 平台將再重試 hello 的動作。
> 
> 

<br>
以下是步驟需要執行移轉程序期間 toobe 流程圖 tooidentify hello 順序

![螢幕擷取畫面顯示 hello 移轉步驟](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a>步驟 1︰為移轉做準備
以下是我們建議您在評估從傳統 tooResource Manager 移轉的 IaaS 資源的一些最佳作法：

* 閱讀 hello[不支援的設定或功能的清單](../windows/migration-classic-resource-manager-overview.md)。 如果您有使用不支援的設定或功能的虛擬機器，我們建議您等待 hello 功能/組態支援 toobe 宣布。 或者，您可以移除該功能，或移出該設定 tooenable 移轉時，如果其符合您的需求。
* 如果您有自動化部署基礎結構和應用程式目前的指令碼，請使用這些指令碼移轉嘗試 toocreate 類似的測試設定。 或者，您可以設定範例環境使用 hello Azure 入口網站。

> [!IMPORTANT]
> 從傳統 tooResource Manager 移轉目前不支援應用程式閘道。 toomigrate 傳統虛擬網路與應用程式閘道，執行準備作業 toomove hello 網路之前先移除 hello 閘道。 Hello 移轉完成之後，重新連接 hello 閘道 Azure 資源管理員中。 
>
>ExpressRoute 閘道連接 tooExpressRoute 電路，另一個訂用帳戶中的不會自動移轉。 在這種情況下，移除 hello ExpressRoute 閘道、 hello 虛擬網路移轉並重新建立 hello 閘道。 請參閱[移轉 ExpressRoute 電路和相關聯的虛擬網路與 hello 傳統 toohello Resource Manager 部署模型](../../expressroute/expressroute-migration-classic-resource-manager.md)如需詳細資訊。
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a>步驟 2： 設定您的訂用帳戶，並註冊 hello 提供者
移轉案例中，您需要的這兩種傳統環境 tooset 和資源管理員。 [安裝 Azure CLI](../../cli-install-nodejs.md) 並[選取您的訂用帳戶](../../xplat-cli-connect.md)。

Tooyour 登入帳戶。

    azure login

使用下列命令的 hello 選取 hello Azure 訂用帳戶。

    azure account set "<azure-subscription-name>"

> [!NOTE]
> 註冊是一次步驟但它需要 toobe 完成一次嘗試移轉。 若未註冊，您會看到下列錯誤訊息的 hello 
> 
> *不正確的要求︰訂用帳戶未針對移轉進行註冊。* 
> 
> 

使用下列命令的 hello 註冊與 hello 移轉資源提供者。 請注意，在某些情況下，此命令會逾時。不過，hello 註冊才會成功。

    azure provider register Microsoft.ClassicInfrastructureMigrate

請等待五分鐘 hello 註冊 toofinish。 您可以使用下列命令的 hello 檢查 hello hello 核准狀態。 請先確定 RegistrationState 是 `Registered` ，再繼續進行。

    azure provider show Microsoft.ClassicInfrastructureMigrate

現在切換 CLI toohello`asm`模式。

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>步驟 3： 請確定您有足夠的 Azure 資源管理員虛擬機器核心 hello 目前的部署或 VNET 的 Azure 區域中
這個步驟您將需要 tooswitch 太`arm`模式。 以下列命令的 hello 這麼做。

```
azure config mode arm
```

您可以使用下列 CLI 命令 toocheck hello 目前量核心有 Azure 資源管理員中的 hello。 toolearn 進一步了解核心配額，請參閱[限制和 hello Azure 資源管理員](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

完成後確認此步驟中，您可以切換回太`asm`模式。

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a>步驟 4：選項 1 - 移轉雲端服務中的虛擬機器
使用下列命令，hello 的雲端服務]，然後按一下 [挑選 hello 雲端服務，而您想 toomigrate 取得 hello 清單。 請注意如果 hello 雲端服務中的 hello Vm 虛擬網路中，或他們有 web/背景工作角色，您會收到錯誤訊息。

    azure service list

執行 hello hello 詳細資訊輸出中的下列命令 tooget hello 部署 hello 雲端服務名稱。 在大部分情況下，hello 部署名稱是 hello 與 hello 雲端服務名稱相同。

    azure service show <serviceName> -vv

首先，驗證是否可以使用下列命令的 hello hello 雲端服務移轉：

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

準備移轉的 hello 雲端服務中的 hello 虛擬機器。 您必須從兩個選項 toochoose。

如果您想 toomigrate hello Vm tooa 平台建立虛擬網路，請使用下列命令的 hello。

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

如果您想 toomigrate tooan 現有 hello Resource Manager 部署模型中的虛擬網路，請使用下列命令的 hello。

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

Hello 準備之後操作是否成功，您可以查看 hello 詳細資訊輸出 tooget hello 的移轉狀態 hello Vm，並確保它們處於 hello`Prepared`狀態。

    azure vm show <vmName> -vv

檢查 hello hello 準備資源使用 CLI 或 hello Azure 入口網站的組態。 如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello。

    azure service deployment abort-migration <serviceName> <deploymentName>

如果 hello 備妥的組態看起來不錯，可以向前移動，並使用下列命令的 hello 認可 hello 資源。

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a>步驟 4：選項 2 - 移轉虛擬網路中的虛擬機器
您想 toomigrate 挑選 hello 虛擬網路。 請注意，是否 hello 虛擬網路包含 web/背景工作角色或 Vm 具有不支援的設定，您會取得驗證錯誤訊息。

使用下列命令的 hello hello 訂用帳戶中取得所有 hello 虛擬網路。

    azure network vnet list

hello 輸出看起來像這樣：

![Hello 與反白顯示的 hello 整個虛擬網路名稱的命令列的螢幕擷取畫面。](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

在上述範例中的 hello，hello **virtualNetworkName** hello 整個名稱**」 群組 classicubuntu16 classicubuntu16"**。

首先，驗證是否使用下列命令的 hello hello 虛擬網路移轉：

```shell
azure network vnet validate-migration <virtualNetworkName>
```

使用下列命令的 hello 準備移轉您選擇的 hello 虛擬網路。

    azure network vnet prepare-migration <virtualNetworkName>

檢查 hello hello 備妥使用 CLI 或 hello Azure 入口網站的虛擬機器的組態。 如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello。

    azure network vnet abort-migration <virtualNetworkName>

如果 hello 備妥的組態看起來不錯，可以向前移動，並使用下列命令的 hello 認可 hello 資源。

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a>步驟 5：移轉儲存體帳戶
一旦您完成移轉 hello 虛擬機器時，我們建議您移轉 hello 儲存體帳戶。

準備移轉中的 hello 儲存體帳戶，使用下列命令的 hello

    azure storage account prepare-migration <storageAccountName>

檢查由使用 CLI 或 hello Azure 入口網站所準備的儲存體帳戶的 hello hello 組態。 如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello。

    azure storage account abort-migration <storageAccountName>

如果 hello 備妥的組態看起來不錯，可以向前移動，並使用下列命令的 hello 認可 hello 資源。

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a>後續步驟

* [平台支援移轉的 IaaS 資源從傳統 tooAzure 資源管理員概觀](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [規劃移轉的 IaaS 資源從傳統 tooAzure 資源管理員](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [使用傳統 tooAzure 資源管理員的 PowerShell toomigrate IaaS 資源](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [社群工具，用以協助移轉的 IaaS 資源從傳統 tooAzure 資源管理員](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [檢閱最常見的移轉錯誤](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [檢閱 hello 最常見問題集從傳統 tooAzure 資源管理員移轉的 IaaS 資源](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
