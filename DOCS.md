Hopefully the backup of docker-compose is enough to restore everything if my server completely dies, but this can be a reference for various setup and commands as I remember to add them for my own reference.

----

## Services

- [homeassistant](https://www.home-assistant.io/) - the main thing that is in charge of everything
- [cloudflared-tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/get-started/) - uses a cloudflare tunnel to let me access home assistant outside of the local network
- [mosquitto](https://mosquitto.org/) - MQTT server to let home assistant talk to frigate and zwave js
- [zwave js](https://github.com/zwave-js/zwave-js-ui) - adds some management to the zwave network so that home assistant can access the devices


### Mosquitto

For frigate, home assistant, and zwave js to talk to mosquitto they need passwords. I have them all set up with separate passwords. To create a new password, log into the mosquitto's shell:
  - In portainer go to the mosquitto container and then Console
  - Choose `/bin/sh` as the shell script interpreter

 and do the following:

```
cd /mosquitto/config
mosquitto_passwd password.txt [username]
[Enter password as prompted twice, remember the password!]
```

> Important: restart the mosquitto docker container so that the changes take effect!

Now that user should be able to use the entered password to connect to the broker.

#### Debugging

I've downloaded this to test various connections and things in a UI

https://mqttx.app/downloads

### ZWave

- https://www.home-assistant.io/integrations/zwave_js#advanced-installation-instructions
- Option 3: The Z-Wave JS UI Docker container
- https://zwave-js.github.io/zwave-js-ui//#/getting-started/quick-start

#### Resetting the stick

I had to reset the stick when I redid everything because I didn't know the old security codes. This software let me reset easily and could be good for future debugging of the zwave network but it was difficult to find the right downloads, I'm not sure which link actually worked. Need an account and then something here https://www.silabs.com/wireless/z-wave?tab=software#software you eventually get a PC Controller inside the Simplicity Studio which recognized the stick and the attached device(s).
