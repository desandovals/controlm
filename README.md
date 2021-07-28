### Automatizando inicio de ControlM

Para automatizar el inicio del agente de ControlM es necesario que previamente haya sido instalado y configurado. Una vez hecho esto, crear el archivo: 

```
/etc/systemd/system/ctmagent.service
```

Y copiar el siguiente contenido: 

```
[Unit]
Description=CtMagent
After=syslog.target network.target network-online.target remote-fs.target

[Service]
Type=simple
ExecStart=/ctmagent/ctm/scripts/start-ag -u ctmagent -p ALL
ExecStop=/ctmagent/ctm/scripts/shut-ag -u ctmagent -p ALL
ExecStop=/bin/killall -v -s 9 p_ctmag
RemainAfterExit=yes

[Install]
WantedBy=default.target
```

Después ejecutar los siguientes comandos para que el servicio sea reconocido por SystemD: 

```
systemctl daemon-reload
systemctl enable ctmagent
systemctl start ctmagent
```

Al finalizar, habremos automatizado el proceso de inicio del agente. 