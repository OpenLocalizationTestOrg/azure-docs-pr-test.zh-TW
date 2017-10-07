---
title: "aaaOptions 偵錯 Azure 雲端服務 |Microsoft 文件"
description: "進行 Azure 雲端服務的偵錯"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a>了解各種 hello toodebug Azure 雲端服務
本文章提供連結 toohello 各種方式 toodebug Azure 雲端服務。 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>在 Visual Studio 中進行 Azure 雲端服務的偵錯
您可以儲存時間和金錢使用 hello Azure 計算模擬器 toodebug 您的雲端服務在本機電腦上。 透過在部署服務之前於本機偵錯服務，您可以改善可靠性和效能，而不需支付運算時間。 不過，某些錯誤可能只有當您在 Azure 中執行雲端服務時才會發生。 在 Azure 中執行雲端服務時，才會發生的錯誤可以藉由啟用遠端偵錯時您發行服務，並再將 hello 偵錯工具 tooa 角色執行個體附加偵錯。 如需詳細資訊，請參閱 [在您的本機電腦上偵錯您的雲端服務](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer)。

## <a name="using-azure-diagnostics"></a>使用 Azure 診斷 
您可以使用 Azure 診斷 toolog 是否在 hello 開發環境中，或在 Azure 中執行 hello 角色的詳細資訊從角色中的程式碼執行。 如需詳細資訊，請參閱 [在 Azure 雲端服務中啟用 Azure 診斷](http://go.microsoft.com/fwlink/p/?LinkId=400450)。

## <a name="using-intellitrace"></a>使用 IntelliTrace 
如果您使用 Visual Studio Enterprise toowrite 角色目標.NET Framework 4.5，您可以啟用 IntelliTrace，在您部署 Azure 雲端服務從 Visual Studio 的 hello 階段。 IntelliTrace 會提供記錄檔，您可以使用 Visual Studio toodebug 與您的應用程式在 Azure 中執行一樣。 如需詳細資訊，請參閱 [使用 IntelliTrace 和 Visual Studio 進行已發佈的雲端服務偵錯](http://go.microsoft.com/fwlink/p/?LinkId=623016)。

## <a name="remote-debugging"></a>遠端偵錯 
您可以啟用遠端偵錯雲端服務在 hello 階段，當您部署 hello 雲端服務，從 Visual Studio。 如果您選擇 tooenable 遠端偵錯部署，執行每個角色執行個體的 hello 虛擬機器上安裝遠端偵錯服務。 這些服務 (例如 `msvsmon.exe`) 不會影響效能或造成額外成本。 如需詳細資訊，請參閱 [在 Azure 中偵錯雲端服務](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure)。

## <a name="next-steps"></a>後續步驟
- [偵錯 Azure 雲端服務或在 Visual Studio 中的 VM](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -了解如何 toodebug Azure 雲端服務的 hello 詳細資料。
