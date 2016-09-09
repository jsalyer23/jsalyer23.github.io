---
layout: page
title:  "Twilio Webhook"
date:   2016-06-21 08:48:55 -0500
categories: jekyll update
---

## Twilio

### Setting up a Webhook

[Twilio](https://www.twilio.com/) allows you to set up a webhook for each of your purchased numbers on your account. After setting up a webhook for your Twilio number, your application will be able to receive new SMS messages sent to your Twilio number. **NOTE:** Before moving on through these steps, you need to have a Twilio account with a phone number set up and a public domain (if your domain is not public use `ngrok` see below).

#### Step One

Twilio needs to know _where_ you want your incoming messages sent. To set this up you need to create a controller action named something like `receiving_incoming_messages` or `new_messages` etc. Your controller action should end up looking something like this:

```ruby
def receiving_incoming_messages
# Your code used to handle the API response
end
```

You will need to add this new controller action to your `config/routes.rb`. Since the only responsibility this action has is to deal with the data Twilio sends, your route will look like this:
```ruby
post "/receiving_incoming_messages" => "YOUR_CONTROLLER_NAME#receiving_incoming_messages"
```

#### Step Two

When receiving `POST` resquests in Rails, you need to add a `skip_before_filter` statement within your contoller so skip the default security feature (CSRF Authenticity Token). You also will receive an error letting you know that there is no view for this controller action so you need to have the action render nothing. This should look like this:

```ruby
class YourController < ApplicationController
	skip_before_filter :verify_authenticity_token, only: [:receiving_incoming_messages]
	def receiving_incoming_messages
		# Your code
		render nothing: true
	end
```

#### Step Three

Now that you have your controller action set up, we just need to tell Twilio to `POST` to the new path we've created. Visit your Twilio account dashboard, click on "Phone Numbers", and click on the phone number you want to set up.

Scroll down to the "Messaging" section:
- "Configure With" should be set to "Webhooks/TwiML"
- "A Message Comes In" should be set to "Webhook"
	- This input field is where you need to add your domain name with the path to your controller action (`http://YOUR_DOMAIN/receiving_incoming_messages`)
	- Since the route we set up uses `POST`, the drop down next to the input box needs to be set to "HTTP POST"

Click the save button and you're done! Send a message to your Twilio number to try it out.

### Testing Twilio Webhook

If your application is not yet deployed, you may not have a publicly accessable domain for Twilio to interact with. With [ngrok](https://ngrok.com/) you can create a secure tunnel to your local server (`localhost:3000` for example). This allows you to point Twilio at the public URL created by `ngrok` and test out receiving messages. The set up process with Twilio is the same but when you tell Twilio which domain you want it to send the messages to, you will use the URL from `ngrok`.

#### Step One

Install `ngrok`: 
	`brew install ngrok`

#### Step Two

In the `Rails.application.configure` block in `config/environments/development.rb`, add this line:
`config.web_console.whitelisted_ips = '192.168.0.100'`

#### Step Three

Start your server (`rails s`) and start `ngrok` in another console tab (`ngrok http 3000`). `http 3000` is telling `ngrok` that you want to start a public HTTP connection on port 3000 which is your local server's default.

#### Step Four

In your `ngrok` tab, there should be two forwarding URLs (`http://7aea90de.ngrok.io` for example) which are the URLs you can choose from. Pick one and go to the page in your browser.

#### Step Five

Now all you need to do is visit Twilio and add the domain with the path to your controller action to the messaging settings for the number you want to test.