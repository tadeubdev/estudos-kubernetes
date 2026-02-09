# kubernetes

Explicações:
- pod.yaml: arquivo de configuração para criar um pod.
- rs.yaml: arquivo de configuração para criar um ReplicaSet. O replicaSet é responsável por manter um número específico de réplicas de um pod em execução.
- deploy.yaml: arquivo de configuração para criar um Deployment. O Deployment é uma camada de abstração sobre o ReplicaSet, que gerencia a criação e atualização de ReplicaSets para garantir que o número desejado de réplicas de um pod esteja sempre em execução. Ele também facilita a atualização de aplicativos sem tempo de inatividade, permitindo a criação de novas réplicas e a exclusão gradual das réplicas antigas. Verifica também a versão do aplicativo em execução, garantindo que a versão correta esteja sempre ativa. O Deployment é uma maneira mais avançada e recomendada de gerenciar a implantação de aplicativos em Kubernetes, em comparação com o uso direto de ReplicaSets.
- service.yaml: arquivo de configuração para criar um Service. O Service é um recurso do Kubernetes que define uma maneira de acessar um conjunto de pods, geralmente por meio de um endereço IP e uma porta. Ele atua como um balanceador de carga interno, distribuindo o tráfego entre os pods que correspondem a um seletor específico. O Service pode ser exposto externamente usando diferentes tipos, como NodePort, LoadBalancer ou Ingress, permitindo que os usuários acessem os aplicativos em execução dentro do cluster Kubernetes. Ele é essencial para garantir a comunicação entre os pods e para expor os serviços para o mundo externo de forma segura e eficiente.

## Comandos:
````
kubectl apply -f pod.yaml
kubectl apply -f rs.yaml
kubectl apply -f deploy.yaml
kubectl apply -f service.yaml
````