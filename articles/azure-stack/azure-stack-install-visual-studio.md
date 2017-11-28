---
title: "aaaInstall Visual Studio 並連接 tooAzure 堆疊 |Microsoft 文件"
description: "了解 hello 步驟所需 tooinstall Visual Studio 並連接 tooAzure 堆疊"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: aa63f9eaf5cd72a0b2f31256c2df99fb41ca11fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-connect-tooazure-stack"></a><span data-ttu-id="34865-103">安裝 Visual Studio 並連接 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="34865-103">Install Visual Studio and connect tooAzure Stack</span></span>

<span data-ttu-id="34865-104">使用 Visual Studio tooauthor 和部署 Azure 資源管理員[範本](azure-stack-arm-templates.md)Azure 堆疊中。</span><span class="sxs-lookup"><span data-stu-id="34865-104">Use Visual Studio tooauthor and deploy Azure Resource Manager [templates](azure-stack-arm-templates.md) in Azure Stack.</span></span> <span data-ttu-id="34865-105">您可以使用 hello 或是此發行項 tooinstall Visual Studio 中所述的步驟從[Azure 堆疊開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 的外部用戶端如果透過連接[VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)。</span><span class="sxs-lookup"><span data-stu-id="34865-105">You can use hello steps described in this article tooinstall Visual Studio either from [Azure Stack Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are connected through [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span> <span data-ttu-id="34865-106">這些逐步執行將會全新安裝 Visual Studio 2015 Community 版本。</span><span class="sxs-lookup"><span data-stu-id="34865-106">These steps perform a new installation of Visual Studio 2015 Community Edition.</span></span> <span data-ttu-id="34865-107">深入了解關於在其他 Visual Studio 版本之間的[共存](https://msdn.microsoft.com/library/ms246609.aspx)。</span><span class="sxs-lookup"><span data-stu-id="34865-107">Read more about [coexistence](https://msdn.microsoft.com/library/ms246609.aspx) between other Visual Studio versions.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="34865-108">安裝 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34865-108">Install Visual Studio</span></span>
1. <span data-ttu-id="34865-109">下載並執行 hello [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="34865-109">Download and run hello [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>             
2. <span data-ttu-id="34865-110">搜尋**Visual Studio Community 2015 與 Microsoft Azure SDK - 2.9.6**；按一下 [新增]，然後 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="34865-110">Search for **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**, click **Add**, and **Install**.</span></span>

    ![WebPI 安裝逐步執行的螢幕擷取畫面](./media/azure-stack-install-visual-studio/image1.png) 

3. <span data-ttu-id="34865-112">解除安裝 hello **Microsoft Azure PowerShell** hello Azure SDK 的一部分安裝。</span><span class="sxs-lookup"><span data-stu-id="34865-112">Uninstall hello **Microsoft Azure PowerShell** that is installed as part of hello Azure SDK.</span></span>

    ![Azure PowerShell 新增/移除程式介面的螢幕擷取畫面](./media/azure-stack-install-visual-studio/image2.png) 

4. [<span data-ttu-id="34865-114">安裝 Azure Stack 適用的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="34865-114">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)

5. <span data-ttu-id="34865-115">Hello 安裝完成之後，請重新啟動 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="34865-115">Restart hello operating system after hello installation completes.</span></span>

## <a name="connect-tooazure-stack"></a><span data-ttu-id="34865-116">連接 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="34865-116">Connect tooAzure Stack</span></span>

1. <span data-ttu-id="34865-117">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="34865-117">Launch Visual Studio.</span></span>

2. <span data-ttu-id="34865-118">從 hello**檢視**功能表上，選取**Cloud Explorer**。</span><span class="sxs-lookup"><span data-stu-id="34865-118">From hello **View** menu, select **Cloud Explorer**.</span></span>

3. <span data-ttu-id="34865-119">在 hello 新窗格中，選取 **新增帳戶**並以您的 Azure Active Directory 認證登入。</span><span class="sxs-lookup"><span data-stu-id="34865-119">In hello new pane, select **Add Account** and sign in with your Azure Active Directory credentials.</span></span>  
    <span data-ttu-id="34865-120">![Cloud Explorer 螢幕擷取畫面一次登入，而且連接 tooAzure 堆疊](./media/azure-stack-install-visual-studio/image6.png)</span><span class="sxs-lookup"><span data-stu-id="34865-120">![Screenshot of Cloud Explorer once logged in and connected tooAzure Stack](./media/azure-stack-install-visual-studio/image6.png)</span></span>

<span data-ttu-id="34865-121">登入之後，您可以[部署範本](azure-stack-deploy-template-visual-studio.md)或瀏覽可用的資源類型和資源群組 toocreate 您自己的範本。</span><span class="sxs-lookup"><span data-stu-id="34865-121">Once logged in, you can [deploy templates](azure-stack-deploy-template-visual-studio.md) or browse available resource types and resource groups toocreate your own templates.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="34865-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34865-122">Next Steps</span></span>

 - [<span data-ttu-id="34865-123">開發適用於 Azure Stack 的範本</span><span class="sxs-lookup"><span data-stu-id="34865-123">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
