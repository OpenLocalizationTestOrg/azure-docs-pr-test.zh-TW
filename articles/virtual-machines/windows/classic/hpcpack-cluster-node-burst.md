---
title: "aaaAdd 高載節點 tooan HPC Pack 叢集 |Microsoft 文件"
description: "了解如何 tooexpand HPC Pack 叢集隨 Azure 中加入雲端服務中執行的背景工作角色執行個體"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a>在 Azure 中新增隨 「 高載 」 節點 tooan HPC Pack 叢集
如果您設定[Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029)叢集在 Azure 中，您可能想 tooquickly 標尺 hello 叢集容量向上或向下而不會維護一組預先設定計算節點 Vm 的方式。 本文章將示範如何 tooadd 隨 「 高載 」 節點 （背景工作角色執行個體執行中雲端服務） 做為 Azure 中的計算資源 tooa 前端節點。 

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

![高載節點][burst]

這篇文章中的 hello 步驟可協助您快速加入 Azure 節點 tooa 雲端 HPC Pack 前端節點 VM 進行測試或概念證明部署。 hello 概要步驟如下 hello 與 hello 步驟太 「 高載 tooAzure 」 相同 tooadd 雲端運算容量 tooan 在內部部署 HPC Pack 叢集。 如需教學課程，請參閱 [使用 Microsoft HPC Pack 設定混合式計算叢集](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)。 詳細指導方針和生產環境部署的考量，請參閱[tooAzure 使用 Microsoft HPC Pack 高載](https://technet.microsoft.com/library/gg481749.aspx)。

## <a name="prerequisites"></a>必要條件
* **部署在 Azure VM 中的 HPC Pack 前端節點** -您可以使用獨立的前端節點 VM 或屬於較大叢集的節點。 toocreate 獨立的前端節點，請參閱[部署 HPC Pack 前端節點的 Azure VM 中](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 如需自動化 HPC Pack 叢集部署選項，請參閱[選項 toocreate 和管理 Windows HPC 叢集，在 Azure 中使用 Microsoft HPC Pack](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
  
  > [!TIP]
  > 如果您使用 hello [HPC Pack IaaS 部署指令碼](hpcpack-cluster-powershell-script.md)toocreate hello 叢集在 Azure 中，您可以在自動化部署中包含 Azure 高載節點。 請參閱文件中的 hello 範例。
  > 
  > 
* **Azure 訂用帳戶**-tooadd Azure 節點，您可以選擇 hello 相同訂用帳戶使用 toodeploy hello 前端節點 VM，或不同的訂用帳戶 （或訂閱）。
* **核心配額**-您可能需要 tooincrease hello 配額的核心，特別是當您選擇 toodeploy 具有多核心大小的數個 Azure 節點。 tooincrease 配額限制時，[開啟線上客戶支援要求](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)不收費。

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a>步驟 1： 建立雲端服務和儲存體帳戶的 hello Azure 節點
使用您的 Azure 節點 hello Azure 傳統入口網站或對等的工具 tooconfigure hello 遵循 toodeploy 所需的資源：

* 新的 Azure 雲端服務
* 新的 Azure 儲存體帳戶

> [!NOTE]
> 請勿重複使用您訂用帳戶中現有的雲端服務。 
> 
> 

**考量**

* 設定每個 Azure 節點範本您計劃 toocreate 個別的雲端服務。 不過，您可以使用 hello 多個節點範本相同的儲存體帳戶。
* 我們建議您在 hello 中尋找 hello 雲端服務和 hello 部署的 hello 儲存體帳戶相同的 Azure 區域。

## <a name="step-2-configure-an-azure-management-certificate"></a>步驟 2：設定 Azure 管理憑證
tooadd Azure 節點當做計算資源，您需要對應憑證 toohello 用於 hello 部署的 Azure 訂用帳戶上 hello 前端節點和上傳管理憑證。

針對此案例中，您可以選擇 hello**預設 HPC Azure 管理憑證**的 HPC Pack 自動安裝與設定前端節點上。 此憑證可用於測試及概念證明部署。 此憑證 toouse 上, 傳從 hello 前端節點 VM toothe 訂用帳戶檔案 C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer。 在 hello tooupload hello 憑證[Azure 傳統入口網站](https://manage.windowsazure.com)，按一下 **設定** > **管理憑證**。

其他選項 tooconfigure hello 管理憑證，請參閱[案例 tooConfigure hello Azure 高載部署的 Azure 管理憑證](http://technet.microsoft.com/library/gg481759.aspx)。

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a>步驟 3： 部署 Azure 節點 toohello 叢集
hello 步驟 tooadd 和啟動 Azure 節點，在此案例中是通常 hello 相同 hello 與內部部署前端節點的步驟。 如需詳細資訊，請參閱下列各節中的 hello[步驟 tooDeploy Azure 節點使用 Microsoft HPC Pack](https://technet.microsoft.com/library/gg481758.aspx):

* 建立 Azure 節點範本
* 新增 Azure 節點 toohello Windows HPC 叢集
* 啟動 （佈建） Azure 節點的 hello

您加入及啟動 hello 節點之後，他們就可以為您 toouse toorun 叢集作業。

如果您在部署 Azure 節點時遇到問題，請參閱 [使用 Microsoft HPC Pack 部署 Azure 節點時的疑難排解](http://technet.microsoft.com/library/jj159097.aspx)。

## <a name="next-steps"></a>後續步驟
* toouse hello 的大量計算執行個體大小高載節點，請參閱中的 hello 考量[高效能計算 VM 大小](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* 如果您想要自動成長或壓縮 hello Azure 運算資源，根據 hello 叢集工作負載，請參閱[自動擴增和縮減 HPC Pack 叢集中的 Azure 計算資源](hpcpack-cluster-node-autogrowshrink.md)。

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
