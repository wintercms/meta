# Build 1.1.11

## Security improvements

- Improved the Twig security policy (blocked methods that write, delete, or modify records and attributes in Database/Eloquent and Halcyon models; blocked access to the theme datasource; prevented extensions from being created or directly interacted with). See https://github.com/wintercms/winter/security/advisories/GHSA-xhw3-4j3m-hq53 for more information.
