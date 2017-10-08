---
title: "aaaUnderstanding Azure 堆疊中的 DNS |Microsoft 文件"
description: "了解 Azure Stack 中的 DNS 特性與功能"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 60f5ac85-be19-49ac-a7c1-f290d682b5de
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: f60128cf98af8e98ac2bc87172b54132ed06cd8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-idns-for-azure-stack"></a>適用於 Azure Stack 的 iDNS 簡介
================================

Idn 是 tooresolve 外部 DNS 名稱 （例如 http://www.bing.com) 可讓您的 Azure 堆疊中的功能。
它也可讓您 tooregister 內部虛擬網路名稱。 如此一來，您可以在相同的虛擬網路名稱，而不是 IP 位址，而不需要自訂 DNS 伺服器項目 tooprovide hello 解決 Vm。

這是 Azure 中的內建功能，但是也可以在 Windows Server 2016 和 Azure Stack 中使用。

## <a name="what-does-idns-do"></a>iDNS 的用途為何？
透過 Azure 堆疊中的 Idn，您可以取得下列功能，而不需要自訂 DNS 伺服器項目 toospecify hello。

* 適用於租用戶工作負載的共用 DNS 名稱解析服務。
* 名稱解析和 hello 租用戶虛擬網路內的 DNS 登錄的授權 DNS 服務。
* 從租用戶 VM 解析網際網路名稱的遞迴 DNS 服務。 租用戶不再需要 toospecify 自訂 DNS 項目 tooresolve 網際網路名稱 (例如，www.bing.com)。

您仍然可以沿用您自己的 DNS，也可以使用自訂的 DNS 伺服器 (如果您想要的話)。 但現在，如果您只想 toobe 無法 tooresolve 網際網路 DNS 名稱，而且可以 tooconnect tooother 虛擬機器中的 hello 相同虛擬網路，您不需要 toospecify 任何項目而且也能夠運作。

## <a name="what-does-idns-not-do"></a>iDNS 不適用於哪些用途？
哪些 Idn 不允許您 toodo 是建立可從外部 hello 虛擬網路解析的名稱的 DNS 記錄。

在 Azure 中，您可以 hello 選擇指定的公用 IP 位址與相關聯的 DNS 名稱標籤。 您可以選擇 hello 標籤 （前置詞），但 Azure 選擇 hello 後置詞，您可以在其中建立 hello 公用 IP 位址的 hello 區域為基礎。

![DNS 名稱標籤的螢幕擷取畫面](media/azure-stack-understanding-dns-in-tp2/image3.png)

Hello 在圖中，Azure 會建立"A"記錄在 DNS 中的 hello hello 區域底下指定的 DNS 名稱標籤**westus.cloudapp.azure.com**。前置詞和 hello 尾碼一起構成完整限定網域名稱 (FQDN)，可以從任何地方解決的 hello 公用網際網路。

Azure 堆疊只支援 Idn 的內部名稱登錄，因此無法 hello 遵循。

* 在現有的託管 DNS 區域 (例如 local.azurestack.external) 底下建立 DNS 記錄。
* 建立 DNS 區域 (例如 Contoso.com)。
* 在您自己的自訂 DNS 區域底下建立記錄。
* 支援 hello 購買網域名稱。

