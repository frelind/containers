name := pihole

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
		-p $(ipaddr):53:53 \
		-p $(ipaddr):53:53/udp \
		-p $(ipaddr):80:80 \
		-p $(ipaddr):443:443 \
		--dns=127.0.0.1,1.1.1.1 \
		-e ServerIP="192.168.1.3" \
		-e TZ="Europe/Stockholm" \
		-e WEBPASSWORD="$(password)" \
		-v "pihole:/etc/pihole/" \
		-v "dnsmasq:/etc/dnsmasq.d/" \
		docker.io/pihole/pihole

service:
	install ../systemd-tmpl.service /etc/systemd/system/$(name).service
	systemctl daemon-reload
	systemctl enable $(name)
