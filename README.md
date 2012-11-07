nagios-plugins-obs
==================

check_obs for nagios

For openSUSE or SLE: it is packaged in the [Open Build Service](https://build.opensuse.org/package/show?package=nagios-plugins-obs&project=server%3Amonitoring)

Example
-------

    > ./check_obs --apiurl=https://api.opensuse.org \
                --http-user=<user> --http-password=- \
                --scheduler-arch=armv5el,armv7l,i586,local,ppc,ppc64,x86_64 \
                --worker=x86_64?w10:?c2:?iw1,ppc64?w3:?c1:?iw1 \
                --packages=x86_64?ww1000,i586?ww1000,ppc,ppc64            
    > Password: **********
    > All schedulers running. Too many packages waiting (x86_64, i586). | worker_amount_x86_64=296;10:;2: worker_idle_x86_64=0;:1 worker_building_x86_64=296 worker_amount_ppc64=18;3:;1: worker_idle_ppc64=0;:1 worker_building_ppc64=18 packages_amount_x86_64=8306 packages_waitin
    > echo $?
    > 1
     
Implicit: `--scheduler-special=dispatcher,publisher,signer,warden`

* checks that all special schedulers are running.
* checks that all mentioned schedulers are running (armv5el,armv7l,i586,local,ppc,ppc64,x86_64)
* returns performance data for worker nodes with architecture x86_64 and ppc64
* returns performance data for packages for architecture x86_64, i586, ppc and ppc64
* a warning is triggered if
  * less than 10 workers with host-architecture x86_64 present
  * less than 3 workers with host-architecture ppc64 present
  * more than 1 worker with host-architecture x86_64 or ppc64 is idle
  * between than 1000 packages with architecture x86_64 or i586 waiting
* a critical is triggered if
  * less than 2 workers with host-architecture x86_64 present
  * less than 1 workers with host-architecture ppc64 present
