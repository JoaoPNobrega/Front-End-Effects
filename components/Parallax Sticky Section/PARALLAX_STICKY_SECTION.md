# Efeito: Sticky Content Parallax (Coluna Esquerda Fixa)

Este efeito mantém um bloco de texto fixo na tela (**sticky**) enquanto o conteúdo lateral continua a rolar, criando um movimento de paralaxe entre as duas colunas.

## 1. Prompt para Reutilização

> **Prompt:** "Crie um componente de 'Sticky Info Section' para React usando Tailwind CSS.
> 1. **Layout:** Use um grid de 2 colunas para desktop (grid-cols-1 lg:grid-cols-2) com um gap generoso (ex: gap-20).
> 2. **Lógica Sticky:** A coluna da ESQUERDA deve ser 'sticky' (utilizando `lg:sticky top-32`), permanecendo fixa no viewport enquanto a coluna da DIREITA é percorrida pelo usuário.
> 3. **Conteúdo da Esquerda:** Coloque um cabeçalho e os parágrafos informativos sobre a glândula prostática. Use uma tipografia sóbria (font-serif para títulos) e cores que transmitam profissionalismo médico (como tons de azul e ardósia).
> 4. **Conteúdo da Direita:** Crie uma série de cards informativos para garantir que a seção tenha altura suficiente para o efeito de scroll ser ativado.
> 5. **Design:** Use bordas arredondadas suaves (rounded-3xl), sombras leves e um fundo limpo (slate-50)."

---

## 2. Código Base (React + Tailwind)

```tsx
import React from 'react';
import { ArrowRight, Activity, ShieldCheck, Microscope } from 'lucide-react';

const UrologiaSection = () => {
  return (
    <section className="bg-slate-50 py-24 px-6 md:px-12">
      <div className="max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-2 gap-16 lg:gap-24 items-start">
        
        {/* ——— COLUNA DA ESQUERDA (STICKY) ——— */}
        <div className="lg:sticky lg:top-32 space-y-8">
          <div className="flex items-center gap-4">
            <div className="h-px w-12 bg-blue-600" />
            <span className="text-xs font-bold uppercase tracking-[0.2em] text-blue-600">
              Especialidade Médica
            </span>
          </div>
          
          <h2 className="font-serif text-[clamp(2.5rem,5vw,3.5rem)] leading-[1.1] text-slate-800">
            Saúde da Próstata e <br />
            <span className="italic text-blue-700">Decisões Conscientes</span>
          </h2>
          
          <div className="space-y-6 text-lg text-slate-600 font-light leading-relaxed max-w-lg">
            <p>
              A próstata é uma glândula do sistema reprodutor masculino localizada abaixo da bexiga. Com o envelhecimento, ela pode ser acometida por condições que vão desde o crescimento benigno até neoplasias malignas — cada uma com perfil clínico, prognóstico e tratamento distintos.
            </p>
            <p className="border-l-4 border-blue-600/20 pl-6 italic">
              Entender as diferentes doenças prostáticas é o primeiro passo para decisões conscientes. A avaliação urológica especializada permite identificar a condição correta e definir o melhor caminho terapêutico para cada paciente.
            </p>
          </div>
        </div>

        {/* ——— COLUNA DA DIREITA (SCROLLING CONTENT) ——— */}
        <div className="space-y-10 lg:pt-12">
          {/* Blocos informativos para criar altura de scroll */}
          {[
            { 
              title: "Hiperplasia Benigna (HPB)", 
              desc: "O aumento benigno da próstata que atinge a maioria dos homens com o passar dos anos.",
              icon: Activity 
            },
            { 
              title: "Prevenção e Rastreio", 
              desc: "Consultas regulares e exames preventivos são fundamentais para diagnósticos precoces.",
              icon: ShieldCheck 
            },
            { 
              title: "Diagnóstico Diferencial", 
              desc: "Análise técnica para distinguir entre inflamações, infecções e alterações celulares.",
              icon: Microscope 
            },
            { 
              title: "Tecnologia e Tratamento", 
              desc: "Abordagens modernas que priorizam a qualidade de vida e a recuperação rápida do paciente.",
              icon: ArrowRight 
            }
          ].map((card, i) => (
            <div 
              key={i} 
              className="group bg-white p-10 rounded-[2.5rem] border border-slate-200 shadow-sm hover:shadow-xl hover:border-blue-100 transition-all duration-500"
            >
              <div className="w-12 h-12 rounded-2xl bg-blue-50 flex items-center justify-center text-blue-600 mb-6 group-hover:bg-blue-600 group-hover:text-white transition-colors duration-300">
                <card.icon size={24} />
              </div>
              <h3 className="font-serif text-2xl font-bold text-slate-800 mb-4">{card.title}</h3>
              <p className="text-slate-600 leading-relaxed font-light">{card.desc}</p>
            </div>
          ))}
        </div>

      </div>
    </section>
  );
};

export default UrologiaSection;
```
