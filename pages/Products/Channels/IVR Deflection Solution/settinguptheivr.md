---
title: Setting up the IVR Deflection for Chat
level1: Solutions
level2: Channels
level3: IVR Deflection
order: 30
permalink: products-ivr-chat-setup.html
indicator: chat
---

To start using the **IVR Deflection Solution for Chat**, set up a LiveEngage campaign with IVR engagement following the key steps listed below:

1.  Create an engagement and select the IVR as the source.

2.  Configure the landing page URL to which consumers will be redirected after clicking on the link attached to the SMS.

  * The page must contain the LiveEngage tag.

  * The page should be a simple page with limited content so that it loads quickly.

{:start="3"}
3.  Copy the static link, as shown below, if choosing to skip the availability check.

    ![IVR3](img/ivr3.png)



### Best Practices for Setting up your IVR

In order to set up your IVR, a scenario must be created by adding a modifying VXML snippet to the IVR decision tree. IVRs support the ability to decide when a scenario is presented to the visitor.

Sample scenarios can be:

* Mobile users only.

* Offer IVR deflection between 09:00 to 17:00.

* Offer IVR deflection to callers if wait time is longer than 10 min.

* Offer IVR deflection to X% of the callers.

Most modern IVRs also have built-in SMS gateways, which allow them to send or receive (SMS) transmissions. IVRs can use gateways to send chat invite links to voice callers. In cases where the IVR does not support an SMS gateway, you can configure the IVR to send SMS using 3rd party SMS gateways.

The [Appendix](products-channels-ivr-deflection-solution-appendix.html){:target="_blank"} provides 2 SMS gateway integration samples.

**The following is an example of VoiceXML 2.1 using a Voxeo IVR SMS solution and a static link:**

```xml

<?xml version="1.0" encoding="UTF-8"?>
<vxml version = "2.1">
<meta name="maintainer" content="<author email>"/>
<form>
<var name="botkey" expr="*****"/>
<var name="apimethod" expr="'send'"/>
<var name="msg" expr="'<Enter the SMS text message and the short URL here. >'"/>
<var name="network" expr="'SMS'"/>
<var name="from" expr="<sender phone number>"/>
<field name="user" type="digits">
<prompt>Please enter a your phone number including the country code and area number. To finish press the pound sign.</prompt>
<filled>
<prompt>A chat link will be send to <say-as interpret-as="vxml:phone"><value expr="user"/></say-as>. Thank you and good bye.</prompt>

```

**Note**: Other SMS providers may use a different method to send SMS text messages.

### Impact of the IVR Deflection Solution on Existing Functionality

The table below illustrates the impact of this feature upon LiveEngage
users.

| User             | Impact                                                                                                                                                                                                                                                |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campaign Manager | The Visits KPI (which is found in the Campaign Manager Data Bar and is used to track website visitors) will not track the voice callers who called the IVR. Instead, it will begin tracking visitors who clicked on the link embedded within the SMS. |


### SMS Vendors Code Examples

The following are VXML examples of sending text messages using leading SMS gateway vendors. The VXML code should be deployed in the appropriate IVR decision tree location (scenario).

**Sample flow**:

1. Prompt caller for phone number.

2. Retrieve phone number.

3. Thank caller.

4. Send request to the SMS gateway.

5. Disconnect.


### clickatell.com

```xml
	<?xml version="1.0" encoding="UTF-8"?>
	<vxml version = "2.1">
	<form>
	<var name="msg" expr="'Please click this URL to chat with an agent http://bit.ly/1FqRKyT'"
	<field name="user" type="digits">
	<audio src="http://s3.amazonaws.com/lpivr/voice/presspound.mp3" fetchhint="prefetch"
	<filled>
	<audio src="http://s3.amazonaws.com/lpivr/voice/thank+you+after+pressed+1.mp3" fetchhint="prefetch"
	<data ecmaxmltype="e4x" name="SendSMS" srcexpr="'http://api.clickatell.com/http/sendmsg?user=hblutrich&amp;password=<password>&amp;api\_id=<id>&amp;to=' + encodeURIComponent(user) + '&amp;text=' + encodeURIComponent(msg)"
	</filled>
	</field>
	</form>
	</vxml>
```

### Voxeo

```xml
	<?xml version="1.0" encoding="UTF-8"?>
	<vxml version = "2.1">
	<form>
	<var name="botkey" expr="<key>"
	<var name="apimethod" expr="'send'"
	<var name="msg" expr="'Please click this URL to chat with an agent http://bit.ly/1IAVehP'"
	<var name="network" expr="'SMS'"
	<var name="from" expr="3477733852"
	<field name="user" type="digits">
	<audio src="http://s3.amazonaws.com/lpivr/voice/presspound.mp3" fetchhint="prefetch"
	<filled>
	<audio src="http://s3.amazonaws.com/lpivr/voice/thank+you+after+pressed+1.mp3" fetchhint="prefetch"
	<data name="SendSMS" srcexpr="'http://<user>:<password>@api.messaging.staging.voxeo.net/1.0/messaging?botkey=' + encodeURIComponent(botkey)+ '&amp;apimethod=' + encodeURIComponent(apimethod) + '&amp;msg=' + encodeURIComponent(msg) + '&amp;user=' + encodeURIComponent(user) + '&amp;network=' + encodeURIComponent(network) + '&amp;from=' + encodeURIComponent(from)"
	</filled>
	</field>
	</form>
	</vxml>
```
