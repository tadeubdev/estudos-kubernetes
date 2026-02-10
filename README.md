# kubernetes

Explicações:
- pod.yaml: arquivo de configuração para criar um pod.
- rs.yaml: arquivo de configuração para criar um ReplicaSet. O replicaSet é responsável por manter um número específico de réplicas de um pod em execução.
- deploy.yaml: arquivo de configuração para criar um Deployment. O Deployment é uma camada de abstração sobre o ReplicaSet, que gerencia a criação e atualização de ReplicaSets para garantir que o número desejado de réplicas de um pod esteja sempre em execução. Ele também facilita a atualização de aplicativos sem tempo de inatividade, permitindo a criação de novas réplicas e a exclusão gradual das réplicas antigas. Verifica também a versão do aplicativo em execução, garantindo que a versão correta esteja sempre ativa. O Deployment é uma maneira mais avançada e recomendada de gerenciar a implantação de aplicativos em Kubernetes, em comparação com o uso direto de ReplicaSets.
- service.yaml: arquivo de configuração para criar um Service. O Service é um recurso do Kubernetes que define uma maneira de acessar um conjunto de pods, geralmente por meio de um endereço IP e uma porta. Ele atua como um balanceador de carga interno, distribuindo o tráfego entre os pods que correspondem a um seletor específico. O Service pode ser exposto externamente usando diferentes tipos, como NodePort, LoadBalancer ou Ingress, permitindo que os usuários acessem os aplicativos em execução dentro do cluster Kubernetes. Ele é essencial para garantir a comunicação entre os pods e para expor os serviços para o mundo externo de forma segura e eficiente.

## Comandos para executar o projeto:

1. **Aplicar o Deployment** (cria os pods):
```bash
kubectl apply -f deploy.yaml
```

2. **Aplicar o Service** (expõe os pods):
```bash
kubectl apply -f service.yaml
```

3. **Verificar os pods criados**:
```bash
kubectl get pods
```

4. **Verificar o service**:
```bash
kubectl get svc
```

5. **Acessar a aplicação** (se estiver usando kind):
```bash
kubectl port-forward service/nginx-service 8080:80
```
Depois acesse: http://localhost:8080

6. **Instalar o Ingress Controller** (necessário antes de usar Ingress):
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.2/deploy/static/provider/cloud/deploy.yaml
```

7. **Aplicar o Ingress** (expõe a aplicação usando um domínio):
```bash
kubectl apply -f ingress.yaml
```

8. **Adicionar o domínio ao /etc/hosts** (para acessar localmente):
```bash
echo "127.0.0.1 api.local" | sudo tee -a /etc/hosts
```

9. **Verificar o conteúdo do /etc/hosts**:
```bash
cat /etc/hosts
```

10. **Fazer port-forward do Ingress Controller** (se estiver usando kind/minikube):
```bash
kubectl port-forward -n ingress-nginx service/ingress-nginx-controller 8080:80
```

11. **Testar o acesso via curl**:
```bash
curl http://api.local:8080
```

Ou, se o Ingress Controller estiver rodando na porta 80:
```bash
curl http://api.local
```

## Comandos úteis:

- Ver detalhes do deployment:
```bash
kubectl describe deployment nginx-deploy
```

- Ver logs de um pod:
```bash
kubectl logs <nome-do-pod>
```

- Deletar recursos:
```bash
kubectl delete -f deploy.yaml
kubectl delete -f service.yaml
kubectl delete -f ingress.yaml
```