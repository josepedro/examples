# How to use Kapua on DC/OS

## Install Kapua
```json
{
  "id": "/kapua-api",
  "cmd": "docker run --link /friendly_leakey:db --link /mystifying_babbage:broker --link /gifted_kowalevski:es --env commons.db.schema.update=true -p 8081:8080 kapua/kapua-api:0.3.2",
  "cpus": 0.2,
  "mem": 128,
  "disk": 0,
  "instances": 1,
  "acceptedResourceRoles": [
    "slave_public"
  ],
  "container": null,
  "networks": [
    {
      "mode": "container/bridge"
    }
  ]
}
```

```json
{
  "id": "/kapua-broker",
  "cmd": "docker run --link /unruffled_dijkstra:db --link /gifted_kowalevski:es --env commons.db.schema.update=true -p 1883:1883 -p 61614:61614 kapua/kapua-broker:0.3.2",
  "cpus": 0.2,
  "mem": 128,
  "disk": 0,
  "instances": 1,
  "acceptedResourceRoles": [
    "slave_public"
  ],
  "container": {
    "type": "MESOS",
    "volumes": [],
    "portMappings": [
      {
        "containerPort": 0,
        "hostPort": 0,
        "labels": {},
        "name": "default",
        "protocol": "tcp",
        "servicePort": 10002
      }
    ]
  },
  "networks": [
    {
      "mode": "container/bridge"
    }
  ],
  "portDefinitions": []
}
```

```json
{
  "id": "/kapua-console",
  "cmd": "docker run --link /friendly_leakey:db --link /mystifying_babbage:broker --link /gifted_kowalevski:es --env commons.db.schema.update=true -p 8080:8080 kapua/kapua-console:0.3.2",
  "cpus": 0.2,
  "mem": 128,
  "disk": 0,
  "instances": 1,
  "acceptedResourceRoles": [
    "slave_public"
  ],
  "container": {
    "type": "MESOS",
    "volumes": [],
    "portMappings": [
      {
        "containerPort": 0,
        "hostPort": 0,
        "labels": {},
        "name": "default",
        "protocol": "tcp",
        "servicePort": 10003
      }
    ]
  },
  "networks": [
    {
      "mode": "container/bridge"
    }
  ],
  "portDefinitions": []
}
```
```json
{
  "id": "/kapua-elasticsearch",
  "cmd": "docker run -p 9200:9200 -p 9300:9300 elasticsearch:5.4.0 -Ecluster.name=kapua-datastore -Ediscovery.type=single-node -Etransport.host=_site_ -Etransport.ping_schedule=-1 -Etransport.tcp.connect_timeout=30s",
  "cpus": 0.3,
  "mem": 128,
  "disk": 0,
  "instances": 1,
  "acceptedResourceRoles": [
    "slave_public"
  ],
  "container": {
    "type": "MESOS",
    "volumes": [],
    "portMappings": [
      {
        "containerPort": 0,
        "hostPort": 0,
        "labels": {},
        "name": "default",
        "protocol": "tcp",
        "servicePort": 10001
      }
    ]
  },
  "networks": [
    {
      "mode": "container/bridge"
    }
  ],
  "portDefinitions": []
}
```

```json
{
  "id": "/kapua-sql",
  "cmd": "docker run -p 8181:8181 -p 3306:3306 kapua/kapua-sql:0.3.2\n",
  "cpus": 0.2,
  "mem": 128,
  "disk": 0,
  "instances": 1,
  "acceptedResourceRoles": [
    "slave_public"
  ],
  "container": {
    "type": "MESOS",
    "volumes": [],
    "portMappings": [
      {
        "containerPort": 0,
        "hostPort": 0,
        "labels": {},
        "name": "default",
        "protocol": "tcp",
        "servicePort": 10000
      }
    ]
  },
  "networks": [
    {
      "mode": "container/bridge"
    }
  ],
  "portDefinitions": []
}
```

on public slave:

docker ps

docker inspect b814c18ef82c | grep Name
