# Achados brutos — auditoria Jornada Games

## Busca
- /search cap fixo de 24 resultados. Sem contagem, sem paginação, sem "carregar mais" (verificado com scroll x4).
- "elsa": 24 resultados, 22 "Sem ofertas" (91,7%). Primeiro comprável = posição 17.
- "elsa" + available=1: 3 resultados. UM deles (Elsa - Ice Artisan 123/224, R$10) NÃO aparecia nos 24 sem filtro => item disponível inalcançável sem filtro.
- "pikachu": 24 resultados, 24 sem ofertas (100%).
- "charizar" (incompleto): 24 resultados, 24 sem ofertas.
- "elza" (typo): tolera erro, retorna Elsa. 23/24 sem ofertas.
- "OP02-013" (exemplo sugerido pelo PRÓPRIO placeholder do site): 6 resultados, 6 sem ofertas.
- Facetas contradizem a grade: em "pikachu" a sidebar diz Comum 193, Rara 11, Ultra Rara 19 etc, mas a grade entrega 24 e não há como chegar no resto.
- Ordenação padrão = "Numeração [0-9]" (número da carta), não relevância nem disponibilidade.
- "Apenas disponíveis" existe mas vem DESMARCADO por padrão.

## Taxonomia / dados
- Produtos SELADOS indexados com nome de carta e imagem de carta única.
  Ex: /product/221320/pikachu = "Rampardos the Attacker Constructed Half Deck" (Outros Selados, Produto lacrado)
  exibido com arte da carta Pikachu + texto de regras da carta. Códigos TP-xxxxx, raridade "None".
- Cards na grade renderizam em tamanhos diferentes (inconsistência visual).

## Home
- Hero 100% orientado a vendedor ("Tem cartas paradas? / Quero anunciar!"). Nenhum CTA de compra.
- Carrossel de coleções dominado por "EM BREVE" (Magic, Yu-Gi-Oh, Digimon, Star Wars, FaB, FF, Dragon Ball).
- Todos os destaques da home marcados "Baixa liquidez".

## CORREÇÕES às notas iniciais
- Paginação EXISTE (Anterior/1/2/.../Próxima) e o param ?page=N funciona; filtros persistem na URL e o scroll é preservado. Meus primeiros testes de scroll infinito me enganaram.
- Carrinho FUNCIONA (localStorage jg_cart) e é bom: agrupa por vendedor, subtotal por vendedor, checkbox "Incluir neste pedido", cross-sell "Aproveite o frete deste vendedor". O badge do header atualiza.

## FRETE — medições reais (comprador em Salvador/BA)
Carrinho A (2 vendedores, 7 cartas):
  Itens R$ 0,75 | Frete R$ 52,35 (Cadu PAC 27,60 + danfox PAC 24,75) | TOTAL R$ 53,10
  Frete = 98,6% do total. SEDEX seria 62,32 + 48,47 = R$110,79.
Carrinho B (1 vendedor, 6 cartas — removida 1 carta de R$0,05):
  Itens R$ 0,70 | Frete R$ 24,75 | TOTAL R$ 25,45
=> Remover UMA carta de 5 centavos de um 2º vendedor economiza R$ 27,65 (52% do total).
   A interface nunca mostra isso: o carrinho só diz "Frete: calculado no checkout".
- PAC R$27,60 para UMA carta em envelope é caro (carta registrada ~R$10-15).
- Consolidação funciona de fato: +2 cartas do danfox custaram R$0,30 e R$0,00 de frete extra.

## Checkout
- "Entrega em / Usando o endereço do seu cadastro." — NÃO mostra o endereço. Não dá para conferir a cidade.
- Botão "Continuar" desabilitado sem explicar (falta escolher pagamento, que fica muito abaixo da dobra).
- Pagamento: Cartão, Saldo Carteira, Boleto, Pix (RECOMENDADO), Cripto (EM BREVE).
  Contradiz o FAQ ("Os pagamentos acontecem pela carteira Jornada") — a favor do usuário.
- Sem opção de retirada local. Sem juntar envios entre vendedores.

## Bug: cross-sell do carrinho não re-renderiza
- Clicar "+" em "Aproveite o frete deste vendedor" grava no localStorage mas NÃO atualiza lista, badge nem resumo. Só aparece após reload. Clicar 2x não duplica (qtd fica 1).

## Contradição documental sobre frete
- /envios: "Compra direta: O frete aparece e é pago no próprio checkout... Um pagamento só, nenhuma surpresa depois."
- /ajuda: "Quem paga o frete? O comprador. Quando o negócio fecha, você recebe uma cobrança de frete com prazo para pagamento."
- /ajuda: "E se eu não pagar o frete no prazo? A compra é cancelada automaticamente."

## Ordenação
- "Numeração [0-9]" e "Nome [A-Z]" produzem resultado idêntico (alfabético). Ordenar por número da carta é impossível.
  Evidência: set 10 default -> Akela(90/224), Aladdin(216/224), Aladdin(123/224), Anna(139/224), Ares(104/224).
