﻿---
title: 'ITPro_R4_Stub_80: Exchange 2013 Help'
TOCTitle: ITPro_R4_Stub_80
ms:assetid: 0e701643-1f18-4cc3-8595-4fd4b15caf6c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt846639(v=EXCHG.150)
ms:contentKeyID: 74520281
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ITPro\_R4\_Stub\_80

 

_**適用版本：** Exchange Server 2013_

_**上次修改主題的時間：** 2018-04-19_

**Summary:**  How administrations can deploy hybrid Modern Authentication and Enterprise Mobility + Security features for Exchange on-premises mailboxes to enable support for Outlook for iOS and Android.

The Outlook app for iOS and Android is designed as the best way to experience Office 365 on your mobile device by leveraging Microsoft services to help find, plan, and prioritize your daily life and work. Outlook provides the security, privacy, and support you need while protecting corporate data via capabilities such as Azure Active Directory conditional access and Intune app protection policies. The following sections provide an overview of the hybrid Modern Authentication architecture, the required pre-requisites for its deployment, and how to securely deploy Outlook for iOS and Android for Exchange on-premises mailboxes.

## Microsoft Cloud architecture for hybrid Exchange Server customers

Outlook for iOS and Android is a cloud-backed application. This means your experience consists of a locally installed app powered by a secure and scalable service running in the Microsoft Cloud.

For Exchange Server mailboxes, Outlook for iOS and Android's new architecture is similar in design to its legacy architecture. However, as the service is now built directly into the Microsoft Cloud (using Office 365 and Microsoft Azure) customers receive the additional benefits of security, privacy, built-in compliance, and transparent operations that Microsoft commits to in the [Office 365 Trust Center](https://products.office.com/business/office-365-trust-center-welcome) and [Azure Trust Center](https://www.microsoft.com/trustcenter/cloudservices/azure).

![適用於 iOS 和 Android 之 Outlook 中混合式新式驗證的架構圖表](images/Mt846639.20a7e963-916d-47e0-bffb-4d86c4777bea(EXCHG.150).png "適用於 iOS 和 Android 之 Outlook 中混合式新式驗證的架構圖表")

Data passing from Exchange Online to the Outlook app is passed via a TLS-secured connection. The protocol translator running on Azure serves to route data, commands and notifications, but has no ability to read the data itself.

The Exchange ActiveSync connection between Exchange Online and the on-premises environment enables synchronization of the users' on-premises data and includes four weeks of email, all calendar data, all contact data, and out-of-office status in your Exchange Online tenant. This data will be removed automatically from Exchange Online after 30 days when the account is deleted in Azure Active Directory.

Data synchronization between the on-premises environment and Exchange Online happens independent of user behavior. This ensures that we can send new messages to the devices very quickly.

Processing information in the Microsoft Cloud enables advanced features and capabilities, such as the categorization of email for the Focused Inbox, customized experience for travel and calendar, and improved search speed. Relying on the cloud for intensive processing and minimizing the resources required from users' devices enhances the app's performance and stability. Lastly, it allows Outlook to build features that work across all email accounts, regardless of the technological capabilities of the underlying servers (such as different versions of Exchange Server, or Office 365).

Specifically, this new architecture has the following improvements:

1.  **Enterprise Mobility + Security support:**  Customers can take advantage of Microsoft Enterprise Mobility + Security (EMS) including Microsoft Intune and Azure Active Directory Premium, to enable conditional access and Intune app protection policies, which control and secure corporate messaging data on the mobile device.

