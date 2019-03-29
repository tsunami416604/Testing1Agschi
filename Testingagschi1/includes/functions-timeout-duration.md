---
title: bestand opnemen
description: bestand opnemen
services: functions
author: nzthiago
ms.service: azure-functions
ms.topic: include
ms.date: 02/21/2018
ms.author: nzthiago
ms.custom: include file
ms.openlocfilehash: ffb29fc76313e8870b52cb0a63936da7853ea6ce
ms.sourcegitcommit: 8a59b051b283a72765e7d9ac9dd0586f37018d30
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/20/2019
ms.locfileid: "58305072"
---
## <a name="timeout"></a><span data-ttu-id="c83fa-103">Duur van functie-app-time-out</span><span class="sxs-lookup"><span data-stu-id="c83fa-103">Function app timeout duration</span></span> 

<span data-ttu-id="c83fa-104">De duur van de time-out van een functie-app wordt gedefinieerd door de eigenschap functionTimeout in de [host.json](../articles/azure-functions/functions-host-json.md#functiontimeout) projectbestand.</span><span class="sxs-lookup"><span data-stu-id="c83fa-104">The timeout duration of a function app is defined by the functionTimeout property in the [host.json](../articles/azure-functions/functions-host-json.md#functiontimeout) project file.</span></span> <span data-ttu-id="c83fa-105">De volgende tabel ziet u de standaard- en maximale waarden in minuten voor beide abonnementen en beide runtimeversies:</span><span class="sxs-lookup"><span data-stu-id="c83fa-105">The following table shows the default and maximum values in minutes for both plans and in both runtime versions:</span></span>

| <span data-ttu-id="c83fa-106">Plannen</span><span class="sxs-lookup"><span data-stu-id="c83fa-106">Plan</span></span> | <span data-ttu-id="c83fa-107">Runtime-versie</span><span class="sxs-lookup"><span data-stu-id="c83fa-107">Runtime Version</span></span> | <span data-ttu-id="c83fa-108">Standaard</span><span class="sxs-lookup"><span data-stu-id="c83fa-108">Default</span></span> | <span data-ttu-id="c83fa-109">Maximum</span><span class="sxs-lookup"><span data-stu-id="c83fa-109">Maximum</span></span> |
|------|---------|---------|---------|
| <span data-ttu-id="c83fa-110">Verbruik</span><span class="sxs-lookup"><span data-stu-id="c83fa-110">Consumption</span></span> | <span data-ttu-id="c83fa-111">1.x</span><span class="sxs-lookup"><span data-stu-id="c83fa-111">1.x</span></span> | <span data-ttu-id="c83fa-112">5</span><span class="sxs-lookup"><span data-stu-id="c83fa-112">5</span></span> | <span data-ttu-id="c83fa-113">10</span><span class="sxs-lookup"><span data-stu-id="c83fa-113">10</span></span> |
| <span data-ttu-id="c83fa-114">Verbruik</span><span class="sxs-lookup"><span data-stu-id="c83fa-114">Consumption</span></span> | <span data-ttu-id="c83fa-115">2.x</span><span class="sxs-lookup"><span data-stu-id="c83fa-115">2.x</span></span> | <span data-ttu-id="c83fa-116">5</span><span class="sxs-lookup"><span data-stu-id="c83fa-116">5</span></span> | <span data-ttu-id="c83fa-117">10</span><span class="sxs-lookup"><span data-stu-id="c83fa-117">10</span></span> |
| <span data-ttu-id="c83fa-118">App Service</span><span class="sxs-lookup"><span data-stu-id="c83fa-118">App Service</span></span> | <span data-ttu-id="c83fa-119">1.x</span><span class="sxs-lookup"><span data-stu-id="c83fa-119">1.x</span></span> | <span data-ttu-id="c83fa-120">Onbeperkt</span><span class="sxs-lookup"><span data-stu-id="c83fa-120">Unlimited</span></span> | <span data-ttu-id="c83fa-121">Onbeperkt</span><span class="sxs-lookup"><span data-stu-id="c83fa-121">Unlimited</span></span> |
| <span data-ttu-id="c83fa-122">App Service</span><span class="sxs-lookup"><span data-stu-id="c83fa-122">App Service</span></span> | <span data-ttu-id="c83fa-123">2.x</span><span class="sxs-lookup"><span data-stu-id="c83fa-123">2.x</span></span> | <span data-ttu-id="c83fa-124">30</span><span class="sxs-lookup"><span data-stu-id="c83fa-124">30</span></span> | <span data-ttu-id="c83fa-125">Onbeperkt</span><span class="sxs-lookup"><span data-stu-id="c83fa-125">Unlimited</span></span> |

> [!NOTE] 
> <span data-ttu-id="c83fa-126">230 seconden is, ongeacht de instelling van de time-out in de functie-app, de maximale hoeveelheid tijd die een door HTTP geactiveerde functie nemen kunt om te reageren op een aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c83fa-126">Regardless of the function app timeout setting, 230 seconds is the maximum amount of time that an HTTP triggered function can take to respond to a request.</span></span> <span data-ttu-id="c83fa-127">Dit is vanwege de [time-out voor inactiviteit van Azure Load Balancer standaard](../articles/app-service/faq-availability-performance-application-issues.md#why-does-my-request-time-out-after-230-seconds).</span><span class="sxs-lookup"><span data-stu-id="c83fa-127">This is because of the [default idle timeout of Azure Load Balancer](../articles/app-service/faq-availability-performance-application-issues.md#why-does-my-request-time-out-after-230-seconds).</span></span> <span data-ttu-id="c83fa-128">Voor langere verwerkingstijden, kunt u overwegen de [duurzame functies asynchrone patroon](../articles/azure-functions/durable/durable-functions-concepts.md#async-http) of [het echte werk uitstellen en direct een reactie terug](../articles/azure-functions/functions-best-practices.md#avoid-long-running-functions).</span><span class="sxs-lookup"><span data-stu-id="c83fa-128">For longer processing times, consider using the [Durable Functions async pattern](../articles/azure-functions/durable/durable-functions-concepts.md#async-http) or [defer the actual work and return an immediate response](../articles/azure-functions/functions-best-practices.md#avoid-long-running-functions).</span></span>
