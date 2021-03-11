# BigBlueButton
Ansible role for a backend bigbluebutton installation. Without any extra features like greenlight, postgres database etc.
*(please visit the documentation on http://docs.bigbluebutton.org/install/install.html)*

```
NO LONGER MAINTAINED

Sorry

```

## What does this role do?

+ add apt repos for bigbluebutton
+ install bigbluebutton and requirements
+ disable freeswitch scheduling options for LXD
+ configure and start nginx.
+ create letsencrypt or self-signed cert
+ configure bigbluebutton *(more in tasks/config.yml)*
+ add watchdog for freeswitch


## Requirements

To run bigbluebutton properly we need mongodb installed.<br/>
This can be done with the role [github.com/roles-ansible/ansible-role-bbb-mongodb](https://github.com/roles-ansible/ansible-role-bbb-mongodb.git)

## Role Variables

| Variable Name | Function | Default value | Comment |
| ------------- | -------- | ------------- | ------- |
| `bbbackend__hostname` | Hostname for this BigBlueButton instance _(required)_ | `{{ ansible_fqdn }}` |
| `bbbackend__state` | Install BigBlueButton to state | `present` | for updating BigBlueButton with this role use `latest` |
| `bbbackend__manage_packages` | install requirements for bbb | `true` | if you manage required packages yourself, disable it. |
| `bbbackend__manage_repositories` | Add repositorys for bbb | `true` | if you add the repositorys for bbb by yourself, disable it. |
| `bbbackend__apt_mirror` | apt repo server for BigBlueButton packages | `https://ubuntu.bigbluebutton.org` | other value would be e.g. `https://packages-eu.bigbluebutton.org` |
| `bbbackend__apt_key` | gpg key for the apt repo | `770C4267C5E63474D171B60937B5DD5EFAB46452` |
| `bbbackend__letsencrypt_enable` | Enable letsencrypt/HTTPS | `true` |
| `bbbackend__letsencrypt_email` | E-mail for use with letsencrypt | | *optional but recomended* |
| `bbbackend__ssl_cert` | Path to TLS Certificate | `/etc/letsencrypt/live/{{ bbbackend__hostname }}/fullchain.pem` |
| `bbbackend__ssl_key` | Path to TLS Certificate Key | `/etc/letsencrypt/live/{{ bbbackend__hostname }}/privkey.pem` |
| `bbbackend__nginx_privacy` | only log errors not access | `true` |
| `bbbackend__nginx_dh` | generate Diff-Hellmann for nginx | `true` | *same place like bbb-install.sh* |
| `bbbackend__turn_enable` | enable the use uf TURN in general | `true` |
| `bbbackend__stun_servers` | a list of STUN-Server to use | `{{ bbbackend__hostname }}` | an array with key `server` - take a look in defaults/main.yml
| `bbbackend__ice_servers` | a list of RemoteIceCandidate for STUN | `[]` | in array with key `server`
| `bbbackend__turn_servers` | a list of TURN-Server to use | `[]` | take a look in defaults/main.yml
| `bbbackend__disable_recordings` | Disable options in gui to have recordings | `true` | [Recordings are running constantly in background](https://github.com/bigbluebutton/bigbluebutton/issues/9202) which is relevant as privacy relevant user data is stored
| `bbbackend__mute_on_start:` | start with muted mic on join | `false` |
| `bbbackend__app_log_level:` | set bigbluebutton log level | `DEBUG` |
| `bbbackend__meteor:` | overwrite settings in meteor | `{}` |
| `bbbackend__cpuschedule` | CPUSchedulingPolicy | `true` | Disable to fix [FreeSWITCH SETSCHEDULER error][bbb_cpuschedule] |
| `bbbackend__freeswitch_ipv6` | Enable IPv6 support in FreeSWITCH | `false` | Disable to fix [FreeSWITCH IPv6 error][bbb_freeswitch_ipv6] |
| `bbbackend__freeswitch_external_ip` | Set stun server for sip and rtp on FreeSWITCH | <code>stun:{{ (bbbackend__stun_servers\|first).server }}</code> | WARNING: the value of the default freeswitch installation is `stun:stun.freeswitch.org` |
| `bbbackend__freeswitch_watchdog` | Install watchdog to keep FreeSWITCH running | `true` |
| `bbbackend__dialplan_quality` | Set quality of dailplan for FreeSWITCH | `cdquality` |
| `bbbackend__dialplan_energy_level` | Set energy level of dailplan for FreeSWITCH | `100` | only for selected profile `bbb_dialplan_quality`
| `bbbackend__dialplan_comfort_noise` | Set comfort noise of dailplan for FreeSWITCH | `1400` | only for selected profile `bbb_dialplan_quality`


## Example Playbook
This is an example, of how to use this role. Warning: the value of the Variables should be changed!
```yaml
tbd
```

## License
MIT
