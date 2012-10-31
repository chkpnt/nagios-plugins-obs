nagios-plugins-obs
==================

check_obs for nagios

Example
-------

    ./check_obs --apiurl=https://api.opensuse.org \
                --http-user=<user> --http-password=- \
                --scheduler-arch=armv5el,armv7l,i586,local,ppc,ppc64,x86_64 \
                --worker=x86_64?w10:?c2:,ppc64?w3:?c1: \
                --packages=i586?ww@3000:4000?wc4000                

Implicit: `--scheduler-special=dispatcher,publisher,signer,warden`

* checks that all special schedulers are running.
* checks that all mentioned schedulers are running (armv5el,armv7l,i586,local,ppc,ppc64,x86_64)
* returns performance data for worker nodes with architecture x86_64 and ppc64
* returns performance data for packages for architecture i586
* a warning is triggered if
  * less than 10 workers with host-architecture x86_64 present
  * less than 3 workers with host-architecture ppc64 present
  * between 3000 and 4000 packages with architecture i586 waiting
* a critical is triggered if
  * less than 2 workers with host-architecture x86_64 present
  * less than 1 workers with host-architecture ppc64 present
  * more than 4000 packages with architecture i586 waiting