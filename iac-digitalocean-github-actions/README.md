# iac-digitalocean-github-actions
[![CI-CD](https://github.com/desafios-08-2022/iac-digitalocean-github-actions/actions/workflows/ci-cd.yml/badge.svg?branch=main)](https://github.com/desafios-08-2022/iac-digitalocean-github-actions/actions/workflows/ci-cd.yml)

crie e populo o arquivo terraform.tfvars conforme exemplo
o Token da DO é na console no menu API

```
terraform plan -out plan1
terraform apply plan1
cp kube_config.yaml ~/.kube/config  # Cuidado - este comando irá sobrepor o arquivo config da pasta ~/.kube

kubectl apply -f kube-news/k8s/deployment.yaml
```
```
watch kubectl get svc
```

espere gerar o IP, acesse a aplicação no navegador e faça seus testes!



Faça a configuração do seu github-actions

crie as secrets em Settings -> secrets -> Actions

```
DOCKERHUB_PWD -> seu usuario no dockerhub
DOCKERHUB_USER -> sua senha no dockerhub
KUBECONFIG_K8S -> conteudo do seu arquivo ~/.kube/config
```

1 - configure conforme sua realidade
2 - suba o projeto
3 - altere o arquivo "./kube-news/src/views/partial/nav-bar.ejs" na linha 5
4 - suba o projeto novamente e verifique a alteração


terraform destroy