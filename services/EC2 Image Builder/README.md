# EC2 Image Builder

## EC2 Image Builder
### Image pipelines
- Pipeline-For-Bastion
  - General
    - Pipeline name - Pipeline-For-Bastion-AMI
    - Enable enhanced metadata collection
  - Build schedule
    - Schedule options
      - Schedule builder
      - Run pipeline every Week on Monday at 09:00 UTC
    - Dependency update settings - Run pipeline at the scheduled time if there are dependency updates
  - Recipe - Recipe-For-Bastion-AMI
  - Infrastructure configuration
    - Configuration options - Create infrastructure configuration using service defaults
  - Distribution settings
    - Configuration options - Create distribution settings using service defaults
    - AMI tags
      - Key - Name
      - Value - Bastion-AMI

- Pipeline-For-Bastion
  - General
    - Pipeline name - Pipeline-For-WAS-AMI
    - Enable enhanced metadata collection
  - Build schedule
    - Schedule options
      - Schedule builder
      - Run pipeline every Week on Monday at 09:00 UTC
    - Dependency update settings - Run pipeline at the scheduled time if there are dependency updates
  - Recipe - Recipe-For-WAS-AMI
  - Infrastructure configuration
    - Configuration options - Create infrastructure configuration using service defaults
  - Distribution settings
    - Configuration options - Create distribution settings using service defaults
    - AMI tags
      - Key - Name
      - Value - WAS-AMI

### Saved configurations - Image recipes
- Recipe-For-Bastion-AMI
  - Recipe details
    - Name - Recipe-For-Bastion-AMI
    - Version - 1.0.0
  - Base image
    - Select image - Select managed images
    - Image Operating System (OS) - Amazon Linux
    - Image origin - Quick start (Amazon-managed)
    - Image name - Amazon Linux Kernel 5 x86
    - Auto-versioning options - Use latest available OS version
  - Instance configuration
    - User data
      ```bash
      #!/bin/bash
      yum update -y

      # Install MySQL Client
      yum localinstall -y https://dev.mysql.com/get/mysql80-community-release-el7-5.noarch.rpm
      yum install -y mysql-community-client

      # Install Redis-CLI
      sudo yum install -y gcc
      wget http://download.redis.io/redis-stable.tar.gz && tar xvzf redis-stable.tar.gz && cd redis-stable && make
      sudo cp src/redis-cli /usr/bin
      ```
  - Components
    - Build components - Amazon Linux
      - update-linux
    - Test components - Amazon Linux
      - reboot-test-linux

- Recipe-For-WAS-AMI
  - Recipe details
    - Name - Recipe-For-WAS-AMI
    - Version - 1.0.0
  - Base image
    - Select image - Select managed images
    - Image Operating System (OS) - Amazon Linux
    - Image origin - Quick start (Amazon-managed)
    - Image name - Amazon Linux Kernel 5 x86
    - Auto-versioning options - Use latest available OS version
  - Instance configuration
    - User data
      ```bash
      #!/bin/bash
      
      # Change these values and keep in safe place
      db_root_password=Password12#$
      db_username=admin
      db_user_password=Password12#$
      db_name=wordpress
      db_host=aurora-cluster-for-wordpress.cluster-camwgkqdniyq.ap-northeast-2.rds.amazonaws.com

      yum update -y

      # Install Apache
      yum install -y httpd

      # Install php
      amazon-linux-extras install -y php8.0

      # Download wordpress package and extract
      cd /var/www/html
      wget https://wordpress.org/latest.tar.gz
      tar -xzf latest.tar.gz

      # Create wordpress configuration file and update database value
      cd /var/www/html/wordpress
      cp wp-config-sample.php wp-config.php

      sed -i "s/database_name_here/$db_name/g" wp-config.php
      sed -i "s/username_here/$db_username/g" wp-config.php
      sed -i "s/password_here/$db_user_password/g" wp-config.php
      sed -i "s/localhost/$db_host/g" wp-config.php
      sed -i "/put your unique phrase here/d" wp-config.php
      sed -i "/ABSPATH/,+6d" wp-config.php
      cat <<"EOF" >>wp-config.php

      define('AUTH_KEY',         '>:#9b!m]RQT9+6f!gbq^&re|$$d$|)AeY;gGLxw++Hg<+xtTXn7{7=&>LY;1.qYu');
      define('SECURE_AUTH_KEY',  '6EKn|JzC|yhA.}3JFLf7WOU}dqM^gyv<{@d`EXQt4:o4uoV2UM|<C5,R3O@KC{-J');
      define('LOGGED_IN_KEY',    '{;J61Ivlc;||)9wCKap(F+6,+u*VQHXSHI7}ns0+iHn4,j|*6sinG%SOp9<Y]lr#');
      define('NONCE_KEY',        'O`NA{,]q(pr9{[G<zlx 3mSH]^ZKwjgI}*W8C9Wc<pUSO$!aC|-G|_+Gvwl.Kiwt');
      define('AUTH_SALT',        '{N-tc}Xnd88JeWdb{_sqCJ}gTC,i1>XpQ1F_)OgY?(0w%&q|}-3=+w$Q<!4|IgAd');
      define('SECURE_AUTH_SALT', 'SX>p3QT0^U**K wh[:VgX:ln_}qhN_4+:x>u/|e;1+|_uk-E-=>Nr0Db|3tWH]%$');
      define('LOGGED_IN_SALT',   '4s)V0nS_H`x7GSONGwj9]xB#<a?cOu{(EN}m`lE+D9]EG?H-kkbYVZR:&4v>n3;+');
      define('NONCE_SALT',       '|lx|{jgY`#h>8o)OjFt@;m2Ce9E/2/;|?h})!f&u6f?]+)tHW%wmZ-C.R0P.!c6t');

      define( 'FS_METHOD', 'direct' );

      define( 'WP_REDIS_HOST', 'redis-cluster-for-wordpress.ye1eiy.ng.0001.apn2.cache.amazonaws.com' );
      define( 'WP_CACHE', true );
      define( 'WP_CACHE_KEY_SALT', 'alb.taesankim.tk' );

      define('FORCE_SSL_ADMIN', true);
      define('FORCE_SSL_LOGIN', true);
      $_SERVER['HTTPS'] = 'on';

      if ( ! defined( 'ABSPATH' ) ) {
              define( 'ABSPATH', __DIR__ . '/' );
      }

      /** Sets up WordPress vars and included files. */
      require_once ABSPATH . 'wp-settings.php';
      EOF

      # Create Heath Check Page
      touch heath.html

      # Change permission of /var/www/html/wordpress
      chown -R apache:apache /var/www/html/wordpress

      # Make apache and mysql to autostart and restart apache
      systemctl enable httpd.service
      systemctl restart httpd.service
      ```
  - Components
    - Build components - Amazon Linux
      - aws-codedeploy-agent-linux
      - update-linux
    - Test components - Amazon Linux
      - reboot-test-linux

<br/>

### ※ 참고
Distribution settings에서 AMI tags 설정은 파이프라인 구성 후 설정할 것
