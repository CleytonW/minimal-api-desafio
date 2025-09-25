# Minimal API - Sistema de Gerenciamento de Veículos

Uma API REST mínima desenvolvida em .NET 7 para gerenciamento de veículos e administradores, utilizando Entity Framework Core, MySQL, autenticação JWT e testes automatizados.

## Principais seções:

- **Autenticação JWT**: Sistema de login seguro com tokens JWT
- **Gerenciamento de Administradores**: CRUD completo com controle de acesso baseado em perfis
- **Gerenciamento de Veículos**: CRUD completo para cadastro de veículos
- **Autorização baseada em Roles**: Diferentes níveis de acesso (Admin, Editor)
- **Paginação**: Listagem paginada de recursos
- **Documentação Swagger**: Interface interativa para testes da API
- **Testes Automatizados**: Suite de testes unitários e de integração

## Tecnologias Utilizadas

- **.NET 7**
- **ASP.NET Core Minimal APIs**
- **Entity Framework Core 7.0.14**
- **MySQL** (via Pomelo.EntityFrameworkCore.MySql)
- **JWT Bearer Authentication**
- **Swagger/OpenAPI**
- **xUnit** (para testes)

## Arquitetura

O projeto segue uma arquitetura em camadas:

```
├── Api/                          # Camada de apresentação
│   ├── Program.cs               # Ponto de entrada da aplicação
│   ├── Startup.cs               # Configuração da aplicação
│   ├── Dominio/                 # Camada de domínio
│   │   ├── DTOs/                # Data Transfer Objects
│   │   ├── Entidades/           # Entidades do domínio
│   │   ├── Enuns/               # Enumerações
│   │   ├── Interfaces/          # Contratos de serviços
│   │   ├── ModelViews/          # Models para visualização
│   │   └── Servicos/            # Serviços de negócio
│   ├── Infraestrutura/          # Camada de infraestrutura
│   │   └── Db/                  # Contexto do banco de dados
│   └── Migrations/              # Migrações do Entity Framework
└── Test/                        # Projeto de testes
    ├── Domain/                  # Testes de domínio
    ├── Requests/               # Testes de endpoints
    ├── Helpers/                # Utilitários para testes
    └── Mocks/                  # Mocks para testes
```

## Pré-requisitos

- [.NET 7 SDK](https://dotnet.microsoft.com/download/dotnet/7.0)
- [MySQL Server](https://dev.mysql.com/downloads/mysql/)
- [Visual Studio Code](https://code.visualstudio.com/) ou [Visual Studio](https://visualstudio.microsoft.com/)

## Configuração

### 1. Clone o repositório
```bash
git clone https://github.com/CleytonW/minimal-api-desafio.git
cd minimal-api-desafio
```

### 2. Configure a string de conexão
Edite o arquivo `Api/appsettings.json` e ajuste a string de conexão para seu MySQL:

```json
{
  "ConnectionStrings": {
    "MySql": "Server=localhost;Database=minimal_api;Uid=root;Pwd=sua_senha;"
  }
}
```

### 3. Execute as migrações
```bash
cd Api
dotnet ef database update
```

### 4. Execute a aplicação
```bash
dotnet run
```

A aplicação estará disponível em `https://localhost:7297` ou `http://localhost:5297`.

## Documentação da API

### Acesse a documentação Swagger
Após executar a aplicação, acesse: `https://localhost:7297/swagger`

### Endpoints principais:

#### Home
- `GET /` - Página inicial da API

#### Administradores
- `POST /administradores/login` - Autenticação
- `GET /administradores` - Listar administradores (Admin apenas)
- `GET /administradores/{id}` - Buscar administrador por ID (Admin apenas)
- `POST /administradores` - Criar novo administrador (Admin apenas)

#### Veículos
- `POST /veiculos` - Criar veículo (Admin/Editor)
- `GET /veiculos` - Listar veículos (Autenticado)
- `GET /veiculos/{id}` - Buscar veículo por ID (Admin/Editor)
- `PUT /veiculos/{id}` - Atualizar veículo (Admin apenas)
- `DELETE /veiculos/{id}` - Excluir veículo (Admin apenas)

### Autenticação

A API utiliza JWT Bearer Token. Para autenticar:

1. Faça login através do endpoint `POST /administradores/login`
2. Utilize o token retornado no header `Authorization: Bearer {token}`

#### Perfis de usuário:
- **Adm**: Acesso total a todos os recursos
- **Editor**: Pode criar e visualizar veículos, mas não pode editar ou excluir

## Executando os Testes

### Testes unitários
```bash
cd Test
dotnet test
```

### Estrutura dos testes:
- **Domain/Entidades/**: Testes das entidades de domínio
- **Domain/Servicos/**: Testes dos serviços de negócio
- **Requests/**: Testes de integração dos endpoints
- **Mocks/**: Implementações mock para testes isolados

## Banco de Dados

### Entidades principais:

#### Administrador
- `Id` (int) - Chave primária
- `Email` (string, 255) - Email único do administrador
- `Senha` (string, 50) - Senha do administrador
- `Perfil` (string, 10) - Perfil de acesso (Adm/Editor)

#### Veiculo
- `Id` (int) - Chave primária
- `Nome` (string, 150) - Nome do veículo
- `Marca` (string, 100) - Marca do veículo
- `Ano` (int) - Ano de fabricação (mínimo 1950)

## Segurança

- Autenticação via JWT tokens
- Senhas armazenadas em texto plano (**Não recomendado para produção**)
- Controle de acesso baseado em roles
- CORS configurado para desenvolvimento

## Status do Projeto

Este projeto foi desenvolvido como um desafio técnico e inclui:

- API REST funcional
- Autenticação JWT
- Autorização por perfis
- CRUD completo
- Documentação Swagger
- Testes automatizados
- Migrações do banco de dados

## Melhorias Sugeridas para Produção

- [ ] Hash das senhas com bcrypt ou similar
- [ ] Validações mais robustas
- [ ] Logging estruturado
- [ ] Rate limiting
- [ ] Health checks
- [ ] Containerização com Docker
- [ ] CI/CD pipeline

## Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## Contribuição

1. Faça o fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

---

Desenvolvido por [CleytonW](https://github.com/CleytonW)
