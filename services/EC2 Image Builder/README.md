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
      sed -i "51,1000d" wp-config.php
      cat <<"EOF" >>wp-config.php

      define('AUTH_KEY',         '-{*8{&9Z0<MH7t/@Y=P^taB(*a.z^kt$>v1$NJ(7v1PD$b/YH4puBGi;bs1bb9<9');
      define('SECURE_AUTH_KEY',  't-1i3H|Hf-1/&ghPr58|^g]Yu:Y ??,Xc|G:%+~NvTO$>]X!i,OB0O1CN23$Y!:}');
      define('LOGGED_IN_KEY',    'T&a-]qw_#J5=}?:-^8pgNV|T!5J;!V<Na<o%]]v3&TY<eV4|A&::VsBT)^9GY0-0');
      define('NONCE_KEY',        '=010PoG)6Bu1|x[{=!iAoi3G-lx;XMVAZ6pzBmg8$/&?7yv+/o}Y+|AziUxdbr(u');
      define('AUTH_SALT',        '#_qSh&b#;tkRe]yn.Atf}dZnji hp/w10xU:k50XLLWF7}E<{.]w2+Eov;6Mb5<w');
      define('SECURE_AUTH_SALT', 'wk3A/q8w6L%UbH( w.K5<PC. U{^4~~Y-6wlQd-[**/[Q[l-5zxpQC}-u-R?Uocs');
      define('LOGGED_IN_SALT',   'Nr^;|&w,x54/pG3}>KiE@U%(TPM~*0rPT*!Tko8eF?V?ke)h,}{1|A)|v8c~n3Z[');
      define('NONCE_SALT',       ' N%WZ||C)L=:|ZZVlqwfNn[@qsKxk7cC,x@~)$O~/g]Y%+jASwH&^{{AWipjGf/r');
      
      /**#@-*/

      /**
       * WordPress database table prefix.
       *
       * You can have multiple installations in one database if you give each
       * a unique prefix. Only numbers, letters, and underscores please!
       */
      $table_prefix = 'wp_';

      /**
       * For developers: WordPress debugging mode.
       *
       * Change this to true to enable the display of notices during development.
       * It is strongly recommended that plugin and theme developers use WP_DEBUG
       * in their development environments.
       *
       * For information on other constants that can be used for debugging,
       * visit the documentation.
       *
       * @link https://wordpress.org/support/article/debugging-in-wordpress/
       */
      define( 'WP_DEBUG', false );

      /* Add any custom values between this line and the "stop editing" line. */

      define( 'FS_METHOD', 'direct' );

      define( 'WP_REDIS_HOST', 'redis-cluster-for-wordpress.ye1eiy.ng.0001.apn2.cache.amazonaws.com' );
      define( 'WP_CACHE', true );
      define( 'WP_CACHE_KEY_SALT', 'taesankim.tk' );

      define('FORCE_SSL_ADMIN', true);
      define('FORCE_SSL_LOGIN', true);
      $_SERVER['HTTPS'] = 'on';
      
      /* That's all, stop editing! Happy publishing. */

      /** Absolute path to the WordPress directory. */
      if ( ! defined( 'ABSPATH' ) ) {
              define( 'ABSPATH', __DIR__ . '/' );
      }

      /** Sets up WordPress vars and included files. */
      require_once ABSPATH . 'wp-settings.php';
      EOF

      # Create Heath Check Page
      touch heath_check.html

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

WordPress wp-config.php 설정 내용 중  
긴 무작위 값을 추가해서 사이트의 보안성을 강화하는 코드는 [이 링크](https://api.wordpress.org/secret-key/1.1/salt/)에서 확인 가능
