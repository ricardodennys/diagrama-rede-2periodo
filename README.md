# Diagrama de Rede - Hierárquico Colapsado

## Aluno
Ricardo Dennys - 2º Período - Redes de Computadores

## Descrição
Diagrama de rede para cenário com 17 PCs, 5 switches e 5 Access Points no mesmo andar, utilizando topologia hierárquica colapsada (Core + Distribuição). Sendo 12 PCs conectados via cabo e 5 PCs via Wi-Fi.

O projeto apresenta duas versões:
- **Versão 1.0:** Topologia simples (sem redundância)
- **Versão 2.0:** Topologia com redundância (2 Switch Core + links duplos)

---

## Versão 1.0 - Sem Redundância

### Equipamentos
- 1 Switch Core L3 (Core + Distribuição)
- 5 Switches de Acesso
- 5 Access Points (Wi-Fi)
- 17 Computadores (12 cabo + 5 Wi-Fi)

### Distribuição dos PCs

| Switch | PCs Cabo | Access Point | PCs Wi-Fi | Total |
|--------|----------|--------------|-----------|-------|
| Switch 1 | 3 | AP-01 | 1 | 4 |
| Switch 2 | 3 | AP-02 | 1 | 4 |
| Switch 3 | 2 | AP-03 | 1 | 3 |
| Switch 4 | 2 | AP-04 | 1 | 3 |
| Switch 5 | 2 | AP-05 | 1 | 3 |
| **Total** | **12** | **5 APs** | **5** | **17** |

### VLANs

| VLAN | Setor | Rede | Hosts |
|------|-------|------|-------|
| 10 | Setor 1 | 192.168.10.0/24 | 4 |
| 20 | Setor 2 | 192.168.20.0/24 | 4 |
| 30 | Setor 3 | 192.168.30.0/24 | 3 |
| 40 | Setor 4 | 192.168.40.0/24 | 3 |
| 50 | Setor 5 | 192.168.50.0/24 | 3 |

### Tabela de Endereçamento IP

| Equipamento | VLAN | IP | Conexão |
|-------------|------|----|---------|
| Switch Core L3 | - | 192.168.0.1/24 | - |
| **Switch 1** | 10 | 192.168.10.1/24 | - |
| PC 1 | 10 | 192.168.10.2 | Cabo |
| PC 2 | 10 | 192.168.10.3 | Cabo |
| PC 3 | 10 | 192.168.10.4 | Cabo |
| AP-01 | 10 | 192.168.10.5 | Cabo |
| PC 4 | 10 | 192.168.10.6 | Wi-Fi |
| **Switch 2** | 20 | 192.168.20.1/24 | - |
| PC 5 | 20 | 192.168.20.2 | Cabo |
| PC 6 | 20 | 192.168.20.3 | Cabo |
| PC 7 | 20 | 192.168.20.4 | Cabo |
| AP-02 | 20 | 192.168.20.5 | Cabo |
| PC 8 | 20 | 192.168.20.6 | Wi-Fi |
| **Switch 3** | 30 | 192.168.30.1/24 | - |
| PC 9 | 30 | 192.168.30.2 | Cabo |
| PC 10 | 30 | 192.168.30.3 | Cabo |
| AP-03 | 30 | 192.168.30.4 | Cabo |
| PC 11 | 30 | 192.168.30.5 | Wi-Fi |
| **Switch 4** | 40 | 192.168.40.1/24 | - |
| PC 12 | 40 | 192.168.40.2 | Cabo |
| PC 13 | 40 | 192.168.40.3 | Cabo |
| AP-04 | 40 | 192.168.40.4 | Cabo |
| PC 14 | 40 | 192.168.40.5 | Wi-Fi |
| **Switch 5** | 50 | 192.168.50.1/24 | - |
| PC 15 | 50 | 192.168.50.2 | Cabo |
| PC 16 | 50 | 192.168.50.3 | Cabo |
| AP-05 | 50 | 192.168.50.4 | Cabo |
| PC 17 | 50 | 192.168.50.5 | Wi-Fi |

---

## Versão 2.0 - Com Redundância

### Alterações realizadas

| Item | Versão 1.0 (Sem Redundância) | Versão 2.0 (Com Redundância) |
|------|------------------------------|------------------------------|
| Switch Core | 1 | 2 (Core A e Core B) |
| Links Core → Acesso | Simples (cada switch ligado apenas ao Core A) | Duplos (cada switch ligado aos dois Cores) |
| Tolerância a falhas | Baixa (ponto único de falha) | Alta (se um Core cair, o outro assume) |
| STP (Spanning Tree) | Não | Sim |
| Custo | Menor | Maior |
| Disponibilidade | 99% | 99,9% |

### Topologia com Redundância
markdown
### Topologia com Redundância
SWITCH CORE L3 A ───── SWITCH CORE L3 B
│ \ / │
│ \ / │
│ \ / │
│ X │
│ / \ │
│ / \ │
│ / \ │
┌────┴────┐ ┌────┴────┐ │
│ │ │ │ │
SWITCH 1 SWITCH 2 SWITCH 3 SWITCH 4 SWITCH 5
(4 PCs) (4 PCs) (3 PCs) (3 PCs) (3 PCs)

AP-01 + AP-02 + AP-03 + AP-04 + AP-05

### Como funciona a redundância

1. **Dois Switch Core L3** (A e B) em cluster
2. **Conexão direta** entre os dois Cores para sincronização
3. **Cada switch de acesso** conectado aos dois Cores
4. **STP (Spanning Tree Protocol)** ativo:
   - Em condições normais, um link fica bloqueado para evitar loops
   - Se o link ativo cair, o STP ativa o link de backup automaticamente
   - Tempo de recuperação: ~30-50 segundos (ou menos com RSTP)

### Benefícios da Redundância

- ✅ **Alta disponibilidade:** Se um Core cair, a rede continua funcionando
- ✅ **Tolerância a falhas:** Falha em um link não para a rede
- ✅ **Manutenção programada:** É possível desligar um Core para manutenção sem afetar a rede
- ✅ **Caminhos alternativos:** O tráfego pode ser balanceado entre os dois Cores

### Protocolos Utilizados

| Protocolo | Função |
|-----------|--------|
| **STP / RSTP** | Gerencia links redundantes, evita loops e ativa links de backup |
| **VRRP / HSRP** | (Opcional) Gateway virtual para alta disponibilidade |
| **EtherChannel** | (Opcional) Agregação de links para aumentar banda |

---

## Ferramentas
- Mermaid (diagrama)
- Git/GitHub (versionamento)

## Como visualizar
1. Acesse: https://mermaid.live/
2. Cole o código do arquivo `diagrama.mmd` (versão 1.0) ou `diagrama-com-redundancia.mmd` (versão 2.0)
3. Exporte como PNG ou SVG

## Link do Repositório
https://github.com/ricardodennys/diagrama-rede-2periodo
