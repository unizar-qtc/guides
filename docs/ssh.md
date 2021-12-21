# Remote connections (SSH)

To remotely connect to the clusters and desktop computers is advised to use
*Secure SHell (ssh)* and related applications.


## Hosts
Directions (DNS/IP addresses) for the BIFI's access point computers. Only *bridge* can be access from non-unauthorized IPs.

|  HOST NAME |       DIRECTION        |
| :--------: | ---------------------- |
| *bridge*   | bridge.bifi.unizar.es  |
| *memento*  | memento.bifi.unizar.es |
| *cierzo*   | cierzo.bifi.unizar.es  |


## Interactive connection
```
ssh {user}@{host}
```
To access to a remote terminal, being *{user}* your user name in the destination computer and *{host}* one of the direction described in [host](#hosts).  Example: `ssh usuario@bridge.bifi.unizar.es`

If graphical interfaces are planned to be imported, the option `-X` must also be used. This method usually works out-of-the-box for Linux/Mac systems but may need support from *Xming* in Windows. Example: `ssh -X usuario@bridge.bifi.unizar.es`

#### Windows terminal
In Windows computers, an access to a terminal is not usually straightforward. In that case, a ssh client must be installed, such as [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html). Nevertheless, a better alternative is to use [WSL v1](https://docs.microsoft.com/es-es/windows/wsl/install-win10), as it provides a whole linux-terminal experience (only available on Windows 10).

#### Android terminal
[JuiceSSH](https://juicessh.com/) app can be used to remotely access from your mobile phone, although this is strongly disadvised as it promotes work addiction. Disconnect!


## Copy files/folders
#### Terminal
The command `scp` has an analogous behaviour to `cp` but trough ssh connections. To copy between computers, the user name and host directions must be specified before the file/folder to send/retrieve and separated by a colon, in the same way done in an [interactive connection](#interactive-connection). To copy folders and its contents, the `-r` option is necessary.

Send / Receive:
```
scp {file} {user}@{host}:{destination}
scp {user}@{host}:{file} {destination}
```

The files and folders paths can be given in absolute or relative directions. In the latter case, by default the remote directory is your `$HOME`.

Examples: `scp usuario@memento.bifi.unizar.es:my_calcs/calc.log .`\
`scp -r calcs usuario@cierzo.bifi.unizar.es:/home/usuario/my_calcs/`

#### Graphical clients
Some desktop applications can offer a more friendly experience with remote file/folder management. Among the freely available, [FileZilla](https://filezilla-project.org/) for Linux and [WinSCP](https://winscp.net/) for Windows are suggested. Tunneling to access *memento*/*cierzo* can be set in the latter.

## Advanced features
These advanced features are only available for Linux (and WSL).

#### *config* file
A text-file named `config` can be created inside the `.ssh` folder at `$HOME` and it will be read every time a ssh service is employed. This file can be used to make alias to hosts and direct tunneling through a server.

Template *config* file. Replace the *{user}* with your remote user name.
```
 Host bridge
   HostName bridge.bifi.unizar.es
   User {user}

 Host memento
   ProxyCommand ssh -q bridge nc -q0 memento.bifi.unizar.es 22
   User {user}

 Host cierzo
   ProxyCommand ssh -q bridge nc -q0 cierzo.bifi.unizar.es 22
   User {user}

 Host *
   ServerAliveInterval 60
   ServerAliveCountMax 10000
   ForwardX11 no
```

After this *config* is set, the alias defined after `Host` can be used to connect directly. The user can also be omitted and the one specified in the file will be used. For *memento* and *cierzo*, a tunnel will be set through *bridge*, so they can be reached directly. If a graphical feedback is necessary, edit to `ForwardX11 yes`. Examples: `ssh cierzo` `scp calc.com memento:my_calcs`


#### Log in without password
Public keys can be avoid entering a password at every connection. It's important to set this **only in a restricted personal account**, as can it will facilitate any unauthorized access.

1. Generate a public/private RSA key pair, type `ssh-keygen` (default options are usually OK)
2. Copy the public key to the remote server, use `ssh-copy-id {user}@{host}`

After that, the entering password step will be skipped. For the tunnel, it may be necessary to generate a key at *bridge* and copy it to *memento*/*cierzo*.
