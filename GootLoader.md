---
title: Facebook
source: https://www.facebook.com/photo/?fbid=1192414096202754&set=a.524653139645523
author:
published:
created: 2026-01-22
description:
tags:
  - clippings
  - secpar
---
GootLoader is back. This week, researchers discovered their newest trick: a way to make security tools completely blind. Your antivirus scans the ZIP file. Nothing found. WinRAR tries to open it. Fails. 7-Zip tries. Also fails. Corrupted file, right? But when you double-click it, Windows opens it just fine. And now you're infected. ![🧐](https://static.xx.fbcdn.net/images/emoji.php/v9/t7c/2/16/1f9d0.png)  
  
The trick is simple but brilliant. They take 500 to 1000 ZIP files and glue them together into one massive file. Most analysis tools read ZIP files from the beginning. They hit the first archive, see garbage, and crash. But here is the thing about ZIP files. They are actually read from the END. The "End of Central Directory" record tells the reader where to find the actual content. Windows knows this. It skips all the junk, finds the last valid archive, and happily extracts the malware.  
  
But they did not stop there.  
  
They deliberately break specific bytes in the file structure:  
→ The End of Central Directory is missing two critical bytes that parsers need  
→ The "Disk Number" fields are randomized, so tools think the ZIP is split across multiple disks that do not exist  
→ The CRC32 checksum is wrong on purpose, making tools think the file is corrupted  
  
Open the ZIP with 7-Zip and it extracts a harmless .TXT file. Open the exact same ZIP with Windows Explorer and it extracts a malicious .JS file. Same archive, different tools, completely different results. Automated security analysis sees a text file and moves on. The victim sees JavaScript and runs it.  
  
Every single download is unique. When a victim clicks that download button, the browser receives an XOR-encrypted blob. The browser then BUILDS the ZIP file itself by decoding and copying that blob hundreds of times. No two victims ever receive the same file. Hash-based detection is completely useless. Network-based detection sees encrypted garbage, not a ZIP file.  
  
They abuse WordPress sites and hide their payload in the comment submission endpoint at /wp-comments-post.php. When someone clicks download, the malicious data comes from what looks like a normal WordPress function.  
  
Before the victim even sees the filename, they have already been tricked. The webpage shows "Contract\_Template.pdf" but the source code contains complete gibberish like "›μI€vSO₽\*'Oaμ==€‚‚33O3". They embed a custom WOFF2 font file directly in the JavaScript using Z85 encoding, a Base85 variant that compresses the 32KB font into 40K of code. The font metadata says the letter "O" maps to the glyph named "O". But they swapped the actual vector paths. The shape that renders on screen is completely different. Security tools scanning the source code see nonsense. The browser renders a clean filename.  
  
The infection chain moves fast.  
  
→ You search for "contract template" or "NDA agreement" on Google  
→ A compromised WordPress site appears in the top results  
→ Looks like a helpful forum, someone posted exactly what you need  
→ You click download, the ZIP opens fine in Windows  
→ Inside is a JavaScript file that looks like a legal document  
→ You double-click it  
  
Game over.  
  
The JavaScript runs via wscript.exe from the Temp folder. It drops a shortcut file in the Startup folder, but not pointing directly to the malware. The shortcut points to ANOTHER shortcut in a random folder, which then points to a second JavaScript file. They use NTFS 8.3 short filenames like FILENA~1.js to hide the real path. Legacy naming from 1993 being used to evade modern security tools.  
  
Those shortcut files have keyboard hotkeys assigned. CTRL+ALT+M or CTRL+ALT+G. If you accidentally hit that key combination at any point, the malware executes again.  
  
Within 20 minutes, the attackers deploy the Supper backdoor, a SOCKS5 proxy that gives them remote access. They start reconnaissance immediately. Kerberoasting. SPN scanning. Looking for paths to the Domain Controller.  
  
Within 17 hours, they own it. Sometimes just one hour.  
  
