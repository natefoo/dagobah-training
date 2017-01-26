layout: true
class: inverse, middle, large

---
class: special
# How to get Galaxy

slides by @martenson

.footnote[\#usegalaxy / @galaxyproject]

---
class: larger

## Please Interrupt!
Your questions will be answered.

---
class: normal
# Reasons to Install Your Own Galaxy

You only need to download Galaxy if you plan to:

- Run a local production Galaxy because you want to
  - Install and use tools unavailable on public Galaxies
  - Use sensitive data (e.g. clinical)
  - Process large datasets that are too big for public Galaxies
  - Plug-in new datasources
- Develop Galaxy tools
- Develop Galaxy itself

Even when you plan any of the above sometimes you can leverage pre-configured
[Docker image](https://github.com/bgruening/docker-galaxy-stable)
or use [Cloudlaunch](https://launch.usegalaxy.org).

---
# Requirements

- Any Linux or Mac OS
- Python 2.7

Optional
  - samtools (metadata etc.)
  - Git code versioning system
  - GNU Make + gcc to compile and install tool dependencies
  - Additional requirements for shipped tools

---
# Get logged in to your VM

For OS X/Linux/Windows w/ Linux Subsystem or OpenSSH:
```console
$ ssh -L 8080:localhost:8080 ubuntu@<your_ip>
```

For PuTTY on Windows:
- Create a session
- See [instructions here](http://realprogrammers.com/how_to/set_up_an_ssh_tunnel_with_putty.html).
- User: ubuntu
- Host Name: `<your_ip>`
- (Tunnel) Source port: 8080
- (Tunnel) Destination: 127.0.0.1:8080

---
# Clone the repository

1. Check what is the latest [release](https://docs.galaxyproject.org/en/master/releases/index.html)
1. Run
```shell
$ git clone -b release_16.10 https://github.com/galaxyproject/galaxy.git
```
Release is defined by the branch name: `release_16.10` see the [branch list](https://github.com/galaxyproject/galaxy/branches/all))

Without specifying branch during clone you are running the *development* version of Galaxy.

For the rolling stable release: `git checkout master`<sup>[1]</sup>.

.footnote[<sup>[1]</sup> This is currently not updated as often as it should be.]

---
# Start Galaxy

1. `$ cd galaxy`
1. `$ ./run.sh`
1. visit `http://localhost:8080`

You should see default Galaxy running.

.footnote[Note that first startup needs internet connection and takes longer than the subsequent ones.]

---
# What happened?

* Galaxy started logging into the terminal from which it is run.
* Galaxy created a Python virtual environment (venv) in `.venv/`.
* Galaxy sourced this environment (`$ source .venv/bin/activate`)
* Galaxy fetched needed Python binaries ('wheels') into this environment.
* Galaxy created the default SQLite database and migrated it to the latest version.
* Galaxy bound to the default port `8080` on `localhost`.

.footnote[All of the above can be configured.]

---
# Look around

1. Run a basic job (e.g. upload a file).
1. Check http://localhost:8080/api/version to see Galaxy's version.
1. Stop Galaxy by terminating the console process (`CTRL+C`).

---
# Basic configuration

- Galaxy works out of the box with default configuration.
- Most important config files are in `config/`.
- Galaxy often uses the files with suffix `*.sample` as declared defaults.

---
# Exercise: make your own config

* Copy the provided sample and open editor.
```shell
$ cp config/galaxy.ini.sample config/galaxy.ini
$ nano config/galaxy.ini
```
* Set the following entries.
```shell
message_box_visible = True
message_box_content = Hey, at least I'm not a popup!
message_box_class = info
```
* (Re)start Galaxy.

---
# Update the welcome page

Welcome page is `$GALAXY_ROOT/static/welcome.html` and is the first thing that
users see. It is a good idea to extend it with things like:
- Downtimes/Maintenance periods
- New tools
- Publications relating to your Galaxy

No restarting is necessary.

???
You can load remote content to this iframe (blog, existing presentation, etc.).

---
# Make yourself an administrator

* Create an account (User -> Register) <sup>[1]</sup>
* Create a user using Galaxy interface.
* Modify `galaxy.ini` to include `admin_users = your@ema.il`.
* (Re)start Galaxy.

.footnote[<sup>[1]</sup> Registering in the UI *before* setting `admin_users` is not strictly necessary, but is the best security practice]

---
# Be secure

```console
$ sudo -l
User ubuntu may run the following commands on server-f5d67052-36ac-40f5-abf7-14939e479df2.novalocal:
    (ALL : ALL) ALL
    (ALL) NOPASSWD: ALL
```

Let's create a Galaxy user:

```console
foo
```

---
# What to do next?

- Keep your code up to date
- Install tools
- Join the mailing list
- Set up a backup process for your instance
- Configure for production
