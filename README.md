# Laravel Tinker Reload Mod

A mod that adds saving and reloading to Laravel tinker.

## Setup
1. Add `tinkerReloadMod.php` to the root directory of your Laravel project.
1. Run `php artisan tinker tinkerReloadMod.php`.
1. Now from the tinker shell run `eval(SETUP_TINKER_RELOAD_MOD)`
1. Run `chmod +x tinker` to mark the new script as executable
1. From now on you will start tinker with `./tinker`

## Tools
- Use `eval(RELOAD)` to reload the current session
- Use `eval(EXIT_MOD)` to exit and clear the session

## Use Example

### Without the Mod
Say you are working with a user in tinker:
```php
>$joe = User::where('username', 'joe')->first()
>$joe->fullName
    JoeSmith // Oh no! Theres a bug!
```

In normal Tinker you would have to fix the bug, close the session, reopen the session, and then rerun the query to get `$joe` again!
This makes interactive development difficult and you will find your self `Ctrl+C` to close, press up to reload previous commands, and repeat.

### With the Mod
```php
>$joe = User::where('username', 'joe')->first()
>$joe->fullName
    JoeSmith // Oh no! Theres a bug!
```

Fix the bug:
```php
function getFullNameAttribute() {
    return $this->first_name . ' ' . $this->last_name;
}
```

Now back to tinker:
```php
>$joe = User::where('username', 'joe')->first()
>$joe->fullName
    JoeSmith // Oh no! Theres a bug!
>eval(RELOAD)

   INFO  Goodbye.

Psy Shell v0.12.4 (PHP 8.4.1 — cli) by Justin Hileman
Tinker Reload Mod
Vars: $joe
> $joe
= App\Models\User {#5175
    name: "Joe",
  }
> $joe->fullName
    Joe Smith
```

This allows the developer to constantly test and tweak and develop interactivley! 
