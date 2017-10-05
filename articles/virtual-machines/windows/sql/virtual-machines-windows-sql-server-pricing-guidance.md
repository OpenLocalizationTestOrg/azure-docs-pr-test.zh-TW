---
title: "有效地管理 Azure 虛擬機器上 SQL Server 的成本 | Microsoft Docs"
description: "提供選擇正確 SQL Server 虛擬機器定價模型的最佳做法。"
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 29a92f0c70bffedeb75c50b7fc3b687ee5ee227d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a><span data-ttu-id="4a288-103">SQL Server Azure VM 的定價指導方針</span><span class="sxs-lookup"><span data-stu-id="4a288-103">Pricing guidance for SQL Server Azure VMs</span></span>

<span data-ttu-id="4a288-104">本主題提供 Azure 中 SQL Server 虛擬機器的定價指導方針。</span><span class="sxs-lookup"><span data-stu-id="4a288-104">This topic provides pricing guidance for SQL Server virtual machines in Azure.</span></span> <span data-ttu-id="4a288-105">影響成本的選項有數個，而挑選平衡成本和業務需求的正確映像相當重要。</span><span class="sxs-lookup"><span data-stu-id="4a288-105">There are several options that affect cost, and it is important to pick the right image that balances costs with business requirements.</span></span>

## <a name="free-licensed-sql-server-editions"></a><span data-ttu-id="4a288-106">免費授權的 SQL Server 版本</span><span class="sxs-lookup"><span data-stu-id="4a288-106">Free-licensed SQL Server editions</span></span>

<span data-ttu-id="4a288-107">如果您想要開發、測試或建置某項概念證明，則請使用免費授權的 **SQL Server Developer 版**。</span><span class="sxs-lookup"><span data-stu-id="4a288-107">If you want to develop, test, or build a proof of concept, then use the free-licensed **SQL Server Developer edition**.</span></span> <span data-ttu-id="4a288-108">此版本包含 SQL Server Enterprise 版的所有功能，因此，您可以使用它來建置您想要的任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a288-108">This edition has everything in SQL Server Enterprise edition, thus you can use it to build whatever application you want.</span></span> <span data-ttu-id="4a288-109">唯一不允許的是以生產環境執行。</span><span class="sxs-lookup"><span data-stu-id="4a288-109">It’s just not allowed to run in production.</span></span> <span data-ttu-id="4a288-110">SQL Server Developer VM 只會收取 VM 費用，不會收取 SQL Server 授權費用。</span><span class="sxs-lookup"><span data-stu-id="4a288-110">A SQL Server Developer VM will only charge for the cost of the VM, not for SQL Server licensing.</span></span>

<span data-ttu-id="4a288-111">如果您想要以生產環境執行輕量型工作負載 (< 4 個核心、< 1 GB 記憶體、< 10 GB/資料庫)，則請使用免費授權的 **SQL Server Express 版**。</span><span class="sxs-lookup"><span data-stu-id="4a288-111">If you want to run a lightweight workload in production (<4 cores, <1 GB memory, <10 GB/database), then use the free-licensed **SQL Server Express edition**.</span></span> <span data-ttu-id="4a288-112">SQL Express VM 只會收取 VM 費用，不會收取 SQL 授權費用。</span><span class="sxs-lookup"><span data-stu-id="4a288-112">A SQL Express VM will only charge for the cost of the VM, not SQL licensing.</span></span>

<span data-ttu-id="4a288-113">針對這些開發/測試或輕量型生產環境工作負載，您也可以選擇符合這些工作負載的較小 VM 大小來節省成本。</span><span class="sxs-lookup"><span data-stu-id="4a288-113">For these development/test or lightweight production workloads, you can also save money by choosing a smaller VM size that matches these workloads.</span></span> <span data-ttu-id="4a288-114">DS1v2 可能是這些工作負載的理想選擇。</span><span class="sxs-lookup"><span data-stu-id="4a288-114">The DS1v2 might be a good choice for these workloads.</span></span>

