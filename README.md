# BOSH Release for cron

This BOSH release is intended to allow you to add generic crontab
entries to any existing BOSH deployment by colocating the `cron`
job alongside your VMs.

### Colocation Instructions

To colocate, ensure your job has the `cron` template specified:

```
instance_groups:
- name: myjob
  jobs
  - name: cron
    release: cron
    properties:
      cron:
        # a key-value map of any environment variables you want
        # set in the crontab
        #
        variables:
          VAR1: val1
          VAR2: val2

        # a list of key-value objects representing cron entries
        entries:

          # run a commmand already installed
        - command: /usr/bin/touch /tmp/test-command-cron
          minute: '*'
          hour: '*'
          day: '*'
          month: '*'
          wday: '*'
          user: vcap

          # ... or specify a script to install and run
        - script:
            name: touch.sh
            contents: |
              #!/bin/bash
              /usr/bin/touch /tmp/test-script-cron
          minute: '*'
          hour: '*'
          day: '*'
          month: '*'
          wday: '*'
          user: vcap
```

When deployed, this release will generate a crontab, stick it in
/etc/cron.d/cron-boshrelease-crontab, and reload the running cron
process to read the new crontab.
