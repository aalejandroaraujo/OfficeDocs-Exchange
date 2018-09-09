---
title: "Configure custom MailTips for recipients"
ms.author: dmaguire
author: msdmaguire
manager: laurawi
ms.date: 11/17/2014
ms.audience: ITPro
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
ms.assetid: df8ee7ae-2486-4890-b057-cda87b4cb1ec
description: "MailTips are informative messages displayed to users in the InfoBar in Outlook Web App and Microsoft Outlook 2010 or later when a user does any of the following while composing an e-mail message:"
---

# Configure custom MailTips for recipients

MailTips are informative messages displayed to users in the InfoBar in Outlook Web App and Microsoft Outlook 2010 or later when a user does any of the following while composing an e-mail message: 
  
- Add a recipient
    
- Add an attachment
    
- Reply or Reply all
    
- Open a message from the Drafts folder that's already addressed to recipients
    
In addition to the built-in MailTips that are available, you can create custom MailTips for all types of recipients. For more information about the built-in MailTips, see [MailTips](mailtips.md).
  
## What do you need to know before you begin?

- Estimated time to complete: 10 minutes
    
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "MailTips" entry in the [Mail flow permissions](http://technet.microsoft.com/library/f49f4fb5-af75-43cb-900f-c5f7b8cfa143.aspx) topic. 
    
- You can configure the primary MailTip in the Exchange admin center (EAC) or in the Shell. However, you can only configure additional MailTip translations in the Shell.
    
- When you add a MailTip to a recipient, two things happen:
    
  - HTML tags are automatically added to the text. For example, if you enter the text:  `This mailbox is not monitored`, the MailTip automatically becomes:  `<html><body>This mailbox is not monitored</body></html>`. Additional HTML tags in the MailTip aren't supported.
    
  - The text is automatically added to the  _MailTipTranslations_ property of the recipient as the default value. If you modify the MailTip text, the default value is automatically updated in the  _MailTipTranslations_ property. 
    
- The length of a MailTip can't exceed 175 displayed characters.
    
- For information about keyboard shortcuts that may apply to the procedures in this topic, see **Keyboard shortcuts in the Exchange admin center**.
    
> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612),[Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351). 
  
## What do you want to do?

### Configure MailTips for recipients

#### Use the EAC to configure MailTips for recipients

1. In the EAC, navigate to **Recipients**.
    
2. Select any of the following recipient tabs based on the recipient type:
    
  - **Mailboxes**
    
  - **Groups**
    
  - **Resources**
    
  - **Contacts**
    
  - **Shared**
    
3. On the recipient tab, select the recipient you want to modify, and click **Edit**![Edit icon](../../media/ITPro_EAC_EditIcon.gif).
    
4. In the recipient properties page that appears, click **MailTips**.
    
5. Enter the text for the MailTip. When you are finished, click **Save**.
    
#### Use the Shell to configure MailTips for recipients

To configure a MailTip for a recipient, use the following syntax.
  
```
Set-<RecipientType> <RecipientIdentity> -MailTip "<MailTip text>"
```

 _\<RecipientType\>_ can be any type of recipient. For example,  `Mailbox`,  `MailUser`,  `MailContact`,  `DistributionGroup`, or  `DynamicDistributionGroup`.
  
For example, suppose you have a mailbox named "Help Desk" for users to submit support requests, and the promised response time is two hours. To configure a custom MailTip that explains this, run the following command:
  
```
Set-Mailbox "Help Desk" -MailTip "A Help Desk representative will contact you within 2 hours."
```

### Use the Shell to configure additional MailTips in different languages

To configure additional MailTip translations without affecting the existing MailTip text or other existing MailTip translations, use the following syntax:
  
```
Set-<RecipientType> -MailTipTranslations @{Add="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...; Remove="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...}
```

 _\<culture\>_ is a valid ISO 639 two-letter culture code associated with the language. 
  
For example, suppose the mailbox named Notifications currently has the MailTip: "This mailbox is not monitored." To add the Spanish translation, run the following command:
  
```
Set-Mailbox -MailTipTranslations @{Add="ES:Este buzón no se supervisa."}
```

### How do you know this worked?

To verify that you have successfully configured a MailTip for a recipient, do the following:
  
1. In Outlook Web App or Outlook 2010 or later, compose an email message addressed to the recipient, but don't send it.
    
2. Verify the MailTip appears in the InfoBar.
    
3. If you configured additional MailTip translations, compose the message in Outlook Web App where the language setting matches the language of the MailTip translation to verify the results.
    

