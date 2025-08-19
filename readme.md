# Sistema de Portaria Alfa V0.1

## 📋 Visão Geral

Sistema de controle de acesso para condomínios e hotéis, desenvolvido em Django. Gerencia moradores, visitantes, funcionários e registros de entrada/saída com interface administrativa completa.

**Status do Projeto**: 40% concluído

## 🚀 Instalação

### Pré-requisitos
- Python 3.8+
- pip

### Configuração Rápida

1. **Configuração Inicial** (primeira vez):
   ```bash
   setup.bat
   ```

2. **Iniciar Sistema**:
   ```bash
   start.bat
   ```

3. **Acesso**:
   - URL: http://localhost:8000/admin/
   - Usuário: `admin`
   - Senha: `admin123`

### Configuração Manual

```bash
# Criar ambiente virtual
python -m venv venv
venv\Scripts\activate

# Instalar dependências
pip install -r requirements.txt

# Configurar banco de dados
python manage.py makemigrations
python manage.py migrate

# Criar superusuário
python manage.py createsuperuser

# Iniciar servidor
python manage.py runserver
```

## 🏗️ Arquitetura

### Aplicações Django

- **authentication**: Sistema de usuários e autenticação
- **residents**: Gestão de moradores/hóspedes
- **visitors**: Controle de visitantes
- **employees**: Gestão de funcionários
- **access_control**: Registros de entrada/saída
- **audit**: Logs e auditoria do sistema

### Banco de Dados
- **Desenvolvimento**: SQLite3
- **Produção**: PostgreSQL (recomendado)

### Estrutura de Diretórios

v0.1/
├── portaria/           # Configurações Django
├── authentication/     # App de autenticação
├── residents/          # App de moradores
├── visitors/           # App de visitantes
├── employees/          # App de funcionários
├── access_control/     # App de controle de acesso
├── audit/              # App de auditoria
├── static/             # Arquivos estáticos
├── templates/          # Templates HTML
└── manage.py           # Gerenciador Django


## 📚 Documentação Adicional

- **Problemas Técnicos**: Ver `troubleshooting.md`
- **Configurações**: Ver arquivo `.env.example`

## 🔧 Comandos Úteis

```bash
# Verificar migrações pendentes
python manage.py showmigrations

# Criar nova migração
python manage.py makemigrations app_name

# Aplicar migrações
python manage.py migrate

# Acessar shell Django
python manage.py shell

# Coletar arquivos estáticos
python manage.py collectstatic
```

## 📊 Status de Desenvolvimento

### ✅ Concluído
- [x] Infraestrutura base Django
- [x] Modelos de dados principais
- [x] Sistema de autenticação
- [x] Interface administrativa
- [x] Migrações de banco de dados

### 🔄 Em Desenvolvimento
- [ ] Interface frontend
- [ ] APIs REST
- [ ] Sistema de notificações
- [ ] Relatórios avançados

### 📋 Próximos Passos
1. Desenvolver interface frontend
2. Implementar APIs REST
3. Adicionar sistema de notificações
4. Criar relatórios e dashboards
5. Testes automatizados