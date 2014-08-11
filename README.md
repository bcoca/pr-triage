# pr-triage

GitHub Pull Request Triage Assistant

## Installing

1. `git clone https://github.com/sivel/pr-triage.git`
1. `cd pr-triage`
1. `pip install -r requirements.txt`
1. Create a `triage.yaml` configuration file as described below

## triage.yaml

This file can live at `./triage.yaml`, `~/.triage.yaml`, or `/etc/triage.yaml`

```yaml
---
# Required Configuration
github_client_id: 1ecad3b34f7b437db6d0
github_client_secret: 6689ba85bb024d1b97370c45f1316a16d08bba20
github_repository: 'ansible/ansible'

# Optional Configuration
use_rackspace: true
pyrax_credentials: ~/.rackspace_cloud_credentials
pyrax_region: DFW
pyrax_container: ansible-pr-triage
```

*The above values are dummy placeholder values and are not valid for use*

### GitHub credentials

You will need to [register an application](https://github.com/settings/applications/new)
to provide API access.  The Client ID and Secret will need to be populated as
shown in the above example.

## Hosting

There are currently 2 options for hosting the HTML files generated by this application.

1. Local
2. Rackspace CloudFiles

### Local

`triage.py` will write out HTML files to a directory called `htmlout`. You can
host these files directly out of that directory using a webserver such as
Apache or nginx.

### Rackspace CloudFiles

It is not required that you upload the files to Rackspace CloudFiles, this is
just here for convenience. The CloudFiles container that you wish to upload to
should already exist and be configured to host a static website. See
[Point And Click Your Way To A Cloud Files Static Website With The Control Panel](http://www.rackspace.com/blog/point-and-click-your-way-to-a-cloud-files-static-website-with-the-control-panel/)
for details on how to configure this.

If you intend on using Rackspace CloudFiles to host the files, you will also
need the [pyrax](https://pypi.python.org/pypi/pyrax) python module installed.
Additionally, you will also need a valid [pyrax credentials file](https://github.com/rackspace/pyrax/blob/master/docs/getting_started.md#authenticating).

#### Installing pyrax

```shell
pip install pyrax
```

## Running

It is recommended that you run `triage.py` via cron. The fewer pull requests a
project has the more frequently you can run the cron job. I'd recommend
starting with every 60 minutes (1 hour).
