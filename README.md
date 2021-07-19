# rails-schema-merge-driver

A basic Git merge driver for Rails' db/schema.rb top-version conflicts.

This is inspired by [this gist](https://gist.github.com/jeromedalbert/afab24e80102b41d75d5f5538f1459c4), and slightly improved upon.

## Installing

1. Grab the [merge driver file](https://raw.githubusercontent.com/deliciousinsights/rails-schema-merge-driver/main/merge-db-schema-top-versions) and save it someplace.  This is a Ruby script intended to run in POSIX environments that support hashbang syntaxes and the `/usr/bin/env` command.  In particular, this will not work straight from Cmd or Powershell as-is.
2. Make it executable (e.g. `chmod a+x merge-db-schemas-top-version`).
3. In a relevant Git attributes file (e.g. `$HOME/.config/git/attributes` or your project's `.git/attributes`), add the following:

```gitconfig
db/schema.rb merge=railsschema
```

4. In a relevant Git config file (e.g. `$HOME/.gitconfig` or your project's `.git/config`), add the following:

```gitconfig
[merge "railsschema"]
  name = Rails schema.db merge driver
  driver = "path/to/the/file" %O %A %B %L %P
```

_(For instance, if you saved the merge driver in `/home/tdd/perso/bin`, this would read `driver = /home/tdd/perso/bin/merge-db-schemas-top-version %O %A %B %L %P`)._

There! Now you should benefit from this merging for merges and rebases.  It likely b0rks on stash applies, tho.  Contributions welcome!

## Learning more

- [git merge-file](https://git-scm.com/docs/git-merge-file)
- [Git attributes](https://git-scm.com/docs/gitattributes)
- [Custom merge drivers](https://git-scm.com/docs/gitattributes#_defining_a_custom_merge_driver)
