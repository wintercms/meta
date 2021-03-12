## Rules for Updating JS Dependencies in the Winter CMS Core:

1. Only use the Official Github Releases Repo or an Official CDN.

2. If getting the updated files from an official CDN, be careful of any '**map**' files linked in the bottom of the files. You may need to remove them or create a new link to avoid creating 404 errors.

3. Always prefer the unminified version of the files. They can be minified by Winter CMS itself and it's easier to test and fix unminified versions.

4. Scan the files before adding them for any forms of malware.

5. You can also check the '**known vulnerabilities**' database at Snyk before adding the updated files, to see if that version number has any issues, see link: https://snyk.io/vuln

6. Add **all** the files in the release, as new files and features that can enhance Winter CMS could be included.

7. Add the version number to the top of all the updated files in a commented out section, to make it easier for other people to do future updates.

8. Create a Github Patch, it makes testing easier. Please note your email address maybe displayed inside the patch and you may want to edit that bit out - to avoid possible spam from the internet. Note: **Add the Patch File separate and not inside the commit**.

9. Check the docs on the Winter CMS website, as there maybe a mention of the library in the docs, so do a quick check by visiting the github repo found here: https://github.com/wintercms/docs

## Process for updating JS Dependencies in Winter CMS:

1. Create the commit with the updates and create a Pull Request into the '**develop**' branch of the Winter CMS GitHub repo.

2. Submit for testing so that any conflicts and issues this new update may cause can be found and fixed.

3. If everything is fine the Pull Request will get a '**Status: Completed**' label.

4. Don't '**close**' the GitHub issue, because it will auto-close itself once the Pull Request has been '**merged**' and appears in the '**master**' branch.

## Other Helpful Tips Updating JS Depedencies in Winter CMS:

All packages should use '**Semantic Versioning**', this is useful to know when updating third-party packages and knowing how big the Testing/Updating process will be.

Take the following two examples:

### Example 1:

Current Version: **1.2.0**
Updated Version: **1.5.1**

Both Versions are '**Version One**' and therefore will require **little** effort for the Testing/Updating process.

### Example 2:

Current Version: **1.2.0**
Updated Version: **2.4.3**

The Current Version is '**Version One**' and the New Version will be '**Version Two**'. This means there will be **MAJOR** Changes to the code for the Testing/Updating process.

To learn more about Semantic Versioning you can see the spec found here: https://semver.org/

>**NOTE:** Winter CMS itself does not use Semantic Versioning.