---
title: "有效的 Azure 虛擬機器上的 SQL Server 的 aaaManage 成本 |Microsoft 文件"
description: "選擇 hello 右 SQL Server 虛擬機器定價模型提供最佳作法。"
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
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a><span data-ttu-id="fdf6c-103">SQL Server Azure VM 的定價指導方針</span><span class="sxs-lookup"><span data-stu-id="fdf6c-103">Pricing guidance for SQL Server Azure VMs</span></span>

<span data-ttu-id="fdf6c-104">本主題提供 Azure 中 SQL Server 虛擬機器的定價指導方針。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-104">This topic provides pricing guidance for SQL Server virtual machines in Azure.</span></span> <span data-ttu-id="fdf6c-105">有幾個選項會影響成本，而且重要 toopick hello 右側影像成本的商務需求之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-105">There are several options that affect cost, and it is important toopick hello right image that balances costs with business requirements.</span></span>

## <a name="free-licensed-sql-server-editions"></a><span data-ttu-id="fdf6c-106">免費授權的 SQL Server 版本</span><span class="sxs-lookup"><span data-stu-id="fdf6c-106">Free-licensed SQL Server editions</span></span>

<span data-ttu-id="fdf6c-107">如果您想 toodevelop，測試，或建立概念證明，然後使用 hello 釋出授權**SQL Server Developer edition**。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-107">If you want toodevelop, test, or build a proof of concept, then use hello free-licensed **SQL Server Developer edition**.</span></span> <span data-ttu-id="fdf6c-108">這個版本的所有項目已在 SQL Server Enterprise edition 中，因此您可以使用它 toobuild 任何您想要的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-108">This edition has everything in SQL Server Enterprise edition, thus you can use it toobuild whatever application you want.</span></span> <span data-ttu-id="fdf6c-109">在生產環境中就不允許 toorun。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-109">It’s just not allowed toorun in production.</span></span> <span data-ttu-id="fdf6c-110">SQL Server 開發人員 VM 了 hello hello VM，不適用於 SQL Server 授權成本時，將只會收取費用。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-110">A SQL Server Developer VM will only charge for hello cost of hello VM, not for SQL Server licensing.</span></span>

<span data-ttu-id="fdf6c-111">如果您想要在生產環境中的輕量工作負載 toorun (< 4 核心，< 1 GB 的記憶體 < 10 GB/資料庫)，然後使用 釋放授權 hello **SQL Server Express edition**。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-111">If you want toorun a lightweight workload in production (<4 cores, <1 GB memory, <10 GB/database), then use hello free-licensed **SQL Server Express edition**.</span></span> <span data-ttu-id="fdf6c-112">SQL Express 的 VM 將會只收取 hello VM，hello 成本不 SQL 授權。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-112">A SQL Express VM will only charge for hello cost of hello VM, not SQL licensing.</span></span>

<span data-ttu-id="fdf6c-113">針對這些開發/測試或輕量型生產環境工作負載，您也可以選擇符合這些工作負載的較小 VM 大小來節省成本。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-113">For these development/test or lightweight production workloads, you can also save money by choosing a smaller VM size that matches these workloads.</span></span> <span data-ttu-id="fdf6c-114">hello DS1v2 可能是不錯的選擇，這些工作負載。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-114">hello DS1v2 might be a good choice for these workloads.</span></span>

<span data-ttu-id="fdf6c-115">toocreate SQL Server 2016 Azure VM 與其中一個這些映像，請參閱下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="fdf6c-115">toocreate a SQL Server 2016 Azure VM with one of these images, see hello following links:</span></span>

