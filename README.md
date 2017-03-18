# phant [![Build Status](https://secure.travis-ci.org/sparkfun/phant.svg?branch=master)](http://travis-ci.org/sparkfun/phant)

phant is a modular logging tool developed by [SparkFun Electronics](https://sparkfun.com) for collecting data from
the [Internet of Things](http://en.wikipedia.org/wiki/Internet_of_Things).  phant is the open source software that powers
[data.sparkfun.com](http://data.sparkfun.com).

If you would like to learn more about phant, please visit [phant.io](http://phant.io) for usage & API docs.

## Changes

### Node.js compatibility upgrade

Even though the docs mention that phant "requires the latest version of node.js", they really mean "up to v4.6.2" which is getting a bit long in the tooth in 2017. This fork pulls some changes from [stoto's repo](https://github.com/stoto/phant) that should enable phant to run under a newer version of node. Tested up to v7.7.2.

### Timestamp submission

You will have the ability to submit timestamps, which is useful if you're thinking of storing some data on your IoT device and batch submitting it to save energy as discussed [here](https://github.com/sparkfun/phant/issues/203). The backend does a `new Date(<your submitted date>)` which means any Javascript Date compatible date will do. ISO formatting (with colons url-encoded as `%3A`) is the recommended way:

```
<usual GET request URL>&timestamp=2017-03-10T13%3A14%3A56.000Z
```

Alternatively you can submit six digits separated by commas. Bear in mind Javascript months are zero-indexed and that this will get you a date *in your server's timezone*, not UTC:

```
<usual GET request URL>&timestamp=2017,02,10,13,14,15
```

If there's interest I might add a special path that does a `new Date(Date.UTC(y,m,d,h,m,s))` if submitted string contains six numbers separated by five commas. Perhaps looks a little easier on the eyes than url-encoded colons.

## Getting Started

### Vagrant

Vagrant is a headless virtual machine that can be run on many different systems.
Vagrant is a safe and easy way to run `phant` without the need to greatly
modify your current system
(see [Why Vagrant?](https://docs.vagrantup.com/v2/why-vagrant/)).

Vagrant Setup:

1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. Install [Vagrant](http://www.vagrantup.com/downloads)
3. Install [Git](http://git-scm.com/downloads)
4. `git clone https://github.com/sparkfun/phant.git`
5. `cd phant && vagrant up --provision`
6. `phant` is now available via http on port 8080 and telnet via port 8081

To restart phant use `vagrant provision` from inside the `phant` directory.

To stop the vagrant virtual machine use `vagrant halt` from inside the
`phant` directory.

To restart vagrant use `vagrant up --provision` from inside the `phant`
directory.

### Local

phant is a [npm](https://www.npmjs.org) package, and requires the latest version of [node.js](http://nodejs.org).

Once you have node.js installed, you can install phant by running `npm install -g phant` from your favorite terminal.
Using the `-g` (global) flag will make the `phant` executable available in your `PATH`.

Now you can start phant:

```bash
$ phant
phant http server running on port 8080
phant telnet server running on port 8081
```

This launches a [telnet](http://en.wikipedia.org/wiki/Telnet) server for stream creation, and a http server for data input & output.
You can now open a separate window, and you should be able to create a stream by connecting to the local telnet server.

```
$ telnet localhost 8081
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
            .-.._
      __  /`     '.
   .-'  `/   (   a \
  /      (    \,_   \
 /|       '---` |\ =|
` \    /__.-/  /  | |
   |  / / \ \  \   \_\  jgs
   |__|_|  |_|__\
   never   forget.

Welcome to phant!
Type 'help' for a list of available commands

phant>
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## License
Copyright (c) 2014 SparkFun Electronics. Licensed under the GPL v3 license.
