I can use [https://docs.ansible.com/ansible/latest/modules/systemd_module.html](ansible systemd) to ensure certain state of certain unit. And these are available value of `state` parameter:
- reloaded
- restarted
- started
- stopped

For some services like [https://github.com/sysstat/sysstat](sysstat), it doens't expose `reload` command to systemd. Which will cause a failure if you're using ansible module to ensure sysstat is reloaded.

Systemctl command, daemon of systemd, has an option called `reload-or-restart`, which will reload the configuration if it's available, and will restart instead if reload is not available. It's interesting to know there are options called `try-restart` and `try-reload-or-restart`, which will try restart/reload if unit is already running, and will not restart/reaload if unit is in stopped state. See `man systemctl` for detailed info.

So far, when I looked into ansible systemd, it doesn't support `reload-or-restart` state. If it's implemented, I guess the value would be something like `state: reloaded-or-restarted`

