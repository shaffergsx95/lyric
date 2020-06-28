# Honeywell Lyric Custom Component (for Home Assistant)

This is an updated, working integration (December 2019), that is based on these two great libraries that unfortunately appear to be abandoned, buggy, and no longer work:

* https://github.com/bramkragten/python-lyric
* https://github.com/bramkragten/lyric

This will give support for the [Honeywell Lyric](http://yourhome.honeywell.com/en/products/thermostat/lyric-thermostat) thermostats in [Home Assistant](https://www.home-assistant.io/)

- Visit [Honeywell Developers](http://developer.honeywell.com/), and sign in. Create an account if you don’t have one already.
- Fill in account details.
- Submit changes
- Click “[My Apps](http://developer.honeywell.com/user/me/apps)” at top of page, under your account.
- Click “[Create New App](http://developer.honeywell.com/user/me/apps/add)”
- Fill in details:
- App name. Can be anything, I use Home Assistant.
- In the “Callback URL” enter the adress to your Home Assistant instance: “https://yourhomeassistant:8123/api/lyric/authenticate”. **If you have base_url in your http config, use this url.** Otherwise use your local ip.
- Click “Save Changes”
- On the apps page, click on the just created app.
- The “Consumer Key” and “Consumer Secret” are shown now. These will be used as client_id and client_secret below.

Once Home Assistant is started, a configurator will pop up asking you to log into your Lyric account.
*NOTE: This may be under "Notifications".*

### Configuration
```yaml
# Example configuration.yaml entry
lyric:
  client_id: CONSUMER_KEY
  client_secret: CONSUMER_SECRET
```

```yaml
# Example configuration.yaml entry to show only devices at your vacation and primary homes
lyric:
  client_id: CONSUMER_KEY
  client_secret: CONSUMER_SECRET
  locations:
    - Vacation
    - Primary
```

Configuration variables:

- *client_id* (Required): Your Lyric developer consumer key.
- *client_secret* (Required): Your Lyric developer consumer secret.
- *locations* (Optional): The location or locations you would like to include devices from. If not specified, this will include all locations in your Lyric account.

### Troubleshooting
#### *"The redirect URL provided does not match the redirect URL registered for the app."*
This error will occur if the callback URL advertised to the Honeywell Home OAuth 2.0 API does not match what was entered upon app creation.
#### Solution
Ensure that *base_url: https://myHAserver.blah.org:myPort* is present in the *http:* entry in configuration.yaml.
*NOTE: This must be externally accessible.*
##### Example:
```yaml
# Example HTTP SSL configuration entry in configuration.yaml
http:
  ssl_certificate: /ssl/fullchain.pem
  ssl_key: /ssl/privkey.pem
  base_url: https://myHAserver.blah.org:myPort
```