- "Menor preço" (sort=price_asc) funciona e joga os disponíveis para cima — é o workaround real.
- Opções: Numeração 0-9/9-0, Nome A-Z/Z-A, Menor preço, Maior preço, Maior liquidez. Sem "Relevância", sem "Disponibilidade".

## Filtros — responsividade (reproduzido)
- Abaixo de ~1024px a sidebar vira botão "Filtros" (accordion inline, não drawer).
- 900x800: painel 1623px (2x a viewport). Primeiro resultado em y=2026. Botão "Filtros" fica ABAIXO do painel (y=1954).
- 390x844 (mobile): painel 1618px, 1º resultado em y=2069.
- Sem X, sem "Aplicar", sem barra fixa, sem contagem de resultados.

## Facetas
- Lorcana: Expansão, Condição, Raridade, Idioma, Tinta, Artista
- Pokémon / One Piece: ... Energia ... (em One Piece os valores são CORES: Vermelho/Azul/Verde/Roxo/Amarelo/Preto -> rótulo errado)
- Mesma faceta chamada "Cor" (busca global) e "Tinta" (página Lorcana).
- NÃO existe: filtro de preço, filtro de localização/estado/cidade, filtro por vendedor, filtro de acabamento (foil/normal).
- Sem contagem de resultados em nenhuma listagem de cartas.

## Vendedor / confiança
- Página do vendedor sem cidade/estado, sem política de envio, sem prazo.
- "Vendedor verificado" com "Vendas: 0" e "Avaliação: -".
- Números divergentes no mesmo perfil: Total de itens 211 / Itens únicos 137 / aba Anúncios 147.
- Sem busca dentro da loja do vendedor; facetas só: Card Game, Idioma, Condição, Graduadoras, Nota. Sem expansão, sem nome, sem preço.

## Preço / liquidez
- Vendedor "danfox" inundou o catálogo Lorcana com centenas de anúncios a R$0,10, definindo o piso de "Menor Vendedor" de todo o set.
- "Baixa liquidez 0/100" e "Sem vendas no período" em praticamente tudo, inclusive nos destaques da home.

