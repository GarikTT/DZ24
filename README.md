Урок 24 - Сбор и анализ логов.  
Цель занятия -  
    понять зачем нужны логи и как их собирать;  
	освоить принципы логирование с помощью rsyslog;  
	понять возможности logrotate для задач ротации логов;  
	научиться работать с journald и auditd;  
	узнать про adrtd и kdump.  
Домашнее задание - Научится проектировать централизованный сбор логов. Рассмотреть особенности   
разных платформ для сбора логов.  
Результат выполнения - полученные навыки по основам работы с rsyslog, logrotate, journald, auditd, abrtd и kdump.  
Ага, приступаем к выполнению.  
34. Создаем инвентори файл ([hosts](hosts)) и ([epel.yml](epel.yml))
1. БОльшую часть работы по синхронизации времени мы, с вами, выполняем в Vagrantfile.  
Объясняю - по умолчанию время на серверах устанавливается на UTC+0, а, нам надо, что бы было наше,  
родное, Красноярское. Ручной метод, описанный в методичке я проверял - тоже работает.  
2. Теперь, просто заходим по очереди на Веб сервер и Log сервер и проверяем время - одинаковое, Красноярское.  
  vagrant ssh web  
	systemctl status chronyd  
	timedatectl  
	exit  
	vagrant ssh log  
	systemctl status chronyd  
	systemctl restart chronyd  
	timedatectl  
	exit  
	Ну, вот, отлично!  

	([cat /var/log/rsyslog/web/nginx_access.log](nginx_access.log))  
	([cat /var/log/rsyslog/web/nginx_error.log](nginx_access.log))  
4. Фсе. Привет!!!
