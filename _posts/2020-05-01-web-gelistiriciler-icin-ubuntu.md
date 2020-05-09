---
layout: post
title: Web Geliştiriciler İçin Ubuntu
date:   2020-05-01 20:00:00 +0530
description: Web geliştiriciler için Ubuntu ortamında geliştirme yapmak için gerekli uygulamaları yüklemek için ufak bir rehber.
categories: Ubuntu Linux
---

Web geliştiriciler için [Ubuntu](https://ubuntu.com/) ortamında geliştirme yapmak için gerekli uygulamaları yüklemek için ufak bir rehber.

İlk olarak sistemimize **Apache** kuracağız.

Bunu için ilk olarak `sudo apt update` ile depolar güncellenerek ardından `sudo apt install apache2` ile kurulumu gerçekleştireceğiz.  http:r//localhost yazdığınızda tarayıcınıza Apache2 sayfanızı görüyor olmanız gerek.

**PHP** ortamında geliştirme yapacağınızı varsaydığım için `sudo apt install php` ile de PHP kurulumunu gerçekleştiriyoruz.

**Ardından Veritabanı**

Veritabanı kurulumu için `sudo apt install php-mysql` ve `sudo apt install mysql-server` komutları ile mysql kurulumu bitmiş oluyor.

Mysql-server kurulumu sırasında dikkat etmeniz gereken bir husus, kurulum esnasında size root kullanıcısı için şifre soracaktır. Bu şifreyi unutmayacağınız bir şifre yapmanız gerek.

**phpMyAdmin**

`sudo apt install phpmyadmin` komutu ile phpMyAdmin için kurulumunu başlatıyoruz. Kurulum aşamasında size 2 tane soru gelecek. İlk olarak sunucu yapılandırma ayarı seçimi. O adımda apache2 seçilmesi gerekiyor. Devamında phpMyAdmin root kullanıcısı için şifre ekranı. Bu kısımda mysql-server kurulumunda yazdığınız şifreyi vermeniz gerekiyor.

Kurulum tamamlandıktan sonra çalıştırmak için link işlemi gerçekleştirmemiz gerek. Bunu için `sudo ln -sf /usr/share/phpmyadmin /var/www/html/phpmyadmin` komutuyla gerekli işlemi gerçekleştiriyoruz.

Son adım olarak `sudo /etc/init.d/apache2 restart` sunucusunu yeniden başlatarak tüm sistemi işler hale getiriyoruz.
