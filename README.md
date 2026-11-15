# 🚀 Projeto Prático — Pipeline CI/CD com Deploy em Nuvem

## 1. Sobre o projeto

Este projeto foi desenvolvido como atividade prática da disciplina de DevOps, com o objetivo de aplicar os conceitos de Integração Contínua (CI) e Entrega Contínua (CD), utilizando ferramentas de versionamento, conteinerização e automação de deploy em nuvem.

A aplicação consiste em uma página web simples, desenvolvida com HTML5 e CSS3, contendo a identificação dos integrantes da equipe e informações sobre o projeto.

O processo de publicação é automatizado por meio do GitHub Actions, utilizando Docker para conteinerização e Render como provedor de hospedagem em nuvem.

## 2. Objetivos

- Desenvolver uma aplicação web simples e funcional.
- Versionar o código-fonte utilizando Git e GitHub.
- Criar um ambiente conteinerizado com Docker.
- Configurar um pipeline CI/CD utilizando GitHub Actions.
- Automatizar o processo de deploy em ambiente de nuvem.
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
- **README.md:** documentação do projeto.

## 6. Arquitetura da solução

O projeto utiliza uma arquitetura simples de integração e entrega contínuas, conectando o repositório GitHub ao ambiente de hospedagem em nuvem.

O fluxo de funcionamento é composto pelas seguintes etapas:

1. O desenvolvedor realiza alterações no código-fonte.
2. As alterações são enviadas para o repositório GitHub, na branch `main`.
3. O GitHub Actions identifica o novo commit e inicia automaticamente o workflow.
4. O pipeline realiza o checkout do código e verifica a existência dos arquivos essenciais.
5. O GitHub Actions envia uma solicitação de deploy ao Render por meio de um Deploy Hook armazenado como segredo.
6. O Render realiza o processo de publicação da aplicação utilizando o Dockerfile.
7. Após a conclusão do deploy, a aplicação fica disponível por meio de uma URL pública.

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

O pipeline foi configurado utilizando o GitHub Actions, por meio do arquivo:

`.github/workflows/deploy.yml`

O workflow é acionado automaticamente sempre que ocorre um `push` na branch `main`.

Atualmente, o pipeline contempla:

- Checkout do código-fonte.
- Validação da existência dos arquivos essenciais.
- Solicitação de deploy ao Render por meio de um endereço armazenado em segredo.

O objetivo é automatizar o processo de publicação, reduzindo a necessidade de execução manual das etapas de deploy.

### Segurança

Para proteger informações sensíveis, o endereço do Deploy Hook do Render é armazenado no recurso **GitHub Secrets**, utilizando a variável:

`RENDER_DEPLOY_HOOK_URL`

Dessa forma, informações confidenciais não precisam ser inseridas diretamente no código-fonte ou disponibilizadas publicamente no repositório.

## 9. Deploy em nuvem

O Render foi escolhido como provedor de hospedagem para disponibilizar a aplicação em ambiente de nuvem.

A integração utiliza o Dockerfile presente no repositório para definir o ambiente de execução da aplicação.

O GitHub Actions realiza a solicitação de deploy automaticamente após as alterações enviadas à branch principal.

**URL da aplicação:** [Inserir aqui a URL pública do Render após a validação do deploy]

## 10. Considerações finais

O desenvolvimento deste projeto proporciona uma experiência prática com conceitos fundamentais de DevOps, permitindo compreender como ferramentas de versionamento, conteinerização e automação podem trabalhar de forma integrada.

A utilização do GitHub Actions permite automatizar etapas do processo de entrega, enquanto o Docker proporciona maior padronização do ambiente de execução e o Render possibilita a disponibilização da aplicação em nuvem.

Além da implementação técnica, o projeto contribui para o aprendizado sobre integração entre ferramentas, organização do código-fonte, segurança de informações e trabalho colaborativo.

---

**Projeto acadêmico desenvolvido para a disciplina de DevOps.**
