# Kubernetes Cluster com Ansible + AWS

Projeto desenvolvido durante o treinamento **Descomplicando o Ansible – LinuxTips**, com foco na **criação automatizada de um cluster Kubernetes na AWS utilizando Ansible**, incluindo observabilidade com Prometheus e Grafana e deploy de aplicações no cluster.

---

## 🎯 Objetivo do Projeto

- Provisionar infraestrutura na AWS
- Criar um cluster Kubernetes utilizando `kubeadm`
- Automatizar bootstrap de master e workers com Ansible
- Instalar Helm
- Instalar Prometheus + Grafana
- Validar métricas com carga real
- Realizar deploy de aplicações Kubernetes via Ansible
- Servir como laboratório e base de estudos DevOps

---

## 🧱 Estrutura do Projeto

```
projeto-k8s-cluster/
├── install_k8s
│   ├── hosts
│   ├── main.yml
│   └── roles
│       ├── bootstrap
│       ├── install-helm
│       ├── install-monitoring
│       └── join-workers
│
├── deploy-app-v1
│   ├── hosts
│   ├── main.yml
│   └── roles
│       └── deploy-app
│           ├── tasks
│           ├── templates
│           ├── files
│           ├── vars
│           └── defaults
└── README.md
```

---

## ⚙️ Pré-requisitos

- Ansible instalado na máquina de controle
- Chave SSH válida para acesso às instâncias EC2
- Instâncias EC2 **Ubuntu 24.04**
- Cluster Kubernetes funcional
- Security Group liberando:
  - SSH (22)
  - NodePort (30000–32767)

---

## 🚀 Criação do Cluster Kubernetes

Dentro do diretório `install_k8s`:

```bash
ansible-playbook -i hosts main.yml
```

---

## 📊 Acesso ao Grafana

Para acessar o Grafana, verifique o IP de algum node:

```bash
kubectl get nodes -o wide
```

Acesse usando o IP público de qualquer node:

```
http://IP_PUBLICO_DO_NODE:31120
```

---

## 🔐 Credenciais do Grafana

Usuário: `admin`

Senha:

```bash
kubectl -n monitoring get secret prometheus-grafana \
  -o jsonpath="{.data.admin-password}" | base64 -d
```

---

## 🚀 Deploy da Aplicação Giropops

Dentro do diretório `deploy-app-v1`:

```bash
ansible-playbook -i hosts main.yml
```

---

## 🌐 Acesso à Aplicação Giropops

```bash
kubectl get svc giropops
```

Exemplo:

```
http://IP_PUBLICO_DO_NODE:32222
```

---

## 📄 Licença

MIT License

