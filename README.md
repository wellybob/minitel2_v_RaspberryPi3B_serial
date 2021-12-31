# minitel2_v_RaspberryPi3B_serial
France Telecom terminal of the 1990s (Minitel2) as a serial connected console for RPI3B

MINITEL 2 Philips & Raspberry Pi 3 model B serial connection

Raspberry Pi 3 model B configuration
ttyS0 is connected by default to GPIO pin 14 (Tx) and 15 (Rx)

EDIT: 
/boot/config.txt
enable_uart=1

/etc/inittab
T0:2345:respawn:/sbin/getty ttyS0 4800v23

/boot/cmdline.txt
console=ttyS0,4800

THEN >reboot

 >sudo chmod 666 /dev/ttyS0
?after every reboot?

CHECK:
user (pi) in the dialout group:
>getent group dialout

ttyS0 -??→ serial0  ??
>ls -l /dev

>ps aux | grep ttyS0
>ls -l  /dev/serial*
>ls -l /dev | grep ttyS0
>sudo tty -F /dev/ttyS0 -a

set baud 4800:
>sudo tty -F /dev/ttyS0 4800

check process:
>fuser /dev/ttyS0
>htop -p<processID>
>top -p<processID>

kill process:
>fuser -k <processID>
>kill <processID>
if not enough:
> kill -9 <processID> (commands kernel direcly)
>killall -9 <name_of_service:e.g. minicom>

SERIAL COMMUNICATION

writes to the minitel screen when typing RPi:
>echo -ne “HELLO” > /dev/ttys0
writes to minicom screen when typing minitel
>cat -v < /dev/ttys0
writes to file when typing minitel
> cat -v < /dev/ttys0 >> minitel_keyboard_listener.txt

APPLICATIONS:
>screen /dev/ttys0
>minicom -o
config: SERIAL PORT SETUP: serial device: /dev/ttys0, Bps/Par/Bits : 4.800 8N1 7N1 (still needs fine tuning...)
& save setup as dfl

MINITEL2 Philips config of serial comm.
(no memory, do it every time you restart minitel)
after plugin: Fnct+T then E, Fnct+T then A, Fnct+P then 4
push: Connection/Fin button

WIRING
Minitel DIN
Bidirectional Voltage level converter 5V/3.3V


 
