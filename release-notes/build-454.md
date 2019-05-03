# Build 454:

## API Changes:
- Moved RichEditor extending JS plugins into their own compiled file to eleminate the need to have the DRM vendor files present in order to build October's specific JS add-ons to the RichEditor

## Bug Fixes:
- Fixed issue where CSRF protection would prevent uploads directly in the RichEditor from succeeding by including the CSRF token in those requests
- Fixed issue with scrolling backend lists on mobile devices
- Fixed issue where the subject and / or user password in the user welcome email could be HTML encoded
- Fixed typo in FormWidget's JS & CSS stub files

## Translation Improvements:
- Improved Finnish translation