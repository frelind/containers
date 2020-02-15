name := prometheus

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
		-p $(ipaddr):9090:9090 \
		-v prometheus:/etc/prometheus \
		prom/prometheus

service:
	install ../systemd-tmpl.service /etc/systemd/system/$(name).service
	systemctl daemon-reload
	systemctl enable $(name)
