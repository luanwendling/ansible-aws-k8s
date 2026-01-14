# Treinamento Descomplicando o Ansible pela LinuxTips

Projeto do treinamento para instação de um cluster kubernetes utilizando o Ansible + AWS


## Fases do projeto
```
- Provisioning => Criar as instâncias/vms para o nosso cluster.
- Install_K8s => Criação do cluster, Criação dos workers, Instalação do Helm, Prometheus e Grafana
- Deploy_app => Deploy de uma aplicação extra
```
## Atualização
- Para acessar o grafana, verifique o ip de algum node: kubectl get nodes -o wide e acessar com o ip publico de algum deles

o usuario do grafana e "admin" e a senha você consegue com esse comando:
kubectl -n monitoring get secret prometheus-grafana \
  -o jsonpath="{.data.admin-password}" | base64 -d

## License

[MIT](https://choosealicense.com/licenses/mit/)
