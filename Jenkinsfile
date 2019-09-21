pipeline {
    agent {
        docker {
            image 'centos:centos7.6.1810'
	    args '-u root:root'
        }
    }
    
    stages {
        stage('Обновляем Ось') {
            steps {
		sh '''
		yum install -y \
		        wget \
		        tar \
		        sudo \
		        openssl-devel \
		        gcc \
		        gcc-c++ \
		        make \
		        zlib-devel \
		        pcre-devel \
		        gd-devel \
		        krb5-devel \
		        git \
		        net-tools
		'''
	    }	
	}
        stage('Стягиваем код из репозитория') {
            steps {
                checkout scm
            }
        }
        stage('Собираем') {
            steps {
                echo "Конфигурируем" 
                sh '''
		   cd ./nginx_src \
                   && ./configure \
		        --user=nginx \
		        --with-debug \
		        --group=nginx \
		        --prefix=/usr/share/nginx \
		        --sbin-path=/usr/sbin/nginx \
		        --conf-path=/etc/nginx/nginx.conf \
		        --pid-path=/run/nginx.pid \
		        --lock-path=/run/lock/subsys/nginx \
		        --error-log-path=/var/log/nginx/error.log \
		        --http-log-path=/var/log/nginx/access.log \
		        --with-http_gzip_static_module \
		        --with-http_stub_status_module \
		        --with-http_ssl_module \
		        --with-pcre \
		        --with-http_image_filter_module \
		        --with-file-aio \
		        --with-http_dav_module \
		        --with-http_flv_module \
		        --with-http_mp4_module \
		        --with-http_gunzip_module \
                     && make \
		     && make install
                '''
            }
 
        }
        stage('Тестируем') {
            steps {
                script {
                    sh 'nginx -v && nginx -t'
                }
            }
        }
    }
}
 
