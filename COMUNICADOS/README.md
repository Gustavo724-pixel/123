# COMUNICADOS — Templates de Armadores

Esta pasta guarda um JSON de template para cada armador. O gerador HTML
(logmakers-cowork) carrega esses arquivos e popula a interface.

## Estrutura

```
COMUNICADOS/
  <NOME DO ARMADOR>/
    template.json
```

## Schema do template.json

```jsonc
{
  "key":         "CMA",                              // identificador curto (sem espaços)
  "name":        "CMA CGM",                          // nome de exibição
  "color":       "#C8102E",                          // cor da marca (hex)
  "fullName":    "CMA CGM (China) Shipping Co., Ltd",
  "salutation":  "Dear Valued Customers,",
  "closing":     "Customer Service Officer\n...",   // pode ter quebras de linha (\n)
  "layout":      "cma",                              // cma | zim | hmm | pil | generic
  "bodyRollover": "We regret to inform... {vO} ... {vN} ...",
  "bodyVessel":   "...",
  "bodyDelay":    "...",
  "bodyOther":    "..."
}
```

## Placeholders disponíveis nos corpos

- `{vO}` — Navio original
- `{vN}` — Novo navio
- `{booking}` — Booking number
- `{bl}` — B/L number
- `{container}` — Container number
- `{pol}` — Porto de origem
- `{pod}` — Porto de destino
- `{name}` — Nome do armador

Se um placeholder estiver vazio no formulário, o gerador substitui por um
fallback razoável (ex.: `{vO}` vazio vira "[VESSEL]").

## Layouts

- `cma`     — Cabeçalho "ASIA - LATAM SERVICES / CUSTOMER ADVISORY", tabela de booking/container.
- `zim`     — Cabeçalho "Customer Advisory — Operational Update", linha de BL/Vessel/POL/POD.
- `hmm`     — Cabeçalho técnico com DATE/FROM/RE, tabela "CNTR NO. / B/L NO. / POR/POL/POD", e blocos ORIGINAL/NEW.
- `pil`     — Cabeçalho "ROLLOVER NOTICE", linha de booking/container, data ISO no rodapé.
- `generic` — Cabeçalho "FM:/DATE:/RE:" + tabela ORIGIN/DESTINATION/ORIGINAL VESSEL/NEW VESSEL (ONE, MSC, MAERSK).

Se um armador novo precisar de um formato diferente, me avise para
estender o gerador com um novo layout.
