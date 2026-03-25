# 3D Marquee Testimonials

## Resumo

Secao de depoimentos com colunas em movimento infinito e perspectiva 3D. O
efeito combina `marquee` vertical, uma parede inclinada de cards e mascaras em
gradiente para que os elementos aparecam e sumam com suavidade.

## Quando usar

- Depoimentos em landing pages premium
- Secoes de social proof com forte impacto visual
- Home pages que pedem movimento continuo sem depender de clique
- Interfaces que se beneficiam de profundidade e sensacao de espaco

## Stack sugerida

- React
- Tailwind CSS
- Framer Motion opcional
- Um utilitario `Marquee` ou keyframes customizados

## Mecanica do efeito

1. O container principal define `perspective`.
2. O plano interno usa `transform-style: preserve-3d`.
3. As colunas deslizam infinitamente no eixo vertical.
4. A coluna central anda no sentido oposto para gerar contraste.
5. Gradientes nas bordas evitam cortes secos.
6. `transform-gpu` e `will-change` ajudam na performance.

## Checklist de implementacao

- Definir perspectiva no wrapper
- Incluir ao menos tres colunas para leitura mais rica
- Duplicar os itens do marquee para criar loop continuo
- Inverter a coluna do meio
- Adicionar mascaras de gradiente em cima, baixo e laterais
- Pausar o movimento no hover, se a UX pedir mais controle

## Prompt de reutilizacao

> Crie uma secao `3D Marquee Testimonials` para React com Tailwind CSS.
> O bloco deve ter perspectiva 3D, uma parede inclinada de cards e tres
> colunas verticais de depoimentos em loop infinito. A coluna central deve se
> mover na direcao oposta. Use cards arredondados com visual clean,
> gradientes nas bordas para fade e otimizacoes de GPU para manter a animacao
> suave.

## Snippet base

```tsx
const reviews = [
  { name: 'Ana', text: 'Atendimento impecavel.' },
  { name: 'Clara', text: 'Experiencia acolhedora e moderna.' },
  { name: 'Marina', text: 'Tudo muito bem pensado.' }
];

const MarqueeColumn = ({
  items,
  reverse = false
}: {
  items: typeof reviews;
  reverse?: boolean;
}) => (
  <div className="relative h-[520px] overflow-hidden">
    <div
      className={`flex flex-col gap-6 will-change-transform ${
        reverse ? 'animate-marquee-up' : 'animate-marquee-down'
      }`}
    >
      {[...items, ...items].map((item, index) => (
        <article
          key={`${item.name}-${index}`}
          className="w-[280px] rounded-[2rem] bg-white/95 p-6 shadow-xl"
        >
          <p className="text-sm text-neutral-700">{item.text}</p>
          <span className="mt-4 block text-sm font-semibold">{item.name}</span>
        </article>
      ))}
    </div>
  </div>
);

const ThreeDMarqueeTestimonials = () => {
  return (
    <section className="relative h-[620px] overflow-hidden [perspective:2000px]">
      <div
        className="flex justify-center gap-8 [transform-style:preserve-3d]"
        style={{
          transform: 'rotateX(15deg) rotateY(-8deg) rotateZ(4deg) translateZ(-120px)'
        }}
      >
        <MarqueeColumn items={reviews} />
        <MarqueeColumn items={reviews} reverse />
        <MarqueeColumn items={reviews} />
      </div>

      <div className="pointer-events-none absolute inset-x-0 top-0 h-24 bg-gradient-to-b from-white to-transparent" />
      <div className="pointer-events-none absolute inset-x-0 bottom-0 h-24 bg-gradient-to-t from-white to-transparent" />
    </section>
  );
};

export default ThreeDMarqueeTestimonials;
```

## Nota de estilo

Para esse efeito funcionar bem, vale adicionar keyframes para o `marquee`
vertical no `tailwind.config.js` ou em um arquivo global de estilos. A ideia
base e mover o track de `translateY(0)` ate `translateY(-50%)`, ja que o
conteudo esta duplicado.

## Referencia original

- Projeto de origem: `stephanie-bolsoni-website`
- Arquivo de notas: `C:/Users/pedro/Desktop/WEB STAR/stephanie-bolsoni-website/3D_INFINITE_MARQUEE_TESTIMONIALS.md`
- Componentes citados nas notas: `src/components/ReviewsSection.tsx` e `src/components/ui/3d-testimonials.tsx`
