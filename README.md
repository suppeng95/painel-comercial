# Painel comercial — pasta de publicação

Este repositório contém **apenas o que vai ao ar**. O gerador (`atualizar_painel.py`),
os logs, o histórico de notícias e qualquer chave ficam de fora, na pasta `../files`.

| Arquivo | Papel |
|---|---|
| `index.html` | o painel, cópia do `painel_comercial.html` gerado |
| `vercel.json` | cabeçalhos de segurança e cache |
| `.gitignore` | barra chaves, logs e a planilha |

## Como publica

O Vercel acompanha este repositório. Cada `git push` publica uma versão nova — não é
preciso instalar Node nem a CLI do Vercel nesta máquina.

## Antes do primeiro push, confirme duas coisas

**1. O repositório precisa ser privado.** Mesmo com o Firestore ligado, um repositório
público expõe a estrutura da aplicação sem necessidade.

**2. Confira se o `index.html` está vazio de dados.** Com o Firestore ligado
(`USAR_FIRESTORE = True` no gerador), o painel vai sem a carteira dentro e busca os
dados do banco depois do login. Para verificar, procure a estrutura de dados no arquivo:

```bash
grep -c "\"regs\":\[\[" index.html
```

O resultado **precisa ser 0**. Se vier 1, os dados estão embutidos: qualquer pessoa com
o endereço vê a carteira inteira no código-fonte da página, **mesmo com tela de login na
frente**. Nesse caso, não publique sem antes proteger o acesso ao próprio arquivo.

## O que fica exposto se essa checagem falhar

Milhares de propostas com nome do cliente, valor, **margem em R$ e em %**, responsável,
descrição e datas. A margem por cliente é o item mais sensível: um cliente veria quanto
se ganha nele, e um concorrente veria a formação de preço.
