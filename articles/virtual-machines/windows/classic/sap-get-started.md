---
title: "在 Windows 虛擬機器上的 SAP aaaUsing |Microsoft 文件"
description: "了解如何在 Microsoft Azure 中的 Windows 虛擬機器 (VM) 上使用 SAP"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: 1b455be4-c02f-43e3-8d39-c2d5f216e646
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 6c4d8a066a4a8805668e78e67fd2110f2000ee75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a>在 Azure 中的 Windows 虛擬機器上使用 SAP
雲端運算廣泛使用的名詞日漸重要內 hello IT 產業、 從小型公司向上 toolarge 和一家跨國企業。 Microsoft Azure 為 hello 它提供了各式各樣的新的可能性的 microsoft 雲端服務平台。 現在的客戶可以 toorapidly 佈建和取消佈建應用程式當成雲端服務，因此不會限制的 tootechnical 或預算限制。 而不是投入時間和預算硬體基礎結構中，公司可以專注於 hello 應用程式、 商務程序和它的優點的客戶與使用者。

Microsoft 透過 Microsoft Azure 虛擬機器，提供完整的基礎結構即服務 (IaaS) 平台。 Azure 虛擬機器 (IaaS) 支援以 SAP NetWeaver 為基礎的應用程式。 下面的 hello 白皮書說明如何 tooplan 和實作 SAP NetWeaver 架構的 Windows Azure 中的虛擬機器上的應用程式。 您也可以在 [Linux 虛擬機器](../../linux/classic/sap-get-started.md)上，實作 SAP NetWeaver 應用程式。

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a>Azure 上的 SAP NetWeaver - HA
標題： aaaSAP NetWeaver on Azure-叢集 SAP ASCS/SCS 執行個體上使用 SIOS DataKeeper Azure 使用 Windows Server 容錯移轉叢集

摘要: ' 本文件說明如何在 Azure 上高可用性的 SAP ASCS/SCS 組態 toouse SIOS DataKeeper tooset。 SAP 可透過需要共用磁碟的 Windows Server 容錯移轉叢集組態，保護其單一失敗點元件，例如 SAP ASCS/SCS 或 Enqueue Replication Services。 這些 SAP 元件不可或缺的 SAP 系統的 hello 功能。 因此 toobe 置於高可用性功能需求將 toomake 確定這些元件可以承受伺服器或 VM 的失敗，因為透過裸機和 HYPER-V 環境的 Windows 叢集組態。 從 2015 年 8 月開始 Azure 本身無法提供需要適用於 hello Windows 的共用的磁碟基礎的高可用性組態所需的這些重要的 SAP 元件。 不過 hello hello SIOS DataKeeper 產品的協助，您可以建立 Windows Server 容錯移轉叢集組態所需的 SAP ASCS/SCS hello Azure IaaS 平台上。 本白皮書說明如何 tooinstall 的共用磁碟的 Windows Server 容錯移轉叢集組態提供在 Azure 中使用 SIOS Datakeeper 所以逐步方法中。 hello 本文將在設定的詳細說明 hello Azure、 Windows 和 SAP 端這會導致 hello 高可用性組態以最佳的方式運作。 平台提供 hello 紙張補充 hello SAP 安裝文件集和 SAP 附註 」 包含 hello 安裝和部署上的 SAP 軟體的主要資源。

更新時間：2015 年 8 月

[立即下載此指南](http://go.microsoft.com/fwlink/?LinkId=613056)

