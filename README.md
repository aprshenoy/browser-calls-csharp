<a href="https://www.twilio.com">
  <img src="https://static0.twilio.com/marketing/bundles/marketing/img/logos/wordmark-red.svg" alt="Twilio" width="250" />
</a>

# Browser Calls (ASP.NET MVC)

![](https://github.com/TwilioDevEd/browser-calls-csharp/workflows/NetFx/badge.svg)
[![Build status](https://ci.appveyor.com/api/projects/status/tiltaaj3tg78i515?svg=true)](https://ci.appveyor.com/project/TwilioDevEd/browser-calls-csharp)

> We are currently in the process of updating this sample template. If you are encountering any issues with the sample, please open an issue at [github.com/twilio-labs/code-exchange/issues](https://github.com/twilio-labs/code-exchange/issues) and we'll try to help you.

Learn how to use [Twilio Client](https://www.twilio.com/client) to make browser-to-phone and browser-to-browser calls with ease. The unsatisfied customers of the Birchwood Bicycle Polo Co. need your help.

[Read the full tutorial here](https://www.twilio.com/docs/tutorials/walkthrough/browser-calls/csharp/mvc)!

## Quickstart

### Create a TwiML App

This project is configured to use a **TwiML App**, which allows us to easily set the voice URLs for all Twilio phone numbers we purchase in this app.

Create a new TwiML app and save its `Sid`. You will need it to setup your app settings.
  Using the [twilio-cli](https://www.twilio.com/docs/twilio-cli) ?
  ```
  twilio api:core:applications:create --friendly-name browser-calls --voice-url [your-app-url]
  ```
  If not you can do it at https://www.twilio.com/console/voice/twiml/apps/create
  See the end of the "Local development" section for details on the exact URL to use in your TwiML app.

Once you have created your TwiML app, configure your Twilio phone number to use it ([instructions here](https://support.twilio.com/hc/en-us/articles/223180928-How-Do-I-Create-a-TwiML-App-)).
If you don't have a Twilio phone number yet, you can purchase a new number in the [Twilio Console](https://www.twilio.com/console/phone-numbers/incoming).

### Local development

1. First clone this repository and `cd` into its directory:
   ```
   git clone https://github.com/TwilioDevEd/browser-calls-csharp.git

   cd browser-calls-csharp
   ```

2. Create a copy of `BrowserCalls.Web/Web.config.sample` and rename it to
   `BrowserCalls.Web/Web.config`.

3. Open `BrowserCalls.Web/Web.config` and update the following keys:
   ```
   <appSettings>
     <!-- omitted for clarity -->
     <add key="TwilioAccountSid" value="TWILIO_ACCOUNT_SID" />
     <add key="TwiMLApplicationSid" value="TWIML_APPLICATION_SID" />
     <add key="TwilioPhoneNumber" value="TWILIO_PHONE_NUMBER" />
     <add key="TwilioApiKey" value="API_KEY" />
      <add key="TwilioApiSecret" value="API_SECRET" />
   </appSettings>
   ```

   You can find your `TWILIO_ACCOUNT_SID` under your
   [Twilio Account Settings](https://www.twilio.com/user/account/settings). Set
   `TWILIO_APPLICATION_SID` to the app SID you created
   before. `TWILIO_PHONE_NUMBER` should be set to the phone number you
   purchased above.

   The `API_KEY` and `API_SECRET` values are your REST API Key information needed
   to create an [Access Token](https://www.twilio.com/docs/iam/access-tokens).
   You can create [one here](https://www.twilio.com/console/project/api-keys).

4. Build the solution.

5. Run `Update-Database` at [Package Manager
   Console](https://docs.nuget.org/consume/package-manager-console) to execute the migrations.

6. Run the application.

7. Check it out at http://localhost:9932

    To actually forward incoming calls, your development server will need to be publicly accessible. [We recommend using ngrok to solve this problem](https://www.twilio.com/blog/2015/09/6-awesome-reasons-to-use-ngrok-when-testing-webhooks.html).

8. To start your ngrok tunnel, run this from a command line (after [downloading ngrok](https://ngrok.com/download)):

	```
	ngrok http -host-header="localhost:9932" 9932
	```

	Or, you can install [Ngrok Extensions](https://marketplace.visualstudio.com/items?itemName=DavidProthero.NgrokExtensions) for Visual Studio.

9. Once you have started ngrok, update your TwiML app's voice URL setting to use your ngrok hostname, so it will look something like this:

	```
	https://<your-ngrok-subdomain>.ngrok.io/Call/Connect
	```

    If you make changes to your ASP.NET application and restart it, there is no need to restart the ngrok tunnel. Leaving it running will avoid getting a new ngrok subdomain and requiring you to update your TwiML app's voice URL.

### Try it out

1. To create a support ticket go to the home page.
   On this page you could fill some fields and create a ticket or you can call to support.

   ```
   https://<your-ngrok-subdomain>.ngrok.io
   ```

   __Note:__ Make sure you use the `https` version of your ngrok URL as some
   browsers won't allow access to the microphone unless you are using a secure
   SSL connection.

1. To respond to support tickets go to the Dashboard page (you should open two windows or tabs).
   On this page you could call customers and answers phone calls.

   ```
   https://<your-ngrok-subdomain>.ngrok.io/Dashboard
   ```

## Meta

* No warranty expressed or implied. Software is as is. Diggity.
* The CodeExchange repository can be found [here](https://github.com/twilio-labs/code-exchange/).
* [MIT License](http://www.opensource.org/licenses/mit-license.html)
* Lovingly crafted by Twilio Developer Education.
