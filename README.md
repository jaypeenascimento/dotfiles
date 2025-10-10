
# Jaypee's dotfiles!

This repository aims to save my endeavouros most important settings.

### Fixing Pipewire to work with JBL Headphones

When i was trying to setup EndeavourOS, i kept getting errors when trying to use my JBL headphones with Pipewire.
When i tried to switch to PulseAudio, it worked fine (Like my work ubuntu does, it also uses pulse audio).
But, since i'm using sway, i need the `xdg-desktop-portal-wlr`, which kept failing with the error: `xdg-desktop-portal-wlr.service failed to start portal service wlroots implementation`.

And why? Because it depends on `Pipewire` xD. (Which is breaking with `spa.alsa snd_pcm_avail after recover: Broken pipe`)

So, i found a solution into this issue of waydroid:
https://github.com/waydroid/waydroid/issues/1683

The user `rhjdvsgsgks` (Actually it's his name) wisely said:

found solution. limit minimum quantum of pipewire to 512. so that it will accept 256 from waydroid, resample it to 512, and send to hardware.
```
# /etc/pipewire/pipewire.conf.d/1.conf
context.properties = {
        default.clock.min-quantum = 512
}
```

you can also quick test it by

```
pw-metadata -n settings 0 clock.force-quantum 512
```

So, yeah, it works very well and saved me from getting a new headphone or do not be able to screenshare on sway.
