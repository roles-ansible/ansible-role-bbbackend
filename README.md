# BigBlueButton
Ansible role for a backend bigbluebutton installation. Without any extra features like greenlight, ipostgres database etc.
*(please visit the documentation on http://docs.bigbluebutton.org/install/install.html)*

```
WORK IN PROGRESS
```

## Role Variables

| Variable Name | Function | Default value | Comment |
| ------------- | -------- | ------------- | ------- |
| `bbbackend.state` | Install BigBlueButton to state | `present` | for updating BigBlueButton with this role use `latest` |

| `bbb_hostname` | Hostname for this BigBlueButton instance _(required)_ | `{{ ansible_fqdn }}` |
| `bbb_apt_mirror` | apt repo server for BigBlueButton packages | `https://ubuntu.bigbluebutton.org` | other value would be e.g. `https://packages-eu.bigbluebutton.org` |
| `bbb_letsencrypt_enable` | Enable letsencrypt/HTTPS | `yes` |
| `bbb_letsencrypt_email` | E-mail for use with letsencrypt | |
| `bbb_nginx_privacy` | only log errors not access | `yes` |
| `bbb_nginx_dh` | generate Diff-Hellmann for nginx | `yes` | same place like bbb-install.sh
| `bbb_coturn_enable` | enable installation of the TURN-server | `yes` |
| `bbb_coturn_server` | server name on coturn (realm) | `{{ bbb_hostname }}` |
| `bbb_coturn_port` | the port for the TURN-Server to use | `3443` |
| `bbb_coturn_port_tls` | the port for tls for the TURN-Server to use | `3443` |
| `bbb_coturn_secret` | Secret for the TURN-Server  _(required)_ | | can be generated with `openssl rand -hex 16`
| `bbb_turn_enable` | enable the use uf TURN in general | `yes` |
| `bbb_stun_servers` | a list of STUN-Server to use | `{{ bbb_hostname }}` | an array with key `server` - take a look in defaults/main.yml
| `bbb_ice_servers` | a list of RemoteIceCandidate for STUN | `[]` | in array with key `server`
| `bbb_turn_servers` | a list of TURN-Server to use | `{{ bbb_hostname }}` with `{{ bbb_coturn_secret }}` | take a look in defaults/main.yml
| `bbb_greenlight_hosts` | the hostname that greenlight is accessible from | `{{ bbb_hostname }}` |
| `bbb_greenlight_secret` | Secret for greenlight _(required when using greenlight)_ |  | can be generated with `openssl rand -hex 64`
| `bbb_greenlight_db_password` | Password for greenlight's database  _(required when using greenlight)_ | | can be generated with `openssl rand -hex 16`
| `bbb_greenlight_default_registration` | Registration option open(default), invite or approval
| `bbb_allow_mail_notifications`  | Set this to true if you want GreenLight to send verification emails upon the creation of a new account | `true` |
| `bbb_disable_recordings` | Disable options in gui to have recordings | `no` | [Recordings are running constantly in background](https://github.com/bigbluebutton/bigbluebutton/issues/9202) which is relevant as privacy relevant user data is stored
| `bbb_api_demos_enable` | enable installation of the api demos | `no` |
| `bbb_mute_on_start:` | start with muted mic on join | `no` |
| `bbb_app_log_level:` | set bigbluebutton log level | `DEBUG` |
| `bbb_meteor:` | overwrite settings in meteor | `{}` |
| `bbb_nodejs_version` | version of nodejs to be installed | `8.x` |
| `bbb_system_locale` | the system locale to use | `en_US.UTF-8` |
| `bbb_cpuschedule` | CPUSchedulingPolicy | `true` | Disable to fix [FreeSWITCH SETSCHEDULER error][bbb_cpuschedule] |
| `bbb_freeswitch_ipv6` | Enable IPv6 support in FreeSWITCH | `true` | Disable to fix [FreeSWITCH IPv6 error][bbb_freeswitch_ipv6] |
| `bbb_freeswitch_external_ip` | Set stun server for sip and rtp on FreeSWITCH | `stun:{{ (bbb_stun_servers | first).server }}` | WARNING: the value of the default freeswitch installation is `stun:stun.freeswitch.org` |
| `bbb_dialplan_quality` | Set quality of dailplan for FreeSWITCH | `cdquality` |
| `bbb_dialplan_energy_level` | Set energy level of dailplan for FreeSWITCH | `100` | only for selected profile `bbb_dialplan_quality`
| `bbb_dialplan_comfort_noise` | Set comfort noise of dailplan for FreeSWITCH | `1400` | only for selected profile `bbb_dialplan_quality`

## Example Playbook
This is an example, of how to use this role. Warning: the value of the Variables should be changed!
```yaml
tbd
```

## License
MIT
