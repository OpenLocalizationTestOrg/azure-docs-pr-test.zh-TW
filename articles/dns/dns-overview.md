---
title: "Azure DNS 的 aaaOverview |Microsoft 文件"
description: "在 Microsoft Azure 上裝載 Azure DNS 服務的概觀。 在 Microsoft Azure 上裝載您的網域。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a>Azure DNS 概觀

hello 網域名稱系統或 DNS，負責將轉譯 （或解決） 的網站或服務名稱 tooits IP 位址。 Azure DNS 是 DNS 網域的主機服務，採用 Microsoft Azure 基礎結構提供名稱解析。 裝載您在 Azure 中的網域，您可以管理您的 DNS 記錄使用相同的認證、 Api、 工具和計費 hello 與其他 Azure 服務。

![DNS 概觀](./media/dns-overview/scenario.png)

## <a name="features"></a>特性

* **可靠性和效能** - Azure DNS 中的 DNS 網域是裝載於 Azure 的 DNS 名稱伺服器全球網路。 我們使用任一傳播網路，讓每個 DNS 查詢由 hello 最接近可用 DNS 伺服器回應。 這為您的網域提供快速的效能與高可用性。

* **緊密整合**-hello Azure DNS 服務可以使用的 toomanage Azure 服務的 DNS 記錄，而且可以是使用的 tooprovide DNS，針對您外部的資源。 Azure DNS 整合 hello Azure 入口網站中，而且會使用相同的認證、 帳單和支援合約 hello 與其他 Azure 服務。

* **安全性**-hello Azure DNS 服務採用 Azure 資源管理員。 因此可得益於 Resource Manager 的功能，如角色型存取控制、稽核記錄檔、資源鎖定。 您的網域和記錄可以透過 hello Azure 入口網站，Azure PowerShell cmdlet，管理和 hello 跨平台 Azure CLI。 需要 DNS 的自動管理的應用程式可以整合透過 hello hello 服務 REST API 和 Sdk。

Azure DNS 目前不支援購買網域名稱。 如果您想 toopurchase 網域時，您會需要 toouse 第三方網域名稱註冊機構。 hello 註冊機構通常費用小年費。 hello 網域的 DNS 記錄管理然後裝載在 Azure DNS。 請參閱[委派網域 tooAzure DNS](dns-domain-delegation.md)如需詳細資訊。

## <a name="pricing"></a>價格

DNS 計費根據裝載在 Azure 中並以 hello 的 DNS 查詢的 DNS 區域的 hello 數目而定。 深入了解定價，請造訪 toolearn [Azure DNS 定價](https://azure.microsoft.com/pricing/details/dns/)。

## <a name="faq"></a>常見問題集

常見問題集疑問 Azure DNS 的詳細資訊，請參閱 hello [Azure DNS 常見問題集](dns-faq.md)。

## <a name="next-steps"></a>後續步驟

如需深入了解 DNS 區域和記錄，請瀏覽：[DNS 區域和記錄的概觀](dns-zones-records.md)。

了解如何太[建立 DNS 區域](./dns-getstarted-create-dnszone-portal.md)Azure DNS 中。

深入了解一些 hello 另一個索引鍵[網路功能](../networking/networking-overview.md)的 Azure。

