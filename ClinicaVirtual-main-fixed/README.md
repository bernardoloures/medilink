# MediLink - Sistema de Gestão para Clínicas Médicas 🏥

**MediLink** é um aplicativo móvel desenvolvido em React Native com Expo para gestão completa de clínicas médicas. Permite o gerenciamento de exames, pacientes, médicos, consultas e planos de assinatura de forma intuitiva e eficiente.

## 🎯 Sobre o Projeto

Este projeto implementa um sistema completo de gestão clínica com as seguintes funcionalidades principais:

- **📋 Gestão de Exames**: CRUD completo de exames médicos com validações
- **👥 Gestão de Pacientes**: Cadastro e controle de dados dos pacientes
- **👨‍⚕️ Gestão de Médicos**: Controle de profissionais médicos e especialidades
- **📅 Gestão de Consultas**: Agendamento e controle de consultas
- **💳 Planos de Assinatura**: Sistema de planos com diferentes níveis

### 🏗️ Arquitetura Técnica

- **Framework**: React Native 0.81.5 com Expo ~54.0.20
- **Navegação**: Expo Router (file-based routing)
- **UI Components**: React Native Paper
- **Padrão**: MVC adaptado com Service Layer
- **Estado**: Gerenciamento local com React Hooks
- **Backend**: API mockada (preparada para migração)

## Get started

1. Install dependencies

   ```bash
   npm install
   ```

2. Start the app

   ```bash
   npx expo start
   ```

In the output, you'll find options to open the app in a

- [development build](https://docs.expo.dev/develop/development-builds/introduction/)
- [Android emulator](https://docs.expo.dev/workflow/android-studio-emulator/)
- [iOS simulator](https://docs.expo.dev/workflow/ios-simulator/)
- [Expo Go](https://expo.dev/go), a limited sandbox for trying out app development with Expo

You can start developing by editing the files inside the **app** directory. This project uses [file-based routing](https://docs.expo.dev/router/introduction).

## 🚀 Funcionalidades

### 📱 Interface do Usuário
- **Tela Inicial**: Navegação intuitiva para as principais funcionalidades
- **Gestão de Exames**: Formulário completo com validações em tempo real
- **Planos Disponíveis**: Visualização de planos de assinatura
- **Design Responsivo**: Adaptado para diferentes tamanhos de tela

### 🔧 Recursos Técnicos
- **Validações Robuste**: Campos obrigatórios e formatos específicos
- **Formatação Automática**: Conversão inteligente de datas (DD/MM/YYYY ↔ YYYY-MM-DD)
- **Feedback Visual**: Mensagens de erro contextuais
- **Navegação Fluida**: Transições suaves entre telas

## 📁 Estrutura do Projeto

```
ClinicaVirtual-main-fixed/
├── app/                          # Código principal da aplicação
│   ├── _layout.js               # Configuração de navegação principal
│   ├── index.js                 # Página inicial (Home)
│   ├── exams.js                 # Página de exames
│   ├── planos.js                # Página de planos
│   ├── components/              # Componentes reutilizáveis
│   │   ├── Api.js              # Camada de API/mock
│   │   ├── Button.js           # Componente de botão customizado
│   │   └── Card.js             # Componente de cartão para exames
│   ├── entities/               # Modelos de dados
│   ├── services/               # Lógica de negócio
│   └── view/                   # Componentes de interface
├── assets/                     # Recursos estáticos
├── app.json                    # Configurações do Expo
├── package.json               # Dependências do projeto
└── DOCUMENTACAO.md            # Documentação técnica completa
```

## 🛠️ Desenvolvimento

### Padrões e Convenções
- **Entidades**: Classes ES6 para modelagem de dados
- **Serviços**: Lógica de negócio centralizada
- **Validações**: Regras de negócio implementadas nas entidades
- **API**: Camada mockada preparada para backend real

### Adicionando Novas Funcionalidades
1. Criar entidade em `entities/`
2. Implementar serviço em `services/`
3. Adicionar endpoints na API (`Api.js`)
4. Criar view em `view/`
5. Configurar rota em `_layout.js`

## 📋 Regras de Negócio

### Gestão de Exames
- **Campos obrigatórios**: Descrição, data, preço, paciente
- **Validações**: Data em formato válido, preço numérico positivo
- **Paciente**: Nome, RG (inteiro), email válido obrigatórios

### Gestão de Pacientes
- **Identificação**: RG como identificador único
- **Dados obrigatórios**: Nome, RG, email
- **Validações**: Email no formato correto, RG numérico

### Sistema de Planos
- **Básico**: R$ 99,00/mês - Recursos essenciais
- **Intermediário**: R$ 199,00/mês - Controle avançado
- **Avançado**: R$ 299,00/mês - Recursos completos

## 🚀 Próximos Passos

### Melhorias Planejadas
- **Backend Real**: Migração da API mockada para servidor
- **Autenticação**: Sistema completo de login/logout
- **Persistência**: Banco de dados para armazenamento
- **Notificações**: Push notifications para lembretes
- **Testes**: Suite completa de testes automatizados

### Recursos Adicionais
- [📖 Documentação Técnica](./DOCUMENTACAO.md) - Análise completa do projeto
- [Expo documentation](https://docs.expo.dev/) - Fundamentos e guias avançados
- [Learn Expo tutorial](https://docs.expo.dev/tutorial/introduction/) - Tutorial passo-a-passo

## 🤝 Contribuição

Contribuições são bem-vindas! Para contribuir:

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

### 📝 Convenções de Commit
- `feat:` - Nova funcionalidade
- `fix:` - Correção de bug
- `docs:` - Mudanças na documentação
- `style:` - Mudanças de formatação
- `refactor:` - Refatoração de código
- `test:` - Adição ou correção de testes

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

## 🌐 Comunidade

- [Expo on GitHub](https://github.com/expo/expo): Plataforma open source
- [Discord community](https://chat.expo.dev): Comunidade Expo
- [Repositório Original](https://github.com/bernardoloures/medilink): Projeto base
