name := unifi

.PHONY: stop start create service

stop:
	systemctl stop $(name) || true
	podman stop $(name) || true

start:
	systemctl start $(name)
	systemctl status $(name)

create: stop
	podman rm $(name) || true
	podman create --name $(name) \
		-p $(ipaddr):8080:8080 \
		-p $(ipaddr):8443:8443 \
		-p $(ipaddr):3478:3478/udp \
		-p $(ipaddr):10001:10001/udp \
		-e TZ='Europe/Stockholm' \
		-v unifi:/unifi \
		jacobalberty/unifi:stable

service:
	install ../systemd-tmpl.service /etc/systemd/system/$(name).service
	systemctl daemon-reload
	systemctl enable $(name)
