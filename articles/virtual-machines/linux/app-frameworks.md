---
title: "在 Azure 中的 Linux VM 上部署應用程式架構 | Microsoft Docs"
description: "使用 Azure Resource Manager 範本在 Linux VM 上建立熱門的應用程式架構，以安裝 Active Directory、Docker 等等。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 90e95919-4611-40d7-8fa8-e38facbde9a7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: rasquill
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5d0d064c0afc4a9a5cb802fce66e219d23dc1ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-popular-application-frameworks-on-linux-using-azure-resource-manager-templates"></a><span data-ttu-id="05934-103">使用 Azure Resource Manager 範本在 Linux 上部署熱門的應用程式架構</span><span class="sxs-lookup"><span data-stu-id="05934-103">Deploy popular application frameworks on Linux using Azure Resource Manager templates</span></span>

<span data-ttu-id="05934-104">工作負載的設計讓它通常需要許多資源才能運作。</span><span class="sxs-lookup"><span data-stu-id="05934-104">Workloads usually require many resources to function according to design.</span></span> <span data-ttu-id="05934-105">Azure 資源管理員範本不只能讓您定義應用程式的設定方式，更能讓您定義如何將資源應加以部署，使其支援已設定的應用程式。</span><span class="sxs-lookup"><span data-stu-id="05934-105">Azure Resource Manager templates make it possible for you to not only define how applications are configured, but also how the resources are deployed to support configured applications.</span></span> <span data-ttu-id="05934-106">本文介紹資源庫中最熱門的範本，並提供您有關使用 Azure 入口網站、Azure CLI 或 PowerShell 來部署這些範本的資訊。</span><span class="sxs-lookup"><span data-stu-id="05934-106">This article introduces you to the most popular templates in the gallery and gives you information for using the Azure portal, Azure CLI, or PowerShell to deploy them.</span></span>

[!INCLUDE [virtual-machines-common-app-frameworks](../../../includes/virtual-machines-common-app-frameworks.md)]
