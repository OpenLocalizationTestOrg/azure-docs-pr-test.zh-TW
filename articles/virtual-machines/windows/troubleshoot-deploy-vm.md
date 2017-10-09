---
title: "部署 Windows Azure 中的虛擬機器問題 aaaTroubleshoot |Microsoft 文件"
description: "針對 Azure Resource Manager 部署模型中的 Windows 虛擬機器部署問題進行疑難排解。"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a>針對 Azure 中的 Windows 虛擬機器部署問題進行疑難排解

tootroubleshoot 虛擬機器 (VM) 部署問題，在 Azure 中，檢閱 hello[排名最前面的問題](#top-issues)常見失敗和解決方式。

如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。 或者，您可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)選取**取得支援**。

## <a name="top-issues"></a>常見問題
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a>無法支援 hello 叢集 hello 要求的 VM 大小
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- 重試 hello 要求使用較小的 VM 大小。
- 如果 hello hello 的大小會要求無法變更 VM:
    - 停止 hello 可用性設定組中的所有 hello Vm。 按一下 [資源群組] > 您的資源群組 > [資源] > 您的可用性設定組 > [虛擬機器] > 您的虛擬機器 > [停止]。
    - 在所有 hello Vm 停止，並建立 hello VM hello 預期大小。
    - 啟動第一次，hello 新的 VM，並選取每個 hello 停止 Vm，然後按一下 [開始]。


## <a name="hello-cluster-does-not-have-free-resources"></a>hello 叢集沒有可用的資源
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- 稍後再重試 hello 要求。
- 如果 hello 新的 VM 可以屬於不同的可用性設定嗎
    - 在不同的可用性設定組中建立 VM (hello 中相同的區域)。
    - 加入新 VM toohello hello 相同虛擬網路。

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a>我要如何使用 Windows 用戶端映像並將其部署到 Azure 中？

如果您有適當的 Visual Studio (先前稱為 MSDN) 訂用帳戶，您可以在 Azure 中使用 Windows 7、Windows 8 或 Windows 10 來進行開發/測試案例。 這[文章](client-images.md)外框 hello 中 Azure，並使用 hello Azure 資源庫映像執行 Windows 用戶端資格需求。

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a>如何部署虛擬機器使用 hello 混合使用權益 （集線器）？

有幾個不同的方式以 hello Azure 混合式使用權益 toodeploy Windows 虛擬機器。

針對 Enterprise 合約訂用帳戶：

•   從已使用 Azure Hybrid Use Benefit 來預先設定的特定 Marketplace 映象部署 VM。

針對 Enterprise 合約：

•   上傳自訂的 VM 並使用 Resource Manager 範本或 Azure PowerShell 來進行部署。

如需詳細資訊，請參閱下列資源的 hello:

 - [Azure Hybrid Use Benefit 概觀](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [可下載的常見問題集](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf) \(英文\)

 - [適用於 Windows Server 和 Windows 用戶端的 Azure Hybrid Use Benefit](hybrid-use-benefit-licensing.md)。

 - [如何使用 Azure 中的 hello 混合使用好處](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>我要如何啟用我的 Visual Studio Enterprise (BizSpark) 每月點數

tooactivate 您每月信用額度，請參閱此[文章](https://azure.microsoft.com/offers/ms-azr-0064p/)。

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a>如何 tooadd 企業開發/測試 toomy Enterprise 合約 (EA) tooget 存取 tooWindow 用戶端映像？

hello 能力 toocreate hello 企業開發/測試為基礎的訂用帳戶提供的是受限制的 tooAccount 擁有者獲得權限 toodo 是由企業系統管理員。 hello 帳戶擁有者建立 hello Azure 帳戶入口網站，透過訂閱，然後再應該加入為共同管理員作用中的 Visual Studio 訂閱者。 使他們可以管理和使用 hello 資源所需的開發和測試。 如需詳細資訊，請參閱 [Enterprise 開發/測試](https://azure.microsoft.com/offers/ms-azr-0148p/)。

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a>我的 Windows N 系列 VM 遺失驅動程式

Windows 型 VM 的驅動程式位於[這裡](n-series-driver-setup.md)。

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>在我的 N 系列 VM 內找不到 GPU 執行個體

tootake 利用 hello GPU 功能的 Azure N 系列 Vm 執行 Windows Server 2016 或 Windows Server 2012 R2，您必須安裝在每個 VM 上 NVIDIA 圖形驅動程式部署之後。 您可以取得 [Windows VM](n-series-driver-setup.md) 和 [Linux VM](../linux/n-series-driver-setup.md) 的驅動程式設定資訊。

## <a name="are-client-images-supported-for-n-series"></a>是否支援 N 系列的用戶端映像？

目前 Azure 僅支援執行 Windows Server 和 Linux 作業系統之 VM 上的 N 系列。

## <a name="is-n-series-vms-available-in-my-region"></a>我的區域是否有提供 N 系列 VM？

您可以檢查來自 hello 的 hello 可用性[產品依區域 」 資料表提供](https://azure.microsoft.com/regions/services)，和定價[這裡](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series)。

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a>哪些用戶端映像使用和部署在 Azure 和 tooI 如何取得它們？

假設您有適當的 Visual Studio (先前稱為 MSDN) 訂用帳戶，您可以在 Azure 中使用 Windows 7、Windows 8 或 Windows 10 進行開發/測試案例。 

- Windows 10 映像可供從 hello Azure 組件庫內[適合開發/測試提供](client-images.md#eligible-offers)。 
- 提供項目的任何型別中的 visual Studio 訂閱者也可以[可以充分地準備及建立](prepare-for-upload-vhd-image.md)64 位元 Windows 7、 Windows 8 或 Windows 10 映像，然後[上載 tooAzure](upload-generalized-managed.md)。 hello 使用仍有限的 toodev/測試的方法是使用 Visual Studio 的 「 訂閱者 」。

這[文章](client-images.md)外框 hello 在 Azure 中並使用 hello 的 Azure 資源庫映像執行 Windows 用戶端資格需求。

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>我不能 toosee VM 大小系列我想要調整大小時我的 VM。

執行 VM 時，它會是已部署的 tooa 實體伺服器。 hello Azure 區域中的實體伺服器分組的常見的實體硬體的叢集。 調整大小需要 hello VM toobe 移動 toodifferent 硬體叢集的 VM 是哪一個部署模型所使用的 toodeploy hello VM 而有所不同。

- 在傳統部署模型，hello 雲端服務部署中部署 Vm 必須移除並重新部署在另一個大小家族 toochange hello Vm tooa 大小。

- 在資源管理員部署模型所部署的 Vm，您必須停止所有 Vm hello 可用性設定組之前變更 hello hello 可用性設定組中的任何 VM 大小中。

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>hello 列出的 VM 大小不支援同時將部署在可用性設定組。

選擇 hello 可用性設定組的叢集支援的大小。 建議建立時的可用性集合 toochoose hello 最大 VM 大小您認為需要並且已是您第一種部署 toohello 可用性設定組。

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>可以加入現有的傳統 VM tooan 可用性集嗎？

是。 您可以加入現有傳統 VM tooa 新或現有的可用性設定組。 如需詳細資訊，請參閱[加入現有的虛擬機器 tooan 可用性集](classic/configure-availability.md#addmachine)。


## <a name="next-steps"></a>後續步驟
如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。

或者，您可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)選取**取得支援**。
