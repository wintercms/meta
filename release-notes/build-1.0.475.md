# Build 1.0.475

Security improvements backported from v1.1:

## Security Improvements
- Improved reliability of the CMS Safe Mode feature. See https://github.com/wintercms/winter/security/advisories/GHSA-q37h-jhf3-85cj for more information.
- Improved reliability of `Winter\Storm\Database\Attach\File->fromData()`. See https://github.com/octobercms/october/security/advisories/GHSA-8v7h-cpc2-r8jp for more information.

## Dependencies
- The Winter core modules now report via composer that they replace the associated version of the October core modules to improve compatibility with the October ecosystem.
