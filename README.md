# Entre Turnos

**Um atlas sobre como o Brasil votou e como seus territórios mudaram.** Explore as eleições de 2018, 2022 e 2026 para presidente e governador. Compare a margem entre os turnos, filtre UFs por indicadores e consulte a trajetória de cada estado ao longo dos governos.

**[Baixar o projeto completo](https://github.com/GabrielBelluco/entre-turnos/raw/refs/heads/main/Entre-Turnos.zip)** · código, dados tratados e Power BI.

A publicação no Pages está configurada. A primeira execução ficou bloqueada por uma pendência de cobrança informada pelo GitHub. [Ver execução](https://github.com/GabrielBelluco/entre-turnos/actions/runs/44358841397).

## Três recortes para explorar

1. **A disputa estadual se estreitou na capital capixaba.** Em Vitória, a vantagem de Lorenzo Pazolini sobre Ricardo Ferraço passou de 31,5 para 7,5 pontos percentuais em 2026. Em Vila Velha, passou de 26,9 para 8,8 p.p. [Vitória](https://gabrielbelluco.github.io/entre-turnos/?ano=2026&cargo=governador&uf=ES&local=3205309&modo=shift#atlas) · [Vila Velha](https://gabrielbelluco.github.io/entre-turnos/?ano=2026&cargo=governador&uf=ES&local=3205200&modo=shift#atlas)
2. **A margem mudou no mesmo sentido para ambos os cargos em Vitória?** Na eleição presidencial de 2026, a desvantagem de Lula sobre Flávio Bolsonaro na cidade passou de 7,9 para 3,6 p.p. É um ganho de 4,2 p.p. para Lula na comparação entre turnos. [Presidencial em Vitória](https://gabrielbelluco.github.io/entre-turnos/?ano=2026&cargo=presidente&uf=ES&local=3205309&modo=shift#atlas)
3. **O Espírito Santo tinha 42,5 homicídios registrados por 100 mil habitantes em 2014 e 26,0 em 2024.** Consulte os anos intermediários e compare com São Paulo na linha do tempo. [Evolução por UF](https://gabrielbelluco.github.io/entre-turnos/#evolucao) · [Atlas da Violência 2026](https://repositorio.ipea.gov.br/entities/publication/9ab87dfc-33eb-4ac2-8a54-f4f1543dabbc)

## Rodar no computador

Abra **Entre-Turnos.html** no navegador se tiver baixado a versão offline. Para desenvolver com Node.js 24, use `npm ci` e `npm run dev`. Na distribuição que contém `dist/`, `node preview.mjs` disponibiliza os arquivos compilados em `http://127.0.0.1:4175/`. Os dados tratados já acompanham o projeto. `npm run build:offline` gera novamente o HTML autônomo.

```bash
npm ci
npm run data:check
npm run build
```

Para refazer a base, use `npm run data:download` e `npm run data:build`. Os ZIPs de votação somam mais de 1,4 GB. O download usa `.data/raw` e a extração usa `.data/cache` por padrão. As variáveis `ENTRE_TURNOS_RAW` e `ENTRE_TURNOS_CACHE` permitem apontar para pastas já existentes. Para estudar o pipeline em escala menor, passe `-- --pilot` aos dois comandos. Os arquivos do piloto saem em `public/pilot`. O comando de validação cobre a base nacional.

## Power BI

Em `bi/`, abra **Entre Turnos.pbip** com uma versão recente do Power BI Desktop. A primeira página tem filtros de ano, cargo, turno e UF, cartões e votação por candidato. A segunda mostra séries anuais e uma tabela de mandatos estaduais. O modelo importa os CSVs com Power Query e define as relações e medidas em código. Os dados estão incorporados às consultas do projeto e os CSVs tratados também estão disponíveis em `bi/data`.

1. Use **Atualizar** na primeira abertura para carregar os dados e abra **Transformar dados** para conferir o passo de tipagem no Power Query.
2. Abra **Modelo** e siga a relação de UF → município → votos. A série anual fica no nível da UF.
3. Compare um resultado capixaba com o site. Abra a medida **Percentual do candidato** para ver como o denominador permanece vinculado à apuração e responde ao recorte.
4. Use **Salvar como** no Desktop para gerar o formato `.pbix`. `npm run bi:build` regenera o projeto aberto a partir dos CSVs.

## Fontes e regras

- O **TSE** fornece votação nominal, detalhe de apuração e correspondência com códigos do IBGE. O pipeline soma zonas por município, cargo e turno, restringe às eleições ordinárias e usa os votos nominais válidos. A auditoria confere a soma dos candidatos em cada localidade e o segundo turno presidencial de cada edição. A visualização nacional usa as 27 UFs. A auditoria presidencial incorpora a votação do exterior. [TSE 2018](https://dadosabertos.tse.jus.br/dataset/resultados-2018) · [TSE 2022](https://dadosabertos.tse.jus.br/dataset/resultados-2022) · [TSE 2026](https://dadosabertos.tse.jus.br/dataset/resultados-2026)
- A **margem** é a diferença percentual entre os mesmos dois finalistas, com ordenação pelo resultado do último turno da disputa. **Mudança** é a margem do segundo turno menos a margem do primeiro. Uma inversão exige sinais opostos. Comparecimento é a soma dos votantes dividida pela soma de aptos. A malha IBGE 2025 é comum a todos os pleitos. [IBGE](https://www.ibge.gov.br/geociencias/organizacao-do-territorio/malhas-territoriais/15774-malhas.html)
- As **séries estaduais** usam o Radar IDHM, a taxa de homicídios registrados do Atlas da Violência e a PNAD Contínua para desocupação e renda domiciliar real. Cada filtro cruza a eleição com o último ano anterior de referência comum. Para 2026, há alfabetização municipal do Censo 2022 e IDHM municipal de 2010. A cobertura histórica do IDHM acompanha a base do Atlas do Desenvolvimento Humano, distribuída também pela ABJ, e aparece incompleta para municípios mais novos. [Radar IDHM](https://www.undp.org/pt/brazil/publications/radar-idhm-evolucao-do-idhm-e-de-seus-componentes-periodo-de-2012-2024) · [Desocupação](https://sidra.ibge.gov.br/tabela/10361) · [Renda real](https://sidra.ibge.gov.br/tabela/7533) · [Alfabetização](https://sidra.ibge.gov.br/tabela/9543) · [ABJ](https://abjur.github.io/abjData/reference/pnud_min.html)
- A cronologia combina registros oficiais e listas biográficas referenciadas. Cada faixa tem um link para a fonte registrada. A curadoria cobre mandatos, sucessões e algumas interinidades documentadas. A série descreve o que ocorreu no território durante o período.
