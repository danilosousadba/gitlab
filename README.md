# impacta
Instalação do GitLab em Docker para laboratório DataOps

## Pré Requisitos
- Sistema Operacional Linux ou MacOs
- git               - https://git-scm.com/downloads
- docker            - https://docs.docker.com/get-docker/
- docker compose    - https://docs.docker.com/compose/install/

## Setup
```
git clone https://github.com/danilosousadba/impacta.git
```
```
mkdir -p /opt/airflow/dags /opt/airflow/logs /opt/airflow/plugins /opt/airflow/data
```
```
cd dataops/impacta-dataops-gitlab
```
```
docker-compose up -d
```


#Reset senha root
```
docker exec -ti gitlabdocker_web_1 bash
gitlab-rake "gitlab:password:reset[root]"

```

## Default url
http://localhost

#Setup Runner

```
docker run --rm -t -i -v /opt/gitlab/runners/shared/config:/etc/gitlab-runner gitlab/gitlab-runner register
```

Preencher os comandos

Alterar o arquivo /opt/gitlab/runners/shared/config/config.toml

Incluindo a linha

clone_url = "http://localhost" dentro da aba runners
volumes = ["/cache","/opt/airflow/dags:/opt/airflow/dags:rw"]

```
docker run -d --name gitlab-runner-shared --restart always -v /opt/gitlab/runners/shared/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock gitlab/gitlab-runner:latest
```





[comment]: <> (## Default Username)

[comment]: <> (root    )

[comment]: <> (## Default Password)

[comment]: <> (root)