The group behind this has been around since 2014. They started as GootKit, a banking trojan targeting banks across Europe. In 2019 they suffered a data leak and went quiet. In 2020 they came back as GootLoader, pivoting from stealing bank credentials to selling network access to ransomware gangs.  
  
Security researchers track them as Storm-0494, Hive0127, or UNC2565 depending on who you ask. But here is the thing about attribution. In cybersecurity, attribution is one of the hardest problems. IP addresses can be spoofed. Tools can be shared. Languages in code can be faked. What we know for sure is how the malware works, not necessarily who is behind it.  
  
What researchers do agree on is that they do not deploy ransomware themselves. They sell access. Their current partner is Vanilla Tempest, also known as Vice Society, the group behind Rhysida ransomware that has been hitting hospitals across the US. McLaren Health Care. NHS Scotland. Healthcare is their favorite target.  
  
A security researcher operating under the name "Gootloader" tracked this group for years. Filing abuse reports. Contacting hosting providers. Getting their infrastructure taken down. On March 31, 2025, his efforts paid off. The entire GootLoader operation went dark.  
  
Seven months later, they came back with all these new tricks.  
  
In previous years, GootLoader malware made up 11 percent of all malware that bypassed other security tools. One in ten. That is how good they are at evading detection.  
  
The ransomware connections run deep. GootLoader has delivered initial access for REvil, BlackCat, Rhysida, INC Ransomware, Zeppelin, and Quantum Locker.  
  
Who are they targeting now?  
  
→ Law firms searching for legal templates  
→ Healthcare organizations  
→ Finance  
→ Education  
→ Manufacturing  
  
Mostly in the US, UK, Australia, Canada, Germany, and France.  
  
How to protect yourself.  
  
Change your Group Policy so JavaScript files open in Notepad instead of executing. This one change stops the entire attack chain. If someone double-clicks a malicious JS file, they just see code instead of running malware.  
  
Block wscript.exe and cscript.exe from running downloaded content if your business does not need them.  
  
Watch for these warning signs:  
→ wscript.exe running JavaScript from the Temp folder  
→ Shortcut files appearing in the Startup folder pointing to strange locations  
→ CScript spawning PowerShell which spawns another PowerShell  
→ Unusual Active Directory enumeration activity  
→ Shortcuts with keyboard hotkeys assigned  
  
The speed of this attack is what makes it dangerous. From first click to domain takeover in under a day. Most organizations cannot detect lateral movement that fast.  
  
Expel released a YARA rule to detect these malformed ZIP files. It looks for more than 100 occurrences of the same local file header and more than 100 End of Central Directory records. Normal ZIP files have one of each.  
  
Security tools see a corrupted file. Windows sees an opportunity to help. And that gap is exactly where GootLoader lives.  
  
This is a perfect example of why understanding how attackers think matters more than memorizing tool names. I cover attack chains like this, from initial access through privilege escalation to maintaining persistence, in my ethical hacking course:  
  
