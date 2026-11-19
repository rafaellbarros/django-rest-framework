# django-rest-framework

Projeto Django com Django REST Framework. Este guia descreve os passos para configurar o ambiente de desenvolvimento no **Linux Mint / Ubuntu** e executar o projeto localmente.

## Pré-requisitos

- Linux Mint ou Ubuntu (ou derivados)
- Acesso ao terminal com permissões `sudo`
- Git instalado
- Projeto já clonado do repositório

## 1. Configuração do ambiente Python

### 1.1 Verificar a versão do Python

```bash
python3 --version
```

> Recomenda-se Python 3.8 ou superior.

### 1.2 Instalar ferramentas essenciais

Atualize a lista de pacotes e instale o Python, o `pip` e o módulo `venv` (necessário para criar ambientes virtuais):

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

## 2. Preparar o projeto

### 2.1 Acessar o diretório do projeto

```bash
cd /basico/escola
```

### 2.2 Criar o ambiente virtual

O ambiente virtual isola as dependências do projeto das bibliotecas globais do sistema:

```bash
python3 -m venv venv
```

### 2.3 Ativar o ambiente virtual

```bash
source venv/bin/activate
```

> Após a ativação, o prompt do terminal exibirá o prefixo `(venv)`.
> **Importante:** sempre ative o ambiente virtual antes de executar qualquer comando do projeto em novas sessões de terminal.

## 3. Instalar dependências

Com o ambiente virtual ativado, instale as dependências listadas no `requirements.txt`:

```bash
pip install -r requirements.txt
```

## 4. Configurar o banco de dados

### 4.1 Executar as migrações

Cria as tabelas no banco de dados conforme os modelos definidos no projeto:

```bash
python manage.py migrate
```

> Se o projeto usar variáveis de ambiente (arquivo `.env`), crie-o com base no exemplo fornecido (ex.: `.env.example`) antes de rodar as migrações.

### 4.2 Criar uma conta de administrador

Permite acessar o painel administrativo do Django em `/admin`:

```bash
python manage.py createsuperuser
```

Siga as instruções para definir usuário, e-mail e senha.

## 5. Executar o projeto

Inicie o servidor de desenvolvimento:

```bash
python manage.py runserver
```

Acesse no navegador:

- Aplicação: http://127.0.0.1:8000/
- Painel admin: http://127.0.0.1:8000/admin/

Para encerrar o servidor, pressione `Ctrl + C`.

## Comandos úteis

| Comando | Descrição |
|---|---|
| `source venv/bin/activate` | Ativa o ambiente virtual |
| `deactivate` | Desativa o ambiente virtual |
| `pip freeze > requirements.txt` | Atualiza o arquivo de dependências |
| `python manage.py makemigrations` | Gera novas migrações a partir dos modelos |
| `python manage.py migrate` | Aplica as migrações ao banco |
| `python manage.py runserver` | Inicia o servidor de desenvolvimento |
| `python manage.py test` | Executa os testes do projeto |

## Solução de problemas

- **`ModuleNotFoundError` ao rodar o projeto:** o ambiente virtual provavelmente não está ativado. Execute `source venv/bin/activate` e tente novamente.
- **Erro de permissão no `pip install`:** verifique se o ambiente virtual está ativo (o prefixo `(venv)` deve aparecer no prompt).
- **Porta 8000 em uso:** inicie o servidor em outra porta com `python manage.py runserver 8080`.
- **`django.db.utils.OperationalError`:** execute `python manage.py migrate` antes de iniciar o servidor.

