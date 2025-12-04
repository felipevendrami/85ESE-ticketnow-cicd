## 📦 Projeto CI/CD – Pipeline Unificado dos Microsserviços

Alunos: Diogo Sardarga, Felipe Vendrami, Graciele Rodrigues

Este repositório centraliza toda a infraestrutura de **Integração Contínua (CI)** e **Entrega Contínua (CD)** utilizada pelos microsserviços do ecossistema da aplicação. Ele funciona como um repositório orquestrador, recebendo alterações espelhadas dos serviços hospedados no GitLab e executando automaticamente testes, análises, build de imagens e deploy.

---

## 🚀 Objetivo do Repositório

O propósito deste repositório é fornecer uma pipeline única, padronizada e desacoplada dos serviços individuais, garantindo que todos os microsserviços sigam os mesmos critérios de qualidade, segurança e entrega.  
A padronização centralizada reduz complexidade, facilita manutenção e permite que todos os serviços evoluam com governança técnica comum.

---

## 🔁 Integração com os Microsserviços (Mirror GitLab → CI/CD Repo)

Cada microsserviço mantém seu repositório principal no **GitLab**, onde ocorre o desenvolvimento.

Este repositório CI/CD recebe o código de cada microsserviço por meio de **espelhamento (mirror)**, acionando a pipeline assim que um novo commit é sincronizado.

Benefícios:
- Padronização de qualidade e build  
- Centralização da gestão das pipelines  
- Versionamento consistente de imagens Docker  
- Menos complexidade nos repositórios individuais  

---

## 🧪 Verificação de Qualidade (SonarCloud/SonarQube)

Conforme definido no T2, cada microsserviço é tratado como um **projeto independente** dentro do SonarCloud/SonarQube.

A pipeline executa:
- análise estática de código  
- verificação de vulnerabilidades  
- análise de code smells  
- cobertura de testes (quando existente)  
- validação de Quality Gates  

Cada microsserviço possui sua própria configuração e seu próprio token armazenado nos **Secrets do GitHub**.

---

## 🛠️ Build e Publicação da Imagem Docker

Após a etapa de qualidade, a pipeline realiza:

1. **Build da imagem Docker** referente ao microsserviço analisado  
2. **Tag automática** (branch + hash)  
3. **Push para o Docker Hub**  

Esse processo garante:
- reprodutibilidade  
- rastreabilidade  
- padronização da estrutura de imagens entre serviços  

---

## 🚢 Deploy Automatizado

O repositório também contém pipelines de **CD (Continuous Deployment)** responsáveis por:

- atualizar automaticamente imagens nos ambientes  
- realizar deploy padronizado via workflows  
- suportar rollback baseado em versões geradas  

O deploy segue o fluxo definido no T2, garantindo consistência e isolamento entre ambientes (dev, homologação e produção).

---


---

## 🔐 Secrets Necessários

| Secret | Finalidade |
|--------|------------|
| `SONAR_TOKEN_<SERVICE>` | Autenticação para análise no Sonar |
| `DOCKERHUB_USERNAME` | Usuário do Docker Hub |
| `DOCKERHUB_TOKEN` | Token do Docker Hub |
| `DEPLOY_KEY` | Token ou chave SSH para executar deploy |

Cada microsserviço possui seu token dedicado para análise, conforme orientações do T2.

---

## 📘 Fluxo Geral da Pipeline (do commit ao deploy)

1. Mirror envia o commit do GitLab → repositório CI/CD  
2. Pipeline inicia automaticamente  
3. Testes unitários são executados  
4. Código analisado no SonarCloud/SonarQube  
5. Quality Gate validado  
6. Imagem Docker compilada  
7. Imagem enviada ao Docker Hub  
8. Deploy executado conforme ambiente selecionado  

---

## 📑 Benefícios da Arquitetura Definida no T2

- Redução de complexidade em cada microsserviço  
- Centralização das políticas de qualidade  
- Deploys consistentes e auditáveis  
- Pipelines reutilizáveis e de fácil manutenção  
- Padronização completa do ciclo de desenvolvimento  



