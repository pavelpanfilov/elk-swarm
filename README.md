# elk-swarm
ELK cluster with elastalert for docker swarm

Xpack license set to basic. Xpack security disabled.
Update slack hook url and elastalert rules (check sample in elastalert/rules.yml) before deployment.

Update target nodes with elk label:
```shell
$ docker node update --label-add elk=true YOUR_NODE
```

Deploy:
```shell
$ docker stack deploy -c docker-stack.yml elk
```