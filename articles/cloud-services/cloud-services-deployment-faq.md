---
title: "Microsoft Azure 雲端服務的常見問題集 aaaDeployment 問題 |Microsoft 文件"
description: "本文列出 Microsoft Azure 雲端服務的部署有關的常見問題集 hello。"
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 8d67e36aa87fb5794d358e5cc235123ac7286028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Azure 雲端服務之部署問題：常見問題集 (FAQ)

本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之部署問題的相關常見問題集。 此外，您也可以參考 hello[雲端服務 VM 大小頁面](cloud-services-sizes-specs.md)大小資訊。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-toohello-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-hello-production-slot"></a>為什麼部署雲端服務 toohello 有時 staging 位置失敗，資源配置錯誤如果已經有 hello 生產位置中的現有部署？
如果雲端服務中任一位置部署，hello 整個雲端服務是已釘選的 tooa 特定叢集。 這表示，如果部署已經存在於 hello 生產位置，新的預備環境部署只可配置在 hello 相同叢集為 hello 生產位置。

您的雲端服務所在的 hello 叢集沒有足夠實體計算資源 toosatisfy 部署要求時，就會發生配置失敗。

如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a>為什麼將雲端服務部署向上擴充或相應放大有時會造成配置失敗？
部署雲端服務時，它通常會取得已釘選的 tooa 特定叢集。 這表示向上延展/出現有雲端服務必須配置 hello 中的新執行個體相同的叢集。 如果 hello 叢集已接近其容量或 hello 所需的 VM 大小/類型無法使用，hello 要求可能會失敗。

如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a>為什麼將雲端服務部署至同質群組時，有時會造成配置失敗？
可以由任何在該區域中，叢集中的 hello 網狀架構配置新的部署 tooan 空的雲端服務，除非 hello 雲端服務是已釘選的 tooan 同質群組。 部署 toohello 相同同質群組將會在 hello 嘗試相同的叢集。 如果 hello 叢集已接近其容量，hello 要求可能會失敗。

如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-tooan-existing-cloud-service-sometimes-result-in-allocation-failure"></a>為什麼沒有變更 VM 大小或新增新 VM tooan 現有的雲端服務，有時會造成配置失敗？
在資料中心的 hello 群集可能會有不同的電腦類型 （例如，系列、 Av2 系列、 D 系列、 Dv2 數列、 G 系列、 H 數列等） 的設定。 但是並非所有的 hello 叢集一定會有所有的 hello 種類的 Vm。 例如，如果您嘗試 tooadd D 系列中的數列僅限叢集已部署的 VM tooa 雲端服務時，就會發生配置失敗。 這將也會發生如果您嘗試 toochange VM SKU 大小 （例如，從 A tooa D 數列切換）。

如需緩和這種配置失敗的協助，請參閱[雲端服務配置失敗：解決方案](cloud-services-allocation-failures.md#solutions)。

toocheck hello 可用的大小在區域中，請參閱[Microsoft Azure： 依地區可用的產品](https://azure.microsoft.com/regions/services)。

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-toolimitsquotasconstraints-on-my-subscription-or-service"></a>為什麼部署雲端服務有時失敗到期 toolimits/配額/條件約束我的訂用帳戶或服務？
如果配置需要的 toobe hello 資源超過 hello 預設值或允許您的服務在 hello 區域/資料中心層級的最大配額，雲端服務部署可能會失敗。 如需詳細資訊，請參閱[雲端服務限制](../azure-subscription-service-limits.md#cloud-services-limits)。

您也可以在 hello 入口網站訂用帳戶在追蹤 hello 目前使用量/配額： Azure 入口網站 = > 訂用帳戶 = >\<適當的訂用帳戶 > = > [使用方式 + 配額]。

也可以透過 hello Azure 計費 Api 擷取資源使用量/耗用量的相關資訊。 請參閱 [Azure 資源使用情況 API (預覽)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview)。

## <a name="how-can-i-change-hello-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a>如何變更已部署的雲端服務 VM 的 hello 大小必須重新部署它？
您無法變更已部署的雲端服務的 hello VM 大小，必須重新部署它。 hello VM 大小是內建 hello CSDEF，只可使用重新部署更新。

如需詳細資訊，請參閱[如何 tooupdate 雲端服務](cloud-services-update-azure-service.md)。

 
