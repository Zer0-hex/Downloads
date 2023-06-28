

![Escape](https://www.hackthebox.com/storage/avatars/55cfc512922d7f56cee2428252edf040.png)

## Overview 

|      Name       |  Template  |
| :-------------: | :--------: |
|  Release Date   | 2023-06-28 |
| Write-up Author |  Zer0-hex  |
| Machine Author  |  Zer0-hex  |
|   Difficulty    |   Medium   |
|    User Flag    |            |
|    Root Flag    |            |



## Relevant Skills

1. File Upload
2. Local File Include
3. vim to shell

## Recon as Nmap

`ports=$(nmap -p- --min-rate=1000 -T4 127.0.0.1 | grep -oE '(^[0-9][^/tcp]*)' | tr '\n' ',')`
`nmap -p$ports -sV -sC -O 127.0.0.1 -oN nmap.txt`

```sh
┌──(root㉿Zer0-hex)-[~/Notes/Template]
└─# nmap -p$ports -sV -sC -O 127.0.0.1 -oN nmap.txt
Starting Nmap 7.94 ( https://nmap.org ) at 2023-06-28 11:33 CST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000064s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    SimpleHTTPServer 0.6 (Python 3.11.2)
|_http-server-header: SimpleHTTP/0.6 Python/3.11.2
|_http-title: Directory listing for /
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 2.6.X
OS CPE: cpe:/o:linux:linux_kernel:2.6.32
OS details: Linux 2.6.32
Network Distance: 0 hops

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.85 seconds
```

## Enumerate

### SMB Enumerate

> Port: 139 389 445 636

`enum4linux -a/-A 127.0.0.1`

```sh
$ enum4linux -A <ip>
```

### Web

> HTTP Web Server, Port Like: 80 443 81 8080 8443 4443 8081

- Finger

#### `whatweb`

```
┌──(root㉿Zer0-hex)-[~/Notes/Template]
└─# whatweb 127.0.0.1
http://127.0.0.1 [200 OK] Country[RESERVED][ZZ], HTML5, HTTPServer[SimpleHTTP/0.6 Python/3.11.2], IP[127.0.0.1], Python[3.11], Title[Directory listing for /]
```

- Directory Enumerate

`dirb http://127.0.0.1`

`dirsearch -u http://127.0.0.1 -r`

`gobuster dir -w ... -u http://127.0.0.1`

```
┌──(root㉿Zer0-hex)-[~/Notes/Template]
└─# dirsearch -u http://127.0.0.1

  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10927

Target: http://127.0.0.1/

[14:52:52] Starting:

Task Completed
```

- Directory Crawling `katana -u http://www.example.com`

```sh

```

- Vuln scan

```sh
$ nikto -h http://www.example.com/
$ nuclei -u https://example.com/
```

### wordlist

- pass.list

```
```

- user.list

```

```

- hash.list

```
```



## Shell as user1



## Shell as user2



### Shell as root

>  Save Screenshot for Flag or Proof

