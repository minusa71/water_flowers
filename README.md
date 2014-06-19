water_flowers
=============

made by Rumen Parunov

#!/bin/bash
#*gpio 1 - PIN10 (platka), PIN17 (cuplung)
echo 3 > /sys/class/gpio/export
echo in > /sys/class/gpio/gpio3/direction
echo -e " \e[92m "
cat /sys/class/gpio/gpio3/value
echo -e " \e[39m "
echo 3 > /sys/class/gpio/unexport
echo -e "if 0 - \e[92m there is water in the tank \e[39m "
echo -e "if 1 - \e[91m no water in the tank \e[39m "
read -p "Continue (y/n)?" choice
case "$choice" in
y|Y )
echo 1 > /sys/class/gpio/export
echo out >  /sys/class/gpio/gpio1/direction
echo 1 > /sys/class/gpio/gpio1/value
echo -e " \e[92m wait water is pumping.... \e[39m "
sleep 12
echo 0 > /sys/class/gpio/gpio1/value
echo 1 > /sys/class/gpio/unexport
echo -e " \e[91m pump stopped. \e[39m "
sleep 2
echo 4 > /sys/class/gpio/export
echo in > /sys/class/gpio/gpio4/direction
echo -e " \e[92m "
cat /sys/class/gpio/gpio4/value
echo -e " \e[39m "
echo 4 > /sys/class/gpio/unexport
sleep 1
echo -e "if 0 - \e[92m water is supplied \e[39m "
echo -e "if 1 - \e[91m water not supplied \e[39m ";;
n|N )
exit;;
* ) echo "invalid entry";;
esac
echo $(date)
