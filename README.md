# Toogether — Gestão Compartilhada de Metas e Listas

**React Native · Expo 54 · TypeScript · iOS & Android**

Aplicativo mobile para gestão pessoal colaborativa: compartilhe metas, listas de compras e organize sua rotina junto com quem importa.

---

## Stack

| Camada | Tecnologia |
|---|---|
| Framework | React Native 0.81 + Expo 54 |
| Linguagem | TypeScript 5.9 (strict) |
| Navegação | Expo Router 6 (file-based) |
| Estado global | Zustand 5 + MMKV (persistência) |
| Server state | TanStack React Query 5 |
| HTTP | Axios com interceptors |
| Formulários | React Hook Form + Zod |
| Autenticação | Google Sign-In · Apple Auth · E-mail/Senha |
| Animações | React Native Reanimated 4 + Skia |
| UI | Sistema de design próprio (tema dark) |
| Build | EAS Build (Expo Application Services) |

---

## Funcionalidades

- **Autenticação completa** — login social (Google/Apple) e e-mail/senha com validação por Zod
- **Navegação file-based** — rotas tipadas com Expo Router (grupos `(auth)` e `(tabs)`)
- **Sistema de metas** — CRUD de goals com integração à API
- **Câmera e mídia** — captura de vídeo/foto com Vision Camera e compressão automática
- **QR Code** — geração nativa de QR codes
- **Geolocalização** — integração com Expo Location
- **Notificações** — serviço estruturado de push notifications
- **Gráficos** — visualização de dados com Victory Native + Skia
- **Carrossel** — Reanimated Carousel com animações fluidas
- **Tema dark** — interface 100% dark com sistema de design consistente

---

## Arquitetura

\```
src/
├── app/                  # Rotas (Expo Router file-based)
│   ├── (auth)/           # Login, cadastro, recuperação de senha
│   ├── (tabs)/           # Home, Perfil (bottom tabs)
│   └── goals/            # Feature de metas
│
├── components/
│   └── ui/               # Design system: Button, Card, Input, Text, View, Flex, Layout
│
├── services/             # Chamadas HTTP por domínio (auth, goals, notifications)
├── queries/              # React Query hooks (server state)
├── stores/               # Zustand stores (client state + MMKV)
├── contexts/             # React Contexts (auth provider)
├── lib/                  # Instância Axios com interceptors
├── hooks/                # Hooks reutilizáveis (useAuth, useDebounce, fonts)
├── models/               # Lógica de página (separada da UI)
├── theme/                # Tokens de design (cores, tipografia, espaçamentos)
├── types/                # Tipagens globais
└── helper/               # Utilitários
\```

**Padrões aplicados:**
- Separação entre UI, lógica de negócio e acesso a dados
- Componentes de UI composicionais e reutilizáveis
- Formulários controlados com validação em runtime via Zod
- Interceptors Axios para refresh de token e tratamento global de erros
- Rotas protegidas por guard no layout raiz

---

## Como rodar

### Pré-requisitos

- Node.js 20+
- Yarn
- Expo CLI (`npm install -g expo-cli`)
- Para iOS: Xcode 15+
- Para Android: Android Studio + emulador configurado

### Instalação

\```bash
git clone https://github.com/jeanmarcos552/jean-app-front.git
cd jean-app-front
yarn install
\```

### Variáveis de ambiente

\```bash
cp .env.example .env
\```

Preencha as variáveis:

\```env
EXPO_PUBLIC_API_URL=             # URL da API backend
EXPO_PUBLIC_GOOGLE_WEB_CLIENT_ID=
EXPO_PUBLIC_GOOGLE_IOS_CLIENT_ID=
EXPO_PUBLIC_GOOGLE_SCOPES=https://www.googleapis.com/auth/userinfo.email,...
\```

### Executar

\```bash
# Expo Go (desenvolvimento rápido)
yarn start

# iOS (simulador)
yarn ios

# Android (emulador)
yarn android
\```

---

## Build de produção

Utiliza **EAS Build** para geração dos binários `.ipa` e `.apk/.aab`:

\```bash
eas build --platform android
eas build --platform ios
\```

---

## Estrutura de autenticação

\```
Usuário abre o app
  └── _layout.tsx verifica token no MMKV
        ├── Token válido → redireciona para (tabs)
        └── Sem token   → redireciona para (auth)/signin
\```

O Axios possui interceptor que renova o token automaticamente em requisições com erro 401.

---

## Configurações do projeto

| Item | Valor |
|---|---|
| Bundle ID (iOS) | `com.jeanapp.front` |
| Package (Android) | `com.jeanapp.front` |
| Orientação | Portrait |
| Tema | Dark |
| New Architecture | Habilitada |
| React Compiler | Habilitado (experimental) |
| iOS mínimo | 15.5 |

---

## Autor

**Jean Marcos**  
[jeansilva.app.br](https://jeansilva.app.br) · [GitHub](https://github.com/jeanmarcos552)
