# vaultwarden-backup-nginx-le

This is docker-compose that run [vaultwarden](https://github.com/dani-garcia/vaultwarden) with [nginx-le](https://github.com/nginx-le/nginx-le) reverse proxy and backups by [vaultwarden-backup](https://github.com/ttionya/vaultwarden-backup/).

It has two version: with ipv6 support and without it. The main difference is ipv6 version can log client ipv6 addresses but requaired some additional actions to setup.

Steps of runing:

### 1 step

Only when used ipv6 version.

You need to run [ipv6nat](https://github.com/robbertkl/docker-ipv6nat)

```
docker run -d --name ipv6nat --privileged --network host --restart unless-stopped -v /var/run/docker.sock:/var/run/docker.sock:ro -v /lib/modules:/lib/modules:ro robbertkl/ipv6nat
```

### 2 step

You need to [configure](https://github.com/ttionya/vaultwarden-backup/#backup) rclone. RemoteName will be used later.

I recomended to use [clouds](https://rclone.org/overview/) that save token or api key like OneDrive and Dropbox and not like mega where used your username and password.

### 3 step

Change docker-compose.yml with your own settings.

You remote name(you can also change other env settings of vaultwarden-backup as you like):
```
RCLONE_REMOTE_NAME: 'BitwardenBackup'
```
You email and domain(recomended to use real email, let encrypt will send you warning if something will goes wrong and Certificate not updated automatic.)
```
LE_EMAIL: 'name@example.com'
LE_FQDN: 'www.example.com'
```

I planed to write somefing more about [vaultwarden-backup](https://github.com/ttionya/vaultwarden-backup/) becourse I find information about setup and recover it not compleatly clear for me and spend a lot time to do it.
