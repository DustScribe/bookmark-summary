Title: GitHub - MHSanaei/3x-ui: Xray panel supporting multi-protocol multi-user expire day & traffic & ip limit (Vmess & Vless & Trojan &  ShadowSocks & Wireguard)

URL Source: https://github.com/MHSanaei/3x-ui

Markdown Content:
[English](https://github.com/MHSanaei/3x-ui/blob/main/README.md) | [中文](https://github.com/MHSanaei/3x-ui/blob/main/README.zh_CN.md) | [Español](https://github.com/MHSanaei/3x-ui/blob/main/README.es_ES.md) | [Русский](https://github.com/MHSanaei/3x-ui/blob/main/README.ru_RU.md)

![Image 64: 3x-ui](https://github.com/MHSanaei/3x-ui/raw/main/media/3x-ui-light.png)

**An Advanced Web Panel • Built on Xray Core**

[![Image 65](https://camo.githubusercontent.com/f3c85cbf6b0ff2a67bd565355191f1552b939153091fa6261ce66034bc13a835/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f762f72656c656173652f6d6873616e6165692f33782d75692e737667)](https://github.com/MHSanaei/3x-ui/releases) [![Image 66](https://camo.githubusercontent.com/d923732d7db96e86969d4085ce211fe362f215f39fe8d130df5cea2d8a4590e4/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f616374696f6e732f776f726b666c6f772f7374617475732f6d6873616e6165692f33782d75692f72656c656173652e796d6c2e737667)](https://github.com/MHSanaei/3x-ui#) [![Image 67: GO Version](https://camo.githubusercontent.com/4e837f965c6010b0cd4e1196654b980d3cbcfe97435321e9c8e2938cd31a4ad4/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f676f2d6d6f642f676f2d76657273696f6e2f6d6873616e6165692f33782d75692e737667)](https://github.com/MHSanaei/3x-ui#) [![Image 68: Downloads](https://camo.githubusercontent.com/a7d9fffcb1ca99a37a576e6b63c5de247fe58c832ee21e3c419bd230625d5414/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f646f776e6c6f6164732f6d6873616e6165692f33782d75692f746f74616c2e737667)](https://github.com/MHSanaei/3x-ui#) [![Image 69: License](https://camo.githubusercontent.com/245b08d301885416953f248444a5153bf9180b535714bfc2012261b480b57aeb/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f6c6963656e73652d47504c25323056332d626c75652e7376673f6c6f6e6743616368653d74727565)](https://www.gnu.org/licenses/gpl-3.0.en.html)

> **Disclaimer:** This project is only for personal learning and communication, please do not use it for illegal purposes, please do not use it in a production environment

**If this project is helpful to you, you may wish to give it a**🌟

[![Image 70: Image](https://github.com/MHSanaei/3x-ui/raw/main/media/buymeacoffe.png)](https://buymeacoffee.com/mhsanaei)

*   USDT (TRC20): `TXncxkvhkDWGts487Pjqq1qT9JmwRUz8CC`
*   MATIC (polygon): `0x41C9548675D044c6Bfb425786C765bc37427256A`
*   LTC (Litecoin): `ltc1q2ach7x6d2zq0n4l0t4zl7d7xe2s6fs7a3vspwv`

Install & Upgrade
-----------------

[](https://github.com/MHSanaei/3x-ui#install--upgrade)

```
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```

Install legacy Version (we don't recommend)
-------------------------------------------

[](https://github.com/MHSanaei/3x-ui#install-legacy-version-we-dont-recommend)

To install your desired version, use following installation command. e.g., ver `v1.7.9`:

```
VERSION=v1.7.9 && bash <(curl -Ls "https://raw.githubusercontent.com/mhsanaei/3x-ui/$VERSION/install.sh") $VERSION
```

SSL Certificate
---------------

[](https://github.com/MHSanaei/3x-ui#ssl-certificate)

Click for SSL Certificate details

### ACME

[](https://github.com/MHSanaei/3x-ui#acme)

To manage SSL certificates using ACME:

1.  Ensure your domain is correctly resolved to the server.
    
2.  Run the `x-ui` command in the terminal, then choose `SSL Certificate Management`.
    
3.  You will be presented with the following options:
    
    *   **Get SSL:** Obtain SSL certificates.
    *   **Revoke:** Revoke existing SSL certificates.
    *   **Force Renew:** Force renewal of SSL certificates.
    *   **Show Existing Domains:** Display all domain certificates available on the server.
    *   **Set Certificate Paths for the Panel:** Specify the certificate for your domain to be used by the panel.

### Certbot

[](https://github.com/MHSanaei/3x-ui#certbot)

To install and use Certbot:

apt-get install certbot -y
certbot certonly --standalone --agree-tos --register-unsafely-without-email -d yourdomain.com
certbot renew --dry-run

### Cloudflare

[](https://github.com/MHSanaei/3x-ui#cloudflare)

The management script includes a built-in SSL certificate application for Cloudflare. To use this script to apply for a certificate, you need the following:

*   Cloudflare registered email
*   Cloudflare Global API Key
*   The domain name must be resolved to the current server through Cloudflare

**How to get the Cloudflare Global API Key:**

1.  Run the `x-ui` command in the terminal, then choose `Cloudflare SSL Certificate`.
2.  Visit the link: [Cloudflare API Tokens](https://dash.cloudflare.com/profile/api-tokens).
3.  Click on "View Global API Key" (see the screenshot below): [![Image 71](https://github.com/MHSanaei/3x-ui/raw/main/media/APIKey1.PNG)](https://github.com/MHSanaei/3x-ui/blob/main/media/APIKey1.PNG)
4.  You may need to re-authenticate your account. After that, the API Key will be shown (see the screenshot below): [![Image 72](https://github.com/MHSanaei/3x-ui/raw/main/media/APIKey2.png)](https://github.com/MHSanaei/3x-ui/blob/main/media/APIKey2.png)

When using, just enter your `domain name`, `email`, and `API KEY`. The diagram is as follows: [![Image 73](https://github.com/MHSanaei/3x-ui/raw/main/media/DetailEnter.png)](https://github.com/MHSanaei/3x-ui/blob/main/media/DetailEnter.png) 

Manual Install & Upgrade
------------------------

[](https://github.com/MHSanaei/3x-ui#manual-install--upgrade)

Click for manual install details

#### Usage

[](https://github.com/MHSanaei/3x-ui#usage)

1.  To download the latest version of the compressed package directly to your server, run the following command:

ARCH=$(uname -m)
case "${ARCH}" in
  x86\_64 | x64 | amd64) XUI\_ARCH="amd64" ;;
  i\*86 | x86) XUI\_ARCH="386" ;;
  armv8\* | armv8 | arm64 | aarch64) XUI\_ARCH="arm64" ;;
  armv7\* | armv7) XUI\_ARCH="armv7" ;;
  armv6\* | armv6) XUI\_ARCH="armv6" ;;
  armv5\* | armv5) XUI\_ARCH="armv5" ;;
  s390x) echo 's390x' ;;
  \*) XUI\_ARCH="amd64" ;;
esac

wget https://github.com/MHSanaei/3x-ui/releases/latest/download/x-ui-linux-${XUI\_ARCH}.tar.gz

2.  Once the compressed package is downloaded, execute the following commands to install or upgrade x-ui:

ARCH=$(uname -m)
case "${ARCH}" in
  x86\_64 | x64 | amd64) XUI\_ARCH="amd64" ;;
  i\*86 | x86) XUI\_ARCH="386" ;;
  armv8\* | armv8 | arm64 | aarch64) XUI\_ARCH="arm64" ;;
  armv7\* | armv7) XUI\_ARCH="armv7" ;;
  armv6\* | armv6) XUI\_ARCH="armv6" ;;
  armv5\* | armv5) XUI\_ARCH="armv5" ;;
  s390x) echo 's390x' ;;
  \*) XUI\_ARCH="amd64" ;;
esac

cd /root/
rm -rf x-ui/ /usr/local/x-ui/ /usr/bin/x-ui
tar zxvf x-ui-linux-${XUI\_ARCH}.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-\* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui

Install with Docker
-------------------

[](https://github.com/MHSanaei/3x-ui#install-with-docker)

Click for Docker details

#### Usage

[](https://github.com/MHSanaei/3x-ui#usage-1)

1.  **Install Docker:**
    
    bash <(curl -sSL https://get.docker.com)
    
2.  **Clone the Project Repository:**
    
    git clone https://github.com/MHSanaei/3x-ui.git
    cd 3x-ui
    
3.  **Start the Service:**
    

Add `--pull always` flag to make docker automatically recreate container if a newer image is pulled. See [https://docs.docker.com/reference/cli/docker/container/run/#pull](https://docs.docker.com/reference/cli/docker/container/run/#pull) for more info.

**OR**

docker run -itd \\
   -e XRAY\_VMESS\_AEAD\_FORCED=false \\
   -v $PWD/db/:/etc/x-ui/ \\
   -v $PWD/cert/:/root/cert/ \\
   --network=host \\
   --restart=unless-stopped \\
   --name 3x-ui \\
   ghcr.io/mhsanaei/3x-ui:latest

4.  **Update to the Latest Version:**
    
    cd 3x-ui
    docker compose down
    docker compose pull 3x-ui
    docker compose up -d
    
5.  **Remove 3x-ui from Docker:**
    
    docker stop 3x-ui
    docker rm 3x-ui
    cd --
    rm -r 3x-ui
    

Nginx Settings
--------------

[](https://github.com/MHSanaei/3x-ui#nginx-settings)

Click for Reverse Proxy Configuration

#### Nginx Reverse Proxy

[](https://github.com/MHSanaei/3x-ui#nginx-reverse-proxy)

location / {
    proxy\_set\_header X-Forwarded-For $proxy\_add\_x\_forwarded\_for;
    proxy\_set\_header X-Forwarded-Proto $scheme;
    proxy\_set\_header Host $http\_host;
    proxy\_set\_header X-Real-IP $remote\_addr;
    proxy\_set\_header Range $http\_range;
    proxy\_set\_header If-Range $http\_if\_range; 
    proxy\_redirect off;
    proxy\_pass http://127.0.0.1:2053;
}

#### Nginx sub-path

[](https://github.com/MHSanaei/3x-ui#nginx-sub-path)

*   Ensure that the "URI Path" in the `/sub` panel settings is the same.
*   The `url` in the panel settings needs to end with `/`.

location /sub {
    proxy\_set\_header X-Forwarded-For $proxy\_add\_x\_forwarded\_for;
    proxy\_set\_header X-Forwarded-Proto $scheme;
    proxy\_set\_header Host $http\_host;
    proxy\_set\_header X-Real-IP $remote\_addr;
    proxy\_set\_header Range $http\_range;
    proxy\_set\_header If-Range $http\_if\_range; 
    proxy\_redirect off;
    proxy\_pass http://127.0.0.1:2053;
}

Recommended OS
--------------

[](https://github.com/MHSanaei/3x-ui#recommended-os)

*   Ubuntu 20.04+
*   Debian 11+
*   CentOS 8+
*   OpenEuler 22.03+
*   Fedora 36+
*   Arch Linux
*   Parch Linux
*   Manjaro
*   Armbian
*   AlmaLinux 8.0+
*   Rocky Linux 8+
*   Oracle Linux 8+
*   OpenSUSE Tubleweed
*   Amazon Linux 2023
*   Windows x64

Supported Architectures and Devices
-----------------------------------

[](https://github.com/MHSanaei/3x-ui#supported-architectures-and-devices)

Click for Supported Architectures and devices detailsOur platform offers compatibility with a diverse range of architectures and devices, ensuring flexibility across various computing environments. The following are key architectures that we support:

*   **amd64**: This prevalent architecture is the standard for personal computers and servers, accommodating most modern operating systems seamlessly.
    
*   **x86 / i386**: Widely adopted in desktop and laptop computers, this architecture enjoys broad support from numerous operating systems and applications, including but not limited to Windows, macOS, and Linux systems.
    
*   **armv8 / arm64 / aarch64**: Tailored for contemporary mobile and embedded devices, such as smartphones and tablets, this architecture is exemplified by devices like Raspberry Pi 4, Raspberry Pi 3, Raspberry Pi Zero 2/Zero 2 W, Orange Pi 3 LTS, and more.
    
*   **armv7 / arm / arm32**: Serving as the architecture for older mobile and embedded devices, it remains widely utilized in devices like Orange Pi Zero LTS, Orange Pi PC Plus, Raspberry Pi 2, among others.
    
*   **armv6 / arm / arm32**: Geared towards very old embedded devices, this architecture, while less prevalent, is still in use. Devices such as Raspberry Pi 1, Raspberry Pi Zero/Zero W, rely on this architecture.
    
*   **armv5 / arm / arm32**: An older architecture primarily associated with early embedded systems, it is less common today but may still be found in legacy devices like early Raspberry Pi versions and some older smartphones.
    
*   **s390x**: This architecture is commonly used in IBM mainframe computers and offers high performance and reliability for enterprise workloads.
    

Languages
---------

[](https://github.com/MHSanaei/3x-ui#languages)

*   English
*   Persian
*   Traditional Chinese
*   Simplified Chinese
*   Japanese
*   Russian
*   Vietnamese
*   Spanish
*   Indonesian
*   Ukrainian
*   Turkish
*   Português (Brazil)

Features
--------

[](https://github.com/MHSanaei/3x-ui#features)

*   System Status Monitoring
*   Search within all inbounds and clients
*   Dark/Light theme
*   Supports multi-user and multi-protocol
*   Supports protocols, including VMESS, VLESS, Trojan, Shadowsocks, Dokodemo-door, Socks, HTTP, wireguard
*   Supports XTLS native Protocols, including RPRX-Direct, Vision, REALITY
*   Traffic statistics, traffic limit, expiration time limit
*   Customizable Xray configuration templates
*   Supports HTTPS access panel (self-provided domain name + SSL certificate)
*   Supports One-Click SSL certificate application and automatic renewal
*   For more advanced configuration items, please refer to the panel
*   Fixes API routes (user setting will be created with API)
*   Supports changing configs by different items provided in the panel.
*   Supports export/import database from the panel

Default Panel Settings
----------------------

[](https://github.com/MHSanaei/3x-ui#default-panel-settings)

Click for default settings details

### Username, Password, Port, and Web Base Path

[](https://github.com/MHSanaei/3x-ui#username-password-port-and-web-base-path)

If you choose not to modify these settings, they will be generated randomly (this does not apply to Docker).

**Default Settings for Docker:**

*   **Username:** admin
*   **Password:** admin
*   **Port:** 2053

### Database Management:

[](https://github.com/MHSanaei/3x-ui#database-management)

You can conveniently perform database Backups and Restores directly from the panel.

*   **Database Path:**
    *   `/etc/x-ui/x-ui.db`

### Web Base Path

[](https://github.com/MHSanaei/3x-ui#web-base-path)

1.  **Reset Web Base Path:**
    
    *   Open your terminal.
    *   Run the `x-ui` command.
    *   Select the option to `Reset Web Base Path`.
2.  **Generate or Customize Path:**
    
    *   The path will be randomly generated, or you can enter a custom path.
3.  **View Current Settings:**
    
    *   To view your current settings, use the `x-ui settings` command in the terminal or `View Current Settings` in `x-ui`

### Security Recommendation:

[](https://github.com/MHSanaei/3x-ui#security-recommendation)

*   For enhanced security, use a long, random word in your URL structure.

**Examples:**

*   `http://ip:port/*webbasepath*/panel`
*   `http://domain:port/*webbasepath*/panel`

WARP Configuration
------------------

[](https://github.com/MHSanaei/3x-ui#warp-configuration)

Click for WARP configuration details

#### Usage

[](https://github.com/MHSanaei/3x-ui#usage-2)

**For versions `v2.1.0` and later:**

WARP is built-in, and no additional installation is required. Simply turn on the necessary configuration in the panel.

IP Limit
--------

[](https://github.com/MHSanaei/3x-ui#ip-limit)

Click for IP limit details

#### Usage

[](https://github.com/MHSanaei/3x-ui#usage-3)

**Note:** IP Limit won't work correctly when using IP Tunnel.

*   **For versions up to `v1.6.1`:**
    *   The IP limit is built-in to the panel

**For versions `v1.7.0` and newer:**

To enable the IP Limit functionality, you need to install `fail2ban` and its required files by following these steps:

1.  Run the `x-ui` command in the terminal, then choose `IP Limit Management`.
    
2.  You will see the following options:
    
    *   **Change Ban Duration:** Adjust the duration of bans.
    *   **Unban Everyone:** Lift all current bans.
    *   **Check Logs:** Review the logs.
    *   **Fail2ban Status:** Check the status of `fail2ban`.
    *   **Restart Fail2ban:** Restart the `fail2ban` service.
    *   **Uninstall Fail2ban:** Uninstall Fail2ban with configuration.
3.  Add a path for the access log on the panel by setting `Xray Configs/log/Access log` to `./access.log` then save and restart xray.
    

*   **For versions before `v2.1.3`:**
    
    *   You need to set the access log path manually in your Xray configuration:
        
        "log": {
          "access": "./access.log",
          "dnsLog": false,
          "loglevel": "warning"
        },
        
*   **For versions `v2.1.3` and newer:**
    
    *   There is an option for configuring `access.log` directly from the panel.

Telegram Bot
------------

[](https://github.com/MHSanaei/3x-ui#telegram-bot)

Click for Telegram bot details

#### Usage

[](https://github.com/MHSanaei/3x-ui#usage-4)

The web panel supports daily traffic, panel login, database backup, system status, client info, and other notification and functions through the Telegram Bot. To use the bot, you need to set the bot-related parameters in the panel, including:

*   Telegram Token
*   Admin Chat ID(s)
*   Notification Time (in cron syntax)
*   Expiration Date Notification
*   Traffic Cap Notification
*   Database Backup
*   CPU Load Notification

**Reference syntax:**

*   `30 \* \* \* \* \*` - Notify at the 30s of each point
*   `0 \*/10 \* \* \* \*` - Notify at the first second of each 10 minutes
*   `@hourly` - Hourly notification
*   `@daily` - Daily notification (00:00 in the morning)
*   `@weekly` - weekly notification
*   `@every 8h` - Notify every 8 hours

### Telegram Bot Features

[](https://github.com/MHSanaei/3x-ui#telegram-bot-features)

*   Report periodic
*   Login notification
*   CPU threshold notification
*   Threshold for Expiration time and Traffic to report in advance
*   Support client report menu if client's telegram username added to the user's configurations
*   Support telegram traffic report searched with UUID (VMESS/VLESS) or Password (TROJAN) - anonymously
*   Menu-based bot
*   Search client by email (only admin)
*   Check all inbounds
*   Check server status
*   Check depleted users
*   Receive backup by request and in periodic reports
*   Multi-language bot

### Setting up Telegram bot

[](https://github.com/MHSanaei/3x-ui#setting-up-telegram-bot)

*   Start [Botfather](https://t.me/BotFather) in your Telegram account: [![Image 74: Botfather](https://github.com/MHSanaei/3x-ui/raw/main/media/botfather.png)](https://github.com/MHSanaei/3x-ui/blob/main/media/botfather.png)
    
*   Create a new Bot using /newbot command: It will ask you 2 questions, A name and a username for your bot. Note that the username has to end with the word "bot". [![Image 75: Create new bot](https://github.com/MHSanaei/3x-ui/raw/main/media/newbot.png)](https://github.com/MHSanaei/3x-ui/blob/main/media/newbot.png)
    
*   Start the bot you've just created. You can find the link to your bot here. [![Image 76: token](https://github.com/MHSanaei/3x-ui/raw/main/media/token.png)](https://github.com/MHSanaei/3x-ui/blob/main/media/token.png)
    
*   Enter your panel and config Telegram bot settings like below: [![Image 77: Panel Config](https://github.com/MHSanaei/3x-ui/raw/main/media/panel-bot-config.png)](https://github.com/MHSanaei/3x-ui/blob/main/media/panel-bot-config.png)
    

Enter your bot token in input field number 3. Enter the user ID in input field number 4. The Telegram accounts with this id will be the bot admin. (You can enter more than one, Just separate them with ,)

*   How to get Telegram user ID? Use this [bot](https://t.me/useridinfobot), Start the bot and it will give you the Telegram user ID. [![Image 78: User ID](https://github.com/MHSanaei/3x-ui/raw/main/media/user-id.png)](https://github.com/MHSanaei/3x-ui/blob/main/media/user-id.png) 

API Routes
----------

[](https://github.com/MHSanaei/3x-ui#api-routes)

Click for API routes details

#### Usage

[](https://github.com/MHSanaei/3x-ui#usage-5)

*   [API Documentation](https://www.postman.com/hsanaei/3x-ui/collection/q1l5l0u/3x-ui)
*   `/login` with `POST` user data: `{username: '', password: ''}` for login
*   `/panel/api/inbounds` base for following actions:

| Method | Path | Action |
| --- | --- | --- |
| `GET` | `"/list"` | Get all inbounds |
| `GET` | `"/get/:id"` | Get inbound with inbound.id |
| `GET` | `"/getClientTraffics/:email"` | Get Client Traffics with email |
| `GET` | `"/getClientTrafficsById/:id"` | Get client's traffic By ID |
| `GET` | `"/createbackup"` | Telegram bot sends backup to admins |
| `POST` | `"/add"` | Add inbound |
| `POST` | `"/del/:id"` | Delete Inbound |
| `POST` | `"/update/:id"` | Update Inbound |
| `POST` | `"/clientIps/:email"` | Client Ip address |
| `POST` | `"/clearClientIps/:email"` | Clear Client Ip address |
| `POST` | `"/addClient"` | Add Client to inbound |
| `POST` | `"/:id/delClient/:clientId"` | Delete Client by clientId\* |
| `POST` | `"/updateClient/:clientId"` | Update Client by clientId\* |
| `POST` | `"/:id/resetClientTraffic/:email"` | Reset Client's Traffic |
| `POST` | `"/resetAllTraffics"` | Reset traffics of all inbounds |
| `POST` | `"/resetAllClientTraffics/:id"` | Reset traffics of all clients in an inbound |
| `POST` | `"/delDepletedClients/:id"` | Delete inbound depleted clients (-1: all) |
| `POST` | `"/onlines"` | Get Online users ( list of emails ) |

\*- The field `clientId` should be filled by:

*   `client.id` for VMESS and VLESS
    
*   `client.password` for TROJAN
    
*   `client.email` for Shadowsocks
    
*   [![Image 79: Run In Postman](https://camo.githubusercontent.com/05724525de78fafb0de980822719a00ca640a42359111762466b7a7904752f76/68747470733a2f2f72756e2e7073746d6e2e696f2f627574746f6e2e737667)](https://app.getpostman.com/run-collection/5146551-dda3cab3-0e33-485f-96f9-d4262f437ac5?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D5146551-dda3cab3-0e33-485f-96f9-d4262f437ac5%26entityType%3Dcollection%26workspaceId%3Dd64f609f-485a-4951-9b8f-876b3f917124)
    

Environment Variables
---------------------

[](https://github.com/MHSanaei/3x-ui#environment-variables)

Click for environment variables details

#### Usage

[](https://github.com/MHSanaei/3x-ui#usage-6)

| Variable | Type | Default |
| --- | --- | --- |
| XUI\_LOG\_LEVEL | `"debug"` | `"info"` | `"warn"` | `"error"` | `"info"` |
| XUI\_DEBUG | `boolean` | `false` |
| XUI\_BIN\_FOLDER | `string` | `"bin"` |
| XUI\_DB\_FOLDER | `string` | `"/etc/x-ui"` |
| XUI\_LOG\_FOLDER | `string` | `"/var/log"` |

Example:

XUI\_BIN\_FOLDER="bin" XUI\_DB\_FOLDER="/etc/x-ui" go build main.go

Preview
-------

[](https://github.com/MHSanaei/3x-ui#preview)

  ![Image 80: 3x-ui](https://github.com/MHSanaei/3x-ui/raw/main/media/01-overview-light.png)  ![Image 81: 3x-ui](https://github.com/MHSanaei/3x-ui/raw/main/media/02-inbounds-light.png)  ![Image 82: 3x-ui](https://github.com/MHSanaei/3x-ui/raw/main/media/03-add-inbound-light.png)  ![Image 83: 3x-ui](https://github.com/MHSanaei/3x-ui/raw/main/media/04-add-client-light.png)  ![Image 84: 3x-ui](https://github.com/MHSanaei/3x-ui/raw/main/media/05-settings-light.png)  ![Image 85: 3x-ui](https://github.com/MHSanaei/3x-ui/raw/main/media/06-configs-light.png) ![Image 86: 3x-ui](https://github.com/MHSanaei/3x-ui/raw/main/media/07-bot-light.png)

A Special Thanks to
-------------------

[](https://github.com/MHSanaei/3x-ui#a-special-thanks-to)

*   [alireza0](https://github.com/alireza0/)

Acknowledgment
--------------

[](https://github.com/MHSanaei/3x-ui#acknowledgment)

*   [Iran v2ray rules](https://github.com/chocolate4u/Iran-v2ray-rules) (License: **GPL-3.0**): _Enhanced v2ray/xray and v2ray/xray-clients routing rules with built-in Iranian domains and a focus on security and adblocking._
*   [Russia v2ray rules](https://github.com/runetfreedom/russia-v2ray-rules-dat) (License: **GPL-3.0**): _This repository contains automatically updated V2Ray routing rules based on data on blocked domains and addresses in Russia._

Stargazers over Time
--------------------

[](https://github.com/MHSanaei/3x-ui#stargazers-over-time)

[![Image 87: Stargazers over time](https://camo.githubusercontent.com/8fa1512f57433b2887e90199b348c497dfbac6f4dcd1c36a84ac25cd171d8774/68747470733a2f2f7374617263686172742e63632f4d4853616e6165692f33782d75692e7376673f76617269616e743d6164617074697665)](https://starchart.cc/MHSanaei/3x-ui)
