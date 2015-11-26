---
layout: post
title: "Documentação Automática de Haskell com Haddock"
date: 2012-03-17 18:43:17 -0300
comments: true
categories: [dica, documentação, haddok, haskell, doc, docs, pt_BR]
---

E aí!

O [Haddock](http://www.haskell.org/haddock/) é uma ferramenta de geração
automática de documentação para código Haskell. Atualmente, apesar de eventuais
bugs e dificuldades de utilização, ele está sendo mantido por seus idealizadores.
Quem utiliza GHC provavelmente já dispõe do comando `> haddock`.

Depois de labutar um bocado, consegui gerar documentação em formato HTML a partir
de meu código Haskell.

<!-- more -->

* O código
```haskell
-- | 'Primos' agrega funções relacionadas aa primalidade dos numerais.
module Primos where
{
-- | A função 'crivo' recebe um número maior que zero e retorna uma lista de Int com todos os números primos até n. Ela utiliza a função 'ehPrimo' para descobrir se um número é primo. :)
;
crivo :: Int -> [Int];
crivo n = if n < 2 then [] else [y | y <- [2..n], ehPrimo y];

-- | 'ehPrimo' recebe um número inteiro maior que zero e retorna True se ele for primo ou False caso contrário.
;
ehPrimo :: Int -> Bool;
ehPrimo 1 = False;
ehPrimo n = (null [y | y <- [1..(truncate(sqrt (fromIntegral n)))], n `mod` y == 0, y /= n, y /= 1]);
}
```
* O comando
```bash
$ mkdir HaddockDoc
$ haddock -h -o HaddockDoc/ Primos.hs
```

* O Resultado

Você vê abrindo o index.html na nova pasta HaddockDoc

Valeu!
