Gitolite-Apache2-Autodeploy on Ubuntu Setup
=================================

Basic Steps
-----------

- [HowtoForge: Minimal 16.04 Server](https://www.howtoforge.com/tutorial/ubuntu-16.04-xenial-xerus-minimal-server/)
  * Minimal Virtual Server Install Mode (if not on virtual machine use Minimal Server)
  * Software Selections:
    - OpenSSH
    - Basic Ubuntu Server / Standard system utilities
  * Personally, I only use sudo -s and do not enable root user. This is up to you, its your machine
  * Secure SSH
  * Update, upgrade, dist-upgrade
  * Set static IP & FQDN
- [HowtoForge: LAMP on 16.04](https://www.howtoforge.com/tutorial/install-apache-with-php-and-mysql-on-ubuntu-16-04-lamp/)
  * Additional PHP packages: (deciding to take an 'install when needed approach') I only added php7.0-mysql.
  * I did not enable SSL (i want to be working before messing with SSL)
  * No PhpMyAdmin

- *Good time for a Snapshot if VM*
- Install Gitolite3 - [Ubuntu Git Guide - See Bottom Section](https://help.ubuntu.com/lts/serverguide/git.html)
  * MAKE SURE YOU INSTALL GITOLITE3!!!! We need v3.6+ for repo-specific-hooks
   - ```apt-get install gitolite3```
  * `gl-setup /tmp/*.pub` run from the `git` user is incorrect on Ubuntus site..
  * Use `gitolite setup -pk /tmp/*.pub` on `git` user
- Configuring Gitolite3 - [Gitolite Basic Admin](http://gitolite.com/gitolite/basic-admin.html)
- Configure Wild Repos - [Gitolite3 Wild Repos](http://gitolite.com/gitolite/wild.html)
- Configure custom hooks (sections 4.2 - 4.4) - [Gitolite3 Cookbook](http://gitolite.com/gitolite/cookbook.html)
  * Add your own hooks in your gitolite-admin repository under:
   - `gitolite-admin/local/hooks/repo-specific/`
   - my post receive hook can be found [here](https://github.com/msashlee/deploy-hook)
  * Enable your hook in `gitolite-admin/conf/gitolite.conf` with a config like
   >``` repo testing```

   >``` RW+     =   @all```

   > ```option hook.post-receive   =  deploy```
- You should now be able to pull the testing directory from your remote, add an `index.html` file, commit it, push it to your server and visit it at `http://yourserver.tdl/testing/index.html`
