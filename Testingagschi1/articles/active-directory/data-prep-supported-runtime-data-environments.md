---
title: 用于 Azure 机器学习数据准备的执行和数据环境的支持组合 | Microsoft Docs
description: 本文档提供了 Azure 机器学习数据准备支持的不同运行时和数据源组合的完整列表
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.custom: ''
ms.devlang: ''
ms.topic: article
ms.date: 02/01/2018
ms.openlocfilehash: bdd1c51c915787d9e9522f6691ae0ff06d546484
ms.sourcegitcommit: a0be2dc237d30b7f79914e8adfb85299571374ec
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2018
---
# <a name="supported-matrix-for-this-release"></a><span data-ttu-id="3e774-103">针对此版本的支持矩阵</span><span class="sxs-lookup"><span data-stu-id="3e774-103">Supported matrix for this release</span></span> 
<span data-ttu-id="3e774-104">如果获取任一 Pandas 或 Spark 数据帧，那么当代码使用 Azure 机器学习数据源或 Azure 机器学习数据准备加载数据时，以下试验计算环境和数据位置的组合将受到支持：</span><span class="sxs-lookup"><span data-stu-id="3e774-104">When your code loads data by using Azure Machine Learning Data Sources or Azure Machine Learning Data Preparations, getting either a Pandas or Spark dataframe, the following combinations of experiment compute environments and data locations are supported:</span></span>

|     |<span data-ttu-id="3e774-105">本地文件</span><span class="sxs-lookup"><span data-stu-id="3e774-105">Local files</span></span>  |<span data-ttu-id="3e774-106">Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="3e774-106">Azure Blob storage</span></span>  |<span data-ttu-id="3e774-107">SQL Server 数据库\*\*\*</span><span class="sxs-lookup"><span data-stu-id="3e774-107">SQL Server database\*\*\*</span></span>  |
|---------|---------|---------|---------|---------|
|<span data-ttu-id="3e774-108">本地 Python</span><span class="sxs-lookup"><span data-stu-id="3e774-108">Local Python</span></span>    |     <span data-ttu-id="3e774-109">支持</span><span class="sxs-lookup"><span data-stu-id="3e774-109">Supported</span></span>    |<span data-ttu-id="3e774-110">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-110">Not supported</span></span>         | <span data-ttu-id="3e774-111">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-111">Not supported</span></span>        |         |
|<span data-ttu-id="3e774-112">Docker (Linux VM) Python</span><span class="sxs-lookup"><span data-stu-id="3e774-112">Docker (Linux VM) Python</span></span>     |<span data-ttu-id="3e774-113">仅在项目文件中受支持\*</span><span class="sxs-lookup"><span data-stu-id="3e774-113">Supported in project files only\*</span></span>         | <span data-ttu-id="3e774-114">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-114">Not supported</span></span>        |        <span data-ttu-id="3e774-115">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-115">Not supported</span></span> |         |
|<span data-ttu-id="3e774-116">Docker (Linux VM) PySpark</span><span class="sxs-lookup"><span data-stu-id="3e774-116">Docker (Linux VM) PySpark</span></span>     |<span data-ttu-id="3e774-117">仅在项目文件中受支持\*</span><span class="sxs-lookup"><span data-stu-id="3e774-117">Supported in project files only\*</span></span>     |<span data-ttu-id="3e774-118">支持</span><span class="sxs-lookup"><span data-stu-id="3e774-118">Supported</span></span>         | <span data-ttu-id="3e774-119">支持 \**</span><span class="sxs-lookup"><span data-stu-id="3e774-119">Supported**</span></span>        |         |
|<span data-ttu-id="3e774-120">Azure 数据科学虚拟机 Python</span><span class="sxs-lookup"><span data-stu-id="3e774-120">Azure Data Science Virtual Machine Python</span></span>     |<span data-ttu-id="3e774-121">仅在项目文件中受支持\*</span><span class="sxs-lookup"><span data-stu-id="3e774-121">Supported in project files only\*</span></span>         |<span data-ttu-id="3e774-122">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-122">Not supported</span></span>         |<span data-ttu-id="3e774-123">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-123">Not supported</span></span>         |         |
|<span data-ttu-id="3e774-124">Azure 数据科学虚拟机 PySPark</span><span class="sxs-lookup"><span data-stu-id="3e774-124">Azure Data Science Virtual Machine PySPark</span></span>     | <span data-ttu-id="3e774-125">仅在项目文件中受支持\*</span><span class="sxs-lookup"><span data-stu-id="3e774-125">Supported in project files only\*</span></span>        |<span data-ttu-id="3e774-126">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-126">Not supported</span></span>         |<span data-ttu-id="3e774-127">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-127">Not supported</span></span>         |         |
|<span data-ttu-id="3e774-128">Azure HDInsight PySpark</span><span class="sxs-lookup"><span data-stu-id="3e774-128">Azure HDInsight PySpark</span></span>     | <span data-ttu-id="3e774-129">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-129">Not supported</span></span>        |<span data-ttu-id="3e774-130">支持</span><span class="sxs-lookup"><span data-stu-id="3e774-130">Supported</span></span>         |<span data-ttu-id="3e774-131">支持 \**</span><span class="sxs-lookup"><span data-stu-id="3e774-131">Supported**</span></span>         |         |
|<span data-ttu-id="3e774-132">Azure HDInsight Python</span><span class="sxs-lookup"><span data-stu-id="3e774-132">Azure HDInsight Python</span></span>     | <span data-ttu-id="3e774-133">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-133">Not supported</span></span>        | <span data-ttu-id="3e774-134">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-134">Not supported</span></span>        | <span data-ttu-id="3e774-135">不支持</span><span class="sxs-lookup"><span data-stu-id="3e774-135">Not supported</span></span>        |         |

