---
title: Azure 監視器 (預覽) 中的 Azure Active Directory 活動記錄 | Microsoft Docs
description: Azure 監視器 (預覽) 中的 Azure Active Directory 活動記錄概觀
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 07/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 357c19700e4388f31c0f07645ff1c3adf442c1aa
ms.sourcegitcommit: 3f8f973f095f6f878aa3e2383db0d296365a4b18
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2018
ms.locfileid: "42023937"
---
# <a name="azure-ad-activity-logs-in-azure-monitor-preview"></a><span data-ttu-id="9e13d-103">Azure 監視器 (預覽) 中的 Azure AD 活動記錄</span><span class="sxs-lookup"><span data-stu-id="9e13d-103">Azure AD activity logs in Azure Monitor (preview)</span></span>

<span data-ttu-id="9e13d-104">您現在可以使用 Azure 監視器，將 Azure Active Directory (Azure AD) 活動記錄路由傳送至您自己的儲存體帳戶或事件中樞。</span><span class="sxs-lookup"><span data-stu-id="9e13d-104">You can now route Azure Active Directory (Azure AD) activity logs to your own storage account or event hub by using Azure Monitor.</span></span> <span data-ttu-id="9e13d-105">透過 Azure 監視器中的公開預覽版 Azure Active Directory 記錄，您可以：</span><span class="sxs-lookup"><span data-stu-id="9e13d-105">With the public preview of Azure Active Directory logs in Azure Monitor, you can:</span></span>

* <span data-ttu-id="9e13d-106">封存 Azure 儲存體帳戶的稽核記錄，讓您長時間保存資料。</span><span class="sxs-lookup"><span data-stu-id="9e13d-106">Archive your audit logs for an Azure storage account, which enables you to retain the data for a long time.</span></span>
* <span data-ttu-id="9e13d-107">將稽核記錄串流至 Azure 事件中樞，以便使用 Splunk 和 QRadar 等常用的安全性資訊與事件管理 (SIEM) 工具進行分析。</span><span class="sxs-lookup"><span data-stu-id="9e13d-107">Stream your audit logs to an Azure event hub for analytics by using popular Security Information and Event Management (SIEM) tools, such as Splunk and QRadar.</span></span>
* <span data-ttu-id="9e13d-108">將稽核記錄串流至事件中樞，將其與您自己的自訂記錄解決方案整合。</span><span class="sxs-lookup"><span data-stu-id="9e13d-108">Integrate your audit logs with your own custom log solutions by streaming them to an event hub.</span></span>

