# Guia de Implementação de Cartões Interativos

## Etapa 1: Adicionando a Seção de Cartões

Vamos começar adicionando uma seção para colocar os cartões:

- Adicione uma seção no seu código.
- Dentro dessa seção, adicione 3 contêineres internos para os cartões.
- Configure controles flexíveis para um layout de linha.
- Rotule os 3 recipientes internos como 'Recipiente - Cartão'.

## Etapa 2: Criando os Cartões

Dentro dos contêineres chamados 'Container – Card':

- Adicione uma classe 'card'.
- Aplique um preenchimento de 1-3px para agir como a largura da borda.
- Defina o índice Z como 0.
- Defina overflow como oculto.
- Estilize o raio da borda e a cor de fundo do seu cartão.

## Etapa 3: Criando o Contêiner Interno para Conteúdo

- Adicione um novo contêiner interno dentro do contêiner do cartão.
- Rotule o recipiente interno como 'Recipiente Interno'.
- Dê ao contêiner interno um nome de classe 'inner'.
- Adicione seu conteúdo dentro do contêiner 'Inner' e estilize-o com configurações flexíveis, incluindo preenchimentos e lacunas internas.
- Defina o raio da borda (deve ser igual ao raio da borda definido dentro do contêiner do Cartão).
- Defina a cor de fundo para opacidade 0,8.
- Defina a cor de foco do fundo para opacidade 0,6.

## Etapa 4: Criando os Elementos de Efeito

Adicione mais 2 contêineres dentro do contêiner do seu cartão:

- Rotule o primeiro contêiner como 'Blob Container'.
- Rotule o segundo contêiner como 'Fake Blob Container'.
- Dê ao contêiner Blob uma classe 'blob'.
- Dê ao contêiner Fake Blob uma classe 'fakeblob'.
- Estilize os contêineres Blob e Fake Blob conforme especificado.

## Etapa 5: Adicionando o CSS

O código CSS armazena o tamanho do blob em uma variável para reutilização.

Adicione o seguinte snippet de código CSS:
```markdown
/* css goes in .card */

selector {
    --blob-size:250px;
}

selector .inner{
    backdrop-filter: blur(80px);
    height: 100%;
}

selector .blob{
    width: var(--blob-size);
    height: 80%;
    left: calc(50% - calc(var(--blob-size)/2));
    filter: blur(40px);
    z-index: -1;
    opacity: 0;    
    transition: opacity 300ms 300ms linear;

}

selector .fakeblob {
  visibility: hidden;
  z-index: -1;
  height: 100%;
}
```

## Etapa 6: Adicionando o JavaScript

No código JavaScript:

- Selecione todos os elementos com a classe 'card'.
- Adicione um ouvinte de evento para ouvir o movimento do mouse sobre qualquer cartão.
- Adicione o método animate para movimentar o elemento blob com o cursor.

Adicione o seguinte código JavaScript:

```javascript
<script type="text/javascript">
    
      const cards = document.querySelectorAll(".card");


window.addEventListener("mousemove", (ev) => {
  
  cards.forEach((e) => {
    const blob = e.querySelector(".blob");
    const fblob = e.querySelector(".fakeblob");
    const rec = fblob.getBoundingClientRect();

  
    blob.animate(
      [
        {
          transform: `translate(${
            (ev.clientX - rec.left) - (rec.width / 2)
          }px,${(ev.clientY - rec.top) - (rec.height / 2)}px)`
        }
      ],
      {
        duration: 300,
        fill: "forwards"
      }
    );
  
    blob.style.opacity = "1";
      
  });
  
});    
</script>
```
