Some software may remove uBlock Origin (uBO), but why is unclear. It could be that uBO contains the malware filter lists as part of its package. The reason is that I want uBO to be up and running with all filters without needing to download them at install time (the update process is automatic, and the filter lists will be updated in the background eventually).

Here is a list of software that is known to have removed uBO:

- Avira AntiVirus:
    - https://github.com/gorhill/uBlock/issues/882
    - https://github.com/gorhill/uBlock/issues/1074

    Report form: https://www.avira.com/en/analysis/submit/

- Bitdefender:
    - https://www.reddit.com/r/uBlockOrigin/comments/rdy62f/bitdefender_detects_ublock_origin_as_a_virus/
    - https://www.reddit.com/r/uBlockOrigin/comments/b0579i/bitdefender_detected_web_threat_from_ublockorigin/

    Report instructions: https://www.bitdefender.com/business/support/en/77209-151121-troubleshooting.html

- ClamAV (optionally with Immunet/Malware Patrol):
    - https://github.com/gorhill/uBlock/issues/2315
    - https://github.com/uBlockOrigin/uBlock-issues/issues/599
    - https://github.com/uBlockOrigin/uBlock-issues/issues/698
    - https://github.com/uBlockOrigin/uBlock-issues/issues/700

    Report forms:
    - ClamAV: https://www.clamav.net/reports/fp
    - Immunet: https://www.immunet.com/false_positive
    - Malware Patrol: `fp (@) malwarepatrol.net`

- Junkware Removal Tool:
    - https://github.com/gorhill/uBlock/issues/882#issuecomment-154879542

    Support forum: https://forums.malwarebytes.com/forum/122-false-positives/

    Update: Malwarebytes has [discontinued](https://forums.malwarebytes.com/topic/213402-junkware-removal-tool-to-be-discontinued/) the Junkware Removal Tool, and false positives will probably not get fixed.

- SpyHunter 4:
    - https://github.com/gorhill/uBlock/issues/1009
    - [Of interest](https://web.archive.org/web/20161125064326/http://www.bleepingcomputer.com/forums/t/550005/spyhunter-vs-malwarebytes-vs-iobit/#entry3491488): "In _my opinion_ SpyHunter is a **dubious program** with a high rate of [false positives](https://www.mywot.com/en/scorecard/enigmasoftware.com)". [via archive.org]