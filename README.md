# filevisor
Monitoring files system for web-servers based on debian/ubuntu (with ISPmanager5 in my case)

#Installing packets

sudo apt-get install inotify-tools supervisord

#Then its enough just to launch daemonized instance by:

inotifywait -e delete -e modify -e create -r -m ~/www -d -o ~/logs/user_file_watch.log --timefmt '%F %T' --format '%T %:e %w %f' --excludei '.*(\.jpg|jpeg|tif|ico|png|tmp|gif)'

#Where options is

#. -e delete - witch event watch to

#. -r -recursively listen to all folders

#. -m ~/www  - folder to monitor

#. -d  - daemonizing rhe process (u can kill it by command listed below)

#. -o ~/logs/user_file_watch.log  - output log file where all changes will be written

#. --timefmt '%F %T'  - a formatted time output for --format option. %F is current date and %T is current time

#. -format '%T %:e %w %f'  - a regex formatted output to -o option, where %T is time from --timefmt, %:e - detected event,  

#. %w - full path to file that changed, %f - file name

#. --excludei '.*(\.jpg|jpeg|tif|ico|png|tmp|gif)'  - excluding by regex (with file ext in my case)

#. Also you can kill the process of monitoring daemon with

pkill -f inotifywait
