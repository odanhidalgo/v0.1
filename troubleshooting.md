# Troubleshooting - Sistema de Portaria Alfa

## 🔧 Problemas Conhecidos e Soluções

### Erro de Importação AppConfig
**Problema**: `ImportError: cannot import name 'AppConfig'`

**Solução**:
```python
# Em cada apps.py, usar:
from django.apps import AppConfig

class AuthenticationConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'authentication'
```

### Conflito de UUID em Migrações
**Problema**: Erro de UUID duplicado durante migrações

**Solução**:
1. Remover migrações conflitantes
2. Recriar migrações:
```bash
python manage.py makemigrations --empty app_name
python manage.py makemigrations
python manage.py migrate
```

### Arquivo __init__.py Ausente
**Problema**: `ModuleNotFoundError` para apps Django

**Solução**:
```bash
# Criar arquivos __init__.py em todos os diretórios de apps
type nul > authentication\__init__.py
type nul > residents\__init__.py
type nul > visitors\__init__.py
type nul > employees\__init__.py
type nul > access_control\__init__.py
type nul > audit\__init__.py
```

### Erro de Normalização de Telefone
**Problema**: Método `normalize_phone()` não encontrado

**Solução**:
```python
# No modelo User (authentication/models.py)
def normalize_phone(self, phone):
    if not phone:
        return ''
    # Remove caracteres não numéricos
    return ''.join(filter(str.isdigit, phone))
```

### Sessão Expirada - Método is_expired()
**Problema**: `AttributeError` no método `is_expired()`

**Solução**:
```python
# No modelo UserSession (authentication/models.py)
from django.utils import timezone
from datetime import timedelta

def is_expired(self):
    if not self.expires_at:
        return True
    return timezone.now() > self.expires_at
```

## 🗂️ Histórico de Correções Implementadas

### Infraestrutura Base
- ✅ Correção de importação AppConfig
- ✅ Resolução de conflito UUID
- ✅ Criação de arquivos `__init__.py`
- ✅ Configuração de `INSTALLED_APPS`
- ✅ Aplicação bem-sucedida das migrações
- ✅ Criação do superusuário

### Modelos de Dados
- ✅ Correção de normalização de telefone no modelo User
- ✅ Correção do método `is_expired()` no modelo UserSession
- ✅ Validação de integridade dos modelos

### Configurações
- ✅ Configuração do banco SQLite
- ✅ Configuração de arquivos estáticos
- ✅ Configuração de templates
- ✅ Configuração de timezone

## 🚨 Problemas Pendentes

### Interface Frontend
- [ ] Templates HTML básicos não implementados
- [ ] Sistema de autenticação frontend pendente
- [ ] Formulários de cadastro não criados

### APIs REST
- [ ] Django REST Framework não configurado
- [ ] Serializers não implementados
- [ ] Endpoints de API não definidos

### Sistema de Notificações
- [ ] Celery não configurado
- [ ] Redis não implementado
- [ ] Templates de email não criados

## 🔍 Comandos de Diagnóstico

```bash
# Verificar status das migrações
python manage.py showmigrations

# Verificar configurações Django
python manage.py check

# Verificar modelos
python manage.py validate

# Acessar shell para debug
python manage.py shell

# Verificar dependências
pip list

# Verificar versão Python
python --version
```

## 📋 Estrutura Criada

### Dependências (requirements.txt)
- Django==4.2.7
- psycopg2-binary==2.9.7
- django-oauth-toolkit==1.7.1
- django-environ==0.11.2
- gunicorn==21.2.0
- celery==5.3.4
- redis==5.0.1

### Arquivos de Configuração
- `manage.py` - Gerenciador Django
- `portaria/settings.py` - Configurações principais
- `portaria/urls.py` - Roteamento principal
- `.env` - Variáveis de ambiente

### Apps Implementados
1. **authentication** - Sistema de usuários
2. **residents** - Gestão de moradores
3. **visitors** - Controle de visitantes
4. **employees** - Gestão de funcionários
5. **access_control** - Registros de acesso
6. **audit** - Logs e auditoria