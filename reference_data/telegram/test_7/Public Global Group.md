2026-08-04 14:30:31, **S F**: How do I figure out if the sync for HA did actually work? When does it get triggered to be synced? Especially if you sync the users and groups? Does it sync the auth backend configs as well?

2026-08-04 14:47:55, **Abolfazl**: you can figure that out via configuring an alias or firewall rule for example and then checking your backup (s-la-ve) firewall to see if that contains it as well or not, if it does then it works, if it doesn't it has not worked

2026-08-04 14:51:08, **Abolfazl**: about users and groups, do you mean users and groups from pfsense itself or have you installed the freeradius package and you mean that? for everything outside of packages, i'm 100 percent sure that the sync works, for packages i'm not quite sure currently but they should work as well, i have not worked with freeradius package myself and use other AAA options outside of pfsense but have used the snort package and its configuration can be synced but it's per package, like snort has a configuration for it in the pages it adds when you install its package

2026-08-04 15:06:03, **S F**:

![photo_924@04-08-2026_12-06-03.jpg](<./photo_924@04-08-2026_12-06-03.jpg>)

> I'm talking about these settings:

2026-08-04 15:07:36, **Abolfazl**: should transfer

2026-08-04 15:07:48, **Abolfazl**: while HA and xmlrpc sync is active

2026-08-04 15:10:48, **S F**: Thank you. Including the Settings and Authentication Servers?

2026-08-07 10:51:12, **Grigory**:

![photo_925@07-08-2026_07-51-12.jpg](<./photo_925@07-08-2026_07-51-12.jpg>)

> Hi everyone!I'm having an issue with an IPsec tunnel between two pfSense boxes. The tunnel stays up for about 5 minutes and then drops and reconnects.The settings on both sides are identical and left at their defaults (encryption algorithms, lifetimes, etc.). Could anyone suggest which settings I should look into? I'm sure someone has run into this before.
