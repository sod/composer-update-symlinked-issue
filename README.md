# composer monorepo linked dependency update issue testcase

Environment: macOS 10.12.5 / composer 1.4.2

### Precondition
I have `mylib` and `myapp`, both in one repository. `myapp` requires `mylib`. It's configured via `repositories => type: "path"` to be symlinked.

### What I want to do
Update a dependency in `mylib`. Then update `mylib` in `myapp`

### How I expected it to work
```sh
cd mylib;
composer require jms/metadata 1.6
cd ../myapp;
composer update mylib
# jms/metadata is still on old version in myapp 1.3
```

### How it actually works
```sh
cd mylib;
composer require jms/metadata 1.6
cd ../myapp;
rm -r vendor # remove vendor
composer update mylib jms/metadata # update both
# jms/metadata was updated to 1.6
```
