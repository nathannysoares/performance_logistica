# 📦 Dashboard de Performance Logística

Este dashboard foi criado para analisar **volume, pontualidade e equipes de logística**, trazendo insights sobre entregas, atrasos e performance por canal, região e vendedor.

---
📷 **Exemplo do Dashboard:**  

![Painel Interativo de logistica](Image/logistica.png)  

---
## 📊 Visão Geral

- **Total de Entregas:** 54 mil  
- **Entregas no Prazo:** 47 mil  
- **Taxa de Pontualidade:** ~87%  
- **Entregas Atrasadas:** 7 mil (12,98%)  

---

## 🔍 Insights de Negócios

### 1. Volume e Pontualidade
- 70,71% das entregas foram **antecipadas**.  
- Apenas 16,31% ocorreram **no prazo exato**.  
- 12,98% foram **atrasadas**.  
➡️ **Excesso de antecipação** pode gerar custos logísticos desnecessários. É importante buscar equilíbrio.

---

### 2. Performance por Região
- **Norte (27,44%)** e **Sudeste (24,87%)** concentram a maior parte das entregas.  
- **Sul (13,35%)** e **Nordeste (16,72%)** têm relevância intermediária.  
- **Internet (10,87%)** e **Televendas (6,25%)** são canais ainda pouco explorados.  

➡️ **Oportunidade de crescimento** via canais digitais e reforço de estrutura no Norte e Sudeste.

---

### 3. Sazonalidade
- Picos de entregas em **março e julho** (~6 mil).  
- Queda acentuada entre **setembro e dezembro**.  

➡️ Ajustar **recursos sazonais** e criar **ações comerciais** em períodos de baixa.

---

### 4. Performance dos Vendedores
- Vendedores **3686 e 3894** lideram em volume.  
- Todos mantêm **rating elevado**.  

➡️ Usar **top vendedores como benchmark** para treinar e melhorar a performance dos demais.

---

### 5. Atrasos por Cidade
- Poucas cidades concentram grande parte dos atrasos (ex: 589, 392, 321).  
➡️ **Foco em soluções locais** pode reduzir significativamente os atrasos totais.

---

## 🎯 Recomendações Estratégicas
1. Equilibrar entregas antecipadas e no prazo para **reduzir custos logísticos**.  
2. Atacar **cidades críticas** para reduzir atrasos.  
3. Expandir presença em **canais digitais** (internet e televendas).  
4. Ajustar operação conforme **sazonalidade** (reforço em picos e eficiência em baixas).  
5. Transformar boas práticas de **vendedores top** em modelo de treinamento.  

---

## ⚙️ Medidas Criadas em DAX

Para construir este dashboard, foram criadas medidas personalizadas no **Power BI (DAX)**, a fim de gerar indicadores de performance e enriquecer a análise.

⭐ Medida de Rating
```
Rating =
VAR __MAX_NUMBER_OF_STARS = 5
VAR __MIN_RATED_VALUE = 1500
VAR __MAX_RATED_VALUE = 2500
VAR __BASE_VALUE = [TotalEntregas]
VAR __NORMALIZED_BASE_VALUE =
    MIN(
        MAX(
            DIVIDE(
                __BASE_VALUE - __MIN_RATED_VALUE,
                __MAX_RATED_VALUE - __MIN_RATED_VALUE
            ),
            0
        ),
        1
    )
VAR __STAR_RATING = ROUND(__NORMALIZED_BASE_VALUE * __MAX_NUMBER_OF_STARS, 0)
RETURN
    IF(
        NOT ISBLANK(__BASE_VALUE),
        REPT(UNICHAR(9733), __STAR_RATING)
            & REPT(UNICHAR(9734), __MAX_NUMBER_OF_STARS - __STAR_RATING)
    )
```
➡️ Essa medida cria um sistema de estrelas (★★★★★) com base no volume de entregas de cada vendedor.
Isso permite comparar desempenho visualmente, facilitando a interpretação rápida pelos gestores.

---


📦 Total de Entregas no Prazo
```
TotalEntregasPrazo =
CALCULATE(
    [TotalEntregas],
    FILTER(
        Logistica,
        Logistica[Status_Entrega] = "Antecipado"
            || Logistica[Status_Entrega] = "No Prazo"
    )
)
```
➡️ Essa medida calcula o total de entregas realizadas sem atraso, agrupando tanto as antecipadas quanto as no prazo.
Assim, conseguimos medir a eficiência operacional.


---

⏱️ Total de Entregas em Atraso

```
TotalEntregasAtraso =
CALCULATE(
    [TotalEntregas],
    FILTER(
        Logistica,
        Logistica[Status_Entrega] = "Atrasado"
    )
)
```
---
🚀 Valor Agregado

Essas medidas mostram que o dashboard não foi apenas uma representação gráfica, mas sim um trabalho completo de modelagem, cálculos personalizados e inteligência analítica.

Com isso, é possível:

Comparar performance de equipes de forma visual e intuitiva.

Mensurar atrasos de forma clara, apoiando decisões estratégicas.

Criar indicadores de satisfação indireta (rating por entregas), que podem ser expandidos para KPIs de cliente.

📌 Este dashboard permite decisões mais assertivas para otimizar logística, reduzir custos e aumentar a satisfação do cliente.

## 📧 Contato
**LinkedIn** - [![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat-square&logo=linkedin)](https://linkedin.com/in/nathannysoares)


## 🎓 Créditos
Este projeto foi desenvolvido com base nos conhecimentos adquiridos no curso de Power BI **Data Science Academy (DSA)**

---
⭐ **Se este projeto foi útil para você, deixe uma star no repositório!**

