---
title: "aaaMove Web 應用程式資源 tooanother 資源群組"
description: "描述，您可以移動 Web 應用程式和應用程式服務從一個資源群組 tooanother hello 案例。"
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a>支援的移動組態
您可以移動 Azure Web 應用程式資源使用 hello[資源管理員移動資源 API](../azure-resource-manager/resource-group-move-resources.md)。

Azure Web 應用程式目前支援下列案例移動 hello:

* 將 hello 整個內容 （web 應用程式、 應用程式服務計劃和憑證） 的資源群組移動 tooanother 資源群組。 
   > [!Note]
   > hello 目的地資源群組不能包含在此案例中的任何 Microsoft.Web 資源。

* 時仍在其目前的應用程式服務方案 （hello 應用程式服務計劃會保留在 hello 舊的資源群組） 中裝載這些移動個別的 web 應用程式 tooa 不同資源群組。


