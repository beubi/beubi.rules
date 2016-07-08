---
currentMenu: composer
---

# ** Composer Guidelines **

### Adding packages

The recommended way to add packages is to do a composer require:

```
composer require package1
```
This command will try to get the best version for you but you are free to change it latter.
If you want the package to go to the require-dev just append the command with `--dev`

### Bootstrapping

When you want to bootstrap a project you MUST do a composer install
```
composer install
```

### Updating packages

To update a package you MUST do a composer udpate.
You can add the packages you want next to the command.
```
composer update package1 package2 package3
```

### Fix lock
Sometimes you might want to update the references of your composer.lock file. E.g. because some package has updated its source name.
You can do that with a composer update --lock
```
composer update --lock
```

### Versions

Versions SHOULD block new features and allow bug fixes.
When this is not possible, you are free to choose the best strategy. Remember that in some cases you might want to block the version to a commit hash.

E.g. of safe versions:
* `~1.2`      (>=1.2 <2.0.0)
* `~1.2.3`    (>=1.2.3 <1.3.0)

The `~` char makes the last digit to go up.
