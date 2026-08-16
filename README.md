# Canopy

Calculadora de cultivo indoor. Estima produtividade a partir da entrega de fótons e confere se o espaço comporta o que você planejou.

**→ https://draudacity.github.io/canopy/**

## O que ela faz

A partir da estufa, da luminária, da genética, do substrato e da linha de fertilizante, a página calcula:

- **Produção estimada** em g, g/m², g/pé², g/W e g/planta, sempre com faixa de variação
- **Entrega de luz** — PPF, PPFD médio no dossel, DLI de vega e de floração
- **Vai caber?** — se os vasos cabem fisicamente no piso, se o dossel está super ou sublotado, e se há altura para o stretch
- **Dimensionamento** — exaustor em m³/h, carga térmica, desumidificador, consumo de água e total de sais
- **Cronograma** semana a semana de EC, ppm, pH e PPFD alvo, com a porcentagem de luz correspondente

## O modelo

Tudo parte da entrega de fótons, não de fatores arbitrários:

```
watts × eficácia (µmol/J)          = PPF
PPF × aproveitamento ÷ dossel (m²) = PPFD
PPFD × fotoperíodo × 0,0036        = DLI
DLI × dias de floração × dossel    = mols totais
mols × g/mol                       = produção
```

Substrato, nutrição, manejo, genética, CO₂ e clima entram como multiplicadores sobre o **g/mol**. Três travas mantêm o resultado honesto:

1. **Bônus empilhados são amortecidos** (×0,75 acima de 1,0) — combinar coco, sais, SCROG e CO₂ nunca entrega o produto cheio na prática. Penalidades acumulam integralmente.
2. **Teto rígido de 0,26 g/mol**, o melhor resultado documentado em sala selada comercial (perto de 2 g/W).
3. **Saturação de fótons** — luz acima de ~900 PPFD com CO₂ ambiente conta só 35%, que é o que dispara os avisos de branqueamento.

A curva calibrada vai de 0,29 g/W (primeiro cultivo malfeito) a 1,80 g/W (sala selada com CO₂), passando por 1,08 g/W no caso intermediário — que é onde fica a referência popular de "1 grama por watt".

## Sobre as tabelas de dose

As linhas de fertilizante servem para classificar o **tipo de programa** e trazer observações de uso. A página **não** publica tabelas de dose em mL/L por marca: a EC é a grandeza física real e independe do frasco. Onde há orientação concreta de produto, ela se limita ao que é bem estabelecido — ordem de mistura da Flora Series, proporção 3-2-1 do Jack's, e a incompatibilidade entre cálcio e sulfato concentrados.

## Técnico

Arquivo único, sem dependências, sem build no cliente, **zero requisições externas** — funciona offline. Para regenerar a partir do fonte:

```bash
node build.js
```

## Aviso

Estimativa, não promessa. O resultado real varia com fenótipo, pragas, secagem e cura. Cultive apenas onde for legal para você e dentro dos limites da sua região.
