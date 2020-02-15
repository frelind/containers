name := grafana

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
		-p $(ipaddr):3000:3000 \
		grafana/grafana:latest

service:
	install ../systemd-tmpl.service /etc/systemd/system/$(name).service
	systemctl daemon-reload
	systemctl enable $(name)
