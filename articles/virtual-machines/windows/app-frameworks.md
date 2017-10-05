---
title: "在 Azure 中的 Windows VM 上部署應用程式架構 | Microsoft Docs"
description: "使用 Azure Resource Manager 範本在 Windows VM 上建立熱門的應用程式架構，以安裝 Active Directory、Docker 等等。"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 67a67141-b095-44ff-bfdf-7311d1c28b89
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 275342413c6f4a9efc7a056bdc80b6489536576f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-popular-application-frameworks-on-windows-using-azure-resource-manager-templates"></a><span data-ttu-id="51673-103">使用 Azure Resource Manager 範本在 Windows 上部署熱門的應用程式架構</span><span class="sxs-lookup"><span data-stu-id="51673-103">Deploy popular application frameworks on Windows using Azure Resource Manager templates</span></span> 

<span data-ttu-id="51673-104">工作負載的設計讓它通常需要許多資源才能運作。</span><span class="sxs-lookup"><span data-stu-id="51673-104">Workloads usually require many resources to function according to design.</span></span> <span data-ttu-id="51673-105">Azure 資源管理員範本不只能讓您定義應用程式的設定方式，更能讓您定義如何將資源應加以部署，使其支援已設定的應用程式。</span><span class="sxs-lookup"><span data-stu-id="51673-105">Azure Resource Manager templates make it possible for you to not only define how applications are configured, but also how the resources are deployed to support configured applications.</span></span> <span data-ttu-id="51673-106">本文介紹資源庫中最熱門的範本，並提供您有關使用 Azure 入口網站、Azure CLI 或 PowerShell 來部署這些範本的資訊。</span><span class="sxs-lookup"><span data-stu-id="51673-106">This article introduces you to the most popular templates in the gallery and gives you information for using the Azure portal, Azure CLI, or PowerShell to deploy them.</span></span>

[!INCLUDE [virtual-machines-common-app-frameworks](../../../includes/virtual-machines-common-app-frameworks.md)]

