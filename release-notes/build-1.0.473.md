# Build 1.0.473

## Security Improvements
- Improved password reset flow by no longer throwing an error message if the provided email address doesn't exist in the system.
- Tightened up the permission checking logic by requiring strict type matches.
- Removed `xml` from the list of default allowed extensions to upload, can be added back through the configuration if required.