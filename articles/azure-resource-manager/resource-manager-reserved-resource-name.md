---
title: "Azure 保留資源名稱的錯誤 | Microsoft Docs"
description: "說明當提供的資源名稱包含保留字時應如何解決錯誤。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: support-article
ms.date: 11/08/2017
ms.author: tomfitz
ms.openlocfilehash: 2f06b7bc65ea309bc5374b41f402f8e7bc4d2a38
ms.sourcegitcommit: adf6a4c89364394931c1d29e4057a50799c90fc0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="resolve-reserved-resource-name-errors"></a>解決保留資源名稱的錯誤

本文說明當您部署的資源名稱包含保留字時會發生的錯誤。

## <a name="symptom"></a>徵狀

當您部署的資源可透過公用端點取得時，可能會遇到下列錯誤：

```
Code=ReservedResourceName;
Message=The resource name <resource-name> or a part of the name is a trademarked or reserved word.
```

## <a name="cause"></a>原因

如果資源具有公用端點，其名稱就不能使用保留字或商標。

下列為保留字：

* ACCESS
* AZURE
* BING
* BIZSPARK
* BIZTALK
* CORTANA
* DIRECTX
* DOTNET
* DYNAMICS
* EXCEL
* EXCHANGE
* FOREFRONT
* GROOVE
* HOLOLENS
* HYPERV
* KINECT
* LYNC
* MSDN
* O365
* OFFICE
* OFFICE365
* ONEDRIVE
* ONENOTE
* OUTLOOK
* POWERPOINT
* SHAREPOINT
* SKYPE
* VISIO
* VISUALSTUDIO

下列為不得在名稱中作為全字拼寫或子字串的字：

* LOGIN
* MICROSOFT
* WINDOWS
* XBOX

## <a name="solution"></a>方案

提供名稱時，不要使用任何一個保留字。