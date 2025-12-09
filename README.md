# Mac Coelho — Site Estático com Envio Automático de Pedidos

Esta versão inclui uma função serverless (Netlify Functions) que envia pedidos automaticamente por e-mail usando SMTP (nodemailer).

Arquivos principais

- `index.html` — página principal
- `styles.css` — estilos
- `scrip.js` — lógica do frontend (carrinho, modal, checkout)
- `netlify/functions/sendOrder.js` — função serverless que envia e-mail com o pedido
- `package.json` — dependências para a função (nodemailer)

Como configurar o envio automático (Netlify)

1. No painel do Netlify, adicione as seguintes variáveis de ambiente (Settings > Build & deploy > Environment):

    - `SMTP_HOST` — host SMTP (ex.: smtp.gmail.com)
    - `SMTP_PORT` — porta (ex.: 587)
    - `SMTP_SECURE` — `false` ou `true` (geralmente `false` com 587)
    - `SMTP_USER` — usuário SMTP (ex.: seu e-mail)
    - `SMTP_PASS` — senha ou app password
    - `SMTP_FROM` — (opcional) endereço From para o e-mail
    - `STORE_EMAIL` — e-mail que receberá os pedidos (ex.: maccoelho.delivery@gmail.com)

2. Faça deploy no Netlify (arraste o diretório ou conecte ao GitHub). O Netlify detectará a pasta `netlify/functions` e instalará dependências do `package.json`.

3. Após o deploy: o frontend chama `/.netlify/functions/sendOrder` para enviar pedidos automaticamente. Se houver erro, o frontend mostrará a mensagem retornada pela função.

Notas de segurança e LGPD

- Não inclua credenciais no repositório. Use variáveis de ambiente.
- Adicione um campo de consentimento no checkout se você armazenar dados pessoais.

Testando localmente

- Você pode testar o frontend abrindo `index.html` no navegador. Para testar a função serverless localmente, use a CLI do Netlify (`netlify dev`) e configure as variáveis de ambiente localmente.

Próximos passos (opcionais que posso implementar)

- Painel administrativo (listar pedidos recebidos) com Firestore/DB
- Integração com gateway de pagamentos (PIX/Stripe/MercadoPago)
- Autenticação para painel administrativo e filtragem de pedidos
