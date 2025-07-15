   

 
Useful Links   
[https://hashcat.net/wiki/doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes "https://hashcat.net/wiki/doku.php?id=example_hashes")

[https://hashes.com/en/decrypt/hash](https://hashes.com/en/decrypt/hash "https://hashes.com/en/decrypt/hash")

|**Hash Type**|**Description / Example**|**Hashcat Mode**|
|---|---|---|
|**MD5**|`5f4dcc3b5aa765d61d8327deb882cf99`|`0`|
|**SHA1**|`5baa61e4c9b93f3f0682250b6cf8331b7ee68fd8`|`100`|
|**SHA256**|`5e884898da28047151d0e56f8dc6292773603d0d6aabbddbc8fba0f1c1e5f57f`|`1400`|
|**SHA512**|Long 128-character hex string|`1700`|
|HMAC-SHA512 (key = $pass)|94cb9e31137913665dbea7b058e10be5f050cc356062a2c9679ed0ad611964[...]28f82bf9f14ed82c1976|1750|
|**sha512crypt**|$652450745524507455245074552450745k5ka2p8bFuSmoVT1tzOyyuaREkkKBcCNqoDKzYiJL9RaE8yMnPgh2XzzF0NDrUhgrcLwg78xs1w5pJiypEdFX/|`1800`|
|**bcrypt**|`$2y$10$...`|`3200`|
|**NTLM**|Windows NT password hash|`1000`|
|**LM**|Legacy Windows (less secure)|`3000`|
|**MySQL 5.x (SHA1)**|Used in MySQL user auth|`300`|
|**MySQL 4.1 (double SHA1)**|`*94BDCEBE19083CE2A1F959FD02F964C7AF4CFC29`|`300`|
|**phpass (WordPress, Joomla)**|`$P$...` or `$H$...`|`400`|
|**WordPress ≥ v5 (bcrypt)**|`$P$...`, depending on settings|`400` or `3200`|
|**WPA/WPA2 (Wi-Fi Handshake)**|From `.cap` or `.hccapx` file|`2500` (deprecated) / `22000` (current)|
|**Kerberos 5, etype 23 (RC4)**|Windows Active Directory ticket|`13100`|

### Cracking Passwords with GPUs

Modern GPUs (Graphics Processing Units) have thousands of cores. They are specialised in digital image processing and accelerating computer graphics. Although they can’t do the same sort of work that a CPU can, they are very good at some mathematical calculations involved in hash functions. You can use a graphics card to crack many hash types quickly. Some hashing algorithms, such as Bcrypt, are designed so that hashing on a GPU does not provide any speed improvement over using a CPU; this helps them resist cracking.

### Cracking on VMs?

It’s worth mentioning that VMs (Virtual Machines) normally don’t have access to the host’s graphics card(s). Depending on the virtualisation software you are using, you can set this up, but it is cumbersome. Furthermore, performance degradation occurs as you use the CPU from a virtualised OS, and when your purpose is to crack a hash, you need every extra CPU cycle.

If you want to run [Hashcat](https://hashcat.net/hashcat/ "https://hashcat.net/hashcat/"), it’s best to run it on your host to make the most of your GPU, if available. If you prefer MS Windows, you are in luck; MS Windows builds are available on the website, and you can run it from PowerShell. You can get Hashcat working with OpenCL in a VM, but the speeds will likely be worse than cracking on your host.

[John the Ripper](https://www.openwall.com/john/ "https://www.openwall.com/john/") uses CPU by default and works in a VM out of the box, although you may get better speeds running it on the host OS to avoid any virtualisation overhead and make the most of your CPU cores and threads.

### Time to Crack Some Hashes

I’ll provide the hashes. Crack them. You can choose how. You’ll need to use online tools, [Hashcat](https://hashcat.net/hashcat/ "https://hashcat.net/hashcat/"), or [John the Ripper](https://www.openwall.com/john/ "https://www.openwall.com/john/"). Although you can use [online rainbow tables](https://hashes.com/ "https://hashes.com/") to solve the following, we strongly advise against doing that as this will restrict your learning experience. For the first three questions, using `hashcat` along with `rockyou.txt` is enough to find the answers.

Hashcat uses the following basic syntax: `hashcat -m <hash_type> -a <attack_mode> hashfile wordlist`, where:

- `-m <hash_type>` specifies the hash-type in numeric format. For example, `-m 1000` is for NTLM. Check the official documentation (`man hashcat`) and [example page](https://hashcat.net/wiki/doku.php?id=example_hashes "https://hashcat.net/wiki/doku.php?id=example_hashes") to find the hash type code to use.
- `-a <attack_mode>` specifies the attack-mode. For example, `-a 0` is for straight, i.e., trying one password from the wordlist after the other.
- `hashfile` is the file containing the hash you want to crack.
- `wordlist` is the security word list you want to use in your attack.

For example, `hashcat -m 3200 -a 0 hash.txt /usr/share/wordlists/rockyou.txt` will treat the hash as Bcrypt and try the passwords in the `rockyou.txt` file.

bcryte