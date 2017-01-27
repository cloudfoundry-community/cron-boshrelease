# Improvements

Cron entries can now have custom environment variables specified in their configuration
via the `variables` map:

```
properties:
  cron:
    entries:
    - command: my-cron-command
      minute: 0
      hour: *
      day: *
      month: *
      wday:*
      user: root
      variables:
        DEBUG: true
```

# Acknowledgments

Many thanks to @jmcarp and a hat tip to @cnelson for this feature!
