# Painel de Engenharia Clínica

Dashboard de monitoramento em tempo real para departamentos de **Engenharia Clínica e Gestão de Tecnologias Medico-Hospitalares** conectado com o GLPI para gestão de chamados e parque tecnológico, desenvolvido com HTML, CSS e JavaScript puro — sem frameworks, sem dependências externas além de fontes Google. 

> **Este repositório contém a versão demo** com dados fictícios gerados localmente. A versão em produção consome dados em tempo real via API REST do [GLPI](https://glpi-project.org/), sistema de gestão de ativos e chamados técnicos.

---

## Visão geral

O painel roda diretamente no navegador (arquivo `.html`) e foi projetado para exibição contínua em TVs e monitores nos setores técnicos do hospital.

> [!WARNING]
> **DADOS FICTÍCIOS GERADOS ALEATORIAMENTE**  
> As informações exibidas nas imagens são apenas para demonstração.

### Tela 1 — Central
![Tela Central](https://github.com/augustxj/painel-engenharia-clinica/blob/main/Imagens/Tela%201.png?raw=true)

- Chamados por status (Novo, Em Atendimento, Planejado, Em Espera, Solucionado, Fechado)
- Distribuição por prioridade (barras horizontais)
- Top setores com mais chamados abertos — clicável para filtrar
- Parque de equipamentos por status operacional
- Chamados críticos (Alta / Muito Alta prioridade) em destaque

### Tela 2 — Métricas do Mês
![KPIs]([https://github.com/augustxj/painel-engenharia-clinica/blob/main/Imagens/Tela%202.png?raw=true])
- KPIs: chamados abertos, resolvidos, tempo médio de resolução, pendentes > 7 dias
- Gráfico de barras verticais: chamados por dia do mês
- Gráfico de rosca: distribuição por status
- Gráfico de rosca: distribuição por prioridade dos abertos
- Indicadores ONA com semáforo visual (verde/amarelo/vermelho)

### Tela 3 — Lista de Chamados
![Chamados]([https://github.com/augustxj/painel-engenharia-clinica/blob/main/Imagens/Tela%203.png?raw=true])
- Chamados abertos ordenados por prioridade
- Coluna de idade com cor dinâmica (verde/amarelo/vermelho)
- Modal de detalhes ao clicar em qualquer chamado

---

## Funcionalidades

| Recurso | Descrição |
|---|---|
| **Rotação automática** | Alterna entre as 3 telas a cada 30s (configurável: 15s / 30s / 60s) |
| **Pausar rotação** | Botão ⏸ na barra inferior ou tecla `Espaço` |
| **Navegação por teclado** | ← → para navegar, 1 2 3 para ir direto, R para atualizar |
| **Dots clicáveis** | Navega diretamente para qualquer tela |
| **KPIs clicáveis** | Cada indicador no header leva à tela relacionada |
| **Filtro por setor** | Clique em qualquer setor na Tela 1 → Tela 3 filtrada |
| **Modal de detalhes** | Clique em qualquer chamado para ver informações completas |
| **Alertas críticos** | Cards flutuantes aparecem automaticamente para chamados de alta prioridade |
| **Animação de contadores** | KPIs sobem animados ao atualizar |
| **Atualização automática** | Dados recarregados a cada 1 minuto (em produção, via API) |

---

## 🛠️ Stack e contexto

### Tecnologias
- **HTML5 / CSS3 / JavaScript ES2020** — sem frameworks
- **SVG nativo** — gráficos de rosca e gauge gerados via código
- **CSS Grid + Flexbox** — layout responsivo para TV fullscreen
- **Google Fonts** — Rajdhani (títulos), Share Tech Mono (dados), Inter (corpo)

### Integração em produção (GLPI)
Em produção, o painel se conecta ao **GLPI** via API REST:

```
GET /api.php/v1/initSession          → autenticação
GET /api.php/v1/Ticket               → chamados técnicos
GET /api.php/v1/Glpi\CustomAsset\... → inventário de equipamentos
```

Os dados são processados localmente no navegador — sem backend intermediário.

### Contexto hospitalar
Desenvolvido para um hospital com **acreditação UNACON** (oncologia) e certificação **ONA (Organização Nacional de Acreditação)**. Os indicadores da Tela 2 foram mapeados conforme os requisitos ONA para engenharia clínica:

- Taxa de resolução de chamados ≥ 80% → ✅ Adequado
- Chamados críticos em aberto → monitoramento contínuo
- Tempo médio de resolução → rastreabilidade para auditorias
- Chamados pendentes > 7 dias → indicador de risco operacional

---

## 🚀 Como usar

### Demo (este repositório)
```bash
# Clone o repositório
git clone https://github.com/seu-usuario/painel-engenharia-clinica

# Abra o arquivo no navegador
open index.html
# ou simplesmente arraste o arquivo para o Chrome
```

Sem instalação, sem servidor, sem dependências. Funciona offline.

### Produção (com GLPI)
1. Configure as credenciais no início do script:
```javascript
const API   = "http://SEU_GLPI/api.php/v1";
const APP_T = "SEU_APP_TOKEN";
const USR_T = "SEU_USER_TOKEN";
```
2. Abra o arquivo no Chrome
3. Para exibição em TV: `F11` para fullscreen

---

## 📁 Estrutura

```
painel-engenharia-clinica/
├── painel.html       → Dashboard completo (demo com dados fictícios)
├── README.md        → Este arquivo
└── Imagens   → Prints do painel em funcionamento
    ├── Tela 1
    ├── Tela 2
    └── Tela 3
```

---

## 👤 Sobre

Desenvolvido por **João Augusto Ferreira** — Biomédico, atuando na gestão de equipamentos médico-hospitalares com foco em qualidade, rastreabilidade e conformidade com padrões de acreditação.

- 📍 Minas Gerais, Brasil
- 🏥 Experiência em ambiente hospitalar com UNACON e processo ONA
- 🛠️ Ferramentas: GLPI, Looker Studio, PDCA, gestão de inventário técnico

---

## 📄 Licença

Este projeto é de uso livre para fins educacionais e de portfólio.
Dados exibidos neste repositório são **inteiramente fictícios**.
