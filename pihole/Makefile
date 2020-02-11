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
		-p 53:53 \
		-p 53:53/udp \
		-p 192.168.1.3:80:80 \
		-p 192.168.1.3:443:443 \
		--dns=127.0.0.1,1.1.1.1 \
		-e ServerIP="192.168.1.3" \
		-e TZ="Europe/Stockholm" \
		-e WEBPASSWORD="$$(pass $(name))" \
		-v "pihole:/etc/pihole/" \
		-v "dnsmasq:/etc/dnsmasq.d/" \
		docker.io/pihole/pihole

service:
	install $(name).service /etc/systemd/system/
	systemctl daemon-reload
	systemctl enable $(name)