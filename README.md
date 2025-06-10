
# FastAPI + React + Jenkins + Kubernetes

Projeto para aprendizado com construção e deploy de uma aplicação (backend + frontend) com deploy no Kubernetes e automação CI/CD utilizando o Jenkins.


## Rodando localmente o backend no Docker + publicação no Dockerhub

Faça o build da imagem (esteja no diretório backend)

```bash
  docker build --no-cache -t fastapi-backend .
```

Execute o container (verifique as portas)

```bash
  docker run -d -p 127.0.0.1:8000:8000 --name fastapi-backend fastapi-backend
```

Renomeie sua imagem para o padrão do Dockerhub (coloque o seu usuário)

```bash
  docker tag fastapi-backend SEU_USUARIO_DOCKERHUB/fastapi-backend:1
```

Publique o container no Dockerhub (esteja logado) (coloque o seu usuário)

```bash
  docker push SEU_USUARIO_DOCKERHUB/fastapi-backend:1
```

