# writeup kioptrix level 1
  This Kioptrix VM Image are easy challenges. The object of the game is to acquire root access via any means possible (except actually hacking the VM server or player). The purpose of these games are to learn the basic tools and techniques in vulnerability assessment and exploitation. There are more ways then one to successfully complete the challenges.
  
# Download vm-machine from vulnhub website:
link: https://www.vulnhub.com/entry/kioptrix-level-1-1,22/ .

# Solution:
  1-At the beginning, we need to perform ping sweep to discover network devices that alive.
    command: sudo nmap -sn 192.168.1.0/24
    
   <img src="https://github.com/BassamMaged/vulnhub_write-ups/blob/master/Kazam_screenshot_00000.png" style="max-width:100%;">
   
   
  2- after finding target IP, we need to perform port scan and banner graabbing over TCP through nmap.
    command: sudo nmap -sS -sV -O 192.168.1.104 -p-
