---
title: "Linux 資料科學虛擬機器上的資料科學 | Microsoft Docs"
description: "如何使用 Linux 資料科學 VM 執行數個常見的資料科學工作。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 6da9a8e3f9f8ac851c2a8deb861ac1d0b3ec5874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="data-science-on-the-linux-data-science-virtual-machine"></a><span data-ttu-id="52b17-103">Linux 資料科學虛擬機器上的資料科學</span><span class="sxs-lookup"><span data-stu-id="52b17-103">Data science on the Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="52b17-104">本逐步解說示範如何使用 Linux 資料科學 VM 執行數個常見的資料科學工作。</span><span class="sxs-lookup"><span data-stu-id="52b17-104">This walkthrough shows you how to perform several common data science tasks with the Linux Data Science VM.</span></span> <span data-ttu-id="52b17-105">Linux 資料科學虛擬機器 (DSVM) 是 Azure 提供的虛擬機器映像，其中預先安裝了一組常用於執行資料分析和機器學習服務的工具。</span><span class="sxs-lookup"><span data-stu-id="52b17-105">The Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="52b17-106">重要的軟體元件可在 [佈建 Linux 資料科學虛擬機器](machine-learning-data-science-linux-dsvm-intro.md) 主題中找到明細。</span><span class="sxs-lookup"><span data-stu-id="52b17-106">The key software components are itemized in the [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="52b17-107">VM 映像可讓使用者輕鬆地在幾分鐘內開始執行資料科學，而不需要個別安裝和設定每個工具。</span><span class="sxs-lookup"><span data-stu-id="52b17-107">The VM image makes it easy to get started doing data science in minutes, without having to install and configure each of the tools individually.</span></span> <span data-ttu-id="52b17-108">您可以在需要時輕鬆地相應增加 VM，並在不使用時加以停止。</span><span class="sxs-lookup"><span data-stu-id="52b17-108">You can easily scale up the VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="52b17-109">因此，這項資源既有彈性，又符合成本效益。</span><span class="sxs-lookup"><span data-stu-id="52b17-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="52b17-110">本逐步解說所示範的資料科學工作遵循 [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="52b17-110">The data science tasks demonstrated in this walkthrough follow the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="52b17-111">此程序可讓使用者以系統化方法執行資料科學，讓資料科學家團隊可以在智慧型應用程式的建置生命週期內有效地共同作業。</span><span class="sxs-lookup"><span data-stu-id="52b17-111">This process provides a systematic approach to data science that enables teams of data scientists to effectively collaborate over the lifecycle of building intelligent applications.</span></span> <span data-ttu-id="52b17-112">資料科學程序也為資料科學提供了可反覆進行的架構供個人遵循。</span><span class="sxs-lookup"><span data-stu-id="52b17-112">The data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="52b17-113">在本逐步解說中，我們會分析 [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) 資料集。</span><span class="sxs-lookup"><span data-stu-id="52b17-113">We analyze the [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="52b17-114">這是一組標示為垃圾郵件或非垃圾郵件 (亦即這些郵件不是垃圾郵件) 的電子郵件，並同時包含關於電子郵件內容的一些統計資料。</span><span class="sxs-lookup"><span data-stu-id="52b17-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on the content of the emails.</span></span> <span data-ttu-id="52b17-115">其中所含的統計資料會在下下一節中討論。</span><span class="sxs-lookup"><span data-stu-id="52b17-115">The statistics included are discussed in the next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52b17-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="52b17-116">Prerequisites</span></span>
<span data-ttu-id="52b17-117">您必須先具有下列項目，才可以使用 Linux 資料科學虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="52b17-117">Before you can use a Linux Data Science Virtual Machine, you must have the following:</span></span>

* <span data-ttu-id="52b17-118">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="52b17-118">An **Azure subscription**.</span></span> <span data-ttu-id="52b17-119">如果您還沒有訂用帳戶，請參閱 [立即建立免費的 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="52b17-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="52b17-120">[**Linux 資料科學 VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm)。</span><span class="sxs-lookup"><span data-stu-id="52b17-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="52b17-121">如需佈建此 VM 的相關資訊，請參閱 [佈建 Linux 資料科學虛擬機器](machine-learning-data-science-linux-dsvm-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="52b17-121">For information on provisioning this VM, see [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="52b17-122">[X2Go](http://wiki.x2go.org/doku.php) 已安裝在電腦上並已開啟 XFCE 工作階段。</span><span class="sxs-lookup"><span data-stu-id="52b17-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="52b17-123">如需安裝和設定 **X2Go 用戶端**的相關資訊，請參閱[安裝和設定 X2Go 用戶端](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client)。</span><span class="sxs-lookup"><span data-stu-id="52b17-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="52b17-124">**AzureML 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="52b17-124">An **AzureML account**.</span></span> <span data-ttu-id="52b17-125">如果您還沒有帳戶，請在 [AzureML 首頁](https://studio.azureml.net/)註冊新帳戶。</span><span class="sxs-lookup"><span data-stu-id="52b17-125">If you don't already have one, sign up for new one at the [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="52b17-126">裡面有免費的使用量層級可幫助您開始使用。</span><span class="sxs-lookup"><span data-stu-id="52b17-126">There is a free usage tier to help you get started.</span></span>

## <a name="download-the-spambase-dataset"></a><span data-ttu-id="52b17-127">下載 spambase 資料集</span><span class="sxs-lookup"><span data-stu-id="52b17-127">Download the spambase dataset</span></span>
<span data-ttu-id="52b17-128">[spambase](https://archive.ics.uci.edu/ml/datasets/spambase) 資料集是一組較小的資料，裡面只有 4601 個範例。</span><span class="sxs-lookup"><span data-stu-id="52b17-128">The [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="52b17-129">在示範資料科學 VM 的某些重要功能時，這樣的大小比較方便使用，因為它會讓所需的資源需求保持適中。</span><span class="sxs-lookup"><span data-stu-id="52b17-129">This is a convenient size to use when demonstrating that some of the key features of the Data Science VM as it keeps the resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="52b17-130">本逐步解說建立在 D2 v2 大小的 Linux 資料科學虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="52b17-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="52b17-131">這個大小的 DSVM 能夠處理此逐步解說中的程序。</span><span class="sxs-lookup"><span data-stu-id="52b17-131">This size DSVM is capable of handling the procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="52b17-132">如果您需要更多儲存空間，您可以建立額外的磁碟，並將它們連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="52b17-132">If you need more storage space, you can create additional disks and attach them to your VM.</span></span> <span data-ttu-id="52b17-133">這些磁碟會使用永續性的 Azure 儲存體，因此，即使伺服器因為調整大小或關閉等緣故而重新佈建，磁碟中的資料仍會保留下來。</span><span class="sxs-lookup"><span data-stu-id="52b17-133">These disks use persistent Azure storage, so their data is preserved even when the server is reprovisioned due to resizing or is shut down.</span></span> <span data-ttu-id="52b17-134">若要新增磁碟並將它連接到 VM，請遵循[在 Linux VM 中新增磁碟](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)的指示。</span><span class="sxs-lookup"><span data-stu-id="52b17-134">To add a disk and attach it to your VM, follow the instructions in [Add a disk to a Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="52b17-135">這些步驟使用 Azure 命令列介面 (Azure CLI)，此介面已安裝在 DSVM 上。</span><span class="sxs-lookup"><span data-stu-id="52b17-135">These steps use the Azure Command-Line Interface (Azure CLI), which is already installed on the DSVM.</span></span> <span data-ttu-id="52b17-136">因此，您完全可以從 VM 本身來執行這些程序。</span><span class="sxs-lookup"><span data-stu-id="52b17-136">So these procedures can be done entirely from the VM itself.</span></span> <span data-ttu-id="52b17-137">另一種可增加儲存體的選項是使用 [Azure 檔案](../storage/files/storage-how-to-use-files-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="52b17-137">Another option to increase storage is to use [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="52b17-138">若要下載資料，請開啟終端機視窗並執行此命令︰</span><span class="sxs-lookup"><span data-stu-id="52b17-138">To download the data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="52b17-139">下載的檔案沒有標題列，因此，讓我們建立另一個有標題的檔案。</span><span class="sxs-lookup"><span data-stu-id="52b17-139">The downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="52b17-140">執行此命令來建立具有適當標題的檔案︰</span><span class="sxs-lookup"><span data-stu-id="52b17-140">Run this command to create a file with the appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="52b17-141">然後，使用下列命令串連兩個檔案︰</span><span class="sxs-lookup"><span data-stu-id="52b17-141">Then concatenate the two files together with the command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="52b17-142">資料集內有多種關於每封電子郵件的統計資料︰</span><span class="sxs-lookup"><span data-stu-id="52b17-142">The dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="52b17-143">***word\_freq\_WORD*** 之類的資料行會指出電子郵件中符合 *WORD* 之字詞的百分比。</span><span class="sxs-lookup"><span data-stu-id="52b17-143">Columns like ***word\_freq\_WORD*** indicate the percentage of words in the email that match *WORD*.</span></span> <span data-ttu-id="52b17-144">例如，如果 *word\_freq\_make* 是 1，則表示電子郵件的所有文字中有 1% 是 *make*。</span><span class="sxs-lookup"><span data-stu-id="52b17-144">For example, if *word\_freq\_make* is 1, then 1% of all words in the email were *make*.</span></span>
* <span data-ttu-id="52b17-145">***char\_freq\_CHAR*** 之類的資料行會指出電子郵件的所有字元中 *CHAR* 所佔的百分比。</span><span class="sxs-lookup"><span data-stu-id="52b17-145">Columns like ***char\_freq\_CHAR*** indicate the percentage of all characters in the email that were *CHAR*.</span></span>
* <span data-ttu-id="52b17-146">***capital\_run\_length\_longest*** 是一連串大寫字母的最長長度。</span><span class="sxs-lookup"><span data-stu-id="52b17-146">***capital\_run\_length\_longest*** is the longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="52b17-147">***capital\_run\_length\_average*** 是所有連串大寫字母的平均長度。</span><span class="sxs-lookup"><span data-stu-id="52b17-147">***capital\_run\_length\_average*** is the average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="52b17-148">***capital\_run\_length\_total*** 是所有連串大寫字母的總長度。</span><span class="sxs-lookup"><span data-stu-id="52b17-148">***capital\_run\_length\_total*** is the total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="52b17-149"> indicates whether the email was considered  or not (1 = , 0 = not ).</span><span class="sxs-lookup"><span data-stu-id="52b17-149">***spam*** indicates whether the email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-the-dataset-with-microsoft-r-open"></a><span data-ttu-id="52b17-150">使用 Microsoft R Open 探索資料集</span><span class="sxs-lookup"><span data-stu-id="52b17-150">Explore the dataset with Microsoft R Open</span></span>
<span data-ttu-id="52b17-151">讓我們使用 R 來檢查資料並執行某些基本的機器學習服務。資料科學 VM 已預先安裝了 [Microsoft R Open](https://mran.revolutionanalytics.com/open/)。</span><span class="sxs-lookup"><span data-stu-id="52b17-151">Let's examine the data and do some basic machine learning with R. The Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="52b17-152">此版本的 R 中有多執行緒的數學程式庫，可提供比單一執行緒版本還要好的效能。</span><span class="sxs-lookup"><span data-stu-id="52b17-152">The multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="52b17-153">Microsoft R Open 也可藉由使用 CRAN 封裝儲存機制的快照來提供重現性。</span><span class="sxs-lookup"><span data-stu-id="52b17-153">Microsoft R Open also provides reproducibility by using a snapshot of the CRAN package repository.</span></span>

<span data-ttu-id="52b17-154">若要取得此逐步解說所使用的程式碼範例複本，請使用 VM 上預先安裝的 git 複製 **Azure-Machine-Learning-Data-Science** 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="52b17-154">To get copies of the code samples used in this walkthrough, clone the **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on the VM.</span></span> <span data-ttu-id="52b17-155">從 git 命令列執行︰</span><span class="sxs-lookup"><span data-stu-id="52b17-155">From the git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="52b17-156">開啟終端機視窗，並使用 R 互動式主控台啟動新的 R 工作階段。</span><span class="sxs-lookup"><span data-stu-id="52b17-156">Open a terminal window and start a new R session with the R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="52b17-157">您也可以使用 RStudio 來進行下列程序。</span><span class="sxs-lookup"><span data-stu-id="52b17-157">You can also use RStudio for the following procedures.</span></span> <span data-ttu-id="52b17-158">若要安裝 RStudio，請在終端機執行下列命令︰ `./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="52b17-158">To install RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="52b17-159">若要匯入資料並設定環境，請執行︰</span><span class="sxs-lookup"><span data-stu-id="52b17-159">To import the data and set up the environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="52b17-160">若要查看關於每個資料行的摘要統計資料︰</span><span class="sxs-lookup"><span data-stu-id="52b17-160">To see summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="52b17-161">針對資料的不同檢視︰</span><span class="sxs-lookup"><span data-stu-id="52b17-161">For a different view of the data:</span></span>

    str(data)

<span data-ttu-id="52b17-162">這會顯示每個變數的類型和資料集內的前幾個值。</span><span class="sxs-lookup"><span data-stu-id="52b17-162">This shows you the type of each variable and the first few values in the dataset.</span></span>

<span data-ttu-id="52b17-163">「spam」  資料行已讀取為整數，但它實際上是類別變數 (或係數)。</span><span class="sxs-lookup"><span data-stu-id="52b17-163">The *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="52b17-164">若要設定其類型︰</span><span class="sxs-lookup"><span data-stu-id="52b17-164">To set its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="52b17-165">若要進行一些探勘分析，請使用 [ggplot2](http://ggplot2.org/) 封裝，這是已安裝在 VM 上的適用於 R 的熱門圖形庫。</span><span class="sxs-lookup"><span data-stu-id="52b17-165">To do some exploratory analysis, use the [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on the VM.</span></span> <span data-ttu-id="52b17-166">請注意，在稍早顯示的摘要資料中，我們擁有關於驚嘆號字元出現頻率的摘要統計資料。</span><span class="sxs-lookup"><span data-stu-id="52b17-166">Note, from the summary data displayed earlier, that we have summary statistics on the frequency of the exclamation mark character.</span></span> <span data-ttu-id="52b17-167">在此，讓我們使用下列命令繪製這些頻率︰</span><span class="sxs-lookup"><span data-stu-id="52b17-167">Let's plot those frequencies here with the following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="52b17-168">由於零軸會影響繪圖的準確性，讓我們將它去除︰</span><span class="sxs-lookup"><span data-stu-id="52b17-168">Since the zero bar is skewing the plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="52b17-169">在 1 上面有看起來很有意思的不尋常密度。</span><span class="sxs-lookup"><span data-stu-id="52b17-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="52b17-170">讓我們只看該資料︰</span><span class="sxs-lookup"><span data-stu-id="52b17-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="52b17-171">然後按照垃圾郵件和非垃圾郵件進行分割：</span><span class="sxs-lookup"><span data-stu-id="52b17-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="52b17-172">這些範例應該能讓您為其他資料行製作類似繪圖，以探索它們內含的資料。</span><span class="sxs-lookup"><span data-stu-id="52b17-172">These examples should enable you to make similar plots of the other columns to explore the data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="52b17-173">訓練和測試 ML 模型</span><span class="sxs-lookup"><span data-stu-id="52b17-173">Train and test an ML model</span></span>
<span data-ttu-id="52b17-174">現在讓我們訓練幾個機器學習服務模型，將資料集內的電子郵件分類為包含垃圾郵件或非垃圾郵件。</span><span class="sxs-lookup"><span data-stu-id="52b17-174">Now let's train a couple of machine learning models to classify the emails in the dataset as containing either span or ham.</span></span> <span data-ttu-id="52b17-175">在本節中，我們會訓練決策樹模型和隨機樹系模型，然後測試其預測的精確度。</span><span class="sxs-lookup"><span data-stu-id="52b17-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="52b17-176">下列程式碼所使用的 RPART (Recursive Partitioning and Regression Trees，遞迴分割和迴歸樹狀結構) 封裝已安裝在資料科學 VM 上。</span><span class="sxs-lookup"><span data-stu-id="52b17-176">The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the Data Science VM.</span></span>
>
>

<span data-ttu-id="52b17-177">首先，讓我們將資料集分割為訓練集和測試集︰</span><span class="sxs-lookup"><span data-stu-id="52b17-177">First, let's split the dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="52b17-178">然後建立決策樹來分類電子郵件。</span><span class="sxs-lookup"><span data-stu-id="52b17-178">And then create a decision tree to classify the emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="52b17-179">結果如下︰</span><span class="sxs-lookup"><span data-stu-id="52b17-179">Here is the result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="52b17-181">若要判斷訓練集的表現有多良好，請使用下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="52b17-181">To determine how well it performs on the training set, use the following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="52b17-182">若要判斷測試集的表現有多良好︰</span><span class="sxs-lookup"><span data-stu-id="52b17-182">To determine how well it performs on the test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="52b17-183">讓我們同時嘗試隨機樹系模型。</span><span class="sxs-lookup"><span data-stu-id="52b17-183">Let's also try a random forest model.</span></span> <span data-ttu-id="52b17-184">隨機樹系會訓練大量決策樹，並輸出屬於所有個別決策樹之分類眾數的類別。</span><span class="sxs-lookup"><span data-stu-id="52b17-184">Random forests train a multitude of decision trees and output a class that is the mode of the classifications from all of the individual decision trees.</span></span> <span data-ttu-id="52b17-185">它們能提供更強大的機器學習服務方法，因為它們會校正決策樹模型傾向以過度擬合訓練資料集。</span><span class="sxs-lookup"><span data-stu-id="52b17-185">They provide a more powerful machine learning approach as they correct for the tendency of a decision tree model to overfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-to-azure-ml"></a><span data-ttu-id="52b17-186">模型部署到 Azure ML</span><span class="sxs-lookup"><span data-stu-id="52b17-186">Deploy a model to Azure ML</span></span>
<span data-ttu-id="52b17-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) 是一項雲端服務，可讓您輕鬆地建置和部署預測性分析模型。</span><span class="sxs-lookup"><span data-stu-id="52b17-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy to build and deploy predictive analytics models.</span></span> <span data-ttu-id="52b17-188">AzureML 的其中一項優秀功能是能夠將任何 R 函數發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="52b17-188">One of the nice features of AzureML is its ability to publish any R function as a web service.</span></span> <span data-ttu-id="52b17-189">AzureML R 封裝可直接從 DSVM 上的 R 工作階段讓部署作業的執行變得簡單無比。</span><span class="sxs-lookup"><span data-stu-id="52b17-189">The AzureML R package makes deployment easy to do right from our R session on the DSVM.</span></span>

<span data-ttu-id="52b17-190">若要部署上一節的決策樹程式碼，您需要登入 Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="52b17-190">To deploy the decision tree code from the previous section, you need to sign in to Azure Machine Learning Studio.</span></span> <span data-ttu-id="52b17-191">您需要工作區識別碼和驗證權杖才能登入。</span><span class="sxs-lookup"><span data-stu-id="52b17-191">You need your workspace ID and an authorization token to sign in.</span></span> <span data-ttu-id="52b17-192">若要找到這些值並以值初始化 AzureML 變數︰</span><span class="sxs-lookup"><span data-stu-id="52b17-192">To find these values and initialize the AzureML variables with them:</span></span>

<span data-ttu-id="52b17-193">選取左側功能表上的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="52b17-193">Select **Settings** on the left-hand menu.</span></span> <span data-ttu-id="52b17-194">記下您的**工作區識別碼**。</span><span class="sxs-lookup"><span data-stu-id="52b17-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="52b17-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="52b17-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="52b17-196">從上方的功能表選取 [授權權杖] 並記下您的**主要授權權杖**。![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="52b17-196">Select **Authorization Tokens** from the overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="52b17-197">載入 **AzureML** 封裝，然後在 DSVM 的 R 工作階段中以您的權杖和工作區識別碼設定變數值：</span><span class="sxs-lookup"><span data-stu-id="52b17-197">Load the **AzureML** package and then set values of the variables with your token and workspace ID in your R session on the DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="52b17-198">讓我們簡化模型，以使這項示範更容易實作。</span><span class="sxs-lookup"><span data-stu-id="52b17-198">Let's simplify the model to make this demonstration easier to implement.</span></span> <span data-ttu-id="52b17-199">挑選決策樹中最接近根部的三個變數，並只用這三個變數建置新的決策樹︰</span><span class="sxs-lookup"><span data-stu-id="52b17-199">Pick the three variables in the decision tree closest to the root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="52b17-200">我們需要會以功能做為輸入並傳回預測值的預測函數︰</span><span class="sxs-lookup"><span data-stu-id="52b17-200">We need a prediction function that takes the features as an input and returns the predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="52b17-201">使用 **publishWebService** 函數將 predictSpam 函數發佈至 AzureML︰</span><span class="sxs-lookup"><span data-stu-id="52b17-201">Publish the predictSpam function to AzureML using the **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="52b17-202">此函數會採用 **predictSpam** 函數、建立名為 **spamWebService** 的 Web 服務以及定義的輸入和輸出，並傳回新端點的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="52b17-202">This function takes the **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about the new endpoint.</span></span>

<span data-ttu-id="52b17-203">使用下列命令檢視已發佈之 Web 服務的詳細資料，包括其 API 端點和存取金鑰︰</span><span class="sxs-lookup"><span data-stu-id="52b17-203">View details of the published web service, including its API endpoint and access keys with the command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="52b17-204">若要對前 10 列測試集試用此服務︰</span><span class="sxs-lookup"><span data-stu-id="52b17-204">To try it out on the first 10 rows of the test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="52b17-205">使用其他可用工具</span><span class="sxs-lookup"><span data-stu-id="52b17-205">Use other tools available</span></span>
<span data-ttu-id="52b17-206">其餘各節示範如何使用一些已安裝在 Linux 資料科學 VM 上的工具。以下是所討論的工具清單︰</span><span class="sxs-lookup"><span data-stu-id="52b17-206">The remaining sections show how to use some of the tools installed on the Linux Data Science VM.Here is the list of tools discussed:</span></span>

* <span data-ttu-id="52b17-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="52b17-207">XGBoost</span></span>
* <span data-ttu-id="52b17-208">Python</span><span class="sxs-lookup"><span data-stu-id="52b17-208">Python</span></span>
* <span data-ttu-id="52b17-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="52b17-209">Jupyterhub</span></span>
* <span data-ttu-id="52b17-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="52b17-210">Rattle</span></span>
* <span data-ttu-id="52b17-211">PostgreSQL 和 Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="52b17-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="52b17-212">SQL Server 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="52b17-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="52b17-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="52b17-213">XGBoost</span></span>
<span data-ttu-id="52b17-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) 工具可提供快速且正確的推進式決策樹實作。</span><span class="sxs-lookup"><span data-stu-id="52b17-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

<span data-ttu-id="52b17-215">XGBoost 也可以從 Python 或命令列進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="52b17-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="52b17-216">Python</span><span class="sxs-lookup"><span data-stu-id="52b17-216">Python</span></span>
<span data-ttu-id="52b17-217">為了能夠使用 Python 進行開發，Anaconda Python 散發套件 2.7 與 3.5 已安裝在 DSVM 中。</span><span class="sxs-lookup"><span data-stu-id="52b17-217">For development using Python, the Anaconda Python distributions 2.7 and 3.5 have been installed in the DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="52b17-218">Anaconda 散發套件包含 [Condas](http://conda.pydata.org/docs/index.html)，可用來為 Python 建立已安裝不同版本和 (或) 封裝的自訂環境。</span><span class="sxs-lookup"><span data-stu-id="52b17-218">The Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used to create custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="52b17-219">讓我們讀入某些 spambase 資料集，並以 scikit-learn 中的支援向量機器分類電子郵件︰</span><span class="sxs-lookup"><span data-stu-id="52b17-219">Let's read in some of the spambase dataset and classify the emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="52b17-220">若要進行預測︰</span><span class="sxs-lookup"><span data-stu-id="52b17-220">To make predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="52b17-221">若要顯示如何發佈 AzureML 端點，讓我們和先前發佈 R 模型時一樣，建立只有三個變數的簡化模型。</span><span class="sxs-lookup"><span data-stu-id="52b17-221">To show how to publish an AzureML endpoint, let's make a simpler model the three variables as we did when we published the R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="52b17-222">若要將模型發佈至 AzureML：</span><span class="sxs-lookup"><span data-stu-id="52b17-222">To publish the model to AzureML:</span></span>

    # Publish the model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about the resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call the model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="52b17-223">此操作只適用於 Python 2.7，3.5 版則尚未支援。</span><span class="sxs-lookup"><span data-stu-id="52b17-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="52b17-224">請使用 **/anaconda/bin/python2.7**來執行。</span><span class="sxs-lookup"><span data-stu-id="52b17-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="52b17-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="52b17-225">Jupyterhub</span></span>
<span data-ttu-id="52b17-226">DSVM 中的 Anaconda 散發套件隨附 Jupyter Notebook，此跨平台環境可用來共用 Python、R 或 Julia 程式碼和分析。</span><span class="sxs-lookup"><span data-stu-id="52b17-226">The Anaconda distribution in the DSVM comes with a Jupyter notebook, a cross-platform environment to share Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="52b17-227">Jupyter 筆記本是透過 JupyterHub 來存取。</span><span class="sxs-lookup"><span data-stu-id="52b17-227">The Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="52b17-228">您可以在 ***https://\<VM DNS 名稱或 IP 位址\>:8000/*** 使用本機 Linux 使用者名稱和密碼來登入。</span><span class="sxs-lookup"><span data-stu-id="52b17-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="52b17-229">JupyterHub 的所有組態檔可在 **eg /etc/ jupyterhub**目錄中找到。</span><span class="sxs-lookup"><span data-stu-id="52b17-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="52b17-230">VM 上已安裝數個 Notebook 範例︰</span><span class="sxs-lookup"><span data-stu-id="52b17-230">Several sample notebooks are already installed on the VM:</span></span>

* <span data-ttu-id="52b17-231">如需 Python 的 Notebook 範例，請參閱 [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) 。</span><span class="sxs-lookup"><span data-stu-id="52b17-231">See the [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="52b17-232">如需 [R](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) 的 Notebook 範例，請參閱 **IntroTutorialinR** 。</span><span class="sxs-lookup"><span data-stu-id="52b17-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="52b17-233">如需 [Python](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) 的其他 Notebook 範例，請參閱 **IrisClassifierPyMLWebService** 。</span><span class="sxs-lookup"><span data-stu-id="52b17-233">See the [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="52b17-234">Julia 語言也可從 Linux 資料科學 VM 上的命令列來使用。</span><span class="sxs-lookup"><span data-stu-id="52b17-234">The Julia language is also available from the command line on the Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="52b17-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="52b17-235">Rattle</span></span>
<span data-ttu-id="52b17-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (R Analytical Tool To Learn Easily) 是用於資料採礦的 R 圖形化工具。</span><span class="sxs-lookup"><span data-stu-id="52b17-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (the R Analytical Tool To Learn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="52b17-237">其直覺式介面可讓您輕鬆地載入、瀏覽和轉換資料以及建置和評估模型。</span><span class="sxs-lookup"><span data-stu-id="52b17-237">It has an intuitive interface that makes it easy to load, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="52b17-238">[Rattle︰R 的資料採礦 GUI](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) 一文提供了逐步解說來示範其功能。</span><span class="sxs-lookup"><span data-stu-id="52b17-238">The article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="52b17-239">使用下列命令安裝並啟動 Rattle︰</span><span class="sxs-lookup"><span data-stu-id="52b17-239">Install and start Rattle with the following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="52b17-240">不需要安裝在 DSVM 上。</span><span class="sxs-lookup"><span data-stu-id="52b17-240">Installation is not required on the DSVM.</span></span> <span data-ttu-id="52b17-241">但 Rattle 可能會在載入時提示您安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="52b17-241">But Rattle may prompt you to install additional packages when it loads.</span></span>
>
>

<span data-ttu-id="52b17-242">Rattle 使用索引標籤式介面。</span><span class="sxs-lookup"><span data-stu-id="52b17-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="52b17-243">大部分索引標籤會對應至 [資料科學程序](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)中的步驟，例如載入資料或瀏覽資料。</span><span class="sxs-lookup"><span data-stu-id="52b17-243">Most of the tabs correspond to steps in the [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="52b17-244">資料科學程序會由左到右經歷所有索引標籤。</span><span class="sxs-lookup"><span data-stu-id="52b17-244">The data science process flows from left to right through the tabs.</span></span> <span data-ttu-id="52b17-245">但最後一個索引標籤包含 Rattle 所執行的 R 命令的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="52b17-245">But the last tab contains a log of the R commands run by Rattle.</span></span>

<span data-ttu-id="52b17-246">若要載入和設定資料集︰</span><span class="sxs-lookup"><span data-stu-id="52b17-246">To load and configure the dataset:</span></span>

* <span data-ttu-id="52b17-247">若要載入檔案，請選取 [資料]  索引標籤，然後</span><span class="sxs-lookup"><span data-stu-id="52b17-247">To load the file, select the **Data** tab, then</span></span>
* <span data-ttu-id="52b17-248">選擇 **Filename** 旁的選取器，然後選擇 **spambaseHeaders.data**。</span><span class="sxs-lookup"><span data-stu-id="52b17-248">Choose the selector next to **Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="52b17-249">若要載入檔案。</span><span class="sxs-lookup"><span data-stu-id="52b17-249">To load the file.</span></span> <span data-ttu-id="52b17-250">選取最上方按鈕列中的 [執行]。</span><span class="sxs-lookup"><span data-stu-id="52b17-250">select **Execute** in the top row of buttons.</span></span> <span data-ttu-id="52b17-251">您應該會看到每個資料行的摘要，包括其識別的資料類型、其為輸入、目標還是其他類型的變數，以及唯一值數目。</span><span class="sxs-lookup"><span data-stu-id="52b17-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and the number of unique values.</span></span>
* <span data-ttu-id="52b17-252">Rattle 已將 [垃圾郵件]  資料行正確地識別為目標。</span><span class="sxs-lookup"><span data-stu-id="52b17-252">Rattle has correctly identified the **spam** column as the target.</span></span> <span data-ttu-id="52b17-253">選取 [垃圾郵件] 資料行，然後將 [目標資料類型] 設定為 [類別]。</span><span class="sxs-lookup"><span data-stu-id="52b17-253">Select the spam column, then set the **Target Data Type** to **Categoric**.</span></span>

<span data-ttu-id="52b17-254">若要瀏覽資料︰</span><span class="sxs-lookup"><span data-stu-id="52b17-254">To explore the data:</span></span>

* <span data-ttu-id="52b17-255">選取 [瀏覽]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="52b17-255">Select the **Explore** tab.</span></span>
* <span data-ttu-id="52b17-256">依序按一下 [摘要] 和 [執行]，以查看一些關於變數類型的資訊和某些摘要統計資料。</span><span class="sxs-lookup"><span data-stu-id="52b17-256">Click **Summary**, then **Execute**, to see some information about the variable types and some summary statistics.</span></span>
* <span data-ttu-id="52b17-257">若要檢視關於每個變數的其他類型的統計資料，請選取其他選項，例如 [描述] 或 [基本資訊]。</span><span class="sxs-lookup"><span data-stu-id="52b17-257">To view other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="52b17-258">[瀏覽]  索引標籤也可讓您產生許多具洞察力的繪圖。</span><span class="sxs-lookup"><span data-stu-id="52b17-258">The **Explore** tab also allows you to generate many insightful plots.</span></span> <span data-ttu-id="52b17-259">若要繪製資料的長條圖︰</span><span class="sxs-lookup"><span data-stu-id="52b17-259">To plot a histogram of the data:</span></span>

* <span data-ttu-id="52b17-260">選取 [分佈] 。</span><span class="sxs-lookup"><span data-stu-id="52b17-260">Select **Distributions**.</span></span>
* <span data-ttu-id="52b17-261">為 **word_freq_remove** 和 **word_freq_you** 勾選 [長條圖]。</span><span class="sxs-lookup"><span data-stu-id="52b17-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="52b17-262">選取 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="52b17-262">Select **Execute**.</span></span> <span data-ttu-id="52b17-263">您應該會在單一圖形視窗中看到這兩個密度圖，其中清楚顯示「you」這個字在電子郵件中的出現頻率遠高於「remove」。</span><span class="sxs-lookup"><span data-stu-id="52b17-263">You should see both density plots in a single graph window, where it is clear that the word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="52b17-264">相互關聯圖也很有趣。</span><span class="sxs-lookup"><span data-stu-id="52b17-264">The Correlation plots are also interesting.</span></span> <span data-ttu-id="52b17-265">若要建立此圖：</span><span class="sxs-lookup"><span data-stu-id="52b17-265">To create one:</span></span>

* <span data-ttu-id="52b17-266">選擇 [相互關聯] 做為 [類型]，然後</span><span class="sxs-lookup"><span data-stu-id="52b17-266">Choose **Correlation** as the **Type**, then</span></span>
* <span data-ttu-id="52b17-267">選取 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="52b17-267">Select **Execute**.</span></span>
* <span data-ttu-id="52b17-268">Rattle 會警告您，它建議的上限為 40 個變數。</span><span class="sxs-lookup"><span data-stu-id="52b17-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="52b17-269">選取 [是]  以檢視此圖。</span><span class="sxs-lookup"><span data-stu-id="52b17-269">Select **Yes** to view the plot.</span></span>

<span data-ttu-id="52b17-270">圖中會浮現一些有趣的相互關聯：例如，「technology」與「HP」和「labs」有高度相互關聯性。</span><span class="sxs-lookup"><span data-stu-id="52b17-270">There are some interesting correlations that come up: "technology" is strongly correlated to "HP" and "labs", for example.</span></span> <span data-ttu-id="52b17-271">它也與「650」有高度相互關聯性，因為資料集捐贈者的區碼是 650。</span><span class="sxs-lookup"><span data-stu-id="52b17-271">It is also strongly correlated to "650", because the area code of the dataset donors is 650.</span></span>

<span data-ttu-id="52b17-272">文字間相互關聯性的數值可在 [瀏覽] 視窗中取得。</span><span class="sxs-lookup"><span data-stu-id="52b17-272">The numeric values for the correlations between words are available in the Explore window.</span></span> <span data-ttu-id="52b17-273">舉例來說，值得注意的是「technology」與「your」和「money」負面相關。</span><span class="sxs-lookup"><span data-stu-id="52b17-273">It is interesting to note, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="52b17-274">Rattle 可以轉換資料集來處理一些常見的問題。</span><span class="sxs-lookup"><span data-stu-id="52b17-274">Rattle can transform the dataset to handle some common issues.</span></span> <span data-ttu-id="52b17-275">例如，它可讓您調整功能大小、插補遺漏值、處理離群值，以及移除具有遺失資料的變數或觀察值。</span><span class="sxs-lookup"><span data-stu-id="52b17-275">For example, it allows you to rescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="52b17-276">Rattle 也可以識別觀察值和 (或) 變數之間的關聯規則。</span><span class="sxs-lookup"><span data-stu-id="52b17-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="52b17-277">這些索引標籤不在此入門逐步解說的討論範圍內。</span><span class="sxs-lookup"><span data-stu-id="52b17-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="52b17-278">Rattle 也可以執行叢集分析。</span><span class="sxs-lookup"><span data-stu-id="52b17-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="52b17-279">讓我們排除部分功能以讓輸出更方便閱讀。</span><span class="sxs-lookup"><span data-stu-id="52b17-279">Let's exclude some features to make the output easier to read.</span></span> <span data-ttu-id="52b17-280">在 [資料] 索引標籤上，選擇每個變數旁的 [忽略]，但下面這十個項目除外︰</span><span class="sxs-lookup"><span data-stu-id="52b17-280">On the **Data** tab, choose **Ignore** next to each of the variables except these ten items:</span></span>

* <span data-ttu-id="52b17-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="52b17-281">word_freq_hp</span></span>
* <span data-ttu-id="52b17-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="52b17-282">word_freq_technology</span></span>
* <span data-ttu-id="52b17-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="52b17-283">word_freq_george</span></span>
* <span data-ttu-id="52b17-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="52b17-284">word_freq_remove</span></span>
* <span data-ttu-id="52b17-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="52b17-285">word_freq_your</span></span>
* <span data-ttu-id="52b17-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="52b17-286">word_freq_dollar</span></span>
* <span data-ttu-id="52b17-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="52b17-287">word_freq_money</span></span>
* <span data-ttu-id="52b17-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="52b17-288">capital_run_length_longest</span></span>
* <span data-ttu-id="52b17-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="52b17-289">word_freq_business</span></span>
* <span data-ttu-id="52b17-290">spam</span><span class="sxs-lookup"><span data-stu-id="52b17-290">spam</span></span>

<span data-ttu-id="52b17-291">然後返回 [叢集] 索引標籤，選擇 [KMeans]，並將 [叢集數目] 設定為 4。</span><span class="sxs-lookup"><span data-stu-id="52b17-291">Then go back to the **Cluster** tab, choose **KMeans**, and set the *Number of clusters* to 4.</span></span> <span data-ttu-id="52b17-292">然後**執行**。</span><span class="sxs-lookup"><span data-stu-id="52b17-292">Then **Execute**.</span></span> <span data-ttu-id="52b17-293">結果會顯示在輸出視窗中。</span><span class="sxs-lookup"><span data-stu-id="52b17-293">The results are displayed in the output window.</span></span> <span data-ttu-id="52b17-294">有一個叢集具有高頻率的「george」和「hp」，因此可能是合法的商業電子郵件。</span><span class="sxs-lookup"><span data-stu-id="52b17-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="52b17-295">若要建置簡單的決策樹機器學習服務模型︰</span><span class="sxs-lookup"><span data-stu-id="52b17-295">To build a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="52b17-296">選取 [模型]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="52b17-296">Select the **Model** tab,</span></span>
* <span data-ttu-id="52b17-297">選擇 [樹狀結構] 做為 [類型]。</span><span class="sxs-lookup"><span data-stu-id="52b17-297">Choose **Tree** as the **Type**.</span></span>
* <span data-ttu-id="52b17-298">選取 [執行]  ，在輸出視窗中以文字形式顯示樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="52b17-298">Select **Execute** to display the tree in text form in the output window.</span></span>
* <span data-ttu-id="52b17-299">選取 [繪製]  按鈕以檢視圖形化版本。</span><span class="sxs-lookup"><span data-stu-id="52b17-299">Select the **Draw** button to view a graphical version.</span></span> <span data-ttu-id="52b17-300">此版本看起來非常類似我們稍早使用「rpart」 取得的樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="52b17-300">This looks quite similar to the tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="52b17-301">Rattle 的其中一項優秀功能是能夠執行數個機器學習服務方法和快速評估這些方法。</span><span class="sxs-lookup"><span data-stu-id="52b17-301">One of the nice features of Rattle is its ability to run several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="52b17-302">程序如下：</span><span class="sxs-lookup"><span data-stu-id="52b17-302">Here is the procedure:</span></span>

* <span data-ttu-id="52b17-303">選擇 [全部] 做為 [類型]。</span><span class="sxs-lookup"><span data-stu-id="52b17-303">Choose **All** for the **Type**.</span></span>
* <span data-ttu-id="52b17-304">選取 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="52b17-304">Select **Execute**.</span></span>
* <span data-ttu-id="52b17-305">執行完畢後，您可以按一下任何單一 [類型] \(例如 **SVM**) 並檢視結果。</span><span class="sxs-lookup"><span data-stu-id="52b17-305">After it finishes you can click any single **Type**, like **SVM**, and view the results.</span></span>
* <span data-ttu-id="52b17-306">您也可以使用 [評估]  索引標籤比較驗證集上模型的效能。例如，[錯誤矩陣]  選取項目會顯示驗證集上每個模型的混淆矩陣、整體錯誤和平均類別錯誤。</span><span class="sxs-lookup"><span data-stu-id="52b17-306">You can also compare the performance of the models on the validation set using the **Evaluate** tab. For example, the **Error Matrix** selection shows you the confusion matrix, overall error, and averaged class error for each model on the validation set.</span></span>
* <span data-ttu-id="52b17-307">您也可以繪製 ROC 曲線、執行敏感度分析和進行其他類型的模型評估。</span><span class="sxs-lookup"><span data-stu-id="52b17-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="52b17-308">建置完模型之後，選取 [記錄]  索引標籤來檢視 Rattle 在工作階段期間執行的 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="52b17-308">Once you're finished building models, select the **Log** tab to view the R code run by Rattle during your session.</span></span> <span data-ttu-id="52b17-309">您可以選取 [匯出]  按鈕來加以儲存。</span><span class="sxs-lookup"><span data-stu-id="52b17-309">You can select the **Export** button to save it.</span></span>

> [!NOTE]
> <span data-ttu-id="52b17-310">最新版 Rattle 中有一個錯誤。</span><span class="sxs-lookup"><span data-stu-id="52b17-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="52b17-311">若要修改指令碼或使用它在稍後重複執行步驟，您必須在記錄文字的 *Export this log ... * 前面插入 # 字元。</span><span class="sxs-lookup"><span data-stu-id="52b17-311">To modify the script or use it to repeat your steps later, you must insert a # character in front of *Export this log ... * in the text of the log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="52b17-312">PostgreSQL 和 Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="52b17-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="52b17-313">DSVM 隨附安裝 PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="52b17-313">The DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="52b17-314">PostgreSQL 是複雜的開放原始碼關聯式資料庫。</span><span class="sxs-lookup"><span data-stu-id="52b17-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="52b17-315">本節說明如何將垃圾郵件資料集載入至 PostgreSQL，然後進行查詢。</span><span class="sxs-lookup"><span data-stu-id="52b17-315">This section shows how to load our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="52b17-316">在載入資料之前，您必須先允許從 localhost 進行密碼驗證。</span><span class="sxs-lookup"><span data-stu-id="52b17-316">Before you can load the data, you need to allow password authentication from the localhost.</span></span> <span data-ttu-id="52b17-317">在命令提示字元中︰</span><span class="sxs-lookup"><span data-stu-id="52b17-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="52b17-318">組態檔末尾附近有幾行詳細說明允許之連線的文字︰</span><span class="sxs-lookup"><span data-stu-id="52b17-318">Near the bottom of the config file are several lines that detail the allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="52b17-319">將「IPv4 local connections」文字行變更為使用 md5 而非 ident，以便可以使用使用者名稱和密碼來登入︰</span><span class="sxs-lookup"><span data-stu-id="52b17-319">Change the "IPv4 local connections" line to use md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="52b17-320">然後重新啟動 postgres 服務︰</span><span class="sxs-lookup"><span data-stu-id="52b17-320">And restart the postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="52b17-321">若要啟動 psql (PostgreSQL 的互動終端機)，請以內建 postgres 使用者身分從命令提示字元執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="52b17-321">To launch psql, an interactive terminal for PostgreSQL, as the built-in postgres user, run the following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="52b17-322">使用和您目前用來登入之 Linux 帳戶相同的使用者名稱建立新的使用者帳戶，並為它指定密碼︰</span><span class="sxs-lookup"><span data-stu-id="52b17-322">Create a new user account, using the same username as the Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="52b17-323">然後，以使用者身分登入 psql︰</span><span class="sxs-lookup"><span data-stu-id="52b17-323">Then log in to psql as your user:</span></span>

    psql

<span data-ttu-id="52b17-324">並將資料匯入新的資料庫︰</span><span class="sxs-lookup"><span data-stu-id="52b17-324">And import the data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="52b17-325">現在，讓我們使用 **Squirrel SQL**來瀏覽資料並執行一些查詢，此圖形化工具可讓您透過 JDBC 驅動程式與資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="52b17-325">Now, let's explore the data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="52b17-326">若要開始使用，請從 [應用程式] 功能表啟動 Squirrel SQL。</span><span class="sxs-lookup"><span data-stu-id="52b17-326">To get started, launch Squirrel SQL from the Applications menu.</span></span> <span data-ttu-id="52b17-327">若要設定驅動程式︰</span><span class="sxs-lookup"><span data-stu-id="52b17-327">To set up the driver:</span></span>

* <span data-ttu-id="52b17-328">依序選取 [Windows] 和 [檢視驅動程式]。</span><span class="sxs-lookup"><span data-stu-id="52b17-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="52b17-329">以滑鼠右鍵按一下 [PostgreSQL]，然後選取 [修改驅動程式]。</span><span class="sxs-lookup"><span data-stu-id="52b17-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="52b17-330">依序選取 [額外類別路徑] 和 [新增]。</span><span class="sxs-lookup"><span data-stu-id="52b17-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="52b17-331">輸入 ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** 做為 [檔案名稱]。</span><span class="sxs-lookup"><span data-stu-id="52b17-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for the **File Name** and</span></span>
* <span data-ttu-id="52b17-332">選取 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="52b17-332">Select **Open**.</span></span>
* <span data-ttu-id="52b17-333">選擇 [列出驅動程式]，接著在 [類別名稱] 中選取 [org.postgresql.Driver]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="52b17-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="52b17-334">若要設定與本機伺服器的連線︰</span><span class="sxs-lookup"><span data-stu-id="52b17-334">To set up the connection to the local server:</span></span>

* <span data-ttu-id="52b17-335">依序選取 [Windows] 和 [檢視別名]。</span><span class="sxs-lookup"><span data-stu-id="52b17-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="52b17-336">選擇 [+] **+** 按鈕建立新的別名。</span><span class="sxs-lookup"><span data-stu-id="52b17-336">Choose the **+** button to make a new alias.</span></span>
* <span data-ttu-id="52b17-337">將其命名為*垃圾郵件資料庫*，然後選擇 [驅動程式] 下拉式清單中的 [PostgreSQL]。</span><span class="sxs-lookup"><span data-stu-id="52b17-337">Name it *Spam database*, choose **PostgreSQL** in the **Driver** drop-down.</span></span>
* <span data-ttu-id="52b17-338">將 URL 設定為 *jdbc:postgresql://localhost/spam*。</span><span class="sxs-lookup"><span data-stu-id="52b17-338">Set the URL to *jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="52b17-339">輸入您的*使用者名稱*和*密碼*。</span><span class="sxs-lookup"><span data-stu-id="52b17-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="52b17-340">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="52b17-340">Click **OK**.</span></span>
* <span data-ttu-id="52b17-341">若要開啟 [連線] 視窗，請按兩下***垃圾郵件資料庫***別名。</span><span class="sxs-lookup"><span data-stu-id="52b17-341">To open the **Connection** window, double-click the ***Spam database*** alias.</span></span>
* <span data-ttu-id="52b17-342">選取 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="52b17-342">Select **Connect**.</span></span>

<span data-ttu-id="52b17-343">若要執行一些查詢︰</span><span class="sxs-lookup"><span data-stu-id="52b17-343">To run some queries:</span></span>

* <span data-ttu-id="52b17-344">選取 [SQL]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="52b17-344">Select the **SQL** tab.</span></span>
* <span data-ttu-id="52b17-345">在 [SQL] 索引標籤頂端的查詢文字方塊中輸入簡單的查詢，例如 `SELECT * from data;` 。</span><span class="sxs-lookup"><span data-stu-id="52b17-345">Enter a simple query such as `SELECT * from data;` in the query textbox at the top of the SQL tab.</span></span>
* <span data-ttu-id="52b17-346">按 **Ctrl-Enter** 來加以執行。</span><span class="sxs-lookup"><span data-stu-id="52b17-346">Press **Ctrl-Enter** to run it.</span></span> <span data-ttu-id="52b17-347">依預設，Squirrel SQL 會傳回查詢的前 100 個資料列。</span><span class="sxs-lookup"><span data-stu-id="52b17-347">By default Squirrel SQL returns the first 100 rows from your query.</span></span>

<span data-ttu-id="52b17-348">還有許多可供您執行以瀏覽此資料的查詢。</span><span class="sxs-lookup"><span data-stu-id="52b17-348">There are many more queries you could run to explore this data.</span></span> <span data-ttu-id="52b17-349">例如，「make」  一字在垃圾郵件和非垃圾郵件之間的出現頻率有何差異？</span><span class="sxs-lookup"><span data-stu-id="52b17-349">For example, how does the frequency of the word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="52b17-350">或者，經常包含「3d」 的電子郵件有何特性？</span><span class="sxs-lookup"><span data-stu-id="52b17-350">Or what are the characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="52b17-351">大部分頻繁出現「3d」  的電子郵件顯然是垃圾郵件，因此是很適合用來建置預測性模型以分類電子郵件的特徵。</span><span class="sxs-lookup"><span data-stu-id="52b17-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model to classify the emails.</span></span>

<span data-ttu-id="52b17-352">如果您想要對 PostgreSQL 資料庫中儲存的資料執行機器學習服務，請考慮使用 [MADlib](http://madlib.incubator.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="52b17-352">If you wanted to perform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="52b17-353">SQL Server 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="52b17-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="52b17-354">Azure SQL 資料倉儲是一種雲端架構、相應放大的資料庫，可處理大量的關聯式與非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="52b17-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="52b17-355">如需詳細資訊，請參閱 [什麼是 Azure SQL 資料倉儲？](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="52b17-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="52b17-356">若要連線到資料倉儲並建立資料表，請從命令提示字元執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="52b17-356">To connect to the data warehouse and create the table, run the following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="52b17-357">然後，在 sqlcmd 提示字元中︰</span><span class="sxs-lookup"><span data-stu-id="52b17-357">Then at the sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="52b17-358">使用 bcp 複製資料︰</span><span class="sxs-lookup"><span data-stu-id="52b17-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="52b17-359">所下載檔案中的行尾結束符號為 Windows 樣式，但 bcp 需要 UNIX 樣式，因此我們必須使用 -r 旗標將這一點告訴 bcp。</span><span class="sxs-lookup"><span data-stu-id="52b17-359">The line endings in the downloaded file are Windows-style, but bcp expects UNIX-style, so we need to tell bcp that with the -r flag.</span></span>
>
>

<span data-ttu-id="52b17-360">並使用 sqlcmd 進行查詢︰</span><span class="sxs-lookup"><span data-stu-id="52b17-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="52b17-361">您也可以使用 Squirrel SQL 進行查詢。</span><span class="sxs-lookup"><span data-stu-id="52b17-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="52b17-362">使用 Microsoft MSSQL Server JDBC 驅動程式 (可在 ***/usr/share/java/jdbcdrivers/sqljdbc42.jar*** 中找到) 按照適用於 PostgreSQL 的類似步驟來進行。</span><span class="sxs-lookup"><span data-stu-id="52b17-362">Follow similar steps for PostgreSQL, using the Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52b17-363">後續步驟</span><span class="sxs-lookup"><span data-stu-id="52b17-363">Next steps</span></span>
<span data-ttu-id="52b17-364">如需能引導您完成在 Azure 中構成資料科學程序之工作的主題概觀，請參閱 [Team Data Science Process](http://aka.ms/datascienceprocess)。</span><span class="sxs-lookup"><span data-stu-id="52b17-364">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="52b17-365">如需會示範 Team Data Science Process 中適用於特定案例之步驟的其他端對端逐步解說的說明，請參閱 [Team Data Science Process 逐步解說](data-science-process-walkthroughs.md)。</span><span class="sxs-lookup"><span data-stu-id="52b17-365">For a description of other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="52b17-366">這些逐步解說也示範如何將雲端和內部部署工具與服務組合成工作流程或管線，以建立智慧型應用程式。</span><span class="sxs-lookup"><span data-stu-id="52b17-366">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>
