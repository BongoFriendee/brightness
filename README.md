# brightness
Bash script to automatically set system brightness when. Run as a cron.

```shell
#!/bin/bash                                                         
#set brightness to a nonblinding level                              

# current time                                                      
T=$(date +%H | sed 's/^0*//')                                        
#brightness file                                                    
BR="/sys/class/backlight/nv_backlight/brightness"                   

#We only want to mess with the brighness if it's the default (100) value or if the value is one set by this script.                     
#Otherwize if it is set to a custom value lets keep it that way and exit without setting anything.                                      

if [[ $(< $BR ) -eq 100 ]] ||   [[ $(< $BR ) -eq 71 ]] || [[ $(< $BR ) -eq 36 ]] || [[ $(< $BR ) -eq 12 ]]                              
then                                                                
  if ((8 <= $T &&  $T < 18  ));                                     
  then echo 71 > $BR                                                
  elif ((18 <= $T && $T < 20 ));                                    
  then echo 36 > $BR                                                
  else echo  12 > $BR                                               
  fi                                                                
fi                                     