- [<span data-ttu-id="fdf6c-116">SQL Server 2016 Developer Azure VM</span><span class="sxs-lookup"><span data-stu-id="fdf6c-116">SQL Server 2016 Developer Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [<span data-ttu-id="fdf6c-117">SQL Server 2016 Express Azure VM</span><span class="sxs-lookup"><span data-stu-id="fdf6c-117">SQL Server 2016 Express Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a><span data-ttu-id="fdf6c-118">付費的 SQL Server 版本</span><span class="sxs-lookup"><span data-stu-id="fdf6c-118">Paid SQL Server editions</span></span>

<span data-ttu-id="fdf6c-119">如果您有非輕量型生產工作負載時，使用下列 SQL Server 版本的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="fdf6c-119">If you have a non-lightweight production workload, use one of hello following SQL Server editions:</span></span>

| <span data-ttu-id="fdf6c-120">SQL Server 版本</span><span class="sxs-lookup"><span data-stu-id="fdf6c-120">SQL Server Edition</span></span> | <span data-ttu-id="fdf6c-121">工作負載</span><span class="sxs-lookup"><span data-stu-id="fdf6c-121">Workload</span></span> |
|-----|-----|
| <span data-ttu-id="fdf6c-122">Web</span><span class="sxs-lookup"><span data-stu-id="fdf6c-122">Web</span></span> | <span data-ttu-id="fdf6c-123">小型網站</span><span class="sxs-lookup"><span data-stu-id="fdf6c-123">Small web sites</span></span> |
| <span data-ttu-id="fdf6c-124">標準</span><span class="sxs-lookup"><span data-stu-id="fdf6c-124">Standard</span></span> | <span data-ttu-id="fdf6c-125">小型 toomedium 工作負載</span><span class="sxs-lookup"><span data-stu-id="fdf6c-125">Small toomedium workloads</span></span> |
| <span data-ttu-id="fdf6c-126">Enterprise</span><span class="sxs-lookup"><span data-stu-id="fdf6c-126">Enterprise</span></span> | <span data-ttu-id="fdf6c-127">大型或任務關鍵性工作負載</span><span class="sxs-lookup"><span data-stu-id="fdf6c-127">Large or mission-critical workloads</span></span>|

<span data-ttu-id="fdf6c-128">您有兩個選項 toopay 對於這些版本的 SQL Server 授權：*每使用量付費*或*自備授權*。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-128">You have two options toopay for SQL Server licensing for these editions: *pay per usage* or *bring your own license*.</span></span>

### <a name="pay-per-usage"></a><span data-ttu-id="fdf6c-129">依使用量付費</span><span class="sxs-lookup"><span data-stu-id="fdf6c-129">Pay per usage</span></span>

<span data-ttu-id="fdf6c-130">**每個使用量付費 hello SQL Server 授權**表示執行 hello Azure VM 中的 hello 每分鐘成本包括 hello hello 的 SQL Server 授權成本。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-130">**Paying hello SQL Server license per usage** means that hello per-minute cost of running hello Azure VM includes hello cost of hello SQL Server license.</span></span> <span data-ttu-id="fdf6c-131">您可以看到 hello 定價 hello 不同 SQL Server 版本 （Web、 Standard、 Enterprise） 在 hello [Azure VM 定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard)。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-131">You can see hello pricing for hello different SQL Server editions (Web, Standard, Enterprise) in hello [Azure VM pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).</span></span> <span data-ttu-id="fdf6c-132">hello 成本是 hello 相同的所有版本的 SQL Server (2008 R2 too2016)。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-132">hello cost is hello same for all versions of SQL Server (2008 R2 too2016).</span></span> <span data-ttu-id="fdf6c-133">一般情況下，授權 hello 與 SQL Server 授權成本的每分鐘視 hello VM 核心的數目。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-133">As with SQL Server licensing in general, hello per-minute licensing cost depends on hello number of VM cores.</span></span>

<span data-ttu-id="fdf6c-134">支付 hello SQL Server 授權使用量每則建議基於：</span><span class="sxs-lookup"><span data-stu-id="fdf6c-134">Paying hello SQL Server licensing per usage is recommended for:</span></span>

- <span data-ttu-id="fdf6c-135">暫時或定期的工作負載。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-135">Temporary or periodic workloads.</span></span> <span data-ttu-id="fdf6c-136">例如，應用程式需要 toosupport 事件在幾個月的每個年份或業務分析，從星期一。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-136">For example, an app that needs toosupport an event for a couple of months every year, or business analysis on Mondays.</span></span>
- <span data-ttu-id="fdf6c-137">存留期或規模不明的工作負載。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-137">Workloads with unknown lifetime or scale.</span></span> <span data-ttu-id="fdf6c-138">例如，有幾個月不需用到或依需求可能需要較多或較少運算能力的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-138">For example, an app that may not be required in a few months, or which may require more, or less compute power, depending on demand.</span></span>

<span data-ttu-id="fdf6c-139">toocreate SQL Server 2016 Azure VM 與其中一個這些支付每次使用量映像，請參閱下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="fdf6c-139">toocreate a SQL Server 2016 Azure VM with one of these pay-per-usage images, see hello following links:</span></span>

- [<span data-ttu-id="fdf6c-140">SQL Server 2016 Web Azure VM</span><span class="sxs-lookup"><span data-stu-id="fdf6c-140">SQL Server 2016 Web Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [<span data-ttu-id="fdf6c-141">SQL Server 2016 Standard Azure VM</span><span class="sxs-lookup"><span data-stu-id="fdf6c-141">SQL Server 2016 Standard Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [<span data-ttu-id="fdf6c-142">SQL Server 2016 Enterprise Azure VM</span><span class="sxs-lookup"><span data-stu-id="fdf6c-142">SQL Server 2016 Enterprise Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> <span data-ttu-id="fdf6c-143">當您在 hello Azure 入口網站中建立 SQL Server 虛擬機器時，hello 估計 hello 上顯示的每月成本**大小選擇 「**刀鋒視窗中不包含 SQL Server 授權成本。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-143">When you create a SQL Server virtual machine in hello Azure portal, hello estimated monthly cost displayed on hello **Choose a size** blade does not include SQL Server licensing costs.</span></span> <span data-ttu-id="fdf6c-144">這是 hello VM 單獨 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-144">This is hello cost of hello VM alone.</span></span>
>
> ![選擇 VM 大小刀鋒視窗](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
><span data-ttu-id="fdf6c-146">Hello 釋出授權 Express 和 Developer edition 的 SQL Server，這是 hello 總估計的成本。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-146">For hello free-licensed Express and Developer editions of SQL Server, this is hello total estimated cost.</span></span> <span data-ttu-id="fdf6c-147">但如 Web、 Standard 和 Enterprise，hello 尋找其他 SQL 授權成本上 hello [Windows 虛擬機器定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-147">But for Web, Standard, and Enterprise, find hello additional SQL licensing costs on hello [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/).</span></span> <span data-ttu-id="fdf6c-148">在 hello 定價頁面，選取您目標的 SQL Server 版本。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-148">On hello pricing page, select your target edition of SQL Server.</span></span>

### <a name="bring-your-own-license-byol"></a><span data-ttu-id="fdf6c-149">自備授權 (BYOL)</span><span class="sxs-lookup"><span data-stu-id="fdf6c-149">Bring your own license (BYOL)</span></span>

<span data-ttu-id="fdf6c-150">**攜帶您自己的 SQL Server 授權的授權流動性透過**，也稱為 tooas **BYOL**、 使用現有的 SQL Server 大量授權與 Azure VM 中的軟體保證的方式。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-150">**Bringing your own SQL Server license through License Mobility**, also referred tooas **BYOL**, means using an existing SQL Server Volume License with Software Assurance in an Azure VM.</span></span> <span data-ttu-id="fdf6c-151">假設您已取得授權和軟體保證透過大量授權方案 hello 執行成本的 hello VM，不適用於 SQL Server 授權，只會收取使用 BYOL 的 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-151">A SQL Server VM using BYOL will only charge for hello cost of running hello VM, not for SQL Server licensing, given that you have already acquired licenses and Software Assurance through a Volume Licensing program.</span></span>

<span data-ttu-id="fdf6c-152">針對下列情況，建議採用透過「授權行動性」自備 SQL 授權：</span><span class="sxs-lookup"><span data-stu-id="fdf6c-152">Bringing your own SQL licensing through License Mobility is recommended for:</span></span>

- <span data-ttu-id="fdf6c-153">持續性工作負載。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-153">Continuous workloads.</span></span> <span data-ttu-id="fdf6c-154">例如，需要 toosupport 24x7 的企業營運應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-154">For example, an app that needs toosupport business operations 24x7.</span></span>
- <span data-ttu-id="fdf6c-155">存留期和規模已知的工作負載。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-155">Workloads with known lifetime and scale.</span></span> <span data-ttu-id="fdf6c-156">例如，hello 整個年度和已預測哪些需求將需要的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-156">For example, an app that will be required for hello whole year and which demand has been forecasted.</span></span>

<span data-ttu-id="fdf6c-157">toouse BYOL 與 SQL Server VM，您必須擁有的授權 SQL Server Standard 或 Enterprise 和[軟體保證](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1)，這是必要的選項，透過一些[大量授權](https://www.microsoft.com/en-us/download/details.aspx?id=10585)程式以及選用性購買與其他人。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-157">toouse BYOL with a SQL Server VM, you must have a license for SQL Server Standard or Enterprise and [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), which is a required option through some [Volume Licensing](https://www.microsoft.com/en-us/download/details.aspx?id=10585) programs and an optional purchase with others.</span></span>  <span data-ttu-id="fdf6c-158">hello 定價提供透過大量授權方案層級會根據合約和 hello 數量，或承諾 tooSQL 伺服器 hello 類型而不同。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-158">hello pricing levels provided through Volume Licensing programs varies, based on hello type of agreement and hello quantity and or commitment tooSQL Server.</span></span> <span data-ttu-id="fdf6c-159">但根據經驗法則，請為攜帶自己的授權以連續生產工作負載具有 hello 下列優點：</span><span class="sxs-lookup"><span data-stu-id="fdf6c-159">But as a rule of thumb, bringing your own license for continuous production workloads has hello following benefits:</span></span>

| <span data-ttu-id="fdf6c-160">BYOL 優點</span><span class="sxs-lookup"><span data-stu-id="fdf6c-160">BYOL benefit</span></span> | <span data-ttu-id="fdf6c-161">說明</span><span class="sxs-lookup"><span data-stu-id="fdf6c-161">Description</span></span> |
|-----|-----|
| <span data-ttu-id="fdf6c-162">**節省成本**</span><span class="sxs-lookup"><span data-stu-id="fdf6c-162">**Cost savings**</span></span> | <span data-ttu-id="fdf6c-163">如果工作負載將持續執行 SQL Server Standard 或 Enterprise 長達「10 個月以上」的時間，則與依使用量付費相比，自備 SQL Server 授權較符合經濟效益。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-163">Bringing your own SQL Server license is more cost effective than paying it per usage if a workload will run continuously SQL Server Standard or Enterprise for *more than 10 months*.</span></span> |
| <span data-ttu-id="fdf6c-164">**長期節省**</span><span class="sxs-lookup"><span data-stu-id="fdf6c-164">**Long-term savings**</span></span> | <span data-ttu-id="fdf6c-165">平均而言，它是*便宜每年的 30%* toobuy 或更新 SQL Server 授權 hello，第一個 3 年。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-165">On average, it is *30% cheaper per year* toobuy or renew a SQL Server license for hello first 3 years.</span></span> <span data-ttu-id="fdf6c-166">此外，3 年之後，您不需要 toorenew hello 授權失效，for Software Assurance 的只是付費。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-166">Furthermore, after 3 years, you don’t need toorenew hello license anymore, just pay for Software Assurance.</span></span> <span data-ttu-id="fdf6c-167">屆時，將可「節省 200% 的費用」。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-167">At that point, it is *200% cheaper*.</span></span> |
| <span data-ttu-id="fdf6c-168">**免費的被動次要複本**</span><span class="sxs-lookup"><span data-stu-id="fdf6c-168">**Free passive secondary replica**</span></span> | <span data-ttu-id="fdf6c-169">攜帶您自己的授權的另一個優點為 hello[免費授權一個被動的次要複本](https://azure.microsoft.com/pricing/licensing-faq/)每部 SQL Server 的高可用性 」 用途。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-169">Another benefit of bringing your own license is hello [free licensing for one passive secondary replica](https://azure.microsoft.com/pricing/licensing-faq/) per SQL Server for high availability purposes.</span></span> <span data-ttu-id="fdf6c-170">這在授權 （例如，使用 Alwayson 可用性群組） 的高可用性 SQL Server 部署的成本的一半 hello 剪下。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-170">This cuts in half hello licensing cost of a highly available SQL Server deployment (e.g. using Always On Availability Groups).</span></span> <span data-ttu-id="fdf6c-171">透過 hello 容錯移轉伺服器軟體保證權益提供 hello 權限 toorun hello 被動次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-171">hello rights toorun hello passive secondary are provided through hello Fail-Over Servers Software Assurance benefit.</span></span> |

<span data-ttu-id="fdf6c-172">toocreate SQL Server 2016 Azure VM 與其中一個這些帶您-擁有-授權映像，請參閱加上"{BYOL}"hello Vm:</span><span class="sxs-lookup"><span data-stu-id="fdf6c-172">toocreate a SQL Server 2016 Azure VM with one of these bring-your-own-license images, see hello VMs prefixed with "{BYOL}":</span></span>

- [<span data-ttu-id="fdf6c-173">SQL Server 2016 Enterprise Azure VM</span><span class="sxs-lookup"><span data-stu-id="fdf6c-173">SQL Server 2016 Enterprise Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [<span data-ttu-id="fdf6c-174">SQL Server 2016 Standard Azure VM</span><span class="sxs-lookup"><span data-stu-id="fdf6c-174">SQL Server 2016 Standard Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> <span data-ttu-id="fdf6c-175">請在 10 天內告訴我們您將在 Azure 中使用多少個 SQL Server 授權。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-175">Please let us know within 10 days how many SQL Server licenses you’ll use in Azure.</span></span> <span data-ttu-id="fdf6c-176">hello 連結 toohello 先前映像具有指示如何 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-176">hello links toohello previous images have instructions on how toodo this.</span></span>

## <a name="avoid-unecessary-costs"></a><span data-ttu-id="fdf6c-177">避免不必要的費用</span><span class="sxs-lookup"><span data-stu-id="fdf6c-177">Avoid unecessary costs</span></span>

<span data-ttu-id="fdf6c-178">如果您將不會持續執行的任何工作負載，請考慮在 hello 非作用中期間關閉 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-178">If you are using any workloads that do not run continuously, consider shutting down hello virtual machine during hello inactive periods.</span></span> <span data-ttu-id="fdf6c-179">您只需依據使用量付費。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-179">You only pay for what you use.</span></span>

<span data-ttu-id="fdf6c-180">例如，如果您只嘗試在 Azure VM 上的 SQL Server 時，您不想 tooincur 費用意外保留週中執行它。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-180">For example, if you are simply trying out SQL Server on an Azure VM, you would not want tooincur charges by accidentally leaving it running for weeks.</span></span> <span data-ttu-id="fdf6c-181">其中一個解決方案是 toouse hello[自動關閉功能](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/)。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-181">One solution is toouse hello [automatic shutdown feature](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).</span></span>

![SQL VM 自動關閉](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

<span data-ttu-id="fdf6c-183">自動關閉是 [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab) 所提供的較大一組相似功能的一部分。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-183">Automatic shutdown is part of a larger set of similar features provided by [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).</span></span>

<span data-ttu-id="fdf6c-184">針對其他工作負載，請考慮使用指令碼解決方案 (例如 [Azure 自動化](https://azure.microsoft.com/services/automation/)) 來自動關閉並重新啟動 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-184">For other workflows, consider automatically shutting down and restarting Azure VMs with a scripting solution,such as [Azure Automation](https://azure.microsoft.com/services/automation/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdf6c-185">正在關閉和解除配置 VM 是 hello 唯一方式 tooavoid 費用。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-185">Shutting down and deallocating your VM is hello only way tooavoid charges.</span></span> <span data-ttu-id="fdf6c-186">只停止，或使用電源選項 tooshut 向 hello VM 仍會產生使用費用。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-186">Simply stopping or using power options tooshut down hello VM still incurs usage charges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdf6c-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fdf6c-187">Next steps</span></span>

<span data-ttu-id="fdf6c-188">如需一般的 Azure 定價指導方針，請參閱[使用 Azure 計費與成本管理避免非預期的成本](../../../billing/billing-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-188">For general Azure pricing guidance, see [Prevent unexpected costs with Azure billing and cost management](../../../billing/billing-getting-started.md).</span></span>

<span data-ttu-id="fdf6c-189">Hello 最新的虛擬機器定價，包括 SQL Server，請參閱 hello [Azure VM 定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard)。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-189">For hello latest Virtual Machines pricing, including SQL Server, see hello [Azure VM pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).</span></span>

<span data-ttu-id="fdf6c-190">請檢閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)中的其他「SQL Server 虛擬機器」主題。</span><span class="sxs-lookup"><span data-stu-id="fdf6c-190">Review other SQL Server Virtual Machine topics at [SQL Server on Azure Virtual Machines Overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
