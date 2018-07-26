---
title: Creazione di un'applicazione accessibile con Mappe di Azure | Microsoft Docs
description: Come compilare un'applicazione accessibile con Mappe di Azure
services: azure-maps
keywords: ''
author: chgennar
ms.author: chgennar
ms.date: 05/18/2018
ms.topic: article
ms.service: azure-maps
documentationcenter: ''
manager: timlt
ms.devlang: na
ms.openlocfilehash: 537a8c80dc0d1fcb2f536d0e30200de19a2111a4
ms.sourcegitcommit: ab3b2482704758ed13cccafcf24345e833ceaff3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2018
ms.locfileid: "37867053"
---
# <a name="building-an-accessible-application"></a><span data-ttu-id="7227a-103">Compilazione di un'applicazione accessibile</span><span class="sxs-lookup"><span data-stu-id="7227a-103">Building an accessible application</span></span>

<span data-ttu-id="7227a-104">Questo articolo illustra come compilare un'applicazione per le mappe che può essere usata da un'utilità per la lettura dello schermo.</span><span class="sxs-lookup"><span data-stu-id="7227a-104">This article shows you how to build a map application that can be used by a screen reader.</span></span>

## <a name="understand-the-code"></a><span data-ttu-id="7227a-105">Informazioni sul codice</span><span class="sxs-lookup"><span data-stu-id="7227a-105">Understand the code</span></span>

<iframe height='500' scrolling='no' title='Creare un'applicazione accessibile' src='//codepen.io/azuremaps/embed/ZoVyZQ/?height=504&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>Vedere l'elemento Pen <a href='https://codepen.io/azuremaps/pen/ZoVyZQ/'>Creare un'applicazione accessibile</a> (Creare un'applicazione accessibile) di Mappe di Azure (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) in <a href='https://codepen.io'>CodePen</a>.
</iframe>

<span data-ttu-id="7227a-108">La mappa viene precompilata con alcune funzionalità di accessibilità.</span><span class="sxs-lookup"><span data-stu-id="7227a-108">The map is prebuilt with some accessibility features.</span></span> <span data-ttu-id="7227a-109">Un utente può spostarsi nella mappa usando la tastiera e, se è in esecuzione un'utilità per la lettura dello schermo, la mappa notificherà all'utente le modifiche dello stato.</span><span class="sxs-lookup"><span data-stu-id="7227a-109">A user can navigate the map using the keyboard and if a screen reader is running, the map will notify the user of changes to its state.</span></span> <span data-ttu-id="7227a-110">L'utente, ad esempio, riceverà una notifica relativa alla nuova latitudine, longitudine, zoom e località quando viene fatta una panoramica o lo zoom della mappa.</span><span class="sxs-lookup"><span data-stu-id="7227a-110">For example, the user will be notified of the map's new latitude, longitude, zoom and locality when the map is panned or zoomed.</span></span> <span data-ttu-id="7227a-111">A eventuali informazioni aggiuntive inserite nella mappa di base devono corrispondere informazioni testuali per gli utenti dell'utilità di lettura dello schermo.</span><span class="sxs-lookup"><span data-stu-id="7227a-111">Any additional information that is placed on the base map should have corresponding textual information for screen reader users.</span></span> <span data-ttu-id="7227a-112">A questo scopo, è possibile usare [Popup](https://docs.microsoft.com/javascript/api/azure-maps-javascript/popup?view=azure-iot-typescript-latest).</span><span class="sxs-lookup"><span data-stu-id="7227a-112">Using [Popup](https://docs.microsoft.com/javascript/api/azure-maps-javascript/popup?view=azure-iot-typescript-latest) is one way to achieve this.</span></span> <span data-ttu-id="7227a-113">Nell'esempio di ricerca precedente viene aggiunto alla mappa un popup con informazioni testuali per ogni segnaposto inserito nella mappa.</span><span class="sxs-lookup"><span data-stu-id="7227a-113">In the above search example, a popup with textual information is added to the map for every pin that is placed on the map.</span></span> <span data-ttu-id="7227a-114">Il metodo attach di [Popup](https://docs.microsoft.com/javascript/api/azure-maps-javascript/popup?view=azure-iot-typescript-latest) consente al popup di essere individuato da un'utilità di lettura dello schermo senza visualizzare il popup nella mappa.</span><span class="sxs-lookup"><span data-stu-id="7227a-114">Using the [Popup's](https://docs.microsoft.com/javascript/api/azure-maps-javascript/popup?view=azure-iot-typescript-latest) attach method allows the popup to be seen by a screen reader without visually displaying the popup on the map.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7227a-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7227a-115">Next steps</span></span>

<span data-ttu-id="7227a-116">Per altre informazioni sulla classe Popup e sui metodi usati in questo articolo, vedere:</span><span class="sxs-lookup"><span data-stu-id="7227a-116">Learn more about the Popup class and its methods used in this article:</span></span>

* [<span data-ttu-id="7227a-117">Popup</span><span class="sxs-lookup"><span data-stu-id="7227a-117">Popup</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-javascript/popup?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="7227a-118">attach</span><span class="sxs-lookup"><span data-stu-id="7227a-118">attach</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-javascript/popup?view=azure-iot-typescript-latest#attach)
    * [<span data-ttu-id="7227a-119">remove</span><span class="sxs-lookup"><span data-stu-id="7227a-119">remove</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-javascript/popup?view=azure-iot-typescript-latest#remove)
    * [<span data-ttu-id="7227a-120">open</span><span class="sxs-lookup"><span data-stu-id="7227a-120">open</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-javascript/popup?view=azure-iot-typescript-latest#open)
    * [<span data-ttu-id="7227a-121">close</span><span class="sxs-lookup"><span data-stu-id="7227a-121">close</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-javascript/popup?view=azure-iot-typescript-latest#close)

<span data-ttu-id="7227a-122">Per altri scenari di mapping, vedere la [pagina dell'esempio di codice](http://aka.ms/AzureMapsSamples).</span><span class="sxs-lookup"><span data-stu-id="7227a-122">Check out our [code sample page](http://aka.ms/AzureMapsSamples) for more mapping scenarios.</span></span>