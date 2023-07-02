# cloudflare-ddns-for-synology
Using Cloudflare DDNS for Synology DSM 7.x

### Access Synology via SSH

1. Login to your DSM
2. Go to Control Panel > Terminal & SNMP > Enable SSH service
3. Use your client to access Synology via SSH.
4. Use your Synology admin account to connect.
5. Use Command `sudo -i` to Root

### Run commands in Synology

1. Download `cloudflare-ddns-v*.sh` from this repository to `/sbin/cloudflare-ddns-v*.sh`

## IP v4

```
wget https://raw.githubusercontent.com/insistent-afk/cloudflare-ddns-for-synology/main/cloudflare-ddns-v4.sh -O /sbin/cloudflare-ddns-v4.sh
```

2. Give others execute permission

```
chmod +x /sbin/cloudflare-ddns-v4.sh
```

3. Add `cloudflare-ddns-v4.sh` to Synology

```
cat >> /etc.defaults/ddns_provider.conf << 'EOF'
[Cloudflare IPv4]
        modulepath=/sbin/cloudflare-ddns-v4.sh
        queryurl=https://www.cloudflare.com
        website=https://www.cloudflare.com
EOF

```

enjoy

## IP v6

```
wget https://raw.githubusercontent.com/insistent-afk/cloudflare-ddns-for-synology/main/cloudflare-ddns-v6.sh -O /sbin/cloudflare-ddns-v6.sh
```

2. Give others execute permission

```
chmod +x /sbin/cloudflare-ddns-v6.sh
```

3. Add `cloudflare-ddns-v6.sh` to Synology

```
cat >> /etc.defaults/ddns_provider.conf << 'EOF'
[Cloudflare IPv6]
        modulepath=/sbin/cloudflare-ddns-v6.sh
        queryurl=https://www.cloudflare.com
        website=https://www.cloudflare.com
EOF

```

enjoy

## Get Cloudflare parameters

1. Go to your domain overview page and copy your zone ID.
2. Go to your profile > **API Tokens** > **Create Token**. It should have the permissions of `Zone > DNS > Edit`. Copy the api token.

### Setup DDNS

1. Login to your DSM
2. Go to Control Panel > External Access > DDNS > Add
3. Enter the following:
   - Service provider: `Cloudflare IPv*`
   - Hostname: `xxx.domainname.com`
   - Username/Email: `<Zone ID>`
   - Password Key: `<API Token>`

enjoy