<span data-ttu-id="3e774-136">目前任何计算目标都不支持 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="3e774-136">Azure Data Lake Store is not currently supported for any compute target.</span></span>

<span data-ttu-id="3e774-137">\*使用本地文件路径时，项目中的文件会被复制到计算环境中，然后在该环境中读取。</span><span class="sxs-lookup"><span data-stu-id="3e774-137">\*When local file paths are used, files within the project are copied into the compute environment and then read there.</span></span> <span data-ttu-id="3e774-138">不会复制项目之外的文件，并且路径将不会在计算环境中解析。</span><span class="sxs-lookup"><span data-stu-id="3e774-138">Files outside the project are not copied, and the paths will no longer resolve in the compute environment.</span></span> <span data-ttu-id="3e774-139">请考虑使用数据源替换，以便在本地运行时代码可以使用本地文件。</span><span class="sxs-lookup"><span data-stu-id="3e774-139">Consider using Data Source Substitution so that your code can use a local file when running locally.</span></span> <span data-ttu-id="3e774-140">然后针对不同运行配置切换到 Azure 存储 Blob。</span><span class="sxs-lookup"><span data-stu-id="3e774-140">Then switch to an Azure Storage blob for a different run configuration.</span></span> <span data-ttu-id="3e774-141">还可以在数据源上使用采样支持，只在某些运行配置中管理大型数据的运行。</span><span class="sxs-lookup"><span data-stu-id="3e774-141">You also can use sampling support on data sources to manage runs on large data only in certain run configurations.</span></span>

<span data-ttu-id="3e774-142">\** 使用 Maven JDBC SQL Server 驱动程序 6.2.1.</span><span class="sxs-lookup"><span data-stu-id="3e774-142">**Uses Maven JDBC SQL Server driver 6.2.1.</span></span> <span data-ttu-id="3e774-143">必须确保此包（或一个兼容包）包含在计算环境的 spark_dependencies.yml 文件中。</span><span class="sxs-lookup"><span data-stu-id="3e774-143">You must ensure that this package (or a compatible one) is included in your spark_dependencies.yml file for the compute environment.</span></span>

<span data-ttu-id="3e774-144">\*\*\*如果可从计算环境访问数据库，则支持 Azure SQL 数据库或 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="3e774-144">\*\*\*Supports Azure SQL Database or SQL Server provided the database can be reached from the compute environment.</span></span> 