2.  **Fully powered by Microsoft Cloud:**  The on-premises mailbox data is synchronized into Exchange Online, which provides the benefits of security, privacy, compliance and transparent operations that Microsoft commits to in the [Office 365 Trust Center](https://products.office.com/business/office-365-trust-center-welcome).

3.  **OAuth protects users' passwords:**  Outlook leverages hybrid Modern Authentication (OAuth) to protect users' credentials. Hybrid Modern Authentication provides Outlook with a secure mechanism to access the Exchange data without ever touching or storing a user’s credentials. At sign in, the user authenticates directly against an identity platform (either Azure Active Directory or an on-premises identity provider like ADFS) and receives an access token in return, which grants Outlook access to the user’s mailbox or files. At no time does the service have access to the user’s password.

4.  **Provides Unique Device IDs:**  Each Outlook connection is uniquely registered in Microsoft Intune and can therefore be managed as a unique connection.

5.  **Unlocks new features on iOS and Android:**  This update enables the Outlook app to take advantage of native Office 365 features that are not supported in Exchange on-premises today, such as leveraging full Exchange Online search and Focused Inbox. These features will only be available when using Outlook for iOS and Android.


> [!NOTE]  
> Device management through the on-premises Exchange Admin Center is not possible. Intune is required to manage mobile devices.




## Data security, access, and auditing controls

With on-premises data being synchronized with Exchange Online, customers have questions about how the data is protected in Exchange Online. The white paper [Encryption in the Microsoft Cloud](http://aka.ms/office365ce) discusses how BitLocker is used for volume-level encryption. Service Encryption with the Customer Key option, as discussed in the white paper, is supported in the Outlook for iOS and Android architecture, but note that the user must have an Office 365 Enterprise E5 license (or the corresponding versions of those plans for Government or Education) to have an encryption policy assigned.

By default, Microsoft engineers have zero standing administrative privileges and zero standing access to customer content in Office 365. The white paper [Office 365 Administrative Access Controls](http://aka.ms/office365aac) discusses personnel screening, background checks, Lockbox and Customer Lockbox, and more.

[ISO Audited Controls on Service Assurance](https://sip.protection.office.com/) documentation provides the status of audited controls from global information security standards and regulations that Office 365 has implemented.

## Connection flow

When Outlook for iOS and Android is enabled with hybrid Modern Authentication, the connection flow is as follows.

![混合式新式驗證中的驗證流程](images/Mt846639.d6e20ddb-cf8e-4154-8a17-95657ef696d1(EXCHG.150).png "混合式新式驗證中的驗證流程")

1.  After the user enters their email address, Outlook for iOS and Android connects to the AutoDetect service. AutoDetect determines the mailbox type by initiating an AutoDiscover query to Exchange Online. Exchange Online determines that the user’s mailbox is on-premises and returns a 302-redirect to AutoDetect with the on-premises Autodiscover URL. AutoDetect initiates a query against the on-premises AutoDiscover service to determine the ActiveSync endpoint for the email address. The URL attempted on-premises is similar to this example: https://autodiscover.contoso.com/autodiscover/autodiscover.json?Email=test%40contoso.com\&Protocol=activesync\&RedirectCount=3.

2.  AutoDetect initiates a connection to the on-premises ActiveSync URL returned in Step 1 above with an empty bearer challenge. The empty bearer challenge tells the on-premises ActiveSync that the client supports Modern Authentication. On-premises ActiveSync responds with a 401-challenge response and includes the *WWW-Authenticate: Bearer* header. Within the WWW-Authenticate: Bearer header is the authorization\_uri value that identifies the Azure Active Directory (AAD) endpoint that should be used to obtain an OAuth token.

3.  AutoDetect returns the AAD endpoint to the client. The client begins the log-in flow and the user is presented with a Web form (or redirected to the Microsoft Authenticator app) and can enter credentials. Depending on the identity configuration, this may or may not involve a federated endpoint redirect to an on-premises identity provider. Ultimately, the client obtains an access-and-refresh token pair, which is named AT1/RT1. This access token is scoped to the Outlook for iOS and Android client with an audience of the Exchange Online endpoint.

4.  Outlook for iOS and Android establishes a connection to the Stateless Protocol Translator where the client’s proprietary device protocol is translated into a protocol that Exchange Online understands.

5.  A provisioning request is passed to Exchange Online which includes the user’s access token (AT1) and the on-premises ActiveSync endpoint.

6.  The MRS provisioning API within Exchange Online utilizes AT1 as input and obtains a second access-and-refresh token pair (named AT2/RT2) to access the on-premises mailbox via an on-behalf-of call to Azure Active Directory. This second access token is scoped with the client being Exchange Online and an audience of the on-premises ActiveSync namespace endpoint.

7.  If the mailbox is not provisioned, then the provisioning API creates a mailbox.

8.  The MRS provisioning API establishes a secure connection to the on-premises ActiveSync endpoint and synchronizes the user’s messaging data using the AT2 access token as the authentication mechanism. RT2 is used periodically to generate a new AT2 so that data can be synchronized in the background without user intervention.

## Technical and licensing requirements

The hybrid Modern Authentication architecture has the following technical requirements:

1.  **Exchange on-premises setup**:
    
      - A minimum cumulative update (CU) deployment on all Exchange servers of Exchange Server 2016 CU8 or Exchange Server 2013 CU19. Note that customers with hybrid deployments in which Exchange is deployed on-premises and in the cloud, or who are using Exchange Online Archiving (EOA) with their on-premises Exchange deployment, are required to deploy the most current CU or one CU prior to the most current.
    
      - All Exchange 2007 or Exchange 2010 servers must be removed from the environment. Exchange Server 2010 SP3 is out of mainstream support and will not work with Intune-managed Outlook for iOS and Android. In this architecture, Outlook for iOS and Android uses OAuth as the authentication mechanism. One of the on-premises configuration changes that occurs enables the OAuth endpoint to the Microsoft Cloud as the default authorization endpoint. When this change is made, clients can start negotiating the use of OAuth. Because this is an organization-wide change, Exchange 2010 mailboxes fronted by either Exchange 2013 or 2016 will incorrectly think they can perform OAuth and will end up in a disconnected state, since Exchange 2010 does not support OAuth as an authentication mechanism.

2.  **Active Directory Synchronization**. Active Directory synchronization of the entire on-premises directory with Azure Active Directory, via Azure AD Connect. You must ensure the following attributes are synchronized:
    
      - Office 365 ProPlus
    
      - Exchange Online
    
      - Exchange Hybrid write-back
    
      - Azure RMS
    
      - Intune

3.  **Exchange hybrid setup:**  Requires full hybrid relationship between Exchange on-premises with Exchange Online.
    
      - Hybrid Office 365 tenant is configured in full hybrid configuration mode and is setup as specified in the [Exchange Deployment Assistant](http://technet.microsoft.com/exdeploy)
    
      - Requires an Office 365 Enterprise, Business, or Education tenant.
    
      - The on-premises mailbox data is synchronized in the same datacenter region where that Office 365 tenant is setup. For more about where Office 365 data is located, visit the [Where is my data?](http://o365datacentermap.azurewebsites.net/) section Office 365 Trust Center.
    
      - Use of Office 365 US Government Community and Defense tenants, Office 365 Germany tenants, and Office 365 China operated by 21Vianet tenants are not supported.
    
      - The external URL host names for Exchange ActiveSync and AutoDiscover must be published as service principals to Azure Active Directory through the Hybrid Configuration Wizard.
    
      - AutoDiscover and Exchange ActiveSync namespaces must be accessible from the Internet and cannot be fronted by a pre-authentication solution.
    
      - Ensure SSL or TLS offloading is not being used between the load balancer and your Exchange servers, as this will affect the use of the OAuth token. SSL and TLS bridging (termination and re-encryption) is supported.

4.  **Intune setup:**  Both cloud-only and hybrid deployments of Intune are supported (MDM for Office 365 is not supported).

5.  **Office 365 licensing\*:**  Each user must have one of the following Office 365 licenses:
    
      - Commercial: Enterprise E3, Enterprise E5, ProPlus, or Business licenses
    
      - Government: U.S. Government Community G3, U.S. Government Community G5
    
      - Education: Office 365 Education E3, Office 365 Education E5
    
    In addition, the licenses must include the Office client applications that are required for Outlook for iOS and Android commercial use.

6.  **EMS licensing\*:**  Each on-premises user must have one of the following licenses:
    
      - Intune standalone + Azure Active Directory Premium standalone
    
      - Enterprise Mobility + Security E3, Enterprise Mobility + Security E5

**\*** Microsoft Secure Productive Enterprise (SPE) includes all licenses necessary for Office 365 and EMS.

## Implementation steps

Enabling support for hybrid Modern Authentication in your organization requires each of the following steps, which are detailed in the following sections:

1.  Create a conditional access policy

2.  Create an Intune app protection policy

3.  Enable hybrid Modern Authentication

4.  Contact Microsoft

## Create a conditional access policy

When an organization decides to standardize how users access Exchange data, using Outlook for iOS and Android as the only email app for end users, they can configure a conditional access policy that blocks other mobile access methods. Outlook for iOS and Android authenticates via the Azure Active Directory identity object and then connects to Exchange Online. Therefore, you will need to create Azure Active Directory conditional access policies to restrict mobile device connectivity to Exchange Online. To do this, you will need two conditional access policies, with each policy targeting all potential users. Details on creating these polices can be found in [Azure Active Directory app-based conditional access](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-mam#exchange-online-policy).

1.  The first policy allows Outlook for iOS and Android, and it blocks OAuth capable Exchange ActiveSync clients from connecting to Exchange Online. See "Step 1 - Configure an Azure AD conditional access policy for Exchange Online."

2.  The second policy prevents Exchange ActiveSync clients leveraging basic authentication from connecting to Exchange Online. See "Step 2 - Configure an Azure AD conditional access policy for Exchange Online with Active Sync (EAS)."

The policies leverage the grant control [Require approved client app](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference), which ensures only Microsoft apps that have integrated the Intune SDK are granted access.


> [!IMPORTANT]  
> To leverage app-based conditional access policies, the Microsoft Authenticator app must be installed on iOS devices. For Android devices, the Intune Company Portal app is leveraged. For more information, see <a href="https://docs.microsoft.com/intune/app-based-conditional-access-intune">App-based conditional access with Intune</a>.




In order to block other mobile device clients (such as the native mail client included in the mobile operating system) from connecting to your on-premises environment (which authenticate via basic authentication against on-premises Active Directory), you have two options:

1.  You can leverage the built-in Exchange mobile device access rules and block all mobile devices from connecting by setting the following in the Exchange Management Shell:
    
    ```powershell
    Set-ActiveSyncOrganizationSettings -DefaultAccessLevel Block
    ```

2.  You can leverage an on-premises conditional access policy within Intune after installing the on-premises Exchange connector. For more information, see [Create a conditional access policy for Exchange on-premises and legacy Exchange Online Dedicated](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).


> [!NOTE]  
> When implementing either of the above on-premises options, be aware that it may impact users connecting to Exchange on their mobile devices.




## Create an Intune app protection policy

After hybrid Modern Authentication is enabled, all on-premises mobile users are able to leverage Outlook for iOS and Android using the Office 365-based architecture. Therefore, it's important to protect corporate data with an Intune app protection policy.

Create Intune app protection policies for both iOS and Android using the steps documented in [How to create and assign app protection policies](https://docs.microsoft.com/intune/app-protection-policies). At a minimum, each policy must include the following:

1.  They include all Microsoft mobile applications, such as Word, Excel, or PowerPoint, as this will ensure that users can access and manipulate corporate data within any Microsoft app in a secure fashion.

2.  They mimic the security features that Exchange provides for mobile devices, including:
    
      - Requiring a PIN for access (which includes Select Type, PIN length, Allow Simple PIN, Allow fingerprint)
    
      - Encrypting app data
    
      - Blocking managed apps from running on "jailbroken" and rooted devices

3.  They are assigned to all users. This ensures that all users are protected, regardless of whether they use Outlook for iOS and Android.

In addition to the above minimum policy requirements, you should consider deploying advanced protection policy settings like **Restrict cut, copy and paste with other apps** to further prevent corporate data leakage. For more information on the available settings, see [Android app protection policy settings in Microsoft Intune](https://docs.microsoft.com/intune/app-protection-policy-settings-android) and [iOS app protection policy settings](https://docs.microsoft.com/intune/app-protection-policy-settings-ios).


> [!IMPORTANT]  
> To apply Intune app protection policies against apps on Android devices that are not enrolled in Intune, the user must also install the Intune Company Portal. For more information, see <a href="https://docs.microsoft.com/en-us/intune/app-protection-enabled-apps-android">What to expect when your Android app is managed by app protection policies</a>.




## Enable hybrid Modern Authentication

If you have not enabled hybrid Modern Authentication, then review and implement the steps outlined in [Hybrid Modern Authentication overview and prerequisites for using it with on-premises Skype for Business and Exchange servers](https://support.office.com/article/hybrid-modern-authentication-overview-and-prerequisites-for-using-it-with-on-premises-skype-for-business-and-exchange-servers-ef753b32-7251-4c9e-b442-1a5aec14e58d?).

If you have already enabled hybrid Modern Authentication to support other versions of Outlook, including Outlook for Mac, for your on-premises users as outlined in [How to configure Exchange Server on-premises to use hybrid Modern Authentication](https://support.office.com/article/how-to-configure-exchange-server-on-premises-to-use-hybrid-modern-authentication-cef3044d-d4cb-4586-8e82-ee97bd3b14ad?), there are only a few additional steps you must take:

1.  Create an Exchange device access allow rule to allow Exchange Online to connect to your on-premises environment using the ActiveSync protocol:
    
        If ((Get-ActiveSyncOrganizationSettings).DefaultAccessLevel -ne "Allow") {New-ActiveSyncDeviceAccessRule -Characteristic DeviceType -QueryString "OutlookService" -AccessLevel Allow}
    
    Note that device management through the on-premises Exchange Admin Center is not possible. Intune is required to manage mobile devices.

2.  Create an Exchange device access rule that prevents users from connecting to the on-premises environment with Outlook for iOS and Android with basic authentication over the Exchange ActiveSync protocol:
    
    ```powershell
    New-ActiveSyncDeviceAccessRule -Characteristic DeviceModel -QueryString "Outlook for iOS and Android" -AccessLevel Block
    ```
    
    > [!NOTE]  
    > Once this rule is created, users who are using Outlook for iOS and Android with Basic authentication will be blocked.


3.  Ensure your EAS maxRequestLength is configured to match your transport configuration’s MaxSendSize/MaxReceiveSize:
    
      - Path: `%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config`
    
      - Property: `maxRequestLength`
    
      - Value: set in KB size (10MB is 10240, for example)

## Contact Microsoft

To enable support of hybrid Modern Authentication for Outlook for iOS and Android, you must contact your Microsoft account team, customer sales and services (CSS) contact, or your technical account manager. You will need to provide all SMTP domains (and UPN domains in the event that your UPN domains don't match the SMTP address). Once the domains are provided and enabled, hybrid Modern Authentication will be supported for on-premises mailboxes using Outlook for iOS and Android.

## Client features that aren't supported

The following features are not supported for on-premises mailboxes using hybrid Modern Authentication with Outlook for iOS and Android.

  - Draft folder and Draft messages synchronization

  - Shared calendar access and Delegate calendar access

  - Cortana Time to Leave

  - Calendar attachments

  - Task management with Microsoft To-Do

## Connection Flow FAQ

**Q:**  My organization has a security policy that requires Internet inbound connections to be restricted to approved IP addresses or FQDNs. Is that possible with this architecture?

**A:**  Microsoft recommends that the on-premises endpoints for AutoDiscover and ActiveSync protocols be opened and accessible from the Internet without any restrictions. In certain situations that may not be possible. For example, if you are in a co-existence period with another MDM solution, you may want to place restrictions on the ActiveSync protocol to prevent users from bypassing the third-party MDM solution while you migrate to Intune and Outlook for iOS and Android. If you must place restrictions on your on-premises firewall or gateway edge devices, Microsoft recommends filtering based on FQDN endpoints. If FQDN endpoints cannot be used, then filter on IP addresses. Make sure the following IP subnets and FQDNs are whitelisted:

  - All Exchange Online URLs and IP subnet ranges as defined in [Office 365 URLs and IP address ranges](https://support.office.com/article/office-365-urls-and-ip-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

  - All Outlook iOS and Android app FQDNs as defined in [Network requests in Office 365 ProPlus and Mobile](https://support.office.com/article/network-requests-in-office-365-proplus-and-mobile-eb73fcd1-ca88-4d02-a74b-2dd3a9f3364d?).

  - All Azure US and EUR datacenter region IP subnets as defined in [Microsoft Azure Datacenter IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653). This is required because the AutoDetect service establishes connections to the on-premises infrastructure, as outlined in Connection flow. Currently, the AutoDetect service does not leverage IP reservations within Azure.

**Q:**  My organization currently uses a third-party MDM solution to control mobile device connectivity. If I expose the Exchange ActiveSync namespace on the Internet, that introduces a way for users to bypass the third-party MDM solution during the co-existence period. How can I prevent this?

**A:**  There are three potential solutions to resolving this issue:

1.  Implement Exchange mobile device access rules to control which devices are approved to connect.

2.  Some third-party MDM solutions integrate with Exchange mobile device access rules, blocking unapproved access, while adding approved devices in the user’s ActiveSyncAllowedDeviceIDs property.

3.  Implement IP restrictions on the Exchange ActiveSync namespace.

**Q:**  Can I leverage Azure ExpressRoute for managing traffic between the Microsoft Cloud and my on-premises environment?

**A:**  Connectivity to the Microsoft Cloud requires Internet connectivity. However, a subset of Office 365 network traffic may be routed over Azure ExpressRoute. For more information, see [Azure ExpressRoute for Office 365](https://support.office.com/article/azure-expressroute-for-office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).

With ExpressRoute, there is no private IP space for ExpressRoute connections, nor can there be “private” DNS resolution. That means that any endpoint your company wants to use over ExpressRoute must resolve in public DNS. If that endpoint resolves to an IP that is contained in the advertised prefixes associated with the ExpressRoute circuit (your company must configure those prefixes in the Azure portal when you enable Microsoft peering on the ExpressRoute connection), then the outbound connection from Exchange Online to your on-premises environment will route through the ExpressRoute circuit. Your company will have to ensure that the return traffic associated with these connections goes through the ExpressRoute circuit (avoiding asymmetric routing).


> [!NOTE]  
> Because your company will be adding the Exchange ActiveSync namespace to the advertised prefixes in the ExpressRoute circuit, the only way to reach the Exchange ActiveSync endpoint will be via the ExpressRoute. In other words, the only mobile device that will be able to connect to on-premises via the ActiveSync namespace will be Outlook for iOS and Android. All other ActiveSync clients (such as mobile devices' native mail clients) will be unable to connect to the on-premises environment as the connection will not be established from the Microsoft Cloud. This is because there can’t be any overlaps of the public IP space advertised to Microsoft on the ExpressRoute circuit and the public IP space advertised on your Internet circuit(s).




**Q:**  Given only four weeks of message data is synchronized to Exchange Online, does this mean that search queries executed in Outlook for iOS and Android cannot return information beyond the data available on the local device?

**A:**  When a search query is performed in Outlook for iOS and Android, items that match the search query are returned if they are located on the device. In addition, the search query is passed to Exchange on-premises via Exchange Online. Exchange on-premises executes the search query against the on-premises mailbox and returns the results to Exchange Online, which relays the results to the client. The on-premises query results are stored in Exchange Online for one day before being deleted.

**Q:**  How do I know that the email account is added correctly in Outlook for iOS and Android?

**A:**  On-premises mailboxes that are added via hybrid Modern Authentication are labelled as **Exchange (Hybrid)** in the account settings in Outlook for iOS and Android, similar to the following example:

![針對混合式新式驗證設定之適用於 iOS 和 Android 帳戶的 Outlook 範例](images/Mt846639.79887a65-e5e1-4501-a274-008393dbb6c9(EXCHG.150).png "針對混合式新式驗證設定之適用於 iOS 和 Android 帳戶的 Outlook 範例")

## Authentication FAQ

**Q:**  What identity configurations are supported with hybrid Modern Authentication and Outlook for iOS and Android?

**A:**  The following identity configurations with Azure Active Directory are supported with hybrid Modern Authentication:

  - Federated Identity with any on-premises identity provider that is supported by Azure Active Directory

  - Password Hash Synchronization via Azure Active Directory Connect

  - Pass-through Authentication via Azure Active Directory Connect

**Q:**  What authentication mechanism is used for Outlook for iOS and Android? Are credentials stored in Office 365?

**A:**  Active Directory Authentication Library (ADAL)-based authentication is what Outlook for iOS and Android uses to access the on-premises mailbox data that is synchronized with Exchange Online. ADAL authentication, used by Office apps on both desktop and mobile devices, involves users signing in directly to Azure Active Directory, which is Office 365’s identity provider, instead of providing credentials to Outlook.

ADAL-based sign in enables OAuth for hybrid Exchange on-premises accounts, and provides Outlook for iOS and Android a secure mechanism to access email without requiring access to user credentials. At sign in, the user authenticates directly with the Microsoft cloud and receives an access token in return. The token grants Outlook for iOS and Android access to the appropriate mailbox. OAuth provides Outlook with a secure mechanism to access Office 365 and the Outlook cloud service without needing or storing a user's credentials.

For more information, see the Office Blog post [New access and security controls for Outlook for iOS and Android](https://blogs.office.com/2015/06/10/new-access-and-security-controls-for-outlook-for-ios-and-android/).

**Q:**  Do Outlook for iOS and Android and other Microsoft Office mobile apps support single sign-on?

**A:**  All Microsoft apps that leverage the Azure Active Directory Authentication Library (ADAL) for authentication support single sign-on. In addition, single sign-on is also supported when the apps are used in conjunction with either the Microsoft Authenticator or Microsoft Company Portal apps.

Tokens can be shared and re-used by other Microsoft apps (such as Word mobile) under the following scenarios:

1.  When the apps are signed by the same signing certificate and use the same service endpoint or audience URL (such as the Office 365 URL). In this case, the token is stored in app shared storage.

2.  When the apps leverage or support single sign-on with a broker app. The tokens are stored within the broker app. Microsoft Authenticator is an example of a broker app. In the broker app scenario, after you attempt to sign in to Outlook for iOS and Android, ADAL will launch the Microsoft Authenticator app, which will make a connection to Azure Active Directory to obtain the token. It will then hold on to the token and re-use it for authentication requests from other apps, for as long as the configured token lifetime allows.

For more information, see [How to enable cross-app SSO on iOS using ADAL](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-sso-ios).

**Q:**  What is the lifetime of the tokens generated and used by the Active Directory Authentication Library (ADAL) in Outlook for iOS and Android?

**A:**  Multiple tokens are generated when an on-premises user authenticates through ADAL-enabled apps like Outlook for iOS and Android, the Authenticator app, or the Company Portal app. The first access-and-refresh token pair is used to access the data that is synchronized into Exchange Online; the second access-and-refresh token pair is used by Exchange Online to access the on-premises mailbox via the Exchange ActiveSync protocol. The access token is used to access the resource (such as Exchange message data), while a refresh token is used to obtain a new access or refresh token pair when the current access token expires.

By default, the access token lifetime is one hour and the refresh token lifetime is fourteen days. These values can be adjusted: for more information see [Configurable token lifetimes in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes). Note that if you choose to reduce these lifetimes, you can also reduce the performance of Outlook for iOS and Android, because a smaller lifetime increases the number of times the application must acquire a fresh access token.

**Q:**  What happens to the access token when a user’s password is changed?

**A:**  A previously granted access token is valid until it expires. The identity model you are utilizing for authentication will have an impact on how password expiration is handled. There are three scenarios:

1.  For a federated identity model, you will need to ensure your on-premises identity provider sends password expiry claims to Azure Active Directory, otherwise, Azure Active Directory will not be able to act on the password expiration. For more information, see [Configure AD FS to Send Password Expiry Claims](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims).

2.  Password Hash Synchronization does not support password expiration. This means apps that had previously obtained an access and refresh token pair will continue to function until the lifetime of the token pair is exceeded or the user changes his or her password. For more information, see [Implement password synchronization with Azure AD Connect sync](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-hash-synchronization#how-password-synchronization-works).

3.  Pass-through Authentication requires that password writeback be enabled in AAD Connect. For more information, see [Azure Active Directory Pass-through Authentication: Frequently asked questions](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication-faq#what-happens-if-my-users-password-has-expired-and-they-try-to-sign-in-by-using-pass-through-authentication).

Upon token expiration, the client will attempt to use the refresh token to obtain a new access token, but because the user’s password has changed, the refresh token will be invalidated (assuming directory synchronization has occurred between on-premises and Azure Active Directory). The invalidated refresh token will force the user to re-authenticate in order to obtain a new access token and refresh token pair.

**Q:**  Is there a way for a user to bypass AutoDetect when adding their account to Outlook for iOS and Android?

**A:**  Yes, a user can bypass AutoDetect at any time and manually configure the connection using Basic authentication over the Exchange ActiveSync protocol. To ensure that the user does not establish a connection to your on-premises environment via a mechanism that does not support Azure Active Directory Conditional Access or Intune app protection policies, the on-premises Exchange Administrator needs to configure an Exchange device access rule that blocks the ActiveSync connection. To do this, type the following command in the Exchange Management Shell:

``` 
 New-ActiveSyncDeviceAccessRule -Characteristic DeviceModel -QueryString "Outlook for iOS and Android" -AccessLevel Block
```

## Troubleshooting

Below are the most common issues or errors with on-premises mailboxes using hybrid Modern Authentication with Outlook for iOS and Android.

**AutoDiscover and ActiveSync**

During profile creation, the user should be presented a Modern Authentication dialog similar to this:

![使用者在成功設定混合式的新式驗證時應該會看到的對話方塊](images/Mt846639.2e17cce9-d4b7-4842-9c5a-d92f055dbf56(EXCHG.150).png "使用者在成功設定混合式的新式驗證時應該會看到的對話方塊")

If, instead, the user is presented with one of the following dialogs, then there is an issue with either the Autodiscover or ActiveSync on-premises endpoints.

Here is an example of a user being presented with the legacy Basic authentication Exchange ActiveSync experience:

![指出使用者面對的是舊版基本驗證 Exchange ActiveSync 體驗的對話方塊](images/Mt846639.32bb9907-9cae-4200-9cbf-8091da2eac83(EXCHG.150).png "指出使用者面對的是舊版基本驗證 Exchange ActiveSync 體驗的對話方塊")

And here's an example of what users see when AutoDetect isn't able to discover the configuration for users' on-premises mailboxes.

![當自動偵測無法探索其內部部署信箱的設定時使用者會看到的對話方塊](images/Mt846639.b481cab4-e5b0-4f52-b931-7c4e059453f1(EXCHG.150).png "當自動偵測無法探索其內部部署信箱的設定時使用者會看到的對話方塊")

In either scenario, verify that your on-premises environment is correctly configured. To do this: from the TechNet Gallery, download and execute the script for [Validating Hybrid Modern Authentication setup for Outlook for iOS and Android](https://gallery.technet.microsoft.com/scriptcenter/validating-hybrid-modern-ad4c2b16).

When you review the output from the script, you should be seeing the following from AutoDiscover:

    {
        "Protocol": "activesync",
        "Url": "https://mail.contoso.com/Microsoft-Server-ActiveSync"
    }

The on-premises ActiveSync endpoint should return the following response, where the WWW-Authenticate header includes an authorization\_uri:

    Content-Length →0
    Date →Mon, 29 Jan 2018 19:51:46 GMT
    Server →Microsoft-IIS/10.0 Microsoft-HTTPAPI/2.0
    WWW-Authenticate →Bearer client_id="00000002-0000-0ff1-ce00-000000000000", trusted_issuers="00000001-0000-0000-c000-000000000000@5de110f8-2e0f-4d45-891d-bcf2218e253d,00000004-0000-0ff1-ce00-000000000000@contoso.com", token_types="app_asserted_user_v1 service_asserted_app_v1", authorization_uri="https://login.windows.net/common/oauth2/authorize"
    Www-Authenticate →Basic realm="mail.contoso.com"
    X-Powered-By →ASP.NET
    request-id →5ca2c827-5147-474c-8457-63c4e5099c6e

If the AutoDiscover or ActiveSync responses are not similar to the above examples, you can investigate the following as possible causes:

1.  If the AutoDiscover endpoint cannot be reached, then it's likely there's a firewall or load balancer configuration issue (for example, IP restrictions are configured and the required IP ranges are not present). Also, there may be a device in front of Exchange requiring pre-authentication to access the AutoDiscover endpoint.

2.  If the AutoDiscover endpoint does not return the correct URL, then there is a configuration issue with the ActiveSync virtual directory’s ExternalURL value.

3.  If the ActiveSync endpoint cannot be reached, then there is a firewall or load balancer configuration issue. Again, one example is IP restrictions are configured and the required IP ranges are not present. Also, there may be a device in front of Exchange requiring pre-authentication to access the ActiveSync endpoint.

4.  If the ActiveSync endpoint does not contain an authorization\_uri value, verify that the EvoSTS authentication server is configured as the default endpoint using Exchange Management Shell:
    
    ```powershell
    Get-AuthServer EvoSts | fl IsDefaultAuthorizationEndpoint
    ```

5.  If the ActiveSync endpoint does not contain a WWW-Authenticate header, then a device in front of Exchange may be responding to the query.

**Client synchronization issues**

There are a few scenarios that can result in data being stale in Outlook for iOS and Android. Typically, this is due to an issue with the second access token (the token used by MRS in Exchange Online to synchronize the data with the on-premises environment). The two most common reasons for this issue are:

1.  SSL/TLS offloading on-premises.

2.  EvoSTS certificate metadata issues.

With SSL/TLS offloading, tokens are issued for a specific uri and that value includes the protocol value ("https://"). When the load balancer offloads SSL/TLS, the request Exchange receives comes in via HTTP, resulting in a claim mismatch due to the protocol value being http://. The following is an example of a response header from a Fiddler trace:

    Content-Length →0
    Date →Mon, 29 Jan 2018 19:51:46 GMT
    Server →Microsoft-IIS/10.0 Microsoft-HTTPAPI/2.0
    WWW-Authenticate →Bearer client_id="00000002-0000-0ff1-ce00-000000000000", trusted_issuers="00000001-0000-0000-c000-000000000000@00c118a9-2de9-41d3-b39a-81648a7a5e4d", authorization_uri="https://login.windows.net/common/oauth2/authorize", error="invalid_token"
    WWW-Authenticate →Basic realm="mail.contoso.com"
    X-Powered-By →ASP.NET
    request-id →2323088f-8838-4f97-a88d-559bfcf92866
    x-ms-diagnostics →2000003;reason="The hostname component of the audience claim value is invalid. Expected 'https://mail.contoso.com'. Actual 'http://mail.contoso.com'.";error_category="invalid_resource"

As specified above in the section *Technical and licensing requirements*, SSL/TLS offloading is not supported for OAuth flows.

For EvoSTS Certificate Metadata, the certifricate metadata leveraged by EvoSTS is occasionally updated in Office 365. The Exchange on-premises arbitration mailbox that has the organization capability of “OrganizationCapabilityManagement” is responsible for detecting the changes and for updating the corresponding metadata on-premises; this process executes every eight hours.

Exchange Administrators can find this mailbox by executing the following cmdlet using Exchange Management Shell:

```powershell
$x=get-mailbox -arbitration | ? {$_.PersistedCapabilities -like "OrganizationCapabilityManagement"};Get-MailboxDatabaseCopyStatus $x.database.name
```

On the server hosting the database for the OrganizationCapabilityManagement arbitration mailbox, review the application event logs for events with a source of **MSExchange AuthAdmin**. The events should tell you if Exchange was able to refresh the metadata. If the metadata is out of date, you can manually refresh it with this ccmdlet:

```powershell
Set-AuthServer EvoSts -RefreshAuthMetadata
```

You can also create a scheduled task that executes the above command every 24 hours.

**Other issues**

There are other issues that may prevent hybrid Modern Authentication from functioning correctly. For more information, see the troubleshooting section in [Announcing Hybrid Modern Authentication for Exchange On-Premises](https://blogs.technet.microsoft.com/exchange/2017/12/06/announcing-hybrid-modern-authentication-for-exchange-on-premises/).

