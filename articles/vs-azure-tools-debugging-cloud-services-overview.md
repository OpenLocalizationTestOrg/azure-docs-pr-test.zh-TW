---
title: "進行 Azure 雲端服務偵錯的選項 | Microsoft Docs"
description: "進行 Azure 雲端服務的偵錯"
services: visual-studio-online
documentationcenter: n/a
author: mikejo
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: mikejo
ms.openlocfilehash: 196a39a75f8a3151c277f0b2a7944e6886192171
ms.sourcegitcommit: b83781292640e82b5c172210c7190cf97fabb704
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2017
---
# <a name="learn-the-various-ways-to-debug-an-azure-cloud-service"></a>了解進行 Azure 雲端服務偵錯的各種方式
本文提供進行 Azure 雲端服務偵錯的各種方法連結。 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>在 Visual Studio 中進行 Azure 雲端服務的偵錯
使用 Azure 計算模擬器在本機電腦上偵錯您的雲端服務可以節省時間和金錢。 透過在部署服務之前於本機偵錯服務，您可以改善可靠性和效能，而不需支付運算時間。 不過，某些錯誤可能只有當您在 Azure 中執行雲端服務時才會發生。 只有當您在 Azure 中執行雲端服務時才會發生的錯誤，可藉由在您發佈服務時啟用遠端偵錯，然後將偵錯工具附加至角色執行個體來進行偵錯。 如需詳細資訊，請參閱 [在您的本機電腦上偵錯您的雲端服務](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer)。

## <a name="using-azure-diagnostics"></a>使用 Azure 診斷 
不論角色是在開發環境中或在 Azure 中執行，您都可以使用 Azure 診斷來記錄在角色內執行的程式碼中的詳細資訊。 如需詳細資訊，請參閱 [在 Azure 雲端服務中啟用 Azure 診斷](http://go.microsoft.com/fwlink/p/?LinkId=400450)。

## <a name="using-intellitrace"></a>使用 IntelliTrace 
如果您使用 Visual Studio Enterprise 來撰寫適用目標為 .NET Framework 4.5 的角色，您可以在從 Visual Studio 部署 Azure 雲端服務時啟用 IntelliTrace。 IntelliTrace 提供您可搭配 Visual Studio 使用於偵錯應用程式 (如同在 Azure 中執行) 的記錄檔。 如需詳細資訊，請參閱 [使用 IntelliTrace 和 Visual Studio 進行已發佈的雲端服務偵錯](http://go.microsoft.com/fwlink/p/?LinkId=623016)。

## <a name="remote-debugging"></a>遠端偵錯 
您可以在從 Visual Studio 部署雲端服務時，啟用雲端服務的遠端偵錯。 如果您選擇對部署啟用遠端偵錯，則會在執行每個角色執行個體的虛擬機器上安裝遠端偵錯服務。 這些服務 (例如 `msvsmon.exe`) 不會影響效能或造成額外成本。 如需詳細資訊，請參閱 [在 Azure 中偵錯雲端服務](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure)。

## <a name="next-steps"></a>後續步驟
- [在 Visual Studio 中進行 Azure 雲端服務或 VM 的偵錯](./vs-azure-tools-debug-cloud-services-virtual-machines.md) - 了解如何進行 Azure 雲端服務偵錯的詳細資料。