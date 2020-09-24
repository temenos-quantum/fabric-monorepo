# Visualizer Monorepo

In most cases the Visualizer project is placed at the root of the source code repository —e.g.: 

```
Repo root
    │
    ├── .gitignore   <- [Git stuff]
    ├── controllers
    ├── forms
    ├── i18n.json
    │
    │   ... [more Visualizer stuff]
    │
    ├── themes
    ├── userwidgets
    └── web
```

However, another approach is to store the Visualizer project along with the Fabric application and any other related projects in the same source code repository, where each occupies its own subfolder —e.g.: 

```
Repo root
    │
    ├── .gitignore   <- [Git stuff]
    └── path
        └── to
            └── FooApp
                ├── controllers
                ├── forms
                ├── i18n.json
                │
                │   ... [more Visualizer stuff]
                │
                ├── themes
                ├── userwidgets
                └── web
```
If this is your case, then you may use this field to specify its path relative to the repository’s root —i.e.: `path/to/FooApp`.
