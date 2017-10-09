---
title: "開始使用 Microsoft Azure 上的雲端 Foundry aaaGetting |Microsoft 文件"
description: "在 Microsoft Azure 上執行 OSS 或 Pivotal Cloud Foundry"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a>Azure 上的 Cloud Foundry

Cloud Foundry 是開放原始碼的平台即服務 (PaaS)，可用於建置、部署和操作以各種不同語言和架構開發的 12-factor 應用程式。 本文件說明您的 Azure 和如何開始執行雲端 Foundry hello 選項。

## <a name="cloud-foundry-offerings"></a>Cloud Foundry 供應項目

有兩種形式的雲端 Foundry 在 Azure 上的可用 toorun： 開放原始碼雲端 Foundry (OSS CF) 和關鍵雲端 Foundry (PCF)。 OS CF 是完全[開放原始碼](https://github.com/cloudfoundry)hello 雲端 Foundry Foundation 管理雲端 Foundry 的版本。 關鍵雲端 Foundry 是雲端 Foundry 關鍵軟體 inc.提供的企業分佈我們看看其中一些 hello hello 兩個供應項目之間的差異。

### <a name="open-source-cloud-foundry"></a>開放原始碼的 Cloud Foundry

您可以部署在 Azure 上的 OSS 雲端 Foundry 第一次部署 BOSH 導向器，然後再部署雲端 Foundry，使用 hello [GitHub 上所提供的指示](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md)。 進一步了解使用 OS CF toolearn 看到 hello[文件](https://docs.cloudfoundry.org/)hello 雲端 Foundry Foundation 所提供。

Microsoft 可透過下列社群管道 hello OSS CF 最佳方式支援：

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a>[Cloud Foundry Slack (英文)](https://slack.cloudfoundry.org/) 上的 bosh-azure-cpi 管道
- [cf-bosh 郵寄清單 (英文)](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- Hello 的 GitHub 問題[CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues)和[service broker](https://github.com/Azure/meta-azure-service-broker/issues)

>[!NOTE]
> hello Azure 資源，例如您用來執行雲端 Foundry hello 虛擬機器的支援層級根據您的 Azure 支援合約。 最大速率社群支援只適用於 toohello 雲端 Foundry 特有的元件。

### <a name="pivotal-cloud-foundry"></a>Pivotal Cloud Foundry

關鍵雲端 Foundry 包含 hello hello OSS 分佈，以及一組專屬的管理工具和企業支援為相同的核心平台。 toorun PCF 在 Azure 上，您必須取得授權的 Pivotal。 hello Azure marketplace hello PCF 提供項目包含的 90 天試用版授權。

hello 工具包括[關鍵的 Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/)，web 應用程式，可簡化部署及管理的雲端 Foundry foundation 和[關鍵應用程式管理員](https://docs.pivotal.io/pivotalcf/console/)，來管理 web 應用程式使用者和應用程式。

除了上述的 OSS CF 列出 toohello 支援管道，PCF 授權允許您 toocontact Pivotal 支援。 Microsoft Pivotal 也啟用了支援工作流程可讓您 toocontact 協助任一個合作對象和一定您正確路由，根據 hello 問題的所在位置的問題。

## <a name="azure-service-broker"></a>Azure Service Broker

雲端 Foundry 鼓勵 hello ["12 個因素 app"](https://12factor.net/)升級清楚分隔無狀態應用程式處理序與備份服務的可設定狀態的方法。 [Service broker](https://docs.cloudfoundry.org/services/api.html)提供一致的方式 tooprovision 並繫結支援服務 tooapplications。 hello [Azure 服務 broker](https://github.com/Azure/meta-azure-service-broker)提供了一些 hello 透過此通道，包括 Azure 儲存體和 Azure SQL 主要 Azure 服務。

如果您使用關鍵雲端 Foundry，hello service broker 也會[可用為方塊](https://docs.pivotal.io/azure-sb/installing.html)從 hello 關鍵的網路。

## <a name="related-resources"></a>相關資源

### <a name="visual-studio-team-services-plugin"></a>Visual Studio Team Services 外掛程式

雲端 Foundry 是很適合的 tooagile 軟體開發，包含 hello 使用持續整合 (CI) 和持續傳遞 (CD)。 如果您使用 Visual Studio Team Services (VSTS) toomanage 您的專案，並希望 tooset 總目標雲端 Foundry CI/CD 管線，您可以使用 hello [VSTS 雲端 Foundry 建置延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension)。 hello 外掛程式可讓簡單 tooconfigure 並自動化部署 tooCloud Foundry，是否在 Azure 或另一個執行環境。

## <a name="next-steps"></a>後續步驟

- [從 hello Azure Marketplace 中部署關鍵雲端 Foundry](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [部署應用程式 tooCloud Foundry 在 Azure 中](./cloudfoundry-deploy-your-first-app.md)
