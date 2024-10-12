# Django on Ubuntu

## System files and directories

| Type      | Name         | Path                                       |
| :-------- | :----------- | :----------------------------------------- |
| Directory | home         | [`/opt/<proj>`](#home)                     |
| Directory | venv         | `/opt/<proj>/venv/`                        |
| Directory | code         | `/opt/<proj>/<proj>/`                      |
| Directory | data         | `/opt/<proj>/data/`                        |
| Directory | logs         | `/var/log/<owner>/<proj>`                  |
| File      | apache2 site | `/etc/apache2/sites-available/<proj>.conf` |
| Directory | supervisor   | `/etc/supervisor/conf.d/`                  |

## Home

```
/opt/<proj>
├── venv
├── <proj>
│   ├── apps
│   ├── common
│   │   ├── css
│   │   └── js
│   ├── project
│   │   └── settings
│   ├── qux
│   ├── requirements
│   └── templates
└── data
```

