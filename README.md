# Pizpalue distribution base

This composer package serves as a base to start new [typo3](https://typo3.org) projects based on
[pizpalue distribution](https://extensions.typo3.org/extension/pizpalue_distribution/).

It uses pizpalue version 12 (bootstrap 5) and TYPO3 version 11.

## Quick start

1. **Get packages**
   ```
   composer create-project buepro/typo3-pizpalue-distribution-base pizpalue
   ```

2. **Enter project directory**
   ```
   cd pizpalue
   ```

3. **Setup TYPO3**
   ```
   php vendor/bin/typo3cms install:setup \
   --no-interaction \
   --use-existing-database \
   --database-host-name="127.0.0.1" \
   --database-port="3306" \
   --database-name="db" \
   --database-user-name="db" \
   --database-user-password="db" \
   --admin-user-name="admin" \
   --admin-password="password" \
   --site-name="Pizpalue site" \
   --web-server-config="apache"
   ```

4. **Review `composer.json`**

   1. Enable platform check

      Depending on the hosting environment the platform check might be enabled:
      ```
      "platform-check": true,
      ```

   2. Define packages

      To have more control maintaining the site the composer configuration might be adjusted according the actual
      requirements. For this replace `"buepro/typo3-pizpalue-distribution": "^3.0.0"` with the required packages:
      ```
      "buepro/typo3-container-elements": "^3.0.0",
      "buepro/typo3-pizpalue": "^12.0.0",
      "buepro/typo3-user-pizpalue": "^2.0.0",
      "georgringer/news": "^9.1.0",
      "typo3/cms-base-distribution": "^11.5",
      "typo3/cms-core": "^11.5",
      "typo3/cms-indexed-search": "^11.5",
      "typo3/cms-lowlevel": "^11.5",
      "typo3/cms-recycler": "^11.5",
      "typo3/cms-redirects": "^11.5"
      ```
      > NOTE: Just add the needed packages. In many projects just `buepro/typo3-pizpalue` and
      `buepro/typo3-container-elements` are used.

      > NOTE: In case the extension `eventnews` is used the site package might need to have a dependency injection
      > configured. [See eventnews issue 132](https://github.com/georgringer/eventnews/issues/132#issuecomment-1051920269).
      > More information can be found in the
      > [pizpalue documentation](https://docs.typo3.org/p/buepro/typo3-pizpalue/main/en-us/Administration/Extensions/Eventnews.html)
      > (release dependent).

   3. Add repository for site package

      ```
      "repositories": [
         {
            "type": "vcs",
            "url": "../../git/user_pizpalue.git"
         }
      ],
      ```

6. **Finalize installation**

   After modifying the composer configuration finalize the installation:
   ```
   composer finalize-installation
   ```

7. **Update root template record**
   Not loaded extensions might still have their static template referenced in the root template record. This can result
   in incorrect rendering issues. To update the root template record open and save the template record on the root page.
