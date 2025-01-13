# Setup voice assist pipeline

https://www.home-assistant.io/voice_control/voice_remote_local_assistant

1. Install [whisper](https://my.home-assistant.io/redirect/supervisor_addon?addon=core_whisper)
2. Install [piper](https://my.home-assistant.io/redirect/supervisor_addon?addon=core_piper)
3. Install [openwakeword](https://my.home-assistant.io/redirect/supervisor_addon?addon=core_openwakeword)
4. Start whisper, piper and openwakeword
5. Install the [Wyoming protocol integration](https://www.home-assistant.io/integrations/wyoming/)
6. Go to each of whisper / piper / openwakeword. The name will be shown. In the configuration page, click on "show disabled ports" and copy the port. By default these will be:
	   * `core-piper`, `10200`
	   * `core-whisper`, `10300`
	   * `core-openwakeword`, `10400`
7. Add each of these as an entry in the Wyoming config page (See last post on [this page](https://community.home-assistant.io/t/wyoming-protocol/625621/14) for more info)

#homeassistant 