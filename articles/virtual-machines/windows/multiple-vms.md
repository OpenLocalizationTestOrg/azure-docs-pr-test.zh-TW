---
title: "aaaCreate 多部虛擬機器 |Microsoft 文件"
description: "在 Windows 上建立多部虛擬機器的選項"
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.openlocfilehash: 37729fabd91049744f6bd94c55221f5c1c65d527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>建立多部 Azure 虛擬機器
有許多案例中您需要 toocreate 大量的類似的虛擬機器 (Vm)。 部分範例包括高效能運算 (HPC)、大規模資料分析、可調整且通常是無狀態的中介層或後端伺服器 (例如 Web 伺服器)，以及分散式資料庫。

這篇文章討論 hello 可用的選項 toocreate 在 Azure 中的多個 Vm。 這些選項超越 hello 簡單案例中手動建立一系列的 Vm。 如果您需要 toocreate 多個 Vm 的少數許多 Vm，您通常使用 hello 處理程序不縮放 toocreate。

許多類似的 Vm 是 toouse hello Azure 資源管理員結構的其中一種方式 toocreate*資源迴圈*。

## <a name="resource-loops"></a>資源迴圈
資源迴圈是 Azure Resource Manager 範本中的速記語法， 它能您在迴圈中建立一組設定相似的資源。 您可以使用資源迴圈 toocreate 多個儲存體帳戶、 網路介面或虛擬機器。 如需資源迴圈的詳細資訊，請參閱太[使用資源迴圈的可用性設定組中的 建立 Vm](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/)。

## <a name="challenges-of-scale"></a>規模的挑戰
雖然資源迴圈在標尺將更容易 toobuild 出雲端基礎結構，而且會產生更精確的範本，就會保留特定的挑戰。 例如，如果您使用資源迴圈 toocreate 100 部虛擬機器，您會需要 toocorrelate 網路介面控制器 (Nic) 對應的 Vm 與儲存體帳戶。 Hello Vm 數目是可能 toobe hello 儲存體帳戶數目不同，因為您必須具有不同的資源迴圈大小，toodeal 太。 這些都是可解決的問題，但是 hello 複雜性會大幅增加小數位數。

另一項挑戰發生於當您需要彈性調整的基礎結構時， 例如，您可以自動調整規模基礎結構會自動增加或減少 Vm 中回應 tooworkload hello 數目。 Vm 未提供的整合的機制 toovary 中數字 （向外的延展和中的小數位數）。 如果您藉由移除 Vm 中調整規模，請藉由確定更新和錯誤網域之間平衡的 Vm 是難以 tooguarantee 高可用性。

最後，當您使用的資源迴圈時，多個呼叫 toocreate 資源移 toohello 基礎網狀架構。 當多個呼叫會建立類似的資源時，Azure 有隱含的機會 tooimprove，在這項設計時，並最佳化部署可靠性和效能。 這正是我們引進「虛擬機器擴展集」  的契機。

## <a name="virtual-machine-scale-sets"></a>虛擬機器擴展集
虛擬機器擴展集是 Azure 計算資源 toodeploy 和管理一組相同的 Vm。 並將所有的 Vm 設定 hello 相同，則 VM 規模集為中的簡單 tooscale 及向外的延展。您只需變更 hello Vm 數目在 hello 集合中。 您也可以設定 VM 規模集 tooautoscale hello hello 工作負載需求為基礎。

需要 tooscale 計算資源，且在標尺的應用程式的作業會隱含地平衡容錯網域和更新網域。

VM 擴展集擁有網路、儲存體、虛擬機器和擴充功能等供您集中設定的屬性，而不需建立 NIC 和 VM 等多種資源之間的關聯。

設定簡介 tooVM 的小數位數，參閱 toohello[虛擬機器規模設定產品頁面](https://azure.microsoft.com/services/virtual-machine-scale-sets/)。 如需詳細資訊，請移 toohello[虛擬機器規模設定文件](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)。

