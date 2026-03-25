# Cinematic Navbar

## Resumo

Navbar flutuante em formato `pill` que expande para um menu editorial largo,
com area de midia e um modo de foco para video. O efeito combina
glassmorphism, transicao de layout e controles customizados para criar uma
sensacao mais cinematica do que um menu tradicional.

## Quando usar

- Portfolio premium
- Site autoral com hero em video
- Landing page de marca pessoal
- Navegacao que precisa causar impacto sem ocupar a tela o tempo todo

## Stack sugerida

- React
- Framer Motion
- Tailwind CSS
- Lucide React para icones

## Mecanica do efeito

1. `scrolled` reduz a navbar quando a pagina desce, mantendo o acesso sem
   competir com o conteudo.
2. `isOpen` expande a `pill` para um container maior com duas colunas.
3. `isVideoFocused` troca o layout interno sem fechar o menu.
4. `layout` do Framer Motion faz o morph entre os estados com movimento fluido.
5. O video usa uma sequencia de `fade out -> layout shift -> fade in` para
   evitar glitches visuais.

## Checklist de implementacao

- Usar `motion.nav` com `layout`
- Separar barra superior e conteudo expandido
- Criar um estado proprio para foco de midia
- Aplicar `backdrop-blur` e bordas suaves no shell principal
- Animar links com `staggered reveal`
- Recriar os controles do video para manter o visual consistente

## Prompt de reutilizacao

> Crie uma `Cinematic Navbar` para React com Framer Motion e Tailwind CSS.
> O estado inicial deve ser uma pill flutuante com glassmorphism. Ao abrir,
> ela precisa expandir para um container largo com duas colunas: links e CTA
> na esquerda, midia na direita. Ao clicar no video, a coluna de links deve
> desaparecer e a area de midia deve ganhar destaque sem fechar o menu.
> Use layout transitions suaves, reveal em cascata para os links, sombras
> discretas e controles de video customizados com visual liquid glass.

## Snippet base

```tsx
import { useState } from 'react';
import { AnimatePresence, motion } from 'framer-motion';

const CinematicNavbar = () => {
  const [isOpen, setIsOpen] = useState(false);
  const [isFocused, setIsFocused] = useState(false);

  return (
    <motion.nav
      layout
      className="overflow-hidden rounded-[2rem] border border-white/20 bg-white/90 shadow-2xl backdrop-blur-xl"
      animate={isOpen ? 'open' : 'closed'}
      variants={{
        closed: { width: '320px', height: '60px', borderRadius: '2rem' },
        open: { width: 'min(1200px, 95vw)', height: 'auto', borderRadius: '2.5rem' }
      }}
    >
      <div className="flex h-[60px] items-center justify-between px-6">
        <div className="text-lg font-semibold">LOGO</div>
        <button type="button" onClick={() => setIsOpen(current => !current)}>
          MENU
        </button>
      </div>

      <AnimatePresence>
        {isOpen && (
          <motion.div
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
            className="flex gap-8 p-8"
          >
            {!isFocused && (
              <div className="flex flex-1 flex-col gap-4">
                <span className="text-sm uppercase tracking-[0.3em] text-neutral-500">
                  Navigation
                </span>
                <a href="#home">Home</a>
                <a href="#services">Services</a>
                <a href="#contact">Contact</a>
              </div>
            )}

            <motion.div
              layout
              onClick={() => setIsFocused(current => !current)}
              className={`cursor-pointer rounded-[2rem] bg-black ${
                isFocused ? 'aspect-video flex-1' : 'aspect-square w-1/2'
              }`}
            />
          </motion.div>
        )}
      </AnimatePresence>
    </motion.nav>
  );
};

export default CinematicNavbar;
```

## Referencia original

- Projeto de origem: `stephanie-bolsoni-website`
- Arquivo de notas: `C:/Users/pedro/Desktop/WEB STAR/stephanie-bolsoni-website/CINEMATIC_NAVBAR_EFFECT.md`
- Componente citado nas notas: `src/components/Header.tsx`
