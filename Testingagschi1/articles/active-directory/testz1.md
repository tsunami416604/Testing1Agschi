---
title: What's new and release notes
description: Outlines important changes and features in this and previous versions.
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 09/25/2017
ms.topic: article
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: kartikk
ms.suite: ems
---

# <a name="whats-new-and-release-notes"></a><span data-ttu-id="4306a-104">새로운 기능 및 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="4306a-104">What's new and Release notes</span></span>

## <a name="whats-new"></a><span data-ttu-id="4306a-105">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="4306a-105">What's new</span></span>

<span data-ttu-id="4306a-106">이 항목에서는 새로운 버전의 RMS SDK v4.x에 포함된 중요한 변경 내용과 기능을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-106">This topic outlines important changes and features in this new version of the RMS  SDK v4.x.</span></span>

-   [<span data-ttu-id="4306a-107">2017년 7월의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="4306a-107">New for July 2017</span></span>](#new-for-july-2017)
-   [<span data-ttu-id="4306a-108">2016년 10월 업데이트</span><span class="sxs-lookup"><span data-stu-id="4306a-108">October 2016 update</span></span>](#October-2016-update)
-   [<span data-ttu-id="4306a-109">2016년 6월 업데이트</span><span class="sxs-lookup"><span data-stu-id="4306a-109">June 2016 update</span></span>](#new-for-June-2016)
-   [<span data-ttu-id="4306a-110">2015년 12월 업데이트</span><span class="sxs-lookup"><span data-stu-id="4306a-110">December 2015 update</span></span>](#december-2015-update)
-   [<span data-ttu-id="4306a-111">2015년 7월 업데이트 - Linux/C++ 개발에 대한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="4306a-111">July 2015 update - Adds support for Linux / C++ development</span></span>](#july-2015-update-adds-support-for-linux-c-developm)
-   [<span data-ttu-id="4306a-112">2015년 5월 업데이트 - 로깅 제어 추가</span><span class="sxs-lookup"><span data-stu-id="4306a-112">May 2015 update - Adds logging control</span></span>](#may-2015-update-adds-logging-control)
-   [<span data-ttu-id="4306a-113">2015년 2월 업데이트 - Windows 스토어 응용 프로그램 지원 추가</span><span class="sxs-lookup"><span data-stu-id="4306a-113">February 2015 update - Adds Windows Store application support</span></span>](#february-2015-update-adds-windows-store-application-support)
-   [<span data-ttu-id="4306a-114">2015년 1월 업데이트 - WinPhone 플랫폼 지원 추가</span><span class="sxs-lookup"><span data-stu-id="4306a-114">January 2015 Update - Adds WinPhone platform support</span></span>](#january-2015-update-adds-winphone-platform-support)
-   [<span data-ttu-id="4306a-115">2014년 10월 업데이트 - Microsoft RMS SDK 4.1로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="4306a-115">October 2014 update - Upgrade to Microsoft RMS SDK 4.1</span></span>](#october-2014-update-upgrade-to-microsoft-rms-sdk-4-1)
-   [<span data-ttu-id="4306a-116">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="4306a-116">Release notes</span></span>](#release-notes)
-   [<span data-ttu-id="4306a-117">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="4306a-117">Frequently asked questions</span></span>](#frequently-asked-questions)

### <a name="new-for-july-2017"></a><span data-ttu-id="4306a-118">2017년 7월의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="4306a-118">New for July 2017</span></span>

<span data-ttu-id="4306a-119">7월 릴리스에 대한 업데이트에는 SDK의 버전이 4.2.5로 증가했습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-119">The update for our July release included incrementing the revision of the SDK, now 4.2.5.</span></span>

- <span data-ttu-id="4306a-120">Android SDK: 이제 Android SDK를 사용하여 앱에서 **로깅 레벨을 즉시 설정**할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-120">Android SDK: Your app can now **set the logging level on-the-fly** with the Android SDK.</span></span> <span data-ttu-id="4306a-121">자세한 내용은 [방법: 오류 및 성능 로깅 사용](https://docs.microsoft.com/en-us/information-protection/develop/enabling-logging)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4306a-121">For more information, see [How to: Enable error and performance logging](https://docs.microsoft.com/en-us/information-protection/develop/enabling-logging)</span></span>
- <span data-ttu-id="4306a-122">iOS SDK는 로깅 수준을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-122">The iOS SDK does not support logging level.</span></span> 
- <span data-ttu-id="4306a-123">이제 SDK가 NULL 액세스 토큰에 대한 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-123">The SDK now returns an error for a NULL access token.</span></span>

### <a name="october-2016-update"></a><span data-ttu-id="4306a-124">2016년 10월 업데이트</span><span class="sxs-lookup"><span data-stu-id="4306a-124">October 2016 update</span></span>

- <span data-ttu-id="4306a-125">몇 가지 백 엔드 버그 수정을 구현.</span><span class="sxs-lookup"><span data-stu-id="4306a-125">Implement a few back-end bug fixes.</span></span>
- <span data-ttu-id="4306a-126">Apple iOS/OSX SDK의 비트 코드를 사용하도록 설정.</span><span class="sxs-lookup"><span data-stu-id="4306a-126">Enable bitcode for the Apple iOS/OSX SDK.</span></span>

### <a name="june-2016-update"></a><span data-ttu-id="4306a-127">2016년 6월 업데이트</span><span class="sxs-lookup"><span data-stu-id="4306a-127">June 2016 update</span></span>

- <span data-ttu-id="4306a-128">**최신 인증에 대한 지원** - RMS 지원 앱에서 ADAL(Active Directory Authentication Library) 기반 로그인이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-128">**Support for Modern Authentication** - brings Active Directory Authentication Library (ADAL)-based sign-in to RMS enlightened apps.</span></span> <span data-ttu-id="4306a-129">MFA(Multi-Factor @Authentication), SAML 기반 타사 ID 공급자와 RMS 클라이언트 응용 프로그램, 스마트 카드 및 인증서 기반 인증과 같은 로그인 기능이 가능하며, 기본 인증 프로토콜을 사용하기 위해 RMS 지원 앱을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-129">It enables sign-in features like Multi-Factor Authentication (MFA), SAML-based third-party Identity Providers with RMS client applications, smart card, and certificate-based authentication and it removes the need for RMS enlightened apps to use the basic authentication protocol.</span></span>
- <span data-ttu-id="4306a-130">**문서 추적 지원** - 이제 개발자는 앱에서 문서를 보호하는 경우 문서 추적을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-130">**Document Tracking support** - developers can now enable document tracking when protecting document in their apps</span></span>
- <span data-ttu-id="4306a-131">성능 향상</span><span class="sxs-lookup"><span data-stu-id="4306a-131">Performance improvements</span></span>
- <span data-ttu-id="4306a-132">버그 수정</span><span class="sxs-lookup"><span data-stu-id="4306a-132">Bug fixes</span></span>

### <a name="december-2015-update"></a><span data-ttu-id="4306a-133">2015년 12월 업데이트</span><span class="sxs-lookup"><span data-stu-id="4306a-133">December 2015 update</span></span>

<span data-ttu-id="4306a-134">이 릴리스에서는 장치용 RMS SDK가 이제 버전 4.2이며 다음 기능이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-134">With this release, the RMS SDK for devices is now at version 4.2 and adds:</span></span>

-   <span data-ttu-id="4306a-135">iOS/OS X 및 Android 운영 체제에 대한 문서 추적(RMS 온라인에만 해당).</span><span class="sxs-lookup"><span data-stu-id="4306a-135">Document tracking, RMS On-line only, for iOS/OS X and Android operating systems.</span></span>

    <span data-ttu-id="4306a-136">iOS/OS X에 대한 자세한 내용과 사용 지침은 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx)에 대한 추적 정보 및 추가 문서 추적 등록 메서드를 제공하는 [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx) 클래스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4306a-136">For details and usage guidance on iOS/OS X, see the [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx) class, which provides tracking information and the additional document tracking registration method on [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx).</span></span> <span data-ttu-id="4306a-137">[LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) 및 [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx)에는 유사한 Android용 항목이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-137">There are similar additions for Android to [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) and [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx).</span></span>

-   <span data-ttu-id="4306a-139">Android API의 비동기 버전을 병렬화하는 동기 메서드 집합:</span><span class="sxs-lookup"><span data-stu-id="4306a-139">A set of synchronous methods that parallel the asynchronous versions for the Android API:</span></span>

    [<span data-ttu-id="4306a-140">CustomProtectedInputStream.create 동기 메서드</span><span class="sxs-lookup"><span data-stu-id="4306a-140">CustomProtectedInputStream.create synchronous method</span></span>](https://msdn.microsoft.com/library/mt631362.aspx)

    [<span data-ttu-id="4306a-141">CustomProtectedOutputStream.create 동기 메서드</span><span class="sxs-lookup"><span data-stu-id="4306a-141">CustomProtectedOutputStream.create synchronous method</span></span>](https://msdn.microsoft.com/library/mt631363.aspx)

    [<span data-ttu-id="4306a-142">ProtectedFileInputStream.create 동기 메서드</span><span class="sxs-lookup"><span data-stu-id="4306a-142">ProtectedFileInputStream.create synchronous method</span></span>](https://msdn.microsoft.com/library/mt631375.aspx)

    [<span data-ttu-id="4306a-143">ProtectedFileOutputStream.create 동기 메서드</span><span class="sxs-lookup"><span data-stu-id="4306a-143">ProtectedFileOutputStream.create synchronous method</span></span>](https://msdn.microsoft.com/library/mt631376.aspx)

    [<span data-ttu-id="4306a-144">TemplateDescriptor.getTemplates 동기 메서드</span><span class="sxs-lookup"><span data-stu-id="4306a-144">TemplateDescriptor.getTemplates synchronous method</span></span>](https://msdn.microsoft.com/library/mt631380.aspx)

    [<span data-ttu-id="4306a-145">UserPolicy.acquire 동기 메서드</span><span class="sxs-lookup"><span data-stu-id="4306a-145">UserPolicy.acquire synchronous method</span></span>](https://msdn.microsoft.com/library/mt631384.aspx)

    [<span data-ttu-id="4306a-146">UserPolicy.create(PolicyDescriptor...) 동기 메서드** </span><span class="sxs-lookup"><span data-stu-id="4306a-146">UserPolicy.create (PolicyDescriptor…) synchronous method**</span></span>](https://msdn.microsoft.com/library/mt631385.aspx)

    [<span data-ttu-id="4306a-147">UserPolicy.create(TempalteDescriptor...) 동기 메서드</span><span class="sxs-lookup"><span data-stu-id="4306a-147">UserPolicy.create (TempalteDescriptor…) synchronous method</span></span>](https://msdn.microsoft.com/library/mt631386.aspx)

-   <span data-ttu-id="4306a-148">새 [ProtectedBuffer](https://msdn.microsoft.com/library/mt631369.aspx)클래스가 Android API에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-148">A new [ProtectedBuffer](https://msdn.microsoft.com/library/mt631369.aspx) class has been added to the Android API.</span></span>
-   <span data-ttu-id="4306a-149">오류 메시지 및 문제 해결 환경을 개선하기 위한 업데이트</span><span class="sxs-lookup"><span data-stu-id="4306a-149">Updates to improve error messaging and troubleshooting experience.</span></span>
-   <span data-ttu-id="4306a-150">암호화 작업 성능 향상</span><span class="sxs-lookup"><span data-stu-id="4306a-150">Significant performance improvements for cryptographic operations.</span></span>

### <a name="july-2015-update---adds-support-for-linux--c-development"></a><span data-ttu-id="4306a-151">2015년 7월 업데이트 - Linux/C++ 개발에 대한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="4306a-151">July 2015 Update - Adds support for Linux / C++ development</span></span>

<span data-ttu-id="4306a-152">이 릴리스에서는 다음 업데이트가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-152">This release adds the following updates:</span></span>

-   <span data-ttu-id="4306a-153">Linux 플랫폼용 RMS SDK 4.1</span><span class="sxs-lookup"><span data-stu-id="4306a-153">RMS SDK 4.1 for Linux platforms</span></span>

   
### <a name="may-2015-update---adds-logging-control"></a><span data-ttu-id="4306a-155">2015년 5월 업데이트 - 로깅 제어 추가</span><span class="sxs-lookup"><span data-stu-id="4306a-155">May 2015 Update - Adds logging control</span></span>

<span data-ttu-id="4306a-156">이 릴리스에서는 다음 업데이트에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-156">This release adds support for the following updates:</span></span>

-   <span data-ttu-id="4306a-157">iOS</span><span class="sxs-lookup"><span data-stu-id="4306a-157">iOS</span></span>

    <span data-ttu-id="4306a-158">앱 암호화 및 암호 해독이 독립적으로 및 병렬로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-158">App encrypt and decrypt can operate independently and in parallel.</span></span>

    <span data-ttu-id="4306a-159">자세한 내용은 [MSProtector](https://msdn.microsoft.com/library/mt210993.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4306a-159">For more information, see [MSProtector](https://msdn.microsoft.com/library/mt210993.aspx).</span></span>

    <span data-ttu-id="4306a-160">로그 수준 제어 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-160">Log level control settings enabled.</span></span>


    <span data-ttu-id="4306a-162">캐시 지우기 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-162">Cache clearing support added.</span></span>

    <span data-ttu-id="4306a-163">자세한 내용은 [MSProtection:resetStateWithCompletionBlock](https://msdn.microsoft.com/library/mt210991.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4306a-163">For more information, see [MSProtection:resetStateWithCompletionBlock](https://msdn.microsoft.com/library/mt210991.aspx).</span></span>

### <a name="february-2015-update---adds-windows-store-application-support"></a><span data-ttu-id="4306a-164">2015년 2월 업데이트 - Windows 스토어 응용 프로그램 지원 추가</span><span class="sxs-lookup"><span data-stu-id="4306a-164">February 2015 Update - Adds Windows Store application support</span></span>

<span data-ttu-id="4306a-165">이 릴리스에서는 Windows 스토어 응용 프로그램에 대한 지원이 추가되었으며 Windows Phone, Android 및 iOS/OS X 릴리스의 RMS SDK 4.1과 기능 패리티를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-165">This release adds support for Windows Store applications and provides functional parity with the Windows Phone, Android, and iOS/OS X release of the RMS SDK 4.1.</span></span>

### <a name="january-2015-update---adds-winphone-platform-support"></a><span data-ttu-id="4306a-166">2015년 1월 업데이트 - WinPhone 플랫폼 지원 추가</span><span class="sxs-lookup"><span data-stu-id="4306a-166">January 2015 Update - Adds WinPhone platform support</span></span>

<span data-ttu-id="4306a-167">이 릴리스에서는 Windows Phone 운영 체제에 대한 지원이 추가되었으며 Android 및 iOS/OS X 릴리스의 RMS SDK 4.1과 기능 패리티를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-167">This release adds support for the Windows Phone operating system and provides functional parity with the Android and iOS/OS X release of the RMS SDK 4.1.</span></span>

### <a name="october-2014-update---upgrade-to-microsoft-rms-sdk-41"></a><span data-ttu-id="4306a-168">2014년 10월 업데이트 - Microsoft RMS SDK 4.1로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="4306a-168">October 2014 Update - Upgrade to Microsoft RMS SDK 4.1</span></span>

<span data-ttu-id="4306a-169">버전 4.1 릴리스의 RMS SDK에서는 Google Android 및 Apple iOS/OS X에 에는 다음과 같은 새로운 기능이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-169">The version 4.1 release of the RMS SDK adds the following new features to the Google Android and Apple iOS / OS X.</span></span>

-   <span data-ttu-id="4306a-170">SDK 동작의 사용자 확인을 허용하는 *사용자 동의* 처리를 위한 Android 및 iOS/OS X SDK API 확장.</span><span class="sxs-lookup"><span data-stu-id="4306a-170">Android and iOS/OS X SDK API extensions for *user consent* processing, allowing user confirmation of SDK behaviors.</span></span> <span data-ttu-id="4306a-171">현재 지원되는 동의 형식은 문서 추적 및 알 수 없는 AD RMS 서비스 URL 액세스입니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-171">Currently, document tracking and accessing unknown AD RMS service URLs are the supported consent types.</span></span>

    <span data-ttu-id="4306a-172">자세한 내용을 보려면 Android API 버전의 [ConsentCallback interface](https://msdn.microsoft.com/library/dn833503.aspx)(ConsentCallback 인터페이스)를 예제로 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4306a-172">For more information, see as example, the Android API version of [ConsentCallback interface](https://msdn.microsoft.com/library/dn833503.aspx).</span></span>

-   <span data-ttu-id="4306a-173">이제 iOS 8 및 OS X 10.10(Yosemite)이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-173">iOS 8 and OS X 10.10 (Yosemite) are now supported.</span></span> <span data-ttu-id="4306a-174">또한 Xcode 6에 필요한 몇 가지 속성 이름 변경이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-174">There have also been a few property name changes required by Xcode 6.</span></span>

    <span data-ttu-id="4306a-175">예를 들어 MSUserPolicy.name이 [MSUserPolicy.policyName](https://msdn.microsoft.com/library/dn790799.aspx)으로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-175">Example; MSUserPolicy.name changed to [MSUserPolicy.policyName](https://msdn.microsoft.com/library/dn790799.aspx).</span></span>

## <a name="release-notes"></a><span data-ttu-id="4306a-176">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="4306a-176">Release notes</span></span>

<span data-ttu-id="4306a-177">이 섹션에서는 개발자가 알고자 하는 현재 및 이전 릴리스의 Microsoft Rights Management SDK 4.x API에 대한 정보를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-177">This section outlines information about the current and previous releases of the Microsoft Rights Management SDK 4.x APIs that you, as a developer, want to be aware of.</span></span>

<span data-ttu-id="4306a-178">**AD RMS SDK 4.1 - iOS/OS X 및 Android 플랫폼 글로벌 가용성 릴리스**</span><span class="sxs-lookup"><span data-stu-id="4306a-178">**AD RMS SDK 4.1 - iOS / OS X and Android platforms Global Availability Release**</span></span>

-   <span data-ttu-id="4306a-179">**AD RMS 지원** - IT 관리자는 모바일 장치에서 새 AD RMS 서버의 모바일 장치 확장과 함께 RMS 사용 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-179">**AD RMS support** - IT administrators can use RMS enabled apps on mobile devices with the new AD RMS server's mobile device extensions.</span></span>
-   <span data-ttu-id="4306a-180">**오프라인 사용** - 최종 사용자는 RMS 보호된 데이터를 오프라인으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-180">**Offline Consumption** - end users can access RMS protected data offline.</span></span>
-   <span data-ttu-id="4306a-181">**분리된 인증** - 개발자는 Azure RMS 및 AD RMS에 대해 고유한 인증 라이브러리를 사용하거나 권장 [Azure ADAL(AD Authentication Library)](https://MSDN.Microsoft.Com/library/jj573266.aspx)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-181">**Segregated Auth** - developers can use their own authentication library for Azure RMS and AD RMS (or use the recommended [Azure AD Authentication Library (ADAL)](https://MSDN.Microsoft.Com/library/jj573266.aspx)).</span></span>
-   <span data-ttu-id="4306a-182">**분리된 UI** - 개발자는 RMS 보호된 문서를 보호하고 사용할 사용자 인터페이스를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-182">**Segregated UI** - developers can build their user interface to protect and consume RMS protected documents.</span></span>
-   <span data-ttu-id="4306a-183">**다시 디자인된 API** – 이제 개발자는 최소한의 노력으로 일관된 RMS 동작과 사용자 환경을 제공하는 간단하고 투명한 암호화 및 암호 해독 API를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-183">**Redesigned API** - developers can now enjoy a straightforward and transparent encryption and decryption API, which provides consistent RMS behaviors and user experience, with minimum effort.</span></span>

<span data-ttu-id="4306a-184">**모든 플랫폼에 공통적으로 적용**</span><span class="sxs-lookup"><span data-stu-id="4306a-184">**Common to all platforms**</span></span>

-   <span data-ttu-id="4306a-185">RMS SDK 4.x API는 *스레드로부터 안전*하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-185">The RMS SDK 4.x APIs are not *thread-safe*.</span></span>

<span data-ttu-id="4306a-186">**OWA(Outlook Web Access)**</span><span class="sxs-lookup"><span data-stu-id="4306a-186">**Android**</span></span>

-   <span data-ttu-id="4306a-187">Amazon® Kindle 장치에서 샘플 앱을 사용하여 .ptxt 첨부 파일을 보는 경우 파일을 보기 전에 먼저 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-187">When you use a sample app on an Amazon® Kindle device to view .ptxt attachments, you must first download the file before you view it.</span></span>

    <span data-ttu-id="4306a-188">**해결 방법** - 알려진 문제이며 나중에 다룰 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-188">**Solution** - a known issue that will be addressed later.</span></span>

-   <span data-ttu-id="4306a-189">다중 인스턴스가 허용되는 경우 SDK를 사용하는 응용 프로그램이 충돌할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-189">An application that uses the SDK may crash if multi-instance is allowed.</span></span>

    <span data-ttu-id="4306a-190">**해결 방법** - 응용 프로그램에서 Android API에 대한 다중 인스턴스 호출을 허용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-190">**Solution** - Make sure the application does not allow multi-instance calls to the Android API.</span></span>

-   <span data-ttu-id="4306a-191">[ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array, int offset, int length) 메서드를 *array.length* 값과 다른 길이로 사용하는 경우 나중에 SDK를 통해 콘텐츠를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-191">When I use the [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write( byte\[\] array, int offset, int length ) method with a length different from the *array.length* value, I am not able to consume the content later using the SDK.</span></span>

    <span data-ttu-id="4306a-192">**해결 방법** - 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-192">**Solution** - This is a known issue.</span></span> <span data-ttu-id="4306a-193">문제를 완화하려면 항상 *byte \[\]* 배열을 length 매개 변수와 동일한 길이 값으로 전달하거나, [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array) 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-193">To mitigate it, either always pass a *byte \[\]* array with the same length value as the length parameter, or use the [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array) method.</span></span>

<span data-ttu-id="4306a-194">**iOS 및 OS X**</span><span class="sxs-lookup"><span data-stu-id="4306a-194">**iOS and OS X**</span></span>

-   <span data-ttu-id="4306a-195">iOS 및 OS X SDK에서 지원하는 두 가지 포르투갈어 언어가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-195">There are two dialects of Portuguese that our iOS and OS X SDKs support.</span></span> <span data-ttu-id="4306a-196">버그로 인해 현재 첫 번째 지역화가 완전히 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-196">Unfortunately, due to a bug, we do not currently support the first localization completely.</span></span> <span data-ttu-id="4306a-197">이 버그 때문에 포르투갈어는 완전히 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-197">Because of this bug, Portuguese is not fully supported.</span></span> <span data-ttu-id="4306a-198">대부분의 텍스트가 번역되었지만 UI는 번역되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-198">Most of the text is translated, but not the UI.</span></span>

    1. <span data-ttu-id="4306a-199">포르투갈어</span><span class="sxs-lookup"><span data-stu-id="4306a-199">Portuguese</span></span>

    2. <span data-ttu-id="4306a-200">포르투갈어(포르투갈)</span><span class="sxs-lookup"><span data-stu-id="4306a-200">Portuguese (Portugal)</span></span>

<span data-ttu-id="4306a-201">**iOS에만 해당**</span><span class="sxs-lookup"><span data-stu-id="4306a-201">**iOS only**</span></span>

-   <span data-ttu-id="4306a-202">RMS SDK 4.x에서는 네트워크 활동 표시기를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-202">The RMS SDK 4.x does not show the network activity indicator.</span></span>

    <span data-ttu-id="4306a-203">이는 Apple Human Interface Guidelines에 따른 iOS에 대해 알려진 선택적 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-203">This is a known optional behavior for iOS according to the Apple Human Interface Guidelines.</span></span>

<span data-ttu-id="4306a-204">**OS X에만 해당**</span><span class="sxs-lookup"><span data-stu-id="4306a-204">**OS X only**</span></span>

-   <span data-ttu-id="4306a-205">RMS SDK 4.x에서는 네트워크 활동 표시기를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-205">The RMS SDK 4.x does not show the network activity indicator.</span></span>

    <span data-ttu-id="4306a-206">이는 Apple Human Interface Guidelines에 따른 OS X에 대해 알려진 선택적 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-206">This is a known optional behavior for OS X according to the Apple Human Interface Guidelines.</span></span>

-   <span data-ttu-id="4306a-207">**해결 방법** - OS X SDK를 사용하여 MDI(다중 문서 인터페이스) 응용 프로그램을 만들려면 다음 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="4306a-207">**Solution** - To create a multiple document interface (MDI) application using our OS X SDK, use the following guidance.</span></span>

    <span data-ttu-id="4306a-208">다음 메서드는 동시에 실행하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-208">The following methods must not be run concurrently.</span></span> <span data-ttu-id="4306a-209">실행 완료를 모니터링하려면 설명된 대로 완료 블록 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-209">In order to monitor for execution completion, use the completion block approach as noted.</span></span>

    - [<span data-ttu-id="4306a-210">MSProtectedData.protectedDataWithProtectedFile</span><span class="sxs-lookup"><span data-stu-id="4306a-210">MSProtectedData.protectedDataWithProtectedFile</span></span>](https://msdn.microsoft.com/library/dn758351.aspx)
    - [<span data-ttu-id="4306a-211">MSCustomProtectedData.customProtectedDataWithPolicy</span><span class="sxs-lookup"><span data-stu-id="4306a-211">MSCustomProtectedData.customProtectedDataWithPolicy</span></span>](https://msdn.microsoft.com/library/dn758315.aspx)



<span data-ttu-id="4306a-212">**참고** MDI 응용 프로그램은 iOS API에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-212">**Note**  MDI applications are not supported by our iOS API.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="4306a-213">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="4306a-213">Frequently asked questions</span></span>

<span data-ttu-id="4306a-214">**모든 플랫폼**</span><span class="sxs-lookup"><span data-stu-id="4306a-214">**All platforms**</span></span>

<span data-ttu-id="4306a-215">**Q**: 보호 워크플로에 **사용자 지정 권한** 선택 UI가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-215">**Q**: I don’t see a **Custom Permissions** selection UI in the protection workflow.</span></span> <span data-ttu-id="4306a-216">그 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="4306a-216">Why?</span></span>

<span data-ttu-id="4306a-217">**A**: 알려진 문제이며 나중에 해결할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-217">**A**: This is a known issue and will be addressed later.</span></span>

<span data-ttu-id="4306a-218">**Q**: SDK와 샘플 응용 프로그램을 사용하기 위해 새 조직 테넌트를 얻으려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="4306a-218">**Q**: How do I get new organizational tenants to try out the SDK and sample applications?</span></span>

<span data-ttu-id="4306a-219">**A**: Azure AD RMS 테스트 조직에 대한 자격 증명을 요청하려면 <rmcstbeta@microsoft.com>으로 메일을 보내십시오.</span><span class="sxs-lookup"><span data-stu-id="4306a-219">**A**: To request credentials for Azure AD RMS test organizations, send email to <rmcstbeta@microsoft.com>.</span></span>

<span data-ttu-id="4306a-220">**Q**: 여기 설명서에 테스트 계층 구조 설명이 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-220">**Q**: I don’t see any test hierarchy discussion here in the documentation.</span></span> <span data-ttu-id="4306a-221">그 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="4306a-221">Why?</span></span>

<span data-ttu-id="4306a-222">**A**: 새 AD RMS SDK에는 테스트 계층 구조 개념이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-222">**A**: There is no test hierarchy concept with the new AD RMS SDKs.</span></span> <span data-ttu-id="4306a-223">항상 프로덕션 계층 구조를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-223">You will always work with the production hierarchy.</span></span>

<span data-ttu-id="4306a-224">**Q**: 2.1 버전의 RMS SDK에서는 정보 보호를 구현하는 각 응용 프로그램에 대해 생성된 매니페스트가 필요했습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-224">**Q**: In the 2.1 version of the RMS SDK, a generated manifest was needed for each application implementing information protection.</span></span> <span data-ttu-id="4306a-225">4.0 이상 버전의 SDK에서도 마찬가지인가요?</span><span class="sxs-lookup"><span data-stu-id="4306a-225">Is this still true for the 4.0 and later versions of the SDK?</span></span>

<span data-ttu-id="4306a-226">**A**: 아니요, 3.0 이상 버전의 권한 관리 SDK에서는 매니페스트가 더 이상 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-226">**A**: No, manifests are no longer needed for the 3.0 and later versions of the Rights Management SDK.</span></span>

<span data-ttu-id="4306a-227">**OWA(Outlook Web Access)**</span><span class="sxs-lookup"><span data-stu-id="4306a-227">**Android**</span></span>

<span data-ttu-id="4306a-228">**Q**: SDK가 테스트된 개발 환경은 무엇인가요.</span><span class="sxs-lookup"><span data-stu-id="4306a-228">**Q**: Which development environments has the SDK been tested with?</span></span>

<span data-ttu-id="4306a-229">**A**: Google API 15 이상을 사용하는 Eclipse Juno입니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-229">**A**: Eclipse Juno using Google API 15 and above.</span></span>

<span data-ttu-id="4306a-230">**Q**: UI 스레드에서 취소 메서드인 cancel()을 호출할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="4306a-230">**Q**: Can I call cancel() a cancel method from the UI thread?</span></span>
<span data-ttu-id="4306a-231">**A**: 네트워크 연결이 중단될 수 있으므로 비 UI 스레드에서 cancel()을 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-231">**A**: You should call cancel() from a non-UI thread, as it may abort network a connection.</span></span>

<span data-ttu-id="4306a-232">**iOS**</span><span class="sxs-lookup"><span data-stu-id="4306a-232">**iOS**</span></span>

<span data-ttu-id="4306a-233">**Q**: SDK 개발에 대해 검증된 플랫폼은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="4306a-233">**Q**: Which platforms were verified for SDK development?</span></span>

<span data-ttu-id="4306a-234">**A**: iOS 7 이상을 사용하는 Xcode 5.0입니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-234">**A**: Xcode 5.0 with iOS 7 and later.</span></span>

<span data-ttu-id="4306a-235">**Q**: 작업에 대해 cancel() 메서드를 호출했는데 작업이 완료되었다는 알림이 표시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-235">**Q**: I called a cancel() method on an operation, however I still got notification that the operation completed.</span></span> <span data-ttu-id="4306a-236">그 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="4306a-236">Why?</span></span>

<span data-ttu-id="4306a-237">**A**: 일부 작업은 취소할 수 없으므로 취소 작업은 가능한 경우에만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-237">**A**: Not all operations can be canceled, so a cancellation operation is executed as best as is possible.</span></span>

<span data-ttu-id="4306a-238">**OS x**</span><span class="sxs-lookup"><span data-stu-id="4306a-238">**OS x**</span></span>

<span data-ttu-id="4306a-239">**Q**: 샘플 앱 프레임워크가 Xcode 5에 맞게 조정되었습니다. Xcode 4.6에서도 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="4306a-239">**Q**: Sample app framework is adapted to Xcode 5, can I work with Xcode 4.6?</span></span>

<span data-ttu-id="4306a-240">**A**: OS X SDK는 Xcode 4.6 이상과 OS X 10.8 이상에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4306a-240">**A**:The OS X SDK works with Xcode 4.6 and later only, as well as OS X 10.8 and later.</span></span>
