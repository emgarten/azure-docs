---
title: 'Tutorial: Azure AD SSO integration with Insignia SAML SSO | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Insignia SAML SSO.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 06/21/2022
ms.author: jeedes
---
# Tutorial: Azure AD SSO integration with Insignia SAML SSO

In this tutorial, you'll learn how to integrate Insignia SAML SSO with Azure Active Directory (Azure AD). When you integrate Insignia SAML SSO with Azure AD, you can:

* Control in Azure AD who has access to Insignia SAML SSO.
* Enable your users to be automatically signed-in to Insignia SAML SSO with their Azure AD accounts.
* Manage your accounts in one central location - the Azure portal.


## Prerequisites

To configure Azure AD integration with Insignia SAML SSO, you need the following items:

* An Azure AD subscription. If you don't have an Azure AD environment, you can get a [free account](https://azure.microsoft.com/free/).
* Insignia SAML SSO single sign-on enabled subscription.

## Scenario description

In this tutorial, you configure and test Azure AD single sign-on in a test environment.

* Insignia SAML SSO supports **SP** initiated SSO.

## Add Insignia SAML SSO from the gallery

To configure the integration of Insignia SAML SSO into Azure AD, you need to add Insignia SAML SSO from the gallery to your list of managed SaaS apps.

1. Sign in to the Azure portal using either a work or school account, or a personal Microsoft account.
1. On the left navigation pane, select the **Azure Active Directory** service.
1. Navigate to **Enterprise Applications** and then select **All Applications**.
1. To add new application, select **New application**.
1. In the **Add from the gallery** section, type **Insignia SAML SSO** in the search box.
1. Select **Insignia SAML SSO** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure and test Azure AD SSO for Insignia SAML SSO

Configure and test Azure AD SSO with Insignia SAML SSO using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between an Azure AD user and the related user in Insignia SAML SSO.

To configure and test Azure AD SSO with Insignia SAML SSO, perform the following steps:

1. **[Configure Azure AD SSO](#configure-azure-ad-sso)** - to enable your users to use this feature.
    1. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with B.Simon.
    2. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable B.Simon to use Azure AD single sign-on.
2. **[Configure Insignia SAML SSO](#configure-insignia-saml-sso)** - to configure the single sign-on settings on application side.
    1. **[Create Insignia SAML SSO test user](#create-insignia-saml-sso-test-user)** - to have a counterpart of B.Simon in Insignia SAML SSO that is linked to the Azure AD representation of user.
3. **[Test SSO](#test-sso)** - to verify whether the configuration works.

## Configure Azure AD SSO

Follow these steps to enable Azure AD SSO in the Azure portal.

1. In the Azure portal, on the **Insignia SAML SSO** application integration page, find the **Manage** section and select **single sign-on**.
1. On the **Select a single sign-on method** page, select **SAML**.
1. On the **Set up single sign-on with SAML** page, click the pencil icon for **Basic SAML Configuration** to edit the settings.

   ![Screenshot showing the edit Basic SAML Configuration screen.](common/edit-urls.png)

4. On the **Basic SAML Configuration** section, perform the following steps:

	a. In the **Sign on URL** text box, type a URL using one of the following patterns:
	
   | Sign on URL|
   |------------|
   | `https://<customername>.insigniails.com/ils` |
   | `https://<customername>.insigniails.com/` |
   | `https://<customername>.insigniailsusa.com/` |
   |
	
	b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern:
    `https://<customername>.insigniailsusa.com/<uniqueid>`

	> [!NOTE]
	> These values are not real. Update these values with the actual Sign on URL and Identifier. Contact [Insignia SAML SSO Client support team](http://www.insigniasoftware.com/insignia/Techsupport.aspx) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section in the Azure portal.

5. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, click **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

	![The Certificate download link](common/certificatebase64.png)

6. On the **Set up Insignia SAML SSO** section, copy the appropriate URL(s) as per your requirement.

	![Copy configuration URLs](common/copy-configuration-urls.png)

### Create an Azure AD test user

In this section, you'll create a test user in the Azure portal called B.Simon.

1. From the left pane in the Azure portal, select **Azure Active Directory**, select **Users**, and then select **All users**.
2. Select **New user** at the top of the screen.
3. In the **User** properties, follow these steps:
   1. In the **Name** field, enter `B.Simon`.  
   2. In the **User name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
   3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
   4. Click **Create**.

### Assign the Azure AD test user

In this section, you'll enable B.Simon to use Azure single sign-on by granting access to Insignia SAML SSO.

1. In the Azure portal, select **Enterprise Applications**, and then select **All applications**.
2. In the applications list, select **Insignia SAML SSO**.
3. In the app's overview page, find the **Manage** section and select **Users and groups**.
4. Select **Add user**, then select **Users and groups** in the **Add Assignment** dialog.
5. In the **Users and groups** dialog, select **B.Simon** from the Users list, then click the **Select** button at the bottom of the screen.
6. If you are expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
7. In the **Add Assignment** dialog, click the **Assign** button.

## Configure Insignia SAML SSO

To configure single sign-on on **Insignia SAML SSO** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from Azure portal to [Insignia SAML SSO support team](http://www.insigniasoftware.com/insignia/Techsupport.aspx). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Insignia SAML SSO test user

In this section, you create a user called Britta Simon in Insignia SAML SSO. Work with [Insignia SAML SSO support team](http://www.insigniasoftware.com/insignia/Techsupport.aspx) to add the users in the Insignia SAML SSO platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Azure AD single sign-on configuration with following options. 

* Click on **Test this application** in Azure portal. This will redirect to Insignia SAML SSO Sign-on URL where you can initiate the login flow. 

* Go to Insignia SAML SSO Sign-on URL directly and initiate the login flow from there.

* You can use Microsoft My Apps. When you click the Insignia SAML SSO tile in the My Apps, this will redirect to Insignia SAML SSO Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Next steps

Once you configure Insignia SAML SSO you can enforce session control, which protects exfiltration and infiltration of your organization’s sensitive data in real time. Session control extends from Conditional Access. [Learn how to enforce session control with Microsoft Defender for Cloud Apps](/cloud-app-security/proxy-deployment-aad).