
# 🚀 Projeto Prático — Pipeline CI/CD com Deploy em Nuvem

## 1. Sobre o projeto

Este projeto foi desenvolvido como atividade prática da disciplina de DevOps, com o objetivo de aplicar os conceitos de Integração Contínua (CI) e Entrega Contínua (CD), utilizando ferramentas de versionamento, conteinerização e automação de deploy em nuvem.

A aplicação consiste em uma página web desenvolvida com HTML5 e CSS3, contendo a identificação dos integrantes da equipe.

O processo de publicação é automatizado por meio do GitHub Actions, utilizando Docker para conteinerização, Nginx como servidor web e Render como provedor de hospedagem em nuvem.

## 2. Objetivos

- Desenvolver uma aplicação web simples e funcional.
- Versionar o código-fonte utilizando Git e GitHub.
- Criar um ambiente conteinerizado com Docker.
- Configurar um pipeline CI/CD utilizando GitHub Actions.
- Automatizar a validação e o processo de deploy em ambiente de nuvem.
- Disponibilizar a aplicação por meio de uma URL pública.

## 3. Tecnologias e ferramentas utilizadas

| Tecnologia | Finalidade |
|---|---|
| HTML5 | Estruturação da página web |
| CSS3 | Estilização e identidade visual |
| Git | Controle de versão |
| GitHub | Hospedagem do código-fonte |
| GitHub Actions | Automação do pipeline CI/CD |
| Docker | Conteinerização da aplicação |
| Nginx | Servidor web para disponibilização da página |
| Render | Hospedagem e deploy em nuvem |

## 4. Integrantes da equipe

- Andrea Freire
- Arthur Cabral
- Bruno Henrique
- Samuel Santana

## 5. Estrutura do projeto

```text
atvd-Devops/
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── docs/
│   └── arquitetura.md
│
├── Dockerfile
├── README.md
├── index.html
└── style.css
```

### Descrição dos arquivos

- **index.html:** contém a estrutura e o conteúdo da aplicação.
- **style.css:** responsável pela estilização e apresentação visual.
- **Dockerfile:** define as instruções para construção da imagem Docker.
- **deploy.yml:** configura o pipeline de automação do GitHub Actions.
- **arquitetura.md:** apresenta a documentação técnica e o diagrama da arquitetura da solução.
- **README.md:** documentação principal do projeto.

## 6. Arquitetura da solução

O projeto utiliza uma arquitetura de integração e entrega contínuas, conectando o repositório GitHub ao ambiente de hospedagem em nuvem.

O fluxo de funcionamento é composto pelas seguintes etapas:

1. O desenvolvedor realiza alterações no código-fonte.
2. As alterações são enviadas para o repositório GitHub, na branch `main`.
3. O GitHub Actions identifica o novo commit e inicia automaticamente o workflow.
4. O pipeline realiza o checkout do código-fonte.
5. É realizada a validação da existência dos arquivos essenciais.
6. O GitHub Actions constrói uma imagem Docker para validar a configuração da aplicação.
7. O pipeline envia uma solicitação de deploy ao Render por meio de um Deploy Hook armazenado como segredo.
8. O Render realiza seu próprio processo de construção e publicação utilizando o Dockerfile.
9. O Nginx disponibiliza a aplicação por meio de uma URL pública.

O diagrama completo e a descrição dos componentes estão disponíveis em:

[Documentação da Arquitetura](docs/arquitetura.md)

## 7. Conteinerização com Docker

A aplicação utiliza Docker para criar um ambiente padronizado de execução.

O Dockerfile utiliza a imagem `nginx:alpine`, uma versão leve do servidor web Nginx.

Durante a construção da imagem, os arquivos `index.html` e `style.css` são copiados para o diretório padrão de publicação do Nginx.

A porta 80 é disponibilizada para acesso à aplicação, enquanto o servidor permanece em execução em primeiro plano.

### Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/
COPY style.css /usr/share/nginx/html/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

### Executar localmente com Docker

Para construir a imagem:

```bash
docker build -t atvd-devops .
```

Para executar o contêiner:

```bash
docker run -d -p 8080:80 --name projeto-devops atvd-devops
```

Após iniciar o contêiner, a aplicação poderá ser acessada em:

`http://localhost:8080`

## 8. Pipeline CI/CD com GitHub Actions

O pipeline foi configurado utilizando GitHub Actions, por meio do arquivo:

`.github/workflows/deploy.yml`

O workflow é acionado automaticamente sempre que ocorre um `push` na branch `main`.

### Etapas do pipeline

O processo automatizado contempla as seguintes etapas:

**1. Checkout do código-fonte**

Obtém os arquivos do repositório para execução das etapas seguintes.

**2. Validação da estrutura de arquivos**

Verifica a existência dos arquivos essenciais para o funcionamento da aplicação, como `index.html` e `Dockerfile`.

**3. Construção da imagem Docker**

Executa o comando `docker build -t atvd-devops .`, verificando se a imagem da aplicação pode ser construída corretamente.

**4. Acionamento do deploy no Render**

Envia uma solicitação HTTP POST ao Deploy Hook do Render, iniciando o processo de publicação em nuvem.

### Segurança

Para proteger informações sensíveis, o endereço do Deploy Hook do Render é armazenado no recurso **GitHub Secrets**, utilizando a variável:

`RENDER_DEPLOY_HOOK_URL`

Dessa forma, informações confidenciais não precisam ser inseridas diretamente no código-fonte ou disponibilizadas publicamente no repositório.

### Histórico de execução

O GitHub Actions mantém o histórico das execuções do workflow, permitindo acompanhar o resultado de cada etapa, identificar falhas e verificar as execuções concluídas com sucesso.

## 9. Deploy em nuvem

O Render foi escolhido como provedor de hospedagem para disponibilizar a aplicação em ambiente de nuvem.

A integração utiliza o Dockerfile presente no repositório para definir o ambiente de execução da aplicação.

Após o acionamento do Deploy Hook pelo GitHub Actions, o Render realiza o processo de construção e publicação da aplicação.

**URL pública da aplicação:**

https://atvd-devops-e3cp.onrender.com/

## 10. Considerações finais

O desenvolvimento deste projeto proporciona uma experiência prática com conceitos fundamentais de DevOps, permitindo compreender como ferramentas de versionamento, conteinerização e automação podem trabalhar de forma integrada.

A utilização do GitHub Actions permite automatizar as etapas de validação e solicitação de publicação, enquanto o Docker proporciona maior padronização do ambiente de execução e o Render possibilita a disponibilização da aplicação em nuvem.

Além da implementação técnica, o projeto contribui para o aprendizado sobre integração entre ferramentas, organização do código-fonte, segurança de informações e trabalho colaborativo.

---

**Projeto acadêmico desenvolvido para a disciplina de DevOps.**
