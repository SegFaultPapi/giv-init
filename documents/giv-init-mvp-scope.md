# 🎯 MVP Scope Final: Giv Init - Octant Hackathon Edition

## Problema Core
Las comunidades de builders web3 en México carecen de financiamiento sostenible recurrente, y los donantes altruistas necesitan un mecanismo para apoyar bienes públicos mientras generan impacto.

---

## 🏗️ Stack Confirmado

### Smart Contracts
- **Scaffold-ETH 2** con Foundry
- **Uniswap V4 hooks** personalizados (5% fee)
- **Morpho Blue** vault para yield generation
- **ERC-4626** estándar para vault
- Deploy en **Base Sepolia** testnet

### Frontend
- Next.js 14 (incluido en Scaffold-ETH 2)
- wagmi + viem para Web3
- RainbowKit para wallet connection
- shadcn/ui + Tailwind

### Compatibilidad Validada
✅ Scaffold-ETH 2 + Base = Native support
✅ Uniswap V4 hooks + Scaffold-ETH 2 = Implementado
✅ Morpho Blue + ERC-4626 = Diseñado para esto
✅ Morpho + Bundler SDK = Integración simplificada

---

## 🔥 Flujo MVP - Hackathon (5 pasos críticos)

1. **Usuario conecta wallet** y ve lista de 3-5 comunidades builder en México (hardcodeadas)
2. **Usuario dona en cualquier ERC-20** (USDC, DAI, ETH) → monto mínimo sugerido
3. **Hook Uniswap V4 ejecuta:**
   - Swap automático a WETH
   - Cobra 5% fee
   - Envía 95% directo a comunidad
4. **5% fee → Morpho Vault ERC-4626** que genera yield automáticamente
5. **Dashboard muestra:** Total donado + yield acumulado en vault (distribución manual para demo)

---

## ✅ Features MVP - Optimizado para Hackathon

### Smart Contracts (Prioridad 1 - Semana 1-2)

#### Hook Uniswap V4 personalizado
- `afterSwap` hook que cobra 5% fee
- Integración con PoolManager de Uniswap V4
- Distribución automática 95% → comunidad wallet

#### Morpho Vault ERC-4626
- Vault básica compatible con Morpho Blue
- Auto-deposit del 5% fee a Morpho para lending
- Una estrategia simple: WETH lending en Morpho Blue
- View functions para mostrar yield acumulado

#### Contrato Registry
- Whitelist de comunidades (address + metadata)
- Función para agregar comunidades (onlyOwner)

### Frontend (Prioridad 2 - Semana 3)

#### Componentes críticos
- Selector visual de comunidades (cards con logo, nombre, descripción)
- Input multi-token con swap preview
- Confirmación de transacción con breakdown (95% comunidad, 5% vault)
- Dashboard donante: historial + total donado
- Vault stats: TVL + yield APY (usando Morpho API)

#### NO incluir en MVP
- Vista para comunidades (solo wallets reciben)
- Yield distribution automática (manual trigger para demo)
- Múltiples estrategias de yield
- Notificaciones
- Sistema de rewards/NFTs

---

## ❌ NO va en MVP

- Yield distribution automática entre comunidades (acumula en v1, distribuye manualmente en demo)
- Registro público de comunidades (whitelist hardcodeada)
- Múltiples estrategias DeFi en Morpho
- Governance o voting
- Mobile app
- Integración con otros DEXs además de Uniswap V4
- Analytics complejas
- Sistema de métricas de impacto

---

## 🎊 Criterios de Éxito - Alineado con Octant

### Octant busca
1. Best use of Yield Donating Strategy ($4,000)
2. Best public goods projects ($3,000)
3. Innovation en ERC-4626 vaults

### Tu MVP funciona si
1. ✅ Hook de Uniswap V4 cobra correctamente el 5% fee en cada swap
2. ✅ Vault Morpho ERC-4626 acumula fees y genera yield verificable
3. ✅ 3+ comunidades piloto reciben donaciones directamente (95%)
4. ✅ Demo muestra yield acumulado distribuible a todas las comunidades
5. ✅ 10+ transacciones exitosas en Base Sepolia durante el demo

---

## 📅 Timeline Hackathon - 10 días (Nov 3-9)

### **Día 1-2 (Nov 3-4): Setup + Hook básico**

```bash
npx create-eth@latest
# Seleccionar Foundry
cd giv-init
yarn install
```

- Configurar Base Sepolia en `scaffold.config.ts`
- Implementar hook básico de Uniswap V4 con 5% fee
- Tests unitarios del hook

### **Día 3-4 (Nov 4-5): Morpho Vault**

- Implementar vault ERC-4626 básica
- Integración con Morpho Blue (una estrategia WETH lending)
- Conectar hook → vault (auto-deposit del 5%)
- Tests de integración

### **Día 5-6 (Nov 6-7): Frontend Core**

- Selector de comunidades (3-5 hardcodeadas México)
- Flow de donación con preview
- Wallet connection + transaction handling
- Integración con contratos usando Scaffold-ETH hooks

### **Día 7-8 (Nov 7-8): Dashboard + Morpho Integration**