<span data-ttu-id="4a288-115">若要使用上述其中一個映像來建立 SQL Server 2016 Azure VM，請參閱下列連結：</span><span class="sxs-lookup"><span data-stu-id="4a288-115">To create a SQL Server 2016 Azure VM with one of these images, see the following links:</span></span>

- [<span data-ttu-id="4a288-116">SQL Server 2016 Developer Azure VM</span><span class="sxs-lookup"><span data-stu-id="4a288-116">SQL Server 2016 Developer Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [<span data-ttu-id="4a288-117">SQL Server 2016 Express Azure VM</span><span class="sxs-lookup"><span data-stu-id="4a288-117">SQL Server 2016 Express Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a><span data-ttu-id="4a288-118">付費的 SQL Server 版本</span><span class="sxs-lookup"><span data-stu-id="4a288-118">Paid SQL Server editions</span></span>

<span data-ttu-id="4a288-119">如果您的生產環境工作負載並非輕量型，請使用下列其中一個 SQL Server 版本：</span><span class="sxs-lookup"><span data-stu-id="4a288-119">If you have a non-lightweight production workload, use one of the following SQL Server editions:</span></span>

| <span data-ttu-id="4a288-120">SQL Server 版本</span><span class="sxs-lookup"><span data-stu-id="4a288-120">SQL Server Edition</span></span> | <span data-ttu-id="4a288-121">工作負載</span><span class="sxs-lookup"><span data-stu-id="4a288-121">Workload</span></span> |
|-----|-----|
| <span data-ttu-id="4a288-122">Web</span><span class="sxs-lookup"><span data-stu-id="4a288-122">Web</span></span> | <span data-ttu-id="4a288-123">小型網站</span><span class="sxs-lookup"><span data-stu-id="4a288-123">Small web sites</span></span> |
| <span data-ttu-id="4a288-124">標準</span><span class="sxs-lookup"><span data-stu-id="4a288-124">Standard</span></span> | <span data-ttu-id="4a288-125">小型到中型工作負載</span><span class="sxs-lookup"><span data-stu-id="4a288-125">Small to medium workloads</span></span> |
| <span data-ttu-id="4a288-126">Enterprise</span><span class="sxs-lookup"><span data-stu-id="4a288-126">Enterprise</span></span> | <span data-ttu-id="4a288-127">大型或任務關鍵性工作負載</span><span class="sxs-lookup"><span data-stu-id="4a288-127">Large or mission-critical workloads</span></span>|

<span data-ttu-id="4a288-128">您有兩個選項來支付這些版本的 SQL Server 授權：「依使用量付費」或「自備授權」。</span><span class="sxs-lookup"><span data-stu-id="4a288-128">You have two options to pay for SQL Server licensing for these editions: *pay per usage* or *bring your own license*.</span></span>

### <a name="pay-per-usage"></a><span data-ttu-id="4a288-129">依使用量付費</span><span class="sxs-lookup"><span data-stu-id="4a288-129">Pay per usage</span></span>

<span data-ttu-id="4a288-130">**依使用量支付 SQL Server 授權費用**意謂著執行 Azure VM 的每分鐘費用都包含 SQL Server 授權的費用。</span><span class="sxs-lookup"><span data-stu-id="4a288-130">**Paying the SQL Server license per usage** means that the per-minute cost of running the Azure VM includes the cost of the SQL Server license.</span></span> <span data-ttu-id="4a288-131">您可以在 [Azure VM 定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard)查看不同 SQL Server 版本 (Web、Standard、Enterprise) 的定價。</span><span class="sxs-lookup"><span data-stu-id="4a288-131">You can see the pricing for the different SQL Server editions (Web, Standard, Enterprise) in the [Azure VM pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).</span></span> <span data-ttu-id="4a288-132">所有 SQL Server 版本 (2008 R2 到 2016) 的費用都相同。</span><span class="sxs-lookup"><span data-stu-id="4a288-132">The cost is the same for all versions of SQL Server (2008 R2 to 2016).</span></span> <span data-ttu-id="4a288-133">一般就 SQL Server 授權而言，每分鐘的授權費用會取決於 VM 核心數量。</span><span class="sxs-lookup"><span data-stu-id="4a288-133">As with SQL Server licensing in general, the per-minute licensing cost depends on the number of VM cores.</span></span>

<span data-ttu-id="4a288-134">針對下列情況，建議採用依使用量支付 SQL Server 授權費用：</span><span class="sxs-lookup"><span data-stu-id="4a288-134">Paying the SQL Server licensing per usage is recommended for:</span></span>

- <span data-ttu-id="4a288-135">暫時或定期的工作負載。</span><span class="sxs-lookup"><span data-stu-id="4a288-135">Temporary or periodic workloads.</span></span> <span data-ttu-id="4a288-136">例如，每年有幾個月需要支援某個事件或每週一需要支援業務分析的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a288-136">For example, an app that needs to support an event for a couple of months every year, or business analysis on Mondays.</span></span>
- <span data-ttu-id="4a288-137">存留期或規模不明的工作負載。</span><span class="sxs-lookup"><span data-stu-id="4a288-137">Workloads with unknown lifetime or scale.</span></span> <span data-ttu-id="4a288-138">例如，有幾個月不需用到或依需求可能需要較多或較少運算能力的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a288-138">For example, an app that may not be required in a few months, or which may require more, or less compute power, depending on demand.</span></span>

<span data-ttu-id="4a288-139">若要使用上述其中一個依使用量付費的映像來建立 SQL Server 2016 Azure VM，請參閱下列連結：</span><span class="sxs-lookup"><span data-stu-id="4a288-139">To create a SQL Server 2016 Azure VM with one of these pay-per-usage images, see the following links:</span></span>

- [<span data-ttu-id="4a288-140">SQL Server 2016 Web Azure VM</span><span class="sxs-lookup"><span data-stu-id="4a288-140">SQL Server 2016 Web Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [<span data-ttu-id="4a288-141">SQL Server 2016 Standard Azure VM</span><span class="sxs-lookup"><span data-stu-id="4a288-141">SQL Server 2016 Standard Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [<span data-ttu-id="4a288-142">SQL Server 2016 Enterprise Azure VM</span><span class="sxs-lookup"><span data-stu-id="4a288-142">SQL Server 2016 Enterprise Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> <span data-ttu-id="4a288-143">在 Azure 入口網站中建立 SQL Server 虛擬機器時，[選擇大小] 刀鋒視窗上顯示的估計每月費用並不包含 SQL Server 授權費用。</span><span class="sxs-lookup"><span data-stu-id="4a288-143">When you create a SQL Server virtual machine in the Azure portal, the estimated monthly cost displayed on the **Choose a size** blade does not include SQL Server licensing costs.</span></span> <span data-ttu-id="4a288-144">這是 VM 單獨的成本。</span><span class="sxs-lookup"><span data-stu-id="4a288-144">This is the cost of the VM alone.</span></span>
>
> ![選擇 VM 大小刀鋒視窗](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
><span data-ttu-id="4a288-146">就免費授權的 SQL Server Express 和 Developer 版本而言，這是預估的總費用。</span><span class="sxs-lookup"><span data-stu-id="4a288-146">For the free-licensed Express and Developer editions of SQL Server, this is the total estimated cost.</span></span> <span data-ttu-id="4a288-147">但針對 Web、Standard 及 Enterprise，則請在 [Windows 虛擬機器定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)查看其他 SQL 授權費用。</span><span class="sxs-lookup"><span data-stu-id="4a288-147">But for Web, Standard, and Enterprise, find the additional SQL licensing costs on the [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/).</span></span> <span data-ttu-id="4a288-148">在定價頁面上，選取您的目標 SQL Server 版本。</span><span class="sxs-lookup"><span data-stu-id="4a288-148">On the pricing page, select your target edition of SQL Server.</span></span>

### <a name="bring-your-own-license-byol"></a><span data-ttu-id="4a288-149">自備授權 (BYOL)</span><span class="sxs-lookup"><span data-stu-id="4a288-149">Bring your own license (BYOL)</span></span>

<span data-ttu-id="4a288-150">**透過「授權行動性」自備 SQL Server 授權** (也稱為 **BYOL**) 意謂著在 Azure VM 中使用現有的「SQL Server 大量授權」搭配「軟體保證」。</span><span class="sxs-lookup"><span data-stu-id="4a288-150">**Bringing your own SQL Server license through License Mobility**, also referred to as **BYOL**, means using an existing SQL Server Volume License with Software Assurance in an Azure VM.</span></span> <span data-ttu-id="4a288-151">使用 BYOL 的 SQL Server VM 只會收取執行 VM 的費用，不會收取 SQL Server 授權費用，但前提是您已經透過「大量授權」方案取得授權和「軟體保證」。</span><span class="sxs-lookup"><span data-stu-id="4a288-151">A SQL Server VM using BYOL will only charge for the cost of running the VM, not for SQL Server licensing, given that you have already acquired licenses and Software Assurance through a Volume Licensing program.</span></span>

<span data-ttu-id="4a288-152">針對下列情況，建議採用透過「授權行動性」自備 SQL 授權：</span><span class="sxs-lookup"><span data-stu-id="4a288-152">Bringing your own SQL licensing through License Mobility is recommended for:</span></span>

- <span data-ttu-id="4a288-153">持續性工作負載。</span><span class="sxs-lookup"><span data-stu-id="4a288-153">Continuous workloads.</span></span> <span data-ttu-id="4a288-154">例如，需要全年無休支援業務營運的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a288-154">For example, an app that needs to support business operations 24x7.</span></span>
- <span data-ttu-id="4a288-155">存留期和規模已知的工作負載。</span><span class="sxs-lookup"><span data-stu-id="4a288-155">Workloads with known lifetime and scale.</span></span> <span data-ttu-id="4a288-156">例如，一整年都需要使用且已預測好需求的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a288-156">For example, an app that will be required for the whole year and which demand has been forecasted.</span></span>

<span data-ttu-id="4a288-157">若要搭配 SQL Server VM 使用 BYOL，您必須具備 SQL Server Standard 或 Enterprise 的授權及[軟體保證](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1)，這是透過某些[大量授權](https://www.microsoft.com/en-us/download/details.aspx?id=10585)方案時的必要選項，也是搭配其他方案時的選選購項目。</span><span class="sxs-lookup"><span data-stu-id="4a288-157">To use BYOL with a SQL Server VM, you must have a license for SQL Server Standard or Enterprise and [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), which is a required option through some [Volume Licensing](https://www.microsoft.com/en-us/download/details.aspx?id=10585) programs and an optional purchase with others.</span></span>  <span data-ttu-id="4a288-158">根據協議的類型及數量和 (或) 對 SQL Server 之承諾的不同，透過「大量授權」方案提供的定價層級也會不同。</span><span class="sxs-lookup"><span data-stu-id="4a288-158">The pricing levels provided through Volume Licensing programs varies, based on the type of agreement and the quantity and or commitment to SQL Server.</span></span> <span data-ttu-id="4a288-159">但根據經驗法則，自備授權可為持續性生產環境工作負載提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="4a288-159">But as a rule of thumb, bringing your own license for continuous production workloads has the following benefits:</span></span>

| <span data-ttu-id="4a288-160">BYOL 優點</span><span class="sxs-lookup"><span data-stu-id="4a288-160">BYOL benefit</span></span> | <span data-ttu-id="4a288-161">說明</span><span class="sxs-lookup"><span data-stu-id="4a288-161">Description</span></span> |
|-----|-----|
| <span data-ttu-id="4a288-162">**節省成本**</span><span class="sxs-lookup"><span data-stu-id="4a288-162">**Cost savings**</span></span> | <span data-ttu-id="4a288-163">如果工作負載將持續執行 SQL Server Standard 或 Enterprise 長達「10 個月以上」的時間，則與依使用量付費相比，自備 SQL Server 授權較符合經濟效益。</span><span class="sxs-lookup"><span data-stu-id="4a288-163">Bringing your own SQL Server license is more cost effective than paying it per usage if a workload will run continuously SQL Server Standard or Enterprise for *more than 10 months*.</span></span> |
| <span data-ttu-id="4a288-164">**長期節省**</span><span class="sxs-lookup"><span data-stu-id="4a288-164">**Long-term savings**</span></span> | <span data-ttu-id="4a288-165">平均而言，前 3 年購買或更新 SQL Server 授權可「每年節省 30% 的費用」。</span><span class="sxs-lookup"><span data-stu-id="4a288-165">On average, it is *30% cheaper per year* to buy or renew a SQL Server license for the first 3 years.</span></span> <span data-ttu-id="4a288-166">此外，3 年之後，您就不再需要更新授權，只要支付「軟體保證」費用即可。</span><span class="sxs-lookup"><span data-stu-id="4a288-166">Furthermore, after 3 years, you don’t need to renew the license anymore, just pay for Software Assurance.</span></span> <span data-ttu-id="4a288-167">屆時，將可「節省 200% 的費用」。</span><span class="sxs-lookup"><span data-stu-id="4a288-167">At that point, it is *200% cheaper*.</span></span> |
| <span data-ttu-id="4a288-168">**免費的被動次要複本**</span><span class="sxs-lookup"><span data-stu-id="4a288-168">**Free passive secondary replica**</span></span> | <span data-ttu-id="4a288-169">自備授權的另一個優點是每一 SQL Server 可享有[一個免費的被動次要複本授權](https://azure.microsoft.com/pricing/licensing-faq/)，以用於提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="4a288-169">Another benefit of bringing your own license is the [free licensing for one passive secondary replica](https://azure.microsoft.com/pricing/licensing-faq/) per SQL Server for high availability purposes.</span></span> <span data-ttu-id="4a288-170">這讓高可用性 SQL Server 部署 (例如使用「Always On 可用性群組」) 的授權費用得以砍半。</span><span class="sxs-lookup"><span data-stu-id="4a288-170">This cuts in half the licensing cost of a highly available SQL Server deployment (e.g. using Always On Availability Groups).</span></span> <span data-ttu-id="4a288-171">執行被動次要複本的權限是透過「容錯移轉伺服器軟體保證」權益來提供。</span><span class="sxs-lookup"><span data-stu-id="4a288-171">The rights to run the passive secondary are provided through the Fail-Over Servers Software Assurance benefit.</span></span> |

<span data-ttu-id="4a288-172">若要使用上述其中一個自備授權映像來建立 SQL Server 2016 Azure VM，請查看前面帶有 "{BYOL}" 的 VM：</span><span class="sxs-lookup"><span data-stu-id="4a288-172">To create a SQL Server 2016 Azure VM with one of these bring-your-own-license images, see the VMs prefixed with "{BYOL}":</span></span>

- [<span data-ttu-id="4a288-173">SQL Server 2016 Enterprise Azure VM</span><span class="sxs-lookup"><span data-stu-id="4a288-173">SQL Server 2016 Enterprise Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [<span data-ttu-id="4a288-174">SQL Server 2016 Standard Azure VM</span><span class="sxs-lookup"><span data-stu-id="4a288-174">SQL Server 2016 Standard Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> <span data-ttu-id="4a288-175">請在 10 天內告訴我們您將在 Azure 中使用多少個 SQL Server 授權。</span><span class="sxs-lookup"><span data-stu-id="4a288-175">Please let us know within 10 days how many SQL Server licenses you’ll use in Azure.</span></span> <span data-ttu-id="4a288-176">上述映像的連結包含如何這麼做的相關指示。</span><span class="sxs-lookup"><span data-stu-id="4a288-176">The links to the previous images have instructions on how to do this.</span></span>

## <a name="avoid-unecessary-costs"></a><span data-ttu-id="4a288-177">避免不必要的費用</span><span class="sxs-lookup"><span data-stu-id="4a288-177">Avoid unecessary costs</span></span>

<span data-ttu-id="4a288-178">如果您要使用任何不會持續執行的工作負載，請考慮在非使用中的期間關閉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4a288-178">If you are using any workloads that do not run continuously, consider shutting down the virtual machine during the inactive periods.</span></span> <span data-ttu-id="4a288-179">您只需依據使用量付費。</span><span class="sxs-lookup"><span data-stu-id="4a288-179">You only pay for what you use.</span></span>

<span data-ttu-id="4a288-180">例如，如果您只是要在 Azure VM 上試用 SQL Server，您就不會希望不小心讓它持續執行數週而產生費用。</span><span class="sxs-lookup"><span data-stu-id="4a288-180">For example, if you are simply trying out SQL Server on an Azure VM, you would not want to incur charges by accidentally leaving it running for weeks.</span></span> <span data-ttu-id="4a288-181">其中一個解決方案就是使用[自動關閉功能](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/)。</span><span class="sxs-lookup"><span data-stu-id="4a288-181">One solution is to use the [automatic shutdown feature](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).</span></span>

![SQL VM 自動關閉](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

<span data-ttu-id="4a288-183">自動關閉是 [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab) 所提供的較大一組相似功能的一部分。</span><span class="sxs-lookup"><span data-stu-id="4a288-183">Automatic shutdown is part of a larger set of similar features provided by [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).</span></span>

<span data-ttu-id="4a288-184">針對其他工作負載，請考慮使用指令碼解決方案 (例如 [Azure 自動化](https://azure.microsoft.com/services/automation/)) 來自動關閉並重新啟動 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="4a288-184">For other workflows, consider automatically shutting down and restarting Azure VMs with a scripting solution,such as [Azure Automation](https://azure.microsoft.com/services/automation/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a288-185">將 VM 關閉並解除配置是唯一可以避免產生費用的方式。</span><span class="sxs-lookup"><span data-stu-id="4a288-185">Shutting down and deallocating your VM is the only way to avoid charges.</span></span> <span data-ttu-id="4a288-186">只是停止或使用電源選項來關閉 VM 仍然會產生使用費。</span><span class="sxs-lookup"><span data-stu-id="4a288-186">Simply stopping or using power options to shut down the VM still incurs usage charges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a288-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a288-187">Next steps</span></span>

<span data-ttu-id="4a288-188">如需一般的 Azure 定價指導方針，請參閱[使用 Azure 計費與成本管理避免非預期的成本](../../../billing/billing-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="4a288-188">For general Azure pricing guidance, see [Prevent unexpected costs with Azure billing and cost management](../../../billing/billing-getting-started.md).</span></span>

<span data-ttu-id="4a288-189">如需最新的「虛擬機器」定價 (包括 SQL Server)，請參閱 [Azure VM 定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard)。</span><span class="sxs-lookup"><span data-stu-id="4a288-189">For the latest Virtual Machines pricing, including SQL Server, see the [Azure VM pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).</span></span>

<span data-ttu-id="4a288-190">請檢閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)中的其他「SQL Server 虛擬機器」主題。</span><span class="sxs-lookup"><span data-stu-id="4a288-190">Review other SQL Server Virtual Machine topics at [SQL Server on Azure Virtual Machines Overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
