# Stacked Cards Scroll

## Resumo

Pilha de cards sobrepostos que se transforma conforme o usuario rola a pagina.
Cada card possui sua propria janela de animacao e sai da pilha em momentos
diferentes, criando um efeito de narrativa visual conduzida por scroll.

## Quando usar

- Depoimentos em formato mais editorial
- Storytelling em paginas "about"
- Blocos de etapas ou cases com scroll imersivo
- Secoes em que o usuario deve sentir progresso e profundidade

## Stack sugerida

- React
- Framer Motion
- Tailwind CSS

## Mecanica do efeito

1. Um container alto, como `400vh`, cria um trilho de scroll longo.
2. Dentro dele, um bloco `sticky` segura os cards na tela.
3. Cada card calcula seu `start` e `end` com base no proprio indice.
4. `useTransform` converte `scrollYProgress` em `y`, `rotate`, opacidade e blur.
5. O deck parece ser desmontado aos poucos, e nao de uma vez.

## Checklist de implementacao

- Criar um wrapper com `relative h-[400vh]`
- Fixar a pilha com `sticky top-0 h-screen`
- Renderizar os cards com `absolute inset-0`
- Calcular janelas de animacao por indice
- Variar profundidade inicial com `zIndex` e `translateZ`
- Ajustar blur e sombra para reforcar a mudanca de foco

## Prompt de reutilizacao

> Crie um componente `Stacked Cards Scroll` para React com Framer Motion.
> Monte um container de scroll alto e, dentro dele, uma pilha `sticky` de
> cards absolutos. Cada card deve sair da pilha em uma janela diferente de
> progresso, movendo para cima, reduzindo opacidade, ajustando blur e
> endireitando a rotacao. O resultado precisa parecer uma pilha fisica sendo
> distribuida uma a uma conforme o usuario rola.

## Snippet base

```tsx
import { motion, useScroll, useTransform } from 'framer-motion';
import { useRef } from 'react';

type CardProps = {
  index: number;
  total: number;
  scrollYProgress: any;
};

const StackedCard = ({ index, total, scrollYProgress }: CardProps) => {
  const start = index / total;
  const end = (index + 1) / total;

  const y = useTransform(scrollYProgress, [start, end], ['0%', '-160%']);
  const rotate = useTransform(scrollYProgress, [start, end], [5, 0]);
  const opacity = useTransform(scrollYProgress, [start, end], [1, 0.35]);
  const filter = useTransform(
    scrollYProgress,
    [start, end],
    ['blur(0px)', 'blur(6px)']
  );

  return (
    <motion.article
      style={{ y, rotate, opacity, filter, zIndex: total - index }}
      className="absolute inset-0 rounded-[2rem] bg-white/80 p-8 shadow-2xl backdrop-blur-xl"
    >
      <h3 className="text-xl font-semibold">Card {index + 1}</h3>
      <p className="mt-3 text-neutral-600">Conteudo do depoimento ou case.</p>
    </motion.article>
  );
};

const StackedCardsScroll = () => {
  const ref = useRef<HTMLDivElement | null>(null);
  const { scrollYProgress } = useScroll({ target: ref });
  const items = [1, 2, 3, 4];

  return (
    <section ref={ref} className="relative h-[400vh]">
      <div className="sticky top-0 flex h-screen items-center justify-center overflow-hidden">
        <div className="relative h-[520px] w-full max-w-xl">
          {items.map((_, index) => (
            <StackedCard
              key={index}
              index={index}
              total={items.length}
              scrollYProgress={scrollYProgress}
            />
          ))}
        </div>
      </div>
    </section>
  );
};

export default StackedCardsScroll;
```

## Referencia original

- Projeto de origem: `stephanie-bolsoni-website`
- Arquivo de notas: `C:/Users/pedro/Desktop/WEB STAR/stephanie-bolsoni-website/STACKED_CARDS_SCROLL_EFFECT.md`
- Componente citado nas notas: `src/components/blocks/animated-cards-stack.tsx`
