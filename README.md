# Tunnelss

Tunnelss is a proxy from HTTPS to HTTP to help with web development over HTTPS.

It's like the [tunnels gem](https://github.com/jugyo/tunnels) (sure, it's a fork), but it does more, since it makes your HTTPS recognized as valid by the browser!

So now you can finally have a not-far-from-real SSL connection with Pow, with a minimum of efforts!

## The Magic

Tunnelss is a mix between the [tunnels gem](https://github.com/jugyo/tunnels) and the [powssl script](https://gist.github.com/paulnicholson/2050941).

1. It builds a root-level certificate (a Certificate Authority) and registers it as a trusted root certificate (you will need to do it manually for Firefox).
2. It generates a SSL certificate matching the Pow `.dev` domains.
2. It runs an EventMachine server which acts as proxy from HTTPS to HTTP (just like tunnels), using the generated certificate so that your browser will not complain your SSL connection is not valid!

## Why?

Because:

* setting up Nginx to do reverse-proxying for development is overkill,
* you would have to add a Nginx config file each time you start a new project,
* you like the `.dev` domains provided by Pow,
* you want to run your app over SSL just like in production so that you can check the redirections,
* working with external APIs over HTTPS, secured cookies and CORS seems really difficult if your SSL certificate is not valid (your browser may refuse to perform CORS requests),
* your app server needs to know that the request was over HTTPS, even if it was proxied to HTTP (which the powssl script which uses Stud doesn't allow).

## Disclaimer

This gem is in early developments and has only been tested under MacOS X 10.8. It may not work in other environments, but feel free to submit pull requests if you make the necessary fixes.

## Installation

    $ gem install tunnelss

If you're using rbenv:

    $ rbenv rehash

## Run

    $ sudo tunnelss

Don't worry, the first time you launch it it will generate a certificate and ask for your permission to add it to trusted authorities (see _The Magic_ above for more details).

If you are using rvm:

    $ rvmsudo tunnels

By default, proxy to 80 port from 443 port.

Specify HTTP port and HTTPS port with:

    $ sudo tunnels 443 3000

or

    $ sudo tunnels 127.0.0.1:443 127.0.0.1:3000

## History

### 0.1.0

Initial release based on tunnels 1.2.2.

## Credits

* [tunnels](https://github.com/jugyo/tunnels) from which most code comes
* [powssl](https://gist.github.com/paulnicholson/2050941), a gist of Paul Nicholson which I translated to Ruby to perform Tunnelss certificate configuration based on Pow's.

## Copyright

[tunnelss](http://github.com/rchampourlier/tunnelss)
Copyright (c) 2013 rchampourlier, released under the MIT license.

[tunnels](https://github.com/jugyo/tunnels)
Copyright (c) 2012 jugyo, released under the MIT license.
