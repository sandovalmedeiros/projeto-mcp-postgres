# 🧠 Projeto MCP + PostgreSQL

Este projeto configura um ambiente Docker que integra o **MCP Server** com um banco de dados **PostgreSQL**. Ele está preparado para funcionar com ferramentas que usam o **Model Context Protocol (MCP)**, como o Claude Desktop ou outros clientes compatíveis com MCP.

---

## 📦 Estrutura do Projeto

```plaintext
.
├── .env                         # Variáveis de ambiente (credenciais e URL de conexão)
├── docker-compose.yml           # Configuração do Docker para PostgreSQL e MCP Server
└── claude_desktop_config.json   # Configuração do MCP Server para Claude Desktop
```

---

## ⚙️ Como Funciona

O projeto sobe dois serviços:

1. **PostgreSQL**
   - Versão: `15`
   - Porta exposta no host: `5433`
   - Banco: `nome_do_banco`
   - Usuário: `seu_usuario`
   - Senha: `sua_senha`
   - Schema usado: `nome_do_schema`

2. **MCP Server (PostgreSQL)**
   - Conecta-se ao banco via `POSTGRES_URL`
   - Exposto para ferramentas externas via protocolo MCP
   - Configurado para trabalhar com o schema `definido_pelo_usuario`

A configuração no `claude_desktop_config.json` permite que o Claude Desktop (ou outro cliente MCP) reconheça automaticamente este servidor.

---

## 🚀 Instalação e Execução

### 1. Pré-requisitos

- Docker instalado: [https://www.docker.com](https://www.docker.com)
- (Opcional) Claude Desktop ou outro cliente MCP instalado

---

### 2. Clonar o repositório

```bash
git clone https://github.com/sandovalmedeiros/projeto-mcp-postgres.git
cd projeto-mcp-postgres
```

---

### 3. Subir os containers

```bash
docker-compose up -d
```

Isso irá:
- Inicializar o banco PostgreSQL na porta `5433`
- Subir o MCP Server vinculado ao banco e ao schema `seu_schema_definido`

---

### 4. Verificar se está rodando

```bash
docker-compose ps
```

Você deve ver ambos os serviços (`postgres` e `mcp-server-postgres`) em execução.

---

## 🗃️ Detalhes do Banco de Dados

| Parâmetro   | Valor           |
|-------------|-----------------|
| **Host**    | `localhost`     |
| **Porta**   | `5433`          |
| **Banco**   | `nome_do Banco` |
| **Usuário** | `nome_usr`      |
| **Senha**   | `senha_do_usr`  |
| **Schema**  | `nome_do_schema`|

> 🔐 As credenciais e configurações são gerenciadas via o arquivo `.env`

---

## 🧠 Integração com Claude Desktop

1. Copie o conteúdo do arquivo `claude_desktop_config.json` para o diretório de configuração do Claude:

   ```
   C:\Users\SeuUsuario\.claude\claude_desktop_config.json
   ```

2. Reinicie o Claude Desktop.
3. Selecione o MCP Server chamado `"postgres"` para começar a consulta estruturada ao seu banco de dados.

---

## 🧼 Encerrar e Limpar o Ambiente

Para parar os serviços e remover volumes (dados do banco), use:

```bash
docker-compose down -v --remove-orphans
```

Se quiser apagar tudo (incluindo imagens e cache):

```bash
docker system prune -a --volumes
```

> ⚠️ Atenção: isso **remove todos os containers, imagens não usadas, volumes e redes**. Use com cuidado.

---

## 📄 Licença

Este projeto é distribuído para fins educacionais e pode ser adaptado livremente.

---

## ✉️ Contato

Para dúvidas, sugestões ou problemas, abra uma [Issue](https://github.com/sandovalmedeiros/projeto-mcp-postgres/issues) no repositório.
