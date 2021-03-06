# Azure Active Directory Token Key Scripts
This respository contains PowerShell scripts that developers and administrators can use to test their Azure Active Directory integrated applications for automatic token signing key rollover. For more information about signing key rollover, check out the [Signing key rollover in Azure Active Directory documentation](https://azure.microsoft.com/en-us/documentation/articles/active-directory-signing-key-rollover/).

# Impact
These scripts set the preferred token signing key on a specific application. As a result, **any user that signs in to the application** after the script is run will receive tokens signed with the preferred certificate.

# Pre-Requisites
These scripts can **only be run by an Azure Active Directory Global Administrator**.

If the application does not support automatic rollover, changing the token signing key will result in downtime. Therefore, it is strongly recommended that these scripts are only run:
- Either on a **test application** for which downtime is acceptable 
- Or on a production application **during downtime window**

# Steps To Run The Script
1.	[Download](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey/blob/master/Zip/AzureADPowershellTokenKey.zip?raw=true) and extract the scripts
2.	Start Windows Powershell
3.	Navigate to the folder where the scripts were extracted
4.	Run .\install-aadGraphModule.ps1
5.	Execute the script .\UpdateThumbprint-RollForward
6.	Test the web application. The change is instantaneous, but make sure you use a new InPrivate browser window to ensure you get a new token.
7.	If the web application signs you in properly, it supports automatic rollover. If it does not, check out the section below.
8.	Execute the script .\UpdateThumbprint-RestoreDefaultBehavior.ps1

#Sign-In Failure After Testing
If the application fails to sign users in after running the scripts then it does not support automatic rollover.
Check out the [Signing key rollover in Azure Active Directory documentation](https://azure.microsoft.com/en-us/documentation/articles/active-directory-signing-key-rollover/) for guidance on how to modify your application in order to add support for automatic rollover.

# Security Reporting
If you find a security issue with our libraries or services please report it to [secure@microsoft.com](mailto:secure@microsoft.com) with as much detail as possible. Your submission may be eligible for a bounty through the [Microsoft Bounty](http://aka.ms/bugbounty) program. Please do not post security issues to GitHub Issues or any other public site. We will contact you shortly upon receiving the information. We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/en-us/security/dd252948) and subscribing to Security Advisory Alerts.

# We Value and Adhere to the Microsoft Open Source Code of Conduct
This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