→ [https://www.udemy.com/.../ethical-hacking-complete.../...](https://l.facebook.com/l.php?u=https%3A%2F%2Fwww.udemy.com%2Fcourse%2Fethical-hacking-complete-course-zero-to-expert%2F%3FcouponCode%3DJANUARY26%26fbclid%3DIwZXh0bgNhZW0CMTAAYnJpZBExTGxHQU52dFNONlV4ZjdSdHNydGMGYXBwX2lkEDIyMjAzOTE3ODgyMDA4OTIAAR5PhXeHKAhBP4LvYHUF4_yq40lMFyWzYm4QN12lqmUDHeTvFxj_a43Xa58EVQ_aem_I-NuPvNSZTzbYK8f4gbIIw&h=AT22ihv4YdSQEcIB4FK89f6V1zKe5RMe0i04lqaDkRkIzHk36hmZZCdO9JA1-vn8KwOUIviwfVJrC--EUyosK4dxCCKtqfp1GqMGAJrMJUC992jLHNFg2Rj8un_9sNuw8yhCG6Q-HClDyYMOqxZLt0fysDebJDqOmzc&__tn__=-UK*F&c[0]=AT2pSk9BfIXRKHoyJjlDtGk2Dyy6Ph39HA_xdKKJ4KqSPhELgprk3-0uwmhWMoRhhnRBSnEbsl8WuetwkTjY5wUkm7Gu7LKq-h6_d8FkXRCC-qC053izrpGNmWplDIq45qrhlyR201W_suby01TQL4nsNGmxIW1NyPw6X7B3J6SeIisrXvnCJ_61P3UgZ5OIDVRg5Fko3XFP0G5S-gy_iPp_eUUVbmo)  
  
(The link supports me directly as the instructor!)  
  
Hacking is not a hobby but a way of life. ![🎯](https://static.xx.fbcdn.net/images/emoji.php/v9/t4f/2/16/1f3af.png)  
  
You can read the whole article here:  
→ [https://hackingpassion.com/gootloader-zip-evasion-2026/](https://hackingpassion.com/gootloader-zip-evasion-2026/?fbclid=IwZXh0bgNhZW0CMTAAYnJpZBExTGxHQU52dFNONlV4ZjdSdHNydGMGYXBwX2lkEDIyMjAzOTE3ODgyMDA4OTIAAR7s-o6TEsIkZ5ic5khAleGjBN7kxazuXBToIa1C2HOdtybpPqf2QYob1mAk3g_aem_G6Xp0XtSrfLDsubCBKIQ0g)  
  
[#EthicalHacking](https://www.facebook.com/hashtag/ethicalhacking?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F) [#GootLoader](https://www.facebook.com/hashtag/gootloader?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F) [#Malware](https://www.facebook.com/hashtag/malware?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F) [#Ransomware](https://www.facebook.com/hashtag/ransomware?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F) [#CyberSecurity](https://www.facebook.com/hashtag/cybersecurity?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F) [#InfoSec](https://www.facebook.com/hashtag/infosec?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F) [#ThreatIntelligence](https://www.facebook.com/hashtag/threatintelligence?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F) [#WindowsSecurity](https://www.facebook.com/hashtag/windowssecurity?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F) [#JavaScript](https://www.facebook.com/hashtag/javascript?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F) [#SEOPoisoning](https://www.facebook.com/hashtag/seopoisoning?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F) [#Rhysida](https://www.facebook.com/hashtag/rhysida?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F) [#Healthcare](https://www.facebook.com/hashtag/healthcare?__eep__=6&__cft__[0]=AZZHcB37SHk_FP0bGZ_c4pLLRsBEw-Bt4RwWLRhw0ZtsPF7XWDXlV9yVy-DU9IuqZJD2cMkVh0eth8R299OyHLcxwYDV5fKBIU_aXHzIzISwJ7E5sU0Zb5Pi3NjvvXoa1GxZ8KNifasISLw1F_zHHJp_ApCQ2sA39fE-XO1kv5IAaSuElaMnZx-WMfst3d7mBKY86PHoHD1fTXBCQJlCb2H-&__tn__=*NK*F)  
  
Research & writing: Jolanda de Koff | [HackingPassion.com](http://hackingpassion.com/?fbclid=IwZXh0bgNhZW0CMTAAYnJpZBExTGxHQU52dFNONlV4ZjdSdHNydGMGYXBwX2lkEDIyMjAzOTE3ODgyMDA4OTIAAR6GTaC2QNPqL6z7ZICI3wgHGWCGyktJSWrPk4pHkX_5mVdxmA0VgXAjoJeV3g_aem_IXnA-5Vm5LdgpTDjhGbvig)  
Sharing is fine. Copying without credit is not.

See less

![](https://www.facebook.com/photo/www.w3.org/2000/svg'%20viewBox='0%200%2016%2016'%3E%3Cpath%20d='M16.0001%207.9996c0%204.418-3.5815%207.9996-7.9995%207.9996S.001%2012.4176.001%207.9996%203.5825%200%208.0006%200C12.4186%200%2016%203.5815%2016%207.9996Z'%20fill='url(%23paint0_linear_15251_63610)'/%3E%3Cpath%20d='M16.0001%207.9996c0%204.418-3.5815%207.9996-7.9995%207.9996S.001%2012.4176.001%207.9996%203.5825%200%208.0006%200C12.4186%200%2016%203.5815%2016%207.9996Z'%20fill='url(%23paint1_radial_15251_63610)'/%3E%3Cpath%20d='M16.0001%207.9996c0%204.418-3.5815%207.9996-7.9995%207.9996S.001%2012.4176.001%207.9996%203.5825%200%208.0006%200C12.4186%200%2016%203.5815%2016%207.9996Z'%20fill='url(%23paint2_radial_15251_63610)'%20fill-opacity='.5'/%3E%3Cpath%20d='M7.3014%203.8662a.6974.6974%200%200%201%20.6974-.6977c.6742%200%201.2207.5465%201.2207%201.2206v1.7464a.101.101%200%200%200%20.101.101h1.7953c.992%200%201.7232.9273%201.4917%201.892l-.4572%201.9047a2.301%202.301%200%200%201-2.2374%201.764H6.9185a.5752.5752%200%200%201-.5752-.5752V7.7384c0-.4168.097-.8278.2834-1.2005l.2856-.5712a3.6878%203.6878%200%200%200%20.3893-1.6509l-.0002-.4496ZM4.367%207a.767.767%200%200%200-.7669.767v3.2598a.767.767%200%200%200%20.767.767h.767a.3835.3835%200%200%200%20.3835-.3835V7.3835A.3835.3835%200%200%200%205.134%207h-.767Z'%20fill='%23fff'/%3E%3Cdefs%3E%3CradialGradient%20id='paint1_radial_15251_63610'%20cx='0'%20cy='0'%20r='1'%20gradientUnits='userSpaceOnUse'%20gradientTransform='rotate(90%20.0005%208)%20scale(7.99958)'%3E%3Cstop%20offset='.5618'%20stop-color='%230866FF'%20stop-opacity='0'/%3E%3Cstop%20offset='1'%20stop-color='%230866FF'%20stop-opacity='.1'/%3E%3C/radialGradient%3E%3CradialGradient%20id='paint2_radial_15251_63610'%20cx='0'%20cy='0'%20r='1'%20gradientUnits='userSpaceOnUse'%20gradientTransform='rotate(45%20-4.5257%2010.9237)%20scale(10.1818)'%3E%3Cstop%20offset='.3143'%20stop-color='%2302ADFC'/%3E%3Cstop%20offset='1'%20stop-color='%2302ADFC'%20stop-opacity='0'/%3E%3C/radialGradient%3E%3ClinearGradient%20id='paint0_linear_15251_63610'%20x1='2.3989'%20y1='2.3999'%20x2='13.5983'%20y2='13.5993'%20gradientUnits='userSpaceOnUse'%3E%3Cstop%20stop-color='%2302ADFC'/%3E%3Cstop%20offset='.5'%20stop-color='%230866FF'/%3E%3Cstop%20offset='1'%20stop-color='%232B7EFF'/%3E%3C/linearGradient%3E%3C/defs%3E%3C/svg%3E)

![](https://www.facebook.com/photo/www.w3.org/2000/svg'%20viewBox='0%200%2016%2016'%3E%3Cg%20clip-path='url(%23clip0_15251_63610)'%3E%3Cpath%20d='M15.9972%207.9996c0%204.418-3.5815%207.9996-7.9996%207.9996-4.418%200-7.9996-3.5816-7.9996-7.9996S3.5796%200%207.9976%200c4.4181%200%207.9996%203.5815%207.9996%207.9996Z'%20fill='url(%23paint0_linear_15251_63610)'/%3E%3Cpath%20d='M15.9973%207.9992c0%204.4178-3.5811%207.9992-7.9987%207.9992C3.5811%2015.9984%200%2012.417%200%207.9992S3.5811%200%207.9986%200c4.4176%200%207.9987%203.5814%207.9987%207.9992Z'%20fill='url(%23paint1_radial_15251_63610)'/%3E%3Cpath%20d='M15.9972%207.9996c0%204.418-3.5815%207.9996-7.9996%207.9996-4.418%200-7.9996-3.5816-7.9996-7.9996S3.5796%200%207.9976%200c4.4181%200%207.9996%203.5815%207.9996%207.9996Z'%20fill='url(%23paint2_radial_15251_63610)'%20fill-opacity='.8'/%3E%3Cpath%20fill-rule='evenodd'%20clip-rule='evenodd'%20d='M5.6144%2010.8866c.159-1.8461%201.127-2.887%202.382-2.887%201.2551%200%202.2231%201.0418%202.3822%202.887.1591%201.8461-.7342%203.1127-2.3821%203.1127-1.648%200-2.5412-1.2666-2.3821-3.1127Z'%20fill='%234B280E'/%3E%3Cellipse%20cx='11.1978'%20cy='5.6997'%20rx='1.3999'%20ry='1.6999'%20fill='%231C1C1D'/%3E%3Cellipse%20cx='4.7979'%20cy='5.6997'%20rx='1.3999'%20ry='1.6999'%20fill='%231C1C1D'/%3E%3Cpath%20fill-rule='evenodd'%20clip-rule='evenodd'%20d='M12.3528%203.166a1.4744%201.4744%200%200%200-1.8591-.3279.4.4%200%201%201-.3976-.6941c.9527-.5457%202.1592-.333%202.8678.5056a.4.4%200%200%201-.6111.5163ZM5.4998%202.8381a1.4744%201.4744%200%200%200-1.859.3278.4.4%200%200%201-.6111-.5162c.7085-.8387%201.915-1.0514%202.8677-.5057a.4.4%200%200%201-.3976.6941Z'%20fill='%23E0761A'/%3E%3C/g%3E%3Cdefs%3E%3CradialGradient%20id='paint1_radial_15251_63610'%20cx='0'%20cy='0'%20r='1'%20gradientUnits='userSpaceOnUse'%20gradientTransform='matrix(0%207.9992%20-7.99863%200%207.9986%207.9992)'%3E%3Cstop%20offset='.5637'%20stop-color='%23FF5758'%20stop-opacity='0'/%3E%3Cstop%20offset='1'%20stop-color='%23FF5758'%20stop-opacity='.1'/%3E%3C/radialGradient%3E%3CradialGradient%20id='paint2_radial_15251_63610'%20cx='0'%20cy='0'%20r='1'%20gradientUnits='userSpaceOnUse'%20gradientTransform='rotate(45%20-4.5262%2010.9226)%20scale(10.1818)'%3E%3Cstop%20stop-color='%23FFF287'/%3E%3Cstop%20offset='1'%20stop-color='%23FFF287'%20stop-opacity='0'/%3E%3C/radialGradient%3E%3ClinearGradient%20id='paint0_linear_15251_63610'%20x1='2.3979'%20y1='2.3999'%20x2='13.5973'%20y2='13.5993'%20gradientUnits='userSpaceOnUse'%3E%3Cstop%20stop-color='%23FFF287'/%3E%3Cstop%20offset='1'%20stop-color='%23F68628'/%3E%3C/linearGradient%3E%3CclipPath%20id='clip0_15251_63610'%3E%3Cpath%20fill='%23fff'%20d='M-.002%200h15.9992v15.9992H-.002z'/%3E%3C/clipPath%3E%3C/defs%3E%3C/svg%3E)

All reactions:

1.6K 1.6K