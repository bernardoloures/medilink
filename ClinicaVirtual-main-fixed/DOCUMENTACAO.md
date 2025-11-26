# Documentação Técnica - ClinicaVirtual

## 📋 Visão Geral do Projeto

**MediLink** é um aplicativo móvel desenvolvido em React Native com Expo para gestão de clínicas médicas. O sistema permite o gerenciamento de exames médicos, pacientes, médicos, consultas e planos de assinatura.

## 🏗️ Arquitetura Técnica

### Tecnologias Principais
- **Framework**: React Native 0.81.5
- **Plataforma**: Expo ~54.0.20
- **Navegação**: Expo Router (file-based routing)
- **UI Components**: React Native Paper
- **Estado**: React Hooks (useState, useEffect)

### Estrutura de Diretórios
```
ClinicaVirtual-main-fixed/
├── app/                          # Código principal da aplicação
│   ├── _layout.js               # Configuração de navegação principal
│   ├── index.js                 # Página inicial (Home)
│   ├── exams.js                 # Página de exames
│   ├── planos.js                # Página de planos
│   ├── legacy_App.js            # Código legado (não utilizado)
│   ├── components/              # Componentes reutilizáveis
│   │   ├── Api.js              # Camada de API/mock
│   │   ├── Button.js           # Componente de botão customizado
│   │   └── Card.js             # Componente de cartão para exames
│   ├── entities/               # Modelos de dados
│   │   ├── Consulta.js
│   │   ├── Exame.js
│   │   ├── Medico.js
│   │   ├── Paciente.js
│   │   └── Usuario.js
│   ├── services/               # Lógica de negócio
│   │   ├── ConsultaService.js
│   │   ├── ExameService.js
│   │   ├── MedicoService.js
│   │   ├── PacienteService.js
│   │   └── UsuarioService.js
│   └── view/                   # Componentes de interface
│       ├── ExamsView.js
│       ├── HeaderView.js
│       ├── HomeView.js
│       ├── LogoView.js
│       └── PlanosView.js
├── assets/                     # Recursos estáticos
│   └── images/
├── app.json                    # Configurações do Expo
├── package.json               # Dependências do projeto
└── babel.config.js           # Configuração do Babel
```

## 🎯 Regras de Negócio

### 1. Gestão de Exames
**Entidade Principal**: Exame
- **Campos obrigatórios**:
  - Descrição (string, não vazia)
  - Data do exame (formato YYYY-MM-DD ou DD/MM/YYYY)
  - Preço (número decimal positivo)
  - Paciente associado

**Regras de Validação**:
- Descrição não pode estar vazia
- Data deve estar em formato válido
- Preço deve ser numérico e positivo
- Paciente deve ter nome, RG válido e email válido

**Funcionalidades**:
- CRUD completo (Create, Read, Update, Delete)
- Listagem ordenada alfabeticamente por descrição
- Modal para criação/edição com validações em tempo real

### 2. Gestão de Pacientes
**Entidade**: Paciente
- **Campos**: nome, RG (inteiro), email
- **Validações**:
  - Nome obrigatório
  - RG deve ser número inteiro válido
  - Email deve ter formato válido (regex: /\S+@\S+\.\S+/)

### 3. Gestão de Médicos
**Entidade**: Medico
- **Campos**: id, nome, especialidade, CRM, telefone
- **Funcionalidades**: CRUD básico

### 4. Gestão de Consultas
**Entidade**: Consulta
- **Campos**: id, pacienteId, medicoId, data, horario, descricao
- **Relacionamentos**: Vincula paciente e médico

### 5. Sistema de Usuários
**Entidade**: Usuario
- **Campos**: id, nome, email, senha, tipo
- **Tipos**: 'paciente', 'medico', 'admin'
- **Funcionalidades**:
  - Login com email/senha
  - Cadastro de novos usuários

### 6. Planos de Assinatura
**Funcionalidade**: Exibição de planos disponíveis
- **Planos**:
  - Básico: R$ 99,00/mês - Recursos essenciais
  - Intermediário: R$ 199,00/mês - Controle e desempenho
  - Avançado: R$ 299,00/mês - Todos os recursos

## 🔧 Arquitetura de Software

### Padrões Utilizados

#### 1. **MVC Adaptado**
- **Models**: Entidades (entities/) - Representam dados e regras de negócio
- **Views**: Componentes de interface (view/) - Apresentação
- **Controllers**: Serviços (services/) - Lógica de negócio

#### 2. **Service Layer Pattern**
- Cada entidade possui seu próprio serviço
- Responsável por operações CRUD
- Centraliza lógica de negócio

#### 3. **Repository Pattern (Simulado)**
- API mockada em `Api.js` simula acesso a dados
- Abstrai operações de persistência
- Permite fácil migração para backend real

### Camada de Dados

#### API Mock (`Api.js`)
- **Funcionalidades**:
  - Simula operações REST (GET, POST, PUT, DELETE)
  - Gerenciamento de dados em memória
  - Compatibilidade com código legado
- **Recursos suportados**:
  - `/exames` - Gestão de exames
  - `/pacientes` - Gestão de pacientes
  - `/medicos` - Gestão de médicos
  - `/consultas` - Gestão de consultas
  - `/usuarios` - Gestão de usuários

