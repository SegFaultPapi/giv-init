# 🎁 GIV INIT - Plataforma de Donaciones Crypto con Yield Sostenible

GIV INIT es una plataforma descentralizada que facilita donaciones crypto a comunidades builder web3 con yield recurrente y UX ultra simple. Permite donar cualquier ERC-20, automatiza el routing de fondos (95% a la comunidad, 5% a un vault Morpho que genera yield sostenible) y proporciona transparencia total con reporting automático.

## 📋 Descripción del Proyecto

**Problema:** Las comunidades builder web3 en México carecen de financiamiento sostenible recurrente. Los donantes enfrentan plataformas fragmentadas, UX frustrante, altos fees y falta de trazabilidad del impacto.

**Solución:** Plataforma que permite donaciones crypto en menos de 30 segundos con:
- Donación en cualquier ERC-20 (USDC, DAI, ETH, etc.)
- Swap automático a WETH vía Uniswap V4
- Fee del 5% que se deposita automáticamente en un vault Morpho para generar yield sostenible
- Dashboard transparente con historial de donaciones y yield generado
- Deploy en Base Sepolia (testnet)

## 🏗️ Stack Tecnológico

Este proyecto está construido con **Scaffold-ETH 2** y utiliza:

- **Smart Contracts:** Foundry, Solidity, Uniswap V4 Hooks, Morpho Blue, ERC-4626
- **Frontend:** Next.js 14 (App Router), TypeScript, shadcn/ui, Tailwind CSS
- **Blockchain:** Wagmi, Viem, RainbowKit
- **Network:** Base Sepolia (testnet)

## 📁 Estructura del Proyecto

```
giv-init/
├── packages/
│   ├── foundry/          # Smart contracts y scripts de deployment
│   │   ├── contracts/    # Contratos Solidity
│   │   ├── script/       # Scripts de deployment
│   │   ├── test/         # Tests de contratos
│   │   └── foundry.toml  # Configuración de Foundry
│   │
│   └── nextjs/           # Frontend Next.js
│       ├── app/          # Páginas y layouts (App Router)
│       ├── components/   # Componentes React
│       ├── hooks/        # Custom hooks para contratos
│       ├── contracts/    # Tipos y ABIs generados
│       └── scaffold.config.ts  # Configuración de redes
│
└── documents/            # Documentación del proyecto
    ├── tickets/          # Tickets de desarrollo
    └── giv-init-mvp-prd.md  # PRD completo
```

## 🚀 Quickstart

### Requisitos Previos

Antes de comenzar, necesitas instalar:

