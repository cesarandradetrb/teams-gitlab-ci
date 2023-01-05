# Notificando canais do Teams a partir de um pipeline GitLab CI

Este repositório contém exemplos de como criar cards de notificação para canais do [Microsoft Teams](https://www.microsoft.com/pt-br/microsoft-teams/) a partir de um pipeline [GitLab](https://gitlab.com) CI.

## Escopo

Este repositório tem como objetivo gerar um card avisando de alguma falha durante a execução do pipeline.

## Usando no .gitlab-ci.yml do seu projeto

* Crie um conector no canal que deverá receber as notificações; se tiver alguma dúvida, [consulte a documentação](https://docs.microsoft.com/pt-br/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook).
* Adicione a variável `WEBHOOK_TEAMS` às variáveis de CI/CD do projeto.
* Copie `simples.yml` e/ou `completo.yaml` para um repositório Gitlab.
* Insira para uma notificação simples:

```yaml
include:
  - remote: "https://gitlab.com/meurepo/raw/main/simples.yml"
```

* Insira para uma notificação completa (o nome do projeto aparece na notificação, o que pode ser útil caso um mesmo conector seja utilizado por vários projetos):

```yaml
include:
  - remote: "https://gitlab.com/meurepo/raw/main/completo.yml"
```

* Insira para que seja enviada uma notificação caso ocorra algum problema no pipeline (caso já exista uma seção `after_script`, basta adicionar a diretiva *!reference* no existente):

```yaml
default:
  after_script:
    - !reference [.notifica_erro, after_script]
```
