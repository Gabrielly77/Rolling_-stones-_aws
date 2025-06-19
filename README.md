# Rolling_-stones-_aws-

🚀 Rolling Deployment / Rolling Update na AWS (e geral também)
👉 É um tipo de estratégia de implantação onde você atualiza sua aplicação aos poucos, trocando as instâncias antigas pelas novas, de forma gradual.
Assim você evita que tudo caia de uma vez, sabe? É tipo trocar os pneus do carro… enquanto ele tá andando! (mas de um jeito seguro, relaxa kkkkk).

🔥 Funciona assim:
Sobe uma nova versão ➡️ derruba uma instância velha ➡️ sobe outra nova ➡️ derruba outra velha… até tudo ser atualizado.

💡 AWS usa isso no CodeDeploy, por exemplo. Você pode escolher "Rolling update" pra atualizar as instâncias do seu app EC2, ECS, etc.

🎯 E o que seria Rolling Batch?
Mesma ideia, só que em lotes. Tipo assim:

Em vez de trocar uma por uma, você fala:
“Quero atualizar de 2 em 2” (ou qualquer quantidade que quiser).

Aí ele faz:
➡️ Derruba 2 velhas ➡️ Sobe 2 novas ➡️ Testa ➡️ Repete até acabar.

📍 Isso te dá um equilíbrio entre:
✅ Não derrubar tudo de uma vez
✅ Ser mais rápido do que fazer uma por uma.

📦 Onde isso aparece na certificação AWS Developer?
🧠 No AWS CodeDeploy, quando ele pergunta sobre estratégias de deployment:

AllAtOnce: tudo de uma vez (rápido, mas arriscado)

Rolling: troca gradual

Rolling with Batch: troca em grupos (batches)

Blue/Green: cria ambiente novo, testa e depois troca o tráfego

🧠 MACETE PRA PROVA:
Se você vê "alta disponibilidade durante o deploy" ➝ pensa em Rolling.
Se vê "trocar todo mundo ao mesmo tempo" ➝ pensa em AllAtOnce.
Se vê "testar tudo antes de colocar no ar" ➝ Blue/Green.

💡 Depende, mas na maioria dos casos… SIM! O Rolling tende a ser mais barato. Bora entender esse rolê rapidinho no jeitinho AWS raiz:

⚖️ Comparando Custos:
Estrategia	Custo	Por quê?
AllAtOnce	🔥Barato, mas arriscado	Sobe tudo de uma vez. Não precisa de instâncias extras. Mas... se der ruim, todo mundo cai.
Rolling	💰Mais barato que Blue/Green	Atualiza de pouquinho em pouquinho. Não precisa de muitas instâncias extras, só o necessário pra segurar o tráfego enquanto atualiza.
Rolling com Batch	💰 Parecido com Rolling	Mesmo esquema, só que em lotes. Um pouco mais rápido, mas ainda econômico.
Blue/Green	🤑 Caro	Cria um ambiente NOVO, inteiro separado, pra depois redirecionar o tráfego. Paga o dobro temporariamente.

🚩 Por que o Rolling sai mais barato?
Porque você usa praticamente o mesmo ambiente, sem precisar duplicar tudo como no Blue/Green. No máximo, sobe uma ou duas instâncias temporárias, dependendo da configuração dos batches, pra garantir que o app não fique indisponível.

📜 Na prática:
🚀 Quer barato e com alguma segurança? Vai de Rolling ou Rolling com Batch.

🧠 Quer zero risco de downtime (queda)? Vai de Blue/Green, mas prepara o bolso (temporariamente $$$).

⚡ Quer atualizar na loucura, rápido e barato, mas com risco de cair tudo? Vai de AllAtOnce (só que AWS não recomenda pra produção, tá? rs).

⚠️ Na prova AWS Developer (DVA-C02) aparece sim:
Eles perguntam sobre:

Custo

Disponibilidade

Risco de falha

Se na questão falar:

"Quer minimizar custo e manter alguma disponibilidade durante o deploy" ➝ Rolling.

"Quer minimizar downtime a todo custo, mesmo pagando mais" ➝ Blue/Green.