- [Node.js](https://nodejs.org/) (>= v20.18.3)
- [Yarn](https://yarnpkg.com/) (v1 o v2+)
- [Git](https://git-scm.com/downloads)
- [Foundry](https://book.getfoundry.sh/getting-started/installation) (para compilar contratos)

### Instalación

1. Clona el repositorio e instala las dependencias:

```bash
yarn install
```

2. Inicia una red local en la primera terminal:

```bash
yarn chain
```

Esto inicia una blockchain local usando Foundry Anvil en `http://127.0.0.1:8545`.

3. En una segunda terminal, despliega el contrato de prueba:

```bash
yarn deploy
```

Esto despliega el contrato de prueba a la red local. Los contratos se encuentran en `packages/foundry/contracts` y los scripts de deployment en `packages/foundry/script`.

4. En una tercera terminal, inicia la aplicación Next.js:

```bash
yarn start
```

Visita la aplicación en: `http://localhost:3000`

Puedes interactuar con tus contratos usando la página `Debug Contracts`.

## 🔧 Comandos Disponibles

### Desarrollo

- `yarn start` - Inicia el frontend Next.js en modo desarrollo
- `yarn chain` - Inicia la blockchain local (Foundry Anvil)
- `yarn deploy` - Despliega contratos a la red local
- `yarn compile` - Compila los contratos Solidity
- `yarn test` - Ejecuta los tests de los contratos

### Testing y Verificación

- `yarn foundry:test` - Ejecuta tests de Foundry
- `yarn foundry:verify` - Verifica contratos en Etherscan

### Formato y Linting

- `yarn format` - Formatea código (Prettier)
- `yarn lint` - Ejecuta linters

## 🌐 Redes Configuradas

El proyecto está configurado para trabajar con múltiples redes. Las principales son:

### Red Local (Desarrollo)
- **Foundry Anvil:** `http://127.0.0.1:8545`
- Chain ID: 31337

### Testnets
- **Base Sepolia:** `https://sepolia.base.org` (Chain ID: 84532)
- **Sepolia:** `https://eth-sepolia.g.alchemy.com/v2/${ALCHEMY_API_KEY}` (Chain ID: 11155111)

### Mainnets
- **Base:** `https://mainnet.base.org` (Chain ID: 8453)
- **Ethereum:** `https://eth-mainnet.alchemyapi.io/v2/${ALCHEMY_API_KEY}` (Chain ID: 1)

> **Nota:** Base Sepolia está disponible en la configuración de Foundry (`packages/foundry/foundry.toml`) y puede ser seleccionada para deployment de testnet.

## 🔐 Configuración de Variables de Entorno

Para desarrollar y desplegar contratos, necesitas configurar variables de entorno. El proyecto incluye archivos `.env.example` como plantillas.

### Configuración para Foundry (Smart Contracts)

1. Copia el archivo de ejemplo:
```bash
cd packages/foundry
cp .env.example .env
```

2. Edita `.env` con tus valores:

**Variables Requeridas para Base Sepolia:**

- `DEPLOYER_PRIVATE_KEY`: Tu clave privada (sin `0x`) para deployar contratos
  - Obtén una cuenta usando: `yarn account:generate`
  - **NUNCA** compartas o commitees esta clave

- `ALCHEMY_API_KEY`: API key de Alchemy para RPC endpoints
  - Obtén una gratuita en: https://dashboard.alchemyapi.io

- `ETHERSCAN_API_KEY`: API key para verificar contratos en Basescan
  - Obtén una en: https://basescan.org/apis (o usa Etherscan)

**Variables Opcionales:**

- `INFURA_API_KEY`: Alternativa a Alchemy
- `BASESCAN_API_KEY`: Si prefieres usar una key específica para Basescan
- `LOCALHOST_KEYSTORE_ACCOUNT`: Cuenta para desarrollo local (default: `scaffold-eth-default`)

### Configuración para Next.js (Frontend)

1. Copia el archivo de ejemplo:
```bash
cd packages/nextjs
cp .env.example .env.local
```

2. Edita `.env.local` con tus valores:

**Variables Requeridas:**

- `NEXT_PUBLIC_ALCHEMY_API_KEY`: API key de Alchemy para el frontend
- `NEXT_PUBLIC_WALLET_CONNECT_PROJECT_ID`: Project ID de WalletConnect para RainbowKit
  - Obtén uno gratuito en: https://cloud.walletconnect.com

**Nota:** Las variables con prefijo `NEXT_PUBLIC_` son expuestas al navegador. No incluyas secretos ahí.

### Deployment en Base Sepolia

Para desplegar contratos en Base Sepolia:

```bash
cd packages/foundry
yarn deploy --network baseSepolia
```

Asegúrate de tener:
- `DEPLOYER_PRIVATE_KEY` configurada en `.env`
- Suficiente ETH en Base Sepolia en tu wallet (obtén ETH de test en: https://www.coinbase.com/faucets/base-ethereum-goerli-faucet)

### Seguridad

⚠️ **IMPORTANTE:**
- **NUNCA** commitees archivos `.env` o `.env.local` con valores reales
- Los archivos `.env` están protegidos por `.gitignore`
- Siempre usa `.env.example` como referencia para documentar variables necesarias
- Para producción, almacena variables de entorno en Vercel/System config

## 📝 Desarrollo de Contratos

### Estructura de Contratos

Los contratos se encuentran en `packages/foundry/contracts/`. Para desarrollar nuevos contratos:

1. Crea tu contrato en `packages/foundry/contracts/`
2. Compila con `yarn compile`
3. Escribe tests en `packages/foundry/test/`
4. Ejecuta tests con `yarn test`
5. Crea un script de deployment en `packages/foundry/script/`

### Interacción desde el Frontend

Scaffold-ETH 2 proporciona hooks personalizados para interactuar con contratos:

#### Leer datos de un contrato:
```typescript
const { data: someData } = useScaffoldReadContract({
  contractName: "YourContract",
  functionName: "functionName",
  args: [arg1, arg2], // opcional
});
```

#### Escribir datos a un contrato:
```typescript
const { writeContractAsync } = useScaffoldWriteContract({
  contractName: "YourContract"
});

await writeContractAsync({
  functionName: "functionName",
  args: [arg1, arg2], // opcional
  value: parseEther("0.1"), // opcional, para funciones payable
});
```

## 🧪 Testing

Los tests están escritos con Foundry. Para ejecutar:

```bash
yarn test
```

Los tests se encuentran en `packages/foundry/test/`. Todos los tests deben pasar antes de hacer commit.

## 📚 Documentación

- [Documentación de Scaffold-ETH 2](https://docs.scaffoldeth.io)
- [Documentación de Foundry](https://book.getfoundry.sh/)
- [Documentación de Next.js](https://nextjs.org/docs)
- [PRD del Proyecto](./documents/giv-init-mvp-prd.md)

## 🎯 Roadmap

### ✅ Completado
- [x] Setup inicial Scaffold-ETH 2 con Foundry
- [x] Configuración de Base Sepolia
- [x] Tests base funcionando

### 🚧 En Progreso
- [ ] Configuración de Base Sepolia para deployment
- [ ] Implementación de hook Uniswap V4
- [ ] Implementación de vault ERC-4626

### 📋 Pendiente
- [ ] Frontend: Selector de comunidades
- [ ] Frontend: Multi-token input
- [ ] Frontend: Dashboard de donaciones
- [ ] Integración con Morpho Blue

Ver más detalles en [tickets](./documents/tickets/).

## 🤝 Contribuir

Por favor, lee [CONTRIBUTING.md](./CONTRIBUTING.md) para más detalles sobre nuestro código de conducta y el proceso para enviar pull requests.

## 📄 Licencia

Este proyecto está bajo la Licencia especificada en [LICENCE](./LICENCE).

---

**Construido con ❤️ usando Scaffold-ETH 2**