> [!VIDEO https://www.youtube.com/embed/syT-9KNfug8]

## <a name="supported-reports"></a><span data-ttu-id="9e13d-109">支援的報告</span><span class="sxs-lookup"><span data-stu-id="9e13d-109">Supported reports</span></span>

<span data-ttu-id="9e13d-110">您可以使用這項功能將稽核活動記錄和登入活動記錄路由至您的 Azure 儲存體帳戶、事件中樞或自訂解決方案。</span><span class="sxs-lookup"><span data-stu-id="9e13d-110">You can route audit activity logs and sign-in activity logs to your Azure storage account, event hub, or custom solution by using this feature.</span></span> 

* <span data-ttu-id="9e13d-111">**稽核記錄**：[稽核記錄活動報告](concept-audit-logs.md)可讓您對每個在租用戶中執行的工作存取歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="9e13d-111">**Audit logs**: The [audit logs activity report](concept-audit-logs.md) gives you access to the history of every task that's performed in your tenant.</span></span>
* <span data-ttu-id="9e13d-112">**登入記錄**：透過[登入活動報告](concept-sign-ins.md)，您可以判斷是誰執行了稽核記錄中所報告的工作。</span><span class="sxs-lookup"><span data-stu-id="9e13d-112">**Sign-in logs**: With the [sign-in activity report](concept-sign-ins.md), you can determine who performed the tasks that are reported in the audit logs.</span></span>

> [!NOTE]
> <span data-ttu-id="9e13d-113">目前不支援與 B2C 相關的稽核和登入活動記錄。</span><span class="sxs-lookup"><span data-stu-id="9e13d-113">B2C-related audit and sign-in activity logs are not supported at this time.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="9e13d-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="9e13d-114">Prerequisites</span></span>

<span data-ttu-id="9e13d-115">若要使用此功能，您必須要有：</span><span class="sxs-lookup"><span data-stu-id="9e13d-115">To use this feature, you need:</span></span>

* <span data-ttu-id="9e13d-116">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e13d-116">An Azure subscription.</span></span> <span data-ttu-id="9e13d-117">如果您沒有 Azure 訂用帳戶，您可以[註冊免費試用](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-117">If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="9e13d-118">Azure AD Free、Basic、Premium 1 或 Premium 2 [授權](https://azure.microsoft.com/pricing/details/active-directory/)，用以存取 Azure 入口網站中的 Azure AD 稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="9e13d-118">Azure AD Free, Basic, Premium 1, or Premium 2 [license](https://azure.microsoft.com/pricing/details/active-directory/), to access the Azure AD audit logs in the Azure portal.</span></span> 
* <span data-ttu-id="9e13d-119">Azure AD Premium 1 或 Premium 2 [授權](https://azure.microsoft.com/pricing/details/active-directory/)，用以存取 Azure 入口網站中的 Azure AD 登入記錄。</span><span class="sxs-lookup"><span data-stu-id="9e13d-119">Azure AD Premium 1, or Premium 2 [license](https://azure.microsoft.com/pricing/details/active-directory/), to access the Azure AD sign-in logs in the Azure portal.</span></span> 

<span data-ttu-id="9e13d-120">根據您要路由稽核記錄資料的位置，您必須要有下列任何一項：</span><span class="sxs-lookup"><span data-stu-id="9e13d-120">Depending on where you want to route the audit log data, you need either of the following:</span></span>

* <span data-ttu-id="9e13d-121">您具有 *ListKeys* 權限的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e13d-121">An Azure storage account that you have *ListKeys* permissions for.</span></span> <span data-ttu-id="9e13d-122">建議您使用一般儲存體帳戶，而不要使用 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e13d-122">We recommend that you use a general storage account and not a Blob storage account.</span></span> <span data-ttu-id="9e13d-123">如需儲存體定價資訊，請參閱 [Azure 儲存體定價計算機](https://azure.microsoft.com/pricing/calculator/?service=storage)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-123">For storage pricing information, see the [Azure Storage pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=storage).</span></span> 
* <span data-ttu-id="9e13d-124">Azure 事件中樞命名空間，以便與第三方解決方案整合。</span><span class="sxs-lookup"><span data-stu-id="9e13d-124">An Azure Event Hubs namespace to integrate with third-party solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="9e13d-125">若要存取 Azure AD 活動記錄，您必須是 Azure AD 租用戶中的「全域系統管理員」或「安全性系統管理員」。</span><span class="sxs-lookup"><span data-stu-id="9e13d-125">To access the Azure AD activity logs, you need to be a *global administrator* or *security administrator* in the Azure AD tenant.</span></span>
>

## <a name="cost-considerations"></a><span data-ttu-id="9e13d-126">成本考量</span><span class="sxs-lookup"><span data-stu-id="9e13d-126">Cost considerations</span></span>

<span data-ttu-id="9e13d-127">如果您已有 Azure AD 授權，您必須要有用來設定儲存體帳戶和事件中樞的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e13d-127">If you already have an Azure AD license, you need an Azure subscription to set up the storage account and event hub.</span></span> <span data-ttu-id="9e13d-128">Azure 訂用帳戶會免費提供，但是您必須付費才能使用 Azure 資源，包括用於封存的儲存體帳戶，和用於串流的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="9e13d-128">The Azure subscription comes at no cost, but you have to pay to utilize Azure resources, including the storage account that you use for archival and the event hub that you use for streaming.</span></span> <span data-ttu-id="9e13d-129">資料量和連帶產生的費用會隨著租用戶大小而有大幅差異。</span><span class="sxs-lookup"><span data-stu-id="9e13d-129">The amount of data and, thus, the cost incurred, can vary significantly depending on the tenant size.</span></span> 

### <a name="storage-size-for-activity-logs"></a><span data-ttu-id="9e13d-130">活動記錄的儲存體大小</span><span class="sxs-lookup"><span data-stu-id="9e13d-130">Storage size for activity logs</span></span>

<span data-ttu-id="9e13d-131">每個稽核記錄事件會使用約 2KB 的資料儲存體。</span><span class="sxs-lookup"><span data-stu-id="9e13d-131">Every audit log event uses about 2 KB of data storage.</span></span> <span data-ttu-id="9e13d-132">對具有 100,000 名使用者的租用戶而言，每天大約會產生 150 萬個事件，因此您每天需要約 3 GB 的資料儲存體。</span><span class="sxs-lookup"><span data-stu-id="9e13d-132">For a tenant with 100,000 users, which would incur about 1.5 million events per day, you would need about 3 GB of data storage per day.</span></span> <span data-ttu-id="9e13d-133">由於寫入會以約 5 分鐘的批次執行，因此您可以預期每個月大概會有 9000 個寫入作業。</span><span class="sxs-lookup"><span data-stu-id="9e13d-133">Because writes occur in approximately five-minute batches, you can anticipate approximately 9,000 write operations per month.</span></span> 

<span data-ttu-id="9e13d-134">下表包含以租用戶大小為準的估計成本，儲存體帳戶是位於美國西部的一般用途 v2 帳戶，保留期間至少一年。</span><span class="sxs-lookup"><span data-stu-id="9e13d-134">The following table contains a cost estimate of, depending on the size of the tenant, a general-purpose v2 storage account in West US for at least one year of retention.</span></span> <span data-ttu-id="9e13d-135">若要針對您預期應用程式將使用的資料量建立更精確的估計值，請使用 [Azure 儲存體定價計算機](https://azure.microsoft.com/pricing/details/storage/blobs/)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-135">To create a more accurate estimate for the data volume that you anticipate for your application, use the [Azure storage pricing calculator](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span> 

| <span data-ttu-id="9e13d-136">記錄分類</span><span class="sxs-lookup"><span data-stu-id="9e13d-136">Log category</span></span> | <span data-ttu-id="9e13d-137">使用者人數</span><span class="sxs-lookup"><span data-stu-id="9e13d-137">Number of users</span></span> | <span data-ttu-id="9e13d-138">每日事件數</span><span class="sxs-lookup"><span data-stu-id="9e13d-138">Events per day</span></span> | <span data-ttu-id="9e13d-139">每月資料量 (估計值)</span><span class="sxs-lookup"><span data-stu-id="9e13d-139">Volume of data per month (est.)</span></span> | <span data-ttu-id="9e13d-140">每月成本 (估計值)</span><span class="sxs-lookup"><span data-stu-id="9e13d-140">Cost per month (est.)</span></span> | <span data-ttu-id="9e13d-141">每年成本 (估計值)</span><span class="sxs-lookup"><span data-stu-id="9e13d-141">Cost per year (est.)</span></span> |
|--------------|-----------------|----------------------|--------------------------------------|----------------------------|---------------------------|
| <span data-ttu-id="9e13d-142">稽核</span><span class="sxs-lookup"><span data-stu-id="9e13d-142">Audit</span></span> | <span data-ttu-id="9e13d-143">100,000</span><span class="sxs-lookup"><span data-stu-id="9e13d-143">100,000</span></span> | <span data-ttu-id="9e13d-144">150&nbsp;萬</span><span class="sxs-lookup"><span data-stu-id="9e13d-144">1.5&nbsp;million</span></span> | <span data-ttu-id="9e13d-145">90 GB</span><span class="sxs-lookup"><span data-stu-id="9e13d-145">90 GB</span></span> | <span data-ttu-id="9e13d-146">$1.93</span><span class="sxs-lookup"><span data-stu-id="9e13d-146">$1.93</span></span> | <span data-ttu-id="9e13d-147">$23.12</span><span class="sxs-lookup"><span data-stu-id="9e13d-147">$23.12</span></span> |
| <span data-ttu-id="9e13d-148">稽核</span><span class="sxs-lookup"><span data-stu-id="9e13d-148">Audit</span></span> | <span data-ttu-id="9e13d-149">1,000</span><span class="sxs-lookup"><span data-stu-id="9e13d-149">1,000</span></span> | <span data-ttu-id="9e13d-150">15,000</span><span class="sxs-lookup"><span data-stu-id="9e13d-150">15,000</span></span> | <span data-ttu-id="9e13d-151">900 MB</span><span class="sxs-lookup"><span data-stu-id="9e13d-151">900 MB</span></span> | <span data-ttu-id="9e13d-152">$0.02</span><span class="sxs-lookup"><span data-stu-id="9e13d-152">$0.02</span></span> | <span data-ttu-id="9e13d-153">$0.24</span><span class="sxs-lookup"><span data-stu-id="9e13d-153">$0.24</span></span> |
| <span data-ttu-id="9e13d-154">登入</span><span class="sxs-lookup"><span data-stu-id="9e13d-154">Sign-ins</span></span> | <span data-ttu-id="9e13d-155">1,000</span><span class="sxs-lookup"><span data-stu-id="9e13d-155">1,000</span></span> | <span data-ttu-id="9e13d-156">34,800</span><span class="sxs-lookup"><span data-stu-id="9e13d-156">34,800</span></span> | <span data-ttu-id="9e13d-157">4 GB</span><span class="sxs-lookup"><span data-stu-id="9e13d-157">4 GB</span></span> | <span data-ttu-id="9e13d-158">$0.13</span><span class="sxs-lookup"><span data-stu-id="9e13d-158">$0.13</span></span> | <span data-ttu-id="9e13d-159">$1.56</span><span class="sxs-lookup"><span data-stu-id="9e13d-159">$1.56</span></span> |
| <span data-ttu-id="9e13d-160">登入</span><span class="sxs-lookup"><span data-stu-id="9e13d-160">Sign-ins</span></span> | <span data-ttu-id="9e13d-161">100,000</span><span class="sxs-lookup"><span data-stu-id="9e13d-161">100,000</span></span> | <span data-ttu-id="9e13d-162">1500&nbsp;萬</span><span class="sxs-lookup"><span data-stu-id="9e13d-162">15&nbsp;million</span></span> | <span data-ttu-id="9e13d-163">1.7 TB</span><span class="sxs-lookup"><span data-stu-id="9e13d-163">1.7 TB</span></span> | <span data-ttu-id="9e13d-164">$35.41</span><span class="sxs-lookup"><span data-stu-id="9e13d-164">$35.41</span></span> | <span data-ttu-id="9e13d-165">$424.92</span><span class="sxs-lookup"><span data-stu-id="9e13d-165">$424.92</span></span> | 


### <a name="event-hub-messages-for-activity-logs"></a><span data-ttu-id="9e13d-166">活動記錄的事件中樞訊息</span><span class="sxs-lookup"><span data-stu-id="9e13d-166">Event hub messages for activity logs</span></span>

<span data-ttu-id="9e13d-167">事件會以約五分鐘的間隔分批處理，並以包含該時間範圍內所有事件的單一訊息形式傳送。</span><span class="sxs-lookup"><span data-stu-id="9e13d-167">Events are batched into approximately five-minute intervals and sent as a single message that contains all the events within that timeframe.</span></span> <span data-ttu-id="9e13d-168">事件中樞內的訊息大小上限為 256 KB，如果在時間範圍內所有訊息的總大小超過該數量，就會傳送多個訊息。</span><span class="sxs-lookup"><span data-stu-id="9e13d-168">A message in the event hub has a maximum size of 256 KB, and if the total size of all the messages within the timeframe exceeds that volume, multiple messages are sent.</span></span> 

<span data-ttu-id="9e13d-169">例如，使用者人數超過 100,000 名的大型租用戶每秒通常會有約 18 個事件，相當於每 5 分鐘有 5,400 個事件。</span><span class="sxs-lookup"><span data-stu-id="9e13d-169">For example, about 18 events per second ordinarily occur for a large tenant of more than 100,000 users, a rate that equates to 5,400 events every five minutes.</span></span> <span data-ttu-id="9e13d-170">稽核記錄是每個事件約 2 KB，因為這相當於 10.8 MB 的資料。</span><span class="sxs-lookup"><span data-stu-id="9e13d-170">Because audit logs are about 2 KB per event, this equates to 10.8 MB of data.</span></span> <span data-ttu-id="9e13d-171">因此，有 43 則訊息會在該五分鐘間隔內傳送至事件中樞。</span><span class="sxs-lookup"><span data-stu-id="9e13d-171">Therefore, 43 messages are sent to the event hub in that five-minute interval.</span></span> 

<span data-ttu-id="9e13d-172">下表包含美國西部基本事件中樞的每月估計成本 (視事件資料量而定)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-172">The following table contains estimated costs per month for a basic event hub in West US, depending on the volume of event data.</span></span> <span data-ttu-id="9e13d-173">若要針對您預期應用程式將使用的資料量計算精確的估計值，請使用[事件中樞定價計算機](https://azure.microsoft.com/pricing/details/event-hubs/)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-173">To calculate an accurate estimate of the data volume that you anticipate for your application, use the [Event Hubs pricing calculator](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

| <span data-ttu-id="9e13d-174">記錄分類</span><span class="sxs-lookup"><span data-stu-id="9e13d-174">Log category</span></span> | <span data-ttu-id="9e13d-175">使用者人數</span><span class="sxs-lookup"><span data-stu-id="9e13d-175">Number of users</span></span> | <span data-ttu-id="9e13d-176">每秒事件數</span><span class="sxs-lookup"><span data-stu-id="9e13d-176">Events per second</span></span> | <span data-ttu-id="9e13d-177">每 5 分鐘間隔的事件數</span><span class="sxs-lookup"><span data-stu-id="9e13d-177">Events per five-minute interval</span></span> | <span data-ttu-id="9e13d-178">每一間隔的數量</span><span class="sxs-lookup"><span data-stu-id="9e13d-178">Volume per interval</span></span> | <span data-ttu-id="9e13d-179">每一間隔的訊息數</span><span class="sxs-lookup"><span data-stu-id="9e13d-179">Messages per interval</span></span> | <span data-ttu-id="9e13d-180">每月訊息數</span><span class="sxs-lookup"><span data-stu-id="9e13d-180">Messages per month</span></span> | <span data-ttu-id="9e13d-181">每月成本 (估計值)</span><span class="sxs-lookup"><span data-stu-id="9e13d-181">Cost per month (est.)</span></span> |
|--------------|-----------------|-------------------------|----------------------------------------|---------------------|---------------------------------|------------------------------|----------------------------|
| <span data-ttu-id="9e13d-182">稽核</span><span class="sxs-lookup"><span data-stu-id="9e13d-182">Audit</span></span> | <span data-ttu-id="9e13d-183">100,000</span><span class="sxs-lookup"><span data-stu-id="9e13d-183">100,000</span></span> | <span data-ttu-id="9e13d-184">18</span><span class="sxs-lookup"><span data-stu-id="9e13d-184">18</span></span> | <span data-ttu-id="9e13d-185">5,400</span><span class="sxs-lookup"><span data-stu-id="9e13d-185">5,400</span></span> | <span data-ttu-id="9e13d-186">10.8 MB</span><span class="sxs-lookup"><span data-stu-id="9e13d-186">10.8 MB</span></span> | <span data-ttu-id="9e13d-187">43</span><span class="sxs-lookup"><span data-stu-id="9e13d-187">43</span></span> | <span data-ttu-id="9e13d-188">371,520</span><span class="sxs-lookup"><span data-stu-id="9e13d-188">371,520</span></span> | <span data-ttu-id="9e13d-189">$10.83</span><span class="sxs-lookup"><span data-stu-id="9e13d-189">$10.83</span></span> |
| <span data-ttu-id="9e13d-190">稽核</span><span class="sxs-lookup"><span data-stu-id="9e13d-190">Audit</span></span> | <span data-ttu-id="9e13d-191">1,000</span><span class="sxs-lookup"><span data-stu-id="9e13d-191">1,000</span></span> | <span data-ttu-id="9e13d-192">0.1</span><span class="sxs-lookup"><span data-stu-id="9e13d-192">0.1</span></span> | <span data-ttu-id="9e13d-193">52</span><span class="sxs-lookup"><span data-stu-id="9e13d-193">52</span></span> | <span data-ttu-id="9e13d-194">104 KB</span><span class="sxs-lookup"><span data-stu-id="9e13d-194">104 KB</span></span> | <span data-ttu-id="9e13d-195">1</span><span class="sxs-lookup"><span data-stu-id="9e13d-195">1</span></span> | <span data-ttu-id="9e13d-196">8,640</span><span class="sxs-lookup"><span data-stu-id="9e13d-196">8,640</span></span> | <span data-ttu-id="9e13d-197">$10.80</span><span class="sxs-lookup"><span data-stu-id="9e13d-197">$10.80</span></span> |
| <span data-ttu-id="9e13d-198">登入</span><span class="sxs-lookup"><span data-stu-id="9e13d-198">Sign-ins</span></span> | <span data-ttu-id="9e13d-199">1,000</span><span class="sxs-lookup"><span data-stu-id="9e13d-199">1,000</span></span> | <span data-ttu-id="9e13d-200">178</span><span class="sxs-lookup"><span data-stu-id="9e13d-200">178</span></span> | <span data-ttu-id="9e13d-201">53,400</span><span class="sxs-lookup"><span data-stu-id="9e13d-201">53,400</span></span> | <span data-ttu-id="9e13d-202">106.8&nbsp;MB</span><span class="sxs-lookup"><span data-stu-id="9e13d-202">106.8&nbsp;MB</span></span> | <span data-ttu-id="9e13d-203">418</span><span class="sxs-lookup"><span data-stu-id="9e13d-203">418</span></span> | <span data-ttu-id="9e13d-204">3,611,520</span><span class="sxs-lookup"><span data-stu-id="9e13d-204">3,611,520</span></span> | <span data-ttu-id="9e13d-205">$11.06</span><span class="sxs-lookup"><span data-stu-id="9e13d-205">$11.06</span></span> |  


## <a name="frequently-asked-questions"></a><span data-ttu-id="9e13d-206">常見問題集</span><span class="sxs-lookup"><span data-stu-id="9e13d-206">Frequently asked questions</span></span>

<span data-ttu-id="9e13d-207">這一節會回答 Azure 監視器中 Azure AD 記錄的常見問題集，以及討論已知的問題。</span><span class="sxs-lookup"><span data-stu-id="9e13d-207">This section answers frequently asked questions and discusses known issues with Azure AD logs in Azure Monitor.</span></span>

<span data-ttu-id="9e13d-208">**問: 我該從何處著手？**</span><span class="sxs-lookup"><span data-stu-id="9e13d-208">**Q: Where should I start?**</span></span> 

<span data-ttu-id="9e13d-209">**答**: 本文討論您部署此功能時所需的項目。</span><span class="sxs-lookup"><span data-stu-id="9e13d-209">**A**: This article discusses what you need to deploy this feature.</span></span> <span data-ttu-id="9e13d-210">在您滿足先決條件後，請前往可協助設定以及將記錄路由傳送至事件中樞的教學課程。</span><span class="sxs-lookup"><span data-stu-id="9e13d-210">After you've satisfied the prerequisites, go to the tutorials that can help you configure and route your logs to an event hub.</span></span>

---

<span data-ttu-id="9e13d-211">**問: 其中包含哪些記錄？**</span><span class="sxs-lookup"><span data-stu-id="9e13d-211">**Q: Which logs are included?**</span></span>

<span data-ttu-id="9e13d-212">**答**: 登入活動記錄和稽核記錄都可透過這項功能路由傳送，但目前不包含 B2C 相關稽核事件。</span><span class="sxs-lookup"><span data-stu-id="9e13d-212">**A**: The sign-in activity logs and audit logs are both available for routing through this feature, although B2C-related audit events are currently not included.</span></span> <span data-ttu-id="9e13d-213">若要找出目前支援哪些類型的記錄和哪些以功能為基礎的記錄，請參閱[稽核記錄結構描述](reference-azure-monitor-audit-log-schema.md)和[登入記錄結構描述](reference-azure-monitor-sign-ins-log-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-213">To find out which types of logs and which feature-based logs are currently supported, see [Audit log schema](reference-azure-monitor-audit-log-schema.md) and [Sign-in log schema](reference-azure-monitor-sign-ins-log-schema.md).</span></span> 

---

<span data-ttu-id="9e13d-214">**問: 在執行動作後，多久會在事件中樞內顯示對應的記錄？**</span><span class="sxs-lookup"><span data-stu-id="9e13d-214">**Q: How soon after an action do the corresponding logs show up in event hubs?**</span></span>

<span data-ttu-id="9e13d-215">**答**: 在執行動作後，記錄應該會在二到五分鐘內顯示於事件中樞。</span><span class="sxs-lookup"><span data-stu-id="9e13d-215">**A**: The logs should show up in your event hub within two to five minutes after the action is performed.</span></span> <span data-ttu-id="9e13d-216">如需事件中樞的詳細資訊，請參閱[什麼是 Azure 事件中樞？](../../event-hubs/event-hubs-about.md)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-216">For more information about Event Hubs, see [What is Azure Event Hubs?](../../event-hubs/event-hubs-about.md).</span></span>

---

<span data-ttu-id="9e13d-217">**問:： 在執行動作後，多久會在儲存體帳戶中顯示對應的記錄？**</span><span class="sxs-lookup"><span data-stu-id="9e13d-217">**Q: How soon after an action do the corresponding logs show up in storage accounts?**</span></span>

<span data-ttu-id="9e13d-218">**答**: 就 Azure 儲存體帳戶而言，延遲介於執行動作後的 5 到 15 分鐘之間。</span><span class="sxs-lookup"><span data-stu-id="9e13d-218">**A**: For Azure storage accounts, the latency is anywhere from 5 to 15 minutes after the action is performed.</span></span>

---

<span data-ttu-id="9e13d-219">**問: 儲存資料需要多少成本？**</span><span class="sxs-lookup"><span data-stu-id="9e13d-219">**Q: How much will it cost to store my data?**</span></span>

<span data-ttu-id="9e13d-220">**答**: 儲存體成本取決於您的記錄大小，以及您所選擇的保留期間。</span><span class="sxs-lookup"><span data-stu-id="9e13d-220">**A**: The storage costs depend on both the size of your logs and the retention period you choose.</span></span> <span data-ttu-id="9e13d-221">如需租用戶的估計成本清單 (取決於所產生的記錄數量)，請參閱[活動記錄的儲存體大小](#storage-size-for-activity-logs)一節。</span><span class="sxs-lookup"><span data-stu-id="9e13d-221">For a list of the estimated costs for tenants, which depend on the volume of logs generated, see the [Storage size for activity logs](#storage-size-for-activity-logs) section.</span></span>

---

<span data-ttu-id="9e13d-222">**問: 將資料串流至事件中樞需要多少成本？**</span><span class="sxs-lookup"><span data-stu-id="9e13d-222">**Q: How much will it cost to stream my data to an event hub?**</span></span>

<span data-ttu-id="9e13d-223">**答**: 串流成本取決於您每分鐘收到的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="9e13d-223">**A**: The streaming costs depend on the number of messages you receive per minute.</span></span> <span data-ttu-id="9e13d-224">本文討論如何計算成本並列出成本估計值 (以訊息數目為基礎)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-224">This article discusses how the costs are calculated and lists cost estimates, which are based on the number of messages.</span></span> 

---

<span data-ttu-id="9e13d-225">**問: 如何整合 Azure AD 活動記錄與我的 SIEM 系統？**</span><span class="sxs-lookup"><span data-stu-id="9e13d-225">**Q: How do I integrate Azure AD activity logs with my SIEM system?**</span></span>

<span data-ttu-id="9e13d-226">**答**: 您可以使用兩種方式執行此動作：</span><span class="sxs-lookup"><span data-stu-id="9e13d-226">**A**: You can do this in two ways:</span></span>

- <span data-ttu-id="9e13d-227">使用 Azure 監視器與事件中樞將記錄串流至您的 SIEM 系統。</span><span class="sxs-lookup"><span data-stu-id="9e13d-227">Use Azure Monitor with Event Hubs to stream logs to your SIEM system.</span></span> <span data-ttu-id="9e13d-228">首先，[將記錄串流至事件中樞](quickstart-azure-monitor-stream-logs-to-event-hub.md)，然後使用已設定的事件中樞[設定您的 SIEM 工具](quickstart-azure-monitor-stream-logs-to-event-hub.md#access-data-from-your-event-hub)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-228">First, [stream the logs to an event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md) and then [set up your SIEM tool](quickstart-azure-monitor-stream-logs-to-event-hub.md#access-data-from-your-event-hub) with the configured event hub.</span></span> 

- <span data-ttu-id="9e13d-229">使用[報告圖形 API](concept-reporting-api.md) 存取資料，然後使用自己的指令碼將資料推送至 SIEM 系統中。</span><span class="sxs-lookup"><span data-stu-id="9e13d-229">Use the [Reporting Graph API](concept-reporting-api.md) to access the data, and push it into the SIEM system using your own scripts.</span></span>

---

<span data-ttu-id="9e13d-230">**問: 目前支援哪些 SIEM 工具？**</span><span class="sxs-lookup"><span data-stu-id="9e13d-230">**Q: What SIEM tools are currently supported?**</span></span> 

<span data-ttu-id="9e13d-231">**答**: 目前支援 Azure 監視器的有 [Splunk](tutorial-integrate-activity-logs-with-splunk.md)、QRadar 及 [Sumo Logic](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-231">**A**: Currently, Azure Monitor is supported by [Splunk](tutorial-integrate-activity-logs-with-splunk.md), QRadar, and [Sumo Logic](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory).</span></span> <span data-ttu-id="9e13d-232">如需連接器運作方式的詳細資訊，請參閱[將 Azure 監視資料串流至事件中樞以供外部工具取用](../../monitoring-and-diagnostics/monitor-stream-monitoring-data-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-232">For more information about how the connectors work, see [Stream Azure monitoring data to an event hub for consumption by an external tool](../../monitoring-and-diagnostics/monitor-stream-monitoring-data-event-hubs.md).</span></span>

---

<span data-ttu-id="9e13d-233">**問: 如何整合 Azure AD 活動記錄與我的 Splunk 執行個體？**</span><span class="sxs-lookup"><span data-stu-id="9e13d-233">**Q: How do I integrate Azure AD activity logs with my Splunk instance?**</span></span>

<span data-ttu-id="9e13d-234">**答**: 首先，[將 Azure AD 活動記錄路由至事件中樞](quickstart-azure-monitor-stream-logs-to-event-hub.md)，然後依照步驟[整合活動記錄與 Splunk](tutorial-integrate-activity-logs-with-splunk.md)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-234">**A**: First, [route the Azure AD activity logs to an event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md), then follow the steps to [Integrate activity logs with Splunk](tutorial-integrate-activity-logs-with-splunk.md).</span></span>

---

<span data-ttu-id="9e13d-235">**問: 如何整合 Azure AD 活動記錄與 Sumo Logic？**</span><span class="sxs-lookup"><span data-stu-id="9e13d-235">**Q: How do I integrate Azure AD activity logs with Sumo Logic?**</span></span> 

<span data-ttu-id="9e13d-236">**答**: 首先，[將 Azure AD 活動記錄路由至事件中樞](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Collect_Logs_for_Azure_Active_Directory)，然後依照步驟[在 SumoLogic 中安裝 Azure AD 應用程式及檢視儀表板](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Install_the_Azure_Active_Directory_App_and_View_the_Dashboards)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-236">**A**: First, [route the Azure AD activity logs to an event hub](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Collect_Logs_for_Azure_Active_Directory), then follow the steps to [Install the Azure AD application and view the dashboards in SumoLogic](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Install_the_Azure_Active_Directory_App_and_View_the_Dashboards).</span></span>

---

<span data-ttu-id="9e13d-237">**問: 是否可在不使用外部 SIEM 工具的情況下從事件中樞存取資料？**</span><span class="sxs-lookup"><span data-stu-id="9e13d-237">**Q: Can I access the data from an event hub without using an external SIEM tool?**</span></span> 

<span data-ttu-id="9e13d-238">**答**: 是。</span><span class="sxs-lookup"><span data-stu-id="9e13d-238">**A**: Yes.</span></span> <span data-ttu-id="9e13d-239">若要從自訂應用程式存取記錄，您可以使用[事件中樞 API](../../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)。</span><span class="sxs-lookup"><span data-stu-id="9e13d-239">To access the logs from your custom application, you can use the [Event Hubs API](../../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md).</span></span> 

---


## <a name="next-steps"></a><span data-ttu-id="9e13d-240">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e13d-240">Next steps</span></span>

* [<span data-ttu-id="9e13d-241">將活動記錄封存至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="9e13d-241">Archive activity logs to a storage account</span></span>](quickstart-azure-monitor-route-logs-to-storage-account.md)
* [<span data-ttu-id="9e13d-242">將活動記錄路由至事件中樞</span><span class="sxs-lookup"><span data-stu-id="9e13d-242">Route activity logs to an event hub</span></span>](quickstart-azure-monitor-stream-logs-to-event-hub.md)
* [<span data-ttu-id="9e13d-243">深入了解 Azure 診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="9e13d-243">Read more about Azure Diagnostic Logs</span></span>](../../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)