- Dashboard donante: historial
- Vault stats usando Morpho SDK
- Manual trigger para yield distribution (para demo)
- Responsive design básico

### **Día 9 (Nov 8): Testing + Deploy**

- Deploy a Base Sepolia
- Testing end-to-end en testnet
- Verificar contratos
- Bug fixes críticos

### **Día 10 (Nov 9): Demo + Submission**

- Video demo (mostrar todo el flow)
- Documentación técnica
- Highlight: yield generation + public goods
- Submit a Devfolio

---

## 🏆 Estrategia para Ganar Octant

### **Prize Target: Best Yield Donating Strategy ($4,000)**

#### Por qué encajas
1. ✅ Usas ERC-4626 vault (requerimiento explícito)
2. ✅ Integras Morpho Blue para yield real
3. ✅ Innovación: Uniswap V4 hooks + donation flow único
4. ✅ Public goods focus (comunidades builder)
5. ✅ Yield sostenible para todas las comunidades registradas

#### Judging Criteria - Hackathons típicos
- **Innovation/Uniqueness:** Hook personalizado + yield donation es único ✅
- **Technical Implementation:** V4 hooks + Morpho + ERC-4626 = avanzado ✅
- **Impact:** Funding sostenible para public goods (builders) ✅
- **Execution:** MVP funcional que demuestra concepto completo ✅

### **Bonus Target: Best Public Goods Project ($3,000)**

#### Ángulo adicional
- Tu proyecto financia public goods (comunidades builder educativas)
- Modelo sostenible vs grants one-time
- Alineado con misión de Octant

---

## 🚨 Red Flags a Evitar

❌ **NO intentes implementar yield distribution automática on-chain** - Demasiado complejo para 10 días. Hazlo manual con botón en UI.

❌ **NO agregues múltiples estrategias Morpho** - Una estrategia (WETH lending) es suficiente para ganar.

❌ **NO gastes tiempo en UI perfecta** - Funcional > Bonito. Scaffold-ETH 2 ya tiene componentes decentes.

❌ **NO deployes a mainnet** - Base Sepolia es suficiente. Mainnet implica auditorías.

❌ **NO trates de registrar comunidades on-chain** - Hardcodea 3-5 en el smart contract, listo.

---

## 💡 Diferenciadores Clave vs Competencia

1. **Uniswap V4 hooks** - Pocos equipos dominan esto (recién Q1 2025)
2. **Morpho Blue integration** - Yield real, no simulado
3. **Public goods angle** - Alineado con Octant mission
4. **Mexico focus** - Local impact, específico
5. **Scaffold-ETH 2 + Base** - Stack moderno, deployment rápido

---

## 📋 Checklist Final Pre-Submission

### **Técnico**
- [ ] Hook Uniswap V4 funciona en Base Sepolia
- [ ] Vault ERC-4626 genera yield real en Morpho
- [ ] Frontend permite donar y ver stats
- [ ] 10+ transacciones test exitosas
- [ ] Contratos verificados en Base explorer

### **Demo**
- [ ] Video 3-5 min mostrando flow completo
- [ ] Explicar problema → solución → arquitectura
- [ ] Mostrar yield acumulado en vault
- [ ] Highlight: public goods + sostenibilidad

### **Docs**
- [ ] README con arquitectura técnica
- [ ] Explicar por qué Uniswap V4 + Morpho
- [ ] Impact statement: cómo ayuda a comunidades
- [ ] Deploy addresses + verified contracts

---

## 🎯 Próximos Pasos Inmediatos

### **HOY (Nov 3)**

```bash
# 1. Setup Scaffold-ETH 2
npx create-eth@latest
# Seleccionar: Foundry + Base

# 2. Instalar dependencias Uniswap V4
cd packages/foundry
forge install Uniswap/v4-core
forge install Uniswap/v4-periphery

# 3. Instalar Morpho SDK (frontend)
cd packages/nextjs
yarn add @morpho-org/blue-sdk @morpho-org/morpho-ts
```

### **MAÑANA (Nov 4)**

- Implementa el hook básico con 5% fee
- Setup Base Sepolia en configs
- Primer test del hook

### **Enfoque Prioritario**

Smart contracts primero (día 1-4), frontend después (día 5-8). El hook + Morpho vault son tu diferenciador técnico core.

---

## 📊 Resumen Ejecutivo

| Aspecto | Detalle |
|---------|---------|
| **Problema** | Financiamiento sostenible para comunidades builder web3 |
| **Solución** | Plataforma de donación con yield automático (Uniswap V4 + Morpho) |
| **Target Users** | Donantes altruistas + comunidades builder (México) |
| **Stack** | Scaffold-ETH 2 + Foundry + V4 Hooks + Morpho + Base |
| **Timeline** | 10 días (Nov 3-9) |
| **Prize Target** | Best Yield Donating Strategy ($4,000) |
| **MVP Success** | 10+ donaciones en testnet, yield verificable en Morpho |
| **Diferenciador** | V4 hooks + Public goods + Morpho integration |

---

**Total: 10 días a submission. La combinación V4 hooks + Morpho + public goods es tu ventaja competitiva. Ship it.** 🚀
