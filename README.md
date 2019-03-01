# Metasploit Cheat Sheet

***
Metasploit Project is a computer security project which provide information about vulnerabilities. Help in the development of penetration tests and IDS signatures, metasploit is very popular tool used by pentest experts.

### Metasploit :

- ###### Search for module:

```
msf > search [regex]
```

- ###### Specify and exploit to use:

```
msf > use exploit/[ExploitPath]
```

- ###### Specify a Payload to use:

```
msf > set PAYLOAD [PayloadPath]
```

- ###### Show options for the current modules:

```
msf > show options
```

- ###### Set options:

```
msf > set [Option] [Value]
```

- ###### Start exploit:

```
msf > exploit 
```
***

### Useful Auxiliary Modules


- ###### Port Scanner:

```
msf > use auxiliary/scanner/portscan/tcp
msf > set RHOSTS 192.168.10.0/24
msf > run
```

- ###### DNS Enumeration:

```
msf > use auxiliary/gather/dns_enum
msf > set DOMAIN target.tgt
msf > run
```

- ###### FTP Server:

```
msf > use auxiliary/server/ftp
msf > set FTPROOT /tmp/ftproot
msf > run
```
