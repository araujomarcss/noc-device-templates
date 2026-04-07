# NOC Device Templates

Repositório de templates de monitoramento SNMP para o sistema NOC Flex (2Flex Telecom).

## Estrutura

```
/
├── index.json              # Índice de todos os templates disponíveis
├── mikrotik/
│   ├── ccr1016-12g.json
│   ├── ccr2004.json
│   ├── crs326.json
│   ├── crs354.json
│   ├── hap-ac2.json
│   ├── rb750gr3.json
│   └── rb4011.json
├── ubiquiti/
│   └── unifi-ap-ac-pro.json
└── cisco/
    └── isr4331.json
```

## Como adicionar um novo template

1. Crie um arquivo JSON na pasta do fabricante
2. Adicione a entrada no `index.json`
3. Siga a estrutura padrão abaixo

## Estrutura de um template

```json
{
  "tipo": "Router",
  "fabricante": "Mikrotik",
  "modelo": "Nome do Modelo",
  "snmp_version": "2c",
  "descricao": "Descrição do equipamento",
  "capabilities": [
    {
      "id": "ping",
      "label": "Nome para o usuário",
      "descricao": "Descrição do que monitora",
      "categoria": "Básico | Recursos | Rede | Wireless | Ambiente | Sistema",
      "requer_discovery": false,
      "itens": [
        {
          "id": "item_id",
          "nome": "Nome do item",
          "tipo": "ICMP_PING | ICMP_LOSS | ICMP_RESPONSE | SNMP_INT | SNMP_FLOAT | SNMP_STRING | SNMP_TIMETICKS | DELTA_BYTES",
          "oid": "1.3.6.1.2.1...",
          "unidade": "%, ms, bytes, bps"
        }
      ]
    }
  ]
}
```

## Tipos de item

| Tipo | Descrição |
|---|---|
| `ICMP_PING` | Ping ICMP (online/offline) |
| `ICMP_LOSS` | Perda de pacotes ICMP |
| `ICMP_RESPONSE` | Tempo de resposta ICMP |
| `SNMP_INT` | Valor inteiro via SNMP |
| `SNMP_FLOAT` | Valor decimal via SNMP |
| `SNMP_STRING` | Texto via SNMP |
| `SNMP_TIMETICKS` | TimeTicks (uptime) |
| `DELTA_BYTES` | Contador acumulado (tráfego) |

## Para capabilities com discovery

Quando `requer_discovery: true`, o sistema faz SNMP walk na OID `discovery_oid` para descobrir instâncias (interfaces, CPUs, etc.). Use `{index}` nos `oid_template` para substituição.
