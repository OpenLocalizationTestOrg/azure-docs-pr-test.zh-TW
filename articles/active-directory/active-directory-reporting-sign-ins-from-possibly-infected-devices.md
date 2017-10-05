---
title: "從可能受感染的裝置登入"
description: "包含從可能正在執行某些惡意程式碼 (惡意軟體) 的裝置執行的登入嘗試的報告。"
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: d0361662-d970-4a66-8eb3-72e9f8824dcf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 3809e20937d8d9829675e20f893101cb849dcea2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-possibly-infected-devices"></a>從可能受感染的裝置登入
這份報告會嘗試識別已變成受感染且現在為殭屍網路一部分的使用者裝置。 我們會讓使用者登入的 IP 位址和我們知道與殭屍網路伺服器聯繫的 IP 位址相互關聯。

建議：此報告會標示 IP 位址，而非使用者裝置。 建議您連絡使用者並掃描所有使用者的裝置以便確定。 使用者的個人裝置也可能受到感染，或者與使用者使用相同 IP 位址的其他使用者的裝置可能受到感染。

如需如何處理惡意程式碼感染的詳細資訊，請參閱 [惡意程式碼防護中心](http://go.microsoft.com/fwlink/?linkid=335773)。

![從可能受感染的裝置登入](./media/active-directory-reporting-sign-ins-from-possibly-infected-devices/signInsFromPossiblyInfectedDevices.PNG)

