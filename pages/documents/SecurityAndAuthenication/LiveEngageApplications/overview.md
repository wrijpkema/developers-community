---
pagename: What Is a LivePerson Application?
redirect_from:
  - guides-le-applications-what-is.html
Keywords:
sitesection: Documents
categoryname: "Security & Authentication"
documentname: LivePerson Applications
level-order: 13
order: 10
permalink: liveperson-applications-what-is-a-liveperson-application.html
root-link: true
indicator: both
---

LivePerson Applications are a code layer developed on top of LivePerson APIs which includes an `App_Install_Id` parameter. This parameter is received when registering a dedicated configuration manifest that defines its scope and components.

There are two different types of LivePerson Applications:

### Private LivePerson Applications

A customer will be able to develop and use their own private LivePerson Applications. These applications won’t be published in the Marketplace.

This type of LivePerson Application will be installed manually by uploading a JSON Manifest based on the [LivePerson Application Installation schema](guides-le-applications-installing.html). This schema will be uploaded under the specific account.

### Global LivePerson Applications

**Global applications are restricted to LivePerson only and can't be developed by 3rd party developers (for now).**

This type of Application needs to be be published to the Marketplace by a LivePerson Developer and will be available for all LP customers to install (use/onboard) and manage within the Applications area.


{: .notice}
To read a more general overview of LivePerson applications and how they work, please visit our Knowledge Center.