## SEO / arquitetura
- Todas as páginas de set/coleção vivem em /search e são "noindex, follow".
- Canonical dessas páginas aponta para a HOME (https://jornadagames.com/) — canonical errado.
- Home e /search sem H1.
- sitemap.xml tem 27 URLs: nenhum produto, nenhuma loja, nenhum set.
- Páginas de produto e de loja são index+follow com JSON-LD (bom), mas fora do sitemap.

## Autocomplete
- 8 sugestões todas com o mesmo nome ("Charizard"), sem nome do set, sem preço, sem disponibilidade.
- Mostra "None" literal como raridade; e "008/108 ·" com separador órfão.
- Duas sugestões sem imagem.
- Abas "Produtos / Artigos / Decks" não aparecem na árvore de acessibilidade; sugestões só clicáveis com mouse.

## Taxonomia
- Produtos SELADOS indexados com nome+arte de carta. /product/221320/pikachu = "Rampardos the Attacker Constructed Half Deck".
- Numeração divergente: site diz (70/224), a carta impressa diz 70/204.

## CORREÇÕES (2ª rodada) — coisas que eu tinha lido errado
- "Comprar agora" e "Dê o seu lance" FUNCIONAM, logado e deslogado. Abrem modal/painel.
  Meu erro: eu lia só os primeiros 400 chars do body e tirava screenshot logo após open() (topo da página).
- NÃO há salto de scroll ao clicar nos CTAs (medido: scrollY 768->768 e 1590->1590). Artefato do meu reload.
- O modal "Frete e total" do "Comprar agora" é MUITO BOM: item + PAC/SEDEX com preço + total + cross-sell + "Ver todas as cartas da loja".

## Frete é bloqueado por cadastro (deslogado)
- Modal deslogado: "Entre na sua conta para calcular o frete até o seu CEP. [Entrar]". Sem campo de CEP.
- Não existe botão de checkout no modal deslogado — o caminho de compra termina ali.
- Para saber que uma carta de R$0,10 custa R$24,85 entregue, é preciso cadastro em 3 etapas com endereço completo.

## Densidade de oferta no marketplace inteiro (24 itens/página)
| Jogo | catálogo (~) | com oferta (~) | % |
| Pokémon | 2.168 pg ~52.000 | 62 pg ~1.490 | ~2,9% |
| Disney Lorcana | 133 pg ~3.190 | 19 pg ~460 | ~14,3% |
| One Piece TCG | 295 pg ~7.080 | 31 pg ~745 | ~10,5% |
| Riftbound | 62 pg ~1.490 | 1 pg <=24 | ~1,6% |
TOTAL ~63.700 produtos, ~2.720 com oferta => ~96% do catálogo sem nenhuma oferta.
(páginas finais podem ser parciais; são limites superiores, a razão se mantém)

## Decklist: teste real com 10 staples de Lorcana
10 buscas manuais, 39 resultados, 1 carta com oferta (Dragon Fire, 1 anúncio).
Elsa-Spirit of Winter 0 | Mickey-Brave Little Tailor 0 | Be Prepared 0 | Beast-Hardheaded 0 |
Maui-Hero to All 0 | Sisu-Divine Water Dragon 0 | Tinker Bell-Giant Fairy 0 | Pete-Games Referee 0 |
Dragon Fire 1 | The Queen-Wicked and Vain 0
=> A jornada "comprar um deck" é hoje inviável por FALTA DE OFERTA, não por falta de importador.

## Causa raiz do catálogo vazio (lado vendedor)
FAQ "Como funciona um anúncio?": "Você busca a carta no catálogo, ENVIA FOTOS REAIS DO SEU EXEMPLAR,
define a condição e o preço. TODO ANÚNCIO PASSA POR REVISÃO DA EQUIPE antes de ir ao ar."
- Nenhuma menção a importar/CSV/planilha/lote/inventário em /ajuda, /blog, /quem-somos, /taxas.
- Cadastro de vendedor = KYC completo antes de ver qualquer tela de anúncio:
  Nome completo, NOME DA MÃE, CPF, RG, Data de nascimento, RENDA MENSAL, País de nascimento -> Telefone -> Identidade.
- As fotos reais exigidas NÃO aparecem para o comprador: a página de produto só mostra a arte oficial
  (assets.jornadagames.com/tcg/.../9-92.avif) e o avatar do vendedor. Custo alto, benefício invisível.
- Página /sell remove toda a navegação; única saída é um link rotulado "Sair" (que na verdade vai para /account).

## Numeração divergente da carta impressa
- "Aladdin - Prince Ali": site (92/225), coleção "Fabled"; carta impressa: 92/204 · EN · 9.
- "Big Nose - Lovesick Poet": site (70/224); carta impressa: 70/204 · EN · 10.
- Buscar "92/204" retorna Tamatoa, Ray, Olivia — NÃO retorna Aladdin.
- Buscar "70/204" retorna Beast, Jasmine — NÃO retorna Big Nose.
- O catálogo mistura convenções: alguns sets usam /204, outros /224 e /225.
- Na mesma tela aparecem 3 notações: título (92/225), modal (9-92), arte (92/204).

## Filtros
- "Apenas disponíveis" persiste na URL, mas precisa ser reaplicado a cada jogo/sessão. Nunca é lembrado.
- Modal "Frete e total" não usa role=dialog / aria-modal.

## CORREÇÕES (3ª rodada) — RECURSOS QUE EXISTEM E EU TINHA DADO COMO AUSENTES
1. FILTRO "Localização do vendedor" EXISTE em todos os jogos (estado + cidade).
   Meu erro: enumerei facetas com filtro length<25 e o rótulo tem 23+ chars... na verdade o seletor
   h3,h4,summary,legend não pegava esse bloco. Erro meu de medição.
   Valores (Pokémon, disponíveis): SP 598, RJ 291, SC 201, DF 191, RS 128, PR 106, ES 89, PB 77,
   MG 52, AM 13, MT 10, PE 9, BA 7, GO 7, PI 3, SE 2, CE 1. Cidades também (Brasília 191, Bariri 35...).
   BUG DE DADOS: aparece uma cidade chamada "257 (SP)" na lista.
2. LOCALIZAÇÃO DO VENDEDOR aparece na página da loja: "Envia de Rio de Janeiro/RJ" / "Envia de São Paulo/SP".
   Visível inclusive DESLOGADO.
3. CALCULADORA DE FRETE na página da loja, com campo "Seu CEP", funciona DESLOGADO.
   Testado: Cadu's Store (RJ) -> CEP 41810-011 (Salvador) = PAC R$27,60 / SEDEX R$62,32.

## O QUE DE FATO FALTA (revisado)
- Localização e frete NÃO aparecem onde a decisão acontece: nem nos cards da busca, nem na página do produto,
  nem na linha do anúncio ("Cadu 's Store | Vendas 0 | Avaliação - | NM | EN | R$0,05 | Comprar").
  Existem na página da LOJA — um lugar que o comprador só visita depois de já ter escolhido a carta.
- Sem filtro de faixa de preço.
- Sem filtro de acabamento (foil/normal) na listagem.
- Sem ordenação por "melhor custo entregue" / relevância / disponibilidade.

## CENÁRIO SALVADOR — números definitivos (itens disponíveis no estado)
Bahia: Pokémon 7 | Lorcana 1 | One Piece 15 | Riftbound 0  => TOTAL 23 itens no marketplace inteiro.
São Paulo: Pokémon ~25 pg (~600) | Lorcana ~16 pg (~380) => só esses dois já ~980.
=> A ferramenta de localização é boa; a GEOGRAFIA DA OFERTA é que inviabiliza a compra local fora do Sudeste.
=> Para um jogador de Lorcana em Salvador, "comprar perto de mim" = 1 carta.
