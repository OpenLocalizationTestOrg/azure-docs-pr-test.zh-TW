---
title: "aaaWindows 驗證和 Azure MFA Server |Microsoft 文件"
description: "這是可協助您部署的 Windows 驗證和 Azure Multi-factor Authentication Server 的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="a8632-103">Windows 驗證與 Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="a8632-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="a8632-104">使用 hello Azure Multi-factor Authentication Server tooenable hello Windows 驗證 區段並設定應用程式的 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="a8632-104">Use hello Windows Authentication section of hello Azure Multi-Factor Authentication Server tooenable and configure Windows authentication for applications.</span></span> <span data-ttu-id="a8632-105">設定 Windows 驗證之前，請記住清單後面的 hello:</span><span class="sxs-lookup"><span data-stu-id="a8632-105">Before you set up Windows Authentication, keep hello following list in mind:</span></span>

* <span data-ttu-id="a8632-106">在安裝之後，重新啟動終端機服務 tootake 效果 hello Azure 多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="a8632-106">After setup, reboot hello Azure Multi-Factor Authentication for Terminal Services tootake effect.</span></span>
* <span data-ttu-id="a8632-107">如果已核取 [需要 Azure Multi-factor Authentication 使用者比對]，而您並不在 hello 使用者清單中，您之後將無法能 toolog hello 機器重新開機。</span><span class="sxs-lookup"><span data-stu-id="a8632-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in hello user list, you will not be able toolog into hello machine after reboot.</span></span>
* <span data-ttu-id="a8632-108">信任的 Ip 是取決於是否 hello 應用程式可以提供 hello 用戶端 IP 與 hello 驗證。</span><span class="sxs-lookup"><span data-stu-id="a8632-108">Trusted IPs is dependent on whether hello application can provide hello client IP with hello authentication.</span></span> <span data-ttu-id="a8632-109">目前僅支援終端機服務。</span><span class="sxs-lookup"><span data-stu-id="a8632-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="a8632-110">這項功能不支援的 toosecure 終端機服務，Windows Server 2012 R2 上。</span><span class="sxs-lookup"><span data-stu-id="a8632-110">This feature is not supported toosecure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a><span data-ttu-id="a8632-111">toosecure 應用程式使用 Windows 驗證時，使用下列程序的 hello。</span><span class="sxs-lookup"><span data-stu-id="a8632-111">toosecure an application with Windows Authentication, use hello following procedure.</span></span>
1. <span data-ttu-id="a8632-112">在 [hello Azure Multi-factor Authentication Server hello Windows 驗證] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a8632-112">In hello Azure Multi-Factor Authentication Server click hello Windows Authentication icon.</span></span>
   <span data-ttu-id="a8632-113">![Windows 驗證](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="a8632-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="a8632-114">檢查 hello**啟用 Windows 驗證**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a8632-114">Check hello **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="a8632-115">預設不核取此方塊。</span><span class="sxs-lookup"><span data-stu-id="a8632-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="a8632-116">hello 應用程式索引標籤可讓 hello 管理員 tooconfigure Windows 驗證的一或多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8632-116">hello Applications tab allows hello administrator tooconfigure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="a8632-117">選取伺服器或應用程式 – 指定是否啟用 hello 伺服器/應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8632-117">Select a server or application – specify whether hello server/application is enabled.</span></span> <span data-ttu-id="a8632-118">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a8632-118">Click **OK**.</span></span>
5. <span data-ttu-id="a8632-119">按一下 [新增...]</span><span class="sxs-lookup"><span data-stu-id="a8632-119">Click **Add…**</span></span>
6. <span data-ttu-id="a8632-120">hello 信任 Ip 索引標籤可讓您源自於特定 Ip 的 tooskip Azure 多重要素驗證的 Windows 工作階段。</span><span class="sxs-lookup"><span data-stu-id="a8632-120">hello Trusted IPs tab allows you tooskip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="a8632-121">例如，如果員工會從 hello 辦公室和家裡使用 hello 應用程式，您可能決定不想其電話響起進行 Azure Multi-factor Authentication 而 hello office。</span><span class="sxs-lookup"><span data-stu-id="a8632-121">For example, if employees use hello application from hello office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at hello office.</span></span> <span data-ttu-id="a8632-122">因此，您可以指定 hello 辦公室子網路作為信任 Ip 項目。</span><span class="sxs-lookup"><span data-stu-id="a8632-122">For this, you would specify hello office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="a8632-123">按一下 [新增...]</span><span class="sxs-lookup"><span data-stu-id="a8632-123">Click **Add…**</span></span>
8. <span data-ttu-id="a8632-124">選取**單一 IP**如果您想要 tooskip 單一 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a8632-124">Select **Single IP** if you would like tooskip a single IP address.</span></span>
9. <span data-ttu-id="a8632-125">選取**IP 範圍**如果您想要 tooskip 整個 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="a8632-125">Select **IP Range** if you would like tooskip an entire IP range.</span></span> <span data-ttu-id="a8632-126">範例：10.63.193.1-10.63.193.100。</span><span class="sxs-lookup"><span data-stu-id="a8632-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="a8632-127">選取**子網路**如果您想要 toospecify Ip 範圍使用子網路標記法。</span><span class="sxs-lookup"><span data-stu-id="a8632-127">Select **Subnet** if you would like toospecify a range of IPs using subnet notation.</span></span> <span data-ttu-id="a8632-128">輸入 hello 子網路的起始 IP 和挑選適當的網路遮罩 hello hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="a8632-128">Enter hello subnet's starting IP and pick hello appropriate netmask from hello drop-down list.</span></span>
11. <span data-ttu-id="a8632-129">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a8632-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8632-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8632-130">Next steps</span></span>

- [<span data-ttu-id="a8632-131">設定 Azure MFA Server 的協力廠商 VPN 應用裝置</span><span class="sxs-lookup"><span data-stu-id="a8632-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="a8632-132">Azure MFA 的強化現有的驗證基礎結構以 hello NPS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="a8632-132">Augment your existing authentication infrastructure with hello NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
