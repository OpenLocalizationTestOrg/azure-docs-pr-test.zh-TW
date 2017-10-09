---
title: "aaaDifferent 方式 toocreate Azure 中的 Windows VM |Microsoft 文件"
description: "列出 hello 不同的方式 toocreate Windows 虛擬機器與資源管理員。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a>不同的方式 toocreate Windows 虛擬機器

因為虛擬機器適用於不同的使用者和用途，azure 將提供不同的方式 toocreate 虛擬機器。 這表示您需要 toomake hello 虛擬機器相關的一些選項以及如何 toocreate 它。 這篇文章會提供這些選項的摘要，並連結 tooinstructions。

## <a name="azure-portal"></a>Azure 入口網站
使用 hello Azure 入口網站是出虛擬機器時，簡單的方式 tootry，特別是如果您剛開始使用 Azure。 

[建立執行 Windows 的 hello 入口網站的虛擬機器](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>範本
虛擬機器需要各種資源 (例如可用性設定組和儲存體帳戶)。 而不是部署與個別管理每個資源，您可以建立的 Azure Resource Manager 範本部署和佈建的所有單一、 協調作業中的 hello 資源。

* [利用 Resource Manager 範本建立 Windows 虛擬機器](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
如果您偏好使用命令殼層，可以使用 Azure PowerShell。

* [使用 PowerShell 建立 Windows VM](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
使用 Visual Studio toobuild、 管理和部署 Vm 使用 hello Azure Tools for Visual Studio 和 hello Azure SDK。

[Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs)

