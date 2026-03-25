# Staggered Stack Carousel

## Resumo

Carrossel de cards com composicao organicamente desalinhada. Os itens ficam
ancorados no centro do container, mas usam offsets alternados em `translateY`
e `rotate` para fugir do visual reto de um carousel convencional.

## Quando usar

- Depoimentos com pegada mais autoral
- Destaque de servicos ou especialidades
- Showcase de projetos em layout artistico
- Interfaces que pedem um clima menos rigido e mais editorial

## Stack sugerida

- React
- Tailwind CSS
- Framer Motion opcional para refinamentos extras

## Mecanica do efeito

1. Todos os cards partem de `left: 50%` e `top: 50%`.
2. O deslocamento horizontal define a ordem visual em torno do centro.
3. A alternancia de `translateY` e `rotate` cria o efeito `staggered`.
4. O card central ganha mais escala, mais opacidade e prioridade visual.
5. A troca de foco acontece rotacionando o array, o que permite um carousel
   infinito sem reposicionamento complexo.

## Checklist de implementacao

- Posicionar todos os cards de forma absoluta no centro
- Calcular `position` relativo ao meio do array
- Destacar o card central com `scale`, `opacity` e `zIndex`
- Aplicar offset vertical e rotacao alternada nos cards laterais
- Permitir clique em cards laterais para trazelos ao centro
- Reduzir numero de itens visiveis no mobile

## Prompt de reutilizacao

> Crie um `Staggered Stack Carousel` para React usando Tailwind CSS.
> Os cards devem nascer no centro do container e ocupar posicoes laterais com
> offsets alternados em Y e rotacao, formando uma composicao mais organica.
> O card central precisa ficar maior, mais opaco e mais alto. A navegacao deve
> girar o array de dados para que o carousel seja infinito e para que qualquer
> card lateral possa virar o foco ao ser clicado.

## Snippet base

```tsx
import { useState } from 'react';

const initialCards = [
  { title: 'Card 1' },
  { title: 'Card 2' },
  { title: 'Card 3' },
  { title: 'Card 4' },
  { title: 'Card 5' }
];

const StaggeredStackCarousel = () => {
  const [cards, setCards] = useState(initialCards);

  const centerIndex = Math.floor(cards.length / 2);

  const move = (steps: number) => {
    const next = [...cards];

    if (steps > 0) {
      for (let i = 0; i < steps; i += 1) {
        const first = next.shift();
        if (first) next.push(first);
      }
    } else {
      for (let i = 0; i < Math.abs(steps); i += 1) {
        const last = next.pop();
        if (last) next.unshift(last);
      }
    }

    setCards(next);
  };

  return (
    <section className="relative h-[520px] overflow-hidden">
      {cards.map((card, index) => {
        const position = index - centerIndex;
        const isCenter = position === 0;
        const offsetX = 180;
        const offsetY = isCenter ? -30 : position % 2 === 0 ? 20 : -20;
        const rotation = isCenter ? 0 : position % 2 === 0 ? 3 : -3;

        return (
          <button
            key={card.title}
            type="button"
            onClick={() => move(position)}
            className="absolute left-1/2 top-1/2 h-[320px] w-[240px] rounded-[2rem] bg-white/70 p-6 text-left shadow-2xl backdrop-blur-md transition-all duration-500"
            style={{
              transform: `translate(-50%, -50%) translateX(${position * offsetX}px) translateY(${offsetY}px) rotate(${rotation}deg) scale(${isCenter ? 1.08 : 0.9})`,
              opacity: isCenter ? 1 : 0.4,
              zIndex: isCenter ? 10 : 10 - Math.abs(position)
            }}
          >
            <h3 className="text-lg font-semibold">{card.title}</h3>
            <p className="mt-3 text-sm text-neutral-600">Conteudo do card.</p>
          </button>
        );
      })}
    </section>
  );
};

export default StaggeredStackCarousel;
```

## Referencia original

- Projeto de origem: `stephanie-bolsoni-website`
- Arquivo de notas: `C:/Users/pedro/Desktop/WEB STAR/stephanie-bolsoni-website/STAGGERED_STACK_CAROUSEL.md`
- Componente citado nas notas: `src/components/ui/stagger-testimonials.tsx`