#### Armazenamento
- **Persistência**: Dados armazenados em arrays em memória
- **ID Generation**:
  - Exames: Contador incremental (`exameIdCounter`)
  - Outros: Timestamp (`Date.now()`) ou contador baseado em array

### Componentes Reutilizáveis

#### 1. **Button** (`components/Button.js`)
- **Props**: title, color, onPress
- **Estilo**: Botão arredondado com texto em maiúsculo
- **Cor padrão**: #24CBAF (azul esverdeado)

#### 2. **Card** (`components/Card.js`)
- **Props**: dados do exame + callbacks (onDelete, onEdit)
- **Estrutura**:
  - Título: Descrição do exame
  - Subtítulo: Nome do paciente
  - Conteúdo: Data e preço
  - Ações: Botões Editar/Excluir

## 🖥️ Interface do Usuário

### Navegação
- **File-based routing** com Expo Router
- **Telas principais**:
  - `/` (index.js) → HomeView
  - `/exams` (exams.js) → ExamsView
  - `/planos` (planos.js) → PlanosView

### Layout
- **Header**: Logo da aplicação com fundo azul (#A7C7E7)
- **Background**: Azul claro (#E2EFF9)
- **Tema**: Azul institucional (#1F3B73)

### Validações de Formulário
- **Tempo real**: Feedback imediato nos campos
- **Mensagens específicas**: Erros contextuais
- **Formatação**: Conversão automática de datas (DD/MM/YYYY → YYYY-MM-DD)

## 🚀 Guia de Desenvolvimento

### Pré-requisitos
```bash
- Node.js
- npm ou yarn
- Expo CLI
```

### Instalação e Execução
```bash
# Clonar o repositório
git clone <repository-url>
cd ClinicaVirtual-main-fixed

# Instalar dependências
npm install

# Executar em desenvolvimento
npm start
# ou
npx expo start
```

### Estrutura de Desenvolvimento

#### Adicionando Nova Entidade
1. Criar classe em `entities/`
2. Implementar serviço em `services/`
3. Adicionar endpoints na API (`Api.js`)
4. Criar view em `view/`
5. Configurar rota em `_layout.js`

#### Exemplo: Nova Entidade "Medicamento"
```javascript
// entities/Medicamento.js
export default class Medicamento {
  constructor(id, nome, dosagem, indicacao) {
    this.id = id;
    this.nome = nome;
    this.dosagem = dosagem;
    this.indicacao = indicacao;
  }
}
```

```javascript
// services/MedicamentoService.js
import Medicamento from '../entities/Medicamento.js';

class MedicamentoService {
  constructor() {
    this.medicamentos = [];
  }

  listar() {
    return this.medicamentos;
  }

  criar(nome, dosagem, indicacao) {
    const id = this.medicamentos.length + 1;
    const medicamento = new Medicamento(id, nome, dosagem, indicacao);
    this.medicamentos.push(medicamento);
    return medicamento;
  }
}

export default new MedicamentoService();
```

### Convenções de Código

#### Nomenclatura
- **Arquivos**: PascalCase para componentes, camelCase para utilitários
- **Variáveis**: camelCase
- **Constantes**: UPPER_SNAKE_CASE
- **Classes**: PascalCase

#### Estilo
- **Indentação**: 2 espaços
- **Aspas**: Single quotes para JSX, double quotes para objetos
- **Semicolons**: Utilizados obrigatoriamente

#### Imports
- Imports do React primeiro
- Imports de bibliotecas externas
- Imports locais (relativos)
- Imports de assets por último

### Testes
**Status**: Não implementados
**Recomendação**: Implementar testes unitários para:
- Validações de entidades
- Lógica de serviços
- Componentes críticos

### Boas Práticas Recomendadas

#### 1. **Tratamento de Erros**
```javascript
try {
  // operação
} catch (error) {
  alert('Erro: ' + error.message);
}
```

#### 2. **Validações**
- Sempre validar entrada do usuário
- Fornecer mensagens de erro claras
- Validar no frontend E backend

#### 3. **Estado**
- Usar hooks apropriados (useState, useEffect)
- Evitar estado desnecessário
- Manter estado consistente

## 🔄 Melhorias Futuras

### Funcionalidades
1. **Autenticação**: Implementar login/logout completo
2. **Backend Real**: Migrar de mock para API REST
3. **Banco de Dados**: Persistência real dos dados
4. **Notificações**: Push notifications para lembretes
5. **Offline**: Funcionamento offline com sincronização

### Arquiteturais
1. **State Management**: Redux ou Context API para estado global
2. **TypeScript**: Migração para tipagem estática
3. **Testes**: Suite completa de testes
4. **CI/CD**: Pipeline de deploy automatizado

### UI/UX
1. **Design System**: Sistema de design consistente
2. **Acessibilidade**: Suporte completo a leitores de tela
3. **Tema Dark**: Modo escuro
4. **Responsividade**: Adaptação a diferentes tamanhos de tela

## 📝 Manutenção

### Versionamento
- **Git Flow**: Branches feature/, develop, main
- **Commits**: Mensagens descritivas em português
- **Tags**: Versionamento semântico (v1.0.0)

### Documentação
- Manter este documento atualizado
- Documentar mudanças significativas
- README atualizado com instruções de instalação

---

**Última atualização**: 26 de novembro de 2025
**Versão do projeto**: 1.0.0
**Desenvolvedor responsável**: [Nome do desenvolvedor]
