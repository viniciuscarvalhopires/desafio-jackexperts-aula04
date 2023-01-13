# desafio-jackexperts-aula04
Repositório dedicado ao desenvolvimento do desafio 04 jackexperts

## Demonstração

Acesse o link: http://desafio-vinicius.stag.jac.bsb.br/

## Passo a passo realizado

Exporte as configurações do kubernetes, neste caso no Windows
```bash
  set KUBECONFIG=Kubeconfig
```

Certifique-se de estar conectado ao cluster kubernetes
```bash
  kubectl cluster-info
```

Crie seu chart localmente

```bash
  helm create <seu-chart>
```

Edite os valores do values.yaml e outros arquivos para que sua imagem seja exibida, por exemplo, neste caso, em values.yaml:

```bash
  image:
  repository: vinicpires/vinicius-jackexperts
  pullPolicy: IfNotPresent
  tag: final
```
Lembre-se de habilitar o Ingress e inserir a url no host:

```bash
  ingress:
  enabled: true
  className: ""
  annotations:
    {}
    # kubernetes.io/ingress.class: nginx
    # kubernetes.io/tls-acme: "true"
  hosts:
    - host: desafio-vinicius.stag.jac.bsb.br
      paths:
        - path: /
          pathType: ImplementationSpecific
```

Após realizar as alterações, utilize o comando:

```bash
    healm install <sua-release> ./<seu-chart> --create-namespace -n <seu-namespace>
```

Caso tenha êxito, basta acessa a url que inseriu no host

