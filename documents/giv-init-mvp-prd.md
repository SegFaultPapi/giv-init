# PRD: GIV INIT MVP – Octant Hackathon

---

## 1. Project Overview

### Problema
Las comunidades builder web3 en México carecen de financiamiento sostenible recurrente. Los donantes enfrentan plataformas fragmentadas, UX frustrante, altos fees y falta de trazabilidad del impacto.

### Objetivos
- Facilitar donaciones crypto a comunidades builder con _yield_ recurrente y UX ultra simple.
- Automatizar el routeo de fondos: 95% a la comunidad, 5% a un vault Morpho que genera yield sostenible.
- Transparencia y reporting automático – impacto visible en dashboard, sin fricción.

### Usuario Target
- Builders/donadores web3 (22-38 años, alto comfort técnico, buscan donar en menos de 30s)
- Admins de comunidades/DAOs (26-45, buscan automatización y reporting, bajo riesgo)
- Donador crypto impact-first/tax optimizer (28-55, comfort intermedio, priorizan emotional impact o tax docs)
- Enfoque MVP: Donantes y admins en 3 comunidades builder mexicanas + donadores crypto latam

---

## 2. User Stories & Acceptance Criteria

### Feature 1: Selección de comunidad y donación multimoneda
**User story:** Como donador, quiero elegir una comunidad de una lista y donar en cualquier ERC-20, para apoyar bienes públicos fácilmente.
**Criterios:**
- Seleccionar comunidad (UI de cards, datos hardcodeados)
- Input y preview para USDC, DAI, ETH
- Monto mínimo visible para donate-btn habilitado
- Conexión de wallet (RainbowKit)
- Solo continúa si wallet conectada

### Feature 2: Swap + Fee automático vía Uniswap V4 Hook
**User story:** Como donador, quiero donar cualquier ERC-20 y que el sistema convierta todo a WETH, cobre 5% fee y mande el 95% a la comunidad automáticamente.
**Criterios:**
- Hook Uniswap V4 `afterSwap` cobra 5%
- Swap automático a WETH
- Transparencia (breakdown en confirm modal)
- Simulación previa de monto recibido por comunidad

### Feature 3: Generación y acumulación de yield en Morpho Vault
**User story:** Como admin/comunidad, quiero que el 5% fee se deposite automáticamente a Morpho, generando yield distribuible después.
**Criterios:**
- Vault tipo ERC-4626 compatible Morpho Blue
- Depósito automático del 5% del fee
- Mostrar yield acumulado en el dashboard sin auto-distribuir (manual para demo)

### Feature 4: Dashboard transparente para donantes
**User story:** Como donador/admin, quiero ver el total donado, yield generado y breakdown visual en un dashboard simple.
**Criterios:**
- Dashboard básico: total donado, yield APY, historial de donaciones, stats de vault
- Visualización responsive (web-only en v1)
- Comprobantes onchain (hash link)

### Feature 5: Seguridad y performance MVP
**User story:** Como usuario, quiero donar sin miedo a hacks ni UX lenta.
**Criterios:**
- Testnet (Base Sepolia, no mainnet)
- Todos los swaps y vaults públicos/verificables
- Feedback claro en caso de error (sin loops infinitos)

---

## 3. UI/UX Requirements

### Diseño general
- Look & feel: Moderno, minimalista, enfocado en simplicidad (shadcn/ui, Tailwind)
- Selector de comunidades: cards visuales, logo, nombre, descripción
- Multi-token input con preview dinámico
- Flow: Connect wallet → select comunidad → monto → confirmar → feedback

### User Flows
- Donador nuevo:
  1. Ingresa → conecta wallet
  2. Selecciona comunidad
  3. Elige token y monto
  4. Ve preview breakdown (95%/5%)
  5. Confirma y envía tx
  6. Ve dashboard: total donado + yield vault

- Admin/comunidad (vía demo):
  - Revisa dashboard de vault/yield (solo lectura en MVP)

### Wireframes (descripciones)
- Home: Header, selector de comunidades (cards), botón connect wallet.
- Comunidad: Dashboard con input donaciones y stats visibles.
- Confirmación: Modal con detalles breakdown fee/yield.
- Dashboard: Panel simple con historial, yield, totals. Link a tx onchain.

---

## 4. Technical Requirements

### Stack Tecnológico
- Smart contracts: Scaffold-ETH 2 (Foundry), Uniswap V4 hooks, Morpho Blue, ERC-4626 vault, deploy en Base Sepolia.
- Frontend: Next.js 14, shadcn/ui, Tailwind, wagmi, viem, RainbowKit.
- Integraciones: Uniswap V4, Morpho Blue API/SDK, Base Sepolia, hardcoded whitelisted communities.
- Seguridad: Deploy solo en testnet, sólo whitelisted addresses para vault, no distribuye yield autos (manual trigger solo demo), sin features de rewards/tokens en MVP.
- Constraints: No mobile, no governance, no auto-distribución de yield, sólo inclusión de 3-5 comunidades predefinidas.

---

## 5. Success Metrics (KPIs)

| Métrica           | Target                  | Timeline   |
|-------------------|------------------------|------------|
| Primeras donaciones | 10                   | Semana 3   |
| Total donado      | $500+                  | Semana 3   |
| Comunidades activas| 3                     | Semana 2   |
| Yield generado    | 1-2% APY mínimo        | Semana 4   |
| Product-market fit| Feedback positivo      | Semana 4   |

---

## 6. Implementation Roadmap

### Semana 1-2: Smart Contracts Core
- Implementar hook Uniswap V4 (5% fee, integración PoolManager)
- Implementar vault ERC-4626 básica (auto-deposit 5%)
- Tests unitarios y de integración
- Deploy contracts en Base Sepolia

### Semana 3: Frontend Core
- Selector de comunidades (visual, hardcoded)
- Multi-token input + flow de donación (interfaz, wagmi, viem)
- Integración wallet (RainbowKit)
- Modal de confirmación con breakdown fee/yield
- Dashboard donante: stats, historial, yield, comprobante tx

### Semana 4: Integración End-to-End + Demo
- Integrar vault stats vía Morpho SDK/API
- Testing end-to-end, bugfixing
- Trigger manual de distribución de yield para demo
- Video demo del flow completo
- Documentación técnica y de usuario

---

## Notas y Consideraciones
- No incluir mobile, rewards, sistemas de puntos o governance en MVP.
- Enfocarse en shipping rápido y funcionalidad end-to-end.
- Validar onboarding real con usuarios en hackathon/demo (feedback inmediato!)

---

**Ready for development: cada feature puede crearse como ticket en GitHub/Zapier/Linear.**