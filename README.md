# Diagrama de Rede - Hierárquico Colapsado

## Aluno
Ricardo Dennys - 2º Período - Redes de Computadores

## Descrição
Diagrama de rede para cenário com 17 PCs e 5 roteadores no mesmo andar, utilizando topologia hierárquica colapsada (Core + Distribuição).

## Equipamentos
- 1 Roteador Principal (Core + Distribuição)
- 5 Roteadores de Acesso
- 17 Computadores

## VLANs
| VLAN | Setor | Rede | Hosts |
|------|-------|------|-------|
| 10 | Setor 1 | 192.168.10.0/24 | 4 |
| 20 | Setor 2 | 192.168.20.0/24 | 4 |
| 30 | Setor 3 | 192.168.30.0/24 | 3 |
| 40 | Setor 4 | 192.168.40.0/24 | 3 |
| 50 | Setor 5 | 192.168.50.0/24 | 3 |

## Ferramentas
- Mermaid (diagrama)
- Git/GitHub (versionamento)

## Como visualizar
1. Acesse: https://mermaid.live/
2. Cole o código do arquivo `diagrama.mmd`
3. Exporte como PNG ou SVG
