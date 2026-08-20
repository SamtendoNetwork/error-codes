# Error Codes

Translated JSON files for known error codes used by the Wii U and 3DS.

## Formatting

We have a script called `format-translation-files.mjs` which will:

-   Ensure all translation strings end with a period
-   If only one of "long_x" or "short_x" is present, the other will be set to the same value so they're equal at least (ideally, long_x should be a more detailed version of short_x)

You can run it on the **directory** containing the translation files you want to format. Example usage:

```sh
$ node format-translation-files.mjs .\data\022
```

## Path Structure

There are paths: modules and codes. The `data` folder contains the error code data. The root of the `data` folder contains the modules. Inside each module folder are the translation files for the module and folders for each of the module's error codes. Inside each module error code folder are the translation files for the error. Example path structure:

```
data
├── 102
│   ├── en_US.json
│   ├── 2482
│   │   └── en_US.json
│   ├── 2483
│   │   └── en_US.json
│   └── etc
└── 103
    ├── en_US.json
    ├── 0504
    │   └── en_US.json
    ├── 1101
    │   └── en_US.json
    └── etc
```

### Module translation file fields

| Name          | Description                                       |
| ------------- | ------------------------------------------------- |
| `name`        | The name of the sysmodule                         |
| `description` | A short description of what the sysmodule handles |
| `system`      | The system the sysmodule is for                   |

### Error translation file fields

| Name                | Description                                                                                                                          |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `name`              | The internal name of the error. Not all errors have an internal name. If missing, `Unknown`                                          |
| `message`           | The message exactly as it appears **_on the console_**. If there is no relevant translation for the message, use the `en_US` version |
| `short_description` | A short description of the error. Intended to be used by the Discord bot. Plain text                                                 |
| `long_description`  | A longer, more detailed, description of the error. Intended to be used by the website. Markdown                                      |
| `short_solution`    | A short solution for the error. Intended to be used by the Discord bot. Plain text                                                   |
| `long_solution`     | A longer, more detailed, solution for the error. Intended to be used by the website. Markdown                                        |
| `support_link`      | Link to a relevant support page for the error. Typically the website, but does not have to be                                        |

### Utility functions

The main purpose of this repository is to maintain the JSON translation files. However 2 utility functions are also included for JavaScript/TypeScript projects.

-   `getModuleInfo(sysmodule, locale)` - Returns the module information for the locale, or `null` if not found
-   `getErrorInfo(sysmodule, code, locale)` - Returns the error information (including the module information) for the locale. Returns null if either the module or error code is not found
-   `getAllErrors()` - Returns an array of all error codes for all modules in the form `MODULE-CODE`

Credits to Pretendo for original repo.
