# Home Assistant Add-on: PodTube

![Supports aarch64 Architecture][aarch64-shield]
![Supports amd64 Architecture][amd64-shield]
![Supports armhf Architecture][armhf-shield]
![Supports armv7 Architecture][armv7-shield]
![Supports i386 Architecture][i386-shield]

[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg

Turn YouTube channels, playlists and videos into instant ad-free playable
RSS feeds or video files.

## About

PodTube is a python script from https://github.com/aquacash5/PodTube

It uses `pytube` and various other libraries to take a YouTube video or channel identifier and extract the video or sequence of videos from it, then either play
directly in the browser, or return an RSS file that can be used to download
videos for offline viewing. All of this happens ad-free, and makes the YouTube experience much more pleasant.

All interaction is done through URLs (there is no user interface).

It works using a google API key, which you can create for free. Once this is entered into the configuration section of the addon, start the addon, and that's it!

## Example uses:

### View one video

Starting from a video url e.g.

```
https://www.youtube.com/watch?v=D936T1Ze8-4
```

Extract video id `D936T1Ze8-4` and create the URL:

```
http://homeassistant.local:9876/video/D936T1Ze8-4
```

PodTube will now respond to this URL with the single video without ads.

The process can be automated further and added to an iOS share sheet using a
[shortcut like this](https://www.icloud.com/shortcuts/2f01d59d3f714dfab7e938561f5262ea).

### Playlists

Get the playlist id from the youtube url

```
https://www.youtube.com/playlist?list=<PlaylistID>
```

Add the url to your podcast client of choice

```
http://homeassistant.local:9876/playlist/<PlaylistID>
```

If you want an audio podcast add a /audio to the url

```
http://homeassistant.local:9876/playlist/<PlaylistID>/audio
```

### Channels

Get the channel id or username from the youtube url

```
https://www.youtube.com/channel/<ChannelID>
```

or

```
https://www.youtube.com/user/<Username>
```

Add the url to your podcast client of choice

```
http://homeassistant.local:9876/channel/<ChannelID>
```

or

```
http://homeassistant.local:9876/channel/<Username>
```

If you want an audio podcast add a /audio to the url

```
http://homeassistant.local:9876/channel/<Username>/audio
```

### More

For more examples see
https://github.com/aquacash5/PodTube
